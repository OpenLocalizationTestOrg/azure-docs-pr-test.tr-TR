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
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="e840c-103">Azure Active Directory etki alanı hello Azure portal (Önizleme) kullanarak Hizmetleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="e840c-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="e840c-104">Görev 3: yönetim grubunu yapılandır</span><span class="sxs-lookup"><span data-stu-id="e840c-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="e840c-105">Bu yapılandırma görevi, Azure AD dizininde bir yönetim grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e840c-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="e840c-106">Bu özel yönetim grubu adı *AAD DC Yöneticiler*.</span><span class="sxs-lookup"><span data-stu-id="e840c-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="e840c-107">Bu grubun üyeleri, etki alanına katılmış toohello yönetilen etki alanı olan makinelere sunucuda yönetici izinleri verilir.</span><span class="sxs-lookup"><span data-stu-id="e840c-107">Members of this group are granted administrative permissions on machines that are domain-joined toohello managed domain.</span></span> <span data-ttu-id="e840c-108">Etki alanına katılmış makinelerde toohello Yöneticiler grubunun bu gruba eklenir.</span><span class="sxs-lookup"><span data-stu-id="e840c-108">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="e840c-109">Ayrıca, bu grubun üyeleri, Uzak Masaüstü tooconnect uzaktan toodomain katılmış makineler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e840c-109">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="e840c-110">Azure Active Directory etki alanı Hizmetleri kullanılarak oluşturulan hello yönetilen etki alanındaki etki alanı yöneticisi veya kuruluş yöneticisi izinlerine sahip değil.</span><span class="sxs-lookup"><span data-stu-id="e840c-110">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="e840c-111">Yönetilen etki alanlarında, bu izinleri hello hizmeti tarafından ayrılmış ve hello Kiracı içinde kullanılabilir toousers duruma getirilmez.</span><span class="sxs-lookup"><span data-stu-id="e840c-111">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="e840c-112">Hello özel yönetim grubu oluşturulan kullanabilirsiniz ancak bu yapılandırma görevi tooperform bazı işlemleri ayrıcalıklı.</span><span class="sxs-lookup"><span data-stu-id="e840c-112">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="e840c-113">Bu işlemler, bilgisayarlar toohello etki alanına katılma, etki alanına katılan makineler toohello yönetim grubuna ait ve Grup İlkesi yapılandırma içerir.</span><span class="sxs-lookup"><span data-stu-id="e840c-113">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="e840c-114">Başlangıç Sihirbazı otomatik olarak Azure AD dizininizi hello yönetim grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e840c-114">hello wizard automatically creates hello administrative group in your Azure AD directory.</span></span> <span data-ttu-id="e840c-115">Bu grubun 'AAD DC Yöneticiler' denir.</span><span class="sxs-lookup"><span data-stu-id="e840c-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="e840c-116">Bu ada sahip varolan bir grubu Azure AD dizininizi varsa, bu grubun hello Sihirbazı'nı seçer.</span><span class="sxs-lookup"><span data-stu-id="e840c-116">If you have an existing group with this name in your Azure AD directory, hello wizard selects this group.</span></span> <span data-ttu-id="e840c-117">Grup üyeliği hello kullanarak yapılandırabilirsiniz **yönetici grubuna** sihirbaz sayfası.</span><span class="sxs-lookup"><span data-stu-id="e840c-117">You can configure group membership using hello **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="e840c-118">tooconfigure grup üyeliği tıklatın **AAD DC Yöneticiler**.</span><span class="sxs-lookup"><span data-stu-id="e840c-118">tooconfigure group membership, click **AAD DC Administrators**.</span></span>

    ![Grup üyeliğini Yapılandır](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="e840c-120">Merhaba tıklatın **üye eklemek** düğmesini tooadd kullanıcılar, Azure AD directory toohello yönetici grubundan.</span><span class="sxs-lookup"><span data-stu-id="e840c-120">Click hello **Add members** button tooadd users from your Azure AD directory toohello administrator group.</span></span>

3. <span data-ttu-id="e840c-121">İşiniz bittiğinde tıklatın **Tamam** toomove toohello üzerinde **özeti** hello sihirbazın sayfası.</span><span class="sxs-lookup"><span data-stu-id="e840c-121">When you are done, click **OK** toomove on toohello **Summary** page of hello wizard.</span></span>

4. <span data-ttu-id="e840c-122">Merhaba üzerinde **Özet** hello sihirbazının hello yönetilen etki alanı için gözden geçirme hello yapılandırma ayarları.</span><span class="sxs-lookup"><span data-stu-id="e840c-122">On hello **Summary** page of hello wizard, review hello configuration settings for hello managed domain.</span></span> <span data-ttu-id="e840c-123">Merhaba Sihirbazı toomake değişikliklerden tooany adım gerekirse geri dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e840c-123">You can go back tooany step of hello wizard toomake changes, if necessary.</span></span> <span data-ttu-id="e840c-124">İşiniz bittiğinde tıklatın **Tamam** toocreate hello yeni yönetilen etki alanı.</span><span class="sxs-lookup"><span data-stu-id="e840c-124">When you are done, click **OK** toocreate hello new managed domain.</span></span>

    ![Özet](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="e840c-126">Azure AD etki alanı Hizmetleri dağıtımınızın hello ilerleme durumunu gösteren bir bildirim görür.</span><span class="sxs-lookup"><span data-stu-id="e840c-126">You see a notification that shows hello progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="e840c-127">Merhaba bildirime tıklayın toosee ayrıntılı hello dağıtımı devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="e840c-127">Click hello notification toosee detailed progress for hello deployment.</span></span>

    ![Bildirim - dağıtımı devam ediyor](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="e840c-129">Yönetilen etki alanınızı sağlama</span><span class="sxs-lookup"><span data-stu-id="e840c-129">Provision your managed domain</span></span>
<span data-ttu-id="e840c-130">Yönetilen etki alanınızı sağlama işleminin hello tooan saat sürebilir.</span><span class="sxs-lookup"><span data-stu-id="e840c-130">hello process of provisioning your managed domain can take up tooan hour.</span></span>

1. <span data-ttu-id="e840c-131">Dağıtımınızı sürerken ' etki alanı Hizmetleri'nde' hello arayabilirsiniz **arama kaynakları** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="e840c-131">While your deployment is in progress, you can search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="e840c-132">Seçin **Azure AD etki alanı Hizmetleri** hello arama sonuç.</span><span class="sxs-lookup"><span data-stu-id="e840c-132">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="e840c-133">Merhaba **Azure AD etki alanı Hizmetleri** sağlanmakta hello yönetilen etki dikey penceresinde listelenir.</span><span class="sxs-lookup"><span data-stu-id="e840c-133">hello **Azure AD Domain Services** blade lists hello managed domain that is being provisioned.</span></span>

    ![Yönetilen etki alanı sağlanacak Bul](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="e840c-135">Merhaba etki alanı hakkında daha fazla ayrıntı hello yönetilen etki alanı (örneğin, ' contoso100.com') toosee Hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e840c-135">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Etki alanı hizmetleri - sağlama durumu](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="e840c-137">Merhaba **genel bakış** sekmesi gösterir hello etki şu anda hazırlanır.</span><span class="sxs-lookup"><span data-stu-id="e840c-137">hello **Overview** tab shows that hello domain is currently being provisioned.</span></span> <span data-ttu-id="e840c-138">Tam olarak sağlanana kadar hello yönetilen etki alanı yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="e840c-138">You cannot configure hello managed domain until it is fully provisioned.</span></span> <span data-ttu-id="e840c-139">Tam olarak sağlanan, yönetilen etki alanı toobe tooan saattir yukarı sürebilir.</span><span class="sxs-lookup"><span data-stu-id="e840c-139">It may take up tooan hour for your managed domain toobe fully provisioned.</span></span>

    ![<span data-ttu-id="e840c-140">Etki alanı hizmetleri - sağlama durumu hello sırasında genel bakış sekmesi</span><span class="sxs-lookup"><span data-stu-id="e840c-140">Domain Services - Overview tab during hello provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="e840c-141">Merhaba yönetilen etki alanı tam olarak sağlandığında hello **genel bakış** sekmesi gösterir hello etki alanı durumu olarak **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="e840c-141">When hello managed domain is fully provisioned, hello **Overview** tab shows hello domain status as **Running**.</span></span>

    ![Etki Alanı Hizmetleri - Tamamen hazır haldeki Genel Bakış sekmesi](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="e840c-143">Merhaba üzerinde **özellikleri** sekmesine, etki alanı denetleyicileri hello sanal ağı için kullanılabilen iki IP adresi bakın.</span><span class="sxs-lookup"><span data-stu-id="e840c-143">On hello **Properties** tab, you see two IP addresses at which domain controllers are available for hello virtual network.</span></span>

    ![Etki Alanı Hizmetleri - tam olarak sağlanan sonra Özellikleri sekmesi](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="e840c-145">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="e840c-145">Next step</span></span>
[<span data-ttu-id="e840c-146">Görev 4: hello hello Azure sanal ağı için DNS ayarlarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e840c-146">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
