# Product brief — remote poker app

Full description of what this is, who it is for, how it makes money, and how it reaches
people. Written to support a decision on approach, so it states reasoning and marks
assumptions rather than asserting a finished plan.

Status: nothing built. No code, no technology chosen, nothing sunk.

---

## 1. In one line

A private poker table your friend group can play from anywhere, that also keeps the books —
tracking buy-ins, cash-outs, and who owes whom, across every session you play.

## 2. The problem

Two problems, and the second is the interesting one.

**Distance.** A recurring home game dies when people move. The group that played every
second Thursday in someone's kitchen loses a player to Dublin, one to London, one to a baby,
and the game quietly stops. There is no venue any more, and nobody wants to open an account
on a real-money site just to play with the same six people.

**The money is a mess.** This is the part existing free products handle badly. A home game
generates a surprising amount of bookkeeping: who bought in for how much, who rebought
twice, who left early and what they left with, who paid whom in cash on the night and who
said "get me next time". By the following morning it is four people's contradictory
memories and a group chat argument. Over a season it is completely untracked, so nobody
knows whether they are actually up or down — which is the single most interesting fact
about a recurring game.

Free tools solve distance. Nothing solves the second problem well, and the second problem is
the one that compounds.

## 3. Who it is for

**The host is the customer.** Every recurring game has exactly one person who organises it:
picks the night, chases people, remembers the rules, settles arguments, and fronts money
when someone is short. They are the only person with a reason to pay, the only person who
feels the bookkeeping pain, and the person whose effort determines whether the game exists.
The entire product should be designed around reducing their workload.

**Guests are not customers, they are the distribution.** A guest wants to be dealt in
within ten seconds of tapping a link, with no account, no download, and no friction. They
never pay. Their experience is what sells the product to the next host — see section 8.

Rough target group: 4-10 friends, playing anything from weekly to monthly, stakes low enough
that the game is social rather than serious. €20-€50 buy-ins, not €500.

## 4. What a session actually looks like

The full lifecycle, because this is the product:

1. **Host creates a table** — stakes, blinds, starting buy-in, seat count. Seconds, not a
   setup wizard.
2. **Host shares a link.** Guests tap it, type a name, and are seated. No signup. This step
   is make-or-break: every point of friction here loses a player and risks the night.
3. **Buy-ins recorded.** Each player's starting stack is logged as a buy-in against their
   name. No money moves — it is a record of what everyone has agreed they are in for.
4. **Play.** Deal, bet, fold, showdown. Server-authoritative, real-time across all seats.
   Mid-hand disconnects handled gracefully, because someone's phone will die every session
   and a hung hand ends the night.
5. **Rebuys and top-ups** logged as they happen, which is exactly what people forget.
6. **Cash out.** A player leaving records their final stack. The app knows their net for the
   session immediately.
7. **Settle-up.** At session end, the app produces the minimum set of transfers that squares
   everyone — not a matrix of who-owes-who, but the shortest list of payments. "Dave pays
   Sarah €35. Tom pays Sarah €20." Done.
8. **Money moves outside the app.** Revolut, cash, bank transfer, whatever the group uses.
   The app shows the number and steps back.
9. **The ledger updates.** The session folds into a running record for the group, so over
   weeks and months everyone knows their actual position.

Step 9 is the product's reason to exist. Steps 1-8 are table stakes that several free
products already offer.

## 5. Feature surface

**Table and play:** hold'em cash game; 4-10 seats; server-authoritative dealing; real-time
sync; disconnect and reconnect mid-hand; host controls (pause, kick, adjust); spectator mode
for the person who busted but is still on the call.

**Money tracking:** buy-ins, rebuys, top-ups, partial and full cash-outs; end-of-session
settle-up with minimised transfers; per-session net per player; running multi-session ledger
per group; export.

**Group:** persistent groups that survive between sessions; per-group history; stats and
leaderboards; light identity (a name and an avatar, not a full account).

**History:** hand history, replay, and searchable archive — genuinely useful for the
recurring argument about what someone had three weeks ago.

## 6. What this deliberately is not

Load-bearing, not marketing. These constrain the build:

- **Not a gambling operator.** No rake, no cut of any pot, no fee correlated with stakes,
  pot size, or volume.
- **Not a payment processor.** No wallet, no stored balance, no top-ups, no escrow, no funds
  held or routed. Ever.
- **Not a ledger of enforceable debt.** Buy-in and cash-out figures are user-entered records
  of what players say happened. The app does arithmetic on them. It does not guarantee,
  enforce, or owe anything, and its output is phrased as arithmetic, not as an invoice.
- **Not a casino app.** No house, no chips for sale, no play-money economy, no slots.

Background: Ireland's Gambling Regulation Act 2024 established the Gambling Regulatory
Authority (GRAI), which began licensing in 2026 with severe penalties for unlicensed
operation. Taking a rake would require a licence that is not realistically obtainable by a
solo developer. *This regulatory summary is the author's working understanding and has not
been independently verified — it should be confirmed with an Irish solicitor before launch.*

## 7. Monetisation

**Principle: only the host pays.** Poker is a 4-9 person coordination problem, so if any
seat can be blocked by a paywall the game does not happen and nobody pays anything. The
free/paid boundary therefore runs along **host capacity and data persistence**, never along
gameplay quality. A guest's experience at the felt must be identical on a free and a paid
table.

| | Free | Paid — $5/mo or $40/yr |
|---|---|---|
| Seats per table | 6 | 10 |
| Concurrent tables per host | 1 | unlimited |
| Guests | unlimited, free, no signup | same |
| Game integrity (shuffle, deal, turns, RNG) | full | full — never gated |
| Hold'em cash game | yes | yes |
| Omaha / short deck / tournament + blind timer | — | yes |
| Session settle-up | current session only | yes |
| **Multi-session running ledger** | locked but visible | yes |
| Hand history | current session, then discarded | full, replayable, exportable |
| Stats, leaderboards, group branding | — | yes |
| Cosmetics | minimal | full library included |

**The ledger is the paid hook.** It is the only feature whose value compounds with use —
one session's arithmetic is a calculator, but twelve weeks of standings is something a group
organises itself around, and it cannot be faked by a free tier. Show it to free hosts with
prior sessions locked but visible. The conversion moment is session two or three, when
someone asks where they ended up last week.

**Cosmetics** at $2-4 one-time, bundled into the subscription. Guest-facing avatars are the
only thing a guest ever buys, and they are purely decorative, so the host-pays rule holds.

**Deferred:** per-table fees (they tax the exact habit you want to build), in-game ads,
B2B/white-label to clubs and societies.

## 8. Outreach and distribution

### The unit of adoption is a group, not a person

You do not acquire users. You acquire **hosts**, and each host brings 4-9 people with them.
This changes what outreach means: a campaign that reaches 100 individuals is worth far less
than one that reaches 15 organisers. Everything below follows from that.

### The organic loop is unusually strong, and it is free to run

Every session puts the product in front of 4-9 people for two or three hours, with no
signup, no download, and no cost to them. The guest experience is not marketing adjacent to
the product — **it is the product, and it is the advertisement**. A guest who enjoys the
night and later wants to run their own game is a new host, acquired at zero cost.

This makes one metric more important than any other: **guest-to-host conversion** — what
fraction of guests eventually create a table of their own. If that number is healthy, growth
compounds without spend. If it is near zero, no amount of outreach fixes the product, and
that is the signal to stop and rethink rather than to market harder.

It also justifies the generous free tier commercially, not just philosophically. The free
tier is the acquisition channel.

### Paid advertising is probably closed — plan as if it is

**This is the most consequential outreach constraint, and it is not obvious.** Meta and
Google both restrict advertising for gambling and real-money gaming, typically requiring
per-country certification and a gambling licence. Their policies also reach "social casino"
apps that involve no real money at all. A product with the word poker in it, that deals real
cards among people playing for real stakes, is a strong candidate to be caught by those
policies regardless of the fact that it never touches funds.

The practical consequence: **assume paid acquisition is unavailable**, and treat any access
you do get as a bonus. This is not a minor channel loss — it removes the default startup
growth lever entirely and makes the organic loop above not merely preferable but the only
option. It also raises the stakes on app store distribution, since Apple and Google apply
similarly strict rules to real-money and gambling apps, which is a direct argument for
web-first rather than native.

*Unverified — ad platform policies change and are applied inconsistently. Confirm against
current Meta, Google, and app store policy before assuming either way. But build the plan
so it survives the restrictive case.*

### Where the first hosts come from

In rough priority order:

1. **Your own game, first.** One real group, played to session ten. Not a launch — a
   working product with real users you can watch. Every serious flaw in the settle-up flow
   will surface by session three, and fixing them before anyone else sees the product is
   enormously cheaper than after.
2. **College societies.** Poker societies exist at most universities, are trivially
   reachable, run recurring games, and have a committee member whose actual job is
   organising them — a host persona concentrated and pre-identified. A society running
   weekly games is worth more than a hundred individual signups, and is also the natural
   first test of whether anyone would pay.
3. **Existing home-game communities.** Subreddits and Discords for home poker are full of
   organisers discussing exactly the bookkeeping problem in section 2. Participate as
   someone who runs a game and built a thing, not as a marketer; these communities detect
   and reject promotion instantly.
4. **Groups already frustrated with the alternatives.** People using a free table product
   plus a spreadsheet plus a group chat have already articulated the need. They are the
   easiest conversion because you are replacing three tools with one.
5. **Content on the long tail.** "Poker settle-up calculator", "who owes who home game",
   "how to run a home poker game" — low-competition search terms where the person searching
   is definitionally an organiser. Slow, cheap, compounds, and unaffected by ad restrictions.

### Sequencing

Do not launch. Get one group to session ten, then five groups, then fifty. The failure mode
for this product is not obscurity, it is a group trying it once, hitting a mid-hand
disconnect or a settle-up that disagrees with the cash on the table, and never returning —
and a wide launch converts that fixable bug into a permanently burned audience.

## 9. Metrics that matter

In order:

1. **Group retention** — does a group play a second session, and a fifth? Everything depends
   on this. A group that plays once is a failure regardless of how it felt on the night.
2. **Guest-to-host conversion** — the growth engine, per section 8.
3. **Sessions per group per month** — habit strength, and the best predictor of willingness
   to pay.
4. **Free-to-paid host conversion**, and specifically whether it clusters at session two or
   three as the ledger theory predicts. If it does not, the paid hook is wrong.
5. Session completion rate — what fraction of started sessions reach a clean settle-up
   rather than collapsing mid-game. This is the technical quality bar.

Deliberately *not* daily active users. This is a product used for three hours a fortnight by
design, and optimising for daily engagement would actively damage it.

## 10. Principal risks

- **The wedge may be too thin.** Free products already do remote tables; spreadsheets
  already do arithmetic. The bet is that combining them for recurring groups is worth paying
  for. Unproven, and the fastest thing to test.
- **Single-payer fragility.** All revenue concentrates on the one person per group who is
  least replaceable. If a host churns, the group churns and the revenue goes with it.
- **Legal footing is thinner than it looks.** The settle-up separation is reasonable but not
  tested. Needs a qualified Irish opinion before any money is taken.
- **Distribution may be structurally constrained** by the advertising and app store policies
  in section 8, leaving only slow organic channels.
- **Real-time multiplayer is genuinely hard**, and disconnect handling — the least glamorous
  part — determines whether groups come back.

## 11. Open questions

- Web-first or native? Section 8 argues strongly for web; needs confirming against app store
  policy.
- Is $5/mo right for a group that already plays for free, and would a per-group price
  split among players convert better than a host-only subscription?
- Should the settle-up deep-link into Revolut with an amount prefilled? Convenient and
  common in bill-splitting apps, but it edges toward facilitating payment for gambling.
  Copy-to-clipboard is the safe version and costs little.
- Does the free tier's 6-seat cap bite too early, pushing hosts to free competitors before
  they ever see the ledger?
