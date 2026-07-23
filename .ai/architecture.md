# Mimari

## Genel Yaklaşım

Build adımı olmayan, tek sayfalık statik site. Üç dosya taşıyor: `index.html`
(yapı + davranış), `styles.css` (sunum), `assets/` (görseller). Sunucu tarafı,
veri katmanı, durum yönetimi yok — içerik doğrudan HTML'e gömülü.

Bu tercih bilinçli: CV içeriği yılda birkaç kez değişiyor, bir build zinciri
bakım maliyetini içerikten daha pahalı hale getirirdi.

## Sayfa Yapısı (`index.html`)

```
<header class="hero">        Ad, ünvan, özet, iletişim listesi
<main class="container layout">
  <section class="experience-section">   Zaman çizelgesi
  <section>  Eğitim
  <section>  Beceriler
  <section>  Lisanslar ve Sertifikalar
  <section>  Diller
  <section>  Projeler          ← .card article'ları
  <div class="solution-details-store">   Gizli detay bölümleri
<div id="detailBackdrop">     Drawer arka planı
<aside id="detailDrawer">     Sağdan açılan detay paneli
<script type="module">        Tüm davranış
```

## Üç Davranışsal Sistem

### 1. Zaman çizelgesi — saf CSS
JS yok. Konumlandırma tamamen inline custom property'lerle yapılır:
`--start` (eksende başlangıç), `--span` (süre). CSS bunları yüzdeye çevirip
mutlak konumlandırır. `side-left`/`side-right` eksenin yanını, `lane-a`/`lane-b`
çakışan dönemler için şeridi belirler.

**Sonuç:** Yeni bir iş eklemek sadece HTML düzenlemesi; hesap manuel.

### 2. İkon yükleyici — konvansiyon tabanlı
`loadProjectIcons()` sayfa yüklendiğinde iki geçiş yapar:
1. `.card[data-app-logo]` ve `.card[data-app-id]` → başlık ikonu
2. `.card[data-is-framework] li[data-app-id]` → alt uygulama ikonları

Yol kuralı: `assets/appstore/${appId}.jpg`. Özel logo varsa `data-app-logo`
onu ezer. `img.onerror` gradyanlı bir inline SVG placeholder'a düşer, böylece
eksik dosya sayfayı bozmaz.

Eskiden iTunes Lookup API'sinden çekiliyordu; GitHub Pages'te ağ bağımlılığı
ve rate-limit sorunu yaratmasın diye yerel asset'e taşındı.

### 3. Detay çekmecesi — klonlama
Uzun anlatımlar `.solution-details-store` içinde DOM'da hazır ama gizli durur.
Butona basınca ilgili `#detail-*` bölümü drawer'a klonlanır, `aria-hidden`
ve `body.drawer-open` sınıfı güncellenir. Kapanışta içerik temizlenir.

**Neden klonlama:** İçerik HTML'de kaldığı için arama motoru ve Ctrl+F
erişebilir; ayrıca JS içinde şablon string tutmak gerekmiyor.

## Stil Sistemi (`styles.css`)

`:root` içinde tanımlı custom property'ler üzerine kurulu koyu tema. Kaskad
sırası: değişkenler → temel eleman stilleri → bileşen sınıfları → responsive
`@media` blokları. Tek kırılma noktası `min-width: 900px` civarında.

## Harici Bağımlılık

Tek bir tane: Mermaid 11, jsDelivr'dan ESM olarak. `startOnLoad: false` ile
kurulur, koyu tema, `securityLevel: "loose"`. Mimari diyagramlarını render eder.
