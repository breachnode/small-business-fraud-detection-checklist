# Response Playbook: When Fraud Is Suspected

**Read this before you need it.** When fraud is suspected, the first hour matters more than the first week. This playbook tells you what to do in the first hour, the first day, and the first week — in order, so you do not have to decide under pressure.

Three principles govern everything below:

1. **Contain first, investigate second.** Stop the loss from growing before you try to understand it.
2. **Document as you go.** Every action, every timestamp, every name. A report without dates and records is a story, not evidence.
3. **Do not try to investigate like a professional.** Your job is to stop the bleeding, preserve the evidence, and hand it to the people whose job it is — your bank, your processor, and law enforcement. Do not contact the suspected fraudster, do not try to "test" what happened, and do not delete anything.

## The first hour

### 1. Stop the money from moving (minutes 0–15)

- **Hold the affected orders.** Do not ship anything connected to the suspected fraud — not the suspicious order, not other orders from the same account, address, or payment method. A held order can be released later. A shipped item cannot be un-shipped.
- **Pause the affected advertising.** If the suspicion involves ad spend, pause the campaigns. Ad money burns while you think.
- **Do not issue refunds** connected to the suspected activity until you understand what happened. A refund issued during an incident can become a second loss.
- **Do not change payout details, passwords, or settings yet** — unless you have evidence an account is actively being used against you right now (for example, a payout destination that was just changed, or orders being placed from your account this minute). If something is actively happening, lock it down first: change the password, revoke the session, then continue below.

### 2. Preserve the evidence (minutes 15–30)

- **Screenshot or export everything relevant, now.** Order details, payment records, login history, messages with the customer, delivery tracking, ad account change history. Screenshots are fine — save them with the date in the file name.
- **Do not delete anything.** Do not delete the customer account, the order, the messages, or the logs — even if they look like they belong to a fraudster. Deleting evidence destroys your ability to dispute a chargeback, file a report, or help an investigation.
- **Write down what happened, in order, with times.** What you saw, when you saw it, and what you have done so far. This becomes the incident record. Use `templates/incident-log.csv` — one row per event, and keep adding rows as the incident develops.

### 3. Contain the account (minutes 30–60)

- **If a customer account is involved:** disable or suspend the account, or force a password reset — whichever your platform allows. Do not delete it.
- **If one of your business accounts is involved** (payment dashboard, store admin, email, ad account): change the password, turn on two-factor authentication if it is not already on, and review the account for changes you did not make — payout details, email addresses, API keys, connected apps, active sessions. Revoke any session or integration you do not recognize.
- **If a payment method is involved:** contact your bank or processor (see "Who to report to" below) and ask what they need from you. Do not cancel a card or close an account on your own initiative before asking — the bank may want the account left open to trace the activity.
- **Tell anyone who needs to know, inside the business.** If an employee processes orders, refunds, or payments, they need to know what to hold and what to watch for — today, not at the next staff meeting.

## The first day

### 4. Assess the scope

- **How many orders, accounts, or payments are affected?** Check whether the same email domain, address, device, or payment method touched other orders. Fraud is rarely a single order — look for the pattern, not just the incident that caught your attention.
- **How much money is involved?** Add up the orders held, the refunds at risk, the chargebacks received, and the ad spend affected. You need a number before you talk to a bank or file a report — "some fraud" is not a reportable amount.
- **Is it still happening?** Check the daily monitoring items again. If the pattern is continuing, the first-hour containment was not enough — escalate faster.

### 5. Contact your bank or payment processor

- **Call your processor's fraud team** (the number is on your processor's website or your monthly statement — find it now and write it in your incident log, so you are not searching for it during an incident).
- **Tell them:** what happened, when it started, how many transactions are involved, the total amount, and what you have already done (orders held, account suspended). Give them the incident log.
- **Ask them:** whether they want you to do anything else, whether they can block the source, and what the dispute deadlines are for any chargebacks. Write down the name of the person you spoke to, the case or reference number, and the time of the call.
- **If a bank account is involved:** call your bank's fraud department the same day. Do not wait to see whether it resolves itself — it will not.

### 6. Notify the platform (if one is involved)

- **If the fraud involves a specific platform** — a marketplace, a payment app, an ad platform, a shipping carrier — report it through that platform's fraud or abuse reporting channel. Give them the same facts: what happened, when, how much, and what you have done.
- **Keep the reference number** from every report you file, in the incident log.

### 7. Notify affected customers (carefully)

- **If a customer's account was taken over:** contact the customer on the contact details you had *before* the incident — not the details that were changed during it. Tell them what happened, what you have done, and what they should do (change their password, check their bank statements, consider a fraud alert with the credit bureaus).
- **Do not accuse anyone.** State facts: "We detected unauthorized activity on your account." Not conclusions about who did it.
- **Do not share details of your investigation** with the customer beyond what they need to protect themselves.

## The first week

### 8. File the formal reports

- **FBI Internet Crime Complaint Center (IC3)** — ic3.gov — for internet crime including fraud and identity theft. File when the loss is significant, when the fraud crosses state lines (most online fraud does), or when you want the incident on record with law enforcement. Keep the complaint number.
- **Federal Trade Commission (FTC)** — reportfraud.ftc.gov — for fraud, scams, and identity theft. File in addition to IC3, not instead of it — they serve different purposes.
- **Local law enforcement** — file a police report if the loss is large, if the fraud involved someone local, or if your bank or insurer asks for one. Bring the incident log and the amounts. A police report number is often required for insurance claims and for some bank processes.
- **Your insurer** (if you have business insurance that covers fraud or cyber events) — notify them within the timeframe your policy requires. Bring the incident log, the amounts, and any reference numbers from the bank, the processor, IC3, and the police.

### 9. Dispute the chargebacks

- **Submit evidence for every chargeback** before its deadline. Dispute deadlines are short — usually days, not weeks — and a missed deadline is an unrecoverable loss.
- **Evidence to submit:** the order details, delivery confirmation, any messages with the customer, and a short written summary of what happened with dates. Keep a copy of everything you submit.
- **Track the outcome** of each dispute in the incident log. A dispute you win is a recovery; a dispute you lose is a process fix — find out why it was lost and fix that process.

### 10. Fix the gap

- **Find the hole the fraud came through.** Name the gap in one sentence: a missing rule, a rule not followed, a notification going to an unread email, a shared password, supplier details changed on the strength of an email.
- **Fix it, and write the fix down.** A new detection rule, a changed process, a notification address updated, two-factor authentication turned on, a refund policy tightened. If the fix is a new rule, add it to `detection-rules/generic-detection-rules.md` with the date and the incident that prompted it.
- **Tell the business.** If employees process orders, refunds, or payments, they need to know what changed and why — in plain language, once, in writing.

### 11. Close the incident

- **Update the incident log** with the final outcome: confirmed fraud or false alarm, total loss, total recovered, reports filed and their reference numbers, and the fix applied.
- **An incident with no outcome is an open question.** Close it. If you cannot determine the outcome, write "unresolved — referred to [bank/processor/law enforcement]" and the reference number. That is a closed incident with a clear status, not an open one.
- **Review the month.** At the next monthly review (see `checklists/monthly-review.md`), look at the incident alongside the month's other numbers. One incident is an event. A pattern of incidents is a strategy problem.

## Who to report to — quick reference

See `resources.md` for the full reporting list with contact details. The short version: bank and processor the same day; IC3 and FTC within the week; local law enforcement and your insurer when the loss is large or they require it.

## What NOT to do

- **Do not contact the suspected fraudster.** Do not message, email, or call them — not to confront them, not to ask for the goods back, not "just to see." Contact risks tipping them off, destroying evidence, and putting you in a conversation you cannot control. Report; do not engage.
- **Do not try to investigate like a professional.** Do not attempt to trace the fraudster, access their accounts, or test whether a card is stolen. That is law enforcement's job, and attempting it yourself can break the law and destroy evidence.
- **Do not delete anything.** Not the account, not the order, not the messages, not the logs. Deletion destroys evidence you will need for chargebacks, reports, and insurance.
- **Do not pay to recover anything.** If someone offers to recover your money, your goods, or your account for a fee, it is almost certainly a second fraud — the recovery scam. Legitimate recovery happens through your bank, your processor, and law enforcement, and none of them charge you a fee to file a report.
- **Do not keep it quiet inside the business.** If employees handle orders, refunds, or payments, they need to know what happened and what to watch for. Silence is how a second incident happens through the same gap.

## Synthetic example — the first hour, done right

*(Synthetic example, invented for illustration. Not real data.)*

A resale shop owner checks the payment dashboard at 9:00 AM and sees 30 failed authorizations from the same email domain in the last hour, plus two successful orders for high-value items shipping to the same address. First hour: both orders held, the burst logged with timestamps, payout details checked (unchanged). First day: the processor's fraud team confirms the pattern and blocks the source. First week: an IC3 report filed, a velocity rule added, the daily checklist updated. Total loss: zero — because the playbook was read before the incident happened.
