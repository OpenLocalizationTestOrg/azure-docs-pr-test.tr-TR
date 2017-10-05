---
title: "Azure Service Fabric güvenilir durumu Yöneticisi ve güvenilir koleksiyonu iç | Microsoft Docs"
description: "Derin Dalış güvenilir koleksiyonu kavramları ve Azure Service Fabric tasarımında."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: d607449a16e886337ab1bd96213fbb4231124353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="b85bd-103">Azure Service Fabric güvenilir durumu Yöneticisi ve güvenilir koleksiyonu dahili bileşenleri</span><span class="sxs-lookup"><span data-stu-id="b85bd-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="b85bd-104">Bu belge, güvenilir durum Yöneticisi ve güvenilir koleksiyonları çekirdek bileşenleri arka planda nasıl çalıştığını görmek için içinde ilgili alır.</span><span class="sxs-lookup"><span data-stu-id="b85bd-104">This document delves inside Reliable State Manager and Reliable Collections to see how core components work behind the scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="b85bd-105">Bu belge iş sürüyor değil.</span><span class="sxs-lookup"><span data-stu-id="b85bd-105">This document is work in-progress.</span></span> <span data-ttu-id="b85bd-106">Daha fazla bilgi edinmek istediğiniz hangi konu bize iletmek için bu makalede yorumlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b85bd-106">Add comments to this article to tell us what topic you would like to learn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="b85bd-107">Yerel Kalıcılık modeli: günlük ve denetim noktası</span><span class="sxs-lookup"><span data-stu-id="b85bd-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="b85bd-108">Durum Yöneticisi'ni güvenilir ve güvenilir koleksiyonları günlük ve denetim noktası adlı Kalıcılık modeli izleyin.</span><span class="sxs-lookup"><span data-stu-id="b85bd-108">The Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="b85bd-109">Bu modelde, her bir durum değişikliği diskte önce oturum açmış ve bellekte uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b85bd-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="b85bd-110">Tam durum nadiren (paketini kalıcı</span><span class="sxs-lookup"><span data-stu-id="b85bd-110">The complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="b85bd-111">Denetim noktası).</span><span class="sxs-lookup"><span data-stu-id="b85bd-111">Checkpoint).</span></span>
<span data-ttu-id="b85bd-112">Farkları sıralı yalnızca Ekle yazma diskteki Gelişmiş performans için içine bırakılacağı avantajdır.</span><span class="sxs-lookup"><span data-stu-id="b85bd-112">The benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="b85bd-113">Günlük ve denetim noktası modeli daha iyi anlamak için ilk sonsuz disk senaryosu bakalım.</span><span class="sxs-lookup"><span data-stu-id="b85bd-113">To better understand the Log and Checkpoint model, let’s first look at the infinite disk scenario.</span></span>
<span data-ttu-id="b85bd-114">Çoğaltılana önce güvenilir durum Yöneticisi her işlemi günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b85bd-114">The Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="b85bd-115">Günlüğe kaydetme güvenilir yalnızca bellekte işlemi uygulamak koleksiyonları sağlar.</span><span class="sxs-lookup"><span data-stu-id="b85bd-115">Logging allows the Reliable Collections to apply the operation only in memory.</span></span>
<span data-ttu-id="b85bd-116">Çoğaltma başarısız olur ve yeniden başlatılması gerekiyor bile günlükleri, kalıcı olduğundan, güvenilir durum Yöneticisi çoğaltma kaybetti tüm işlemleri yürütme kendi günlüğünde yeterli bilgiye sahip.</span><span class="sxs-lookup"><span data-stu-id="b85bd-116">Since logs are persisted, even when the replica fails and needs to be restarted, the Reliable State Manager has enough information in its log to replay all the operations the replica has lost.</span></span>
<span data-ttu-id="b85bd-117">Disk sonsuz olduğu gibi günlük kayıtlarını hiçbir zaman kaldırılmaları gerekir ve yalnızca bellek içi durumunu yönetmek güvenilir koleksiyonu gerekir.</span><span class="sxs-lookup"><span data-stu-id="b85bd-117">As the disk is infinite, log records never need to be removed and the Reliable Collection needs to manage only the in-memory state.</span></span>

<span data-ttu-id="b85bd-118">Şimdi sınırlı disk senaryosu bakalım.</span><span class="sxs-lookup"><span data-stu-id="b85bd-118">Now let’s look at the finite disk scenario.</span></span>
<span data-ttu-id="b85bd-119">Günlük kayıtlarını birleştirdiğinizde güvenilir durum yöneticisinin disk alanı yetersiz çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b85bd-119">As log records accumulate, the Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="b85bd-120">Bu durum önce güvenilir durum Yöneticisi'ni yeni kayıtlar için yer açmak için baytta bir kesecek gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="b85bd-120">Before that happens, the Reliable State Manager needs to truncate its log to make room for the newer records.</span></span>
<span data-ttu-id="b85bd-121">Güvenilir durum Yöneticisi'ni kontrol noktası güvenilir koleksiyonlarına bellek içi durumlarına disk ister.</span><span class="sxs-lookup"><span data-stu-id="b85bd-121">Reliable State Manager requests the Reliable Collections to checkpoint their in-memory state to disk.</span></span>
<span data-ttu-id="b85bd-122">Bu noktada, güvenilir koleksiyonları bellek içi durumuna kalıcı.</span><span class="sxs-lookup"><span data-stu-id="b85bd-122">At this point, the Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="b85bd-123">Güvenilir koleksiyonları bunların denetim noktaları tamamlandığında, güvenilir durum Yöneticisi disk alanını boşaltmak için günlük kısaltabilir.</span><span class="sxs-lookup"><span data-stu-id="b85bd-123">Once the Reliable Collections complete their checkpoints, the Reliable State Manager can truncate the log to free up disk space.</span></span>
<span data-ttu-id="b85bd-124">Çoğaltma yeniden başlatılması gerektiğinde, güvenilir koleksiyonları belirttiğinizde durumlarına geri yükleyin ve güvenilir durum Yöneticisi kurtarır ve en son kontrol bu yana gerçekleşen tüm durum değişikliklerini geri kazanır.</span><span class="sxs-lookup"><span data-stu-id="b85bd-124">When the replica needs to be restarted, Reliable Collections recover their checkpointed state, and the Reliable State Manager recovers and plays back all the state changes that occurred since the last checkpoint.</span></span>

<span data-ttu-id="b85bd-125">Başka bir değer denetim noktası oluşturma ekleme olan yaygın senaryolar kurtarma sürelerini artırır.</span><span class="sxs-lookup"><span data-stu-id="b85bd-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="b85bd-126">Günlüğü, son denetim noktasının bu yana gerçekleşen tüm işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b85bd-126">Log contains all operations that have happened since the last checkpoint.</span></span>
<span data-ttu-id="b85bd-127">Bu nedenle, güvenilir sözlükte belirli bir satır için birden çok değer gibi bir öğede birden fazla sürümünü içerebilir.</span><span class="sxs-lookup"><span data-stu-id="b85bd-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="b85bd-128">Buna karşılık, güvenilir koleksiyonu kontrol noktaları her bir anahtar değeri yalnızca en son sürümü.</span><span class="sxs-lookup"><span data-stu-id="b85bd-128">In contrast, a Reliable Collection checkpoints only the latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b85bd-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b85bd-129">Next steps</span></span>
* [<span data-ttu-id="b85bd-130">İşlemler ve kilitleri</span><span class="sxs-lookup"><span data-stu-id="b85bd-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

