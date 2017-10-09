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
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a>Grup Yönetimi için Azure Active Directory sürüm 2 cmdlet'leri
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-groups-create-azure-portal.md)
> * [Klasik Azure Portalı](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Bu makalede örnekleri içeren toouse PowerShell toomanage gruplarınızı Azure Active Directory'de (Azure AD).  Bu ayrıca, tooget hello Azure AD PowerShell modülü ile nasıl ayarlanan bildirir. İlk olarak, şunları yapmalısınız [hello Azure AD PowerShell modülünü indirin](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="installing-hello-azure-ad-powershell-module"></a>Hello Azure AD PowerShell modülü yükleniyor
tooinstall hello Azure AD PowerShell modülü hello aşağıdaki komutları kullanın:

    PS C:\Windows\system32> install-module azuread

Modül hello tooverify yüklendi, hello aşağıdaki komutu kullanın:

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

Şimdi hello modülünde hello cmdlet'leri kullanmaya başlayabilirsiniz. Hello Azure AD modülü hello cmdlet'leri tam bir açıklaması için lütfen toohello çevrimiçi başvuru belgelerine bakın [Azure Active Directory PowerShell sürüm 2](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="connecting-toohello-directory"></a>Toohello dizin bağlanma
Azure AD PowerShell cmdlet'lerini kullanarak gruplarını yönetme başlamadan önce toomanage istediğiniz PowerShell oturumu toohello dizininize bağlanmanız gerekir. Merhaba aşağıdaki komutu kullanın:

    PS C:\Windows\system32> Connect-AzureAD

Merhaba, kimlik bilgileri için hello cmdlet ister toouse tooaccess dizininize istiyor. Bu örnekte, kullanıyoruz karen@drumkit.onmicrosoft.com tooaccess hello tanıtım dizin. Merhaba cmdlet'i bir onay tooshow hello oturum bağlı başarıyla döndürür tooyour dizini:

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

Şimdi dizininizde hello Azuread'i cmdlet'leri toomanage grupları kullanmaya başlayabilirsiniz.

## <a name="retrieving-groups"></a>Grupları alınıyor
Get-AzureADGroups cmdlet'i tooretrieve var olan grupları kullanabilirsiniz dizininizden hello. tooretrieve tüm gruplar hello dizininde parametresiz hello cmdlet'ini kullanın:

    PS C:\Windows\system32> get-azureadgroup

Merhaba cmdlet'ini tüm gruplar hello bağlı dizininde döndürür.

Merhaba - objectID parametresi tooretrieve kullanabileceğiniz hello grubun objectID belirttiğiniz belirli bir grup:

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

Merhaba cmdlet şimdi girdiğiniz hello parametresinin hello değeri olan objectID eşleşen hello Grup döndürür:

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

Belirli bir grup kullanmak için arama hello - filtre parametresi. Bu parametre bir ODATA filtre yan tümcesi alır ve aşağıdaki örneğine hello olduğu gibi hello filtreyle eşleşen tüm grupları döndürür:

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
> Merhaba Azuread'i PowerShell cmdlet'leri hello standart OData sorgusunu uygulayın. Daha fazla bilgi için bkz: **$filter** içinde [hello OData uç noktasını kullanarak OData sorgu seçeneklerinin](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).

## <a name="creating-groups"></a>Grupları oluşturma
toocreate yeni bir grup dizininizde, hello yeni AzureADGroup cmdlet'ini kullanın. Bu cmdlet "Pazarlama" adlı yeni bir güvenlik grubu oluşturur:

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a>Güncelleştirme grupları
Varolan bir grubu tooupdate hello kümesi AzureADGroup cmdlet'ini kullanın. Bu örnekte, biz hello DisplayName özelliği "Intune yöneticileri" Merhaba grubunun değiştirirsiniz İlk olarak, biz hello Get-AzureADGroup cmdlet'i ve hello DisplayName özniteliği kullanarak filtre kullanarak hello grubu bulma:

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

Ardından, biz hello açıklama özelliği toohello yeni değer "Intune cihaz yöneticileri" değiştirirsiniz:

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

Biz hello grubu yeniden bulamazsanız, biz hello Description özelliği bakın artık olduğu güncelleştirilmiş tooreflect hello yeni değer:

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

## <a name="deleting-groups"></a>Grup silme
dizininizi, toodelete gruplarından hello Kaldır AzureADGroup cmdlet şu şekilde kullanın:

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a>Grupların üyeleri yönetme
Tooadd yeni üyeler tooa grubu gerekiyorsa, hello Ekle-AzureADGroupMember cmdlet'ini kullanın. Bu komut kullandık üyesi toohello Intune Yöneticileri grubu hello önceki örnekte ekler:

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

Merhaba - objectID hello objectID parametredir tooadd üyesi istiyoruz hello Grup toowhich ve hello - RefObjectId olan hello objectID hello kullanıcısı tooadd toohello grubu üyeleri olarak istiyoruz.

tooget hello var olan bir grubun üyeleri, bu örnekte olduğu gibi hello Get-AzureADGroupMember cmdlet'ini kullanın:

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

tooremove hello üye önceden toohello grup, aşağıda gösterildiği gibi hello Kaldır AzureADGroupMember cmdlet'ini kullanın, eklediğimiz:

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

bir kullanıcının tooverify hello grup üyelikleri hello seçin AzureADGroupIdsUserIsMemberOf cmdlet'ini kullanın. Bu cmdlet parametreleri hello kullanıcının hangi toocheck hello grup üyelikleri için objectID hello gibi alır ve hangi toocheck hello üyeliklerini gruplarının listesi. "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck" türünde bir karmaşık değişken Hello formunda böylece biz öncelikle bir değişken bu türüyle oluşturmanız gerekir sağlanan hello gruplarının listesini olması gerekir:

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

Ardından, biz hello grup kimlikleri toocheck hello öznitelik bu karmaşık değişkeninin "Grup" kimlikleri için değerler sağlayın:

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

Şimdi, biz toocheck hello grup üyeliklerini $g hello gruplarında karşı objectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea sahip bir kullanıcının istiyorsanız, biz kullanmanız gerekir:

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


döndürülen hello değeri, bu kullanıcının üye olduğu grupları listesidir. Bu yöntem toocheck kişiler, gruplar ya da hizmet asıl adı üyeliği Seç-AzureADGroupIdsContactIsMemberOf, Select AzureADGroupIdsGroupIsMemberOf kullanarak grupları, belirli bir listesi için geçerli olabilir veya AzureADGroupIdsServicePrincipalIsMemberOf seçin

## <a name="managing-owners-of-groups"></a>Grupları sahiplerini yönetme
tooadd sahipleri tooa grubu, hello Ekle-AzureADGroupOwner cmdlet'ini kullanın:

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

Merhaba - objectID hello objectID parametredir tooadd sahibi istiyoruz hello Grup toowhich ve hello - RefObjectId olan hello objectID hello kullanıcısı tooadd hello Grup sahibi olarak istiyoruz.

tooretrieve hello bir grubun sahiplerini hello Get-AzureADGroupOwner cmdlet'ini kullanın:

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

Merhaba cmdlet'i hello belirtilen grubun sahiplerini hello listesini döndürür:

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

Tooremove bir gruptan bir sahip hello Kaldır AzureADGroupOwner cmdlet'ini kullanın:

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a>Ayrılmış diğer adlar 
Grup oluşturulduğunda, belirli uç noktaları hello son kullanıcı toospecify hello e-posta adresi hello grubunun bir parçası olarak kullanılan bir mailNickname veya diğer toobe izin verin. Üst düzey ayrıcalıklı e-posta diğer adlar aşağıdaki hello gruplarıyla yalnızca Azure AD genel yönetici tarafından oluşturulabilir. 
  
* Uygunsuz kullanım 
* Yönetici 
* Yönetici 
* hostmaster 
* majordomo 
* Yöneticisi 
* kök 
* Güvenli 
* Güvenlik 
* SSL-Yönetim 
* Web Yöneticisi 

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla Azure Active Directory PowerShell belgeleri bulabilirsiniz [Azure Active Directory cmdlet'leri](/powershell/azure/install-adv2?view=azureadps-2.0).

* [Azure Active Directory grupları ile erişim tooresources yönetme](active-directory-manage-groups.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
