---
title: "aaaAzure AD Connect eşitleme hizmet özellikleri ve yapılandırma | Microsoft Docs"
description: "Azure AD Connect eşitleme hizmeti için hizmet tarafı özelliklerini açıklar."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="3a7e1-103">Azure AD Connect eşitleme hizmeti özellikleri</span><span class="sxs-lookup"><span data-stu-id="3a7e1-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="3a7e1-104">Azure AD Connect eşitleme özelliği Hello iki bileşenden oluşur:</span><span class="sxs-lookup"><span data-stu-id="3a7e1-104">hello synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="3a7e1-105">adlı hello şirket içi bileşeni **Azure AD Connect eşitleme**, olarak da bilinir **eşitleme altyapısı**.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-105">hello on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="3a7e1-106">Azure AD'de olarak da bilinen bulunan hello hizmet **Azure AD Connect eşitleme hizmeti**</span><span class="sxs-lookup"><span data-stu-id="3a7e1-106">hello service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="3a7e1-107">Bu konuda aşağıdaki hello nasıl özellikleri açıklanmaktadır Merhaba, **Azure AD Connect eşitleme hizmeti** çalışma ve bunları Windows PowerShell kullanarak nasıl yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-107">This topic explains how hello following features of hello **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="3a7e1-108">Bu ayarları hello tarafından yapılandırılan [Azure Active Directory için Windows PowerShell Modülü](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="3a7e1-108">These settings are configured by hello [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="3a7e1-109">İndirin ve Azure AD Connect'ten ayrı olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="3a7e1-110">Bu konudaki belgelenen hello cmdlet'leri hello sunuldu [2016 Mart sürümünden (yapı 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="3a7e1-110">hello cmdlets documented in this topic were introduced in hello [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="3a7e1-111">Bu konudaki belgelenen hello cmdlet'leri varsa değil veya aynı sonucu sonra emin olun hello oluşturmaya hello en son sürümünü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-111">If you do not have hello cmdlets documented in this topic or they do not produce hello same result, then make sure you run hello latest version.</span></span>

<span data-ttu-id="3a7e1-112">toosee hello çalıştırmak Azure AD dizininizi yapılandırmasında `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-112">toosee hello configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="3a7e1-113">![Get-MsolDirSyncFeatures sonucu](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="3a7e1-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="3a7e1-114">Bu ayarların çoğu, yalnızca Azure AD Connect tarafından değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="3a7e1-115">Merhaba aşağıdaki ayarları tarafından yapılandırılabilir `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="3a7e1-115">hello following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="3a7e1-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="3a7e1-116">DirSyncFeature</span></span> | <span data-ttu-id="3a7e1-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a7e1-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="3a7e1-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="3a7e1-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="3a7e1-119">Nesneleri toojoin toplama tooprimary SMTP adresi userPrincipalName olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-119">Allows objects toojoin on userPrincipalName in addition tooprimary SMTP address.</span></span> |
| [<span data-ttu-id="3a7e1-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="3a7e1-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="3a7e1-121">Merhaba eşitleme altyapısı tooupdate hello userPrincipalName özniteliği, yönetilen ve lisanslı (Federasyon olmayan) kullanıcılar için sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-121">Allows hello sync engine tooupdate hello userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="3a7e1-122">Bir özellik etkinleştirdikten sonra onu yeniden devre dışı bırakılamaz.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="3a7e1-123">Özellik 24 Ağustos 2016'dan hello *yinelenen öznitelik dayanıklılık* yeni Azure için varsayılan olarak etkin AD dizinleri.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-123">From August 24, 2016 hello feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="3a7e1-124">Bu özellik ayrıca alındı ve olması bu tarihten önce oluşturulan dizinleri etkin.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="3a7e1-125">Dizininizi hakkında tooget bu özelliği etkin olduğunda, bir e-posta bildirimi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-125">You will receive an email notification when your directory is about tooget this feature enabled.</span></span>
> 
> 

<span data-ttu-id="3a7e1-126">Merhaba aşağıdaki ayarları Azure AD Connect tarafından yapılandırılır ve tarafından değiştirilemez `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="3a7e1-126">hello following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="3a7e1-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="3a7e1-127">DirSyncFeature</span></span> | <span data-ttu-id="3a7e1-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a7e1-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="3a7e1-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="3a7e1-129">DeviceWriteback</span></span> |[<span data-ttu-id="3a7e1-130">Azure AD Connect: cihaz geri yazma özelliğini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3a7e1-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="3a7e1-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="3a7e1-131">DirectoryExtensions</span></span> |[<span data-ttu-id="3a7e1-132">Azure AD Connect eşitleme: dizin uzantıları</span><span class="sxs-lookup"><span data-stu-id="3a7e1-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="3a7e1-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="3a7e1-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="3a7e1-134">Dışa aktarma sırasında hello nesnenin tamamı başarısız yerine başka bir nesnenin yinelemesi karantinaya bir öznitelik toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-134">Allows an attribute toobe quarantined when it is a duplicate of another object rather than failing hello entire object during export.</span></span> |
| <span data-ttu-id="3a7e1-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="3a7e1-135">PasswordSync</span></span> |[<span data-ttu-id="3a7e1-136">Parola Eşitleme ile Azure AD Connect eşitleme uygulama</span><span class="sxs-lookup"><span data-stu-id="3a7e1-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="3a7e1-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="3a7e1-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="3a7e1-138">Önizleme: Grup geri yazma</span><span class="sxs-lookup"><span data-stu-id="3a7e1-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="3a7e1-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="3a7e1-139">UserWriteback</span></span> |<span data-ttu-id="3a7e1-140">Şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="3a7e1-141">Yinelenen öznitelik dayanıklılık</span><span class="sxs-lookup"><span data-stu-id="3a7e1-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="3a7e1-142">Yinelenen UPN ile tooprovision başarısız yerine nesneleri / proxyAddresses, hello yinelenen öznitelik "karantinaya" ve geçici bir değeri atanır.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-142">Instead of failing tooprovision objects with duplicate UPNs / proxyAddresses, hello duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="3a7e1-143">Merhaba çakışma giderildikten sonra UPN hello geçici olan toohello doğru değer otomatik olarak değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-143">When hello conflict is resolved, hello temporary UPN is changed toohello proper value automatically.</span></span> <span data-ttu-id="3a7e1-144">Daha fazla ayrıntı için bkz: [kimlik eşitleme ve yinelenen öznitelik dayanıklılık](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="3a7e1-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="3a7e1-145">UserPrincipalName yumuşak eşleşmiyor</span><span class="sxs-lookup"><span data-stu-id="3a7e1-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="3a7e1-146">Bu özellik etkinleştirildiğinde, soft-match toplama toohello için UPN etkin [birincil SMTP adresi](https://support.microsoft.com/kb/2641663), her zaman etkin.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-146">When this feature is enabled, soft-match is enabled for UPN in addition toohello [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="3a7e1-147">Soft-kullanılan toomatch mevcut bulut kullanıcıları şirket içi kullanıcıları Azure AD'de eşleşmedir.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-147">Soft-match is used toomatch existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="3a7e1-148">Gerekirse toomatch AD hesaplarıyla hello bulutta oluşturulan mevcut şirket içi ve Exchange Online kullanmıyorsanız, sonra bu özellik yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-148">If you need toomatch on-premises AD accounts with existing accounts created in hello cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="3a7e1-149">Bu senaryoda, genellikle hello bulutta bir nedenle tooset hello SMTP özniteliği yok.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-149">In this scenario, you generally don’t have a reason tooset hello SMTP attribute in hello cloud.</span></span>

<span data-ttu-id="3a7e1-150">Bu özellik için varsayılan olarak yeni Azure AD dizinlerinden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="3a7e1-151">Bu özellik, çalıştırarak etkin olup olmadığını görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3a7e1-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="3a7e1-152">Bu özellik, Azure AD dizini için etkin değilse, ardından onu çalıştırarak etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3a7e1-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="3a7e1-153">UserPrincipalName güncelleştirmelerini eşitleme</span><span class="sxs-lookup"><span data-stu-id="3a7e1-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="3a7e1-154">Bu koşulların her ikisi de doğruysa sürece tarihsel olarak, şirket içi hello eşitleme hizmeti kullanarak güncelleştirmeleri toohello UserPrincipalName özniteliği, engellendi:</span><span class="sxs-lookup"><span data-stu-id="3a7e1-154">Historically, updates toohello UserPrincipalName attribute using hello sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="3a7e1-155">Merhaba kullanıcı (Federasyon olmayan) yönetilir.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-155">hello user is managed (non-federated).</span></span>
* <span data-ttu-id="3a7e1-156">Merhaba kullanıcı bir lisans atanmadı.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-156">hello user has not been assigned a license.</span></span>

<span data-ttu-id="3a7e1-157">Daha fazla ayrıntı için bkz: [kullanıcı Office 365, Azure veya Intune adları eşleşmiyor hello şirket içi UPN veya alternatif oturum açma kimliği](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="3a7e1-157">For more details, see [User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="3a7e1-158">Bu özelliği etkinleştirmek, değiştirilen şirket içi olduğunda ve Parola Eşitleme'yi kullanmaya hello eşitleme altyapısı tooupdate hello userPrincipalName sağlar. Federasyon kullanırsanız, bu özellik desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-158">Enabling this feature allows hello sync engine tooupdate hello userPrincipalName when it is changed on-premises and you use password sync. If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="3a7e1-159">Bu özellik için varsayılan olarak yeni Azure AD dizinlerinden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-159">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="3a7e1-160">Bu özellik, çalıştırarak etkin olup olmadığını görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3a7e1-160">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="3a7e1-161">Bu özellik, Azure AD dizini için etkin değilse, ardından onu çalıştırarak etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3a7e1-161">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="3a7e1-162">Bu özellik etkinleştirildikten sonra varolan userPrincipalName değerleri olarak kalır-değil.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-162">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="3a7e1-163">Merhaba userPrincipalName özniteliği şirket içi sonraki değişiminde hello normal delta eşitleme kullanıcıları hello UPN güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-163">On next change of hello userPrincipalName attribute on-premises, hello normal delta sync on users will update hello UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="3a7e1-164">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="3a7e1-164">See also</span></span>
* [<span data-ttu-id="3a7e1-165">Azure AD Connect eşitleme</span><span class="sxs-lookup"><span data-stu-id="3a7e1-165">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="3a7e1-166">[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="3a7e1-166">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

