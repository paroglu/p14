# PAROGLU MEDIA V14 — BEYOND THE FRAME
## Cinematic Premium Experience | UX, Visual Direction, Storyboard & Non-Destructive Development Specification
**Tarih:** 3 Kasım 2026  
**Repo:** https://github.com/paroglu/paroglumedia  
**Üretim alan adı:** https://paroglumedia.com/  
**Durum:** Tasarım/geliştirme spesifikasyonu. Mevcut site veya depoda değişiklik yapılmadı.

## 1. Ürün hedefi
ParogluMedia, işi sadece göstermeyen; prodüksiyon dünyasını hissettiren, hızlı, erişilebilir ve satış odaklı bir kreatif stüdyo portföyüne dönüşür.

**Temel mesaj:** “Görünen değil, hatırlanan işler.”  
**Alt mesaj:** “Karelerin ötesinde hikâyeler üretiyorum.”  
**Birincil CTA:** “Projeleri Keşfet” → `#selected-work`  
**İkincil CTA:** “Proje Konuşalım” → mevcut `teklif-al.html`  
**Video CTA:** “Showreel’i İzle” → erişilebilir modal / on-demand video.

Kişisel ton korunur: “üretiyorum / yönetiyorum”. Site bir kolektif ajansmış gibi hayali ekip, müşteri ve rakam göstermez. Gerçek iş arşivinin hak sahipliği, izin ve rol bilgileri net verilir.

## 2. Doğrulanmış mevcut durum
GitHub ana dalında HTML/CSS/vanilla JS tabanlı çok sayfalı yapı gözlemlendi. Başlıca dosyalar:
- `index.html` ve `styles.css` — ana sayfa/görsel sistem.
- `app.js` — etkileşimler, sayfa akışı.
- `motion-v12.css`, `motion-v12.js` — intro, mask typography, sayfa/geçiş animasyonları; `prefers-reduced-motion` destek notu.
- `backend-config.js`, `data-store.js` — Supabase REST bağlantısı; `window.PMData` altında `content()`, `projects()`, `brands()`, `assistant()`, `submitBrief()`.
- `admin-panel.html`, `admin-panel.js`, `admin.css` ve diğer yönetim paneli dosyaları.
- `teklif-al.html`, `isler.html`, `hizmetler.html`, `fotograf.html`, `drone.html`, `tasarim.html`, spor/konser ayrıntı sayfaları.
- Gerçek medya: `ack-bicak-preview.mp4`, `ack-bicak-poster.jpg`, `concert-sefo-poster.jpg`, `cover-karabuk.jpg`, `cover-drone.jpg`, vb.

V13 değişiklik notu: CMS'deki 'featured' projeler ana sayfada öncelikli; brief Supabase'e kaydedilip WhatsApp/e-posta akışına gidiyor; 3 neon noktalı komut menüsü; mevcut SEO ve 404 düzenlemeleri var.

**Uyarı:** Canlı site otomatik erişimde açılamadı. Repo ve belgeleri üzerinden mimari analizi yapıldı. GitHub kaynakları tüm davranışların tarayıcıda doğrulandığı anlamına gelmez.

## 3. Tasarım sistemi

| Token | Değer | Kullanım |
|---|---|---|
| `--bg` | `#08070D` | Ana arka plan |
| `--surface` | `#14101D` | Paneller |
| `--violet` | `#9D56E8` | İmza vurgu |
| `--violet-soft` | `#BE8BFF` | Işık ve hover |
| `--cream` | `#F6F3F8` | Ana tipografi |
| `--muted` | `#A49EAE` | İkincil tipografi |
| `--line` | `rgba(255,255,255,.12)` | İnce ayırıcılar |

Tipografi: Projede zaten lisanslı Gotham/Nexa varsa kullan; yoksa ticari kullanım lisansı uygun alternatif ile sistem fontu fallback. Başlıklar 72–120px desktop (clamp), 40–56px mobil. Body 16–18px. 12 kolon masaüstü grid, max-width ~1440px, sayfa padding desktop 48–72px, mobil 20–24px, sections 120–160px desktop / 72–96px mobile. Border-radius poster 16px, kart 20px. Gece siyahı + kontrollü mor. Glow en fazla belirli odaklarda; bütün sayfaya neon/blur uygulanmaz.

## 4. Bilgi mimarisi — mevcut URL'ler korunur
| Yeni menü etiketi | Hedef | Durum |
|---|---|---|
| Ana Sayfa | `/` | Ana sayfa yenilenir |
| İşler | `isler.html` | Korunur |
| Hizmetler | `hizmetler.html` | Korunur |
| Hakkımda | `hakkimda.html` | Korunur |
| Proje Konuşalım | `teklif-al.html` | Korunur |
| İletişim | `iletisim.html` | Korunur |

Konser, spor, fotoğraf, drone ve tasarım sayfaları da korunur. Yeni URL gerektiğinde eski bağlantılara yönlendirme + canonical uygulanır.

## 5. Ana sayfa: bölüm bölüm tasarım

### 00 — Header (sabit, 72–82px)
Sol: logo. Orta: İşler / Hizmetler / Hakkımda. Sağ: açık mor vurgu CTA “Proje Konuşalım”. İlk ekranda şeffaf, scroll sonrasında koyu cam yüzey + 1px border. Mobil: logo, CTA, menü; tam ekran açılır menü ve Escape desteği. V13 komut menüsü kaldırılmayacak; yeni navigasyonda çakışma testi yapılacak.

### 01 — Hero / Opening frame
- Yükseklik: `min-height: 100svh` (mobilde dinamik viewport).
- Arka plan: kendi çekimlerinden 8–12 saniyelik sessiz, döngüye giren, poster görselli ve mobilde koşullu oynayan sinematik showreel; doğrudan otomatik ses yok.
- Koyu `linear-gradient` overlay; ana başlık sol-alt/merkez sol. H1: “Görünen değil, / hatırlanan işler.”
- Eyebrow: `CREATIVE PRODUCTION / PHOTO / DESIGN / 2026`.
- Açıklama: “Markalar, sahneler ve şehirler için güçlü görsel hikâyeler.”
- CTA 1: “Projeleri Keşfet” (`#selected-work`), CTA 2: “Proje Konuşalım” (`teklif-al.html`); showreel oynatma kontrolü.
- Sağ alt köşede `SCROLL TO EXPLORE` + sakin animasyonlu çizgi; sol altta kısa lokasyon bilgisi.
- İlk anlamlı içerik animasyon beklemeden görünür olmalı.

### 02 — Manifesto / İmza metni
Karanlık zemin, dev tipografi: “Her marka bir hikâye. Her hikâye bir dünya.” Kelimeler scroll ile harf harf değil, satır maskesiyle görünür. Alt bölümde sade açıklama; gerçek içerik, görselin önüne geçmeyecek.

### 03 — Selected Work / 4 ana dünya
Başlık: “Dört farklı dünya. Tek bir yaratıcı bakış.”
- Film & Brand: `ack-bicak-poster.jpg` + tam filme geçiş.
- Live & Concert: `concert-sefo-poster.jpg` / fotoğraf galeri.
- Sport & Identity: `cover-karabuk.jpg` / kulüp projeleri.
- Aerial & Places: `cover-drone.jpg` / havadan çekimler.
Desktop: 2×2 asimetrik grid, büyük yatay/portre kartlar. Mobil: tek sütun, tamamen normal scroll. Hover: görsel scale 1 → 1.045, başlık 10px hareket, “Projeyi Gör ↗” ortaya çıkar; klavyede focus eşdeğeri. Video lightbox'ta on demand yüklenir.
Dinamik CMS önceliği korunur: `PMData.projects()` sonuçlarından `featured` filtresi, mevcut V13 algoritması referans alınarak bir adaptörle yeni UI'a aktarılır. Sabit örnek içerik yalnızca network/sorgu başarısızsa kullanılacak fallback.

### 04 — Showreel / The film
16:9 geniş film alanı; mümkünse `ack-bicak-preview.mp4` veya yeni 45–60 sn özel showreel. Önizlemede oynat/autoplay koşullu, tam video tıkla açılır. Video bitince isteğe bağlı sonraki proje önerisi; zorunlu yönlendirme yok.

### 05 — Services / Yetkinlikler
Büyük numaralı 5 satır: `01 Video & Reels`, `02 Fotoğraf`, `03 Grafik Tasarım`, `04 Sosyal Medya`, `05 Drone`. Hover/focus ile küçük ilgili görsel önizleme; mobilde görsel her satırın altında. Satırlar ilgili mevcut sayfalara yönlendirir.

### 06 — Process / Perde arkası
`01 Keşif → 02 Fikir → 03 Prodüksiyon → 04 Post-Prodüksiyon → 05 Teslim` şeklinde 5 aşamalı yatay film kareleri. Mobilde dikey timeline. Her aşamaya 1 cümle açıklama. Ağır 3D zorunlu değil.

### 07 — Trust / Referanslar
Dinamik marka logoları ya da izinli metin adları. Gerçek, izinli çalışmalar ile kişisel/ajans işi katkı rolleri net gösterilecek. Hakkında kanıt sunulamayan “500+ proje”, müşteri kazanımı gibi rakamlar pazarlama vaadine dönüşmeyecek. CMS `brands()` dinamiği korunur.

### 08 — About / Signature
Mevcut neon gözlüklü imza görseli (`paroglu-neon-glasses.png`) premium editorial portreye dönüşür. “Fikirden kadraja, tek bir yaratıcı çizgi.” kopyası korunabilir. CTA → `hakkimda.html`.

### 09 — Conversion / Final frame
Tüm ekran bölüm: “Bir sonraki hikâyen, birlikte başlasın.” İki açık eylem: “Proje Konuşalım” → `teklif-al.html`, “WhatsApp'tan Yaz” → mevcut bağlantı. Footer'da gerçek iletişim, lokasyon, sosyal platformlar ve yasal bağlantılar.

## 6. İlk giriş ve animasyon storyboard'u
Bu süreler **uygulama hedefleridir**; kullanıcının cihazına ve `prefers-reduced-motion` ayarına uyarlanır. İlk ekranda uzun zorunlu intro olmaz.

| An | Görsel | Animasyon | Teknik not |
|---|---|---|---|
| 0.0–0.25sn | Koyu ekran + poster | Kısa fade | Hero poster ilk HTML paint'inde hazır |
| 0.25–0.65sn | Logo/marka çizgisi | Opacity + translateY(12px) | Daha önce intro görülmüşse atla |
| 0.65–1.25sn | H1 iki satır | Mask reveal + stagger | SEO/AT için gerçek H1 DOM'da |
| 1.0–1.6sn | Açıklama, CTA | Fade/translateY | CTA tıklanabilir kalır |
| 1.6sn+ | Arka plandaki video | Poster → video crossfade | Yalnız yeterli cihaz/ağ kapasitesi |
| Scroll 10–35% | Manifesto | Satır maskeleri | Scroll hijack yok |
| Work viewport | Proje görselleri | 0.5–0.7sn kısa reveal | Her kart tekrarlanarak yüklenmez |
| Services viewport | Satırlar | Hafif y hareketi | Hover/focus eşdeğeri |
| About viewport | Portre + metin | Küçük scale + fade | Mobilde statik |
| CTA viewport | Final slogan | Tek reveal | CTA her zaman erişilebilir |

**Hareket prensipleri:** Hero bir kez yüklenir; sayfa geri geldiğinde intro tekrarlanmaz. Gereksiz scroll kilidi yok. Ses yalnız kullanıcı tıklamasıyla açılır. Reduced-motion modunda animasyonlar minimum ve videolar durgun posterle değiştirilir. Animasyon CSS transform/opacity üzerinden yürür. Geçiş süreleri 200–700ms aralığında tutulur; uzun süreli giriş seyirciye dayatılmaz.

## 7. Kullanıcı akışı
**Potansiyel müşteri:** Hero → 1–2 seçili proje → hizmetler → kanıt → `teklif-al.html` → brief Supabase kaydı → WhatsApp/e-posta yönlendirme.  
**İşe alım/iş ortaklığı:** Hero → portföy seçkisi → Hakkımda → iletişim.  
**Hızlı ziyaretçi:** Header'dan doğrudan İşler/Hizmetler/İletişim.  
**Mobil ziyaretçi:** Poster tabanlı hero → tek sütun projeler → doğrudan CTA.  
Bütün akışlarda modal kapanması (Escape/backdrop), görünür klavye odağı, geri navigasyonu, boş/veri yok halleri ve video yüklenme hataları ele alınır.

## 8. Teknik mimari ve kritik korunacak sistemler

**Önerilen ilk faz:** Mevcut statik HTML/CSS/JS mimarisini koru. Next.js/React'e aniden geçme; V14 tek sayfalık deneyim böyle bir migration gerektirmiyor.

Örnek eklenecek dosyalar:
```
index-v14-preview.html        # V13 index.html kopyasından türetilen geliştirme sürümü
v14/
  tokens.css                  # Renk, tipografi, spacing, utility
  homepage.css                # V14 ana sayfa layout
  motion.css                  # UI animasyonları, reduced-motion
  homepage.js                 # Intro, scene states, observer
  cms-adapter.js              # PMData ile V14 component DOM adaptörü
  media.js                    # Önizleme, autoplay kontrolleri, modal
assets-v14/
  hero-poster.webp
  hero-mobile-poster.webp
  hero-showreel-desktop.mp4
  hero-showreel-mobile.mp4
  selected-work-*.webp
```

**Değişmeden kalacak:** `backend-config.js`, `data-store.js`, yönetim paneli, Supabase tabloları, existing URL ve dosyalar, proje medyaları, mevcut brief akışı. `app.js` değiştirilecekse DOM seçicilerine ve `data-cms` alanlarına dair regresyon testi yap. Tekrarlayan event listener oluşturmadan tek kaynak doğruluk sağla. `motion-v12.js` ile V14 hareketlerinin aynı elementte çakışmasını önlemek için özellik bayrağı veya yalnız V14'te yükleme uygulaması kullan. Kod değişikliğinde secret/service_role anahtarları tarayıcıya taşınmaz; publishable key'nin kullanımında Supabase RLS politikaları doğrulanır.

**Güvenli sürümleme:**
```
git checkout main
git pull --ff-only
git switch -c feature/v14-cinematic-premium
# Değişiklikler sadece bu dalda
```
Dağıtım öncesi tam geri alma için `backup/v13-stable` etiketi veya ayrı ref oluştur; repo ve Supabase şema/yapılandırma yedeğini bağımsız al. Public preview URL'si kullan; admin ve gerçek müşteri brief endpoint'lerini preview'da test verisiyle tetikleme. GitHub Pages yayın dalı `main` ise preview branch'i production'a bağlama. PR ile review → staged preview → production merge.

## 9. Performans ve erişilebilirlik hedefleri
- CWV hedefleri, alan verileriyle doğrulanmak üzere: LCP ≤ 2.5sn, INP ≤ 200ms, CLS ≤ 0.1 (75. persentil hedefleri).
- Mobil başlangıç: hero poster önden; video lazy/şarta bağlı; showreel yalnız etkileşim sonrası tam yükleme.
- Responsive assetler: WebP/AVIF poster, `srcset`, width/height belirtilmiş görseller.
- Ana sayfa için uygun bütçe: ilk açılışta kritik render payload ideal olarak 1.5–2.5MB altında hedeflenir; son karar gerçek ölçümlere göre. Video bu ilk bütçeye dahil edilmemeli/önceliklendirilmemeli.
- Meta/title/og tags güncellenir; canonical korunur; schema.org `ProfessionalService` veya uygun `Person` yapısı gerçek işletme durumuna göre seçilir.
- `prefers-reduced-motion`, görünür focus, alt metin, renk kontrastı, Escape ve klavye navigasyonu.
- Mobil test: 360/390/430/768px; desktop: 1280/1440/1920px. Safari iOS, Chrome Android, masaüstü Chrome/Firefox/Safari.

## 10. Uygulama fazları ve onay kapıları

### Faz A — Envanter ve güvenli kopya
Mevcut `index.html`/CSS/JS selector audit; çalışan sayfaların ekran görüntüleri; Supabase/CMS ve form akışlarının örnek testleri; V13 tag/backup. **Kabul:** V13 referans olarak geri döndürülebilir, mevcut URL listesi çıkarılmış.

### Faz B — Design system + hero prototip
Tokenlar, header, hero, poster/video mantığı, iki CTA, mobil kırılımlar, intro. **Kabul:** Mobilde hero açık, metin okunaklı, CTA çalışıyor, intro atlanabiliyor.

### Faz C — Portfolio + motion + CMS
Proje kartları, showreel modalı, hizmetler, süreç, markalar, imza bölümü, dinamik `PMData` adaptörü; V12 conflict remediation. **Kabul:** Admin'de yayınlanan featured proje yeni ana sayfada doğru sırada görünür; sayfa JS hatasız.

### Faz D — QA, ölçüm ve kontrollü yayın
Form, RLS ve iş bağlantıları, mobil, klavye, SEO, 404, Analytics eventleri, LCP/INP/CLS, gerçek cihaz testi. **Kabul:** Kritik hata yok; önceki işlevler korunmuş; production rollback yolu hazır.

## 11. Yayın öncesi kontrol listesi
- [ ] V13 backup/geri alma noktası var.
- [ ] Eski proje sayfaları ve dosya yolları açılıyor.
- [ ] Supabase featured sıralaması korunuyor.
- [ ] Admin giriş ve projeleri düzenleme testleri başarılı.
- [ ] Brief gerçekten Supabase'e kaydediliyor; başarı/hatada kullanıcı doğru bilgilendiriliyor.
- [ ] Tüm CTA bağlantıları doğru sayfalara gidiyor.
- [ ] Video `muted`, `playsinline`, poster ve lazy davranışı test edildi.
- [ ] Hareket azaltma, klavye ve ekran okuyucu kontrolleri yapıldı.
- [ ] Mobil Safari/Chrome dikey ekran ve adres çubuğu davranışı test edildi.
- [ ] Lighthouse ve mümkünse gerçek kullanıcı performans ölçümleri alındı.
- [ ] Copyright/izin, doğru çalışma rolleri, gerçek müşteri logoları kontrol edildi.
- [ ] SEO canonical, OG image, sitemap, robots/noindex kontrol edildi.
- [ ] Preview'da onaylandıktan sonra PR merge yapıldı.

## 12. Claude / Codex için doğrudan uygulama talimatı
> GitHub deposu: https://github.com/paroglu/paroglumedia. Bu belge ParogluMedia V14 Cinematic Premium master spesifikasyonudur. Önce dosya ağacını ve `index.html`, `styles.css`, `app.js`, `motion-v12.js`, `motion-v12.css`, `data-store.js`, admin ve brief akışlarını oku. Mevcut HTML/CSS/vanilla JS mimarisini, proje medyalarını, tüm mevcut sayfa URL'lerini, Supabase CMS'yi, featured proje sıralamasını ve brief gönderim akışını koru. `main` üzerinde değişiklik yapma; `feature/v14-cinematic-premium` dalında ilerle. İlk PR'da yalnız design tokens, header, hero, intro, mobil ve accessibility temellerini hayata geçir. Sonraki PR'da proje seçkisi, services, process, about ve CTA bölümlerini uygula; CMS adaptörünü ekle. V12 animasyonlarıyla çift bind/çakışmayı önle. Harici görseli kendi çalışması gibi sunma; mevcut repo medyalarını kullan. Performans ve mobil öncelikli yaklaş. Bitince değişen dosya listesi, test sonuçları, ekran görüntüleri, riskler, geri alma adımları ve PR açıklaması üret. Repo/production'a onaysız merge veya deploy yapma.

---
**Kaynaklar:**
- https://github.com/paroglu/paroglumedia
- https://github.com/paroglu/paroglumedia/blob/main/README-V13-FINAL.txt
- https://github.com/paroglu/paroglumedia/blob/main/README-V12-MOTION.txt
- https://github.com/paroglu/paroglumedia/blob/main/index.html
- https://github.com/paroglu/paroglumedia/blob/main/data-store.js
