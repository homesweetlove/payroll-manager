[![English](https://img.shields.io/badge/README-English-24292f?style=for-the-badge)](./README.md) [![한국어](https://img.shields.io/badge/README-%ED%95%9C%EA%B5%AD%EC%96%B4-24292f?style=for-the-badge)](./README.ko.md)

# Payroll Manager

**From attendance files to reviewable payroll statements.**

Payroll Manager (조교급여대장 / Payroll Desk) is a browser-based payroll workflow for academy assistants and instructors. It collects employee settings, imports attendance records, calculates wage components with editable options, and exports reports for review.

The application currently runs **in the browser**: employee and payroll data are stored in that browser's `localStorage`, with manual JSON backup/restore. This is a project for organizing payroll calculations, **not a certified payroll or legal compliance system**.

## Features

| Workflow | Available functionality |
| --- | --- |
| Employee management | Names, roles, hourly wages, weekly schedules, paydays, default deductions and allowances; resignation information |
| Attendance import | Load `.xlsx`, `.xls` or `.csv` records; match attendance rows to registered employee names |
| Attendance review | Adjust breaks, absences, paid leave, public-holiday work, night work and per-week holiday-pay eligibility |
| Calculations | Base pay, weekly holiday allowance, overtime/night/holiday premiums, paid-leave pay, itemized allowances and deductions |
| Statements | Individual wage statements, PDF download and batch PDFs in a ZIP archive |
| Exports | Styled `.xlsx` payroll workbook, audit `.csv`, report `.json` and employee/full-backup `.json` |
| Dashboard | Saved payroll reports, historical inspection, comparisons and basic payroll summaries |

Deduction modes in the source include **3.3% freelancer**, **four-major-insurance estimates** and a **custom rate**. The preset percentages are code-defined assumptions, not a guarantee that they match current regulations or individual employment arrangements.

## Run locally

**Requirements:** Node.js and npm compatible with Vite 6. Node.js 20 or newer is recommended.

```bash
git clone https://github.com/homesweetlove/payroll-manager.git
cd payroll-manager
npm install
npm run dev
```

Open `http://localhost:3000` in your browser.

```bash
npm run lint     # TypeScript check
npm run build    # Production build
npm run preview  # Preview the production build
```

No external API key or database is required for the current workflow. See [`.env.example`](./.env.example).

## Typical workflow

1. In **조교 관리 (Employees)**, register each employee, hourly wage, standard work schedule and default deduction settings.
2. Go to **급여 정산 (Payroll)**, enter the academy name and upload an attendance spreadsheet.
3. Review imported attendance and choose how breaks, paid leave, holiday work and weekly holiday pay should be treated.
4. Check each employee's calculated amounts and adjust allowance or tax choices if needed.
5. Export an `.xlsx` payroll workbook or wage-statement PDFs, and save a report `.json` package for later inspection.
6. From the dashboard, inspect previous reports and periodically download a **full JSON backup**.

### Attendance file columns

The importer uses the **first worksheet**, skips the header row and reads these positions:

| Column | Meaning |
| --- | --- |
| A | Attendance date (Excel date or date string) |
| B | Employee name — must match a registered employee name |
| E | Clock-in time |
| F | Clock-out time |

Other columns are not used by the current attendance parser. Missing or unmatched names are skipped, so verify the imported row count and each employee's attendance before payroll export.

### Exported files

- **Excel workbook (`.xlsx`):** dashboard, payroll ledger, employee-specific details, attendance log and an optional prior-period comparison worksheet.
- **Statements:** single PDFs and a ZIP of employee PDF statements.
- **Audit report (`.csv`):** dashboard export for reviewing saved payroll data.
- **JSON (`.json`):** employee list backups, complete backups and payroll report packages with source settings and attendance records.

## Data handling and safety

**Important:** The employee model can contain resident registration numbers, bank accounts, salaries and attendance records.

- Data are stored in browser `localStorage`, **not in an encrypted database**. Other people with access to the same browser profile or device may access them.
- JSON/Excel/PDF exports can contain sensitive personal data; protect them outside the app and do not commit real employee files to GitHub.
- Clearing browser data or changing devices can remove your saved records. Keep backups somewhere you control and test restoring them with non-sensitive sample data.
- There is no built-in multi-user account system, access-control service or synchronized server-side storage in this repository.
- Before real payroll use, independently review labor-law eligibility, rates, rounding, tax/insurance rules and each calculated statement. Preset rates can become outdated.

For a public demonstration, use **fictional people and fabricated attendance records only**.

## Implementation map

```text
src/
├── App.tsx                  # Navigation, state persistence
├── views/
│   ├── Main.tsx             # Dashboard, history, audit / backups
│   ├── EmployeeManagement.tsx
│   └── PayrollCreation.tsx  # Import, review and calculation flow
├── components/
│   └── WageStatementSheet.tsx
├── lib/
│   ├── storage.ts           # Browser storage
│   ├── dataValidation.ts    # JSON backup validation
│   ├── excelExport.ts       # Styled Excel workbook
│   └── pdfExport.ts         # PDF and ZIP export
└── types.ts                 # Payroll data structures
```

**Stack:** React 19, TypeScript, Vite 6, Tailwind CSS, `xlsx-js-style`, `jspdf`, `html2canvas-pro`, `jszip` and `date-fns`.

## Scope

This repository documents a local-first operational prototype. It does not claim secure production handling of private payroll records, integration with tax authorities or automatic verification of the correctness of wage-law calculations.
