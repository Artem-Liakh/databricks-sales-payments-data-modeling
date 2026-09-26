# Data Documentation

This directory documents the input data sources used by the Databricks Sales & Payments Data Modeling project.

> **Note on Raw Data Storage:**
> Raw source CSV files (`sales.csv` and `payments.csv`) are not committed to this Git repository. Instead, they are hosted directly in a Databricks Unity Catalog Volume to simulate an enterprise Lakehouse ingestion architecture.

---

## Storage Location

In the Databricks Lakehouse workspace, the input CSV files reside in the following Unity Catalog Volume:

```text
/Volumes/data_lab/shop/raw/
├── sales.csv
└── payments.csv
```

Catalog: `data_lab`  
Schema: `shop`  
Volume: `raw`

---

## Source Datasets

### 1. `sales.csv`

* **Purpose:** Represents retail/e-commerce order line items exported from a CRM or Point of Sale (POS) system.
* **Grain:** One product line within a customer order.
* **Format:** Comma-Separated Values (CSV) with header row.

| Column Name | Inferred Spark Type | Description |
|:---|:---|:---|
| `order_id` | `integer` | Unique identifier of the customer order |
| `order_date` | `date` | Date when the order was placed (`YYYY-MM-DD`) |
| `customer_id` | `integer` | Unique identifier of the purchasing customer |
| `customer_name` | `string` | Full name of the customer |
| `city` | `string` | City associated with the customer order |
| `product_id` | `integer` | Unique identifier of the purchased item |
| `product_name` | `string` | Commercial title of the product |
| `category` | `string` | Product merchandise category (e.g., Ноутбуки, Смартфони, Аксесуари) |
| `quantity` | `integer` | Number of units purchased in this order line |
| `unit_price` | `integer` | Price per single unit in local currency (UAH) |

---

### 2. `payments.csv`

* **Purpose:** Represents individual financial payment transactions recorded by billing or payment gateway systems.
* **Grain:** One payment transaction event.
* **Format:** Comma-Separated Values (CSV) with header row.

| Column Name | Inferred Spark Type | Description |
|:---|:---|:---|
| `payment_id` | `integer` | Unique transaction identifier for the payment |
| `order_id` | `integer` | Business identifier of the order being paid for |
| `payment_date` | `date` | Date the payment transaction settled (`YYYY-MM-DD`) |
| `customer_id` | `integer` | Unique identifier of the paying customer |
| `customer_name` | `string` | Full name of the customer |
| `city` | `string` | City associated with the customer |
| `method` | `string` | Payment method utilized (e.g., `картка`, `готівка`, `Apple Pay`) |
| `amount` | `integer` | Amount settled in the transaction in local currency (UAH) |

---

## Relationship Between Sources

- An order in `sales.csv` can have multiple line items (multiple products per `order_id`).
- An order can be paid across multiple transactions in `payments.csv` (split payments, installments, or down payments) or have zero payments recorded yet.
- Both files contain denormalized customer attributes (`customer_name`, `city`), which are extracted, deduplicated, and conformed into `dim_customer` during data modeling.
