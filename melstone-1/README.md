# Milestone 1 — Project Proposal & Conceptual Database Design

## 1. Application Overview

### 1.1 Project Title
**Sneaker Catalog Database System**

### 1.2 Problem Statement
A sneaker storefront requires structured storage for products, variants (size/color), inventory, orders, and users. Without a relational database, the system risks duplicate product entries, inconsistent inventory counts, and poor order traceability. A relational model enforces data integrity and supports reporting and business rules.

### 1.3 System Users
- **Customer** — creates account, places orders, views order history (reads/writes `user`, `order`, `order_item`).  
- **Store Admin** — manages products and inventory (creates/updates `product`, `product_variant`).  
- **Guest** — browses catalog (reads `product`, `product_variant`).

### 1.4 Specific Data to Be Stored (7 examples)
- Product SKU  
- Product name  
- Variant size  
- Variant colorway  
- Inventory quantity  
- Order date  
- Customer email

## 2. Core System Features
1. **User registration & login** — creates `user` records; reads user profile; updates password.  
2. **Browse catalog** — reads `product` and `product_variant` tables.  
3. **Place order** — creates `order` and `order_item` records; updates `product_variant.inventory_quantity`.  
4. **Manage inventory** — admin updates `product_variant.inventory_quantity` (Update).  
5. **Product management** — admin creates/edits/deletes `product` records (Create/Read/Update/Delete).

## 3. Relational Table Definitions
**User**  
- `user_id` (PK)  
- `first_name`  
- `last_name`  
- `email`  
- `password_hash`  
- `role`

**Product**  
- `product_id` (PK)  
- `sku`  
- `name`  
- `brand`  
- `category`  
- `description`

**ProductVariant**  
- `variant_id` (PK)  
- `product_id` (FK)  
- `size`  
- `colorway`  
- `inventory_quantity`  
- `price`

**Order**  
- `order_id` (PK)  
- `user_id` (FK)  
- `order_date`  
- `status`  
- `total_amount`

**OrderItem**  
- `order_item_id` (PK)  
- `order_id` (FK)  
- `variant_id` (FK)  
- `quantity`  
- `unit_price`

## 4. CRUD Operations Overview
| Table | Create | Read | Update | Delete |
|---|---|---|---|---|
| User | Register account | View profile | Edit profile | Delete account |
| Product | Add product | View product | Edit product | Remove product |
| ProductVariant | Add variant | View variants | Update inventory | Remove variant |
| Order | Place order | View order history | Update status | Cancel order |
| OrderItem | Add order item | View order items | Update quantity | Remove item |

## 5. Relationship Logic
- **Product -> ProductVariant**: 1:M — a product can have many variants (size/color); each variant belongs to one product.  
- **Order -> OrderItem**: 1:M — an order contains many items; each item belongs to one order.  
- **User -> Order**: 1:M — a user can place many orders; each order belongs to one user.  
- **ProductVariant -> OrderItem**: 1:M — a variant can appear in many order items; each order item references one variant.

## 6. Business Rules
1. Product SKU must be unique.  
2. Inventory quantity cannot be negative.  
3. An order must reference an existing user and at least one order item.  
4. A user email must be unique.  
5. When an order is placed, `product_variant.inventory_quantity` must be decremented accordingly.

## 7. ER Diagram
See `er-diagram.png` in this folder. The diagram uses Crow’s Foot notation and matches the table and attribute names above.
