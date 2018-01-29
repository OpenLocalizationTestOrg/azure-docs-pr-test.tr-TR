---
title: "MySQL için Azure veritabanında fiyatlandırma katmanları | Microsoft Docs"
description: "MySQL için Azure veritabanında fiyatlandırma katmanları"
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 11/03/2017
ms.openlocfilehash: ae7e57e9b40f5194c15525a48843060bbccaa956
ms.sourcegitcommit: 38c9176c0c967dd641d3a87d1f9ae53636cf8260
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/06/2017
---
# <a name="azure-database-for-mysql-options-and-performance-understand-whats-available-in-each-pricing-tier"></a>Azure veritabanı için MySQL seçenekleri ve performansı: her fiyatlandırma katmanında nelerin kullanılabildiğini anlama
MySQL sunucusu için bir Azure veritabanı oluşturduğunuzda, bu sunucu için ayrılan kaynaklar yapılandırmak için üç ana seçeneğiniz bağlı karar verin. Bu seçenek, performansı ve sunucunun ölçeği etkileyebilir.
- Fiyatlandırma katmanı
- İşlem Birimleri
- Depolama (GB)

Her fiyatlandırma katmanının bir seçebileceğiniz, iş yüklerini gereksinimlerinize bağlı olarak performans düzeyleri (işlem birimleri) sahiptir. Daha yüksek performans düzeyleri daha yüksek verimlilik sağlamak üzere tasarlanmış sunucunuz için ek kaynaklar sağlar. Neredeyse hiçbir uygulama kapalı kalma süresi ile bir fiyatlandırma katmanı içinde sunucu performans düzeyini değiştirebilirsiniz.

> [!IMPORTANT]
> Hizmeti genel önizlemede olsa da, garantili bir hizmet düzeyi sözleşmesi (SLA) yok.

MySQL sunucusu için Azure Veritabanı içinde bir veya birden fazla veritabanınız olabilir. Tüm kaynakları kullanmak için sunucu başına tek bir veritabanı oluşturmayı veya kaynakları paylaşmak için birden çok veritabanı oluşturmayı seçebilirsiniz. 

## <a name="choose-a-pricing-tier"></a>Fiyatlandırma katmanı seçin
Önizleme sırasında Azure veritabanı MySQL için iki fiyatlandırma katmanlarına sunar: temel ve standart. Premium katmanı henüz kullanılabilir değil ancak yakında çıkıyor. 

Aşağıdaki tabloda, en iyi fiyatlandırma katmanları farklı uygulama iş yükleri için uygun örnekleri sağlar.

| Fiyatlandırma katmanı | Hedef iş yükleri |
| :----------- | :----------------|
| Temel | En iyi IOPS garanti olmadan ölçeklenebilir bilgi işlem ve depolama gerektiren küçük iş yükleri için uygundur. Geliştirme veya test için kullanılan sunucuları örnekler veya küçük ölçekli uygulamalar kullanılmayan. |
| Standart | Bulut için gidilecek seçeneği IOPS ihtiyaç duyan uygulamalar garanti ile yüksek verimlilik. Web veya analitik uygulamaları örnek olarak verilebilir. |
| Premium | En düşük gecikme süresi işlemleri ve g/ç için gereken iş yükleri için uygundur. Çok sayıda eşzamanlı kullanıcı için en iyi desteği sağlar. İş açısından önemli uygulamaları destekleyen veritabanları için geçerlidir.<br />Premium fiyatlandırma katmanı Önizleme'de kullanılamaz. |

Fiyatlandırma katmanı olarak karar vermek için önce İş yükünüzün bir IOPS garantisi gerekiyorsa belirleyerek başlayın. Bu durumda, standart fiyatlandırma katmanı kullanın.

| **Fiyatlandırma katmanı özellikleri** | **Temel** | **Standart** |
| :------------------------ | :-------- | :----------- |
| En fazla işlem birimleri | 100 | 800 | 
| En fazla toplam depolama alanı | 1 TB | 1 TB | 
| Depolama IOPS garantisi | Yok | Evet | 
| Maksimum depolama IOPS | Yok | 3.000 | 
| Veritabanı yedekleme bekletme süresi | 7 gün | 35 gün | 

Sunucu oluşturulduktan sonra Önizleme çerçevesine fiyatlandırma katmanı değiştirilemiyor. Gelecekte, yükseltme veya indirgeme bir fiyatlandırma katmanı bir sunucudan başka bir katmana mümkün olacaktır.

## <a name="understand-the-price"></a>Fiyat anlama
İçinde MySQL için yeni bir Azure veritabanı oluşturduğunuzda [Azure portal](https://portal.azure.com/#create/Microsoft.MySQLServer)seçin **fiyatlandırma katmanı** sayfası ve aylık maliyeti gösterilir tabanlı seçtiğiniz seçenekleri. Bir Azure aboneliğiniz yoksa, Azure fiyatlandırma hesaplayıcısı tahmini fiyatı almak için kullanın. Ziyaret [Azure fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/) Web sitesi, ardından **Öğe Ekle**, genişletin **veritabanları** kategorisi ve seçin **Azure veritabanı için MySQL** seçenekleri özelleştirmek için.

## <a name="choose-a-performance-level-compute-units"></a>Bir performans düzeyine (işlem birimleri) seçin
MySQL sunucusu için Azure veritabanı fiyatlandırma katmanı belirledikten sonra işlem gerekli birim sayısını seçerek performans düzeyini belirlemek hazırsınız. İyi bir başlangıç noktası 200 veya 400 işlem kendi web veya analitik iş yükleri için yüksek kullanıcı eşzamanlılık gerektiren ve gerektiği gibi artırarak Ayarla uygulamaları birimidir. 

MySQL sunucusu için tek bir Azure veritabanı için kullanılabilir olmasını garanti CPU işleme verimlilik ölçü birimleridir işlem. Bir işlem CPU ve bellek kaynakları oluşan karışık bir ölçüyü birimdir.  Daha fazla bilgi için bkz: [açıklayan işlem birimleri](concepts-compute-unit-and-storage.md)

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

\*En fazla sunucu depolama boyutu sunucunuz için en fazla sağlanan depolama boyutunu ifade eder.

## <a name="storage"></a>Depolama 
Depolama yapılandırması kullanılabilir depolama kapasitesi miktarını MySQL sunucusu için bir Azure veritabanı tanımlar. Veritabanı dosyaları, işlem günlüklerinin ve MySQL sunucu günlükleri hizmeti tarafından kullanılan depolama alanını içerir. Veritabanlarınızı ve performans gereksinimlerini (IOPS) depolama yapılandırması seçerken barındırmak için gerekli depolama alanının boyutunu göz önünde bulundurun.

Bazı depolama kapasitesi "Eklenen depolama boyutu." olarak önceki tabloda belirtildiği her fiyatlandırma katmanının ile en az bulunur Sunucu oluşturulduğunda izin verilen maksimum depolama kadar 125 GB artışlarla ek depolama kapasitesi eklenebilir. Ek depolama kapasitesi işlem birimleri yapılandırma bağımsız olarak yapılandırılabilir. Seçili depolama alanı miktarına göre fiyat değişiklikleri.

Her performans düzeyi IOPS yapılandırmasında fiyatlandırma katmanı ve seçilen depolama boyutu ilgilidir. Temel katman bir IOPS garanti sağlamaz. Standart fiyatlandırma katmanı içinde IOPS için bir sabit 3:1 oranında en fazla depolama boyutunu orantılı olarak ölçeklendirilir. 375 125 GB garantiler dahil depolanmasını IOPS, her bir g/ç boyutu en fazla 256 KB ile sağlandı. Ek depolama alanı 1 TB en fazla 3000 sağlanan IOPS güvence altına almak için seçebileceğiniz.

Azure portalında ölçümleri grafiği izlemek veya depolama ve IOP tüketiminin ölçmek için Azure CLI komutları yazın. İzlemek için ilgili depolama sınırı, depolama yüzdesi, kullanılan depolama alanı ve g/ç yüzde ölçümleridir.

>[!IMPORTANT]
> Önizleme sırasında depolama alanı miktarını sunucu oluşturulduğunda aynı anda seçin. Varolan sunucuda depolama boyutunu değiştirme henüz desteklenmiyor. 

## <a name="scaling-a-server-up-or-down"></a>Bir sunucu yukarı veya aşağı Ölçeklendirmesi
Azure veritabanı için MySQL oluşturduğunuzda, başlangıçta fiyatlandırma katmanını ve performans düzeyini seçin. Daha sonra işlem birimleri ölçeklendirebilirsiniz yukarı veya dinamik olarak aynı fiyatlandırma katmanı aralık içinde aşağı. Azure portalında işlem birimleri sunucusunun fiyatlandırma katmanı sayfasında kaydırın veya bu örnek izleyerek betiği: [İzleyici ve ölçek Azure CLI kullanarak MySQL sunucusu için bir Azure veritabanı](scripts/sample-scale-server.md)

İşlem birimleri ölçeklendirme seçmiş olduğunuz en fazla depolama boyutunu bağımsız olarak gerçekleştirilir.

Arka planda bir sunucu performans düzeyini değiştirme, yeni performans düzeyinde özgün sunucunun bir kopyasını oluşturur ve ardından kopyalanan sunucuya bağlantıları geçer. Hiçbir veri bu işlem sırasında kaybolur. Yürütülen bazı işlemler geri alınamaz böylece sunucunun yeni kopya için ne zaman sistem geçer kısa süre sırasında veritabanı bağlantılarını, devre dışı bırakılır. Bu pencere değişir, ancak ortalama olarak 4 saniyenin altındadır ve örneklerin %99’undan fazlasında 30 saniyeden daha kısadır. Bağlantıların devre dışı bırakıldığı sırasında uçuşta çok fazla işlem varsa, bu süre uzayabilir.

Hem boyutu hem de önce ve fiyatlandırma katmanı sunucusunun değişiklikten sonra tüm ölçek işleminin süresi bağlıdır. Örneğin, işlem birimleri standart fiyatlandırma katmanı içinde değiştiriyor. bir sunucu tamamlamanız gereken birkaç dakika içinde. Sunucu için yeni özellikleri değişiklikler tamamlanana kadar uygulanmaz.

## <a name="next-steps"></a>Sonraki adımlar
- İşlem birimleri hakkında daha fazla bilgi için bkz: [açıklayan işlem birimleri](concepts-compute-unit-and-storage.md)
- Bilgi edinmek için nasıl [İzleyici ve ölçek Azure CLI kullanarak MySQL sunucusu için bir Azure veritabanı](scripts/sample-scale-server.md)
