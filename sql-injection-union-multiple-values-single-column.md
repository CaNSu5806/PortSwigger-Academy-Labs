# Lab: SQL injection UNION attack, retrieving multiple values in a single column

## Hedef
Ürün kategorisi filtresindeki SQL enjeksiyon zafiyetini kullanarak, veritabanındaki `users` tablosundan tüm kullanıcı adlarını ve şifrelerini çekmek. Bu labda zorluk, orijinal sorgunun sadece tek bir metin (string) sütunu döndürmesidir.

## Çözüm Süreci

### Adım 1: Sütun Sayısını ve Tipini Belirleme
Önceki lablardaki teknikleri kullanarak sorgunun kaç sütun döndürdüğünü ve hangisinin metin kabul ettiğini belirledim. Bu senaryoda sadece tek bir sütun metin verisi kabul ediyordu.

### Adım 2: String Concatenation (Metin Birleştirme)
Elde etmek istediğim iki farklı veriyi (kullanıcı adı ve şifre) tek bir sütuna sığdırmak için "String Concatenation" yöntemini kullandım. Farklı veritabanları için farklı operatörler gerekse de, bu laboratuvarda Oracle/PostgreSQL tarzı birleştirme operatörünü (`||`) tercih ettim.

### Adım 3: Payload Oluşturma
Kullanıcı adlarını ve şifreleri aralarına bir ayraç (örneğin `~`) koyarak birleştirdim. Bu sayede dönen sonuçta hangi kısmın kullanıcı adı, hangi kısmın şifre olduğu kolayca anlaşılabiliyordu.

- **Kullanılan Payload:** `' UNION SELECT NULL, username || '~' || password FROM users--`

### Adım 4: Veri Sızdırma ve Giriş
Dönen sonuçlar arasından `administrator` kullanıcısına ait satırı buldum:
`administrator~s3cr3tp4ss`

Buradaki şifreyi alarak administrator hesabına giriş yaptım ve laboratuvarı tamamladım.

## Teknik Notlar
- **String Concatenation:** Veritabanının döndürdüğü sütun sayısı kısıtlı olduğunda birden fazla veriyi tek seferde çekmek için hayati bir tekniktir.
- **Delimiter (Ayraç):** Çekilen verileri birbirinden ayırmak için `~`, `:` veya `-` gibi özel karakterler kullanılır.

## Kullanılan Araçlar
- Burp Suite (Repeater)
- SQL Injection (UNION-based)
