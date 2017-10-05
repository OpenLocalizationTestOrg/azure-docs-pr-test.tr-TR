---
title: "StorSimple 8000 serisi cihazda, StorSimple birim kapsayıcıları yönetme | Microsoft Docs"
description: "Ekleme, değiştirme ve bir birim kapsayıcısı silmek için StorSimple cihaz Yöneticisi hizmeti birim kapsayıcıları sayfası nasıl kullanabileceğiniz açıklanır."
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
ms.openlocfilehash: 0f8e00d6d07224f56625482f339e612e68914be2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-storsimple-volume-containers"></a><span data-ttu-id="8962b-103">StorSimple birim kapsayıcıları yönetmek için StorSimple cihaz Yöneticisi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="8962b-103">Use the StorSimple Device Manager service to manage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="8962b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8962b-104">Overview</span></span>
<span data-ttu-id="8962b-105">Bu öğretici StorSimple cihaz Yöneticisi hizmeti oluşturmak ve StorSimple birim kapsayıcıları yönetmek için nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="8962b-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage StorSimple volume containers.</span></span>

<span data-ttu-id="8962b-106">Microsoft Azure StorSimple aygıtta bir birim kapsayıcısı depolama hesabı, şifreleme ve bant genişliği tüketimi ayarları paylaşan bir veya daha fazla birimleri içerir.</span><span class="sxs-lookup"><span data-stu-id="8962b-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="8962b-107">Bir aygıt tüm birimlerde için birden çok birim kapsayıcıları olabilir.</span><span class="sxs-lookup"><span data-stu-id="8962b-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="8962b-108">Birim kapsayıcısı aşağıdaki özniteliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="8962b-108">A volume container has the following attributes:</span></span>

* <span data-ttu-id="8962b-109">**Birimleri** – katmanlı veya birim kapsayıcı içinde bulunan StorSimple birimlerini'yerel olarak sabitlenmiş.</span><span class="sxs-lookup"><span data-stu-id="8962b-109">**Volumes** – The tiered or locally pinned StorSimple volumes that are contained within the volume container.</span></span> 
* <span data-ttu-id="8962b-110">**Şifreleme** – her birim kapsayıcısı için tanımlanabilen bir şifreleme anahtarı.</span><span class="sxs-lookup"><span data-stu-id="8962b-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="8962b-111">Bu anahtar StorSimple Cihazınızı buluta gönderilen verileri şifrelemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8962b-111">This key is used for encrypting the data that is sent from your StorSimple device to the cloud.</span></span> <span data-ttu-id="8962b-112">Askeri düzeyde AES 256 bit anahtar kullanıcı tarafından girilen anahtarla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8962b-112">A military-grade AES-256 bit key is used with the user-entered key.</span></span> <span data-ttu-id="8962b-113">Verilerinizin güvenliğini sağlamak için bulut depolama şifreleme her zaman etkinleştirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="8962b-113">To secure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="8962b-114">**Depolama hesabı** – verilerini depolamak için kullanılan Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="8962b-114">**Storage account** – The Azure storage account that is used to store the data.</span></span> <span data-ttu-id="8962b-115">Birim kapsayıcısı içinde bulunan tüm birimleri bu depolama hesabını paylaşır.</span><span class="sxs-lookup"><span data-stu-id="8962b-115">All the volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="8962b-116">Varolan bir listesinden bir depolama hesabını seçin veya birim kapsayıcısı oluşturduğunuzda ve bu hesaba erişim kimlik bilgilerini belirtin yeni bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8962b-116">You can choose a storage account from an existing list, or create a new account when you create the volume container and then specify the access credentials for that account.</span></span>
* <span data-ttu-id="8962b-117">**Bulut bant genişliği** – verileri CİHAZDAN buluta gönderildiğinde aygıt tarafından kullanılan bant genişliği.</span><span class="sxs-lookup"><span data-stu-id="8962b-117">**Cloud bandwidth** – The bandwidth consumed by the device when the data from the device is being sent to the cloud.</span></span> <span data-ttu-id="8962b-118">Bu kapsayıcı oluşturduğunuzda, 1 MB/sn ile 1000 MB/sn arasında bir değer belirterek bant genişliği denetimini uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8962b-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="8962b-119">Kullanılabilir tüm bant genişliği aygıta istiyorsanız, bu alan kümesi'ne **sınırsız**.</span><span class="sxs-lookup"><span data-stu-id="8962b-119">If you want the device to consume all available bandwidth, set this field to **Unlimited**.</span></span> <span data-ttu-id="8962b-120">Ayrıca, oluşturma ve bant genişliği zamanlamaya göre ayırmak için bant genişliği şablonu uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8962b-120">You can also create and apply a bandwidth template to allocate bandwidth based on schedule.</span></span>

<span data-ttu-id="8962b-121">Aşağıdaki yordamlar StorSimple nasıl kullanacağınıza ilişkin **birim kapsayıcıları** dikey aşağıdaki ortak işlemleri tamamlamak için:</span><span class="sxs-lookup"><span data-stu-id="8962b-121">The following procedures explain how to use the StorSimple **Volume containers** blade to complete the following common operations:</span></span>

* <span data-ttu-id="8962b-122">Birim kapsayıcısı Ekle</span><span class="sxs-lookup"><span data-stu-id="8962b-122">Add a volume container</span></span>
* <span data-ttu-id="8962b-123">Birim kapsayıcısı değiştirme</span><span class="sxs-lookup"><span data-stu-id="8962b-123">Modify a volume container</span></span>
* <span data-ttu-id="8962b-124">Birim kapsayıcısı Sil</span><span class="sxs-lookup"><span data-stu-id="8962b-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="8962b-125">Birim kapsayıcısı Ekle</span><span class="sxs-lookup"><span data-stu-id="8962b-125">Add a volume container</span></span>
<span data-ttu-id="8962b-126">Birim kapsayıcısı eklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8962b-126">Perform the following steps to add a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="8962b-127">Birim kapsayıcısı değiştirme</span><span class="sxs-lookup"><span data-stu-id="8962b-127">Modify a volume container</span></span>
<span data-ttu-id="8962b-128">Birim kapsayıcısı değiştirmek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8962b-128">Perform the following steps to modify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="8962b-129">Birim kapsayıcısı Sil</span><span class="sxs-lookup"><span data-stu-id="8962b-129">Delete a volume container</span></span>
<span data-ttu-id="8962b-130">Birim kapsayıcısı içindeki birimi vardır.</span><span class="sxs-lookup"><span data-stu-id="8962b-130">A volume container has volumes within it.</span></span> <span data-ttu-id="8962b-131">Yalnızca kapsadığı tüm birimler ilk silindiğinde silinebilir.</span><span class="sxs-lookup"><span data-stu-id="8962b-131">It can be deleted only if all the volumes contained in it are first deleted.</span></span> <span data-ttu-id="8962b-132">Birim kapsayıcısı silmek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8962b-132">Perform the following steps to delete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="8962b-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8962b-133">Next steps</span></span>
* <span data-ttu-id="8962b-134">Daha fazla bilgi edinmek [StorSimple birimlerini yönetme](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="8962b-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="8962b-135">Daha fazla bilgi edinmek [StorSimple Cihazınızı yönetmek için StorSimple cihaz Yöneticisi hizmetini kullanarak](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="8962b-135">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

