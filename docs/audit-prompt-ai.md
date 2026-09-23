# Audit prompt — AI layer, bank-record analysis and budgeting

> Paste everything below the line into the reviewing model or person.
> Fill the `[FILL IN]` fields first.
>
> **Assumption to correct if wrong:** this audits the existing settle-up/ledger app extended
> with an AI layer over connected bank data. If the intended subject is a standalone personal
> finance app with no poker component, delete section 2's poker framing and section H; the
> rest applies unchanged.

---

You are auditing a proposed AI and open-banking layer for an early-stage product. Nothing is
built: the repository holds planning documents and no application code. Your job is to
pressure-test the plan and recommend the best approach, not to validate it. Assume the author
prefers a hard problem now to a discovered one in three months.

## 1. Where this sits

An earlier audit of this project established the following. Treat these as prior findings you
may contest, not as settled fact — but do not spend the audit re-deriving them:

- The original plan took a 1-2% rake off each pot. That is **ruled out**: it would require a
  gambling licence under Ireland's Gambling Regulation Act 2024, administered by the GRAI.
- More seriously, **section 67 of that Act prohibits *providing a game* without a licence**,
  with no commercial-purpose qualifier that the prior audit could find, and section 70
  prohibits supplying gambling software without a B2B licence that may not fit a product
  supplied to unlicensed friends. So the card-dealing engine is legally exposed independently
  of how money is made. The conclusion was to ship the ledger and not the felt.
- Market research then found the ledger itself largely commoditised: **Revolut ships "Group
  Bills", which tracks shared expenses across a group over time**, in Ireland and 40-plus
  European countries, with payments included. PokerSquad ships cross-session leaderboards and
  persistent groups. Free browser extensions add persistent cross-session tracking on top of
  PokerNow. Multiple open-source tools do minimum-transfer settle-up for nothing.
- The conclusion was that the ledger does not work as a differentiated business.

**This proposal is the response to that conclusion.** The bet is that an AI layer over
connected bank data is the differentiator the plain ledger lacked. Your central task is to
judge whether that bet is sound, or whether it adds regulatory surface, cost and risk to a
product whose underlying position is already weak.

## 2. What is proposed

The existing product: players record buy-ins, rebuys and cash-outs for a home poker game; the
app computes the minimum set of transfers that squares everyone at the end of a session, and
folds each session into a running multi-session ledger for the group. Money moves outside the
app entirely — Revolut, cash, bank transfer. The app never holds or routes funds.

The proposed additions:

1. **Bank connection.** A user links their bank account so the app can read transactions.
2. **Reconciliation.** The app matches real transactions against the ledger's expectations —
   "the app says Dave owes you €35; a €35 transfer from Dave landed on Friday, so mark it
   settled" — including cash withdrawals before game night.
3. **Categorisation and budgeting.** Transactions are classified, and the user sees what the
   game actually costs them over weeks and months, against a budget or limit they set.
4. **AI insight.** Natural-language summaries and explanations of position, trends and
   spending, rather than only tables.

## 3. Context on the author

- Solo developer, student in Ireland. Stack: Next.js, Supabase, Vercel, Tailwind.
- ~20 hrs/week in bursts, little during term. Free service tiers only; **no legal or
  compliance budget**.
- Studying abroad on Erasmus from January, so several months without physical presence in
  Ireland.
- Target: real revenue, on the order of [FILL IN: monthly figure] within twelve months.
- First audience: [FILL IN].
- Appetite for a regulated path — becoming or partnering with a licensed entity: [FILL IN:
  none / would consider a licensed intermediary / would consider authorisation].
- Whether the AI component is the point (author wants to build AI) or a means to an end:
  [FILL IN — this materially changes your recommendation].

## 4. What to audit

Work through all nine. Do not summarise the plan back.

**A. Open banking and payment-services licensing — do this first and hardest.** Reading a
user's bank transactions as a service is, in the EU, the regulated activity of an **Account
Information Service Provider** under PSD2, supervised in Ireland by the Central Bank. Assess:
does this product require AISP authorisation? Can it be avoided by building on a licensed
aggregator (TrueLayer, Plaid, GoCardless/Nordigen, Tink and similar), and if so, does the
author become a regulated agent, an exempt customer of the provider, or something in between?
What does each aggregator actually require of a solo developer with no company and no
compliance function — and will any of them onboard one at all? Note whether PSD3 or the
Financial Data Access framework changes this. **If the honest answer is that this cannot be
done compliantly by an unincorporated student, say so plainly and early — it ends the
audit.**

**B. The gambling overlay on financial data.** The prior audit's section 67 problem does not
disappear here; it may worsen. The product would hold, against identified bank accounts, a
structured record of individuals' gambling stakes and losses. Assess: does systematically
tracking gambling spend attract any duty under the Gambling Regulation Act 2024 — safer
gambling, advertising, inducement or self-exclusion provisions? Does holding this data change
the author's position relative to sections 67 and 70? Do banks' and card networks' own
gambling controls interact with this (for example, Revolut's gambling blocks)? Is a product
that makes gambling spend easier to sustain defensible, and what duty of care follows?

**C. AI architecture and numerical correctness.** State the architecture you would require,
and be specific about the division of labour. The prior view in this project is that
deterministic code must compute every monetary figure and the model must only label, match and
explain — never do arithmetic. Confirm, refute or refine that. Then address: how transaction
categorisation should actually be done (model, rules, a learned classifier, or a hybrid), and
whether an LLM is the right tool for it at all given per-transaction cost; how transaction
matching should handle the genuinely hard cases (partial payments, a €50 transfer settling two
debts, cash, someone paying for drinks instead of settling); and how confidence is represented
so the user is asked rather than told when the match is uncertain. A wrong reconciliation is
not a bug, it is an argument between friends with the app's name on it.

**D. AI-specific legal exposure.** Cover: the **EU AI Act** — is any part of this a high-risk
system (note that creditworthiness assessment is listed in Annex III) and does budgeting
guidance come near that boundary; whether natural-language guidance about money risks
straying into **regulated financial advice**; **GDPR** obligations for what is plainly
sensitive-in-practice financial data, including lawful basis, the data-processor relationship
with any model provider, transfers outside the EEA, automated-processing rules and data
minimisation; and what must be true before a single transaction is sent to a third-party
model.

**E. Security.** Two things specifically. First, the threat model for storing bank tokens and
transaction data on a solo developer's free-tier infrastructure — and whether that is
acceptable at all, or whether the data should never be persisted. Second, and easily missed:
**transaction description fields are attacker-controlled text.** Anyone who can send the user
a payment can choose the reference. If descriptions are fed to a model that has tools or acts
on its output, that is a prompt-injection channel into a system holding financial data.
Specify the mitigation.

**F. Competitive reality.** The personal finance management graveyard is large — Money
Dashboard, Yolt and others closed; Emma, Plum, Moneyhub and similar persist. Meanwhile banks
ship budgeting and spending analytics free and by default, and Revolut already does both
budgeting *and* the group ledger. Is there a defensible wedge in "AI that reconciles your
home game against your bank", or is this a feature Revolut could ship and the author cannot
market? Answer in one sentence, and say plainly if the answer is no.

**G. Unit economics.** This layer has real cost of goods, unlike the plain ledger. Estimate,
with your reasoning shown: per-connected-account aggregator fees, model inference cost per
user per month at a realistic transaction volume, and infrastructure. Then state the gross
margin at a €5/month subscription and say whether the price must change. Include the practical
consequence of **PSD2 consent re-authentication**, which forces users to reconnect
periodically and is a well-documented source of churn in this category.

**H. The contradiction that may sink the design.** The product's founding principle was that
**guests join with a tapped link and a first name — no account, no signup** — because poker is
a 4-9 person coordination problem and any friction loses the game. But bank reconciliation
only works for people who connect a bank account. So either only the host gets reconciliation,
which reconciles one side of every transfer, or every player must onboard through a bank
connection, which destroys the frictionless-guest property the product depended on. Resolve
this, or say it is unresolvable and what that means for the plan.

**I. Scope.** Given the constraints in section 3 — no compliance budget, ~20 hrs/week, abroad
from January — define the smallest version worth building, and say whether it should include
bank connectivity at all in v1. Consider explicitly whether manual CSV import or a shared
screenshot achieves most of the value with none of the licensing, and whether the AI component
should ship before the regulated data pipe rather than after.

## 5. How to answer

- Open with a verdict: proceed, proceed with modifications, or do not build this. If section A
  is fatal, say so in the first line and keep the rest brief.
- Then take the areas in order. Give firm recommendations with reasoning, not menus.
- Where the plan is sound, say so briefly and move on.
- Separate what you know from what you are inferring. Irish and EU regulatory specifics, AI
  Act classifications, aggregator onboarding requirements and current pricing are all things
  to mark clearly as verified or not — the author has no budget to discover you were guessing.
- Note explicitly where **not** building the AI or bank layer is the stronger answer, if that
  is what you conclude.
- End with the three things to do first, in order, and the single question a qualified person
  must answer before any code is written.
