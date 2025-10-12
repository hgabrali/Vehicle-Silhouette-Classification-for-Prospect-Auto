# 🚀 Proje Organizasyon Planı: Araç Sınıflandırma (Vehicle Classification)

Bu proje, "Prospect Auto" için gövde özelliklerine (silhouette features) dayalı olarak araçları (otobüs, minibüs, otomobil) sınıflandırmak üzere tek bir Google Colab not defterinde altı ana başlık altında yürütülecektir.

# 🇹🇷 Turkish Description: Content Summary

##### * This file, named `Turkish description`, serves as an internal reference and quick summary document for the project's key concepts.

## 📝 Purpose and Rationale

The primary purpose of this file is to enhance clarity and comprehension regarding complex Machine Learning topics discussed throughout the project workflow.

| Feature | Description | Benefit |
| :--- | :--- | :--- |
| **Language** | Turkish (Türkçe) | Facilitates immediate understanding of definitions, terminology, and project steps for Turkish-speaking team members or reviewers. |
| **Content** | Summaries and brief explanations of core concepts (e.g., Regression Metrics, Hyperparameter Tuning, Cross-Validation). | Ensures all participants have a solid, clear foundation of the theoretical and methodological aspects of the project. |
| **Professionalism** | Acts as a supplementary document to the primary English-language documentation. | Demonstrates a professional approach to knowledge management and accessibility within the project repository. |

**In short:** This file contains concise Turkish summaries to ensure accurate and fast concept validation during development and review stages.
---

## 1. 💾 Ayarlama ve Veri Yükleme (Setup and Data Loading)

Bu adım, tüm projenin temelini oluşturur.

| 📂 Kısım | Açıklama |
| :--- | :--- |
| **Kütüphane İthalatı (Import)** | `pandas`, `numpy`, `matplotlib`, `seaborn` ve scikit-learn'den (`model_selection`, `preprocessing`, `metrics`, `classifiers`) **gerekli tüm kütüphaneleri yükleyin.** |
| **Veri Yükleme** | Veri setini doğrudan indirme bağlantısından veya GitHub'dan yükleyerek **`DataFrame`** olarak okuyun. |


## 2. 🔍 Keşifçi Veri Analizi (Exploratory Data Analysis - EDA)

Verinin yapısını anlamak, modellemenin başarısı için kritik öneme sahiptir.

| 🧩 Kısım | Analiz Türü | Vurgu |
| :--- | :--- | :--- |
| **Yapısal Kontrol** | `.info()`, `.describe()`, `.shape` | Eksik değer (missing values) var mı? Özelliklerin veri tipleri doğru mu? |
| **Hedef Değişken Analizi** | Sınıfların dağılımı (`value_counts()`) | Sınıf dengesizliği (class imbalance) var mı? (Beklenen: Otobüs, Minibüs ve Otomobilin yaklaşık eşit olması). |
| **Görselleştirme (Visual)** | Kutu grafikleri (boxplot), çift grafikler (pairplot) veya ısı haritası (heatmap) | Özellikler (features) arasındaki korelasyonu (correlation) ve her bir özelliğin sınıfları ne kadar iyi ayırdığını görselleştirin. |

## 3. 🧹 Veri Hazırlama ve Ön İşleme (Data Preprocessing)

Modelin düzgün çalışması için verinin dönüştürülmesi.

| 🧩 Kısım | İşlem | Neden? |
| :--- | :--- | :--- |
| **Özellik/Hedef Ayırma** | Veriyi özellikler (`X`) ve hedef (`y`) olarak ayırın. | Denetimli öğrenme (supervised learning) için standart gereklilik. |
| **Ölçeklendirme (Scaling)** | Sayısal özellikleri **StandardScaler** veya **MinMaxScaler** kullanarak ölçeklendirin. | Özellikle mesafe tabanlı algoritmalar (KNN, SVM) için özelliklerin eşit ağırlığa sahip olmasını sağlamak. |
| **Eğitim/Test Bölme** | Veriyi `train_test_split` kullanarak eğitim ve test setlerine ayırın (örn. %70 eğitim, %30 test). | Modelin görülmeyen veriler üzerindeki genelleme performansını ölçmek. |

## 4. 🧠 Sınıflandırma Modellerinin Eğitimi (Model Training)

"Prospect Auto"nun talebini karşılamak için çoklu sınıflandırma modelleri kullanın.

| 🧩 Kısım | Modeller | Amaç |
| :--- | :--- | :--- |
| **Basit Model** | **Lojistik Regresyon (Logistic Regression)** | Temel bir karşılaştırma çizgisi (baseline) oluşturmak. |
| **Ağaç Tabanlı** | **Karar Ağacı (Decision Tree)** ve **Rastgele Orman (Random Forest)** | Doğrusal olmayan ilişkileri yakalama ve basit modelle karşılaştırma. |
| **Destek Vektör Makinesi** | **SVM (Support Vector Machine)** veya **KNN** | Farklı matematiksel prensiplere dayalı modelleri test etmek. |

## 5. ✅ Model Değerlendirme (Evaluation and Metrics)

Çoklu sınıflandırma problemine uygun metrikleri seçmek önemlidir.

| 📊 Metrik | Neden Önemli? | Vurgu |
| :--- | :--- | :--- |
| **Doğruluk (Accuracy)** | Genel doğru tahmin yüzdesi. (Sınıflar dengeliyse kullanın.) | En basit performans ölçüsü. |
| **Sınıflandırma Raporu (Classification Report)** | Her sınıf için **Hassasiyet** (Precision), **Geri Çağırma** (Recall) ve **F1 Skoru**'nu sağlar. | Özellikle Otomobil/Otobüs arasındaki ayrım zorluğu gibi ince ayrımları değerlendirmek. |
| **Karmaşıklık Matrisi (Confusion Matrix)** | Hangi araç sınıflarının birbiriyle karıştırıldığını (örn. araba ile minibüs) görselleştirir. | Modelin hata türlerini (Type I/Type II Errors) analiz etmek. |

## 6. 📝 Sonuç ve Özet (Conclusion and Summary)

Projenin çıktılarını ve bulgularını özetleyin.

| 🧩 Kısım | Açıklama |
| :--- | :--- |
| **En İyi Model** | Hangi modelin (örneğin Rastgele Orman), seçilen metriktere göre en iyi performansı gösterdiğini belirtin. |
| **İş Bağlamı (Business Context)** | Modelin, "Prospect Auto"nun beklentilerini karşılayıp karşılamadığını ve pratik uygulamada kullanılıp kullanılamayacağını değerlendirin. |
| **Gelecek Çalışmalar** | Performansı daha da artırmak için **Hiperparametre Ayarlama (Hyperparameter Tuning)** veya **Özellik Mühendisliği (Feature Engineering)** gibi sonraki adımları önerin. |
