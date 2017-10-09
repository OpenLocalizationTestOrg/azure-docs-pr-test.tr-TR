---
title: "Azure Active Directory'deki grupları yönetmek için aaaPowerShell örnekleri | Microsoft Docs"
description: "Bu sayfa, PowerShell örnekleri toohelp sağlar. Azure Active Directory'de gruplarınızı yönetme"
keywords: "Azure AD, Azure Active Directory PowerShell grupları, Grup Yönetimi"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7a5023dc-2727-4c25-8254-b531fc3244ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: ba049babc436e99a290f20899b3a87bcfa811d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="13cb4-104">Grup Yönetimi için Azure Active Directory sürüm 2 cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="13cb4-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13cb4-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="13cb4-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="13cb4-106">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="13cb4-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="13cb4-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13cb4-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="13cb4-108">Bu makalede örnekleri içeren toouse PowerShell toomanage gruplarınızı Azure Active Directory'de (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="13cb4-108">This article contains examples of how toouse PowerShell toomanage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="13cb4-109">Bu ayrıca, tooget hello Azure AD PowerShell modülü ile nasıl ayarlanan bildirir.</span><span class="sxs-lookup"><span data-stu-id="13cb4-109">It also tells you how tooget set up with hello Azure AD PowerShell module.</span></span> <span data-ttu-id="13cb4-110">İlk olarak, şunları yapmalısınız [hello Azure AD PowerShell modülünü indirin](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="13cb4-110">First, you must [download hello Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-hello-azure-ad-powershell-module"></a><span data-ttu-id="13cb4-111">Hello Azure AD PowerShell modülü yükleniyor</span><span class="sxs-lookup"><span data-stu-id="13cb4-111">Installing hello Azure AD PowerShell module</span></span>
<span data-ttu-id="13cb4-112">tooinstall hello Azure AD PowerShell modülü hello aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="13cb4-112">tooinstall hello Azure AD PowerShell module, use hello following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="13cb4-113">Modül hello tooverify yüklendi, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="13cb4-113">tooverify that hello module was installed, use hello following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="13cb4-114">Şimdi hello modülünde hello cmdlet'leri kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13cb4-114">Now you can start using hello cmdlets in hello module.</span></span> <span data-ttu-id="13cb4-115">Hello Azure AD modülü hello cmdlet'leri tam bir açıklaması için lütfen toohello çevrimiçi başvuru belgelerine bakın [Azure Active Directory PowerShell sürüm 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="13cb4-115">For a full description of hello cmdlets in hello Azure AD module, please refer toohello online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-toohello-directory"></a><span data-ttu-id="13cb4-116">Toohello dizin bağlanma</span><span class="sxs-lookup"><span data-stu-id="13cb4-116">Connecting toohello directory</span></span>
<span data-ttu-id="13cb4-117">Azure AD PowerShell cmdlet'lerini kullanarak gruplarını yönetme başlamadan önce toomanage istediğiniz PowerShell oturumu toohello dizininize bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="13cb4-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session toohello directory you want toomanage.</span></span> <span data-ttu-id="13cb4-118">Merhaba aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="13cb4-118">Use hello following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="13cb4-119">Merhaba, kimlik bilgileri için hello cmdlet ister toouse tooaccess dizininize istiyor.</span><span class="sxs-lookup"><span data-stu-id="13cb4-119">hello cmdlet prompts you for hello credentials you want toouse tooaccess your directory.</span></span> <span data-ttu-id="13cb4-120">Bu örnekte, kullanıyoruz karen@drumkit.onmicrosoft.com tooaccess hello tanıtım dizin.</span><span class="sxs-lookup"><span data-stu-id="13cb4-120">In this example, we are using karen@drumkit.onmicrosoft.com tooaccess hello demonstration directory.</span></span> <span data-ttu-id="13cb4-121">Merhaba cmdlet'i bir onay tooshow hello oturum bağlı başarıyla döndürür tooyour dizini:</span><span class="sxs-lookup"><span data-stu-id="13cb4-121">hello cmdlet returns a confirmation tooshow hello session was connected successfully tooyour directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="13cb4-122">Şimdi dizininizde hello Azuread'i cmdlet'leri toomanage grupları kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13cb4-122">Now you can start using hello AzureAD cmdlets toomanage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="13cb4-123">Grupları alınıyor</span><span class="sxs-lookup"><span data-stu-id="13cb4-123">Retrieving groups</span></span>
<span data-ttu-id="13cb4-124">Get-AzureADGroups cmdlet'i tooretrieve var olan grupları kullanabilirsiniz dizininizden hello.</span><span class="sxs-lookup"><span data-stu-id="13cb4-124">tooretrieve existing groups from your directory you can use hello Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="13cb4-125">tooretrieve tüm gruplar hello dizininde parametresiz hello cmdlet'ini kullanın:</span><span class="sxs-lookup"><span data-stu-id="13cb4-125">tooretrieve all groups in hello directory, use hello cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="13cb4-126">Merhaba cmdlet'ini tüm gruplar hello bağlı dizininde döndürür.</span><span class="sxs-lookup"><span data-stu-id="13cb4-126">hello cmdlet returns all groups in hello connected directory.</span></span>

<span data-ttu-id="13cb4-127">Merhaba - objectID parametresi tooretrieve kullanabileceğiniz hello grubun objectID belirttiğiniz belirli bir grup:</span><span class="sxs-lookup"><span data-stu-id="13cb4-127">You can use hello -objectID parameter tooretrieve a specific group for which you specify hello group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="13cb4-128">Merhaba cmdlet şimdi girdiğiniz hello parametresinin hello değeri olan objectID eşleşen hello Grup döndürür:</span><span class="sxs-lookup"><span data-stu-id="13cb4-128">hello cmdlet now returns hello group whose objectID matches hello value of hello parameter you entered:</span></span>

    DeletionTimeStamp            :
    ObjectId                     : e29bae11-4ac0-450c-bc37-6dae8f3da61b
    ObjectType                   : Group
    Description                  :
    DirSyncEnabled               :
    DisplayName                  : Pacific NW Support
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 9bb4139b-60a1-434a-8c0d-7c1f8eee2df9
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

<span data-ttu-id="13cb4-129">Belirli bir grup kullanmak için arama hello - filtre parametresi.</span><span class="sxs-lookup"><span data-stu-id="13cb4-129">You can search for a specific group using hello -filter parameter.</span></span> <span data-ttu-id="13cb4-130">Bu parametre bir ODATA filtre yan tümcesi alır ve aşağıdaki örneğine hello olduğu gibi hello filtreyle eşleşen tüm grupları döndürür:</span><span class="sxs-lookup"><span data-stu-id="13cb4-130">This parameter takes an ODATA filter clause and returns all groups that match hello filter, as in hello following example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

> [!NOTE] 
> <span data-ttu-id="13cb4-131">Merhaba Azuread'i PowerShell cmdlet'leri hello standart OData sorgusunu uygulayın.</span><span class="sxs-lookup"><span data-stu-id="13cb4-131">hello AzureAD PowerShell cmdlets implement hello OData query standard.</span></span> <span data-ttu-id="13cb4-132">Daha fazla bilgi için bkz: **$filter** içinde [hello OData uç noktasını kullanarak OData sorgu seçeneklerinin](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span><span class="sxs-lookup"><span data-stu-id="13cb4-132">For more information, see **$filter** in [OData system query options using hello OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="13cb4-133">Grupları oluşturma</span><span class="sxs-lookup"><span data-stu-id="13cb4-133">Creating groups</span></span>
<span data-ttu-id="13cb4-134">toocreate yeni bir grup dizininizde, hello yeni AzureADGroup cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="13cb4-134">toocreate a new group in your directory, use hello New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="13cb4-135">Bu cmdlet "Pazarlama" adlı yeni bir güvenlik grubu oluşturur:</span><span class="sxs-lookup"><span data-stu-id="13cb4-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="13cb4-136">Güncelleştirme grupları</span><span class="sxs-lookup"><span data-stu-id="13cb4-136">Updating groups</span></span>
<span data-ttu-id="13cb4-137">Varolan bir grubu tooupdate hello kümesi AzureADGroup cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="13cb4-137">tooupdate an existing group, use hello Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="13cb4-138">Bu örnekte, biz hello DisplayName özelliği "Intune yöneticileri" Merhaba grubunun değiştirirsiniz</span><span class="sxs-lookup"><span data-stu-id="13cb4-138">In this example, we’re changing hello DisplayName property of hello group “Intune Administrators.”</span></span> <span data-ttu-id="13cb4-139">İlk olarak, biz hello Get-AzureADGroup cmdlet'i ve hello DisplayName özniteliği kullanarak filtre kullanarak hello grubu bulma:</span><span class="sxs-lookup"><span data-stu-id="13cb4-139">First, we’re finding hello group using hello Get-AzureADGroup cmdlet and filter using hello DisplayName attribute:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

<span data-ttu-id="13cb4-140">Ardından, biz hello açıklama özelliği toohello yeni değer "Intune cihaz yöneticileri" değiştirirsiniz:</span><span class="sxs-lookup"><span data-stu-id="13cb4-140">Next, we’re changing hello Description property toohello new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="13cb4-141">Biz hello grubu yeniden bulamazsanız, biz hello Description özelliği bakın artık olduğu güncelleştirilmiş tooreflect hello yeni değer:</span><span class="sxs-lookup"><span data-stu-id="13cb4-141">Now if we find hello group again, we see hello Description property is updated tooreflect hello new value:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Device Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

## <a name="deleting-groups"></a><span data-ttu-id="13cb4-142">Grup silme</span><span class="sxs-lookup"><span data-stu-id="13cb4-142">Deleting groups</span></span>
<span data-ttu-id="13cb4-143">dizininizi, toodelete gruplarından hello Kaldır AzureADGroup cmdlet şu şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="13cb4-143">toodelete groups from your directory, use hello Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="13cb4-144">Grupların üyeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="13cb4-144">Managing members of groups</span></span>
<span data-ttu-id="13cb4-145">Tooadd yeni üyeler tooa grubu gerekiyorsa, hello Ekle-AzureADGroupMember cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="13cb4-145">If you need tooadd new members tooa group, use hello Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="13cb4-146">Bu komut kullandık üyesi toohello Intune Yöneticileri grubu hello önceki örnekte ekler:</span><span class="sxs-lookup"><span data-stu-id="13cb4-146">This command adds a member toohello Intune Administrators group we used in hello previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="13cb4-147">Merhaba - objectID hello objectID parametredir tooadd üyesi istiyoruz hello Grup toowhich ve hello - RefObjectId olan hello objectID hello kullanıcısı tooadd toohello grubu üyeleri olarak istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="13cb4-147">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd a member, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as a member toohello group.</span></span>

<span data-ttu-id="13cb4-148">tooget hello var olan bir grubun üyeleri, bu örnekte olduğu gibi hello Get-AzureADGroupMember cmdlet'ini kullanın:</span><span class="sxs-lookup"><span data-stu-id="13cb4-148">tooget hello existing members of a group, use hello Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="13cb4-149">tooremove hello üye önceden toohello grup, aşağıda gösterildiği gibi hello Kaldır AzureADGroupMember cmdlet'ini kullanın, eklediğimiz:</span><span class="sxs-lookup"><span data-stu-id="13cb4-149">tooremove hello member we previously added toohello group, use hello Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="13cb4-150">bir kullanıcının tooverify hello grup üyelikleri hello seçin AzureADGroupIdsUserIsMemberOf cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="13cb4-150">tooverify hello group membership(s) of a user, use hello Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="13cb4-151">Bu cmdlet parametreleri hello kullanıcının hangi toocheck hello grup üyelikleri için objectID hello gibi alır ve hangi toocheck hello üyeliklerini gruplarının listesi.</span><span class="sxs-lookup"><span data-stu-id="13cb4-151">This cmdlet takes as its parameters hello ObjectId of hello user for which toocheck hello group memberships, and a list of groups for which toocheck hello memberships.</span></span> <span data-ttu-id="13cb4-152">"Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck" türünde bir karmaşık değişken Hello formunda böylece biz öncelikle bir değişken bu türüyle oluşturmanız gerekir sağlanan hello gruplarının listesini olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="13cb4-152">hello list of groups must be provided in hello form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="13cb4-153">Ardından, biz hello grup kimlikleri toocheck hello öznitelik bu karmaşık değişkeninin "Grup" kimlikleri için değerler sağlayın:</span><span class="sxs-lookup"><span data-stu-id="13cb4-153">Next, we provide values for hello groupIds toocheck in hello attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="13cb4-154">Şimdi, biz toocheck hello grup üyeliklerini $g hello gruplarında karşı objectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea sahip bir kullanıcının istiyorsanız, biz kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="13cb4-154">Now, if we want toocheck hello group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against hello groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="13cb4-155">döndürülen hello değeri, bu kullanıcının üye olduğu grupları listesidir.</span><span class="sxs-lookup"><span data-stu-id="13cb4-155">hello value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="13cb4-156">Bu yöntem toocheck kişiler, gruplar ya da hizmet asıl adı üyeliği Seç-AzureADGroupIdsContactIsMemberOf, Select AzureADGroupIdsGroupIsMemberOf kullanarak grupları, belirli bir listesi için geçerli olabilir veya AzureADGroupIdsServicePrincipalIsMemberOf seçin</span><span class="sxs-lookup"><span data-stu-id="13cb4-156">You can also apply this method toocheck Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="13cb4-157">Grupları sahiplerini yönetme</span><span class="sxs-lookup"><span data-stu-id="13cb4-157">Managing owners of groups</span></span>
<span data-ttu-id="13cb4-158">tooadd sahipleri tooa grubu, hello Ekle-AzureADGroupOwner cmdlet'ini kullanın:</span><span class="sxs-lookup"><span data-stu-id="13cb4-158">tooadd owners tooa group, use hello Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="13cb4-159">Merhaba - objectID hello objectID parametredir tooadd sahibi istiyoruz hello Grup toowhich ve hello - RefObjectId olan hello objectID hello kullanıcısı tooadd hello Grup sahibi olarak istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="13cb4-159">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd an owner, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as an owner of hello group.</span></span>

<span data-ttu-id="13cb4-160">tooretrieve hello bir grubun sahiplerini hello Get-AzureADGroupOwner cmdlet'ini kullanın:</span><span class="sxs-lookup"><span data-stu-id="13cb4-160">tooretrieve hello owners of a group, use hello Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="13cb4-161">Merhaba cmdlet'i hello belirtilen grubun sahiplerini hello listesini döndürür:</span><span class="sxs-lookup"><span data-stu-id="13cb4-161">hello cmdlet returns hello list of owners for hello specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="13cb4-162">Tooremove bir gruptan bir sahip hello Kaldır AzureADGroupOwner cmdlet'ini kullanın:</span><span class="sxs-lookup"><span data-stu-id="13cb4-162">If you want tooremove an owner from a group, use hello Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="13cb4-163">Ayrılmış diğer adlar</span><span class="sxs-lookup"><span data-stu-id="13cb4-163">Reserved aliases</span></span> 
<span data-ttu-id="13cb4-164">Grup oluşturulduğunda, belirli uç noktaları hello son kullanıcı toospecify hello e-posta adresi hello grubunun bir parçası olarak kullanılan bir mailNickname veya diğer toobe izin verin.</span><span class="sxs-lookup"><span data-stu-id="13cb4-164">When a group is created, certain endpoints allow hello end user toospecify a mailNickname or alias toobe used as part of hello email address of hello group.</span></span> <span data-ttu-id="13cb4-165">Üst düzey ayrıcalıklı e-posta diğer adlar aşağıdaki hello gruplarıyla yalnızca Azure AD genel yönetici tarafından oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="13cb4-165">Groups with hello following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="13cb4-166">Uygunsuz kullanım</span><span class="sxs-lookup"><span data-stu-id="13cb4-166">abuse</span></span> 
* <span data-ttu-id="13cb4-167">Yönetici</span><span class="sxs-lookup"><span data-stu-id="13cb4-167">admin</span></span> 
* <span data-ttu-id="13cb4-168">Yönetici</span><span class="sxs-lookup"><span data-stu-id="13cb4-168">administrator</span></span> 
* <span data-ttu-id="13cb4-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="13cb4-169">hostmaster</span></span> 
* <span data-ttu-id="13cb4-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="13cb4-170">majordomo</span></span> 
* <span data-ttu-id="13cb4-171">Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="13cb4-171">postmaster</span></span> 
* <span data-ttu-id="13cb4-172">kök</span><span class="sxs-lookup"><span data-stu-id="13cb4-172">root</span></span> 
* <span data-ttu-id="13cb4-173">Güvenli</span><span class="sxs-lookup"><span data-stu-id="13cb4-173">secure</span></span> 
* <span data-ttu-id="13cb4-174">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="13cb4-174">security</span></span> 
* <span data-ttu-id="13cb4-175">SSL-Yönetim</span><span class="sxs-lookup"><span data-stu-id="13cb4-175">ssl-admin</span></span> 
* <span data-ttu-id="13cb4-176">Web Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="13cb4-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="13cb4-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="13cb4-177">Next steps</span></span>
<span data-ttu-id="13cb4-178">Daha fazla Azure Active Directory PowerShell belgeleri bulabilirsiniz [Azure Active Directory cmdlet'leri](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="13cb4-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="13cb4-179">Azure Active Directory grupları ile erişim tooresources yönetme</span><span class="sxs-lookup"><span data-stu-id="13cb4-179">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="13cb4-180">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="13cb4-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
