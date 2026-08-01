# Stock Price Prediction with PyTorch (LSTM vs GRU)

Bu proje, PyTorch kullanılarak zaman serisi analizi ile hisse senedi (Amazon - AMZN) fiyatlarının tahmin edilmesini amaçlamaktadır. Projede LSTM ve GRU olmak üzere iki farklı Derin Öğrenme (RNN) modeli kullanılmış ve performansları karşılaştırılmıştır. 

Makine öğrenmesine yeni giriş yaptığım için kodları mümkün olduğunca sade tutmaya ve temel adımları (veri işleme, model kurma, eğitim ve test) adım adım uygulamaya çalıştım. Lineer cebir dersinde gördüğüm matris mantığını tensör boyutlarını ayarlarken bol bol kullanmam gerekti.

## Kullanılan Veriseti
Yahoo Finance kütüphanesi (`yfinance`) kullanılarak Amazon'un son 10 yıllık kapanış fiyatları ("Close") çekilmiştir. Veriler, modellerin daha iyi öğrenebilmesi için `MinMaxScaler` ile -1 ve 1 aralığına normalize edilmiştir. 

Sliding window (kayan pencere) yöntemiyle, geçmiş 20 günlük fiyatlara (lookback=20) bakılarak 21. günün fiyatı tahmin edilmeye çalışılmıştır.

## Kurulum ve Çalıştırma
Projeyi çalıştırmak için aşağıdaki kütüphanelerin yüklü olması gerekiyor:
- `torch`
- `pandas`
- `numpy`
- `yfinance`
- `scikit-learn`
- `matplotlib`

Jupyter Notebook'u sırayla yukarıdan aşağıya çalıştırdığınızda veriyi çekecek, eğitecek ve en sonda karşılaştırma grafiklerini çizecektir.

## Değerlendirme ve Sonuçlar
Modellerin başarısını ölçmek için Hata Kareler Ortalaması (MSE) kullanıldı:
$MSE = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$

**Test Sonuçları:**
- LSTM eğitim süresi GRU'ya göre biraz daha uzun sürdü.
- GRU modeli daha az parametreye sahip olduğu için (hidden state yapısı daha basit) yaklaşık %15 daha hızlı çalıştı.
- Test verisi üzerinde GRU, LSTM'e çok yakın hatta bir tık daha düşük bir MSE değeri verdi. 

İki model de hisse senedi fiyatının genel trendini yakalamayı başardı ancak ani dalgalanmalarda (örneğin pandeminin başlarındaki düşüşler) gecikmeli tepki verdiklerini gözlemledim. Finansal veriler sadece geçmiş fiyatlara bağlı olmadığı için %100 kesin bir tahmin yapmak zaten zor.

sunumu aşağıdaki linkten izleyebilirsiniz

https://drive.google.com/file/d/1dR_JegDAGNJuTCLjhDdZA3mY92oJyC3L/view?usp=sharing
