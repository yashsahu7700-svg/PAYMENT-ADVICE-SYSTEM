# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **Frontend**: React + Vite + Tailwind CSS + wouter

## Artifacts

### Payment Advice Manager (`/`)
A full-stack payment advice management system for three trading companies:
- **KSA** → Kaluram Sambhudayal Agrawal
- **AT** → Agrawal Traders
- **KSE** → KS Enterprises

All at Gandhi Ganj Chhindwara.

Features:
- Dashboard with company cards and summary stats
- Per-company payment advice list
- Create / Edit payment advices with live auto-calculations:
  - Net Weight = Billed Weight - Shortage/Reject/Return Weight
  - Gross Amount = Net Weight × Rate
  - TDS = 10% of Gross
  - Dhalta = 0.1% of Gross
  - Quality Claim = user-entered % of Gross (auto-calculated)
  - Brokerage and Bank Charge (user-entered)
  - Payable Amount = Gross - TDS - Dhalta - QC - Brokerage - Bank Charge
  - Advance Payment (user-entered)
  - Leftover Amount = Payable - Advance
- Formal print-ready payment advice view (Edit + Print buttons)
- All data stored in PostgreSQL via Drizzle ORM

### API Server (`/api`)
Express REST API serving the payment advice endpoints.

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

## DB Schema

Table: `payment_advices` — see `lib/db/src/schema/paymentAdvices.ts`

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
