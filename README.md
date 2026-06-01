TELCO CUSTOMER CHURN ANALİZİ VE TAHMİNLEME 
1. Giriş 
Bu projede müşteri kaybı problemi analiz edilmiştir. Amaç, müşterilerin hangi durumlarda şirketten 
ayrıldığını incelemek ve gelecekte ayrılabilecek müşterileri tahmin eden modeller oluşturmaktır. 
Çalışmada Orange Data Mining Tool kullanılmıştır. Veri yükleme ,veri temizleme,veri modelleme ve 
modeller arasinda karşılaştırma yapma gibi işlemler yapılmıştır. 
2. Veri Seti Tanıtımı 
Projede kullanılan veri seti “Telco Customer Churn” veri setidir. 
Veri setinde müşterilere ait: 
• cinsiyet,  
• internet hizmeti,  
• sözleşme tipi,  
• aylık ödeme,  
• toplam ödeme,  
• müşteri şirkette kalma süresi (tenure) 
gibi bilgiler bulunmaktadır.  
Hedef değişken “Churn” sütunudur. 
• Churn = Yes → müşteri ayrılmış  
• Churn = No → müşteri şirkette kalmıştır 
Veri setinin Orange Data Table üzerindeki görünümü
<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/bced099e-b4c5-49cb-972b-1d5a2fd49ef2" />


4. Veri Ön İşleme (Preprocessing) 
İlk olarak veri seti Datasets kullanılarak Orange yüklenmiştir. 
Daha sonra Data Table ile veri incelenmiştir. 
Yapılan incelemede “TotalCharges” sütununun sayısal veri olmasına rağmen text olarak algılandığı 
görülmüştür. Bunun nedeni bazı satırlarda boş değer bulunmasıdır. Orange boş değer içeren sayısal 
sütunları bazen metin olarak algılayabilmektedir. 
Eksik verileri düzeltmek için Impute araç’i kullanılmıştır. Boş değerler ortalama değer yöntemi ile 
doldurulmuştur. 
Ardından Select Columns ile customerID sütunu kaldırılmıştır.  
Temizlenmiş veri tekrar Data Table üzerinde kontrol edilmiştir ve save date ile excel üzerine 
kaydedılmıştır.
<img width="647" height="678" alt="image" src="https://github.com/user-attachments/assets/2fdcec71-a811-4556-a32c-aaf8303b0db1" />

TEMİZLENMİŞ VERİ: 
temizlenmiş veri.xlsx  
6. Görsel Veri Analizi  
 Contract ve Churn İlişkisi 
Distributions  kullanılarak sözleşme tipi ile müşteri ayrılması arasındaki ilişki incelenmiştir. 
Analiz sonucunda: 
• Aydan aya ücret ödeyen müşteri sözleşmesıne sahip müşterilerin ayrılma oranının daha 
yüksek olduğu,  
• Yıldan yıla ücret ödeyen müşteri sözleşmesıne sahip müşterilerin ise şirkette daha uzun süre 
kaldığı görülmüştür.  
Bu durum uzun süreli sözleşmelerin müşteri sadakatini artırdığını göstermektedir. 
<img width="1146" height="748" alt="image" src="https://github.com/user-attachments/assets/2c503080-b12c-4ee0-9626-fa396491d39f" />

MonthlyCharges ve Tenure Analizi 
Scatter Plot kullanılarak MonthlyCharges ve Tenure değişkenleri Churn değerine göre 
renklendirilmiştir. 
Grafikte: 
Yüksek aylık ödeme yapan,fakat şirkette kısa süre kalan müşterilerin daha fazla ayrıldığı görülmüştür.  
Uzun süreli müşterilerde ise ayrılma oranı daha düşük gözlemlenmiştir. 
<img width="1282" height="759" alt="image" src="https://github.com/user-attachments/assets/7b7ffefb-4990-448c-8d46-fddce3d8a78f" />

7. Modelleme 
Temizlenmiş veri Data Sampler ile: 
• %80 eğitim verisi,  
• %20 test verisi 
olacak şekilde ayrılmıştır.  
Daha sonra üç farklı makine öğrenmesi algoritması kullanılmıştır: 
• Logistic Regression  
• Decision Tree  
• Random Forest  
Modeller Test and Score widget’ına bağlanarak performansları karşılaştırılmıştır. 
8. Model Sonuçları
   <img width="977" height="664" alt="image" src="https://github.com/user-attachments/assets/d82b2a7e-d237-4f02-b4a8-b8fdccbecc54" />

Sonuçlara göre en başarılı model logistic regression olmuştur 
 Confusion Matrix Analizi 
Confusion Matrix kullanılarak modelin hata yaptığı tahminler incelenmiştir. 
False Positive değeri: 
• sistemin “müşteri ayrılacak” dediği  
• fakat gerçekte ayrılmayan müşeti tiplerini göstermektedir 
<img width="940" height="464" alt="image" src="https://github.com/user-attachments/assets/9a1df94c-bd13-4e5f-af16-282dda2dedfe" />

9. Sonuç ve Genel Değerlendirme 
Bu projede müşteri kaybı problemi Orange Data Mining Tool kullanılarak analiz edilmiştir. 
Yapılan analizlerde: 
• kısa süreli sözleşmelerin,  
• yüksek aylık ücretlerin,  
• düşük müşteri sadakatinin 
müşteri kaybını artırdığı görülmüştür. 
10.SORULAR  
Soru 1: 
TotalCharges sütunundaki sayısal değerlerin neden text olarak algılandığını açıklayınız. 
Cevap: 
TotalCharges sütununda boş değerler bulunduğu için Orange bu sütunu text olarak algılamıştır. Eksik 
değerler temizlendikten sonra sütun sayısal olarak kullanılabilmiştir. 
Soru 2: 
customerID sütunu neden kaldırılmıştır? 
Cevap: 
customerID sütunu her müşteri için benzersiz olduğu için tahminleme açısından anlamlı bilgi 
sağlamamaktadır. Bu nedenle modelden çıkarılmıştır. 
Soru 3: 
Şirket için en riskli müşteri profili nedir? 
Cevap: 
Kısa süreli üyeliğe sahip, yüksek aylık ödeme yapan, month-to-month sözleşmeli 
Soru 4: 
En başarılı model hangisidir? 
Cevap: 
AUC ve Classification Accuracy değerlerine göre en başarılı model logistic regression olmuştur  
