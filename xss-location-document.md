Laboratuvar Özeti
Bu lab, jQuery kütüphanesinin URL'den aldığı veriyi (location.search), bir linkin adres kısmına (href) hiçbir denetim yapmadan yerleştirmesiyle oluşan DOM-based XSS zafiyetini gösterir. Etiket açmaya (<script>) gerek kalmadan, doğrudan linkin çalışma mantığı manipüle edilmiştir.

Teknik Süreç
1. Analiz (Source & Sink)

Kaynak (Source): URL'deki returnPath parametresi.

Alıcı (Sink): jQuery'nin .attr('href', ...) fonksiyonu.

Durum: URL'ye ne yazarsan linkin href özniteliğine o biniyor.

2. Sömürme (Exploitation)
Normal bir URL yerine JavaScript protokolü kullanılarak kod enjekte edilmiştir:

Payload: ?returnPath=javascript:alert(document.cookie)

3. Tetikleme

Kullanıcı sayfadaki "Back" (Geri) linkine tıkladığı an, tarayıcı bir sayfaya gitmek yerine javascript: komutunu algılar ve alert() fonksiyonunu çalıştırır.
