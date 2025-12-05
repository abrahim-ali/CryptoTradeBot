# CryptoTrade Pro - Professional Cryptocurrency Trading Platform

## Overview

CryptoTrade Pro is a professional-grade cryptocurrency trading platform built with modern web technologies. The application provides real-time market data, interactive trading charts, order management, and portfolio tracking capabilities. It's designed to emulate professional exchanges like Binance, Pionex, and Kraken with a focus on data density, real-time updates, and functional efficiency.

The platform features a multi-panel dashboard layout optimized for traders, with live price feeds, candlestick charts, order books, recent trades, and comprehensive order entry interfaces. The application currently uses mock data with plans to integrate live trading functionality.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework & Build System:**
- React 18 with TypeScript for type-safe component development
- Vite as the build tool and development server for fast HMR and optimized production builds
- Wouter for lightweight client-side routing
- TanStack Query (React Query) for server state management and data fetching

**UI Component System:**
- shadcn/ui component library based on Radix UI primitives
- Tailwind CSS for utility-first styling with custom design tokens
- Design system follows "New York" style variant with professional trading platform aesthetics
- Custom CSS variables for theme management (dark/light mode support)
- Monospace fonts (JetBrains Mono) for numerical data to ensure readability

**State Management:**
- Zustand for client-side global state (trading store)
- Manages cryptocurrency assets, selected trading pairs, order books, recent trades, open orders, portfolio data, and watchlists
- TanStack Query handles server state, caching, and background refetching

**Data Visualization:**
- Lightweight Charts library for professional-grade candlestick and volume charts
- Real-time chart updates with multiple timeframe support (1m, 5m, 15m, 1H, 4H, 1D, 1W)
- Mock data generation for charts (to be replaced with real OHLC data)

**Layout System:**
- Responsive multi-panel dashboard using CSS Grid and Flexbox
- Resizable panels for customizable workspace
- Three-column desktop layout: trading chart (60-65%), order entry panel (35-40%), order book/trades
- Mobile-responsive with tab-based navigation and single-column stacking

**Key Features:**
- Real-time price ticker scrolling across major cryptocurrencies
- Interactive order book with click-to-fill prices
- Market statistics display with 24h high/low, volume, and market cap
- Order entry forms supporting limit and market orders
- Portfolio view showing holdings, P&L, and available balances
- Watchlist functionality for favorite trading pairs
- Market selector dialog for switching between trading pairs

### Backend Architecture

**Server Framework:**
- Express.js for HTTP server and API routing
- Node.js runtime with ES modules
- HTTP server wraps Express for potential WebSocket upgrades

**API Design:**
- RESTful endpoints for cryptocurrency data
- `/api/crypto/prices` - Fetches top 50 cryptocurrencies by market cap with 24h price changes
- Formatted response includes symbol, price, volume, market cap, and price change percentage

**Data Storage:**
- In-memory storage implementation (`MemStorage` class) for development
- User schema defined with Drizzle ORM (PostgreSQL-compatible)
- Prepared for database migration with schema files in `shared/schema.ts`

**Build & Deployment:**
- Custom build script using esbuild for server bundling
- Vite handles client build with code splitting
- Production build outputs to `dist/` directory
- Server dependencies are selectively bundled to reduce cold start times

**Development Environment:**
- Vite middleware integration for HMR during development
- Request logging with timing information
- Separate development and production modes

### External Dependencies

**Third-Party APIs:**
- **CoinGecko API** - Primary data source for cryptocurrency market data
  - Fetches real-time prices, 24h changes, volume, market cap
  - Free tier with rate limiting (current implementation)
  - No authentication required for basic market data
  - Returns data for top 50 cryptocurrencies by market cap

**WebSocket Integration:**
- Custom WebSocket client (`cryptoWebSocket`) for real-time price updates
- Maps cryptocurrency symbols to CoinGecko IDs for proper data streaming
- Reconnection logic with exponential backoff (max 3 attempts)
- Ping/pong heartbeat mechanism to maintain connection
- Connection status tracking for UI indicators

**Database (Configured but Not Active):**
- **Neon Serverless PostgreSQL** - Configured via Drizzle ORM
- Schema defined for user authentication (username/password)
- Migration system ready via Drizzle Kit
- Currently using in-memory storage; database can be activated by setting `DATABASE_URL`

**UI Component Libraries:**
- Radix UI primitives for accessible, unstyled components
- React Hook Form with Zod resolvers for form validation
- date-fns for date formatting and manipulation
- class-variance-authority (CVA) for component variant management
- Embla Carousel for carousel components

**Development Tools:**
- TypeScript for type safety across the codebase
- ESBuild for fast server bundling
- PostCSS with Autoprefixer for CSS processing
- Replit-specific plugins for development environment integration

**Planned Integrations:**
- Real OHLC (candlestick) data endpoints to replace mock chart data
- WebSocket for order book depth updates
- User authentication system (passport-local ready)
- Session management (express-session with connect-pg-simple)

**Note on Architecture:**
The application is structured as a monorepo with shared TypeScript types between client and server. The `shared/schema.ts` file defines database schemas and validation schemas that are consumed by both frontend and backend, ensuring type consistency across the stack.