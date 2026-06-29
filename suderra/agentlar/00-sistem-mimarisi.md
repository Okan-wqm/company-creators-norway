# Suderra AS — Agent Sistemi Mimarisi

## Genel Bakış

```
                        ┌─────────────────────────┐
                        │     FOUNDER (SEN)        │
                        │   Yönlendirme & Onay     │
                        └────────────┬────────────┘
                                     │
                        ┌────────────▼────────────┐
                        │       CEO AGENT          │
                        │  Orchestrator & Sentez   │
                        └──┬─────────┬──────────┬─┘
                           │         │          │
          ┌────────────────┘    ┌────┘    ┌─────┘
          ▼                     ▼         ▼
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│   HUKUK BLOĞU   │  │   MALİ BLOK     │  │   VERGİ BLOĞU   │
│                 │  │                 │  │                 │
│ 03-aksjeloven   │  │ 02-cfo          │  │ 07-reverse-tax  │
│ 04-founder-kor  │  │ 05-yat-dostu    │  │                 │
│ 06-sweat-equity │  │                 │  │                 │
│                 │  │                 │  │                 │
│  AVUKAT GRUBU   │  │                 │  │                 │
│ 08-norveç-avuk  │  │                 │  │                 │
│ 09-dava-uzman   │  │                 │  │                 │
│ 10-founder-avuk │  │                 │  │                 │
└─────────────────┘  └─────────────────┘  └─────────────────┘
          │                     │                  │
          └─────────────────────┼──────────────────┘
                                ▼
               ┌────────────────────────────────┐
               │      ARAŞTIRMA KATMANI          │
               │   13-emsal-arastirma-agent      │
               │   (davalar, hatalar, vakalar)   │
               └────────────────────────────────┘
                                │
                                ▼
               ┌────────────────────────────────┐
               │       KALİTE KATMANI           │
               │   12-seytan-avukati-agent       │
               │   (her şeyi çürütmeye çalışır) │
               └────────────────────────────────┘
                                │
                                ▼
               ┌────────────────────────────────┐
               │      ÇIKTI KATMANI             │
               │   11-belge-uzmani-agent         │
               │   (nihai imzaya hazır belgeler) │
               └────────────────────────────────┘
```

---

## Agent Listesi (13 Agent)

| # | Agent | Blok | Görev |
|---|-------|------|-------|
| 01 | CEO Agent | Koordinasyon | Orkestrasyon, sentez, nihai karar |
| 02 | CFO Agent | Mali | Cap table, dilution, finansal yapı |
| 03 | Aksjeloven Agent | Hukuk | Norveç şirket kanunu uyumu |
| 04 | Founder Koruma Agent | Hukuk | Founder haklarını maksimize eder |
| 05 | Yatırımcı Dostu Agent | Hukuk/Mali | Ürkütücü maddeleri tespit eder |
| 06 | Sweat Equity Agent | Hukuk | B hissesi vesting, co-founder hakları |
| 07 | Reverse Tax Optimizer | Vergi | Vergi fırsatı avcısı (uyum değil) |
| 08 | Norveç Avukat Agent | Avukat | Aksjeloven davası deneyimi, uyum |
| 09 | Dava Uzmanı Agent | Avukat | Mahkeme testi, ispat yükü analizi |
| 10 | Founder Avukatı Agent | Avukat | Agresif founder savunuculuğu |
| 11 | Belge Uzmanı Agent | Çıktı | Nihai format, imzaya hazır |
| 12 | Şeytan'ın Avukatı | Kalite | Kötü senaryo testi, boşluk avcısı |
| 13 | Emsal Araştırma Agent | Araştırma | Davalar, hatalar, vakalar veritabanı |

---

## Çalışma Sırası (Fazlar)

```
FAZ 0 — Araştırma (Agent 13)
  ↓ Paralel: Norveç davaları + Uluslararası vakalar + Yazım hataları kataloğu
  
FAZ 1 — Uzman Araştırması (Agent 03, 07, 05)
  ↓ Paralel: Aksjeloven + Vergi fırsatları + Yatırımcı beklentileri

FAZ 2 — Taslak Belgeler (Agent 04, 06, 07, 08)
  ↓ Paralel: 7 belge aynı anda hazırlanır

FAZ 3 — Tartışma & Eleştiri (Agent 08, 09, 10, 05, 07)
  ↓ Paralel: 5 farklı perspektiften eleştiri

FAZ 4 — CEO Sentezi (Agent 01)
  ↓ Tüm eleştirileri değerlendirir, nihai direktif verir

FAZ 5 — Şeytan'ın Avukatı (Agent 12)
  ↓ 7 kötü senaryo testi

FAZ 6 — Final Belgeler (Agent 11)
  ↓ Tüm revizyonları dahil eder, imzaya hazır 8 belge üretir
```

---

## Üretilecek Belgeler

```
01-stiftelsesdokument.md     → Kuruluş Senedi (Norveçce)
02-vedtekter.md              → Esas Sözleşme A/B/C hisse (Norveçce)
03-sweat-equity-avtale.md    → Co-founder Vesting Anlaşması (Norveçce)
04-aksjonaer-avtale.md       → Shareholder Agreement (Norveçce)
05-holding-transfer-plan.md  → Holding Yapı Planı (Norveçce + Türkçe)
06-term-sheet-template.md    → Yatırımcı Term Sheet (İngilizce)
07-skattefunn-soknad.md      → AR-GE Vergi Kredisi Başvurusu (Norveçce)
00-founder-ozet.md           → Tüm belgeler Türkçe özet (Founder için)
```

---

## Şirket Parametreleri

```yaml
sirket_adi: Suderra AS
holding: Suderra Holding AS
sektor: Aquaculture çiftlik yönetim yazılımı
sermaye: 30,000 NOK
hisse_yapisi:
  A: "%90 — Founder — 10:1 oy"
  B: "%5+%5 — Co-founder — 1:1 oy — 4 yıl vesting"
  C: "Yatırımcı — 1:1 oy — 1x non-participating liq pref"
holding_zamanlama: "30k NOK değerindeyken — değer artmadan"
hukuk: "Aksjeloven 2026"
```
