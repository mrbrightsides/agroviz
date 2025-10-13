# Changelog

All notable changes to RANTAI AgroViz will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### To Be Implemented
- SpacetimeDB full component integration
- Wallet-based authentication
- Real commodity price API
- IoT sensor connectivity
- Computer vision disease detection
- Mobile app (React Native)

---

## [0.2.0] - 2025-01-09

### ✨ Added - Real Weather Intelligence
- **Real Weather API Integration** with WeatherAPI.com
  - Live weather data with 7-day forecasts
  - Temperature, rainfall, humidity, wind speed, UV index
  - Auto-refresh every 10 minutes
  - 1 million free API calls per month
- **Smart Weather Alerts System**
  - 6 alert types: extreme heat, heavy rain, drought, strong wind, frost, high UV
  - Severity levels: critical, high, medium
  - Actionable recommendations for each alert type
  - Push notifications via toast alerts
- **Location Management**
  - 8 quick-select Indonesian regions
  - Manual location search
  - Live location display with region info
- **Enhanced Weather Dashboard**
  - Live weather status banner
  - Real-time metrics display
  - Interactive weather charts
  - Last update timestamp

### 🗄️ Added - Database Infrastructure
- **SpacetimeDB Integration**
  - Server module with 8 tables (User, Crop, WeatherAlert, MarketPrice, Product, DAOProposal, DAOVote, FuzzyRecommendation)
  - 14 server-side reducers for CRUD operations
  - Auto-generated TypeScript client bindings
  - Real-time WebSocket connection
  - `useSpacetimeDB` custom hook for client integration
  - Database status indicator in UI

### 🎨 Improved
- Weather dashboard now uses real API data instead of simulated
- Alert system provides actionable farming recommendations
- Location-based weather tracking for accurate regional data
- Database connection status visible to users

### 📝 Documentation
- Comprehensive README.md with all features
- CONTRIBUTING.md guidelines for contributors
- MIT LICENSE added
- Code examples and setup instructions

---

## [0.1.0] - 2025-01-08

### ✨ Added - Initial Release
- **Farm Data Dashboard**
  - Multi-crop management (8 crop types)
  - Soil metrics tracking (moisture, temperature, NPK)
  - Harvest analytics with charts
  - Crop status monitoring
- **Blockchain Supply Chain**
  - Ethereum Sepolia integration
  - Smart contract connection (0x2a6eA164...)
  - QR code generation for products
  - Supply chain stage tracking
  - OnchainKit wallet integration
- **Fuzzy Logic AI Advisor**
  - 6-parameter analysis (soil, weather, crop age, pH, nutrients)
  - Smart action recommendations (harvest, irrigate, fertilize, plant, wait, pest_control)
  - Confidence scoring (0-100%)
  - Reasoning explanations
  - Real-time parameter adjustment
- **Market Analytics**
  - 5 commodity price tracking (Rice, Coffee, Palm Oil, Corn, Soybean)
  - 30-day historical trends
  - 7-day price predictions
  - Technical analysis (volatility, buy/sell signals)
  - Market sentiment indicators
- **AgroDAO Governance**
  - Proposal system (4 categories: purchase, resource, policy, partnership)
  - Democratic voting (for/against)
  - Treasury management
  - Member reputation system
  - Active/Passed/Rejected proposal statuses
- **UI/UX**
  - Web3 cyberpunk theme
  - Dark/light mode toggle
  - Responsive mobile design
  - shadcn/ui component library
  - Gradient effects and animations
  - Interactive data visualizations

### 🛠️ Technical
- Next.js 14 with App Router
- TypeScript strict mode
- Tailwind CSS styling
- Recharts for data visualization
- OnchainKit for Web3 features
- Wagmi + Viem for Ethereum
- Framer Motion animations

### 📊 Performance
- Build size: 468kB (main bundle)
- First load JS: 702kB
- Build time: ~60 seconds
- Zero build errors

---

## Version History Summary

| Version | Date | Key Features |
|---------|------|--------------|
| 0.2.0 | 2025-01-09 | Real weather API, Smart alerts, SpacetimeDB infrastructure |
| 0.1.0 | 2025-01-08 | Initial release with 6 core features |

---

## Upcoming Milestones

### v0.3.0 - Data Persistence (Planned)
- [ ] Connect SpacetimeDB to all components
- [ ] Persistent crop records
- [ ] Weather alert history
- [ ] DAO vote storage
- [ ] Market price tracking

### v0.4.0 - Authentication (Planned)
- [ ] Wallet-based user authentication
- [ ] Farmer profile management
- [ ] Multi-farm support
- [ ] Team collaboration features

### v0.5.0 - Real Market Data (Planned)
- [ ] Live commodity price API
- [ ] Jakarta Futures Exchange integration
- [ ] Price alert notifications
- [ ] Historical price analysis

### v1.0.0 - Production Ready (Planned)
- [ ] Full feature integration
- [ ] IoT sensor support
- [ ] Mobile app release
- [ ] Multi-language support
- [ ] Security audit
- [ ] Farmer pilot program

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for details on how to contribute to this changelog and the project.

## Links

- [Repository](https://github.com/mrbrightsides/agroviz)
- [Website](https://rantai.elpeef.com)
- [Issues](https://github.com/mrbrightsides/agroviz/issues)
- [Pull Requests](https://github.com/mrbrightsides/agroviz/pulls)
