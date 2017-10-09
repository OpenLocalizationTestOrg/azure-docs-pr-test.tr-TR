---
title: "aaaManage StorSimple birim kapsayıcıları | Microsoft Docs"
description: "Merhaba StorSimple hizmeti birim kapsayıcıları tooadd sayfasında, değiştirmek veya birim kapsayıcısı silmek Yöneticisi nasıl kullanabileceğinizi açıklar."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="171a2-103">Merhaba StorSimple Yöneticisi hizmet toomanage StorSimple birim kapsayıcıları kullanma</span><span class="sxs-lookup"><span data-stu-id="171a2-103">Use hello StorSimple Manager service toomanage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="171a2-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="171a2-104">Overview</span></span>
<span data-ttu-id="171a2-105">Bu öğretici nasıl toouse StorSimple Yöneticisi hizmet toocreate hello ve StorSimple birim kapsayıcıları yönetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="171a2-105">This tutorial explains how toouse hello StorSimple Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="171a2-106">Microsoft Azure StorSimple aygıtta bir birim kapsayıcısı depolama hesabı, şifreleme ve bant genişliği tüketimi ayarları paylaşan bir veya daha fazla birimleri içerir.</span><span class="sxs-lookup"><span data-stu-id="171a2-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="171a2-107">Bir aygıt tüm birimlerde için birden çok birim kapsayıcıları olabilir.</span><span class="sxs-lookup"><span data-stu-id="171a2-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="171a2-108">Birim kapsayıcısı öznitelikleri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="171a2-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="171a2-109">**Birimleri** – hello katmanlı veya hello birim kapsayıcı içinde bulunan StorSimple birimlerini'yerel olarak sabitlenmiş.</span><span class="sxs-lookup"><span data-stu-id="171a2-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> <span data-ttu-id="171a2-110">Birim kapsayıcısı too256 StorSimple birimleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="171a2-110">A volume container may contain up too256 StorSimple volumes.</span></span>
* <span data-ttu-id="171a2-111">**Şifreleme** – her birim kapsayıcısı için tanımlanabilen bir şifreleme anahtarı.</span><span class="sxs-lookup"><span data-stu-id="171a2-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="171a2-112">Bu anahtar StorSimple cihaz toohello buluttan gönderilen hello verileri şifrelemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="171a2-112">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="171a2-113">Askeri düzeyde AES 256 bit anahtar hello kullanıcı tarafından girilen anahtarla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="171a2-113">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="171a2-114">toosecure, verilerinizin her zaman bulut depolama şifrelemesini etkinleştir olan öneririz.</span><span class="sxs-lookup"><span data-stu-id="171a2-114">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="171a2-115">**Depolama hesabı** – hello bağlantılı tooyour bulut depolama hizmeti sağlayıcısıdır depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="171a2-115">**Storage account** – hello storage account that is linked tooyour cloud storage service provider.</span></span> <span data-ttu-id="171a2-116">Birim kapsayıcısı içinde bulunan tüm hello birimleri bu depolama hesabını paylaşır.</span><span class="sxs-lookup"><span data-stu-id="171a2-116">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="171a2-117">Varolan bir listesinden bir depolama hesabını seçin veya hello birim kapsayıcısı oluşturduğunuzda ve bu hesabın hello erişim kimlik bilgilerini belirtin yeni bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="171a2-117">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="171a2-118">**Bulut bant genişliği** – hello cihazdaki hello verileri toohello bulut gönderildiğinde hello aygıt tarafından kullanılan bant genişliği hello.</span><span class="sxs-lookup"><span data-stu-id="171a2-118">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="171a2-119">Bu kapsayıcı tanımlarken 1 ile 1000 MB/sn arasında bir değer belirterek bir bant genişliği denetimini uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="171a2-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="171a2-120">Kullanılabilir tüm bant genişliği hello aygıt tooconsume istiyorsanız bu alanı tooUnlimited ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="171a2-120">If you want hello device tooconsume all available bandwidth, set this field tooUnlimited.</span></span> <span data-ttu-id="171a2-121">Ayrıca, oluşturmak ve bant genişliği şablonu tooallocate bant zamanlamaya göre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="171a2-121">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

![Birim kapsayıcıları sayfası](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="171a2-123">Bu aşağıdaki yordamlarda, nasıl toouse hello StorSimple açıklanmaktadır **birim kapsayıcıları** ortak işlemleri aşağıdaki sayfayı toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="171a2-123">This following procedures explain how toouse hello StorSimple **Volume containers** page toocomplete hello following common operations:</span></span>

* <span data-ttu-id="171a2-124">Birim kapsayıcısı Ekle</span><span class="sxs-lookup"><span data-stu-id="171a2-124">Add a volume container</span></span> 
* <span data-ttu-id="171a2-125">Birim kapsayıcısı değiştirme</span><span class="sxs-lookup"><span data-stu-id="171a2-125">Modify a volume container</span></span> 
* <span data-ttu-id="171a2-126">Birim kapsayıcısı Sil</span><span class="sxs-lookup"><span data-stu-id="171a2-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="171a2-127">Birim kapsayıcısı Ekle</span><span class="sxs-lookup"><span data-stu-id="171a2-127">Add a volume container</span></span>
<span data-ttu-id="171a2-128">Aşağıdaki adımları tooadd birim kapsayıcısı hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="171a2-128">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="171a2-129">Birim kapsayıcısı değiştirme</span><span class="sxs-lookup"><span data-stu-id="171a2-129">Modify a volume container</span></span>
<span data-ttu-id="171a2-130">Aşağıdaki adımları toomodify birim kapsayıcısı hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="171a2-130">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="171a2-131">Birim kapsayıcısı Sil</span><span class="sxs-lookup"><span data-stu-id="171a2-131">Delete a volume container</span></span>
<span data-ttu-id="171a2-132">Birim kapsayıcısı içindeki birimi vardır.</span><span class="sxs-lookup"><span data-stu-id="171a2-132">A volume container has volumes within it.</span></span> <span data-ttu-id="171a2-133">Yalnızca kapsadığı tüm hello birimler ilk silindiğinde silinebilir.</span><span class="sxs-lookup"><span data-stu-id="171a2-133">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="171a2-134">Aşağıdaki adımları toodelete birim kapsayıcısı hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="171a2-134">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="171a2-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="171a2-135">Next steps</span></span>
* <span data-ttu-id="171a2-136">Daha fazla bilgi edinmek [StorSimple birimlerini yönetme](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="171a2-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="171a2-137">Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="171a2-137">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

