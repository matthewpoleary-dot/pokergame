# Market research — does the ledger product work?

Date: 2026-09-20. Method: web search only. **Confidence caveat:** the App Store
(`apps.apple.com`), the products' own sites (`pokersquad.app`), and the home-game host
forums were all blocked by this session's network egress policy, so nothing below comes from
using the products or reading their reviews directly. It rests on search-result summaries of
those pages. Treat specific prices and feature claims as indicative and verify by installing
the apps; treat the aggregate picture as reliable, because many independent sources describe
the same features.

## Verdict

**The ledger does not work as a business in the shape we specified.** Not because the idea is
wrong — because it has been independently discovered by roughly fifteen teams, and the single
most important one is the bank your users already have.

The claimed wedge was one word: *multi-session*. A running record for a group, carried across
sessions. That wedge does not survive contact with the market. It exists in at least four
places already, three of them free.

## What already exists

### 1. Revolut has it natively — this is the finding that matters

Revolut ships two relevant features: **Split Bill**, which divides a payment and sends each
person a request they accept in one tap, and **Group Bills**, which *tracks shared expenses
across a group over time*. Available in Ireland and 40-plus European countries.

That is the multi-session group ledger, inside the app every Irish user already has, with the
payments built in — the one part our plan deliberately could not touch for legal reasons.
Competing against a free feature of a bank, on the bank's own turf, with a product that
stops short of the payment, is not a winnable position.

### 2. PokerSquad already does the poker-specific version

Its own description: **live leaderboards to "see who's running hot across all your
sessions"**, every game saved automatically, "create your poker squad, invite your regulars,
keep your crew organized, everyone's stats in one place." Free for unlimited games up to 5
players; Pro for unlimited players.

That is v1 plus most of v2 from our scope document, already shipped. Note also that it gates
its free tier on player count — the same mistake the audit talked us out of.

### 3. The PokerNow-integration idea is already built, free, several times over

The audit's sharpest suggestion was to be the layer that remembers on top of wherever people
already play. That layer exists as free browser extensions and open-source tools:

- **Poker Now Ledger** (Chrome extension) — snapshots a game's ledger, stores it locally,
  aggregates across games, and identifies players who changed name or device.
- **PokerNow HUD** — persistent player profiles whose "full history follows them across
  sessions even when PokerNow assigns a new player ID."
- **pokernow-tracker** — a persistent queryable database keyed to stable player identity.
- At least one such tool advertises "persistent groups — recurring home-game circles,
  carry-over balances, and group roles (organizers, regulars, guests)," which is our v2
  feature list almost verbatim.

Useful detail: PokerNow deletes hand histories after five days, which is a real gap — but
free tools already fill it.

### 4. The arithmetic is free and open source

Multiple single-file web apps do settle-up with no account and no backend, e.g.
`calvinkim85/home-poker-ledger` — "who pays whom in the fewest payments. Free, no account,
runs in the browser." One full-stack project (`officiallywily/poker-ledger`) enforces that
**"sessions cannot close until the books balance."**

### 5. The consumer tracker category is saturated

Distinct home-game tracker apps surfaced in a single search pass: Poker Ledger Tracker, Poker
Ledger Pro, PokerSquad, ChipUp, PokerPot, PokerTally, Pokertally (a second, different app of
nearly the same name), PROker, Poker Homie, Poker Note+, Chip Stack, Poker Boss, Poker Stats
Tracker, plus the open-source ones. Most have recent App Store IDs, i.e. shipped within
roughly the last year.

Fourteen products with near-identical descriptions is not a gap in the market. It is a gap
that fourteen people noticed at the same time.

### 6. Above it, a paid club/league tier that is genuinely monetising

- **Poker Hawk** — from $14.99/mo; club layer with RSVPs, check-in, leaderboards, lifetime
  stats.
- **The Club House** — free tier, explicitly built around "how independent organizers
  actually grow — from a cleaner home game to a recurring night to multiple tables to a
  league," tracking results across events with standings, season progress and club history.
- **LynxPoker**, **Home Poker System**, **Poker League Franchise** — similar.
- One product prices at free up to 9 players, $7/mo to 20, $29/mo unlimited plus commercial
  use. **Poker Ledger Tracker** asks $29.99/mo or $249.99/yr.

Two readings, both true. Good news: people *do* pay for this, at 3-6x the €5/mo we proposed,
which means the willingness-to-pay assumption was too pessimistic rather than too
optimistic. Bad news: the segment that pays is clubs and leagues — a sales motion against
funded competitors — not friend groups.

## So how is it optimisable?

Optimisation is the wrong frame here, and worth saying plainly: you optimise a product that
has users and a position. The blocker is not conversion rate, pricing or onboarding — it is
that every version of this product already exists, and the best-distributed one is a bank
feature. No amount of tuning moves that.

For completeness, the levers that would exist *if* the position were defensible:

1. **Books-must-balance validation.** Total buy-ins must equal total cash-outs, and a session
   that does not reconcile is an error caught on the night rather than an argument the next
   morning. Revolut's generic Group Bills cannot do this because it does not know what a
   rebuy or a chip count is. This is the one genuinely poker-shaped piece of logic in the
   whole product.
2. **Disputes, corrections and an audit trail.** "Dave says he bought in for 20, not 30",
   three weeks later, without destroying the history. Nothing in the research surfaced this
   in any competitor, and the audit reached the same conclusion independently. It is the one
   remaining unclaimed patch of ground — and it is a feature, not a company.
3. **Revolut-native settle in Europe.** Every paid competitor is US-centric (Venmo, Zelle).
   But this is exactly the payment deep-link the audit told us not to build, and it puts you
   head-on against Revolut's own feature. Both reasons point the same way: don't.

## What this means

The poker space is closed to this project on both sides. The table is legally blocked by
s.67 of the Gambling Regulation Act 2024 — you cannot license it and cannot safely charge for
it. The books are commercially saturated — fourteen apps, free open-source equivalents, free
browser extensions, a paid club tier held by better-resourced products, and Revolut.

That is a genuinely useful result rather than a failure. It cost an hour of searching instead
of a term of building, which is precisely what the audit's first recommendation was for.

**What is still worth doing:** build the ledger for your own game, free, in a weekend or two.
It is real, it will get used, it teaches the stack, and the append-only event schema is a
good thing to have written. Just do it knowing it is a tool for your friends and a portfolio
piece, not a startup.

**What to verify before believing any of this:** install PokerSquad and open Revolut's Group
Bills, and run your last three sessions through both. Those are the two products that
directly occupy the position, and they are the two I could not reach from here. If both turn
out to be genuinely bad at a recurring poker game — possible, since neither is built for one
— the picture improves. That is a single evening, and it is the only step that should change
this verdict.
