# Case Study: Webinar Registration Funnel — GoHighLevel

**Role:** Sole builder (funnel design, automation workflow, custom variables, branch logic)  
**Stack:** GoHighLevel (GHL), Email, SMS, Custom Values, Workflow Automation

---

## The problem

Service businesses running webinars — coaches, consultants, agencies — typically manage registration, reminders, and follow-ups manually or with disconnected tools. The result: registrants fall through the cracks, no-shows never get a replay link, and attendees never get a timely follow-up offer. Every webinar cycle requires the same manual work.

The ask: a fully automated webinar funnel that handles registration to post-webinar follow-up without manual intervention, and is reusable for any future webinar without rebuilding from scratch.

---

## What was built

A complete end-to-end webinar funnel in GoHighLevel:

**Funnel pages (3 steps):**
1. Landing page with headline, value proposition, and 3 CTA buttons
2. Registration page with form (First Name, Last Name, Email, Phone)
3. Thank You page with confirmation message

**Automation workflow:**
1. Trigger: Contact Created (fires on form submission)
2. Confirmation email + SMS sent immediately on registration
3. Wait 5 days → 24-hour reminder email
4. Wait 23 hours → 1-hour reminder email
5. Wait 2 hours → If/Else split:
   - **Attended branch:** follow-up email with next step / offer
   - **No-show branch:** replay link email

**Custom Values (dynamic variables):**
- `{{custom_values.webinar_date}}` — webinar date
- `{{custom_values.webinar_time}}` — webinar time  
- `{{custom_values.webinar_link}}` — join/replay link

Updating these three values updates all emails in the workflow automatically — no editing individual steps per webinar cycle.

---

## Design decisions worth noting

### Relative waits over fixed dates
The workflow uses duration-based waits (5 days, 23 hours, 2 hours) instead of hardcoded dates. This makes the funnel reusable — launch it for any webinar date and the timing chain adjusts automatically per registrant. Fixed dates would require editing the workflow for every new webinar.

### Custom Values for all dynamic content
All webinar-specific content (date, time, join link) is managed through GHL's Custom Values system rather than hardcoded in each email. One update propagates across the entire workflow.

### Tag-based attended/no-show split
The post-webinar branch checks for the `attended-webinar` tag. In production, this tag is applied via GHL's Zoom integration after the session ends. For clients using other platforms (WebinarJam, Demio), the same tag can be applied via a Zapier or Make.com webhook post-webinar. The automation logic is platform-agnostic — only the tag source changes.

### Contact Created as workflow trigger
GHL's Form Submitted trigger does not surface funnel-embedded forms directly. Using Contact Created as the trigger achieves the same result — every new registrant enters the workflow — while remaining reliable across GHL's funnel builder versions.

---

## Result

A fully automated webinar funnel: registration → confirmation → reminders → attended/no-show split → follow-up. Zero manual steps from registration to post-webinar follow-up. Reusable for any future webinar by updating 3 custom values and publishing.

📹 [Watch workflow walkthrough](./screenshots/workflow-demo.mp4)

---

## Honest gaps

- **No live Zoom integration:** the attended/no-show split requires a webinar platform integration to tag attendees. Documented as a design note in the workflow — straightforward to wire up with GHL's native Zoom connector.
- **No payment step:** the follow-up offer link is a placeholder. A production funnel would connect to a GHL order form or external payment link (Stripe, ThriveCart).
- **No A/B testing:** email subject lines and copy are single variants. A production engagement would run split tests on subject lines and CTA copy.

---

*Built as a portfolio demonstration of GoHighLevel funnel and automation capabilities.*
