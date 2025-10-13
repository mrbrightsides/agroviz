# 🔌 API Documentation

Comprehensive guide for integrating external APIs and services with RANTAI AgroViz.

---

## 📋 Table of Contents

1. [Weather API Integration](#weather-api-integration)
2. [Blockchain Smart Contract](#blockchain-smart-contract)
3. [SpacetimeDB Database](#spacetimedb-database)
4. [Internal API Routes](#internal-api-routes)
5. [External API Proxy](#external-api-proxy)

---

## 🌦️ Weather API Integration

### Provider: WeatherAPI.com

**Base URL:** `https://api.weatherapi.com/v1`

### Authentication
```typescript
const API_KEY = 'your_api_key_here';
```

### Endpoints Used

#### 1. Current Weather + Forecast
```http
GET /forecast.json?key={API_KEY}&q={location}&days=7&alerts=yes
```

**Parameters:**
- `key` (required): Your API key
- `q` (required): Location (city name, coordinates, IP)
- `days` (optional): Number of forecast days (1-10)
- `alerts` (optional): Include weather alerts (yes/no)

**Example Request:**
```typescript
const response = await fetch('/api/proxy', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    protocol: 'https',
    origin: 'api.weatherapi.com',
    path: '/v1/forecast.json',
    method: 'GET',
    headers: {},
    queryParams: {
      key: API_KEY,
      q: 'Jakarta',
      days: 7,
      alerts: 'yes'
    }
  })
});
```

**Response Format:**
```typescript
interface WeatherResponse {
  location: {
    name: string;
    region: string;
    country: string;
    lat: number;
    lon: number;
  };
  current: {
    temp_c: number;
    condition: {
      text: string;
      icon: string;
    };
    humidity: number;
    wind_kph: number;
    precip_mm: number;
    uv: number;
    pressure_mb: number;
    vis_km: number;
    feelslike_c: number;
  };
  forecast: {
    forecastday: Array<{
      date: string;
      day: {
        maxtemp_c: number;
        mintemp_c: number;
        avgtemp_c: number;
        totalprecip_mm: number;
        avghumidity: number;
        maxwind_kph: number;
        condition: {
          text: string;
          icon: string;
        };
      };
    }>;
  };
  alerts?: {
    alert: Array<{
      headline: string;
      severity: string;
      desc: string;
    }>;
  };
}
```

### Rate Limits
- **Free Tier**: 1,000,000 calls/month
- **Rate**: ~33,333 calls/day
- **Recommended Refresh**: Every 10 minutes

### Error Handling
```typescript
try {
  const data = await fetchWeatherData(location);
  // Use data
} catch (error) {
  console.error('Weather API error:', error);
  // Fallback to cached data
  return getFallbackWeatherData();
}
```

---

## ⛓️ Blockchain Smart Contract

### Network: Ethereum Sepolia Testnet

**Contract Address:** `0x2a6eA164FcAD56d88EB4e66307960B9230fD3208`

**RPC Endpoint:** `https://sepolia.infura.io/v3/f8d248f838ec4f12b0f01efd2b238206`

### Contract ABI

```typescript
const ABI = [
  {
    "inputs": [
      { "internalType": "string", "name": "name", "type": "string" },
      { "internalType": "string", "name": "origin", "type": "string" },
      { "internalType": "string", "name": "ipfsHash", "type": "string" }
    ],
    "name": "addProduct",
    "outputs": [],
    "stateMutability": "nonpayable",
    "type": "function"
  },
  {
    "inputs": [
      { "internalType": "uint256", "name": "id", "type": "uint256" },
      { "internalType": "address", "name": "newOwner", "type": "address" }
    ],
    "name": "transferProduct",
    "outputs": [],
    "stateMutability": "nonpayable",
    "type": "function"
  },
  {
    "inputs": [],
    "name": "productCount",
    "outputs": [
      { "internalType": "uint256", "name": "", "type": "uint256" }
    ],
    "stateMutability": "view",
    "type": "function"
  },
  {
    "inputs": [
      { "internalType": "uint256", "name": "", "type": "uint256" }
    ],
    "name": "products",
    "outputs": [
      { "internalType": "string", "name": "name", "type": "string" },
      { "internalType": "string", "name": "origin", "type": "string" },
      { "internalType": "string", "name": "ipfsHash", "type": "string" },
      { "internalType": "address", "name": "owner", "type": "address" }
    ],
    "stateMutability": "view",
    "type": "function"
  }
];
```

### Integration with OnchainKit

```typescript
import { useWriteContract, useReadContract } from 'wagmi';

// Add Product
const { writeContract } = useWriteContract();

const addProduct = async (name: string, origin: string, ipfsHash: string) => {
  await writeContract({
    address: '0x2a6eA164FcAD56d88EB4e66307960B9230fD3208',
    abi: ABI,
    functionName: 'addProduct',
    args: [name, origin, ipfsHash],
  });
};

// Read Product
const { data: product } = useReadContract({
  address: '0x2a6eA164FcAD56d88EB4e66307960B9230fD3208',
  abi: ABI,
  functionName: 'products',
  args: [productId],
});
```

### Events

#### ProductAdded
```solidity
event ProductAdded(
    uint256 id,
    string name,
    string origin,
    address owner
);
```

#### OwnershipTransferred
```solidity
event OwnershipTransferred(
    uint256 id,
    address from,
    address to
);
```

### Listening to Events
```typescript
import { useWatchContractEvent } from 'wagmi';

useWatchContractEvent({
  address: '0x2a6eA164FcAD56d88EB4e66307960B9230fD3208',
  abi: ABI,
  eventName: 'ProductAdded',
  onLogs(logs) {
    console.log('New product added:', logs);
  },
});
```

---

## 🗄️ SpacetimeDB Database

### Connection

**Module Name:** `rantai-agroviz`

**Connection URL:** `wss://maincloud.spacetimedb.com`

### Client Integration

```typescript
import { useSpacetimeDB } from '@/hooks/useSpacetimeDB';

function MyComponent() {
  const {
    isConnected,
    identity,
    crops,
    weatherAlerts,
    addCrop,
    saveWeatherAlert,
    // ... other helpers
  } = useSpacetimeDB();

  if (!isConnected) return <div>Connecting to database...</div>;

  return <div>Connected as {identity}</div>;
}
```

### Tables

#### 1. User Table
```rust
pub struct User {
    pub identity: Identity,       // Primary key
    pub wallet_address: String,
    pub farm_name: String,
    pub location: String,
}
```

#### 2. Crop Table
```rust
pub struct Crop {
    pub id: u64,                  // Auto-increment primary key
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
```

#### 3. WeatherAlert Table
```rust
pub struct WeatherAlert {
    pub id: u64,
    pub owner: Identity,
    pub alert_type: String,
    pub severity: String,
    pub message: String,
    pub action_required: String,
    pub timestamp: String,
    pub dismissed: bool,
}
```

### Reducers (Server-Side Functions)

#### Create User
```typescript
await createUser({
  walletAddress: '0x...',
  farmName: 'Green Valley Farm',
  location: 'Jakarta'
});
```

#### Add Crop
```typescript
await addCrop({
  cropType: 'Rice',
  areaHectares: 2.5,
  plantedDate: '2025-01-01',
  soilMoisture: 65.0,
  temperature: 28.0,
  nitrogen: 45.0,
  phosphorus: 30.0,
  potassium: 25.0,
  status: 'growing'
});
```

#### Save Weather Alert
```typescript
await saveWeatherAlert({
  alertType: 'heavy_rain',
  severity: 'critical',
  message: 'Heavy rainfall expected',
  actionRequired: 'Clear drainage systems',
  timestamp: new Date().toISOString()
});
```

### Real-time Subscriptions

```typescript
// Subscribe to all tables
const { disconnect } = subscribe(() => {
  onUserUpdate: (users) => console.log('Users updated:', users),
  onCropUpdate: (crops) => console.log('Crops updated:', crops),
  onWeatherAlertUpdate: (alerts) => console.log('Alerts updated:', alerts),
  // ... other callbacks
});

// Cleanup
useEffect(() => {
  return () => disconnect();
}, []);
```

---

## 🛣️ Internal API Routes

### 1. Health Check
```http
GET /api/health
```

**Response:**
```json
{
  "status": "healthy",
  "timestamp": "2025-01-09T12:00:00.000Z",
  "uptime": 3600,
  "version": "0.2.0"
}
```

### 2. Logger
```http
POST /api/logger
Content-Type: application/json

{
  "level": "info",
  "message": "User action logged",
  "metadata": {
    "userId": "123",
    "action": "crop_added"
  }
}
```

**Response:**
```json
{
  "success": true,
  "logged": true,
  "timestamp": "2025-01-09T12:00:00.000Z"
}
```

### 3. Proxy (External API Gateway)
```http
POST /api/proxy
Content-Type: application/json

{
  "protocol": "https",
  "origin": "api.example.com",
  "path": "/endpoint",
  "method": "GET",
  "headers": {
    "Authorization": "Bearer token"
  },
  "body": {
    "key": "value"
  }
}
```

**Response:** Forward response from external API

---

## 🌐 External API Proxy

### Purpose
All external API calls from client-side code MUST go through `/api/proxy` to:
- Hide API keys from client
- Enable CORS
- Add rate limiting
- Log requests
- Handle errors centrally

### Usage Pattern

```typescript
// ❌ WRONG - Direct external call from client
const response = await fetch('https://external-api.com/data', {
  headers: { 'X-API-Key': 'secret_key' } // API key exposed!
});

// ✅ CORRECT - Through proxy
const response = await fetch('/api/proxy', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    protocol: 'https',
    origin: 'external-api.com',
    path: '/data',
    method: 'GET',
    headers: {
      'X-API-Key': process.env.API_KEY // Server-side only
    }
  })
});
```

### Supported Content Types

1. **application/json** (default)
```typescript
{
  protocol: 'https',
  origin: 'api.example.com',
  path: '/json-endpoint',
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: { key: 'value' }
}
```

2. **multipart/form-data** (for file uploads)
```typescript
const formData = new FormData();
formData.append('file', file);
formData.append('protocol', 'https');
formData.append('origin', 'api.example.com');
formData.append('path', '/upload');
formData.append('method', 'POST');

await fetch('/api/proxy', {
  method: 'POST',
  body: formData // Browser sets Content-Type automatically
});
```

### Error Handling

```typescript
try {
  const response = await fetch('/api/proxy', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      protocol: 'https',
      origin: 'api.example.com',
      path: '/data',
      method: 'GET',
      headers: {}
    })
  });

  if (!response.ok) {
    throw new Error(`Proxy error: ${response.status}`);
  }

  const data = await response.json();
  return data;
} catch (error) {
  console.error('API call failed:', error);
  // Handle error appropriately
}
```

---

## 🔐 Security Best Practices

### 1. API Key Management
```typescript
// ❌ NEVER expose API keys in client code
const API_KEY = 'sk_live_abc123...';

// ✅ Store in environment variables
const API_KEY = process.env.WEATHER_API_KEY;

// ✅ Access only from server-side
// (API routes, server components, reducers)
```

### 2. Input Validation
```typescript
// Validate all external inputs
function validateLocation(location: string): boolean {
  if (!location || location.length < 2 || location.length > 100) {
    return false;
  }
  // Additional validation
  return true;
}

if (!validateLocation(userInput)) {
  throw new Error('Invalid location');
}
```

### 3. Rate Limiting
```typescript
// Implement request throttling
const lastRequest = Date.now();
const MIN_INTERVAL = 10000; // 10 seconds

if (Date.now() - lastRequest < MIN_INTERVAL) {
  console.log('Rate limit: please wait');
  return;
}
```

### 4. Error Messages
```typescript
// ❌ Don't expose internal details
throw new Error(`Database connection failed at ${DB_HOST}:${DB_PORT}`);

// ✅ Use generic messages
throw new Error('Unable to fetch data. Please try again later.');
```

---

## 📊 API Performance Tips

### 1. Caching
```typescript
const cache = new Map();
const CACHE_DURATION = 600000; // 10 minutes

async function getCachedWeather(location: string) {
  const cached = cache.get(location);
  if (cached && Date.now() - cached.timestamp < CACHE_DURATION) {
    return cached.data;
  }

  const data = await fetchWeatherData(location);
  cache.set(location, { data, timestamp: Date.now() });
  return data;
}
```

### 2. Batch Requests
```typescript
// ❌ Multiple sequential requests
for (const location of locations) {
  await fetchWeather(location);
}

// ✅ Parallel batch request
await Promise.all(
  locations.map(location => fetchWeather(location))
);
```

### 3. Debouncing
```typescript
import { debounce } from 'lodash';

const debouncedSearch = debounce(async (query: string) => {
  const results = await searchLocations(query);
  setResults(results);
}, 300);
```

---

## 🧪 Testing API Integration

### Mock Weather Response
```typescript
export function getMockWeatherData(): WeatherResponse {
  return {
    location: { name: 'Jakarta', region: 'Jakarta', country: 'Indonesia' },
    current: { temp_c: 28, humidity: 75, wind_kph: 15 },
    forecast: { forecastday: [/* ... */] }
  };
}
```

### Test Proxy Endpoint
```typescript
describe('API Proxy', () => {
  it('should forward requests correctly', async () => {
    const response = await fetch('/api/proxy', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        protocol: 'https',
        origin: 'api.example.com',
        path: '/test',
        method: 'GET',
        headers: {}
      })
    });

    expect(response.ok).toBe(true);
  });
});
```

---

## 📞 Support

For API integration issues:
- **GitHub Issues**: [Report bugs](https://github.com/yourusername/rantai-agroviz/issues)
- **Discussions**: [Ask questions](https://github.com/yourusername/rantai-agroviz/discussions)
- **Email**: support@rantai.elpeef.com

---

**Last Updated:** January 9, 2025

**Version:** 0.2.0
