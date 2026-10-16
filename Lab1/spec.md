# Специфікація моделі даних (spec.md)
## 1.Опис предметної області
Система призначена для автоматизації оренди автомобілів клієнтами у філіях компанії. 
## 2.Сутності, атрибути та ключі
- **User(Клієнт):**
  - `user_id` (UUID, PK) — унікальний ідентифікатор клієнта
  - `full_name` (string) — повне ім'я
  - `email` (string) — електронна пошта
  - `phone` (string) — номер телефону
- **Car(Автомобіль):**
  - `car_id` (UUID, PK) — унікальний ідентифікатор авто
  - `office_id` (UUID, FK) — посилання на філію прив'язки
  - `brand` (string) — марка автомобіля
  - `model` (string) — модель автомобіля
  - `daily_rate` (number) — добова вартість оренди
- **Office(Філія / Офіс):**
  - `office_id` (UUID, PK) — унікальний ідентифікатор філії
  - `city` (string) — місто розташування
  - `address` (string) — адреса
- **Booking(Бронювання — Асоціативна сутність):**
  - `booking_id` (UUID, PK) — унікальний ідентифікатор бронювання
  - `user_id` (UUID, FK) — посилання на клієнта
  - `car_id` (UUID, FK) — посилання на авто
  - `start_date` (string) — дата початку оренди
  - `end_date` (string) — дата завершення оренди
  - `total_price` (number) — загальна вартість оренди
## 3.Критерії прийняття
1. Модель знаходиться в 3-й нормальній формі (3NF).
2. Чистий зв'язок M:N між User та Car реалізовано через асоціативну сутність Booking, оскільки він має власні атрибути (дати, вартість).
3. Усі первинні та зовнішні ключі мають уніфікований тип `UUID`.
## 4.Концептуальна ER-діаграма (Mermaid)
```mermaid
erDiagram
    USER ||--o{ BOOKING : "створює"
    CAR ||--o{ BOOKING : "включає"
    OFFICE ||--|{ CAR : "розміщує"
    USER {
        string user_id PK
        string full_name
        string email
        string phone
    }
    CAR {
        string car_id PK
        string office_id FK
        string brand
        string model
        number daily_rate
    }
    OFFICE {
        string office_id PK
        string city
        string address
    }
    BOOKING {
        string booking_id PK
        string user_id FK
        string car_id FK
        string start_date
        string end_date
        number total_price
    }
    ```