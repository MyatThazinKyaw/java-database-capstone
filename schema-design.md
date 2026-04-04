## MySQL Database Design

### Table: patients
- id: INT, Primary Key, Auto Increment
- first_name: VARCHAR(50), Not Null
- last_name: VARCHAR(50), Not Null
- date_of_birth: DATE, Not Null
- gender: ENUM('male','female','other')
- email: VARCHAR(100), UNIQUE, Not Null
- phone: VARCHAR(20), UNIQUE, Not Null
- address: TEXT
- is_active: BOOLEAN, Default TRUE
- created_at: TIMESTAMP, Default CURRENT_TIMESTAMP

Comments:
- Soft delete using is_active preserves medical history
- Email/phone format validated in application layer

### Table: clinic_locations
- id: INT, Primary Key, Auto Increment
- name: VARCHAR(100), Not Null
- address: TEXT, Not Null
- phone: VARCHAR(20), Not Null

### Table: doctors
- id: INT, Primary Key, Auto Increment
- first_name: VARCHAR(50), Not Null
- last_name: VARCHAR(50), Not Null
- specialization: VARCHAR(100), Not Null
- email: VARCHAR(100), UNIQUE, Not Null
- phone: VARCHAR(20), UNIQUE, Not Null
- clinic_location_id: INT, NULL, Foreign Key → clinic_locations(id), ON DELETE SET NULL
- is_active: BOOLEAN, Default TRUE
- created_at: TIMESTAMP

Comments:
- Doctor records are never hard deleted
- If clinic is removed → doctor remains (SET NULL)
  
### Table: appointments
- id: INT, Primary Key, Auto Increment
- doctor_id: INT, Foreign Key → doctors(id), Not Null, ON DELETE RESTRICT
- patient_id: INT, Foreign Key → patients(id), Not Null, ON DELETE RESTRICT
- appointment_start: DATETIME, Not Null
- appointment_end: DATETIME, Not Null
- status: ENUM('scheduled','completed','cancelled'), Default 'scheduled'
- notes: TEXT

Constraint (Prevents Double Booking):
- UNIQUE (doctor_id, appointment_start)
- CHECK (appointment_end > appointment_start)

Comments:
- Start/end time allows flexible durations
- Overlap validation is handled in application layer
- Appointments must be preserved for audit/history; deletion of doctors/patients is restricted to prevent orphan records

### Table: admin
- id: INT, Primary Key, Auto Increment
- username: VARCHAR(50), UNIQUE, Not Null
- password_hash: VARCHAR(255), Not Null
- email: VARCHAR(100), UNIQUE, Not Null
- role: ENUM('admin','staff','manager'), Default 'admin'
- created_at: TIMESTAMP

### Table: payments
- id: INT, Primary Key, Auto Increment
- appointment_id: INT, Foreign Key → appointments(id), Not Null, ON DELETE CASCADE
- amount: DECIMAL(10,2), Not Null
- payment_method ENUM('cash','card','online','insurance')
- transaction_reference: VARCHAR(100), UNIQUE
- status: ENUM('pending','completed','failed'), Default 'pending'
- payment_date: TIMESTAMP, Default CURRENT_TIMESTAMP

Comments:
- Linked to appointment for billing traceability
- Cascade ensures cleanup if appointment is removed

### Table: doctor_availability
- id: INT, Primary Key, Auto Increment
- doctor_id: INT, Foreign Key → doctors(id), Not Null, ON DELETE CASCADE
- day_of_week: INT (0 = Sunday, 6 = Saturday), Not Null
- start_time: TIME, Not Null
- end_time: TIME, Not Null

Constraint:
- CHECK (start_time < end_time)
- UNIQUE (doctor_id, day_of_week, start_time)

Comments:
- Defines valid working hours
- Prevents invalid schedule entries

### Table: prescriptions
- id: INT, Primary Key, Auto Increment
- appointment_id: INT, Foreign Key → appointments(id), Not Null, ON DELETE CASCADE
- medication_details: TEXT, Not Null
- created_at: TIMESTAMP

Comments:
- Fully tied to appointment
- Ensures legal and medical traceability

### Indexes:
- INDEX (appointments, appointment_start)
- INDEX (appointments, doctor_id)
- INDEX (appointments, patient_id)
- INDEX (payments, appointment_id)
- INDEX (prescriptions, appointment_id)
- INDEX (doctor_availability, doctor_id)

## MongoDB Collection Design
### Collection: logs
```json
{
  "_id": "ObjectId('66d91ab4c91f2a001e8a9c77')",
  "eventType": "APPOINTMENT_CREATED",
  "action": "CREATE",
  "status": "SUCCESS",
  "severity": "INFO",
  "timestamp": "2026-04-04T09:58:12Z",
  "actor": {
    "userType": "patient",
    "userId": 12
  },
  "target": {
    "entityType": "appointment",
    "entityId": 88
  },
  "details": {
    "doctorId": 5,
    "appointmentStart": "2026-04-04T10:00:00Z",
    "appointmentEnd": "2026-04-04T10:30:00Z",
    "appointmentStatus": "scheduled"
  },
  "context": {
    "source": "appointment_service",
    "environment": "production",
    "version": "v1"
  },
  "tags": [
    "appointment",
    "booking",
    "audit",
    "system-generated"
  ],
  "traceId": "tr_8f21a9c3_global",
  "metadata": {
    "requestId": "req_8f21a9c3",
    "ipAddress": "192.168.1.10",
    "device": "mobile",
    "platform": "android"
  }
}
