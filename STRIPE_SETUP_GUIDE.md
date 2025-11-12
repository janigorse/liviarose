# Stripe Checkout Setup Guide for LiviaRose

This guide will help you set up Stripe payments with **zero custom code** using Stripe Payment Links.

## Prerequisites

1. Create a Stripe account at https://stripe.com
2. Complete your business profile in Stripe Dashboard

---

## Step 1: Create Products in Stripe Dashboard

### Go to Products Section
1. Login to Stripe Dashboard: https://dashboard.stripe.com
2. Navigate to: **Product catalog** → **Products** → Click **"Add product"**

### Product 1: Single Handmade Hair Clip
- **Name:** `Single Handmade Hair Clip`
- **Description:** `1 handmade hair clip in random color with free thank you card. Lovingly handcrafted by Olivia, each clip is unique and special.`
- **Pricing:**
  - Type: One-time
  - Price: `$5.00 USD`
- **Upload product image** (use images/hero.png or take a photo of a single clip)
- Click **"Save product"**

### Product 2: Clip Set - 3 Hair Clips
- **Name:** `Clip Set - 3 Hair Clips`
- **Description:** `3 handmade hair clips in random colors with gift box and free thank you card. Save $3!`
- **Pricing:**
  - Type: One-time
  - Price: `$12.00 USD`
- **Upload product image**
- Click **"Save product"**

### Product 3: Deluxe Collection - 6 Hair Clips
- **Name:** `Deluxe Collection - 6 Hair Clips`
- **Description:** `6 handmade hair clips in random colors with gift box and free thank you card. Save $10!`
- **Pricing:**
  - Type: One-time
  - Price: `$20.00 USD`
- **Upload product image**
- Click **"Save product"**

---

## Step 2: Create Payment Links

For **each product** you just created:

1. Click on the product name
2. Click **"Create payment link"** button
3. Configure the payment link:

### Basic Settings
- **Product and pricing:** Should be pre-filled
- **Quantity:** Set to 1 (or allow customer to adjust if they want multiple)

### Customer Information
- ✅ **Collect shipping address** (REQUIRED)
- ✅ **Collect phone number** (Optional but recommended)
- ✅ **Collect billing address** (Auto-enabled)

### After Payment
- **Success URL:** `https://www.liviarose.shop/thank-you.html`
- **Cancel URL:** `https://www.liviarose.shop/index.html#shop` (optional)

### Advanced Options (Optional)
- **Allow promotion codes:** Enable if you want to offer discount codes
- **Collect tax automatically:** Enable if required in your location
- **Payment methods:** Credit card, Apple Pay, Google Pay (all recommended)

4. Click **"Create link"**
5. **Copy the payment link URL** (looks like: `https://buy.stripe.com/test_xxxxxxxxxx`)

Repeat this for all 3 products.

---

## Step 3: Update Your Website

Replace the placeholder links in `index.html` with your actual Stripe Payment Links:

```html
<!-- Single Clip - Line 1078 -->
<a href="YOUR_ACTUAL_STRIPE_LINK_HERE" class="pricing-btn" target="_blank" rel="noopener noreferrer">Buy Now!</a>

<!-- 3-Pack - Line 1094 -->
<a href="YOUR_ACTUAL_STRIPE_LINK_HERE" class="pricing-btn" target="_blank" rel="noopener noreferrer">Buy Now!</a>

<!-- 6-Pack - Line 1110 -->
<a href="YOUR_ACTUAL_STRIPE_LINK_HERE" class="pricing-btn" target="_blank" rel="noopener noreferrer">Buy Now!</a>
```

### Example:
```html
<a href="https://buy.stripe.com/test_abc123xyz789" class="pricing-btn" target="_blank" rel="noopener noreferrer">Buy Now!</a>
```

---

## Step 4: Configure Email Notifications

### Automatic Customer Emails (Already Enabled)
Stripe automatically sends:
- ✅ **Payment confirmation** with receipt
- ✅ **Invoice** (PDF attached)
- ✅ **Refund confirmation** (if needed)

### Customize Customer Email Template
1. Go to: **Settings** → **Emails**
2. Click **"Customize email template"**
3. Edit the message:

**Example custom message:**
```
Hi {customer_name},

Thank you so much for your order from LiviaRose! 🎀

Your beautiful handmade hair clips will be lovingly crafted by Olivia and shipped to you within 1-3 business days.

Order Details:
{order_details}

You can expect delivery in 4-10 business days total.

Each clip is made with care and love, just for you! Thank you for supporting a young creator! ✨

With love,
Olivia & the LiviaRose Team

P.S. Follow us on Instagram @LiviaRose for new designs and updates!
```

4. Click **"Save changes"**

### Enable Owner Notifications
1. Go to: **Settings** → **Emails** → **Email notifications**
2. Enable these notifications for the shop owner's email:

   ✅ **Successful payments** - Get notified for every sale
   ✅ **Failed payments** - Know if something goes wrong
   ✅ **Refunds** - Track refund requests
   ✅ **Disputes** - Handle customer disputes immediately

3. Enter owner email address (your email)
4. Click **"Save"**

---

## Step 5: Configure Shipping & Return Policy

### Shipping Rates (Optional but Recommended)
1. Go to: **Settings** → **Shipping rates**
2. Add shipping rates:
   - **Flat rate shipping:** $3.00 for single clip, $5.00 for sets
   - **Free shipping threshold:** Consider free shipping over $20
   - **Geographic restrictions:** US only (or expand as needed)

### Return Policy
1. Go to: **Settings** → **Policies**
2. Add your return policy:

**Example:**
```
30-Day Return Policy

We want you to love your handmade hair clips! If you're not satisfied:
- Returns accepted within 30 days of delivery
- Items must be unused and in original packaging
- Free return shipping
- Full refund to original payment method

Contact us at: returns@liviarose.shop
```

---

## Step 6: Testing Before Going Live

### Test Mode
Stripe starts in **Test Mode** by default. Test your payment flow:

1. Use test payment links (they have `/test_` in the URL)
2. Use test card numbers:
   - **Success:** `4242 4242 4242 4242`
   - **Decline:** `4000 0000 0000 0002`
   - **Exp Date:** Any future date (e.g., 12/34)
   - **CVC:** Any 3 digits (e.g., 123)
   - **ZIP:** Any 5 digits (e.g., 12345)

3. Test the complete flow:
   - ✅ Click "Buy Now" button
   - ✅ Stripe checkout page opens
   - ✅ Enter shipping address
   - ✅ Enter test card details
   - ✅ Complete payment
   - ✅ Redirects to thank-you.html
   - ✅ Check email for receipt

### Go Live
1. Complete Stripe's verification requirements:
   - Business information
   - Bank account for payouts
   - Tax information
2. Toggle from **Test Mode** to **Live Mode** (top right corner)
3. Create **new Payment Links** in Live Mode
4. Update website with **Live Mode** payment links
5. Test again with a small real purchase

---

## Step 7: Additional Stripe Features (Optional)

### 1. Inventory Management
- Track stock levels in Stripe Dashboard
- Set low-stock alerts
- Auto-disable payment link when sold out

### 2. Discount Codes
- Create promotion codes: **Settings** → **Promotion codes**
- Examples: `FIRST10` (10% off first order), `WELCOME5` ($5 off)

### 3. Analytics
- View sales dashboard: **Home** → **Dashboard**
- Track revenue, customer count, payment success rate

### 4. Webhooks (Advanced - Optional)
- Automate inventory updates
- Sync with email marketing (Mailchimp, etc.)
- Track orders in Google Sheets

---

## Checklist Before Launch

- [ ] All 3 products created in Stripe
- [ ] All 3 payment links created and configured
- [ ] Payment links updated in index.html
- [ ] thank-you.html uploaded to website
- [ ] Customer email template customized
- [ ] Owner email notifications enabled
- [ ] Shipping rates configured
- [ ] Return policy added
- [ ] Test purchase completed successfully
- [ ] Stripe account verified and switched to Live Mode
- [ ] Live mode payment links deployed

---

## Customer Purchase Flow

Here's what happens when a customer buys:

1. **Customer** clicks "Buy Now" on liviarose.shop
2. **Redirected** to Stripe Checkout page
3. **Customer enters:**
   - Shipping address
   - Phone number
   - Credit card details
4. **Payment processed** by Stripe (secure, PCI-compliant)
5. **Customer receives:**
   - Order confirmation email with invoice PDF
   - Payment receipt from Stripe
6. **Shop owner receives:**
   - Notification email about new order
   - Customer details in Stripe Dashboard
7. **Customer redirected** to thank-you.html page
8. **Order fulfillment:** Check Stripe Dashboard daily for new orders

---

## Support & Resources

- **Stripe Documentation:** https://stripe.com/docs/payments/checkout
- **Payment Links Guide:** https://stripe.com/docs/payment-links
- **Test Cards:** https://stripe.com/docs/testing
- **Stripe Support:** https://support.stripe.com

---

## Troubleshooting

### Payment link doesn't work
- Check that link is from Live Mode (not Test Mode)
- Verify payment link is active in Stripe Dashboard
- Make sure success URL is correct

### Emails not sending
- Check spam/junk folder
- Verify email address in Stripe settings
- Check email notification settings are enabled

### Orders not appearing
- Confirm you're in Live Mode (not Test Mode)
- Check Dashboard → Payments for all transactions
- Verify webhook endpoints if using custom integrations

---

**Need Help?** Contact Stripe support at https://support.stripe.com
