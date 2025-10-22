# System Features - TokoFlow

Dokumen ini menjelaskan daftar fitur sistem TokoFlow berdasarkan modul utama yang akan dikembangkan. Struktur ini menjadi panduan implementasi bertahap untuk solo developer.

---

## 1. Authentication & Access Module (MVP)

| Feature          | Description                                | Dependency       |
| ---------------- | ------------------------------------------ | ---------------- |
| Login            | Authenticate user with username & password | -                |
| JWT Access Token | Generate access token                      | Login            |
| Refresh Token    | Renew expired access token                 | JWT Access Token |
| RBAC             | Role-Based Access Control                  | Login            |
| Auth Middleware  | Protect backend routes                     | JWT Access Token |
| Logout           | Clear user session                         | Login            |

---

## 2. User & Store Management Module (MVP)

| Feature              | Description         | Dependency     |
| -------------------- | ------------------- | -------------- |
| Create User          | Add new user        | Authentication |
| Assign Role          | Owner/Admin/Kasir   | Create User    |
| Manage Stores        | CRUD store branches | -              |
| Assign User to Store | Bind user to store  | Manage Stores  |
| Deactivate User      | Disable user        | Create User    |

---

## 3. Product Management Module (MVP)

| Feature                    | Description         | Dependency     |
| -------------------------- | ------------------- | -------------- |
| Create Product             | SKU, Name           | User & Store   |
| Category                   | Organize products   | Create Product |
| Unit                       | pcs/box/pack        | Create Product |
| Pricing                    | Cost & sale price   | Create Product |
| Product Status             | Activate/Deactivate | Create Product |
| Barcode Support (optional) | Scan with barcode   | Create Product |

---

## 4. Inventory Module (MVP)

| Feature            | Description          | Dependency      |
| ------------------ | -------------------- | --------------- |
| Stock per Store    | Track stock by store | Product Module  |
| Initial Stock      | First stock input    | Stock per Store |
| Stock Ledger       | Track stock IN/OUT   | Stock per Store |
| Auto Reduce        | Reduce stock on POS  | POS Module      |
| Adjustment         | +/- stock difference | Stock Ledger    |
| Transfer (Phase 2) | Inter-store transfer | Stock Ledger    |

---

## 5. Point of Sale (POS) Module (MVP)

| Feature                | Description                        | Dependency       |
| ---------------------- | ---------------------------------- | ---------------- |
| Search Product         | Search product by name/SKU/barcode | Product Module   |
| Add to Cart            | Add/remove product from cart       | Search Product   |
| Quantity Update        | Edit quantity directly in cart     | Add to Cart      |
| Auto Total Calculate   | Subtotal & total calculation       | Quantity Update  |
| Payment                | Cash / Transfer                    | Auto Total       |
| Save Transaction       | Save sales and sales detail        | Payment          |
| Auto Stock Reduce      | Stock deducted per sold item       | Save Transaction |
| Draft Transaction (\*) | Save transaction as pending        | Save Transaction |
| Receipt Print          | Print/download invoice             | Save Transaction |
| Barcode Support (\*)   | Ready for barcode scanner input    | Search Product   |

---

## 6. Customer Module (Next Phase)

| Feature                   | Description                    | Dependency    |
| ------------------------- | ------------------------------ | ------------- |
| Customer List             | View all customers             | -             |
| Create Customer           | Add new customer               | Customer List |
| Edit Customer             | Update customer details        | Customer List |
| Customer Purchase History | Track customer transactions    | POS Module    |
| Customer Search           | Search customers by name/phone | Customer List |

## 7. Supplier Module (Next Phase)

| Feature                   | Description                   | Dependency    |
| ------------------------- | ----------------------------- | ------------- |
| Supplier List             | View supplier data            | -             |
| Add Supplier              | Register new supplier         | Supplier List |
| Edit Supplier             | Update supplier data          | Supplier List |
| Supplier Purchase History | Track purchases from supplier | -             |

## 8. Purchase Order Module (Next Phase)

| Feature          | Description                       | Dependency       |
| ---------------- | --------------------------------- | ---------------- |
| PO List          | View list of purchase orders      | Supplier Module  |
| Create PO        | Create purchase order to supplier | PO List          |
| Approve PO       | Approve purchase order            | Create PO        |
| Receive Products | Input stock from supplier         | Inventory Module |
| PO History       | View PO activities                | PO List          |

## 9. Reporting Module (MVP)

| Feature               | Description                    | Dependency     |
| --------------------- | ------------------------------ | -------------- |
| Daily Sales Report    | Show daily transaction summary | POS Module     |
| Monthly Sales Report  | Monthly sales performance      | POS Module     |
| Stock Report          | Current stock by product/store | Inventory      |
| Stock Movement Report | Track stock in/out history     | Inventory      |
| Export Excel          | Export report to Excel         | Reporting Data |

---

## 10. Audit Trail Module (MVP)

| Feature                 | Description                         | Dependency       |
| ----------------------- | ----------------------------------- | ---------------- |
| User Activity Log       | Track user login/logout activity    | Authentication   |
| Data Change Log         | Record create/update/delete actions | All Modules      |
| Stock Movement Trace    | Monitor stock mutation history      | Inventory Module |
| Transaction Tracking    | Monitor POS transaction activities  | POS Module       |
| Audit Report Export(\*) | Export audit logs                   | Reporting Module |

---

Dokumen ini menjadi dasar untuk menyusun API Spec dan UI Flow selanjutnya.
