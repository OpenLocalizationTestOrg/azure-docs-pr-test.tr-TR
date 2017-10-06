---
title: "Azure Active Directory cmdlet'lerini kullanarak aaaConfigure grup ayarları | Microsoft Docs"
description: "Nasıl grupları Azure Active Directory cmdlet'lerini kullanarak hello ayarlarını yönetin"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 9f2090e6-3af4-4f07-bbb2-1d18dae89b73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro;
ms.openlocfilehash: 46db49d9dec3eaa41c97ca74c57854189eddc16d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a>Grup ayarlarını yapılandırmak için Azure Active Directory cmdlet'leri

> [!IMPORTANT]
> Bu içerik yalnızca tooOffice 365 grupları geçerlidir. Hakkında daha fazla bilgi için tooallow kullanıcılar toocreate güvenlik gruplarını, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` açıklandığı gibi [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0). 

Office 365 grupları ayarları, bir ayar nesnesi ve SettingsTemplate nesnesi kullanılarak yapılandırılır. Başlangıçta, dizininize hello varsayılan ayarlarla yapılandırıldığından dizininizde, tüm ayarları nesnelerini görmüyorum. toochange hello varsayılan ayarları, ayarları şablon kullanarak yeni bir ayarları nesnesi oluşturmanız gerekir. Ayarları şablonları Microsoft tarafından tanımlanır. Birkaç farklı ayarlar şablonu vardır. tooconfigure Office 365 grup ayarları dizininiz için "Group.Unified" adlı hello şablonu kullanın. tek bir grup tooconfigure Office 365 Grup ayarlarını "Group.Unified.Guest" adlı hello şablonu kullanın. Bu şablon kullanılan toomanage Konuk erişimi tooan Office 365 grubudur. 

Merhaba cmdlet'leri hello Azure Active Directory PowerShell V2 modülünde bir parçasıdır. Yönergeler için nasıl toodownload ve bilgisayarınızın, yükleme hello modülü hello makaleye bakın [Azure Active Directory PowerShell sürüm 2](https://docs.microsoft.com/powershell/azuread/). Merhaba modülünden hello sürüm 2 sürümü yükleyebilirsiniz [hello PowerShell Galerisi](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="retrieve-a-specific-settings-value"></a>Belirli ayarları değeri Al
Merhaba adını biliyorsanız ayarı hello tooretrieve istediğiniz, cmdlet tooretrieve hello geçerli ayarları değeri aşağıda hello kullanabilirsiniz. Bu örnekte, biz "UsageGuidelinesUrl." adlı bir ayarı hello değeri alınırken Dizin ayarlarını ve adları hakkında daha fazla aşağı bu makalede daha fazla bilgi edinebilirsiniz.

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a>Merhaba dizin düzeyinde ayarları oluştur
Bu adımları ayarları dizin düzeyinde hello dizinindeki tooall Office 365 grupları (Birleşik gruplar) uygulanacak oluşturun.

1. Hello DirectorySettings cmdlet'leri, hello toouse istediğiniz SettingsTemplate hello kimliği belirtmelisiniz. Bu kimliği bilmiyorsanız bu cmdlet'i tüm ayarları şablonları hello listesini döndürür:
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  Bu cmdlet çağrısı kullanılabilir tüm şablonları döndürür:
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define hello different settings that can be used for hello associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. tooadd Kullanım Kılavuzu URL, öncelikle hello Kullanım Kılavuzu URL değeri tanımlayan tooget hello SettingsTemplate nesnesi gerekir; diğer bir deyişle, Group.Unified şablonu hello:
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. Ardından, bu şablona dayalı yeni bir ayar nesnesi oluşturun:
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. Ardından hello Kullanım Kılavuzu değeri güncelleştirin:
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. Son olarak, hello ayarlarını uygulayın:
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

Başarıyla tamamlandığında, hello cmdlet'i hello yeni ayarları nesnesinin hello kimliği döndürür:
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
Merhaba Group.Unified SettingsTemplate tanımlanan hello ayarları aşağıdadır.

| **Ayar** | **Açıklama** |
| --- | --- |
|  <ul><li>EnableGroupCreation<li>Tür: Boolean<li>Varsayılan: True |Unified grubu oluşturma hello dizinde izin verilip verilmediğini belirten hello bayrak. |
|  <ul><li>GroupCreationAllowedGroupId<li>Türü: Dize<li>Varsayılan: "" |Merhaba güvenlik grubu için hangi hello üyeleri toocreate birleşik grupları verilir GUİD'si bile EnableGroupCreation == false. |
|  <ul><li>UsageGuidelinesUrl<li>Türü: Dize<li>Varsayılan: "" |Bağlantı toohello Grup kullanım yönergeleri. |
|  <ul><li>ClassificationDescriptions<li>Türü: Dize<li>Varsayılan: "" | Sınıflandırma açıklamaları virgülle ayrılmış listesi. |
|  <ul><li>DefaultClassification<li>Türü: Dize<li>Varsayılan: "" | Hiçbiri belirtilmemişse hello varsayılan sınıflandırma bir grup için kullanılan toobe olan hello sınıflandırması.|
|  <ul><li>PrefixSuffixNamingRequirement<li>Türü: Dize<li>Varsayılan: "" |Henüz uygulanmadı
|  <ul><li>AllowGuestsToBeGroupOwner<li>Tür: Boolean<li>Varsayılan: False | Konuk kullanıcı gruplarının sahibi olması olup olmadığını gösteren bir Boole değeri. |
|  <ul><li>AllowGuestsToAccessGroups<li>Tür: Boolean<li>Varsayılan: True | Konuk kullanıcı erişim tooUnified grupları içeriğe sahip olup olmadığını gösteren bir Boole değeri. |
|  <ul><li>GuestUsageGuidelinesUrl<li>Türü: Dize<li>Varsayılan: "" | bir bağlantı toohello Konuk kullanım yönergeleri Hello URL'si. |
|  <ul><li>AllowToAddGuests<li>Tür: Boolean<li>Varsayılan: True | İzin verilen tooadd konuklar toothis dizin olup olmadığını gösteren bir Boole değeri.|
|  <ul><li>ClassificationList<li>Türü: Dize<li>Varsayılan: "" |Uygulanan tooUnified grupları olabilir geçerli sınıflandırma değerleri virgülle ayrılmış listesi. |
|  <ul><li>EnableGroupCreation<li>Tür: Boolean<li>Varsayılan: True | Yönetici olmayan kullanıcıların yeni Unified grupları oluşturabilirsiniz olup olmadığını gösteren bir Boole değeri. |


## <a name="read-settings-at-hello-directory-level"></a>Merhaba dizin düzeyinde ayarlarını okuma
Bu adımları tooall Office grupları hello dizininde geçerli olan ayarları dizin düzeyinde okuyun.

1. Tüm mevcut directory ayarları okuyun:
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  Bu cmdlet, tüm dizin ayarları listesini döndürür:
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. Belirli bir grup için tüm ayarların okuyun:
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. Tüm dizin ayarlarının değerleri ayarları kimliği GUID kullanarak bir özel dizin ayarları nesnesinin okuyun:
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  Bu cmdlet, belirli bu grup için bu ayarları nesnesinde hello adları ve değerleri döndürür:
  ```
  Name                          Value
  ----                          -----
  ClassificationDescriptions
  DefaultClassification
  PrefixSuffixNamingRequirement
  AllowGuestsToBeGroupOwner     False 
  AllowGuestsToAccessGroups     True
  GuestUsageGuidelinesUrl
  GroupCreationAllowedGroupId
  AllowToAddGuests              True
  UsageGuidelinesUrl            <https://guideline.com>
  ClassificationList
  EnableGroupCreation           True
  ```

## <a name="update-settings-for-a-specific-group"></a>Belirli bir grup için güncelleştirme ayarları

1. "Groups.Unified.Guest" adlı hello ayarları şablonu için arama
  ```
  Get-AzureADDirectorySettingTemplate
  
  Id                                   DisplayName            Description
  --                                   -----------            -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Unified Group
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
  ```
2. Merhaba Groups.Unified.Guest şablonu için başlangıç şablonu nesnesi Al:
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. Merhaba şablondan yeni bir ayar nesnesi oluşturun:
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. Merhaba ayarı gerekli toohello değerini ayarlayın:
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. Yeni bir ayar Hello hello gerekli grup için hello dizini oluşturun:
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a>Merhaba dizin düzeyinde ayarlarını güncelleştirme

Bu adımları dizin düzeyinde tooall Unified gruplar hello dizinde uygulamanızı ayarlarını güncelleştirin. Bu örnekler, dizininizde bir ayar nesnesi bulunmakta varsayar.

1. Merhaba olan ayar nesnesini bulun:
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. Güncelleştirme başlangıç değeri:
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. Merhaba ayarını güncelleştirin:
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a>Merhaba dizin düzeyinde ayarlarını Kaldır
Bu adım tooall Office grupları hello dizininde uygulanacak ayarları dizin düzeyinde kaldırır.
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a>Cmdlet'in söz dizimi başvurusu
Daha fazla Azure Active Directory PowerShell belgeleri bulabilirsiniz [Azure Active Directory cmdlet'leri](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="additional-reading"></a>Ek kaynaklar

* [Azure Active Directory grupları ile erişim tooresources yönetme](active-directory-manage-groups.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
