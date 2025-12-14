# CryptoCollector - Multi-Chain Portfolio Manager

## Overview

CryptoCollector is a multi-chain cryptocurrency portfolio management application that allows users to track wallet balances across Bitcoin, Ethereum, Litecoin, and Dogecoin networks. The app provides portfolio monitoring, balance tracking with USD conversion, dust detection for small balances, and withdrawal request functionality.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight React router)
- **State Management**: TanStack React Query for server state and caching
- **UI Components**: shadcn/ui component library built on Radix UI primitives
- **Styling**: Tailwind CSS with custom CSS variables for theming (light/dark mode support)
- **Forms**: React Hook Form with Zod validation
- **Build Tool**: Vite with custom plugins for Replit integration

### Backend Architecture
- **Runtime**: Node.js with Express
- **Language**: TypeScript with ESM modules
- **API Pattern**: RESTful JSON API at `/api/*` endpoints
- **Database ORM**: Drizzle ORM with PostgreSQL dialect
- **Schema Validation**: Zod with drizzle-zod integration for type-safe schemas

### Data Storage
- **Database**: PostgreSQL (configured via DATABASE_URL environment variable)
- **Schema Location**: `shared/schema.ts` contains all table definitions
- **Tables**: 
  - `users` - User authentication
  - `wallets` - Tracked cryptocurrency wallets with balances
  - `tokens` - Token balances within wallets
- **Fallback**: In-memory storage implementation available for development

### Key Features
- Multi-chain wallet tracking (BTC, ETH, LTC, DOGE)
- Real-time balance fetching from blockchain APIs
- USD price conversion via CoinGecko API with caching
- Dust balance detection (< $1 USD)
- Portfolio statistics and asset aggregation
- Dark/light theme toggle

### Project Structure
```
├── client/           # React frontend
│   ├── src/
│   │   ├── components/  # UI components
│   │   ├── pages/       # Route pages
│   │   ├── hooks/       # Custom React hooks
│   │   └── lib/         # Utilities and query client
├── server/           # Express backend
│   ├── index.ts      # Server entry point
│   ├── routes.ts     # API route definitions
│   ├── storage.ts    # Data access layer
│   └── blockchain.ts # Blockchain API integrations
├── shared/           # Shared code between client/server
│   └── schema.ts     # Database schema and types
└── migrations/       # Drizzle database migrations
```

### Build and Development
- Development: `npm run dev` - runs tsx for hot reloading
- Production build: `npm run build` - bundles client with Vite, server with esbuild
- Database sync: `npm run db:push` - pushes schema changes via Drizzle Kit

## External Dependencies

### Third-Party APIs
- **CoinGecko API**: Cryptocurrency price data for USD conversions (60-second cache TTL)
- **Blockchain APIs**: Balance fetching for supported chains (implementation in `server/blockchain.ts`)

### Database
- **PostgreSQL**: Primary database, connection via `DATABASE_URL` environment variable
- **connect-pg-simple**: Session storage for Express (if sessions are enabled)

### UI Component Libraries
- **Radix UI**: Accessible primitive components (dialogs, dropdowns, tooltips, etc.)
- **Lucide React**: Icon library
- **embla-carousel-react**: Carousel component
- **react-day-picker**: Calendar/date picker
- **recharts**: Charting library
- **vaul**: Drawer component

### Fonts
- **Google Fonts**: Inter (UI), JetBrains Mono/Fira Code/Geist Mono (monospace for addresses)