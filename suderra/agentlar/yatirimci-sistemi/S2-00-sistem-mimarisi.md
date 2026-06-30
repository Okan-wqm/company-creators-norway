# Sistem 2 — Yatırımcı Zekası Sistemi Mimarisi

## Amaç
Norveç'teki potansiyel yatırımcıları bul, profilini çıkar, Suderra'ya uygunluğunu sırala
ve kişiye özel ilk temas stratejisi hazırla.

---

## Genel Yapı

```
                    ┌────────────────────────────┐
                    │  FOUNDER (SEN)              │
                    │  "Hangi yatırımcıya gitmeliyim?" │
                    └──────────────┬─────────────┘
                                   │
              ┌────────────────────▼────────────────────┐
              │           S2-01: EKOSİSTEM HARİTALAMA   │
              │   Norveç aquaculture yatırım ekosistemi  │
              │   tam harita: VC, angel, devlet, ivme    │
              └──┬──────────┬──────────┬──────────┬─────┘
                 │          │          │          │
                 ▼          ▼          ▼          ▼
          ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
          │S2-02     │ │S2-03     │ │S2-04     │ │S2-06     │
          │PROFİL    │ │PORTFÖLİO │ │EŞLEŞME & │ │YATIRIMCI │
          │ARAŞTIRMA │ │ANALİST   │ │SIRALAMA  │ │SORULARI  │
          │          │ │          │ │          │ │          │
          │Her kişi  │ │Ne zaman, │ │Suderra'ya│ │Due dilig.│
          │hakkında  │ │neye, kaç │ │en uygun  │ │soruları  │
          │derin     │ │yatırdılar│ │20 kişi   │ │ve cevapla│
          │profil    │ │          │ │öncelikli │ │rı hazırla│
          └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘
               │            │            │            │
               └────────────┴────────────┘            │
                            │                         │
                            ▼                         │
              ┌─────────────────────────┐             │
              │    S2-05: OUTREACH      │◄────────────┘
              │    YAZARI               │
              │  Kişiye özel mesajlar   │
              │  + pitch deck notu      │
              └─────────────┬───────────┘
                            │
                            ▼
              ┌─────────────────────────┐
              │  ÇIKTI: YATIRIMCİ      │
              │  İSTİHBARAT PAKETI      │
              │                         │
              │  - Öncelikli 20 kişi   │
              │  - Her kişi profili     │
              │  - Özel mesajlar        │
              │  - Due diligence hazırlık│
              └─────────────────────────┘
```

---

## Agent Listesi (14 Agent — Güncellenmiş)

| # | Agent | Görev | Çıktı | Faz |
|---|-------|-------|-------|-----|
| S2-07 | Founder Onboarding | Suderra Pitch Datasheeti üretir (TÜM sistemin girdi kaynağı) | JSON datasheet + readiness score | FAZ -1 |
| S2-01 | Ekosistem Haritalama | 50-80 yatırımcı listesi (Havbruksfond + Banka VC + Stratejik dahil) | Yatırımcı listesi | FAZ 0 |
| S2-13 | Rekabet İstihbaratı | Rakip analizi — S2-06 ve S2-10'a veri sağlar | Competitor cards + positioning | FAZ 0 |
| S2-08 | Veri Doğrulama | S2-01 listesini bağımsız kaynaklarla çapraz kontrol eder | Doğrulanmış liste | FAZ 0b |
| S2-02 | Profil Araştırmacı | Her yatırımcı için derin kişi/şirket profili | Yapılandırılmış profil kartları | FAZ 1 |
| S2-03 | Portfolio Analist | Geçmiş yatırımların deseni, tutar, zamanlama | Yatırım davranış analizi | FAZ 1 |
| S2-04 | Eşleşme & Sıralama | Suderra uyum skoru (8 kriter, bonus cap ±2) — PHASE-1 only default | Top 20 liste + gerekçe | FAZ 2 |
| S2-09 | Devlet Fonu Başvuru | Skattefunn + SIVA + Innovasjon Norge + BIA başvuruları | Hazır başvuru paketleri | FAZ 2 |
| S2-10 | Pitch Deck İçerik | 10 slide için metin içerik (traction seviyesine göre) | Slide content | FAZ 2 |
| S2-14 | Yatırım Süreci Yönetim | Yatırımcı tipi başına tam süreç haritası + vergi dönüm noktaları | Süreç rehberi + vergi takvimi | FAZ 3 |
| S2-05 | Outreach Yazarı | Kişiye özel ilk temas mesajı + e-posta | Hazır iletişim şablonları | FAZ 3 |
| S2-06 | Yatırımcı Soruları | Due diligence soruları + hazır cevaplar (S2-07 datasheeti ile doldurulur) | Q&A belgesi | FAZ 3 |
| S2-11 | Toplantı Hazırlık | Her yatırımcı toplantısı için 2 sayfalık brifing | Meeting briefing | FAZ 3 (on-demand) |
| S2-12 | Geri Bildirim | Outreach sonuçlarını analiz eder, S2-04 skorlarını günceller | Updated priority list | FAZ ∞ |

---

## Hedef Yatırımcı Kategorileri

### Kategori A — AquaTech Odaklı (En Yüksek Öncelik)
```
Hatch AS (Bergen)           — Aquaculture accelerator, seed stage
Aqua-Spark                  — Global, Norveç odaklı, aquaculture VC
Katapult Ocean              — Impact VC, blue economy
Spawn Capital               — AquaTech, food tech, seed/Series A
```

### Kategori B — Devlet & Yarı-Devlet Fonlar
```
Investinor AS               — Norveç devlet yatırım fonu, early stage
Innovasjon Norge            — Hibe + loan + equity, aquaculture için özel programlar
Norges Forskningsråd (BIA)  — AR-GE hibeleri, Skattefunn koordinasyonu (S2-09 başvuru hazırlar)
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
Balderton Capital         — European tech, Norveç portföyü var
Northzone                 — Nordic focused VC
```

### Kategori F — Havbruksfond (Municipal Aquaculture Funds)
```
Bergen kommune            — Havbruksfond geliri, aquaculture-yakın yatırım
Tromsø kommune            — Kuzey Norveç aquaculture merkezi
Ålesund kommune           — Balıkçılık geleneği, yerel destek
Kinn kommune              — Vestland, havbruksfond aktif
```
Not: Bu fonlar özel yatırımcı değil — ancak yerel destek, inkübatör erişimi,
pilot müşteri bağlantısı için kritik. S2-09 bu müzelerin programlarını araştırır.

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
| **PHASE-2** | İlk ödeme yapan müşteri veya imzalı LOI | AB dahil | Aqua-Spark (NL), EIC Accelerator (max €2.5M equity), Nordic Investment Bank |
| **PHASE-3** | ARR > 5M NOK veya Series A hazırlığı | Uluslararası | Chile/CORFO, Kanada, IFC (Dünya Bankası), Asia Pacific aquaculture |

S2-04 varsayılan olarak SADECE PHASE-1 yatırımcılarını sıralar.
S2-07 Modül 9'da founder "Yalnızca Norveç" seçerse PHASE-1 hard filter aktif olur.

---

## Güncellenmiş Çalışma Sırası

```
FAZ -1: S2-07 Founder Onboarding (TÜM sistemden önce çalışır)
  ↓ Suderra Pitch Datasheet üretilir — tüm [boşluklar] doldurulur
  ↓ Investor Readiness Score: 0-10

FAZ 0:  S2-01 (Ekosistem) + S2-13 (Rekabet İstihbaratı) [paralel]
  ↓ S2-01: 50-80 yatırımcı listesi (Havbruksfond dahil)
  ↓ S2-13: Fishtalk, AquaCloud, Excel/WhatsApp rakip kartları

FAZ 0b: S2-08 (Veri Doğrulama)
  ↓ S2-01 listesinin %70+ PASS kontrolü — başarısız olanlar elenir

FAZ 1:  S2-02 + S2-03 [paralel — validated liste üzerinde]
  ↓ Profil kartları + portfolio analizi

FAZ 2:  S2-04 (Eşleştirme) + S2-09 (Devlet Fonu) + S2-10 (Pitch Deck) [paralel]
  ↓ Top 20 priority list + hazır başvuru paketleri + pitch içerik

FAZ 3:  S2-14 + S2-05 + S2-06 + S2-11 [paralel]
  ↓ S2-14: Yatırımcı tipi başına süreç haritası + vergi dönüm takvimi ← YENİ
  ↓ Outreach mesajları + Q&A + toplantı brifingleri (on-demand)

FAZ ∞:  S2-12 (Geri Bildirim) — her outreach dalgası sonrası tekrar çalışır
  ↓ Skorlar güncellenir, sonraki dalga optimize edilir
```

---

## Suderra Pitch Parametreleri

```yaml
sirket: Suderra AS
sektor: Aquaculture çiftlik yönetim yazılımı
neden_norveç: Dünya aquaculture liderinin teknoloji çözüme ihtiyacı var
pazar: Norveç + global aquaculture (250B USD market)
aşama: Pre-seed / Seed
aranılan_yatrım: [TBD] NOK
kullanim: Yazılım geliştirme, ilk müşteriler, ekip
diferansiyasyon: [Founder tarafından belirtilecek]
rekabet_avantajı: [Founder tarafından belirtilecek]
```
