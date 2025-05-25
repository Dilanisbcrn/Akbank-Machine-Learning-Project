🌧️ Akbank Makine Öğrenmesi Projesi – Yağmur Tahmini
Bu proje, Akbank ve Global AI Hub iş birliğiyle düzenlenen Makine Öğrenmesine Giriş Bootcamp kapsamında hazırladığım denetimli öğrenme projesidir. Projenin temel amacı, geçmiş hava durumu verilerini kullanarak ertesi gün yağmur yağıp yağmayacağını tahmin etmektir. Bu çalışmayla, farklı makine öğrenmesi algoritmalarını uygulayarak hangisinin bu problem üzerinde daha başarılı sonuçlar verdiğini analiz ettim.

📊 Kullanılan Veri Seti
Projede kullandığım veri seti, Kaggle platformunda yer alan Weather Dataset from Rattle Package adlı veri setidir. Bu veri seti, Avustralya’nın çeşitli bölgelerine ait günlük hava durumu verilerini içermektedir.

📌 Toplam veri sayısı: ~145.000

📌 Değişken sayısı: 24

📌 Tahmin edilmeye çalışılan hedef değişken: RainTomorrow (Yarın yağmur yağacak mı? – Yes/No)

Veri setinde sıcaklık, nem, rüzgar yönü, yağış miktarı gibi pek çok hava durumu ölçümü bulunmaktadır.

🧹 Veri Ön İşleme
Projeye ilk olarak veriyi tanımakla başladım:

python
Kopyala
Düzenle
data.head()
data.info()
data.describe()
✅ Eksik Değerlerin Temizlenmesi
Bazı sütunlarda (örneğin bulut verileri) çok fazla eksik veri bulunduğu için bu sütunları veri setinden çıkardım.

Geriye kalan sütunlardaki eksik değerleri ise medyan veya en yaygın değer (mode) ile doldurdum.

Veri temizliği aşaması modelin doğruluğunu doğrudan etkilediği için bu adıma özellikle önem verdim.

🔢 Kategorik Verilerin Dönüştürülmesi
Makine öğrenmesi modelleri yalnızca sayısal verilerle çalışabildiği için metinsel ifadeleri sayısal formata çevirdim.

RainToday ve RainTomorrow gibi sütunları Label Encoding yöntemiyle 0 ve 1'e çevirdim.

WindGustDir, WindDir9am, WindDir3pm gibi rüzgar yönlerini ise One-Hot Encoding yöntemiyle dönüştürdüm.

Değişkenler arasındaki ilişkileri analiz etmek amacıyla korelasyon matrisi çizdim.

🧠 Modelleme Süreci
Veri ön işleme tamamlandıktan sonra modeli eğitmek için şu adımları uyguladım:

Özellik (feature) ve hedef (target) değişkenlerini ayırdım.

Veriyi %80 eğitim ve %20 test olarak ikiye böldüm (train_test_split).

Üç farklı makine öğrenmesi algoritmasını karşılaştırdım:

Random Forest Classifier

Logistic Regression

Decision Tree Classifier

Daha güvenilir sonuçlar için cross-validation (çapraz doğrulama) uyguladım.

🎯 Doğruluk Skorları
Model	Doğruluk (Accuracy)
Random Forest	0.843
Logistic Regression	0.838
Decision Tree	0.774

🧪 Precision / Recall Analizi (Random Forest)
Yağmur Yağmayacak (No):

Precision: 0.87

Recall: 0.95

Yağmur Yağacak (Yes):

Precision: 0.74

Recall: 0.49

Random Forest modeli, özellikle yağmurun yağmayacağı durumları çok başarılı bir şekilde tahmin etti. Yağmur yağacak durumlarda ise daha düşük başarı gösterdi ki bu da doğaldır; çünkü bu sınıf genellikle daha az örnek içerir ve tahmin edilmesi daha zordur.

📌 Model Seçimi
Elde ettiğim sonuçlara göre en iyi performansı Random Forest modeli gösterdi. Bu model:

Karmaşık veri yapılarından öğrenme konusunda başarılı,

Aşırı öğrenmeye (overfitting) karşı daha dirençli,

Yağmur yağmayacak durumları yüksek doğrulukla tahmin edebiliyor.

Bu nedenle projenin sonraki adımlarında Random Forest modeli ile ilerledim.

📊 Ek Analizler
🔍 Confusion Matrix (Karmaşıklık Matrisi)
Modelin hangi sınıflarda doğru/yanlış tahmin yaptığını görselleştirmek için kullandım.

🌟 Feature Importance (Özellik Önemi)
Modelin en çok önem verdiği değişkenleri incelediğimde şu sonuçlara ulaştım:

Humidity3pm

Pressure3pm

Humidity9am

WindGustSpeed

Bu değişkenler, modelin yağmur tahmini yaparken karar vermesinde önemli rol oynuyor.

🎓 Kazanımlarım
Bu proje sayesinde:

Gerçek dünya verileri üzerinde veri temizleme, dönüştürme ve analiz etme pratiği kazandım.

Farklı sınıflandırma algoritmalarını karşılaştırma ve değerlendirme becerisi geliştirdim.

Model başarı metriklerini yorumlama konusunda deneyim edindim.

Tüm süreci uçtan uca (veri analizi → modelleme → değerlendirme) tek başıma gerçekleştirdim.
