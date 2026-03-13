# E-commerce Data Model

This repository contains the database schema and entity-relationship design for a foundational E-commerce management system.

## 📊 Entity-Relationship Diagram

The following diagram illustrates the logical structure of the database, including primary keys, foreign keys, and the cardinality of relationships between entities.

![E-commerce Data Model](./E-commerce-Data-Model-2026-03-13-041534.svg)

---

## 🏗️ Schema Overview

The model is composed of four core entities designed to maintain data integrity and minimize redundancy:

### 1. Categories (`Categorias`)
* **Purpose:** Organizes products into logical groups (e.g., Electronics, Home, Clothing).
* **Key Fields:** `id_categoria` (PK), `nombre`.
* **Relationship:** Acts as a parent table for `Productos`.

### 2. Products (`Productos`)
* **Purpose:** Stores specific item data and pricing.
* **Key Fields:** `id_producto` (PK), `nombre`, `precio`, `id_categoria` (FK).
* **Constraint:** Each product must belong to a valid category.

### 3. Clients (`Clientes`)
* **Purpose:** Manages user information and contact details.
* **Key Fields:** `id_cliente` (PK), `nombre`, `email` (Unique).
* **Constraint:** The email field is unique to prevent duplicate accounts.

### 4. Orders (`Pedidos`)
* **Purpose:** Records the transaction header, linking a specific client to a specific date.
* **Key Fields:** `id_pedido` (PK), `id_cliente` (FK), `fecha`.
* **Relationship:** A single client can place multiple orders over time (1:N).

---

## 🚀 SQL Implementation

You can use the following script to initialize the database:

```sql
CREATE TABLE Categorias (
    id_categoria INT PRIMARY KEY,
    nombre VARCHAR(50)
);

CREATE TABLE Productos (
    id_producto INT PRIMARY KEY,
    nombre VARCHAR(100),
    precio DECIMAL(10, 2),
    id_categoria INT,
    FOREIGN KEY (id_categoria) REFERENCES Categorias(id_categoria)
);

CREATE TABLE Clientes (
    id_cliente INT PRIMARY KEY,
    nombre VARCHAR(100),
    email VARCHAR(100) UNIQUE
);

CREATE TABLE Pedidos (
    id_pedido INT PRIMARY KEY,
    id_cliente INT,
    fecha DATE,
    FOREIGN KEY (id_cliente) REFERENCES Clientes(id_cliente)
);
