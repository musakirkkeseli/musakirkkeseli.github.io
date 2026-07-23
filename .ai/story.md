# Proje Günlüğü

## 2026-07-23 — BankoAsist'e rol ve süreç kapsamı eklendi

Karta **Kapsanan Süreçler** maddesi girdi: muayene dosyası oluşturma ve ödeme,
kontrol muayenesi oluşturma, özel sağlık sigortası provizyon işlemleri,
anlaşmalı kurumlara göre indirim tanımlama, tahlil/tetkik ödeme işlemleri.

Proje yöneticiliği önce ayrı bir `Rol:` maddesi olarak eklendi, sonra kullanıcı
tercihiyle tanıtım paragrafının içine taşındı — etiketli bir alan yerine
anlatının parçası olarak. Bu yüzden sitede hâlâ `Rol:` gibi bir etiket örüntüsü
yok; kartlar serbest metin + maddeler biçiminde kalıyor.

Drawer'da proje yöneticiliği zaten yazılıydı ama "Flutter geliştirme süreçlerini
ve proje yöneticiliğini" sırasındaydı; sıra ters çevrildi, çünkü öne çıkan rol
proje yöneticiliği. Süreç listesi orada da ayrı bir madde olarak eklendi.

`Rol:` etiketi şu an yalnızca bu kartta var. Diğer projelere de yayılırsa
tutarlı bir örüntü olur; şimdilik tek örnek.

## 2026-07-23 — Zaman çizelgesi tarihleri güncellendi

Eksen sonu Mar 2026'da kalmıştı; Pratik Bilişim ve Techno Soft'ta çalışma
sürdüğü için Tem 2026 yapıldı.

İlk denemede ekseni geometrik olarak da uzattım (`--total` 112 → 124, devam
eden işlerin `--span` değerleri). **Kullanıcı bunu geri aldırdı** — çizelgenin
fiziksel uzunluğu bilgi taşımıyor, sadece etiketin doğru olması yeterliymiş.
`styles.css` geri alındı, `--span` değerleri eski hâline döndü.

**Ders:** Bu çizelgede tarih güncellemesi = etiket güncellemesi. Ekseni
uzatmaya kalkma; yalnızca yeni bir kayıt eklenirken geometriye dokun.

Kalan (istenen) değişiklikler:
- Eksen sonu etiketi "Mar 2026" → "Tem 2026"
- Süre metinleri: toplam 7 yıl 10 ay, Pratik Bilişim 2 yıl 6 ay, Proje
  Yöneticisi rolü 1 yıl 3 ay, Techno Soft 1 yıl 5 ay

Referans olarak ölçek: eksen doğrusal değil — 2019–2024 ~10 birim/yıl,
2024 sonrası ~28 birim/yıl.

## 2026-07-22 — BankoAsist artık yayında

Kiosk projesinin durumu "test tamamlandı, ön sipariş alındı"dan "yayında ve
aktif kullanımda"ya geçti.

- **Aktif kullanımda:** Merkez Prime, Buhara, Hürrem Sultan, Çakırtepe
- **Kurulum aşamasında:** NEV, Büyük Anadolu Darıca, Moodist, Vatan
- **Ön sipariş aşamasında:** Ekol, Optimum, Acıbadem, Leton

Kart özetindeki tek satırlık "ön sipariş" ifadesi, satış hunisini yansıtan
üç aşamalı bir listeye dönüştürüldü; drawer detayı da aynı üç aşamayı
maddeler halinde tekrarlıyor.

Eski ön sipariş listesindeki Lokman Hekim Hastanesi yeni aşamaların hiçbirinde
geçmiyor. Kullanıcı doğruladı: kiosk için geliştirme yapılmış ancak hastane
projeyi kendi imkanlarıyla sürdürme kararı almış. Kiosk metninden çıkarıldı.
(Lokman Hekim'in **mobil uygulama** kaydı ayrı bir iş; altyapı listesinde
duruyor, dokunulmadı.)

Ayrıca donanım tarafı eklendi: Sunmi, Unisoft ve CCL firmalarıyla tedarik ve
uyumluluk süreçleri; 9 adet Unisoft cihaz sahada. Bu madde yalnızca drawer
detayına kondu — kart özeti kurum listeleriyle zaten dolu, donanım tedariki
detay seviyesinde bir bilgi.

**Teknik yapı diyagramı eklendi.** Kullanıcı kiosk–POS ödeme akışını gösteren
bir PNG paylaştı. Görsel zaten Mermaid ile üretilmişti (metinlerde kaçmamış
`\n` kalıntıları görünüyordu), sitede de Mermaid kurulu olduğu için PNG'yi
`assets/` altına koymak yerine diyagram `sequenceDiagram` olarak yeniden
yazıldı. Böylece koyu temaya uyuyor, metin seçilebilir/aranabilir kalıyor ve
ileride düzenlemesi kolay oluyor.

Drawer açılışında `mermaid.run()` zaten çağrılıyor, ek JS gerekmedi.
`.mermaid` üzerinde `overflow-x: auto` olduğu için geniş sequence diagram
kendi içinde kayıyor.

Pavo POS da kendi maddesine ayrıldı. Önceden "Pavo POS altyapılarıyla uyumlu"
şeklinde HBYS entegrasyonu cümlesinin kuyruğundaydı; oysa iki ayrı kazanım
var — POS cihazı **satış yetkisi** ve kiosk ile kurulan **REST entegrasyonu**.
Yetki tarafı ticari bir kazanım olduğu için entegrasyon detayının içinde
kaybolmaması gerekiyordu.

## 2026-07-22 — Datalab uygulaması referanslara eklendi

Datalab Tıbbi Tahlil Laboratuvarı uygulaması (`com.pratikbilisim.datalab`,
App Store `6748526302`) altyapı projesinin aktif uygulama listesine eklendi.
İkon `itunes.apple.com/lookup` üzerinden `assets/appstore/6748526302.jpg`
olarak indirildi — mevcut konvansiyona uyuyor.

**Karar:** Liste başlığı "Aktif Hastane Uygulamaları" → "Aktif Kurum Uygulamaları"
olarak değiştirildi. Datalab bir laboratuvar; aynı altyapıyı kullanıyor ama
hastane değil. Başlığı genişletmek, uygulamayı ayrı bir listeye ayırmaktan
daha sade bir çözümdü.

Bu sırada fark edilen tutarsızlık: Çevre Hastanesi kart listesinde pasife
alınmış ama drawer kopyasında hâlâ aktif görünüyor. Kullanıcı istemediği için
dokunulmadı, `active-context.md`'ye not düşüldü.

## 2026-07-22 — BankoAsist referans URL'i değişti

`ivr.ikbalperde.com/kiosk` yerine `https://pratikbilisim.com.tr` kondu. Eski adres
bir müşteri alt alanıydı; kurumsal siteye yönlendirildi.

Not: URL hem proje kartında hem de drawer detay bölümünde ayrı ayrı yazılıydı —
detay içerikleri DOM'da kopya olarak durduğu için bu tekrar yapısal. Metin
değiştirirken tek geçişe güvenme.

## 2026-07-22 — `.ai/` dokümantasyonu kuruldu

Proje bugüne kadar dokümantasyonsuz ilerlemişti. Global CLAUDE.md `.ai/rules.md`'yi
tek doğruluk kaynağı olarak işaret ettiği için klasör oluşturuldu ve içerik mevcut
kod okunarak geriye dönük yazıldı.

Kayda değer bulgular:
- Zaman çizelgesi tamamen CSS custom property'leriyle çalışıyor, JS içermiyor.
  Konumlar (`--start` / `--span`) elle hesaplanmış — yeni iş eklerken dikkat gerektiren
  tek yer burası.
- İkon sistemi konvansiyon üzerine kurulu: `data-app-id` → `assets/appstore/<id>.jpg`.
- Detay içerikleri DOM'da gizli tutulup drawer'a klonlanıyor; şablon string yerine
  bu yaklaşım seçilmiş, içerik böylece aranabilir kalıyor.

Kod değişikliği yapılmadı.

## Öncesi (git geçmişinden)

- **2026-03-26** — `1495467` bilgi ve beceri güncellemesi.
- **2026-03-25** — `b313477` zaman çizelgesi yönü değiştirildi; `c9ec6de` içerik düzenlemeleri.
- **Daha önce** — `6404d63` çevre hastanesi uygulaması pasif uygulamalara taşındı;
  `d38a159` logo hatası düzeltildi.
- App Store ikonları bir noktada uzak API çağrısından yerel asset'lere taşındı
  (kod yorumu: "GitHub Pages uyumlu").
