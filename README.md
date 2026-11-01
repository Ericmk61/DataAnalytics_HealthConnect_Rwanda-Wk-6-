# HealthConnect Rwanda Healthcare Analytics

**AnalystLab Africa Experience Lab — Week 6 — Data Analytics Track**

A healthcare analytics project using **MySQL, Power Query and Power BI** to explore patient demographics, appointments, clinical activity, hospital operations, financial performance and patient experience.

## Project Objectives

- Understand the patient population and recorded healthcare demand.
- Analyze appointment patterns and clinical workload.
- Compare billing, collected payments and reported revenue.
- Examine staffing, hospital capacity and patient feedback.
- Present findings through a six-page Power BI dashboard.
- Document data-quality issues and analytical limitations.

## Tools Used

| Tool | Purpose |
|---|---|
| Excel | Initial data inspection and preparation |
| Power Query | Data transformation, appending and merging |
| MySQL / MySQL Workbench | SQL analysis |
| Power BI | Data modelling, DAX measures and dashboards |

The project guide specifies PostgreSQL. This project was implemented using MySQL, and the difference is documented. The supplied SQL script is a MySQL script.

## SQL Analysis

The SQL script is organized into 40 numbered analysis questions:

| Analysis Area | Questions |
|---|---|
| Patient analysis | 1–10 |
| Appointment analysis | 11–20 |
| Clinical analysis | 21–30 |
| Financial analysis | 31–40 |

Question 33 documents why service-level revenue cannot be calculated reliably from the available relationships.

The Week 6 SQL script uses the database name `HEALTHCARE_ANALYTICS`.

## Power BI Dashboard

The report contains six pages:

| Page | Focus |
|---|---|
| Executive Dashboard | Main healthcare performance indicators |
| Patient Analytics | Patient demographics, residence and chronic conditions |
| Clinical Analytics | Diagnoses, laboratory tests, prescriptions and referrals |
| Financial Dashboard | Billing, collections, payment methods and revenue |
| Operational Dashboard | Staff distribution, activity and hospital capacity |
| Patient Experience Dashboard | Ratings, feedback categories and satisfaction |

## Key Results

| Indicator | Result |
|---|---:|
| Registered patients | 20,000 |
| Recorded appointments | 5,000 |
| Facilities represented in appointments | 20 |
| Doctors | 350 |
| Total staff | 1,250 |
| Total billed | RWF 9,309,401,961 |
| Collected payments | RWF 8,389,454,556 |
| Outstanding billing balance | RWF 919,947,405 |
| Collection ratio | 90.12% |
| Average patient satisfaction | 2.99 / 5 |
| Feedback records | 21,064 |
| Beds | 2,000 |
| Equipment records | 200 |

Currency is treated as RWF based on the country master. The transaction files do not contain explicit currency fields.

## Main Findings

### Patient Profile

- Male patients: 10,090.
- Female patients: 9,910.
- Average recorded age: 45.03 years.
- Patients above 65: 5,487, representing 27.44% of registered patients.
- A chronic condition is recorded for 14,929 patients, representing 74.65%.
- Province-level patient counts describe patient residence.

### Appointments and Clinical Activity

- Follow-up appointments: 1,694.
- Consultations: 1,656.
- Emergency visits: 1,650.
- Most recorded diagnosis: Hypertension, with 1,059 records.
- Most recorded laboratory test: Malaria, with 1,272 records.
- Most prescribed medication: Amlodipine, with 1,068 prescription records.
- Average recorded admission duration: 5.49 days.
- Referrals: 4,708, of which 415 link to the supplied appointment table.

### Financial Performance

- Collected payments equal 90.12% of billed value.
- The outstanding balance is RWF 919,947,405 across 11,887 bills.
- Insurance claims total RWF 4,881,863,293.88.
- The separate Revenue Summary reports RWF 1,132,677,500 across 12 monthly records.
- Billing, payments, insurance claims and reported revenue represent different financial concepts.
- The outstanding balance does not establish a financial loss. Expense data are unavailable.

### Patient Experience

- Average satisfaction is 2.99 out of 5 across 21,064 feedback records.
- Feedback categories include Good, Poor, Excellent and Average.
- Only 1,756 feedback records link to the supplied appointment table.
- The feedback file has no response date or formal complaint indicator.

## Data Preparation and Modelling

- Preserved the original CSV files.
- Applied transformations in prepared copies and Power Query.
- Combined the geography hierarchy for patient residence analysis.
- Appended six staff-role files into one Medical Staff table.
- Imported one Doctor copy where duplicate source copies existed.
- Joined records using IDs.
- Retained unmatched records and unknown attributes.
- Kept clinical and financial tables at their appropriate record grain to avoid inflated totals.
- Did not treat repeated names as proof of the same person.

## Data-Quality Issues and Limitations

### Missing Appointment Parent Records

The supplied Appointments table contains `APT000001` through `APT005000`.

Across the source files, 60,000 distinct appointment IDs are observed. Therefore, 55,000 appointment references have no parent record in the supplied Appointments table.

| Related Dataset | Total Records | Matched Appointments | Unmatched |
|---|---:|---:|---:|
| Diagnoses | 5,000 | 5,000 | 0 |
| Laboratory tests | 5,000 | 2,272 | 2,728 |
| Prescriptions | 5,000 | 4,003 | 997 |
| Admissions | 5,000 | 586 | 4,414 |
| Referrals | 4,708 | 415 | 4,293 |
| Patient feedback | 21,064 | 1,756 | 19,308 |
| Billing | 60,000 | 5,000 | 55,000 |

Overall totals use the relevant source table. Breakdowns requiring appointment attributes must preserve an Unknown group or clearly describe the linked subset.

### Facility and Department Assignments

Recorded facility assignments differ from department-master associations in 1,187 staff records and 4,744 appointments.

The recorded IDs are preserved. Facility assignments are not guessed or overwritten without an authoritative mapping.

### Financial Interpretation

- Billing, payment and insurance-claim records lack transaction or effective dates.
- Recorded billing statuses differ from a billed-versus-paid classification on 39,961 bills.
- Without effective dates, these differences do not prove that every recorded status is incorrect.
- Approved insurance claims do not establish that reimbursement was received.
- Only RWF 694,551,320 of payments can be attributed through the supplied appointment table.
- Service-level revenue cannot be established because a direct service-to-appointment or service-to-billing relationship is missing.
- Expense data are absent, preventing profit and margin calculations.

### Capacity and Utilization

- All 2,000 beds are marked Available.
- Recorded bed occupancy is therefore 0% for this status snapshot.
- Dated bed-allocation history is unavailable.
- Equipment records contain no usage-hour history or operating-time denominator.
- Bed and equipment utilization over time cannot be established from these files.

## Project Files

| File or Folder | Contents |
|---|---|
| `README.md` | Project overview, findings and limitations |
| `sql/` | MySQL analysis script |
| `dashboards/` | Power BI dashboard and exported dashboard PDF |
| `reports/` | Business Insights Report |
| `presentation/` | Executive Presentation |
| `data/` | Project datasets, where included |

## How to Use the Project

1. Download the project files.
2. Import the prepared datasets into MySQL.
3. Use the table names expected by the SQL script.
4. Select `HEALTHCARE_ANALYTICS`, or update the database name consistently.
5. Check CSV encoding and ID column headers before running queries.
6. Open the Power BI file in Power BI Desktop.
7. Update the Power Query source paths to your local dataset folder.
8. Refresh the report and explore the six dashboard pages.
9. Read the documented limitations when interpreting totals and comparisons.

## Recommendations

- Restore missing appointment parent records from an authoritative source.
- Establish consistent facility and department mappings.
- Capture transaction dates and billing-status effective dates.
- Record services against appointments or billing records.
- Capture dated bed allocations and equipment usage.
- Retain unknown groups and clearly state the population behind each comparison.

## Project Scope

This repository presents the Week 6 healthcare analytics work: data preparation, MySQL analysis, Power BI dashboards, business findings and presentation.
