# QPass: A QR-Based Context-Aware Student Safety Monitoring and Emergency Alert System Using a Progressive Web Application

## Thesis Project Information

### Recommended Title
QPass: A QR-Based Context-Aware Student Safety Monitoring and Emergency Alert System Using a Progressive Web Application

### Alternative Title
QPass: A Progressive Web Application for Student Campus Movement Verification, Guardian Notification, and Emergency Response

## 1. Project Overview

QPass is a privacy-aware and context-aware Progressive Web Application (PWA) designed to improve student safety through secure QR-based campus movement verification, geofencing, guardian/parent SMS notifications, safety-status monitoring, scan anomaly detection, and location-based emergency alerts.

Students register their personal, guardian/parent, emergency, and medical information and receive a secure personal QR code. Campus Security Personnel generate a dynamic campus QR code for authorized entry and exit verification. The system validates each scan using the student account, QR validity, timestamp, geofence, and scan history.

When a student enters or exits the campus, the system records the transaction and notifies the registered Guardian/Parent through SMS. On exit, the student may provide a destination, reason, transportation type, and estimated arrival time. When commuting or going home is selected, the system activates Emergency Mode, which provides SOS and Mark as Safe functions.

QPass is not merely an attendance system. It is a student safety and emergency coordination platform. SOS location is a location snapshot captured when the button is pressed; QPass does not provide continuous real-time tracking.

## 2. Problem Statement

Traditional attendance and manual monitoring processes may not provide timely information about student entry, exit, destination, or emergencies. Guardians may not know when a student entered or left campus, while Campus Security Personnel may lack a unified dashboard for monitoring student status and responding to alerts.

QPass addresses delayed guardian notification, incomplete movement records, weak scan validation, difficulty identifying students during emergencies, limited emergency coordination, and lack of suspicious-scan monitoring through one integrated PWA.

## 3. Objectives

### General Objective

To develop a Progressive Web Application that improves student safety through secure QR-based campus entry and exit verification, geofence-based validation, Guardian/Parent SMS notifications, safety-status monitoring, and location-based emergency alerts.

### Specific Objectives

1. Allow students to create accounts and maintain personal, guardian, emergency, and medical information.
2. Generate a privacy-aware personal QR code for student identification.
3. Generate dynamic campus QR codes for entry and exit verification.
4. Validate scans using identity, QR validity, time, location, and scan history.
5. Use geofencing to identify scans inside or outside the authorized campus area.
6. Record verified entry and exit transactions.
7. Notify Guardians/Parents when students enter or exit campus.
8. Record destination, reason, transportation type, and estimated arrival time at exit.
9. Activate Emergency Mode for commuting or going home.
10. Send SOS alerts containing a location snapshot and Google Maps link.
11. Allow students to Mark as Safe.
12. Provide Campus Security Personnel with monitoring and alert-management tools.
13. Detect suspicious scans using rule-based anomaly detection.
14. Protect personal, medical, contact, and location information through role-based access control.
15. Maintain scan, notification, emergency, and audit logs.
16. Evaluate usability, accuracy, response time, reliability, security, privacy, and PWA performance.

## 4. System Users

### Student

Students can register, manage their profile, view their personal QR code, perform entry and exit scans, declare destinations, select transportation, activate Emergency Mode, send SOS alerts, Mark as Safe, and view their own records.

### Campus Security Personnel

Campus Security Personnel can generate dynamic campus QR codes, monitor entry and exit, verify student identity, view student statuses, manage emergency alerts, review suspicious scans, acknowledge and resolve incidents, and generate reports.

### Guardian/Parent

The Guardian/Parent primarily receives SMS notifications for entry, exit, SOS activation, Mark as Safe events, delayed arrivals, and other configured safety events. A future guardian portal may show only the linked student's information.

### Optional Administrator

An administrator may manage accounts, geofence settings, notification templates, system configuration, audit logs, and data-retention policies.

## 5. Personal Information and Privacy

Student information may include full name, student ID, photo, address, department/course, year level, cellphone number, Guardian/Parent name and cellphone number, emergency contacts, medical information, and account status.

The personal QR code must not expose the complete personal profile, home address, cellphone number, or medical information. It should contain a secure identifier, encrypted reference, or temporary token. An authorized scan retrieves only the information permitted for the scanning role.

| Information | Student | Campus Security Personnel | Guardian/Parent |
|---|---:|---:|---:|
| Full name | Yes | Yes | Yes |
| Student ID | Yes | Yes | Yes |
| Department/course | Yes | Yes | Optional |
| Home address | Yes | Restricted | No |
| Medical information | Yes | Authorized access only | As appropriate |
| SOS location | Yes | Yes | Yes through SMS |
| Entry/exit history | Own records | Yes | Notification only |

## 6. QR-Code Design

### Personal Student QR Code

The personal student QR code identifies a student using a secure identifier or token. It should support token validation, expiration or revocation, and role-controlled data retrieval. It should not contain sensitive personal or medical data in readable form.

### Dynamic Campus QR Code

The dynamic campus QR code is generated by Campus Security Personnel for an entrance or exit location. It may contain a campus identifier, location identifier, purpose, temporary token, creation time, expiration time, and digital signature.

The code should expire or change periodically to reduce screenshot reuse, copying, replay attacks, and unauthorized scans. The server must validate the token and transaction instead of trusting data supplied by the device.

## 7. Geofencing and Scan Validation

The system validates GPS coordinates, distance from the campus boundary, scan timestamp, QR expiration, student account status, previous transactions, device/session information, and scan frequency. GPS and geofencing are supporting controls and cannot guarantee physical presence because accuracy varies by device, building, network, and environmental conditions.

Possible scan classifications are:

- Valid scan
- Out-of-zone scan
- Expired QR-code scan
- Invalid token
- Repeated scan
- Unusual scan
- Possible location-spoofing attempt
- Pending synchronization
- Failed transaction

## 8. Student Safety Statuses

Recommended statuses are:

- Not Yet Entered
- Inside Campus
- Exited Campus
- Commuting
- Going Home
- Emergency Activated
- Alert Acknowledged
- Marked Safe
- Arrival Delayed
- Emergency Resolved
- Invalid/Suspicious Scan

## 9. Campus Entry Workflow

1. The student logs in to the QPass PWA.
2. The student scans the dynamic campus QR code.
3. The system validates identity, QR validity, time, location, geofence, and scan history.
4. The system records student identity, date, time, location, session/device information, and result.
5. The student status changes to Inside Campus.
6. The Guardian/Parent receives an entry SMS.
7. Campus Security Personnel view the transaction on the dashboard.

**Sample entry SMS:**

> QPass Notification: Your child, [Student Name], entered the campus on [Date] at [Time]. This is an automated safety notification.

## 10. Campus Exit Workflow

1. The student scans the dynamic campus QR code.
2. The system validates the transaction.
3. The student provides destination, reason for leaving, transportation type, and estimated arrival time.
4. The system records the exit.
5. The status changes to Exited Campus, Commuting, or Going Home.
6. If applicable, Emergency Mode is activated.
7. The Guardian/Parent receives an exit SMS.
8. Campus Security Personnel can view the declared travel information.

**Sample exit SMS:**

> QPass Notification: Your child, [Student Name], exited the campus on [Date] at [Time]. Destination: [Destination]. Transportation: [Transportation Type]. Expected arrival: [Time].

## 11. Emergency Mode

Emergency Mode is activated when the student selects commuting, going home, or another approved off-campus activity. It displays the student's safety status, SOS button, Mark as Safe button, destination, expected arrival time, emergency instructions, and last verified scan.

The system must clearly explain that the SOS location is a location snapshot, not continuous real-time tracking.

## 12. SOS Workflow

1. The student presses SOS.
2. The system displays a confirmation message and optional short countdown to prevent accidental activation.
3. The student may cancel during the countdown.
4. The system captures the device location at activation time.
5. An emergency record is created and the status changes to Emergency Activated.
6. Campus Security Personnel receive a dashboard alert and SMS.
7. The Guardian/Parent receives an emergency SMS containing a Google Maps location link.
8. Authorized security personnel acknowledge, investigate, respond, and resolve the alert.
9. The student may use Mark as Safe after the situation is resolved.

The alert may include student name, ID, alert time, location snapshot, Google Maps link, destination, transportation, expected arrival, last scan, authorized medical information, priority, and acknowledgment status.

**Sample Guardian/Parent SOS SMS:**

> QPass EMERGENCY ALERT: [Student Name] activated an SOS alert on [Date] at [Time]. Last recorded location: [Google Maps Link]. Please contact Campus Security Personnel immediately.

**Sample security SMS:**

> QPass SECURITY ALERT: Student [Name], ID [Student ID], activated an SOS alert at [Time]. Location: [Google Maps Link]. Check the QPass dashboard for details.

## 13. Mark as Safe

The student confirms safety using account authentication, a confirmation prompt, PIN, or another approved verification method. The system records the time, updates the status to Marked Safe, informs Campus Security Personnel, and sends the Guardian/Parent a notification.

**Sample SMS:**

> QPass Update: [Student Name] has marked themselves as safe on [Date] at [Time].

## 14. Safety Check-In and Expected Arrival

At exit, the student may provide an expected arrival time. If the student has not marked themselves safe after that time, the system can send a reminder, change the status to Arrival Delayed, warn Campus Security Personnel, and notify the Guardian/Parent according to institutional policy.

## 15. Rule-Based Scan Anomaly Detection

The system may flag scans outside the geofence, expired codes, rapid repeated scans, entry without exit, exit without entry, one QR code used on multiple devices, one device scanning many accounts unusually quickly, implausible location changes, and attempts to bypass required destination information.

An anomaly is a warning for authorized review and does not automatically prove misconduct.

## 16. Campus Security Personnel Dashboard

### Overview

The dashboard can show registered students, students inside campus, exited students, commuters, students going home, active emergencies, unresolved alerts, suspicious scans, and delayed safety check-ins.

### Student Monitoring

The dashboard can show student name, ID, current status, last scan, entry and exit times, destination, expected arrival, and emergency status.

### QR Management

Campus Security Personnel can generate, expire, enable, disable, and review dynamic campus QR codes and invalid scan attempts.

### Emergency Management

Personnel can view locations, acknowledge alerts, assign priority, add notes, update response status, and mark alerts resolved.

### Reports

Reports may include daily entry/exit records, students currently inside, emergency alerts, suspicious scans, SMS logs, safety check-ins, and average acknowledgment time.

## 17. Notification Management

The notification log should include recipient, type, message, timestamp, delivery status, retry status, linked student, and linked transaction or emergency event.

Statuses may be Pending, Sent, Delivered, Failed, Retrying, and Expired. The system should only report Delivered when the SMS provider returns a delivery status.

## 18. Role-Based Access Control

Students may access their own information and actions. Campus Security Personnel may access authorized verification, monitoring, emergency, and reporting information. Guardians/Parents may receive notifications and, if a portal is implemented, see only linked student records. Administrators may manage configuration and audit records.

## 19. Data Security and Privacy

Required controls include password hashing, HTTPS, secure authentication, role-based access, session expiration, login-attempt restrictions, input validation, QR-token validation, audit logs, restricted medical/address access, secure backups, consent for notifications, and data-retention/deletion rules. The system must comply with applicable privacy laws, school policies, and institutional data-protection requirements.

## 20. Progressive Web Application Features

QPass should be installable on supported mobile devices, responsive, camera-enabled for QR scanning, supported by a service worker, and usable across modern browsers. It may cache basic interface resources and emergency instructions and synchronize pending data when connectivity returns.

The interface must clearly show Waiting for Connection, Pending Synchronization, Successfully Synchronized, Verification Failed, and Retry Required. It must never falsely display an offline scan as server-verified. Emergency transmission should provide clear feedback when the network is unavailable.

## 21. Functional Requirements

1. Student registration and secure login.
2. Profile, Guardian/Parent, emergency, and medical information management.
3. Personal QR generation and revocation.
4. Dynamic campus QR generation and expiration.
5. Identity, token, timestamp, geofence, and scan-history validation.
6. Entry and exit recording.
7. Destination, reason, transportation, and expected-arrival capture.
8. Guardian/Parent entry and exit SMS.
9. Emergency Mode, SOS, location snapshot, and Mark as Safe.
10. Google Maps emergency link generation.
11. Dashboard alert acknowledgment and resolution.
12. Scan anomaly detection.
13. Safety check-in monitoring.
14. Notification, audit, scan, and emergency logs.
15. Reports and PWA access.

## 22. Nonfunctional Requirements

- **Usability:** Simple and understandable for all roles.
- **Performance:** Fast verification and dashboard response under normal conditions.
- **Reliability:** Preserve records and retry failed notifications appropriately.
- **Security:** Protect accounts, tokens, personal data, medical information, and emergency records.
- **Availability:** Accessible through supported browsers and devices.
- **Scalability:** Support growth in users and transactions.
- **Maintainability:** Modular code and documented components.
- **Compatibility:** Modern mobile and desktop browsers.
- **Privacy:** Minimize data exposure and apply least-privilege access.

## 23. Suggested Database Entities

- Users
- Students
- Campus Security Personnel
- Guardians
- Student-Guardian Relationships
- Personal QR Codes
- Campus QR Codes
- Campus Locations
- Entry Records
- Exit Records
- Destinations
- Transportation Types
- Safety Statuses
- Emergency Alerts
- Emergency Responses
- Notifications
- Notification Logs
- Scan Logs
- Scan Anomalies
- Medical Information
- Audit Logs
- System Settings

One student may have multiple entry, exit, scan, and emergency records. Guardians may be linked to one or more students. Each transaction or emergency event may generate notification records. An anomaly is linked to the scan that triggered it.

## 24. Scope

The scope includes student registration, personal and dynamic campus QR codes, entry and exit verification, geofencing, destination and transportation declaration, Guardian/Parent SMS, Campus Security Personnel dashboard, Emergency Mode, SOS location snapshot, Google Maps link, Mark as Safe, anomaly detection, safety check-in, PWA behavior, logs, and reports.

## 25. Exclusions and Limitations

The initial system does not provide continuous real-time tracking, automatic police or emergency-service dispatch, facial recognition, biometric identity verification, guaranteed GPS accuracy, guaranteed SMS delivery, automatic determination that a student is safe, medical diagnosis, direct gate control, or guaranteed success during network outages. It also cannot prevent a student from entering inaccurate destination information. These may be future enhancements.

## 26. Research Novelty and Contribution

QPass integrates secure QR-based campus movement verification, geofence-based validation, Guardian/Parent SMS notification, safety-status monitoring, rule-based scan anomaly detection, expected-arrival monitoring, privacy-controlled student information, and location-based emergency alerts in one PWA. Its contribution is a privacy-aware, context-aware student safety and emergency coordination platform rather than a basic attendance system.

## 27. Evaluation Criteria

Evaluate the system using:

- QR verification accuracy
- Geofence validation accuracy
- Entry, exit, SOS, and Mark as Safe processing time
- SMS sending and delivery success rate
- Emergency alert acknowledgment and resolution time
- Rule-based anomaly detection accuracy
- Usability and user satisfaction
- Security and privacy controls
- PWA loading, responsiveness, installability, offline behavior, synchronization, and browser compatibility

## 28. Suggested Use Cases

1. Student Registration
2. Personal QR Generation
3. Dynamic Campus QR Generation
4. Campus Entry
5. Campus Exit
6. Guardian/Parent Notification
7. SOS Activation
8. Emergency Response
9. Mark as Safe
10. Suspicious Scan Review
11. Delayed Arrival Monitoring

## 29. Final System Description

QPass is a Progressive Web Application designed to enhance student safety through secure QR-based campus movement verification and emergency communication. Students register personal, Guardian/Parent, emergency, and medical information and receive a secure personal QR code. Dynamic campus QR codes are used for entry and exit verification while geofencing, QR expiration, timestamps, and scan history help identify invalid or suspicious scans. The system sends SMS notifications when students enter or leave campus. During exit, students may declare their destination, transportation type, and expected arrival time. When commuting or going home is selected, Emergency Mode provides SOS and Mark as Safe functions. An SOS captures a location snapshot at activation and sends a Google Maps link to Campus Security Personnel and the Guardian/Parent. The system provides safety-status monitoring, anomaly detection, emergency management, privacy controls, and reports. QPass does not provide continuous real-time tracking; it records verified movement events and emergency location snapshots. It is a privacy-aware and context-aware student safety platform, not merely an attendance system.

## 30. Recommended Abstract

Student safety is an important concern for educational institutions, particularly when students travel to and from campus. Traditional attendance and monitoring systems may provide limited information about student movement and may not immediately notify Guardians/Parents during campus entry, exit, or emergency situations. This study proposes QPass, a QR-based context-aware student safety monitoring and emergency alert system implemented as a Progressive Web Application. The system enables students to register personal, Guardian/Parent, emergency, and medical information and receive a secure personal QR code. Dynamic campus QR codes are used for entry and exit verification while geofencing, QR expiration, timestamp validation, and scan-history analysis help detect invalid or suspicious scanning activities. The system sends SMS notifications when students enter or leave campus. During exit, students may declare their destination, transportation type, and expected arrival time. When commuting or going home is selected, Emergency Mode provides an SOS feature that captures a location snapshot at activation and sends an emergency notification containing a Google Maps link to Campus Security Personnel and the Guardian/Parent. The system also provides Mark as Safe, safety-status monitoring, scan anomaly detection, emergency alert management, and safety check-in monitoring. QPass aims to support faster communication, improve campus monitoring, protect sensitive student information, and organize emergency response. The system will be evaluated based on QR verification accuracy, geofence validation, SMS success, emergency response time, anomaly detection, usability, security, privacy, reliability, and PWA performance.
