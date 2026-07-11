# Sistem 2 — Yatırımcı Zekası Sistemi Mimarisi

## Amaç
Norveç'teki potansiyel yatırımcıları bul, profilini çıkar, Suderra'ya uygunluğunu sırala
ve kişiye özel ilk temas stratejisi hazırla.

---

## Genel Yapı

Bu diyagram FAZ akışının üst düzey özetidir. Tam ve otoriter sıralama için aşağıdaki
"Güncellenmiş Çalışma Sırası" ve "Agent Listesi" bölümlerine bakın.

```
┌─────────────────────────┐
│  FOUNDER (SEN)            │
│  "Hangi yatırımcıya gitmeliyim?" │
└────────────┬─────────────┘
             ▼
┌──────────────────────────────────────────┐
│ FAZ -1 — Onboarding + Pre-Flight [sıralı] │
│ S2-07 (Pitch Datasheet) → S2-00.5 (Gate)  │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│ FAZ 0 — Ekosistem + Rekabet [paralel]     │
│ S2-01 (50-80 yatırımcı) + S2-13 (rakipler)│
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│ FAZ 0b — Veri Doğrulama (S2-08)           │
│ %70 kuralı: yatırımcı başına 7 kontrolün  │
│ ≥%70'i (≥5) Green değilse elenir          │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│ FAZ 1 — Derinlemesine Araştırma [paralel] │
│ S2-02 (profil) + S2-03 (portfolio)        │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│ FAZ 2 — Eşleştirme + Hazırlık [paralel]   │
│ S2-04 (Top 20) + S2-09 (devlet fonu) +    │
│ S2-10 (pitch deck içerik)                 │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│ FAZ 3 — Outreach Hazırlığı [paralel]      │
│ S2-14 (süreç haritası) + S2-05 (outreach) │
│ + S2-06 (Q&A) + S2-11 (toplantı brifingi) │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│  ÇIKTI: YATIRIMCİ İSTİHBARAT PAKETİ       │
│  Öncelikli 20 kişi + profiller + mesajlar │
│  + Q&A + devlet fonu başvuruları + deck   │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│ FAZ 3.5 — Term Sheet Analiz (S2-15)       │
│ [on-demand] red-line + karşı teklif →     │
│ imza sonrası S1-Agent 22 (FAZ 7) tetikler │
└────────────────────┬──────────────────────┘
                      ▼
┌──────────────────────────────────────────┐
│ FAZ ∞ — Geri Bildirim (S2-12)             │
│ Her outreach dalgası sonrası tekrar çalışır│
└──────────────────────────────────────────┘

Sürekli: S2-17 (GDPR & outreach uyum — dalga öncesi blokaj) ·
S2-16 (data room, FAZ 3) · S0 durum protokolü (durum.json)
```

---

## Agent Listesi (18 Agent — Güncellenmiş)

| # | Agent | Görev | Çıktı | Faz |
|---|-------|-------|-------|-----|
| S2-07 | Founder Onboarding | Suderra Pitch Datasheeti üretir (TÜM sistemin girdi kaynağı) | JSON datasheet + readiness score | FAZ -1 |
| S2-00.5 | Pre-Flight Doğrulama | Sistem 1 tamamlığını kontrol eder — GEÇMEDEN sistemi başlatma | PASS/PARTIAL/FAIL raporu | FAZ -1 |
| S2-01 | Ekosistem Haritalama | 50-80 yatırımcı listesi (Havbruksfond + Banka VC + Stratejik dahil) | Yatırımcı listesi JSON | FAZ 0 |
| S2-13 | Rekabet İstihbaratı | Rakip analizi — S2-06 ve S2-10'a veri sağlar | Competitor cards + positioning | FAZ 0 |
| S2-08 | Veri Doğrulama | S2-01 listesini bağımsız kaynaklarla çapraz kontrol eder | Doğrulanmış liste | FAZ 0b |
| S2-02 | Profil Araştırmacı | Her yatırımcı için derin kişi/şirket profili | Yapılandırılmış profil kartları | FAZ 1 |
| S2-03 | Portfolio Analist | Geçmiş yatırımların deseni, tutar, zamanlama | Yatırım davranış analizi | FAZ 1 |
| S2-04 | Eşleşme & Sıralama | Suderra uyum skoru (8 kriter, bonus cap ±2) — PHASE-1 only default | Top 20 liste + gerekçe | FAZ 2 |
| S2-09 | Devlet Fonu Başvuru | Skattefunn + SIVA + Innovasjon Norge + IPN (eski BIA) başvuruları | Hazır başvuru paketleri | FAZ 2 |
| S2-10 | Pitch Deck İçerik | 10 slide için metin içerik (traction seviyesine göre) | Slide content | FAZ 2 |
| S2-14 | Yatırım Süreci Yönetim | Yatırımcı tipi başına tam süreç haritası + vergi dönüm noktaları | Süreç rehberi + vergi takvimi | FAZ 3 |
| S2-05 | Outreach Yazarı | Kişiye özel ilk temas mesajı + e-posta | Hazır iletişim şablonları | FAZ 3 |
| S2-06 | Yatırımcı Soruları | Due diligence soruları + hazır cevaplar (S2-07 datasheeti ile doldurulur) | Q&A belgesi | FAZ 3 |
| S2-11 | Toplantı Hazırlık | Her yatırımcı toplantısı için 2 sayfalık brifing | Meeting briefing | FAZ 3 (on-demand) |
| S2-12 | Geri Bildirim | Outreach sonuçlarını analiz eder, S2-04 skorlarını günceller | Updated priority list | FAZ ∞ |
| S2-15 | Term Sheet Analiz | Gelen term sheet'i S1 belge 06 + kırmızı çizgilere karşı test eder, karşı-teklif üretir | Red-line raporu + karşı teklif | FAZ 3.5 (on-demand) |
| S2-16 | Data Room Hazırlık | DD klasör manifesti, eksik/bayat belge raporu, tier erişim matrisi | Data room raporu | FAZ 3 |
| S2-17 | GDPR & Outreach Uyum | LIA, veri minimizasyonu, saklama/silme, markedsføringsloven — dalga öncesi BLOKAJ | LIA + dalga kontrol verdikti | FAZ 0'dan itibaren sürekli |

---

## Hedef Yatırımcı Kategorileri

### Kategori A — AquaTech Odaklı (En Yüksek Öncelik)
```
Hatch AS (Bergen)           — Aquaculture accelerator, seed stage
Aqua-Spark                  — Global, Norveç odaklı, aquaculture VC
Katapult Ocean              — Impact VC, blue economy
Spawn Capital               — AquaTech, food tech, seed/Series A
                              (DOĞRULANMALI — varlığı web + proff.no fetch ile
                              teyit edilmeli; bulunamazsa listeden çıkar,
                              Bluefront Equity gibi alternatifleri araştır)
```

### Kategori B — Devlet & Yarı-Devlet Fonlar
```
Investinor AS               — Norveç devlet yatırım fonu, early stage
Innovasjon Norge            — Hibe + loan + equity, aquaculture için özel programlar
Norges Forskningsråd (IPN)  — AR-GE hibeleri ("Innovasjonsprosjekt i næringslivet",
                              eski BIA'nın yerini aldı; løpende başvuru), Skattefunn
                              koordinasyonu (S2-09 başvuru hazırlar)
SIVA                        — Teknoloji transfer, inkübatör (S2-09 başvuru hazırlar)
```

### Kategori C — Sektör Bağlantılı Family Offices
```
Bergen merkezli family offices    — Salmon/aquaculture servetleri
Ålesund merkezli family offices   — Balıkçılık geçmişi
Tromsø merkezli yatırımcılar      — Kuzey Norveç aquaculture
Stavanger merkezli (enerji geçiş) — Offshore'dan blue economy'ye geçiş
```

### Kategori D — Teknoloji & AgriTech VC'ler
```
Norban (Norwegian Business Angels Network)
Alliance Venture
Ferd AS
Kistefos
Middelthon-familien
```

### Kategori E — Uluslararası ama Norveç Odaklı
```
Eir Ventures              — Nordic digital health & food tech
                            (DOĞRULANMALI — bilinen profili yaşam bilimleri;
                            eirventures.eu fetch ile food tech odağını teyit et)
Balderton Capital         — European tech, Norveç portföyü var
                            (DOĞRULANMALI — Norveç portföyü web'de doğrula;
                            balderton.com portfolio fetch)
Northzone                 — Nordic focused VC
```

### Kategori F — Havbruksfond (Municipal Aquaculture Funds)
```
Bergen kommune            — Havbruksfond geliri, aquaculture-yakın yatırım
Tromsø kommune            — Kuzey Norveç aquaculture merkezi
Ålesund kommune           — Møre og Romsdal, balıkçılık geleneği, yerel destek
Kinn kommune              — Vestland, havbruksfond aktif
```
Not: Bu fonlar özel yatırımcı değil — ancak yerel destek, inkübatör erişimi,
pilot müşteri bağlantısı için kritik. S2-09 bu belediyelerin programlarını araştırır.
DOĞRULANMALI: Bu belediye listesi resmi Havbruksfond dağıtım verisiyle
(Fiskeridirektoratet) doğrulanmalı — en büyük alıcılar tipik olarak Frøya,
Nærøysund, Alta gibi belediyelerdir; liste resmi dağıtım verisine göre revize edilmeli.

### Kategori G — Norveç Banka & Sigorta VC Kolları ← YENİ
```
DNB Ventures              — DNB Bank'ın VC kolu, Norveç B2B tech & sustainability
SpareBank 1 SR-Bank       — Stavanger merkezli, blue economy/denizcilik eğilimi
Sparebanken Vest          — Bergen merkezli (laks bölgesi), lokal yatırım
Storebrand Impact         — ESG odaklı, sürdürülebilir aquaculture uyumu
Gjensidige Forsikring     — Büyük sigorta, VC kolu var mı araştır
```
KURAL: Sadece bankanın/sigortanın dedicated VC kolu dahil edilir.
KESINLIKLE HARİÇ: KLP (emeklilik fonu — sadece halka açık piyasa),
NBIM/Norges Bank Investment Management (varlık fonu — sadece halka açık piyasa).
Her ikisi de pre-seed'e yatırım yapmaz, minimum tutar çok yüksek.

### Kategori H — Stratejik / Kurumsal Yatırımcılar ← YENİ
```
AKVA Group ASA            — Norveç aquaculture donanım lideri (⚠️ FishTalk = rakip — CEO onayı gerek)
Mowi ASA                  — Dünyanın en büyük somon şirketi, Mowi Innovation araştır
Lerøy Seafood Group ASA   — Bergen merkezli, corporate venture kolu var mı?
SalMar ASA                — SalMar Innovation, dijital tarım teknolojisi
Cermaq (Mitsubishi)       — Düşük öncelik (Japon ana şirket yapısı)
```
Not: Stratejik yatırımcı = potansiyel pilot müşteri + fon = çift değer.
S2-04'te +1.0 bonus: equity + pilot partnership + distribution = üçlü değer.

---

## Faz Genişleme Tablosu

| Faz | Tetikleyici | Kapsam | Kategoriler |
|-----|-------------|--------|-------------|
| **PHASE-1** | Şimdi (gelir öncesi) | Yalnızca Norveç | A, B, C, D, E, F, G, H |
| **PHASE-2** | İlk ödeme yapan müşteri veya imzalı LOI | AB dahil | Aqua-Spark (NL), EIC Accelerator (max €2.5M grant + €0.5-15M equity, EIC Fund) (DOĞRULANMALI — başvuru anında ec.europa.eu fetch), Nordic Investment Bank |
| **PHASE-3** | ARR > 5M NOK veya Series A hazırlığı | Uluslararası | Chile/CORFO, Kanada, IFC (Dünya Bankası), Asia Pacific aquaculture |

S2-04 varsayılan olarak SADECE PHASE-1 yatırımcılarını sıralar.
S2-07 Modül 9'da founder "Yalnızca Norveç" seçerse PHASE-1 hard filter aktif olur.

---

## Güncellenmiş Çalışma Sırası

```
FAZ -1: S2-07 (Founder Onboarding) → S2-00.5 (Pre-Flight Doğrulama) [sıralı]
  ↓ S2-07 ÖNCE çalışır: Suderra Pitch Datasheet üretilir — valid JSON formatında
  ↓ S2-00.5 SONRA çalışır (M1 + JSON şema kontrolü S2-07 çıktısını gerektirir):
    Hukuki/vergi/materyal hazırlık kontrol — PASS olmadan FAZ 0 başlamaz
  ↓ Investor Readiness Score: 0-10

FAZ 0:  S2-01 (Ekosistem) + S2-13 (Rekabet İstihbaratı) [paralel]
  ↓ S2-01: 50-80 yatırımcı listesi (Havbruksfond dahil)
  ↓ S2-13: Fishtalk, AquaCloud, Excel/WhatsApp rakip kartları

FAZ 0b: S2-08 (Veri Doğrulama)
  ↓ S2-01 listesinin %70 kuralı ile kontrolü — yatırımcı başına 7 kontrolün
    ≥%70'i (≥5) Green (ve Red yok) → PASS; başarısız olanlar elenir

FAZ 1:  S2-02 + S2-03 [paralel — validated liste üzerinde]
  ↓ Profil kartları + portfolio analizi

FAZ 2:  S2-04 (Eşleştirme) + S2-09 (Devlet Fonu) + S2-10 (Pitch Deck) [paralel]
  ↓ Top 20 priority list + hazır başvuru paketleri + pitch içerik

FAZ 3:  S2-14 + S2-05 + S2-06 + S2-11 + S2-16 [paralel]
  ↓ S2-14: Yatırımcı tipi başına süreç haritası + vergi dönüm takvimi
  ↓ Outreach mesajları + Q&A + toplantı brifingleri (on-demand)
  ↓ S2-16: Data room hazırlığı (DD başlamadan hazır olmalı) ← YENİ
  ↓ GATE: S2-17 dalga kontrol listesi GEÇMEDEN S2-05 gönderim yapmaz

FAZ 3.5: S2-15 (Term Sheet Analiz) [on-demand — term sheet geldiğinde] ← YENİ
  ↓ Madde madde red-line analizi (S1 belge 06 + kırmızı çizgiler) + karşı teklif
  ↓ İmza kararı sonrası: S1-Agent 22 (Kapanış & Emisyon, FAZ 7) tetiklenir —
    vedtekter/aksjonæravtale v2 + kapitalforhøyelse S1 tarafında yürütülür

FAZ ∞:  S2-12 (Geri Bildirim) — her outreach dalgası sonrası tekrar çalışır
  ↓ Skorlar güncellenir, sonraki dalga optimize edilir

SÜREKLI: S2-17 (GDPR & Outreach Uyum) — FAZ 0'dan itibaren ← YENİ
  ↓ Veri toplama kuralları (S2-01/02/03'e bağlayıcı), LIA, saklama/silme,
    her dalga öncesi kontrol listesi (BLOKAJ yetkili)
```

**Durum yönetimi:** Her agent `../S0-durum-yonetimi.md` protokolüne uyar —
başlarken `suderra/durum.json` okunur, bitirirken kendi alanı güncellenir.
S1 ile senkronizasyon (belge versiyonları, kapanış döngüsü) bu dosya üzerinden yürür.

---

## Suderra Pitch Parametreleri

```yaml
sirket: Suderra AS
sektor: Aquaculture çiftlik yönetim yazılımı
neden_norveç: Dünya aquaculture liderinin teknoloji çözüme ihtiyacı var
pazar: Norveç + global aquaculture (~$300B — FAO SOFIA 2024 tahmini; güncel raporla doğrula)
aşama: Pre-seed / Seed
aranılan_yatrım: [TBD] NOK
kullanim: Yazılım geliştirme, ilk müşteriler, ekip
diferansiyasyon: [Founder tarafından belirtilecek]
rekabet_avantajı: [Founder tarafından belirtilecek]
```
