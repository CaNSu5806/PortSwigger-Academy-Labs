Lab: SQL injection attack, listing the database contents on non-Oracle databases
Zafiyet Özeti
Bu laboratuvarda, PostgreSQL tabanlı bir uygulamada SQL enjeksiyonu kullanarak veritabanı şemasını (schema) enumerate ettim ve yönetici (administrator) bilgilerini başarıyla sızdırdım (exfiltrate). Dinamik ve rastgele isimlendirilmiş tabloların bulunduğu ortamlarda veriye nasıl ulaşılacağını deneyimledim.

Teknik Analiz ve Çözüm Süreci
Sütun Sayısı ve Veri Tipi Tespiti: ORDER BY ve UNION SELECT 'a', 'b'-- tekniklerini kullanarak orijinal sorgunun 2 sütun döndürdüğünü ve her iki sütunun da metin (string) verisi kabul ettiğini doğruladım.

Dinamik Tablo İsminin Tespiti: Veritabanındaki yüzlerce sistem tablosu arasından hedef tabloyu bulmak için information_schema.tables yapısını ve LIKE operatörünü kullandım: ' UNION SELECT table_name, NULL FROM information_schema.tables WHERE table_name LIKE 'users_%'-- Bu sorgu sonucunda laboratuvara özel oluşturulan users_kcxusp (veya senin bulduğun isim) tablosunu tespit ettim.

Sütun İsimlerinin Numaralandırılması (Enumeration): Hedef tablodaki kullanıcı adı ve şifre sütunlarının isimlerini öğrenmek için şu sorguyu çalıştırdım: ' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name = 'users_kcxusp'-- Buradan username_... ve password_... formatındaki sütun isimlerine ulaştım.

Veri Sızıntısı (Exfiltration): Elde ettiğim kesin tablo ve sütun isimlerini birleştirerek administrator kullanıcısının kimlik bilgilerini sızdırdım: ' UNION SELECT username_column, password_column FROM users_kcxusp--

Öğrenilen Teknikler
Information Schema: Veritabanı meta-verilerine erişim ve haritalama.

Filtreleme: LIKE operatörü ile gürültülü veriler arasından hedefi seçme.

HTML Entity Handling: Yanıtlardaki &apos; (tek tırnak) gibi kodlamaları çözümleme.

URL Encoding: Özel karakterlerin (', --, +) sunucuya bozulmadan iletilmesi için Ctrl+U kullanımı.
