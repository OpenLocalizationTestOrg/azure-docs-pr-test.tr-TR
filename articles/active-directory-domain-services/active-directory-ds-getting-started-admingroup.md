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
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: f87bcf33d3b1eb21c7d84814e4c4086f664e293d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="2d94a-103">Azure Active Directory etki alanı (Önizleme) Azure portalını kullanarak Hizmetleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="2d94a-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="2d94a-104">Görev 3: yönetim grubunu yapılandır</span><span class="sxs-lookup"><span data-stu-id="2d94a-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="2d94a-105">Bu yapılandırma görevi, Azure AD dizininde bir yönetim grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2d94a-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="2d94a-106">Bu özel yönetim grubu adı *AAD DC Yöneticiler*.</span><span class="sxs-lookup"><span data-stu-id="2d94a-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="2d94a-107">Bu grubun üyeleri, etki alanı yönetilen etki alanına katılmış makinede yönetici izinleri verilir.</span><span class="sxs-lookup"><span data-stu-id="2d94a-107">Members of this group are granted administrative permissions on machines that are domain-joined to the managed domain.</span></span> <span data-ttu-id="2d94a-108">Etki alanına katılmış makinelerde bu Grup administrators grubuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="2d94a-108">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="2d94a-109">Ayrıca, bu grubun üyeleri, etki alanına katılmış makinelere uzaktan bağlanmak için Uzak Masaüstü'nü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d94a-109">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="2d94a-110">Azure Active Directory etki alanı Hizmetleri kullanılarak oluşturulan yönetilen etki alanında etki alanı yöneticisi veya kuruluş yöneticisi izinlerine sahip değil.</span><span class="sxs-lookup"><span data-stu-id="2d94a-110">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="2d94a-111">Yönetilen etki alanlarında, bu izinleri hizmeti tarafından ayrılmış ve Kiracı içinde kullanıcılar için kullanılabilir duruma getirilmez.</span><span class="sxs-lookup"><span data-stu-id="2d94a-111">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="2d94a-112">Ancak, bazı ayrıcalıklı işlemleri gerçekleştirmek için bu yapılandırma görevi oluşturulan özel yönetim grubunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d94a-112">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="2d94a-113">Bu işlemler, bilgisayarları etki alanına katılma, etki alanına katılmış makinede yönetim grubuna ait ve Grup İlkesi yapılandırma içerir.</span><span class="sxs-lookup"><span data-stu-id="2d94a-113">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="2d94a-114">Sihirbaz, yönetim grubu, Azure AD dizininde otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2d94a-114">The wizard automatically creates the administrative group in your Azure AD directory.</span></span> <span data-ttu-id="2d94a-115">Bu grubun 'AAD DC Yöneticiler' denir.</span><span class="sxs-lookup"><span data-stu-id="2d94a-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="2d94a-116">Azure AD dizininizi bu ada sahip varolan bir grubu varsa, sihirbaz bu grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="2d94a-116">If you have an existing group with this name in your Azure AD directory, the wizard selects this group.</span></span> <span data-ttu-id="2d94a-117">Grup üyeliği kullanarak yapılandırabilirsiniz **yönetici grubuna** sihirbaz sayfası.</span><span class="sxs-lookup"><span data-stu-id="2d94a-117">You can configure group membership using the **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="2d94a-118">Grup üyeliğini yapılandırmak için tıklatın **AAD DC Yöneticiler**.</span><span class="sxs-lookup"><span data-stu-id="2d94a-118">To configure group membership, click **AAD DC Administrators**.</span></span>

    ![Grup üyeliğini Yapılandır](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="2d94a-120">Tıklatın **üye eklemek** kullanıcıları Azure AD dizininizi yönetici grubuna eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2d94a-120">Click the **Add members** button to add users from your Azure AD directory to the administrator group.</span></span>

3. <span data-ttu-id="2d94a-121">İşiniz bittiğinde tıklatın **Tamam** üzerinde taşımayı **Özet** sihirbazın.</span><span class="sxs-lookup"><span data-stu-id="2d94a-121">When you are done, click **OK** to move on to the **Summary** page of the wizard.</span></span>

4. <span data-ttu-id="2d94a-122">Üzerinde **Özet** sayfası, yönetilen etki alanı için yapılandırma ayarlarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="2d94a-122">On the **Summary** page of the wizard, review the configuration settings for the managed domain.</span></span> <span data-ttu-id="2d94a-123">Değişiklik yapmak için sihirbazın herhangi bir adıma gerekirse geri dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d94a-123">You can go back to any step of the wizard to make changes, if necessary.</span></span> <span data-ttu-id="2d94a-124">İşiniz bittiğinde tıklatın **Tamam** yeni yönetilen etki alanı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="2d94a-124">When you are done, click **OK** to create the new managed domain.</span></span>

    ![Özet](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="2d94a-126">Azure AD etki alanı Hizmetleri dağıtımınızın ilerlemesini gösteren bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="2d94a-126">You see a notification that shows the progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="2d94a-127">Dağıtım için ayrıntılı ilerleme durumunu görmek için bildirime tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2d94a-127">Click the notification to see detailed progress for the deployment.</span></span>

    ![Bildirim - dağıtımı devam ediyor](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="2d94a-129">Yönetilen etki alanınızı sağlama</span><span class="sxs-lookup"><span data-stu-id="2d94a-129">Provision your managed domain</span></span>
<span data-ttu-id="2d94a-130">Yönetilen etki alanınızı sağlama işleminin bir saate kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="2d94a-130">The process of provisioning your managed domain can take up to an hour.</span></span>

1. <span data-ttu-id="2d94a-131">Dağıtımınızı sürerken içinde 'etki alanı Hizmetleri'nde' arayabilirsiniz **arama kaynakları** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="2d94a-131">While your deployment is in progress, you can search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="2d94a-132">Seçin **Azure AD etki alanı Hizmetleri** arama sonuç.</span><span class="sxs-lookup"><span data-stu-id="2d94a-132">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="2d94a-133">**Azure AD etki alanı Hizmetleri** sağlanmakta yönetilen etki alanı dikey penceresinde listelenir.</span><span class="sxs-lookup"><span data-stu-id="2d94a-133">The **Azure AD Domain Services** blade lists the managed domain that is being provisioned.</span></span>

    ![Yönetilen etki alanı sağlanacak Bul](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="2d94a-135">Etki alanı hakkında daha fazla ayrıntı görmek için yönetilen etki alanının adını (örneğin, ' contoso100.com')'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2d94a-135">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Etki alanı hizmetleri - sağlama durumu](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="2d94a-137">**Genel bakış** sekmesi gösterir etki alanı şu anda sağlanıyor.</span><span class="sxs-lookup"><span data-stu-id="2d94a-137">The **Overview** tab shows that the domain is currently being provisioned.</span></span> <span data-ttu-id="2d94a-138">Tam olarak sağlanana kadar yönetilen etki alanı yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="2d94a-138">You cannot configure the managed domain until it is fully provisioned.</span></span> <span data-ttu-id="2d94a-139">Bu tamamen sağlanması yönetilen etki alanınız için bir saate kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="2d94a-139">It may take up to an hour for your managed domain to be fully provisioned.</span></span>

    ![<span data-ttu-id="2d94a-140">Etki alanı hizmetleri - sağlama durumu sırasında genel bakış sekmesi</span><span class="sxs-lookup"><span data-stu-id="2d94a-140">Domain Services - Overview tab during the provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="2d94a-141">Yönetilen etki alanı tam olarak sağlandığında **genel bakış** sekmesi olarak etki alanı durumunu gösterir **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="2d94a-141">When the managed domain is fully provisioned, the **Overview** tab shows the domain status as **Running**.</span></span>

    ![Etki Alanı Hizmetleri - Tamamen hazır haldeki Genel Bakış sekmesi](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="2d94a-143">Üzerinde **özellikleri** sekmesine, etki alanı denetleyicileri sanal ağı için kullanılabilen iki IP adresi bakın.</span><span class="sxs-lookup"><span data-stu-id="2d94a-143">On the **Properties** tab, you see two IP addresses at which domain controllers are available for the virtual network.</span></span>

    ![Etki Alanı Hizmetleri - tam olarak sağlanan sonra Özellikleri sekmesi](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="2d94a-145">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="2d94a-145">Next step</span></span>
[<span data-ttu-id="2d94a-146">Görev 4: Azure sanal ağı için DNS ayarlarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="2d94a-146">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
