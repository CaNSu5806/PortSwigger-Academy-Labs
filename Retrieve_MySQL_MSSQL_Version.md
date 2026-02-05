# Lab: SQL injection vulnerability - Querying the database type and version on MySQL and Microsoft

### **Zafiyet Özeti**
Bu laboratuvarda, MySQL ve Microsoft SQL Server tabanlı sistemlerde veritabanı türünü ve sürümünü sızdırmak için SQL enjeksiyon tekniklerini kullandım.

### **Teknik Detaylar ve Çözüm**
Farklı veritabanı yönetim sistemlerinin (DBMS) kendine has sözdizimi (syntax) kuralları olduğu için şu adımları izledim:

1.  **Sütun Tespiti:** `ORDER BY` yöntemiyle sorgunun kaç sütun döndürdüğünü ve hangi sütunların metin (string) verisi kabul ettiğini belirledim.
2.  **Sürüm Sorgulama:** * **Microsoft (MSSQL)** için: `' UNION SELECT @@VERSION, NULL--` payload'unu kullandım.
    * **MySQL** için: `' UNION SELECT VERSION(), NULL#` payload'unu kullandım.
3.  **Yorum Satırları:** MySQL'de sorgunun geri kalanını etkisiz hale getirmek için `#` karakterinin kullanımını deneyimledim.

### **Öğrenilenler**
- Veritabanı "fingerprinting" (parmak izi belirleme) sürecinde DBMS'e özgü fonksiyonların (`VERSION()` vs `@@VERSION`) önemi.
- URL encoding'in (Ctrl+U) özel karakterlerin iletimindeki kritik rolü.
