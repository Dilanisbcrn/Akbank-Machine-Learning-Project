# Akbank Makine Öğrenmesi Projesi – Yağmur Tahmini
Bu proje, Akbank ve Global AI Hub iş birliğiyle düzenlenen Makine Öğrenmesine Giriş Bootcamp için hazırladığım denetimli öğrenme projesidir. Amacım, elimdeki hava durumu verilerini kullanarak ertesi gün yağmur yağacak mı, yağmayacak mı onu tahmin etmekti. Bu proje sonucunda da ne kadar doğru şekilde yağmurun yağıp yağmamasını tahmin edebiliyor test etmiş oldum.

Kullandığım veri seti, Kaggle’da bulduğum "Weather Dataset from Rattle Package" adlı veri setidir. Avustralya’dan günlük hava durumu verileri içeriyor. İçinde sıcaklık, nem, rüzgar hızı, yağış miktarı gibi bilgiler var. Veri setimde toplamda 145 bin civarı veri var ve 24 farklı değişken bulunuyor. Benim tahmin etmeye çalıştığım değişken ise RainTomorrow(yarın yağmur yağacak mı). Bu değişken bize ertesi gün yağmur yağacak mı sorusunun cevabını "Yes" ya da "No" olarak veriyor.

İlk olarak veri setini projeme dahil ettim ve kod tarafında: head(), info(), describe() fonksiyonlarını kullanarak veriyi tanıdım.

Veriyle çalışırken karşılaştığım ilk zorluk eksik değerlerdi.Bazı sütunlarda çok fazla eksik veri vardı (örneğin bulut verileri)bunları tamamen kaldırdım. Diğer sütunlardaki eksik değerleri ise medyan gibi yöntemlerle doldurarak veriyi daha düzenli hale getirdim. Veri temizliği adımına özellikle özen gösterdim çünkü bu adım doğru yapılmazsa modelin test verisi üzerindeki başarımı etkileyecekti.

Veri setini incelediğimde bazı sütunların sayılar yerine metinlerden oluştuğunu fark ettim. Mesela Yes/No şeklinde yanıtlar ya da rüzgar yönleri gibi kategorik ifadeler vardı. Ama makine öğrenmesi modelleri bu metinleri anlayacağı sadece sayılarla çalışsacağı için bu verileri modelin anlayabileceği hale getirmem gerekiyordu. Bunun için iki farklı yöntem kullandım: Label Encoding ve One-Hot Encoding. RainToday ve RainTomorrow gibi sütunları 0 ve 1 şeklinde dönüştürdüm. Bu, özellikle "RainTomorrow" değişkenim için çok önemliydi çünkü model bu sayısal değerleri sınıflandırma yaparken kullanıyor.

WindGustDir, WindDir9am ve WindDir3pm gibi rüzgar yönlerini ise One-Hot Encoding yöntemiyle dönüştürdüm. Yani her rüzgar yönü için ayrı bir sütun oluşturdum. Böylece model, hangi yönün daha etkili olduğunu daha rahat ayırt edebiliyor hale geldi. Değişkenler arasındaki ilişkileri anlamak için korelasyon matrisi çizdim.

Tahmin yapabilmek için RainTomorrow dışındaki tüm hava durumu verilerini giriş değişkeni (feature) olarak belirledim. Ardından veriyi eğitim ve test olarak ikiye ayırdım.Eğitim verisi (%80) modeli öğretmek için, test verisi (%20) ise modelin ne kadar doğru çalıştığını ölçmek için kullandım.Bu işlemde train_test_split fonksiyonunu kullandım.

Model karşılaştırma sürecinde projem için üç farklı makine öğrenmesi algoritmasını denedim: Random Forest, Logistic Regression ve Decision Tree Classifier. Amacım, hangi modelin verim açısından en iyi performansı gösterdiğini gözlemleyerek en uygun algoritmayla ilerlemekti.Bu süreci daha güvenilir hale getirmek adına çapraz doğrulama (cross-validation) yöntemini kullandım ve elde ettiğim ortalama doğruluk (accuracy) skorları şu şekildeydi:

Random Forest: 0.843

Logistic Regression: 0.838

Decision Tree: 0.774

Bu sonuçlara göre en iyi performansı Random Forest modeli gösterdi. Karmaşık veri yapılarından bile etkili şekilde öğrenebilen bu algoritma, aynı zamanda overfitting problemlerine karşı da oldukça dayanıklı. Özellikle "yağmur yağmayacak" durumları tahmin etmede çok başarılıydı. Örneğin:

Yağmur yok tahminlerinde: Precision = 0.87, Recall = 0.95

Yağmur var tahminlerinde: Precision = 0.74, Recall = 0.49

Yağmurun yağacağı durumlarda model biraz daha zorlandı. Bu da aslında anlaşılır bir durum çünkü bu tür olaylar genellikle daha az sayıda gerçekleştiği ve öngörülmesi zor olduğu için modelin bu sınıfta zorlanması beklenebilir.

Logistic Regression modeli ise daha basit ve hızlı çalışan bir algoritma. %83 doğruluk oranıyla oldukça iyi performans gösterdi, ancak özellikle yağmurun yağacağı durumları yakalamada Random Forest kadar başarılı değildi.

Decision Tree Classifier ise karar verme süreçlerini görselleştirebilmesi açısından anlaşılır bir yapı sunuyordu. Fakat modelin aşırı öğrenmeye (overfitting) yatkın olması, test doğruluğunu olumsuz etkiledi. %77 doğruluk oranıyla diğer modellere kıyasla daha düşük bir performans sergiledi.

Tüm bu değerlendirmeler sonucunda, projemin kalan adımlarında Random Forest ile ilerlemeye karar verdim. Çünkü bu model, hem genel doğruluk açısından yüksek başarı sağladı hem de yağmur yağmayacak durumları güvenilir şekilde tahmin edebildi.Ayrıca modelin başarısını daha detaylı analiz etmek için Confusion Matrix (Karmaşıklık Matrisi) kullandım. Bu sayede her bir sınıfın ne kadar doğru tahmin edildiğini görselleştirdim. Ek olarak, Feature Importance (Özellik Önemi) analizini gerçekleştirdim ve model üzerinde en etkili değişkenlerin şunlar olduğunu gözlemledim:
Humidity3pm
Pressure3pm
Humidity9am
WindGustSpeed

Bu analizler, modelin karar verirken hangi verilere daha fazla ağırlık verdiğini gösterdi ve genel doğruluk başarısını daha da anlamlı kıldı.

Bu projede hem veri ön işleme hem de makine öğrenmesi algoritmalarının kıyaslanması üzerine güzel deneyimler kazandım.Kendi başıma veriyi indirip, analiz edip, temizleyip, modelleyip değerlendirmek bana çok şey kattı.

## Kaggle Linki
Projeyi buradan detaylı inceleyebilirsiniz:  https://www.kaggle.com/code/dilanisb/akbank-machine-learning-project

Projem için kullandığım veri setim:
https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package
