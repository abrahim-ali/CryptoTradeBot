# Design Guidelines: Cryptocurrency Trading Platform

## Design Approach
**Reference-Based:** Drawing from professional crypto exchanges (Pionex, Binance, Coinbase Pro, Kraken) where data density, real-time updates, and functional efficiency are paramount. This is a utility-focused trading dashboard requiring specialized financial UI patterns.

## Layout System

### Primary Structure
**Multi-Panel Dashboard Layout:**
- Fixed header (h-16) with logo, market selector, and account controls
- Main content divided into 3-4 core zones:
  - Primary chart area (60-65% width on desktop)
  - Order entry panel (35-40% width, right side)
  - Order book + recent trades (full width bottom or side column)
  - Portfolio/positions drawer (collapsible)

**Grid System:**
- Desktop: Complex 12-column grid with flexible panel sizing
- Tablet: 2-column stacked layout (chart above, controls below)
- Mobile: Single column with tab-based navigation

**Spacing Units:** Tailwind units of 1, 2, 3, 4, 6, and 8
- Panel padding: p-3 to p-4
- Section gaps: gap-3 or gap-4
- Component margins: m-2 to m-4
- Tight data tables: p-1 to p-2

## Typography

**Font Families:**
- Primary: Inter or IBM Plex Sans (excellent number readability)
- Monospace: JetBrains Mono or Roboto Mono (for prices, amounts, technical data)

**Hierarchy:**
- Page title: text-xl font-semibold
- Section headers: text-sm font-medium uppercase tracking-wide
- Data labels: text-xs font-medium
- Primary values (prices): text-lg to text-2xl font-bold monospace
- Secondary data: text-sm monospace
- Micro labels: text-xs

**Number Formatting:**
- Use monospace for all numerical values
- Tabular figures for alignment in tables
- Clear decimal separation with consistent precision

## Component Library

### Navigation & Headers
**Top Navigation Bar:**
- Logo (left, h-8)
- Primary market pair selector (prominent, center-left)
- Quick stats ticker (scrolling market overview)
- User menu, notifications, settings (right aligned)
- Account balance display (prominent)

### Trading Interface Components

**Chart Panel:**
- TradingView-style candlestick chart (primary focus)
- Toolbar: timeframe selector (1m, 5m, 15m, 1h, 4h, 1D)
- Chart type toggle (candlestick, line, area)
- Indicator controls (volume, MA, RSI, MACD)
- Full-screen toggle button
- Drawing tools icon row

**Order Entry Panel:**
- Tab switcher: Limit / Market / Stop-Limit
- Input fields stacked vertically with labels above:
  - Price input (with current market price reference)
  - Amount input (with max/percentage buttons: 25%, 50%, 75%, 100%)
  - Total calculation (auto-computed, read-only display)
- Buy/Sell action buttons (full width, h-12, prominent)
- Available balance display (small text, above inputs)
- Order summary preview before execution

**Order Book:**
- Three-column table: Price | Amount | Total
- Spread indicator (highlighted row between bids/asks)
- Depth visualization (subtle background bars)
- Row height: h-6 to h-7 (compact)
- Bid/ask color differentiation through opacity/weight
- Clickable rows to populate order form

**Recent Trades:**
- Simple table: Price | Amount | Time
- Compact rows (h-6)
- Auto-scrolling new trades indicator
- Trade direction indicator (small icon/weight)

**Market Selector:**
- Search/filter input
- Categorized tabs: Favorites / USDT / BTC / ETH
- Sortable columns: Pair | Price | 24h Change | Volume
- Star icon for favorites
- Hover state highlighting

**Portfolio Panel:**
- Asset breakdown table: Coin | Holdings | Value | 24h Change
- Total portfolio value (large, prominent)
- Profit/loss summary card
- Asset allocation pie/donut chart (small, visual reference)

### Data Display Components

**Price Ticker:**
- Scrolling horizontal ticker (top of page or within header)
- Format: SYMBOL PRICE ±CHANGE%
- Auto-updating every few seconds

**Statistics Cards:**
- Compact info blocks: 24h High, 24h Low, Volume, Market Cap
- Label (text-xs) above value (text-base font-semibold)
- Grid layout: grid-cols-2 md:grid-cols-4 gap-3

**Watchlist Sidebar:**
- Compact list with mini price charts (sparklines)
- Quick access to favorite pairs
- Add/remove toggle

### Forms & Inputs

**Trading Input Fields:**
- Labeled inputs with clear units (USDT, BTC, etc.)
- Increment/decrement buttons for precision
- Max button aligned right within input
- Validation messages below fields
- Consistent h-10 input height

**Percentage Selector:**
- Button group: 25% | 50% | 75% | 100%
- Compact, equal-width buttons
- Active state clearly indicated

## Information Architecture

**Screen Layout Priority:**
1. **Central Focus:** Trading chart (largest real estate)
2. **Right Panel:** Order entry and execution
3. **Lower Section:** Order book + trade history (split or tabbed)
4. **Collapsible Drawer:** Portfolio, order history, settings
5. **Header:** Navigation, market selector, account

**Data Hierarchy:**
- Most critical: Current price, chart, order entry
- Secondary: Order book depth, recent trades
- Tertiary: Portfolio value, statistics
- Background: Market lists, settings

## Responsive Behavior

**Desktop (1440px+):** Full multi-panel layout
**Laptop (1024-1439px):** Slightly compressed panels, maintain multi-column
**Tablet (768-1023px):** Chart full-width top, order entry below, tabbed order book/trades
**Mobile (<768px):** 
- Bottom tab navigation (Chart | Trade | Markets | Portfolio)
- Single column views
- Collapsible panels
- Simplified order entry

## Real-Time Data Updates
- Live price tickers update smoothly
- Order book refreshes without jarring shifts
- Chart updates with new candles
- Portfolio values recalculate instantly
- Use subtle transitions (duration-100 to duration-200)

## Accessibility
- Keyboard navigation for order entry
- Focus states on all interactive elements
- Clear labels for screen readers
- Sufficient contrast for data readability (critical in trading)
- Error states clearly marked

## Performance Considerations
- Virtualized scrolling for large order books
- Debounced input updates
- Efficient chart rendering
- Cached market data with smart refresh intervals