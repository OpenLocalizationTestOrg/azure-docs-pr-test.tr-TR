---
title: "Azure Active Directory Domain Services: Azure Active Directory Domain Services’ı etkinleştirme | Microsoft Docs"
description: "Azure Active Directory etki alanı hello Klasik Azure portalı kullanarak Hizmetleri etkinleştir"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="99c82-103">Azure Active Directory etki alanı hello Klasik Azure portalı kullanarak Hizmetleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="99c82-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="99c82-104">Görev 3: Azure Active Directory Domain Services'i etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="99c82-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="99c82-105">Bu görevde, aşağıdaki adımları hello yaparak dizininiz için Azure Active Directory etki alanı Hizmetleri (Azure AD DS) etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="99c82-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing hello following steps:</span></span>

1. <span data-ttu-id="99c82-106">Toohello Git [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="99c82-106">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="99c82-107">Merhaba Hello sol bölmesinde seçin **Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="99c82-107">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="99c82-108">Azure AD DS tooenable istediğiniz hello Azure Active Directory (Azure AD) kiracısını (dizin) seçin.</span><span class="sxs-lookup"><span data-stu-id="99c82-108">Select hello Azure Active Directory (Azure AD) tenant (directory) for which you want tooenable Azure AD DS.</span></span>

    ![Azure AD Dizini Seçme](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="99c82-110">Merhaba üzerinde **Önizleme dizin** hello sayfasında, **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="99c82-110">On hello **preview directory** page, click hello **Configure** tab.</span></span>

    ![Dizinin yapılandır sekmesi](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="99c82-112">Altında **etki alanı Hizmetleri**, hello değiştirme **bu dizin için etki alanı Hizmetleri'ni etkinleştirme** çok seçenek**Evet**.</span><span class="sxs-lookup"><span data-stu-id="99c82-112">Under **domain services**, change hello **Enable domain services for this directory** option too**Yes**.</span></span>  
    <span data-ttu-id="99c82-113">Ek Azure Active Directory etki alanı Hizmetleri yapılandırma seçenekleri hello sayfasında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="99c82-113">Additional Azure Active Directory Domain Services configuration options appear on hello page.</span></span>

    ![Etki Alanı Hizmetlerini Etkinleştirme](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="99c82-115">Azure Active Directory etki alanı Hizmetleri kiracınız için etkinleştirdiğinizde, Azure AD oluşturur ve kullanıcıların kimliğini doğrulamak için gerekli olan hello Kerberos ve NTLM kimlik bilgisi karmalarını depolar.</span><span class="sxs-lookup"><span data-stu-id="99c82-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores hello Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="99c82-116">Merhaba belirtin **DNS etki alanı adı, etki alanı Hizmetleri'nin**.</span><span class="sxs-lookup"><span data-stu-id="99c82-116">Specify hello **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="99c82-117">Merhaba dizinin Hello varsayılan etki alanı adı (ile bir **. onmicrosoft.com** soneki) varsayılan olarak seçilidir.</span><span class="sxs-lookup"><span data-stu-id="99c82-117">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="99c82-118">Merhaba liste Azure AD dizininiz için yapılandırılan tüm etki alanlarını içerir, her ikisi de dahil olmak üzere doğrulandı ve doğrulanmamış hello üzerinde yapılandırdığınız etki alanları **etki alanları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="99c82-118">hello list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on hello **Domains** tab.</span></span>

   * <span data-ttu-id="99c82-119">Özel bir etki alanı adı da girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99c82-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="99c82-120">Bu örnekte, hello özel etki alanı adıdır *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="99c82-120">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="99c82-121">Belirtilen etki alanı adınızı Hello önek (örneğin, *contoso100* hello içinde *contoso100.com* etki alanı adı) 15 veya daha az karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="99c82-121">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="99c82-122">15 karakterden uzun bir ön ek ile Azure Active Directory Domain Services etki alanı oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="99c82-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="99c82-123">Etki alanı zaten hello sanal ağında yok, yönetilen hello için seçtiğiniz bu hello DNS etki alanı adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="99c82-123">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="99c82-124">Özellikle, toosee olup olmadığını kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="99c82-124">Specifically, check toosee whether:</span></span>

   * <span data-ttu-id="99c82-125">Merhaba sahip bir etki alanı zaten hello sanal ağda aynı DNS etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="99c82-125">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="99c82-126">Merhaba seçtiğiniz sanal ağ varsa ile şirket içi ağınıza bir VPN bağlantısı ve bir etki alanı hello ile şirket içi ağınızda aynı DNS etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="99c82-126">hello virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="99c82-127">Bu ada sahip olan bir bulut hizmetini hello sanal ağda bulunan.</span><span class="sxs-lookup"><span data-stu-id="99c82-127">You have an existing cloud service with that name on hello virtual network.</span></span>
8. <span data-ttu-id="99c82-128">Azure Active Directory etki alanı Hizmetleri toobe kullanılabilir istediğiniz bir sanal ağı seçin.</span><span class="sxs-lookup"><span data-stu-id="99c82-128">Select a virtual network on which you want Azure Active Directory Domain Services toobe available.</span></span> <span data-ttu-id="99c82-129">Merhaba sanal ağ ve hello oluşturduğunuz ayrılmış bir alt ağ seçin **Bağlan etki alanı Hizmetleri toothis sanal ağ** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="99c82-129">Select hello virtual network and dedicated subnet you created in hello **Connect domain services toothis virtual network** drop-down list.</span></span> <span data-ttu-id="99c82-130">Ayrıca hello aşağıdakileri dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="99c82-130">Also consider hello following:</span></span>

   * <span data-ttu-id="99c82-131">Belirttiğiniz hello sanal ağının tooan Azure Active Directory etki alanı Hizmetleri tarafından desteklenen Azure bölgesine ait emin olun.</span><span class="sxs-lookup"><span data-stu-id="99c82-131">Ensure that hello virtual network that you have specified belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="99c82-132">tooascertain Azure Active Directory etki alanı Hizmetleri kullanılabilir olduğu Azure bölgelerini Merhaba, bkz: [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="99c82-132">tooascertain hello Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="99c82-133">Burada Azure Active Directory etki alanı Hizmetleri desteklenmiyor tooa bölgeye ait sanal ağlar hello aşağı açılan listesinde görünmüyor.</span><span class="sxs-lookup"><span data-stu-id="99c82-133">Virtual networks that belong tooa region where Azure Active Directory Domain Services is not supported do not show up in hello drop-down list.</span></span>

   * <span data-ttu-id="99c82-134">Ayrılmış bir alt ağ hello sanal ağ içinde Azure Active Directory etki alanı Hizmetleri için kullanın.</span><span class="sxs-lookup"><span data-stu-id="99c82-134">Use a dedicated subnet within hello virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="99c82-135">Yapmak *değil* hello ağ geçidi alt ağı seçin.</span><span class="sxs-lookup"><span data-stu-id="99c82-135">Do *not* select hello gateway subnet.</span></span> <span data-ttu-id="99c82-136">Bkz. [ağ ile ilgili dikkat edilmesi gerekenler](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="99c82-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="99c82-137">Benzer şekilde, Azure Resource Manager kullanılarak oluşturulan sanal ağlar hello aşağı açılan listede görünmez.</span><span class="sxs-lookup"><span data-stu-id="99c82-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in hello drop-down list.</span></span> <span data-ttu-id="99c82-138">Resource Manager tabanlı sanal ağlar şu anda Azure Active Directory Domain Services'de desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="99c82-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="99c82-139">tooenable Azure Active Directory etki alanı Hizmetleri, hello sayfanın hello sonundaki hello görev bölmesinde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="99c82-139">tooenable Azure Active Directory Domain Services, in hello task pane at hello bottom of hello page, click **Save**.</span></span>
    * <span data-ttu-id="99c82-140">Azure Active Directory etki alanı Hizmetleri dizininiz için etkin durumdayken, hello sayfası durumunu görüntüler *bekleyen*.</span><span class="sxs-lookup"><span data-stu-id="99c82-140">While Azure Active Directory Domain Services is being enabled for your directory, hello page displays a status of *Pending*.</span></span>

        ![Domain Services Etkinleştirme penceresi](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="99c82-142">Azure Active Directory Domain Services, yönetilen etki alanınız için yüksek kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="99c82-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="99c82-143">Azure Active Directory etki alanı Hizmetleri'ni etkinleştirdikten sonra etki alanı Hizmetleri hello sanal ağda kullanılabilir hello IP görüntülenen birer birer adresleridir.</span><span class="sxs-lookup"><span data-stu-id="99c82-143">After you enable Azure Active Directory Domain Services, hello IP addresses at which domain services are available on hello virtual network are displayed one at a time.</span></span> <span data-ttu-id="99c82-144">Yakında hello hizmet etki alanınız için yüksek kullanılabilirlik sağlar gibi hello ikinci IP adresi kısa bir süre sonra hello ilk olarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="99c82-144">hello second IP address is displayed shortly after hello first, as soon hello service enables high availability for your domain.</span></span> <span data-ttu-id="99c82-145">Ne zaman yüksek kullanılabilirlik yapılandırılmış ve etki alanınız için etkin, hello iki IP adresi görmeniz gerekir **etki alanı Hizmetleri** hello bölümünü **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="99c82-145">When high availability is configured and active for your domain, you should see two IP addresses in hello **domain services** section of hello **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="99c82-146">Etki alanı Hizmetleri'nin kullanılabilir sanal ağınızdaki hello hello ilk IP adresi yaklaşık 20 too30 dakika sonra **IP adresi** hello alanını **yapılandırma** sayfası.</span><span class="sxs-lookup"><span data-stu-id="99c82-146">After about 20 too30 minutes, hello first IP address at which domain services are available on your virtual network in hello **IP address** field on hello **Configure** page.</span></span>

        ![Sağlanan ilk IP’yi gösteren Domain Services penceresi](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="99c82-148">Yüksek kullanılabilirlik etki alanınız için işletimsel olduğunda, iki IP adresi hello sayfasında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="99c82-148">When high availability is operational for your domain, two IP addresses are displayed on hello page.</span></span> <span data-ttu-id="99c82-149">Yönetilen etki alanınız, bu iki IP adresindeki seçilen sanal ağlarınız üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="99c82-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="99c82-150">Sanal ağınız için hello DNS ayarlarını güncelleştirebilmeniz için hello iki IP adresi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="99c82-150">Note hello two IP addresses so that you can update hello DNS settings for your virtual network.</span></span> <span data-ttu-id="99c82-151">Bunun yapılması, sanal makinelerin hello sanal ağ tooconnect toohello etki alanındaki etki alanına katılım gibi işlemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="99c82-151">Doing so enables virtual machines on hello virtual network tooconnect toohello domain for operations such as domain join.</span></span>

    ![Sağlanan her iki IP’yi gösteren Domain Services penceresi](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="99c82-153">Azure AD kiracınız (örneğin, kullanıcıların veya grupların hello numarası) Hello boyutuna bağlı olarak, eşitleme tooyour yönetilen etki alanı biraz uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="99c82-153">Depending on hello size of your Azure AD tenant (for example, hello number of users or groups), synchronization tooyour managed domain takes a while.</span></span> <span data-ttu-id="99c82-154">Bu eşitleme işlemi hello arka planda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="99c82-154">This synchronization process happens in hello background.</span></span> <span data-ttu-id="99c82-155">On binlerce nesne içeren büyük kiracılar için veya tüm kullanıcılar, grup üyelikleri ve kimlik bilgilerini toobe eşitlenen için iki gün sürebilir.</span><span class="sxs-lookup"><span data-stu-id="99c82-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials toobe synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="99c82-156">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="99c82-156">Next step</span></span>
[<span data-ttu-id="99c82-157">Görev 4: hello hello Azure sanal ağı için DNS ayarlarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="99c82-157">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
