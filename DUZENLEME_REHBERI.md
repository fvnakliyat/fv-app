# Kaynakları kendin düzenleyebilmen için rehber

## Düzenleme prensipleri
- Kaynak kodu sakla; sadece APK dosyasını saklamak yeterli değildir.
- Her değişiklikten önce yedek al ve mümkünse Git gibi bir sürüm kontrol sistemi kullan.
- Geliştirme, test ve canlı ortamları ayrı tut.
- Şema değişikliklerini eski dosyayı ezerek değil yeni migration dosyası oluşturarak yap.
- Şifre, servis anahtarı, veritabanı parolası ve imzalama anahtarını kaynak koda veya ZIP'e koyma.
- İstemcide ekranı gizlemek güvenlik sağlamaz; izinler sunucu tarafında da kontrol edilmelidir.

## Özelleştirmesi kolay tutulacak alanlar
- İşletme adı, logo, renkler ve iletişim bilgileri
- Araç türleri, plaka, kapasite ve tüketim varsayımları
- Sefer formu alanları ve ölçü birimleri
- Yakıt türleri ve gider kategorileri
- Onay adımları
- Rapor filtreleri ve dışa aktarma biçimleri
- Kullanıcı rolleri/izinleri
- Abonelik planları ve özellik limitleri

## Yeni özellik ekleme yöntemi
1. Kullanıcı ihtiyacını ve rolünü tanımla.
2. Veri alanlarını ve gizlilik etkisini belirle.
3. Yeni bir veritabanı migration dosyası ekle.
4. API doğrulamasını ve tenant/rol politikasını yaz.
5. Web ve Android arayüzlerini aynı API'ye bağla.
6. Normal kullanıcı, başka işletme kullanıcısı ve yönetici testlerini çalıştır.
7. Test ortamında onaylandıktan sonra sürüm yayınla.

## Kimlik ve hesaplar
Yönetici hesabı güvenli kimlik sağlayıcısında açılır. Şoför hesapları sunucu tarafı yönetici işlemiyle oluşturulur veya davet edilir. Kullanıcı rolü doğrudan istemciden değiştirilemez. Çok faktörlü kimlik doğrulama, parola sıfırlama ve oturum kapatma akışları canlı sürüm öncesinde eklenmelidir.
