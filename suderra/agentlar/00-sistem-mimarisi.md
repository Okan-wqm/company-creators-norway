# Suderra AS — Agent Sistemi Mimarisi

## Genel Bakış

Bu diyagram FAZ akışının üst düzey özetidir. Tam ve otoriter sıralama için aşağıdaki
"Çalışma Sırası" bölümüne bakın — herhangi bir çelişki durumunda o bölüm geçerlidir.

```
┌─────────────────────────┐
│     FOUNDER (SEN)        │
│   Yönlendirme & Onay     │
└────────────┬────────────┘
             │
             ▼
┌──────────────────────────────────────────┐
│  FAZ 0 — ARAŞTIRMA (Agent 13)             │
│  Davalar + yazım hataları kataloğu         │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  FAZ 1 — UZMAN ARAŞTIRMASI [paralel]      │
│  03-aksjeloven · 07-reverse-tax · 05-yat-dostu │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  FAZ 2 — TASLAK BELGELER [paralel]        │
│  9 taslak: stiftelsesdokument, vedtekter,  │
│  sweat-equity (06), aksjonæravtale (04),   │
│  holding-plan, term-sheet, skattefunn,     │
│  ip-politikasi (14), styrereglement (17)   │
│  + opsiyonel: 20-çalışan-sözleşmesi        │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  FAZ 2b — TUTARLILIK GEÇİDİ (Agent 16)    │
│  BLOKAJ: kritik çelişkiler çözülmeden      │
│  FAZ 3'e geçilmez                          │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  FAZ 3 — TÜM ELEŞTİRİLER [paralel]        │
│  08-norveç-avuk · 09-dava-uzman ·          │
│  10-founder-avuk · 12-şeytan-avukatı ·     │
│  14-ip · 15-gdpr · 18-cofounder-perspektif │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  FAZ 4 — CEO SENTEZİ (Agent 01)           │
│  3-seviye karar hiyerarşisi: Aksjeloven >  │
│  Founder koruması > Yatırımcı dostu        │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  FAZ 5 — FİNAL BELGELER (Agent 11)        │
│  10 belge, imzaya hazır format             │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  FAZ 6 — OPERASYONEL UYGULAMA [sıralı/sürekli] │
│  19-brønnøysund-kayıt · 21-yıllık-uyum     │
└──────────────────────────────────────────┘
```

---

## Agent Listesi (21 Agent)

| # | Agent | Blok | Görev |
|---|-------|------|-------|
| 01 | CEO Agent | Koordinasyon | Orkestrasyon, sentez, nihai karar (3-level hierarchy) |
| 02 | CFO Agent | Mali | Cap table, dilution, finansal yapı + arbeidsgiveravgift + MVA |
| 03 | Aksjeloven Agent | Hukuk | Norveç şirket kanunu uyumu (Lovdata.no protokolü) |
| 04 | Founder Koruma Agent | Hukuk | KANTİTATİF: oy yüzdeleri, cap table math, dilution modelleri |
| 05 | Yatırımcı Dostu Agent | Hukuk/Mali | Ürkütücü maddeleri tespit eder |
| 06 | Sweat Equity Agent | Hukuk | B hissesi vesting, co-founder hakları, oransal bad leaver |
| 07 | Reverse Tax Optimizer | Vergi | Vergi fırsatı (Fritaksmetoden, Skattefunn, opsjonsordning §5-14) |
| 08 | Norveç Avukat Agent | Avukat | Preliminary legal review (NOT certification) |
| 09 | Dava Uzmanı Agent | Avukat | Mahkeme testi — 10 senaryo (A-J) |
| 10 | Founder Avukatı Agent | Avukat | ADVERSARİAL: karşı taraf avukatının argümanları |
| 11 | Belge Uzmanı Agent | Çıktı | Nihai format, imzaya hazır 10 belge |
| 12 | Şeytan'ın Avukatı | Kalite | FAZ 3'te çalışır — CEO'dan ÖNCE kötü senaryoları test eder |
| 13 | Emsal Araştırma Agent | Araştırma | Davalar (anti-hallüsinasyon korumalı), 20 yazım hatası |
| 14 | IP & Yazılım Hakları | Hukuk | IP atama, açık kaynak politikası, veri sahipliği |
| 15 | GDPR & Veri Uyum | Hukuk | Personopplysningsloven, Databehandleravtale şablonu |
| 16 | Belge Tutarlılık | Kalite | BLOKAJ GEÇIDI: 10 belge çapraz kontrol, çelişki tespiti |
| 17 | Styrereglement | Çıktı | Norveç yönetim kurulu tüzüğü (Aksjeloven §6-23) |
| 18 | Co-founder Perspektif | Kalite | "Bu sözleşmeyi imzalar mıydım?" testi |
| 19 | Brønnøysund Kayıt Rehberi | Süreç/YENİ | Altinn adım adım tescil, pre-registration uyarısı |
| 20 | Çalışan Sözleşmesi | Hukuk/YENİ | Norveç arbeidskontrakt (co-founder çalışan ise) |
| 21 | Yıllık Uyum Takvimi | Süreç/YENİ | Tüm yıllık son tarihler: vergi, Brønnøysund, GDPR |

---

## Çalışma Sırası (Güncellenmiş 8 Faz)

```
FAZ 0 — Araştırma (Agent 13)
  ↓ Paralel: Norveç davaları (anti-hallüsinasyon korumalı) + 20 yazım hatası kataloğu

FAZ 1 — Uzman Araştırması (Agent 03, 07, 05) [paralel]
  ↓ Aksjeloven + Vergi fırsatları (Fritaksmetoden, Skattefunn, opsjonsordning) + Yatırımcı beklentileri

FAZ 2 — Taslak Belgeler (9 taslak + 1 opsiyonel) [paralel]
  ↓ Stiftelsesdokument + Vedtekter + Sweat Equity + Aksjonæravtale
  ↓ Holding Plan + Term Sheet + Skattefunn + IP Policy + Styrereglement
  ↓ Opsiyonel: Çalışan Sözleşmesi (Agent 20) — yalnızca co-founder çalışan sayılırsa
  NOT: GDPR/Databehandleravtale (Agent 15) burada DRAFT edilmez — Agent 15 FAZ 3'te
  inceleme yapar; databehandleravtale şablonu 08-ip-politikasi.md belgesi içinde özetlenir
  (bkz. Agent 11 belge #8 içeriği), ayrı bir belge sayılmaz.

FAZ 2b — Tutarlılık Kontrolü (Agent 16) ← YENİ BLOKAJ GEÇIDI
  ↓ FAZ 2 taslakları çapraz kontrol — KRITIK çelişkiler çözülmeden FAZ 3'e geçilmez

FAZ 3 — TÜM ELEŞTİRİLER (Agent 08, 09, 10, 12, 14, 15, 18) [paralel] ← Agent 12 buraya taşındı
  ↓ Preliminary legal review (08) — 8+2 mahkeme senaryosu (09) — Adversarial argümanlar (10)
  ↓ Şeytan'ın avukatı / kötü senaryolar (12) — IP (14) — GDPR (15) — Co-founder testi (18)
  ↓ NOT: Agent 12 artık Agent 01'den ÖNCE çalışır; CEO tüm eleştirileri alır

FAZ 4 — CEO Sentezi (Agent 01)
  ↓ 3-seviye karar hiyerarşisi: Aksjeloven uyumu > Founder koruması > Yatırımcı dostu
  ↓ FAZ 3'teki TÜM eleştiri çıktılarını alır (08+09+10+12+14+15+18)

FAZ 5 — Final Belgeler (Agent 11)
  ↓ CEO direktifini uygular, imzaya hazır 10 belge üretir

FAZ 6 — Operasyonel Uygulama (Agent 19, 21) [sıralı, sonrasında sürekli]
  ↓ Agent 19: Final stiftelsesdokument ile Brønnøysund/Altinn tescil rehberi uygulanır
  ↓ Agent 21: Tescil sonrası yıllık uyum takvimi kurulur — bu noktadan itibaren sürekli/
    tekrarlayan bir agent olarak çalışır (FAZ 0-5'in tek seferlik kuruluş döngüsünün dışında)
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
