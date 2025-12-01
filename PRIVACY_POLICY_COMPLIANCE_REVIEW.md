# Privacy Policy Compliance Review

_Generated: December 19, 2024_

## Executive Summary

This document compares what the Work App project **actually collects** versus what is stated in the Privacy Policy. Several gaps and inaccuracies were identified that need to be addressed.

**Overall Assessment: ⚠️ PARTIALLY COMPLIANT**

The privacy policy covers most data collection but is missing several specific data types and details that are actually collected by the system.

---

## 1. Chat Data Collection

### What Privacy Policy Says:
> "Chat content, announcements, and file-sharing metadata (file name, size, type)."

### What Project Actually Collects:

**✅ Covered:**
- Chat message text content
- Sender ID, receiver ID
- Timestamps
- Message status (sent, delivered, read)

**❌ Missing/Incomplete:**
- **File attachments**: The policy mentions "file-sharing metadata" but the system actually stores:
  - `attachmentUrl` - Full URL to uploaded files in Firebase Storage
  - `attachmentName` - File name
  - `attachmentType` - File MIME type
  - **Actual files are stored**, not just metadata
- **Chat threads**: Thread metadata including:
  - Participants list
  - Thread type (direct, group, company)
  - Last message preview
  - Unread counts
  - Thread creation/update timestamps

**Recommendation:**
Update Section 2 (Operational Data) to clarify:
- "Chat content, message metadata, and file attachments (including file URLs, names, and types stored in Firebase Storage)."
- Add mention of chat thread metadata collection.

---

## 2. Photo/Image Collection

### What Privacy Policy Says:
> "Profile photos supplied during registration or created by administrators."

### What Project Actually Collects:

**✅ Covered:**
- Profile photos (selfies with face detection)

**❌ Missing:**
- **Check-in photos**: Stored in `check_in_photos/` Firebase Storage path
  - Collected during worker check-in
  - Linked to attendance records
  - Used for verification
- **Check-out photos**: Stored in `check_out_photos/` Firebase Storage path
  - Collected during worker check-out
  - Linked to attendance records
- **Company profile photos**: Company logos and profile images
- **Company contact photos**: Contact person photos
- **Document photos**: Photos of IDs, certificates, work authorizations

**Code Evidence:**
- `mobile/lib/services/check_in_out_service.dart`: Lines 59-66, 88, 140-164
- `storage.rules`: Lines 49-51 (attendance photos)
- `mobile/lib/screens/worker_profile_completion_screen.dart`: Lines 902-920 (selfie upload)

**Recommendation:**
Update Section 2 (Account & Profile Data) to include:
- "Profile photos (selfies with face detection), check-in/check-out verification photos, company logos, and document photos (IDs, certificates, work authorizations)."

---

## 3. User Profile Data Collection

### What Privacy Policy Says:
> "Name, email, phone, role, company assignment, worker status, and profile photos..."

### What Project Actually Collects:

**✅ Covered:**
- Name (firstName, lastName)
- Email
- Phone
- Role
- Company assignment
- Worker status
- Profile photos

**❌ Missing:**
- **Date of Birth**: Required field collected during registration
  - Used for age verification (minimum 16 years)
  - Stored as `dateOfBirth` timestamp
- **Structured Address Components**: 
  - `addressComponents.area` (city/area)
  - `addressComponents.street` (street name)
  - `addressComponents.number` (street number)
  - `addressComponents.postalCode` (optional)
  - Full address string also stored
- **Emergency Contact Information**:
  - Emergency contact name
  - Emergency contact phone
  - Relationship to worker
- **Skills**: Array of worker skills
- **Performance Data**: Performance ratings, evaluations
- **Preferences**: User preferences and settings
- **Location Data**: 
  - Current location coordinates
  - Check-in/check-out locations with addresses
  - Location accuracy metrics

**Code Evidence:**
- `WORKAPP/WORKER_REGISTRATION_REQUIREMENTS.md`: Lines 71-80 (date of birth requirement)
- `mobile/lib/models/worker_model.dart`: Lines 18, 26, 139 (locationData, emergencyContact, skills, performanceData, preferences)
- `mobile/lib/screens/worker_profile_completion_screen.dart`: Lines 207-213 (address components)

**Recommendation:**
Update Section 2 (Account & Profile Data) to include:
- "Name, email, phone, date of birth, structured address (area, street, number, postal code), role, company assignment, worker status, profile photos, emergency contact information, skills, performance data, and user preferences."

---

## 4. Location Data Collection

### What Privacy Policy Says:
> "Location coordinates and sensor data used for geofencing, indoor positioning, and check-in verification (when enabled by policy)."

### What Project Actually Collects:

**✅ Covered:**
- Location coordinates
- Geofencing data
- Check-in verification location

**❌ Missing Details:**
- **Check-in location data structure**:
  - `checkInLocation.latitude`
  - `checkInLocation.longitude`
  - `checkInLocation.address` (reverse geocoded)
  - `checkInLocation.accuracy` (meters)
  - `checkInTimestamp`
- **Check-out location data** (same structure)
- **Current location tracking**: Real-time location updates during work shifts
- **Location accuracy requirements**: System enforces minimum accuracy thresholds

**Code Evidence:**
- `mobile/lib/services/check_in_out_service.dart`: Lines 68-77 (location data structure)
- `docs/database_design.md`: Lines 89-100 (attendance location structure)

**Recommendation:**
The policy is mostly accurate but could be more specific. Consider adding:
- "Location coordinates with accuracy metrics, reverse-geocoded addresses, and timestamps for check-in/check-out verification and real-time location tracking during active work shifts."

---

## 5. Document Collection

### What Privacy Policy Says:
> "Worker documents, IDs, certificates, and company-specific requirements (blocking vs non-blocking) with verification status."

### What Project Actually Collects:

**✅ Covered:**
- Worker documents
- IDs
- Certificates
- Verification status

**❌ Missing Details:**
- **Document types explicitly collected**:
  - ID documents
  - Work authorization documents
  - Safety certifications
  - Tax documents
- **Document metadata**:
  - Document name
  - Document URL (Firebase Storage)
  - Expiry dates
  - Verification status (pending, verified, rejected, expired)
  - Verified by (admin ID)
  - Verification timestamp
  - Notes/rejection reasons
- **Document requirements**: Company-specific document requirements with urgency levels (blocking vs non-blocking)

**Code Evidence:**
- `docs/database_design.md`: Lines 151-168 (documents collection structure)
- `mobile/lib/models/worker_model.dart`: Lines 21-22 (documents, documentRequirements)

**Recommendation:**
The policy is accurate but could be more specific. Consider expanding to:
- "Worker documents including IDs, work authorizations, safety certifications, and tax documents. Each document includes metadata such as name, storage URL, expiry date, verification status, verification timestamp, and verification notes. Company-specific document requirements with urgency levels (blocking vs non-blocking) are also stored."

---

## 6. Biometric Data Collection

### What Privacy Policy Says:
> "Consent for optional features such as biometric photo verification or push notifications..."

### What Project Actually Collects:

**✅ Covered:**
- Biometric photo verification (face detection)

**⚠️ Clarification Needed:**
- The system uses **face detection** (not face recognition/biometric templates)
- Google ML Kit Face Detection is used to verify a face is present in photos
- **No biometric templates or face recognition data is stored**
- Only the photo itself is stored (as profile photo or check-in photo)

**Code Evidence:**
- `mobile/lib/widgets/face_detection_camera.dart`: Uses Google ML Kit for face detection
- `mobile/pubspec.yaml`: Line 62 (google_mlkit_face_detection dependency)

**Recommendation:**
Clarify in Section 4 (Legal Bases) and Section 16 (Right to Withdraw Consent):
- "Biometric photo verification uses face detection technology (Google ML Kit) to verify the presence of a face in photos. No biometric templates or face recognition data is stored—only the photo itself. Face detection is performed locally on the device and is not used for identification or recognition purposes."

---

## 7. Chat File Attachments

### What Privacy Policy Says:
> "File-sharing metadata (file name, size, type)."

### What Project Actually Collects:

**❌ Incomplete:**
- The system stores **full file attachments**, not just metadata
- Files are uploaded to Firebase Storage
- Storage paths: `messages/{messageId}/{fileName}`
- Full download URLs are stored in chat messages
- File types supported: images, documents, potentially other file types

**Code Evidence:**
- `mobile/lib/models/chat_message.dart`: Lines 10-12, 35-37, 48-50 (attachmentUrl, attachmentName, attachmentType)
- `mobile/lib/services/chat_service.dart`: Lines 551-554, 583-585 (attachment handling)
- `storage.rules`: Lines 44-47 (message attachments storage rules)

**Recommendation:**
Update Section 2 (Operational Data):
- Change "file-sharing metadata" to "file attachments including file URLs, names, types, and sizes. Files are stored in Firebase Storage and linked to chat messages."

---

## 8. Missing Data Categories

### Not Mentioned in Privacy Policy:

1. **Emergency Contact Information**
   - Name, phone, relationship
   - Stored in worker profile

2. **Skills and Certifications**
   - Array of skills
   - Certifications list

3. **Performance Data**
   - Performance ratings
   - Evaluation data
   - Performance history

4. **User Preferences**
   - App settings
   - Notification preferences
   - Display preferences

5. **Chat Thread Metadata**
   - Thread participants
   - Thread types
   - Last message info
   - Unread counts

**Recommendation:**
Add a new subsection under Section 2:
- "Additional Profile Data: Emergency contact information, skills, certifications, performance data, and user preferences."

---

## Summary of Required Updates

### High Priority (Missing Critical Information):

1. **Section 2 - Account & Profile Data:**
   - Add: Date of birth, structured address components, emergency contact, skills, performance data, preferences
   - Expand: Profile photos to include check-in/check-out photos, company photos, document photos

2. **Section 2 - Operational Data:**
   - Clarify: Chat file attachments are stored (not just metadata)
   - Add: Chat thread metadata collection

3. **Section 4 - Legal Bases:**
   - Clarify: Face detection vs biometric templates (no templates stored)

4. **New Section or Subsection:**
   - Add: Emergency contact, skills, performance data, preferences

### Medium Priority (Clarifications):

1. **Section 2 - Device & Technical Data:**
   - Expand: Location data details (accuracy metrics, reverse geocoding, real-time tracking)

2. **Section 2 - Document & Compliance Data:**
   - Expand: Document metadata details (expiry dates, verification workflow)

---

## Compliance Status

| Category | Status | Notes |
|----------|--------|-------|
| Chat Content | ⚠️ Partial | Missing file attachment details |
| Photos | ❌ Incomplete | Missing check-in/out photos, company photos |
| Profile Data | ⚠️ Partial | Missing DOB, address structure, emergency contact, skills, performance |
| Location Data | ✅ Mostly OK | Could be more specific |
| Documents | ✅ Mostly OK | Could include more metadata details |
| Biometric | ⚠️ Needs Clarification | Should clarify face detection vs recognition |
| File Attachments | ❌ Incomplete | Says "metadata" but stores full files |

**Overall: 4/7 categories fully compliant, 3/7 need updates**

---

## Recommended Action Items

1. ✅ Update Privacy Policy Section 2 with all missing data types
2. ✅ Clarify biometric data collection (face detection only)
3. ✅ Update chat/file attachment language
4. ✅ Add emergency contact, skills, performance data to policy
5. ✅ Expand photo collection description
6. ✅ Review and update after implementation

---

## Notes

- All data collection identified in this review is legitimate and necessary for the Service functionality
- No unauthorized or unnecessary data collection was found
- The gaps are primarily about **completeness and specificity** rather than compliance violations
- Once updated, the privacy policy will accurately reflect all data collection practices

