---
title: "Azure anahtar kasası etkiler kesintisi hizmet durumunda Azure yapmanız gerekenler | Microsoft Docs"
description: "Azure anahtar kasası etkileyen bir Azure hizmet kesintisi durumunda yapmanız gerekenler hakkında bilgi edinin."
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 6419d54c54e7d19103419262b79e7a5268b2268c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="aa78f-103">Azure anahtar kasası kullanılabilirlik ve artıklık</span><span class="sxs-lookup"><span data-stu-id="aa78f-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="aa78f-104">Azure anahtar kasası hizmetinin bileşenleri tek tek başarısız olsa bile anahtarları ve gizli anahtarları uygulamanıza kullanılabilir olarak kaldıklarından emin olmak için artıklık birden çok katman özellikleri.</span><span class="sxs-lookup"><span data-stu-id="aa78f-104">Azure Key Vault features multiple layers of redundancy to make sure that your keys and secrets remain available to your application even if individual components of the service fail.</span></span>

<span data-ttu-id="aa78f-105">Anahtar kasanızı içeriğini, bölge içinde ve ikincil bir bölgeye en az 150 mil hemen ancak aynı Coğrafya içinde çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="aa78f-105">The contents of your key vault are replicated within the region and to a secondary region at least 150 miles away but within the same geography.</span></span> <span data-ttu-id="aa78f-106">Bu anahtarları ve gizli anahtarları, yüksek dayanıklılık tutar.</span><span class="sxs-lookup"><span data-stu-id="aa78f-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="aa78f-107">Bkz: [Azure bölgeleri eşleştirilmiş](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) belirli bir bölge çiftleri hakkındaki ayrıntılar için belge.</span><span class="sxs-lookup"><span data-stu-id="aa78f-107">See the [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="aa78f-108">Anahtar kasası hizmetinde bileşenleri tek tek başarısız olursa, bölge içindeki diğer bileşenleri isteğiniz işlevlerin düşüşü olmadan olduğundan emin olmak için hizmet adımı.</span><span class="sxs-lookup"><span data-stu-id="aa78f-108">If individual components within the key vault service fail, alternate components within the region step in to serve your request to make sure that there is no degradation of functionality.</span></span> <span data-ttu-id="aa78f-109">Bu tetiklemek için herhangi bir eylemde bulunmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="aa78f-109">You do not need to take any action to trigger this.</span></span> <span data-ttu-id="aa78f-110">Otomatik olarak gerçekleşir ve size saydam olacaktır.</span><span class="sxs-lookup"><span data-stu-id="aa78f-110">It happens automatically and will be transparent to you.</span></span>

<span data-ttu-id="aa78f-111">Ender olayda, tüm bir Azure bölgesi kullanılamıyor, bu bölgedeki Azure anahtar kasası, yaptığınız istekleri otomatik olarak yönlendirilir (*devredilir*) ikincil bir bölgeye.</span><span class="sxs-lookup"><span data-stu-id="aa78f-111">In the rare event that an entire Azure region is unavailable, the requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) to a secondary region.</span></span> <span data-ttu-id="aa78f-112">Birincil bölge yeniden kullanılabilir duruma geldiğinde, istekleri geri yönlendirilir (*geri başarısız*) birincil bölge için.</span><span class="sxs-lookup"><span data-stu-id="aa78f-112">When the primary region is available again, requests are routed back (*failed back*) to the primary region.</span></span> <span data-ttu-id="aa78f-113">Yeniden, bu otomatik olarak gerçekleşir çünkü herhangi bir eylemde bulunmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="aa78f-113">Again, you do not need to take any action because this happens automatically.</span></span>

<span data-ttu-id="aa78f-114">Dikkat edilmesi gereken birkaç uyarılar vardır:</span><span class="sxs-lookup"><span data-stu-id="aa78f-114">There are a few caveats to be aware of:</span></span>

* <span data-ttu-id="aa78f-115">Bölge yük devretmesi durumunda, yük devretme hizmet birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="aa78f-115">In the event of a region failover, it may take a few minutes for the service to fail over.</span></span> <span data-ttu-id="aa78f-116">Yük devretme işlemi tamamlanana kadar bu süre boyunca olan istekler başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="aa78f-116">Requests that are made during this time may fail until the failover completes.</span></span>
* <span data-ttu-id="aa78f-117">Bir yük devretme işlemi tamamlandıktan sonra anahtar kasanızı salt okunur modda değil.</span><span class="sxs-lookup"><span data-stu-id="aa78f-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="aa78f-118">Bu modda desteklenen istekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="aa78f-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="aa78f-119">Anahtar kasalarının listesi</span><span class="sxs-lookup"><span data-stu-id="aa78f-119">List key vaults</span></span>
  * <span data-ttu-id="aa78f-120">Anahtar kasalarını özelliklerini alır</span><span class="sxs-lookup"><span data-stu-id="aa78f-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="aa78f-121">Gizli anahtarları listeleme</span><span class="sxs-lookup"><span data-stu-id="aa78f-121">List secrets</span></span>
  * <span data-ttu-id="aa78f-122">Gizli kod dizeleri alma</span><span class="sxs-lookup"><span data-stu-id="aa78f-122">Get secrets</span></span>
  * <span data-ttu-id="aa78f-123">Liste anahtarları</span><span class="sxs-lookup"><span data-stu-id="aa78f-123">List keys</span></span>
  * <span data-ttu-id="aa78f-124">Get (özelliklerini) anahtarları</span><span class="sxs-lookup"><span data-stu-id="aa78f-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="aa78f-125">Şifreleme</span><span class="sxs-lookup"><span data-stu-id="aa78f-125">Encrypt</span></span>
  * <span data-ttu-id="aa78f-126">Şifre çözme</span><span class="sxs-lookup"><span data-stu-id="aa78f-126">Decrypt</span></span>
  * <span data-ttu-id="aa78f-127">Kaydırma</span><span class="sxs-lookup"><span data-stu-id="aa78f-127">Wrap</span></span>
  * <span data-ttu-id="aa78f-128">Kaydırma</span><span class="sxs-lookup"><span data-stu-id="aa78f-128">Unwrap</span></span>
  * <span data-ttu-id="aa78f-129">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="aa78f-129">Verify</span></span>
  * <span data-ttu-id="aa78f-130">Oturum</span><span class="sxs-lookup"><span data-stu-id="aa78f-130">Sign</span></span>
  * <span data-ttu-id="aa78f-131">Backup</span><span class="sxs-lookup"><span data-stu-id="aa78f-131">Backup</span></span>
* <span data-ttu-id="aa78f-132">Bir yük devretme geri başarısız olduktan sonra tüm istek türleri (okuma dahil olmak üzere *ve* yazma isteklerine) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aa78f-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

