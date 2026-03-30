# Admin User Stories
**Admin Login:**
_As an admin, , I want to log into the portal using my username and password, so that I can securely access and manage the platform._

**Acceptance Criteria:**
1. Admin can enter valid username and password
2. System authenticates credentials
3. Admin is redirected to the dashboard on success
4. Error message is shown for invalid credentials

**Priority:** High

**Story Points:** 5

**Notes:**
- Implement password hashing and secure authentication (e.g., Spring Security)
- Consider account lockout after multiple failed attempts
- Handle session timeout for security
____________________________________________________________________________________________________

**Admin Logout:**
_As an admin, I want to log out of the portal, so that I can prevent unauthorized access to the system._

**Acceptance Criteria:**
1. Admin can click a logout button
2. Session is terminated securely
3. Admin is redirected to the login page
   
**Priority:** High

**Story Points:** 2

**Notes:**
- Ensure session invalidation on logout
- Clear cookies/token if applicable
____________________________________________________________________________________________________

**Add Doctor:**
_As an admin, I want to add doctors to the portal, o that they can be available for appointments._

**Acceptance Criteria:**
1. Admin can access an “Add Doctor” form
2. Required fields (name, specialization, contact, etc.) are validated
3. Doctor is saved successfully in the system
4. Confirmation message is displayed
   
**Priority:** High

**Story Points:** 5

**Notes:**
- Validate unique fields (e.g., email or license number)
- Consider file upload for profile image
- Handle incomplete or invalid form submissions
____________________________________________________________________________________________________

**Delete Doctor:**
_As an admin, I want to delete a doctor’s profile, so that outdated or inactive doctors are removed from the system._

**Acceptance Criteria:**
1. Admin can view a list of doctors
2. Admin can select and delete a doctor
3. System asks for confirmation before deletion
4. Doctor is removed from the database
   
**Priority:** Medium

**Story Points:** 3

**Notes:**
- Check for existing appointments before deletion
- Consider soft delete instead of permanent removal
- Maintain audit logs for deletions
 ____________________________________________________________________________________________________

 **View Appointment Statistics:**
_As an admin, I want to run a stored procedure in MySQL CLI to view the number of appointments per month, so that I can track system usage and trends._

**Acceptance Criteria:**
1. Stored procedure exists in the database
2. Admin can execute it via MySQL CLI
3. Output shows monthly appointment counts
4. Data is accurate and up-to-date
   
**Priority:** Medium

**Story Points:** 3

**Notes:**
- Ensure proper indexing for performance
- Handle cases with no appointment data
- Consider exposing this via dashboard instead of CLI in future

# Patient User Stories
**View Doctors Without Login:**
_As a patient, I want to view a list of doctors without logging in, so that I can explore options before registering._

**Acceptance Criteria:**
1. Patient can access doctor list without authentication
2. Doctor details (name, specialization, availability) are visible
3. No booking actions are allowed without login
   
**Priority:** Medium

**Story Points:** 3

**Notes:**
- Ensure sensitive doctor data is not exposed
- Optimize for fast loading (public endpoint)
 ____________________________________________________________________________________________________

 **Patient Sign Up:**
_As a patient, I want to sign up using my email and password, sso that I can book appointments._

**Acceptance Criteria:**
1. Patient can register with email and password
2. Email format is validated
3. Duplicate accounts are prevented
4. Account is created successfully
   
**Priority:** High

**Story Points:** 5

**Notes:**
- Implement email uniqueness constraint
- Consider email verification in future
- Store passwords securely
 ____________________________________________________________________________________________________

 **Patient Login:**
_As a patient, I want to log into the portal, so that I can manage my bookings._

**Acceptance Criteria:**
1. Patient can enter valid credentials
2. System authenticates successfully
3. Patient is redirected to dashboard
4. Error shown for invalid login
   
**Priority:** High

**Story Points:** 5

**Notes:**
- Role-based authentication required
- Handle session management securely
 ____________________________________________________________________________________________________

 **Patient Logout:**
_As a patient, I want to log out of the portal, so that I can secure my account._

**Acceptance Criteria:**
1. Patient can click logout
2. Session is invalidated
3. Redirected to login page
   
**Priority:** High

**Story Points:** 2

**Notes:**
- Clear authentication tokens/cookies
- Prevent unauthorized access after logout
 ____________________________________________________________________________________________________

 **Book Appointment:**
_As a patient, I want to log in and book an hour-long appointment with a doctor, so that I can receive consultation._

**Acceptance Criteria:**
1. Patient must be logged in to book
2. Patient can select doctor, date, and available time slot
3. Appointment duration is fixed to one hour
4. Booking is confirmed and stored in the system
   
**Priority:** High

**Story Points:** 8

**Notes:**
- Prevent double booking of the same slot
- Respect doctor availability and unavailability
- Consider confirmation notification (email/SMS)
 ____________________________________________________________________________________________________
 
 **View Upcoming Appointments:**
_As a patient, I want to view my upcoming appointments, so that I can prepare accordingly._

**Acceptance Criteria:**
1. Patient can see a list of upcoming appointments
2. Each appointment shows doctor, date, and time
3. Past appointments are separated or filtered
   
**Priority:** Medium

**Story Points:** 3

**Notes:**
- Sort appointments by date
- Consider adding reminders in future

# Doctor User Stories
**Doctor Login:**
_As a doctor, I want to log into the portal, so that I can manage my appointments._

**Acceptance Criteria:**
1. Doctor can enter valid credentials
2. System authenticates doctor role correctly
3. Doctor is redirected to their dashboard
4. Error message is shown for invalid login
   
**Priority:** High

**Story Points:** 5

**Notes:**
- Use role-based authentication (Doctor vs Admin)
- Implement secure password storage and session handling
 ____________________________________________________________________________________________________

**Doctor Logout:**
_As a doctor, I want to log out of the portal, so that I can protect my data._

**Acceptance Criteria:**
1. Doctor can click logout
2. Session is invalidated
3. Redirected to login page
   
**Priority:** High

**Story Points:** 2

**Notes:**
- Clear session/token securely
- Prevent back-button access after logout
 ____________________________________________________________________________________________________

 **View Appointment Calendar:**
_As a doctor, I want to view my appointment calendar, so that I can stay organized._

**Acceptance Criteria:**
1. Doctor can see all scheduled appointments
2. Appointments are displayed by date and time
3. Calendar view supports daily/weekly/monthly modes
   
**Priority:** High

**Story Points:** 5

**Notes:**
- Consider integrating a calendar UI
- Handle timezone differences if applicable
 ____________________________________________________________________________________________________

 **Mark Unavailability:**
_As a doctor, I want to mark my unavailability, so that patients can only book available time slots._

**Acceptance Criteria:**
1. Doctor can select date/time ranges as unavailable
2. System prevents booking during those slots
3. Changes reflect immediately in scheduling system
   
**Priority:** High

**Story Points:** 5

**Notes:**
- Handle overlapping availability/unavailability rules
- Consider recurring unavailability (e.g., weekends, holidays)
 ____________________________________________________________________________________________________

 **Update Profile:**
_As a doctor, I want to update my profile with specialization and contact information, so that patients have up-to-date information._

**Acceptance Criteria:**
1. Doctor can edit profile fields (specialization, contact info, etc.)
2. Changes are validated and saved
3. Updated information is visible to patients
   
**Priority:** Medium

**Story Points:** 3

**Notes:**
- Validate phone/email formats
- Consider audit tracking for profile updates
 ____________________________________________________________________________________________________

 **View Patient Details:**
_As a doctor, I want to view patient details for upcoming appointments, so that I can be prepared._

**Acceptance Criteria:**
1. Doctor can access patient information from appointment view
2. Relevant details (name, history, notes) are displayed
3. Access is limited to assigned patients only
   
**Priority:** High

**Story Points:** 5

**Notes:**
- Ensure data privacy and authorization controls
- Consider integration with patient medical records (if available)

