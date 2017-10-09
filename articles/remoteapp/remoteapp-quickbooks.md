---
title: Azure remoteapp'te QuickBooks aaaDeploy | Microsoft Docs
description: "Bilgi nasıl tooshare QuickBooks Azure RemoteApp ile."
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
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>Azure remoteapp'te QuickBooks nasıl dağıttığınız?
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure remoteapp'te bir uygulama olarak bilgi tooshare QuickBooks aşağıdaki hello kullanın.

QuickBooks 2015 kurumsal bir karma veya Bulut koleksiyonunda Azure RemoteApp ile paylaşabilirsiniz. Merhaba şirket dosyası hello Azure RemoteApp sunucularından ayrıdır QuickBooks veritabanı sunucusunu çalıştıran bir VM'de bulunmalıdır. Hiçbir zaman hello şirket dosyası, Azure RemoteApp görüntüsüne depolamak - bunu yapmanız durumunda veri kaybını beklenir. Yalnızca QuickBooks kuruluş QuickBooks veritabanı sunucusuyla standart Windows ağ üzerinden erişilebilir bir dış paylaşımında barındırma hello QuickBooks dosya destekler.   

> [!IMPORTANT]
> Merhaba hello şirket dosyası barındırma QuickBooks veritabanı sunucusu hello içinde ayrı bir VM'de aynı bulunmalıdır hello Azure RemoteApp koleksiyonu olarak VNET.  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a>Adımları toodeploy QuickBooks
1. Bir Azure VM oluşturun ve QuickBooks, QuickBooks veritabanı sunucusu, yükleyin ve bir Azure VM hello şirket dosyayı yerleştirin.  Güvenlik duvarı kurallarını yapılandırma emin tooproperly olun.
2. QuickBooks yüklemek bir [özel görüntü](remoteapp-imageoptions.md) ve oluşturma bir [Azure RemoteApp koleksiyonu](remoteapp-collections.md), Bulut veya başlangıç içinde nerede hello VM barındırma izin ver hello QuickBooks veritabanı sunucusuyla aynı VNET'i tam karma Şirket dosyaları bulunur. 
3. [Yayımlama](remoteapp-publish.md) QuickBooks uygulama toousers
4. Hello Azure RemoteApp barındırılan QuickBooks istemcisi başlatmak, standart Windows toohello VM barındırma hello QuickBooks veritabanı sunucusuna ağ kullanarak gidin ve hello şirket dosyasını açın. 

## <a name="documentation-references"></a>Belge başvuruları
* QuickBooks [desteklenen yapılandırmalar](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* QuickBooks [dağıtım seçenekleri](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

Ignite sunumu kontrol edebilirsiniz [temelleri Microsoft Azure RemoteApp yönetimi ve Yönetim](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -ileri sarma too1:02:45 tooget toohello QuickBooks bölümü.

## <a name="deployment-architecture"></a>Dağıtım mimarisi
![QuickBooks + Azure RemoteApp dağıtım](./media/remoteapp-quickbooks/ra-quickbooks.png)

