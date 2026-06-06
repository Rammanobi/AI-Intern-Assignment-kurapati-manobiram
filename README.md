# Part C — Student Lead Capture Form (n8n Webhook Integration)

A fully client-side **Student Lead Capture Form** built with pure HTML, CSS, and Vanilla JavaScript. On submission, form data is posted to an **n8n webhook** that triggers an automated lead-notification workflow.

---

## 📋 Features

### Form Fields
| Field | Type | Validation |
|-------|------|------------|
| Full Name | Text input | Required, min 3 characters |
| Email Address | Email input | Required, valid email format |
| Country | Dropdown (dynamic) | Required, populated via JS |
| Course Level | Radio buttons (UG / PG / PhD) | Required |
| Preferred University | Text input | Required, min 3 characters |
| Message | Textarea | Required, max 300 characters |

### Validation
- ✅ **Real-time inline validation** — errors clear as the user corrects input
- ✅ **On-blur validation** — checks fields when focus leaves each input
- ✅ **Full-form validation on submit** — all fields validated before sending
- ✅ **Auto-scroll & focus** — scrolls to and focuses the first invalid field
- ✅ **Character counter** — live `0 / 300` counter for the message textarea

### UX & Accessibility
- ✅ **Error toast notification** — visible dismissable error above submit button on webhook failure
- ✅ **Loading state** — spinner on submit button while awaiting webhook response
- ✅ **Success state** — animated success card replaces the form on HTTP 200
- ✅ **ARIA attributes** — `aria-required`, `aria-describedby`, `aria-live`, `role="alert"` throughout
- ✅ **Reduced motion support** — `prefers-reduced-motion` media query disables animations
- ✅ **Keyboard accessible** — all interactions work without a mouse

### Design
- 🎨 **Inter font** from Google Fonts
- 🎨 **8-point spacing grid** via CSS custom properties
- 🎨 **Blue gradient hero header** (`#2563eb` → `#1e40af`)
- 🎨 **Glassmorphism-style form card** with subtle shadow and hover lift
- 📱 **Responsive layout** — single-column on mobile, two-column grid on desktop

---

## 🔗 n8n Webhook Integration

Form data is submitted as a **JSON POST** to the configured n8n webhook endpoint.

### Webhook Endpoint
```
POST https://n8n.srv1304884.hstgr.cloud/webhook/9b8fa142-ff2e-41b1-8d04-64fbd2e8d76f
Content-Type: application/json
```

### Payload Structure
```json
{
  "fullName": "Jane Doe",
  "email": "jane@example.com",
  "country": "India",
  "courseLevel": "PG",
  "preferredUniversity": "University of Melbourne",
  "message": "I am interested in a Masters in Computer Science..."
}
```

### Response Handling
| HTTP Status | Behaviour |
|-------------|-----------|
| `200 OK` | Hides form, shows animated success card |
| Any other status | Shows error toast with status code, resets button to "Try Again" |
| Network error | Shows error toast with connectivity message |

---

## 🗂️ File Structure

```
part-c/
└── index.html        # Single self-contained file (HTML + CSS + JS)
```

> All styles and scripts are embedded inline — no external dependencies beyond Google Fonts.

---

## 🚀 How to Run

No build step required. Simply open in a browser:

```bash
# Option 1 — Open directly
open part-c/index.html

# Option 2 — Serve locally (recommended to avoid CORS on webhook)
npx serve part-c
# then visit http://localhost:3000
```

---

## ⚙️ Configuration

To point the form at a different webhook, update the constant at the top of the `<script>` block in `index.html`:

```js
var WEBHOOK_URL = 'https://your-n8n-instance/webhook/your-id-here';
```

---

## 🧱 Tech Stack

| Layer | Technology |
|-------|-----------|
| Markup | Semantic HTML5 |
| Styling | Vanilla CSS (CSS custom properties, Grid, Flexbox) |
| Logic | Vanilla JavaScript (ES2017 async/await) |
| Font | Inter — Google Fonts |
| Automation | n8n webhook (external) |

---

## ♿ Accessibility

- All form controls have associated `<label>` elements
- Error messages use `role="alert"` and `aria-live="polite"` for screen readers
- Success card uses `aria-live="assertive"` for immediate announcement
- Radio group uses `role="radiogroup"` with `aria-label`
- Submit button communicates loading/success states via text content

---

© 2026 Student Admissions Portal
