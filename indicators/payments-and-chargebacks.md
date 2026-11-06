# Red Flags: Payments and Chargebacks

How payment fraud actually shows up in a small business. Each entry follows the same shape: **what you see**, **what it might mean**, **what to do**. "Might mean" is deliberate — a red flag is a reason to look closer, not a verdict. A legitimate customer can trip any single flag; a fraudster usually trips several at once.

## Card testing

### Rapid small-value authorizations

- **What you see:** many authorization attempts for small amounts (often the smallest amount a card can be charged, or a round number just above it), arriving in a burst — dozens within minutes — mostly failing, a few succeeding.
- **What it might mean:** someone is checking which stolen card numbers are still valid by running them against your checkout. Your store is being used as a card validator. The small amounts are chosen to avoid triggering fraud alerts and to stay under the cardholder's notice.
- **What to do:** log the burst with the shared attributes (same email domain, same billing details, same device or network source if your processor shows it). Hold any orders from the successful attempts for manual review. Do not re-run failed authorizations. If the burst continues, contact your processor's fraud team — they can block the source and will want the timestamps. See `detection-rules/generic-detection-rules.md` rule V-1.

### Many cards, one customer

- **What you see:** several different card numbers used by the same customer account, email address, or shipping address in a short period — especially if each card fails once or twice before another is tried.
- **What it might mean:** the buyer is working through a list of card numbers until one is accepted. A legitimate customer rarely cycles through several cards in one session.
- **What to do:** hold the order. Check whether the cards share a billing address or name pattern. If the order is high-value or for easily resold goods, verify the customer by phone on the number on the order before shipping.

### One card, many customers

- **What you see:** the same card number used across several different customer accounts, names, or email addresses.
- **What it might mean:** a single stolen card being used through multiple accounts, often to spread the activity so no one account looks suspicious.
- **What to do:** hold all affected orders and contact your processor. This pattern is worth reporting even if the individual amounts are small — it indicates a card that is being actively abused.

## Payment anomalies

### Billing and shipping mismatch on a first order

- **What you see:** a first-time customer whose billing address and shipping address are in different states or countries, with no order history.
- **What it might mean:** the buyer has the card details but not the cardholder's address, so the goods go somewhere else. This is one of the most common fraud shapes in online retail.
- **What to do:** for a low-value order, it may be a gift or a customer who moved — use judgment. For a high-value order, for easily resold goods, or when combined with any other flag on this page, verify before shipping: call the phone number on the order, or ask the customer to confirm a detail only the cardholder would know. Do not ship first and verify later.

### Rushed high-value first order

- **What you see:** a brand-new account places a large order within minutes of being created, selects the fastest shipping, and the items are high-value or easy to resell.
- **What it might mean:** the buyer wants the goods shipped before anyone looks closely. Speed is the fraudster's friend — every hour of delay is an hour in which a cardholder or a bank might notice.
- **What to do:** hold the order for a manual check. A one-day delay on a first order is normal business practice and costs far less than a chargeback plus a lost item.

### Payment method changed just before purchase

- **What you see:** a customer account changes its saved payment method and then immediately places an order, or adds a new card and uses it within minutes.
- **What it might mean:** the account may have been taken over, and the new payment method is the attacker's card — or the attacker's way of testing a stolen card through a legitimate-looking account.
- **What to do:** if the account also changed its email address, phone number, or shipping address recently, treat the order as high-risk and verify it. See `accounts-and-identity.md`.

### Unusual payment types for your business

- **What you see:** a customer insists on an unusual payment method for your business — a wire transfer where you normally take cards, a payment app you do not normally accept, a gift card as payment for goods.
- **What it might mean:** the buyer is trying to move the transaction outside the protections (and the paper trail) of the normal payment flow.
- **What to do:** as a standing rule, accept only the payment methods you have set up and understand. Do not improvise a payment method for a single customer, however urgent they say it is.

## Chargebacks

### "Product not received" on a delivered order

- **What you see:** a chargeback claiming the product was never received, on an order with delivery confirmation to the address on the order.
- **What it might mean:** it may be a genuine delivery problem — or a friendly-fraud claim, where the customer received the goods and disputes the charge anyway. Either way, the evidence decides the outcome.
- **What to do:** keep delivery confirmation for every order, and keep it somewhere you can find it in minutes, not hours. Submit the tracking record, the delivery confirmation, and any customer communication with the dispute. See `response-playbook.md` for dispute deadlines.

### "Did not recognize" on a recognizable charge

- **What you see:** a chargeback saying the customer did not recognize the transaction, on an order with a matching name, address, and delivery.
- **What it might mean:** the cardholder genuinely did not recognize your business name on their statement (fix: make your statement descriptor recognizable), or the card was used without the cardholder's knowledge.
- **What to do:** first, check your statement descriptor — if it shows an unfamiliar name, fix it; that alone prevents a share of these disputes. Then submit your evidence as usual. A clear descriptor is the cheapest chargeback prevention there is.

### Chargebacks clustering on one product or address

- **What you see:** several chargebacks in a short period for the same product, the same shipping address, or the same reason code.
- **What it might mean:** a targeted abuse pattern — someone has found a product or a process that is easy to exploit, and is repeating it.
- **What to do:** treat the cluster as one incident, not several unrelated ones. Log it as a single pattern in the incident log, look for the shared attribute, and consider a temporary rule (for example, manual review on all orders for that product above a certain value) until you understand it.

### Chargeback rate climbing

- **What you see:** your chargeback rate — chargebacks divided by total transactions — rising month over month, approaching or passing about 1%.
- **What it might mean:** your fraud exposure is growing, whether from one scheme or from several small ones. Around 1% is roughly where card networks and processors start treating a merchant as high-risk, which can mean reserve holds, higher fees, or account review.
- **What to do:** do not wait for a threshold to be crossed. A rising rate is the warning. Review the daily and weekly checklists for what changed, and talk to your processor's fraud team before the processor talks to you.

## Refunds

### Refund to a different payment method

- **What you see:** a request to refund a purchase to a different card, a different account, or a payment app — instead of the original payment method.
- **What it might mean:** this is a classic refund fraud shape: pay with a stolen card, then have the refund sent somewhere the fraudster controls. The original cardholder disputes the original charge, and the business loses both the goods and the refund.
- **What to do:** refunds go back to the original payment method only. No exceptions, no matter how reasonable the request sounds. Make this a written rule, tell anyone who processes refunds, and do not let a single persuasive customer override it.

### Refund without customer contact

- **What you see:** a refund issued with no customer message, no support ticket, and no record of a problem with the order.
- **What it might mean:** an internal problem — a refund processed by mistake, or by someone who should not be processing refunds — or a test of whether refunds are monitored.
- **What to do:** restrict who can issue refunds, and review every refund weekly (see `checklists/weekly-review.md`). If a refund was issued by an employee account, ask that person what the reason was and whether there is a record.

### Repeated refunds for the same customer or product

- **What you see:** the same customer refunding repeatedly, or the same product being refunded far more often than others.
- **What it might mean:** a customer abusing a generous return policy, a product with a real quality problem, or a refund scheme. The first step is the same in all three cases: look at the pattern.
- **What to do:** check the reason each time. If the reasons are vague or inconsistent, or if the goods are never returned, tighten the process for that customer or that product — require a return before refund, or require a manager's approval above a value threshold.

## Synthetic examples

*(Synthetic examples, invented for illustration. Not real data.)*

**Example 1 — card testing:** A shop's payment dashboard shows 47 failed authorizations between 2:04 and 2:21 AM, all for the same small amount, all from the same email domain, all with different card numbers. Three attempts succeed. The shop holds the three successful orders, logs the burst, and contacts the processor. The three orders share a shipping address that matches none of the billing addresses. Nothing ships.
