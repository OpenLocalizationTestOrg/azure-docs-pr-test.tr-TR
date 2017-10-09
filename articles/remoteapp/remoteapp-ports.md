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
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="3d8d5-103">Listesi bağlantı noktaları ve URL'leri toopermit erişim için Azure RemoteApp dağıtılan müşteri sanal ağ</span><span class="sxs-lookup"><span data-stu-id="3d8d5-103">List of Ports and URLs toopermit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3d8d5-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3d8d5-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3d8d5-106">Bir sanal ağ (VNET) içinde bir Azure RemoteApp Bulut veya karma koleksiyonu dağıtıyorsanız, bağlantı noktası bilgilerini aşağıdaki hello gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review hello following port information.</span></span> <span data-ttu-id="3d8d5-107">Sanal ağlar hakkında daha fazla bilgi için okuma [Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3d8d5-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="3d8d5-108">Trafik toohello sanal ağ kaynaklarına koleksiyonunuzdaki kısıtlayarak ağ güvenlik grubu (NSG) oluşturduysanız, erişilebilir ve hello sanal ağda hello güvenlik ilkeleri aracılığıyla izin verilen bağlantı noktaları aşağıdaki hello olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-108">If you have created a network security group (NSG) restricting traffic toohello virtual network resources in your collection, make sure hello following ports are accessible and allowed through hello security policies on hello virtual network.</span></span> <span data-ttu-id="3d8d5-109">Ağ güvenlik grupları hakkında daha fazla bilgi için okuma [bir ağ güvenlik grubu nedir? (NSG) ](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="3d8d5-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a><span data-ttu-id="3d8d5-110">Azure RemoteApp alt ağ erişim toothese uç noktaları ve URL'leri gerekir:</span><span class="sxs-lookup"><span data-stu-id="3d8d5-110">Azure RemoteApp subnet needs access toothese endpoints and URLs:</span></span>
* <span data-ttu-id="3d8d5-111">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="3d8d5-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="3d8d5-112">*. servicebus.net</span><span class="sxs-lookup"><span data-stu-id="3d8d5-112">*.servicebus.net</span></span>
* <span data-ttu-id="3d8d5-113">https://*.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="3d8d5-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="3d8d5-114">https://www.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="3d8d5-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="3d8d5-115">https://*RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="3d8d5-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="3d8d5-116">https://*.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="3d8d5-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="3d8d5-117">Giden: TCP: TCP: 443, 9351, 9352, 10101 10175</span><span class="sxs-lookup"><span data-stu-id="3d8d5-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="3d8d5-118">İsteğe bağlı – UDP: 10201 10275</span><span class="sxs-lookup"><span data-stu-id="3d8d5-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a><span data-ttu-id="3d8d5-119">Azure RemoteApp istemcileri toothese uç noktaları ve URL'leri erişim:</span><span class="sxs-lookup"><span data-stu-id="3d8d5-119">Azure RemoteApp clients need access toothese endpoints and URLs:</span></span>
<span data-ttu-id="3d8d5-120">Hello kullan tooconnect toohello uygulamaları Azure RemoteApp koleksiyonu dağıtılan ı masaüstleri, cihazları vb. kişilerin hello anlamına istemciler tarafından.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-120">By clients I mean hello desktops, devices etc. that people use tooconnect toohello apps deployed in hello Azure RemoteApp collection.</span></span>

* <span data-ttu-id="3d8d5-121">https://telemetry.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="3d8d5-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="3d8d5-122">https://*.RemoteApp.windowsazure.com (Merhaba isteğe bağlı UDP bağlantı noktalarının bu adres için)</span><span class="sxs-lookup"><span data-stu-id="3d8d5-122">https://*.remoteapp.windowsazure.com (hello optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="3d8d5-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="3d8d5-123">https://login.windows.net</span></span>  
* <span data-ttu-id="3d8d5-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="3d8d5-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="3d8d5-125">https://www.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="3d8d5-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="3d8d5-126">https://*.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="3d8d5-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="3d8d5-127">Giden: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="3d8d5-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="3d8d5-128">İsteğe bağlı - UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="3d8d5-128">Optional - UDP: 3391</span></span> 

