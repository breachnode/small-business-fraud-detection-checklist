# Daily Monitoring Checklist

**Time required:** about 15 minutes, once a day, every business day.
**Purpose:** catch the common fraud patterns while they are still small — a card-testing run in progress, a compromised account placing orders, a refund scheme starting up.

Do this at the same time every day, ideally before you start fulfilling orders. The point of a fixed time is that anything unusual stands out against yesterday's normal. If you skip days, you lose the baseline — and the baseline is the whole detection method for a small business.

## The checklist

Check each item off. If anything is marked **investigate**, log it in `templates/incident-log.csv` before you move on — do not trust yourself to remember it later.

### 1. Failed payments

- [ ] Open your payment dashboard and look at failed authorizations from the last 24 hours.
- [ ] **Normal:** a handful of failures scattered across the day — expired cards, insufficient funds, typos. A few per day is background noise for any business that takes cards.
- [ ] **Investigate:** a burst of failures from the same source (same cardholder name, same billing address, same device or IP range, same email pattern) in a short window. Several small-value failures in minutes is the classic signature of card testing: someone checking which stolen card numbers are still live by running small authorizations against your checkout.
- [ ] **Investigate:** failures that are all for the same amount, or amounts that step up in a regular pattern (for example, a run of identical small charges followed by one larger one).
- [ ] **Do:** if you see a burst, note the shared attribute (same email domain, same billing ZIP, same device fingerprint if your processor shows one) and watch whether it continues. Do not refund or re-run failed authorizations. See `detection-rules/generic-detection-rules.md` rule V-1.

### 2. New orders — a quick scan

- [ ] Scan today's orders (or yesterday's, if you check in the morning) for anything that looks different from a normal order.
- [ ] **Investigate:** an order where the billing and shipping addresses are in different states or countries with no prior order history from that customer — especially if the order is high-value, rushed, or for items that resell easily.
- [ ] **Investigate:** several orders from different customer names shipping to the same address, or the same phone number or email appearing under different names.
- [ ] **Investigate:** an order placed minutes after an account was created, with no browsing history and a first purchase that is large or high-value.
- [ ] **Investigate:** a customer whose email address is a random-looking string of letters and numbers, or an email domain you have never seen before, combined with any of the above.
- [ ] **Do:** hold the order for a manual check (see `response-playbook.md`, "Hold, don't cancel") rather than shipping it and hoping. A one-day delay costs far less than a chargeback plus a lost item.

### 3. Chargebacks and disputes

- [ ] Check for any new chargeback or dispute notices from your processor or bank.
- [ ] **Normal:** an occasional dispute is part of taking cards. One every few weeks, for a recognizable reason (customer did not recognize the charge, item arrived damaged), is background.
- [ ] **Investigate:** two or more chargebacks in one day, or chargebacks that share a pattern — same product, same shipping address, same reason code.
- [ ] **Investigate:** a chargeback on an order that was delivered to an address different from the billing address, or on an order placed from a brand-new account.
- [ ] **Do:** start the evidence file immediately (order details, delivery confirmation, any messages with the customer). Dispute deadlines are short — usually days, not weeks — and the evidence is hardest to find after the fact. See `indicators/payments-and-chargebacks.md`.

### 4. Refunds

- [ ] Look at refunds issued in the last 24 hours.
- [ ] **Normal:** refunds tied to a customer message, a damaged item, or a cancelled order, with the refund going back to the original payment method.
- [ ] **Investigate:** a refund to a different payment method or a different account than the one that paid. This is one of the oldest small-business fraud patterns: pay with a stolen card, then get the refund sent somewhere the fraudster controls.
- [ ] **Investigate:** a refund issued without any customer contact or support ticket — especially if it was processed by an employee account rather than by you.
- [ ] **Investigate:** several refunds for the same product or the same customer in a short period.
- [ ] **Do:** as a standing rule, refunds go back to the original payment method only. No exceptions, no matter how reasonable the request sounds. See `indicators/payments-and-chargebacks.md`.

### 5. Account logins

- [ ] Check login activity for your own business accounts (payment dashboard, store admin, email) and, if your store shows it, customer login anomalies.
- [ ] **Investigate:** a burst of failed logins on any business account, or a successful login from a place or device you do not recognize.
- [ ] **Investigate:** password-reset requests for customer accounts followed quickly by an order, an address change, or a payment-method change on that account.
- [ ] **Investigate:** a customer account whose email address or phone number changed and then placed an order within hours.
- [ ] **Do:** if a business account shows a login you do not recognize, change the password immediately, turn on two-factor authentication if it is not already on, and check whether anything was changed in the account (payout details, email addresses, API keys). See `detection-rules/generic-detection-rules.md` rule L-1 and `response-playbook.md`.

### 6. Payout and account details

- [ ] Glance at your payout/bank details in your payment dashboard.
- [ ] **Normal:** the payout account is the one you set up, and nothing has changed.
- [ ] **Investigate:** any change to the payout bank account, the payout email, or the business contact email — especially a change you did not make. A changed payout destination is how a compromised account turns into stolen money.
- [ ] **Do:** treat any unexpected change as an incident, not a curiosity. Follow `response-playbook.md` from the first hour.

### 7. Advertising (if you run paid ads)

- [ ] Check yesterday's ad spend against what you expected.
- [ ] **Normal:** spend roughly in line with your daily budget, clicks and leads in their usual range.
- [ ] **Investigate:** a sudden spike in spend with no matching increase in real inquiries or orders, or traffic from regions you do not serve.
- [ ] **Investigate:** leads that all share the same pattern — same first name repeated, phone numbers that do not answer, email addresses that bounce.
- [ ] **Do:** pause the affected campaign before investigating further. Ad spend burns while you think. See `indicators/ads-suppliers-fulfillment.md`.

### 8. End of the day — write it down

- [ ] If anything was marked **investigate**, make sure it is in `templates/incident-log.csv` with the date, the indicator, and what you did.
- [ ] If nothing was unusual, write nothing. A blank day is a good day, and a log full of "nothing happened" entries is a log nobody will read.

## What "normal" means

"Normal" in this checklist means *normal for your business*. A shop doing ten orders a day will see one or two failed payments on a busy day; a shop doing a thousand will see dozens. Learn your own numbers over the first two weeks of doing this routine, write them down, and use them as the baseline. A rule that fires on your normal volume is a rule that needs tuning, not a business under attack.

## Synthetic example — a normal day vs. a card-testing day

*(Synthetic example, invented for illustration. Not real data.)*

**Normal day:** 42 orders, 3 failed authorizations (two expired cards, one insufficient funds), 1 refund (customer message, damaged item, refunded to the original card), 0 chargebacks, 0 login anomalies. Total check time: 12 minutes.

**Card-testing day:** 44 orders, 38 failed authorizations — all for the same small amount, all from the same email domain, all within 20 minutes, all between 2:00 and 2:20 AM. Two of the attempts succeeded. That is not background noise. That is a burst, and it gets logged, the successful orders get held for review, and the shared attributes go into the detection rules.
