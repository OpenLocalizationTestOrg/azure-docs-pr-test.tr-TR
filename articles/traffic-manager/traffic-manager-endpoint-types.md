---
title: "aaaTraffic Yöneticisi uç nokta türleri | Microsoft Docs"
description: "Bu makalede, Azure Traffic Manager ile kullanılan uç noktalarını farklı türleri açıklanmaktadır."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 4e506986-f78d-41d1-becf-56c8516e4d21
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: kumud
ms.openlocfilehash: 787412ac6207f76791bf3ff753d1df2767b1a964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoints"></a>Traffic Manager uç noktaları
Microsoft Azure trafik Yöneticisi nasıl ağ trafiğidir toocontrol verir dağıtılmış farklı veri merkezlerinde çalışan tooapplication dağıtımları. Trafik Yöneticisi'nde her uygulama dağıtımı 'Bitiş' olarak yapılandırın. Trafik Yöneticisi DNS isteği aldığında, kullanılabilir uç nokta tooreturn hello DNS yanıtı seçer. Trafik Yöneticisi hello seçim hello geçerli uç nokta durumu ile Merhaba trafik yönlendirme yöntemini temel alır. Daha fazla bilgi için bkz: [nasıl trafik Yöneticisi çalışır](traffic-manager-how-traffic-manager-works.md).

Uç nokta Traffic Manager tarafından desteklenen üç tür vardır:
* **Azure uç noktaları** Azure içinde barındırılan hizmetler için kullanılır.
* **Dış uç noktalar** dış Azure, hem şirket içinde barındırılan hizmetlere veya farklı bir barındırma sağlayıcısı ile kullanılır.
* **İç içe uç noktaları** kullanılan toocombine trafik Yöneticisi profilleri toocreate daha esnek trafik yönlendirme düzenleri toosupport hello ihtiyaçlarını daha büyük ve daha karmaşık dağıtımlar şunlardır.

Farklı türlerdeki uç noktaları içinde tek bir trafik Yöneticisi profili nasıl birleştirilir üzerinde herhangi bir kısıtlama yoktur. Her profil uç nokta türlerinin bir karışımını içerebilir.

Aşağıdaki bölümlerde hello daha derinlemesine her uç nokta türü açıklanmaktadır.

## <a name="azure-endpoints"></a>Azure uç noktaları

Azure uç noktaları Azure tabanlı hizmetler trafik Yöneticisi'nde için kullanılır. şu Azure kaynak türlerini hello desteklenir:

* Bulut Hizmetleri 'Klasik' Iaas Vm'leri ve PaaS.
* Web Apps
* (Olabilen bağlı tooVMs doğrudan veya bir Azure yük dengeleyici üzerinden) Publicıpaddress kaynaklar. Hello Publicıpaddress bir Traffic Manager profilini kullanılan toobe atanmış bir DNS adı olmalıdır.

Publicıpaddress, Azure Resource Manager kaynaklarını kaynaklardır. Merhaba Klasik dağıtım modelinde mevcut değil. Bu nedenle yalnızca desteklenir trafik Yöneticisi'nin Azure Resource Manager deneyimleri oldukları. Merhaba diğer uç nokta türleri Resource Manager ve hello Klasik dağıtım modeli aracılığıyla desteklenir.

'Klasik' Iaas VM, bulut hizmeti veya bir Web uygulaması durdurulduğunda ve başlatıldığında Azure uç noktaları kullanırken, trafik Yöneticisi algılar. Bu durum hello uç nokta durumu yansıtılır. Bkz: [trafik Yöneticisi uç nokta izleme](traffic-manager-monitoring.md#endpoint-and-profile-status) Ayrıntılar için. Arka plandaki hizmet hello durdurulduğunda, trafik Yöneticisi uç noktası durumu denetimleri veya doğrudan trafiği toohello endpoint gerçekleştirmez. Hiçbir trafik Yöneticisi için hello fatura olaylarından örneği durdurdu. Merhaba hizmeti yeniden başlatıldığında, sürdürür faturalama ve hello uç noktası uygun tooreceive trafiği olduğunda. Bu algılama tooPublicIpAddress uç noktaları geçerli değildir.

## <a name="external-endpoints"></a>Dış uç noktalar

Dış uç noktalar dışında Azure Hizmetleri için kullanılır. Örneğin, bir hizmeti şirket içi barındırılan veya farklı bir sağlayıcı ile. Dış uç noktalar tek başına kullanılan ya da hello Azure uç noktaları ile birlikte aynı trafik Yöneticisi profili. Azure uç noktaları dış uç noktalar ile birleştirerek çeşitli senaryolara olanak sağlar:

* Ya da bir yük devretme etkin-etkin veya etkin-pasif modelinde, artan Azure tooprovide artıklık için mevcut şirket içi uygulama kullanın.
* tooreduce uygulama gecikme Merhaba Dünya kullanıcılar için bir mevcut şirket içi uygulama tooadditional coğrafi konumlarda Azure genişletir. Daha fazla bilgi için bkz: ['Performans' Traffic Manager trafik yönlendirme](traffic-manager-routing-methods.md#performance).
* Azure tooprovide ek kapasite olan bir şirket içi uygulamanın sürekli olarak ya da 'veri bloğu-bulut' çözümü toomeet bir ani talep olarak kullanın.

İsteğe bağlı olarak bazı durumlarda, yararlı toouse dış uç noktalar tooreference Azure olan Hizmetleri (Merhaba örnekler için bkz [SSS](traffic-manager-faqs.md#traffic-manager-endpoints)). Bu durumda, sistem durumu denetimlerinin hello Azure uç noktaları hızında, hello dış uç noktalar oranı faturalandırılır. Ancak, Azure uç noktaları, durdurmak veya hizmetini, arka plandaki hello silerseniz sistem durumu denetimi faturalama devre dışı bırakır veya trafik Yöneticisi'nde hello uç noktasını silmek kadar devam eder.

## <a name="nested-endpoints"></a>İç içe geçmiş uç noktaları

İç içe geçmiş uç noktalar birden çok trafik Yöneticisi profilleri toocreate esnek trafik yönlendirme şemasını birleştirmek ve daha büyük ve karmaşık dağıtımlar hello gereksinimlerini destekler. İç içe uç ile bir 'alt' profili bir uç nokta tooa 'parent' profili eklenir. Her iki hello alt ve üst profilleri diğer uç noktaları diğer iç içe profil de dahil olmak üzere, her tür içerebilir. Daha fazla bilgi için bkz: [iç içe trafik Yöneticisi profillerine](traffic-manager-nested-profiles.md).

## <a name="web-apps-as-endpoints"></a>Web uygulamaları uç noktalar olarak

Web Apps trafiği Manager'da uç noktalar olarak yapılandırırken bazı hususlar geçerlidir:

1. Yalnızca Web uygulamaları hello 'Standart' SKU veya üstü, trafik Yöneticisi ile kullanılması için uygundur. Bir Web uygulaması daha düşük bir SKU başarısız tooadd çalışır. Merhaba eski sürüme düşürmeyi var olan bir Web uygulamasının SKU'su trafiği artık trafiği toothat Web uygulaması gönderme Yöneticisi'nde sonuçlanır.
2. Bir uç nokta bir HTTP isteği aldığında, hello 'konağı' üstbilgisinde hello isteği toodetermine hangi Web uygulaması hizmet hello istemeniz gerekir kullanır. Merhaba ana bilgisayar üstbilgisi hello DNS ad kullanılan tooinitiate hello isteği, örneğin 'contosoapp.azurewebsites.net' içerir. Merhaba uygulama için bir özel etki alanı adı olarak toouse farklı bir DNS adı, Web uygulamanızın hello DNS adı ile kayıtlı olması gerekir. Azure uç noktası olarak bir Web uygulaması uç noktası eklerken, hello trafik Yöneticisi profili DNS adı Merhaba uygulama otomatik olarak kaydedilir. Merhaba endpoint silindiğinde, bu kayıt otomatik olarak kaldırılır.
3. Her trafik Yöneticisi profili en çok bir Web uygulaması uç nokta her Azure bölgesinden olabilir. Bu kısıtlama için toowork geçici bir Web uygulaması bir dış uç noktası olarak yapılandırabilirsiniz. Daha fazla bilgi için bkz: Merhaba [SSS](traffic-manager-faqs.md#traffic-manager-endpoints).

## <a name="enabling-and-disabling-endpoints"></a>Etkinleştirme ve uç noktaları devre dışı bırakma

Bir uç nokta trafik Yöneticisi'nde devre dışı bırakma yararlı tootemporarily Kaldır Bakım modu veya yeniden dağıtılmakta olan bir uç nokta trafiğinden olabilir. Merhaba uç nokta yeniden çalışır duruma geldiğinde yeniden etkinleştirilebilir.

Uç noktaları etkin ve hello trafik Yöneticisi portal, PowerShell, CLI ya da hem Resource Manager hem de hello Klasik dağıtım modeli desteklenen REST API aracılığıyla devre dışı.

> [!NOTE]
> Azure uç noktası devre dışı bırakma, sahip hiçbir şey toodo azure'da dağıtım durumuna sahip. Bir Azure hizmet gibi (bir VM veya Web uygulaması bile trafik Yöneticisi'nde devre dışı bırakıldığında çalışıp çalışmadığını ve tooreceive trafiği kalır. Toohello örneği hizmet yerine doğrudan DNS adı hello trafik Yöneticisi Profil trafiği çözülebilir. Daha fazla bilgi için bkz: [trafik Yöneticisi nasıl çalıştığını](traffic-manager-how-traffic-manager-works.md).

her uç nokta tooreceive trafiği geçerli uygunluğunu Hello Etkenler aşağıdaki hello üzerinde bağlıdır:

* hello profil durumu (etkin/devre dışı)
* Merhaba uç nokta durumu (etkin/devre dışı)
* Bu uç hello sistem durumu denetimlerinin Hello sonuçlarını

Ayrıntılar için bkz [trafik Yöneticisi uç nokta izleme](traffic-manager-monitoring.md#endpoint-and-profile-status).

> [!NOTE]
> Trafik Yöneticisi DNS düzeyi hello çalışır olduğundan, oluşturulamıyor tooinfluence varolan bağlantılar tooany uç noktadır. Bir uç nokta kullanılamaz duruma geldiğinde, trafik Yöneticisi yeni bağlantıları tooanother kullanılabilir uç nokta yönlendirir. Ancak, bu oturumlar durduruluncaya kadar devre dışı hello veya sağlıksız endpoint arkasındaki hello konak tooreceive trafiği varolan bağlantılar yoluyla devam edebilir. Uygulamaları hello oturum süresi tooallow trafiği toodrain varolan bağlantılardan sınırlamanız gerekir.

Bir profildeki tüm uç noktaları devre dışı bırakılmışsa veya hello profili kendisi devre dışı bırakılırsa, Traffic Manager bir 'NXDOMAIN' yanıt tooa yeni DNS sorgusu gönderir.


## <a name="next-steps"></a>Sonraki adımlar

* Bilgi [trafik Yöneticisi nasıl çalıştığını](traffic-manager-how-traffic-manager-works.md).
* Trafik Yöneticisi hakkında bilgi edinin [uç nokta izleme ve otomatik yük devretme](traffic-manager-monitoring.md).
* Trafik Yöneticisi hakkında bilgi edinin [trafik yönlendirme yöntemleri](traffic-manager-routing-methods.md).
