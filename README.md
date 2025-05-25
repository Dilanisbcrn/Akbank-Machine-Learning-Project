Akbank Makine Öğrenmesi Projesi – Yağmur Tahmini
Bu proje, Akbank ve Global AI Hub iş birliğiyle düzenlenen Makine Öğrenmesine Giriş Bootcamp kapsamında, denetimli öğrenme yaklaşımıyla gerçekleştirdiğim bir sınıflandırma projesidir. Projenin amacı, geçmiş hava durumu verilerini kullanarak ertesi gün yağmur yağıp yağmayacağını tahmin etmek ve farklı algoritmalarla bu sınıflandırma problemini çözmeye çalışmaktır.

Kullanılan Veri Seti
Projede kullandığım veri seti, Kaggle platformunda yer alan Weather Dataset from Rattle Package adlı açık veri setidir. Bu veri seti, Avustralya'nın farklı bölgelerinde ölçülen günlük hava durumu bilgilerini içermektedir.

Toplam örnek sayısı yaklaşık 145.000

24 adet değişken

Hedef değişken: RainTomorrow (Yarın yağmur yağacak mı? Evet/Hayır)

Veri setinde sıcaklık, nem, rüzgar yönü, yağış miktarı gibi hava durumu ile ilgili birçok parametre yer almaktadır.

Veri Ön İşleme Süreci
İlk olarak veri setini genel olarak inceledim ve eksik değerlerin yoğunlukta olduğu sütunları belirledim. Bu doğrultuda:

Bulut verileri gibi çok fazla eksik veri içeren sütunlar veri setinden çıkarıldı.

Diğer eksik veriler ise uygun istatistiksel yöntemlerle medyan ile dolduruldu.

Kategorik değişkenler sayısal formata çevrildi. RainToday ve RainTomorrow sütunları label encoding ile; WindGustDir, WindDir9am, WindDir3pm gibi sütunlar ise one-hot encoding yöntemiyle dönüştürüldü.

Değişkenler arasındaki ilişkiyi görmek için korelasyon matrisi oluşturuldu.

Veri ön işleme adımı tamamlandıktan sonra veriyi modellemeye uygun hale getirmiş oldum.

Modelleme ve Uygulanan Algoritmalar
Veri setini %80 eğitim ve %20 test olacak şekilde ikiye ayırdıktan sonra üç farklı sınıflandırma algoritması üzerinde çalıştım:

Random Forest Classifier

Logistic Regression

Decision Tree Classifier

Modelleri değerlendirmek için sadece doğruluk skoruna bakmakla yetinmedim, aynı zamanda precision, recall gibi sınıflandırma metriklerini de inceledim. Ayrıca modellerin güvenilirliğini artırmak adına cross-validation uyguladım.

Doğruluk Skorları
Model	Doğruluk
Random Forest	0.843
Logistic Regression	0.838
Decision Tree	0.774

Bu sonuçlara göre en iyi performansı Random Forest modeli gösterdi.

Precision / Recall Değerleri (Random Forest)
Yağmur yağmayacak (No):
Precision: 0.87 – Recall: 0.95

Yağmur yağacak (Yes):
Precision: 0.74 – Recall: 0.49

Model, özellikle yağmurun yağmayacağı durumları oldukça başarılı bir şekilde tahmin etti. Yağmur yağacak sınıfı ise hem örnek sayısının azlığı hem de verinin dengesiz doğası nedeniyle daha zor tahmin edildi.

Model Seçimi ve Değerlendirme
Elde ettiğim sonuçlar doğrultusunda, Random Forest modeli, bu problem için en uygun algoritma olarak öne çıktı. Hem genel doğruluk oranı hem de istikrarlı sonuçlar vermesi sebebiyle diğer modellerin önüne geçti.

Ek olarak:

Confusion Matrix (karmaşıklık matrisi) ile modelin hangi sınıflarda başarılı ya da başarısız olduğunu görselleştirdim.

Özellik önem düzeylerini inceleyerek modelin karar verirken en çok hangi değişkenlere ağırlık verdiğini analiz ettim. Bu analiz sonucunda en önemli değişkenlerin sırasıyla Humidity3pm, Pressure3pm, Humidity9am ve WindGustSpeed olduğu görüldü.

Projeden Elde Ettiklerim
Bu proje sayesinde:

Gerçek bir veri seti üzerinde kapsamlı veri temizleme ve ön işleme pratiği yaptım.

Farklı makine öğrenmesi algoritmalarını karşılaştırma ve değerlendirme sürecini deneyimledim.

Modelleme sürecini baştan sona tek başıma yürütme becerisi kazandım.

Doğruluk, precision, recall gibi metrikleri yorumlamayı öğrendim.

Daha önce teorik olarak öğrendiğim bilgileri uygulamalı bir şekilde pekiştirdim.

Kaynaklar
Proje not defteri (Kaggle):
https://www.kaggle.com/code/dilanisb/akbank-machine-learning-project

Kullanılan veri seti:
https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package

