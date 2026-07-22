# Customer Support Analytics Platform

![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat&logo=postgresql&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![KPIs](https://img.shields.io/badge/KPIs%20%26%20Performance%20Analytics-6c757d)
![ETL](https://img.shields.io/badge/ETL%20%26%20Data%20Transformation-6c757d)
 
## Overview
Customer support analytics project built on top of a ticketing system database
(schema modeled after a real Freshdesk style deployment). The project focuses
on writing SQL queries that turn raw ticket data into three analytical layers
(case level detail, team performance, SLA performance), transforming that
output with Power Query and DAX, and loading it into Power BI to build an
interactive support operations dashboard.
 
Beyond the technical build, a core part of this project was designing the
KPIs themselves: defining which metrics actually reflect support team
efficiency and process health, not just visualizing numbers that already
existed.
 
All data used in the public version of this project is synthetic, generated
to preserve the exact table structure, column names and business logic of
the original production queries, without exposing any real company data.
 
## Features
- Relational data model for a support ticketing system (Tickets, Agents,
  Groups, Sources)
- Three SQL queries covering case level detail, team performance and SLA
  performance, using CTEs, window style time comparisons and duration
  calculations
- Rolling time window logic (last 24 hours, last 7 days, last 30 days) for
  team workload monitoring
- Monthly SLA tracking for first response time and resolution time
- Custom KPI design for support process optimization: first response
  resolution rate by ticket type and channel, team productivity vs target
  (overall and per agent), productivity deficit tracking, and segmented
  resolution time by category, month over month
- Power BI dashboard with calculated columns (business hours vs weekend,
  current month flag, hour bucketing) built on top of the SQL output
## Technologies
- SQL
- Power BI
- Power Query / DAX for ETL and the calculated report columns
- KPI design & Business Intelligence
## Workflow
- Ticket data lives in a relational database (Tickets, Agents, Groups,
  Sources)
- Three SQL queries extract and aggregate that data into three purpose
  built datasets: ticket detail, team performance and SLA performance
- KPIs are defined based on what actually drives support team efficiency
  (response speed, resolution speed, productivity vs target, workload
  distribution), not just what is easy to chart
- Power Query and DAX transform the SQL output into the calculated columns
  the dashboard needs
- Interactive dashboards are built on top of them to monitor support
  performance indicators
## Dashboard
The Power BI dashboard provides insights into:
- Support volume evolution (tickets, calls, chats, cases)
- First response resolution rate, by ticket type and channel
- Resolution time tracking, current month vs previous month
- Team productivity vs target, overall and per agent, with productivity
  deficit tracking
- Segmented resolution time by ticket category
- Call answer and resolution rates by team
## Project Purpose
The objective of this project was twofold: first, to design the KPIs that
actually reflect support process efficiency and team performance, not just
report on volume; and second, to build the SQL layer and Power BI dashboard
needed to track those KPIs on a recurring basis. The result is a monthly
support operations report that reduces manual reporting work and gives
managers a clear, up to date view of where the team is meeting targets and
where it is falling behind.
 
## Repository Contents
```
├── data_bd
│   ├── Data_BD_Tickets.csv
│   ├── Data_BD_Agentes.csv
│   ├── Data_BD_Grupos.csv
│   ├── Data_BD_Fuentes.csv
│   └── README.md
│
├── powerbi
│   ├── Dashboard.pbix
│   └── README.md
│
├── sql
│   ├── 01_Extraccion_Detalle_Tickets.sql
│   ├── 02_Rendimiento_Equipo.sql
│   ├── 03_Rendimiento_SLA.sql
│   └── README.md
│
└── README.md
```

## Author

Jorge Lozano




