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
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="1bb5c-103">Grup ayarlarını yapılandırmak için Azure Active Directory cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="1bb5c-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1bb5c-104">Bu içerik yalnızca tooOffice 365 grupları geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-104">This content applies only tooOffice 365 groups.</span></span> <span data-ttu-id="1bb5c-105">Hakkında daha fazla bilgi için tooallow kullanıcılar toocreate güvenlik gruplarını, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` açıklandığı gibi [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="1bb5c-105">For more information on how tooallow users toocreate Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="1bb5c-106">Office 365 grupları ayarları, bir ayar nesnesi ve SettingsTemplate nesnesi kullanılarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="1bb5c-107">Başlangıçta, dizininize hello varsayılan ayarlarla yapılandırıldığından dizininizde, tüm ayarları nesnelerini görmüyorum.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with hello default settings.</span></span> <span data-ttu-id="1bb5c-108">toochange hello varsayılan ayarları, ayarları şablon kullanarak yeni bir ayarları nesnesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-108">toochange hello default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="1bb5c-109">Ayarları şablonları Microsoft tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="1bb5c-110">Birkaç farklı ayarlar şablonu vardır.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-110">There are several different settings templates.</span></span> <span data-ttu-id="1bb5c-111">tooconfigure Office 365 grup ayarları dizininiz için "Group.Unified" adlı hello şablonu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-111">tooconfigure Office 365 group settings for your directory, you use hello template named "Group.Unified".</span></span> <span data-ttu-id="1bb5c-112">tek bir grup tooconfigure Office 365 Grup ayarlarını "Group.Unified.Guest" adlı hello şablonu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-112">tooconfigure Office 365 group settings on a single group, use hello template named "Group.Unified.Guest".</span></span> <span data-ttu-id="1bb5c-113">Bu şablon kullanılan toomanage Konuk erişimi tooan Office 365 grubudur.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-113">This template is used toomanage guest access tooan Office 365 group.</span></span> 

<span data-ttu-id="1bb5c-114">Merhaba cmdlet'leri hello Azure Active Directory PowerShell V2 modülünde bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-114">hello cmdlets are part of hello Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="1bb5c-115">Yönergeler için nasıl toodownload ve bilgisayarınızın, yükleme hello modülü hello makaleye bakın [Azure Active Directory PowerShell sürüm 2](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="1bb5c-115">For instructions how toodownload and install hello module on your computer, see hello article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="1bb5c-116">Merhaba modülünden hello sürüm 2 sürümü yükleyebilirsiniz [hello PowerShell Galerisi](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="1bb5c-116">You can install hello version 2 release of hello module from [hello PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="1bb5c-117">Belirli ayarları değeri Al</span><span class="sxs-lookup"><span data-stu-id="1bb5c-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="1bb5c-118">Merhaba adını biliyorsanız ayarı hello tooretrieve istediğiniz, cmdlet tooretrieve hello geçerli ayarları değeri aşağıda hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-118">If you know hello name of hello setting you want tooretrieve, you can use hello below cmdlet tooretrieve hello current settings value.</span></span> <span data-ttu-id="1bb5c-119">Bu örnekte, biz "UsageGuidelinesUrl." adlı bir ayarı hello değeri alınırken</span><span class="sxs-lookup"><span data-stu-id="1bb5c-119">In this example, we're retrieving hello value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="1bb5c-120">Dizin ayarlarını ve adları hakkında daha fazla aşağı bu makalede daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a><span data-ttu-id="1bb5c-121">Merhaba dizin düzeyinde ayarları oluştur</span><span class="sxs-lookup"><span data-stu-id="1bb5c-121">Create settings at hello directory level</span></span>
<span data-ttu-id="1bb5c-122">Bu adımları ayarları dizin düzeyinde hello dizinindeki tooall Office 365 grupları (Birleşik gruplar) uygulanacak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-122">These steps create settings at directory level, which apply tooall Office 365 groups (Unified groups) in hello directory.</span></span>

1. <span data-ttu-id="1bb5c-123">Hello DirectorySettings cmdlet'leri, hello toouse istediğiniz SettingsTemplate hello kimliği belirtmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-123">In hello DirectorySettings cmdlets, you must specify hello ID of hello SettingsTemplate you want toouse.</span></span> <span data-ttu-id="1bb5c-124">Bu kimliği bilmiyorsanız bu cmdlet'i tüm ayarları şablonları hello listesini döndürür:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-124">If you do not know this ID, this cmdlet returns hello list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="1bb5c-125">Bu cmdlet çağrısı kullanılabilir tüm şablonları döndürür:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-125">This cmdlet call returns all templates that are available:</span></span>
  
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
2. <span data-ttu-id="1bb5c-126">tooadd Kullanım Kılavuzu URL, öncelikle hello Kullanım Kılavuzu URL değeri tanımlayan tooget hello SettingsTemplate nesnesi gerekir; diğer bir deyişle, Group.Unified şablonu hello:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-126">tooadd a usage guideline URL, first you need tooget hello SettingsTemplate object that defines hello usage guideline URL value; that is, hello Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="1bb5c-127">Ardından, bu şablona dayalı yeni bir ayar nesnesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="1bb5c-128">Ardından hello Kullanım Kılavuzu değeri güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-128">Then update hello usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="1bb5c-129">Son olarak, hello ayarlarını uygulayın:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-129">Finally, apply hello settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="1bb5c-130">Başarıyla tamamlandığında, hello cmdlet'i hello yeni ayarları nesnesinin hello kimliği döndürür:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-130">Upon successful completion, hello cmdlet returns hello ID of hello new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="1bb5c-131">Merhaba Group.Unified SettingsTemplate tanımlanan hello ayarları aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-131">Here are hello settings defined in hello Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="1bb5c-132">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="1bb5c-132">**Setting**</span></span> | <span data-ttu-id="1bb5c-133">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="1bb5c-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="1bb5c-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="1bb5c-134">EnableGroupCreation</span></span><li><span data-ttu-id="1bb5c-135">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="1bb5c-135">Type: Boolean</span></span><li><span data-ttu-id="1bb5c-136">Varsayılan: True</span><span class="sxs-lookup"><span data-stu-id="1bb5c-136">Default: True</span></span> |<span data-ttu-id="1bb5c-137">Unified grubu oluşturma hello dizinde izin verilip verilmediğini belirten hello bayrak.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-137">hello flag indicating whether Unified Group creation is allowed in hello directory.</span></span> |
|  <ul><li><span data-ttu-id="1bb5c-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="1bb5c-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="1bb5c-139">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="1bb5c-139">Type: String</span></span><li><span data-ttu-id="1bb5c-140">Varsayılan: ""</span><span class="sxs-lookup"><span data-stu-id="1bb5c-140">Default: “”</span></span> |<span data-ttu-id="1bb5c-141">Merhaba güvenlik grubu için hangi hello üyeleri toocreate birleşik grupları verilir GUİD'si bile EnableGroupCreation == false.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-141">GUID of hello security group for which hello members are allowed toocreate Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="1bb5c-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="1bb5c-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="1bb5c-143">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="1bb5c-143">Type: String</span></span><li><span data-ttu-id="1bb5c-144">Varsayılan: ""</span><span class="sxs-lookup"><span data-stu-id="1bb5c-144">Default: “”</span></span> |<span data-ttu-id="1bb5c-145">Bağlantı toohello Grup kullanım yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-145">A link toohello Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="1bb5c-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="1bb5c-146">ClassificationDescriptions</span></span><li><span data-ttu-id="1bb5c-147">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="1bb5c-147">Type: String</span></span><li><span data-ttu-id="1bb5c-148">Varsayılan: ""</span><span class="sxs-lookup"><span data-stu-id="1bb5c-148">Default: “”</span></span> | <span data-ttu-id="1bb5c-149">Sınıflandırma açıklamaları virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="1bb5c-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="1bb5c-150">DefaultClassification</span></span><li><span data-ttu-id="1bb5c-151">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="1bb5c-151">Type: String</span></span><li><span data-ttu-id="1bb5c-152">Varsayılan: ""</span><span class="sxs-lookup"><span data-stu-id="1bb5c-152">Default: “”</span></span> | <span data-ttu-id="1bb5c-153">Hiçbiri belirtilmemişse hello varsayılan sınıflandırma bir grup için kullanılan toobe olan hello sınıflandırması.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-153">hello classification that is toobe used as hello default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="1bb5c-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="1bb5c-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="1bb5c-155">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="1bb5c-155">Type: String</span></span><li><span data-ttu-id="1bb5c-156">Varsayılan: ""</span><span class="sxs-lookup"><span data-stu-id="1bb5c-156">Default: “”</span></span> |<span data-ttu-id="1bb5c-157">Henüz uygulanmadı</span><span class="sxs-lookup"><span data-stu-id="1bb5c-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="1bb5c-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="1bb5c-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="1bb5c-159">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="1bb5c-159">Type: Boolean</span></span><li><span data-ttu-id="1bb5c-160">Varsayılan: False</span><span class="sxs-lookup"><span data-stu-id="1bb5c-160">Default: False</span></span> | <span data-ttu-id="1bb5c-161">Konuk kullanıcı gruplarının sahibi olması olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="1bb5c-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="1bb5c-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="1bb5c-163">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="1bb5c-163">Type: Boolean</span></span><li><span data-ttu-id="1bb5c-164">Varsayılan: True</span><span class="sxs-lookup"><span data-stu-id="1bb5c-164">Default: True</span></span> | <span data-ttu-id="1bb5c-165">Konuk kullanıcı erişim tooUnified grupları içeriğe sahip olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-165">Boolean indicating whether or not a guest user can have access tooUnified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="1bb5c-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="1bb5c-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="1bb5c-167">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="1bb5c-167">Type: String</span></span><li><span data-ttu-id="1bb5c-168">Varsayılan: ""</span><span class="sxs-lookup"><span data-stu-id="1bb5c-168">Default: “”</span></span> | <span data-ttu-id="1bb5c-169">bir bağlantı toohello Konuk kullanım yönergeleri Hello URL'si.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-169">hello url of a link toohello guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="1bb5c-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="1bb5c-170">AllowToAddGuests</span></span><li><span data-ttu-id="1bb5c-171">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="1bb5c-171">Type: Boolean</span></span><li><span data-ttu-id="1bb5c-172">Varsayılan: True</span><span class="sxs-lookup"><span data-stu-id="1bb5c-172">Default: True</span></span> | <span data-ttu-id="1bb5c-173">İzin verilen tooadd konuklar toothis dizin olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-173">A boolean indicating whether or not is allowed tooadd guests toothis directory.</span></span>|
|  <ul><li><span data-ttu-id="1bb5c-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="1bb5c-174">ClassificationList</span></span><li><span data-ttu-id="1bb5c-175">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="1bb5c-175">Type: String</span></span><li><span data-ttu-id="1bb5c-176">Varsayılan: ""</span><span class="sxs-lookup"><span data-stu-id="1bb5c-176">Default: “”</span></span> |<span data-ttu-id="1bb5c-177">Uygulanan tooUnified grupları olabilir geçerli sınıflandırma değerleri virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-177">A comma-delimited list of valid classification values that can be applied tooUnified Groups.</span></span> |
|  <ul><li><span data-ttu-id="1bb5c-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="1bb5c-178">EnableGroupCreation</span></span><li><span data-ttu-id="1bb5c-179">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="1bb5c-179">Type: Boolean</span></span><li><span data-ttu-id="1bb5c-180">Varsayılan: True</span><span class="sxs-lookup"><span data-stu-id="1bb5c-180">Default: True</span></span> | <span data-ttu-id="1bb5c-181">Yönetici olmayan kullanıcıların yeni Unified grupları oluşturabilirsiniz olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-hello-directory-level"></a><span data-ttu-id="1bb5c-182">Merhaba dizin düzeyinde ayarlarını okuma</span><span class="sxs-lookup"><span data-stu-id="1bb5c-182">Read settings at hello directory level</span></span>
<span data-ttu-id="1bb5c-183">Bu adımları tooall Office grupları hello dizininde geçerli olan ayarları dizin düzeyinde okuyun.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-183">These steps read settings at directory level, which apply tooall Office groups in hello directory.</span></span>

1. <span data-ttu-id="1bb5c-184">Tüm mevcut directory ayarları okuyun:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="1bb5c-185">Bu cmdlet, tüm dizin ayarları listesini döndürür:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="1bb5c-186">Belirli bir grup için tüm ayarların okuyun:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="1bb5c-187">Tüm dizin ayarlarının değerleri ayarları kimliği GUID kullanarak bir özel dizin ayarları nesnesinin okuyun:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="1bb5c-188">Bu cmdlet, belirli bu grup için bu ayarları nesnesinde hello adları ve değerleri döndürür:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-188">This cmdlet returns hello names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="1bb5c-189">Belirli bir grup için güncelleştirme ayarları</span><span class="sxs-lookup"><span data-stu-id="1bb5c-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="1bb5c-190">"Groups.Unified.Guest" adlı hello ayarları şablonu için arama</span><span class="sxs-lookup"><span data-stu-id="1bb5c-190">Search for hello settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="1bb5c-191">Merhaba Groups.Unified.Guest şablonu için başlangıç şablonu nesnesi Al:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-191">Retrieve hello template object for hello Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="1bb5c-192">Merhaba şablondan yeni bir ayar nesnesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-192">Create a new settings object from hello template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="1bb5c-193">Merhaba ayarı gerekli toohello değerini ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-193">Set hello setting toohello required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="1bb5c-194">Yeni bir ayar Hello hello gerekli grup için hello dizini oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-194">Create hello new setting for hello required group in hello directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a><span data-ttu-id="1bb5c-195">Merhaba dizin düzeyinde ayarlarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="1bb5c-195">Update settings at hello directory level</span></span>

<span data-ttu-id="1bb5c-196">Bu adımları dizin düzeyinde tooall Unified gruplar hello dizinde uygulamanızı ayarlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-196">These steps update settings at directory level, which apply tooall Unified groups in hello directory.</span></span> <span data-ttu-id="1bb5c-197">Bu örnekler, dizininizde bir ayar nesnesi bulunmakta varsayar.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="1bb5c-198">Merhaba olan ayar nesnesini bulun:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-198">Find hello existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="1bb5c-199">Güncelleştirme başlangıç değeri:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-199">Update hello value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="1bb5c-200">Merhaba ayarını güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="1bb5c-200">Update hello setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a><span data-ttu-id="1bb5c-201">Merhaba dizin düzeyinde ayarlarını Kaldır</span><span class="sxs-lookup"><span data-stu-id="1bb5c-201">Remove settings at hello directory level</span></span>
<span data-ttu-id="1bb5c-202">Bu adım tooall Office grupları hello dizininde uygulanacak ayarları dizin düzeyinde kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-202">This step removes settings at directory level, which apply tooall Office groups in hello directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="1bb5c-203">Cmdlet'in söz dizimi başvurusu</span><span class="sxs-lookup"><span data-stu-id="1bb5c-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="1bb5c-204">Daha fazla Azure Active Directory PowerShell belgeleri bulabilirsiniz [Azure Active Directory cmdlet'leri](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="1bb5c-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="1bb5c-205">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1bb5c-205">Additional reading</span></span>

* [<span data-ttu-id="1bb5c-206">Azure Active Directory grupları ile erişim tooresources yönetme</span><span class="sxs-lookup"><span data-stu-id="1bb5c-206">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="1bb5c-207">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1bb5c-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
