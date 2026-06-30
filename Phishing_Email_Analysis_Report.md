# Task 2: Phishing Email Analysis Report

## 1. Sample Phishing Email

```
From: "PayPaI Security" <security@paypa1-support.com>
To: victim@example.com
Subject: URGENT: Your Account Will Be Suspended in 24 Hours!

Dear Customer,

We detected unusual activity on your account. To avoid permanent
suspension, you must verify your identity immediately by clicking
the link below.

>> Verify My Account Now <<
(Link displayed: https://paypal.com/verify — actual href: http://paypa1-support-verify.ru/login.php)

Failure to act within 24 hours will result in permanent account
closure and loss of funds.

Thanks for you cooperation,
PayPaI Security Team
```

## 2. Header Snapshot (from analyzer)

| Field | Value | Flag |
|---|---|---|
| Return-Path | bounce@mailblast-svc.ru | Mismatched domain |
| Received (originating IP) | 185.220.xx.xx (Russia) | Inconsistent with claimed US company |
| SPF | fail | Sender not authorized |
| DKIM | none | No signature |
| DMARC | fail | Policy violation |
| Reply-To | support@paypa1-support.com | Differs from From domain |

## 3. Phishing Indicators Found

1. **Spoofed display name** — "PayPaI" uses a capital "I" instead of lowercase "l" to mimic PayPal.
2. **Lookalike domain** — `paypa1-support.com` (digit "1" replacing "l") instead of `paypal.com`.
3. **Authentication failures** — SPF fail, DKIM missing, DMARC fail confirm the sender is not PayPal's mail server.
4. **Mismatched URL** — Displayed link text shows the real PayPal URL, but the actual hyperlink points to a `.ru` domain.
5. **Urgency/threat language** — "24 hours," "permanent suspension," "loss of funds" pressure the user into rash action.
6. **Generic greeting** — "Dear Customer" instead of the user's actual name.
7. **Grammar/spelling errors** — "Thanks for you cooperation" (missing "r").
8. **Suspicious call-to-action button** — Designed to look official but leads to a credential-harvesting page.

## 4. Summary

This sample exhibits all classic phishing traits: domain spoofing, failed email authentication (SPF/DKIM/DMARC), a deceptive hyperlink, urgency-based social engineering, and language errors. A user should never click the link, should report the email as phishing, and should verify any account concern by typing the official website URL directly into the browser.
