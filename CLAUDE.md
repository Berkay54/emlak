# Selvira Gayrimenkul (emlak konsept demosu)

DAB Labs portföyü için premium emlak ofisi konsept sitesi. Marka, fiyatlar, metrekareler ve çalışma saatleri **uydurma** (konsept); footer'da "Konsept çalışma" linkiyle dablabs.net'e backlink var. Kişiler arası eşitleme olmadığı için kalıcı bağlam bu dosyada.

## Konsept

- Sapanca ve Kartepe'de villa, müstakil ev ve daire satan premium emlak ofisi. Ofis: Kırkpınar, Sapanca (sokak/numara yok).
- Ana eylem her yerde aynı: **"Randevu al"** → `#randevu` formu (alıcı, satıcı, değerleme, kiralama tek formda).
- Marka adı "Selvira Gayrimenkul": web aramasında birebir eşleşen firma çıkmadı (`names.json`).

## Yapı

- Düz statik site, build yok: `index.html`, `credits.html`, `assets/`.
- Tasarım: **taste-skill 2.5** eklentisi (`/taste-skill:design-taste-frontend`). `assets/` klasörü eklentinin kitinin kopyası (`system.css`, `system.js`, `layout/`, `motion/`…); kit dosyaları elle düzenlenmez, sayfa CSS'i `index.html` içindeki ikinci `<style>`da.
- Deal (eklentinin dağıttığı, değiştirme): tür `service`, hero `split`, nav `nav-mega`, close `close-type`, footer `footer-dark`, ritim `dark-band` (#hizmetler), butonlar `arrow`, işaret `stack`, palet `offwhite-bottle-yellow` (şişe yeşili #0d2a1c + sarı #f6e016), font `source-serif` (Source Serif 4 + Libre Franklin).
- Bölümler: hero · #portfoy (6 ilan, 2 ekran) · #ilan (peek-list, oda oda Kırkpınar villası) · #hizmetler (koyu bant) · #sss · #surec (3 adım) · #randevu (form) · footer.
- Fotoğraflar `assets/img/<ad>-1600.webp` ve `-800.webp`: Openverse üzerinden Rawpixel ve StockSnap, hepsi CC0; liste `credits.html`. Unsplash arama ucu bot engeli verdiği için kullanılmadı.

## Yeniden tasarım (2026-11-09, sürüyor)

Kullanıcı tasarımı tamamen değiştirmek istedi; yukarıdaki "Deal" artık geçerli değil. Bölüm bölüm gidiliyor, ilk adım hero.

- Palet "göl taşı ve pirinç": kireçtaşı #f3efe8, orman kömürü #1b201d, pirinç #a97f4c / koyu zeminde #c9a678. Fontlar: Cormorant Garamond 500 (başlık) + Jost (metin). Vurgu kelimeleri italik değil, sadece pirinç renkte. İlk tercih Instrument Serif + Manrope idi, kullanıcı çok sevmedi ("kusacam"). Dört seçenekli karşılaştırmadan (klasik lüks / modern sans / editoryal / hafif geometrik) kullanıcı "A · Klasik lüks"ü seçti.
- Hero (`.hero.hv`): tam ekran arka plan videosu (Pexels 16673488, Bolu Gölcük, Kenan Turguç; göl kıyısında orman içinde ev, drone). Orijinal H.264 dosyalar değiştirilmeden: `assets/video/hero-1440.mp4` (geniş/yüksek DPI ekran) ve `hero-1080.mp4`, 11,9 sn döngü, poster `hero-poster.webp`. Yatayda aynalanıyor (ev sağa düşsün diye). İlk deneme Mixkit 720p idi, kullanıcı kalitesiz buldu: en az 1080p kullan. Oynatma JS ile: `prefers-reduced-motion`'da oynamaz, durdur/oynat düğmesi var, ekran dışındayken durur.
- Menü çubuğu hero'nun üstünde şeffaf (`.nav.is-clear`), hero geçince kitin opak çubuğuna döner.
- Kit tuzağı: `main > section > .wrap:not(.grid)` flex sütun yapar; hero'da grid kuralları işlemez, `margin-top:auto` ile hizalanır.
- Portföy (`#portfoy.pf`, bitti): eyebrow + italik pirinç vurgulu h2, solda büyük "Haftanın evi" ve sağda iki küçük kartla bento (yazı fotoğrafın üstünde), altında üç klasik kart (yazı fotoğrafın altında); "40+ ev" kapanış satırı kullanıcı isteğiyle kaldırıldı. Kartlar `.pcard`, `.pcard--over`. `data-ilan` taşıyan karta tıklanınca randevu formundaki "Hangi ev?" seçimi doluyor. Ortak parçalar: `.eyebrow`, `h2 em`, `[data-rv]` giriş efekti (bir kez, reduced-motion'da kapalı).
- Karar: yeniden tasarlanan bölümler kitin "tam 1 ya da 2 ekran" kuralına uymuyor, `height:auto` (mobil taşma hatası bu kuraldan çıkıyordu). consistency/check'teki screen-height uyarıları bu bölümler için beklenen davranış.
- Tam bölüm ekran görüntüsü için kit aracı yetmiyor (sadece ilk ekranı alır); scratchpad'de CDP ile `shoot.mjs` yazıldı.
- Ev turu (`#ilan.tour`, bitti): koyu bant (ground-inverse).
  - Yapı: başlık + künye (oda/ev/arsa/göle/fiyat), solda odalar arası geçişli büyük fotoğraf, sağda numaralı oda listesi (aktif odanın açıklaması açılır), "Bu evi yerinde görün" butonu.
  - Künyedeki rakamlar Jost: Google Fonts'taki Cormorant Garamond yalnızca eski stil rakam veriyor, lnum işe yaramıyor. Serif başlıklara rakam koyma.
  - Davranış: görünür olunca 6 sn'de bir otomatik ilerler (pirinç çizgi dolar), hover duraklatır, tıklama otomatiği kapatır, reduced-motion'da kapalı.
- Hizmetler (`#hizmetler.sv`, bitti): açık zemin.
  - Yapı: başlık, 21:9 sinema şeridinde video, altında dört numaralı hizmet sütunu (ücret altta, "Ücretsiz" pirinç renkte).
  - Video: kullanıcının verdiği dosya (`Downloads/Drone_filming_luxury_villa_interior_…_1080p.mp4`), `assets/video/hizmet-1080.mp4`, 10 sn, poster `hizmet-poster.webp`. Yalnızca ekrandayken yüklenip oynar; durdur düğmesi var; reduced-motion'da oynamaz.
  - Eski `assets/img/hizmet-*.webp` artık kullanılmıyor.
- SSS (`#sss.qa`, bitti): kum rengi bant (`--p-surface`).
  - Yapı: solda sabit (sticky) başlık ve "Sorunuzu danışmanımıza sorun" kartı, sağda `<details name="sss">` akordeon (aynı anda tek cevap açık; `::details-content` destekleyen tarayıcıda yumuşak açılır).
  - Akordeon `.faq` içinde değil, çünkü kitin system.js'i `.faq details`'i zorla açık tutuyor.
  - Sorular 6'ya çıktı: tapu harcı (%4, alıcı-satıcı %2'şer + döner sermaye) eklendi. Yabancıya satış cevabı yumuşatıldı (askeri/güvenlik bölgesi kontrolü).
- Süreç (`#surec.proc`, bitti): koyu bant, fotoğrafsız (eski s1-s3 fotoğrafları adımlarla örtüşmüyordu, artık kullanılmıyor).
  - Yapı: başlık + "Ücretsiz değerleme isteyin" butonu, üç adımı birleştiren pirinç ray (ekrana girince bir kez çizilir; ≤1023px'te sola dikey döner). Her adımda süre etiketi, açıklama ve "teslim ettiklerimiz" listesi.
- Form ön seçimi: `data-ilan` "Hangi ev?"i, `data-konu` "Ne için geliyorsunuz?"u doldurur; ilan kartı tıklanınca konu "Ev almak istiyorum"a döner.
- Ritim: hero koyu, portföy açık, tur koyu, hizmetler açık, SSS kum, süreç koyu.
- Sıradaki: randevu (açık olmalı), footer.

## Durum (2026-11-09 checkpoint)

- Sayfa yazıldı, tarayıcıda açılıyor. Kullanıcı henüz görsel geri bildirim vermedi.
- `consistency.mjs` ilk çalıştırmada **69 FAIL / 51 WARN**. Çoğu: section-height / one-section / section-air (bölümler tam 1 veya 2 ekran değil, özellikle 390 ve 768'de), container-edges, split-pair, copy-headings, contrast, photo-upscale, no-visual, empty-visual, spill, overlap-text. Henüz düzeltilmedi.
- impeccable hook: hero float karttaki yanıp sönen nokta kaldırıldı. Açık kalanlar: koyu zeminde radial-halo (muhtemelen kit CSS'i) ve iki "cramped-padding" (yer belirtilmedi).
- Form `mailto:randevu@selvira.example`'a gidiyor; yayına çıkarken Web3Forms'a bağlanmalı (dablabs.net'teki gibi).

## Sıradaki adımlar

1. Kullanıcının görsel geri bildirimini al.
2. Kontrolleri çalıştır ve FAIL'leri düzelt (eklenti `<skill>` yolu: `~/.claude/plugins/cache/taste-skill/taste-skill/2.5.0/skills/taste-skill`):
   `node <skill>/scripts/consistency.mjs index.html --widths 1440,1024,820,768,390 --rhythm-widths 1440,820,768,390 --profile .profile --page service --category "satılık villa ve göl evi" --primary "Randevu al"`
   `node <skill>/assets/layout/check.mjs --url index.html --profile .profile --sizes 1440x900,1024x768,820x1180,768x1024,390x844 --shots shots/layout`
3. Yayın: Vercel'e `emlak.dablabs.net` (dablabs CLAUDE.md'deki demo alt alan adı adımları), dablabs.net'e vaka sayfası ve çalışma kartı ekle.

## Yerelde açma

`python -m http.server 5180` sonra http://127.0.0.1:5180/ (dosyayı çift tıklayarak açma: fontlar/modüller yüklenmez).
