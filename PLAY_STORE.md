# Go Route Taksi (müştəri) — Play Store hazırlıq bələdçisi

| | |
|---|---|
| Təklif olunan Android paket ID | `com.goroute.taksi` (digər tətbiqlər: `com.goroute.user`, `com.goroute.kuryer`) |
| Repo / Pages ünvanı | `https://github.com/seymur048ibrahimov-wq/youtaxi` |
| Firebase layihəsi | `bkaugo` |

## Firebase qurulumu (layihə: `bkaugo`)

> `bkaugo` layihəsi digər Go Route tətbiqləri ilə ortaqdır. Aşağıdakı addımlar mövcud məlumata toxunmur.

1. **Authentication → Sign-in method:** *Email/Password* və *Google* aktiv olsun.
   **Settings → Authorized domains:** `seymur048ibrahimov-wq.github.io` (və Firebase Hosting domenləriniz) siyahıda olsun.
2. **Firestore qaydaları:** `firestore.taxi.rules` faylındakı funksiyaları və `match` bloklarını
   Console → Firestore → Rules-dakı **mövcud** qaydaların `match /databases/{database}/documents { … }` daxilinə **əlavə edin**
   (faylı olduğu kimi `firebase deploy` ETMƏYİN — bu, kuryer/müştəri qaydalarını silər). Sonra **Publish**.
3. **Admin:** Firestore-da `admins` kolleksiyası → sənəd ID-si = sizin Firebase UID-niz (Authentication səhifəsində görünür), sahə: `role: "admin"`.
4. **Sürücü təsdiqi:** yeni sürücü qeydiyyatdan keçəndə `taxiDriverProfiles/{uid}` yaranır (`approved: false`).
   Sənədləri (vəsiqə, texpasport) yoxladıqdan sonra Console-da `approved` sahəsini **true** edin — sürücü tətbiqi avtomatik açılır.
5. **Google Maps açarı** (müştəri tətbiqi): Google Cloud Console → Credentials → açarın *HTTP referrers* siyahısına
   `https://seymur048ibrahimov-wq.github.io/*` əlavə olunub-olmadığını yoxlayın. API-lər: Maps JavaScript, Places (New), Directions/Routes, Geocoding.
6. **Blaze planı** aktivdir — Firestore üçün əlavə addım lazım deyil. İstəsəniz *Budget alert* qurun.

## Google Play-ə çıxarış (PWABuilder / TWA — digər tətbiqlərinizdəki kimi)

1. Repo → **Settings → Pages → Deploy from branch → main / (root)**. Ünvan: `https://seymur048ibrahimov-wq.github.io/<repo>/`.
2. https://www.pwabuilder.com → həmin ünvan → **Package for stores → Android**. Parametrlər:
   - Package ID: aşağıdakı cədvələ görə; *Signing key*: **Create new** (açarı və parolu saxlayın!).
   - **Location delegation: ON** (xəritə/GPS üçün vacibdir), *Notifications delegation* — istəyə bağlı.
   - Display: standalone, Orientation: portrait.
3. Play Console-da **Play App Signing** SHA-256 barmaq izini götürün (Setup → App signing) və kök repo
   `seymur048ibrahimov-wq.github.io/.well-known/assetlinks.json` faylına bu tətbiqin blokunu əlavə edin
   (mövcud tətbiqlərin bloklarını silməyin, massivə əlavə edin).
4. Mağaza məlumatı: `store/` qovluğundakı ikon (512) və feature graphic (1024×500) + öz telefonunuzdan ən azı 2 skrinşot.
   Mətnlər aşağıdadır. **Privacy policy URL:** `https://seymur048ibrahimov-wq.github.io/<repo>/privacy-policy.html`.
   **Account deletion URL:** `…/delete-account.html` (tətbiqdə də var: Profil → Hesabı sil).
5. Şəxsi hesab qaydası: istehsalatdan əvvəl **Closed testing — ən azı 12 test istifadəçisi, 14 gün fasiləsiz**.

## Mağaza mətnləri (Azərbaycan dili)


**Ad:** Go Route Taksi
**Qısa təsvir (80):** Bakıda taksi: bir toxunuşla sifariş, sabit qiymət, canlı izləmə.
**Tam təsvir:**
Go Route Taksi ilə Bakıda taksi çağırmaq asandır. Götürülmə və təyinat ünvanını seçin, qiyməti əvvəlcədən görün və sürücünün xəritədə sizə necə yaxınlaşdığını canlı izləyin.

• Sabit qiymət — səfərdən əvvəl bilirsiniz
• Ekonom, Komfort, Biznes, Minivan, Yük və Ev heyvanı sinifləri
• Canlı izləmə, sürücünün adı, avtomobili və nömrəsi
• Başqası üçün sifariş, planlaşdırılmış səfər, dayanacaqlar
• SOS və səfəri yaxınlarınızla paylaşma
• Səfər tarixçəsi, Ev/İş ünvanları, promo kodlar

Qeyd: tətbiq işləmək üçün internet və yer icazəsi tələb edir.
**Kateqoriya:** Maps & Navigation (və ya Travel & Local)  **Əlaqə e-poçtu/WhatsApp:** +994 70 248 48 52

## Data safety (Play Console → App content) — doldurma cədvəli

| Məlumat | Toplanır | Paylaşılır | Məqsəd | Qeyd |
|---|---|---|---|---|
| Dəqiq yer | Bəli | Bəli (sifarişi qəbul edən sürücü) | Tətbiq funksionallığı | Yalnız tətbiq açıq olanda |
| Ad, e-poçt, telefon | Bəli | Bəli (sürücü: ad, telefon) | Hesab, funksionallıq | |
| Səfər/sifariş tarixçəsi | Bəli | Xeyr | Funksionallıq | |
| Qiymətləndirmə/rəy | Bəli | Xeyr | Funksionallıq | |
Şifrələmə: **Bəli (HTTPS)** · Silmə mexanizmi: **Bəli** (tətbiq daxilində + veb link) · Üçüncü tərəf: Google (Firebase, Maps).

Digər bəyannamələr: *Ads* → Xeyr · *Target audience* → 18+ · *News app* → Xeyr · *Government app* → Xeyr ·
*Content rating* anketi → şiddət/cinsi məzmun yoxdur · *Financial features* → yoxdur (ödəniş tətbiqdə deyil, nağd).

## Test siyahısı (yayımdan əvvəl telefonda keçin)

- [ ] Qeydiyyat → daxil ol → çıx → Google ilə daxil ol
- [ ] Yer icazəsi: ver / rədd et (xəta mesajı düzgündür)
- [ ] Ünvan axtarışı, xəritədə seçim, marşrut və qiymət göstərilir
- [ ] Sifariş → (sürücü tətbiqində) qəbul → "çatdım" → "başla" → "bitir" → qiymətləndirmə
- [ ] Sifariş ləğvi (axtarış zamanı və sürücü gələndən sonra)
- [ ] Sürücü tapılmadıqda 5 dəqiqədən sonra "tapılmadı" və yenidən axtarış
- [ ] İnternet kəsiləndə offline səhifə, qayıdanda bərpa
- [ ] Profil → Hesabı və məlumatlarımı sil (sonra yenidən qeydiyyat mümkündür)
- [ ] Gizlilik siyasəti və hesab silmə səhifələri açılır
