---
title: "azure'da aaaCreate SharePoint server grupları | Microsoft Docs"
description: "Hızlı bir şekilde Azure'da hello Azure portal Market kullanarak yeni bir SharePoint 2013 veya SharePoint 2016 grubu oluşturun."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a><span data-ttu-id="44358-103">Azure portal Market Hello kullanarak SharePoint sunucu grupları oluşturma</span><span class="sxs-lookup"><span data-stu-id="44358-103">Create SharePoint server farms using hello Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="44358-104">SharePoint 2013 grupları</span><span class="sxs-lookup"><span data-stu-id="44358-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="44358-105">İle Merhaba Microsoft Azure portal Market, önceden yapılandırılmış SharePoint Server 2013 grupları kolayca oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44358-105">With hello Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="44358-106">Bu, çok zaman bir geliştirme ve test ortamı için bir temel veya yüksek kullanılabilirlik SharePoint grubu gerektiğinde veya, SharePoint Server 2013, kuruluşunuz için işbirliği çözüm olarak değerlendirmek kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44358-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="44358-107">Merhaba **SharePoint sunucu grubu** hello Azure portal hello Azure Market öğesi kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="44358-107">hello **SharePoint Server Farm** item in hello Azure Marketplace of hello Azure portal has been removed.</span></span> <span data-ttu-id="44358-108">Merhaba ile değiştirilen **SharePoint 2013 olmayan HA grubu** ve **SharePoint 2013 HA grubu** öğeleri.</span><span class="sxs-lookup"><span data-stu-id="44358-108">It has been replaced with hello **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="44358-109">Bu yapılandırmada üç sanal makinelerin Hello temel SharePoint grubu oluşur.</span><span class="sxs-lookup"><span data-stu-id="44358-109">hello basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="44358-111">Bu grubu yapılandırmasını SharePoint uygulama geliştirme için Basitleştirilmiş kurulumu veya ilk kez değerlendirmenize SharePoint 2013 için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44358-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="44358-112">toocreate hello temel (üç sunuculu) SharePoint grubu:</span><span class="sxs-lookup"><span data-stu-id="44358-112">toocreate hello basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="44358-113">Tıklatın [burada](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span><span class="sxs-lookup"><span data-stu-id="44358-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="44358-114">Tıklatın **dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="44358-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="44358-115">Merhaba üzerinde **SharePoint 2013 olmayan HA grubu** bölmesinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="44358-115">On hello **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="44358-116">Merhaba hello adımlarından ayarlarını belirtin **oluşturma SharePoint 2013 olmayan HA grubu** bölmesi ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="44358-116">Specify settings on hello steps of hello **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="44358-117">Bu yapılandırmada dokuz sanal makinelerin Hello yüksek kullanılabilirlik SharePoint grubu oluşur.</span><span class="sxs-lookup"><span data-stu-id="44358-117">hello high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="44358-119">Bir SharePoint grubu için bu grubu yapılandırma tootest daha yüksek istemci yüklerini, hello dış SharePoint sitesi yüksek kullanılabilirliğini ve SQL Server AlwaysOn Kullanılabilirlik gruplarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44358-119">You can use this farm configuration tootest higher client loads, high availability of hello external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="44358-120">Bu yapılandırma, bir yüksek kullanılabilirlik ortamında SharePoint uygulama geliştirme için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44358-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="44358-121">toocreate hello yüksek kullanılabilirlik (dokuz sunuculu) SharePoint grubu:</span><span class="sxs-lookup"><span data-stu-id="44358-121">toocreate hello high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="44358-122">Tıklatın [burada](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span><span class="sxs-lookup"><span data-stu-id="44358-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="44358-123">Tıklatın **dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="44358-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="44358-124">Merhaba üzerinde **SharePoint 2013 HA grubu** bölmesinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="44358-124">On hello **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="44358-125">Merhaba hello yedi adımlarından ayarlarını belirtin **oluşturma SharePoint 2013 HA grubu** bölmesi ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="44358-125">Specify settings on hello seven steps of hello **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="44358-126">Merhaba oluşturulamıyor **SharePoint 2013 olmayan HA grubu** veya **SharePoint 2013 HA grubu** Azure ücretsiz deneme sürümü ile.</span><span class="sxs-lookup"><span data-stu-id="44358-126">You cannot create hello **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="44358-127">Hello Azure portal bu grupları her ikisinin bir Internet'e yönelik web varlığı ile yalnızca bulut sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="44358-127">hello Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="44358-128">Siteden siteye VPN veya ExpressRoute bağlantı geri tooyour kuruluş ağ yok.</span><span class="sxs-lookup"><span data-stu-id="44358-128">There is no site-to-site VPN or ExpressRoute connection back tooyour organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="44358-129">Ne zaman hello temel oluşturun veya yüksek kullanılabilirlik SharePoint grupları hello Azure portal kullanarak, varolan bir kaynak grubu belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="44358-129">When you create hello basic or high-availability SharePoint farms using hello Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="44358-130">Bu sınırlamaya geçici toowork Azure PowerShell ile bu grupları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="44358-130">toowork around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="44358-131">Daha fazla bilgi için bkz: [oluşturma SharePoint 2013 geliştirme ve test grupları Azure PowerShell ile](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span><span class="sxs-lookup"><span data-stu-id="44358-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="44358-132">SharePoint 2016 grupları</span><span class="sxs-lookup"><span data-stu-id="44358-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="44358-133">Bkz: [bu makalede](https://technet.microsoft.com/library/mt723354.aspx) tek sunuculu SharePoint Server 2016 aşağıdaki hello yönergeleri toobuild Merhaba grubu.</span><span class="sxs-lookup"><span data-stu-id="44358-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for hello instructions toobuild hello following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a><span data-ttu-id="44358-135">Merhaba SharePoint grupları yönetme</span><span class="sxs-lookup"><span data-stu-id="44358-135">Managing hello SharePoint farms</span></span>
<span data-ttu-id="44358-136">Uzak Masaüstü bağlantıları üzerinden bu grupları hello sunucuları yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44358-136">You can administer hello servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="44358-137">Daha fazla bilgi için bkz: [toohello sanal makinede oturum](quick-create-portal.md#connect-to-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="44358-137">For more information, see [Log on toohello virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="44358-138">Merhaba Merkezi Yönetim SharePoint sitesinden Sitelerim, SharePoint uygulamaları ve diğer işlevleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44358-138">From hello Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="44358-139">Daha fazla bilgi için bkz: [SharePoint Yapılandırma](http://technet.microsoft.com/library/ee836142.aspx).</span><span class="sxs-lookup"><span data-stu-id="44358-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="44358-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="44358-140">Next steps</span></span>
* <span data-ttu-id="44358-141">Ek Bul [SharePoint yapılandırmaları](https://technet.microsoft.com/library/dn635309.aspx) Azure altyapı Hizmetleri'nde.</span><span class="sxs-lookup"><span data-stu-id="44358-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
