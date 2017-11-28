---
title: "StorSimple birim kapsayıcıları yönetme | Microsoft Docs"
description: "Ekleme, değiştirme ve bir birim kapsayıcısı silmek için StorSimple Yöneticisi hizmeti birim kapsayıcıları sayfası nasıl kullanabileceğiniz açıklanır."
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
ms.openlocfilehash: bb55a7a4bff0fd4319de6f6ce958686ad8a4142b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-storsimple-volume-containers"></a><span data-ttu-id="aac0f-103">StorSimple birim kapsayıcıları yönetmek için StorSimple Yöneticisi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="aac0f-103">Use the StorSimple Manager service to manage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="aac0f-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="aac0f-104">Overview</span></span>
<span data-ttu-id="aac0f-105">Bu öğretici oluşturmak ve StorSimple birim kapsayıcıları yönetmek için StorSimple Yöneticisi hizmetini kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="aac0f-105">This tutorial explains how to use the StorSimple Manager service to create and manage StorSimple volume containers.</span></span>

<span data-ttu-id="aac0f-106">Microsoft Azure StorSimple aygıtta bir birim kapsayıcısı depolama hesabı, şifreleme ve bant genişliği tüketimi ayarları paylaşan bir veya daha fazla birimleri içerir.</span><span class="sxs-lookup"><span data-stu-id="aac0f-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="aac0f-107">Bir aygıt tüm birimlerde için birden çok birim kapsayıcıları olabilir.</span><span class="sxs-lookup"><span data-stu-id="aac0f-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="aac0f-108">Birim kapsayıcısı aşağıdaki özniteliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="aac0f-108">A volume container has the following attributes:</span></span>

* <span data-ttu-id="aac0f-109">**Birimleri** – katmanlı veya birim kapsayıcı içinde bulunan StorSimple birimlerini'yerel olarak sabitlenmiş.</span><span class="sxs-lookup"><span data-stu-id="aac0f-109">**Volumes** – The tiered or locally pinned StorSimple volumes that are contained within the volume container.</span></span> <span data-ttu-id="aac0f-110">Birim kapsayıcısı en fazla 256 StorSimple birimlerini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="aac0f-110">A volume container may contain up to 256 StorSimple volumes.</span></span>
* <span data-ttu-id="aac0f-111">**Şifreleme** – her birim kapsayıcısı için tanımlanabilen bir şifreleme anahtarı.</span><span class="sxs-lookup"><span data-stu-id="aac0f-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="aac0f-112">Bu anahtar StorSimple Cihazınızı buluta gönderilen verileri şifrelemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aac0f-112">This key is used for encrypting the data that is sent from your StorSimple device to the cloud.</span></span> <span data-ttu-id="aac0f-113">Askeri düzeyde AES 256 bit anahtar kullanıcı tarafından girilen anahtarla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aac0f-113">A military-grade AES-256 bit key is used with the user-entered key.</span></span> <span data-ttu-id="aac0f-114">Verilerinizin güvenliğini sağlamak için bulut depolama şifreleme her zaman etkinleştirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="aac0f-114">To secure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="aac0f-115">**Depolama hesabı** – bulut depolama hizmet sağlayıcınıza bağlı depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="aac0f-115">**Storage account** – The storage account that is linked to your cloud storage service provider.</span></span> <span data-ttu-id="aac0f-116">Birim kapsayıcısı içinde bulunan tüm birimleri bu depolama hesabını paylaşır.</span><span class="sxs-lookup"><span data-stu-id="aac0f-116">All the volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="aac0f-117">Varolan bir listesinden bir depolama hesabını seçin veya birim kapsayıcısı oluşturduğunuzda ve bu hesaba erişim kimlik bilgilerini belirtin yeni bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aac0f-117">You can choose a storage account from an existing list, or create a new account when you create the volume container and then specify the access credentials for that account.</span></span>
* <span data-ttu-id="aac0f-118">**Bulut bant genişliği** – verileri CİHAZDAN buluta gönderildiğinde aygıt tarafından kullanılan bant genişliği.</span><span class="sxs-lookup"><span data-stu-id="aac0f-118">**Cloud bandwidth** – The bandwidth consumed by the device when the data from the device is being sent to the cloud.</span></span> <span data-ttu-id="aac0f-119">Bu kapsayıcı tanımlarken 1 ile 1000 MB/sn arasında bir değer belirterek bir bant genişliği denetimini uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aac0f-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="aac0f-120">Tüm kullanılabilir bant genişliği aygıta istiyorsanız, bu alan için sınırsız ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="aac0f-120">If you want the device to consume all available bandwidth, set this field to Unlimited.</span></span> <span data-ttu-id="aac0f-121">Ayrıca, oluşturma ve bant genişliği zamanlamaya göre ayırmak için bant genişliği şablonu uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aac0f-121">You can also create and apply a bandwidth template to allocate bandwidth based on schedule.</span></span>

![Birim kapsayıcıları sayfası](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="aac0f-123">Bu aşağıdaki yordamları StorSimple nasıl kullanacağınıza ilişkin **birim kapsayıcıları** sayfasını aşağıdaki ortak işlemleri tamamlamak için:</span><span class="sxs-lookup"><span data-stu-id="aac0f-123">This following procedures explain how to use the StorSimple **Volume containers** page to complete the following common operations:</span></span>

* <span data-ttu-id="aac0f-124">Birim kapsayıcısı Ekle</span><span class="sxs-lookup"><span data-stu-id="aac0f-124">Add a volume container</span></span> 
* <span data-ttu-id="aac0f-125">Birim kapsayıcısı değiştirme</span><span class="sxs-lookup"><span data-stu-id="aac0f-125">Modify a volume container</span></span> 
* <span data-ttu-id="aac0f-126">Birim kapsayıcısı Sil</span><span class="sxs-lookup"><span data-stu-id="aac0f-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="aac0f-127">Birim kapsayıcısı Ekle</span><span class="sxs-lookup"><span data-stu-id="aac0f-127">Add a volume container</span></span>
<span data-ttu-id="aac0f-128">Birim kapsayıcısı eklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="aac0f-128">Perform the following steps to add a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="aac0f-129">Birim kapsayıcısı değiştirme</span><span class="sxs-lookup"><span data-stu-id="aac0f-129">Modify a volume container</span></span>
<span data-ttu-id="aac0f-130">Birim kapsayıcısı değiştirmek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="aac0f-130">Perform the following steps to modify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="aac0f-131">Birim kapsayıcısı Sil</span><span class="sxs-lookup"><span data-stu-id="aac0f-131">Delete a volume container</span></span>
<span data-ttu-id="aac0f-132">Birim kapsayıcısı içindeki birimi vardır.</span><span class="sxs-lookup"><span data-stu-id="aac0f-132">A volume container has volumes within it.</span></span> <span data-ttu-id="aac0f-133">Yalnızca kapsadığı tüm birimler ilk silindiğinde silinebilir.</span><span class="sxs-lookup"><span data-stu-id="aac0f-133">It can be deleted only if all the volumes contained in it are first deleted.</span></span> <span data-ttu-id="aac0f-134">Birim kapsayıcısı silmek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="aac0f-134">Perform the following steps to delete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="aac0f-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aac0f-135">Next steps</span></span>
* <span data-ttu-id="aac0f-136">Daha fazla bilgi edinmek [StorSimple birimlerini yönetme](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="aac0f-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="aac0f-137">Daha fazla bilgi edinmek [StorSimple Cihazınızı yönetmek için StorSimple Yöneticisi hizmetini kullanma](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="aac0f-137">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

