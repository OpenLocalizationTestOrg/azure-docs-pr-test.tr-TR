---
title: "Azure Active Directory etki alanı Hizmetleri: Başlarken | Microsoft Docs"
description: "Azure Active Directory etki alanı hello Azure portal (Önizleme) kullanarak Hizmetleri etkinleştir"
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
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="bbff3-103">Azure Active Directory etki alanı hello Azure portal (Önizleme) kullanarak Hizmetleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="bbff3-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>
<span data-ttu-id="bbff3-104">Bu makalede, Azure portal tooenable Azure Active Directory etki alanı kullanarak Hizmetleri (Azure AD DS) nasıl hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bbff3-104">This article shows how tooenable Azure Active Directory Domain Services (Azure AD DS) using hello Azure portal.</span></span>


<span data-ttu-id="bbff3-105">toolaunch hello **etkinleştirmek Azure AD etki alanı Hizmetleri** aşağıdaki adımları sihirbazında, tam hello:</span><span class="sxs-lookup"><span data-stu-id="bbff3-105">toolaunch hello **Enable Azure AD Domain Services** wizard, complete hello following steps:</span></span>

1. <span data-ttu-id="bbff3-106">Toohello Git [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bbff3-106">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bbff3-107">Merhaba sol bölmede tıklayın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="bbff3-107">In hello left pane, click on **New**.</span></span>
3. <span data-ttu-id="bbff3-108">Merhaba, **yeni** dikey penceresinde, türü **etki alanı Hizmetleri** hello arama çubuğunu içine.</span><span class="sxs-lookup"><span data-stu-id="bbff3-108">In hello **New** blade, type **Domain Services** into hello search bar.</span></span>

    ![Etki Alanı Hizmetleri için arama](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="bbff3-110">Tooselect tıklatın **Azure AD etki alanı Hizmetleri** arama önerileri hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="bbff3-110">Click tooselect **Azure AD Domain Services** from hello list of search suggestions.</span></span> <span data-ttu-id="bbff3-111">Merhaba üzerinde **Azure AD etki alanı Hizmetleri** dikey penceresinde hello tıklatın **oluşturma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bbff3-111">On hello **Azure AD Domain Services** blade, click hello **Create** button.</span></span>

    ![Etki Alanı Hizmetleri dikey penceresini](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="bbff3-113">Merhaba **etkinleştirmek Azure AD etki alanı Hizmetleri** Sihirbazı başlatıldığında.</span><span class="sxs-lookup"><span data-stu-id="bbff3-113">hello **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="bbff3-114">Görev 1: temel ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bbff3-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="bbff3-115">Merhaba, **Temelleri** sayfa hello Sihirbazı'nın hello yönetilen etki alanı için hello DNS etki alanı adı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bbff3-115">In hello **Basics** page of hello wizard, you can specify hello DNS domain name for hello managed domain.</span></span> <span data-ttu-id="bbff3-116">Merhaba kaynak grubunu da seçebilirsiniz ve Azure konumu toowhich hello yönetilen etki alanı dağıtılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bbff3-116">You can also choose hello resource group and Azure location toowhich hello managed domain should be deployed.</span></span>

![Temel yapılandırma](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="bbff3-118">Merhaba seçin **DNS etki alanı adı** yönetilen etki alanınız için.</span><span class="sxs-lookup"><span data-stu-id="bbff3-118">Choose hello **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="bbff3-119">Merhaba dizinin Hello varsayılan etki alanı adı (ile bir **. onmicrosoft.com** soneki) varsayılan olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="bbff3-119">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="bbff3-120">Ayrıca, bir özel etki alanı adını yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bbff3-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="bbff3-121">Bu örnekte, hello özel etki alanı adıdır *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="bbff3-121">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="bbff3-122">Belirtilen etki alanı adınızı Hello önek (örneğin, *contoso100* hello içinde *contoso100.com* etki alanı adı) 15 veya daha az karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="bbff3-122">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="bbff3-123">15 karakterden daha uzun bir önek ile yönetilen bir etki alanı oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="bbff3-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="bbff3-124">Etki alanı zaten hello sanal ağında yok, yönetilen hello için seçtiğiniz bu hello DNS etki alanı adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="bbff3-124">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="bbff3-125">Özellikle, denetleme olup olmadığını:</span><span class="sxs-lookup"><span data-stu-id="bbff3-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="bbff3-126">Merhaba sahip bir etki alanı zaten hello sanal ağda aynı DNS etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="bbff3-126">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="bbff3-127">Burada tooenable hello yönetilen etki alanı planlama hello sanal ağ ile şirket içi ağınıza bir VPN bağlantısı vardır.</span><span class="sxs-lookup"><span data-stu-id="bbff3-127">hello virtual network where you plan tooenable hello managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="bbff3-128">Bu senaryoda, yok hello olan bir etki alanında olduğundan emin olun, şirket içi ağınızda aynı DNS etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="bbff3-128">In this scenario, ensure you don't have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="bbff3-129">Bu ada sahip olan bir bulut hizmetini hello sanal ağda bulunan.</span><span class="sxs-lookup"><span data-stu-id="bbff3-129">You have an existing cloud service with that name on hello virtual network.</span></span>

3. <span data-ttu-id="bbff3-130">Merhaba seçin **sanal ağ türü**.</span><span class="sxs-lookup"><span data-stu-id="bbff3-130">Choose hello **type of virtual network**.</span></span> <span data-ttu-id="bbff3-131">Varsayılan olarak, hello **Resource Manager** sanal ağ türü seçilidir.</span><span class="sxs-lookup"><span data-stu-id="bbff3-131">By default, hello **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="bbff3-132">Bu sanal ağ türü yönetilen etki alanları yeni oluşturulan tüm kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="bbff3-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="bbff3-133">Select hello Azure **abonelik** toocreate hello yönetilen etki alanı içinde istediğinizi.</span><span class="sxs-lookup"><span data-stu-id="bbff3-133">Select hello Azure **Subscription** in which you would like toocreate hello managed domain.</span></span>

5. <span data-ttu-id="bbff3-134">Select hello **kaynak grubu** toowhich hello yönetilen etki alanına ait olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bbff3-134">Select hello **Resource group** toowhich hello managed domain should belong.</span></span> <span data-ttu-id="bbff3-135">Her iki hello seçebilirsiniz **Yeni Oluştur** veya **var olanı kullan** seçenekleri tooselect hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="bbff3-135">You can choose either hello **Create new** or **Use existing** options tooselect hello resource group.</span></span>

6. <span data-ttu-id="bbff3-136">Hello Azure'ı seçin **konumu** hangi hello yönetilen etki alanı oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bbff3-136">Choose hello Azure **Location** in which hello managed domain should be created.</span></span> <span data-ttu-id="bbff3-137">Merhaba üzerinde **ağ** sayfa hello Sihirbazı'nın, seçtiğiniz toohello konumu ait yalnızca sanal ağlar görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="bbff3-137">On hello **Network** page of hello wizard, you see only virtual networks that belong toohello location you have selected.</span></span>

7. <span data-ttu-id="bbff3-138">İşiniz bittiğinde tıklatın **Tamam** toohello üzerinde toomove **ağ** hello sihirbazın sayfası.</span><span class="sxs-lookup"><span data-stu-id="bbff3-138">When you are done, click **OK** toomove on toohello **Network** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="bbff3-139">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="bbff3-139">Next step</span></span>
[<span data-ttu-id="bbff3-140">2. Görev: Ağ ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bbff3-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
