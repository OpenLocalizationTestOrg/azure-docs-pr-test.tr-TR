---
title: "aaaManage, StorSimple birim kapsayıcıları hello StorSimple 8000 serisi aygıtta | Microsoft Docs"
description: "Merhaba hizmet birim kapsayıcıları tooadd sayfasında, değiştirmek veya birim kapsayıcısı silmek Aygıt Yöneticisi'ni StorSimple nasıl kullanabileceğinizi açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="b5bed-103">Merhaba StorSimple cihaz Yöneticisi hizmeti toomanage StorSimple birim kapsayıcıları kullanma</span><span class="sxs-lookup"><span data-stu-id="b5bed-103">Use hello StorSimple Device Manager service toomanage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="b5bed-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b5bed-104">Overview</span></span>
<span data-ttu-id="b5bed-105">Bu öğretici nasıl toouse StorSimple cihaz Yöneticisi hizmeti toocreate hello ve StorSimple birim kapsayıcıları yönetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b5bed-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="b5bed-106">Microsoft Azure StorSimple aygıtta bir birim kapsayıcısı depolama hesabı, şifreleme ve bant genişliği tüketimi ayarları paylaşan bir veya daha fazla birimleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b5bed-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="b5bed-107">Bir aygıt tüm birimlerde için birden çok birim kapsayıcıları olabilir.</span><span class="sxs-lookup"><span data-stu-id="b5bed-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="b5bed-108">Birim kapsayıcısı öznitelikleri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b5bed-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="b5bed-109">**Birimleri** – hello katmanlı veya hello birim kapsayıcı içinde bulunan StorSimple birimlerini'yerel olarak sabitlenmiş.</span><span class="sxs-lookup"><span data-stu-id="b5bed-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> 
* <span data-ttu-id="b5bed-110">**Şifreleme** – her birim kapsayıcısı için tanımlanabilen bir şifreleme anahtarı.</span><span class="sxs-lookup"><span data-stu-id="b5bed-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="b5bed-111">Bu anahtar StorSimple cihaz toohello buluttan gönderilen hello verileri şifrelemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b5bed-111">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="b5bed-112">Askeri düzeyde AES 256 bit anahtar hello kullanıcı tarafından girilen anahtarla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b5bed-112">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="b5bed-113">toosecure, verilerinizin her zaman bulut depolama şifrelemesini etkinleştir olan öneririz.</span><span class="sxs-lookup"><span data-stu-id="b5bed-113">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="b5bed-114">**Depolama hesabı** – kullanılan toostore hello veriler Azure depolama hesabı hello.</span><span class="sxs-lookup"><span data-stu-id="b5bed-114">**Storage account** – hello Azure storage account that is used toostore hello data.</span></span> <span data-ttu-id="b5bed-115">Birim kapsayıcısı içinde bulunan tüm hello birimleri bu depolama hesabını paylaşır.</span><span class="sxs-lookup"><span data-stu-id="b5bed-115">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="b5bed-116">Varolan bir listesinden bir depolama hesabını seçin veya hello birim kapsayıcısı oluşturduğunuzda ve bu hesabın hello erişim kimlik bilgilerini belirtin yeni bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b5bed-116">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="b5bed-117">**Bulut bant genişliği** – hello cihazdaki hello verileri toohello bulut gönderildiğinde hello aygıt tarafından kullanılan bant genişliği hello.</span><span class="sxs-lookup"><span data-stu-id="b5bed-117">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="b5bed-118">Bu kapsayıcı oluşturduğunuzda, 1 MB/sn ile 1000 MB/sn arasında bir değer belirterek bant genişliği denetimini uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5bed-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="b5bed-119">Kullanılabilir tüm bant genişliği hello aygıt tooconsume istiyorsanız, bu alan çok ayarlayın**sınırsız**.</span><span class="sxs-lookup"><span data-stu-id="b5bed-119">If you want hello device tooconsume all available bandwidth, set this field too**Unlimited**.</span></span> <span data-ttu-id="b5bed-120">Ayrıca, oluşturmak ve bant genişliği şablonu tooallocate bant zamanlamaya göre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5bed-120">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

<span data-ttu-id="b5bed-121">Merhaba aşağıdaki yordamlar nasıl toouse hello StorSimple açıklamaktadır **birim kapsayıcıları** ortak işlemleri aşağıdaki dikey toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="b5bed-121">hello following procedures explain how toouse hello StorSimple **Volume containers** blade toocomplete hello following common operations:</span></span>

* <span data-ttu-id="b5bed-122">Birim kapsayıcısı Ekle</span><span class="sxs-lookup"><span data-stu-id="b5bed-122">Add a volume container</span></span>
* <span data-ttu-id="b5bed-123">Birim kapsayıcısı değiştirme</span><span class="sxs-lookup"><span data-stu-id="b5bed-123">Modify a volume container</span></span>
* <span data-ttu-id="b5bed-124">Birim kapsayıcısı Sil</span><span class="sxs-lookup"><span data-stu-id="b5bed-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="b5bed-125">Birim kapsayıcısı Ekle</span><span class="sxs-lookup"><span data-stu-id="b5bed-125">Add a volume container</span></span>
<span data-ttu-id="b5bed-126">Aşağıdaki adımları tooadd birim kapsayıcısı hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b5bed-126">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="b5bed-127">Birim kapsayıcısı değiştirme</span><span class="sxs-lookup"><span data-stu-id="b5bed-127">Modify a volume container</span></span>
<span data-ttu-id="b5bed-128">Aşağıdaki adımları toomodify birim kapsayıcısı hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b5bed-128">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="b5bed-129">Birim kapsayıcısı Sil</span><span class="sxs-lookup"><span data-stu-id="b5bed-129">Delete a volume container</span></span>
<span data-ttu-id="b5bed-130">Birim kapsayıcısı içindeki birimi vardır.</span><span class="sxs-lookup"><span data-stu-id="b5bed-130">A volume container has volumes within it.</span></span> <span data-ttu-id="b5bed-131">Yalnızca kapsadığı tüm hello birimler ilk silindiğinde silinebilir.</span><span class="sxs-lookup"><span data-stu-id="b5bed-131">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="b5bed-132">Aşağıdaki adımları toodelete birim kapsayıcısı hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b5bed-132">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="b5bed-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b5bed-133">Next steps</span></span>
* <span data-ttu-id="b5bed-134">Daha fazla bilgi edinmek [StorSimple birimlerini yönetme](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="b5bed-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="b5bed-135">Daha fazla bilgi edinmek [StorSimple Cihazınızı hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="b5bed-135">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

