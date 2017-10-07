---
title: "aaaHow tooplan sanal ağınız için bir Azure RemoteApp koleksiyonu | Microsoft Docs"
description: "Bilgi nasıl tooplan sanal ağınız için bir Azure RemoteApp koleksiyonu."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: ad9aff0e-f374-49c0-951d-4a7be1c36de0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: d7eeefc3c66815b18f9338e2e428585e6f81a12a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooplan-your-virtual-network-for-azure-remoteapp"></a>Nasıl tooplan Azure RemoteApp için sanal ağınıza
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Bu belgede açıklanan nasıl tooset Azure sanal ağı (VNET) ve Azure RemoteApp için hello alt ağ. Azure sanal ağlar ile bilginiz yoksa, bu, toovirtualize ağ altyapısı toohello Bulut ve toocreate karma çözümleriniz üzerinde Azure ve şirket içi kaynaklarınıza yardımcı olan bir yetenektir. Bunun hakkında daha fazla bilgiyi [buradan](../virtual-network/virtual-networks-overview.md) edinebilirsiniz.

Azure RemoteApp dağıttığınız sanal ağınızda (gelen ve giden) trafiği için toodefine güvenlik ilkeleri istiyorsanız, Azure RemoteApp için ayrı bir alt ağ dağıtımlarınızda hello Azure hello kalan oluşturuluyor öneririz sanal ağ. Nasıl toodefine güvenlik ilkeleri, Azure sanal alt ağ ile ilgili daha fazla bilgi için lütfen okuyun [bir ağ güvenlik grubu (NSG) nedir?](../virtual-network/virtual-networks-nsg.md).

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>Azure sanal ağlar ile Azure RemoteApp koleksiyonları türleri
bir sanal ağ toouse istediğinizde hello aşağıdaki grafik hello iki farklı koleksiyon seçeneklerini gösterin.

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>VNET ile Azure RemoteApp bulut koleksiyonu
 ![Azure RemoteApp - VNET ile bulut koleksiyonu](./media/remoteapp-planvpn/ra-cloudvpn.png)

Bu, Azure'da hello RemoteApp oturumu konakları tooaccess ihtiyacınız tüm hello kaynakları dağıtıldığı bir Azure RemoteApp koleksiyonunu temsil eder. Aynı sanal ağ hello RemoteApp Koleksiyonunuzla olarak veya farklı bir VNET Azure hello olabilirler.

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>VNET ile Azure RemoteApp karma koleksiyonu
![Azure RemoteApp - karma koleksiyon bir VNET ile](./media/remoteapp-planvpn/ra-hybridvpn.png)

Bu, bazı hello RemoteApp oturumu konakları tooaccess ihtiyacınız hello kaynakları içi dağıtılmış olduğu bir Azure RemoteApp koleksiyonunu temsil eder. Merhaba RemoteApp Koleksiyonunuzla siteden siteye VPN veya hızlı rota gibi Azure karma teknolojilerini kullanarak bağlantılı toohello şirket içi ağdır.

## <a name="how-hello-system-works"></a>Merhaba sistem nasıl çalışır?
Merhaba perde arkasında Azure RemoteApp sağlama sırasında seçtiğiniz Azure sanal makinelerle (karşıya yüklenen görüntünüzü) toohello sanal ağ alt dağıtır. Karma koleksiyon için ettiyseniz, biz tooresolve hello hello sanal ağda sağlanan hello DNS sunucusu ile iş akışı sağlama hello girdiğiniz hello etki alanı denetleyicisinin FQDN'sini deneyin.  
Tooan var olan sanal ağ bağlanıyorsanız emin tooexpose hello gerekli bağlantı noktaları, ağ güvenlik grupları, Azure RemoteApp alt yapın. 

Şunu kullanmanızı öneririz bir [Azure RemoteApp için yeterince büyük alt](remoteapp-vnetsizing.md). Azure sanal ağ tarafından desteklenen en büyük hello olan /8 (CIDR alt ağ tanımlarının kullanarak). Alt ağınız sırasında tüm hello Azure RemoteApp VM'ler daha fazla kullanıcı hello uygulamalara erişirken büyütme büyüklükte tooaccommodate olmalıdır. 

Merhaba şey, sanal ağ alt ağı üzerinde tooenable gerekir şunlardır: 

1. Bağlantı noktası aralığı 10101 10175 toocommunicate hello iç Azure RemoteApp hizmetlerden biri ile üzerinde hello alt ağdan giden trafiğe izin verilmelidir.
2. Alt ağ tooconnect tooAzure bağlantı noktası 443 üzerinden depolama alanından giden trafiğe izin
3. Azure üzerinde barındırılan Active Directory varsa, Azure RemoteApp hello sanal ağ alt ağ içindeki herhangi bir VM mümkün tooconnect toothat etki alanı denetleyicisi olduğundan emin olun. Merhaba sanal ağındaki DNS Hello mümkün tooresolve hello bu etki alanı denetleyicisinin FQDN'sini olmalıdır.

## <a name="virtual-network-with-forced-tunneling"></a>Zorlamalı tünel ile sanal ağ
[Zorlanan tünel](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) tüm yeni Azure RemoteApp koleksiyonları için artık desteklenmektedir. Şu anda zorlanan tünel mevcut bir koleksiyonu toosupport hello geçişini desteklemiyoruz.  Merhaba tooAzure RemoteApp bağlama ve zorlanan tünel koleksiyonlarınızı üzerinde etkin yeni bir tek tooget oluşturma VNET kullanarak tüm mevcut koleksiyonlarınızı toodelete gerekir. 

