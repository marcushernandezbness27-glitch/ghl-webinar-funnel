# GHL Webinar Registration Funnel

End-to-end webinar funnel built in GoHighLevel — registration, automated reminders, and post-webinar attended/no-show split.

## Demo

📹 [Watch workflow walkthrough video](./test.mp4)

## Funnel Structure

| Step | Page | Purpose |
|---|---|---|
| 1 | Landing Page | Value proposition + 3 CTA buttons |
| 2 | Registration | Form capture (name, email, phone) |
| 3 | Thank You | Confirmation message |

## Automation Workflow

```
Contact Created (form submit)
  → Confirmation Email + SMS
  → Wait 5 days
  → 24hr Reminder Email
  → Wait 23 hours
  → 1hr Reminder Email
  → Wait 2 hours
  → If/Else: tag "attended-webinar"
      ├── YES → Follow-up offer email
      └── NO  → Replay link email
```

## Custom Values (dynamic variables)

| Variable | Used in |
|---|---|
| `{{custom_values.webinar_date}}` | All reminder emails |
| `{{custom_values.webinar_time}}` | All reminder emails |
| `{{custom_values.webinar_link}}` | Reminder + replay emails |

Update these once in GHL Settings → Custom Values to update all emails automatically.

## Stack

`GoHighLevel` `Email Automation` `SMS` `Workflow Builder` `Custom Values`

## Screenshots & Recording

See `screenshots/` folder for:
- Funnel steps overview
- Landing page design
- Full workflow map
- Branch split (attended vs no-show)
- Custom Values configuration
- Test contact workflow history
- Workflow walkthrough video (MP4)
