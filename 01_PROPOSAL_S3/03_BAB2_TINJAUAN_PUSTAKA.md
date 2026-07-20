# BAB 2: TINJAUAN PUSTAKA

## 2.1 SUSTAINABILITY AUDIT & ENVIRONMENTAL COMPLIANCE

### 2.1.1 Definisi & Framework

**Sustainability Audit** adalah proses sistematis untuk mengidentifikasi, mengukur, dan memverifikasi kinerja organisasi terhadap environmental dan sustainability objectives (ISO 14001:2015) [4].

**Framework utama yang digunakan industri:**

1. **ISO 14001:2015 - Environmental Management System** [4]
   - Standard untuk environmental compliance
   - Mencakup planning, implementation, checking, improvement
   - Adopted oleh 350,000+ organizations globally
   - Audit dilakukan setiap 1-3 tahun

2. **GRI Standards (Global Reporting Initiative)**
   - Framework untuk sustainability reporting
   - GRI 305: Emissions
   - GRI 302: Energy consumption
   - GRI 306: Waste management
   - Voluntary standard, widely used untuk ESG reporting

3. **Carbon Accounting Standards**
   - Greenhouse Gas Protocol (GHG Protocol) [3]
   - International Carbon Offset Council (ICOC)
   - Carbon Trust Standard
   - Methodologi untuk calculate emissions

4. **Financial ESG Rating Standards**
   - MSCI ESG Ratings
   - Sustainalytics
   - Bloomberg ESG Data
   - Used oleh investor untuk decision-making

### 2.1.2 Current Audit Process & Limitations

**Traditional Audit Flow:**

```
MONTH 1-3: DATA COLLECTION
├─ Company self-reports emissions (biased!)
├─ Collect energy bills, production records
└─ Estimated 50% error rate (Leuenberger et al., 2019) [19]

MONTH 4-9: VERIFICATION & SITE VISIT
├─ External auditor (Big 4: Deloitte, PWC, EY, KPMG)
├─ Manual checking of records
├─ Site inspection (1-2 weeks on-site)
└─ Cost: $2-5 million per audit

MONTH 10-12: REPORT DRAFTING & APPROVAL
├─ Auditor writes report
├─ Client reviews & provides feedback
├─ Final report published
└─ 12 MONTHS TOTAL PROCESS

PROBLEM: Data sudah stale sebelum hasil audit dipublikasi!
```

**Key Limitations:**

| Limitation | Impact | Root Cause |
|-----------|--------|-----------|
| **Manual verification** | Slow, expensive, subjective | Human-dependent review |
| **Delayed reporting** | 6-12 bulan lag | Linear sequential process |
| **No real-time monitoring** | Fraud window exists | Batch processing paradigm |
| **High cost** | Only large corporations can afford | Labor-intensive auditor work |
| **Not transparent** | Different standards per region | Decentralized governance |
| **Greenwashing prone** | Easy to manipulate data | Self-reported basis |

### 2.1.3 Greenwashing: The Growing Problem

**Definition:** Greenwashing adalah praktek korporasi yang mengklaim komitmen environmental tetapi tidak backed by substantive action [5].

**Scale of Problem:**
- 🔴 56% dari sustainability claims di iklan tidak substantive (Nielsen, 2015) [19]
- 🔴 Volkswagen scandal (2015): Claimed "TDI Clean Diesel" — case documented by EPA enforcement actions [6]
- 🔴 Fast fashion industry: "Sustainable collection" dengan highly polluting supply chain

**Detection Difficulty:**
- ❌ No standard verification protocol
- ❌ Self-reported data tidak independent-verified
- ❌ Anomalies dalam data dapat di-explain away
- ❌ Cross-country inconsistencies sulit di-identify

---

## 2.2 BLOCKCHAIN TECHNOLOGY & SMART CONTRACTS

### 2.2.1 Blockchain Fundamentals

**Definition:** Blockchain adalah distributed ledger technology (DLT) yang maintain record transaksi across decentralized network dengan cryptographic security & immutability [8].

**Key Characteristics:**

| Karakteristik | Deskripsi | Benefit untuk Audit |
|---|---|---|
| **Immutability** | Data sekali tercatat tidak bisa diubah retroaktif | Mencegah fraud & data manipulation |
| **Transparency** | All stakeholders melihat semua transactions | Accountability & openness |
| **Decentralization** | Tidak ada single point of failure | Reduces corruption risk |
| **Cryptography** | Setiap block ter-hash & linked | Data integrity assurance |
| **Consensus** | Multiple nodes agree sebelum accept transaction | Democratic validation |

### 2.2.2 Blockchain Architecture Overview

```
┌─────────────────────────────────────────────────────────┐
│                    BLOCKCHAIN NETWORK                    │
│                                                          │
│  ┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐        │
│  │ Node 1 │  │ Node 2 │  │ Node 3 │  │ Node N │        │
│  │(China) │  │(USA)   │  │(German)│  │(Regulator)     │
│  └────────┘  └────────┘  └────────┘  └────────┘        │
│      │           │           │           │              │
│      └───────────┼───────────┼───────────┘              │
│                  │           │                          │
│              ┌───────────────────┐                      │
│              │  SHARED LEDGER    │                      │
│              │                   │                      │
│              │  Block 1 ────→    │                      │
│              │  Block 2 ────→    │                      │
│              │  Block 3 ────→    │                      │
│              │  (Immutable)      │                      │
│              └───────────────────┘                      │
│                                                          │
│  Consensus: Raft (Hyperledger) atau PoW (Bitcoin)      │
└─────────────────────────────────────────────────────────┘
```

### 2.2.3 Smart Contracts

**Definition:** Smart Contract adalah self-executing program yang berjalan on blockchain, mengotomatisasi agreements ketika kondisi pre-defined terpenuhi (Szabo, 1994; Ethereum, 2015) [8].

**Key Properties:**
1. **Deterministic** — Same input selalu menghasilkan same output
2. **Immutable** — Once deployed, cannot be changed
3. **Autonomous** — Execute automatically tanpa intermediary
4. **Transparent** — Logic dapat di-audit & diverifikasi

### 2.2.4 Hyperledger Fabric vs Public Blockchains

**Comparison untuk use case sustainability audit:**

| Aspek | Hyperledger Fabric | Bitcoin | Ethereum |
|---|---|---|---|
| **Type** | Permissioned | Permissionless | Permissionless |
| **Access Control** | Strict (great untuk regulated industry) | Open to all | Open to all |
| **Consensus** | Raft, PBFT (fast) | PoW (slow) | PoS (medium) |
| **Transaction Speed** | 1000+ TPS | 7 TPS | 15 TPS |
| **Privacy** | Excellent (channels) | Transparent all | Transparent all |
| **Energy Cost** | Low | Extremely high | High |
| **Smart Contracts** | Chaincode (Go, Node, Java) | Limited | Solidity (powerful) |
| **Enterprise Adoption** | High (Maersk, IBM, etc) | Limited | Growing |
| **Regulatory Compliance** | Excellent | Challenging | Challenging |

**Why Hyperledger untuk sustainability audit:**
✅ Permissioned: Only authorized nations/corporations join  [9]
✅ Privacy channels: Sensitive data protected  [9]
✅ Fast consensus: Real-time audit trigger
✅ Enterprise-proven: Already used by Maersk, TradeLens  [9]
✅ Energy-efficient: No PoW wastage

### 2.2.5 Related Blockchain Sustainability Studies

**Recent Literature:**

1. **Tiwari et al. (2023)** — "Blockchain for Carbon Credit Management" [10]
   - Focus: Using blockchain untuk track carbon credits
   - Limitation: Tidak ada ML integration, static thresholds

2. **Sharma et al. (2022)** — "Smart Contracts untuk Environmental Compliance" [11]
   - Focus: Smart contract design untuk compliance
   - Limitation: Belum implement pada Hyperledger, theoretical only

3. **Chen et al. (2021)** — "Supply Chain Transparency via Blockchain" [12]
   - Focus: Track supply chain emissions
   - Limitation: Focused on supply chain, tidak mencakup audit automation

**Gap:** Belum ada paper yang mengintegrasikan clustering + blockchain + ML untuk comprehensive audit system.

---

## 2.3 K-MEANS CLUSTERING & SUSTAINABILITY SEGMENTATION

### 2.3.1 K-Means Algorithm Fundamentals

**Definition:** K-Means adalah unsupervised machine learning algorithm yang mengelompokkan data points menjadi K kluster berdasarkan feature similarity (Lloyd, 1982; MacQueen, 1967) [14], [13].

**Algorithm Steps:**

```
1. INITIALIZE: Random centroid untuk K kluster
2. ASSIGN: Assign setiap point ke nearest centroid
3. UPDATE: Recalculate centroid based on assigned points
4. REPEAT steps 2-3 sampai convergence (centroid tidak berubah)
5. OUTPUT: K kluster dengan centroid clear
```

### 2.3.2 Optimal K Determination

**Methods untuk find optimal K:**

1. **Elbow Method**
2. **Silhouette Analysis**
3. **Davies-Bouldin Index**

### 2.3.3 Application untuk Sustainability Segmentation

**Features untuk clustering:**
```
X = [co2_emission, energy_consumption, renewable_share, 
     industrial_activity_index, energy_price]

Normalization: StandardScaler (mean=0, std=1) untuk equal weighting
```

**Expected Cluster Profiles:**

| Dimensi | High Emitter | Medium Emitter | Low Emitter |
|---|---|---|---|
| Mean CO₂ (kg/kWh) | 0.60–0.80 | 0.30–0.50 | 0.10–0.25 |
| Mean Renewable (%) | 10–25% | 30–50% | 60–95% |
| Mean Industrial Index | 120–150 | 90–120 | 50–80 |
| Contoh Negara | China, USA, India | Brazil, Mexico, Turkey | Iceland, Norway, Costa Rica |

**Why Clustering untuk sustainability audit:**

1. **Benchmark**: Country dapat compare diri dengan peer group
2. **Threshold Setting**: Threshold emisi berbeda per cluster (contextual)
3. **Policy Making**: Government dapat design policy per segment
4. **Investment**: Investor dapat allocate capital per risk profile

### 2.3.4 Related Clustering Studies

**Literature:**

1. **Jolliffe & Cadima (2016)** — PCA overview (opsional untuk dimensionality reduction)
2. **Murtagh & Legendre (2014)** — Hierarchical clustering (alternative)
3. **Moran et al. (2020)** — Clustering countries berdasarkan energy profile

**Gap:** Tidak ada study yang menggabungkan clustering hasil dengan blockchain smart contract logic.

---

## 2.4 MACHINE LEARNING FOR ANOMALY DETECTION

### 2.4.1 Anomaly Detection Concepts

**Definition:** Anomaly detection adalah task mengidentifikasi data points yang deviate significantly dari normal behavior [15].

### 2.4.2 Isolation Forest Algorithm

**Principle:** Anomalies are "few and different" → easier to isolate [16].

### 2.4.3 LSTM Autoencoder for Temporal Anomalies

**LSTM (Long Short-Term Memory):** Good untuk time-series data [17].

### 2.4.4 Statistical Anomaly Detection

Methods: Z-score, IQR (statistical baseline)

### 2.4.5 Ensemble Approach

Combine Isolation Forest, LSTM Autoencoder, and statistical methods for robust detection.

### 2.4.6 Related Anomaly Detection Literature

Foundational papers: [15]–[17]; energy-specific anomaly detection and fraud detection: [18].

---

## 2.5 INTEGRATION OF CLUSTERING, BLOCKCHAIN, & ML

### 2.5.1 Literature Gaps

**Current State:**
- ✅ Papers on blockchain untuk sustainability (but not operational) [10]
- ✅ Papers on clustering untuk environmental segmentation (standalone) [13]
- ✅ Papers on anomaly detection untuk energy (but not emission audit) [15], [16], [17]
- ❌ **NO PAPERS** yang integrate ketiganya secara operasional

**Research Opportunities:**

| Gap | Solution in Our Research |
|---|---|
| **Clustering without action** | → Use thresholds dalam smart contract [13]
| **Blockchain without intelligence** | → Add ML anomaly detection layer [9], [16]
| **ML without verification** | → Blockchain immutably record decisions [8]
| **No real-world validation** | → Validate pada 50-country dataset
| **No publication roadmap** | → 3-paper integrated narrative

---

## 2.6 RELATED WORK SUMMARY TABLE

| Paper | Year | Topic | Relevant To | Gap |
|---|---|---|---|---|
| Nakamoto (Bitcoin) | 2008 | Blockchain foundation | Architecture | Cryptocurrency focus [8] |
| Lloyd (K-Means) | 1982 | Clustering algorithm | Methodology | General, not environmental [14] |
| Chandola et al. | 2009 | Anomaly detection survey | ML component | Not blockchain-aware [15] |
| Liu et al. (IF) | 2008 | Isolation Forest | ML algorithm | General outlier detection [16] |
| Hyperledger Fabric | 2018 | Permissioned blockchain | Architecture | Not sustainability-specific [9] |
| ISO 14001 | 2015 | Environmental standard | Problem context | Manual audit process [4] |
| GRI Standards | 2020 | Sustainability reporting | Problem context | Self-reported data |
| Tiwari et al. | 2023 | Blockchain + carbon credits | Blockchain app | No ML, static thresholds [10] |
| Sharma et al. | 2022 | Smart contracts compliance | Smart contract design | Theoretical, not implemented [11] |
| Chen et al. | 2021 | Supply chain + blockchain | Related domain | Supply chain, not audit [12] |

---

## 2.7 THEORETICAL FOUNDATION

(Section continues — components support one another; references as above.)

---

## 2.8 RESEARCH POSITIONING

(Section continues — contributions and impact; references cross-referenced.)

---

## 2.9 CONCLUSION OF LITERATURE REVIEW

(Summary and positioning; references.)

---

**NEXT: BAB 3 akan detail Methodology & Research Framework**
