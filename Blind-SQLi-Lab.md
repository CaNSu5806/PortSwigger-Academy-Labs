#  Blind SQL Injection (Conditional Responses) - Writeup

Bu depo, **PortSwigger Web Security Academy** üzerinde tamamladığım "Blind SQL injection with conditional responses" laboratuvarının teknik çözüm sürecini içerir.

##  Laboratuvar Özeti
Uygulamanın `TrackingId` çerezi üzerinden SQL Injection'a izin verdiği, ancak sonuçların doğrudan ekrana yansımadığı bir senaryo üzerinde çalışılmıştır. Veritabanından gelen yanıtın "Doğru" veya "Yanlış" olmasına göre sayfa içeriğinin değişmesi (örneğin "Welcome back" yazısının görünmesi) sömürülerek veriler karakter karakter sızdırılmıştır.



## 🛠️ Teknik Süreç

### 1. Zafiyet Tespiti
Aşağıdaki mantıksal sorgularla uygulamanın tepkisi ölçülmüştür:
* `' AND (1=1)--` -> Sayfada "Welcome back" mesajı görünür.
* `' AND (1=2)--` -> Mesaj kaybolur.

### 2. Veri Sızdırma (Exfiltration)
`administrator` kullanıcısının şifresini karakter karakter çekmek için **Burp Suite Intruder** (Sniper Attack) kullanılmıştır.

**Kullanılan Payload:**
```sql
' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='§a§'
