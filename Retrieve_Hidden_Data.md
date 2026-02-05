Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
Zafiyet Özeti
Bu laboratuvarda, ürün kategori filtresindeki bir parametrenin SQL sorgusuna doğrudan eklenmesi sonucu oluşan SQL enjeksiyon zafiyetini sömürdüm. Bu açık, normalde kullanıcıların görmemesi gereken "yayınlanmamış" ürünlerin veritabanından çekilmesine olanak tanıyor.

Teknik Analiz ve Çözüm
Uygulamanın arka planda çalıştırdığı zayıf sorgu yapısı muhtemelen şöyledir: SELECT * FROM products WHERE category = '[KATEGORİ]' AND released = 1

Buradaki released = 1 kısıtlamasını aşmak için şu adımları izledim:

Payload: Kategori parametresine ' OR 1=1-- ifadesini ekledim.

Mantık: * ' ile kategori metnini kapattım.

OR 1=1 ekleyerek sorgunun her zaman "doğru" (True) dönmesini sağladım.

-- ile sorgunun geri kalanındaki kısıtlamaları (yayınlanmış ürün kontrolü) yorum satırına dönüştürerek devre dışı bıraktım.

Sonuç: Veritabanındaki tüm gizli veriler başarıyla listelendi.
