# Generic Detection Rules

Rules written in plain language, not code tied to a product. Each rule follows the same shape: **rule** (the logic), **what to look for**, **what to do when it fires**, and **tuning notes**.

Implement these in whatever you already use — your processor's fraud settings, your store's built-in rules, or a manual check. A rule you can run by hand beats one you cannot implement.

**All thresholds are illustrative starting points — tune them to your volume.** A threshold is not a measured fraud rate. Watch how often each rule fires for a week, and adjust until it fires on genuinely unusual events and stays quiet on normal ones. Change one rule at a time, and write down what you changed and why.

## How to read a rule

- **Alert** means: stop and look. It does not mean the transaction is fraud.
- **Hold** means: do not ship, do not refund, do not release the goods until the check is done.
- **Log** means: record the event in `templates/incident-log.csv` with the date, the rule that fired, and what you did.

A rule that fires constantly is a rule that needs tuning, not a business under attack. A rule that never fires may be fine — or may be set too loose. Test each rule against one real incident from your log and see whether it would have fired.

---

## Velocity rules

Velocity rules watch for *too much, too fast*. They are the most useful rules a small business can run, because most fraud is a volume game: many attempts, many accounts, many orders, in a short window.

### V-1 — Failed-authorization burst

- **Rule:** Alert when the same source produces 3 or more failed authorizations within 10 minutes.
- **What counts as "the same source":** the same email address, the same billing address, the same cardholder name, the same device or network source if your processor shows it, or the same email domain. Any one shared attribute is enough to group the attempts.
- **What to look for:** a burst of small-value attempts, mostly declined, with a few successes mixed in. Card testing is the pattern this rule exists for — and the pattern counts even when some attempts succeed.
- **What to do:** log the burst. Hold any orders from the successful attempts for manual review. Do not re-run failed authorizations. If the burst continues, contact your processor's fraud team with the timestamps and the shared attributes.
- **Tuning:** if your volume is high, try 5 in 10 minutes or 10 in an hour. If your volume is low, 3 in 10 minutes is already a lot. Watch it for a week, then adjust.

### V-2 — New-account burst

- **Rule:** Alert when 5 or more new customer accounts are created from the same source within 1 hour.
- **What counts as "the same source":** the same device, network source, or email domain, or email addresses that follow the same generated pattern (same structure, sequential numbers, random-looking strings from one domain).
- **What to look for:** accounts that never order, or accounts that all become active at once days later. Bulk account creation is usually the setup phase for a later scheme.
- **What to do:** flag the accounts. Require extra verification on their first orders. Do not delete them — the record of the pattern is more useful than an empty list.
- **Tuning:** a promotion can create a legitimate burst. If it lines up with a promotion you ran, it is probably real. If it lines up with nothing, it is probably not.

### V-3 — Order burst

- **Rule:** Alert when the same customer, address, or payment method places 3 or more orders within 24 hours, or when total orders in a day are more than double the recent daily average with no promotion to explain it.
- **What to look for:** several orders for the same product, shipping to the same address under different names, or one account ordering far more than it ever has.
- **What to do:** hold the orders for manual review. Check whether the payments are good and whether the shipping addresses make sense. A legitimate bulk buyer will answer a phone call; a fraudster usually will not.
- **Tuning:** if your business normally takes bulk orders, watch for *new* accounts ordering in bulk, not your regulars.

### V-4 — Refund velocity

- **Rule:** Alert when the same customer receives 2 or more refunds within 7 days, or when total refunds in a week are more than double the recent weekly average.
- **What to look for:** refunds clustering on one customer, one product, or one employee account. Refund abuse is usually a pattern before it is a large loss.
- **What to do:** review the reason for each refund. Require a return before refund for the affected product or customer. If refunds are being issued by an employee account, check who issued them and whether there is a record for each one.
- **Tuning:** a product with a genuine quality problem will trip this rule legitimately. If the refunds are real and documented, fix the product, not the rule.

---

## Login and account rules

### L-1 — Failed-login burst

- **Rule:** Alert when the same account (or the same source across many accounts) records 5 or more failed logins within 15 minutes.
- **What to look for:** many failures on one account (someone trying to get into that account), or one failure each across many accounts from the same source (someone testing a list of credentials — credential stuffing).
- **What to do:** if it is one account, check whether a login eventually succeeded — if it did, treat the account as possibly compromised: force a password reset, review recent activity, and check for changed contact details or orders. If it is many accounts from one source, note the source and watch for successful logins from it.
- **Tuning:** legitimate customers mistype passwords, but five failures in 15 minutes is past "mistyped." Do not set this lower — you will drown in noise.

### L-2 — Password reset, then change, then purchase

- **Rule:** Alert when an account requests a password reset, then changes its email address, phone number, or shipping address, then places an order — all within 24 hours.
- **What to look for:** the sequence, in that order. Each step alone is normal. The sequence in a short window is the account-takeover shape.
- **What to do:** hold the order. Contact the customer on the *original* contact details (the ones on file before the change), not the new ones. If you cannot reach the original owner, do not ship. Log the sequence.
- **Tuning:** this is a sequence rule, so the only question is the window. 24 hours is a reasonable start; shorten it to 4 hours if it fires on legitimate customers who reset a password, update an address, and order in the same evening.

### L-3 — New device and new location, then purchase

- **Rule:** Alert when an account logs in from a device and a location it has never used before, and places an order in the same session.
- **What to look for:** a new device plus a new location plus an immediate purchase — especially a high-value purchase, or a purchase of easily resold goods.
- **What to do:** a new device alone is not fraud. If this rule fires together with L-2 (a recent reset or detail change), hold the order and verify. If it fires alone, note it and move on — customers travel and buy new phones.
- **Tuning:** if your store does not show device or location data, run the manual version: on any first order after a long silence, or any high-value first order, check the account's history before shipping.

### L-4 — Dormant account reactivation

- **Rule:** Alert when an account with no activity for 90 days or more places an order, changes its details, or requests a refund.
- **What to look for:** a long-quiet account waking up and immediately doing something valuable — ordering, refunding, changing payout or contact details.
- **What to do:** treat the first order after a long silence as a first order: apply the same checks you would to a brand-new account. Age alone is not trust.
- **Tuning:** set the window to twice your normal gap between orders — longer if your customers order seasonally.

---

## Payment rules

### P-1 — Billing and shipping mismatch on a first order

- **Rule:** Alert when a first-time customer's billing address and shipping address are in different states or countries, and the order is above your normal order value.
- **What to look for:** the mismatch plus one more factor — high value, express shipping, easily resold goods, or a brand-new account.
- **What to do:** hold the order and verify by phone on the number on the order. A legitimate customer with a gift order or a recent move will confirm without difficulty.
- **Tuning:** set the value threshold at roughly double your average order value.

### P-2 — High-value first order

- **Rule:** Alert when a brand-new account places a first order above a value threshold (starting point: three times your average order value), especially with express shipping.
- **What to look for:** a large first purchase, minutes after account creation, with the fastest shipping option.
- **What to do:** hold the order for a manual check. A one-day delay on a first order is normal business practice.
- **Tuning:** set the threshold from your own numbers, with a floor (a fixed dollar amount you choose) so you are not reviewing every slightly-above-average order.

### P-3 — Payment method changed, then immediate purchase

- **Rule:** Alert when an account adds or changes a saved payment method and uses it to place an order within 1 hour.
- **What to look for:** a new card added and used immediately, especially on an account that also changed contact details recently.
- **What to do:** if the account also tripped L-2, hold the order and verify on the original contact details. If not, note it and move on — customers do add a new card and buy something with it.
- **Tuning:** the 1-hour window is the point — a card added a week ago and used today is normal; a card added four minutes ago and used immediately is worth a look.

### P-4 — Refund to a different payment method

- **Rule:** Alert on ANY request to refund a purchase to a different payment method, card, or account than the one that paid. This rule has no threshold and no tuning — it fires every time.
- **What to look for:** a customer asking for the refund to go to a different card "because the first one was cancelled," to a payment app, or to a different person's account.
- **What to do:** decline. Refunds go back to the original payment method only. Log the request. If the customer insists, offer to re-issue the refund to the original method once the customer confirms the original method is still valid.
- **Tuning:** none. This is a policy, not a threshold. The only correct setting is "always alert, always decline."

---

## Rule list at a glance

| Rule | Watches | Starting threshold | Action on fire |
|---|---|---|---|
| V-1 | Failed-authorization burst | 3 failures, same source, 10 min | Log, hold successful orders |
| V-2 | New-account burst | 5 accounts, same source, 1 hr | Flag accounts, verify first orders |
| V-3 | Order burst | 3 orders / 24 hr, or 2× daily average | Hold for manual review |
| V-4 | Refund velocity | 2 refunds / customer / 7 days, or 2× weekly average | Review reasons, require returns |
| L-1 | Failed-login burst | 5 failures, 15 min | Check for success, force reset if compromised |
| L-2 | Reset → change → purchase | Sequence within 24 hr | Hold, contact original details |
| L-3 | New device + location + purchase | Same session | Verify if combined with L-2 |
| L-4 | Dormant account reactivation | 90 days quiet, then activity | Treat as first order |
| P-1 | Billing/shipping mismatch, first order | Above normal order value | Hold, verify by phone |
| P-2 | High-value first order | 3× average order value | Hold for manual check |
| P-3 | Payment method changed, immediate purchase | Within 1 hr | Verify if combined with L-2 |
| P-4 | Refund to different method | Any occurrence | Decline, log |

## A note on false positives

Every rule in this file will fire on a legitimate customer eventually. That is expected. A rule is not a verdict — it is a reason to look. The cost of looking is a phone call or a one-day hold. The cost of not looking is a chargeback, a lost item, and a refund that also goes out the door. When in doubt, look.

And when a rule fires on the same legitimate customer repeatedly, write that customer down as a known exception. A rulebook that cannot recognize its regulars gets ignored, and an ignored rulebook protects no one.
