---
title: "aaaUsing App-V uygulamalarını Azure RemoteApp ile | Microsoft Docs"
description: "Bilgi nasıl toouse App-V uygulamalarını Azure RemoteApp içinde."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a>Azure Remoteapp'te App-V uygulamaları kullanma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

App-V uygulamalarını etki alanına katılma gerektiren bir Azure RemoteApp karma koleksiyonu içinde kullanabilirsiniz.

Başlamadan önce hello en son güncelleştirmeleri içeren emin tooinstall hello App-V 5.1 istemci olun. Toocreate ihtiyacınız olacak bir [özel görüntü](remoteapp-create-custom-image.md) hello App-V istemcisi içerir.  

Kolay toouse olan mevcut App-V altyapınızı Azure RemoteApp ile. Karma koleksiyon erişim tooyour etki alanı denetleyicisine sahip bir Azure sanal dağıtılan ve hello VM'ler etki alanına katılmış olduğundan, var olan App-v altyapınıza ve dağıtım yöntemleri tooeasyily konak App-V uygulamanızda Azure RemoteApp yararlanabilirsiniz. App-V dağıtım şu anda hello türüne göre farkında olmanız gereken bazı noktalar şunlardır:

| Yapılandırma seçenekleri |  | Pozitif | Negatif |
| --- | --- | --- | --- |
| Teslim yöntemi |Akış (isteğe bağlı) |Uygulama her zaman hello son ve güncel değil |İlk zaman gecikmesini |
| Takılı |Hızlı; Uygulama hello VM üzerinde zaten |Oluşan şişirmeyi - (127 GB sınırını) görüntüsü yer alır | |
| Uygulama konumu depolama |Paylaşılan içerik |Uygulama Azure RemoteApp örneği bellekte çalıştırır |Bellek ve iyi bağlantı toostreaming (dosya) sunucusu hello uygulama bulunduğu eats |
| Disk (önbelleğe alınmış) |Hızlı yürütme. Uygulama içerik kaynağı kullanılabilirliğine bağlı değil |Oluşan şişirmeyi - (127 GB sınırını) görüntüsü yer alır | |
| Hedefleme |Kullanıcı |Tam tek başına App-V altyapısı gerektirir | |
| Genel (makine) |Önceden yayımlama veya yayımlama kullanarak hedef sunucu |Tooupdate hello uygulama (büyük) istiyorsanız tooupdate Azure görüntünüzü gerekir. Görüntü alan kaplar. | |

 Özel görüntünüzü ve karma koleksiyonunuzda oluşturduktan sonra uygulamanızı yayımlamak, kullanıcılar atayın ve herhangi bir yere tooany aygıt teslim Azure Remoteapp'te barındırılan, var olan App-V uygulamalarınızın keyfini çıkarın.

