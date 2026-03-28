# Frontend Visual Review Guide

## Amaç
Bu rehber, modern fintech tasarım turundan sonra kontrol edilmesi gereken ana görsel ve deneyim noktalarını hızlıca doğrulamak için hazırlandı.

## 1. Genel Tema Kontrolü
- `/login` ve `/dashboard` arasında renk dili aynı aileden geliyor mu?
- Arka planlar düz gri yerine katmanlı mavi/cyan fintech hissi veriyor mu?
- Light mode ana yüzey olarak net, parlak ve premium görünüyor mu?
- Dark mode kırılmadan çalışıyor mu?

## 2. Türkçe Metin Kontrolü
- Türkçe seçildiğinde `ı, İ, ş, ğ, ü, ö, ç` karakterleri düzgün görünüyor mu?
- Şu yüzeylerde bozuk ASCII metin kaldı mı kontrol edin:
  - `/dashboard`
  - `/dashboard/payroll`
  - `/dashboard/employees`
  - `/dashboard/companies`
  - `/dashboard/authorizations`
  - `/dashboard/settings`

## 3. Header / Sidebar / Nav Kontrolü
- Üst bar butonları hizalı mı?
- Dil seçici, tema butonu, bildirim butonu ve profil alanı aynı görsel dilde mi?
- Sidebar aktif menü durumu net seçiliyor mu?
- Mobilde hamburger ile açılan sidebar taşma yapıyor mu?

## 4. Motion Kontrolü
- Sayfa ilk açılışında section girişleri görünür biçimde ama rahatsız etmeyecek kadar yumuşak mı?
- Auth ekranı, dashboard intro ve timeline alanlarında motion hissediliyor mu?
- Motion performansı özellikle mobilde takılma yaratıyor mu?

## 5. Dashboard Kontrolü
- Hero alanı daha güçlü ve premium hissediyor mu?
- Timeline, employee services ve help/activity alanları tek tasarım dili içinde mi?
- Kartlar birbirinden kopuk değil de aynı sistemin parçası gibi mi görünüyor?

## 6. Payroll Kontrolü
- `/dashboard/payroll` ekranında filtre alanı, özet chips ve tablo birlikte düzenli mi?
- Bordro detail sheet içinde tab yapısı çalışıyor mu?
- `Summary`, `Document`, `Guide` sekmeleri görsel olarak net mi?
- Print / full page akışı bozulmadan korunuyor mu?

## 7. Auth Kontrolü
- `/login` ekranı iki kolonlu premium auth hissi veriyor mu?
- SMS doğrulama modalı eski görünüme göre daha net ve kaliteli mi?
- `/forgot-password` ve `/reset-password` aynı auth ailesinden geliyor mu?

## 8. Responsive Kontrol
- 390px genişlik civarında yatay taşma var mı?
- Header öğeleri alt alta kırıldığında düzen korunuyor mu?
- Dashboard kartları ve payroll tablo/kart yapısı mobilde okunabilir mi?
- Sidebar sheet, modal ve action button alanlarında taşma var mı?

## 9. Hızlı Kabul Kriteri
Aşağıdaki 5 madde "evet" ise tur başarılı kabul edilebilir:
- Türkçe metinler bozuk değil.
- Nav/header butonları görsel olarak tutarlı.
- Tema eski halden belirgin biçimde daha canlı ve fintech karakterli.
- Motion en az dashboard ve auth tarafında görünür.
- Mobil görünümde kırılma veya yatay scroll yok.
