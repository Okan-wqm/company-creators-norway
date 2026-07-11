# BASLAT.md — Suderra AS Agent Sistemi Kickoff Runbook

Bu dosya, `suderra/agentlar/` altındaki 23 agent'lık sistemin (S1 — şirket
kuruluşu) nasıl başlatılacağını ve oturumlar arasında nasıl yürütüleceğini
tanımlar. Mimari için `suderra/agentlar/00-sistem-mimarisi.md`, durum
yönetimi için `suderra/agentlar/S0-durum-yonetimi.md` dosyasına bakın.

---

## (a) Ön Koşullar + ZORUNLU GİRDİ CHECKLIST'İ

Sistemi başlatmadan önce aşağıdaki bilgileri hazırlayın. FAZ 0-4
(araştırma, taslak, eleştiri, sentez) bu veriler olmadan placeholder ile
yürüyebilir; **FAZ 5 (imzaya hazır final belgeler) ve FAZ 6 (tescil) bu
veriler olmadan ÜRETİLEMEZ.**

### Kişi bilgileri
- [ ] Founder ad-soyad
- [ ] Founder fødselsnummer veya D-numarası
- [ ] Founder adresi
- [ ] Co-founder 1 ad-soyad + fødselsnummer/D-numarası + adres
- [ ] Co-founder 2 ad-soyad + fødselsnummer/D-numarası + adres

### Şirket bilgileri
- [ ] Forretningsadresse (şirket iş adresi — arbeidsgiveravgift sonesi
      bu adresin kommune'sine göre belirlenir)
- [ ] Styre (yönetim kurulu) üyeleri: kimler, hangi roller
      (styreleder zorunlu)

### Parametre onayı
- [ ] `00-sistem-mimarisi.md` "Şirket Parametreleri" bloğunun founder
      tarafından onayı: şirket adı, holding, sermaye (30.000 NOK),
      A/B/C/D hisse yapısı, holding zamanlaması

### Teknik ön koşullar
- [ ] Bu repo'ya erişimi olan bir LLM oturumu (dosya okuma/yazma yetkili)
- [ ] Tercihen web erişimi (agent'ların "MANDATORY WEB VERIFICATION"
      adımları için). Web erişimi yoksa: S0 fallback kuralı uygulanır —
      bulgu CONFIDENCE: LOW işaretlenir ve `acik_aksiyonlar`'a
      "manuel doğrulama" kaydı düşülür.
- [ ] `suderra/durum.json` mevcut (repo'da hazır bootstrap şablonu vardır;
      yoksa S0 şemasından oluşturulur)

---

## (b) Yol Standartları

Tüm agent'lar çıktılarında şu yolları kullanır (bağlayıcı standart):

| İçerik | Yol |
|--------|-----|
| Taslak belgeler (FAZ 2) | `suderra/belgeler/taslak/` |
| Final belgeler (FAZ 5+) | `suderra/belgeler/` |
| Faz raporları | `suderra/raporlar/` (örn. `faz3-agent08.md`) |
| S2 ara çıktıları | `suderra/s2/` (`datasheet.json`, `yatirimcilar.json`, `profiller/`) |
| Outreach log | `suderra/outreach-log.json` |
| Ortak durum dosyası | `suderra/durum.json` |

---

## (c) Oturum Planı

**Varsayılan kural: 1 oturum = 1 agent.** Her agent kendi oturumunda,
kendi tanım dosyasıyla çalıştırılır — böylece bağlam şişmez ve her rapor
temiz bir perspektiften üretilir.

- **Paralel fazlarda (FAZ 1a, FAZ 2, FAZ 3):** her agent AYRI bir
  oturumda çalıştırılır. Paralellik "aynı anda" değil "birbirinden
  bağımsız sırayla" da olabilir — önemli olan her agent'ın diğerlerinin
  taslağını değil, faz girdilerini almasıdır.
- **Rapor disiplini:** her agent raporunu
  `suderra/raporlar/fazX-agentYY.md` dosyasına yazar
  (örn. `faz3-agent09.md`). Sonraki fazın oturumu bu dosyaları girdi alır.
- **durum.json disiplini:** her oturum sonunda agent yalnız KENDİ alanını
  günceller (S0 protokolü, 2 kural).
- **Gate/checkpoint'lerde durulur:** FAZ 2b ve FAZ 5b geçitleri PASS
  olmadan sonraki faza geçilmez; FOUNDER CHECKPOINT 1 (FAZ 4 sonrası),
  CHECKPOINT 2 (FAZ 5b sonrası, imza-ve-tescil onayı) ve CHECKPOINT 3
  (FAZ 7 kapanış paketi) founder onayı olmadan geçilmez.

---

## (d) Oturum Açılış Promptu (kopyala-yapıştır şablonu)

Her yeni oturumu şu şablonla açın (köşeli parantezleri doldurun):

```
Şu dosyaları oku:
- suderra/agentlar/[<agent-dosyası>.md]  (örn. 03-aksjeloven-agent.md)
- suderra/agentlar/S0-durum-yonetimi.md
- suderra/agentlar/00-sistem-mimarisi.md (özellikle "Şirket Parametreleri" bloğu)
- suderra/durum.json
- [fazın girdi raporları: suderra/raporlar/faz<X>-agent<YY>.md ...]

Rolünü uygula. Raporunu suderra/raporlar/faz[X]-agent[YY].md dosyasına yaz
(belge üretiyorsan belgeyi suderra/belgeler/taslak/ veya suderra/belgeler/
altına yaz). Bitirirken suderra/durum.json'da yalnız kendi alanını güncelle.
```

### Faz sırası (FAZ 0 → FAZ 7)

| Faz | Agent(lar) | Not |
|-----|-----------|-----|
| FAZ 0 | 13 | Araştırma: davalar + yazım hataları kataloğu |
| FAZ 1a | 03, 07, 05 | Paralel — her biri ayrı oturum |
| FAZ 1b | 02 | 05 ve 07'nin FAZ 1a raporlarını girdi alır |
| FAZ 2 | 03, 04, 05, 06, 07, 14, 17 (+02, 08 destek; ops. 20) | 9 taslak + 1 opsiyonel, paralel — taslaklar `belgeler/taslak/` altına |
| FAZ 2b | 16 (1. invokasyon) | ⛔ BLOKAJ GEÇİDİ — KRİTİK çakışmalar çözülmeden FAZ 3'e geçilmez; çözülmeyen çakışmalar Agent 01 ön-arbitrajına |
| FAZ 3 | 08, 09, 10, 12, 14, 15, 18 (+03/04/05/07 ikincil) | Paralel eleştiriler — her biri ayrı oturum |
| FAZ 4 | 01 | CEO sentezi → ✋ FOUNDER CHECKPOINT 1 (direktif onayı) |
| FAZ 5 | 11 | Final 10 belge → `suderra/belgeler/` |
| FAZ 5b | 16 (2. invokasyon) | ⛔ BLOKAJ GEÇİDİ + traceability → ✋ FOUNDER CHECKPOINT 2 (imza & tescil onayı) |
| FAZ 6 | 19, 21 (+ on-demand 23) | Tescil + yıllık takvim; sonrası Sistem 2'ye geçiş |
| FAZ 7 | 02/04 → 22 → 16 (FAZ 7 modu) → 11 (v2) | Olay-tetiklemeli (imzalı term sheet); ✋ FOUNDER CHECKPOINT 3 |

---

## (e) Devam Senaryosu (kaldığın yerden)

Çalışma yarıda kaldıysa yeni oturumu tek satırla açın:

```
suderra/durum.json'u oku ve kaldığımız yerden devam et.
```

Agent/oturum, durum.json'daki belge versiyonlarına, gate verdiktlerine ve
`acik_aksiyonlar` listesine bakarak hangi fazda/agent'ta kalındığını tespit
eder ve (d)'deki şablonla ilgili agent'ı çalıştırmayı önerir.

---

## (f) Sistem 2'ye Geçiş (yatırım turu)

FAZ 6 tamamlandığında (şirket tescilli, final belgeler imzalı) yatırım turu
süreci Sistem 2'de (`suderra/agentlar/yatirimci-sistemi/`) yürütülür. Sıra:

1. **S2-07 (Founder Onboarding)** — pitch datasheet üretilir
   (`suderra/s2/datasheet.json`). S2-00.5'in M1 kontrolü bu çıktıyı
   gerektirdiği için ÖNCE çalıştırılır.
2. **S2-00.5 (Pre-flight Doğrulama)** — S1 çıktılarının yatırım turuna
   hazırlığı doğrulanır; verdikt `durum.json`
   `gate_sonuclari.s2_00_5_preflight` alanına yazılır.
3. Sonrası S2 mimarisine göre devam eder
   (`yatirimci-sistemi/S2-00-sistem-mimarisi.md`).

Yatırım kapandığında S2 → **Agent 22 (FAZ 7)** geri besleme döngüsü
devreye girer (yukarıdaki faz tablosunun son satırı).
