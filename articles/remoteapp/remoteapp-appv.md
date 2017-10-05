---
title: "Azure RemoteApp ile App-V uygulamaları kullanma | Microsoft Docs"
description: "App-V uygulamaları Azure Remoteapp'te kullanmayı öğrenin."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e55bb8db83c04025c46b383a9ebbef4399178116
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="1c8fa-103">Azure Remoteapp'te App-V uygulamaları kullanma</span><span class="sxs-lookup"><span data-stu-id="1c8fa-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1c8fa-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="1c8fa-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1c8fa-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="1c8fa-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1c8fa-106">App-V uygulamalarını etki alanına katılma gerektiren bir Azure RemoteApp karma koleksiyonu içinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c8fa-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="1c8fa-107">Başlamadan önce App-V 5.1 istemci ile en son güncelleştirmeleri yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="1c8fa-107">Before you get started, make sure to install the App-V 5.1 client with the latest updates.</span></span> <span data-ttu-id="1c8fa-108">Oluşturmanız gereken bir [özel görüntü](remoteapp-create-custom-image.md) App-V istemcisi içerir.</span><span class="sxs-lookup"><span data-stu-id="1c8fa-108">You will need to create a [custom image](remoteapp-create-custom-image.md) that includes the App-V client.</span></span>  

<span data-ttu-id="1c8fa-109">Var olan App-V altyapınızı Azure RemoteApp ile kullanmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="1c8fa-109">It’s easy to use your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="1c8fa-110">Karma koleksiyon etki alanı denetleyicinizi erişimi olan bir Azure sanal içine dağıtılan ve sanal makinelerin etki alanına katılmış olduğundan, var olan App-v altyapınıza ve dağıtım yöntemlerinizi easyily konak App-V uygulamaya Azure remoteapp'te yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c8fa-110">Since a hybrid collection is deployed into an Azure VNET that has access to your domain controller and the VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods to easyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="1c8fa-111">Şu anda App-V dağıtım türüne göre farkında olmanız gereken bazı noktalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1c8fa-111">Here are some considerations that you should be aware of based on the type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="1c8fa-112">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="1c8fa-112">Configuration options</span></span> |  | <span data-ttu-id="1c8fa-113">Pozitif</span><span class="sxs-lookup"><span data-stu-id="1c8fa-113">Positive</span></span> | <span data-ttu-id="1c8fa-114">Negatif</span><span class="sxs-lookup"><span data-stu-id="1c8fa-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1c8fa-115">Teslim yöntemi</span><span class="sxs-lookup"><span data-stu-id="1c8fa-115">Delivery method</span></span> |<span data-ttu-id="1c8fa-116">Akış (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="1c8fa-116">Streaming (on-demand)</span></span> |<span data-ttu-id="1c8fa-117">Uygulama her zaman en son ve yeni değil</span><span class="sxs-lookup"><span data-stu-id="1c8fa-117">App is always the latest and fresh</span></span> |<span data-ttu-id="1c8fa-118">İlk zaman gecikmesini</span><span class="sxs-lookup"><span data-stu-id="1c8fa-118">First time latency</span></span> |
| <span data-ttu-id="1c8fa-119">Takılı</span><span class="sxs-lookup"><span data-stu-id="1c8fa-119">Mounted</span></span> |<span data-ttu-id="1c8fa-120">Hızlı; Uygulama, VM üzerinde zaten var</span><span class="sxs-lookup"><span data-stu-id="1c8fa-120">Fastest; app is already present on the VM</span></span> |<span data-ttu-id="1c8fa-121">Oluşan şişirmeyi - (127 GB sınırını) görüntüsü yer alır</span><span class="sxs-lookup"><span data-stu-id="1c8fa-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="1c8fa-122">Uygulama konumu depolama</span><span class="sxs-lookup"><span data-stu-id="1c8fa-122">App location storage</span></span> |<span data-ttu-id="1c8fa-123">Paylaşılan içerik</span><span class="sxs-lookup"><span data-stu-id="1c8fa-123">Shared content</span></span> |<span data-ttu-id="1c8fa-124">Uygulama Azure RemoteApp örneği bellekte çalıştırır</span><span class="sxs-lookup"><span data-stu-id="1c8fa-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="1c8fa-125">Uygulama bulunduğu bellek ve (dosya) sunucusu akış iyi bağlantı eats</span><span class="sxs-lookup"><span data-stu-id="1c8fa-125">Eats memory and good connection to streaming (file) server where the app resides</span></span> |
| <span data-ttu-id="1c8fa-126">Disk (önbelleğe alınmış)</span><span class="sxs-lookup"><span data-stu-id="1c8fa-126">Disk (Cached)</span></span> |<span data-ttu-id="1c8fa-127">Hızlı yürütme.</span><span class="sxs-lookup"><span data-stu-id="1c8fa-127">Fast execution.</span></span> <span data-ttu-id="1c8fa-128">Uygulama içerik kaynağı kullanılabilirliğine bağlı değil</span><span class="sxs-lookup"><span data-stu-id="1c8fa-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="1c8fa-129">Oluşan şişirmeyi - (127 GB sınırını) görüntüsü yer alır</span><span class="sxs-lookup"><span data-stu-id="1c8fa-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="1c8fa-130">Hedefleme</span><span class="sxs-lookup"><span data-stu-id="1c8fa-130">Targeting</span></span> |<span data-ttu-id="1c8fa-131">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="1c8fa-131">User</span></span> |<span data-ttu-id="1c8fa-132">Tam tek başına App-V altyapısı gerektirir</span><span class="sxs-lookup"><span data-stu-id="1c8fa-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="1c8fa-133">Genel (makine)</span><span class="sxs-lookup"><span data-stu-id="1c8fa-133">Global (machine)</span></span> |<span data-ttu-id="1c8fa-134">Önceden yayımlama veya yayımlama kullanarak hedef sunucu</span><span class="sxs-lookup"><span data-stu-id="1c8fa-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="1c8fa-135">(Büyük) uygulamasını güncelleştirmek istiyorsanız, Azure görüntünüzü güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c8fa-135">Need to update your Azure image if you want to update the app (huge).</span></span> <span data-ttu-id="1c8fa-136">Görüntü alan kaplar.</span><span class="sxs-lookup"><span data-stu-id="1c8fa-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="1c8fa-137">Özel görüntü ve karma koleksiyonunuzda oluşturduktan sonra uygulamanızı yayımlamak, kullanıcılar atayın ve herhangi bir yerden herhangi cihaza teslim Azure remoteapp'te barındırılan, var olan App-V uygulamalarınızın keyfini çıkarın.</span><span class="sxs-lookup"><span data-stu-id="1c8fa-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered to any device anywhere.</span></span>

