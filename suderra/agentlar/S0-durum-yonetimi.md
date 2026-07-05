# S0 — Ortak Durum & Versiyon Yönetimi Protokolü (durum.json)

## Kimlik
- **Rol:** İki sistemin (S1 hukuki belgeler + S2 yatırımcı zekası) üzerinde
  oturan hafif koordinasyon protokolü — tam bir agent değil, HER agent'ın
  uyduğu iki satırlık kural + tek bir dosya şeması
- **Çalışma zamanı:** Her oturum başı (oku) ve her agent bitişi (güncelle)

---

## Neden Var

Bu sistemler bir insan founder tarafından ayrı LLM oturumlarında çalıştırılır.
Oturumlar arası durum aktarımı için tanımlı mekanizma parça parçaydı:
OUTREACH_LOG yalnız outreach'i kapsar, S2-07 datasheet'inin versiyon kuralı
yoktu, Agent 11'in revizyon notu belge içindeydi. Hangi belgenin hangi
versiyonda olduğu, preflight verdikti, hangi yatırımcıya ne zaman yazıldığı
tek yerden okunamıyordu — her yeni oturum founder hafızasından başlıyordu.

---

## Protokol (her agent tanımına uygulanan 2 kural)

```
1. BAŞLARKEN: suderra/durum.json dosyasını oku. Kendi girdilerinin
   versiyonlarını buradaki kayıtla karşılaştır — uyuşmazlık varsa
   (örn. "vedtekter v1 ama cap table v2") önce founder'a raporla.
2. BİTİRİRKEN: yalnızca KENDİ alanını güncelle (belge ürettiyse versiyon+tarih,
   gate çalıştırdıysa verdikt, outreach yaptıysa log yolu). Başka agent'ın
   alanına yazma.
```

Yeni bir LLM oturumu açıldığında founder'ın tek yapması gereken:
"suderra/durum.json'u oku ve kaldığımız yerden devam et."

---

## durum.json Şeması

```json
{
  "son_guncelleme": "YYYY-MM-DD",
  "guncelleyen_agent": "Agent 11",

  "sirket": {
    "org_nr": null,
    "tescil_tarihi": null,
    "tescil_durumu": "NOT_STARTED | FILED | REGISTERED"
  },

  "belgeler": {
    "01-stiftelsesdokument": { "versiyon": "v1", "tarih": "YYYY-MM-DD", "imza": "DRAFT | SIGNED" },
    "02-vedtekter":          { "versiyon": "v1", "tarih": null, "imza": "DRAFT" },
    "03-sweat-equity-avtale":{ "versiyon": null, "tarih": null, "imza": null },
    "04-aksjonaer-avtale":   { "versiyon": null, "tarih": null, "imza": null },
    "05-holding-transfer-plan": { "versiyon": null, "tarih": null, "imza": null },
    "06-term-sheet-template":   { "versiyon": null, "tarih": null, "imza": "N/A" },
    "07-skattefunn-soknad":     { "versiyon": null, "tarih": null, "imza": null },
    "08-ip-politikasi":         { "versiyon": null, "tarih": null, "imza": null },
    "09-styrereglement":        { "versiyon": null, "tarih": null, "imza": null },
    "00-founder-ozet":          { "versiyon": null, "tarih": null, "imza": "N/A" },
    "opsiyonel-arbeidskontrakt": { "versiyon": null, "tarih": null, "imza": null },
    "opsiyonel-saas-sozlesme":   { "versiyon": null, "tarih": null, "imza": null },
    "opsiyonel-oppdragsavtale":  { "versiyon": null, "tarih": null, "imza": null }
  },

  "gate_sonuclari": {
    "faz2b_tutarlilik": { "verdikt": null, "tarih": null, "acik_cakismalar": [] },
    "faz5b_tutarlilik": { "verdikt": null, "tarih": null },
    "s2_00_5_preflight": { "verdikt": null, "skor": null, "tarih": null },
    "s2_17_outreach_uyum": { "verdikt": null, "tarih": null }
  },

  "cap_table": {
    "versiyon": "v1",
    "kaynak": "Agent 02",
    "ozet": "A:900 (founder) / B:50+50 (co-founder) / C:0 / D(ESOP):0"
  },

  "s2_durum": {
    "datasheet_versiyon": null,
    "outreach_log_yolu": "suderra/outreach-log.json",
    "aktif_yatirimcilar": [],
    "imzali_term_sheet": null,
    "data_room_tier_durumu": null
  },

  "faz7_kapanis_dongusu": {
    "aktif": false,
    "tur": null,
    "10_9_uc_ay_son_tarih": null
  },

  "acik_aksiyonlar": [
    { "sahip": "founder | Agent XX", "aksiyon": "", "son_tarih": null }
  ]
}
```

---

## Tutarsızlık Kuralları

| Tespit | Aksiyon |
|--------|---------|
| Belge X v2 ama onu referanslayan belge Y hâlâ v1'e göre | Agent 16'yı (tutarlılık) tetikle |
| Gate verdikti FAIL ama sonraki faz çalışmış görünüyor | DUR — founder'a eskalasyon |
| İmzalı belge üzerinde yeni taslak değişikliği | UYARI: imzalı belge değiştirilemez; v+1 taslağı + yeniden imza süreci gerekir |
| durum.json 30+ gün güncellenmemiş ve aktif outreach var | S2-08 mini-revalidation + S2-17 dalga kontrolü öner |

---

## Sahiplik

- Dosya yolu: `suderra/durum.json` (repo kökünde, belgelerin yanında)
- Şema değişikliği yalnız bu dosyada (S0) yapılır; agent'lar şemayı genişletemez.
- CEO Agent (01) her FAZ geçişinde durum.json'un güncel olduğunu doğrular;
  S1-Agent 22 (FAZ 7) kapanış döngüsü alanının tek yazarıdır.
