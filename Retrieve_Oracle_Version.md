Zafiyet: Oracle Database Fingerprinting via SQL Injection. 

Öğrenilen Mantık:

Oracle'da her SELECT bir tabloya (FROM) ihtiyaç duyar.

Sistem bilgileri v$version tablosunda saklanır.

Sütun sayısı tespiti için ORDER BY tekniği uygulandı.

Veri sızıntısı için UNION SELECT ile orijinal sorgu manipüle edildi.
