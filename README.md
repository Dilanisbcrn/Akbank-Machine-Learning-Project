# Akbank Makine Öğrenmesi Projesi – Yağmur Tahmini

Bu proje, Akbank ve Global AI Hub iş birliğiyle düzenlenen "Makine Öğrenmesine Giriş Bootcamp" kapsamında geliştirdiğim bir sınıflandırma problemine odaklanan çalışmadır. Temel hedefim, geçmiş hava durumu verilerine dayanarak ertesi gün yağmur yağıp yağmayacağını tahmin etmekti. Bu süreçte farklı makine öğrenmesi algoritmalarını karşılaştırarak, sınıflandırma problemlerine yönelik çözüm geliştirme pratiği yapmış oldum.

-Kullanılan Veri Seti
Projede kullandığım veri seti, Kaggle platformunda açık kaynak olarak paylaşılan "Weather Dataset from Rattle Package" adlı veri setidir. Bu veri seti, Avustralya'nın çeşitli bölgelerine ait günlük hava durumu ölçümlerini içermektedir.

Yaklaşık 145.000 örnek

24 bağımsız değişken

Hedef değişken: RainTomorrow (Yarın yağmur yağacak mı? "Yes" / "No")

Veri setinde sıcaklık, nem, rüzgar yönü, yağış miktarı gibi birçok meteorolojik parametre yer almaktadır.

-Veri Ön İşleme Süreci
Veri setini projeye dahil ettikten sonra ilk olarak temel bir analiz gerçekleştirdim. head(), info(), describe() gibi temel fonksiyonlarla verinin yapısını inceledim. Eksik veri oranlarını analiz ettikten sonra şu adımları izledim:

Bulut verileri gibi çok sayıda eksik bilgi içeren sütunları veri setinden çıkardım.

Diğer eksik verileri ise medyan ya da mod gibi istatistiksel yöntemlerle doldurdum.

Kategorik değişkenleri sayısal forma dönüştürdüm:

RainToday ve RainTomorrow gibi ikili kategorik sütunları Label Encoding ile,

Rüzgar yönleri (WindGustDir, WindDir9am, WindDir3pm) gibi çok kategorili sütunları ise One-Hot Encoding yöntemiyle dönüştürdüm.

Değişkenler arasındaki ilişkiyi anlamak adına korelasyon matrisi oluşturarak görsel analiz yaptım.

Bu adımlar sonucunda veri, modelleme süreci için daha uygun ve temiz bir hale geldi.

-Modelleme ve Kullanılan Algoritmalar
Veri setini %80 eğitim ve %20 test olmak üzere ikiye ayırdıktan sonra üç farklı sınıflandırma algoritması uyguladım:

Random Forest Classifier

Logistic Regression

Decision Tree Classifier

Model performanslarını yalnızca doğruluk (accuracy) oranıyla değil, aynı zamanda precision, recall gibi sınıflandırma metrikleriyle de değerlendirdim. Sonuçların güvenilirliğini artırmak adına cross-validation yöntemini de kullandım.

Model	Doğruluk Oranı
Random Forest	0.843
Logistic Regression	0.838
Decision Tree	0.774

Bu sonuçlara göre en iyi performansı Random Forest modeli gösterdi. Özellikle karmaşık verileri anlamada ve genelleştirme kapasitesinde güçlü bir model olduğunu gözlemledim.

Precision / Recall Değerleri (Random Forest)
Yağmur yağmayacak (No):

Precision: 0.87

Recall: 0.95

Yağmur yağacak (Yes):

Precision: 0.74

Recall: 0.49

Model, özellikle yağmurun yağmayacağı durumları oldukça başarılı şekilde tahmin ederken, yağmur yağacak sınıfında daha düşük başarı gösterdi. Bunun temel nedeni, bu sınıfa ait örneklerin veri setinde daha az yer alması ve verinin dengesiz yapısıydı.

-Ek Analizler
Model seçimi sonrasında, Confusion Matrix (Karmaşıklık Matrisi) yardımıyla modelin hangi sınıflarda ne kadar başarılı olduğunu görselleştirdim. Ayrıca, özellik önem düzeyi (feature importance) analizini gerçekleştirerek modelin karar sürecinde en çok hangi değişkenlere dayandığını belirledim. En önemli değişkenler şunlardı:

Humidity3pm

Pressure3pm

Humidity9am

WindGustSpeed

Bu analiz, modelin mantığını daha iyi anlamamı sağladı.

-Projeden Kazandıklarım
Bu projeyle birlikte;

Gerçek bir veri seti üzerinde veri temizleme ve ön işleme pratiği yaptım.

Farklı makine öğrenmesi algoritmalarını uygulayıp karşılaştırarak model seçimi konusunda tecrübe kazandım.

Sıfırdan bir projeyi tasarlayıp uygulayarak, süreci baştan sona bağımsız şekilde yönetme becerisi edindim.

Accuracy, precision, recall gibi değerlendirme metriklerini uygulamalı olarak kullanma fırsatı buldum.

Teorik bilgileri pratiğe dökerek kendimi geliştirdim.

## Kaggle Linki
Proje not defteri (Kaggle):
https://www.kaggle.com/code/dilanisb/akbank-machine-learning-project

Kullanılan veri seti:
https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package

