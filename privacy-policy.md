# Work App Privacy & Data Protection Policy

_Last updated: December 19, 2024_

This Privacy & Data Protection Policy ("Policy") describes how the Work App platform collects, uses, stores, and shares information when you access the Flutter mobile applications, admin console, or web console (collectively, the "Service"). The project follows an offline-capable, Firebase-backed architecture with AI-assisted automation. Please read this Policy carefully to understand our practices.

## 1. Data Controller and Roles
- The managing organization (employer, contractor, or venue) that provisions accounts acts as the primary data controller.
- The Work App development team operates as a service provider / data processor, maintaining infrastructure and implementing security controls.

## 2. Information We Collect
### Account & Profile Data
- **Personal Information**: Name (first name, last name), email address, phone number, date of birth, role, company assignment, worker status, and profile photos (selfies with face detection) supplied during registration or created by administrators.
- **Address Information**: Full address and structured address components including area/city, street name, street number, and postal code (optional).
- **Additional Profile Data**: Emergency contact information (name, phone, relationship), skills, certifications, performance data (ratings, evaluations, performance history), and user preferences (app settings, notification preferences, display preferences).

### Operational Data
- **Attendance & Scheduling**: Check-in/out timestamps, shift assignments, schedule edits, attendance records, and finance-related entries.
- **Check-in/Check-out Photos**: Verification photos taken during check-in and check-out processes, stored in Firebase Storage and linked to attendance records.
- **Chat Content**: Message text content, sender and receiver IDs, timestamps, message status (sent, delivered, read), and chat thread metadata (participants, thread types, last message info, unread counts).
- **File Attachments**: Files shared through chat including images, documents, and other file types. Files are uploaded to Firebase Storage with associated metadata (file name, size, type, download URL). Full file attachments are stored, not just metadata.
- **Announcements**: Company announcements and notifications sent through the Service.

### Device & Technical Data
- Mobile device identifiers, OS version, localization settings, notification tokens, and network status required for offline sync.
- **Location Data**: Location coordinates with accuracy metrics, reverse-geocoded addresses, and timestamps used for geofencing, indoor positioning, check-in/check-out verification, and real-time location tracking during active work shifts (when enabled by policy).

### Document & Compliance Data
- **Worker Documents**: IDs, work authorizations, safety certifications, tax documents, and other compliance documents. Each document includes metadata such as document name, storage URL (Firebase Storage), expiry date, verification status (pending, verified, rejected, expired), verification timestamp, verified by (admin ID), and verification notes.
- **Company-Specific Requirements**: Document requirements with urgency levels (blocking vs non-blocking) that determine access to certain features or positions.

### Photo & Image Data
- **Profile Photos**: Selfie photos with face detection verification, stored in Firebase Storage at `worker_photos/` path.
- **Check-in/Check-out Photos**: Verification photos taken during attendance check-in and check-out, stored at `check_in_photos/` and `check_out_photos/` paths in Firebase Storage.
- **Company Photos**: Company logos and profile images, stored at `company_profiles/` path.
- **Company Contact Photos**: Contact person photos, stored at `company_contacts/` path.
- **Document Photos**: Photos of IDs, certificates, and work authorizations uploaded as part of document compliance.

### Analytics & AI Inputs
- Aggregated usage metrics, scheduling constraints, bottleneck indicators, and anomaly flags used for predictive alerts and automated reports (no LLM content is stored).

## 3. How We Use Information
- Provide role-specific experiences (worker environment, manager console, company modules).
- Authenticate users and enforce session security.
- Power offline-first operations, including caching, sync queues, and conflict resolution.
- Automate scheduling, attendance insights, document validation, and notification workflows using deterministic rules and specialized models (not large language models).
- Monitor system health, debug issues, and improve platform performance.
- Comply with legal or contractual obligations, including audit trails for HR or payroll records.

## 4. Legal Bases
Processing is based on one or more of the following:
- Performance of a contract between the managing organization and its workforce.
- Legitimate interests in coordinating field operations, safety, and payroll readiness.
- Compliance with labor, safety, or financial regulations.
- Consent for optional features such as photo verification with face detection or push notifications (collected within the mobile app settings where required).

**Note on Biometric Data**: The Service uses face detection technology (Google ML Kit) to verify the presence of a face in photos during registration and check-in processes. This is face detection, not face recognition—no biometric templates or face recognition data is stored. Face detection is performed locally on the device and is used only to verify that a valid photo contains a face. Only the photo itself is stored in Firebase Storage. Face detection is not used for identification or recognition purposes.

## 5. Data Sharing
- Firebase: authentication, database, storage, and messaging services hosted by Google.
- Cloud Functions / APIs: secure service endpoints required for syncing schedules, documents, and notifications.
- Third-party modules explicitly approved by the managing organization (e.g., map providers, payment processors). No data is sold or shared for advertising.

## 6. Offline Storage and Sync
- The mobile app stores relevant data in encrypted local containers (Hive/SQLite) to ensure continuity during connectivity loss.
- Pending actions are queued until a connection becomes available; after successful sync, local caches are trimmed according to retention rules.
- Users are informed of offline status via UI indicators; administrators may enforce minimum sync frequency.

## 7. Data Retention
- Operational records (attendance, schedule, finance) follow the managing organization’s retention policies, typically 3–7 years depending on jurisdiction.
- Application logs and debug traces are retained for up to 180 days unless longer storage is legally required.
- Cached mobile data is cleared when a worker loses active status or after 30 days of inactivity.

## 8. Security Measures
- End-to-end TLS encryption, Firebase security rules, role-based access control, and the unified TabManager to prevent unauthorized DOM manipulation.
- Background sync tasks include integrity checks, retry logic, and conflict detection.
- Access to administrative consoles requires multi-factor authentication if enabled by the organization.

## 9. Your Rights
Depending on your jurisdiction, you may request to:
- Access, correct, or update personal data.
- Object to processing or request deletion, subject to contractual and legal requirements.
- Export attendance or schedule records in a machine-readable format (JSON, CSV, or PDF). Export requests are typically processed within 30 days and delivered via secure email, download link, or secure file transfer as appropriate.
- File a complaint with the relevant data protection authority.
Requests should be directed to your organization's administrator, who will coordinate with the Work App support team if needed.

## 10. Children’s Privacy
The Service is not intended for individuals under 16 years of age. Accounts are provisioned only for authorized workers, managers, or company contacts.

## 11. International Transfers
- Data may be stored in Firebase regions selected by the managing organization. Cross-border transfers follow the data processing terms offered by the underlying cloud providers (e.g., Google Cloud Standard Contractual Clauses).

## 12. Changes to This Policy
- We may update this Policy as features evolve or regulatory requirements change. Material updates will be communicated through admin notifications or release notes, and the "Last updated" date will change accordingly.
- Continued use of the Service after an update signifies acceptance of the revised Policy.

## 13. Contact
- Primary contact: the managing organization's compliance or HR lead.
- Project contact: support@workapp.example for technical privacy inquiries, incident reporting, or data processing clarifications.
- Note: The contact email address above is a placeholder and will be updated with the actual contact information prior to production deployment.

## 14. Cookies and Tracking Technologies
- **Essential Cookies**: Required for authentication, session management, and core Service functionality. These cannot be disabled without impacting Service availability.
- **Functional Storage**: The mobile app uses local storage (Hive/SQLite) to enable offline functionality, cache user data, and maintain sync queues. This storage is encrypted and managed according to the retention policies outlined in Section 7.
- **Analytics**: Firebase Analytics may collect aggregated usage metrics, performance data, and error logs to improve Service reliability and user experience. This data is anonymized and does not identify individual users.
- **Third-Party Tracking**: The Service does not use third-party advertising trackers or sell data to advertising networks. Any third-party integrations (e.g., map providers) are explicitly approved by the managing organization and subject to their respective privacy policies.
- **User Controls**: You can manage notification preferences and location sharing through the mobile app settings. Local storage can be cleared by uninstalling the mobile app, though this will require re-syncing data upon reinstallation.

## 15. Data Breach Notification
- In the event of a security breach that may compromise your personal data, we will notify affected users and relevant data protection authorities within 72 hours of becoming aware of the breach, as required by applicable data protection laws (including GDPR).
- Notification methods may include email to registered addresses, in-app notifications, or announcements through the admin console, depending on the severity and scope of the breach.
- Breach notifications will include: (1) a description of the nature of the breach, (2) the categories and approximate number of affected individuals, (3) the likely consequences of the breach, and (4) measures taken or proposed to address the breach and mitigate its effects.
- The managing organization, as the primary data controller, is responsible for coordinating breach notifications with the Work App support team and ensuring compliance with all applicable notification requirements.

## 16. Right to Withdraw Consent
- You have the right to withdraw your consent for optional features at any time, including location tracking, photo verification with face detection, and push notifications.
- To withdraw consent, you can adjust settings within the mobile app (Settings > Privacy) or contact your organization's administrator to process the withdrawal request.
- Withdrawing consent for certain features may impact Service functionality. For example, disabling location services may prevent geofenced check-ins, disabling photo verification may prevent check-in/check-out processes that require photo verification, and disabling notifications may delay important schedule updates.
- Withdrawal requests are typically processed within 14 days. Once processed, the relevant data processing will cease, though data collected prior to withdrawal may be retained as required by law or contractual obligations (see Section 7 on Data Retention).

## 17. Automated Decision-Making
- The Service uses automated systems and AI-assisted features for scheduling optimization, attendance pattern analysis, predictive alerts, and automated reporting. These systems operate using deterministic rules and specialized models, not large language models that generate content.
- You have the right to request human review of any automated decision that significantly affects you, such as schedule assignments, performance evaluations, or compliance determinations.
- To request human review, contact your organization's administrator or use the "Request Review" option available in relevant Service modules. Human supervisors retain final authority over all operational decisions.
- You may opt out of certain automated features (e.g., AI-suggested schedule optimizations) through admin console settings, though core automated functions required for Service operation (e.g., sync, conflict resolution) cannot be disabled.
- Automated decisions are subject to audit trails and can be reviewed by authorized administrators. The Service maintains transparency by labeling AI-generated suggestions and allowing supervisors to override automated recommendations.

---

By installing or accessing the Work App you acknowledge that you have read and understood this Privacy & Data Protection Policy.

