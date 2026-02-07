# Lab: SQL injection UNION attack, retrieving data from other tables

## Hedef
Ürün kategorisi filtresindeki SQL enjeksiyon zafiyetini kullanarak `users` tablosuna erişmek ve `administrator` kullanıcısının parolasını ele geçirmek.

## Çözüm Süreci

### Adım 1: Sütun Sayısını ve Tipini Belirleme
Önceki tekniklerle (ORDER BY ve NULL denemeleri) sorgunun 2 sütun döndürdüğünü ve her iki sütunun da metin (string) verisi kabul ettiğini doğruladım.
- Payload: `' UNION SELECT 'abc', 'def'--`

### Adım 2: Tablo Yapısını Anlama
Veritabanı dökümantasyonundan  kullanıcı bilgilerinin `users` tablosunda, kullanıcı adlarının `username` ve şifrelerin `password` sütunlarında tutulduğunu öğrendim.

### Adım 3: Verileri Çekme
`UNION SELECT` komutunu kullanarak orijinal ürün listesinin altına `users` tablosundaki tüm verileri ekledim:
- **Payload:** `' UNION SELECT username, password FROM users--`

### Adım 4: Sonuç
Gelen cevap (Response) içinde `administrator` kullanıcısının yanındaki şifreyi buldum ve bu şifreyle giriş yaparak laboratuvarı tamamladım.

## Kullanılan Araçlar
- Burp Suite Repeater
- SQL Injection (UNION-based)
