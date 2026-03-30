This Spring Boot application uses both MVC and REST controllers. Thymeleaf templates are used for the Admin and Doctor dashboards, while REST APIs serve all other modules. The application interacts with two databases—MySQL (for patient, doctor, appointment, and admin data) and MongoDB (for prescriptions). All controllers route requests through a common service layer, which in turn delegates to the appropriate repositories. MySQL uses JPA entities while MongoDB uses document models.

1. The user accesses the Admin Dashboard or Appointment pages through the frontend UI.

2. The request is routed to the appropriate Thymeleaf controller (for web pages) or REST controller (for API calls).

3. The controller delegates the request to the service layer, which contains the business logic.

4. The service processes the request and interacts with the relevant domain models (Patient, Doctor, Appointment, Admin, or Prescription).

5. For structured relational data (Patient, Doctor, Appointment, Admin), the service communicates with the MySQL database via repositories/DAOs.

6. For unstructured or document-based data (e.g., Prescription), the service interacts with the MongoDB database through its respective repositories.

7. The service returns processed data to the controller, which then sends the response back to the UI (rendered view or JSON response).
