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
