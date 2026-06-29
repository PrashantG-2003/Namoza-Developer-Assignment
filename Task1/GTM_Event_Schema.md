# Task 1 - GTM Event Schema

## Project

(Client introduction)

---

## GTM Event Schema

| Event Name | Trigger Type | Key Parameters | GA4 Report / Audience |
|------------|--------------|----------------|------------------------|
| ... your complete table ... |

---

# Booking Form dataLayer Push Events

## Step 1

```javascript
window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 1,
  step_name: "location_specialty_selected",
  clinic_location: "Bengaluru",
  specialty: "Knee Pain"
});
```

## Step 2

```javascript
window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 2,
  step_name: "patient_details_entered",
  patient_name: "Rahul Sharma",
  phone_number: "9876543210",
  preferred_date: "2026-07-15"
});
```

## Step 3

```javascript
window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 3,
  step_name: "booking_confirmed",
  clinic_location: "Bengaluru",
  specialty: "Knee Pain",
  booking_status: "Confirmed"
});
```

---

# Funnel Drop-off Tracking

Each booking step sends a separate `booking_step_complete` event with a different `step_number`.

The GTM Custom Event trigger listens for `booking_step_complete` and forwards the event to GA4.

In GA4 Funnel Exploration, define the funnel as:

**Step 1:** `booking_step_complete` where `step_number = 1`

↓

**Step 2:** `booking_step_complete` where `step_number = 2`

↓

**Step 3:** `booking_step_complete` where `step_number = 3`

↓

**Final Conversion:** `consultation_form_submitted`

Using this funnel, GA4 automatically shows how many users move from one step to the next and exactly where users abandon the booking process. This helps identify which booking step needs improvement.

---

# Google Ads Conversion

**Selected Conversion:** `consultation_form_submitted`

Reason:
This event represents a completed consultation enquiry, making it the most valuable conversion for optimizing Google Ads campaigns.