# FV Nakliye — Açık Uçlu Ürün Başlangıç Paketi

Bu paket FV Nakliye'yi önce kendi işletmende kullanıp sonra başka nakliye işletmelerine veya bireysel kullanıcılara sunabilecek şekilde geliştirmek için hazırlanmış **kaynak dosya ve teknik plan paketidir**. Kurulabilir APK veya canlıya alınmış hizmet değildir.

## Ana ürün kararı
- Android uygulaması + bilgisayarda web paneli.
- Her işletme/kullanıcı kendi hesabına ve kendi verilerine sahip olur.
- Bir platform yöneticisi (ürün sahibi) ve her müşteri işletmenin kendi yöneticisi bulunabilir.
- İşletme yöneticisi kendi şoförlerini davet eder ve hesaplarını yönetir.
- Şoför yalnızca sefer/yakıt kaydı gönderir; kayıtlar işletme yöneticisi onaylayana kadar bekler.
- Finans ve kullanıcı yönetimi işletme yöneticisine aittir.
- Her işletmenin verisi diğer işletmelerden kesin olarak ayrılır.

## Paket yapısı
- `web/index.html` — mevcut statik ekran taslağı; gerçek giriş veya bulut bağlantısı yok.
- `database/schema_v1_single_business.sql` — ilk tek işletmeli şema taslağı; çok müşterili ticari yayına doğrudan uygulanmamalı.
- `docs/V1_GEREKSINIMLER.md` — ilk sürümün gereksinimleri.
- `docs/MIMARI_VE_COK_MUSTERILI_YAPI.md` — büyüyebilir ürün mimarisi ve tenant izolasyonu.
- `docs/DUZENLEME_REHBERI.md` — kaynakları düzenleme, sürümleme ve özelleştirme rehberi.
- `docs/YOL_HARITASI.md` — gerçek uygulamaya giden geliştirme aşamaları.
- `docs/TICARI_KULLANIM_VE_LISANS.md` — ürünü satma/yayımlama öncesi lisans ve ticari hazırlık notları.
- `api/openapi-taslak.yaml` — istemci, web paneli ve sunucu için taslak API sözleşmesi.
- `assets/FV_Nakliye_logo.jpg` — amblem görseli.

## Önemli
Bu paket kaynak ve plan sağlar; APK, canlı web adresi, kimlik doğrulama sunucusu veya kurulmuş veritabanı sağlamaz. Ticari kullanıma açılmadan önce çok-müşterili veri izolasyonu, rol güvenliği, yedekleme, KVKK, lisanslar ve güvenlik testleri uygulanmalıdır. `schema_v1_single_business.sql` sadece referans/başlangıç taslağıdır; SaaS sürümünde tenant bazlı şema ve politikalar tasarlanmalıdır.
