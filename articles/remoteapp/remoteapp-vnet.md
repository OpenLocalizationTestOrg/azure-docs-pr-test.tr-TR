---
title: "Azure RemoteApp ile kullanmak için Azure VNET doğrulama | Microsoft Docs"
description: "Azure sanal Azure RemoteApp ile kullanıma hazır olduğundan emin olun öğrenin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 05c8a0ff04293947cec391b6467cc4adddb6a7b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="validate-the-azure-vnet-to-use-with-azure-remoteapp"></a>Azure RemoteApp ile kullanmak için Azure VNET doğrula
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Azure RemoteApp ile bir Azure sanal kullanmadan önce sanal ağ doğrulamak isteyebilirsiniz. Bu bağlantı sorunları önlemeye yardımcı olur.

Azure sanal doğrulamak için aşağıdakileri yapın:

1. Azure RemoteApp ile kullanmak istediğiniz Azure sanal alt ağ içindeki bir Azure sanal makine oluşturun.
2. Bağlan'kullanarak bu VM'ye **Bağlan** Yönetim Portalı'nda seçeneği.
3. Sanal makineyi Azure RemoteApp ile kullanmak istediğiniz aynı etki alanına katılın. Şirket içi ağınıza bağlanan bir karma koleksiyon oluşturuyorsanız, sanal makinenin yerel etki alanınıza ekleyin.

Bu başarılı olursa, Azure VNET RemoteApp ile kullanmak hazırdır.

Uçtan uca karma koleksiyonu iş akışı hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

* [Azure RemoteApp için sanal ağınızı planlama hakkında](remoteapp-planvnet.md)
* [Karma koleksiyon oluşturma](remoteapp-create-hybrid-deployment.md)
* [Azure sanal ağınıza (desteğiyle ExpressRoute) Azure RemoteApp koleksiyonu dağıtma](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

