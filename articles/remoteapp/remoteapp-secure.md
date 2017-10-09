---
title: "aaaSecure uygulamalarına ve kaynaklarına Azure remoteapp'te | Microsoft Docs"
description: "Bilgi nasıl uygulamalarına ve kaynaklarına Azure remoteapp'te aşağı toolock"
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
ms.openlocfilehash: 26325826e92855a12a0087f19a3e32cbe1116449
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>Güvenli uygulamalar ve Azure RemoteApp Kaynakları
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp kullanıcılara erişim toocentrally yönetilen Windows uygulamalarını ne kullanıcılarınız ve yapamayacağı denetlemenize olanak sağlayan sağlar.  Merhaba kullanıcı yönetilmeyen bir aygıt (ör. kendi kişisel Macbook) ve, istediğiniz toocontrol hello kullanıcı erişimini bağlanma ya da deneyimi özellikle yararlıdır.

Örneğin, bir uygulama dışında veri kopyalama, kullanıcıların tooprevent istediğiniz ve kullanıcı kimlik doğrulaması için Active Directory'yi kullanarak, veri kopyalama bir Uzak Masaüstü Grup İlkesi tooblock kullanıcıların yapılandırabilirsiniz.

Koleksiyonunuzda tooblock Internet erişimi için belirli bir uygulamanın istiyorsanız başka bir örnektir. Koleksiyonunuz için hello görüntüsü oluşturduğunuzda blokları erişim hello bir Windows Güvenlik duvarı kuralı oluşturabilirsiniz.

## <a name="implementation-options"></a>Uygulama Seçenekleri
  Gerektiğinde ayrı ayrı veya dağıtımınızla birlikte kullanılabilir hello anahtar uygulama seçenekleri şunlardır:

1. RemoteApp koleksiyonunuzun etki alanına katılmış ise herhangi zorlayabilir [Grup İlkesi](https://technet.microsoft.com/library/cc725828.aspx) (açıklanan hello boşta ve bağlantı kesme zaman aşımı ilkelerine hello durumla [burada](../azure-subscription-service-limits.md)).
2. Bir alternatif tooGroup (koleksiyonunuzu etki alanına katılmış veya AD'de hello sağ ayrıcalığa sahip değilsiniz değilse) ilkesi, yapılandırdığınız [yerel ilkeler](https://technet.microsoft.com/library/cc775702.aspx) şablon görüntüsü.  Bir çakışma olduğunda bu grubun koz yerel ilkeleri ilkeler unutmayın.
3. Bazı işletim sistemi/uygulama ayarları ilke aracılığıyla yapılandırılabilir değildir, ancak hello kullanarak kayıt defteri anahtarı olabilir [RegEdit aracı](remoteapp-hybridtrouble.md) şablon görüntünüzü yapılandırılırken.
4. Kullanabileceğiniz [Windows Güvenlik Duvarı](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) toocontrol ağ erişim tooand hello uygulama çalıştığı hello makineden. Yalnızca hello URL'lerin ve bağlantı noktalarının burada tanımlanan engelleme emin olun.
5. Kullanabileceğiniz [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) hangi uygulamaları ve dosyaları kullanıcıların çalıştırabileceği toocontrol. Örneğin, deneyimli kullanıcılar, yayımlanmayacak ancak hello bulunan toorun uygulamalar, kullanılan toocreate hello koleksiyonu nasıl görüntü çıkışı şekil - AppLocker bu engelleyebilirsiniz.

## <a name="detailed-information"></a>Ayrıntılı bilgi
* RDS ilkelere hello büyük olasılıkla toobe en yararlı şunlardır:
  * [Cihaz ve kaynak yeniden yönlendirmesi](https://technet.microsoft.com/library/ee791794.aspx)
  * [Yazıcı yeniden yönlendirme](https://technet.microsoft.com/library/ee791784.aspx)
  * [Profilleri](https://technet.microsoft.com/library/ee791865.aspx).
* Yapılandırma yeniden yönlendirme aracılığıyla RemoteApp PowerShell modülü hello Not (görülen [burada](remoteapp-redirection.md)) güvenlik hello birincil amacı ise tooenforce hello İlkesi aracılığıyla isteyeceksiniz şekilde hello istemci makine tooenforce hello İlkesi'ne Merhaba şablon görüntüsü yerel ilke veya Grup İlkesi aracılığıyla.
* [Windows Server 2012 R2 ilkeleri](https://technet.microsoft.com/library/hh831791.aspx).
* [Office 2013 ilkeleri](https://technet.microsoft.com/library/cc178969.aspx) (dahil olmak üzere [nasıl toocustomize hello Office araç çubuğu](https://technet.microsoft.com/library/cc179143.aspx)).

