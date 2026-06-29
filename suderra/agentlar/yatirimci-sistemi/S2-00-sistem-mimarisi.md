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

## Agent Listesi (6 Agent)

| # | Agent | Görev | Çıktı |
|---|-------|-------|-------|
| S2-01 | Ekosistem Haritalama | Norveç AquaTech yatırım ekosistemini tam haritalandırır | 50+ yatırımcı listesi |
| S2-02 | Profil Araştırmacı | Her yatırımcı için derin kişi/şirket profili | Yapılandırılmış profil kartları |
| S2-03 | Portfolio Analist | Geçmiş yatırımların deseni, tutar, zamanlama | Yatırım davranış analizi |
| S2-04 | Eşleşme & Sıralama | Suderra uyum skoru, öncelik sırası | Top 20 liste + gerekçe |
| S2-05 | Outreach Yazarı | Kişiye özel ilk temas mesajı + e-posta | Hazır iletişim şablonları |
| S2-06 | Yatırımcı Soruları | Due diligence soruları + hazır cevaplar | Q&A belgesi |

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
Norges Forskningsråd        — AR-GE hibeleri, Skattefunn koordinasyonu
SIVA                        — Teknoloji transfer, inkübatör
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

---

## Çalışma Sırası

```
FAZ 0: S2-01 Ekosistem Haritalama (önce çalışır, sonraki 4'e liste sağlar)
FAZ 1: S2-02 + S2-03 (paralel — profil ve portfolio analizi)
FAZ 2: S2-04 Eşleşme & Sıralama (S2-02 ve S2-03 bitince)
FAZ 3: S2-05 + S2-06 (paralel — outreach + due diligence hazırlık)
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
