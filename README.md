🚦 Stop Tabelası Tespiti – YOLOv11 Projesi
Bu proje, STOP (dur) tabelalarının tespiti için YOLOv11 algoritmasını kullanır. Model, Ultralytics altyapısıyla eğitilmiş olup .zip formatında paylaşılmıştır. Aşağıdaki adımları izleyerek ortamı kurabilir ve modeli test edebilirsiniz.

💾 Başlarken
🔹 1. Proje dosyasını indir
Repo'daki yolo.zip dosyasını indirip çıkar:

📦 Dosyayı indir (.zip)

Zip'i çıkarınca içinde predict.py, model dosyaları ve test klasörü bulunmalı.

🔹 2. Ortamı oluştur
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
🧪 Kullanım
🔸 Görsel Testi
Test etmek istediğiniz görselleri test/ klasörüne yerleştirin

Terminalden predict.py dosyasını çalıştırın:

bash
Copy
Edit
python predict.py
🔸 Çıktılar
Sonuç görselleri runs/detect/predict/ klasörüne kaydedilir. Tespit edilen STOP tabelaları görseller üzerinde kutu içinde gösterilir.

📌 Ek Bilgi
Proje sadece STOP tabelası tespiti üzerine odaklanmıştır.

Model eğitimi tamamlanmış olup, yeniden eğitim yapılmasına gerek yoktur.

.zip dosyası içinde tüm gerekli dosyalar mevcuttur.
