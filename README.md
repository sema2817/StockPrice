# Stock-Price
# Amazon Hisse Senedi Fiyat Tahmini (LSTM & GRU)

## Genel Bakış
Bu proje, **Amazon (AMZN) hisse senedi kapanış fiyatlarını** tahmin etmek için **RNN tabanlı derin öğrenme modelleri** (LSTM ve GRU) kullanmaktadır.  
Amaç, geçmiş fiyat verilerini kullanarak gelecekteki kapanış fiyatlarını öngörmek ve farklı RNN mimarilerinin performansını karşılaştırmaktır.  

Finansal zaman serileri, yüksek volatilite ve karmaşık bağımlılıklar içerdiğinden, klasik regresyon yöntemleri yerine **LSTM (Long Short-Term Memory)** ve **GRU (Gated Recurrent Unit)** gibi gelişmiş sekans modelleri tercih edilmiştir.  

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

Aşağıdaki adımlar, projeyi kendi bilgisayarınızda çalıştırmak için izlenmesi gereken basit yönergeleri içerir.

### Gerekli Kütüphaneleri Yükleyin
Proje için gerekli Python kütüphanelerini yüklemek üzere terminal veya Anaconda Prompt’a aşağıdaki komutu yazın:
```bash
pip install numpy pandas matplotlib scikit-learn torch torchvision torchaudio seaborn jupyterlab
