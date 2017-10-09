Aşağıdaki tablonun hello hello ana kotaları, sınırları, Varsayılanları ve Azure Scheduler kısıtlamaları açıklar.

| Kaynak | Sınır açıklaması |
| --- | --- |
| **İş boyutu** |Maksimum iş boyutu 16 K'dır. PUT veya bir düzeltme eki bu sınırlardan daha büyük bir işin sonuçlanırsa, 400 Hatalı istek durum kodu döndürülür. |
| **İstek URL boyutu** |En fazla hello istek URL'si 2048 karakter boyutudur. |
| **Toplam üstbilgi boyutu** |En fazla toplam üstbilgi boyutu 4096 karakter değil. |
| **Üstbilgi sayısı** |En fazla üstbilgi, 50 üstbilgileri sayısıdır. |
| **Gövde boyutu** |En fazla gövdesi, 8192 karakter boyutudur. |
| **Yineleme aralığı** |En fazla yineleme aralığı 18 ay ' dir. |
| **Zamanı toostart süresi** |"Zaman toostart zaman" en fazla 18 ay ' dir. |
| **İş geçmişi** |İş geçmişinde depolanan en büyük yanıt gövdesi 2048 bayttır. |
| **Sıklık** |Merhaba varsayılan max sıklığı kota, 1 saat içinde bir ücretsiz iş koleksiyonu ve 1 dakika içinde bir standart iş koleksiyonu ' dir. Merhaba max sıklığı hello en büyük daha düşük bir iş koleksiyonu toobe üzerinde yapılandırılabilir. Merhaba iş koleksiyonundaki tüm işleri hello iş koleksiyonu üzerinde sınırlı hello değerlerdir. Toocreate hello iş koleksiyonu üzerinde hello maksimum sıklığından daha yüksek bir sıklık işlemiyle çalışırsanız isteği 409 çakışma durum kodu ile başarısız olur. |
| **İşler** |Hello varsayılan en büyük iş kotası ücretsiz iş koleksiyonu 5 işler ve 50 işler standart iş koleksiyonu ' dir. Merhaba en fazla iş sayısı üzerinde bir iş koleksiyonu yapılandırılabilir. Merhaba iş koleksiyonundaki tüm işleri hello iş koleksiyonu üzerinde sınırlı hello değerlerdir. Toocreate çalışırsanız hello en büyük iş kotası sonra hello isteği'den daha fazla iş 409 çakışma durum kodu ile başarısız olur. |
| **İş koleksiyonları** |En fazla iş koleksiyonu abonelik başına 200.000 sayısıdır. |
| **İş Geçmişi bekletme** |İş geçmişi için too2 ayda korunur veya toohello 1000 yürütmeleri son. |
| **Tamamlanan ve hatalı iş bekletme** |Tamamlanan ve hatalı işler 60 gün boyunca saklanır. |
| **Zaman aşımı** |Bir statik (yapılandırılamaz) istek zaman aşımı süresi 60 saniye HTTP eylemler için yoktur. Uzun çalışan işlemleri için zaman uyumsuz HTTP protokolleri izleyin; Örneğin, bir 202 hemen geri ancak hello arka planda çalışmaya devam. |

