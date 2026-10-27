# FV Nakliye V1 — Ürün ve kabul şartnamesi

## 1. Roller

### Yönetici
- Tüm şoförleri, seferleri ve yakıt kayıtlarını görebilir.
- Bekleyen kayıtları onaylayabilir, reddedebilir veya düzeltme isteyebilir.
- Kesinleşmiş kayıtlarda düzeltme yapabilir; eski/yeni değer ve işlem yapan kişi denetim kaydında tutulur.
- Ciro, gider, yakıt maliyeti, tahmini kâr ve raporları görür.
- Şoför hesaplarını oluşturur, devre dışı bırakır ve şifre sıfırlama akışını başlatır.
- Araç, yakıt fiyatı ve işletme ayarlarını yönetir.

### Şoför
- Yalnızca kendi hesabıyla giriş yapar.
- Sefer ve yakıt kaydı oluşturabilir.
- Kendi gönderdiği kayıtların durumunu görebilir: Beklemede, Onaylandı, Reddedildi, Düzeltme istendi.
- Finans ekranı, işletme kârı, diğer şoförlerin özel kayıtları ve kullanıcı yönetimine erişemez.
- Onaylanmış kaydı doğrudan değiştiremez veya silemez.

## 2. Sefer alanları
- Tarih/saat
- Araç
- Güzergâh: çıkış, varış/döküm sahası
- Yük miktarı (m³ veya ton; işletme ayarından seçilir)
- Sefer ücreti (şoför ekranında gösterilmezse yalnızca yönetici doldurabilir)
- Açıklama ve fiş/belge fotoğrafı
- Kaydı oluşturan kullanıcı, oluşturulma zamanı
- Durum, onaylayan kişi ve onay zamanı

## 3. Yakıt alanları
- Tarih/saat, araç, litre, litre fiyatı
- İstasyon/konum ve fiş fotoğrafı
- Açıklama
- Oluşturan kullanıcı ve zaman
- Durum, onaylayan kişi ve onay zamanı

## 4. Onay akışı
1. Şoför kaydı gönderir; kayıt `pending` durumundadır.
2. Yönetici bekleyenler listesinde kaydı ve ekleri inceler.
3. Yönetici onaylarsa `approved`, reddederse `rejected`, düzeltme isterse `changes_requested` olur.
4. Yalnızca `approved` kayıtlar kesin raporlara ve finans hesaplarına katılır.
5. Onay/ret ve sonradan yapılan yönetici düzeltmeleri denetim kaydına yazılır.

## 5. İlk sürüm ekranları
- Giriş
- Yönetici ana paneli
- Bekleyen kayıtlar / kayıt detayları
- Şoför sefer ekle
- Şoför yakıt ekle
- Kendi kayıtlarım ve durumları
- Araçlar ve ayarlar (yönetici)
- Finans ve raporlar (yönetici)
- Şoför hesapları (yönetici)

## 6. Güvenlik şartları
- Kayıt ve rol kontrolleri yalnızca arayüzde değil, veritabanı/sunucu tarafında da yapılır.
- Kullanıcı kendi rolünü değiştiremez.
- Şoför finans verilerine API üzerinden de erişemez.
- Kullanıcı oluşturma için yönetici yetkisi kontrol edilen sunucu tarafı fonksiyon kullanılır; servis anahtarı istemciye konulmaz.
- Parolalar düz metin olarak saklanmaz; kimlik doğrulama sağlayıcısı kullanılır.
- HTTPS, yedekleme ve denetim kaydı zorunludur.

## 7. V1 kabul testleri
- Şoför giriş yapıp sefer ve yakıt kaydı gönderebilir.
- Gönderilen kayıtlar yönetici onayından önce kesin raporlarda görünmez.
- Yönetici onayladığında kayıt raporlara girer.
- Şoför URL/API değiştirerek finans ekranına veya başka şoförün kayıtlarına erişemez.
- Şoför kendine yönetici rolü veremez.
- Yönetici bir şoför hesabını devre dışı bırakabilir.
- Web paneli ve Android uygulaması aynı kayıtları gösterir.
