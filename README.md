# 🧠 VisDrone2019-DET ile Çoklu Sınıf Nesne Tespiti ve Sınıflandırma (Deep Learning)

Bu repository, Aksaray Üniversitesi Yönetim Bilişim Sistemleri bölümü kapsamında gerçekleştirilen, drone (İHA) görüntülerinde nesne tespiti ve sınıflandırma odaklı kapsamlı bir derin öğrenme projesini içermektedir.

## 🎯 1. Proje Özeti
İnsansız hava araçlarının (İHA) yaygınlaşmasıyla kentsel planlama ve trafik analizi gibi alanlarda havadan çekilen görüntülerin otomatik analizi kritik bir ihtiyaç haline gelmiştir. Bu projede, akademik literatürdeki en zorlu küçük obje benchmarklarından biri olan **VisDrone2019-DET** veri seti kullanılarak 10 farklı nesne sınıfının hem tespiti (detection) hem de sınıflandırılması (classification) gerçekleştirilmiştir.

* **Nesne Tespiti (Detection):** YOLOv8l ve YOLOv10l modelleri.
* **Sınıflandırma (Classification):** Özgün Custom CNN (4'lü Ablasyon) mimarileri, ResNet50 ve EfficientNetB0 (Transfer Learning).

---

## 📊 2. Kullanılan Teknolojiler & Kütüphaneler
* **Programlama Dili:** Python 3.12
* **Derin Öğrenme Çatırları:** TensorFlow / Keras, PyTorch, Ultralytics YOLO
* **Optimizasyon & Takip:** Weights & Biases (W&B), Scikit-Learn
* **Donanım Optimizasyonu:** TensorFloat-32 (TF32) & Mixed Precision (FP16)

---

## 🛠️ 3. Veri Hazırlığı ve Metodoloji
1. **YOLO Format Dönüşümü:** VisDrone piksel bazlı orijinal etiketleri YOLO standartlarına (0-1 normalize merkez koordinatları) uyarlanmıştır.
2. **Kırpma (Classification Crop):** Tespit edilen nesneler bbox koordinatlarına göre kırpılmış, 32 piksel altındaki gürültülü kutular filtrelenmiş ve 224x224 boyutuna getirilerek **45.345 örnekli** sınıflandırma veri seti oluşturulmuştur.
3. **Sınıf Ağırlıkları (Class Weights):** Sınıf dengesizliğini önlemek için `compute_class_weight` kullanılarak kayıp fonksiyonuna dengeli ağırlıklar entegre edilmiştir.

---

## 🏆 4. Deneysel Sonuçlar & Karşılaştırma

### 🎯 Nesne Tespiti (Detection) Sonuçları
* **YOLOv8l:** Test mAP@50 = **0.3502** (71 epoch'ta erken durdurma)
* **YOLOv10l:** Test mAP@50 = **0.3566** (NMS-free mimari avantajıyla daha yüksek verimlilik)

### 🎨 Sınıflandırma (Classification) Sonuçları
* **ResNet50 (Transfer Learning):** Test Doğruluğu = **%62.45** (Macro F1: 0.5723) — *En Başarılı Model*
* **EfficientNetB0:** Test Doğruluğu = **%53.00**
* **Custom CNN V4 (Ablasyon Kazananı):** Test Doğruluğu = **%52.54** (Dense 64 + ReLU + Adam)


