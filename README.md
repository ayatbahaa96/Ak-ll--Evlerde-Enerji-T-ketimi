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

<img width="585" height="565" alt="image" src="https://github.com/user-attachments/assets/7d3b42ee-f6bc-4ac0-acfb-a30be227e8a5" /> 

<img width="792" height="610" alt="image" src="https://github.com/user-attachments/assets/21744fb7-1924-42bf-bb15-77b27ffeaba3" />


Veri kümesi başlangıçta her aygıt için ayrı sütunlar içerir. Cihaz tabanlı analizi etkinleştirmek için veriler uzun bir formata dönüştürüldü. Bu dönüşüm, her satırın belirli bir zamanda tek bir cihazın tüketimini temsil etmesini sağlar.

<img width="762" height="691" alt="image" src="https://github.com/user-attachments/assets/3ed14c73-7c64-4d73-afe9-bd9801088ba6" />


# Pivot Tablosu ve Baseline Oluşturma

Cihazların enerji tüketimleri birbirinden oldukça farklıdır. Örneğin bazı cihazlar sürekli düşük enerji tüketirken, bazıları belirli saatlerde yüksek tüketim yapmaktadır. Bu nedenle tüm cihazlar için tek bir ortalama değer kullanmak doğru sonuçlar vermemektedir.

Bu problemi çözmek için pivot tablo kullanılmıştır. Pivot tablo ile her cihaz için:

**günün saati**

**sıcaklık aralığı**

<img width="747" height="327" alt="image" src="https://github.com/user-attachments/assets/2e688af2-afc6-4693-b0b9-a21196e88885" />

bazında ortalama enerji tüketimi ve standart sapma değerleri hesaplanmıştır. Bu değerler, cihazların normal tüketim davranışını temsil eden baseline olarak kabul edilmiştir.

<img width="875" height="286" alt="image" src="https://github.com/user-attachments/assets/47ca0772-eddd-4fcf-8aa7-db513458f43c" />


# Anomali Tanımı

Anormal tüketimler z-score yöntemi kullanılarak belirlenmiştir. Gerçek tüketim değeri ile pivot tablo üzerinden hesaplanan ortalama değer arasındaki fark, standart sapmaya bölünerek z-score elde edilmiştir.

Belirli bir eşik değerin (|z| > 2) üzerinde olan tüketimler anormal olarak etiketlenmiştir. Bu yöntem sayesinde her cihaz kendi normal davranışına göre değerlendirilmiştir.

<img width="877" height="522" alt="image" src="https://github.com/user-attachments/assets/e01adea4-fb4b-4b56-a27a-092a0bd960e9" />


# Makine Öğrenmesi Modeli

Anomali tespiti için Random Forest sınıflandırma modeli kullanılmıştır, Pivot tablo ile elde edilen baseline özellikleri kullanılarak ve pivot tablo kullanılan modelin anormal tüketimleri iyi sonuç vermiştir.

<img width="757" height="376" alt="image" src="https://github.com/user-attachments/assets/594852be-99c4-49db-ad35-7917efe9f723" />

<img width="961" height="115" alt="image" src="https://github.com/user-attachments/assets/d1dcff67-0325-49b2-8608-5ef1b3098351" />

<img width="650" height="367" alt="image" src="https://github.com/user-attachments/assets/ca74be43-a758-4a39-8cb2-1892ddc1706d" />

# Sonuç

Elde edilen sonuçlara göre, pivot tablo kullanılarak oluşturulan taban değerleri, cihazların normal davranışını doğru bir şekilde temsil etmektedir. Bu, makine öğrenimi modelinin anormal tüketimi doğru bir şekilde algılamasını sağladı.

<img width="547" height="497" alt="image" src="https://github.com/user-attachments/assets/30a91d8c-fa06-4f22-bcdd-699672e323fb" />



