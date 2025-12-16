# RT-IoT2022 Veri Kümesi Üzerinde Karmaşık IoT Saldırı Senaryolarının Çok Sınıflı Sınıflandırılması


# RT-IoT2022 Saldırı Tespit Sistemi (IDS)

Bu proje, **RT-IoT2022** veri setini kullanarak IoT (Nesnelerin İnterneti) ağlarındaki siber saldırıları tespit etmek için geliştirilmiş gelişmiş bir makine öğrenmesi yaklaşımı sunar. Çalışma; veri temizleme, boyut azaltma, özellik seçimi ve hiperparametre optimizasyonu için modern teknikleri (CatBoost, SHAP, Optuna, PSO, JAYA) bir araya getirir.

## 🚀 Proje Özellikleri ve Akış

Proje aşağıdaki ana adımlardan oluşmaktadır:

1.  **Veri Ön İşleme (Preprocessing):**
    - Gereksiz sütunların temizlenmesi.
    - Kategorik değişkenlerin kodlanması (Label Encoding & One-Hot Encoding).
    - **Local Outlier Factor (LOF)** ile aykırı değerlerin (outlier) tespit edilip temizlenmesi.
    - Bellek kullanımını azaltmak için veri tipi optimizasyonu.
2.  **Veri Alt Kümeleme (Subsampling):**
    - Büyük veri setini temsil eden dengeli bir alt küme oluşturmak için **UMAP** (boyut azaltma) ve **K-Means** kümeleme algoritmalarının birlikte kullanımı.
3.  **Model Eğitimi:**
    - Temel model olarak **CatBoost Classifier** kullanımı (GPU desteği ile).
4.  **Özellik Seçimi (Feature Selection):**
    - **SHAP (SHapley Additive exPlanations):** Model kararlarını açıklayarak en önemli özniteliklerin belirlenmesi.
    - **PSO (Particle Swarm Optimization):** İkili (Binary) PSO ile en iyi öznitelik alt kümesinin seçilmesi.
    - **JAYA Algoritması:** Alternatif bir meta-sezgisel algoritma ile özellik seçimi.
5.  **Hiperparametre Optimizasyonu:**
    - **Optuna:** Bayesyen optimizasyon ile model parametrelerinin ayarlanması.
    - **PSO:** Parçacık Sürü Optimizasyonu ile hiperparametrelerin ayarlanması.
6.  **Değerlendirme (Evaluation):**
    - **Nested Cross-Validation (İç İçe Çapraz Doğrulama):** Modelin genelleme yeteneğini tarafsız bir şekilde ölçmek için Outer ve Inner döngüler kullanılarak yapılan kapsamlı testler.

## 🛠️ Gereksinimler (Requirements)

Projeyi çalıştırmak için aşağıdaki Python kütüphanelerine ihtiyacınız vardır:

```txt
numpy
pandas
matplotlib
seaborn
scikit-learn
shap
optuna
catboost
xgboost
umap-learn
pyswarms
tqdm
kagglehub
```

Kurulum için:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn shap optuna catboost xgboost umap-learn pyswarms tqdm kagglehub
```

## 📊 Kullanılan Yöntemler

### 1. Aykırı Değer Analizi (LOF)

Sınıf bazında `LocalOutlierFactor` uygulanarak gürültülü veriler temizlenmiş ve modelin daha temiz veriyle eğitilmesi sağlanmıştır.

### 2. Hibrit Alt Kümeleme (UMAP + K-Means)

Tüm veri seti üzerinde çalışmak yerine, verinin yapısını koruyan temsili örnekler seçilmiştir. Önce UMAP ile boyut indirgenmiş, ardından K-Means ile her sınıftan merkezlere en yakın örnekler seçilmiştir.

### 3. Özellik Seçimi (Feature Selection)

Model performansını artırmak ve karmaşıklığı azaltmak için üç farklı yöntem denenmiştir:

- **SHAP:** Özelliklerin modele katkısına göre sıralama.
- **Binary PSO:** En iyi F1 skorunu veren özellik kombinasyonunu bulma.
- **Binary JAYA:** Parametresiz bir optimizasyon algoritması ile özellik seçimi.

### 4. Nested Cross-Validation

Modelin başarısını doğrulamak için 5-Fold Outer, 3-Fold Inner döngüden oluşan Nested CV yapısı kullanılmıştır. Bu sayede veri sızıntısı (data leakage) engellenmiş ve hiperparametre optimizasyonu güvenilir bir şekilde yapılmıştır.

## ▶️ Kullanım

Notebook dosyasını (`.ipynb`) Jupyter Notebook, JupyterLab veya VS Code ortamında açın ve hücreleri sırasıyla çalıştırın.

> **Not:** CatBoost ve bazı optimizasyon adımları GPU kullanımına göre yapılandırılmıştır (`task_type='GPU'`). Eğer GPU'nuz yoksa bu parametreyi `task_type='CPU'` olarak değiştirebilirsiniz.

## 📈 Sonuçlar

Notebook çalıştırıldığında aşağıdaki metrikler raporlanır:

- F1 Score (Weighted)
- Accuracy
- Precision
- Recall
- Confusion Matrix
- Eğitim/Doğrulama Kayıp Grafikleri

---

_Bu proje, IoT güvenliği alanında makine öğrenmesi ve meta-sezgisel optimizasyon tekniklerinin entegrasyonuna bir örnektir._
