# Task 3 - Integration Design

## End-to-End Architecture

When a patient submits the consultation form, the website first validates the entered name and phone number. After successful validation, the form data is sent to a backend API using an HTTPS POST request.

The backend checks whether a contact with the same phone number already exists in HubSpot. Since HubSpot uses email as the default unique identifier, a custom lookup by phone number is required before creating or updating the contact. If the phone number exists, the contact is updated; otherwise, a new contact is created. The contact includes Name, Phone Number, Clinic Preference, Lead Source as "Google Ads - Consultation Landing Page", and Lead Status as "New Enquiry".

After the contact is successfully stored in HubSpot, the backend triggers the Karix WhatsApp Business API to send a confirmation message to the patient. This message should be sent within two minutes of form submission.

At the same time, the backend records the `consultation_form_submitted` conversion event, allowing Google Ads to optimize campaigns based on completed consultation enquiries.

### Biggest Failure Point

The biggest failure point is the HubSpot contact creation or update process. If the HubSpot API is unavailable or returns an error, patient information could be lost.

To prevent this, every form submission should first be stored temporarily in a database or message queue. If HubSpot fails, an automatic retry mechanism should attempt the request again after a short interval while logging the failure for monitoring.

### WhatsApp SLA Monitoring

The two-minute WhatsApp delivery SLA could fail due to API downtime, network issues, or high server load. To monitor this, every message request should include timestamps for submission, API response, and delivery status. A monitoring dashboard and alerting system should notify the development team whenever message delivery exceeds the two-minute threshold.
