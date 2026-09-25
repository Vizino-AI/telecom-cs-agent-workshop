# Mock Data — Schema & Seed SQL

[← Back to course overview](README.md)

Ready-to-run SQL for Blazz's Supabase database: schema for Scenario 1 (billing/plans/travel) and Scenario 2 (technician dispatch), plus seed data. Scenario 3's contract terms live as a document in Supabase Storage, not a table — see [Unit 3](units/unit-3.md).

This is prepared as a reference/fallback. The intent in [Unit 2](units/unit-2.md)/[Unit 3](units/unit-3.md) is still to have Claude write this SQL live with the student from the data design below — this file is what that exercise should land on, not a replacement for doing it live.

## Schema

```sql
CREATE TABLE plans (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  monthly_price NUMERIC NOT NULL,
  data_allowance_gb NUMERIC,           -- NULL = unlimited
  roaming_included BOOLEAN NOT NULL DEFAULT FALSE,
  roaming_rate_per_gb NUMERIC          -- NULL if roaming_included
);

CREATE TABLE customers (
  id SERIAL PRIMARY KEY,
  full_name TEXT NOT NULL,
  phone_number TEXT NOT NULL UNIQUE,
  account_pin TEXT NOT NULL,           -- 4-digit second factor for identity verification
  email TEXT NOT NULL,
  plan_id INT NOT NULL REFERENCES plans(id),
  service_region TEXT NOT NULL,        -- matches technicians.region
  contract_start_date DATE NOT NULL,
  contract_term_months INT NOT NULL DEFAULT 24,
  plan_last_changed_at TIMESTAMP,      -- NULL = never changed since signup; see Scenario 1's Plan Change SOP
  created_at TIMESTAMP NOT NULL DEFAULT now()
);

CREATE TABLE bills (
  id SERIAL PRIMARY KEY,
  customer_id INT NOT NULL REFERENCES customers(id),
  billing_month DATE NOT NULL,
  base_amount NUMERIC NOT NULL,
  roaming_charges NUMERIC NOT NULL DEFAULT 0,
  other_charges NUMERIC NOT NULL DEFAULT 0,
  total_amount NUMERIC NOT NULL,
  due_date DATE NOT NULL,
  status TEXT NOT NULL DEFAULT 'unpaid'
);

CREATE TABLE travel_histories (
  id SERIAL PRIMARY KEY,
  customer_id INT NOT NULL REFERENCES customers(id),
  destination_country TEXT NOT NULL,
  start_date DATE NOT NULL,
  end_date DATE NOT NULL,
  roaming_data_used_gb NUMERIC NOT NULL
);

CREATE TABLE technicians (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  region TEXT NOT NULL                 -- matches customers.service_region
);

CREATE TABLE technician_availability (
  id SERIAL PRIMARY KEY,
  technician_id INT NOT NULL REFERENCES technicians(id),
  date DATE NOT NULL,
  time_slot TEXT NOT NULL,             -- e.g. '09:00-11:00'
  status TEXT NOT NULL DEFAULT 'available'
);

CREATE TABLE dispatch_requests (
  id SERIAL PRIMARY KEY,
  customer_id INT NOT NULL REFERENCES customers(id),
  technician_availability_id INT REFERENCES technician_availability(id),
  issue_description TEXT,
  status TEXT NOT NULL DEFAULT 'pending_approval',  -- pending_approval / approved / rescheduling
  slack_message_ts TEXT,               -- so the bot can update the same Slack message after a button click
  created_at TIMESTAMP NOT NULL DEFAULT now()
);
-- dispatch_requests starts empty — rows get created live during the Scenario 2 demo, not seeded
```

## Seed Data

### `plans`

```sql
INSERT INTO plans (id, name, monthly_price, data_allowance_gb, roaming_included, roaming_rate_per_gb) VALUES
(1, 'Basic 5GB', 35, 5, FALSE, 50),
(2, 'Standard 15GB', 55, 15, FALSE, 50),
(3, 'Unlimited Talk & Text 30GB', 75, 30, FALSE, 50),
(4, 'Family Share 50GB', 120, 50, FALSE, 50),
(5, 'Global Roamer Unlimited', 500, NULL, TRUE, NULL);
```

### `customers`

10 customers across 5 Canadian cities — each region also has technician coverage (see below). Robert Nguyen's `plan_last_changed_at` is deliberately recent (within a day), as the demo case for the Plan Change SOP's eligibility check.

```sql
INSERT INTO customers (id, full_name, phone_number, account_pin, email, plan_id, service_region, contract_start_date, contract_term_months, plan_last_changed_at) VALUES
(1, 'Sarah Chen', '555-0101', '4821', 'sarah.chen@example.com', 2, 'Toronto, ON', '2025-01-15', 24, NULL),
(2, 'Marcus Webb', '555-0102', '7734', 'marcus.webb@example.com', 1, 'Vancouver, BC', '2024-06-01', 24, NULL),
(3, 'Priya Nair', '555-0103', '2298', 'priya.nair@example.com', 5, 'Montreal, QC', '2023-11-20', 24, NULL),
(4, 'David Kim', '555-0104', '5510', 'david.kim@example.com', 3, 'Toronto, ON', '2025-03-10', 24, NULL),
(5, 'Fatima Al-Rashid', '555-0105', '9081', 'fatima.alrashid@example.com', 4, 'Calgary, AB', '2024-09-05', 24, NULL),
(6, 'James O''Connor', '555-0106', '3345', 'james.oconnor@example.com', 1, 'Ottawa, ON', '2025-05-22', 24, NULL),
(7, 'Li Wei', '555-0107', '6623', 'li.wei@example.com', 2, 'Vancouver, BC', '2024-02-14', 24, NULL),
(8, 'Emma Larsson', '555-0108', '1187', 'emma.larsson@example.com', 3, 'Montreal, QC', '2023-08-01', 24, NULL),
(9, 'Robert Nguyen', '555-0109', '8842', 'robert.nguyen@example.com', 1, 'Winnipeg, MB', '2025-07-18', 24, '2026-09-24 14:30:00'),
(10, 'Aisha Okafor', '555-0110', '4456', 'aisha.okafor@example.com', 4, 'Halifax, NS', '2024-12-01', 24, NULL);
```

### `bills` (all: `billing_month = 2026-09-01`, `due_date = 2026-09-25`, `status = 'unpaid'`)

| customer | total | design intent |
| --- | --- | --- |
| Sarah Chen | $2,005 | **the core "why is my bill $2,000" demo** — Japan + Korea trip |
| Marcus Webb | $120 | modest charge, but 3 trips in travel history is a *pattern* even though this bill isn't shocking |
| Priya Nair | $500 | already on Global Roamer — control case, no upsell needed |
| David Kim | $75 | normal, no travel — baseline negative case |
| Fatima Al-Rashid | $165 | one modest trip — tests against over-upselling off a single small trip |
| James O'Connor | $95 | spike from **data overage, not roaming** — tests correct diagnosis |
| Li Wei | $365 | two trips, clear pattern |
| Emma Larsson | $965 | large multi-country trip — alternate "big bill" demo |
| Robert Nguyen | $35 | normal |
| Aisha Okafor | $120 | normal |

```sql
INSERT INTO bills (customer_id, billing_month, base_amount, roaming_charges, other_charges, total_amount, due_date, status) VALUES
(1, '2026-09-01', 55, 1950, 0, 2005, '2026-09-25', 'unpaid'),
(2, '2026-09-01', 35, 85, 0, 120, '2026-09-25', 'unpaid'),
(3, '2026-09-01', 500, 0, 0, 500, '2026-09-25', 'unpaid'),
(4, '2026-09-01', 75, 0, 0, 75, '2026-09-25', 'unpaid'),
(5, '2026-09-01', 120, 45, 0, 165, '2026-09-25', 'unpaid'),
(6, '2026-09-01', 35, 0, 60, 95, '2026-09-25', 'unpaid'),
(7, '2026-09-01', 55, 310, 0, 365, '2026-09-25', 'unpaid'),
(8, '2026-09-01', 75, 890, 0, 965, '2026-09-25', 'unpaid'),
(9, '2026-09-01', 35, 0, 0, 35, '2026-09-25', 'unpaid'),
(10, '2026-09-01', 120, 0, 0, 120, '2026-09-25', 'unpaid');
```

### `travel_histories`

Customers 3, 4, 6, 9, 10 have no travel rows — consistent with their bills.

```sql
INSERT INTO travel_histories (customer_id, destination_country, start_date, end_date, roaming_data_used_gb) VALUES
(1, 'Japan', '2026-08-03', '2026-08-10', 24),
(1, 'South Korea', '2026-08-10', '2026-08-14', 15),
(2, 'United Kingdom', '2026-06-05', '2026-06-09', 1.2),
(2, 'Germany', '2026-07-12', '2026-07-15', 1.0),
(2, 'Singapore', '2026-08-01', '2026-08-05', 0.5),
(5, 'Mexico', '2026-08-20', '2026-08-27', 0.9),
(7, 'Taiwan', '2026-07-15', '2026-07-20', 3.1),
(7, 'Thailand', '2026-08-25', '2026-09-02', 3.1),
(8, 'France/Italy/Spain (multi-leg)', '2026-08-01', '2026-08-15', 17.8);
```

### `technicians` (15, coast to coast)

```sql
INSERT INTO technicians (id, name, region) VALUES
(1, 'Priya Sharma', 'Toronto, ON'),
(2, 'Marco Ricci', 'Toronto, ON'),
(3, 'Chen Ming', 'Vancouver, BC'),
(4, 'Aaliyah Brown', 'Vancouver, BC'),
(5, 'Jean Tremblay', 'Montreal, QC'),
(6, 'Sophie Gagnon', 'Montreal, QC'),
(7, 'Ryan MacDonald', 'Calgary, AB'),
(8, 'Grace Okonkwo', 'Ottawa, ON'),
(9, 'Tyler Fontaine', 'Winnipeg, MB'),
(10, 'Liam O''Brien', 'Halifax, NS'),
(11, 'Noor Hassan', 'Edmonton, AB'),
(12, 'Isabelle Roy', 'Quebec City, QC'),
(13, 'Dakota Whitehorse', 'Saskatoon, SK'),
(14, 'Connor Walsh', 'St. John''s, NL'),
(15, 'Émilie Bernard', 'Fredericton, NB');
```

David Kim (customer 4, Toronto) is the Scenario 2 demo customer — Toronto has 2 technicians (Priya Sharma, Marco Ricci), so he always has real alternatives to offer if a slot needs rescheduling.

### `technician_availability` — all of October 2026, generated

Rather than hand-typing ~150+ rows, this generates 2 time slots on roughly 1-in-4 weekdays per technician across October — a realistic, non-identical spread (each technician's available days differ from the others') rather than everyone free on the same days:

```sql
INSERT INTO technician_availability (technician_id, date, time_slot, status)
SELECT
  t.id,
  d::date,
  slot,
  'available'
FROM technicians t
CROSS JOIN generate_series('2026-10-01'::date, '2026-10-31'::date, interval '1 day') AS d
CROSS JOIN (VALUES ('09:00-11:00'), ('13:00-15:00')) AS s(slot)
WHERE EXTRACT(ISODOW FROM d) NOT IN (6, 7)              -- weekdays only
  AND (EXTRACT(DAY FROM d)::int + t.id) % 4 = 0;          -- ~1 in 4 weekdays per technician, offset by technician id
```

This yields roughly 10–12 slots per technician (~150–180 rows total) spanning the entire month, so the workshop has real availability to query no matter which October date it's actually run on.
