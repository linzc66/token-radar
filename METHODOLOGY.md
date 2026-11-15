# How this radar is built

This note explains, in plain words, how the entry decides which protocols
belong on the board, how it scores them, and what the numbers mean.

## Where the numbers come from

- Every figure the program uses comes from one sealed snapshot file.
- That snapshot was taken from DefiLlama's public protocol data.
- It holds 758 protocols whose total value locked is at least five million dollars.
- Each protocol in it carries a slug, a display name, a category, and a chain list.
- It also carries total value locked, the seven-day change, and a market cap when one exists.
- Protocols without a token carry no market cap, no CoinGecko id, and no symbol.
- The snapshot also records the date it was taken, so ages can be computed from it.
- Nothing is fetched from the network while the program runs.
- The program reads the snapshot once and derives everything from those fields.
- Because the input is fixed, the same snapshot always produces the same board.

## Which protocols can appear

- A protocol counts as rankable when DefiLlama records no token for it at all.
- Rankable also means it is not a wrapped, staked, or bridged product.
- Bridge, liquid staking, liquid restaking, restaked BTC, and exchange categories are out.
- Names containing the whole word wrapped, staked, or staking are out as well.
- Names that start with an exchange name are out, and versioned names are out too.
- Those filters leave 198 rankable protocols in this snapshot.
- Forty of them form the watchlist the bounty defines.
- The watchlist needs total value locked of at least fifty million dollars.
- It also needs no token, and it must pass the same product filters.
- The other 158 rankable protocols sit below the watchlist floor.
- They are still ranked, because a small protocol can launch a large token.
- Twenty-four protocols that already have a live token are set aside.
- They appear on a separate tab of the page and never enter the ranking.

## What implied value means

- Implied value is the program's guess at what a future token might be worth.
- It starts from total value locked and applies a base multiple of one quarter.
- Very large protocols get a smaller multiple, because size dampens the ratio.
- The dampening uses the hundredth root of the size ratio, floored at 0.55.
- A protocol growing over the last seven days gets a lift of up to half its growth.
- A protocol shrinking gets a drag instead, but the drag is capped at sixty percent down.
- Older protocols get more credit, up to a forty-five percent maturity bonus.
- Maturity is measured in days since listing, capped at four years.
- A protocol nobody knows the listing date for is treated as one year old.
- Each extra chain adds four percent, up to five extra chains.
- The result is rounded to a whole dollar amount.
- The figure is a model output, not a price and not a promise.
- It never says whether a token will launch, or when one might appear.

## How the signal is chosen

- The signal compares implied value with total value locked.
- That ratio is called value density in the code.
- A density of 0.20 or higher earns a buy signal.
- A density from 0.15 up to 0.20 earns a watch signal.
- Anything below 0.15 earns an avoid signal.
- The board holds 42 buy, 109 watch, and 47 avoid signals.
- The top three rows by implied value are all avoid on density.
- That is expected: the largest vaults are rich in locked value already.
- Density rewards smaller protocols whose locked value looks cheap.
- The signal is a screening label, not investment advice.

## How the rows are ordered

- Rows sort by implied value, highest first.
- Ties break by confidence, then by slug in alphabetical order.
- Rank one is Steakhouse Financial at about three hundred fifty-seven million.
- Rank two is Sentora Curator at about three hundred twenty-one million.
- Rank three is Gauntlet at about two hundred thirty-one million.
- The board's combined locked value is about twenty point seven billion dollars.
- The watchlist's combined locked value is about twelve point nine billion dollars.
- The watchlist's median seven-day change is about minus three point three percent.
- The watchlist's median age is about one point four years.
- Only three of the forty watchlist protocols earn a buy signal.

## What each farm plan covers

- Every ranked protocol gets a seven-step plan on the page.
- The steps are built from its category, its chains, its size, and its age.
- Step one says to use a fresh wallet holding only the farming funds.
- Step two suggests a first deposit of about one hundred fifty dollars.
- Step three says to do one qualifying action each week.
- Step four says to hold the position for at least thirty days.
- Step five says to claim only from links the protocol itself publishes.
- Step six says to unwind half if locked value falls by a fifth in a week.
- Step seven says to keep a written log of wallets, dates, and transactions.
- Each step names a rough cost in gas or capital and a rough time.
- The plans are generic guidance, not a guarantee of any reward.

## What the page shows

- The page opens with the board's headline facts.
- Ten watchlist cards summarise the strongest watchlist names.
- A bar chart shows the top ten by implied value.
- Red dots on the chart mark each protocol's seven-day growth.
- The table lists every ranked protocol with its key figures.
- The table sorts by rank, implied value, name, locked value, growth, or age.
- A search box and a category filter narrow the table.
- Top 25, Top 50, and Top 100 buttons limit how many rows show.
- Tabs switch between pre-token protocols and live-token ones.
- Clicking a row opens its detail view.
- The detail view shows why the protocol ranks where it does.
- It shows every multiplier that went into its implied value.
- It recomputes the value live so the reader can check the arithmetic.
- It lists the protocol's seven-step farm plan in full.
- Sliders let the reader try other base multiples and weights.
- The sliders are exploratory only and never change the submitted board.
- A methodology section states the formula and its caveats.

## Limits of this radar

- The snapshot is a single point in time and goes stale quickly.
- A protocol can launch a token the day after the snapshot was taken.
- DefiLlama recording no token is not proof that none exists.
- Locked value can be inflated by incentives or by a few large depositors.
- Seven-day growth is noisy and says little about the next month.
- Chain count is a rough proxy for reach, not a measure of quality.
- The model has no view of a protocol's team, audits, or governance.
- It has no view of points programs, vesting, or unlock schedules.
- Nothing here is investment advice, and nothing here is a launch prediction.
- The board is a screening tool for further research, nothing more.
