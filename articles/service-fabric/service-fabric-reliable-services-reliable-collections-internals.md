---
title: "Service Fabric güvenilir durum Yöneticisi ve güvenilir koleksiyonu iç aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="86c00-103">Azure Service Fabric güvenilir durumu Yöneticisi ve güvenilir koleksiyonu dahili bileşenleri</span><span class="sxs-lookup"><span data-stu-id="86c00-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="86c00-104">Bu belge, çekirdek bileşenleri hello arka planda nasıl güvenilir durum Yöneticisi ve güvenilir koleksiyonları toosee içinde ilgili alır.</span><span class="sxs-lookup"><span data-stu-id="86c00-104">This document delves inside Reliable State Manager and Reliable Collections toosee how core components work behind hello scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="86c00-105">Bu belge iş sürüyor değil.</span><span class="sxs-lookup"><span data-stu-id="86c00-105">This document is work in-progress.</span></span> <span data-ttu-id="86c00-106">Yorumlar toothis makale tootell bize eklemek hangi konu hakkında daha fazla toolearn istersiniz.</span><span class="sxs-lookup"><span data-stu-id="86c00-106">Add comments toothis article tootell us what topic you would like toolearn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="86c00-107">Yerel Kalıcılık modeli: günlük ve denetim noktası</span><span class="sxs-lookup"><span data-stu-id="86c00-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="86c00-108">Merhaba güvenilir durum Yöneticisi ve güvenilir koleksiyonları günlük ve denetim noktası adlı Kalıcılık modeli izleyin.</span><span class="sxs-lookup"><span data-stu-id="86c00-108">hello Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="86c00-109">Bu modelde, her bir durum değişikliği diskte önce oturum açmış ve bellekte uygulanır.</span><span class="sxs-lookup"><span data-stu-id="86c00-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="86c00-110">Merhaba tam durum kendisini nadiren (paketini kalıcı</span><span class="sxs-lookup"><span data-stu-id="86c00-110">hello complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="86c00-111">Denetim noktası).</span><span class="sxs-lookup"><span data-stu-id="86c00-111">Checkpoint).</span></span>
<span data-ttu-id="86c00-112">Merhaba avantaj farkları içine sıralı yalnızca Ekle yazma diskteki Gelişmiş performans için açık emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86c00-112">hello benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="86c00-113">toobetter hello günlük ve denetim noktası modeli anlamak, ilk hello sonsuz disk senaryosu bakalım.</span><span class="sxs-lookup"><span data-stu-id="86c00-113">toobetter understand hello Log and Checkpoint model, let’s first look at hello infinite disk scenario.</span></span>
<span data-ttu-id="86c00-114">çoğaltılana önce hello güvenilir durum Yöneticisi her işlemi günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="86c00-114">hello Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="86c00-115">Günlüğe kaydetme hello güvenilir koleksiyonları tooapply hello işlemi yalnızca bellekte sağlar.</span><span class="sxs-lookup"><span data-stu-id="86c00-115">Logging allows hello Reliable Collections tooapply hello operation only in memory.</span></span>
<span data-ttu-id="86c00-116">Günlükleri kalıcı yaptığınızdan, hatta hello çoğaltma başarısız olur ve yeniden, toobe gerektiğinde Merhaba güvenilir durum Yöneticisi yeterli bilgi kendi günlük tooreplay hello çoğaltma kaybetti tüm hello işlemler var.</span><span class="sxs-lookup"><span data-stu-id="86c00-116">Since logs are persisted, even when hello replica fails and needs toobe restarted, hello Reliable State Manager has enough information in its log tooreplay all hello operations hello replica has lost.</span></span>
<span data-ttu-id="86c00-117">Merhaba disk sonsuz olduğu gibi hello güvenilir koleksiyonu toomanage yalnızca hello bellek içi durumunun gerekiyor ve günlük kayıtlarını hiçbir zaman kaldırılan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="86c00-117">As hello disk is infinite, log records never need toobe removed and hello Reliable Collection needs toomanage only hello in-memory state.</span></span>

<span data-ttu-id="86c00-118">Şimdi hello sınırlı disk senaryosu bakalım.</span><span class="sxs-lookup"><span data-stu-id="86c00-118">Now let’s look at hello finite disk scenario.</span></span>
<span data-ttu-id="86c00-119">Günlük kayıtlarını birleştirdiğinizde hello güvenilir durum Yöneticisi disk alanı yetersiz çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="86c00-119">As log records accumulate, hello Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="86c00-120">Gerçekleşmeden önce hello güvenilir durum Yöneticisi tootruncate hello yeni kayıtlar için kendi günlük toomake yer gerekir.</span><span class="sxs-lookup"><span data-stu-id="86c00-120">Before that happens, hello Reliable State Manager needs tootruncate its log toomake room for hello newer records.</span></span>
<span data-ttu-id="86c00-121">Güvenilir durum Yöneticisi isteklerine güvenilir koleksiyonları toocheckpoint kendi bellek içi durumu toodisk hello.</span><span class="sxs-lookup"><span data-stu-id="86c00-121">Reliable State Manager requests hello Reliable Collections toocheckpoint their in-memory state toodisk.</span></span>
<span data-ttu-id="86c00-122">Bu noktada, hello güvenilir koleksiyonları bellek içi durumuna kalıcı.</span><span class="sxs-lookup"><span data-stu-id="86c00-122">At this point, hello Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="86c00-123">Bunların denetim noktaları Hello güvenilir koleksiyonları tamamladıktan sonra hello güvenilir durum Yöneticisi hello günlük toofree disk alanı kısaltabilir.</span><span class="sxs-lookup"><span data-stu-id="86c00-123">Once hello Reliable Collections complete their checkpoints, hello Reliable State Manager can truncate hello log toofree up disk space.</span></span>
<span data-ttu-id="86c00-124">Merhaba çoğaltma yeniden toobe gerektiğinde güvenilir koleksiyonları belirttiğinizde durumlarına kurtarmak ve hello güvenilir durum Yöneticisi kurtarır ve hello son denetim noktasının bu yana gerçekleşen tüm hello durum değişiklikleri geri kazanır.</span><span class="sxs-lookup"><span data-stu-id="86c00-124">When hello replica needs toobe restarted, Reliable Collections recover their checkpointed state, and hello Reliable State Manager recovers and plays back all hello state changes that occurred since hello last checkpoint.</span></span>

<span data-ttu-id="86c00-125">Başka bir değer denetim noktası oluşturma ekleme olan yaygın senaryolar kurtarma sürelerini artırır.</span><span class="sxs-lookup"><span data-stu-id="86c00-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="86c00-126">Günlük hello son denetim noktasının bu yana gerçekleşen tüm işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="86c00-126">Log contains all operations that have happened since hello last checkpoint.</span></span>
<span data-ttu-id="86c00-127">Bu nedenle, güvenilir sözlükte belirli bir satır için birden çok değer gibi bir öğede birden fazla sürümünü içerebilir.</span><span class="sxs-lookup"><span data-stu-id="86c00-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="86c00-128">Buna karşılık, güvenilir koleksiyonu kontrol noktalarını yalnızca bir anahtar için her bir değerin en son sürümünü hello.</span><span class="sxs-lookup"><span data-stu-id="86c00-128">In contrast, a Reliable Collection checkpoints only hello latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86c00-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="86c00-129">Next steps</span></span>
* [<span data-ttu-id="86c00-130">İşlemler ve kilitleri</span><span class="sxs-lookup"><span data-stu-id="86c00-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

