# Monetization: free vs paid

**Model:** settle-up tracker + play. No rake, no funds held, no cut of pot size.
See "Legal guardrails" at the bottom — these constrain the feature list, not just the marketing.

## The one rule that shapes everything

**Only the host pays. Guests always join free, forever, with no account required beyond a name.**

Poker is a 4-9 person coordination problem. If any seat can be blocked by a paywall, the
game doesn't happen and nobody pays. So the free/paid line runs along *host capacity and
persistence*, never along *gameplay quality*. A guest at a paid table and a guest at a free
table should have an identical experience at the felt.

Corollary: the free tier has to be good enough to run a real Friday game start to finish.
The paid tier sells the *recurring* game, not the first one.

## Where the line goes

| | Free | Paid — "Home Game" $5/mo (or $40/yr) |
|---|---|---|
| Seats at a table | up to 6 | up to 10 |
| Concurrent tables per host | 1 | unlimited |
| Guests | unlimited, free, no signup | same |
| Game integrity (shuffle, deal, turn order, RNG) | full | full — never gated |
| Texas hold'em cash game | yes | yes |
| Omaha / short deck / other variants | — | yes |
| Tournament mode + blind-level timer | — | yes |
| End-of-session settle-up ("who owes whom") | yes, current session | yes |
| **Multi-session ledger** (running tab across weeks) | locked, but visible | yes |
| Hand history | current session, then discarded | full, searchable, replayable, exportable |
| Stats + group leaderboards | — | yes |
| Group identity (name, logo, custom felt) | — | yes |
| Cosmetics | 1 felt, 1 card back | full library included |
| Ads | none in-game; light on dashboard only | none |

## Why these specific lines

**6 seats free / 10 paid.** Six covers most casual home games, so the free tier isn't a
demo. Ten is the upgrade trigger for the group that actually grew — and that group has a
host who's already invested.

**The multi-session ledger is the product.** It's the single strongest paid feature, because
it's the only one whose value *compounds with use*. One session's maths is a calculator.
Twelve weeks of "Dave is down €140 overall" is a thing a group organises itself around, and
it's exactly what the free tier can't fake. Show the ledger screen to free hosts with
history beyond the current session locked — not hidden. The upgrade prompt writes itself at
session two or three, when someone asks "wait, where did I end up last week?"

**Never gate anything that affects fairness or the feel of a hand.** No faster deals for
subscribers, no "premium" RNG, no ad break mid-hand, no timer pressure on free tables. The
moment the game feels degraded, the host switches to PokerNow and a group chat, which is
free and works.

**Cosmetics are one-time purchases ($2-4), bundled free into the subscription.** They give
non-subscribing hosts something to spend on and subscribers a reason to feel the sub is
good value. Sell to the host (table felt, card backs) and to guests (avatars) — guest
cosmetics are the only thing a guest ever pays for, and they're purely decorative, so
they don't violate the rule above.

## Deliberately not doing

- **Per-table hosting fee.** Taxes the exact behaviour we want (more games = more habit =
  more subscriptions). Keep as a fallback only if subscription conversion stalls.
- **Ads in-game.** Cheapens the one surface that has to feel good. Dashboard only, and only
  if there's ever volume worth selling.
- **B2B / white-label.** Right thing eventually, wrong thing now — it's a sales motion, not
  a product feature, and it needs the recurring-group features built first anyway. Revisit
  once there are groups running 10+ sessions.

## Legal guardrails (constrain the build, not just the copy)

Money must never touch the app:

- No holding, escrowing, or transferring funds. No wallet, no balance, no "top up".
- No fee tied to pot size, stake level, buy-in amount, or session volume. Fees are flat and
  time-based, so revenue is uncorrelated with what's wagered.
- Buy-ins and cash-outs are **user-entered numbers**, a record of what players tell the app.
  The app does arithmetic on them. It does not owe anyone anything or enforce anything.
- Settle-up output is a statement of maths, phrased as such. Not an invoice, not a debt.
- **Open question before shipping the ledger:** deep-linking a settle-up line into
  Revolut/Venmo with the amount prefilled is convenient and is what Splitwise-style apps do,
  but it moves closer to facilitating payment for gambling. Probably fine (no funds held, no
  cut), but worth a quick opinion from someone Irish-law-qualified before it ships. Plain
  copy-to-clipboard of "Dave owes you €35" is the safe version and costs almost nothing in UX.

Context: Ireland's Gambling Regulation Act 2024 / GRAI licensing regime. Taking a cut of
real-money pots would make the operator a licensee. Flat subscription for a tracker and a
card-dealing UI is a different thing — but only as long as every bullet above holds.
