# BAB 3: METODOLOGI & RESEARCH FRAMEWORK

## 3.1 OVERALL RESEARCH DESIGN

### 3.1.1 Research Paradigm & Approach

**Research Paradigm:** Mixed-method design combining:
- **Quantitative:** Data analysis, clustering, ML modeling
- **Qualitative:** Literature review, expert validation, case study analysis
- **Design Science:** System architecture, implementation, validation

**Research Type:**
- **Primary:** Applied research (solve real sustainability audit problem)
- **Secondary:** Method research (integrate existing techniques)
- **Tertiary:** Implementation research (deploy operational system)

**Research Questions (RQ):**

```
PRIMARY RESEARCH QUESTION:
"Bagaimana mengintegrasikan K-Means clustering, blockchain smart contracts, 
dan machine learning anomaly detection untuk mengotomasi audit keberlanjutan 
global dan mendeteksi greenwashing?"

SUB-RESEARCH QUESTIONS:
RQ1: Bagaimana mensegmentasi 50+ negara berdasarkan profil emisi & energi 
     menggunakan K-Means clustering, dan apa threshold emisi optimal per segment?

RQ2: Bagaimana merancang dan mengimplementasikan Hyperledger Fabric architecture 
     dengan smart contract yang mengotomasi compliance audit berbasis threshold 
     dari RQ1?

RQ3: Bagaimana merancang ensemble ML model (Isolation Forest + LSTM + Statistical) 
     untuk mendeteksi anomali greenwashing dalam data emisi real-time?

RQ4: Bagaimana mengintegrasikan results dari RQ1, RQ2, RQ3 menjadi sistem end-to-end 
     yang operasional dan validated pada real-world dataset?

RQ5: Seberapa efektif sistem terintegrasi dalam mendeteksi greenwashing, mencegah fraud, 
     dan meningkatkan transparency dalam global sustainability reporting?
```

### 3.1.2 Research Methodology Framework

```
┌─────────────────────────────────────────────────────────────────┐
│              INTEGRATED 3-STAGE RESEARCH FRAMEWORK              │
│                                                                 │
│  STAGE 1: DATA-DRIVEN SEGMENTATION (Months 1-6)               │
│  ├─ RQ1 Focus: Clustering foundation                            │
│  ├─ Deliverable: K-Means results + thresholds                  │
│  └─ Output: Paper 1 (IEEE Access, Q2)                          │
│                                                                 │
│  STAGE 2: BLOCKCHAIN IMPLEMENTATION (Months 6-10)              │
│  ├─ RQ2 Focus: Smart contract architecture                     │
│  ├─ Deliverable: Hyperledger network + chaincode              │
│  └─ Output: Paper 2 (IEEE TSE, Q1)                            │
│                                                                 │
│  STAGE 3: ML INTEGRATION & VALIDATION (Months 10-14)           │
│  ├─ RQ3-5 Focus: Anomaly detection + system integration        │
│  ├─ Deliverable: Full operational system                       │
│  └─ Output: Paper 3 (J. Cleaner Production, Q1)               │
│                                                                 │
│  OVERLAP & INTERDEPENDENCIES:                                  │
│  ├─ Stage 1 results → Feed into Stage 2 design                 │
│  ├─ Stage 2 ledger → Training data untuk Stage 3               │
│  └─ Stage 3 validation → Refine Stages 1-2                     │
└─────────────────────────────────────────────────────────────────┘
```

---

## 3.2 STAGE 1: K-MEANS CLUSTERING & THRESHOLD DETERMINATION

### 3.2.1 Objectives

- **Primary:** Segment 50+ negara menjadi 3 kluster emisi (High/Medium/Low)
- **Secondary:** Determine empirical threshold per kluster
- **Tertiary:** Validate clustering stability across time period 2020-2024

### 3.2.2 Data Collection & Preparation

**Data Source:**
```
Primary Dataset: Kaggle - Climate & Energy Consumption Dataset 2020-2024
├─ Provider: emirhanakku
├─ URL: https://www.kaggle.com/datasets/emirhanakku/climate-and-energy-consumption-dataset-20202024
├─ Period: 1 January 2020 - 31 December 2024
├─ Coverage: 50+ countries, daily records
├─ Total Records: ~100,000 rows
└─ Data Format: CSV (single file global_climate_energy_2020_2024.csv)

Supplementary Data (optional):
├─ World Bank: GDP, population, development index
├─ IEA: Detailed energy statistics
├─ IPCC: Emission factors & methodology
└─ For external validation only
```

**Variables Selection:**

| Variable | Unit | Type | Purpose |
|----------|------|------|---------|
| `date` | YYYY-MM-DD | Temporal | Track time-series |
| `country` | ISO 3166-1 | Categorical | Geographic dimension |
| `co2_emission` | kg/kWh | Continuous | PRIMARY clustering feature |
| `energy_consumption` | MWh | Continuous | Production scale |
| `renewable_share` | % | Continuous | Energy mix dimension |
| `industrial_activity_index` | Index | Continuous | Economic activity proxy |
| `energy_price` | $/kWh | Continuous | Economic context |
| `avg_temperature` | °C | Continuous | Climate context |
| `humidity` | % | Continuous | Climate context |
| `urban_population` | % | Continuous | Population distribution |

**Data Cleaning Pipeline:**

```python
# Step 1: Load & type conversion
df = pd.read_csv('global_climate_energy_2020_2024.csv')
df['date'] = pd.to_datetime(df['date'])

# Step 2: Handle missing values (< 0.2% expected)
df = df.sort_values(['country', 'date'])
df = df.fillna(method='ffill').fillna(method='bfill')  # Forward/backward fill

# Step 3: Remove duplicates
df = df.drop_duplicates(subset=['date', 'country'])

# Step 4: Outlier detection (domain knowledge)
# Extreme values: check jika legitimate atau data error
# Example: Saudi Arabia energy price bisa extreme, tapi legitimate
Q1 = df['co2_emission'].quantile(0.25)
Q3 = df['co2_emission'].quantile(0.75)
IQR = Q3 - Q1
outliers = df[(df['co2_emission'] < Q1-3*IQR) | (df['co2_emission'] > Q3+3*IQR)]
# Review & validate sebelum remove

# Step 5: Final validation
assert df.isnull().sum().sum() == 0, "Still have NaN values"
assert len(df) > 50000, "Too few records"
print(f"Cleaned dataset: {df.shape} records")
```

### 3.2.3 Feature Engineering & Normalization

**Feature Selection untuk Clustering:**

```python
# Select features yang representa sustainability profile
features_for_clustering = [
    'co2_emission',              # Core: emission intensity
    'energy_consumption',         # Scale: energy volume
    'renewable_share',           # Mix: renewable percentage
    'industrial_activity_index', # Context: economic activity
    'energy_price'               # Context: economic incentives
]

X = df.groupby('country')[features_for_clustering].mean()
# Result: 50+ x 5 matrix (countries x features)

# Normalization: StandardScaler (mean=0, std=1)
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Verify normalization
print(f"Mean: {X_scaled.mean(axis=0)}")    # Should be ~0
print(f"Std: {X_scaled.std(axis=0)}")      # Should be ~1
```

**Rationale untuk feature selection:**

| Feature | Why Include | Weight Factor |
|---------|---|---|
| `co2_emission` | Core metric untuk emisi intensity | HIGH |
| `energy_consumption` | Proxy untuk production scale | MEDIUM |
| `renewable_share` | Inverse proxy untuk decarbonization | HIGH |
| `industrial_activity_index` | Context: industrial development | MEDIUM |
| `energy_price` | Economic incentive untuk efficiency | LOW-MEDIUM |

**Why NOT include other variables:**

| Variable | Why Exclude |
|----------|---|
| `date` | Temporal dimension, not feature untuk clustering |
| `country` | Categorical ID, not feature |
| `avg_temperature`, `humidity` | Climate context (fixed geografis), not performance metric |
| `urban_population` | Development level (fixed time), not dynamic metric |

### 3.2.4 Optimal K Determination

**Method 1: Elbow Method**

```python
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

inertias = []
silhouette_scores = []
K_range = range(2, 10)

for k in K_range:
    kmeans = KMeans(n_clusters=k, random_state=42, n_init=10)
    kmeans.fit(X_scaled)
    inertias.append(kmeans.inertia_)
    
    from sklearn.metrics import silhouette_score
    score = silhouette_score(X_scaled, kmeans.labels_)
    silhouette_scores.append(score)

# Plot untuk visualisasi
fig, axes = plt.subplots(1, 2, figsize=(14, 5))
axes[0].plot(K_range, inertias, 'bo-')
axes[0].set_title('Elbow Method')
axes[0].axvline(x=3, color='red', linestyle='--', label='Optimal K=3')
axes[0].legend()

axes[1].plot(K_range, silhouette_scores, 'go-')
axes[1].set_title('Silhouette Score')
axes[1].axvline(x=3, color='red', linestyle='--', label='Optimal K=3')
axes[1].legend()

plt.tight_layout()
plt.savefig('optimal_k_analysis.png', dpi=300)
```

**Decision Criteria untuk K=3:**

```
IF K=2: Oversimplified (tidak capture medium emitters)
IF K=3: ✅ OPTIMAL (clear 3-tier segmentation)
    - High Emitter: Industrial nations (China, USA, India, etc)
    - Medium Emitter: Emerging markets (Brazil, Mexico, etc)
    - Low Emitter: Renewable-based (Iceland, Norway, etc)
IF K=4+: Overfitting (kluster terlalu fragmented, fuzzy boundaries)

Evidence:
├─ Silhouette score peaks at K=3
├─ Elbow point clearly at K=3
└─ Business logic: 3-tier makes sense untuk policy segmentation
```

**Method 2: Silhouette Analysis**

```python
from sklearn.metrics import silhouette_samples
import matplotlib.cm as cm

# Detailed silhouette untuk K=3
kmeans = KMeans(n_clusters=3, random_state=42, n_init=10)
cluster_labels = kmeans.fit_predict(X_scaled)
silhouette_vals = silhouette_samples(X_scaled, cluster_labels)

# Visualisasi: bar plot per cluster
fig, ax = plt.subplots()
y_lower = 10

colors = cm.nipy_spectral(cluster_labels.astype(float) / 3)

for i in range(3):
    ith_cluster_silhouette_vals = silhouette_vals[cluster_labels == i]
    ith_cluster_silhouette_vals.sort()
    
    size_cluster_i = ith_cluster_silhouette_vals.shape[0]
    y_upper = y_lower + size_cluster_i
    
    ax.fill_betweenx(np.arange(y_lower, y_upper),
                      0, ith_cluster_silhouette_vals,
                      facecolor=colors[i], edgecolor=colors[i], alpha=0.7)
    y_lower = y_upper + 10

ax.set_xlabel("Silhouette coefficient")
ax.set_ylabel("Cluster label")
ax.axvline(x=silhouette_vals.mean(), color="red", linestyle="--",
           label=f"Average: {silhouette_vals.mean():.3f}")
ax.legend()
plt.tight_layout()
plt.savefig('silhouette_analysis.png', dpi=300)

print(f"Average silhouette score: {silhouette_vals.mean():.3f}")
print(f"Per-cluster scores: {[silhouette_vals[cluster_labels==i].mean() for i in range(3)]}")
```

### 3.2.5 K-Means Clustering Implementation

```python
# Final K-Means dengan K=3
optimal_k = 3
kmeans_final = KMeans(n_clusters=optimal_k, random_state=42, n_init=10)
country_clusters = kmeans_final.fit_predict(X_scaled)

# Assign cluster labels
df_country_clusters = pd.DataFrame({
    'country': X.index,
    'cluster': country_clusters,
    'co2_mean': X['co2_emission'].values,
    'renewable_mean': X['renewable_share'].values
})

# Rename clusters based pada CO2 emission mean
cluster_emissions = df_country_clusters.groupby('cluster')['co2_mean'].mean()
cluster_ranking = cluster_emissions.argsort()

cluster_names = {
    cluster_ranking[2]: 'High Emitter',    # Highest emissions
    cluster_ranking[1]: 'Medium Emitter',
    cluster_ranking[0]: 'Low Emitter'      # Lowest emissions
}

df_country_clusters['cluster_name'] = df_country_clusters['cluster'].map(cluster_names)

print("CLUSTER ASSIGNMENT:")
print(df_country_clusters.sort_values('cluster_name'))
```

### 3.2.6 Threshold Determination

**Methodology untuk determine thresholds:**

```
THRESHOLD LOGIC:
├─ Per-cluster threshold, tidak global
├─ Based pada percentiles (75th, 90th)
├─ 75th percentile → WARNING level (yellow alert)
├─ 90th percentile → CRITICAL level (red alert)

RATIONALE:
├─ 75th percentile: Top 25% performers within cluster
├─ 90th percentile: Extreme outliers within cluster
├─ Within-cluster comparison: Contextual fairness
└─ Not cross-cluster comparison: Avoid unfair penalty untuk High Emitters
```

**Python Implementation:**

```python
# Calculate thresholds untuk setiap cluster
thresholds = {}

for cluster_id in range(3):
    # Get countries dalam cluster ini
    countries_in_cluster = df_country_clusters[
        df_country_clusters['cluster'] == cluster_id
    ]['country'].values
    
    # Get semua CO2 values untuk negara-negara ini (full time series)
    cluster_emissions_ts = df[
        df['country'].isin(countries_in_cluster)
    ]['co2_emission'].values
    
    # Calculate percentiles
    p75 = np.percentile(cluster_emissions_ts, 75)  # WARNING threshold
    p90 = np.percentile(cluster_emissions_ts, 90)  # CRITICAL threshold
    p50 = np.percentile(cluster_emissions_ts, 50)  # Median
    
    cluster_name = cluster_names[cluster_id]
    
    thresholds[cluster_name] = {
        'countries': list(countries_in_cluster),
        'count': len(countries_in_cluster),
        'median': round(p50, 4),
        'warning_threshold': round(p75, 4),
        'critical_threshold': round(p90, 4),
        'max_observed': round(cluster_emissions_ts.max(), 4),
        'mean_observed': round(cluster_emissions_ts.mean(), 4)
    }

# Display results
import json
print(json.dumps(thresholds, indent=2))
```

**Expected Results:**

```json
{
  "High Emitter": {
    "countries": ["China", "USA", "India", "Russia", ...],
    "count": 15,
    "median": 0.62,
    "warning_threshold": 0.75,
    "critical_threshold": 0.88,
    "max_observed": 1.05,
    "mean_observed": 0.68
  },
  "Medium Emitter": {
    "countries": ["Brazil", "Mexico", "Turkey", ...],
    "count": 20,
    "median": 0.40,
    "warning_threshold": 0.48,
    "critical_threshold": 0.58,
    "max_observed": 0.72,
    "mean_observed": 0.44
  },
  "Low Emitter": {
    "countries": ["Iceland", "Norway", "Costa Rica", ...],
    "count": 18,
    "median": 0.15,
    "warning_threshold": 0.22,
    "critical_threshold": 0.30,
    "max_observed": 0.38,
    "mean_observed": 0.18
  }
}
```

### 3.2.7 Validation & Robustness Checks

**Temporal Stability Test:**

```python
# Check: Apakah clustering consistent across years?

for year in [2020, 2021, 2022, 2023, 2024]:
    df_year = df[df['date'].dt.year == year]
    X_year = df_year.groupby('country')[features_for_clustering].mean()
    X_year_scaled = scaler.transform(X_year)
    
    # Re-cluster
    clusters_year = kmeans_final.predict(X_year_scaled)
    
    # Compare dengan overall clustering
    consistency_score = np.mean(clusters_year == country_clusters)
    print(f"Year {year} consistency: {consistency_score:.2%}")

# Expected: > 80% consistency (allow some variation)
```

**Geographic Diversity Check:**

```python
# Verify: Apakah clusters geografically diverse (not regional biased)?

# Group by region
regions = {
    'Asia': ['China', 'India', 'Japan', 'Korea', ...],
    'Americas': ['USA', 'Brazil', 'Mexico', 'Canada', ...],
    'Europe': ['Germany', 'France', 'UK', 'Russia', ...],
    'Africa': ['South Africa', 'Egypt', ...],
    'Oceania': ['Australia', 'New Zealand', ...]
}

for cluster_id in range(3):
    countries_cluster = set(df_country_clusters[
        df_country_clusters['cluster'] == cluster_id
    ]['country'].values)
    
    print(f"\nCluster {cluster_id}: Geographic distribution")
    for region, region_countries in regions.items():
        count = len(countries_cluster & set(region_countries))
        print(f"  {region}: {count} countries")

# Expected: Mix of regions dalam each cluster (tidak monolithic)
```

---

## 3.3 STAGE 2: HYPERLEDGER FABRIC BLOCKCHAIN IMPLEMENTATION

### 3.3.1 Objectives

- **Primary:** Design & implement Hyperledger Fabric network untuk real-time emission recording
- **Secondary:** Develop smart contract (chaincode) dengan threshold-based alert logic
- **Tertiary:** Validate system performance & security

### 3.3.2 System Architecture Design

**Network Topology:**

```
┌──────────────────────────────────────────────────────────────────┐
│                 HYPERLEDGER FABRIC NETWORK                       │
│                                                                  │
│  ORGANIZATIONS (5 network participants):                        │
│  ├─ China Organization                                          │
│  ├─ USA Organization                                            │
│  ├─ Germany Organization                                        │
│  ├─ Regulator Organization (Government/UN)                      │
│  └─ Observer Organization (NGO/Media)                           │
│                                                                  │
│  NODES PER ORGANIZATION:                                        │
│  ├─ Peer node (maintain ledger copy)                            │
│  └─ CA (Certificate Authority untuk identity)                   │
│                                                                  │
│  CONSENSUS MECHANISM:                                           │
│  ├─ Orderer (Raft consensus) - centralized ordering service     │
│  └─ Endorsement policy: Require approval dari 2+ peers          │
│                                                                  │
│  CHANNELS (private subnetworks):                                │
│  ├─ emission-data-channel (all participants)                    │
│  ├─ regulatory-channel (Regulator + Peers)                      │
│  └─ audit-channel (Regulator only)                              │
└──────────────────────────────────────────────────────────────────┘
```

**Network Configuration (docker-compose.yaml structure):**

```yaml
# Pseudo-configuration (simplified)

version: '3.7'

services:
  # Certificate Authority
  ca.org1.example.com:
    image: hyperledger/fabric-ca
    environment:
      - FABRIC_CA_HOME=/etc/hyperledger/fabric-ca-server

  # Peer nodes (1 per organization)
  peer0.org1.example.com:
    image: hyperledger/fabric-peer
    environment:
      - CORE_PEER_ID=peer0.org1.example.com
      - CORE_PEER_CHAINCODEADDRESS=peer0.org1.example.com:7052

  # Orderer service
  orderer.example.com:
    image: hyperledger/fabric-orderer
    environment:
      - ORDERER_CFG_PATH=/var/hyperledger/config

  # CouchDB (state database)
  couchdb:
    image: hyperledger/fabric-couchdb
    ports:
      - "5984:5984"
```

### 3.3.3 Smart Contract (Chaincode) Design

**Chaincode Language:** Golang (production-grade, type-safe)

**Core Functions:**

```go
// SustainabilityAuditChaincode.go

package main

import (
    "encoding/json"
    "fmt"
    "github.com/hyperledger/fabric-contract-api-go/contractapi"
    "time"
)

// EmissionRecord: data structure untuk emission data
type EmissionRecord struct {
    Country              string    `json:"country"`
    Timestamp            int64     `json:"timestamp"`
    CO2Emission          float64   `json:"co2_emission"`       // kg/kWh
    EnergyConsumption    float64   `json:"energy_consumption"` // MWh
    RenewableShare       float64   `json:"renewable_share"`    // %
    Cluster              string    `json:"cluster"`            // High/Medium/Low
    Status               string    `json:"status"`             // GREEN/YELLOW/RED
    TxHash               string    `json:"tx_hash"`            // blockchain transaction hash
    AnomalyScore         float64   `json:"anomaly_score"`      // ML anomaly detection result
}

// ThresholdConfig: threshold per cluster
type ThresholdConfig struct {
    Cluster              string  `json:"cluster"`
    WarningThreshold     float64 `json:"warning_threshold"`
    CriticalThreshold    float64 `json:"critical_threshold"`
}

// SustainabilityAuditContract: smart contract business logic
type SustainabilityAuditContract struct {
    contractapi.Contract
}

// Initialize: set thresholds saat deploy
func (s *SustainabilityAuditContract) Initialize(ctx contractapi.TransactionContextInterface,
    thresholdsJSON string) error {
    
    // Only authorized deployer can initialize
    // Parse thresholds dari JSON
    
    var thresholds []ThresholdConfig
    err := json.Unmarshal([]byte(thresholdsJSON), &thresholds)
    if err != nil {
        return fmt.Errorf("failed to parse thresholds: %v", err)
    }
    
    // Store di ledger
    for _, threshold := range thresholds {
        key := fmt.Sprintf("threshold-%s", threshold.Cluster)
        thresholdBytes, _ := json.Marshal(threshold)
        ctx.GetStub().PutState(key, thresholdBytes)
    }
    
    return nil
}

// RecordEmission: main function untuk record emission data
func (s *SustainabilityAuditContract) RecordEmission(ctx contractapi.TransactionContextInterface,
    country string, co2Emission float64, energyConsumption float64,
    renewableShare float64, cluster string, anomalyScore float64) (*EmissionRecord, error) {
    
    // Input validation
    if country == "" || co2Emission < 0 {
        return nil, fmt.Errorf("invalid input parameters")
    }
    
    // Determine status based threshold
    thresholdKey := fmt.Sprintf("threshold-%s", cluster)
    thresholdBytes, err := ctx.GetStub().GetState(thresholdKey)
    if err != nil {
        return nil, fmt.Errorf("failed to read threshold: %v", err)
    }
    
    var threshold ThresholdConfig
    json.Unmarshal(thresholdBytes, &threshold)
    
    // Logic untuk determine status
    status := "GREEN"
    alertSeverity := ""
    
    if co2Emission > threshold.CriticalThreshold {
        status = "RED"
        alertSeverity = "CRITICAL"
    } else if co2Emission > threshold.WarningThreshold {
        status = "YELLOW"
        alertSeverity = "WARNING"
    }
    
    // Create emission record
    record := EmissionRecord{
        Country:           country,
        Timestamp:         time.Now().Unix(),
        CO2Emission:       co2Emission,
        EnergyConsumption: energyConsumption,
        RenewableShare:    renewableShare,
        Cluster:           cluster,
        Status:            status,
        TxHash:            ctx.GetStub().GetTxID(),
        AnomalyScore:      anomalyScore,
    }
    
    // Store dalam ledger (immutable)
    recordKey := fmt.Sprintf("emission-%s-%d", country, record.Timestamp)
    recordBytes, _ := json.Marshal(record)
    ctx.GetStub().PutState(recordKey, recordBytes)
    
    // Emit event untuk notification
    ctx.GetStub().SetEvent("EmissionRecorded", recordBytes)
    
    // Trigger alert jika needed
    if alertSeverity != "" {
        s.TriggerAlert(ctx, country, alertSeverity, co2Emission, threshold.CriticalThreshold)
    }
    
    return &record, nil
}

// TriggerAlert: handle alert logic
func (s *SustainabilityAuditContract) TriggerAlert(ctx contractapi.TransactionContextInterface,
    country string, severity string, currentValue float64, threshold float64) error {
    
    alertData := map[string]interface{}{
        "country":      country,
        "severity":     severity,
        "currentValue": currentValue,
        "threshold":    threshold,
        "timestamp":    time.Now().Unix(),
    }
    
    alertBytes, _ := json.Marshal(alertData)
    ctx.GetStub().SetEvent("AlertTriggered", alertBytes)
    
    // Jika RED alert: execute compliance action
    if severity == "CRITICAL" {
        ctx.GetStub().SetEvent("ComplianceAction", []byte(
            fmt.Sprintf("LOCK_FINANCING for %s - exceeds critical threshold", country),
        ))
        
        // Could call external system untuk:
        // - Lock financing transactions
        // - Notify regulator
        // - Initiate investigation
    }
    
    return nil
}

// QueryEmissionHistory: query historical data
func (s *SustainabilityAuditContract) QueryEmissionHistory(ctx contractapi.TransactionContextInterface,
    country string) ([]EmissionRecord, error) {
    
    queryString := fmt.Sprintf(`
        {
            "selector": {
                "country": "%s"
            },
            "sort": ["timestamp"]
        }
    `, country)
    
    resultsIterator, err := ctx.GetStub().GetQueryResultsIterator(queryString)
    if err != nil {
        return nil, err
    }
    defer resultsIterator.Close()
    
    var records []EmissionRecord
    for resultsIterator.HasNext() {
        queryResponse, err := resultsIterator.Next()
        if err != nil {
            return nil, err
        }
        
        var record EmissionRecord
        json.Unmarshal(queryResponse.Value, &record)
        records = append(records, record)
    }
    
    return records, nil
}

// UpdateThreshold: admin function untuk update thresholds
func (s *SustainabilityAuditContract) UpdateThreshold(ctx contractapi.TransactionContextInterface,
    cluster string, newWarning float64, newCritical float64) error {
    
    // Authorization check (only regulator)
    // (In production: verify sender certificate)
    
    threshold := ThresholdConfig{
        Cluster:           cluster,
        WarningThreshold:  newWarning,
        CriticalThreshold: newCritical,
    }
    
    key := fmt.Sprintf("threshold-%s", cluster)
    thresholdBytes, _ := json.Marshal(threshold)
    ctx.GetStub().PutState(key, thresholdBytes)
    
    ctx.GetStub().SetEvent("ThresholdUpdated", thresholdBytes)
    return nil
}

// Main entry point
func main() {
    cc, err := contractapi.NewChaincode(&SustainabilityAuditContract{})
    if err != nil {
        fmt.Printf("Error creating chaincode: %s", err)
        return
    }
    
    if err := cc.Start(); err != nil {
        fmt.Printf("Error starting chaincode: %s", err)
    }
}
```

### 3.3.4 Deployment & Testing

**Deployment Steps:**

```bash
# 1. Install Hyperledger Fabric binaries
export PATH=$PATH:~/fabric-samples/bin

# 2. Start network
cd fabric-samples/test-network
./network.sh up createChannel -c emission-data-channel

# 3. Package chaincode
peer lifecycle chaincode package sustainability.tar.gz \
  --path ~/sustainability-chaincode/ \
  --lang golang \
  --label sustainability_1

# 4. Install chaincode pada peers
peer lifecycle chaincode install sustainability.tar.gz

# 5. Approve chaincode untuk each organization
peer lifecycle chaincode approveformyorg \
  --channelID emission-data-channel \
  --name sustainabilityaudit \
  --version 1.0 \
  --sequence 1

# 6. Commit chaincode
peer lifecycle chaincode commit \
  --channelID emission-data-channel \
  --name sustainabilityaudit \
  --version 1.0 \
  --sequence 1

# 7. Initialize thresholds
peer chaincode invoke \
  -C emission-data-channel \
  -n sustainabilityaudit \
  -c '{"function":"Initialize","Args":["<thresholds_json>"]}'
```

**Unit Testing (Go):**

```go
// sustainabilityaudit_test.go

package main

import (
    "testing"
    "github.com/hyperledger/fabric-chaincode-go/shim"
    "github.com/hyperledger/fabric-protos-go/peer"
)

func TestRecordEmission(t *testing.T) {
    // Setup mock context
    stub := shim.NewMockStub("sustainabilityaudit", new(SustainabilityAuditContract))
    
    // Initialize thresholds
    res := stub.MockInvoke("1", [][]byte{
        []byte("Initialize"),
        []byte(`[{"cluster":"High Emitter","warning":0.75,"critical":0.88}]`),
    })
    
    if res.Status != shim.OK {
        t.Fatalf("Init failed: %s", res.Message)
    }
    
    // Test recording green status
    res = stub.MockInvoke("2", [][]byte{
        []byte("RecordEmission"),
        []byte("China"),
        []byte("0.65"),  // Below warning
        []byte("500"),
        []byte("25"),
        []byte("High Emitter"),
        []byte("0.2"),
    })
    
    if res.Status != shim.OK {
        t.Fatalf("RecordEmission failed: %s", res.Message)
    }
    
    // Verify recording
    res = stub.MockInvoke("3", [][]byte{
        []byte("QueryEmissionHistory"),
        []byte("China"),
    })
    
    if res.Status != shim.OK {
        t.Fatalf("Query failed: %s", res.Message)
    }
    
    t.Logf("Test passed: %s", res.Payload)
}
```

### 3.3.5 REST API Gateway

**Purpose:** Allow external systems to interact dengan blockchain

**Framework:** Express.js (Node.js) dengan fabric-sdk

```javascript
// server.js - REST API Gateway

const express = require('express');
const fabricSDK = require('fabric-sdk-node');
const app = express();

app.use(express.json());

// Initialize fabric gateway
let gateway, network, contract;

async function initFabric() {
    // Connect ke Hyperledger network
    const config = fabricSDK.getDefaultConfig();
    gateway = new fabricSDK.Gateway();
    
    await gateway.connect(config, {
        wallet: // fabric wallet
        identity: 'admin'
    });
    
    network = await gateway.getNetwork('emission-data-channel');
    contract = network.getContract('sustainabilityaudit');
}

// API endpoint 1: Record emission
app.post('/api/emissions/record', async (req, res) => {
    try {
        const { country, co2_emission, energy_consumption, renewable_share, cluster } = req.body;
        
        // Call smart contract
        const result = await contract.submitTransaction('RecordEmission',
            country,
            co2_emission.toString(),
            energy_consumption.toString(),
            renewable_share.toString(),
            cluster,
            "0.2"  // placeholder anomaly score
        );
        
        res.json({
            success: true,
            txHash: result.toString(),
            message: `Emission recorded for ${country}`
        });
    } catch (error) {
        res.status(400).json({ error: error.message });
    }
});

// API endpoint 2: Query history
app.get('/api/emissions/history/:country', async (req, res) => {
    try {
        const { country } = req.params;
        const result = await contract.evaluateTransaction('QueryEmissionHistory', country);
        
        res.json({
            country: country,
            records: JSON.parse(result.toString())
        });
    } catch (error) {
        res.status(400).json({ error: error.message });
    }
});

// API endpoint 3: Update thresholds
app.post('/api/config/thresholds', async (req, res) => {
    try {
        const { cluster, warning, critical } = req.body;
        
        await contract.submitTransaction('UpdateThreshold',
            cluster,
            warning.toString(),
            critical.toString()
        );
        
        res.json({ success: true, message: `Threshold updated for ${cluster}` });
    } catch (error) {
        res.status(400).json({ error: error.message });
    }
});

app.listen(3000, async () => {
    await initFabric();
    console.log('REST API Gateway listening on port 3000');
});
```

---

## 3.4 STAGE 3: ML ANOMALY DETECTION & SYSTEM INTEGRATION

### 3.4.1 Objectives

- **Primary:** Build ensemble ML model untuk detect greenwashing anomalies
- **Secondary:** Integrate dengan blockchain results untuk verification
- **Tertiary:** End-to-end system validation & performance metrics

### 3.4.2 ML Data Preparation

**Training Data Source:**

```python
# Data untuk train ML model dari blockchain ledger

# Query historical emissions dari blockchain
emissions_data = []
for country in countries_list:
    history = contract.evaluateTransaction('QueryEmissionHistory', country)
    emissions_data.extend(json.loads(history))

# Convert ke time-series format
df_timeseries = pd.DataFrame(emissions_data)
df_timeseries['date'] = pd.to_datetime(df_timeseries['timestamp'], unit='s')
df_timeseries = df_timeseries.sort_values('date')

# Features untuk ML models
feature_columns = [
    'co2_emission',
    'energy_consumption',
    'renewable_share',
    'industrial_activity_index'
]

X_train = df_timeseries[feature_columns].values
```

### 3.4.3 Isolation Forest Implementation

```python
from sklearn.ensemble import IsolationForest

# Train Isolation Forest
iso_forest = IsolationForest(
    contamination=0.05,  # Expect ~5% anomalies
    random_state=42,
    n_estimators=100
)

# Fit model
iso_forest.fit(X_train)

# Predict anomalies
anomaly_scores_if = iso_forest.score_samples(X_train)
predictions_if = iso_forest.predict(X_train)

# Normalize scores ke 0-1 range
from sklearn.preprocessing import MinMaxScaler
scaler_if = MinMaxScaler(feature_range=(0, 1))
anomaly_scores_if_normalized = scaler_if.fit_transform(
    anomaly_scores_if.reshape(-1, 1)
).flatten()

print(f"Isolation Forest: {sum(predictions_if == -1)} anomalies detected")
```

### 3.4.4 LSTM Autoencoder Implementation

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import LSTM, RepeatVector, TimeDistributed, Dense
from sklearn.preprocessing import MinMaxScaler

# Prepare time-series sequences
sequence_length = 30  # 30-day window

def create_sequences(data, seq_length):
    X = []
    for i in range(len(data) - seq_length):
        X.append(data[i:i+seq_length])
    return np.array(X)

X_sequences = create_sequences(X_train, sequence_length)

# Normalize
scaler_lstm = MinMaxScaler()
X_scaled = scaler_lstm.fit_transform(X_train.reshape(-1, 1)).reshape(X_train.shape)
X_sequences_scaled = create_sequences(X_scaled, sequence_length)

# Build LSTM Autoencoder
model = Sequential([
    LSTM(32, activation='relu', input_shape=(sequence_length, X_train.shape[1]),
         return_sequences=False),
    RepeatVector(sequence_length),
    LSTM(32, activation='relu', return_sequences=True),
    TimeDistributed(Dense(X_train.shape[1]))
])

model.compile(optimizer='adam', loss='mse')

# Train
history = model.fit(X_sequences_scaled, X_sequences_scaled,
                   epochs=50, batch_size=32, validation_split=0.1)

# Predict & calculate reconstruction error
reconstructed = model.predict(X_sequences_scaled)
reconstruction_errors = np.mean(np.abs(X_sequences_scaled - reconstructed), axis=(1, 2))

# Normalize
scaler_lstm_ae = MinMaxScaler(feature_range=(0, 1))
anomaly_scores_lstm = scaler_lstm_ae.fit_transform(
    reconstruction_errors.reshape(-1, 1)
).flatten()

print(f"LSTM: Mean reconstruction error: {np.mean(reconstruction_errors):.4f}")
```

### 3.4.5 Statistical Anomaly Detection

```python
from scipy import stats

# Z-Score method
z_scores = np.abs(stats.zscore(X_train[:, 0]))  # CO2 emission column
anomaly_threshold_z = 3

# IQR method
Q1 = np.percentile(X_train[:, 0], 25)
Q3 = np.percentile(X_train[:, 0], 75)
IQR = Q3 - Q1
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

# Combine both methods
anomaly_scores_stat = np.zeros(len(X_train))
for i in range(len(X_train)):
    z_anomaly = 1.0 if z_scores[i] > 3 else z_scores[i] / 3
    iqr_anomaly = 1.0 if (X_train[i, 0] < lower_bound or X_train[i, 0] > upper_bound) else 0.0
    anomaly_scores_stat[i] = (z_anomaly + iqr_anomaly) / 2

# Normalize ke 0-1
anomaly_scores_stat = (anomaly_scores_stat - anomaly_scores_stat.min()) / \
                     (anomaly_scores_stat.max() - anomaly_scores_stat.min())

print(f"Statistical: {sum(anomaly_scores_stat > 0.5)} high-risk points")
```

### 3.4.6 Ensemble Voting & Final Score

```python
# Combine semua 3 models dengan weighted voting

weights = {
    'isolation_forest': 0.35,
    'lstm_autoencoder': 0.35,
    'statistical': 0.30
}

# Ensure same length
min_length = min(len(anomaly_scores_if_normalized), 
                 len(anomaly_scores_lstm),
                 len(anomaly_scores_stat))

ensemble_scores = (
    weights['isolation_forest'] * anomaly_scores_if_normalized[:min_length] +
    weights['lstm_autoencoder'] * anomaly_scores_lstm[:min_length] +
    weights['statistical'] * anomaly_scores_stat[:min_length]
)

# Decision logic
GREEN_THRESHOLD = 0.3
YELLOW_THRESHOLD = 0.6
RED_THRESHOLD = 0.8

anomaly_labels = []
for score in ensemble_scores:
    if score >= RED_THRESHOLD:
        anomaly_labels.append('RED')
    elif score >= YELLOW_THRESHOLD:
        anomaly_labels.append('YELLOW')
    elif score >= GREEN_THRESHOLD:
        anomaly_labels.append('ORANGE')
    else:
        anomaly_labels.append('GREEN')

print(f"Ensemble final anomaly classifications:")
print(f"  RED: {sum([x == 'RED' for x in anomaly_labels])}")
print(f"  YELLOW: {sum([x == 'YELLOW' for x in anomaly_labels])}")
print(f"  ORANGE: {sum([x == 'ORANGE' for x in anomaly_labels])}")
print(f"  GREEN: {sum([x == 'GREEN' for x in anomaly_labels])}")
```

### 3.4.7 Integration dengan Blockchain

```python
# Send ML results ke blockchain untuk verification

for i, country in enumerate(countries_list):
    anomaly_score = ensemble_scores[i]
    
    # Get current emission from blockchain
    current_emission = emissions_data[i]['co2_emission']
    cluster = emissions_data[i]['cluster']
    
    # Update blockchain dengan ML anomaly score
    contract.submitTransaction(
        'RecordEmission',
        country,
        str(current_emission),
        str(emissions_data[i]['energy_consumption']),
        str(emissions_data[i]['renewable_share']),
        cluster,
        str(anomaly_score)  # ML anomaly score
    )
    
    print(f"{country}: Anomaly score {anomaly_score:.3f} recorded on blockchain")

# Query blockchain untuk verify
for country in countries_list:
    history = contract.evaluateTransaction('QueryEmissionHistory', country)
    records = json.loads(history)
    latest = records[-1]
    print(f"{country}: Latest anomaly score: {latest['anomaly_score']}")
```

---

## 3.5 VALIDATION STRATEGY

### 3.5.1 Data Validation

**Completeness Check:**

```python
# Ensure no missing data dalam final dataset
assert df.isnull().sum().sum() == 0, "Still have NaN"
assert len(df) >= 50000, "Not enough records"
print(f"✅ Data completeness: 100%")
```

**Temporal Continuity:**

```python
# Check: Apakah ada gaps dalam time series?
dates = sorted(df['date'].unique())
date_diffs = pd.Series(dates).diff().dt.days

gaps = date_diffs[date_diffs > 1]
if len(gaps) == 0:
    print(f"✅ No temporal gaps detected")
else:
    print(f"⚠️ Found {len(gaps)} gaps - investigate")
```

### 3.5.2 Clustering Validation

**Internal Validation:**

```python
from sklearn.metrics import davies_bouldin_score, calinski_harabasz_score

# Davies-Bouldin Index (lower is better)
db_score = davies_bouldin_score(X_scaled, kmeans_final.labels_)
print(f"Davies-Bouldin Index: {db_score:.3f} (lower is better)")

# Calinski-Harabasz Score (higher is better)
ch_score = calinski_harabasz_score(X_scaled, kmeans_final.labels_)
print(f"Calinski-Harabasz Score: {ch_score:.1f} (higher is better)")
```

**External Validation (Domain Expert):**

```
Submit clustering results untuk domain expert review:
├─ Environmental scientist
├─ Energy policy maker
├─ ESG investment professional
└─ Ask: "Does clustering align dengan real-world emission profiles?"

Expected: >80% agreement dengan expert judgment
```

### 3.5.3 Blockchain Testing

**Functional Testing:**

```bash
# Test 1: Can record emission?
peer chaincode invoke -C emission-channel -n audit -c '{"function":"RecordEmission","Args":["China","0.7"]}'
# Expected: Success ✓

# Test 2: Can query history?
peer chaincode query -C emission-channel -n audit -c '{"function":"QueryEmissionHistory","Args":["China"]}'
# Expected: Return list of records ✓

# Test 3: Does alert trigger?
peer chaincode invoke -C emission-channel -n audit -c '{"function":"RecordEmission","Args":["China","0.95"]}'
# Expected: Event "AlertTriggered" emitted ✓

# Test 4: Can update thresholds?
peer chaincode invoke -C emission-channel -n audit -c '{"function":"UpdateThreshold","Args":["High","0.8","0.95"]}'
# Expected: Success ✓
```

**Performance Testing:**

```python
import time

# Measure transaction latency
start = time.time()
for i in range(100):
    contract.submitTransaction('RecordEmission', 'China', '0.7', '500', '25', 'High', '0.2')
end = time.time()

avg_latency = (end - start) / 100
throughput = 100 / (end - start)

print(f"Average latency: {avg_latency*1000:.1f} ms")
print(f"Throughput: {throughput:.0f} TPS (transactions per second)")

# Expected: < 500ms latency, > 10 TPS
```

### 3.5.4 ML Model Validation

**Holdout Test Set:**

```python
# Split data: 70% train, 30% test
train_size = int(len(df_timeseries) * 0.7)
train_data = df_timeseries[:train_size]
test_data = df_timeseries[train_size:]

# Train models on train_data
# Evaluate on test_data

# Metrics
from sklearn.metrics import precision_score, recall_score, f1_score

# Assume test_data has ground truth labels (from domain expert)
y_true = test_data['is_anomaly'].values  # Domain expert annotation
y_pred = (ensemble_scores[-len(test_data):] > 0.6).astype(int)

precision = precision_score(y_true, y_pred)
recall = recall_score(y_true, y_pred)
f1 = f1_score(y_true, y_pred)

print(f"Precision: {precision:.3f}")
print(f"Recall: {recall:.3f}")
print(f"F1-Score: {f1:.3f}")

# Expected: Precision > 0.8, Recall > 0.75, F1 > 0.75
```

**Cross-Validation:**

```python
from sklearn.model_selection import TimeSeriesSplit

tscv = TimeSeriesSplit(n_splits=5)
cv_scores = []

for train_idx, test_idx in tscv.split(X_train):
    X_tr, X_te = X_train[train_idx], X_train[test_idx]
    y_tr, y_te = y_true[train_idx], y_true[test_idx]
    
    # Train model
    # Evaluate on test fold
    # Record score
    
cv_mean = np.mean(cv_scores)
cv_std = np.std(cv_scores)

print(f"Cross-validation score: {cv_mean:.3f} ± {cv_std:.3f}")
```

### 3.5.5 End-to-End Integration Testing

**Scenario Testing:**

```
SCENARIO 1: Normal Operation
├─ Input: Country X reports 0.65 kg/kWh (normal)
├─ Blockchain: Record, status=GREEN
├─ ML: Anomaly score = 0.15 (normal)
├─ Expected: No alert
└─ Result: ✓ PASS

SCENARIO 2: Threshold Breach
├─ Input: Country Y reports 0.92 kg/kWh (exceed critical for High Emitter)
├─ Blockchain: Record, status=RED, trigger alert
├─ ML: Anomaly score = 0.42 (slight anomaly)
├─ Expected: RED alert + financing lock
└─ Result: ✓ PASS

SCENARIO 3: Greenwashing Detection
├─ Input: Country Z reports 0.35 kg/kWh (50% drop from 0.70 previous day)
├─ Blockchain: Record, status=GREEN (within threshold)
├─ ML: Anomaly score = 0.85 (extreme anomaly - pattern break)
├─ Expected: YELLOW alert (investigate despite Green status)
└─ Result: ✓ PASS

SCENARIO 4: Coordinated Fraud
├─ Input: 5 countries report identical 10% reduction → too perfect
├─ Blockchain: All records, status=GREEN
├─ ML: Correlation anomaly detection flags suspicious sync
├─ Expected: Red alert for cross-country coordination check
└─ Result: ✓ PASS
```

---

## 3.6 RESEARCH TIMELINE & MILESTONES

```
STAGE 1: CLUSTERING (Months 1-6)
├─ M1: Literature review complete, PoC design ✓
├─ M2: Data download, cleaning, preprocessing
├─ M3: K-Means clustering implementation
├─ M4: Threshold determination & validation
├─ M5: PAPER 1 SUBMISSION (IEEE Access)
├─ M6: Revise if needed
└─ Deliverable: Paper 1 accepted (expected M9)

STAGE 2: BLOCKCHAIN (Months 6-10)
├─ M6: Hyperledger Fabric setup
├─ M7: Smart contract design & coding
├─ M8: Testing & deployment
├─ M9: REST API development
├─ M10: PAPER 2 SUBMISSION (IEEE TSE)
└─ Deliverable: Paper 2 accepted (expected M12-13)

STAGE 3: ML & INTEGRATION (Months 10-14)
├─ M10: ML data preparation from blockchain
├─ M11: Model training (IF, LSTM, Statistical)
├─ M12: Ensemble voting & integration
├─ M13: End-to-end testing
├─ M14: PAPER 3 SUBMISSION (J. Cleaner Production)
└─ Deliverable: Paper 3 accepted (expected M16-17)

FINALIZATION (Months 14-16)
├─ M14-15: Dissertation writing
├─ M16: DEFENSE & GRADUATION
└─ Deliverable: PhD completed! 🎓
```

---

## 3.7 RISK MANAGEMENT & CONTINGENCY PLANNING

### 3.7.1 Identified Risks

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| **Data quality issues** | Medium | High | Early validation, backup datasets |
| **Hyperledger learning curve** | Medium | Medium | Pre-training workshops, vendor support |
| **ML model overfitting** | Medium | Medium | Cross-validation, regularization |
| **Paper rejection** | Low | High | Prepare alternative journals, quick revision |
| **Timeline pressure** | Medium | Medium | Overlap stages, weekly milestone checks |
| **Lack of domain expert access** | Low | Medium | Leverage academic network, online experts |

### 3.7.2 Contingency Plans

**If Paper 1 rejected from IEEE Access:**
```
Plan B: Submit ke Sustainability (Q2, easier acceptance)
Plan C: Submit ke Energy Policy (Q2)
Timeline: 1 month to revise & resubmit → still on track
```

**If Hyperledger deployment complex:**
```
Plan B: Use simulated blockchain (Ganache) untuk validation
Plan C: Simplify network topology (2 organizations instead of 5)
Timeline: 2 weeks buffer → can delay start of Stage 2 slightly
```

**If ML model performance weak:**
```
Plan B: Use simpler models (Random Forest instead of LSTM)
Plan C: Reduce ensemble complexity (2 models instead of 3)
Timeline: Additional 2 weeks untuk retraining → acceptable
```

---

## 3.8 RESEARCH ETHICS & DATA GOVERNANCE

### 3.8.1 Data Privacy

**Measures:**
- Aggregate country-level data (tidak individual corporation)
- Use public dataset dari Kaggle (already permissioned)
- No personal identifiable information (PII)
- Blockchain privacy channels untuk sensitive emission data

### 3.8.2 Research Integrity

**Commitments:**
- ✅ Transparent methodology (publish all code & data)
- ✅ Reproducible results (version control, documentation)
- ✅ Conflict of interest disclosure (none anticipated)
- ✅ Ethical approval (not required untuk non-human subjects)

### 3.8.3 Data Retention

**Plan:**
- Keep raw dataset: 2 years post-publication
- Keep processed datasets: Permanent (for reproducibility)
- Keep blockchain ledger: Permanent (immutable by nature)

---

## 3.9 CONCLUSION OF METHODOLOGY

**Summary:**

This 3-stage methodology provides **systematic, rigorous approach** untuk research questions:

✅ **Stage 1** addresses RQ1 dengan data-driven clustering & threshold determination  
✅ **Stage 2** addresses RQ2 dengan Hyperledger architecture & smart contracts  
✅ **Stage 3** addresses RQ3-5 dengan ML integration & end-to-end validation  

**Key Strengths:**
- Interdependencies between stages create strong integration
- Real-world data validation (not simulation)
- Comprehensive testing strategy (functional, performance, security)
- Clear timeline dengan realistic milestones
- Risk mitigation plans untuk major blockers

**Expected Outcomes:**
- 3 publikasi Scopus Q1/Q2
- Operational system ready untuk adoption
- Contribution ke literature pada 3 domains (clustering, blockchain, ML)

---

**NEXT: BAB 4 akan cover Expected Results & Contribution ke Knowledge**

