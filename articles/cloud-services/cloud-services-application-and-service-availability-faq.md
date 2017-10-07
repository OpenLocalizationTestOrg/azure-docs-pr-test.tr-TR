---
title: "Microsoft Azure bulut Hizmetleri ile ilgili SSS aaaApplication ve hizmet kullanılabilirliği sorunlarını | Microsoft Docs"
description: "Bu makalede sık sorulan Microsoft Azure bulut Hizmetleri için uygulama ve hizmet kullanılabilirliği hakkında sorular hello listelenmektedir."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: cd0d9ba0beb1dc72d4761f8b89c2ecadb51c7e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Uygulama ve hizmet kullanılabilirliği sorunlarını Azure Cloud Services: sık sorulan sorular (SSS)

Bu makale, uygulama ve hizmet kullanılabilirliği sorunlarını hakkında sık sorulan sorular içermektedir [Microsoft Azure bulut Hizmetleri](https://azure.microsoft.com/services/cloud-services). Merhaba de başvurabilirsiniz [bulut Hizmetleri VM boyutu sayfa](cloud-services-sizes-specs.md) boyutu bilgi.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a>My rol geri aldı. My bulut hizmeti için toplu herhangi bir güncelleştirme oluştu?
Kabaca ayda bir kez Microsoft yeni bir konuk işletim sistemi sürümü Windows Azure PaaS VM'ler için serbest bırakır. Konuk işletim sistemi yalnızca bir tür hello ardışık düzeninde güncelleştirmesidir. Bir yayın birçok diğer faktörler tarafından etkilenebilir. Ayrıca, Azure yüz binlerce makineler üzerinde çalışır. Bu nedenle imkansız toopredict hello tam tarihi ve saati rollerinizi ne zaman yeniden olur. Biz sahip hello en son bilgilerle hello konuk işletim sistemi güncelleştirme RSS akışı güncelleştiriyoruz ancak zaman toobe yaklaşık bir değer bildirilen göz önünde bulundurmanız gerekir. Biz bu müşteriler için sorunlu olduğunu farkında olduğundan ve bir plan toolimit veya tam olarak zaman yeniden başlatmalar çalışma.

Yeni konuk işletim sistemi güncelleştirmeleri hakkında tam Ayrıntılar için bkz: [Azure konuk işletim sistemi sürümleri ve SDK uyumluluk matrisi](cloud-services-guestos-update-matrix.md).

Merhaba MSDN blog gönderisi Konuk ve ana bilgisayar işletim sistemi güncelleştirmelerinin yeniden başlatılır ve işaretçileri tootechnical ayrıntıları yararlı bilgi için bkz [rol örneği yeniden son tooOS yükseltmeler](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).

## <a name="why-does-hello-first-request-toomy-cloud-service-after-hello-service-has-been-idle-for-some-time-take-longer-than-usual"></a>Merhaba hizmet biraz zaman boşta kaldıktan sonra hello ilk istek toomy bulut hizmeti neden normalden daha uzun sürer?
Merhaba Web sunucusu hello ilk isteği aldığında, önce hello kodu yeniden derler ve hello isteğini işler. Bu neden hello uzun ilk isteği alır başkalarının hello olduğu. Varsayılan olarak, hello uygulama havuzu kullanıcı etkinlik durumlarda kapatıldı. Merhaba uygulama havuzu da varsayılan olarak 1,740 dakikada (29 saat) geri.

Internet Information Services (IIS) uygulama havuzları tooapplication çökme (Crash), askıda veya bellek sızıntıları açabilir düzenli aralıklarla geri dönüştürüldüğünde tooavoid kararsız durumlar olabilir.

Aşağıdaki belgeler hello anlamanıza ve bu sorunu azaltmak yardımcı olur:
* [IIS için yavaş ilk yük çözme](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [Uygulama havuzu geri dönüşümü çok yavaş sonra IIS 7.5 web uygulaması ilk istek](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

IIS toochange hello varsayılan davranışını isterseniz, değişiklikleri toohello Web rolü örneklerini elle uygularsanız, hello değişiklikleri sonunda kaybolacağı için toouse başlangıç görevleri, gerekir.

Daha fazla bilgi için bkz: [nasıl tooconfigure ve çalıştırma başlangıç için bir bulut hizmeti görevleri](cloud-services-startup-tasks.md).
