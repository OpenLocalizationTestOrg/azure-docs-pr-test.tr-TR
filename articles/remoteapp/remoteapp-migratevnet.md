---
title: bir RemoteApp Koleksiyonunuzla tooan Azure VNET gelen aaaHow toomigrate | Microsoft Docs
description: "Bilgi nasıl RemoteApp Koleksiyonunuzla tooan Azure VNET gelen toomigrate"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a><span data-ttu-id="e3aa4-103">Nasıl toomigrate RemoteApp Koleksiyonunuzla tooan Azure VNET karma koleksiyonundan</span><span class="sxs-lookup"><span data-stu-id="e3aa4-103">How toomigrate a hybrid collection from a RemoteApp VNET tooan Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e3aa4-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e3aa4-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e3aa4-106">İyi haber!</span><span class="sxs-lookup"><span data-stu-id="e3aa4-106">Good news!</span></span> <span data-ttu-id="e3aa4-107">Biz, toodeploy karma RemoteApp RemoteApp özel sanal ağlar oluşturmak yerine doğrudan, mevcut Azure sanal ağlar (Vnet'ler) koleksiyonlara etkinleştirmiş olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-107">We have enabled you toodeploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="e3aa4-108">Bu, son VNET özelliklerine (örneğin, ExpressRoute) hello yararlanmak ve Azure Hizmetleri, karma koleksiyonlar doğrudan ağ erişim tooother verin sağlar ve toothat VNET dağıtılan sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-108">This lets you take advantage of hello latest VNET features (like ExpressRoute) and give your hybrid collections direct network access tooother Azure services and virtual machines deployed toothat VNET.</span></span>  <span data-ttu-id="e3aa4-109">(Bu, daha iyi performans ve VNET-VNET yapılandırmaları daha kolay kurulum alır).</span><span class="sxs-lookup"><span data-stu-id="e3aa4-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="e3aa4-110">Adlı karma RemoteApp koleksiyonu zaten oluşturduğunuzu düşünelim *OriginalCollection* bir RemoteApp sanal ağı ile adlı *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="e3aa4-111">Merhaba adımları toomigrate İşte bunu yeni Azure VNET adlı tooa *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-111">Here are hello steps toomigrate it tooa new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="e3aa4-112">Merhaba üzerinde **ağlar** hello sekmesinde [Yönetim Portalı](http://manage.windowsazure.com/), adlı bir VNET oluşturma *AzureVNET*kullanarak hello aynı konumda, DNS yapılandırması ve adres alanı (en az biri için Merhaba, *AzureVNET* alt ağlar) için kullanılan aynı *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-112">On hello **Networks** tab in hello [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using hello same location, DNS configuration, and address space (for at least one of hello *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="e3aa4-113">Yapılandırma *AzureVNET* tooeither konak veya ağ bağlantısı toohello Active Directory dağıtımınız varsa, *OriginalCollection* etki alanına katıldı.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-113">Configure *AzureVNET* tooeither host or have network connectivity toohello Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="e3aa4-114">Merhaba üzerinde **Remoteapps'leri** sekmesinde, adı verilen yeni bir RemoteApp koleksiyonu oluşturun *yeni koleksiyon*.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-114">On hello **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="e3aa4-115">(Kullanım hello **Create VNET ile** seçeneği değil, **hızlı Oluştur**.)</span><span class="sxs-lookup"><span data-stu-id="e3aa4-115">(Use hello **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="e3aa4-116">Yapılandırma *NewCollection* toobe tooa alt ağda dağıtılan *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-116">Configure *NewCollection* toobe deployed tooa subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="e3aa4-117">Yapılandırma *NewCollection* toouse hello aynı görüntü ve etki alanına katılım bilgileri için kullanılan aynı *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-117">Configure *NewCollection* toouse hello same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="e3aa4-118">Birkaç saat sonra *NewCollection* koleksiyonu listenize etkin duruma ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="e3aa4-119">Herhangi bir kullanıcı bilgisi koleksiyonundan hello özgün koleksiyonu toohello yeni toomigrate gerekmiyorsa, artık, ardından bu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="e3aa4-119">Now, if you DON’T need toomigrate any user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="e3aa4-120">Silme *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="e3aa4-121">Silme *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="e3aa4-122">Ve bitirdiniz!</span><span class="sxs-lookup"><span data-stu-id="e3aa4-122">And, you’re done!</span></span>

<span data-ttu-id="e3aa4-123">Merhaba özgün koleksiyonu toohello yeni koleksiyon toomigrate kullanıcı bilgilerini gerekiyorsa, alternatif olarak, ardından bu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="e3aa4-123">Alternately, if you DO need toomigrate user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="e3aa4-124">Bir e-posta çok gönderme[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) Azure abonelik Kimliğinizi ile Merhaba, özgün koleksiyonun adını ve yeni koleksiyonunuzu hello adını ve toomigrate isteyin kullanıcı bilgilerinizi.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-124">Send an email too[remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, hello name of your original collection, and hello name of your new collection, and ask them toomigrate your user information.</span></span>
2. <span data-ttu-id="e3aa4-125">2 iş günü içinde hello RemoteApp ekibi hello kullanıcı erişim listesi ve tüm kullanıcı belgeleri ve kullanıcı ayarlarını hello özgün koleksiyonu toohello yeni koleksiyondan taşınır.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-125">Within 2 business days hello RemoteApp team will move hello user access list and all user documents and user settings from hello original collection toohello new collection.</span></span>
3. <span data-ttu-id="e3aa4-126">Silme *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="e3aa4-127">Silme *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="e3aa4-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="e3aa4-128">Ve şimdi bitirdiniz!</span><span class="sxs-lookup"><span data-stu-id="e3aa4-128">And now, you’re done!</span></span>

<span data-ttu-id="e3aa4-129">Sorularınız veya özel Yardım gerekirse, lütfen e-posta [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="e3aa4-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

