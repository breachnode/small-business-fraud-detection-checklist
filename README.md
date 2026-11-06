# Small-Business Fraud Detection Checklist

**Author:** Barry Harris — Greensboro, NC — bhar856@wgu.edu — [linkedin.com/in/barryha](https://www.linkedin.com/in/barryha)

**Background:** CompTIA CySA+ (Apr 2025), CompTIA PenTest+ (Jun 2025), CompTIA Security+ (Jul 2024), Google Cybersecurity Certificate (Mar 2025), ISC2 Certified in Cybersecurity (Mar 2025). Currently pursuing a BS in Cybersecurity and Information Assurance at Western Governors University (May 2023–Present).

## What this is

A practical fraud-detection starter kit for a small business that takes online payments. It covers what to monitor, what the warning signs look like, a set of generic detection rules written in plain language, and a step-by-step response playbook for the moment something looks wrong.

The one-line version: **fraud detection for a business with no fraud team — a Monday-morning routine that catches the common schemes before they become losses.**

This repo is written for a business owner or a junior analyst who has no fraud department, no dedicated tooling, and no time for theory. Every item in it is something one person can actually check, with the tools a small business already has: a payment dashboard, an email inbox, a bank statement, and a spreadsheet.

It is informed by running a phone-resale business (Direct Phone Buyer, Jun 2021–Jan 2025), where device and payment fraud were daily operational risks — stolen-device checks, payment verification, and account-takeover attempts were part of ordinary operations, not a separate security function. That experience is why this checklist is organized around the rhythms of a real small business instead of around an enterprise security program.

## Who it is for

- **Small-business owners** who take online or card payments and want a routine that catches fraud early without hiring anyone.
- **Junior fraud analysts and SOC analysts** who want to see detection-rule writing applied to realistic small-business scenarios.
- **Hiring managers** evaluating practical, business-facing security thinking — this repo shows detection work, not just theory.

## How to use this repo

1. **Start with the daily checklist** (`checklists/daily-monitoring.md`). Do it every business day. It takes about 15 minutes once it is a habit, and it catches most problems while they are still small.
2. **Do the weekly review** (`checklists/weekly-review.md`) once a week. It looks for patterns the daily check cannot see: trends, velocity, refund and chargeback drift.
3. **Do the monthly review** (`checklists/monthly-review.md`) once a month. It is the reconciliation pass: bank statements against payment records, supplier terms against invoices, and a look at whether your rules still fit your volume.
4. **Learn the red flags** (`indicators/`). Each file covers one area of the business — payments and chargebacks, accounts and identity, advertising, suppliers, and shipping — with what to look for and what to do when you see it.
5. **Set up the detection rules** (`detection-rules/generic-detection-rules.md`). They are written as plain-language logic ("alert when…"), not code tied to a product, so you can implement them in whatever tool you already use — or as a manual check.
6. **Know the response playbook before you need it** (`response-playbook.md`). When fraud is suspected, the first hour matters more than the first week. Read it now, not during an incident.
7. **Log every suspected event** with the template in `templates/incident-log.csv`. A written record is what turns a suspicion into a report a bank or investigator can act on.

## Scope and limits

- This repo covers **fraud detection, prevention, and response for small businesses**: payment fraud, card testing, chargebacks and refunds, account takeover, identity theft, advertising fraud, supplier and invoice fraud, and shipping/fulfillment fraud.
- It contains **no instructions for committing fraud**: no how-tos for wrongdoing, no operational detail that would let someone carry out a scheme, no evasion techniques, and no instructions for reaching or using illicit markets.
- All examples in this repo are **synthetic (labeled as such)** or **generic small-business scenarios** drawn from public fraud-prevention guidance. No real business data, no real victim data, and no real transaction details appear anywhere.
- Every threshold in the detection rules is an **illustrative starting point — tune it to your volume**. A threshold is not a claim about observed fraud rates, and a rule that fires constantly is a rule that needs tuning, not a business under attack.
- This repo does **not** cover penetration testing, incident response forensics, or malware analysis. Those are separate disciplines. The response playbook here is about containing a suspected fraud event and reporting it properly — not about forensic investigation.
- It names **no specific products, vendors, marketplaces, or platforms**. The rules are written to be transferable to whatever tools you already use.

## Disclaimer

This material is a **defensive fraud-prevention resource**. All examples are synthetic or generic small-business scenarios, and nothing in this repository is intended to enable wrongdoing. This is **general information, not legal or financial advice** — the author is not a lawyer or a financial advisor. Fraud, payment, and reporting obligations vary by jurisdiction, by card network, and by your agreements with your bank and payment processor; consult a qualified attorney or your bank's fraud team before acting on anything you are unsure about. If anything in this repo conflicts with your bank's guidance, your processor's rules, or applicable law, the bank, the processor, and the law win.

## Repository structure

```
small-business-fraud-detection-checklist/
├── README.md                              # This file
├── checklists/
│   ├── daily-monitoring.md                # The 15-minute daily routine
│   ├── weekly-review.md                   # Pattern-spotting once a week
│   └── monthly-review.md                  # Reconciliation and rule-tuning once a month
├── indicators/
│   ├── payments-and-chargebacks.md        # Card testing, payment anomalies, chargebacks, refunds
│   ├── accounts-and-identity.md           # Account takeover, identity theft, new-account abuse
│   └── ads-suppliers-fulfillment.md       # Ad fraud, supplier/invoice fraud, shipping fraud
├── detection-rules/
│   └── generic-detection-rules.md         # Plain-language rules: velocity, login, payment
├── response-playbook.md                   # First hour, first day, first week after suspected fraud
├── templates/
│   └── incident-log.csv                   # Blank log for suspected fraud events (with synthetic examples)
└── resources.md                           # Public sources and where to report fraud
```

## What this repo demonstrates

A hiring manager reading this repo should see three things: **detection-rule writing** (the core of fraud-analyst and SOC work, in generic, transferable form), **business-facing security thinking** (controls a one-person business can actually run, not an enterprise program shrunk down), and **judgment about what belongs in writing** (indicators and responses only — never instructions for the other side).

## A note on thresholds

Every number in this repo that looks like a threshold — "three failed authorizations in ten minutes," "five new accounts from one source in an hour" — is an **illustrative starting point** chosen to make the rule concrete. It is not a measured fraud rate and not a recommendation for your business specifically. A shop doing ten orders a day and a shop doing a thousand need different numbers. Tune every rule to your own volume, watch how often it fires for a week, and adjust until it fires on genuinely unusual events and stays quiet on normal ones. A rule that never fires is decoration; a rule that fires all day is noise.
