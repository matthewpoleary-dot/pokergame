# Audit prompt — remote poker app ("settle-up" model)

> Paste everything below the line into the reviewing model/person.
> Fill the `[FILL IN]` fields first — the audit is only as good as those.

---

You are auditing an early-stage product plan. Nothing has been built yet: the repository
contains planning documents and no application code. Your job is to pressure-test the plan
and recommend the best approach, not to validate it. Assume the author would rather hear a
hard problem now than discover it after three months of building.

## 1. The product

A remote poker app for friends. People invite each other to a private table and play from
anywhere, rather than needing to be in the same room. The core loop is: deal cards, manage
the pot, take turns, sync state in real time across players.

The differentiator is not the poker engine — plenty exist. It is that the app handles the
**social accounting** of a recurring home game: who bought in for what, who cashed out for
what, and who therefore owes whom, tracked across sessions over months.

## 2. The hard constraint that shapes everything

The original plan was to take a 1-2% rake off every pot, like a real poker room. **That is
ruled out** and is not up for reconsideration in this audit.

Reason: it would make the author a gambling operator under Irish law rather than someone
hosting a private game. Ireland's Gambling Regulatory Authority (GRAI), created under the
Gambling Regulation Act 2024, has been issuing licences since February 2026, with severe
penalties for unlicensed operation. There is also unresolved uncertainty about whether poker
falls under the Act's proposed €10 maximum bet / €3,000 maximum win caps — this was still
open as of a public consultation in 2026. Obtaining a gambling licence is not realistic for
a solo developer.

**Verify this before relying on it.** The regulatory description above is the author's
working understanding as of September 2026 and has not been independently confirmed against
primary sources. Treat it as a claim to check, not a given — if the licensing timeline, the
stake and prize caps, or their application to poker differ from what is stated, say so, and
let the corrected facts drive your answer to section 5A.

The pivot is a **"settle-up" model**:

- Players record buy-ins and cash-outs in the app.
- The app calculates who owes whom at the end of a session, and cumulatively across sessions.
- **Actual money moves entirely outside the app** — Revolut, Venmo, bank transfer, cash.
- The app never holds, escrows, routes, or takes a cut of any funds.
- Positioning: friends doing their own private game's arithmetic, not an operator running a
  gambling business. Comparable to existing home-game tracker apps.

Derived build constraints, all of which are load-bearing:

- No wallet, no stored balance, no "top up", no escrow.
- No fee tied to pot size, stake level, buy-in amount, or session volume. Revenue must be
  mathematically uncorrelated with what is wagered.
- Buy-in and cash-out figures are **user-entered records** of what players say happened. The
  app performs arithmetic on them. It does not enforce, guarantee, or owe anything.
- Settle-up output is phrased as a statement of arithmetic, not an invoice or a debt.

## 3. The monetization plan as it currently stands

**Principle: only the host pays. Guests join free, forever, with no signup beyond a name.**
Rationale: poker is a 4-9 person coordination problem, so if any seat can be blocked by a
paywall, the game does not happen and nobody pays. The free/paid line therefore runs along
host capacity and data persistence, never along gameplay quality — a guest's experience at
the felt must be identical on free and paid tables.

| | Free | Paid — $5/mo or $40/yr |
|---|---|---|
| Seats per table | 6 | 10 |
| Concurrent tables per host | 1 | unlimited |
| Guests | unlimited, free | same |
| Game integrity (shuffle, deal, turn order, RNG) | full | full — never gated |
| Hold'em cash game | yes | yes |
| Omaha / short deck / tournament + blind timer | — | yes |
| Session settle-up | current session only | yes |
| **Multi-session running ledger** | locked but visible | yes |
| Hand history | current session, then discarded | full, replayable, exportable |
| Stats, leaderboards, group branding | — | yes |
| Cosmetics (felts, card backs, avatars) | minimal | full library included |

Supporting bets: cosmetics sold one-time at $2-4 and bundled free into the subscription.
The multi-session ledger is treated as the primary paid hook, on the theory that it is the
only feature whose value compounds with use, and that the conversion moment is session two
or three when someone asks "where did I end up last week?"

Explicitly deferred: per-table hosting fees, in-game advertising, and B2B/white-label sales
to clubs and societies.

## 4. Context about the author and the project

- Solo developer, based in Ireland. Building this primarily [FILL IN: as a side project /
  as a business / as a portfolio piece / other].
- Technical background: [FILL IN: languages and frameworks you are already fluent in, and
  whether you have shipped and operated a production web app before].
- Time available: [FILL IN: hours per week, and target date for a first playable version].
- Budget for infrastructure and services: [FILL IN: monthly ceiling].
- Initial audience: [FILL IN: e.g. one specific friend group of N people, a college society,
  open public launch].
- Target scale if it works: [FILL IN: a handful of groups vs thousands of concurrent tables].
- Appetite for legal spend: [FILL IN: can you afford a one-off opinion from an Irish
  solicitor, roughly what budget].
- No technology choices have been made yet. No code exists. Nothing is sunk.

## 5. What to audit

Work through all five areas. Do not merely summarise the plan back.

**A. Legal and regulatory.** Does the settle-up model actually achieve the separation it
claims under Irish law and the Gambling Regulation Act 2024, or is that separation thinner
than assumed? Specifically: does dealing real cards for real stakes while tracking real
debts constitute facilitating gambling even with no funds touched and no rake taken? Does
charging a subscription to the host change the analysis versus being entirely free? What
about app store policies (Apple, Google) on real-money gambling and social casino apps,
which are stricter than national law and are a separate gate? What about GDPR obligations
given the app would hold records of individuals' gambling losses, which is sensitive in
practice even if not a special category under Article 9? Flag anything that needs a
qualified Irish solicitor rather than a best guess, and rank those by urgency.

**B. The monetization design.** Is "only the host pays" the right axis, or does it
concentrate all revenue on the single least replaceable person in each group — and what
happens when that host churns? Is the multi-session ledger genuinely the strongest paid
hook, or is it the feature most easily replaced by a free spreadsheet? Is $5/mo right for
this audience? Is the 6-vs-10 seat split a real constraint or an irritant that pushes hosts
to free competitors? Name the single weakest assumption in the table above.

**C. Competitive reality.** PokerNow and similar products already let people run free
private tables with no signup. Home-game tracker apps already exist. Is there a real wedge
here, or is this a worse version of two existing free things? If there is a wedge, say
precisely what it is in one sentence. If there is not, say so plainly.

**D. Technical approach.** Recommend a concrete stack and architecture for real-time
multiplayer card state across 4-10 clients, given a solo developer and the constraints
above. Address at minimum: server-authoritative state and why card dealing cannot be
client-trusted; how RNG and shuffling should work so players can believe the game is fair,
including whether provable/verifiable shuffling is worth the complexity at this scale;
real-time transport choice; reconnection and disconnect handling mid-hand, which is the
single most common failure mode in home-game apps; persistence for the ledger; hosting cost
at idle, since most tables will be empty most of the time. Web-only versus native is an open
question — recommend one and justify it, factoring in the app store policy issue from A.

**E. Scope.** Define the smallest version that is genuinely worth playing with one real
friend group, and say explicitly what to cut to reach it. Then say what the second version
adds. Be aggressive about cutting.

## 6. How to answer

- Open with the single highest-risk item across all five areas, and say whether you would
  proceed, proceed with modifications, or not build this at all.
- Then take the areas in order. Be specific and concrete; prefer a firm recommendation with
  its reasoning over a menu of options.
- Where the plan is sound, say so briefly and move on — do not pad.
- Where you are uncertain or a claim depends on facts you cannot verify (particularly Irish
  regulatory specifics and current app store policy), mark it clearly as such rather than
  asserting it. Distinguish what you know from what you are inferring.
- End with the three things the author should do first, in order.
