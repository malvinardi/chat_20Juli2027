# RENCANA OUTPUT: 3 PUBLIKASI SCOPUS Q1/Q2
## Pengembangan Blockchain untuk Audit Keberlanjutan

**Program:** S3 (Doktor) - Universitas Indonesia  
**Periode:** 16 bulan (Bulan 3 – Bulan 14 S3)  
**Status:** Proposal Rencana Publikasi  
**Tanggal Penyusunan:** 20 Juli 2026

---

## RINGKASAN PUBLIKASI

| # | Judul Paper | Target Journal | Target Q | Timeline | Status |
|---|---|---|---|---|---|
| **Paper 1** | Clustering-Based Sustainability Segmentation of Global Nations Using Energy & Climate Data | IEEE Access / Sustainability | Q2 | Bulan 3–6 | 📋 Preparation |
| **Paper 2** | Hyperledger Fabric Architecture for Real-Time Environmental Compliance Auditing in Green Supply Chains | IEEE Transactions on Software Engineering / Blockchain Research | Q1 | Bulan 6–10 | 📋 Preparation |
| **Paper 3** | Integrated Machine Learning & Blockchain System for Detecting Greenwashing in Sustainability Reporting: Architecture, Implementation & Validation | Journal of Cleaner Production / Environmental Science & Technology | Q1 | Bulan 10–14 | 📋 Preparation |

---

## PAPER 1: CLUSTERING-BASED SUSTAINABILITY SEGMENTATION

### 1.1 METADATA

| Aspek | Detail |
|-------|--------|
| **Judul Lengkap** | "Clustering-Based Sustainability Segmentation of Global Nations Using Energy & Climate Data: Identifying Emission Thresholds for Automated Compliance Auditing" |
| **Target Journal** | IEEE Access (Q2, IF: 3.9) atau Sustainability (Q2, IF: 3.2) |
| **Submission Target** | Bulan 5–6 S3 |
| **Expected Publication** | Bulan 9–10 S3 (4-5 bulan review cycle) |
| **Paper Type** | Research Article (8–12 pages) |
| **Author Order** | Malvin Ardi (1st), Promotor (2nd), Co-Promotor (3rd) |

### 1.2 KONTRIBUSI UTAMA

✅ **Scientific Contribution:**
- Pertama kali menerapkan K-Means Clustering untuk mensegmentasi 50+ negara berdasarkan profil emisi & energi
- Mengidentifikasi 3 kluster sustainability dengan threshold emisi yang statistically valid
- Menyediakan empirical baseline untuk smart contract logic dalam blockchain systems

✅ **Practical Contribution:**
- Framework untuk negara/korporasi mengidentifikasi peer group untuk benchmarking
- Threshold empiris dapat langsung diaplikasikan dalam policy & investment decisions

### 1.3 RESEARCH QUESTIONS

1. **RQ1:** Bagaimana cara mengelompokkan 50+ negara berdasarkan kombinasi emisi, energi, & sustainability metrics?
2. **RQ2:** Apa karakteristik unik setiap kluster? Apa faktor utama pembeda?
3. **RQ3:** Apakah threshold emisi per kluster valid untuk policy making & smart contract implementation?

### 1.4 METODOLOGI

**Data:**
- Dataset: Climate & Energy Consumption 2020–2024 (50+ negara, 1,827 hari)
- Variabel: CO₂ emission, energy consumption, renewable share, industrial activity, energy price

**Methods:**
- Data preprocessing & normalization (StandardScaler)
- Elbow Method & Silhouette Analysis untuk optimal K determination
- K-Means Clustering (K=3)
- PCA untuk visualisasi
- Statistical analysis: mean, std, percentile per cluster

**Validation:**
- Silhouette score & Davies-Bouldin Index
- Temporal stability check: consistency 2020-2024
- Domain expert validation

### 1.5 EXPECTED RESULTS

```
KLUSTER 1: HIGH EMITTER (15 negara)
├─ Negara: China, USA, India, Russia, Japan, Germany, Korea, Iran, Saudi Arabia, Indonesia, etc.
├─ Mean CO₂: 0.65 kg/kWh
├─ Renewable Share: 15–25%
└─ Threshold (90th percentile): 0.82 kg/kWh

KLUSTER 2: MEDIUM EMITTER (20 negara)
├─ Negara: Brazil, Mexico, Turkey, South Africa, Thailand, Vietnam, etc.
├─ Mean CO₂: 0.42 kg/kWh
├─ Renewable Share: 35–45%
└─ Threshold (90th percentile): 0.58 kg/kWh

KLUSTER 3: LOW EMITTER (15+ negara)
├─ Negara: Iceland, Norway, Costa Rica, New Zealand, Canada (hydro/wind), etc.
├─ Mean CO₂: 0.18 kg/kWh
├─ Renewable Share: 70–98%
└─ Threshold (90th percentile): 0.25 kg/kWh
```

### 1.6 OUTLINE PAPER 1

```
1. INTRODUCTION
   1.1 Background: Climate crisis & need for sustainability audit
   1.2 Problem statement: Heterogeneity dalam emisi global
   1.3 Research gap: Belum ada empirical segmentation untuk audit standards
   1.4 Contribution & objectives

2. RELATED WORK
   2.1 Sustainability reporting & compliance standards (ISO 14001, GRI)
   2.2 Clustering methods in environmental studies
   2.3 Emission benchmarking & performance comparison
   2.4 Smart contract requirements (why clustering matters)

3. METHODOLOGY
   3.1 Data collection & preprocessing
   3.2 Feature selection & normalization
   3.3 Optimal K determination (Elbow Method)
   3.4 K-Means Clustering algorithm
   3.5 Cluster characterization & threshold identification

4. RESULTS
   4.1 Cluster profiles (High, Medium, Low emitters)
   4.2 Statistical characteristics per cluster
   4.3 Temporal stability analysis
   4.4 Correlation analysis (renewable vs emisi)
   4.5 Visualization & interpretation

5. DISCUSSION
   5.1 Cluster characteristics & interpretations
   5.2 Implication untuk sustainability policy
   5.3 Threshold validity untuk compliance audit
   5.4 Comparison dengan existing standards (IPCC, IEA)

6. CONCLUSION & FUTURE WORK
   6.1 Key findings
   6.2 Limitations
   6.3 Application untuk blockchain smart contracts
   6.4 Future research directions

7. REFERENCES (40-50 citations)
```

### 1.7 PUBLICATION STRATEGY

- **Timeline:** Submit Bulan 5, Expected acceptance Bulan 9–10
- **Journal Selection:** IEEE Access (lebih mudah accepted, impact factor masih Q2)
- **Review Cycle:** ~4 bulan
- **Minor/Major Revisions:** ~2 minggu untuk revise

---

## PAPER 2: HYPERLEDGER FABRIC ARCHITECTURE FOR COMPLIANCE AUDIT

### 2.1 METADATA

| Aspek | Detail |
|-------|--------|
| **Judul Lengkap** | "Hyperledger Fabric Architecture for Real-Time Environmental Compliance Auditing in Green Supply Chains: Design, Implementation & Validation" |
| **Target Journal** | IEEE Transactions on Software Engineering (Q1, IF: 6.2) atau Blockchain Research (Q1, IF: 5.5) |
| **Submission Target** | Bulan 8–9 S3 |
| **Expected Publication** | Bulan 12–13 S3 (5-6 bulan review cycle) |
| **Paper Type** | System Design & Implementation Paper (12–15 pages) |
| **Author Order** | Malvin Ardi (1st), Promotor (2nd), Co-Promotor (3rd), [Optional: industry partner] |

### 2.2 KONTRIBUSI UTAMA

✅ **Scientific Contribution:**
- Pertama kali design complete Hyperledger Fabric architecture khusus untuk sustainability compliance
- Smart contract logic yang otomatis trigger alert berdasarkan emission thresholds
- Multi-stakeholder integration (negara, korporasi, regulator, NGO, investor)
- Real-time monitoring vs. traditional 6-12 month audit cycle

✅ **Technical Contribution:**
- Chaincode (smart contract) implementation dalam Golang
- REST API untuk third-party integration
- Privacy channels untuk sensitive data protection
- Consensus mechanism optimization untuk high-frequency transactions

### 2.3 RESEARCH QUESTIONS

1. **RQ1:** Bagaimana merancang Hyperledger Fabric network yang scalable untuk global sustainability audit?
2. **RQ2:** Bagaimana smart contract logic dapat mengautomatisasi compliance checking?
3. **RQ3:** Apakah sistem dapat terintegrasi dengan existing environmental reporting standards?

### 2.4 SYSTEM ARCHITECTURE

```
┌─────────────────────────────────────────────────────────┐
│                  BLOCKCHAIN LAYER                        │
│  ┌─────────────────────────────────────────────────────┐ │
│  │  Hyperledger Fabric Network (5+ Peer Nodes)         │ │
│  │  ├─ Orderer (Raft consensus)                        │ │
│  │  ├─ Peer 1 (China)                                  │ │
│  │  ├─ Peer 2 (USA)                                    │ │
│  │  ├─ Peer 3 (Germany)                                │ │
│  │  ├─ Peer 4 (Regulator)                              │ │
│  │  └─ Peer 5 (Observer - NGO)                         │ │
│  └─────────────────────────────────────────────────────┘ │
│                                                          │
│  ┌─────────────────────────────────────────────────────┐ │
│  │  Smart Contract (Chaincode)                         │ │
│  │  ├─ Record emission data                            │ │
│  │  ├─ Validate vs. threshold                          │ │
│  │  ├─ Trigger alert logic                             │ │
│  │  ├─ Update ESG score                                │ │
│  │  └─ Execute financing lock/unlock                   │ │
│  └─────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│              APPLICATION LAYER                           │
│  ├─ REST API Gateway                                     │
│  ├─ Dashboard (Real-time monitoring)                     │
│  ├─ Mobile App (Alert notification)                      │
│  └─ Integration modules (SAP, Salesforce, custom)        │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│              DATA INPUT LAYER                            │
│  ├─ IoT Sensors (Real-time emission measurement)         │
│  ├─ SCADA Systems (Energy grid monitoring)               │
│  ├─ Manual Data Entry (Government reporting)             │
│  └─ Third-party APIs (Weather, electricity generation)   │
└─────────────────────────────────────────────────────────┘
```

### 2.5 SMART CONTRACT PSEUDOCODE

```solidity
// Smart Contract untuk Sustainability Compliance Audit

pragma solidity ^0.5.0;

contract SustainabilityAudit {
    
    struct EmissionRecord {
        string country;
        uint256 timestamp;
        float co2_emission;       // kg/kWh
        string cluster;           // High/Medium/Low
        string status;            // Green/Yellow/Red
        string txHash;
    }
    
    mapping(string => EmissionRecord[]) public emissionHistory;
    mapping(string => float) public thresholds;
    
    event EmissionRecorded(string indexed country, float co2, string status);
    event AlertTriggered(string indexed country, string severity);
    
    // Set thresholds per cluster (dari Paper 1 results)
    function setThreshold(string memory cluster, float warningLevel, float criticalLevel) public {
        // Only authorized (regulator/promotor)
        require(msg.sender == authorizedRegulator);
        thresholds[cluster] = criticalLevel;
    }
    
    // Record emission & auto-audit
    function recordEmission(string memory country, float co2_emission, string memory cluster) public {
        
        uint256 timestamp = now;
        string memory status = "GREEN";
        
        // Get threshold dari cluster
        float threshold = thresholds[cluster];
        
        // Trigger logic
        if (co2_emission > threshold) {
            status = "RED";
            emit AlertTriggered(country, "CRITICAL");
            // Lock financing transactions
            lockFinancing(country);
            // Notify regulator
            notifyRegulator(country, co2_emission, threshold);
        } 
        else if (co2_emission > threshold * 0.8) {
            status = "YELLOW";
            emit AlertTriggered(country, "WARNING");
            // Restrict new investments
            restrictInvestments(country);
        }
        
        // Record to ledger (immutable)
        EmissionRecord memory record = EmissionRecord({
            country: country,
            timestamp: timestamp,
            co2_emission: co2_emission,
            cluster: cluster,
            status: status,
            txHash: getCurrentTxHash()
        });
        
        emissionHistory[country].push(record);
        emit EmissionRecorded(country, co2_emission, status);
    }
    
    // Query historical data
    function getEmissionHistory(string memory country) public view returns (EmissionRecord[]) {
        return emissionHistory[country];
    }
    
    // Anomaly detection trigger (untuk ML integration)
    function triggerAnomalyCheck(string memory country) public {
        // Call ML model for anomaly score
        float anomalyScore = callMLModel(country);
        if (anomalyScore > 0.8) {
            emit AlertTriggered(country, "ANOMALY_DETECTED");
        }
    }
}
```

### 2.6 OUTLINE PAPER 2

```
1. INTRODUCTION
   1.1 Background: Limitations of traditional audit
   1.2 Blockchain potential untuk transparency & automation
   1.3 Gap: Belum ada production-ready architecture untuk compliance
   1.4 Objectives: Design, implement, validate Hyperledger system

2. RELATED WORK
   2.1 Blockchain technology overview (Bitcoin, Ethereum, Hyperledger)
   2.2 Smart contracts untuk supply chain & compliance
   2.3 Environmental data management on blockchain
   2.4 Sustainability auditing standards

3. SYSTEM DESIGN
   3.1 Architecture overview
   3.2 Network topology (peers, orderer, channels)
   3.3 Smart contract design & logic
   3.4 Data model & ledger structure
   3.5 Consensus mechanism & performance optimization
   3.6 Security & privacy considerations

4. IMPLEMENTATION
   4.1 Technology stack (Hyperledger Fabric 2.5, Golang, Docker)
   4.2 Chaincode implementation
   4.3 REST API development
   4.4 Dashboard & monitoring interface
   4.5 Integration dengan existing systems

5. VALIDATION & TESTING
   5.1 Functional testing
   5.2 Performance testing (throughput, latency)
   5.3 Security testing (penetration, privilege escalation)
   5.4 Real dataset testing (Climate & Energy 2020-2024)
   5.5 Comparison dengan traditional audit process

6. RESULTS
   6.1 System performance metrics
   6.2 Real-time monitoring capability
   6.3 Cost reduction analysis (vs. traditional)
   6.4 User acceptance testing feedback

7. DISCUSSION
   7.1 Architecture effectiveness
   7.2 Scalability considerations
   7.3 Regulatory compliance (GDPR, environmental regulations)
   7.4 Lessons learned & challenges faced

8. CONCLUSION & FUTURE WORK
   8.1 Summary of contributions
   8.2 Practical applications & adoption pathways
   8.3 Open challenges & future research

9. REFERENCES (50-60 citations)
```

### 2.7 PUBLICATION STRATEGY

- **Timeline:** Submit Bulan 8–9, Expected acceptance Bulan 12–13
- **Journal Selection:** IEEE Transactions on Software Engineering (Q1, prestigious)
- **Review Cycle:** ~5-6 bulan (lebih ketat dari IEEE Access)
- **Strategy:** Emphasize technical novelty & implementation depth

---

## PAPER 3: INTEGRATED ML & BLOCKCHAIN FOR GREENWASHING DETECTION

### 3.1 METADATA

| Aspek | Detail |
|-------|--------|
| **Judul Lengkap** | "Integrated Machine Learning & Blockchain System for Detecting Greenwashing in Sustainability Reporting: End-to-End Architecture, Implementation & Validation on Global Energy Data" |
| **Target Journal** | Journal of Cleaner Production (Q1, IF: 7.8) atau Environmental Science & Technology (Q1, IF: 8.2) |
| **Submission Target** | Bulan 12–13 S3 |
| **Expected Publication** | Bulan 16–17 S3 (4-5 bulan review, bisa overlap dengan defense prep) |
| **Paper Type** | Comprehensive System Paper (15–18 pages) |
| **Author Order** | Malvin Ardi (1st), Promotor (2nd), Co-Promotor (3rd), [Optional: domain expert] |

### 3.2 KONTRIBUSI UTAMA

✅ **Scientific Contribution:**
- Pertama kali integrate K-Means Clustering → Hyperledger Smart Contract → ML Anomaly Detection
- Novel ensemble ML model untuk detect greenwashing (Isolation Forest + LSTM)
- Comprehensive system validation pada real-world dataset
- Quantitative evidence dari greenwashing detection capability

✅ **Impact Contribution:**
- Memperkuat global sustainability reporting credibility
- Support untuk SDG #13 (Climate Action), #12 (Responsible Consumption)
- Potential adoption oleh korporasi global & financial institutions
- Startup/spin-off opportunity

### 3.3 RESEARCH QUESTIONS

1. **RQ1:** Bagaimana mengidentifikasi greenwashing dalam data emisi menggunakan ensemble ML?
2. **RQ2:** Apakah kombinasi Isolation Forest + LSTM lebih akurat dibanding single models?
3. **RQ3:** Bagaimana blockchain dapat memperkuat verifikasi anomaly detection results?
4. **RQ4:** Apakah sistem end-to-end dapat operasional dalam production environment?

### 3.4 ML COMPONENT DETAIL

**Algorithm: Ensemble Approach**

```
┌─────────────────────────────────────────────────────────┐
│          ENSEMBLE ANOMALY DETECTION MODEL               │
│                                                          │
│  INPUT: Time-series emission data per country           │
│                                                          │
│  ┌──────────────────────┐                               │
│  │  Isolation Forest    │ ──→ Anomaly Score 1          │
│  │  (Unsupervised)      │                               │
│  └──────────────────────┘                               │
│                     │                                    │
│                     ↓                                    │
│  ┌──────────────────────────────────────────┐           │
│  │  ENSEMBLE VOTING                         │           │
│  │  Final Anomaly Score = avg(Score1, 2, 3)│           │
│  │  IF score > 0.75 → ANOMALY DETECTED     │           │
│  └──────────────────────────────────────────┘           │
│                     ↑                                    │
│  ┌──────────────────────┐                               │
│  │  LSTM Autoencoder   │ ──→ Anomaly Score 2          │
│  │  (Temporal pattern)  │                               │
│  └──────────────────────┘                               │
│                                                          │
│  ┌──────────────────────┐                               │
│  │  Statistical Test   │ ──→ Anomaly Score 3          │
│  │  (Z-score, IQR)      │                               │
│  └──────────────────────┘                               │
│                                                          │
│  OUTPUT: Anomaly Flag + Confidence Score                │
│          + Feature attribution (why anomaly?)           │
└─────────────────────────────────────────────────────────┘
```

**Isolation Forest:**
- Detects extreme outliers (sudden emisi spike)
- Unsupervised: no labeling needed
- Fast & efficient

**LSTM Autoencoder:**
- Learns normal temporal pattern
- Detects deviation dari expected trajectory
- Good untuk detecting gradual anomalies

**Statistical Tests:**
- Z-score: how many std dev away dari mean
- IQR: interquartile range method

### 3.5 GREENWASHING DETECTION SCENARIOS

```
SCENARIO 1: Sudden Spike Anomaly
├─ Emisi China naik 200% dalam 1 hari
├─ ML: Isolation Forest detects outlier
├─ Blockchain: Alert triggered, data locked untuk investigation
└─ Root cause: Coal plant accident atau data entry error?

SCENARIO 2: Gradual Drift Anomaly
├─ Emisi Brazil menurun consistently 10% per bulan → seems good?
├─ But: Renewable share TIDAK meningkat → suspicious
├─ ML: LSTM detects pattern inconsistency
├─ Blockchain: Red alert - possible greenwashing
└─ Investigation: Apakah really reduced atau just relocated?

SCENARIO 3: Seasonal Anomaly
├─ USA emisi tinggi musim dingin (heating demand)
├─ BUKAN anomaly, tapi normal seasonal pattern
├─ ML: Model learns seasonal cycle → tidak trigger false alert
├─ Blockchain: Status YELLOW only if exceed seasonal baseline
└─ Smart: Context-aware anomaly detection

SCENARIO 4: Coordinated Manipulation
├─ Multiple countries report same emisi reduction pattern → too perfect
├─ Not possible due to different industrial mix
├─ ML: Detect correlation anomaly
├─ Blockchain: Cross-country consistency check
└─ Investigation: Possible data sharing/collusion?
```

### 3.6 OUTLINE PAPER 3

```
1. INTRODUCTION
   1.1 Background: Greenwashing epidemic in sustainability reporting
   1.2 Current detection limitations (manual, reactive)
   1.3 Opportunity: ML + Blockchain untuk proactive detection
   1.4 Research objectives & paper contribution

2. LITERATURE REVIEW
   2.1 Greenwashing definition & prevalence
   2.2 Anomaly detection methods (IF, LSTM, Statistical)
   2.3 Ensemble learning approaches
   2.4 Blockchain untuk verification & immutability
   2.5 Integration approaches (rare in literature)

3. METHODOLOGY
   3.1 Overall framework & integration logic
   3.2 Data preparation & feature engineering
   3.3 Isolation Forest implementation
   3.4 LSTM Autoencoder training
   3.5 Statistical anomaly detection
   3.6 Ensemble voting & confidence scoring
   3.7 Blockchain verification layer
   3.8 Alert & notification system

4. VALIDATION STRATEGY
   4.1 Dataset: Climate & Energy 2020-2024
   4.2 Synthetic anomaly injection (controlled testing)
   4.3 Real anomaly benchmarking (known greenwashing cases)
   4.4 Cross-validation (temporal, geographic)
   4.5 Evaluation metrics (precision, recall, F1-score, ROC-AUC)

5. EXPERIMENTAL RESULTS
   5.1 Individual model performance
   5.2 Ensemble vs. single model comparison
   5.3 True positive rate (TPR) & false positive rate (FPR)
   5.4 Detection latency & system throughput
   5.5 Real-world anomalies detected (case studies)
   5.6 Blockchain verification overhead analysis

6. CASE STUDIES
   6.1 Case 1: Volkswagen diesel-gate (historical simulation)
   6.2 Case 2: COVID-19 emission drop (legitimate vs. manipulation)
   6.3 Case 3: Renewable energy misreporting (country X case)
   6.4 Lessons learned dari setiap case

7. DISCUSSION
   7.1 Model effectiveness & limitations
   7.2 Blockchain integration benefits & costs
   7.3 Practical deployment considerations
   7.4 Regulatory framework alignment
   7.5 Stakeholder adoption barriers

8. CONCLUSION & FUTURE WORK
   8.1 Summary of integrated system
   8.2 Policy implications & recommendations
   8.3 Commercialization potential (startup angle)
   8.4 Open research challenges
   8.5 Long-term vision untuk global sustainability audit

9. REFERENCES (60-70 citations)
```

### 3.7 PUBLICATION STRATEGY

- **Timeline:** Submit Bulan 12–13, Expected acceptance Bulan 16–17
- **Journal Selection:** Journal of Cleaner Production (prestigious, high impact)
- **Review Cycle:** ~4-5 bulan (stringent review)
- **Strength:** Full integrated system + multiple validation methods → strong paper

---

## TIMELINE & MILESTONES

```
┌─────────────────────────────────────────────────────────────────┐
│                    PUBLICATION TIMELINE                         │
├──────┬─────────────────────┬──────────────────────────────────┤
│Month │ Activity            │ Deliverable / Milestone          │
├──────┼─────────────────────┼──────────────────────────────────┤
│ 1-2  │ Proposal finalization│ Executive summary, Bab 1-3      │
│ 3-6  │ PAPER 1 writing     │ Manuscript finalization (P1)    │
│      │ + PoC clustering    │ Submit to IEEE Access (M5)      │
│ 5-6  │                     │ SUBMIT Paper 1 ✉️               │
│      │                     │                                 │
│ 6-10 │ PAPER 2 writing     │ Manuscript finalization (P2)    │
│      │ + Blockchain impl.  │ Submit to IEEE TSE (M8)         │
│ 8-9  │                     │ SUBMIT Paper 2 ✉️               │
│      │                     │                                 │
│ 10-14│ PAPER 3 writing     │ Manuscript finalization (P3)    │
│      │ + ML integration    │ Submit to J. Cleaner Prod (M12) │
│ 12-13│                     │ SUBMIT Paper 3 ✉️               │
│      │                     │                                 │
│ 14-16│ Revision cycles     │ Major/minor revisions           │
│      │ + Disertasi writing │ Finalize disertasi              │
│ 16-17│ EXPECTED ACCEPT     │ Paper 1 accepted ✅ (M9-10)    │
│      │ NOTIFICATIONS       │ Paper 2 accepted ✅ (M12-13)   │
│      │                     │ Paper 3 accepted ✅ (M16-17)   │
│      │ DEFENSE             │ Sidang disertasi (M16)          │
└──────┴─────────────────────┴──────────────────────────────────┘
```

---

## STRATEGI PUBLIKASI KESELURUHAN

### Fase 1: PAPER 1 (Positioning)
- **Fokus:** Establish empirical foundation (clustering results)
- **Target:** IEEE Access (easier acceptance, Q2 impact factor)
- **Audience:** Academic + industry practitioner
- **Goal:** Publikasi di bulan 9-10 → establish credibility

### Fase 2: PAPER 2 (Implementation)
- **Fokus:** Showcase technical innovation (blockchain architecture)
- **Target:** IEEE TSE (prestigious, Q1, harder acceptance)
- **Audience:** Software engineer + blockchain community
- **Goal:** Publikasi di bulan 12-13 → demonstrate engineering excellence

### Fase 3: PAPER 3 (Integration & Impact)
- **Fokus:** Comprehensive system + real-world validation + policy implication
- **Target:** Journal of Cleaner Production (high impact, Q1, most cited)
- **Audience:** Environmental scientist + policy maker + investor
- **Goal:** Publikasi di bulan 16-17 → maximum impact & visibility

### Cross-Paper Coherence

```
PAPER 1 → PAPER 2 → PAPER 3
   ↓           ↓           ↓
Clustering → Blockchain → Full System
   ↓           ↓           ↓
Foundation  Implementation Integration
   ↓           ↓           ↓
Reads: "Identifikasi 3 threshold emisi"
              ↓
       "Gunakan thresholds ini dalam smart contract"
              ↓
       "Detect anomali dengan ML + verify with blockchain"
```

**Key:** Setiap paper standalone tetapi together membentuk complete story → very compelling narratif!

---

## SUBMISSION CHECKLIST

### Sebelum Submit Paper 1:
- [ ] Manuscript ditulis 8-12 halaman
- [ ] 40-50 citations (latest papers 2020-2026)
- [ ] Figures & tables disiapkan (high resolution, 300 DPI)
- [ ] Abstract & keywords finalized
- [ ] Proofread oleh promotor + native speaker
- [ ] Author guidelines IEEE Access diikuti
- [ ] Conflict of interest statement prepared
- [ ] Data availability statement (dataset sharing policy)

### Sebelum Submit Paper 2:
- [ ] Manuscript ditulis 12-15 halaman
- [ ] System architecture diagram clear & detailed
- [ ] Pseudocode/implementation code appendix
- [ ] Performance metrics & comparison table
- [ ] 50-60 citations (strong blockchain + software engineering refs)
- [ ] All author guidelines IEEE TSE diikuti
- [ ] Supplementary materials (code, config files)

### Sebelum Submit Paper 3:
- [ ] Manuscript ditulis 15-18 halaman (most comprehensive)
- [ ] Case studies dengan real data
- [ ] ML model comparison table
- [ ] Statistical significance tests
- [ ] 60-70 citations (comprehensive literature)
- [ ] Policy recommendations section
- [ ] Commercialization/adoption pathway discussion
- [ ] All supporting documents (evaluation metrics, datasets)

---

## EXPECTED OUTCOMES

### Publication Impact

| Paper | Expected IF | Expected Citations (Year 1) | Career Impact |
|-------|---|---|---|
| Paper 1 | 3.9 | 10-20 citations | Establish field position |
| Paper 2 | 6.2 | 15-30 citations | Technical credibility |
| Paper 3 | 7.8 | 30-50 citations | Research leader status |
| **TOTAL** | **~6** | **55-100 citations** | **Strong PhD output** |

### Tangible Outcomes

✅ **Academic:**
- 3 Scopus Q1/Q2 publications
- ~75-100 citations dalam 1 tahun pertama
- Positioning sebagai leader dalam blockchain + sustainability

✅ **Professional:**
- Invitations untuk conference talks (IEEE, ACM, environmental conferences)
- Collaboration offers dari research groups global
- Reviewer roles untuk top-tier journals

✅ **Industrial:**
- Interest dari blockchain startup / sustainability consulting firm
- Consulting opportunities
- Potential untuk tech transfer / IP licensing

✅ **Policy:**
- Engagement dengan environmental agencies (UNEP, IEA)
- Policy brief opportunities
- Input untuk international sustainability standards

---

## KONTRIBUSI INOVASI PER PAPER

### Paper 1: DATA-DRIVEN INSIGHT
**Innovation:** Mengidentifikasi scientifically-valid threshold emisi per negara cluster
**Novelty:** Belum pernah ada sebelumnya di literatur sustainability
**Impact:** Memberikan empirical foundation untuk smart contract design

### Paper 2: TECHNICAL ARCHITECTURE
**Innovation:** Complete Hyperledger Fabric architecture khusus untuk compliance audit
**Novelty:** First production-ready blockchain system untuk environmental audit
**Impact:** Can be immediately adopted oleh korporasi & government

### Paper 3: INTEGRATED AI + BLOCKCHAIN
**Innovation:** Ensemble ML model untuk detect greenwashing with blockchain verification
**Novelty:** First comprehensive integrated system (K-Means + Blockchain + ML)
**Impact:** Game-changer untuk global sustainability reporting credibility

---

## NOTES FOR PROMOTOR

> "Prof, saya merancang 3 publikasi sebagai integrated narrative:
>
> **Paper 1** berikan fondasi data (clustering + threshold).
> 
> **Paper 2** implementasi blockchain yang memanfaatkan threshold dari Paper 1.
> 
> **Paper 3** integrasi ML untuk deteksi anomali dan verify dengan blockchain dari Paper 2.
>
> Setiap paper standalone tetapi bersama membentuk complete system yang bisa langsung diterapkan di industri. Target publikasi Q1/Q2 dengan timeline realistis (submit M5, M8, M12) dan expected acceptance sebelum defense (M16-17).
>
> Kontribusi inovasi: Pertama kali ada integrated framework seperti ini di literatur global, dengan validasi real-world data, dan commercialization potential."

---

**Status:** ✅ READY FOR EXECUTION  
**Next Action:** Finalize Paper 1 manuscript dalam 4 minggu ke depan  
**Timeline:** Submit Paper 1 → Bulan 5–6 S3

