# Proje Kuralları — Tek Doğruluk Kaynağı

## Proje Nedir

Musa KIRKKESELİ'nin kişisel özgeçmiş (CV) web sitesi. Türkçe, tek sayfa,
tamamen statik. GitHub Pages üzerinden `musakirkkeseli.github.io` adresinde
yayınlanıyor (remote: `musakirkkeseli/musakirkkeseli.github.io`, branch `main`).

## Teknoloji Yığını

- **HTML5** — `index.html`, tek dosya, tüm içerik + inline `<script type="module">`
- **CSS3** — `styles.css`, custom property tabanlı koyu tema, framework yok
- **Mermaid 11** — CDN'den ESM olarak import, mimari diyagramları için
- **Build yok, bağımlılık yok, `package.json` yok.** Dosyalar doğrudan servis edilir.

## Yerel Çalıştırma

```bash
cd /Users/musakirkkeseli/Desktop/person/cv
python3 -m http.server 8765
# http://localhost:8765
```

`file://` ile açma — inline script `type="module"` olduğu için CORS'a takılır.
Mutlaka HTTP sunucusu üzerinden aç.

## Dizin Yapısı

```
index.html            # Tüm sayfa: hero, deneyim, eğitim, beceriler,
                      # sertifikalar, diller, projeler, gizli detay bölümleri
styles.css            # Tüm stiller
assets/
  appstore/<appId>.jpg  # App Store ikonları, dosya adı = numeric app id
  *.png | *.jpeg        # Özel logolar (App Store'da olmayan projeler)
.ai/                  # Bu klasör — proje hafızası
```

## Kodlama Standartları

- **Dil:** Tüm kullanıcıya görünen metin Türkçe. Kod yorumları da Türkçe.
- **Girinti:** HTML ve CSS'te 4 boşluk.
- **CSS:** Yeni renk/ölçü eklerken `:root` içindeki custom property'leri kullan,
  sabit değer gömme. Yeni bir tema değeri gerekiyorsa önce `:root`'a ekle.
- **JS:** ES modülü, `const` + arrow function. Framework ekleme.
- **Harici bağımlılık:** Mermaid dışında CDN kaynağı ekleme. Yeni bir kütüphane
  gerekiyorsa önce gerekçesini konuş.

## Alan-Özel Kurallar

### Zaman çizelgesi (`.experience-axis`)
Her `.timeline-item` konumunu inline CSS değişkenleriyle alır:
`style="--start: 0; --span: 28;"` — birim, eksen boyunca yüzdesel konum.
Sınıflar: `side-left` / `side-right` (eksenin hangi yanı), `lane-a` / `lane-b`
(çakışmayı önlemek için şerit), `align-top` (dikey hizalama).
Yıl etiketleri `.axis-year` + `style="--pos: N;"` ile yerleşir.
Yeni iş eklerken `--start` / `--span` değerlerini mevcut yıl etiketlerine göre
hesapla ve çakışan kayıtları farklı `lane`'e al.

**Ölçek doğrusal değil:** 2019–2024 arası ~10 birim/yıl, 2024 sonrası ~28
birim/yıl (≈2,33 birim/ay).

**Tarih güncellerken ekseni uzatma.** Eksen sonu yeni bir aya taşınacaksa
yalnızca `.axis-end` etiketini ve süre metinlerini değiştir; `styles.css`
içindeki `--total` ile devam eden işlerin `--span` değerlerine dokunma.
Çizelgenin fiziksel uzunluğu bilgi taşımıyor. Geometriye yalnızca yeni bir
kayıt eklerken müdahale et.

`h2` başlığındaki toplam süre ve kart içi süre metinleri elle yazılıdır —
tarih değişince onları yeniden hesapla.

### Proje ikonları
Kart `data-app-id="<numeric>"` taşıyorsa ikon `assets/appstore/<id>.jpg`
yolundan otomatik yüklenir. App Store'da olmayan projeler için
`data-app-logo="assets/<dosya>"` kullanılır. Yükleme başarısız olursa inline
SVG placeholder devreye girer — bu davranışı bozma.
Çerçeve projesi (`data-is-framework`) içindeki `li[data-app-id]` öğeleri de
aynı mantıkla ikon alır.

### Detay çekmecesi (drawer)
Uzun proje açıklamaları `.solution-details-store` içinde gizli `<section id="detail-*">`
olarak durur. `<button class="detail-button" data-detail-id="detail-*">` bunları
sağdan açılan drawer'a klonlar. Yeni detay eklerken bu iki parçayı birlikte ekle.

## Yayınlama

`main` branch'e push = canlıya çıkış (GitHub Pages). Push işlemini kullanıcı
onaylamadan yapma.
