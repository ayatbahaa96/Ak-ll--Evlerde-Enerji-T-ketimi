# Akıllı Evlerde Enerji Tüketimi Anomali Analizi

# Proje Açıklaması

Bu proje akıllı evlerde kullanılan elektrikli cihazların enerji tüketimini inceliyor. Amaç, cihazların normal kullanım davranışlarından saptığı durumları belirlemektir.Bu amaçla enerji tüketim verileri ve hava durumu bilgileri birlikte kullanılmıştır.

Çalışma, cihazların farklı zamanlarda ve farklı hava koşullarında tüketim davranışlarını değerlendirdi. Bu nedenle, her aygıt için tek bir normal değer kullanmak yerine, bağlamsal olarak değişken referans değerleri oluşturuldu.

# Kullanılan Veri Seti

Bu projede Kaggle üzerinde paylaşılan Smart Home Energy Consumption and Weather Data veri seti kullanılmıştır.

Veri seti şu bilgileri içermektedir:

**1-** Cihazlara ait enerji tüketimleri (kW)

**2-** Zaman bilgisi (Unix timestamp)

**3-** Hava durumu değişkenleri (sıcaklık, nem vb.)

# Problem Tanımı

Problem, enerji tüketimlerinin normal mi yoksa anormal mi olduğunu belirlemek şeklinde ele alınmıştır.

**0 → Normal tüketim**

**1 → Anormal tüketim**

Bu nedenle problem bir ikili sınıflandırma (binary classification) problemi olarak modellenmiştir.

# Veri Ön İşleme

İlk olarak, zaman bilgisi Unıx zaman damgası biçiminden tarih-saat biçimine dönüştürüldü.  Daha sonra bu bilgilerden günün saati ve haftanın günü gibi ek özellikler çıkarıldı

Öncelikle zaman bilgisi Unix timestamp formatından tarih-saat formatına dönüştürülmüştür. Daha sonra bu bilgiden günün saati ve haftanın günü gibi ek özellikler çıkarılmıştır.

Veri kümesi başlangıçta her aygıt için ayrı sütunlar içerir. Cihaz tabanlı analizi etkinleştirmek için veriler uzun bir formata dönüştürüldü. Bu dönüşüm, her satırın belirli bir zamanda tek bir cihazın tüketimini temsil etmesini sağlar.
<img width="585" height="565" alt="image" src="https://github.com/user-attachments/assets/7d3b42ee-f6bc-4ac0-acfb-a30be227e8a5" />




# Pivot Tablosu ve Baseline Oluşturma

Cihazların enerji tüketimleri birbirinden oldukça farklıdır. Örneğin bazı cihazlar sürekli düşük enerji tüketirken, bazıları belirli saatlerde yüksek tüketim yapmaktadır. Bu nedenle tüm cihazlar için tek bir ortalama değer kullanmak doğru sonuçlar vermemektedir.

Bu problemi çözmek için pivot tablo kullanılmıştır. Pivot tablo ile her cihaz için:

**günün saati**

**sıcaklık aralığı**

bazında ortalama enerji tüketimi ve standart sapma değerleri hesaplanmıştır. Bu değerler, cihazların normal tüketim davranışını temsil eden baseline olarak kabul edilmiştir.

# Anomali Tanımı

Anormal tüketimler z-score yöntemi kullanılarak belirlenmiştir. Gerçek tüketim değeri ile pivot tablo üzerinden hesaplanan ortalama değer arasındaki fark, standart sapmaya bölünerek z-score elde edilmiştir.

Belirli bir eşik değerin (|z| > 2) üzerinde olan tüketimler anormal olarak etiketlenmiştir. Bu yöntem sayesinde her cihaz kendi normal davranışına göre değerlendirilmiştir.

# Makine Öğrenmesi Modeli

Anomali tespiti için Random Forest sınıflandırma modeli kullanılmıştır, Pivot tablo ile elde edilen baseline özellikleri kullanılarak ve pivot tablo kullanılan modelin anormal tüketimleri iyi sonuç vermiştir.

