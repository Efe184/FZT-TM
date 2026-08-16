# Fzt-TM — Fzt. Turgay Mersin Kişisel Web Sitesi

## Proje

Evde fizik tedavi ve rehabilitasyon hizmeti veren **Fizyoterapist Turgay Mersin** için
Awwwards tarzı, tek sayfalık (one-page) kişisel web sitesi.

**Niş / konumlandırma:** Evde fizik tedavi — ağırlıklı nörolojik rehabilitasyon
(hemipleji/inme) ve geriatrik hasta grubu; pediatrik rehabilitasyon geçmişi var.
Hedef kitle: hastalar ve **hasta yakınları** (çoğunlukla 45+ yaş, mobilde geziyor).

**Marka konsepti: B — "Bütünsel Yenilenme & Organik İyileşme"** (Kreatif Brief'teki
Seçenek B). Gerekçe: hedef kitle yaşlı/nörolojik hasta aileleri; güven, sıcaklık ve
okunabilirlik önce gelir. Koyu zemin + neon (Seçenek A) bu kitleye uygun değil.

## Renk paleti ve tipografi

| Değişken | Renk | Kullanım |
|---|---|---|
| `--bg` | `#F7F5F0` | Sıcak bej zemin |
| `--sage` | `#2D5A27` | Adaçayı yeşili — ana marka rengi, vurgular |
| `--charcoal` | `#1A202C` | Kömür — metin |
| `--purple` | `#805AD5` | Otorite moru — küçük aksanlar (numaralar, çizgiler) |
| `--soft` | `#E2E8F0` | Yumuşak gri |
| `--muted` | `#6b7280` | İkincil metin |

**Tipografi (Google Fonts):** Başlıklar **Fraunces** (soft serif — wellness trendi;
italik vurgular adaçayı yeşili). Gövde/UI: **Instrument Sans** (Awwwards'lardaki
neo-grotesk estetiğin ücretsiz karşılığı; 45+ kitle için yüksek okunabilirlik).
CSS değişkenleri: `--font-head`, `--font-body`. Fallback: Georgia / Segoe UI.
Gerekçe: Awwwards kazananları çoğunlukla ücretli Diatype/Suisse kullanıyor;
sağlık-wellness tarafında trend "soft serif + sessiz sans" ikilisi.

## Teknoloji

- **Sıfır bağımlılık**: tek dosya vanilla HTML/CSS/JS. Framework, CDN, build yok.
- **Hero animasyonu**: Kling AI ile üretilmiş X-ray omurga videosu
  (`sol_alttaki_kling_ai_omni.mp4`, 8sn/24fps/1280x720) → `frames-spine/` 96 kare WebP
  (fps=12, q=62, ~3.8 MB) → scroll-scrub. Figür oturur kambur pozdan dik duruşa kalkar.
  HERO KOYU: sticky zemin #0A1633, metinler açık (#f4f2ea / #a8d5a0), soldan koyu veil;
  sayfanın kalanı bej — bilinçli "koyu hero → açık gövde" geçişi. "duruş 000/100" HUD.
  NOT: videodaki omurga KIRMIZI parlıyor; ileride yeşil vurgulu versiyon üretilirse
  (iyileşme=yeşil hikayesi) tercih edilir. Eski Pexels video scrub'ı demo-b.html +
  frames/ klasöründe arşiv duruyor.
- `prefers-reduced-motion`: scrub kapatılır, son kare statik gösterilir.
- Erişilebilirlik/okunabilirlik öncelikli: yaşlı kitle → büyük punto, yüksek kontrast.

## Dosyalar

- `index.html` — **asıl site** (tüm bölümler burada)
- `demo.html` / `demo-b.html` — Konsept A/B teknik demoları (arşiv; site index.html'de ilerler)
- `frames/frame_001..104.webp` — hero kare dizisi (1600px, ~2.3 MB toplam)
- `6111091-uhd_3840_2160_25fps.mp4` — kaynak stok video (Pexels; PLACEHOLDER —
  ileride Turgay Bey ile gerçek çekimle değişecek)
- `assets/step1..5.jpg` — Tedavi Süreci kart fotoğrafları (Pexels, telifsiz;
  ID'ler: 1→7984814 telefonla arayan hasta yakını, 2→7551622 evde değerlendirme, 3→7176036 plan/pano,
  4→6111585 egzersiz (hero videosuyla aynı çekim serisi), 5→7699526 seans notu;
  gerçek çekim yapılınca bunlar da değişebilir)
- `Kreatif_Brief_ve_Tasarim_Stratejisi.pdf`, `Kişisel Markalaşma Stratejileri.pdf` — strateji dokümanları

### Kare dizisi üretimi (ffmpeg pipeline)

ffmpeg sistemde kurulu değil; portable sürüm scratchpad'e indirilip kullanıldı (geçici).
Yeni video geldiğinde:

```
ffmpeg -i kaynak.mp4 -vf "fps=7.5,scale=1600:-1" -c:v libwebp -q:v 78 frames/frame_%03d.webp
# mobil set (ileride): scale=800:-1 → frames-mobile/
```

## Site bölümleri (index.html sırası)

1. **Hero** — scrub video + "evde fizik tedavi" mesajı + Ücretsiz Ön Değerlendirme CTA
2. **Paradigma köprüsü** — kısa scroll geçişi (tedavi felsefesi)
3. **Ben Kimim** — Turgay Mersin'in tam metni (müşteriden geldi, DEĞİŞTİRME;
   kariyer akışı: Pediatri → Hastane/Nöroloji+Geriatri → Evde rehab ~4 yıl)
4. **Tedavi Sürecimiz** — dikey scroll'un sürdüğü YATAY panel şeridi (sticky,
   6 panel: 5 adım + koyu "Hedefimiz" finali; dev hayalet numaralar, adım sayacı,
   ilerleme çizgisi; ≤820px ve reduced-motion'da dikey yığına düşer):
   İlk İletişim → Ücretsiz Ön Değerlendirme → Kişiye Özel Plan → Tedavi ve Takip →
   Periyodik Değerlendirme (10-15 seansta yeniden değerlendirme) + "Hedefimiz" kapanışı
5. **Hasta Hikayeleri** — anonim kartlar (baş harf + yaş + tanı), alıntı formatında
6. **İletişim / CTA** — telefon + WhatsApp kart butonları (SVG ikonlu) + iletişim formu.
   Form BACKEND'SİZ "WhatsApp köprüsü": alanlar (ad, tel, arama zamanı, açıklama) hazır
   WhatsApp mesajına dönüşüp wa.me/905528004434'e açılır; sunucuda veri saklanmaz.
   KVKK açık rıza kutusu önceden işaretsiz, işaretlenmeden gönder butonu pasif.
   Aydınlatma Metni linki hâlâ placeholder (hukukçu metni bekleniyor).
7. **Footer** — unvan, diploma no, KVKK, yasal uyarı

## Yasal kurallar (HER içerik değişikliğinde uygulanır)

- Sağlık tanıtım mevzuatı: **"kesin iyileşme/garanti" vaadi YASAK**; "başarılı sonuçlar
  elde ettik" gibi ifadeler kalabilir ama tanı koyucu/garanti dili kullanma.
- Hasta hikayeleri: **anonim** (isim yok, baş harf + yaş), yayın öncesi **yazılı onay** şart.
  Şu anki hikayeler PLACEHOLDER — gerçekleriyle değiştirilecek.
- Her sağlık içeriğinin yanına: "Bu içerik genel bilgilendirme amaçlıdır." ibaresi.
- KVKK: iletişim formu eklenirse açık rıza kutusu (önceden işaretsiz) + aydınlatma metni.

## Bekleyen içerik (müşteriden istenecek)

- [x] Gerçek telefon numarası + WhatsApp: **+90 552 800 44 34** (tel:, wa.me linkleri
      ve form köprüsü bu numaraya bağlı)
- [x] Hizmet bölgesi: **İstanbul — Avrupa Yakası** + 19 ilçe (Arnavutköy, Avcılar,
      Bağcılar, Bahçelievler, Bakırköy, Başakşehir, Bayrampaşa, Beyoğlu, Esenler,
      Eyüpsultan, Fatih, Gaziosmanpaşa, Güngören, Kağıthane, Küçükçekmece, Sarıyer,
      Sultangazi, Şişli, Zeytinburnu) + "Avrupa Yakası'ndaki tüm hastaneler".
      İletişim bölümündeki `.area` bloğunda ve JSON-LD `areaServed` dizisinde.
- [x] Turgay Bey'in fotoğrafı: `assets/turgay-mersin.jpeg` (Ben Kimim bölümü;
      3:4 dikey, 4:5 kutuda `object-position:62% 28%` ile kadrajlanıyor)
- [x] Gerçek hasta hikayeleri (3 adet: "Annem Yeniden Hayata Döndü" / Küçükçekmece,
      "Babamın Yeniden Kendine Güvenmesini Sağladı" / Alibeyköy,
      "Babaannem Yeniden Camın Önüne Gidebiliyor" / Sultangazi — 82 yaş, 20 seans,
      kalça protezi sonrası; metinler müşteriden geldiği gibi, DEĞİŞTİRME)
      — ⚠ yazılı hasta yakını onaylarının alındığı Turgay Bey'e teyit ettirilecek
- [x] Diploma / mezuniyet: **Yakın Doğu Üniversitesi — Sağlık Bilimleri Fakültesi,
      Fizyoterapi ve Rehabilitasyon (2023), Diploma No: 61391** (footer güven bölümü).
      ⚠ Kaynak YÖK Mezun Belgesi'nde T.C. kimlik no, anne/baba adı, doğum tarihi ve
      diploma notu da var — bunlar KİŞİSEL VERİ, siteye ASLA konmaz.
- [ ] Dernek üyelikleri / sertifikalar — footer'da satır YORUMA ALINDI
      (`Güven & Yeterlilik` bloğu); bilgi gelince yorum açılacak
- [~] KVKK aydınlatma metni: `kvkk.html` TASLAK hazır (form alanlarına birebir uygun,
      sağlık verisi = özel nitelikli veri vurgusuyla). ⚠ AVUKAT ONAYI BEKLİYOR.
      İçindeki kırmızı `.todo` kutuları doldurulmalı: e-posta, tebligat adresi,
      sağlık kayıtları saklama süresi. Onaydan sonra `.box.warn` taslak uyarısı ve
      `meta robots noindex` kaldırılacak.
- [x] E-posta: **turgay.mrsn00@gmail.com** (KVKK metninde veri sorumlusu bilgileri
      ve başvuru bölümünde; sitenin iletişim bölümünde HENÜZ YOK — telefon/WhatsApp
      odaklı tasarım korunuyor)
- [ ] Tebligat adresi (KVKK m.11 yazılı başvuru yolu için zorunlu — son eksik alan)
- [ ] Gerçek çekim hero videosu (yarım günlük çekim önerildi)

## Yol haritası

1. ✅ Konsept demoları (A/B) + scrub pipeline
2. ✅ Konsept B'ye gerçek video bağlama
3. ⏳ index.html: tüm bölümlerle tam site (bu aşamadayız)
4. Mobil ince ayar + mobil kare seti (800px)
5. SEO/meta: title, description, Open Graph, `Physiotherapy`/`LocalBusiness` schema,
   yerel anahtar kelimeler ("evde fizik tedavi + [şehir]")
6. Hosting + domain (öneri: turgaymersin.com vb.) + yayın
