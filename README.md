# NHL Stats Connector for Power BI

A custom Power Query connector that brings NHL team, roster, player, and season-stat data into Power BI. It turns responses from the NHL Stats REST API into tables you can explore and use in reports.

> **Project status:** This is a small portfolio/demo connector, not an official NHL product. It currently exposes a fixed set of tables and seasons. The NHL API is an external dependency, so verify that the endpoints and response formats used by this project are still available before relying on it.

## What it does

The connector calls the NHL Stats API, parses its JSON responses, and presents the results through a Power Query navigation table:

| Table | Data |
| --- | --- |
| **Teams** | Team names, abbreviations, venue, division, and conference |
| **Players** | Team rosters and player details such as position, jersey number, and nationality |
| **2019 stats** | Single-season player statistics for the 2019 season |
| **2018 stats** | Single-season player statistics for the 2018 season |

Once connected, these tables can be shaped in Power Query, related in the Power BI data model, and used to build reports.

## Why this project

This project demonstrates a practical data-integration workflow: connecting a BI tool to a REST API, parsing nested JSON, transforming records and lists into tabular data, and packaging the result as a reusable Power Query data source. It is a focused example of **Power Query M**, API integration, and data preparation for analytics.

## How it works

1. `NHLStatsConnector.Contents` creates the connector's navigation table.
2. The connector requests team, roster, player, and season-stat resources from the NHL Stats API.
3. Power Query M expands the nested API responses into tables and columns.
4. Power BI can load those tables for further transformation and reporting.

The connector uses implicit authentication; no API key or account credentials are configured in this project.

## Repository layout

```text
NHLStatsConnector/
├── NHLStatsConnector.sln
└── NHLStatsConnector/
    ├── NHLStatsConnector.pq        # Connector logic and API transformations
    ├── NHLStatsConnector.query.pq  # Query used to exercise the connector
    ├── NHLStatsConnector.mproj     # Power Query connector project/build definition
    └── NHLStatsConnector*.png      # Connector icons
```

## Build and try it

This is a Power Query custom connector project, not a standalone application.

1. On Windows, install **Visual Studio** and the **Power Query SDK** extension.
2. Open `NHLStatsConnector.sln` in Visual Studio and build the solution. The project is configured to produce `NHLStatsConnector.mez` under `NHLStatsConnector/bin/Debug/` (or `Release/` for a Release build).
3. Install the `.mez` file using the custom-connector instructions for your Power BI product. Power BI Desktop may require you to configure its custom connector security/trust settings.
4. Restart Power BI Desktop, select **Get Data**, and look for **NHL - REST API DEMO**.
5. Connect and select one or more tables in the Navigator.

`NHLStatsConnector/NHLStatsConnector.query.pq` contains a sample Power Query expression that calls `NHLStatsConnector.Contents()`. Use the Power Query SDK's query/testing workflow to evaluate it while developing.

For current installation and security requirements, see Microsoft's [Power Query custom connector documentation](https://learn.microsoft.com/power-query/).

## Scope and limitations

- The seasons are currently hard-coded to **2018** and **2019**; users cannot select a season in the Navigator.
- The connector requests team rosters and then retrieves player details and statistics. These multi-step requests can be slow and depend on the API's availability and response shape.
- This repository does not include automated tests, a published `.mez` release, or a ready-made Power BI report.
- The API hostname and endpoints in the code may have changed since this demo was created.

## Technology

- Power Query M
- Power BI custom connector (`.mproj` / `.mez`)
- NHL Stats REST API (JSON)
- Visual Studio and the Power Query SDK for development
