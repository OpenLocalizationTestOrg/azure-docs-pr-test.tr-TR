---
title: "aaaService Fabric uygulama yükseltme | Microsoft Docs"
description: "Bu makalede bir giriş tooupgrading seçme yükseltme modları ve gerçekleştirme durumu denetimleri de dahil olmak üzere bir Service Fabric uygulaması sağlar."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 803c9c63-373a-4d6a-8ef2-ea97e16e88dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 6f649ef4a5c0afab682522bcba7d2d66a4268ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade"></a>Service Fabric uygulaması yükseltme
Azure Service Fabric uygulama hizmetleri koleksiyonudur. Yükseltme sırasında Service Fabric hello yeni karşılaştırır [uygulama bildirimi](service-fabric-application-model.md#describe-an-application) hello önceki sürümüyle ve hangi hizmetlerin hello uygulamada güncelleştirmelerindeki belirler. Service Fabric hello sürüm numaraları hello hizmetindeki hello önceki sürümde hello sürüm numaralarıyla bildirimleri karşılaştırır. Bu hizmet, hizmet değişmemişse yükseltilmez.

## <a name="rolling-upgrades-overview"></a>Yükseltmeler genel bakış alınıyor
Çalışırken bir uygulama yükseltmede hello yükseltme aşamada gerçekleştirilir. Her aşamada hello yükseltme bir güncelleştirme etki alanı adında hello kümedeki düğümler uygulanan tooa alt kümesidir. Sonuç olarak, Merhaba uygulaması hello yükseltme kullanılabilir olarak kalır. Merhaba yükseltme sırasında hello küme hello eski ve yeni sürümleri bir karışımını içerebilir.

Bu nedenle, hello iki sürümleri ileriye ve geriye dönük uyumlu. Uyumlu değillerse, birden çok aşaması yükseltme toomaintain kullanılabilirlik hazırlama için Merhaba uygulama yönetici sorumludur. Bir çoklu aşama yükseltmesinin hello ilk adımı hello önceki sürümü ile uyumlu olup hello uygulama ara sürümü tooan yükseltiyor. Merhaba ikinci adım hello güncelleştirme öncesi sürümüyle uyumluluğu keser, ancak hello Ara sürümü ile uyumlu olup tooupgrade hello son sürümüdür.

Merhaba kümesini yapılandırırken güncelleştirme etki alanları hello küme bildiriminde belirtilir. Güncelleştirme etki alanları, belirli bir sırada güncelleştirmeleri almaz. Bir güncelleştirme etki alanı için bir uygulama dağıtımının mantıksal bir birimdir. Güncelleştirme etki alanları hello Hizmetleri tooremain yükseltme sırasında yüksek kullanılabilirlik sağlar.

Merhaba yükseltme uygulanan tooall kümedeki düğümler hello uygulama yalnızca bir güncelleştirme etki alanı varsa, hello durumdur hello ise olmayan çalışırken yükseltme mümkündür. Bu yaklaşım önerilmez, bu Hello hizmet arıza ve yükseltme hello aynı anda kullanılamaz. Ayrıca, bir küme yalnızca tek bir güncelleştirme etki alanı ile ayarlandığında, Azure garanti sağlamaz.

## <a name="health-checks-during-upgrades"></a>Yükseltme sırasında sistem durumu denetimleri
Bir yükseltme için sistem durumu ilkeleri ayarlamak toobe sahip (veya varsayılan değerleri kullanılabilir) kullanın. Yükseltme başarılı olarak adlandırılır belirtilen zaman aşımlarını tüm güncelleştirme etki alanları hello zaman yükseltilir ve tüm güncelleştirdiğinizde etki alanları sağlıklı olarak kabul edilen.  Sağlıklı güncelleştirme etki alanı hello güncelleştirme etki hello sistem durumu İlkesi'nde belirtilen tüm hello durumu denetimleri geçirilen anlamına gelir. Örneğin, bir sistem durumu ilkesi uygulama örneğini içindeki tüm hizmetler olmalıdır zorunlu kılabilir *sağlıklı*, sistem durumu Service Fabric tarafından tanımlanan.

Sistem durumu ilkeleri ve denetimler Service Fabric tarafından yükseltme sırasında hizmet ve uygulama bağımsızdır. Diğer bir deyişle, hizmete özgü testleri yapılır.  Örneğin, hizmetiniz bir işleme gereksinimi olabilir, ancak Service Fabric hello bilgi toocheck işleme sahip değil. Toohello başvuran [sistem durumu makaleleri](service-fabric-health-introduction.md) gerçekleştirilen hello denetimleri için. Merhaba örneği başlayıp başlamadığını hello uygulama paketi doğru kopyalanmıştır bir yükseltme INCLUDE testleri sırasında gerçekleşecek hello denetler ve benzeri.

Merhaba uygulama sistem hello alt varlıkları hello uygulamasının toplamı olur. Kısacası, Service Fabric hello uygulaması üzerinde bildirilen hello sistem durumu üzerinden hello uygulama hello durumunu değerlendirir. Ayrıca bu şekilde hello uygulama için tüm hello Hizmetleri hello durumunu değerlendirir. Daha fazla Service Fabric hello hizmet çoğaltma gibi bunların alt öğeleri hello durumunu toplayarak hello uygulama hizmetleri hello durumunu değerlendirir. Merhaba uygulama durumu ilkesi sağlanıyorsa sonra hello yükseltme devam edebilirsiniz. Merhaba sistem durumu ilkesi ihlal hello uygulama yükseltme başarısız olur.

## <a name="upgrade-modes"></a>Yükseltme modları
Uygulama yükseltme için önerdiğimiz hello modu yaygın olarak kullanılan hello modu izlenen hello modudur. İzlenen modu tek bir güncelleştirme etki alanında hello yükseltme gerçekleştirir ve tüm sistem durumu denetliyorsa (her hello İlkesi) belirtilen, geçişi taşır toohello sonraki güncelleştirme etki alanında otomatik olarak.  Sistem durumu denetimi başarısız ve/veya zaman aşımları ulaşıldığında, hello yükseltme ya da hello güncelleştirme etki alanı için geri ya da değiştirilmiş toounmonitored el ile Merhaba modudur. Yükseltme toochoose hello başarısız yükseltmeler için bu iki moddan birini yapılandırabilirsiniz. 

İzlenmeyen el ile moduna el ile müdahale her bir güncelleştirme etki alanında yükseltme, hello yükseltme hello sonraki güncelleştirme etki alanı dışı tookick sonra gerekir. Herhangi bir Service Fabric sistem durumu denetimi gerçekleştirilir. Hello Yöneticisi hello sonraki güncelleştirme etki alanında hello Yükseltmeyi başlatmadan önce hello sistem durumu veya durum denetimi gerçekleştirir.

## <a name="upgrade-default-services"></a>Varsayılan Hizmetleri yükseltme
Service Fabric uygulaması içindeki varsayılan Hizmetleri hello yükseltme sırasında bir uygulama yükseltilebilir. Varsayılan Hizmetleri hello tanımlanmış [uygulama bildirimi](service-fabric-application-model.md#describe-an-application). Varsayılan Hizmetleri yükseltme hello standart kurallar şunlardır:

1. Varsayılan hello yeni Hizmetleri'nde [uygulama bildirimi](service-fabric-application-model.md#describe-an-application) hello kümede olmayan oluşturulur.
> [!TIP]
> [EnableDefaultServicesUpgrade](service-fabric-cluster-fabric-settings.md#fabric-settings-that-you-can-customize) toobe kuralları aşağıdaki tootrue tooenable hello kümesinin. Bu özellik, v5.5 desteklenir.

2. Varsayılan hem de önceki varolan hizmetlerini [uygulama bildirimi](service-fabric-application-model.md#describe-an-application) ve yeni sürümü güncelleştirilir. Hizmet açıklamasında hello yeni sürüm zaten hello küme de üzerine yazacak. Uygulama yükseltme varsayılan hizmet hatası güncelleştirme sırasında otomatik olarak geri alma olacaktır.
3. Varsayılan hello önceki Hizmetleri'nde [uygulama bildirimi](service-fabric-application-model.md#describe-an-application) ancak hello yeni sürümde değil silinir. **Bu silme varsayılan Hizmetleri değil döndürülebilir unutmayın.**

Bir uygulamaya yükseltme döndürülüyor durumunda, yükseltmeyi başlatmadan önce varsayılan döndürülen toohello durum hizmetleridir. Ancak silinmiş Hizmetleri hiçbir zaman oluşturulabilir.

## <a name="application-upgrade-flowchart"></a>Uygulama yükseltme akış çizelgesi
Bu paragraf aşağıdaki hello akış çizelgesi, bir Service Fabric uygulaması hello yükseltme işlemini anlamanıza yardımcı olabilir. Özellikle, hello akışını açıklar nasıl da dahil olmak üzere zaman aşımları,'ı hello *HealthCheckStableDuration*, *HealthCheckRetryTimeout*, ve *UpgradeHealthCheckInterval*, Merhaba yükseltme tek bir güncelleştirme etki alanındaki bir başarı veya hata olarak kabul edildiğinde denetlemenize yardımcı olur.

![Service Fabric uygulaması için Hello yükseltme işlemi][image]

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama kullanarak Visual Studio yükseltme](service-fabric-application-upgrade-tutorial.md) Visual Studio kullanarak bir uygulama yükseltme yol gösterir.

[Uygulama Powershell kullanarak yükseltme](service-fabric-application-upgrade-tutorial-powershell.md) PowerShell kullanarak bir uygulama yükseltme yol gösterir.

Uygulamanızı kullanarak yükseltme nasıl kontrol [yükseltme parametreleri](service-fabric-application-upgrade-parameters.md).

Uygulama yükseltme öğrenme tarafından uyumlu hale getirmek nasıl toouse [veri seri hale getirme](service-fabric-application-upgrade-data-serialization.md).

Uygulamanız çok başvurarak yükseltirken toouse işlevselliği nasıl Gelişmiş öğrenin[Gelişmiş konular](service-fabric-application-upgrade-advanced.md).

Toohello adımlarda başvurarak uygulama yükseltmeleri sık karşılaşılan sorunları düzeltmek [sorun giderme uygulama yükseltmelerini](service-fabric-application-upgrade-troubleshooting.md).

[image]: media/service-fabric-application-upgrade/service-fabric-application-upgrade-flowchart.png
