---
title: "aaaUsing App-V uygulamalarını Azure RemoteApp ile | Microsoft Docs"
description: "Bilgi nasıl toouse App-V uygulamalarını Azure RemoteApp içinde."
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
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="8bc87-103">Azure Remoteapp'te App-V uygulamaları kullanma</span><span class="sxs-lookup"><span data-stu-id="8bc87-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8bc87-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="8bc87-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8bc87-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="8bc87-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8bc87-106">App-V uygulamalarını etki alanına katılma gerektiren bir Azure RemoteApp karma koleksiyonu içinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc87-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="8bc87-107">Başlamadan önce hello en son güncelleştirmeleri içeren emin tooinstall hello App-V 5.1 istemci olun.</span><span class="sxs-lookup"><span data-stu-id="8bc87-107">Before you get started, make sure tooinstall hello App-V 5.1 client with hello latest updates.</span></span> <span data-ttu-id="8bc87-108">Toocreate ihtiyacınız olacak bir [özel görüntü](remoteapp-create-custom-image.md) hello App-V istemcisi içerir.</span><span class="sxs-lookup"><span data-stu-id="8bc87-108">You will need toocreate a [custom image](remoteapp-create-custom-image.md) that includes hello App-V client.</span></span>  

<span data-ttu-id="8bc87-109">Kolay toouse olan mevcut App-V altyapınızı Azure RemoteApp ile.</span><span class="sxs-lookup"><span data-stu-id="8bc87-109">It’s easy toouse your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="8bc87-110">Karma koleksiyon erişim tooyour etki alanı denetleyicisine sahip bir Azure sanal dağıtılan ve hello VM'ler etki alanına katılmış olduğundan, var olan App-v altyapınıza ve dağıtım yöntemleri tooeasyily konak App-V uygulamanızda Azure RemoteApp yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc87-110">Since a hybrid collection is deployed into an Azure VNET that has access tooyour domain controller and hello VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods tooeasyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="8bc87-111">App-V dağıtım şu anda hello türüne göre farkında olmanız gereken bazı noktalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8bc87-111">Here are some considerations that you should be aware of based on hello type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="8bc87-112">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="8bc87-112">Configuration options</span></span> |  | <span data-ttu-id="8bc87-113">Pozitif</span><span class="sxs-lookup"><span data-stu-id="8bc87-113">Positive</span></span> | <span data-ttu-id="8bc87-114">Negatif</span><span class="sxs-lookup"><span data-stu-id="8bc87-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8bc87-115">Teslim yöntemi</span><span class="sxs-lookup"><span data-stu-id="8bc87-115">Delivery method</span></span> |<span data-ttu-id="8bc87-116">Akış (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="8bc87-116">Streaming (on-demand)</span></span> |<span data-ttu-id="8bc87-117">Uygulama her zaman hello son ve güncel değil</span><span class="sxs-lookup"><span data-stu-id="8bc87-117">App is always hello latest and fresh</span></span> |<span data-ttu-id="8bc87-118">İlk zaman gecikmesini</span><span class="sxs-lookup"><span data-stu-id="8bc87-118">First time latency</span></span> |
| <span data-ttu-id="8bc87-119">Takılı</span><span class="sxs-lookup"><span data-stu-id="8bc87-119">Mounted</span></span> |<span data-ttu-id="8bc87-120">Hızlı; Uygulama hello VM üzerinde zaten</span><span class="sxs-lookup"><span data-stu-id="8bc87-120">Fastest; app is already present on hello VM</span></span> |<span data-ttu-id="8bc87-121">Oluşan şişirmeyi - (127 GB sınırını) görüntüsü yer alır</span><span class="sxs-lookup"><span data-stu-id="8bc87-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="8bc87-122">Uygulama konumu depolama</span><span class="sxs-lookup"><span data-stu-id="8bc87-122">App location storage</span></span> |<span data-ttu-id="8bc87-123">Paylaşılan içerik</span><span class="sxs-lookup"><span data-stu-id="8bc87-123">Shared content</span></span> |<span data-ttu-id="8bc87-124">Uygulama Azure RemoteApp örneği bellekte çalıştırır</span><span class="sxs-lookup"><span data-stu-id="8bc87-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="8bc87-125">Bellek ve iyi bağlantı toostreaming (dosya) sunucusu hello uygulama bulunduğu eats</span><span class="sxs-lookup"><span data-stu-id="8bc87-125">Eats memory and good connection toostreaming (file) server where hello app resides</span></span> |
| <span data-ttu-id="8bc87-126">Disk (önbelleğe alınmış)</span><span class="sxs-lookup"><span data-stu-id="8bc87-126">Disk (Cached)</span></span> |<span data-ttu-id="8bc87-127">Hızlı yürütme.</span><span class="sxs-lookup"><span data-stu-id="8bc87-127">Fast execution.</span></span> <span data-ttu-id="8bc87-128">Uygulama içerik kaynağı kullanılabilirliğine bağlı değil</span><span class="sxs-lookup"><span data-stu-id="8bc87-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="8bc87-129">Oluşan şişirmeyi - (127 GB sınırını) görüntüsü yer alır</span><span class="sxs-lookup"><span data-stu-id="8bc87-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="8bc87-130">Hedefleme</span><span class="sxs-lookup"><span data-stu-id="8bc87-130">Targeting</span></span> |<span data-ttu-id="8bc87-131">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="8bc87-131">User</span></span> |<span data-ttu-id="8bc87-132">Tam tek başına App-V altyapısı gerektirir</span><span class="sxs-lookup"><span data-stu-id="8bc87-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="8bc87-133">Genel (makine)</span><span class="sxs-lookup"><span data-stu-id="8bc87-133">Global (machine)</span></span> |<span data-ttu-id="8bc87-134">Önceden yayımlama veya yayımlama kullanarak hedef sunucu</span><span class="sxs-lookup"><span data-stu-id="8bc87-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="8bc87-135">Tooupdate hello uygulama (büyük) istiyorsanız tooupdate Azure görüntünüzü gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bc87-135">Need tooupdate your Azure image if you want tooupdate hello app (huge).</span></span> <span data-ttu-id="8bc87-136">Görüntü alan kaplar.</span><span class="sxs-lookup"><span data-stu-id="8bc87-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="8bc87-137">Özel görüntünüzü ve karma koleksiyonunuzda oluşturduktan sonra uygulamanızı yayımlamak, kullanıcılar atayın ve herhangi bir yere tooany aygıt teslim Azure Remoteapp'te barındırılan, var olan App-V uygulamalarınızın keyfini çıkarın.</span><span class="sxs-lookup"><span data-stu-id="8bc87-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered tooany device anywhere.</span></span>

