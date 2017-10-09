---
title: "Azure mikro aaaSpecify ölçümleri ve yerleştirme ayarları | Microsoft Docs"
description: "Service Fabric hizmeti, ölçümler, yerleştirme kısıtlamaları ve diğer yerleşim ilkeleri belirterek açıklayan."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 16e135c1-a00a-4c6f-9302-6651a090571a
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c633518b5dbf0c7b84e0d46c06bf1f92365d184d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-cluster-resource-manager-settings-for-service-fabric-services"></a>Service Fabric Hizmetleri için küme kaynak yönetici ayarlarını yapılandırma
Merhaba Service Fabric kümesi Kaynak Yöneticisi adlı hizmetin her kişi yöneten hello kurallarını üzerinde ayrıntılı denetim sağlar. Her adlandırılmış hizmet hello kümesinde nasıl ayrılmalıdır kuralları belirtebilirsiniz. Her adlandırılmış hizmet tooreport ne kadar önemli toothat hizmet oldukları dahil olmak üzere, istediği ölçümleri hello kümesi de tanımlayabilirsiniz. Hizmetleri yapılandırma üç farklı görevlere parçalara ayırır:

1. Yerleştirme kısıtlamalarını yapılandırma
2. Ölçümleri yapılandırma
3. Gelişmiş yerleşim ilkeleri ve diğer kurallar (daha az ortak) yapılandırma

## <a name="placement-constraints"></a>Yerleştirme kısıtlamaları
Yerleştirme kullanılan toocontrol hello kümedeki hangi düğümlerin bir hizmeti aslında üzerinde çalışabilir sınırlamalardır. Tipik olarak belirli bir hizmet örneği veya belirli bir düğüm türü üzerinde belirtilen türle kısıtlı toorun tüm hizmetlerin adlı. Kısıtlamalarından genişletilebilir. Tüm düğüm türü başına özellikler kümesini tanımlar ve sonra bunlar için kısıtlamalarıyla Hizmetleri oluştururken seçin. Çalışırken bir hizmetin kısıtlamalarından de değiştirebilirsiniz. Bu, toorespond toochanges hello küme veya hello gereksinimleri hello hizmet sağlar. belirli bir düğümün Hello özelliklerini de hello kümede dinamik olarak güncelleştirilebilir. Yerleştirme kısıtlamaları ve nasıl tooconfigure bunları bulunabilir hakkında daha fazla bilgi [bu makalede](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)

## <a name="metrics"></a>Ölçümler
Ölçüm, belirli bir adlandırılmış hizmeti gereken kaynakların hello kümesidir. Bir hizmet ölçüm yapılandırmasının varsayılan olarak her bir durum bilgisi olan çoğaltma veya hizmet durum bilgisiz örneğiniz tüketir bu kaynağın ne kadarının içerir. Ölçümleri bileşim gerekli olduğu durumlarda, toothat hizmeti, ölçüm Dengeleme ne kadar önemli olduğunu belirten bir ağırlık de içerir.

## <a name="advanced-placement-rules"></a>Gelişmiş yerleştirme kuralları
Diğer kullanışlı daha az yaygın senaryolar yerleştirme kuralı türü vardır. Bazı örnekler şunlardır:
- Coğrafi olarak dağıtılmış kümeleriyle yardım eden kısıtlamaları
- Belirli uygulama mimarisi

Diğer yerleştirme kuralları bağıntıları veya ilkeleri aracılığıyla yapılandırılır.

## <a name="next-steps"></a>Sonraki adımlar
- Kullanım ve kapasite hello kümedeki hello Service Fabric kümesi kaynak yöneticisi nasıl yönettiğini ölçümleridir. Ölçümler hakkında daha fazla toolearn ve nasıl tooconfigure bunları kullanıma [bu makalede](service-fabric-cluster-resource-manager-metrics.md)
- Benzeşim hizmetlerinizi için yapılandırabileceğiniz bir moddur. Ortak değildir, ancak ihtiyacınız varsa onu hakkında bilgi edinebilirsiniz [burada](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
- Hizmet toohandle ek senaryolarınızı üzerinde yapılandırılmış birçok farklı yerleştirme kuralları vardır. Bu farklı yerleşim ilkeleri hakkında bilgi almak [burada](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
- Merhaba baştan başlatın ve [giriş toohello Service Fabric kümesi Kaynak Yöneticisi Al](service-fabric-cluster-resource-manager-introduction.md)
- toofind hello Küme Kaynak Yöneticisi yönetir ve dengeleyen hello kümedeki yük hakkında hello makalesine üzerinde kullanıma [Yük Dengeleme](service-fabric-cluster-resource-manager-balancing.md)
- Merhaba küme Resource Manager hello küme açıklamak için birçok seçeneğiniz vardır. toofind bunlarla ilgili daha fazla bilgi, bu makalede denetleyin [açıklayan bir Service Fabric kümesi](service-fabric-cluster-resource-manager-cluster-description.md)
