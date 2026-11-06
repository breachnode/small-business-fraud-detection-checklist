# Red Flags: Ads, Suppliers, and Fulfillment

Fraud does not stop at the checkout. A small business that advertises, buys from suppliers, and ships goods has three more places where money can leak: the ad account, the supplier relationship, and the delivery itself. Each area below follows the same shape as the other indicator files: **what you see**, **what it might mean**, **what to do**.

## Advertising fraud

### Spend up, customers flat

- **What you see:** ad spend rises (or stays high) while genuine inquiries and completed orders stay flat — or fall.
- **What it might mean:** the ads are reaching people who are not customers. That may be bad targeting, a broken landing page, or fraudulent traffic: automated clicks, fake leads, or an ad account that has been compromised and is running spend you did not approve.
- **What to do:** pause the spend first and investigate second — ad money burns while you think. Compare cost per genuine inquiry (not cost per click) with last week and last month. If the gap opened suddenly, look at what changed: a new campaign, a new audience, a new person with access to the ad account. Check the ad account's login history and active campaigns for anything you did not create.

### Leads that never become customers

- **What you see:** a stream of leads — form fills, messages, calls — that share a pattern: the same first names repeated, phone numbers that never answer, email addresses that bounce or look generated, messages that say almost nothing.
- **What it might mean:** fake leads, generated to consume ad budget or to make a campaign look effective. A lead that cannot be contacted is not a lead.
- **What to do:** track leads to contact, not just leads to form-fill. Count how many leads you actually reach. If a campaign produces volume and no conversations, pause it and look at the lead details before spending more. A campaign that only produces clicks is a cost, not an investment.

### Traffic from places you do not serve

- **What you see:** clicks, leads, or engagement coming from regions you do not serve, or at hours when your real customers are not awake — especially if it starts suddenly.
- **What it might mean:** your ads are being shown to the wrong audience (a targeting mistake), or the traffic is not human. Either way, you are paying for it.
- **What to do:** check the geographic and time breakdown in your ad reporting. Narrow the targeting to the areas you actually serve. If the traffic persists after targeting is fixed, the problem is not targeting.

### Campaigns or ads you did not create

- **What you see:** an ad campaign, ad set, or ad in your account that you do not recognize — or an existing campaign whose budget, audience, or destination link has changed without your knowledge.
- **What it might mean:** your ad account has been compromised. A changed destination link is a particularly serious sign: your ads may be sending your customers (and your money) somewhere else entirely.
- **What to do:** Treat this as an incident: pause the campaigns, change the password, turn on two-factor authentication, and review who has access. Then follow `response-playbook.md` and notify the platform's support team. Check your billing — a compromised ad account often shows spend you did not approve.

### Ad account access you do not recognize

- **What you see:** a user, a business manager, or an agency you do not recognize has access to your ad account, or a former contractor's access is still active.
- **What it might mean:** access granted for a one-off job and never revoked, or access granted by someone who should not have granted it. Every active access is a door; every forgotten door is a risk.
- **What to do:** review access monthly (see `checklists/monthly-review.md`). Remove anyone who no longer needs it. If you find access you cannot explain, revoke it and check the account's change history for what that access did.

## Supplier and invoice fraud

### A supplier's payment details change by email

- **What you see:** an email — apparently from a supplier you already use — saying their bank details have changed, asking you to send future payments to a new account, often with a reason (new bank, new accountant, urgent payment needed).
- **What it might mean:** this is business email compromise: someone impersonating your supplier to redirect your payments. It is one of the most expensive frauds a small business can suffer, because a single redirected payment can be large and is very hard to recover.
- **What to do:** Never change a supplier's payment details on the strength of an email alone — not even if it looks perfect and references a real invoice. Call the supplier on a number you already have (not one in the email) and confirm verbally. This one rule, followed every time, stops this fraud completely.

### An invoice you do not recognize

- **What you see:** an invoice from a supplier you have never used, or for goods or services you never ordered — often for a small amount, often looking official, sometimes marked urgent or overdue.
- **What it might mean:** a fake invoice sent in the hope that a busy business pays it without checking. Small amounts are deliberate: they are below the threshold where anyone looks twice.
- **What to do:** match every invoice to a purchase order or a real delivery before paying it. If there is no purchase order and no delivery, do not pay it — and do not call the number on the invoice to ask about it. If the invoice claims to be from a real supplier, call that supplier on a number you already have.

### Duplicate invoices

- **What you see:** the same invoice number paid twice, or two different invoices for the same goods, the same amount, and the same date.
- **What it might mean:** a billing error, or a deliberate duplicate sent to get paid twice for one delivery.
- **What to do:** check the invoice number and the delivery record before paying anything. Keep a simple list of invoices paid each month — even a spreadsheet — and check new invoices against it. The check takes a minute; the duplicate costs the full invoice amount.

### A supplier who suddenly wants a different payment method

- **What you see:** a supplier who has always been paid by card or check suddenly asks for a wire transfer, a payment app, or a gift card — especially with urgency attached.
- **What it might mean:** the request may not be from your supplier at all, or the supplier's email may be compromised. Wire transfers and gift cards are effectively irreversible; that is why fraudsters prefer them.
- **What to do:** do not change the payment method on an urgent request. Call the supplier on a number you already have and confirm. If the supplier genuinely changed methods, the change will survive a phone call.

### A new supplier with no purchase order

- **What you see:** a new supplier appears in your payables — an invoice arrives, or a payment is requested — with no purchase order, no email thread, and no one in the business remembering ordering anything from them.
- **What it might mean:** a fake supplier created to extract a payment, or an internal process gap where someone ordered without recording it. Either way, the payment should not go out until the order is explained.
- **What to do:** do not pay. Find out who ordered it and what was delivered. If nobody can say, treat it as a suspected fraud and log it.

## Shipping and fulfillment fraud

### Orders shipped to an address that keeps changing

- **What you see:** a customer whose shipping address changes on every order, or an order whose shipping address was changed after the order was placed.
- **What it might mean:** the buyer is trying to get goods sent somewhere the cardholder would not expect — or the account has been taken over and the shipping address is being redirected. An address changed after payment is a stronger signal than an unusual address at checkout.
- **What to do:** for a high-value order, or when the address changed after payment, hold the shipment and verify with the customer on the original contact details. See `accounts-and-identity.md`.

### Delivery claims that do not match tracking

- **What you see:** a customer claims an order never arrived, but tracking shows it delivered to the address on the order — or a customer claims an item arrived damaged and asks for a refund or a replacement, while the tracking and packaging show nothing wrong.
- **What it might mean:** a genuine delivery problem, a damaged item, or a false claim (friendly fraud). The tracking record is the evidence; the claim is the question.
- **What to do:** keep delivery confirmation for every order and keep it findable. For a "not received" claim with confirmed delivery, submit the tracking record if it becomes a chargeback. For a damage claim, ask for a photo before refunding or replacing — a real damaged item produces a photo without argument.

### Returns that do not come back

- **What you see:** refunds issued for returned goods, but the goods never arrive back — or the returned item is not the item that was sold (a different model, a damaged substitute, an empty box).
- **What it might mean:** return fraud: the refund is claimed and the goods are kept, or a cheaper item is returned in place of the expensive one. In a resale business, this is a daily risk — a returned device that is not the device that was sold.
- **What to do:** as a standing rule, inspect every return before issuing the refund — and for high-value items, check the serial number or identifying mark against the one you shipped. Refund after inspection, not before. A customer who objects to an inspection is telling you something.

### Orders for easily resold goods, in bulk, from new accounts

- **What you see:** new accounts ordering multiples of the same high-value, easily resold item — phones, electronics, gift cards, branded goods — often with express shipping and different names shipping to the same address.
- **What it might mean:** the goods are the point, not the account. Easily resold items are the preferred target of payment fraud because they convert to cash fast.
- **What to do:** for bulk orders of resalable goods from new accounts, apply a manual review before shipping. Check the payment, the account age, and the shipping address together — no single one of them is decisive, but the combination usually is.

## Synthetic examples

*(Synthetic examples, invented for illustration. Not real data.)*

**Example 1 — the supplier email:** A small business receives an email from its regular parts supplier: "We have changed banks — please send all future payments to the attached account details." The email uses the supplier's logo, references a real invoice number, and is signed with the name of the person the business normally deals with. The owner calls the supplier on the number saved in their phone — not the number in the email — and the supplier says they have not changed banks. The email was fake. One phone call saved a payment that would have been unrecoverable.
