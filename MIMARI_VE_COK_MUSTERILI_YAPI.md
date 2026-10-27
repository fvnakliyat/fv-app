# Mimari: büyüyebilir ve çok müşterili FV Nakliye

## Hedef
İlk kullanım FV Nakliye işletmesinde başlar; ileride başka nakliye şirketleri, tek araçlı esnaf veya bağımsız kullanıcılar da kayıt olabilir. Her müşteri ayrı bir çalışma alanıdır (tenant). Bir müşterinin kullanıcıları başka müşterinin verisini asla göremez.

## Önerilen katmanlar
1. **Android istemci:** APK; aynı API'yi kullanır.
2. **Web paneli:** masaüstü ve mobil tarayıcı; aynı API'yi kullanır.
3. **Kimlik doğrulama:** güvenli parola/oturum sağlayıcısı. Parola düz metin tutulmaz.
4. **Sunucu/API:** yetki ve iş kurallarının tek merkezi.
5. **PostgreSQL veritabanı:** kayıtların ortak kaynağı.
6. **Dosya depolama:** fiş ve belge fotoğrafları; erişim imzalı/kısa ömürlü bağlantılarla verilir.
7. **Denetim ve yedekleme:** onaylar, rol değişiklikleri ve kritik düzenlemeler kaydedilir.

## Roller
- `platform_owner`: ürünü işleten kişi; platform ayarları ve destek işlemleri. Müşteri finansını varsayılan olarak görmemeli.
- `business_owner`: kendi işletmesinde kullanıcı, araç, onay, finans ve rapor yönetimi.
- `driver`: kendi sefer/yakıt kayıtlarını gönderir ve durumlarını görür.
- İleride `accountant`, `dispatcher`, `read_only` gibi izinleri ayrı ayrı tanımlamak mümkün olmalı.

Rol adları tek başına güvenlik değildir: sunucu her istekte kullanıcı kimliğini, işletme üyeliğini ve işlem iznini kontrol etmelidir.

## Çok müşterili veri modeli
Temel tablolar tenant/işletme kimliği taşımalıdır:
- `organizations` (müşteri işletmeler)
- `organization_members` (kullanıcı-işletme üyeliği ve rol)
- `vehicles`, `trip_submissions`, `fuel_submissions`, `expenses`, `audit_log` (her kayıtta `organization_id`)
- `subscriptions` ve `plans` (ileride ücretli paketler için)
- `feature_flags` (özellikleri kademeli açmak için)

Bütün okuma/yazma politikaları `organization_id` ve üyelik üzerinden sınırlandırılmalıdır. İstemciden gelen `organization_id` tek başına güvenilir kabul edilmemelidir; sunucu oturumdaki kullanıcının üyeliğini doğrulamalıdır. Birincil/benzersiz anahtarlar ve ilişkilerde de tenant sınırları gözetilmelidir.

## Onay ve finans kuralları
- Şoförün gönderdiği kayıt `pending` olur.
- Yalnızca işletmenin `business_owner` rolü (ve ileride izin verilmiş yetkili) onaylar.
- Yalnızca `approved` kayıtlar kesin rapor/finans hesaplarına girer.
- Reddedilen veya düzeltme istenen kayıtlar gerekçesiyle saklanır.
- Onaylanmış kayıt değişirse eski ve yeni değer, kullanıcı, zaman ve gerekçe denetim kaydına yazılır.
- Ürün sahibi/platform yöneticisi, destek amacıyla müşteri verisine erişecekse bu işlem açık yetki, gerekçe ve denetim kaydı gerektirmelidir.

## Ücretli ürün için ileride eklenebilecekler
- Ücretsiz/ücretli planlar ve araç/kullanıcı limitleri
- Abonelik durumu ve fatura entegrasyonu
- Deneme süresi, iptal ve dışa aktarma
- Her müşteri için logo/renk/şirket bilgisi (white-label seçenekleri)
- E-posta/SMS bildirimleri
- Birden fazla araç, depo, şube ve yetki grupları
- İthalat/ihracat, CSV/Excel raporları, muhasebe entegrasyonu
- API anahtarları ve üçüncü taraf entegrasyonları (yalnızca güvenli kapsam ve limitlerle)

## Sağlamlık ilkeleri
- Sunucu anahtarları APK veya web istemcisine koyulmaz.
- Veritabanı değişiklikleri sürümlü migration dosyalarıyla yapılır.
- Test, staging ve production ortamları ayrılır.
- Otomatik testler: tenant izolasyonu, rol sınırları, onay akışı, finans erişimi, yedek geri yükleme.
- Veri dışa aktarma ve hesabı kapatma/silme süreçleri tasarlanır.
