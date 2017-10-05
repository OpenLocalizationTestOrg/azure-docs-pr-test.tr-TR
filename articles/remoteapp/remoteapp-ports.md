---
title: "Bağlantı noktaları ve listesi URL'leri güvenilir listeye için Azure RemoteApp dağıtılan müşteri sanal ağındaki | Microsoft Docs"
description: "Hangi bağlantı noktalarının ve URL'leri Azure RemoteApp aracılığıyla iletişimi yapılandırmanız gerekir öğrenin."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c17ff8d5441ca92f7b893edb541a1e9730c2a847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="list-of-ports-and-urls-to-permit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a>Bağlantı noktaları ve URL'leri erişim Azure RemoteApp dağıtılan için müşteri sanal ağ izin vermek için listesi
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Bir sanal ağ (VNET) içinde bir Azure RemoteApp Bulut veya karma koleksiyonu dağıtıyorsanız, aşağıdaki bağlantı noktası bilgilerini gözden geçirin. Sanal ağlar hakkında daha fazla bilgi için okuma [Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md). Sanal ağ kaynaklarına koleksiyonunuzdaki trafiği kısıtlama bir ağ güvenlik grubu (NSG) oluşturduysanız, erişilebilir ve sanal ağda güvenlik ilkeleri aracılığıyla izin verilen aşağıdaki bağlantı noktaları olduğundan emin olun. Ağ güvenlik grupları hakkında daha fazla bilgi için okuma [bir ağ güvenlik grubu nedir? (NSG) ](../virtual-network/virtual-networks-nsg.md).

## <a name="azure-remoteapp-subnet-needs-access-to-these-endpoints-and-urls"></a>Azure RemoteApp alt Bu uç noktaları ve URL'leri erişimi olmalıdır:
* *. servicebus.windows.net
* *. servicebus.net
* https://*.RemoteApp.windowsazure.com  
* https://www.RemoteApp.windowsazure.com 
* https://*RemoteApp.windowsazure.com  
* https://*.Core.Windows.NET  
* Giden: TCP: TCP: 443, 9351, 9352, 10101 10175 
* İsteğe bağlı – UDP: 10201 10275  

## <a name="azure-remoteapp-clients-need-access-to-these-endpoints-and-urls"></a>Azure RemoteApp istemcilerin bu uç noktaları ve URL'leri erişim gerekir:
İstemciler tarafından ı masaüstleri, vb. kişilerin kullanmak Azure RemoteApp koleksiyonunda dağıtılan uygulamalar bağlanmak için cihazları anlamına gelir.

* https://telemetry.RemoteApp.windowsazure.com  
* (isteğe bağlı UDP bağlantı noktaları için bu adresi olan) https://*.remoteapp.windowsazure.com 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.RemoteApp.windowsazure.com 
* https://*.Core.Windows.NET  
* Giden: TCP: 443  
* İsteğe bağlı - UDP: 3391 

