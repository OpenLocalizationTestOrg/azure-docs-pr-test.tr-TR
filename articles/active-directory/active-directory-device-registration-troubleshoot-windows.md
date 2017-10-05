---
title: "Azure AD etki alanının otomatik kayıt sorunlarını giderme alanına katılmış bilgisayarları Windows 10 ve Windows Server 2016 için | Microsoft Docs"
description: "Azure AD etki alanının otomatik kayıt sorunlarını giderme bilgisayarları Windows 10 ve Windows Server 2016 için katıldı."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 5b7f95f302f716d9221b5fae59aa2df5c956a524
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="ad6b8-103">Azure AD ile – Windows 10 ve Windows Server 2016 alanına katılmamış bilgisayarlar etki alanının otomatik kayıt sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="ad6b8-103">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="ad6b8-104">Bu konu, aşağıdaki istemciler için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="ad6b8-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="ad6b8-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="ad6b8-105">Windows 10</span></span>
-   <span data-ttu-id="ad6b8-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ad6b8-106">Windows Server 2016</span></span>

<span data-ttu-id="ad6b8-107">Diğer Windows istemcileri için bkz: [etki alanının otomatik kaydı sorun giderme bilgisayarları Windows alt düzey istemciler için Azure AD alanına](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="ad6b8-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="ad6b8-108">Bu konu, etki alanına katılmış aygıtlar otomatik kaydı nda olarak açıklanan yapılandırmış olduğunuz varsayılır, [Azure Active Directory ile etki alanına katılmış Windows cihazlarının otomatik kaydını yapılandırma](active-directory-device-registration-get-started.md) aşağıdaki senaryoları desteklemek için:</span><span class="sxs-lookup"><span data-stu-id="ad6b8-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) to support the following scenarios:</span></span>

- [<span data-ttu-id="ad6b8-109">Cihaz temelli koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="ad6b8-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="ad6b8-110">Kurumsal Dolaşım ayarları</span><span class="sxs-lookup"><span data-stu-id="ad6b8-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="ad6b8-111">İş İçin Windows Hello</span><span class="sxs-lookup"><span data-stu-id="ad6b8-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="ad6b8-112">Bu belge hakkında olası sorunları gidermek sorun giderme kılavuzu sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 

<span data-ttu-id="ad6b8-113">Windows kayıt desteklenen 10 Kasım 2015 güncelleştirmesi ve üstü.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-113">The registration is supported in the Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="ad6b8-114">Yukarıdaki senaryoları etkinleştirmek için Yıldönümü güncelleştirme kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-114">We recommend using the Anniversary Update for enabling the scenarios above.</span></span>

## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="ad6b8-115">1. adım: kayıt durumunu alma</span><span class="sxs-lookup"><span data-stu-id="ad6b8-115">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="ad6b8-116">**Kayıt durumunu almak için:**</span><span class="sxs-lookup"><span data-stu-id="ad6b8-116">**To retrieve the registration status:**</span></span>

1. <span data-ttu-id="ad6b8-117">Komut istemini yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-117">Open the command prompt as an administrator.</span></span>

2. <span data-ttu-id="ad6b8-118">Tür **dsregcmd/Status**</span><span class="sxs-lookup"><span data-stu-id="ad6b8-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="ad6b8-119">+----------------------------------------------------------------------+
   | Cihaz durumu |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="ad6b8-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="ad6b8-120">EnterpriseJoined: Cihaz kimliği yok: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 parmak izi: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platformu Crypto sağlayıcısı TpmProtected: Evet KeySignTest:: test etmek için yükseltilmiş çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="ad6b8-121">IDP: login.windows.net Tenantıd: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ JoinSrvVersion ==: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: Evet DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="ad6b8-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="ad6b8-122">+----------------------------------------------------------------------+
   | Kullanıcı durumunu |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="ad6b8-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="ad6b8-123">WamDefaultAuthority: kuruluşların WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (Azuread'i) AzureAdPrt: Evet</span><span class="sxs-lookup"><span data-stu-id="ad6b8-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="ad6b8-124">2. adım: kayıt durumunu değerlendirme</span><span class="sxs-lookup"><span data-stu-id="ad6b8-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="ad6b8-125">Aşağıdaki alanları gözden geçirin ve beklenen değerleri sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="ad6b8-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="ad6b8-126">AzureAdJoined: Evet</span><span class="sxs-lookup"><span data-stu-id="ad6b8-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="ad6b8-127">Bu alan, Azure AD ile cihazın kayıtlı olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-127">This field shows whether the device is registered with Azure AD.</span></span> <span data-ttu-id="ad6b8-128">Değer 'Hayır' gösteriliyorsa, kayıt tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-128">If the value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="ad6b8-129">**Olası nedenler:**</span><span class="sxs-lookup"><span data-stu-id="ad6b8-129">**Possible causes:**</span></span>

- <span data-ttu-id="ad6b8-130">Kayıt bilgisayarın kimlik doğrulaması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-130">Authentication of the computer for registration failed.</span></span>

- <span data-ttu-id="ad6b8-131">Bilgisayar tarafından bulunan kuruluştaki bir HTTP proxy yok</span><span class="sxs-lookup"><span data-stu-id="ad6b8-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="ad6b8-132">Bilgisayar kimlik doğrulaması için Azure AD veya Azure DRS kaydı için ulaşamıyor</span><span class="sxs-lookup"><span data-stu-id="ad6b8-132">The computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="ad6b8-133">Bilgisayar VPN veya kuruluşunuzun iç ağ üzerinde doğrudan görüş bir şirket içi ile olmayabilir AD etki alanı denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="ad6b8-134">Bilgisayar bir TPM varsa, hatalı durumda olabilir.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-134">If the computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="ad6b8-135">Olabilir yetersizliğini Hizmetleri'ndeki not ettiğiniz belgede daha önce yeniden doğrulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-135">There may be a misconfiguration in services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="ad6b8-136">Ortak örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ad6b8-136">Common examples are:</span></span>

    - <span data-ttu-id="ad6b8-137">Federasyon sunucunuz etkin WS-Trust uç nokta yok</span><span class="sxs-lookup"><span data-stu-id="ad6b8-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="ad6b8-138">Federasyon sunucunuz bilgisayarlardan gelen kimlik doğrulama tümleşik Windows kimlik doğrulaması kullanarak ağınızda izin vermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="ad6b8-139">Bilgisayar için ait olduğu AD ormanında Azure AD'de doğrulanmış etki alanı adınızı işaret hizmet bağlantı noktası nesnesi yok</span><span class="sxs-lookup"><span data-stu-id="ad6b8-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="ad6b8-140">DomainJoined: Evet</span><span class="sxs-lookup"><span data-stu-id="ad6b8-140">DomainJoined : YES</span></span>  

<span data-ttu-id="ad6b8-141">Bu alan, cihaz bir şirket içi Active Directory veya alanına katılıp katılmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-141">This field shows whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="ad6b8-142">Değer olarak gösteriliyorsa **Hayır**, aygıt otomatik-Azure AD ile kayıt olamaz.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-142">If the value shows as **NO**, the device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="ad6b8-143">İlk olarak Azure AD ile kaydedebilmek için şirket içi Active Directory cihaz birleştirir denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-143">Check first that the device joins to the on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="ad6b8-144">Lütfen doğrudan Azure AD ile bilgisayarın katılmasını istiyorsanız, Azure Active Directory katılım yeteneklerini hakkında edinin gidin.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-144">If you are looking for joining the computer to Azure AD directly, please go to Learn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="ad6b8-145">WorkplaceJoined: Hayır</span><span class="sxs-lookup"><span data-stu-id="ad6b8-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="ad6b8-146">Bu alan, aygıt Azure AD ile ancak ('Çalışma alanına katılmış ' işaretli) bir kişisel cihaz olarak kayıtlı olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-146">This field shows whether the device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="ad6b8-147">Bu değer, Azure AD ile kayıtlı bir etki alanına katılmış bilgisayar için 'Hayır' göstermesi gerekir, Evet olarak görünüyorsa ancak bu bir iş veya Okul hesabı kayıt Tamamlanıyor bilgisayar önce eklendiğini anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior to the computer completing registration.</span></span> <span data-ttu-id="ad6b8-148">Bu durumda hesaba Windows 10 (zaman WinVer çalışan komut 'Çalışma' veya bir komut istemi penceresinde 1607) Yıldönümü güncelleştirme sürümünü kullanıyorsanız yoksayılacak.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-148">In this case the account will be ignored if using the Anniversary Update version of Windows 10 (1607 when running the WinVer command in the ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="ad6b8-149">WamDefaultSet: Evet ve AzureADPrt: Evet</span><span class="sxs-lookup"><span data-stu-id="ad6b8-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="ad6b8-150">Bu alanlar cihaza oturum açtıktan sonra Azure ad kullanıcı başarıyla kimliğini doğrulamasından gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad6b8-150">These fields show that the user has successfully authenticated to Azure AD upon signing in to the device.</span></span> <span data-ttu-id="ad6b8-151">Olası nedenler şunlardır gösterdikleri 'Hayır' ise:</span><span class="sxs-lookup"><span data-stu-id="ad6b8-151">If they show ‘NO’ the following are possible causes:</span></span>

- <span data-ttu-id="ad6b8-152">Hatalı depolama anahtar aygıt kaydı (denetimi yükseltilmiş çalışırken KeySignTest) ile ilişkili TPM (STK).</span><span class="sxs-lookup"><span data-stu-id="ad6b8-152">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="ad6b8-153">Alternatif oturum açma kimliği</span><span class="sxs-lookup"><span data-stu-id="ad6b8-153">Alternate Login ID</span></span>

- <span data-ttu-id="ad6b8-154">HTTP Proxy bulunamadı</span><span class="sxs-lookup"><span data-stu-id="ad6b8-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad6b8-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ad6b8-155">Next steps</span></span>

<span data-ttu-id="ad6b8-156">Daha fazla bilgi için bkz: [otomatik cihaz kaydı SSS](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="ad6b8-156">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 