````markdown
# 💳 SecureBill – PayPal Business Integration

SecureBill is a lightweight, secure HTML-based PayPal payment form designed for businesses to accept credit cards and PayPal transactions online using PayPal’s official SDK.

---

## 🧭 Table of Contents

- [Features](#features)
- [Setting Up PayPal Business](#setting-up-paypal-business)
- [Getting Your Client ID](#getting-your-client-id)
- [Code Overview](#code-overview)
- [Deploying SecureBill](#deploying-securebill)
- [License](#license)

---

## ✅ Features

- Accepts PayPal and credit card payments
- Clean input formatting (`000.00`)
- Responsive and styled for desktops
- Fast integration with PayPal Buttons

---

## 💼 Setting Up PayPal Business

1. Visit [PayPal Business Signup](https://www.paypal.com/business)
2. Click **Get Started** and create a PayPal Business account.
3. Provide business and banking info.
4. Confirm your email and verify your account.

---

## 🔑 Getting Your PayPal Client ID

1. Go to [PayPal Developer Dashboard](https://developer.paypal.com/dashboard/applications)
2. Click **"Create App"** under **REST API Apps**.
3. Name your app (e.g., `SecureBill`) and select your business account.
4. Copy your **Client ID** from the app screen.
5. Replace `YOUR_CLIENT_ID` in the HTML script with your live Client ID when you're ready.

---

## 🧾 Code Overview

### 1. PayPal SDK Script

```html
<script src="https://www.paypal.com/sdk/js?client-id=YOUR_CLIENT_ID&components=buttons,funding-eligibility&currency=USD&enable-funding=card"></script>
````

* Loads PayPal SDK with support for PayPal + Card payments.
* `client-id` should be replaced with your Live or Sandbox ID.

---

### 2. Amount Input

```html
<input type="text" id="amount" placeholder="000.00" inputmode="numeric" oninput="formatCurrency(this)" maxlength="9">
```

* Accepts only numeric input.
* Automatically formats input into currency (`000.00`) as the user types.

---

### 3. formatCurrency() Function

```js
function formatCurrency(input) {
  const cleaned = input.value.replace(/\D/g, '');
  const number = parseInt(cleaned || '0', 10);
  const formatted = (number / 100).toFixed(2);
  input.value = formatted.padStart(6, '0');
}
```

* Removes all non-digits.
* Pads input with zeros.
* Divides by 100 to simulate cents.
* Ensures output like `005.75`, `000.99`, etc.

---

### 4. PayPal Buttons (Two Render Calls)

```js
paypal.Buttons({...}).render('#paypal-button-container');
```

* Rendered twice: one for `PayPal`, one for `Card`.
* `createOrder`: pulls amount from the formatted input.
* `onApprove`: shows a thank-you alert with payer's first name.

---

## 🚀 Deploying SecureBill

1. Save the full HTML file as `index.html`.
2. Upload to your secure web host (https preferred).
3. Replace the logo and client ID as needed.
4. Share the page with customers to receive payments.

---

## 📄 License

```
Copyright 2025 ShipWr3ck

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0
```

---

```
💬 Need help customizing SecureBill? Reach out at https://shipwr3ck.com
```


