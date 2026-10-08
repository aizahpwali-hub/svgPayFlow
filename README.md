# PayFlow

PayFlow is a demo digital wallet. Send payments by email, watch balances update in real time and track every transaction from one dashboard.

No real money moves. All data lives in your browser, which makes the project easy to run, fork and demo.

## Features

- Open a wallet with an email address and start with $1,000 of play money
- Send payments to any other wallet by email, with an optional note
- Balances update live, including across browser tabs
- Transaction history with Sent and Received filters and search
- Seven day activity chart for money in and money out
- Input validation for amounts, emails, self payments and overdrafts
- Keyboard accessible, responsive down to phone width, respects reduced motion

## Try the live update

Open the app in two browser tabs and sign in as two different people, for example Ayesha Khan in one tab and a new wallet in the other. Send a payment from one tab and the other tab updates without a refresh.

This works because the shared ledger lives in `localStorage` and each tab keeps its own signed in user in `sessionStorage`.

## Tech stack

- React 19 and TypeScript
- Vite
- Vitest and Testing Library
- Plain CSS with design tokens, Sora and Inter fonts bundled through Fontsource

## Getting started

You need Node.js 20 or newer.

```bash
npm install
npm run dev
```

The app opens at http://localhost:5173.

### Scripts

| Script | What it does |
| --- | --- |
| `npm run dev` | Start the dev server |
| `npm run build` | Type check and create a production build in `dist` |
| `npm run preview` | Serve the production build locally |
| `npm run typecheck` | Run the TypeScript compiler without emitting files |
| `npm test` | Run unit and UI tests |

## Project structure

```
src/
  lib/
    ledger.ts        Wallet and payment logic, storage backed
    ledger.test.ts   Unit tests for the ledger
    money.ts         Currency formatting and amount parsing
  components/
    AuthScreen.tsx   Sign in and wallet creation
    Dashboard.tsx    Balance, totals and page layout
    SendForm.tsx     Payment form
    ActivityChart.tsx
    TransactionList.tsx
  hooks.ts           Ledger store hook, live balance animation
  App.tsx
  App.test.tsx       UI flow tests
```

## Customising

- **Currency:** change `CURRENCY` in `src/lib/money.ts`, for example to `PKR`.
- **Starting balance and top up:** edit `STARTING_BALANCE` and `TOP_UP_AMOUNT` in `src/lib/ledger.ts`.
- **Demo contacts:** edit `seedLedger` in `src/lib/ledger.ts`.
- **Colors and fonts:** all design tokens are at the top of `src/styles.css`.

## Turning it into a real product

`src/lib/ledger.ts` is the only module that knows where data is stored. To connect a real backend, keep the same methods (`signIn`, `send`, `addFunds`, `signOut`) and replace the storage calls with API requests. Real payments also need server side authentication, authorization checks and an audited ledger. Do not trust balances calculated in the browser.

## Deploy to GitHub Pages

1. Push this repository to GitHub.
2. In the repository, open Settings, then Pages, and set Source to GitHub Actions.
3. Push to `main`. The workflow in `.github/workflows/deploy.yml` runs the tests, builds the app and publishes it.

The build uses relative asset paths, so it works under any repository name.

## License

MIT, see [LICENSE](LICENSE).
