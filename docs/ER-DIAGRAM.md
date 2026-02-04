# ER Diagram - Doctor Patient System

## Entities

```mermaid
erDiagram
    USER ||--o| PATIENT : "is a"
    USER ||--o| DOCTOR : "is a"

    PATIENT ||--o{ APPOINTMENT : books
    DOCTOR ||--o{ APPOINTMENT : attends
    DOCTOR ||--|{ SLOT : has
    DOCTOR ||--|| PROFILE : has
    DOCTOR ||--o{ SPECIALIZATION : has

    USER {
        uuid id PK
        string email
        string password
        string role
        boolean verified
        datetime created_at
    }

    PATIENT {
        uuid id PK
        uuid user_id FK
        string name
        date dob
        string gender
    }

    DOCTOR {
        uuid id PK
        uuid user_id FK
        string name
        string license_no
        int experience
        decimal fee
    }

    PROFILE {
        uuid id PK
        uuid doctor_id FK
        text bio
        string clinic_address
    }

    SPECIALIZATION {
        uuid id PK
        uuid doctor_id FK
        string name
    }

    SLOT {
        uuid id PK
        uuid doctor_id FK
        string day
        time start_time
        time end_time
        int max_bookings
    }

    APPOINTMENT {
        uuid id PK
        uuid patient_id FK
        uuid doctor_id FK
        uuid slot_id FK
        datetime date
        string status
        text notes
    }
```

## Relationships

- User can be Patient or Doctor (role based)
- Doctor has Profile (1:1)
- Doctor has multiple Slots
- Doctor has multiple Specializations
- Patient books Appointments
- Doctor attends Appointments
