# Aktif Bağlam

**Son güncelleme:** 2026-07-22

## Mevcut Durum

Site çalışır ve yayında. Son commit `1495467 update info and skils` (2026-03-26).
Çalışma ağacı temiz, branch `main`.

Yerel sunucu bu oturumda `python3 -m http.server 8765` ile ayağa kaldırıldı —
http://localhost:8765

## Bu Oturumdaki Değişiklikler

- `.ai/` klasörü kuruldu: `rules.md`, `architecture.md`, `active-context.md`,
  `roadmap.md`, `story.md`. Proje daha önce dokümantasyonsuzdu; mevcut kod
  okunarak geriye dönük yazıldı.
- BankoAsist referans URL'i `ivr.ikbalperde.com/kiosk` → `pratikbilisim.com.tr`
  olarak değiştirildi. İki yerde geçiyordu: proje kartı (satır ~200) ve detay
  çekmecesi içeriği (satır ~554).
- Datalab Tıbbi Tahlil Laboratuvarı uygulaması altyapı referanslarına eklendi
  (`com.pratikbilisim.datalab` / App Store `6748526302`). İkon indirildi:
  `assets/appstore/6748526302.jpg`. Liste başlığı "Aktif Hastane Uygulamaları"
  → "Aktif Kurum Uygulamaları" yapıldı (laboratuvar hastane değil).
- BankoAsist (kiosk) projesi "ön sipariş alındı" durumundan "yayında" durumuna
  güncellendi, üç aşamalı kurum listesi eklendi. Aktif: Merkez Prime, Buhara,
  Hürrem Sultan, Çakırtepe. Kurulum: NEV, Büyük Anadolu Darıca, Moodist, Vatan.
  Ön sipariş: Ekol, Optimum, Acıbadem, Leton. Hem kart hem drawer detayı
  güncellendi.
- BankoAsist drawer detayına donanım iş ortakları maddesi eklendi (Sunmi,
  Unisoft, CCL; 9 adet Unisoft cihaz teslim edildi). Sadece drawer'da —
  kartta gösterilmiyor.
- Pavo POS bilgisi kendi maddesine ayrıldı: POS cihazı satış yetkisi + kiosk
  ile REST entegrasyonu. HBYS entegrasyonu maddesinden çıkarıldı.
- BankoAsist drawer detayına Mermaid `sequenceDiagram` eklendi: kiosk–POS
  ödeme akışının backend üzerinden yönetimi. Kaynak, kullanıcının paylaştığı
  `~/Desktop/pratik/pavo/images/StartPaymentDiagramNew.png` görseliydi; PNG
  gömmek yerine diyagram Mermaid olarak yeniden yazıldı.
  **Tarayıcıda render doğrulanmadı** — drawer açılıp kontrol edilmeli.
- BankoAsist kartına "Kapsanan Süreçler" maddesi eklendi. Proje yöneticiliği
  ayrı bir `Rol:` maddesi olarak değil, tanıtım paragrafının içinde anlatılıyor
  (kullanıcı tercihi). Drawer'da da süreç listesi ayrı madde oldu ve rol
  sıralaması proje yöneticiliği öne alınacak şekilde düzeltildi.
- Zaman çizelgesinde **sadece etiket ve süre metinleri** güncellendi: eksen
  sonu "Mar 2026" → "Tem 2026", başlıktaki toplam 7 yıl 6 ay → 7 yıl 10 ay,
  Pratik Bilişim 2 yıl 6 ay, Proje Yöneticisi rolü 1 yıl 3 ay, Techno Soft
  1 yıl 5 ay. Eksen geometrisi (`--total`, `--span`) değiştirilmedi —
  `styles.css` bu oturumda hiç değişmedi.
- Hiçbiri commit edilmedi.

## Bilinmesi Gerekenler

- Sitede build adımı yok — `index.html` düzenle, tarayıcıyı yenile.
- `file://` ile açma; inline script ES modülü olduğu için HTTP sunucusu şart.
- `main`'e push doğrudan canlıya çıkar (GitHub Pages).

- Bir referans URL genellikle hem kartta hem drawer detayında tekrar eder.
  Metin değişikliklerinde `grep` ile tüm geçişleri kontrol et.
- **Bilinen tutarsızlık:** Çevre Hastanesi, kart listesinde "sözleşmesi sonlanan"
  bölümüne taşınmış (commit `6404d63`) ama drawer kopyasında hâlâ aktif listede
  duruyor (`index.html` ~satır 792). Düzeltilmedi.
- App Store ikonu eklemek için:
  `curl -s "https://itunes.apple.com/lookup?id=<appId>&country=tr"` →
  `artworkUrl512` alanını `assets/appstore/<appId>.jpg` olarak indir.

## Sonraki Adımlar

Kullanıcıyla birlikte içerik düzenlemeleri sürüyor. Bekleyen commit var —
kullanıcı onaylayınca commit/push edilecek (push = canlıya çıkış).
