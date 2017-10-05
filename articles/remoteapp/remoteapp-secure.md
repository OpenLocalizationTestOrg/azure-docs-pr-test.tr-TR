---
title: "Güvenli uygulamalar ve Azure RemoteApp kaynaklarında | Microsoft Docs"
description: "Uygulamalar ve Azure RemoteApp kaynakları kilitleme öğrenin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 1c052906788f0f4fe4ca9fd6d3af63336245174a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>Güvenli uygulamalar ve Azure RemoteApp Kaynakları
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Azure RemoteApp kullanıcıların ne kullanıcılarınız ve yapamayacağı denetlemenize olanak sağlayan Windows uygulamalarını, merkezi olarak yönetilen erişmesini sağlar.  Bu kullanıcının yönetilmeyen bir CİHAZDAN (ör. kendi kişisel Macbook) bağlanma ve kullanıcı erişimini denetlemek veya deneyimi istediğinizde özellikle yararlıdır.

Örneğin, kullanıcı kimlik doğrulaması için Active Directory'yi kullanarak ve kullanıcılarınızın bir uygulama dışında veri kopyalamasını engellemek istiyorsanız, bir Uzak Masaüstü Grup İlkesi blok kullanıcılara veri kopyalama yapılandırabilirsiniz.

Belirli bir uygulamanın koleksiyonunuzdaki internet erişimini engellemek istiyorsanız başka bir örnektir. Koleksiyonunuz için görüntüyü oluştururken erişimini engelleyen bir Windows Güvenlik duvarı kural oluşturabilirsiniz.

## <a name="implementation-options"></a>Uygulama Seçenekleri
  Gerektiğinde ayrı ayrı veya dağıtımınızla birlikte kullanılabilir anahtar uygulama seçenekleri şunlardır:

1. RemoteApp koleksiyonunuzun etki alanına katılmış ise herhangi zorlayabilir [Grup İlkesi](https://technet.microsoft.com/library/cc725828.aspx) (açıklanan boşta ve bağlantı kesme zaman aşımı ilkeleri dışında [burada](../azure-subscription-service-limits.md)).
2. Grup (koleksiyonunuzu etki alanına katılmış veya AD'de sağ ayrıcalığa sahip değilsiniz değilse) ilkesi alternatif olarak, yapılandırdığınız [yerel ilkeler](https://technet.microsoft.com/library/cc775702.aspx) şablon görüntüsü.  Bir çakışma olduğunda bu grubun koz yerel ilkeleri ilkeler unutmayın.
3. Bazı işletim sistemi/uygulama ayarları için ilke aracılığıyla yapılandırılabilir değildir, ancak bu kayıt defteri anahtarı kullanarak aracılığıyla olabilir [RegEdit aracı](remoteapp-hybridtrouble.md) şablon görüntünüzü yapılandırılırken.
4. Kullanabileceğiniz [Windows Güvenlik Duvarı](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) uygulamanın çalıştığı makine gelen ve giden ağ erişimi denetlemek. Yalnızca URL'lerin ve bağlantı noktalarının burada tanımlanan engelleme emin olun.
5. Kullanabileceğiniz [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) denetimine hangi uygulamaları ve dosyaları kullanıcıların çalıştırabilirsiniz. Örneğin, deneyimli kullanıcılar, yayımlanmayacak ancak koleksiyonu oluşturmak için kullanılan görüntüde kullanılabilir - AppLocker'ın bu engelleme uygulamaları çalıştırmak nasıl anlayabilir.

## <a name="detailed-information"></a>Ayrıntılı bilgi
* Aşağıdaki RDS ilkeleri büyük olasılıkla en yararlı şunlardır:
  * [Cihaz ve kaynak yeniden yönlendirmesi](https://technet.microsoft.com/library/ee791794.aspx)
  * [Yazıcı yeniden yönlendirme](https://technet.microsoft.com/library/ee791784.aspx)
  * [Profilleri](https://technet.microsoft.com/library/ee791865.aspx).
* Bu yapılandırma Not RemoteApp PowerShell modülü aracılığıyla yeniden yönlendirme (görülen [burada](remoteapp-redirection.md)) güvenlik birincil amacı ise politikasını şablon görüntüsü aracılığıyla istersiniz ilkeyi uygulamak için istemci makinede kullanır Yerel ilke veya Grup İlkesi aracılığıyla.
* [Windows Server 2012 R2 ilkeleri](https://technet.microsoft.com/library/hh831791.aspx).
* [Office 2013 ilkeleri](https://technet.microsoft.com/library/cc178969.aspx) (dahil olmak üzere [Office araç çubuğunu özelleştirme](https://technet.microsoft.com/library/cc179143.aspx)).

