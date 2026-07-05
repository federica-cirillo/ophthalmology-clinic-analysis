# Ophthalmology Clinic Simulation, Network & Data Management Model

A comprehensive analysis of the ophthalmology outpatient department at 
Clinica Mediterranea (Naples), covering workflow simulation, network 
infrastructure design, and database modeling. Developed for the 
**Healthcare Information Systems** university exam.

## Overview

The project analyzes the patient journey for a first or follow-up 
ophthalmology visit, covering three dimensions:
- **Workflow** — discrete-event simulation of the booking and visit process
- **Network infrastructure** — design of the clinic's network model
- **Data management** — relational database design

## 1. Workflow Simulation

The clinic operates Monday to Friday, 8:00–20:00. Bookings are handled by 
a call center (CUP) open Monday to Saturday, 9:00–17:00, via phone or email.

### AS-IS Model — Key Issues

Over a 1-year simulation period, two major bottlenecks were identified:

**Booking drop-out** (~20.49% of requests lost before becoming a booking):
| Channel | Requests | Drop-out rate |
|---------|----------|---------------|
| Phone | 10,135 | 25.84% (wait > 15 min) |
| Email | 8,759 | 13.33% (no reply within 4 days) |

**No-show / waiting list drop-out**: of 15,020 accepted bookings, **57.82%** 
were lost due to waiting times exceeding 40 days.

**Overall result**: only **24.89%** of the 18,894 yearly booking requests 
were fully processed (4,702 completed services).

### Objectives

- Reduce phone drop-out by at least 80%
- Reduce email drop-out by at least 80%
- Fully process at least 50% of booking requests

### WHAT-IF Model — Solution & Results

| Resource | AS-IS | WHAT-IF |
|----------|-------|---------|
| CUP operator | 1 | 2 |
| Ophthalmologist | 1 | 2 |
| Outpatient visit activity | 1 | 2 |

Results:
| Metric | AS-IS | WHAT-IF | Change |
|--------|-------|---------|--------|
| Phone/email drop-out | 25.84% / 13.33% | 0% / 0% | -100% |
| Fully processed requests | 24.89% (4,702) | 52.86% (9,987) | +112.4% |
| Avg. waiting time (visit queue) | 210.65 min | 119.24 min | -43.39% |
| Max waiting time (visit queue) | 435.00 min | 230.00 min | -47.13% |

All three objectives were met.

## 2. Network Infrastructure

The network design supports online booking (email to the clinic's call 
center) and a public website for service information, plus report 
delivery to patients via email. The clinic requires its own **mail 
server**, **DNS server**, and **HTTP server**; patients rely on external 
email providers.

Workstation layout:
- **Ground floor**: booking center, one PC per operator
- **First floor** (ophthalmology department): dedicated PCs for the 
  reception secretary, the physician's office, each diagnostic/treatment 
  room, and the pre-operative room

## 3. Database Design

A relational database was designed to track patients, bookings, visits, 
and prescribed exams/treatments. Main entities include:

`Patient`, `Medical History`, `Address`, `Booking`, `CUP Operator`, 
`Reception`, `Secretary`, `Visit`, `Doctor`, `Nurse`, `Report`, 
`Diagnostic Exam`, `Treatment`

Key relationships: a patient has one address and one medical history 
(1:1), can make multiple bookings (1:N), each booking maps to one 
reception record (1:1) and one visit (1:1); a visit produces one report, 
which may generate multiple diagnostic exams and/or treatments (1:N).

See the database diagram (`Modello_DataBase.png`) for the full schema.

## Repository Contents

- [`ElaboratoSIS_FedericaCirillo.pdf`](./ElaboratoSIS_FedericaCirillo.pdf) — full project report
- `ASIS.zip` — Simul8 AS-IS simulation model
- `WHATIF.zip` — Simul8 WHAT-IF simulation model
- `Cisco_ClinicaMediterranea.pkt` — Cisco Packet Tracer network model
- `Modello_DataBase.png` — entity-relationship diagram

## Tools

- **Simul8** — discrete-event simulation
- **Cisco Packet Tracer** — network modeling
- Relational database design (ER modeling)
