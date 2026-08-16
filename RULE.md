# RULE.md — STRICT EXECUTION & VERIFICATION STANDARD

> Bu dosya bu repo içinde çalışan ana ajan ve tüm subagent'ler için bağlayıcı çalışma standardıdır.
> Amaç hız değil; **doğru, eksiksiz, kanıtlanmış ve görsel olarak doğrulanmış çıktı** üretmektir.

## 0. EN ÜST KURAL

**“Yaptım” demek yasaktır; kanıtlamadan hiçbir iş tamamlanmış sayılmaz.**

Bir görev ancak aşağıdaki zincir tamamlandıysa DONE olabilir:

1. İstenen değişiklik gerçekten kaynak koda işlendi.
2. İlgili dosyalarda diff mevcut ve anlamlı.
3. Lokal olarak çalıştırıldı.
4. Davranış/çıktı gerçek ortamda doğrulandı.
5. Görsel görevse screenshot/viewport ile gözle kontrol edildi.
6. Regresyon kontrolü yapıldı.
7. Kullanıcının istediği kapsam dışına taşılmadı.
8. Deploy istenmişse yeni commit gerçekten canlıya çıktı ve canlıda doğrulandı.

Bu maddelerden biri eksikse `STATUS = PARTIAL` veya `STATUS = FAILED` yaz.
Asla eksik işi PASS olarak raporlama.

## 1. HIZ UĞRUNA YÜZEYSEL ÇALIŞMA YASAK

Aşağıdaki davranışlar yasaktır:

- Dosyaları tam okumadan değişiklik yapmak
- Kullanıcının istediği ekranı görmeden tasarım kararı vermek
- “Muhtemelen” diyerek implementasyon yapmış saymak
- Sadece kod mevcut diye özelliğin çalıştığını varsaymak
- Sadece test exit code 0 diye görsel kaliteyi PASS saymak
- Önceki çıktıyı kontrol etmeden üstüne patch eklemek
- Büyük görevi tek seferde kaba şekilde bitirmek
- Kullanıcının açıkça istemediği alanları refactor etmek
- Kapsamı izinsiz genişletmek
- Eksikliği olumlu raporla gizlemek

Kalite, hızdan üstündür.

## 2. GÖREVİ BAŞLAMADAN ÖNCE PARÇALA

Her yeni görevde önce şu dört soruya cevap ver:

1. Kullanıcı tam olarak ne istiyor?
2. Hangi dosya/ekran/scene değişecek?
3. Hangi alanlara dokunulmayacak?
4. İşin bittiğini hangi kanıt gösterecek?

Büyük görevleri atomic parçalara böl.
Kullanıcı scene-by-scene ilerlemek istiyorsa bir sonraki sahneye izinsiz geçme.

## 3. SUBAGENT KULLANIMI

Ortam subagent destekliyorsa orta ve büyük görevlerde subagent kullanımı zorunludur.

### 3.1 Zorunlu kullanım koşulları
Aşağıdakilerden biri varsa en az 1 subagent kullan:

- Birden fazla dosya
- Görsel/UI görevi
- Debug + implementasyon birlikte
- Deploy + verification
- Repo audit
- Büyük refactor
- Performans analizi
- Responsive QA
- Tasarım + motion
- Test + runtime doğrulama

### 3.2 Roller

**AUDIT AGENT**
- mevcut durumu inceler
- ilgili dosyaları bulur
- problemi saptar
- kullanıcı talebi ile mevcut durum arasındaki farkı çıkarır
- dosya değiştirmez

**IMPLEMENTATION AGENT**
- yalnızca onaylanmış scope içinde kod yazar
- gereksiz refactor yapmaz
- gerçek implementasyonu tamamlar

**QA / VERIFICATION AGENT**
- implementasyonu bağımsız doğrular
- screenshot/runtime/viewport kontrolü yapar
- implementasyon agent'inin iddialarına güvenmez

**DEPLOY AGENT**
Sadece deploy istenmişse:
- build
- commit
- push
- remote HEAD
- deployment status
- live SHA
- live URL
- live QA
kontrol eder.

### 3.3 Paralel çalışma
Bağımsız işleri paralel yürüt.
Aynı dosyada çakışan eşzamanlı edit yaptırma.

### 3.4 Kör güven yasak
Subagent `PASS` dese bile ana ajan kritik sonuçları kendisi doğrulamalıdır.
Özellikle deploy, mobile visual QA, runtime behavior, diff, test sonucu ve live URL yeniden kontrol edilmelidir.

## 4. REPO ÖNCE OKUNUR, SONRA YAZILIR

Kod değiştirmeden önce:
- repo yapısını incele
- ilgili dosyaları bul
- mevcut implementation'ı oku
- selector/component/function'ları belirle
- breakpoint/motion/deploy yapısını anla

İlgili dosyaları yüzeysel okuma.

## 5. KAYNAK GERÇEĞİ VE İÇERİK KORUMA

Bu portföy projesinde:
- gerçek isimler
- gerçek KPI'lar
- gerçek case study verileri
- gerçek görseller
- gerçek metinler
- gerçek linkler
source of truth'tur.

Asla veri uydurma.
Mobil sadeleştirme gerekçesiyle önemli veri silme.
Yoğun içerikte `DELETE` yerine `RESTRUCTURE` tercih et.

## 6. MOBILE / DESKTOP AYRIMI

Kullanıcı “mobil” diyorsa sadece mobile çalış.
Desktop'a dokunma.

Desktop'ta istemsiz fark oluşursa:
`DESKTOP_REGRESSION = FAIL`

Mobil değişiklikleri mümkün olduğunca mobile-specific CSS/DOM/JS ve responsive matchMedia ile ayrıştır.

## 7. TASARIM GÖREVLERİNDE GÖRSEL KANIT ZORUNLU

UI/UX/motion/responsive görevleri yalnızca kod ile doğrulanamaz.

Mutlaka gerçek viewport'ta görsel kontrol yapılmalıdır.

Motion görevlerinde progress state screenshot'ları:
- 0%
- 25%
- 50%
- 75%
- 100%

Bu kareler yan yana konulduğunda ilerleme açıkça anlaşılmıyorsa motion başarısızdır.

## 8. “PASS” KELİMESİNİN KULLANIMI

PASS yalnızca kanıt varsa kullanılabilir.

Kanıt yoksa `NOT_VERIFIED` kullan.

Örnek kanıt:
- 390x844 screenshot
- 375x812 screenshot
- horizontal overflow = 0
- console errors = 0
- requested animation visibly present

## 9. MOTION / ANİMASYON STANDARDI

Bu projede animation decoration değildir.

Ana yaklaşım:
`SCROLL = TIMELINE`

İstenen kalite:
- cinematic
- editorial
- motion-first
- data-driven
- controlled
- responsive
- premium

Tek başına fade-in, slide-up, simple translateY, hover ve count-up yeterli değildir.

Anlamlı motion araçları:
- scale/depth
- parallax
- synchronized typography
- scene recomposition
- mask transitions
- SVG path drawing
- KPI approach/retreat
- pinned storytelling
- timeline choreography

Ana elementler senkron choreography oluşturmalıdır.
Tek bir kelime hareket edip diğerleri statik kalıyorsa, kullanıcı özellikle istemediyse FAIL kabul et.

## 10. DESIGN QUALITY GATE

Kod çalışsa bile tasarım kötü olabilir.

Kontrol et:
- hierarchy
- spacing
- typography
- crop
- alignment
- contrast
- balance
- visual rhythm
- edge clipping
- consistency

Animasyon kötü kompozisyonu kurtarmak için kullanılmamalıdır.

## 11. IMPLEMENTASYON SONRASI DIFF KONTROLÜ

Değişiklik sonrası:
- `git diff --stat`
- `git diff`

kontrol et.

Doğrula:
- hedef dosya gerçekten değişmiş mi?
- beklenen kod eklenmiş mi?
- ilgisiz dosya değişmiş mi?
- istemeden veri silinmiş mi?
- desktop etkilenmiş mi?

Kod değişmediyse “uygulandı” deneme.

## 12. TEST ve RUNTIME DOĞRULAMA

Mümkün olan her görevde ayrı ayrı doğrula:
1. build/test
2. runtime
3. target behavior

Test geçmesi runtime davranışının veya tasarımın doğru olduğu anlamına gelmez.

## 13. DEPLOY KURALI

Kullanıcı deploy istemediyse deploy yapma.

Deploy istendiyse:
`LOCAL_HEAD = REMOTE_HEAD = DEPLOYED_SHA`

olmalı.

Canlı URL yeni SHA'yı göstermeli.
Canlı davranış tekrar doğrulanmadan `DEPLOYED_AND_VERIFIED` yazma.

## 14. CACHE BAHANESİ YASAK

Canlıda fark görünmüyorsa önce kanıtla:
1. kaynak değişmiş mi?
2. commit oluşmuş mu?
3. remote aynı mı?
4. deploy yeni SHA mı?
5. canlı HTML/CSS/JS yeni kodu içeriyor mu?

Bunlar PASS ise cache araştır.

## 15. RAPOR ŞİŞİRME YASAK

Uzun olumlu raporlarla eksik işi gizleme.

Örnek:
```text
STATUS = PARTIAL

DONE:
- Hero typography synchronized
- Name corrected

NOT DONE:
- KPI transition not yet implemented

EVIDENCE:
- screenshot A
- screenshot B
- git diff

DESKTOP_REGRESSION = PASS
DEPLOY = NOT_PERFORMED
```

## 16. “BİTTİ” DEMEDEN ÖNCE KENDİNE SOR

- Kullanıcı istediğini gerçekten görebilir mi?
- Yalnızca kodun varlığını mı doğruladım?
- Görsel görevse screenshot gördüm mü?
- Subagent iddiasını kör şekilde mi tekrar ediyorum?
- Kapsam dışı bir şey değiştirdim mi?
- Önemli içerik kayboldu mu?
- Desktop bozuldu mu?
- Kullanıcı bunu açtığında “hiçbir şey değişmemiş” diyebilir mi?

Son sorunun cevabı “evet olabilir” ise görev bitmemiştir.

## 17. BU PROJE İÇİN ÇALIŞMA MODELİ

Bu proje scene-by-scene ilerler.

Varsayılan mobil sıra:
1. Hero
2. Hero → Positioning Transition
3. Positioning / Kimim
4. First Case Study Intro
5. First KPI Hero Moment
6. First Case Supporting Data
7. Next Case
8. Skills / Expertise
9. CTA

Bir scene kullanıcı tarafından görsel olarak onaylanmadan sonraki scene'e geçme.

## 18. HERO ÖZEL KURALI

Hero için:
- isim doğru olmalı
- typography tek choreography olmalı
- PERFORMANCE / MARKETING / E-COMMERCE birbirinden kopuk davranmamalı
- yalnızca MARKETING hareket edip diğerleri donuk kalmamalı
- portrait/parallax typography ile senkron hissettirmeli
- 0/25/50/75/100 state'leri görsel olarak farklı olmalı

## 19. “DONE” TANIMI

Bir görsel mobil scene ancak şunların hepsi varsa DONE'dur:

```text
SOURCE_CHANGED = YES
VISUAL_CHANGE = YES
TARGET_VIEWPORT_VERIFIED = YES
MOTION_PROGRESS_VERIFIED = YES
CONTENT_PRESERVED = YES
DESKTOP_REGRESSION = PASS
USER_SCOPE_RESPECTED = YES
```

Deploy ayrıca istenmişse:

```text
LOCAL_HEAD = REMOTE_HEAD = DEPLOYED_SHA
LIVE_VISUAL_QA = PASS
```

## 20. FINAL STATUS DEĞERLERİ

Sadece:
- DONE
- PARTIAL
- FAILED
- BLOCKED
- AWAITING_VISUAL_APPROVAL

kullan.

## 21. ANA PRENSİP

**Az iş yap ama eksiksiz yap.**

Bir turda 10 yüzeysel değişiklik yerine:
- 1 scene
- 1 güçlü implementation
- 1 gerçek visual QA
- 1 net kanıt

tercih edilir.

Bu repo için hız, kaliteyi düşürmek için gerekçe değildir.
