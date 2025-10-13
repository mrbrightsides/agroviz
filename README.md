# 🌱 RANTAI AgroViz

**Tagline:** *"Data-Driven Agriculture Insights"*

A comprehensive agricultural platform combining real-time weather data, blockchain supply chain tracking, AI decision support, market analytics, and decentralized governance for farmers and agricultural stakeholders.

![Web3 Theme](https://img.shields.io/badge/Theme-Web3%20Cyberpunk-00D9FF?style=for-the-badge)
![Next.js](https://img.shields.io/badge/Next.js-14-black?style=for-the-badge&logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?style=for-the-badge&logo=typescript)
![SpacetimeDB](https://img.shields.io/badge/SpacetimeDB-Real--time-purple?style=for-the-badge)
![Ethereum](https://img.shields.io/badge/Ethereum-Sepolia-627EEA?style=for-the-badge&logo=ethereum)

---

## 🎯 **Vision**

RANTAI AgroViz empowers farmers, cooperatives, governments, and agricultural buyers with:
- **Data-driven decision making** instead of intuition alone
- **Transparent supply chain** from farm to consumer
- **Real-time weather intelligence** with actionable alerts
- **AI-powered recommendations** for optimal farming practices
- **Community governance** through decentralized autonomous organization (DAO)

---

## ✨ **Key Features**

### 1️⃣ **Farm Data Dashboard**
- **Real-time Crop Monitoring**: Track soil moisture, temperature, NPK nutrients
- **Multi-crop Management**: Rice, coffee, palm oil, corn, soybean, vegetables, fruits
- **Harvest Analytics**: Yield trends, quality metrics, price analysis
- **Weather Integration**: Live weather data with 7-day forecasts

### 2️⃣ **Real Weather Data + Smart Alerts** 🌦️
- **Live Weather API**: Integration with WeatherAPI.com (1M free calls/month)
- **7-Day Forecasts**: Temperature, rainfall, humidity, wind speed, UV index
- **6 Smart Alert Types**:
  - 🔥 Extreme Heat Alert (>35°C)
  - 🌧️ Heavy Rainfall Warning (>50mm/3 days)
  - ☀️ Drought Alert (No rain 5+ days)
  - 💨 Strong Wind Warning (>40 km/h)
  - ❄️ Frost Warning (<5°C)
  - ☀️ High UV Index (>8)
- **Push Notifications**: Real-time toast alerts for critical conditions
- **Location Management**: 8 quick-select regions + manual search
- **Auto-refresh**: Data updates every 10 minutes

### 3️⃣ **Blockchain Supply Chain Tracking** ⛓️
- **Product Registration**: Register agricultural products on Ethereum Sepolia
- **QR Code Generation**: Traceability from farmer to consumer
- **Smart Contract Integration**: 
  - Contract: `0x2a6eA164FcAD56d88EB4e66307960B9230fD3208`
  - Network: Sepolia Testnet
- **Ownership Transfer**: Track product journey through supply chain
- **OnchainKit Integration**: Seamless wallet connection and transactions

### 4️⃣ **Fuzzy Logic Decision Support** 🤖
- **AI-Powered Recommendations**: Analyze 6+ parameters
  - Soil moisture, temperature, rainfall
  - Crop age, soil pH, nutrient levels
- **Smart Actions**: harvest, irrigate, fertilize, plant, wait, pest_control
- **Confidence Scoring**: 0-100% confidence with reasoning
- **Recommendation History**: Track past suggestions and outcomes
- **Real-time Analysis**: Auto-update every 2 seconds

### 5️⃣ **Market Analytics & Price Intelligence** 📈
- **5 Commodity Tracking**: Rice, Coffee, Palm Oil, Corn, Soybean
- **Price Trends**: 30-day historical data + 7-day predictions
- **Technical Analysis**:
  - Volatility metrics
  - Buy/Sell/Hold recommendations
  - Support/resistance levels
- **Market Sentiment**: Bullish/Bearish indicators
- **Price Alerts**: (UI ready, backend pending)

### 6️⃣ **AgroDAO - Community Governance** 🏛️
- **Proposal System**: 4 categories
  - Bulk purchases (collective buying power)
  - Shared resources (equipment, storage)
  - Community policies
  - Strategic partnerships
- **Democratic Voting**: One farmer, one vote
- **Treasury Management**: Transparent fund allocation
- **Member Reputation**: Contribution-based ranking
- **Active/Passed/Rejected Status**: Full proposal lifecycle

### 7️⃣ **SpacetimeDB Persistence** 💾
- **Real-time Database**: Built on SpacetimeDB
- **8 Data Tables**:
  - Users, Crops, WeatherAlerts, MarketPrices
  - Products, DAOProposals, DAOVotes, FuzzyRecommendations
- **14 Server Reducers**: Complete CRUD operations
- **Auto-generated Client Bindings**: Type-safe TypeScript integration
- **Cross-device Sync**: Access data from anywhere

---

## 🛠️ **Tech Stack**

### **Frontend**
- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript (Strict Mode)
- **Styling**: Tailwind CSS + shadcn/ui components
- **Charts**: Recharts
- **State Management**: React Hooks + Context
- **Theme**: Dark/Light mode with Web3 cyberpunk aesthetic

### **Blockchain**
- **SDK**: OnchainKit (Coinbase)
- **Library**: Wagmi + Viem
- **Network**: Ethereum Sepolia Testnet
- **RPC**: Infura (`https://sepolia.infura.io/v3/f8d248f838ec4f12b0f01efd2b238206`)

### **Database**
- **Primary**: SpacetimeDB (Real-time database with compute layer)
- **Connection**: WebSocket-based real-time sync
- **Server Module**: Rust (auto-deployed)
- **Client Bindings**: Auto-generated TypeScript

### **APIs**
- **Weather**: WeatherAPI.com
- **Blockchain RPC**: Infura
- **Proxy**: Custom Next.js API route (`/api/proxy`)

---

## 🚀 **Getting Started**

### **Prerequisites**
- Node.js 18+ and npm
- Git
- (Optional) Ethereum wallet for blockchain features

### **Installation**

```bash
# Clone the repository
git clone https://github.com/yourusername/rantai-agroviz.git
cd rantai-agroviz

# Install dependencies
npm install

# Run development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### **Environment Variables**

The app uses hardcoded API endpoints for demo purposes. For production:

```env
# WeatherAPI.com (get free key at https://weatherapi.com)
NEXT_PUBLIC_WEATHER_API_KEY=your_weather_api_key

# Infura (for Ethereum RPC)
NEXT_PUBLIC_INFURA_RPC=https://sepolia.infura.io/v3/YOUR_PROJECT_ID

# SpacetimeDB (auto-configured)
NEXT_PUBLIC_SPACETIME_MODULE=your_module_name
```

### **API Keys Setup**

1. **WeatherAPI.com**: 
   - Sign up at https://weatherapi.com
   - Get free API key (1M calls/month)
   - Currently hardcoded in `src/lib/weather-service.ts`

2. **Infura**: 
   - Sign up at https://infura.io
   - Create Ethereum project
   - Use Sepolia testnet endpoint

3. **SpacetimeDB**:
   - Automatically configured
   - No additional setup needed

---

## 📁 **Project Structure**

```
rantai-agroviz/
├── src/
│   ├── app/
│   │   ├── page.tsx              # Main application entry
│   │   ├── layout.tsx            # Root layout with theme provider
│   │   └── api/
│   │       ├── proxy/route.ts    # API proxy for external calls
│   │       ├── health/route.ts   # Health check endpoint
│   │       └── logger/route.ts   # Logging endpoint
│   │
│   ├── components/
│   │   ├── FarmDashboard.tsx     # Crop management & weather dashboard
│   │   ├── SupplyChainTracker.tsx # Blockchain supply chain
│   │   ├── FuzzyLogicAdvisor.tsx  # AI decision support
│   │   ├── MarketAnalytics.tsx    # Price intelligence
│   │   ├── AgroDAO.tsx            # Governance system
│   │   ├── WeatherAlerts.tsx      # Weather alert system
│   │   ├── LocationSelector.tsx   # Location management
│   │   ├── ThemeProvider.tsx      # Dark/light theme provider
│   │   └── ui/                    # shadcn/ui components
│   │
│   ├── lib/
│   │   ├── weather-service.ts     # WeatherAPI integration
│   │   ├── fuzzy-logic.ts         # Fuzzy logic algorithms
│   │   └── utils.ts               # Utility functions
│   │
│   ├── hooks/
│   │   └── useSpacetimeDB.ts      # SpacetimeDB client hook
│   │
│   ├── spacetime_module_bindings/ # Auto-generated SpacetimeDB types
│   │
│   └── styles/
│       └── globals.css            # Global styles + theme variables
│
├── spacetime-server/
│   └── src/
│       └── lib.rs                 # SpacetimeDB Rust module
│
├── public/
│   ├── .well-known/
│   │   └── farcaster.json         # Farcaster mini-app config
│   └── ...
│
├── package.json
├── tsconfig.json
├── tailwind.config.ts
└── README.md
```

---

## 🎨 **Design System**

### **Color Palette**

#### Dark Mode (Cyberpunk Agriculture)
- **Primary**: Matrix Green (`#00ff41`)
- **Accent**: Cyber Cyan (`#00d9ff`)
- **Background**: Deep Black (`#0a0a0a`)
- **Cards**: Dark Gray (`#1a1a1a`)

#### Light Mode (Clean Professional)
- **Primary**: Fresh Green (`#10b981`)
- **Accent**: Sky Blue (`#0ea5e9`)
- **Background**: Pure White (`#ffffff`)
- **Cards**: Light Gray (`#f9fafb`)

### **UI Components**
- **shadcn/ui**: 40+ pre-built components
- **Recharts**: Interactive data visualizations
- **Lucide Icons**: Consistent iconography
- **Framer Motion**: Smooth animations

---

## 🔗 **Smart Contract Details**

### **AgroSupplyChain Contract**
- **Network**: Ethereum Sepolia Testnet
- **Address**: `0x2a6eA164FcAD56d88EB4e66307960B9230fD3208`
- **Chain ID**: 11155111

### **Contract Functions**
```solidity
// Add new product
function addProduct(
    string name,
    string origin,
    string ipfsHash
) external

// Transfer ownership
function transferProduct(
    uint256 id,
    address newOwner
) external

// View product details
function products(uint256 id) external view returns (
    string name,
    string origin,
    string ipfsHash,
    address owner
)
```

### **Events**
- `ProductAdded(uint256 id, string name, string origin, address owner)`
- `OwnershipTransferred(uint256 id, address from, address to)`

---

## 📊 **SpacetimeDB Schema**

### **Tables**

```rust
// User profile
#[table(name = user, public)]
pub struct User {
    #[primary_key]
    pub identity: Identity,
    pub wallet_address: String,
    pub farm_name: String,
    pub location: String,
}

// Crop records
#[table(name = crop, public)]
pub struct Crop {
    #[primary_key]
    #[auto_inc]
    pub id: u64,
    pub owner: Identity,
    pub crop_type: String,
    pub area_hectares: f32,
    pub planted_date: String,
    pub soil_moisture: f32,
    pub temperature: f32,
    pub nitrogen: f32,
    pub phosphorus: f32,
    pub potassium: f32,
    pub status: String,
}

// Weather alerts
#[table(name = weather_alert, public)]
pub struct WeatherAlert {
    #[primary_key]
    #[auto_inc]
    pub id: u64,
    pub owner: Identity,
    pub alert_type: String,
    pub severity: String,
    pub message: String,
    pub action_required: String,
    pub timestamp: String,
    pub dismissed: bool,
}

// ... 5 more tables (MarketPrice, Product, DAOProposal, DAOVote, FuzzyRecommendation)
```

### **Reducers**

14 server-side functions for CRUD operations:
- User: `create_user`, `update_user_location`
- Crop: `add_crop`, `update_crop_metrics`, `harvest_crop`, `delete_crop`
- Weather: `save_weather_alert`, `dismiss_weather_alert`
- Market: `save_market_price`
- Supply Chain: `register_product`
- DAO: `create_dao_proposal`, `cast_dao_vote`, `update_proposal_status`
- AI: `save_fuzzy_recommendation`

---

## 🧪 **Testing**

```bash
# Run type checking
npm run type-check

# Build for production
npm run build

# Lint code
npm run lint
```

---

## 🚢 **Deployment**

### **Vercel (Recommended)**
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel --prod
```

### **Environment Configuration**
- Node.js 18+
- Build Command: `npm run build`
- Output Directory: `.next`
- Install Command: `npm install`

---

## 🎯 **Roadmap**

### **Phase 1: MVP** ✅
- [x] Farm dashboard with crop management
- [x] Real weather API integration
- [x] Smart weather alerts system
- [x] Blockchain supply chain (UI)
- [x] Fuzzy logic decision support
- [x] Market analytics visualization
- [x] DAO governance interface
- [x] SpacetimeDB infrastructure
- [x] Dark/light theme toggle

### **Phase 2: Data Integration** 🚧
- [ ] Connect SpacetimeDB to all components
- [ ] Implement wallet-based authentication
- [ ] Real commodity price API
- [ ] IoT sensor integration (MQTT/LoRaWAN)
- [ ] Smart contract read/write operations
- [ ] Historical data analytics

### **Phase 3: Advanced Features** 📋
- [ ] Computer vision disease detection
- [ ] Satellite imagery integration
- [ ] Predictive yield modeling
- [ ] Financial tools (lending, insurance)
- [ ] Mobile app (React Native)
- [ ] Offline mode with sync
- [ ] Multi-language support (ID, EN)

### **Phase 4: Production** 🎯
- [ ] User testing with real farmers
- [ ] Performance optimization
- [ ] Security audit
- [ ] Mainnet deployment
- [ ] Partnership with agricultural cooperatives
- [ ] Government pilot programs

---

## 🤝 **Contributing**

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

---

## 📄 **License**

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👥 **Credits**

**Created by:** [mrbrightsides](https://github.com/mrbrightsides)

**Powered by:**
- [OnchainKit](https://onchainkit.xyz) - Coinbase Web3 SDK
- [SpacetimeDB](https://spacetimedb.com) - Real-time database
- [WeatherAPI.com](https://weatherapi.com) - Weather data
- [shadcn/ui](https://ui.shadcn.com) - UI components
- [Ohara](https://ohara.ai) - AI development platform

**Website:** [rantai.elpeef.com](https://rantai.elpeef.com)

---

## 📞 **Support**

- **Issues**: [GitHub Issues](https://github.com/mrbrightsides/agroviz/issues)
- **Discussions**: [GitHub Discussions](https://github.com/mrbrightsides/agroviz/discussions)
- **Email**: support@rantai.elpeef.com

---

## 🌟 **Acknowledgments**

Special thanks to:
- Indonesian farmers for inspiration
- Blockchain community for transparency vision
- Open-source contributors
- Agricultural technology researchers
- Climate scientists for weather algorithms

---

## 📈 **Stats**

- **Build Size**: 468kB (optimized)
- **First Load JS**: 702kB
- **Build Time**: ~60 seconds
- **Components**: 50+
- **API Integrations**: 3 (Weather, Blockchain, Database)
- **Supported Crops**: 8 types
- **Weather Alerts**: 6 categories
- **DAO Proposals**: 4 types

---

<div align="center">

### 🌱 **RANTAI AgroViz** - Empowering Farmers with Data & Blockchain

*Built with ❤️ for Indonesian Agriculture*

**[Website](https://rantai.elpeef.com)** • **[GitHub](https://github.com/mrbrightsides)** • **[Demo](https://agroviz.elpeef.com)**

</div>

