# Performance Analyzer

**Inspect web performance, compare analyses, and export a report.**

A Next.js dashboard that combines a server-side Google PageSpeed Insights integration with metric breakdowns, comparison views, saved history, and PDF/JSON/CSV exports.

## What it includes

- URL analysis through `/api/pagespeed`, with the Google API key kept on the server.
- Performance metric cards, resource views, and comparison screens.
- Browser-persisted analysis history using Zustand.
- Performance budgets and export controls.
- Local, rule-based optimization suggestions by default.

The dashboard starts with **sample data** so the interface can be explored without an API key. New URL analyses require your own PageSpeed Insights API key. Sample charts and derived component estimates are illustrative; they are not independently measured results.

## Run locally

Use Node.js 22+ and npm.

```bash
git clone https://github.com/pranjal9044/performance-analysis-app.git
cd performance-analysis-app
npm ci
cp .env.example .env.local
npm run dev
```

Set `PAGESPEED_API_KEY` in `.env.local` to enable live URL analysis. Never commit the key. Open http://localhost:3000.

```bash
npm run build
npm start
```

## Architecture

| Layer | Implementation |
| --- | --- |
| Application | Next.js 16 App Router, React 19, TypeScript |
| API | `src/app/api/pagespeed/route.ts` validates input and calls Google |
| State | `src/store/performanceStore.ts`, Zustand and localStorage |
| Visualization | Recharts, metric and comparison components |
| Export | jsPDF, JSON and CSV download helpers |
| Recommendations | Local rules in `src/lib/aiService.ts` |

The API supports GET and POST with a URL and a `mobile` or `desktop` strategy. The current main interface submits mobile analysis. URLs submitted for live analysis are sent to Google PageSpeed Insights.

## Current limitations

This is a portfolio prototype. Some detailed component breakdowns are estimates rather than raw audit measurements. Missing metrics and field-vs-lab distinctions need further work; use the original PageSpeed report for decisions. The optional AI-provider controls are experimental, and local rule-based suggestions are the default.

The production build passes. The existing lint command currently reports React hook/component errors; lint is not yet a clean quality gate. Before exposing a hosted instance, add rate limiting and restrict use of the API quota.

## Contributing

Include a reproducible example, expected behavior, and a screenshot for UI changes. Keep API credentials in server environment variables. Useful improvements include metric provenance, empty/missing-data states, hook cleanup, and automated API tests.
