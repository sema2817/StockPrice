# Amazon Hisse Senedi Fiyat Tahmini (LSTM & GRU)

## Proje Özeti
Bu proje, **Amazon (AMZN)** hisse senedi kapanış fiyatlarını tahmin etmek için **RNN tabanlı derin öğrenme modelleri** (LSTM ve GRU) kullanmaktadır.  
Amaç, geçmiş fiyat verilerini kullanarak gelecekteki kapanış fiyatlarını öngörmek ve farklı RNN mimarilerinin performansını karşılaştırmaktır.  

Finansal zaman serileri yüksek volatilite ve karmaşık bağımlılıklar içerdiğinden, klasik regresyon yöntemleri yerine **LSTM (Long Short-Term Memory)** ve **GRU (Gated Recurrent Unit)** gibi gelişmiş sekans modelleri tercih edilmiştir.  

---

## Veri Seti
- **Kaynak:** `AMZN_2006-01-01_to_2018-01-01.csv`  
- **Özellikler:** Tarih, Açılış, Kapanış, En Yüksek, En Düşük, Hacim  
- **Kullanılan Değişken:** Kapanış fiyatları  
- **Ön İşleme:**
  - `MinMaxScaler` ile kapanış fiyatları **-1 ile 1** aralığına ölçeklendi.  
  - **Lookback:** 20 günlük geçmiş kapanış fiyatı kullanılarak bir sonraki gün tahmin edildi.  
  - Eğitim verisi `TensorDataset` ve `DataLoader` ile PyTorch formatına dönüştürüldü.  

---

## Kurulum ve Çalıştırma Adımları
Aşağıdaki adımlar, projeyi kendi bilgisayarınızda çalıştırmak için izlenmesi gereken yönergeleri içerir.

### 1. Gerekli Kütüphaneleri Yükleyin
```bash
pip install numpy pandas matplotlib scikit-learn torch torchvision torchaudio seaborn jupyterlab
```

### 2. Veri Dosyasını Yerleştirin
Amazon hisse fiyatları verisini (AMZN_2006-01-01_to_2018-01-01.csv) proje dizininde data/ klasörüne koyun.

### 3. JupyterLab’i Başlatın
- bash  
- jupyter lab  

### 4. Notebook’u Açın
StockPrice.ipynb dosyasını açın ve hücreleri sırayla çalıştırın.
Kod hücreleri sırasıyla:
  1. Veriyi yükler ve ölçekler  
  2. LSTM ve GRU modellerini tanımlar  
  3. Modelleri eğitir  
  4. Tahminleri ve grafik sonuçlarını üretir  

## Modelleme Yaklaşımı

LSTM Modeli
- Katmanlar: 1 LSTM katmanı + 1 Tam Bağlantılı (FC) katman  
- Kayıp Fonksiyonu: Mean Squared Error (MSE)  
- Optimizasyon: Adam optimizer (lr=0.001)  

GRU Modeli
- Katmanlar: 1 GRU katmanı + 1 FC katman  
- Kayıp Fonksiyonu: MSE  
- Optimizasyon: Adam optimizer (lr=0.001)  

Her iki model de 10 epoch boyunca eğitilmiş, ardından tahminler görselleştirilmiştir.

## Sonuçlar ve Değerlendirme
- LSTM Modeli MSE: 167.90  
- GRU Modeli MSE: 115.50  
GRU modeli, LSTM’e göre daha düşük hata ile daha iyi performans göstermiştir.  
Her iki model de kapanış fiyatlarını başarılı şekilde tahmin etmiştir.  

## Grafik Analizi
Grafiklerde mavi çizgi gerçek fiyatları, yeşil çizgi LSTM tahminlerini, turuncu çizgi ise GRU tahminlerini göstermektedir.
Her iki model genel trendi yakalamış, ancak GRU daha hızlı öğrenme eğilimi göstermiştir.


## Kısa Rapor
Bu çalışma, zaman serisi tahmininde RNN tabanlı modellerin gücünü göstermektedir.
LSTM ve GRU modelleri, geçmiş 20 günlük kapanış fiyatlarını kullanarak bir sonraki günün fiyatını tahmin etmiştir.
Sonuçlar, GRU modelinin daha düşük MSE değeriyle LSTM’e göre daha iyi performans sergilediğini ortaya koymuştur.

## Özetle:
- LSTM MSE ≈ 157.0  
- GRU MSE ≈ 92.0  
- LSTM RMSE≈ 12.5  
- GRU RMSE≈ 9.6  
GRU modeli daha hızlı öğrenmiş ve daha düşük hata oranı elde etmiştir.  

## Geliştirme Önerileri
- Daha uzun epoch sayısı ile modellerin performansı artırılabilir.  
- Farklı özellikler (hacim, açılış, en yüksek, en düşük) modele dahil edilerek çok değişkenli tahmin yapılabilir.  
- LSTM ve GRU’ya ek olarak Transformer tabanlı modeller denenebilir.  
