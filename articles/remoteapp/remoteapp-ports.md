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
# <a name="list-of-ports-and-urls-to-permit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="da799-103">Bağlantı noktaları ve URL'leri erişim Azure RemoteApp dağıtılan için müşteri sanal ağ izin vermek için listesi</span><span class="sxs-lookup"><span data-stu-id="da799-103">List of Ports and URLs to permit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="da799-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="da799-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="da799-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="da799-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="da799-106">Bir sanal ağ (VNET) içinde bir Azure RemoteApp Bulut veya karma koleksiyonu dağıtıyorsanız, aşağıdaki bağlantı noktası bilgilerini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="da799-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review the following port information.</span></span> <span data-ttu-id="da799-107">Sanal ağlar hakkında daha fazla bilgi için okuma [Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="da799-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="da799-108">Sanal ağ kaynaklarına koleksiyonunuzdaki trafiği kısıtlama bir ağ güvenlik grubu (NSG) oluşturduysanız, erişilebilir ve sanal ağda güvenlik ilkeleri aracılığıyla izin verilen aşağıdaki bağlantı noktaları olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="da799-108">If you have created a network security group (NSG) restricting traffic to the virtual network resources in your collection, make sure the following ports are accessible and allowed through the security policies on the virtual network.</span></span> <span data-ttu-id="da799-109">Ağ güvenlik grupları hakkında daha fazla bilgi için okuma [bir ağ güvenlik grubu nedir? (NSG) ](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="da799-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-to-these-endpoints-and-urls"></a><span data-ttu-id="da799-110">Azure RemoteApp alt Bu uç noktaları ve URL'leri erişimi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="da799-110">Azure RemoteApp subnet needs access to these endpoints and URLs:</span></span>
* <span data-ttu-id="da799-111">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="da799-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="da799-112">*. servicebus.net</span><span class="sxs-lookup"><span data-stu-id="da799-112">*.servicebus.net</span></span>
* <span data-ttu-id="da799-113">https://*.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="da799-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="da799-114">https://www.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="da799-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="da799-115">https://*RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="da799-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="da799-116">https://*.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="da799-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="da799-117">Giden: TCP: TCP: 443, 9351, 9352, 10101 10175</span><span class="sxs-lookup"><span data-stu-id="da799-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="da799-118">İsteğe bağlı – UDP: 10201 10275</span><span class="sxs-lookup"><span data-stu-id="da799-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-to-these-endpoints-and-urls"></a><span data-ttu-id="da799-119">Azure RemoteApp istemcilerin bu uç noktaları ve URL'leri erişim gerekir:</span><span class="sxs-lookup"><span data-stu-id="da799-119">Azure RemoteApp clients need access to these endpoints and URLs:</span></span>
<span data-ttu-id="da799-120">İstemciler tarafından ı masaüstleri, vb. kişilerin kullanmak Azure RemoteApp koleksiyonunda dağıtılan uygulamalar bağlanmak için cihazları anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="da799-120">By clients I mean the desktops, devices etc. that people use to connect to the apps deployed in the Azure RemoteApp collection.</span></span>

* <span data-ttu-id="da799-121">https://telemetry.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="da799-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="da799-122">(isteğe bağlı UDP bağlantı noktaları için bu adresi olan) https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="da799-122">https://*.remoteapp.windowsazure.com (the optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="da799-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="da799-123">https://login.windows.net</span></span>  
* <span data-ttu-id="da799-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="da799-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="da799-125">https://www.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="da799-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="da799-126">https://*.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="da799-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="da799-127">Giden: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="da799-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="da799-128">İsteğe bağlı - UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="da799-128">Optional - UDP: 3391</span></span> 

