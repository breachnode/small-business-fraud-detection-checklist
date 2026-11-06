# Red Flags: Accounts and Identity

How account takeover and identity theft show up in a small business. The pattern to remember is a **sequence**: reset, change, purchase. Any one step on its own is usually innocent. The steps in order, in a short window, are the signal.

## Account takeover

### Password-reset bursts

- **What you see:** a sudden burst of password-reset requests — on one account, or across many accounts at once.
- **What it might mean:** someone is testing which accounts they can get into, either by requesting resets in bulk or by working through a list of email addresses to see which ones have accounts with you.
- **What to do:** check whether any of the reset requests were followed by a login, a contact-detail change, or an order. A reset alone is noise; a reset followed by activity is the incident. If your store shows it, look at whether the resets came from the same source. Consider rate-limiting reset requests if your platform allows it.

### Reset, change, purchase — in that order

- **What you see:** a customer account requests a password reset, then changes its email address, phone number, or shipping address, then places an order — all within hours.
- **What it might mean:** this is the standard account-takeover shape. The attacker gets in, changes the contact details so the real owner stops receiving notifications, and then orders goods to an address the attacker controls.
- **What to do:** hold the order. Try to contact the customer on the *original* contact details (the ones on file before the change), not the new ones — the new ones may belong to the attacker. If you cannot reach the original owner, do not ship. Log the sequence in the incident log.

### Dormant account suddenly active

- **What you see:** an account with no activity for months suddenly logs in and places a large order, changes its details, or requests a refund.
- **What it might mean:** the account credentials were exposed in a breach elsewhere and are now being used, or the account was created long ago and left dormant deliberately so it would look established when it was finally used.
- **What to do:** treat the first order after a long silence as a first order — apply the same checks you would to a brand-new account. Age alone is not trust.

### Login from a new device and a new place, then a purchase

- **What you see:** an account logs in from a device and a location it has never used before, and places an order in the same session.
- **What it might mean:** the login may be the account owner travelling or on a new phone — or it may be someone else entirely.
- **What to do:** a new device alone is not fraud. A new device plus a password reset plus an immediate high-value purchase is a pattern. If two or more of those are present, hold the order and verify.

### Multiple accounts, one source

- **What you see:** many customer accounts created from the same device, network source, or email pattern in a short period — especially if they never order, or all order the same thing at once.
- **What it might mean:** accounts being staged for later abuse. Creating accounts in bulk is cheap; using them later is when the fraud happens. A wave of accounts that never convert is often the setup phase, not a marketing success.
- **What to do:** flag the accounts. If they later become active, require extra verification on their first order. Do not delete them immediately — a record of the pattern is more useful than an empty account list.

## Identity theft

### Synthetic identity signs

- **What you see:** a new account whose identity details do not quite fit together — a name that matches no public record pattern, an address that is a vacant lot or a mail drop, a phone number that is newly issued, a date of birth that makes the customer implausibly young or old for the purchase.
- **What it might mean:** a synthetic identity — an identity assembled from a mix of real and invented details — being used to open an account or place an order. Synthetic identities are built to pass automated checks that look at each field in isolation, which is why the mismatch only shows when a person looks at the whole picture.
- **What to do:** do not try to verify an identity by collecting more personal data — that creates its own risk. Instead, verify the *transaction*: call the phone number on the order, check that the shipping address is a real deliverable address, and hold high-value orders until the customer confirms. If the details do not hold up, do not ship.

### Identity details that change with every order

- **What you see:** a customer whose name, address, or phone number is slightly different on every order — a different spelling, a different apartment number, a different phone digit.
- **What it might mean:** someone avoiding exact-match checks by varying the details, or a customer who is simply careless. The difference is the pattern: fraud varies details deliberately and consistently; carelessness is random.
- **What to do:** look at the orders together. If the variations all point to the same person receiving goods at the same place, and the payments are all good, it is probably carelessness. If the variations spread across different payment methods and shipping addresses, hold the orders and look closer.

### High-velocity new accounts

- **What you see:** many new accounts created in a short period, especially if they share an email pattern (same domain, same naming structure) or all use details that look generated rather than human.
- **What it might mean:** automated account creation — the front end of a larger scheme. The accounts may be used for fraudulent orders, for fake reviews, for refund abuse, or sold onward.
- **What to do:** compare the week's new-account count with your baseline (see `checklists/weekly-review.md`). If it is far above normal with no marketing explanation, treat the cohort as high-risk: require extra verification on their first orders, and watch for the reset-change-purchase sequence.

### Orders under a name that does not match the payment

- **What you see:** the name on the order and the name on the payment method are different, with no obvious explanation (no gift note, no shared surname, no prior order history under either name).
- **What it might mean:** the card belongs to someone other than the person placing the order. It may be a legitimate gift — or it may be a stolen card.
- **What to do:** for low-value orders, accept the risk and move on. For high-value orders, or when combined with any other flag, verify: a phone call to the number on the order is usually enough to tell a gift from a fraud.

## Employee and insider signals

Fraud is not always external. A small business has few employees, which makes internal fraud easier to miss and more damaging when it happens. These are not accusations — they are controls.

- **Refunds only one person issues.** If all refunds in a week come from one employee account, and there is no reason that person should be the only one issuing refunds, look at the refunds, not the person. The pattern is the signal.
- **Orders or discounts that bypass the normal process.** An order fulfilled without payment, a discount applied without a code, a manual price override — any of these can be legitimate, but each one should have a record and a reason.
- **Access that outlasts employment.** A former employee or contractor whose login still works is an open door. Check access monthly (see `checklists/monthly-review.md`).

## Synthetic examples

*(Synthetic examples, invented for illustration. Not real data.)*

**Example 1 — the sequence:** A customer account that has ordered twice in the past year requests a password reset at 9:12 AM. At 9:19 AM the account's email address changes. At 9:26 AM the shipping address changes to a different city. At 9:31 AM a high-value order is placed for easily resold goods with express shipping. Each step alone is unremarkable. Together, in nineteen minutes, they are the account-takeover shape. The shop holds the order and emails the original address on file. The real customer replies within the hour: they did not request any of it.
