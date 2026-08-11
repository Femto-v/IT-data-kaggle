## About the Dataset

This project utilizes an **IT Support Ticket Dataset** containing 29,651 helpdesk service requests across 10 distinct operational departments. The dataset captures raw incident text, assigned departments, urgency levels, and multi-label topic tags.

### Data Schema & Attributes

| Field Name | Data Type | Description | Usage in Power BI Model |
| :--- | :--- | :--- | :--- |
| **`Body`** | String (Text) | Verbatim, free-form issue description reported by the user. | Source for text length diagnostics and detail table inspection. |
| **`Department`** | Categorical String | Team assigned to resolve the request (e.g., *Technical Support, Billing & Payments*). | Primary category dimension for ticket volume breakdowns. |
| **`Priority`** | Categorical (Ordinal) | Ticket urgency level (*Low, Medium, High*). | Used in DAX filters to compute escalation rates (`High Priority %`). |
| **`Tags`** | List of Strings | Granular keywords and issue labels (e.g., `['Network', 'VPN', 'Disruption']`). | Explanatory dimension in the Decomposition Tree visual. |

### Feature Engineering & Data Transformations

To transform raw Kaggle data into an enterprise Star Schema model, the following Power Query transformations were applied:
* **Primary Key:** Created a unique `Ticket ID` text key mapped from original row indexes.
* **Text Complexity Metric:** Calculated `Body Character Count` via `Text.Length([Body])` as a proxy measure for issue complexity.
* **Date Dimension:** Generated a continuous 2025 calendar dataset (`Created Date`) linked to a DAX dynamic date table (`Dim_Date`).
* **Tag Cleaning:** Stripped bracket and quote string artifacts to display clean multi-label tags for category drill-downs.
