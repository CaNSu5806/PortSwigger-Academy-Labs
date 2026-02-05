# Lab: SQL injection vulnerability allowing login bypass

### Zafiyet Tanımı
Bu laboratuvar, kullanıcı giriş formunda bir SQL enjeksiyon zafiyeti barındırmaktadır. Bu açık, veritabanı sorgusunun mantığını manipüle ederek geçerli bir şifre olmadan sisteme erişmeyi mümkün kılar.

### Çözüm Adımları
1. Giriş sayfası Burp Suite ile analiz edildi.
2. `POST /login` isteği yakalanarak **Repeater** sekmesine gönderildi.
3. Kullanıcı adı (username) alanına `administrator'--` payload'u eklendi.
4. Buradaki `'` işareti mevcut SQL sorgusunu sonlandırmak, `--` ise şifre kontrolü yapan kısmın yorum satırı olarak algılanmasını sağlamak için kullanıldı.
5. İstek gönderildiğinde sunucudan `302 Found` yanıtı alındı ve yönetici olarak giriş yapıldı.

### Teknik Detaylar
- **Payload:** `administrator'--`
- **Etkilenen Parametre:** `username`

- <img width="875" height="760" alt="Ekran görüntüsü 2026-02-05 144150" src="https://github.com/user-attachments/assets/d9dd7cbd-e020-4057-ae6e-bf1710bec44a" />
