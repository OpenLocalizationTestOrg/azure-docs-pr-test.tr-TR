---
title: "PostgreSQL için işlem birimleri Azure veritabanındaki açıklayan | Microsoft Docs"
description: "Azure DB PostgreSQL için: Bu makalede, işlem birimleri ve İş yükünüzün ulaştığında olanlar hello kavramlarını hello en fazla işlem birimleri açıklanmaktadır."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 42ec766ff6ce82ceee34d42e0f4a4ad86bc7b45d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-compute-units-in-azure-database-for-postgresql"></a>Azure veritabanı işlem birimleri için PostgreSQL açıklayan
Bu makalede, işlem birimleri hello kavramını ve en fazla işlem birimleri, iş yükü ulaştığında hello ne olur açıklanmaktadır.

## <a name="what-are-compute-units"></a>İşlem birimleri nelerdir?
Birimleridir toobe kullanılabilir tooa garanti CPU işleme verimlilik ölçüsü işlem PostgreSQL sunucusu için tek bir Azure veritabanı. Bir işlem CPU ve bellek kaynakları oluşan karışık bir ölçüyü birimdir. Genel olarak, bir çekirdek toohalf 50 işlem birimleri eşitlemek. 100 işlem birimleri tooone çekirdek eşitlemek. 2000 işlem birimleri tootwenty çekirdek garantili işleme verimlilik kullanılabilir tooyour sunucusunun eşitlemek.

İşlem birim başına bellek miktarını Hello hello temel ve standart fiyatlandırma katmanları için optimize edilmiştir. Merhaba performans düzeyi artırarak Hello işlem birimleri Katlama karşılık gelir toodoubling hello kaynak kullanılabilir toothat kümesi PostgreSQL için tek bir Azure veritabanı.

Örneğin, bir standart 800 işlem birimleri 8 x daha fazla CPU işleme ve standart 100 işlem birimleri yapılandırma daha bellek sağlar. Ancak, standart 100 işlem birimleri sunarken aynı hello CPU işleme tooBasic 100 işlem birimleri karşılaştırıldığında, hello fiyatlandırma katmanı standart olarak önceden yapılandırılmış olan bellek miktarıdır çift hello fiyatlandırma katmanı Basic için yapılandırılmış bellek miktarı. Bu nedenle, daha iyi iş yükü performansını ve temel fiyatlandırma katmanı ile aynı işlem birimleri seçili hello daha düşük işlem gecikme standart fiyatlandırma katmanı sağlar.

## <a name="how-can-i-determine-hello-number-of-compute-units-needed-for-my-workload"></a>My iş yükü için gerekli birimlerin işlem hello sayısını nasıl belirleyebilirim?
Bir sanal makinede veya toomigrate şirket içi çalıştıran mevcut bir PostgreSQL sunucu arıyorsanız, iş yükü işleme sn'ye kaç çekirdek gerekiyor tahminlerle hello işlem birim sayısı belirleyebilirsiniz. 

Mevcut şirket içi veya sanal makine sunucu şu anda 4 çekirdek (CPU hiper iş parçacığı sayımı olmadan) kullanılarak olduğundan, PostgreSQL server için Azure veritabanınızın 400 işlem birimleri yapılandırarak başlatın. İşlem birimleri dinamik olarak yukarı veya aşağı neredeyse hiçbir uygulama kapalı kalma süresi ile iş yükü gereksinimlerinize bağlı olarak genişletilebilir. 

İzleyicisi Merhaba ölçümleri hello Azure portal ya da yazma Azure CLI komutları - toomeasure grafiğinde birimleri işlem. İlgili ölçümleri toomonitor hello işlem birim yüzdesi ve birim işlem sınırı olan.

>[!IMPORTANT]
> Toohello maksimum IOPS tam olmayan depolama kullanılan bulursanız, hello işlem birimleri kullanımı da izleme göz önünde bulundurun. Merhaba işlem birimleri oluşturma hello performans düşüklüğü toolimited CPU veya bellek nedeniyle lessening tarafından daha yüksek g/ç işleme için izin verebilir.

## <a name="what-happens-when-i-hit-my-maximum-compute-units"></a>My en fazla işlem birimleri isabet ne olur?
Performans düzeyleri ayarlandığından ve veritabanının yükünüzü hello seçilen fiyatlandırma katmanı ve performans düzeyi için en fazla sınırları toohello yukarı tooprovide kaynakları toorun kapsamındadır. 

İş yükünüzün da hello işlem birimleri en fazla sınırları hello veya sağlanan IOPS sınırları ulaşırsa, hello izin verilen en yüksek düzeyde tooutilize hello kaynakları devam edebilirsiniz, ancak sorgularınızı artan büyük olasılıkla toosee gecikmeleri şunlardır. Merhaba yavaşlama zaman aşımı sorgular nedenle önemli hale sürece bu sınırları hataları, ancak yerine yavaşlama hello iş yükü içinde neden değil. 

İş yükünüzün hello en fazla bağlantı sayısı sınırlamaları ulaşırsa, açık hatalar ortaya çıkar. Kaynakları sınırları hakkında daha fazla bilgi için bkz: [PostgreSQL Azure veritabanındaki sınırlamalar](concepts-limits.md).

## <a name="next-steps"></a>Sonraki adımlar
Fiyatlandırma katmanları hakkında daha fazla bilgi için bkz: [Azure veritabanı fiyatlandırma katmanlarına PostgreSQL için](./concepts-service-tiers.md).
