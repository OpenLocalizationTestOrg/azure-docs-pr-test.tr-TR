---
title: "Azure RemoteApp koleksiyonunuzun güncelleştirme | Microsoft Docs"
description: "Azure RemoteApp koleksiyonunuzun güncelleştirme konusunda bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 454d78445d6092aec9eaa383e4c50cf15195848c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="1d3a1-103">Azure RemoteApp koleksiyonunda güncelleştir</span><span class="sxs-lookup"><span data-stu-id="1d3a1-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1d3a1-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1d3a1-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1d3a1-106">Uygulamaları veya Azure RemoteApp koleksiyonunuzun görüntüde güncelleştirmek için gerektiğinde bir zaman kaçınılmaz olarak, gelen.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-106">There will come a time, inevitably, when you need to update the apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="1d3a1-107">Bir bulut veya karma koleksiyonunda Azure RemoteApp aboneliğiniz ile birlikte gelen görüntülerden birini kullanıyorsanız, tüm güncelleştirmeleri kolay tuttuğunuzda şekilde Azure RemoteApp tarafından kendisine ele alınır.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-107">If you are using one of the images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="1d3a1-108">Ancak, özel bir görüntü (sıfırdan yerleşik veya bizim görüntülerden birini değiştirerek oluşturulan) kullanıyorsanız, görüntü ve uygulamaların güncelliğini sorumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining the image and apps.</span></span> <span data-ttu-id="1d3a1-109">Görüntünüzü veya diğer uygulamalar içindeki güncellemeniz gerekiyorsa, görüntüyü yeni ve güncelleştirilmiş bir sürümünü oluşturur ve ardından mevcut koleksiyonunuzdaki bu yeni güncelleştirilmiş görüntünüzle değiştirin gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-109">If you need to update your image or any of the apps inside it, you need to create a new, updated version of the image, and then replace the existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="1d3a1-110">Bu nedenle, nasıl gittiğiniz koleksiyonunuzu güncelleştirme hakkında?</span><span class="sxs-lookup"><span data-stu-id="1d3a1-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="1d3a1-111">Bu oldukça basittir:</span><span class="sxs-lookup"><span data-stu-id="1d3a1-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="1d3a1-112">Koleksiyonda kullanılan görüntüyü güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-112">Update the image that you used in your collection.</span></span> <span data-ttu-id="1d3a1-113">Herhangi bir düzeltme ekleri veya gerekli güncelleştirmeleri uygulamak ve yeni bir adla kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="1d3a1-114">[Karşıya yükleme](remoteapp-uploadimage.md) veya [alma](remoteapp-image-on-azurevm.md) RemoteApp görüntüsünü.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image to RemoteApp.</span></span>
3. <span data-ttu-id="1d3a1-115">Şimdi, koleksiyon sayfasında, tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-115">Now, on the collection page, click **Update**.</span></span>
4. <span data-ttu-id="1d3a1-116">Yeni görüntüden seçin **şablon görüntüsü** listesi.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-116">Choose the new image from the **Template Image** list.</span></span>
5. <span data-ttu-id="1d3a1-117">Hassas bölümü İşte - koleksiyonda bir uygulama kullanmakta olduğunuz herhangi bir kullanıcının uğraşmanız nasıl karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-117">Here's the tricky part - you need to decide how to deal with any users that are currently using an app in the collection.</span></span> <span data-ttu-id="1d3a1-118">İçin şu seçenekleriniz vardır:</span><span class="sxs-lookup"><span data-stu-id="1d3a1-118">You have the following choices:</span></span>
   
   * <span data-ttu-id="1d3a1-119">**Kullanıcılara güncelleştirmeden sonra 60 dakika ver**.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-119">**Give users 60 minutes after the update**.</span></span> <span data-ttu-id="1d3a1-120">Güncelleştirme tamamlandıktan hemen sonra Azure RemoteApp çalışmalarını kaydetmeleri ve oturumu kapatın ve tekrar oturum açmak için onları belirten etkin hiçbir kullanıcı bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-120">As soon as the update is finished, Azure RemoteApp will display a message to any active users telling them to save their work and log off and log back in.</span></span> <span data-ttu-id="1d3a1-121">60 dakika sonra kapattınız olmayan herhangi bir etkin kullanıcılar otomatik olarak oturumunuz kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="1d3a1-122">Kullanıcılar hemen oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="1d3a1-123">**Kullanıcıların oturumunu hemen kapat**.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-123">**Sign users out immediately**.</span></span> <span data-ttu-id="1d3a1-124">Güncelleştirme tamamlandıktan hemen sonra herhangi bir uyarı olmadan otomatik olarak tüm kullanıcıların oturumunu.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-124">As soon as the update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="1d3a1-125">Bu seçeneği seçerseniz, kullanıcılar veri kaybedebilir.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="1d3a1-126">Ancak, bunlar uygulamaya hemen bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-126">However, they can reconnect to the app immediately.</span></span>
6. <span data-ttu-id="1d3a1-127">Güncelleştirmeyi başlatmak için onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1d3a1-127">Click the check mark to start the update.</span></span>

