---
title: "Azure RemoteApp dağıtılan için bağlantı noktalarını ve URL'leri toowhitelist müşteri sanal ağındaki aaaList | Microsoft Docs"
description: "Hangi bağlantı noktalarının ve Azure RemoteApp aracılığıyla iletişimi tooconfigure gerekir URL'leri öğrenin."
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
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a>Listesi bağlantı noktaları ve URL'leri toopermit erişim için Azure RemoteApp dağıtılan müşteri sanal ağ
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Bir sanal ağ (VNET) içinde bir Azure RemoteApp Bulut veya karma koleksiyonu dağıtıyorsanız, bağlantı noktası bilgilerini aşağıdaki hello gözden geçirin. Sanal ağlar hakkında daha fazla bilgi için okuma [Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md). Trafik toohello sanal ağ kaynaklarına koleksiyonunuzdaki kısıtlayarak ağ güvenlik grubu (NSG) oluşturduysanız, erişilebilir ve hello sanal ağda hello güvenlik ilkeleri aracılığıyla izin verilen bağlantı noktaları aşağıdaki hello olduğundan emin olun. Ağ güvenlik grupları hakkında daha fazla bilgi için okuma [bir ağ güvenlik grubu nedir? (NSG) ](../virtual-network/virtual-networks-nsg.md).

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a>Azure RemoteApp alt ağ erişim toothese uç noktaları ve URL'leri gerekir:
* *. servicebus.windows.net
* *. servicebus.net
* https://*.RemoteApp.windowsazure.com  
* https://www.RemoteApp.windowsazure.com 
* https://*RemoteApp.windowsazure.com  
* https://*.Core.Windows.NET  
* Giden: TCP: TCP: 443, 9351, 9352, 10101 10175 
* İsteğe bağlı – UDP: 10201 10275  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a>Azure RemoteApp istemcileri toothese uç noktaları ve URL'leri erişim:
Hello kullan tooconnect toohello uygulamaları Azure RemoteApp koleksiyonu dağıtılan ı masaüstleri, cihazları vb. kişilerin hello anlamına istemciler tarafından.

* https://telemetry.RemoteApp.windowsazure.com  
* https://*.RemoteApp.windowsazure.com (Merhaba isteğe bağlı UDP bağlantı noktalarının bu adres için) 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.RemoteApp.windowsazure.com 
* https://*.Core.Windows.NET  
* Giden: TCP: 443  
* İsteğe bağlı - UDP: 3391 

