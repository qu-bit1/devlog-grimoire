or mongosh 
##  MongoDB?

MongoDB is a **NoSQL** database. Instead of storing data in **tables and rows** (like SQL), it stores data as **documents** in **collections**. Each document is a JSON-like structure (called **BSON** under the hood).

---

## Core Concepts

| SQL Term    | MongoDB Equivalent |
| ----------- | ------------------ |
| Database    | Database           |
| Table       | Collection         |
| Row         | Document           |
| Column      | Field              |
| Primary Key | `_id`              |

---

## Example Document

```json
{
  "_id": "123",
  "name": "Rey",
  "email": "rey@example.com",
  "roles": ["admin", "user"],
  "profile": {
    "age": 24,
    "location": "India"
  }
}
```

---

## Structure
![[mongo-structure.excalidraw]]

