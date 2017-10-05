---
title: "Azure remoteapp'te QuickBooks dağıtma | Microsoft Docs"
description: "QuickBooks Azure RemoteApp ile paylaştığınız öğrenin."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: bbfac45220f6ef36c9951daae0ced1974e8ddabb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>Azure remoteapp'te QuickBooks nasıl dağıttığınız?
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Azure remoteapp'te bir uygulama olarak QuickBooks paylaşmak için aşağıdaki bilgileri kullanın.

QuickBooks 2015 kurumsal bir karma veya Bulut koleksiyonunda Azure RemoteApp ile paylaşabilirsiniz. Şirket dosyası Azure RemoteApp sunucularından ayrıdır QuickBooks veritabanı sunucusunu çalıştıran bir VM'de bulunmalıdır. Hiçbir zaman şirket dosyası, Azure RemoteApp görüntüsüne depolamak - bunu yapmanız durumunda veri kaybını beklenir. Yalnızca QuickBooks kuruluş QuickBooks veritabanı sunucusuyla standart Windows ağ üzerinden erişilebilen bir harici paylaşımda QuickBooks dosyasını barındıran destekler.   

> [!IMPORTANT]
> Şirket dosyası barındırma QuickBooks veritabanı sunucusu, Azure RemoteApp koleksiyonu olarak aynı sanal ağ içinde ayrı bir VM üzerinde bulunmalıdır.  
> 
> 

## <a name="steps-to-deploy-quickbooks"></a>QuickBooks dağıtma adımları
1. Bir Azure VM oluşturun ve QuickBooks, QuickBooks veritabanı sunucusu, yükleyin ve bir Azure VM şirket dosyayı yerleştirin.  Güvenlik duvarı kuralları doğru şekilde yapılandırdığınızdan emin olun.
2. QuickBooks yüklemek bir [özel görüntü](remoteapp-imageoptions.md) ve oluşturma bir [Azure RemoteApp koleksiyonu](remoteapp-collections.md), Bulut veya karma burada QuickBooks barındırma VM veritabanı sunucusu şirket dosyaları ile tam aynı sanal ağ içinden yer alıyor. 
3. [Yayımlama](remoteapp-publish.md) kullanıcılara QuickBooks uygulama
4. Azure RemoteApp barındırılan QuickBooks istemcisi başlatmak, standart Windows ağ QuickBooks veritabanı sunucusunu barındıran VM kullanarak gidin ve şirket dosyasını açın. 

## <a name="documentation-references"></a>Belge başvuruları
* QuickBooks [desteklenen yapılandırmalar](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* QuickBooks [dağıtım seçenekleri](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

Ignite sunumu kontrol edebilirsiniz [temelleri Microsoft Azure RemoteApp yönetimi ve Yönetim](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -ileri sarma QuickBooks bölümünü almak için 1:02:45.

## <a name="deployment-architecture"></a>Dağıtım mimarisi
![QuickBooks + Azure RemoteApp dağıtım](./media/remoteapp-quickbooks/ra-quickbooks.png)

