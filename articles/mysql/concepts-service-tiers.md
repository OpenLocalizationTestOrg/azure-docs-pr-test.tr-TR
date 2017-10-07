---
title: "aaa \"Azure veritabanında MySQL için fiyatlandırma katmanları | Microsoft Docs\""
description: "MySQL için Azure veritabanında fiyatlandırma katmanları"
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 2a05f00aff4f7166f04e035eb2a47e7662888ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-options-and-performance-understand-whats-available-in-each-pricing-tier"></a>Azure veritabanı için MySQL seçenekleri ve performansı: her fiyatlandırma katmanında nelerin kullanılabildiğini anlama
MySQL sunucusu için bir Azure veritabanı oluşturduğunuzda, bu sunucu için ayrılan tooconfigure hello kaynaklar üzerinde üç ana seçeneğiniz karar verin. Bu seçenekler hello performansı ve ölçeği hello sunucusunun etkileyebilir.
- Fiyatlandırma katmanı
- İşlem Birimleri
- Depolama (GB)

Her fiyatlandırma katmanının bir iş yükleri gereksinimlerinize bağlı olarak, performans düzeyleri (işlem birimleri) toochoose sahiptir. Daha yüksek performans düzeyleri ek kaynaklar için sunucu tasarlanmış toodeliver daha yüksek verimliliği sağlayın. Neredeyse hiçbir uygulama kapalı kalma süresi ile bir fiyatlandırma katmanı içinde hello sunucunun performans düzeyini değiştirebilirsiniz.

> [!IMPORTANT]
> Genel önizlemede Hello hizmeti olmakla birlikte, garantili bir hizmet düzeyi sözleşmesi (SLA) yok.

MySQL sunucusu için Azure Veritabanı içinde bir veya birden fazla veritabanınız olabilir. Tüm hello kaynakları toocreate sunucu tooutilize başına tek bir veritabanı opt veya birden çok veritabanları tooshare hello kaynakları oluşturun. 

## <a name="choose-a-pricing-tier"></a>Fiyatlandırma katmanı seçin
Önizleme sırasında Azure veritabanı MySQL için iki fiyatlandırma katmanlarına sunar: temel ve standart. Premium katmanı henüz kullanılabilir değil ancak yakında çıkıyor. 

Merhaba aşağıdaki tabloda fiyatlandırma katmanları en iyi farklı uygulama iş yükleri için uygun hello örnekleri sağlar.

| Fiyatlandırma katmanı | Hedef iş yükleri |
| :----------- | :----------------|
| Temel | En iyi IOPS garanti olmadan ölçeklenebilir bilgi işlem ve depolama gerektiren küçük iş yükleri için uygundur. Geliştirme veya test için kullanılan sunucuları örnekler veya küçük ölçekli uygulamalar kullanılmayan. |
| Standart | Bulut için Git toooption hello IOPS ihtiyaç duyan uygulamalar garanti ile yüksek verimlilik. Web veya analitik uygulamaları örnek olarak verilebilir. |
| Premium | En düşük gecikme süresi işlemleri ve g/ç için gereken iş yükleri için uygundur. Merhaba en iyi desteği için çok sayıda eşzamanlı kullanıcıyı sağlar. İş açısından önemli uygulamaları destekleyen geçerli toodatabases.<br />Merhaba Premium fiyatlandırma katmanı Önizleme'de kullanılamaz. |

bir fiyatlandırma hakkında toodecide katmanı, İş yükünüzün bir IOPS garantisi gerekiyorsa belirleme tarafından ilk Başlat. Bu durumda, standart fiyatlandırma katmanı kullanın.

| **Fiyatlandırma katmanı özellikleri** | **Temel** | **Standart** |
| :------------------------ | :-------- | :----------- |
| En fazla işlem birimleri | 100 | 800 | 
| En fazla toplam depolama alanı | 1 TB | 1 TB | 
| Depolama IOPS garantisi | Yok | Evet | 
| Maksimum depolama IOPS | Yok | 3.000 | 
| Veritabanı yedekleme bekletme süresi | 7 gün | 35 gün | 

Merhaba Önizleme çerçevesine Hello sunucu oluşturulduktan sonra fiyatlandırma katmanı değiştirilemiyor. Hello gelecekteki, bu olası tooupgrade olması veya bir sunucudan bir fiyatlandırma katmanı tooanother katmanı düşürmek.

## <a name="understand-hello-price"></a>Merhaba fiyat anlama
Oluşturduğunuzda, yeni bir Azure veritabanı için MySQL hello içinde [Azure Portal](https://portal.azure.com/#create/Microsoft.MySQLServer), hello tıklatın **fiyatlandırma katmanı** dikey penceresinde ve aylık maliyeti hello gösterilecek tabanlı seçtiğiniz hello seçenekleri. Bir Azure aboneliğiniz yoksa, hello Azure fiyatlandırma hesaplayıcısı tooget tahmini fiyat kullanın. Hello ziyaret [Azure fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/) Web sitesi, ardından **Öğe Ekle**, hello genişletin **veritabanları** kategorisi ve seçin **Azure veritabanı için MySQL**  toocustomize hello seçenekleri.

## <a name="choose-a-performance-level-compute-units"></a>Bir performans düzeyine (işlem birimleri) seçin
MySQL sunucusu için Azure veritabanı fiyatlandırma katmanı hello belirledikten sonra hazır toodetermine hello performans düzeyi işlem gerekli birimlerin hello numarası seçerek demektir. İyi bir başlangıç noktası 200 veya 400 işlem kendi web veya analitik iş yükleri için yüksek kullanıcı eşzamanlılık gerektiren ve gerektiği gibi artırarak Ayarla uygulamaları birimidir. 

Birimleridir toobe kullanılabilir tooa garanti CPU işleme verimlilik ölçüsü işlem tek Azure veritabanı için MySQL sunucu. Bir işlem CPU ve bellek kaynakları oluşan karışık bir ölçüyü birimdir.  Daha fazla bilgi için bkz: [açıklayan işlem birimleri](concepts-compute-unit-and-storage.md)

### <a name="basic-pricing-tier-performance-levels"></a>Temel fiyatlandırma katmanı performans düzeyleri:

| **Performans düzeyi** | **50** | **100** |
| :-------------------- | :----- | :------ |
| En fazla işlem birimleri | 50 | 100 |
| Eklenen depolama boyutu | 50 GB | 50 GB |
| En fazla sunucu depolama boyutu\* | 1 TB | 1 TB |

### <a name="standard-pricing-tier-performance-levels"></a>Standart fiyatlandırma katmanı performans düzeyleri:

| **Performans düzeyi** | **100** | **200** | **400** | **800** |
| :-------------------- | :------ | :------ | :------ | :------ |
| En fazla işlem birimleri | 100 | 200 | 400 | 800 |
| Eklenen depolama boyutu ve sağlanan IOPS | 125 GB<br/> 375 IOPS | 125 GB<br/> 375 IOPS | 125 GB<br/> 375 IOPS | 125 GB<br/> 375 IOPS |
| En fazla sunucu depolama boyutu\* | 1 TB | 1 TB | 1 TB | 1 TB |
| En fazla sunucu IOPS sağlanması | 3000 IOPS | 3000 IOPS | 3000 IOPS | 3000 IOPS |
| IOPS GB başına en fazla sunucu sağlandı | Her GB sabit 3 IOPS | Her GB sabit 3 IOPS | Her GB sabit 3 IOPS | Her GB sabit 3 IOPS |

\*En fazla sunucu depolama boyutu sunucunuz için toohello sağlanan en fazla depolama boyutunu ifade eder.

## <a name="storage"></a>Depolama 
Merhaba depolama yapılandırması depolama kapasitesi, kullanılabilir MySQL sunucusu için tooan Azure veritabanı hello miktarını tanımlar. Hello hizmeti tarafından kullanılan hello depolama hello veritabanı dosyaları, işlem günlüklerinin ve hello MySQL server günlükleri içerir. Veritabanlarınızı gerekli depolama toohost Hello boyutunu göz önünde bulundurun ve performans gereksinimlerini (IOPS) hello depolama yapılandırması seçerken hello.

Bazı depolama kapasitesi, tablo "Eklenen depolama boyutu." olarak önceki hello Not her fiyatlandırma katmanının ile en az dahil Merhaba sunucu oluşturulduğunda toohello izin verilen maksimum depolama yukarı 125 GB artışlarla ek depolama kapasitesi eklenebilir. Merhaba ek depolama kapasitesi hello işlem birimleri yapılandırma bağımsız olarak yapılandırılabilir. Merhaba fiyat değişiklikleri Hello seçili depolama alanı miktarına göre.

her performans düzeyi Hello IOPS yapılandırmasında fiyatlandırma katmanı ve seçilen hello depolama boyutu toohello ilişkilendirir. Temel katman bir IOPS garanti sağlamaz. Merhaba standart fiyatlandırma katmanını içinde hello IOPS ölçeklendirme orantılı olarak toomaximum depolama boyutu bir sabit 3:1 oranında. 375 125 GB garantiler dahil hello depolanmasını IOPS, her bir g/ç boyutu too256 KB yukarı sağlandı. Ek depolama alanı too1 TB maksimum seçebilirsiniz, ancak tooguarantee 3, 000 IOPS sağlandı.

Merhaba ölçümleri hello Azure portal ya da yazma Azure CLI komutları toomeasure hello tüketimini depolama ve IOP grafiğinde izleyin. İlgili ölçümleri toomonitor: depolama sınırı, depolama yüzdesi, kullanılan depolama alanı ve g/ç yüzdesi.

>[!IMPORTANT]
> Önizleme sırasında depolama hello miktarını hello sunucu oluşturulduğunda hello aynı anda seçin. Varolan sunucuda Hello depolama boyutunu değiştirme henüz desteklenmiyor. 

## <a name="scaling-a-server-up-or-down"></a>Bir sunucu yukarı veya aşağı Ölçeklendirmesi
Başlangıçta, Azure veritabanı için MySQL oluşturduğunuzda fiyatlandırma katmanını ve performans düzeyi hello de seçin. Daha sonra işlem birimleri yukarı ya da dinamik olarak hello hello aralık içinde aynı aşağı hello ölçeklendirebilirsiniz fiyatlandırma katmanı. İçinde Azure portal Merhaba, hello sunucusunun fiyatlandırma katmanı dikey penceresinde hello işlem birimleri kaydırın veya bu örnek izleyerek betiği: [İzleyici ve ölçek Azure CLI kullanarak MySQL sunucusu için bir Azure veritabanı](scripts/sample-scale-server.md)

Merhaba işlem birimleri ölçeklendirme seçmiş olduğunuz hello en fazla depolama boyutunu bağımsız olarak gerçekleştirilir.

Hello perde arkasında bir veritabanı hello performans düzeyini değiştirme, hello yeni performans düzeyinde hello özgün veritabanının bir kopyasını oluşturur ve sonra bağlantıları toohello çoğaltma geçer. Hiçbir veri bu işlem sırasında kaybolur. Ne zaman biz toohello çoğaltma geçiş hello kısa süre sırasında bağlantıları toohello veritabanı devre dışı bırakıldı, yürütülen bazı işlemler geri alınamaz böylece. Bu pencere değişir, ancak ortalama olarak 4 saniyenin altındadır ve örneklerin %99’undan fazlasında 30 saniyeden daha kısadır. Varsa büyük sayılar hello şu anda bağlantıları, yürütülen işlemler devre dışı bırakıldı, bu pencereyi daha uzun olabilir.

Merhaba tüm ölçek işlemin Hello süresi hello boyutu hem fiyatlandırma katmanı önce hello sunucusunun ve hello değiştirdikten sonra bağlıdır. Örneğin, işlem birimleri hello standart fiyatlandırma katmanını içinde değiştiriyor. bir sunucu tamamlamanız gereken birkaç dakika içinde. Merhaba değişiklikler tamamlanana kadar hello sunucu için yeni özellikleri hello uygulanmaz.

## <a name="next-steps"></a>Sonraki Adımlar
- İşlem birimleri hakkında daha fazla bilgi için bkz: [açıklayan işlem birimleri](concepts-compute-unit-and-storage.md)
- Nasıl çok öğrenin[İzleyici ve ölçek Azure CLI kullanarak MySQL sunucusu için bir Azure veritabanı](scripts/sample-scale-server.md)
