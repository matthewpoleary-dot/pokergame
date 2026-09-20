# Idea assessment — tips & gratuities compliance for Irish hospitality

Date: 2026-09-20. Method: web search. **Confidence caveat:** the WRC's own guidance PDF,
workplacerelations.ie, and the statute book were all blocked by this session's network egress
policy. Legal specifics below come from law-firm and government summaries, which agree with
each other, but the primary sources should be read directly before building. Nothing here is
legal advice.

## Verdict

**Better shaped than the poker idea, and still hard — but hard for reasons of sales and
timing rather than because the market is already taken.** The problem is real, legally
compelled, recurring, and largely invisible to developers outside Ireland. The risk has
moved: it is no longer "fourteen people built this", it is "the systems that already hold the
data could add a button".

Recommended shape: build the free compliance-artefact generator now, sell the paid
distribution tool next summer when physically present. Reasoning at the end.

## The legal obligation, precisely

Under the **Payment of Wages (Amendment) (Tips and Gratuities) Act 2022**, in force since
1 December 2022, covering restaurants, pubs, hotels, guesthouses, tour companies, hairdressing,
beauty salons, taxis, delivery and bookmakers:

1. **Electronic tips must be distributed fairly** to employees, and the employer **may not
   retain any share** of them.
2. **A written policy** on how electronic tips are distributed must be given to each employee
   **within five days of starting work**.
3. **A statement** must be given to each employee showing **the total tips distributed by the
   employer for the period** and **the amount distributed to that employee** — provided
   **within 10 days of the distribution**.
4. **A public "Tips and Gratuities Notice"** must be displayed, stating whether tips are
   distributed to staff, **how**, and **the amounts**; and the same for mandatory service
   charges.
5. **Service charges** must be treated as tips.

### Enforcement is specific and named

WRC inspectors can issue **Fixed Payment Notices of up to €2,000** for, among others:
failure to provide a tips and gratuities statement; failure to treat service charges as tips;
failure to post the tips and gratuities notice. Payable within 42 days, after which the
Commission brings prosecution proceedings.

That matters more than the law itself. The penalties attach to *exactly the artefacts a
software tool would produce*. There is a named fine for not having the document you would be
selling.

## Market

- **6,793 pubs and nightclubs** in Ireland (2026), plus restaurants, cafés, hotels, salons
  and taxi firms — a covered population plausibly in the 15,000-20,000 range.
- The drinks and hospitality industry employs **92,000 people**.
- **But the sector is contracting and cost-pressured.** A quarter of Irish pubs have closed
  since 2005, declines in all 26 counties, and 22% of pubs cut staff in the past year citing
  cost pressure. Dublin is the exception at -1.1%, which is where you are.

Selling new software into a shrinking, margin-squeezed sector is the central commercial
difficulty. The compliance fear is what overcomes it — a €2,000 notice is more than a decade
of subscription.

## Who already serves this, and the honest gap

The ecosystem splits three ways, and none of the three spans the whole obligation:

| Layer | What it does | What it doesn't |
|---|---|---|
| **POS** (Square, SumUp) | Square Ireland supports tipping team members directly, or pooling each card tip "across all tip-eligible team members clocked in at the time of the transaction" | Requires staff to clock in and out on the POS, which small Irish pubs largely don't do. Produces a payout, not the statutory statement |
| **Payroll** (BrightPay — 350k employers IE/UK, Thesaurus, Collsoft) | Taxes tips through payroll | No dedicated tips-statement feature surfaced in research. Holds amounts, not the fair-allocation logic or the notice |
| **Tronc operators / accountants** (Troncmaster services, IRIS) | Professional governance of pooled tips | A professional-services price, aimed at multi-site restaurant groups, not a 6-person pub |

**The gap is the join.** The statement requires the *card tip total for a period* (which lives
in the POS) crossed with *who actually worked which shifts* (which lives in a WhatsApp rota
or the manager's head), run through a *fairness rule*, producing *per-employee statements
within 10 days* plus a retained record. Nobody owns both sides unless the venue runs
integrated POS clock-in — and most small ones don't.

That is a narrow, specific, unglamorous wedge. Which is what a good one looks like.

## The real risks, in order

1. **Someone who already holds the data adds a button.** BrightPay or Square could ship
   "generate tips statement" in a sprint and the product evaporates. This is the same
   platform-adjacency test that killed the poker ledger, and it is a genuine yellow flag.
   The one piece of evidence in your favour: the Act has been in force since December 2022
   and, as far as research shows, neither has. Four years of neglect is weak but real
   evidence that it sits below their roadmap threshold.
2. **Payroll and tax adjacency.** Tips are taxable through payroll; allocation sits next to
   PAYE/PRSI. Getting it wrong is worse than not offering it, and you have no accounting or
   legal budget. This is a milder version of the pattern that killed the felt — so apply the
   same discipline: **produce records, never move money and never give tax advice.** Do not
   become the troncmaster. Do not hold funds. Output documents.
3. **B2B sales needs your physical presence**, and you leave in January.
4. **The buyer is cutting costs**, so price must sit obviously below the fine.

## Suggestions

### 1. Build the free artefact generator first — a weekend, no sales required

A public web tool, no signup, that generates the two documents every covered business needs:
the **Tips and Gratuities Notice** for display, and a compliant **tips statement** template.
Free, forever.

Why this first: it ranks for "tips and gratuities notice Ireland", "tips statement template",
"do I have to display a tips notice" — searches made by a business owner at the exact moment
they are worried about compliance. It has no legal exposure, no payment surface and no sales
motion, so it runs unattended while you are abroad. And it is the cheapest possible way to
find out whether anyone is looking for this at all.

Caveat worth knowing: IBEC/SFA already publish a free notice template PDF. So the notice
alone is not a product — it is the doorway. The recurring statement is the product.

### 2. The paid product, built next summer

Manager inputs the period's card-tip total (typed, or pasted from a POS report) and who
worked which shifts, picks a share rule (equal, by hours, weighted by role), and the tool
produces per-employee statements inside the 10-day window, retains the records with an audit
trail, and versions the written policy. Deliberately *not* a rota product and *not* a payroll
product — it is the join between them.

Price €15-25/month per venue, annual option at a discount, framed against the €2,000 notice.
A hundred venues is €18-30k/year, which is a genuine side income — and also about a hundred
sales conversations, which is the actual work.

### 3. Do the validation this week, at work, for free

You have something no outside founder has: you work in one of these businesses. Ask your own
manager three questions:

1. Do staff get a written statement of tips within 10 days of each distribution?
2. Who produces it — you, the accountant, the POS, or nobody?
3. What would happen if a WRC inspector walked in on Tuesday?

Then ask five other Dublin pubs the same. If most answer "our accountant handles it" or "Square
does it", the idea is dead and it cost you an afternoon. If most answer "we don't really do
that", you have found a compliance gap with a €2,000 price tag and no product serving it.

**That conversation is worth more than any further research I can do from here**, and it is
the step that the poker project skipped.

### 4. What not to do

Don't start in the UK. The [Employment (Allocation of Tips) Act 2023](https://www.legislation.gov.uk/ukpga/2023/13/notes/division/2/index.htm)
(in force 1 October 2024) makes it a market ten times the size with the same problem — but it
already has established tronc operators, payroll integrations and accountancy practices
competing for it. Ireland's advantage is precisely that it is too small for them to bother
with and too obscure for foreign indie developers to find.

## Why this sequencing resolves your constraints

The tension named earlier was that the best-shaped idea needs a sales motion you cannot run
from Erasmus. Splitting it removes the conflict: the free generator is buildable in a weekend,
needs no selling, and accrues search traffic while you are away; the paid tool needs a summer
of in-person selling in Dublin, which is exactly what you will have. And if the free tool
attracts nobody in six months, you have your answer before writing the hard part.
