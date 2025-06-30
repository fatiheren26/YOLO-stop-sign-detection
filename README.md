Stop Tabelası Tespiti – YOLOv11 Projesi
Bu proje, STOP (dur) tabelalarının tespiti için YOLOv11 algoritmasını kullanır. Model, Ultralytics altyapısıyla eğitilmiş olup .zip formatında paylaşılmıştır. Aşağıdaki adımları izleyerek ortamı kurabilir ve modeli test edebilirsiniz.

Başlarken
1. Proje dosyasını indir
Repo'daki yolo.zip dosyasını indirip çıkar:

Dosyayı indir (.zip)

Zip'i çıkarınca içinde predict.py, model dosyaları ve test klasörü bulunmalı.

2. Ortamı oluştur
Conda ile ortam kur:
bash
Copy
Edit
conda create -n stop_detection python=3.11 -y
conda activate stop_detection
Gerekli kütüphaneler:
bash
Copy
Edit
pip install ultralytics
CUDA destekli sistemlerde PyTorch'u ayrıca şu şekilde kurabilirsin (Windows için):

bash
Copy
Edit
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu126
Kullanım
Görsel Testi
Test etmek istediğiniz görselleri test/ klasörüne yerleştirin

Terminalden predict.py dosyasını çalıştırın:

bash
Copy
Edit
python predict.py
Çıktılar
Sonuç görselleri runs/detect/predict/ klasörüne kaydedilir. Tespit edilen STOP tabelaları görseller üzerinde kutu içinde gösterilir.

Ek Bilgi
Proje sadece STOP tabelası tespiti üzerine odaklanmıştır.

Model eğitimi tamamlanmış olup, yeniden eğitim yapılmasına gerek yoktur.

.zip dosyası içinde tüm gerekli dosyalar mevcuttur.

EKSTRA
Parametrelerinin ve sonuç değerlerinin ne anlama geldiğinin açıklanması

Kullanılan Modelin Eğitim Parametreleri ve Açıklamaları
Bu projede kullanılan hazır YOLOv11 modeli, aşağıdaki hiperparametrelerle eğitilmiştir:

Epoch (30):
Model, eğitim veri seti üzerinde toplam 30 kez tam tur yapmıştır. Yani tüm veri seti 30 defa modele gösterilmiştir. Bu, modelin veriyi yeterince öğrenmesi için yeterli bir sayıdır.

Batch Size (8):
Her eğitim adımında modele 8 görüntü aynı anda verilmiştir. Bu sayı, bellek kullanımını dengelerken öğrenme sürecinin stabil olmasını sağlar.

Image Size (416):
Modelin girişine verilen tüm görüntüler 416x416 piksele yeniden boyutlandırılmıştır. Bu boyut, modelin hem yeterince detay görmesini hem de işlem süresinin makul kalmasını sağlar.

Optimizer:
Optimizasyon için Ultralytics tarafından varsayılan olarak kullanılan Stochastic Gradient Descent (SGD) tercih edilmiştir. Bu algoritma, modelin ağırlıklarını güncelleyerek hatayı azaltmaya çalışır.

Workers (0):
Veri yüklemede çoklu iş parçacığı kullanılmamıştır. Bu, bazı sistemlerde eğitim sırasında veri yükleme işleminin nasıl yönetileceğini belirtir.

Device (0):
Eğitim işlemi, GPU'nun 0 numaralı cihazında gerçekleştirilmiştir. GPU kullanımı eğitim hızını önemli ölçüde artırır.

Test Aşamasında Kullanılan Parametreler ve Açıklamaları
Model eğitildikten sonra test sürecine geçilmiştir. Bu süreçte aşağıdaki parametreler önemli rol oynar:

Confidence Threshold (Güven Eşiği):
Modelin bir nesneyi tespit ettiğinde, bu tespitin doğruluğuna olan güven skorudur. Belirli bir eşik değerin altında kalan tahminler geçerli kabul edilmez. Böylece modelin kararsız tahminleri filtrelenmiş olur.

IoU Threshold (Intersection over Union):
Tespit edilen kutular ile gerçek kutular arasındaki örtüşme oranına göre doğruluk hesaplanır. IoU eşik değeri, hangi kutuların doğru kabul edileceğini belirler.

Non-Maximum Suppression (NMS):
Aynı nesneye ait birden fazla tespit olduğunda, sadece en güvenilir olanı seçmek için kullanılır. Bu işlem sayesinde yinelenen kutular ortadan kaldırılır.

Image Size (Giriş Görüntü Boyutu):
Test sürecinde de modelin girişine verilen görseller sabit bir boyuta getirilir. Bu sayede eğitim ve test tutarlılığı sağlanır.

Bu parametrelerin doğru seçilmesi, test doğruluğunu ve modelin güvenilirliğini doğrudan etkiler.

Test Sonuçları ve Eğitim Değerlendirmesi
Eğitim tamamlandığında Ultralytics tarafından runs/train/ klasörü altında eğitimle ilgili detaylı sonuçlar ve grafikler üretilmiştir. Özellikle runs/detect/train 4 dosyasındaki png ve results.csv dosyaları ile kayıplar (loss) ve başarı metrikleri gözlemlenebilir.

Eğitim Sonuçları:

Box Loss: Modelin nesnenin konumunu tahmin etme başarısını ölçer. Genelde eğitim süreci boyunca düşer.

Class Loss: Modelin doğru sınıf tahmini yapma başarısını ifade eder.

mAP@0.5: Ortalama Doğruluk Skoru. Genellikle %70-90 arası iyi kabul edilir. Bu değer eğitim sonunda results.csv dosyasında bulunabilir.

Precision / Recall: Doğru pozitif tahminlerin oranını verir. Bunlar da results.csv içinde yer alır.

Eğitim süreci boyunca bu metrikler takip edilerek modelin başarısı analiz edilmiştir. Grafiksel sonuçlar runs/train/exp*/results.png içinde görselleştirilmiştir.

