---
title: "Azure Active Directory etki alanı Hizmetleri: hello Azure AD DC Yöneticiler grubu oluşturma | Microsoft Docs"
description: "Azure Active Directory etki alanı hello Klasik Azure portalı kullanarak Hizmetleri etkinleştir"
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
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="fd0f3-103">Azure Active Directory etki alanı hello Klasik Azure portalı kullanarak Hizmetleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="fd0f3-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>
<span data-ttu-id="fd0f3-104">Bu makalede ve sizin tooenable Azure Active Directory etki alanı Hizmetleri (Azure AD DS) Azure Active Directory (Azure AD) kiracınız için gerekli olan hello yapılandırma görevleri anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-104">This article describes and walks through hello configuration tasks that are required for you tooenable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="fd0f3-105">[**Bunun yerine Hello yeni (Önizleme) Azure portal deneyimi deneyin**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="fd0f3-105">[**Try hello new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a><span data-ttu-id="fd0f3-106">Görev 1: hello Azure AD DC Yöneticiler grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="fd0f3-106">Task 1: create hello Azure AD DC administrators group</span></span>
<span data-ttu-id="fd0f3-107">Merhaba ilk toocreate Azure AD kiracınıza yönetim grubunda bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-107">hello first task is toocreate an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="fd0f3-108">Bu özel yönetim grubu adı *AAD DC Yöneticiler*.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="fd0f3-109">Bu grubun üyeleri, etki alanına katılmış toohello Azure Active Directory etki alanı Hizmetleri tarafından yönetilen etki alanı olan makinelere sunucuda yönetici izinleri verilir.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-109">Members of this group are granted administrative permissions on machines that are domain-joined toohello Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="fd0f3-110">Etki alanına katılmış makinelerde toohello Yöneticiler grubunun bu gruba eklenir.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-110">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="fd0f3-111">Ayrıca, bu grubun üyeleri, Uzak Masaüstü tooconnect uzaktan toodomain katılmış makineler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-111">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="fd0f3-112">Azure Active Directory etki alanı Hizmetleri kullanılarak oluşturulan hello yönetilen etki alanındaki etki alanı yöneticisi veya kuruluş yöneticisi izinlerine sahip değil.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-112">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="fd0f3-113">Yönetilen etki alanlarında, bu izinleri hello hizmeti tarafından ayrılmış ve hello Kiracı içinde kullanılabilir toousers duruma getirilmez.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-113">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="fd0f3-114">Hello özel yönetim grubu oluşturulan kullanabilirsiniz ancak bu yapılandırma görevi tooperform bazı işlemleri ayrıcalıklı.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-114">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="fd0f3-115">Bu işlemler, bilgisayarlar toohello etki alanına katılma, etki alanına katılan makineler toohello yönetim grubuna ait ve Grup İlkesi yapılandırma içerir.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-115">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="fd0f3-116">Bu yapılandırma görevde hello yönetim grubu oluşturun ve bir veya daha fazla kullanıcı dizin toohello grubunuza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-116">In this configuration task, you create hello administrative group and add one or more users in your directory toohello group.</span></span> <span data-ttu-id="fd0f3-117">Azure Active Directory etki alanı Hizmetleri, toocreate hello yönetim grubu hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="fd0f3-117">toocreate hello administrative group for Azure Active Directory Domain Services, do hello following:</span></span>

1. <span data-ttu-id="fd0f3-118">Toohello Git [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fd0f3-118">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="fd0f3-119">Merhaba Hello sol bölmesinde seçin **Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-119">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="fd0f3-120">Tooenable Azure Active Directory etki alanı Hizmetleri istediğiniz hello Azure AD kiracısını (dizin) seçin.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-120">Select hello Azure AD tenant (directory) for which you want tooenable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="fd0f3-121">Her Azure AD dizini için yalnızca bir etki alanı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Azure AD dizini seçin](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="fd0f3-123">Merhaba üzerinde **Önizleme dizin** hello sayfasında, **grupları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-123">On hello **preview directory** page, click hello **Groups** tab.</span></span>
5. <span data-ttu-id="fd0f3-124">hello görev bölmesinde hello pencerenin hello altındaki bir grubun tooyour Azure AD Kiracı tooadd tıklatın **Grup Ekle**.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-124">tooadd a group tooyour Azure AD tenant, on hello task pane at hello bottom of hello window, click **Add Group**.</span></span>

    ![Merhaba Grup Ekle düğmesi](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="fd0f3-126">Merhaba, **Grup Ekle** iletişim kutusunda, adlı bir grup oluşturun **AAD DC Yöneticiler**ve ardından **grup türü** çok**güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-126">In hello **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** too**Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="fd0f3-127">Azure Active Directory etki alanı Hizmetleri tarafından yönetilen etki alanınızda, tooenable erişim tam bu ada sahip bir grup oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-127">tooenable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![Merhaba Grup Ekle iletişim kutusu](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="fd0f3-129">Merhaba, **açıklama** kutusuna, diğerleri sağlayan bir açıklama girin toounderstand bu grup içinde Azure Active Directory etki alanı yönetim izinleri verir.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-129">In hello **Description** box, enter a description that enables others toounderstand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="fd0f3-130">Hello grubu oluşturduktan sonra hello grup adı tooview, Özellikler'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-130">After you've created hello group, click hello group name tooview its properties.</span></span>
9. <span data-ttu-id="fd0f3-131">Merhaba pencerenin hello altındaki hello grubunun üyeleri olarak tooadd kullanıcılar'ı hello **Add Members** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-131">tooadd users as members of hello group, at hello bottom of hello window, click hello **Add Members** button.</span></span>

    ![Grup üyeleri düğme ekleme](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="fd0f3-133">Merhaba, **üye eklemek** iletişim kutusu,, bu grubun üyesi olması ve hello hello onay işareti simgesine tıklayın select hello kullanıcılar alt sağ.</span><span class="sxs-lookup"><span data-stu-id="fd0f3-133">In hello **Add members** dialog box, select hello users who should be members of this group, and then click hello checkmark icon at hello lower right.</span></span>

    ![Kullanıcıların tooadministrators grubu Ekle](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="fd0f3-135">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="fd0f3-135">Next step</span></span>
[<span data-ttu-id="fd0f3-136">Görev 2: oluşturun veya bir Azure sanal ağı seçin</span><span class="sxs-lookup"><span data-stu-id="fd0f3-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
