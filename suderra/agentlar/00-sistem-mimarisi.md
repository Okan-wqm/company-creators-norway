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
│  FAZ 1 — UZMAN ARAŞTIRMASI [iki alt dalga]│
│  1a: 03-aksjeloven · 07-reverse-tax ·      │
│      05-yat-dostu [paralel]                │
│  1b: 02-cfo (05 ve 07 çıktılarını alır)    │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  FAZ 2 — TASLAK BELGELER [paralel]        │
│  9 taslak: stiftelsesdokument (03),        │
│  vedtekter (03), sweat-equity (06),        │
│  aksjonæravtale (04), holding-plan (07),   │
│  term-sheet (05), skattefunn (07+02),      │
│  ip-politikasi (14), styrereglement (17)   │
│  + opsiyonel: 20-çalışan-sözleşmesi        │
│  (08 taslak desteği verir)                 │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  FAZ 2b — TUTARLILIK GEÇİDİ (Agent 16)    │
│  BLOKAJ: kritik çelişkiler çözülmeden      │
│  FAZ 3'e geçilmez — geri-döngü: taslak     │
│  agent'ları matrise göre revize eder       │
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
│  3-seviye karar hiyerarşisi: Emredici      │
│  hukuk > Founder koruması > Yatırımcı dostu│
│  ✋ FOUNDER CHECKPOINT 1: direktif onayı   │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  FAZ 5 — FİNAL BELGELER (Agent 11)        │
│  10 belge, imzaya hazır format             │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  FAZ 5b — FİNAL TUTARLILIK (Agent 16, 2.  │
│  invokasyon): final set + CEO direktif     │
│  traceability kontrolü                     │
│  ✋ FOUNDER CHECKPOINT 2: imza & tescil    │
│  onayı (FAZ 6 öncesi)                      │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  FAZ 6 — OPERASYONEL UYGULAMA [sıralı/sürekli] │
│  19-brønnøysund-kayıt · 21-yıllık-uyum     │
│  + on-demand: 23-ticari-sözleşmeler        │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  FAZ 7 — KAPANIŞ & EMİSYON (Agent 22)     │
│  [olay-tetiklemeli: imzalı term sheet]     │
│  22 → 02/04 (cap table) → 16 (yeniden     │
│  geçit) → 11 (v2 belgeler) → ✋ FOUNDER   │
│  → Altinn bildirimi → 21 (yeni takvim)     │
│  Her yatırım turunda tekrar çalışır        │
└──────────────────────────────────────────┘

NOT: Her agent, oturumlar arası durum takibi için S0 protokolüne uyar —
bkz. S0-durum-yonetimi.md (suderra/durum.json şeması).
```

---

## Agent Listesi (23 Agent + S0 Protokolü)

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
| 09 | Dava Uzmanı Agent | Avukat | Mahkeme testi — 11 senaryo (A-K) |
| 10 | Founder Avukatı Agent | Avukat | ADVERSARİAL: karşı taraf avukatının argümanları |
| 11 | Belge Uzmanı Agent | Çıktı | Nihai format, imzaya hazır 10 belge |
| 12 | Şeytan'ın Avukatı | Kalite | FAZ 3'te çalışır — CEO'dan ÖNCE kötü senaryoları test eder |
| 13 | Emsal Araştırma Agent | Araştırma | Davalar (anti-hallüsinasyon korumalı), 20 yazım hatası |
| 14 | IP & Yazılım Hakları | Hukuk | IP atama, açık kaynak politikası, veri sahipliği |
| 15 | GDPR & Veri Uyum | Hukuk | Personopplysningsloven, Databehandleravtale şablonu |
| 16 | Belge Tutarlılık | Kalite | BLOKAJ GEÇIDI: FAZ 2b'de 9 taslak (+ ops. arbeidskontrakt) çapraz kontrol; FAZ 5b'de final 10 belge + traceability |
| 17 | Styrereglement | Çıktı | Norveç yönetim kurulu tüzüğü (Aksjeloven §6-23) |
| 18 | Co-founder Perspektif | Kalite | "Bu sözleşmeyi imzalar mıydım?" testi |
| 19 | Brønnøysund Kayıt Rehberi | Süreç/YENİ | Altinn adım adım tescil, pre-registration uyarısı |
| 20 | Çalışan Sözleşmesi | Hukuk/YENİ | Norveç arbeidskontrakt (co-founder çalışan ise) |
| 21 | Yıllık Uyum Takvimi | Süreç/YENİ | Tüm yıllık son tarihler: vergi, Brønnøysund, GDPR |
| 22 | Kapanış & Emisyon | Süreç/YENİ | FAZ 7: imzalı term sheet → kapitalforhøyelse belgeleri, §10-9 üç-ay takibi, S2→S1 geri besleme döngüsü |
| 23 | Ticari Sözleşmeler | Hukuk/YENİ | SaaS müşteri sözleşmesi + oppdragsavtale (aml §1-8 testi, yüklenici IP devri) — on-demand |
| S0 | Durum Yönetimi Protokolü | Koordinasyon | Agent değil protokol: suderra/durum.json ile oturumlar arası belge versiyonu/gate/outreach durumu takibi |

---

## Çalışma Sırası (Güncellenmiş Fazlar)

```
FAZ 0 — Araştırma (Agent 13)
  ↓ Paralel: Norveç davaları (anti-hallüsinasyon korumalı) + 20 yazım hatası kataloğu

FAZ 1 — Uzman Araştırması [iki alt dalga]
  ↓ FAZ 1a (Agent 03, 07, 05) [paralel]: Aksjeloven + Vergi fırsatları
    (Fritaksmetoden, Skattefunn, opsjonsordning) + Yatırımcı beklentileri
  ↓ FAZ 1b (Agent 02): CFO — cap table, dilution, arbeidsgiveravgift, MVA;
    Agent 05 ve 07'nin FAZ 1a çıktılarını girdi olarak alır (faz-içi bağımlılık
    bu yüzden iki alt dalgaya bölündü)

FAZ 2 — Taslak Belgeler (9 taslak + 1 opsiyonel) [paralel] (08 taslak desteği verir)
  ↓ Stiftelsesdokument (03) + Vedtekter (03) + Sweat Equity (06) + Aksjonæravtale (04)
  ↓ Holding Plan (07) + Term Sheet (05) + Skattefunn (07, mali kısım 02 desteğiyle)
    + IP Policy (14) + Styrereglement (17)
  ↓ Opsiyonel: Çalışan Sözleşmesi (Agent 20) — yalnızca co-founder çalışan sayılırsa
  NOT: GDPR/Databehandleravtale (Agent 15) burada DRAFT edilmez — Agent 15 FAZ 3'te
  inceleme yapar; databehandleravtale şablonu 08-ip-politikasi.md belgesi içinde özetlenir
  (bkz. Agent 11 belge #8 içeriği), ayrı bir belge sayılmaz.

FAZ 2b — Tutarlılık Kontrolü (Agent 16, 1. invokasyon) ← BLOKAJ GEÇIDI
  ↓ FAZ 2'nin 9 taslağı (+ opsiyonel arbeidskontrakt) çapraz kontrol —
    KRITIK çelişkiler çözülmeden FAZ 3'e geçilmez
  ↓ GERİ-DÖNGÜ: KRİTİK çakışma bulunursa ilgili taslak agent'ları belgelerini
    Agent 16'nın tutarlılık matrisine göre revize eder; taslak agent'larının
    çözemediği çakışmalarda Agent 01 sınırlı bir "ön-arbitraj" turu yapar
    (yalnızca çakışan hükümler için — tam sentez FAZ 4'te)

FAZ 3 — TÜM ELEŞTİRİLER (Agent 08, 09, 10, 12, 14, 15, 18) [paralel] ← Agent 12 buraya taşındı
  ↓ Preliminary legal review (08) — 11 mahkeme senaryosu A-K (09) — Adversarial argümanlar 7 saldırı vektörü (10)
  ↓ Şeytan'ın avukatı / kötü senaryolar (12) — IP (14) — GDPR (15) — Co-founder testi (18)
  ↓ (+ 03/04/05/07 ikincil inceleme: kendi uzmanlık alanındaki taslak
    değişikliklerini doğrular)
  ↓ NOT: Agent 12 artık Agent 01'den ÖNCE çalışır; CEO tüm eleştirileri alır

FAZ 4 — CEO Sentezi (Agent 01)
  ↓ 3-seviye karar hiyerarşisi: Emredici Norveç hukuku uyumu > Founder koruması > Yatırımcı dostu
  ↓ FAZ 3'teki TÜM eleştiri çıktılarını alır (08+09+10+12+14+15+18
    + 03/04/05/07 ikincil inceleme çıktıları)
  ✋ FOUNDER CHECKPOINT 1: CEO direktif raporu founder'a sunulur — founder
    onaylamadan FAZ 5 başlamaz

FAZ 5 — Final Belgeler (Agent 11)
  ↓ CEO direktifini uygular, imzaya hazır 10 belge üretir

FAZ 5b — Final Tutarlılık Kontrolü (Agent 16, 2. invokasyon) ← BLOKAJ GEÇIDI
  ↓ Agent 16 final belgeler üzerinde ikinci kez çalışır: Agent 11 çıktı setini
    aynı tutarlılık matrisiyle tarar + CEO direktifindeki kabul edilen
    revizyonların belgelere gerçekten işlendiğini kontrol eder (traceability)
  ✋ FOUNDER CHECKPOINT 2: imza-ve-tescil onayı — founder final belgeleri
    inceleyip onaylamadan FAZ 6 (tescil) başlamaz

FAZ 6 — Operasyonel Uygulama (Agent 19, 21) [sıralı, sonrasında sürekli]
  ↓ Agent 19: Final stiftelsesdokument ile Brønnøysund/Altinn tescil rehberi uygulanır
  ↓ Agent 21: Tescil sonrası yıllık uyum takvimi kurulur — bu noktadan itibaren sürekli/
    tekrarlayan bir agent olarak çalışır (FAZ 0-5b'nin tek seferlik kuruluş döngüsünün dışında)
  ↓ SONRAKİ SİSTEM (el değiştirme): Kuruluş tamamlandığında yatırım turu süreci
    için Sistem 2 ile devam edin — yatirimci-sistemi/S2-00.5 pre-flight ile başlayın
  ↓ On-demand: Agent 23 (Ticari Sözleşmeler) — ilk müşteri/pilot veya ilk
    yüklenici gündeme geldiğinde (kuruluş döngüsünü bloklamaz)

FAZ 7 — Kapanış & Emisyon (Agent 22) [olay-tetiklemeli, her yatırım turunda]
  ↓ Tetikleyici: Sistem 2'den (S2-14/S2-15) veya founder'dan "imzalı term sheet" sinyali
  ↓ Agent 22: GK protokolü + tegningsliste + revize belge direktifleri (v2)
  ↓ Agent 02/04: post-round cap table + oy matematiği doğrulaması
  ↓ Agent 16 (yeniden geçit) → Agent 11 (v2 final belgeler)
  ✋ FOUNDER CHECKPOINT 3: kapanış paketi onayı
  ↓ Foretaksregisteret bildirimi (§10-9 — tegningsfrist bitiminden itibaren 3 ay!)
  ↓ Agent 21: yeni yükümlülükler takvime; S2-12: yatırımcı durumu "INVESTED";
    durum.json güncellenir
```

**Durum yönetimi:** Tüm fazlarda her agent, `S0-durum-yonetimi.md` protokolüne
uyar: başlarken `suderra/durum.json` okunur, bitirirken yalnız kendi alanı
güncellenir. Yeni LLM oturumu = "durum.json'u oku ve devam et".

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

Opsiyonel / olay-tetiklemeli belgeler (10-belge sayımına dahil değildir):
- arbeidskontrakt (Agent 20 — co-founder çalışan sayılırsa)
- saas-musteri-sozlesmesi + oppdragsavtale (Agent 23 — ilk müşteri/yüklenici)
- FAZ 7 kapanış seti: GK protokolü, tegningsliste, vedtekter v2,
  aksjonæravtale v2 (Agent 22 — her yatırım turunda)

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
  D: "Çalışan opsiyon havuzu — 1:1 oy — tercihsiz (ESOP)"
holding_zamanlama: "30k NOK değerindeyken — değer artmadan"
hukuk: "aksjeloven (LOV-1997-06-13-44, güncel hali)"
```

---

## Sistem 2 (yatirimci-sistemi/) ile İlişki

Bu sistem (S1) şirket kuruluşunu kapsar. Yatırım turu süreci ayrı bir sistemde
(Sistem 2 — `yatirimci-sistemi/`) yürütülür. Bu repo'daki bazı agent'lar
(örn. Agent 19, Agent 21) Sistem 2 bileşenlerine referans verir:

- **S2-00.5** — Pre-flight kontrol: S1 çıktılarının (final belgeler, tescil)
  yatırım turuna hazır olduğunu doğrular. FAZ 6 tamamlandığında buradan devam edilir.
- **S2-07** — Yatırım turu süreç bileşeni (Sistem 2 içinde tanımlı).
- **S2-14** — Term sheet / emisyon varsayımları bileşeni; C hissesi emisyon
  ön-yetkilendirmesinin (vedtekter styrefullmakt) S1 belgelerinde hazır olmasını bekler
  (bkz. Agent 11 belge #2 ve Agent 16 kontrol matrisi).
- **S2-15** — Gelen term sheet'leri S1 belge 06 şablonuna ve kırmızı çizgilere
  karşı analiz eder; müzakere bitince Agent 22'yi (FAZ 7) tetikler.
- **S2-16** — Data room hazırlığı: S1 belgelerinin DD-hazır paketlenmesi
  (durum.json versiyonlarıyla).
- **S2-17** — GDPR & outreach uyum: S1 Agent 15'in çerçevesini yatırımcı
  istihbaratı bağlamına uyarlar.

Geri besleme döngüsü: yatırım kapandığında S2 → **Agent 22 (FAZ 7)** → S1
belgeleri v2 olarak güncellenir ve Agent 16/11 geçitlerinden yeniden geçer.
Ortak durum: iki sistem de `suderra/durum.json` üzerinden senkronize olur
(bkz. S0-durum-yonetimi.md).

Bu referansların detayları için `yatirimci-sistemi/` klasörüne bakın.
