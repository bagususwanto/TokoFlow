// Use DBML to define database structure
// Docs: https://dbml.dbdiagram.io/docs

/////////////////////////////////////////////////////////////
// SISTEM KASIR & STOK TOKO KECIL
// Author: Bagus Uswanto
// Created: 2025
/////////////////////////////////////////////////////////////

Table users {
id uuid [pk, not null]
username varchar [unique, not null]
password_hash varchar [not null]
role varchar [note: 'admin | kasir']
created_at timestamp
updated_at timestamp
}

Table products {
id uuid [pk, not null]
name varchar [not null]
category varchar
price decimal [not null, note: 'Harga satuan barang']
stock integer [not null, default: 0]
barcode varchar [unique, note: 'Optional, untuk scan barcode']
created_at timestamp
updated_at timestamp
}

Table sales {
id uuid [pk, not null]
user_id uuid [not null, note: 'Kasir yang melakukan transaksi']
total_price decimal [not null]
payment_type varchar [default: 'cash', note: 'cash | qris | transfer']
created_at timestamp
}

Table sale_items {
id uuid [pk, not null]
sale_id uuid [not null]
product_id uuid [not null]
quantity integer [not null, default: 1]
price decimal [not null, note: 'Harga per unit saat transaksi']
subtotal decimal [not null]
}

Table logs {
id uuid [pk, not null]
user_id uuid [not null]
action varchar [note: 'create_product, update_stock, delete_sale, etc.']
description text
created_at timestamp
}

/////////////////////////////////////////////////////////////
// RELATIONS
/////////////////////////////////////////////////////////////

// Relasi antar tabel utama
Ref: sales.user_id > users.id // many sales per user
Ref: sale_items.sale_id > sales.id // many items per sale
Ref: sale_items.product_id > products.id // many sale_items per product

// Log aktivitas user
Ref: logs.user_id > users.id
