---
title: "Bir RemoteApp sanal ağdan bir Azure sanal ağına geçiş yapma | Microsoft Docs"
description: "Bir RemoteApp sanal ağdan bir Azure sanal ağına geçiş hakkında bilgi edinin"
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
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a><span data-ttu-id="a4198-103">Karma koleksiyon için bir Azure sanal bir RemoteApp sanal ağdan geçirme</span><span class="sxs-lookup"><span data-stu-id="a4198-103">How to migrate a hybrid collection from a RemoteApp VNET to an Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a4198-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="a4198-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a4198-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="a4198-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a4198-106">İyi haber!</span><span class="sxs-lookup"><span data-stu-id="a4198-106">Good news!</span></span> <span data-ttu-id="a4198-107">Karma RemoteApp koleksiyonları RemoteApp özel sanal ağlar oluşturmak yerine doğrudan, mevcut Azure sanal ağlar (Vnet'ler) halinde dağıtmak etkin.</span><span class="sxs-lookup"><span data-stu-id="a4198-107">We have enabled you to deploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="a4198-108">Bu, (örneğin, ExpressRoute) en son VNET özelliklerden yararlanmak ve karma koleksiyonlarınızı doğrudan ağ diğer Azure Hizmetleri ve bu VNET'e dağıtılan sanal makineleri erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4198-108">This lets you take advantage of the latest VNET features (like ExpressRoute) and give your hybrid collections direct network access to other Azure services and virtual machines deployed to that VNET.</span></span>  <span data-ttu-id="a4198-109">(Bu, daha iyi performans ve VNET-VNET yapılandırmaları daha kolay kurulum alır).</span><span class="sxs-lookup"><span data-stu-id="a4198-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="a4198-110">Adlı karma RemoteApp koleksiyonu zaten oluşturduğunuzu düşünelim *OriginalCollection* bir RemoteApp sanal ağı ile adlı *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="a4198-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="a4198-111">Adlı yeni Azure VNET için geçirmek için adımlar şunlardır *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="a4198-111">Here are the steps to migrate it to a new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="a4198-112">Üzerinde **ağlar** sekmesinde [Yönetim Portalı](http://manage.windowsazure.com/), adlı bir VNET oluşturma *AzureVNET*kullanarak aynı konum, DNS yapılandırması ve adres alanı (en az biri için *AzureVNET* alt ağlar) için kullanılan aynı *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="a4198-112">On the **Networks** tab in the [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using the same location, DNS configuration, and address space (for at least one of the *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="a4198-113">Yapılandırma *AzureVNET* ana bilgisayar veya Active Directory dağıtımı için bir ağ bağlantınız için *OriginalCollection* etki alanına katıldı.</span><span class="sxs-lookup"><span data-stu-id="a4198-113">Configure *AzureVNET* to either host or have network connectivity to the Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="a4198-114">Üzerinde **Remoteapps'leri** sekmesinde, adı verilen yeni bir RemoteApp koleksiyonu oluşturun *yeni koleksiyon*.</span><span class="sxs-lookup"><span data-stu-id="a4198-114">On the **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="a4198-115">(Kullanım **Create VNET ile** seçeneği değil, **hızlı Oluştur**.)</span><span class="sxs-lookup"><span data-stu-id="a4198-115">(Use the **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="a4198-116">Yapılandırma *NewCollection* bir alt ağda dağıtmak üzere *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="a4198-116">Configure *NewCollection* to be deployed to a subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="a4198-117">Yapılandırma *NewCollection* için kullanılan aynı etki alanına katılım bilgileri ve aynı görüntü kullanılacak *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="a4198-117">Configure *NewCollection* to use the same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="a4198-118">Birkaç saat sonra *NewCollection* koleksiyonu listenize etkin duruma ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a4198-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="a4198-119">Herhangi bir kullanıcı bilgisi özgün koleksiyondan yeni koleksiyon geçişi gerekmiyorsa, artık, ardından bu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="a4198-119">Now, if you DON’T need to migrate any user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="a4198-120">Silme *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="a4198-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="a4198-121">Silme *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="a4198-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="a4198-122">Ve bitirdiniz!</span><span class="sxs-lookup"><span data-stu-id="a4198-122">And, you’re done!</span></span>

<span data-ttu-id="a4198-123">Kullanıcı bilgilerini özgün koleksiyondan yeni koleksiyon geçişi gerekiyorsa, alternatif olarak, ardından bu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="a4198-123">Alternately, if you DO need to migrate user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="a4198-124">E-posta Gönder [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) Azure abonelik Kimliğinizi, özgün koleksiyonun adını ve yeni koleksiyonunuzu adını ve kullanıcı bilgilerinizi geçirmek isteyin.</span><span class="sxs-lookup"><span data-stu-id="a4198-124">Send an email to [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, the name of your original collection, and the name of your new collection, and ask them to migrate your user information.</span></span>
2. <span data-ttu-id="a4198-125">2 iş günü içinde yeni koleksiyon, özgün koleksiyondan RemoteApp ekibi kullanıcı erişim listesi ve tüm kullanıcı belgeleri ve kullanıcı ayarlarını taşınır.</span><span class="sxs-lookup"><span data-stu-id="a4198-125">Within 2 business days the RemoteApp team will move the user access list and all user documents and user settings from the original collection to the new collection.</span></span>
3. <span data-ttu-id="a4198-126">Silme *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="a4198-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="a4198-127">Silme *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="a4198-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="a4198-128">Ve şimdi bitirdiniz!</span><span class="sxs-lookup"><span data-stu-id="a4198-128">And now, you’re done!</span></span>

<span data-ttu-id="a4198-129">Sorularınız veya özel Yardım gerekirse, lütfen e-posta [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="a4198-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

