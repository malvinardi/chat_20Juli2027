# BAB 1: LATAR BELAKANG

## 1.1 KONTEKS GLOBAL: KRISIS IKLIM & TRANSISI ENERGI

### 1.1.1 Realitas Perubahan Iklim

Pada tahun 2024, dunia sedang menghadapi krisis iklim yang belum pernah terjadi sebelumnya. Berdasarkan laporan IPCC (Intergovernmental Panel on Climate Change) 2021:

- **Emisi CO₂ global mencapai 36.3 gigatons** per tahun (tertinggi dalam sejarah manusia)
- **Suhu global sudah naik 1.1°C** dibanding era pre-industrial
- **Jika tren berlanjut, akan mencapai 1.5°C pada 2030** → bencana ekstreem (banjir, kekeringan, krisis pangan)

Penyebab utama: 
1. **Pembakaran bahan bakar fosil** (coal, oil, gas) → 73% emisi CO₂
2. **Deforestasi** → 18% emisi
3. **Industri & manufaktur** → 9% emisi

### 1.1.2 Respons Global & Komitmen Paris

Sejak Perjanjian Paris 2015, lebih dari 190 negara berkomitmen:
- ✅ Membatasi kenaikan suhu ke **1.5°C–2°C** di atas pre-industrial level
- ✅ Mencapai **net-zero emissions** pada 2050
- ✅ Melaporkan emisi secara **transparan & terukur**

**Namun, realitasnya jauh lebih kompleks:**

Negara-negara besar seperti China, USA, India, dan Rusia masih mengandalkan energi fosil. Transisi ke energi terbarukan (renewable) tidak berjalan secepat yang diharapkan karena:
1. Infrastruktur yang sudah ada (lock-in effect)
2. Biaya investasi yang sangat besar
3. Kurangnya mekanisme verifikasi yang andal

---

## 1.2 MASALAH UTAMA: AUDIT KEBERLANJUTAN YANG TIDAK EFISIEN & TIDAK TRANSPARAN

### 1.2.1 Kondisi Saat Ini: Audit Manual & Lambat

Saat ini, audit lingkungan dan kepatuhan keberlanjutan (sustainability compliance) dilakukan secara **tradisional** melalui proses:

```
1. Korporasi mengumpulkan data emisi (sering self-reported) → 1–3 bulan
2. Auditor eksternal (Big 4 consulting: Deloitte, PWC, EY, KPMG) 
   melakukan site visit & verifikasi manual → 3–6 bulan
3. Laporan audit diterbitkan & disetujui → 2–3 bulan
TOTAL: 6–12 BULAN per audit + Biaya: $2–5 juta USD
```

**Masalah dengan pendekatan ini:**

| Masalah | Dampak | Contoh |
|--------|--------|--------|
| **Manual & Lambat** | Informasi emisi terlambat 12 bulan | Jika emisi lolos audit, baru ketahuan tahun depan |
| **Tidak Transparan** | Stakeholder (regulator, investor, NGO) tidak bisa akses data real-time | Public tidak tahu emisi perusahaan sebenarnya |
| **Mudah Dimanipulasi** | Korporasi bisa merekayasa data (greenwashing) | Perusahaan lapor emisi 100 ton, sebenarnya 300 ton |
| **Biaya Mahal** | Hanya korporasi besar yang mampu audit rutin | UMKM & startup hijau tidak teraudit |
| **Tidak Terstandar** | Setiap negara/region punya standar berbeda | Data tidak bisa dibanding lintas negara |

### 1.2.2 Greenwashing: Rekayasa Data Lingkungan

**Greenwashing** adalah praktik korporasi yang mengklaim komitmen lingkungan tetapi tidak didukung aksi nyata.

**Contoh Kasus:**
- **Volkswagen (2015):** Mengklaim mobil "clean diesel" tapi sebenarnya melebihi emisi standard
- **Shell (2023):** Mundur dari target net-zero sambil terus drilling minyak
- **Fast Fashion Brands:** Klaim "sustainable" padahal supply chain masih highly polluting

**Kenapa Greenwashing Terjadi?**
1. Regulasi lemah (khususnya di negara berkembang)
2. Tidak ada verifikasi independent real-time
3. Insentif finansial besar (ESG rating → investor confidence → stock price ↑)

**Dampak:**
- 🔴 Investor terpesona memberi dana ke perusahaan "fake green"
- 🔴 Regulasi global tidak bisa berbasis data akurat
- 🔴 Transisi energi nyata terhambat

---

## 1.3 SOLUSI TEKNOLOGI: BLOCKCHAIN + SMART CONTRACT

### 1.3.1 Mengapa Blockchain?

Blockchain adalah teknologi **distributed ledger** yang memiliki karakteristik unik:

| Karakteristik | Manfaat untuk Audit |
|---|---|
| **Immutability** | Data emisi yang tercatat tidak bisa diubah retroaktif (anti-greenwashing) |
| **Transparency** | Semua stakeholder (regulator, investor, NGO, publik) bisa akses data real-time |
| **Decentralization** | Tidak bergantung satu auditor pusat → mengurangi single point of failure |
| **Automation (Smart Contract)** | Audit trigger otomatis tanpa perlu manual review |
| **Cost Efficiency** | Menghilangkan middleman (auditor) → biaya turun 70% |

### 1.3.2 Smart Contract untuk Audit Otomatis

**Smart Contract** adalah program yang berjalan otomatis di blockchain berdasarkan kondisi tertentu.

**Contoh Smart Contract untuk Sustainability Audit:**

```solidity
// Pseudocode Smart Contract
IF emisi_CO2_per_kWh > threshold_kluster THEN
    → TRIGGER alert merah ("excessive emissions detected")
    → LOCK finansial reward sampai emisi turun
    → NOTIFY regulator + investor secara otomatis
ELSE IF emisi_menurun_konsisten THEN
    → APPROVE green bond financing
    → INCREASE ESG score
```

**Keuntungan:**
- ✅ Audit terjadi **real-time** (bukan 12 bulan kemudian)
- ✅ **Tidak subjektif** — logic berbasis threshold emisi empiris
- ✅ **Otomatis** — tidak perlu auditor manual
- ✅ **Transparan** — semua stakeholder lihat proses

### 1.3.3 Hyperledger Fabric sebagai Platform

Kami memilih **Hyperledger Fabric** (bukan Bitcoin atau Ethereum) karena:
1. **Enterprise-grade** — trusted oleh IBM, Maersk, TradeLens
2. **Permissioned** — hanya negara/korporasi authorized yang bisa join
3. **Scalable** — bisa handle jutaan transaksi per hari
4. **Privacy** — channel terpisah untuk berbagai koalisi negara/industri

---

## 1.4 GAP PENELITIAN: BELUM ADA SOLUSI TERINTEGRASI

### 1.4.1 Literature Review Singkat

Kami melakukan pencarian di Scopus & Web of Science dengan query:
- "Blockchain sustainability audit"
- "Smart contract environmental compliance"
- "Distributed ledger climate monitoring"

**Temuan:**
| Kategori | Jumlah Paper | Fokus |
|---|---|---|
| Blockchain untuk IoT & supply chain | ~200 papers | Tracking produk, bukan emisi |
| Blockchain untuk sustainability (general) | ~30 papers | Teori, bukan implementasi |
| Blockchain + audit emisi (spesifik) | **< 5 papers** | Belum ada yang terintegrasi |

**Kesimpulan:** Penelitian Blockchain untuk sustainability compliance masih **very nascent** & belum ada solusi end-to-end yang terintegrasi.

### 1.4.2 Gap Spesifik

Gap penelitian kami:

1. **Gap #1: Segmentasi Negara** 
   - ❌ Belum ada penelitian yang mengelompokkan negara berdasarkan profil emisi & energi
   - ❌ Threshold Smart Contract diatur secara ad-hoc, bukan empiris
   - ✅ **Kami akan gunakan K-Means Clustering pada 50 negara** → dapatkan threshold berbasis data

2. **Gap #2: Arsitektur Blockchain Holistik**
   - ❌ Penelitian existing hanya membahas blockchain secara general, tidak spesifik untuk compliance
   - ❌ Belum ada chaincode/smart contract yang detail & teruji
   - ✅ **Kami akan develop Hyperledger Fabric network lengkap** dengan 5+ peer nodes

3. **Gap #3: Deteksi Greenwashing via ML**
   - ❌ Belum ada mekanisme otomatis untuk detect anomali/greenwashing dalam data emisi
   - ❌ Audit hanya check apakah data valid, bukan apakah suspicious
   - ✅ **Kami akan integrate ML (Isolation Forest + LSTM) untuk anomaly detection** → detect greenwashing attempts

4. **Gap #4: Validasi pada Dataset Riil**
   - ❌ Mayoritas paper blockchain sustainability hanya teori/simulasi
   - ✅ **Kami punya dataset riil Climate & Energy 2020–2024** (50+ negara, 5 tahun) untuk validation

---

## 1.5 JUSTIFIKASI: MENGAPA PENELITIAN INI PENTING?

### 1.5.1 Urgensi Akademik

1. **Novel Architecture** — Pertama kali: kombinasi K-Means Clustering + Hyperledger Fabric Smart Contract + ML Anomaly Detection untuk sustainability audit
2. **Methodological Rigor** — Validasi pada dataset riil, bukan simulasi
3. **Scopus-Ready Output** — Dirancang untuk 3 publikasi Q1/Q2 (IEEE Access, IEEE TSE, Journal of Cleaner Production)

### 1.5.2 Relevansi Praktis

1. **SDG Alignment** — Mendukung UN Sustainable Development Goal:
   - SDG #13 (Climate Action)
   - SDG #12 (Responsible Consumption & Production)
   - SDG #17 (Partnerships for Goals)

2. **Adopsi Industri** — Blockchain sustainability audit bisa diadopsi oleh:
   - 🏢 Korporasi multinasional (untuk ESG reporting)
   - 🏛️ Regulator & pemerintah (untuk monitoring emisi nasional)
   - 🏦 Financial institution (untuk sustainable finance)

3. **Dampak Ekonomi** — Potensial:
   - Mengurangi biaya audit global dari $500 juta → $150 juta per tahun
   - Menciptakan startup/spin-off baru di bidang blockchain sustainability

### 1.5.3 Kontribusi Indonesia

Indonesia memiliki peran strategis:
- 🌴 Hutan tropis terbesar di dunia (penyimpan karbon)
- ⚡ Transisi energi baru jalan (20% renewable target 2025)
- 🏭 Industri manufaktur/tekstil besar (emisi tinggi)

**Penelitian ini relevant untuk:** Monitoring emisi industri Indonesia, mendukung kebijakan net-zero 2060, & positioning Indonesia sebagai leader dalam "green blockchain technology".

---

## 1.6 TUJUAN PENELITIAN

### Tujuan Umum:
Mengembangkan & memvalidasi **arsitektur blockchain terintegrasi** untuk audit kepatuhan keberlanjutan otomatis yang menggabungkan clustering, smart contract, & machine learning.

### Tujuan Khusus:
1. **TS1:** Mengidentifikasi & mensegmentasi 50+ negara menjadi kluster emisi berbasis K-Means, menghasilkan threshold baseline untuk Smart Contract
2. **TS2:** Merancang & mengimplementasikan Hyperledger Fabric network dengan chaincode smart contract untuk audit compliance otomatis
3. **TS3:** Mengembangkan ensemble ML model untuk deteksi anomali emisi & greenwashing attempts
4. **TS4:** Mengintegrasikan ketiga komponen menjadi sistem end-to-end & memvalidasi pada dataset Climate & Energy 2020–2024

---

## 1.7 MANFAAT PENELITIAN

| Pihak | Manfaat |
|------|---------|
| **Akademik** | Publikasi 3 paper Scopus Q1/Q2; metodologi novel |
| **Industri** | Platform audit blockchain reusable untuk berbagai sektor |
| **Regulator** | Mekanisme monitoring emisi real-time & transparan |
| **Masyarakat** | Transparansi data emisi → informed decision untuk investasi/produk |
| **Planet** | Accelerasi transisi energi → mitigasi perubahan iklim |

---

## 1.8 ROADMAP PENELITIAN (TIMELINE S3)

```
BULAN 1-2 (Semester 1):
├─ Eksplorasi dataset & data cleaning
├─ Literature review mendalam (Blockchain + Sustainability + ML)
├─ Finalisasi proposal & ethical clearance
└─ Output: Executive Summary + Bab 1-3 + PoC clustering

BULAN 3-6 (Semester 2):
├─ Tahap 1: K-Means Clustering (50 negara → 3 kluster)
├─ Analisis threshold emisi per kluster
└─ Output: Paper #1 (Q2 Journal: IEEE Access / Sustainability)

BULAN 6-10 (Semester 3):
├─ Tahap 2: Design & implement Hyperledger Fabric network
├─ Develop smart contract chaincode (Golang)
├─ Testing & validation
└─ Output: Paper #2 (Q1 Journal: IEEE TSE)

BULAN 10-14 (Semester 4):
├─ Tahap 3: ML anomaly detection (Isolation Forest + LSTM)
├─ Full system integration & testing
├─ Final validation on real dataset
└─ Output: Paper #3 (Q1 Journal: Journal of Cleaner Production)

BULAN 14-16 (Semester 5-6):
├─ Finalisasi disertasi
├─ Revisi paper dari reviewer
└─ Defense + Graduation
```

---

## 1.9 ORIGINALITAS & INOVASI

**Originalitas:**
- Pertama di Indonesia: Blockchain architecture untuk sustainability audit
- Belum ada di literatur global: Integrated framework (Clustering + Blockchain + ML)

**Inovasi:**
- Smart contract yang trigger otomatis berdasarkan threshold emisi
- ML model untuk detect greenwashing in real-time
- Open-source implementation (Hyperledger Fabric) yang bisa diadopsi industri

---

**NEXT SECTION:** BAB 2 akan membahas Tinjauan Pustaka secara mendalam untuk setiap komponen (Blockchain, Smart Contract, K-Means Clustering, Anomaly Detection, Sustainability Audit Standards).

