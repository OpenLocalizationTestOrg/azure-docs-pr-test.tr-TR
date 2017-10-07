---
title: "azure'da aaaCreate SharePoint server grupları | Microsoft Docs"
description: "Hızlı bir şekilde Azure'da hello Azure portal Market kullanarak yeni bir SharePoint 2013 veya SharePoint 2016 grubu oluşturun."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a>Azure portal Market Hello kullanarak SharePoint sunucu grupları oluşturma

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a>SharePoint 2013 grupları
İle Merhaba Microsoft Azure portal Market, önceden yapılandırılmış SharePoint Server 2013 grupları kolayca oluşturabilirsiniz. Bu, çok zaman bir geliştirme ve test ortamı için bir temel veya yüksek kullanılabilirlik SharePoint grubu gerektiğinde veya, SharePoint Server 2013, kuruluşunuz için işbirliği çözüm olarak değerlendirmek kaydedebilirsiniz.

> [!NOTE]
> Merhaba **SharePoint sunucu grubu** hello Azure portal hello Azure Market öğesi kaldırıldı. Merhaba ile değiştirilen **SharePoint 2013 olmayan HA grubu** ve **SharePoint 2013 HA grubu** öğeleri.
>
>

Bu yapılandırmada üç sanal makinelerin Hello temel SharePoint grubu oluşur.

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

Bu grubu yapılandırmasını SharePoint uygulama geliştirme için Basitleştirilmiş kurulumu veya ilk kez değerlendirmenize SharePoint 2013 için kullanabilirsiniz.

toocreate hello temel (üç sunuculu) SharePoint grubu:

1. Tıklatın [burada](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).
2. Tıklatın **dağıtmak**.
3. Merhaba üzerinde **SharePoint 2013 olmayan HA grubu** bölmesinde tıklatın **oluşturma**.
4. Merhaba hello adımlarından ayarlarını belirtin **oluşturma SharePoint 2013 olmayan HA grubu** bölmesi ve ardından **oluşturma**.

Bu yapılandırmada dokuz sanal makinelerin Hello yüksek kullanılabilirlik SharePoint grubu oluşur.

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

Bir SharePoint grubu için bu grubu yapılandırma tootest daha yüksek istemci yüklerini, hello dış SharePoint sitesi yüksek kullanılabilirliğini ve SQL Server AlwaysOn Kullanılabilirlik gruplarını kullanabilirsiniz. Bu yapılandırma, bir yüksek kullanılabilirlik ortamında SharePoint uygulama geliştirme için de kullanabilirsiniz.

toocreate hello yüksek kullanılabilirlik (dokuz sunuculu) SharePoint grubu:

1. Tıklatın [burada](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).
2. Tıklatın **dağıtmak**.
3. Merhaba üzerinde **SharePoint 2013 HA grubu** bölmesinde tıklatın **oluşturma**.
4. Merhaba hello yedi adımlarından ayarlarını belirtin **oluşturma SharePoint 2013 HA grubu** bölmesi ve ardından **oluşturma**.

> [!NOTE]
> Merhaba oluşturulamıyor **SharePoint 2013 olmayan HA grubu** veya **SharePoint 2013 HA grubu** Azure ücretsiz deneme sürümü ile.
>
>

Hello Azure portal bu grupları her ikisinin bir Internet'e yönelik web varlığı ile yalnızca bulut sanal ağ oluşturur. Siteden siteye VPN veya ExpressRoute bağlantı geri tooyour kuruluş ağ yok.

> [!NOTE]
> Ne zaman hello temel oluşturun veya yüksek kullanılabilirlik SharePoint grupları hello Azure portal kullanarak, varolan bir kaynak grubu belirtemezsiniz. Bu sınırlamaya geçici toowork Azure PowerShell ile bu grupları oluşturun. Daha fazla bilgi için bkz: [oluşturma SharePoint 2013 geliştirme ve test grupları Azure PowerShell ile](https://technet.microsoft.com/library/mt743093.aspx#powershell).
>
>

## <a name="sharepoint-2016-farms"></a>SharePoint 2016 grupları
Bkz: [bu makalede](https://technet.microsoft.com/library/mt723354.aspx) tek sunuculu SharePoint Server 2016 aşağıdaki hello yönergeleri toobuild Merhaba grubu.

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a>Merhaba SharePoint grupları yönetme
Uzak Masaüstü bağlantıları üzerinden bu grupları hello sunucuları yönetebilirsiniz. Daha fazla bilgi için bkz: [toohello sanal makinede oturum](quick-create-portal.md#connect-to-virtual-machine).

Merhaba Merkezi Yönetim SharePoint sitesinden Sitelerim, SharePoint uygulamaları ve diğer işlevleri yapılandırabilirsiniz. Daha fazla bilgi için bkz: [SharePoint Yapılandırma](http://technet.microsoft.com/library/ee836142.aspx).

## <a name="next-steps"></a>Sonraki adımlar
* Ek Bul [SharePoint yapılandırmaları](https://technet.microsoft.com/library/dn635309.aspx) Azure altyapı Hizmetleri'nde.
