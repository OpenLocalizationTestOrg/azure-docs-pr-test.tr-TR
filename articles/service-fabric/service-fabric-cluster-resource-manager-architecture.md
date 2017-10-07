---
title: "aaaResource Yöneticisi Mimarisi | Microsoft Docs"
description: "Service Fabric Küme Kaynağı Yöneticisi'nin mimari bir özeti."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 6c4421f9-834b-450c-939f-1cb4ff456b9b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9ea80273d0566a2ac25143ada3662875656b57b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-architecture-overview"></a>Küme kaynak Yönetici Mimarisine Genel Bakış
Merhaba Service Fabric kümesi Kaynak Yöneticisi hello kümede çalışan merkezi bir hizmettir. İstenen hello özellikle saygı tooresource tüketim ve herhangi bir yerleştirme kuralı ile Merhaba kümede hello hizmetlerinin durumunu yönetir. 

toomanage hello kaynakları kümenizdeki hello Service Fabric kümesi Resource Manager çeşitli bilgi parçalarını sahip olmanız gerekir:

- Hangi Hizmetleri şu anda var
- Her hizmet geçerli (veya varsayılan) kaynak tüketimi 
- Merhaba kalan küme kapasite 
- Merhaba kümedeki hello düğümler Hello kapasitesi 
- Her bir düğümde tüketilen kaynaklarının Hello miktarı

belirli bir hizmeti Hello kaynak tüketimini zamanla değişebilir ve Hizmetleri genellikle birden çok kaynak türü hakkında dikkat edin. Farklı hizmetler arasında ölçülen gerçek fiziksel ve fiziksel kaynakları olabilir. Hizmetleri, bellek ve disk kullanımı gibi fiziksel ölçümleri izleyebilirsiniz. Daha yaygın olarak, hizmetler, mantıksal ölçümleri - "WorkQueueDepth" veya "TotalRequests" gibi şeyleri önem verdiğiniz. Mantıksal ve fiziksel ölçümleri hello kullanılabilir aynı küme. Ölçümleri birçok hizmetleri arasında paylaşılabilir veya belirli tooa belirli bir hizmet olmalıdır.

## <a name="other-considerations"></a>Diğer konular
Merhaba sahipleri ve işleçler hello kümenin farklı olabilir hizmet ve uygulama yazarları hello veya en düşük olan aynı farklı şapkası kartı kişiler hello. Uygulamanızı geliştirirken hangi gerektirdiğini hakkında birkaç şey bildirin. Tahmini sahip tüketen kaynakları ve farklı Hizmetleri hello dağıtılması gerekir. Örneğin, Hello veritabanı hizmetleri vermemelisiniz sırada hello web katmanı açığa düğümleri toohello Internet üzerinde toorun gerekir. Başka bir örnek olarak, hello web Hizmetleri büyük olasılıkla CPU ve bellek ve disk kullanımı hakkında daha fazla hello veri katmanı Hizmetleri bakım sırasında ağ tarafından kısıtlanmıştır. Ancak, işleme Canlı site olay üretimde bu hizmet için veya bir yükseltme toohello hizmeti yönettiği hello kişi farklı iş toodo var ve farklı araçlar gerektiriyor. 

Merhaba küme ve Hizmetleri dinamik şunlardır:

- Merhaba hello kümedeki düğüm sayısını büyür ve küçültme
- Farklı boyutlarda ve türleri düğümlerinin dönün ve Git
- Hizmetleri kaldırılmış oluşturulabilir ve onların istenen kaynak ayırma ve yerleştirme kuralları değiştirme
- Yükseltme veya diğer yönetim işlemleri hello küme hello uygulama aracılığıyla altyapı düzeylerini geri alabilirsiniz
- Herhangi bir zamanda hataları oluşabilir.

## <a name="cluster-resource-manager-components-and-data-flow"></a>Küme Kaynak Yöneticisi bileşenleri ve veri akışı
Merhaba Küme Kaynak Yöneticisi, bu hizmetlerin içindeki her hizmet nesnesi tarafından her hizmet ve hello tüketiminin kaynakların tootrack hello gereksinimleri vardır. Merhaba küme Resource Manager da iki kavramsal bölümden oluşur: her düğüm ve hataya dayanıklı bir hizmeti çalıştıran aracılar. Her düğüm izleme yük Hello aracısında Hizmetleri'nden toplama bunları bildirir ve düzenli aralıklarla rapor. Merhaba Küme Kaynak Yöneticisi hizmeti hello yerel aracılardan gelen tüm hello bilgi toplayan ve geçerli yapılandırmasına göre tepki verir.

Diyagram aşağıdaki hello bakalım:

<center>
![Kaynak dengeleyici mimarisi][Image1]
</center>

Çalışma zamanı sırasında meydana gelebilir birçok değişiklik yoktur. Örneğin, hello tutar düşünelim kaynakları bazı hizmetlerini değişiklikleri, bazı hizmetleri başarısız kullanma ve bazı düğümler katılma ve hello küme bırakın. Bir düğümdeki tüm hello değişiklikleri toplanır ve düzenli aralıklarla burada bunlar yeniden birleştirilir, analiz ve depolanan toohello Küme Kaynak Yöneticisi Hizmeti'ni (1,2) gönderilir. Hizmet hello değişikliklerini arar ve herhangi bir eylem gerekli olup olmadığını belirleyen her birkaç saniyede (3). Örneğin, bazı boş düğümleri toohello kümeye eklenmiş fark. Sonuç olarak, bazı hizmetleri toothose düğümleri toomove verir. Merhaba Küme Kaynak Yöneticisi ayrıca belirli bir düğüme aşırı yüklendiğinde veya belirli hizmetleri başarısız veya silinmiş, fark başka bir yerde kaynakları serbest bırakma.

Şimdi diyagramı aşağıdaki hello bakın ve ne olacağını bakın. Şimdi deyin küme Resource Manager'ı hello değişikliklerin gerekli olduğunu belirler. Diğer sistem hizmetleri (belirli hello Yük Devretme Yöneticisi) toomake hello gerekli değişiklikleri düzenler. Ardından hello gerekli komutları toohello uygun düğümler (4) gönderilir. Örneğin, Resource Manager Düğüm5 fazlaydı ve bu nedenle Düğüm5 tooNode4 B hizmetinden toomove karar fark hello varsayalım. Merhaba yeniden yapılandırma (5) Hello sonunda hello küme şöyle görünür:

<center>
![Kaynak dengeleyici mimarisi][Image2]
</center>

## <a name="next-steps"></a>Sonraki adımlar
- Merhaba küme Resource Manager hello küme açıklamak için birçok seçeneğiniz vardır. toofind bunlarla ilgili daha fazla bilgi, bu makalede denetleyin [açıklayan bir Service Fabric kümesi](./service-fabric-cluster-resource-manager-cluster-description.md)
- Merhaba Küme Kaynak Yöneticisi'nin birincil görevlerini hello küme dengelenmesi ve yerleştirme kuralları uygulanması. Bu davranışların yapılandırma hakkında daha fazla bilgi için bkz: [Dengeleme Service Fabric kümesi](./service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-1.png
[Image2]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-2.png
