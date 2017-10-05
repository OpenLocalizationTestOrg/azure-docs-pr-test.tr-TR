---
title: "Azure RemoteApp ile App-V uygulamaları kullanma | Microsoft Docs"
description: "App-V uygulamaları Azure Remoteapp'te kullanmayı öğrenin."
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
ms.openlocfilehash: e55bb8db83c04025c46b383a9ebbef4399178116
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a>Azure Remoteapp'te App-V uygulamaları kullanma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

App-V uygulamalarını etki alanına katılma gerektiren bir Azure RemoteApp karma koleksiyonu içinde kullanabilirsiniz.

Başlamadan önce App-V 5.1 istemci ile en son güncelleştirmeleri yüklediğinizden emin olun. Oluşturmanız gereken bir [özel görüntü](remoteapp-create-custom-image.md) App-V istemcisi içerir.  

Var olan App-V altyapınızı Azure RemoteApp ile kullanmak kolaydır. Karma koleksiyon etki alanı denetleyicinizi erişimi olan bir Azure sanal içine dağıtılan ve sanal makinelerin etki alanına katılmış olduğundan, var olan App-v altyapınıza ve dağıtım yöntemlerinizi easyily konak App-V uygulamaya Azure remoteapp'te yararlanabilirsiniz. Şu anda App-V dağıtım türüne göre farkında olmanız gereken bazı noktalar şunlardır:

| Yapılandırma seçenekleri |  | Pozitif | Negatif |
| --- | --- | --- | --- |
| Teslim yöntemi |Akış (isteğe bağlı) |Uygulama her zaman en son ve yeni değil |İlk zaman gecikmesini |
| Takılı |Hızlı; Uygulama, VM üzerinde zaten var |Oluşan şişirmeyi - (127 GB sınırını) görüntüsü yer alır | |
| Uygulama konumu depolama |Paylaşılan içerik |Uygulama Azure RemoteApp örneği bellekte çalıştırır |Uygulama bulunduğu bellek ve (dosya) sunucusu akış iyi bağlantı eats |
| Disk (önbelleğe alınmış) |Hızlı yürütme. Uygulama içerik kaynağı kullanılabilirliğine bağlı değil |Oluşan şişirmeyi - (127 GB sınırını) görüntüsü yer alır | |
| Hedefleme |Kullanıcı |Tam tek başına App-V altyapısı gerektirir | |
| Genel (makine) |Önceden yayımlama veya yayımlama kullanarak hedef sunucu |(Büyük) uygulamasını güncelleştirmek istiyorsanız, Azure görüntünüzü güncelleştirmeniz gerekir. Görüntü alan kaplar. | |

 Özel görüntü ve karma koleksiyonunuzda oluşturduktan sonra uygulamanızı yayımlamak, kullanıcılar atayın ve herhangi bir yerden herhangi cihaza teslim Azure remoteapp'te barındırılan, var olan App-V uygulamalarınızın keyfini çıkarın.

