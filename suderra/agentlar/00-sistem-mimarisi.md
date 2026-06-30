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

## Agent Listesi (18 Agent)

| # | Agent | Blok | Görev |
|---|-------|------|-------|
| 01 | CEO Agent | Koordinasyon | Orkestrasyon, sentez, nihai karar (3-level hierarchy) |
| 02 | CFO Agent | Mali | Cap table, dilution, finansal yapı |
| 03 | Aksjeloven Agent | Hukuk | Norveç şirket kanunu uyumu |
| 04 | Founder Koruma Agent | Hukuk | KANTİTATİF: oy yüzdeleri, cap table math, dilution modelleri |
| 05 | Yatırımcı Dostu Agent | Hukuk/Mali | Ürkütücü maddeleri tespit eder |
| 06 | Sweat Equity Agent | Hukuk | B hissesi vesting, co-founder hakları |
| 07 | Reverse Tax Optimizer | Vergi | Vergi fırsatı (Fritaksmetoden, Skattefunn, opsjonsordning §5-14) |
| 08 | Norveç Avukat Agent | Avukat | Preliminary legal review (NOT certification) |
| 09 | Dava Uzmanı Agent | Avukat | Mahkeme testi — 8 senaryo (A-H) |
| 10 | Founder Avukatı Agent | Avukat | ADVERSARİAL: karşı taraf avukatının argümanları |
| 11 | Belge Uzmanı Agent | Çıktı | Nihai format, imzaya hazır 10 belge |
| 12 | Şeytan'ın Avukatı | Kalite | Kötü senaryo testi, somut vergi cezaları |
| 13 | Emsal Araştırma Agent | Araştırma | Davalar (anti-hallüsinasyon korumalı), 20 yazım hatası |
| 14 | IP & Yazılım Hakları | Hukuk/YENİ | IP atama, açık kaynak politikası, veri sahipliği |
| 15 | GDPR & Veri Uyum | Hukuk/YENİ | Personopplysningsloven, Databehandleravtale şablonu |
| 16 | Belge Tutarlılık | Kalite/YENİ | BLOKAJ GEÇIDI: 10 belge çapraz kontrol, çelişki tespiti |
| 17 | Styrereglement | Çıktı/YENİ | Norveç yönetim kurulu tüzüğü (Aksjeloven §6-23) |
| 18 | Co-founder Perspektif | Kalite/YENİ | "Bu sözleşmeyi imzalar mıydım?" testi |

---

## Çalışma Sırası (Güncellenmiş 8 Faz)

```
FAZ 0 — Araştırma (Agent 13)
  ↓ Paralel: Norveç davaları (anti-hallüsinasyon korumalı) + 20 yazım hatası kataloğu

FAZ 1 — Uzman Araştırması (Agent 03, 07, 05) [paralel]
  ↓ Aksjeloven + Vergi fırsatları (Fritaksmetoden, Skattefunn, opsjonsordning) + Yatırımcı beklentileri

FAZ 2 — Taslak Belgeler (10 belge) [paralel]
  ↓ Stiftelsesdokument + Vedtekter + Sweat Equity + Aksjonæravtale
  ↓ Holding Plan + Term Sheet + Skattefunn + IP Policy + GDPR/Databehandleravtale + Styrereglement

FAZ 2b — Tutarlılık Kontrolü (Agent 16) ← YENİ BLOKAJ GEÇIDI
  ↓ 10 belge çapraz kontrol — KRITIK çelişkiler çözülmeden FAZ 3'e geçilmez

FAZ 3 — Tartışma & Eleştiri (Agent 08, 09, 10, 05, 07, 14, 15, 18) [paralel]
  ↓ Preliminary legal review (08) — 8 mahkeme senaryosu (09) — Adversarial argümanlar (10)
  ↓ Yatırımcı dostu kontrol (05) — Vergi eksik (07) — IP (14) — GDPR (15) — Co-founder testi (18)

FAZ 4 — CEO Sentezi (Agent 01)
  ↓ 3-seviye karar hiyerarşisi: Aksjeloven uyumu > Founder koruması > Yatırımcı dostu

FAZ 5 — Şeytan'ın Avukatı (Agent 12)
  ↓ 7 kötü senaryo + somut vergi cezaları (Skatteforvaltningsloven §14-3)

FAZ 6 — Final Belgeler (Agent 11)
  ↓ Tüm revizyonları dahil eder, imzaya hazır 10 belge üretir
```

---

## Üretilecek Belgeler (10 Belge)

```
01-stiftelsesdokument.md     → Kuruluş Senedi + fravalg av revisjon (Norveçce)
02-vedtekter.md              → Esas Sözleşme A/B/C hisse (Norveçce)
03-sweat-equity-avtale.md    → Co-founder Vesting Anlaşması (Norveçce)
04-aksjonaer-avtale.md       → Shareholder Agreement (Norveçce)
05-holding-transfer-plan.md  → Holding Yapı Planı (Norveçce + Türkçe)
06-term-sheet-template.md    → Yatırımcı Term Sheet (İngilizce)
07-skattefunn-soknad.md      → AR-GE Vergi Kredisi Başvurusu (Norveçce)
08-ip-politikasi.md          → IP + Yazılım Hakları Politikası (Agent 14'ten) ← YENİ
09-styrereglement.md         → Yönetim Kurulu Tüzüğü (Agent 17'den) ← YENİ
00-founder-ozet.md           → Tüm belgeler Türkçe özet + Brønnøysund kayıt adımları
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
