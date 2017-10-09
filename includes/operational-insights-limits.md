
>[!NOTE]
>Log Analytics daha önce Operasyonel Öngörüler olarak biliniyordu.
>
>

sınırları aşağıdaki hello tooLog analizi kaynaklarını abonelik başına uygulanır:

| Kaynak | Varsayılan Sınır | Yorumlar
| --- | --- | --- |
| Abonelik başına ücretsiz çalışma alanı sayısı | 10 | Bu sınır yükseltilemez. |
| Abonelik başına ücretli çalışma alanı sayısı | Yok | Kaynakları bir kaynak grubu içinde hello sayısı ve kaynak grupları abonelik başına sayısı sınırlıdır | 


sınırları aşağıdaki hello tooeach günlük analizi çalışma alanı Uygula:

|  | Ücretsiz | Standart | Premium | Tek Başına | OMS |
| --- | --- | --- | --- | --- | --- |
| Gün başına toplanan veri birimi |500 MB<sup>1</sup> |None |None | None | None
| Veri saklama süresi |7 gün |1 ay |12 ay | 1 ay<sup>2</sup> | 1 ay <sup>2</sup>|

<sup>1</sup> müşteriler kendi 500 MB günlük veri aktarım sınırına ulaştığında, veri analizi durdurur ve sonraki gün hello hello başlangıcında sürdürür. Bir gün için UTC temel alınır.

<sup>2</sup> hello tek başına ve fiyatlandırma planı OMS hello veri bekletme süresini, artan too730 gün olabilir.

| Kategori | Sınırlar | Yorumlar
| --- | --- | --- |
| Veri Toplayıcı API’si | Tek bir gönderi için boyut üst sınırı 30 MB'tır<br>Alan değerleri için en büyük boyut 32 KB'dir | Büyük hacimleri birden fazla gönderiye bölme<br>32 KB'den daha uzun alanlar kesilir. |
| Arama API’si | Toplu olmayan veriler için 5000 kayıt döndürülür<br>Toplu veriler için 500000 kayıt döndürülür | Birleşik verilerdir hello içeren bir arama `measure` komutu
 
