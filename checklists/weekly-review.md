# Weekly Review

**Time required:** about 45 minutes, once a week, same day each week.
**Purpose:** see patterns a daily check cannot — trends, velocity, drift. A single day of card testing is a daily-check item. Three weeks of slowly rising refund rates is a weekly-review item, and it is usually the more expensive problem.

Do this with the daily logs from the week in front of you. If you have not been keeping the daily log, the weekly review is where you will feel it — reconstructing a week from memory is guesswork, and guesswork is how fraud hides.

## The review

### 1. Velocity trends

- [ ] Count failed authorizations for the week and compare with last week.
- [ ] Count new customer accounts created this week and compare with last week.
- [ ] Count orders per day and look for a day that is far above or below the week's average.
- [ ] **Investigate:** failed authorizations up sharply with no matching increase in orders — someone may be testing cards against you and mostly failing, which still costs you processor fees and risk flags.
- [ ] **Investigate:** new accounts up sharply with no marketing push or promotion to explain it. A spike in account creation that does not turn into real customers is often the setup phase for account-takeover or new-account abuse.
- [ ] **Investigate:** one day with far more orders than the rest of the week, especially if those orders share an attribute (same product, same shipping area, same payment pattern). A burst day is worth a closer look even if every individual order looked fine on its own.
- [ ] **Do:** write the week's numbers down in one place — even a single line in a spreadsheet: week, orders, failed authorizations, new accounts, refunds, chargebacks. After a month you have a baseline, and after a quarter you can see drift that no single day would show.

### 2. Refund and chargeback patterns

- [ ] List every refund and chargeback from the week.
- [ ] **Investigate:** refunds concentrated on one product, one customer, or one employee account. A refund pattern that clusters is a pattern worth understanding — it may be a process problem (a product that keeps arriving damaged) or a fraud problem (refunds routed to a different payment method). Either way, it costs money until you find it.
- [ ] **Investigate:** chargeback rate rising week over week. As a rough guide, a chargeback rate above about 1% of transactions is the level where card networks and processors start paying attention — treat a rising rate as an early warning, not a number to argue with after it crosses a threshold.
- [ ] **Investigate:** chargebacks with the same reason code repeating (for example, several "product not received" claims on orders that show as delivered).
- [ ] **Do:** for every chargeback, confirm the evidence file was submitted on time. Missed dispute deadlines are unrecoverable losses. See `response-playbook.md`.

### 3. Account-takeover signals

- [ ] Look at password-reset requests for the week — count them and look for bursts.
- [ ] Look for customer accounts where contact details (email, phone, shipping address) changed and an order followed within a day.
- [ ] Look for accounts with a long quiet period that suddenly became active and placed a large order.
- [ ] **Investigate:** a burst of password resets on accounts that then place orders, change payment methods, or change shipping addresses. That sequence — reset, change, purchase — is the standard account-takeover shape.
- [ ] **Do:** if you find one compromised account, check whether the same email domain, device, or IP range touched other accounts. Account takeover is rarely a single account.

### 4. Device and location changes

- [ ] If your payment dashboard or store shows device or location data, scan for accounts logging in from a new device and a new location in the same session, especially if a purchase follows immediately.
- [ ] **Investigate:** several accounts logging in from the same new device or the same unusual location in a short period.
- [ ] **Do:** remember that legitimate customers travel and buy new phones. A new device alone is not fraud — a new device plus a password reset plus an immediate high-value purchase is a pattern.

### 5. Advertising review (if you run paid ads)

- [ ] Compare this week's ad spend, leads, and orders with last week.
- [ ] **Investigate:** spend up and orders flat, or leads up and orders flat. Paying for attention that never becomes a customer is either a bad campaign or a fake one — both cost money, and the fix starts with pausing the spend, not with debating which it is.
- [ ] **Investigate:** leads that share a pattern (same name fragments, phone numbers that never answer, email addresses that bounce or look generated).
- [ ] **Investigate:** clicks or leads from regions you do not serve, or at hours when your real customers are not awake.
- [ ] **Do:** record cost per genuine inquiry, not cost per click. Clicks are what you buy; inquiries are what you need.

### 6. Supplier and invoice check

- [ ] List every invoice paid this week and match each one to a purchase order or a real delivery.
- [ ] **Investigate:** an invoice from a supplier you do not recognize, or from a known supplier with changed bank details, a new email address, or an urgent payment request.
- [ ] **Investigate:** duplicate invoices — the same invoice number paid twice, or two invoices for the same goods.
- [ ] **Investigate:** a supplier who suddenly asks to be paid by a different method (wire transfer instead of card, a new account number, a payment app you have never used with them).
- [ ] **Do:** as a standing rule, never change a supplier's payment details on the strength of an email alone. Confirm the change by calling the supplier on a number you already have — not a number in the email asking for the change. See `indicators/ads-suppliers-fulfillment.md`.

### 7. Rule tuning

- [ ] Look at which detection rules fired this week (see `detection-rules/generic-detection-rules.md`).
- [ ] **Tune:** a rule that fired on normal business is set too tight — raise the threshold or narrow the condition.
- [ ] **Tune:** a rule that never fires may be set too loose, or the thing it watches may not happen in your business. Either is fine — a quiet rule costs nothing. Do not tighten a rule just to make it fire.
- [ ] **Tune:** a rule that fired and caught something real is working. Leave it alone.
- [ ] **Do:** change one rule at a time, and write down what you changed and why. Changing three rules at once means you will never know which change mattered.

## Synthetic example — what a weekly review catches that a daily check misses

*(Synthetic example, invented for illustration. Not real data.)*

A small online shop does its daily checks faithfully and sees nothing alarming: a few failed payments a day, one or two refunds a week, no chargebacks. In the weekly review, the owner lines up four weeks of numbers:

| Week | Orders | Failed authorizations | Refunds | New accounts |
|---|---|---|---|---|
| 1 | 210 | 14 | 3 | 38 |
| 2 | 218 | 19 | 4 | 41 |
| 3 | 205 | 31 | 7 | 66 |
| 4 | 212 | 47 | 11 | 94 |

Orders are flat. Everything else is climbing. The daily checks saw each day as "a few failures, a refund or two" — nothing that looked like an incident. The weekly view shows a trend: someone is testing cards and opening accounts against this shop, and the refund count is starting to follow. The owner tightens the velocity rule, starts holding first-time high-value orders for a manual check, and the numbers flatten the following week. No single day would have shown it.
