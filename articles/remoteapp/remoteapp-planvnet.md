---
title: "Sanal ağınız bir Azure RemoteApp koleksiyonu için plan yapma | Microsoft Docs"
description: "Sanal ağınız için bir Azure RemoteApp koleksiyonu planlama hakkında bilgi edinin."
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
ms.openlocfilehash: 1eb8115b13fb18074b4c4726b69e3d9faf387c32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-plan-your-virtual-network-for-azure-remoteapp"></a>Azure RemoteApp için sanal ağınızı planlama hakkında
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Bu belge, Azure sanal ağı (VNET) ve alt ağ için Azure RemoteApp ayarlama açıklar. Azure sanal ağlar ile bilginiz yoksa, bu, ağ altyapınızı buluta sanallaştırmanızı ve Azure ve şirket içi kaynaklarınıza karma çözümler oluşturmak için yardımcı olan bir yetenektir. Bunun hakkında daha fazla bilgiyi [buradan](../virtual-network/virtual-networks-overview.md) edinebilirsiniz.

Azure RemoteApp dağıttığınız sanal ağınızda trafiği (gelen ve giden) için güvenlik ilkelerini tanımlamak istiyorsanız, Azure sanal ağı dağıtımlarınızda geri kalanından Azure RemoteApp için ayrı bir alt ağ oluşturmak önerilir. Güvenlik ilkeleri, Azure sanal ağ alt ağı üzerinde tanımlama hakkında daha fazla bilgi için lütfen okuyun [bir ağ güvenlik grubu (NSG) nedir?](../virtual-network/virtual-networks-nsg.md).

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>Azure sanal ağlar ile Azure RemoteApp koleksiyonları türleri
Bir sanal ağ kullanmak istediğinizde aşağıdaki grafik iki farklı koleksiyon seçeneklerini gösterin.

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>VNET ile Azure RemoteApp bulut koleksiyonu
 ![Azure RemoteApp - VNET ile bulut koleksiyonu](./media/remoteapp-planvpn/ra-cloudvpn.png)

Bu, Azure RemoteApp oturumu konakları erişmesi gereken tüm kaynakların dağıtıldığı bir Azure RemoteApp koleksiyonunu temsil eder. Bunlar, aynı sanal ağ RemoteApp Koleksiyonunuzla olarak ya da farklı bir VNET Azure içinde olabilir.

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>VNET ile Azure RemoteApp karma koleksiyonu
![Azure RemoteApp - karma koleksiyon bir VNET ile](./media/remoteapp-planvpn/ra-hybridvpn.png)

Bu, bazı RemoteApp oturumu konakları erişmesi gereken kaynaklara içi dağıtılmış olduğu bir Azure RemoteApp koleksiyonunu temsil eder. RemoteApp Koleksiyonunuzla siteden siteye VPN veya hızlı rota gibi Azure karma teknolojilerini kullanarak şirket ağına bağlanır.

## <a name="how-the-system-works"></a>Sistem nasıl çalışır?
Perde arkasında Azure RemoteApp sağlama sırasında seçtiğiniz sanal ağ alt ağına Azure sanal makinelerle (karşıya yüklenen görüntünüzü) dağıtır. Karma koleksiyon için ettiyseniz, sanal ağ içinde sağlanan DNS sunucusuyla sağlama iş akışında girdiğiniz etki alanı denetleyicisinin FQDN'sini çözümleyebilmesi deneyin.  
Mevcut bir sanal ağa bağlanıyorsanız, Azure RemoteApp alt ağındaki ağ güvenlik gruplarındaki gerekli bağlantı noktalarını kullanıma emin olun. 

Şunu kullanmanızı öneririz bir [Azure RemoteApp için yeterince büyük alt](remoteapp-vnetsizing.md). Azure sanal ağ tarafından desteklenen en büyük 8 uzunluğudur (CIDR alt ağ tanımlarının kullanarak). Alt ağınız daha fazla kullanıcı uygulamalara erişirken tüm Azure RemoteApp VM'ler büyütme sırasında uyabilecek kadar büyük olmalıdır. 

Aşağıda, sanal ağ alt ağı üzerinde etkinleştirmek için gerekir gerekenler şunlardır: 

1. Giden trafik alt ağdan, iç Azure RemoteApp hizmetlerden biri ile iletişim kurmak için bağlantı noktası aralığı 10101 10175 izin verilmelidir.
2. Giden trafik alt ağdan Azure Storage bağlantı noktası 443 üzerinden bağlanmasına izin
3. Azure üzerinde barındırılan Active Directory varsa, Azure RemoteApp için sanal ağ alt ağ içindeki herhangi bir VM o etki alanı denetleyicisine bağlanmak mümkün olduğundan emin olun. Sanal ağın DNS bu etki alanı denetleyicisinin FQDN'sini çözümleyebilmesi gerekir.

## <a name="virtual-network-with-forced-tunneling"></a>Zorlamalı tünel ile sanal ağ
[Zorlanan tünel](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) tüm yeni Azure RemoteApp koleksiyonları için artık desteklenmektedir. Şu anda zorlamalı tünel desteklemek için var olan bir koleksiyon geçiş desteklemiyoruz.  Azure RemoteApp bağlama VNET kullanarak, tüm mevcut koleksiyonları silmek ve zorunlu için yeni bir tane oluşturun gerekecek koleksiyonlarınızı üzerinde etkin tünel. 

