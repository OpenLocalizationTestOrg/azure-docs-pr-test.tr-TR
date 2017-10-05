---
title: "Azure Active Directory etki alanı Hizmetleri: Başlarken | Microsoft Docs"
description: "Azure Active Directory etki alanı (Önizleme) Azure portalını kullanarak Hizmetleri etkinleştir"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 47507096a6245d4f1ba57a652ddf5167b3776ae9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="b6a9f-103">Azure Active Directory etki alanı (Önizleme) Azure portalını kullanarak Hizmetleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b6a9f-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>
<span data-ttu-id="b6a9f-104">Bu makalede, Azure Active Directory etki alanı Azure portalını kullanarak hizmetlerin (Azure AD DS) nasıl etkinleştirileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-104">This article shows how to enable Azure Active Directory Domain Services (Azure AD DS) using the Azure portal.</span></span>


<span data-ttu-id="b6a9f-105">Başlatmak için **etkinleştirmek Azure AD etki alanı Hizmetleri** Sihirbazı, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="b6a9f-105">To launch the **Enable Azure AD Domain Services** wizard, complete the following steps:</span></span>

1. <span data-ttu-id="b6a9f-106">[Azure Portal](https://portal.azure.com) gidin.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-106">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b6a9f-107">Sol bölmede tıklayın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-107">In the left pane, click on **New**.</span></span>
3. <span data-ttu-id="b6a9f-108">İçinde **yeni** dikey penceresinde, türü **etki alanı Hizmetleri** arama çubuğunu içine.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-108">In the **New** blade, type **Domain Services** into the search bar.</span></span>

    ![Etki Alanı Hizmetleri için arama](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="b6a9f-110">Seçmek için tıklatın **Azure AD etki alanı Hizmetleri** arama önerileri listesinden.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-110">Click to select **Azure AD Domain Services** from the list of search suggestions.</span></span> <span data-ttu-id="b6a9f-111">Üzerinde **Azure AD etki alanı Hizmetleri** dikey penceresinde tıklatın **oluşturma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-111">On the **Azure AD Domain Services** blade, click the **Create** button.</span></span>

    ![Etki Alanı Hizmetleri dikey penceresini](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="b6a9f-113">**Etkinleştirmek Azure AD etki alanı Hizmetleri** Sihirbazı başlatıldığında.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-113">The **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="b6a9f-114">Görev 1: temel ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6a9f-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="b6a9f-115">İçinde **Temelleri** Sayfa Sihirbazı'nın, yönetilen etki alanı için DNS etki alanı adı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-115">In the **Basics** page of the wizard, you can specify the DNS domain name for the managed domain.</span></span> <span data-ttu-id="b6a9f-116">Ayrıca, yönetilen etki alanı dağıtılmalıdır Azure konumu ve kaynak grubu seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-116">You can also choose the resource group and Azure location to which the managed domain should be deployed.</span></span>

![Temel yapılandırma](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="b6a9f-118">Seçin **DNS etki alanı adı** yönetilen etki alanınız için.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-118">Choose the **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="b6a9f-119">Dizinin varsayılan etki alanı adını (ile bir **. onmicrosoft.com** soneki) varsayılan olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-119">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="b6a9f-120">Ayrıca, bir özel etki alanı adını yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="b6a9f-121">Bu örnekte özel etki alanı adı *contoso100.com* şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-121">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="b6a9f-122">Belirttiğiniz etki alanı adının ön eki (örneğin, *contoso100.com* etki alanı adında *contoso100*) 15 veya daha az karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-122">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="b6a9f-123">15 karakterden daha uzun bir önek ile yönetilen bir etki alanı oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="b6a9f-124">Yönetilen etki alanı için seçtiğiniz DNS etki alanı adının sanal ağda zaten bulunmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-124">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="b6a9f-125">Özellikle, denetleme olup olmadığını:</span><span class="sxs-lookup"><span data-stu-id="b6a9f-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="b6a9f-126">Sanal ağda aynı DNS etki alanı adına sahip bir etki alanınız zaten varsa.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-126">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="b6a9f-127">Yönetilen etki alanını etkinleştirmek planladığınız sanal ağ ile şirket içi ağınıza bir VPN bağlantısı vardır.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-127">The virtual network where you plan to enable the managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="b6a9f-128">Bu senaryoda, şirket içi ağınızda aynı DNS etki alanı adına sahip bir etki alanı olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-128">In this scenario, ensure you don't have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="b6a9f-129">Sanal ağda bu ada sahip bir bulut hizmetiniz zaten varsa.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-129">You have an existing cloud service with that name on the virtual network.</span></span>

3. <span data-ttu-id="b6a9f-130">Seçin **sanal ağ türü**.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-130">Choose the **type of virtual network**.</span></span> <span data-ttu-id="b6a9f-131">Varsayılan olarak, **Resource Manager** sanal ağ türü seçilidir.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-131">By default, the **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="b6a9f-132">Bu sanal ağ türü yönetilen etki alanları yeni oluşturulan tüm kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="b6a9f-133">Azure seçin **abonelik** , yönetilen etki alanı oluşturmak istediğinizi içinde.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-133">Select the Azure **Subscription** in which you would like to create the managed domain.</span></span>

5. <span data-ttu-id="b6a9f-134">Seçin **kaynak grubu** için yönetilen etki alanına ait olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-134">Select the **Resource group** to which the managed domain should belong.</span></span> <span data-ttu-id="b6a9f-135">Ya da seçebilirsiniz **Yeni Oluştur** veya **var olanı kullan** seçenekleri kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-135">You can choose either the **Create new** or **Use existing** options to select the resource group.</span></span>

6. <span data-ttu-id="b6a9f-136">Azure seçin **konumu** , yönetilen etki alanında oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-136">Choose the Azure **Location** in which the managed domain should be created.</span></span> <span data-ttu-id="b6a9f-137">Üzerinde **ağ** sayfasında sihirbazın, seçtiğiniz konuma ait yalnızca sanal ağlar görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-137">On the **Network** page of the wizard, you see only virtual networks that belong to the location you have selected.</span></span>

7. <span data-ttu-id="b6a9f-138">İşiniz bittiğinde tıklatın **Tamam** üzerinde taşımayı **ağ** Sihirbazı sayfası.</span><span class="sxs-lookup"><span data-stu-id="b6a9f-138">When you are done, click **OK** to move on to the **Network** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="b6a9f-139">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="b6a9f-139">Next step</span></span>
[<span data-ttu-id="b6a9f-140">2. Görev: Ağ ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6a9f-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
