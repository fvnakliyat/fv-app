# Yol haritası

## Aşama 1 — Gereksinim ve tasarım
- Bu paketteki roller, ekranlar, kayıt alanları ve onay akışı kesinleştirilir.
- Şoförün sefer ücretini görüp görmeyeceği, fiş zorunluluğu ve araç atama kuralları kararlaştırılır.

## Aşama 2 — Güvenli çok müşterili backend
- Organizasyonlar/işletmeler ve üyelikler oluşturulur.
- Tenant bazlı veritabanı şeması ve erişim politikaları hazırlanır.
- Yönetici şoför hesabı açma işlemi güvenli sunucu fonksiyonu üzerinden yapılır.
- Onay, audit log, belge depolama ve yedekleme eklenir.

## Aşama 3 — Web paneli
- Giriş ve şifre sıfırlama
- Yönetici paneli, bekleyen kayıtlar, kullanıcılar, araçlar, finans ve raporlar
- Şoförün sefer/yakıt formları ve kendi kayıtlarının durumu

## Aşama 4 — Android APK
- Aynı backend'e bağlanan Android istemci oluşturulur.
- Uygulama simgesi FV amblemi olur.
- İmzalı APK/AAB derlenir; sürüm numarası ve güncelleme yöntemi belirlenir.

## Aşama 5 — Pilot test
- Önce FV Nakliye ve birkaç test hesabı kullanır.
- Yetki, tenant izolasyonu, onay, finans, yedekleme ve geri yükleme test edilir.
- Hata düzeltmeleri tamamlanır.

## Aşama 6 — Ticari yayın
- Alan adı, HTTPS, gizlilik metni, kullanım koşulları, destek süreci ve KVKK değerlendirmesi hazırlanır.
- Ücretsiz/ücretli paketler, ödeme sağlayıcısı ve abonelik yönetimi eklenir.
- Güvenlik değerlendirmesinden sonra halka açılır.

**Durum:** Bu ZIP bir geliştirme başlangıç paketidir. Aşamalar tamamlanmadan APK veya canlı SaaS hazır kabul edilmemelidir.
