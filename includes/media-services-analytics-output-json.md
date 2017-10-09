Merhaba iş algılanan ve izlenen yüzeyleri hakkında meta veriler içeren bir JSON çıktı dosyası oluşturur. Merhaba meta verileri yüzeyleri hello konumunu yanı sıra, bir yazıtipi kimliği numara belirten hello izlenmesini bu tek tek gösteren koordinatları içerir. Merhaba tamamen çıplak yüz kaybolduğunda veya hello çerçevede çakışan yüz kimliği koşullarda yatkın tooreset birden çok kimliği atanan bazı kişiler kaynaklanan numaralarıdır.

Merhaba hello öznitelikleri aşağıdaki JSON içerir çıktı:

| Öğesi | Açıklama |
| --- | --- |
| Sürüm |Bu toohello hello Video API sürümü ifade eder. |
| Dizin | (Yalnızca medya Redactor tooAzure geçerlidir) hello geçerli olay hello çerçeve dizini tanımlar. |
| Zaman Çizelgesi |"Hello videonun saniyede"çizgilerine. |
| uzaklık |Tarih damgası başlangıç zaman farkı budur. Video API'leri 1.0 sürümünde, bu her zaman 0 olacaktır. Gelecekte destekliyoruz senaryoları, bu değeri değiştirebilirsiniz. |
| Kare hızı |Saniyedeki kare sayısı hello video. |
| Parçaları |Merhaba meta verilerini yukarı parçaları olarak adlandırılan farklı kesimler halinde öbekli. Her parça başlangıç, süre, aralığı sayısı ve olay içerir. |
| start |Merhaba başlangıç saati 'ticks' hello ilk olay. |
| Süre |Merhaba parçadaki "çizgilerine" Merhaba uzunluğu. |
| interval |her olay girişi hello parçadaki "çizgilerine" içinde Hello aralığı. |
| etkinlikler |Her olay algılandı ve bu süre içinde izlenen hello yüzeyleri içerir. Olaylar dizisi dizisidir. Merhaba dış dizi bir zaman aralığı temsil eder. Merhaba iç dizi 0 veya zamandaki o noktada daha fazla olayları oluşur. Boş köşeli ayraç [] hiçbir yüzeyleri algılandı anlamına gelir. |
| id |izlenmekte olan hello yüz Hello kimliği. Bu sayı, bir yazıtipi algılanmayan hale gelirse yanlışlıkla değişebilir. Belirli bir birey aynı kimliği hello genel video hello olmalıdır, ancak bu son garanti edilemez hello algılama algoritması (kapanması, vb.) toolimitations |
| x, y |sol üst X ve Y koordinatları 0.0 too1.0 normalleştirilmiş ölçeğinde kutusu sınırlayıcı hello yazıtipinin hello. <br/>-X ve Y koordinatları her göreli toolandscape zaman, bir dikey video (veya görüntülemediğini, iOS hello durumda) varsa, tootranspose hello koordinatları uygun şekilde gerekir. |
| Genişlik, yükseklik |Merhaba genişlik ve yükseklik 0.0 too1.0 normalleştirilmiş ölçeğinde kutusu sınırlayıcı hello yazıtipinin. |
| facesDetected |Bu hello hello JSON sonuçları sonunda bulunan ve video hello sırasında algılanan bu hello algoritması yüzeyleri hello sayısı özetlenmektedir. Bir yazıtipi algılanmayan hale gelirse hello kimlikleri yanlışlıkla sıfırlanabilir olmadığından (örneğin yüz gider ekranı, hemen görünür), bu her zaman hello true sayısı, yüzler hello videoda eşit değil. |

