---
title: "Sık kullanılan otomatik ölçeklendirme desenlerini aaaOverview | Microsoft Docs"
description: "Azure'da hello ortak desenler tooauto bazıları kaynağınız ölçeklendirmek öğrenin."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a>Sık kullanılan otomatik ölçeklendirme desenlerini genel bakış
Bu makalede, Azure kaynak hello ortak desenler tooscale bazıları açıklanmaktadır.

Azure İzleyici otomatik ölçek tooVirtual makine ölçek kümeleri (VMSS), bulut Hizmetleri, uygulama hizmeti planları ve uygulama hizmeti ortamları yalnızca geçerlidir. 

# <a name="lets-get-started"></a>Sağlar kullanmaya başlama

Bu makalede, otomatik ölçekli bilgi sahibi olduğunuzu varsayar. Yapabilecekleriniz [başlatılan burada tooscale, kaynak alma][1]. Merhaba hello ortak ölçek desenler bazıları verilmiştir.

## <a name="scale-based-on-cpu"></a>CPU üzerinde göre ölçeklendirin

Bir web uygulaması (/ VMSS/bulut hizmeti rolü) sahip ve 

- Tooscale istediğiniz çıkış/dayalı olarak CPU ölçek.
- Ayrıca, tooensure istediğiniz en az bir örnek sayısı yoktur. 
- Ayrıca, bir şekilde ölçeklendirebilirsiniz örnekleri sınırı toohello sayısını ayarlayın tooensure istiyor.

![CPU üzerinde göre ölçeklendirin][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a>Haftanın günü vs hafta sonu farklı ölçeklendirme

Bir web uygulaması (/ VMSS/bulut hizmeti rolü) sahip ve

- Varsayılan olarak (günlerinde) 3 örneklerinin istediğiniz
- Hafta sonu trafiği beklemeyen ve bu nedenle hafta sonu too1 örneği aşağı tooscale istiyorsunuz.

![Haftanın günü vs hafta sonu farklı ölçeklendirme][3]

## <a name="scale-differently-during-holidays"></a>Farklı tatilleri ölçeklendirme

Bir web uygulaması (/ VMSS/bulut hizmeti rolü) sahip ve 

- Yukarı/Aşağı CPU kullanımında varsayılan olarak temel tooscale istediğiniz
- Ancak, tatilde (veya işletmeniz için önemli olan belirli gün) sırasında toooverride hello Varsayılanları istediğiniz ve elinizin daha fazla kapasiteye sahip.

![Ölçek farklı üzerinde tatiller][4]

## <a name="scale-based-on-custom-metric"></a>Özel bir ölçü göre ölçeklendirin

Bir web ön uç ve hello arka ucuyla iletişim kuran bir API katmanı vardır. 

- Özel olaylar hello ön uçtaki göre tooscale hello API katmanı istediğiniz (örnek: Merhaba alışveriş sepeti hello öğelerin sayısı temel kullanıma alma işleminizi tooscale istediğiniz)

![Özel bir ölçü göre ölçeklendirin][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png