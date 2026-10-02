[![English](https://img.shields.io/badge/README-English-24292f?style=for-the-badge)](./README.md) [![한국어](https://img.shields.io/badge/README-%ED%95%9C%EA%B5%AD%EC%96%B4-24292f?style=for-the-badge)](./README.ko.md)

# Payroll Manager

A payroll management web app for academies that calculates weekly holiday allowance, night/holiday premiums, and taxes from assistant/instructor attendance records, and generates wage statements and Excel payroll workbooks.

## Features

- Manage employee/assistant information and work schedules
- Upload and automatically parse attendance files (xlsx/csv)
- Automatically calculate weekly holiday allowance, night-work premium, holiday-work premium, and paid annual-leave allowance
- Support 3.3% freelancer withholding, four major insurance schemes, and custom tax rates
- Print wage statements and save them as PDF
- **Export Excel (.xlsx) payroll workbooks** with formatted sheets for dashboard, payroll ledger, employee details, and attendance records

## Tech Stack

- React 19 + TypeScript + Vite
- Tailwind CSS
- xlsx-js-style (attendance parsing and formatted Excel payroll export)
- date-fns, framer motion (Motion), lucide-react
