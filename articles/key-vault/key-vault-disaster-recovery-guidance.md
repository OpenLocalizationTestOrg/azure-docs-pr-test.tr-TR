---
title: "Azure anahtar kasası etkileyen bir Azure hizmet kesintisi hello olayı içinde aaaWhat toodo | Microsoft Docs"
description: "Azure anahtar kasası etkileyen bir Azure hizmet kesintisi hello olayı içinde hangi toodo öğrenin."
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
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="a09cc-103">Azure anahtar kasası kullanılabilirlik ve artıklık</span><span class="sxs-lookup"><span data-stu-id="a09cc-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="a09cc-104">Azure anahtar kasası artıklık toomake hello bileşenleri tek tek hizmet başarısız olsa bile, anahtarları ve gizli anahtarları kullanılabilir tooyour uygulama kalmasını çok katmanlı özellikleri.</span><span class="sxs-lookup"><span data-stu-id="a09cc-104">Azure Key Vault features multiple layers of redundancy toomake sure that your keys and secrets remain available tooyour application even if individual components of hello service fail.</span></span>

<span data-ttu-id="a09cc-105">Merhaba anahtar kasanızı içeriğini hello bölge ve tooa ikincil bölge içinde en az 150 mil hemen ancak hello içinde çoğaltılır aynı coğrafi konum.</span><span class="sxs-lookup"><span data-stu-id="a09cc-105">hello contents of your key vault are replicated within hello region and tooa secondary region at least 150 miles away but within hello same geography.</span></span> <span data-ttu-id="a09cc-106">Bu anahtarları ve gizli anahtarları, yüksek dayanıklılık tutar.</span><span class="sxs-lookup"><span data-stu-id="a09cc-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="a09cc-107">Merhaba bkz [Azure bölgeleri eşleştirilmiş](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) belirli bir bölge çiftleri hakkındaki ayrıntılar için belge.</span><span class="sxs-lookup"><span data-stu-id="a09cc-107">See hello [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="a09cc-108">Merhaba anahtar kasası hizmetinde bileşenleri tek tek başarısız olursa, diğer bileşenleri hello bölge içinde istek toomake işlevlerin düşüşü olmadan olduğundan emin tooserve içinde adım.</span><span class="sxs-lookup"><span data-stu-id="a09cc-108">If individual components within hello key vault service fail, alternate components within hello region step in tooserve your request toomake sure that there is no degradation of functionality.</span></span> <span data-ttu-id="a09cc-109">Tüm eylem tootrigger tootake gerekmez bu.</span><span class="sxs-lookup"><span data-stu-id="a09cc-109">You do not need tootake any action tootrigger this.</span></span> <span data-ttu-id="a09cc-110">Otomatik olarak gerçekleşir ve saydam tooyou olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a09cc-110">It happens automatically and will be transparent tooyou.</span></span>

<span data-ttu-id="a09cc-111">Tüm bir Azure bölgesi kullanılamıyor hello ender olayda, bu bölgedeki Azure anahtar kasası, yaptığınız hello istekleri otomatik olarak yönlendirilir (*devredilir*) tooa ikincil bölge.</span><span class="sxs-lookup"><span data-stu-id="a09cc-111">In hello rare event that an entire Azure region is unavailable, hello requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) tooa secondary region.</span></span> <span data-ttu-id="a09cc-112">Merhaba birincil bölge yeniden kullanılabilir duruma geldiğinde, istekleri geri yönlendirilir (*geri başarısız*) toohello birincil bölge.</span><span class="sxs-lookup"><span data-stu-id="a09cc-112">When hello primary region is available again, requests are routed back (*failed back*) toohello primary region.</span></span> <span data-ttu-id="a09cc-113">Yeniden, bu otomatik olarak gerçekleşir çünkü tootake herhangi bir eylem gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a09cc-113">Again, you do not need tootake any action because this happens automatically.</span></span>

<span data-ttu-id="a09cc-114">Farkında birkaç uyarılar toobe vardır:</span><span class="sxs-lookup"><span data-stu-id="a09cc-114">There are a few caveats toobe aware of:</span></span>

* <span data-ttu-id="a09cc-115">Bir bölge yük devretme Hello olayda onu hello hizmet toofail birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="a09cc-115">In hello event of a region failover, it may take a few minutes for hello service toofail over.</span></span> <span data-ttu-id="a09cc-116">Merhaba yük devretme işlemi tamamlanana kadar bu süre boyunca olan istekler başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="a09cc-116">Requests that are made during this time may fail until hello failover completes.</span></span>
* <span data-ttu-id="a09cc-117">Bir yük devretme işlemi tamamlandıktan sonra anahtar kasanızı salt okunur modda değil.</span><span class="sxs-lookup"><span data-stu-id="a09cc-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="a09cc-118">Bu modda desteklenen istekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a09cc-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="a09cc-119">Anahtar kasalarının listesi</span><span class="sxs-lookup"><span data-stu-id="a09cc-119">List key vaults</span></span>
  * <span data-ttu-id="a09cc-120">Anahtar kasalarını özelliklerini alır</span><span class="sxs-lookup"><span data-stu-id="a09cc-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="a09cc-121">Gizli anahtarları listeleme</span><span class="sxs-lookup"><span data-stu-id="a09cc-121">List secrets</span></span>
  * <span data-ttu-id="a09cc-122">Gizli kod dizeleri alma</span><span class="sxs-lookup"><span data-stu-id="a09cc-122">Get secrets</span></span>
  * <span data-ttu-id="a09cc-123">Liste anahtarları</span><span class="sxs-lookup"><span data-stu-id="a09cc-123">List keys</span></span>
  * <span data-ttu-id="a09cc-124">Get (özelliklerini) anahtarları</span><span class="sxs-lookup"><span data-stu-id="a09cc-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="a09cc-125">Şifreleme</span><span class="sxs-lookup"><span data-stu-id="a09cc-125">Encrypt</span></span>
  * <span data-ttu-id="a09cc-126">Şifre çözme</span><span class="sxs-lookup"><span data-stu-id="a09cc-126">Decrypt</span></span>
  * <span data-ttu-id="a09cc-127">Kaydırma</span><span class="sxs-lookup"><span data-stu-id="a09cc-127">Wrap</span></span>
  * <span data-ttu-id="a09cc-128">Kaydırma</span><span class="sxs-lookup"><span data-stu-id="a09cc-128">Unwrap</span></span>
  * <span data-ttu-id="a09cc-129">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="a09cc-129">Verify</span></span>
  * <span data-ttu-id="a09cc-130">Oturum</span><span class="sxs-lookup"><span data-stu-id="a09cc-130">Sign</span></span>
  * <span data-ttu-id="a09cc-131">Backup</span><span class="sxs-lookup"><span data-stu-id="a09cc-131">Backup</span></span>
* <span data-ttu-id="a09cc-132">Bir yük devretme geri başarısız olduktan sonra tüm istek türleri (okuma dahil olmak üzere *ve* yazma isteklerine) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a09cc-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

