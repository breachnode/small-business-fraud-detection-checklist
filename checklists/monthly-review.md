# Monthly Review

**Time required:** about 90 minutes, once a month.
**Purpose:** reconciliation and strategy. The daily check catches incidents; the weekly review catches trends; the monthly review answers the only question that matters over time: *is the money leaving the business the way it should?*

Do this after the month's bank statement arrives. The statement is the ground truth — everything else (payment dashboard, store records, invoices) is a claim about what happened. The monthly review is where claims get checked against truth.

## The review

### 1. Bank reconciliation

- [ ] Match every deposit in your bank statement to a payout from your payment processor. Every payout should have a matching deposit; every deposit should have a matching payout.
- [ ] Match every withdrawal and fee to a known cause: processor fees, chargeback debits, refunds, subscriptions, supplier payments.
- [ ] **Investigate:** a deposit you cannot match to a payout, or a payout you cannot find as a deposit. Either direction matters — money arriving from nowhere and money leaving without a record are both problems.
- [ ] **Investigate:** any withdrawal, fee, or debit you do not recognize, however small. Small unrecognized debits are how compromised accounts and forgotten subscriptions hide, and they are also how a fraudster tests whether anyone is watching.
- [ ] **Investigate:** a change in processor fees that does not match a change in volume. A sudden fee increase can mean a higher chargeback tier, a rate change you were not told about, or a billing error. All three are worth a phone call.
- [ ] **Do:** write down the month's totals — gross sales, processor fees, refunds, chargebacks, net deposits. One line a month, in the same spreadsheet as your weekly numbers. After six months you can see seasonality; after a year you can see whether your fraud costs are growing faster than your sales.

### 2. Chargeback rate and dispute outcomes

- [ ] Calculate the month's chargeback rate: chargebacks divided by total transactions.
- [ ] Count how many disputes you won and lost, and how much each outcome cost (chargeback amount plus any dispute fee).
- [ ] **Investigate:** a chargeback rate climbing toward 1% of transactions. That is roughly the level where card networks and processors start treating a merchant as high-risk. A rising rate is a warning to act before it becomes a program review, a reserve hold, or an account termination.
- [ ] **Investigate:** disputes lost for preventable reasons — evidence submitted late, delivery confirmation missing, no record of customer communication. Each lost dispute is a process fix, not just a loss.
- [ ] **Do:** if you lost a dispute because the evidence was not available, fix the evidence process this month (delivery tracking saved automatically, customer messages archived, order details exportable). The next dispute will come; the question is whether you are ready for it.

### 3. Customer and account audit

- [ ] Look for customer accounts with no activity for months that suddenly placed orders, changed details, or requested refunds.
- [ ] Look for accounts created in bulk (many accounts from the same source in a short period) that never ordered anything. Unused accounts created in bulk are often staged for later abuse.
- [ ] **Investigate:** a cluster of dormant accounts reactivating at once, or a wave of new accounts that never convert.
- [ ] **Do:** consider closing or flagging accounts that show the classic staged pattern (created in a burst, no activity, then sudden high-value activity). At minimum, require extra verification on their first order after a long silence.

### 4. Supplier and vendor review

- [ ] Confirm the payment details on file for every supplier you paid this month are still the ones you originally verified.
- [ ] Review any supplier who changed bank details, email addresses, or payment methods during the month — and confirm each change was verified by phone on a number you already had.
- [ ] **Investigate:** a supplier whose invoices rose sharply with no change in what you ordered, or a new supplier who appeared in your payables with no purchase order behind them.
- [ ] **Do:** once a year, re-verify every supplier's payment details from scratch. Supplier bank-detail fraud (sometimes called business email compromise) works precisely because nobody re-checks details that have been "fine for years."

### 5. Advertising and lead quality

- [ ] For the month, compare total ad spend with genuine inquiries and completed orders. Calculate cost per genuine inquiry.
- [ ] **Investigate:** cost per genuine inquiry rising while spend is flat or falling — you are paying for more of something that is not customers.
- [ ] **Investigate:** a campaign or ad set whose leads almost never convert, or whose leads share the same suspicious patterns (non-answering numbers, bouncing emails, repeated name fragments).
- [ ] **Do:** cut the spend that does not produce customers. A campaign that only produces clicks is a cost, not an investment, and fraud or not, the money is gone either way.

### 6. Rules and thresholds — the monthly tune

- [ ] Review every detection rule (see `detection-rules/generic-detection-rules.md`) against the month's numbers.
- [ ] **Tune:** any rule that fired more than a few times a week on normal business is too tight. Loosen it.
- [ ] **Tune:** any rule that never fired in a month is either watching for something that does not happen in your business (fine — leave it) or set too loose to catch what it is for (check it against one known incident from the month and see if it would have fired).
- [ ] **Tune:** thresholds should move with volume. If your order volume grew 50% this month, a velocity rule based on last month's numbers will fire constantly. Recalculate thresholds from the current month's baseline, not from when you first wrote the rule.
- [ ] **Do:** write down every change: rule, old threshold, new threshold, reason, date. A rulebook with no change history is a rulebook nobody trusts.

### 7. Access and credential hygiene

- [ ] List everyone (and every system) with access to your payment dashboard, store admin, email, and bank accounts. Remove anyone who no longer needs it.
- [ ] Confirm two-factor authentication is on for every business account that offers it — payment processor, store admin, email, bank, ad accounts.
- [ ] Change passwords on any shared account, and check whether any password is shared between two different services. A password used in two places is a single point of failure.
- [ ] Check for API keys, app integrations, or connected services you no longer use, and revoke them. An integration you forgot about is an open door you forgot to lock.
- [ ] **Do:** if an employee or contractor left this month, their access should already be revoked. If it is not, revoke it now and check the access logs for anything they did in their final days.

### 8. Incident log review

- [ ] Read through the month's incident log (`templates/incident-log.csv`).
- [ ] Count how many events were logged, how many were confirmed fraud, how many were false alarms, and how much confirmed fraud cost.
- [ ] **Investigate:** the same indicator appearing repeatedly. A repeated indicator is a rule waiting to be written — turn it into a detection rule.
- [ ] **Investigate:** incidents that were logged but never resolved. An open incident is an open question; close it with an outcome (confirmed, false alarm, or referred) or escalate it.
- [ ] **Do:** if the month's confirmed fraud cost is rising, that is the number to take to your bank or processor — not a feeling, not a single bad day, but a documented trend with dates and amounts.

## Synthetic example — what reconciliation catches

*(Synthetic example, invented for illustration. Not real data.)*

A resale business reconciles its October bank statement and finds a payout from its payment processor that is $640 short of what the dashboard predicted. The dashboard shows the payout; the bank shows a smaller deposit. Digging in, the owner finds two chargebacks debited the same week — one for an order shipped to an address that did not match the billing address, one for an order placed minutes after the account was created. Neither chargeback had produced an email the owner noticed, because the notification went to an old email address on the processor account. The monthly review caught what the daily checks missed: the notification address was stale. The fix took ten minutes. The lesson — check that your processor's notification email is one you actually read — is now a line in the monthly checklist.
