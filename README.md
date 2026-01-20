# Akıllı Evlerde Enerji Tüketimi Anomali Analizi

# Proje Açıklaması

Bu projede akıllı evlerde kullanılan elektrikli cihazların enerji tüketimleri incelenmiştir. Amaç, cihazların normal kullanım davranışlarının dışına çıktığı durumları tespit etmektir. Bunun için enerji tüketim verileri ve hava durumu bilgileri birlikte kullanılmıştır.

Çalışma kapsamında, cihazların farklı saatlerde ve farklı hava koşullarında gösterdikleri tüketim davranışları dikkate alınmıştır. Bu nedenle her cihaz için tek bir normal değer kullanmak yerine, bağlama göre değişen referans değerler oluşturulmuştur.

# Kullanılan Veri Seti

Bu projede Kaggle üzerinde paylaşılan Smart Home Energy Consumption and Weather Data veri seti kullanılmıştır.

Veri seti şu bilgileri içermektedir:

**1** Cihazlara ait enerji tüketimleri (kW)
**2** Zaman bilgisi (Unix timestamp)
**3** Hava durumu değişkenleri (sıcaklık, nem vb.)
