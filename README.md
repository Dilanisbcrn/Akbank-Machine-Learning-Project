# Akbank Makine Öğrenmesi Projesi – Yağmur Tahmini

Bu proje, Akbank ve Global AI Hub iş birliğiyle düzenlenen Makine Öğrenmesine Giriş Bootcamp için hazırladığım denetimli öğrenme projesidir. Amacım, elimdeki hava durumu verilerini kullanarak ertesi gün yağmur yağacak mı, yağmayacak mı bunu tahmin etmektir. Proje sonucunda yağmurun yağıp yağmayacağını ne kadar doğru tahmin edebildiğimi test etme fırsatı buldum.

Kullandığım veri seti, Kaggle’da bulunan "Weather Dataset from Rattle Package" adlı veri setidir. Bu set, Avustralya’ya ait günlük hava durumu verilerini içermektedir. İçerisinde sıcaklık, nem, rüzgar hızı, yağış miktarı gibi 24 farklı değişken bulunmakta ve toplamda yaklaşık 145.000 veri yer almaktadır. Tahmin etmeye çalıştığım hedef değişken ise RainTomorrow (yarın yağmur yağacak mı) olup, bu değişkenin değerleri “Yes” ya da “No” şeklindedir.

İlk olarak veri setini projeme dahil ettim ve head(), info(), describe() gibi fonksiyonlarla veriyi tanıyarak genel bir analiz gerçekleştirdim.

Veriyle çalışırken karşılaştığım ilk zorluk eksik değerlerdi. Özellikle bulut verileri gibi bazı sütunlarda çok fazla eksik değer bulunduğundan bu sütunları veri setinden çıkardım. Diğer sütunlardaki eksik değerleri ise medyan gibi uygun istatistiksel yöntemlerle doldurarak veri temizliğini sağladım. Bu adım, model başarımını doğrudan etkileyebileceği için büyük önem taşıyordu.

Ayrıca, bazı sütunlar sayısal yerine metinsel ifadeler içeriyordu. Örneğin Yes/No yanıtları veya rüzgar yönleri gibi kategorik veriler. Makine öğrenmesi algoritmaları sayısal verilerle çalıştığı için bu kategorik verileri sayısal forma dönüştürdüm. Bu dönüşümler için:

Label Encoding yöntemini RainToday ve RainTomorrow gibi sütunlarda uyguladım.

One-Hot Encoding yöntemini ise WindGustDir, WindDir9am ve WindDir3pm gibi rüzgar yönlerini dönüştürmek için kullandım.

Modelin değişkenler arasındaki ilişkileri daha iyi öğrenebilmesi adına korelasyon matrisi oluşturdum.

Tahmin işlemleri için RainTomorrow dışındaki tüm değişkenleri giriş (feature) olarak kullandım. Veriyi %80 eğitim – %20 test olarak ayırdım. Bu işlemde train_test_split fonksiyonunu kullandım.

Model karşılaştırması için üç farklı makine öğrenmesi algoritmasını denedim:

Random Forest

Logistic Regression

Decision Tree Classifier

Bu süreçte daha güvenilir sonuçlar elde etmek adına çapraz doğrulama (cross-validation) yöntemini uyguladım. Elde ettiğim ortalama doğruluk (accuracy) skorları şu şekildedir:

Random Forest: 0.843

Logistic Regression: 0.838

Decision Tree: 0.774

Bu sonuçlara göre, en iyi performansı Random Forest modeli gösterdi. Özellikle karmaşık veri yapılarından etkili biçimde öğrenebilmesi ve overfitting'e karşı dayanıklı olması sayesinde modelin güvenilirliğini artırdı.

Özellikle:

Yağmur yok tahminlerinde: Precision = 0.87, Recall = 0.95

Yağmur var tahminlerinde: Precision = 0.74, Recall = 0.49

Model, yağmurun yağacağı durumları tahmin etmede biraz daha zorlandı. Bu durum anlaşılır bir sonuçtur çünkü bu olaylar genelde daha az sıklıkta gerçekleşir ve öngörülmesi daha zordur.

Logistic Regression modeli daha basit ve hızlı çalışsa da özellikle yağmur yağacağı durumları tahmin etmede Random Forest kadar başarılı değildi.
Decision Tree Classifier ise modelin karar yapısını anlamak için faydalıydı fakat overfitting eğilimi nedeniyle daha düşük doğruluk sağladı.

Tüm bu değerlendirmelerin ardından projemin sonraki adımlarında Random Forest modeliyle ilerlemeye karar verdim. Bu modeli değerlendirirken:

Confusion Matrix (Karmaşıklık Matrisi) yardımıyla sınıflandırma performansını daha iyi gözlemledim.

Feature Importance (Özellik Önemi) analizini yaparak modelin karar sürecinde en etkili olan değişkenleri belirledim:

Humidity3pm

Pressure3pm

Humidity9am

WindGustSpeed

Bu analizler modelin hangi verileri ön planda tuttuğunu anlamamı sağladı ve genel doğruluk başarısının sebeplerini daha iyi açıklamamı sağladı.

Bu proje sayesinde gerçek dünya verileriyle çalışma pratiği kazandım. Özellikle eksik verilerin temizlenmesi, kategorik verilerin dönüştürülmesi ve veri setinin analiz edilmesi gibi veri ön işleme adımlarını etkin bir şekilde uyguladım. Farklı makine öğrenmesi algoritmalarını deneyimleyerek hangisinin daha uygun olduğuna karar verebilme becerimi geliştirdim.Ayrıca, model değerlendirme metriklerini (accuracy, precision, recall) kullanarak modellerin güçlü ve zayıf yönlerini yorumlamayı öğrendim. Uygulamalı olarak gerçekleştirdiğim bu süreçler, teorik bilgilerimi pekiştirmemi sağladı. Genel olarak, baştan sona bir makine öğrenmesi projesini bağımsız şekilde yürütmek, hem teknik yetkinliğimi hem de problem çözme becerilerimi önemli ölçüde artırdı.

## Kaggle Linki

Projeyi buradan detaylı inceleyebilirsiniz:
https://www.kaggle.com/code/dilanisb/akbank-machine-learning-project

Projede kullandığım veri seti:
https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package

