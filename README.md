# Elys Asset Registry

Official Elys Network asset registry providing standardized blockchain and token configurations for all Elys ecosystem projects. This registry serves as the single source of truth for chain metadata, RPC endpoints, token information, and feature capabilities across the entire Elys ecosystem.

## 🎯 Purpose

- **Universal Access**: Consumable by any programming language (Go, Java, JavaScript, C++, Python, Rust)
- **Centralized Configuration**: Single source of truth for all blockchain assets
- **Standardized Format**: Standardized data structure with JSON Schema validation
- **Automatic Updates**: Centralized updates that propagate to all applications
- **Multi-Environment**: Support for mainnet, testnet and devnet

## 🚀 Quick Start

### Direct JSON Access

The registry is available as static JSON files:

```bash
# Complete registry
curl https://registry.elys.network/assets.json

# Mainnet assets only
curl https://registry.elys.network/assets/mainnet.json

# Specific asset
curl https://registry.elys.network/assets/cosmos.json

# Validation schema
curl https://registry.elys.network/schema.json
```

### Available Endpoints

| Endpoint | Description |
|----------|-------------|
| `/assets.json` | Complete registry |
| `/assets/mainnet.json` | Mainnet assets only |
| `/assets/testnet.json` | Testnet assets only |
| `/assets/{asset-key}.json` | Specific asset |
| `/currencies.json` | List of all currencies |
| `/schema.json` | JSON Schema for validation |

## 📊 Data Structure

```json
{
  "assets": {
    "cosmos": {
      "chainNetwork": "mainnet",
      "chainId": "cosmoshub-4",
      "chainName": "Cosmos Hub",
      "addressPrefix": "cosmos",
      "rpcURL": "https://cosmos-rpc.publicnode.com:443",
      "restURL": "https://cosmos-api.publicnode.com",
      "explorerURL": {
        "transaction": "https://mintscan.io/cosmos/transactions/{transaction}"
      },
      "isEnabled": true,
      "priority": 1,
      "currencies": [
        {
          "coinDenom": "ATOM",
          "coinMinimalDenom": "uatom",
          "coinDecimals": 6,
          "canSwap": true,
          "canDeposit": true,
          "isFeeCurrency": true
        }
      ]
    }
  }
}
```

## 🔧 Integration Examples

### JavaScript/TypeScript
```javascript
const response = await fetch('https://registry.elys.network/assets.json');
const registry = await response.json();
const cosmosAsset = registry.assets.cosmos;
```

### Go
```go
type AssetRegistry struct {
    Assets map[string]ChainAsset `json:"assets"`
}

resp, _ := http.Get("https://registry.elys.network/assets.json")
var registry AssetRegistry
json.NewDecoder(resp.Body).Decode(&registry)
```

### Java
```java
ObjectMapper mapper = new ObjectMapper();
AssetRegistry registry = mapper.readValue(
    new URL("https://registry.elys.network/assets.json"), 
    AssetRegistry.class
);
```

### Python
```python
import requests
registry = requests.get("https://registry.elys.network/assets.json").json()
cosmos_asset = registry["assets"]["cosmos"]
```

### C++
```cpp
// Usando nlohmann/json
json registry = json::parse(curl_response);
auto cosmos = registry["assets"]["cosmos"];
```

### Rust
```rust
#[derive(Deserialize)]
struct AssetRegistry {
    assets: HashMap<String, ChainAsset>,
}

let registry: AssetRegistry = reqwest::get("https://registry.elys.network/assets.json")
    .await?.json().await?;
```

## 📁 Repository Structure

```
elys-asset-registry/
├── 📁 data/
│   ├── assets.json              # Main registry
│   ├── mainnet.json            # Mainnet assets only
│   ├── testnet.json            # Testnet assets only
│   └── currencies.json         # Currencies list
├── 📁 schema/
│   └── asset-registry.schema.json  # JSON Schema
├── 📁 scripts/
│   ├── validate.sh             # Validation script
│   ├── generate-splits.sh      # Generate files by network
│   └── update-version.sh       # Update version
├── 📁 examples/
│   ├── javascript/             # JavaScript examples
│   ├── go/                     # Go examples
│   ├── java/                   # Java examples
│   ├── python/                 # Python examples
│   └── rust/                   # Rust examples
├── 📁 .github/
│   └── workflows/
│       ├── validate.yml        # CI for validation
│       └── deploy.yml          # Automatic deployment
├── 📄 README.md
├── 📄 CONTRIBUTING.md
└── 📄 CHANGELOG.md
└── 📄 .version
```

## ✅ Validation

The registry includes automatic validation:

```bash
# Validate JSON structure
./scripts/validate.sh

# Verify against schema
ajv validate -s schema/asset-registry.schema.json -d data/assets.json
```

### Validation Rules

- ✅ Valid and well-formatted JSON
- ✅ Complies with defined JSON Schema
- ✅ No duplicate chainIds
- ✅ Valid URLs for RPC/REST endpoints
- ✅ Required properties present
- ✅ Valid date formats

## 🤝 Contributing

### Adding New Assets

1. Fork the repository
2. Add asset to `data/assets.json` following the schema
3. Run validation: `./scripts/validate.sh`
4. Create pull request

### Asset Schema

Each asset must include:

```json
{
  "chainNetwork": "mainnet|testnet",
  "chainId": "unique-chain-id",
  "chainName": "Human Readable Name",
  "addressPrefix": "bech32prefix",
  "rpcURL": "https://rpc.example.com",
  "restURL": "https://api.example.com",
  "explorerURL": {
    "transaction": "https://explorer.com/tx/{transaction}"
  },
  "currencies": [...]
}
```

### Quality Standards

- 🎯 **Accuracy**: Verified and updated information
- 🔒 **Reliability**: Functional and stable endpoints
- 📊 **Completeness**: All required information present
- 🚀 **Performance**: Endpoints with good latency
- 🔄 **Maintenance**: Regularly updated information

## 🔄 Versioning

We follow [Semantic Versioning](https://semver.org/):

- **MAJOR**: Breaking changes to data structure
- **MINOR**: New assets or compatible features
- **PATCH**: Bug fixes and data updates


## 🛠️ Used By

This registry is used by:

- **Frontend Applications**: Elys web and mobile applications
- **Backend Services**: APIs and microservices
- **CLI Tools**: Command line tools
- **Third-party Integrations**: DeFi and wallet integrations
- **Development Tools**: SDKs and frameworks

## 📊 Statistics

- 📦 **Total Assets**: Multiple supported chains
- 🌍 **Networks**: Mainnet, Testnet
- 🔄 **Update Frequency**: Updates as needed
