---
title: "PostgreSQL için işlem birimleri Azure veritabanındaki açıklayan | Microsoft Docs"
description: "Azure DB PostgreSQL için: Bu makalede işlem birimleri ve işleminizi iş yükü en fazla işlem birimleri ulaştığında olanlar kavramlarını açıklar."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6077e52f60c7ef0afe7df9201ec05081ba81c179
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="explaining-compute-units-in-azure-database-for-postgresql"></a>Azure veritabanı işlem birimleri için PostgreSQL açıklayan
Bu makalede kavramını işlem birimleri ve işleminizi iş yükü en fazla işlem birimleri ulaştığında ne olacağını açıklar.

## <a name="what-are-compute-units"></a>İşlem birimleri nelerdir?
Tek bir Azure veritabanı PostgreSQL sunucu için kullanılabilir olmasını garanti CPU işleme verimlilik ölçü birimleridir işlem. Bir işlem CPU ve bellek kaynakları oluşan karışık bir ölçüyü birimdir. Genel olarak, 50 işlem birimleri yarısı çekirdek eşitlemek. 100 işlem birimleri için bir çekirdek eşitlemek. Garantili işleme sn'ye sunucunuza kullanılabilir yirmi çekirdekleri 2000 işlem birimleri eşitlemek.

İşlem birim başına bellek miktarını temel ve standart fiyatlandırma katmanları için optimize edilmiştir. Performans düzeyinin artırarak işlem birimleri Katlama, kaynağın tek Azure veritabanına kullanılabilir kümesi PostgreSQL için Katlama için karşılık gelir.

Örneğin, bir standart 800 işlem birimleri 8 x daha fazla CPU işleme ve standart 100 işlem birimleri yapılandırma daha bellek sağlar. Ancak, standart 100 işlem birimleri temel 100 birimlerine işlem karşılaştırıldığında aynı CPU verimliliği sağlayın, ancak standart fiyatlandırma katmanında önceden yapılandırılmış bellek miktarı çift temel fiyatlandırma katmanı için yapılandırılmış bellek miktarı ' dir. Bu nedenle, daha iyi iş yükü performans standart fiyatlandırma katmanı sağlar ve aynı işlem birimleri ile temel fiyatlandırma katmanı daha düşük işlem gecikme seçtiniz.

## <a name="how-can-i-determine-the-number-of-compute-units-needed-for-my-workload"></a>İşlem my iş yükü için gereken birim sayısını nasıl belirleyebilirim?
Şirket içi çalıştıran varolan bir PostgreSQL sunucusu geçirmek için aradığınız isterseniz bir sanal makinede, iş yükü işleme sn'ye kaç çekirdek gerekiyor tahminlerle işlem birim sayısını belirleyebilirsiniz. 

Mevcut şirket içi veya sanal makine sunucu şu anda 4 çekirdek (CPU hiper iş parçacığı sayımı olmadan) kullanılarak olduğundan, PostgreSQL server için Azure veritabanınızın 400 işlem birimleri yapılandırarak başlatın. İşlem birimleri dinamik olarak yukarı veya aşağı neredeyse hiçbir uygulama kapalı kalma süresi ile iş yükü gereksinimlerinize bağlı olarak genişletilebilir. 

Ölçümleri Azure portalında grafik veya Azure CLI yazma İzleyicisi - işlem birimleri ölçmek için kullanılan komutlar. İzlemek için ilgili işlem birim yüzdesi ve işlem birim sınırı ölçümleridir.

>[!IMPORTANT]
> En büyük IOPS tam olarak kullanılmaz depolama bulursanız, işlem birimleri kullanımı da izleme göz önünde bulundurun. İşlem birimleri oluşturma sınırlı CPU veya bellek nedeniyle performans düşüklüğü lessening tarafından daha yüksek g/ç işleme için izin verebilir.

## <a name="what-happens-when-i-hit-my-maximum-compute-units"></a>My en fazla işlem birimleri isabet ne olur?
Performans düzeyleri kalibre ve veritabanının yükünüzü seçilen fiyatlandırma katmanını ve performans düzeyi için en fazla sınırlarına kadar çalıştırmak için kaynaklar sağlamak için kapsamındadır. 

İş yükünüzün ya da işlem birimleri en fazla sınırları veya sağlanan IOPS sınırları ulaşırsa, en çok izin verilen düzeyi kaynakları kullanmaya devam edebilirsiniz, ancak sorgularınızı daha yüksek gecikme görmeniz olasıdır. Yavaşlama zaman aşımı sorgular nedenle önemli hale sürece bu sınırları hataları, ancak bunun yerine iş yavaşlama neden değil. 

İş yükünüzün en fazla bağlantı sayısı sınırlamaları ulaşırsa, açık hatalar ortaya çıkar. Kaynakları sınırları hakkında daha fazla bilgi için bkz: [PostgreSQL Azure veritabanındaki sınırlamalar](concepts-limits.md).

## <a name="next-steps"></a>Sonraki adımlar
Fiyatlandırma katmanları hakkında daha fazla bilgi için bkz: [Azure veritabanı fiyatlandırma katmanlarına PostgreSQL için](./concepts-service-tiers.md).
