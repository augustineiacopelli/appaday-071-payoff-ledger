# AppADay 071 — Payoff Ledger

**Compare loan payoff strategies on one chart, including the option of investing the money instead.**

Live: https://augustineiacopelli.github.io/appaday-071-payoff-ledger/
Portfolio: https://augustineiacopelli.github.io/appaday/

Category: **D — Data Viz and Dashboards** · Shipped 2026-07-17

---

## What it does

Almost every amortization calculator on the web shows you one loan, offers exactly one flavor of extra payment, and stops. Payoff Ledger treats a scenario as a first-class object — principal, rate, term, and an extra-payment strategy — and lets you stack up to six of them on the same axes. The gap between two curves at any month is the answer to "what does a quarter point actually cost me," read as distance rather than as two numbers you have to hold in your head.

It also asks the question the other calculators skip. If those extra dollars had gone into an investment account instead of into the loan, would you be further ahead? At your assumed return, and at what month does the crossover happen?

## Views

**Balance** — remaining principal for every scenario, plotted together. Where a curve hits zero is the payoff date.

**Interest paid** — cumulative interest to date. The curves never come back down; the flat part is where the loan is gone and the meter has stopped.

**Payment split** — for one scenario at a time, a stacked area showing where each monthly payment actually goes: interest on the bottom, principal above it, extra principal on top. A dashed red line marks the first month where more of the payment builds equity than pays the bank. On the default $350,000 at 6.75% that lands at month 238, roughly twenty years into a thirty-year note.

**Pay down vs. invest** — the opportunity-cost view, described below.

## Extra payment strategies

Five, against a single loan, so scenarios can differ by strategy rather than only by rate.

**No extra payments** — the baseline schedule.
**Extra every month** — a fixed recurring amount added to principal.
**One-time lump sum** — an amount applied at a chosen month.
**Lump sum every year** — an annual amount applied in a chosen month of the year, for a bonus or a tax refund.
**Biweekly half-payments** — half the payment every two weeks lands 26 half-payments a year, which is one extra full payment. Modeled as one twelfth of the payment as extra principal each month, and the app says so on screen rather than pretending to simulate discrete fortnightly cycles.

## The opportunity-cost model

Both paths spend an identical amount of cash every single month. Nothing is being compared against a strawman that quietly spends less.

**Path A, pay the loan down.** The extra goes to principal. Once the loan is gone, the entire freed-up outlay — base payment plus extra — goes into the investment account for the remainder of the original term.

**Path B, invest the difference.** The base payment goes to the loan, which runs its full original term. The extra goes into the investment account from month one. After the loan retires on schedule, the whole outlay is invested.

Net position at any month is investments minus remaining loan balance. The chart plots both, and marks the month paying down pulls ahead if it ever does.

Returns compound at a steady geometric monthly rate derived from the annual assumption, `(1 + r)^(1/12) − 1`, which is more defensible than dividing by twelve but is still a fiction no real market delivers. Taxes, the mortgage interest deduction, capital gains, fees, and sequence-of-returns risk are all ignored. The point of the view is the shape and the crossover, not a number to take to a lender.

At the default 7% assumption against a 6.75% loan, investing finishes about $1,800 ahead across thirty years — close enough to a coin flip that the honest answer is "it depends." Drag the return slider to 5% and paying down takes the lead immediately. Push it to 9% and the gap opens wide. That slider is the whole argument in one gesture.

## Also in there

Hover or drag anywhere on the chart to read every plotted series at that month. The summary table shows payment, payoff term, total interest, and interest and time saved against whichever scenario sits first in the list. The export button writes the full schedule of the focused scenario to CSV — month, payment, interest, principal, extra principal, balance, cumulative interest — so you can check the arithmetic in Excel. Scenarios persist in `localStorage`.

A loan whose payment does not cover its interest is caught and labeled rather than looped over forever. A zero-percent rate is handled without dividing by zero.

## Deliberately left out

PMI drop-off at 80% LTV, escrow separated from principal and interest, day-count conventions, and inflation-adjusted real dollars. Each is defensible; each drags in edge cases that would have blown the ninety-minute budget for marginal insight.

## Build

Single file. Vanilla HTML, CSS, and JavaScript. No build step, no framework, no dependencies beyond Google Fonts. The chart is hand-drawn SVG. Runs from `file://`.

Design is a green accounting ledger: ruled paper, a red margin rule down the left of every panel and down the chart's y-axis, Zilla Slab for the masthead, IBM Plex Sans for text, and IBM Plex Mono for every number so the columns align the way they would on a real schedule.

## Not financial advice

It's a model. Check the math before you act on it.
