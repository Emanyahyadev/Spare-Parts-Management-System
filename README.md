# Munir Enterprises — Spare Parts Management & Sales System

<div align="center">
  <img src="screenshots/logo.png" alt="Munir Enterprises Logo" width="180" style="margin-bottom: 15px;"/>
  <br/>
  <h2>Munir Enterprises — Industrial Spare Parts & POS Management System</h2>
  <p><em>A custom enterprise business management platform engineered for <strong>Munir Enterprises</strong> for industrial sewing and textile machinery spare parts inventory, multi-machine cross-referencing, POS billing, and ledger accounting.</em></p>

  <p>
    <a href="#-system-architecture"><img src="https://img.shields.io/badge/Architecture-Normalized%20Relational%20%2B%20FTS5-0052CC?style=for-the-badge&logo=sqlite&logoColor=white" alt="Architecture" /></a>
    <a href="#-technology-stack"><img src="https://img.shields.io/badge/Stack-Python%20%7C%20Flask%20%7C%20Vanilla%20JS-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Tech Stack" /></a>
    <a href="#-machinery--parts-catalog-statistics"><img src="https://img.shields.io/badge/Dataset-25%2C299%20Parts%20%7C%2041%20Machines-4CAF50?style=for-the-badge" alt="Dataset" /></a>
    <a href="#-project-status--deployment"><img src="https://img.shields.io/badge/Client-Munir%20Enterprises-orange?style=for-the-badge" alt="Client" /></a>
    <a href="#-project-status--deployment"><img src="https://img.shields.io/badge/Status-Live%20Commercial%20Deployment-success?style=for-the-badge" alt="Status" /></a>
  </p>
</div>

---

## 📑 Table of Contents
- [Executive Overview](#-executive-overview)
- [Client Context & Business Problem](#-client-context--business-problem)
- [The Engineering Solution](#-the-engineering-solution)
- [Core Functional Modules](#-core-functional-modules)
- [Machinery & Parts Catalog Statistics](#-machinery--parts-catalog-statistics)
- [Visual Interface Walkthrough & Technical Details](#-visual-interface-walkthrough--technical-details)
  - [1. Executive Central Dashboard](#1-executive-central-dashboard)
  - [2. Sub-5ms Instant Full-Text Search](#2-sub-5ms-instant-full-text-search)
  - [3. Machine Catalog & Sub-Assembly Explorer](#3-machine-catalog--sub-assembly-explorer)
  - [4. Single Part Profile & Cross-Machine Matrix](#4-single-part-profile--cross-machine-matrix)
  - [5. Rapid Point of Sale (POS) Cashier Terminal](#5-rapid-point-of-sale-pos-cashier-terminal)
  - [6. Sales Invoicing & Order Lifecycle Management](#6-sales-invoicing--order-lifecycle-management)
  - [7. Stock Intake & Procurement Workflow](#7-stock-intake--procurement-workflow)
  - [8. Customer Credit Ledger (Khata) & Receivables](#8-customer-credit-ledger-khata--receivables)
  - [9. Vendor Procurement & Payables Ledger](#9-vendor-procurement--payables-ledger)
- [System Architecture & Data Modeling](#-system-architecture--data-modeling)
- [End-to-End Operational Workflows](#-end-to-end-operational-workflows)
- [Technology Stack Matrix](#-technology-stack-matrix)
- [Key Engineering Highlights & Algorithms](#-key-engineering-highlights--algorithms)
- [Role & Engineering Contributions](#-role--engineering-contributions)
- [Project Status & Deployment](#-project-status--deployment)
- [Proprietary Notice & Privacy Policy](#-proprietary-notice--privacy-policy)

---

## 🌟 Executive Overview

The **Munir Enterprises Spare Parts Management & Sales System** is a custom enterprise platform architected and developed specifically for **Munir Enterprises**, a premier distributor and retailer of industrial sewing and textile equipment spare parts.

Industrial apparel machinery (overlockers, direct-drive lockstitchers, flatbed coverstitchers, automated electronic bartackers, buttonholers, and straight-knife cutting machines) involves intricate sub-assemblies and tens of thousands of individual mechanical components.

To streamline Munir Enterprises' counter sales, warehouse management, and commercial accounting, this platform unifies **25,299 unique spare parts**, **76,987 machine diagram cross-references**, and **41 heavy industrial machine models** across **14 international manufacturers**. It serves as an all-in-one operational system connecting OEM technical manuals to physical warehouse bins (`Rack`/`Bin`), rapid POS billing, and automated customer/vendor credit ledgers (*Khata*).

---

## 🏢 Client Context & Business Problem

Prior to the deployment of this custom platform at **Munir Enterprises**, the daily retail and wholesale distribution operations faced critical bottlenecks:

1. **Extreme Cross-Machine Compatibility**:
   - Standardized parts (needle clamps, loopers, feed dogs, tension disks, screws) fit across multiple machine models and diagram sub-sections.
   - *Problem*: Generic inventory software required creating duplicate entries for each machine, leading to fractured stock numbers, phantom inventory, and stockout errors.
2. **High-Speed Counter Sales & Search Latency**:
   - Customers arrive at Munir Enterprises requesting parts via varying formats: official OEM part codes (`B1521-555-000`), punctuation-stripped numbers (`B1521555000`), machine model names (`Juki 8700 needle bar`), or colloquial Urdu/English trade names.
   - *Problem*: Manually thumbing through heavy paper parts manuals caused customer wait times and counter congestion.
3. **Dual Data Lifecycle (OEM Catalogs vs. Shop Inventory)**:
   - Parts required two distinct contexts:
     - **OEM Technical Blueprint**: Exploded diagram reference numbers, section names (e.g., *Needle Bar & Thread Take-up Mechanism*), page numbers, and catalog quantities.
     - **Munir Enterprises Physical Inventory**: Physical warehouse coordinates (`Rack B-04`, `Bin 12`), purchase cost, dynamic selling prices, supplier links, and vernacular Urdu descriptions.
4. **Credit Accounting (*Khata*) & Zero-Downtime Offline Needs**:
   - Industrial wholesale depends heavily on customer credit accounts with rolling balances and partial collections.
   - Cloud-dependent web software suffered from internet unreliability in commercial wholesale markets, making a high-speed offline desktop solution an absolute necessity.

---

## 💡 The Engineering Solution

```
┌───────────────────────────────────────────────────────────────────────────────────────┐
│                    MUNIR ENTERPRISES UNIFIED PLATFORM ARCHITECTURE                    │
├───────────────────────────────┬───────────────────────────────┬───────────────────────┤
│    Catalog Blueprint Layer    │    Physical Inventory Layer   │  Financial & POS Layer│
│  (Many-to-Many Cross Mappings)│   (Unique Physical Stock Bin) │  (Real-Time Balances) │
├───────────────────────────────┼───────────────────────────────┼───────────────────────┤
│ • 14 Global Manufacturers     │ • Unified Part Code Key       │ • <50ms POS Checkout  │
│ • 41 Industrial Machine Books │ • Warehouse Rack Coordinates  │ • Atomic Stock Deduct │
│ • 76,987 Diagram Mappings     │ • Live On-Hand Quantity       │ • Customer Khata Book │
│ • Exploded Schematic Ref #s   │ • Safety Reorder Alerts       │ • Vendor Payables Log │
│ • PDF Page & Section Guides   │ • Weighted Unit Cost History  │ • Audit Trail Logging │
└───────────────────────────────┴───────────────────────────────┴───────────────────────┘
```

The system delivered for Munir Enterprises provides:
- **Normalized Many-to-Many Relational Structure**: Cleanly isolates OEM technical blueprints from physical stock bins. One physical bin in the warehouse serves all compatible machines automatically.
- **Sub-5ms Symbol-Agnostic FTS5 Search**: An indexed full-text engine tokenizing codes and names into alphanumeric keys (`normalize_code()`), resolving search queries instantly regardless of hyphens, slashes, or spacing.
- **High-Speed Keyboard-Driven POS**: Complete point-of-sale cashier terminal supporting live stock deduction, split payments (Cash / Credit Khata / Bank), and instant thermal receipt printing.
- **Double-Entry Customer & Vendor Khata**: Real-time balance tracking, credit limit enforcement, and printable account statements.
- **Self-Contained Standalone Windows Deployment**: Low-footprint, zero cloud dependency, node-locked hardware activation, and automated database backups.

---

## ⚙️ Core Functional Modules

- **🔍 Multi-Parametric Search Engine**: Instant lookup across 25,000+ parts by part number, model, section, or English/Urdu keywords in under 5 milliseconds.
- **📚 Interactive Machinery Catalog**: Visual navigation across 41 industrial machine models, sub-assemblies, schematic reference numbers, and page guides.
- **⚡ Point-of-Sale (POS) & Billing**: Rapid checkout terminal with keyboard shortcuts, live cart calculations, flexible discounts, and instant thermal receipt generation.
- **📦 Warehouse Rack Location System**: Binds each item to its physical storage coordinates (`Rack`, `Row`, `Bin`) for warehouse fulfillment.
- **📒 Customer Ledger (*Khata*)**: Real-time customer balance calculations, credit limit controls, and transaction statements.
- **🚚 Vendor Procurement & Payables**: Supplier consignment intake, automated weighted average cost updates, and payment ledgers.
- **🚨 Stock Movement & Audit Trail**: Chronological event logging for all stock moves (`sale`, `purchase`, `adjustment`, `return`) and master price modifications.

---

## 📊 Machinery & Parts Catalog Statistics

The Munir Enterprises platform manages an extensive dataset extracted, normalized, and indexed across 14 major equipment manufacturers:

### Summary Metrics
| Metric | Benchmark Count |
| :--- | :--- |
| **Client / System Deployment** | **Munir Enterprises** |
| **Total Equipment Manufacturers** | **14 International Brands** |
| **Total Industrial Machine Models** | **41 Machine Catalogs** |
| **Total Unique Spare Parts** | **25,299 Parts** |
| **Active Cataloged Inventory** | **24,054 Products** |
| **Total Machine-to-Part Mappings** | **76,987 Cross-References** |
| **Average Query Retrieval Speed** | **< 5 ms (SQLite FTS5)** |

### Complete Machine & Parts Breakdown Table
| Manufacturer | Machine Model | Cataloged Parts | Industrial Machine Category / Function |
| :--- | :--- | :---: | :--- |
| **Yamato** | `VG2700` | **4,820** | High-speed Cylinder Bed Interlock Stitch Machine |
| **Pegasus** | `L32 / L52` | **4,167** | High-speed Overlock / Safety Stitch Machine |
| **Pegasus** | `EX3200 / EX5200` | **3,902** | Advanced High-Speed Overedger Series |
| **Juki** | `LK-1900B` | **3,792** | Computer-controlled High-speed Bartacking Machine |
| **Juki** | `LH-3528` | **3,736** | Semi-Dry-Head 2-Needle Lockstitch Machine |
| **Brother** | `LH4-B814 MKII` | **3,629** | Lockstitch Buttonholer Machine |
| **Juki** | `LK-1850` | **3,229** | High-Speed Bartacking Machine |
| **Pegasus** | `W500 Series` | **3,173** | Flatbed Interlock / Coverstitch Machine Series |
| **Yamato** | `VC2700` | **3,029** | Cylinder Bed Interlock Stitch Machine |
| **Juki** | `LH-3168` | **2,845** | 2-Needle Lockstitch Machine with Large Hooks |
| **Zoje** | `ZJC2500` | **2,330** | High-speed Interlock Sewing Machine |
| **Pegasus** | `M732 / M752 (M700)` | **2,260** | Integrated High-Speed Overedger Series |
| **Generic** | `DCM-204` | **2,113** | Heavy Duty Industrial Lockstitch Machine |
| **Juki** | `LH-3128` | **1,920** | 2-Needle Lockstitch Machine |
| **Juki** | `DDL-9000B` | **1,914** | Direct-drive High-speed 1-Needle Lockstitch |
| **Brother** | `S-7200A` | **1,758** | Direct Drive Single Needle Lockstitcher |
| **Brother** | `KE-430H` | **1,755** | Electronic Direct Drive Lockstitch Bartacker |
| **Juki** | `DDL-900` | **1,743** | High-speed 1-Needle Lockstitch Machine |
| **Brother** | `KE-430FXII` | **1,674** | Electronic Programmable Lockstitch Bartacker |
| **Juki** | `MB-372 / MB-373` | **1,630** | Single-thread Chainstitch Button Sewing Machine |
| **Kingtex** | `CT4600` | **1,602** | High-speed Cylinder Bed Interlock Machine |
| **Brother** | `S-7300A` | **1,564** | Nexio Direct Drive Lockstitch Machine |
| **Eastman** | `Blue Streak` | **1,446** | Straight Knife Cloth Cutting Machine |
| **Brother** | `S-7100A` | **1,438** | Direct Drive Single Needle Lockstitch Machine |
| **Juki** | `DDL-8700-7` | **1,360** | 1-Needle Lockstitch with Automatic Thread Trimmer |
| **Juki** | `LBH-761 / 762 / 763` | **1,319** | 1-Needle Lockstitch Buttonholing Machine |
| **Kansai Special**| `B9500` | **1,310** | High-speed Feed-up-the-arm Interlock Machine |
| **Zoje** | `ZJ7000E` | **1,260** | Direct Drive Overlock Sewing Machine |
| **Newlong** | `NP-7A` | **1,221** | Portable Bag Closer Sewing Machine |
| **Juki** | `LBH-1790` | **1,211** | Computer-controlled High-speed Buttonholing |
| **Juki** | `DDL-8700 Series` | **1,119** | Standard 1-Needle Lockstitch Machine |
| **Juki** | `LK-1900` | **1,077** | Computer-controlled High-speed Bartacking Machine |
| **Siruba** | `700K / 700KD` | **1,006** | High-Speed Overlock Machine Series |
| **Pegasus** | `M900 Series` | **866** | Ultra High-Speed Overlock Machine Series |
| **Siruba** | `700F` | **839** | Super High-Speed Overedger |
| **Juki** | `MH-380` | **834** | High-speed Flatbed 2-Needle Chainstitch |
| **Juki** | `LBH-781/782/783/784`| **768** | Lockstitch Buttonholing Machine Series |
| **Juki** | `DDL-555-4` | **757** | 1-Needle Lockstitch Machine with Trimmer |
| **BS** | `BS-101` | **357** | Industrial Blindstitch Machine |
| **KM** | `KS-AU` | **177** | Vertical Cloth Cutting Machine |
| **Arrow** | `CM11` | **37** | Portable Blindstitch Machine |

---

## 📸 Visual Interface Walkthrough & Technical Details

Below is a walkthrough of the production user interfaces developed for Munir Enterprises, illustrating the user experience, workflow, and backend architectural implementations.

---

### 1. Executive Central Dashboard

<div align="center">
  <img src="screenshots/01_dashboard.png" alt="Executive Central Dashboard" width="95%"/>
</div>

#### 📋 Business Purpose & Workflow
The central dashboard provides the Munir Enterprises management team and cashier staff with real-time operational visibility: total cataloged items, low stock warnings, daily sales volume, and total outstanding customer credit receivables.

#### 🔧 Technical & Architectural Implementation
- **Instant Metric Aggregation**: Queries indexed summary views in SQLite with sub-10ms latency.
- **Quick Action Hub**: Instant keyboard shortcuts to Point-of-Sale (`POS`), Universal Search, Stock Inward, and Customer Accounts.
- **Automated Reorder Badging**: Dynamically highlights products requiring replenishment where `stock_qty <= min_level`.

---

### 2. Sub-5ms Instant Full-Text Search

<div align="center">
  <img src="screenshots/02_instant_search.png" alt="Instant Full-Text Search" width="95%"/>
</div>

#### 📋 Business Purpose & Workflow
Enables counter sales staff to locate any spare part in less than a second while attending customers. Staff can search using fragmented part numbers, machine models, or colloquial terms. Results display physical rack coordinates (`Rack B-04`), live stock levels, sales prices, and multi-machine compatibility.

#### 🔧 Technical & Architectural Implementation
- **SQLite FTS5 Trigram Engine**: Leverages virtual full-text search tables synchronized with master inventory.
- **Code Normalization Engine**: Preprocesses part codes through `normalize_code(code)` to strip hyphens, slashes, and spaces (`B1521-555-000` -> `B1521555000`), guaranteeing instant matches regardless of punctuation.
- **Compatibility Badge**: Shows real-time count of compatible machine models sharing the part.

---

### 3. Machine Catalog & Sub-Assembly Explorer

<div align="center">
  <img src="screenshots/03_machine_catalog.png" alt="Machine Catalog & Sub-Assembly Explorer" width="95%"/>
</div>

#### 📋 Business Purpose & Workflow
Allows technicians, machinists, and storekeepers to browse equipment catalogs organized by brand (Juki, Brother, Pegasus, Yamato, etc.) and model. Selecting a machine displays all schematic sub-assemblies (e.g., *Needle Bar Mechanism*, *Feed Dog Assembly*, *Hook Driving Shaft*), exploded diagram reference numbers, and catalog pages.

#### 🔧 Technical & Architectural Implementation
- **Many-to-Many Relational Traversal**: Joins `machines` -> `catalog_entries` -> `products`.
- **Schematic Reference Mapping**: Retains exact OEM reference numbers (Ref #) and PDF page indexes for visual verification.
- **Section Grouping & Pagination**: Server-side pagination handling machines with up to 4,820 individual parts smoothly.

---

### 4. Single Part Profile & Cross-Machine Matrix

<div align="center">
  <img src="screenshots/04_part_details.png" alt="Part Profile & Compatibility Matrix" width="95%"/>
</div>

#### 📋 Business Purpose & Workflow
The master record for a single inventory item. Displays OEM engineering specs alongside Munir Enterprises' physical shop data (rack coordinates, custom name, unit purchase cost, selling price, current stock, and safety threshold). Features an interactive matrix of every compatible machine model.

#### 🔧 Technical & Architectural Implementation
- **Single-Source Stock Integrity**: Modifications to rack coordinates or pricing propagate instantly to all machine associations.
- **Compatibility Cross-Join Query**: 
  ```sql
  SELECT m.model, mf.name as manufacturer, ce.section, ce.ref_number, ce.pdf_page
  FROM catalog_entries ce
  JOIN machines m ON ce.machine_id = m.id
  JOIN manufacturers mf ON m.manufacturer_id = mf.id
  WHERE ce.product_id = ?;
  ```
- **Live Stock Indicator & Edit Triggers**: Allows immediate price adjustments and stock modifications with automatic audit logging.

---

### 5. Rapid Point of Sale (POS) Cashier Terminal

<div align="center">
  <img src="screenshots/05_pos_checkout.png" alt="Point of Sale Cashier Terminal" width="95%"/>
</div>

#### 📋 Business Purpose & Workflow
Engineered for rapid checkout during rush counter hours. Cashiers search parts directly inside the POS screen, add items to the cart, adjust quantities, apply discounts, and assign the customer. Supports one-click payment mode toggling (Cash, Customer Khata Credit, or Bank Deposit).

#### 🔧 Technical & Architectural Implementation
- **Vanilla JavaScript Reactive Cart**: Zero-dependency client-side cart calculation with instant total, tax, and discount computations.
- **Customer Balance HUD**: Selecting an account customer immediately displays their current outstanding ledger balance and credit limit.
- **Stock Guard Validation**: Visual warnings prevent cashier from selling items exceeding available stock in hand.

---

### 6. Sales Invoicing & Order Lifecycle Management

<div align="center">
  <img src="screenshots/06_sales_invoices.png" alt="Sales Invoices & Order Management" width="95%"/>
</div>

#### 📋 Business Purpose & Workflow
A central register of all completed customer transactions. Provides instant search by invoice number, customer name, date range, or payment type. Cashiers can reprint formatted 80mm thermal receipts or full-page A4 invoices and perform invoice revisions or returns.

#### 🔧 Technical & Architectural Implementation
- **Atomic Stock Reversal Engine**: When modifying or cancelling an invoice, the system automatically restores deducted inventory, creates audit log entries, and recalculates the customer's ledger balance.
- **Printable CSS Media Queries**: Native browser print styling formatted for standard ESC/POS thermal receipt printers and desktop printers without third-party drivers.

---

### 7. Stock Intake & Procurement Workflow

<div align="center">
  <img src="screenshots/07_stock_intake.png" alt="Stock Intake & Inward Procurement" width="95%"/>
</div>

#### 📋 Business Purpose & Workflow
The receiving dock interface used when new spare parts shipments arrive from manufacturers or distributors. The storekeeper selects the vendor, enters the consignment bill number, and logs received quantities alongside new unit purchase costs.

#### 🔧 Technical & Architectural Implementation
- **Batch Transaction Inward**: Executes multi-item stock increments within a single ACID database transaction.
- **Cost Averaging & Inventory Update**: Automatically updates `products.stock_qty` and records weighted `purchase_price`.
- **Vendor Ledger Synchronization**: Automatically posts a payable credit entry into the selected vendor's ledger account.

---

### 8. Customer Credit Ledger (Khata) & Receivables

<div align="center">
  <img src="screenshots/08_customer_khata.png" alt="Customer Credit Ledger Khata" width="95%"/>
</div>

#### 📋 Business Purpose & Workflow
Comprehensive ledger accounting for customer credit accounts. Tracks running balances, credit limits, chronological purchases, cash collections, bank transfers, and balance settlements. Provides quick payment recording with instant ledger receipt generation.

#### 🔧 Technical & Architectural Implementation
- **Double-Entry Balance Verification**: Computes real-time balances using `Opening Balance + Total Invoiced Sales - Total Payments Recorded`.
- **Credit Limit Guardrails**: Warns operators when a customer's total unpaid balance approaches or exceeds their defined credit ceiling.
- **Date-Filtered Ledger Export**: Formats chronological statement summaries for customer accounts.

---

### 9. Vendor Procurement & Payables Ledger

<div align="center">
  <img src="screenshots/09_vendor_ledger.png" alt="Vendor Procurement & Payables Ledger" width="95%"/>
</div>

#### 📋 Business Purpose & Workflow
Dedicated supplier accounting module recording all inventory purchases, returns, advance payments, and outstanding payables across all manufacturing and wholesale vendors.

#### 🔧 Technical & Architectural Implementation
- **Supplier Liability Tracking**: Automatically increments liabilities upon stock intake and decrements them upon recording vendor payment disbursements.
- **Procurement History Breakdown**: Inspects historical purchase orders, unit prices, and delivered batch quantities per supplier.

---

## 🏗️ System Architecture & Data Modeling

The system is architected as a modular, three-tier desktop application optimized for reliability and zero latency:

```mermaid
graph TD
    subgraph ClientLayer ["Presentation & Cashier Layer (HTML5 / CSS3 / Vanilla ES6)"]
        UI_Dash[Executive Dashboard]
        UI_FTS[Sub-5ms FTS Search]
        UI_POS[POS Billing Terminal]
        UI_Cat[Machine & Parts Explorer]
        UI_Ledger[Customer & Vendor Khata]
    end

    subgraph AppLayer ["Application & Business Logic (Python 3.12 / Flask Engine)"]
        Ctrl_Search[Search & Token Normalizer]
        Ctrl_POS[POS & Invoicing Transaction Manager]
        Ctrl_Stock[Stock Intake & Inventory Guard]
        Ctrl_Khata[Ledger Accounting & Credit Limits]
        Ctrl_Audit[Audit Logging & Backup Service]
    end

    subgraph StorageLayer ["Relational Database & FTS Engine (SQLite3)"]
        DB_Prod[(products - Master Stock & Bins)]
        DB_Mach[(machines & manufacturers)]
        DB_CatEntry[(catalog_entries - Many-to-Many Join)]
        DB_Sales[(sales & sale_items)]
        DB_Khata[(customers, vendors & payments)]
        DB_Moves[(stock_moves & audit_log)]
        DB_FTS5[(products_fts - FTS5 Virtual Table)]
    end

    ClientLayer --> AppLayer
    AppLayer --> StorageLayer

    Ctrl_Search --> DB_FTS5
    Ctrl_Search --> DB_Prod
    Ctrl_POS --> DB_Sales
    Ctrl_POS --> DB_Prod
    Ctrl_POS --> DB_Moves
    Ctrl_POS --> DB_Khata
    Ctrl_Stock --> DB_Prod
    Ctrl_Stock --> DB_Moves
    Ctrl_Stock --> DB_Khata
    Ctrl_Khata --> DB_Khata
```

### Relational Entity-Relationship Diagram (ERD)

```
┌─────────────────────┐          ┌─────────────────────┐          ┌─────────────────────┐
│    manufacturers    │1        *│      machines       │1        *│   catalog_entries   │
├─────────────────────┼──────────┼─────────────────────┼──────────┼─────────────────────┤
│ id (PK)             │          │ id (PK)             │          │ id (PK)             │
│ name                │          │ manufacturer_id(FK) │          │ product_id (FK) ────┼──┐
└─────────────────────┘          │ model               │          │ machine_id (FK)     │  │
                                 │ source_file         │          │ ref_number          │  │
                                 └─────────────────────┘          │ section             │  │
                                                                  │ pdf_page            │  │
                                                                  └─────────────────────┘  │
                                                                                           │
┌─────────────────────┐          ┌─────────────────────┐                                   │
│       vendors       │1        *│      products       │*                                 1│
├─────────────────────┼──────────┼─────────────────────┼───────────────────────────────────┘
│ id (PK)             │          │ id (PK)             │
│ name                │          │ manufacturer_id(FK) │          ┌─────────────────────┐
│ phone               │          │ vendor_id (FK)      │1        *│     sale_items      │
│ opening_balance     │          │ part_code           ├──────────┼─────────────────────┤
└─────────────────────┘          │ code_key (Indexed)  │          │ id (PK)             │
                                 │ custom_name         │          │ sale_id (FK)        │
                                 │ rack (Location)     │          │ product_id (FK)     │
                                 │ stock_qty, min_level│          │ qty, price, cost    │
                                 │ purchase/sale_price │          └─────────────────────┘
                                 └─────────────────────┘                     │*
                                            │1                               │
                                            │*                               │1
                                 ┌─────────────────────┐          ┌─────────────────────┐
                                 │     stock_moves     │          │        sales        │
                                 ├─────────────────────┤          ├─────────────────────┤
                                 │ id (PK)             │          │ id (PK)             │
                                 │ product_id (FK)     │          │ invoice_no (Unique) │
                                 │ qty_change, kind    │          │ customer_id (FK)    │
                                 │ unit_cost, date     │          │ subtotal, discount  │
                                 └─────────────────────┘          │ total, paid_amount  │
                                                                  └─────────────────────┘
```

---

## 🔄 End-to-End Operational Workflows

### POS Sale & Inventory Deduct Transaction Cycle

```mermaid
sequenceDiagram
    autonumber
    actor Cashier
    participant UI as POS Terminal (Browser UI)
    participant Server as Flask Controller
    participant FTS as FTS5 Engine
    participant DB as SQLite3 Transaction Engine

    Cashier->>UI: Types "B1521" or "needle clamp" into search bar
    UI->>Server: GET /api/search?q=B1521
    Server->>FTS: Query normalized code & trigrams
    FTS-->>Server: Matched Product IDs
    Server->>DB: Fetch prices, rack coords & current stock_qty
    Server-->>UI: JSON Search Results (Instant Dropdown)
    Cashier->>UI: Adds 2 items to Cart & selects Customer
    Cashier->>UI: Submits Checkout (Payment: Cash / Credit)
    UI->>Server: POST /sales/create (Cart Payload)
    critical ACID Transaction Execution
        Server->>DB: Validate stock availability (stock_qty >= 2)
        Server->>DB: INSERT INTO sales (invoice_no, total, paid)
        Server->>DB: INSERT INTO sale_items (product_id, qty, price, cost)
        Server->>DB: UPDATE products SET stock_qty = stock_qty - 2
        Server->>DB: INSERT INTO stock_moves (product_id, qty_change=-2, kind='sale')
        Server->>DB: UPDATE customers SET balance (if credit sale)
    end
    Server-->>UI: 200 OK + Invoice Payload
    UI->>Cashier: Displays Printable Thermal Invoice
```

---

## 💻 Technology Stack Matrix

| Layer / Domain | Technology Choice | Engineering Rationale & Implementation |
| :--- | :--- | :--- |
| **Backend Framework** | **Python 3.12 / Flask** | High-performance, lightweight WSGI server architecture with rapid request execution and Jinja2 templates. |
| **Database Engine** | **SQLite3 (ACID Embedded)** | Zero-configuration, serverless relational database offering robust multi-table transactions and low memory footprint. |
| **Full-Text Search** | **SQLite FTS5 Virtual Tables** | Trigram and prefix-tokenized indexing delivering sub-5ms query resolution over 25,000+ items. |
| **Token Normalization**| **Regex / Custom Tokenizer** | Neutralizes hyphens, slashes, and spaces to support robust symbol-agnostic lookups (`normalize_code()`). |
| **Frontend UI/UX** | **HTML5, CSS3, Vanilla JS** | Lightweight, responsive, keyboard-driven POS interface with zero external framework runtime overhead. |
| **Desktop Distribution**| **PyInstaller + Inno Setup** | Packaged into a standalone Windows installer (`.exe`) with auto-start batch routines and embedded SQLite storage. |
| **Security & Integrity**| **Hardware Node-Locking** | Machine-fingerprinted licensing mechanism and immutable audit trail logging. |

---

## 💡 Key Engineering Highlights & Algorithms

1. **Many-to-Many Catalog Normalization**:
   Eliminated duplicate inventory records across 41 industrial machine catalogs by introducing the `catalog_entries` normalization bridge. One physical bin of screws in `Rack A-02` automatically maps to 12 different machine schematics.
2. **Separator-Free Code Key Search**:
   Industrial part numbers are inconsistent across manufacturers (e.g., `B1521-555-000`, `B1521.555.000`, `B1521 555 000`). The system automatically indexes an alphanumeric key `B1521555000` via automated triggers, ensuring 100% search accuracy regardless of punctuation.
3. **Atomic Financial & Stock Transactions**:
   All stock deductions, invoice insertions, ledger balance updates, and stock move records are executed inside atomic `BEGIN ... COMMIT` database transactions to prevent partial writes during system interruptions.
4. **Air-Gapped Offline-First Reliability**:
   Engineered to run seamlessly without an active internet connection, featuring automated database backups on startup and shutdown to protect business data against power interruptions.

---

## 👨‍💻 Role & Engineering Contributions

As the **Lead Architect & Full-Stack Developer**, I developed the custom platform for **Munir Enterprises**:
- **System Architecture**: Designed the normalized relational schema, FTS5 virtual tables, and transactional ledger model.
- **Data Engineering**: Implemented the extraction and normalization pipeline that ingested 76,000+ parts mappings from 41 OEM machine manuals.
- **Application Development**: Built the Flask backend APIs, reactive JavaScript POS cart, and thermal printing stylesheets.
- **Desktop Engineering**: Created the standalone Windows packaging pipeline using PyInstaller and Inno Setup with node-locked hardware activation.

---

## 🚀 Project Status & Deployment

- **Client**: **Munir Enterprises**
- **Status**: **Completed & Deployed in Commercial Production**
- **Operational Profile**: Live production backbone powering daily retail counter sales, warehouse inventory management, and financial accounting.
- **Maintenance**: Active operational support with automated local backup routines.

---

## 🔒 Proprietary Notice & Privacy Policy

> **Intellectual Property & Portfolio Notice:**  
> This repository is a **public portfolio case study and architectural reference** of the custom software developed for Munir Enterprises.  
> 
> The underlying source code, database implementations, and client business datasets are private commercial assets and are **not distributed publicly**. All screenshots and examples displayed in this documentation feature sanitized demonstration data.

---

<div align="center">
  <sub>Developed for Munir Enterprises • Engineered by Abdul Nafay</sub>
</div>
