# 🌱 Beslenenbahçe

<div align="center">

**Toprak & Gübre Algoritması**  
*Ankara Kent Bostanları için Organik Gübreleme Karar Destek Sistemi*

[![PWA](https://img.shields.io/badge/PWA-Çevrimdışı%20Çalışır-4a7c2f?style=flat-square&logo=pwa)](https://hekim05.github.io/Beslenenbahce)
[![HTML](https://img.shields.io/badge/Tek%20Dosya-HTML-orange?style=flat-square&logo=html5)](index.html)
[![License](https://img.shields.io/badge/Lisans-MIT-blue?style=flat-square)](LICENSE)

**[🚀 Canlıya Git](https://hekim05.github.io/Beslenenbahce)**

</div>

---

## 📌 Ne İşe Yarar?

Çankaya Belediyesi Kent Bostanları Programı kapsamında geliştirilen bu uygulama; hobist bahçecilerin ve kent tarımı koordinatörlerinin **organik gübre uygulamalarını bilimsel temelde planlamasını** sağlar.

- Hangi gübreden kaç gram atacağını söyler
- Her uygulamadan sonra "sezon sonuna kadar ne eksik kaldı?" gösterir
- Ankara'nın alkalin kireçli toprak koşullarına göre kalibre edilmiştir
- Sunucu yok, hesap yok, internet bağlantısı gerekmez

---

## 📱 Ekranlar

| Özet & Plan | Besin Durumu | Kümülatif Takip |
|:-----------:|:------------:|:----------------:|
| Sonraki 3 uygulama | N/P/K kalan ihtiyaç | Sezon toplamı |

---

## 🧪 Algoritma — 6 Katmanlı Besin Hesabı

Her gübre uygulamasında bitkiye gerçekte ulaşan besin miktarı:

```
Verilen gübre (kg/m²)
  × Besin içeriği       (g/kg)
  × PAN                 İlk sezon yarayışlılığı — gübreye özgü
  × SOIL_RET            Toprak tutma kapasitesi — toprak tipine göre
  × phFactor            pH bağlanma kaybı — Ankara pH 7.5–8.2
  × PHASE_LOSS          Faz bazlı kayıp — dikim öncesi en yüksek
  × LEACH_FACTOR        Yıkanma — Ankara ~400 mm yağış, düşük
  × IMMOB_FACTOR        Mikroorganizma immobilizasyonu
─────────────────────────────────────────────────────
= Bitkiye ulaşan besin (g/m²)
```

### Ankara Kalibrasyonu

> **Referans:** Kuru büyükbaş gübresi, kök başına 200 gr, 4 büyüme fazında uygulandığında Ankara koşullarında N açığı gözlemlenmemektedir. *(Çankaya Belediyesi Kent Bostanları, 15 sezon saha verisi)*

Bu referans noktasına göre:

| Parametre | Değer | Açıklama |
|-----------|-------|----------|
| `PAN` büyükbaş | 0.70 | Ankara sıcak yaz → hızlı mineralizasyon |
| `SOIL_RET.N` tinli | 0.70 | Az yağış, OM birikimi → N tutma iyi |
| `LEACH.N` tinli | 0.92 | Düşük yıkanma — ~400 mm/yıl |

---

## 🌿 Desteklenen Bitkiler

| Bitki | N g/m² | P g/m² | K g/m² |
|-------|:------:|:------:|:------:|
| Domates | 20 | 8 | 28 |
| Biber | 15 | 7 | 22 |
| Salatalık | 18 | 8 | 26 |
| Patlıcan | 16 | 7 | 20 |
| Kabak | 14 | 6 | 18 |
| Marul/Yapraklı | 12 | 5 | 14 |
| Fasulye | 8 | 6 | 14 |
| Havuç/Kök | 10 | 6 | 16 |
| Lahana/Brassica | 18 | 8 | 20 |
| Soğan/Sarımsak | 12 | 6 | 18 |
| **Karışık (ortalama)** | **16** | **7** | **22** |

Karışık profilde bitki sayıları girilir → ağırlıklı ortalama hesaplanır.

---

## 🧴 Gübre Veritabanı

| Gübre | N g/kg | PAN | Önerilen Doz |
|-------|:------:|:---:|:------------:|
| 🐄 Büyükbaş (kuru) | 20 | 0.70 | 1–3 kg/m² |
| 🐔 Kanatlı (toz) | 40 | 0.55 | 0.5–1.5 kg/m² |
| 🐑 Koyun/Keçi | 23 | 0.45 | 1–3 kg/m² |
| ♻️ Kompost (olgun) | 12 | 0.18 | 2–6 kg/m² |
| 🪱 Solucan Gübresi | 16 | 0.60 | 0.3–1 kg/m² |
| 🧬 Bokashi/EM | 15 | 0.50 | 0.5–2 kg/m² |
| 🔴 Hümik & Fulvik Asit | — | — | 0.05–0.2 kg/m² |
| 🪣 Toz Kükürt | — | — | 0.1–0.3 kg/m² |
| 💧 Kül Suyu (Odun Külü) | — | — | 0.1–0.5 kg/m² |

---

## 📅 Büyüme Fazları & Kayıp Oranları

| Faz | N Ulaşma | K Ulaşma | Ne Zaman |
|-----|:--------:|:--------:|----------|
| Dikim Öncesi | %55 | %60 | Dikimden 4–6 hafta önce |
| Erken Büyüme | %75 | %72 | Fide tutundu, kök gelişimi |
| Çiçeklenme | %85 | %85 | Aktif çekim, düşük kayıp |
| Meyve Dönemi | %90 | %90 | Hemen alır, en verimli faz |

---

## ⚠️ Ankara Toprağı Özel Uyarıları

| Element | Sorun | Öneri |
|---------|-------|-------|
| **P** | Kireçle bağlanır → %10–30 bitkiye ulaşır | Humik asit ile birlikte ver |
| **Ca** | Doğal olarak bol | Ek uygulama genellikle gereksiz |
| **Mg** | Kireçli toprakta yeterli | Kloroz görülmezse ekleme yapma |
| **S** | Toz kükürt pH düşürür | Besin kaynağı değil, pH düzenleyici |
| **N** | Yıkanır, uçar | Her fazda yeniden ver |
| **K** | Yıkanır | Sezon boyunca bölünmüş uygulama |

---

## 🚀 Kurulum

### Yöntem 1 — Doğrudan Kullan
```
https://hekim05.github.io/Beslenenbahce
```

### Yöntem 2 — Telefona Yükle (PWA)
1. Yukarıdaki adresi Chrome'da aç
2. Adres çubuğu yanındaki **"Yükle"** ikonuna bas
3. Ana ekrana eklenir, çevrimdışı çalışır

### Yöntem 3 — Kendi Sunucuna Kur
```bash
git clone https://github.com/Hekim05/Beslenenbahce.git
cd Beslenenbahce
# Herhangi bir web sunucusuyla yayınla:
python3 -m http.server 8080
# → http://localhost:8080
```

### Yöntem 4 — Sadece Dosyayı Aç
`index.html` dosyasını indirip doğrudan tarayıcıda aç. Sunucu gerekmez.

---

## 📁 Dosya Yapısı

```
Beslenenbahce/
├── index.html        ← Tüm uygulama (tek dosya, ~3000 satır)
├── manifest.json     ← PWA tanım dosyası
├── sw.js             ← Service worker (çevrimdışı destek)
├── icon-192.png      ← PWA ikonu
├── icon-512.png      ← PWA ikonu
└── README.md         ← Bu dosya
```

> **Not:** Tüm uygulama mantığı, veritabanı, CSS ve HTML tek bir `index.html` dosyasındadır. Bağımlılık yok, build adımı yok.

---

## 💾 Veri Saklama

- Tüm veriler **tarayıcının LocalStorage**'ında saklanır
- Sunucuya hiçbir veri gönderilmez
- Geçmiş kayıtlar, tarayıcı temizlenmediği sürece kalır
- Yedek almak için: Geçmiş sekmesi → Dışa Aktar *(geliştirme aşamasında)*

---

## 📚 Akademik Kaynaklar

- Brady & Weil (2010) — *The Nature and Properties of Soils* — toprak tutma oranları
- Havlin et al. (2005) — *Soil Fertility and Fertilizers* — faz bazlı kayıp katsayıları
- Möller (2009), Eghball (2002) — organik gübreden K yarayışlılığı
- UF/IFAS Extension, Yara, UC IPM, Haifa Group — bitki besin ihtiyaçları
- Ohioline OSU (2016) — PAN (Plant Available Nitrogen) katsayıları
- Mengel & Kirkby (2001) — toprak bazlı yıkanma faktörleri

---

## 🔄 Sürüm Geçmişi

### v17 — Haziran 2026 *(güncel)*
- ✅ 6 katmanlı besin hesabı motoru (faz + yıkanma + immobilizasyon)
- ✅ "Kalan ihtiyaç" modeli — %200-600 fazla sorunu çözüldü
- ✅ Ankara kalibrasyonu (200 gr/kök büyükbaş referansı)
- ✅ Özet + Ayrıntı aç/kapat yapısı
- ✅ Sonraki 3 ardışık uygulama planı (kompakt tablo)
- ✅ Parsel besin ihtiyacı paneli

### v16
- Karışık bitki profili, ağırlıklı ortalama
- Sezon ilerlemesi ve split uygulama takvimi

### v1–v15
- Temel algoritma, gübre veritabanı, kursiyer/uzman modu

---

## 👤 Geliştirici

**Sertaç Hekim**  
Ziraat Mühendisi · Çankaya Belediyesi Kent Tarım Koordinatörü  

[![GitHub](https://img.shields.io/badge/GitHub-Hekim05-black?style=flat-square&logo=github)](https://github.com/Hekim05)

---

## 

