---
title: "Karma Azure Active Directory sorun giderme alanına katılmış Windows 10 ve Windows Server 2016 cihazları | Microsoft Docs"
description: "Karma Azure Active Directory sorun giderme Windows 10 ve Windows Server 2016 cihazları katıldı."
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 51962c14a3c32bbfa9a613fa203cc48cfea50c0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="2a2db-103">Katılmış Windows 10 ve Windows Server 2016 cihazlarda karma Azure Active Directory sorun giderme</span><span class="sxs-lookup"><span data-stu-id="2a2db-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="2a2db-104">Bu konu, aşağıdaki istemciler için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="2a2db-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="2a2db-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="2a2db-105">Windows 10</span></span>
-   <span data-ttu-id="2a2db-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2a2db-106">Windows Server 2016</span></span>

<span data-ttu-id="2a2db-107">Diğer Windows istemcileri için bkz: [sorun giderme karma Azure Active Directory birleştirilmiş alt düzey aygıtları](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="2a2db-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="2a2db-108">Bu konu, sahibi olduğunuzu varsayar [yapılandırılmış karma Azure Active Directory'ye katılmış cihazları](device-management-hybrid-azuread-joined-devices-setup.md) aşağıdaki senaryoları desteklemek için:</span><span class="sxs-lookup"><span data-stu-id="2a2db-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) to support the following scenarios:</span></span>

- <span data-ttu-id="2a2db-109">Cihaz temelli koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="2a2db-109">Device-based conditional access</span></span>

- [<span data-ttu-id="2a2db-110">Kurumsal Dolaşım ayarları</span><span class="sxs-lookup"><span data-stu-id="2a2db-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="2a2db-111">İş İçin Windows Hello</span><span class="sxs-lookup"><span data-stu-id="2a2db-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="2a2db-112">Bu belge hakkında olası sorunları gidermek sorun giderme kılavuzu sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a2db-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 


<span data-ttu-id="2a2db-113">Windows 10 ve Windows Server 2016, karma Azure Active Directory katılım desteklediği için Windows 10 Kasım 2015 güncelleştirme ve üstü.</span><span class="sxs-lookup"><span data-stu-id="2a2db-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports the Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="2a2db-114">Yıldönümü güncelleştirme kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2a2db-114">We recommend using the Anniversary update.</span></span>

## <a name="step-1-retrieve-the-join-status"></a><span data-ttu-id="2a2db-115">1. adım: katılım durumunu alma</span><span class="sxs-lookup"><span data-stu-id="2a2db-115">Step 1: Retrieve the join status</span></span> 

<span data-ttu-id="2a2db-116">**Birleşim durumunu almak için:**</span><span class="sxs-lookup"><span data-stu-id="2a2db-116">**To retrieve the join status:**</span></span>

1. <span data-ttu-id="2a2db-117">Komut istemini yönetici olarak açın</span><span class="sxs-lookup"><span data-stu-id="2a2db-117">Open the command prompt as an administrator</span></span>

2. <span data-ttu-id="2a2db-118">Tür **dsregcmd/Status**</span><span class="sxs-lookup"><span data-stu-id="2a2db-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="2a2db-119">+----------------------------------------------------------------------+
   | Cihaz durumu |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="2a2db-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="2a2db-120">EnterpriseJoined: Cihaz kimliği yok: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 parmak izi: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform şifreleme sağlayıcısı TpmProtected: Evet KeySignTest:: test etmek için yükseltilmiş çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a2db-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="2a2db-121">IDP: login.windows.net Tenantıd: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/ msitsupp.microsoft.com/oauth2/Token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https:// Portal.Manage-Beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ JoinSrvVersion ==: 1.0 JoinSrvUrl: https:// enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs: enterpriseregistration.Windows.NET DomainJoined: Evet DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="2a2db-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="2a2db-122">+----------------------------------------------------------------------+
   | Kullanıcı durumunu |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="2a2db-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="2a2db-123">WamDefaultAuthority: kuruluşların WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (Azuread'i) AzureAdPrt: Evet</span><span class="sxs-lookup"><span data-stu-id="2a2db-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-the-join-status"></a><span data-ttu-id="2a2db-124">2. adım: katılım durumunu değerlendirme</span><span class="sxs-lookup"><span data-stu-id="2a2db-124">Step 2: Evaluate the join status</span></span> 

<span data-ttu-id="2a2db-125">Aşağıdaki alanları gözden geçirin ve beklenen değerleri sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="2a2db-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="2a2db-126">AzureAdJoined: Evet</span><span class="sxs-lookup"><span data-stu-id="2a2db-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="2a2db-127">Bu alan, Azure AD ile cihaz katıldığından olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="2a2db-127">This field indicates whether the device is joined with Azure AD.</span></span> <span data-ttu-id="2a2db-128">Değer ise **Hayır**, Azure ad birleştirme henüz tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="2a2db-128">If the value is **NO**, the join to Azure AD has not completed yet.</span></span> 

<span data-ttu-id="2a2db-129">**Olası nedenler:**</span><span class="sxs-lookup"><span data-stu-id="2a2db-129">**Possible causes:**</span></span>

- <span data-ttu-id="2a2db-130">Bilgisayar bir birleştirme için kimlik doğrulaması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="2a2db-130">Authentication of the computer for a join failed.</span></span>

- <span data-ttu-id="2a2db-131">Bilgisayar tarafından bulunan kuruluştaki bir HTTP proxy yok</span><span class="sxs-lookup"><span data-stu-id="2a2db-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="2a2db-132">Bilgisayar kimlik doğrulaması için Azure AD alanına erişilemiyor veya kayıt için Azure DRS</span><span class="sxs-lookup"><span data-stu-id="2a2db-132">The computer cannot reach Azure AD to authenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="2a2db-133">Bilgisayar VPN veya kuruluşunuzun iç ağ üzerinde doğrudan görüş bir şirket içi ile olmayabilir AD etki alanı denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="2a2db-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="2a2db-134">Bilgisayar bir TPM varsa, hatalı durumda olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2db-134">If the computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="2a2db-135">Olabilir yetersizliğini hizmetlerinde not ettiğiniz belgede daha önce yeniden doğrulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a2db-135">There might be a misconfiguration in the services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="2a2db-136">Ortak örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2a2db-136">Common examples are:</span></span>

    - <span data-ttu-id="2a2db-137">Federasyon sunucunuz etkin WS-Trust uç nokta yok</span><span class="sxs-lookup"><span data-stu-id="2a2db-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="2a2db-138">Federasyon sunucunuz bilgisayarlardan gelen kimlik doğrulama tümleşik Windows kimlik doğrulaması kullanarak ağınızda izin vermiyor.</span><span class="sxs-lookup"><span data-stu-id="2a2db-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="2a2db-139">Bilgisayar için ait olduğu AD ormanında Azure AD'de doğrulanmış etki alanı adınızı işaret hizmet bağlantı noktası nesnesi yok</span><span class="sxs-lookup"><span data-stu-id="2a2db-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="2a2db-140">DomainJoined: Evet</span><span class="sxs-lookup"><span data-stu-id="2a2db-140">DomainJoined : YES</span></span>  

<span data-ttu-id="2a2db-141">Bu alan, cihaz bir şirket içi Active Directory veya alanına katılıp katılmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="2a2db-141">This field indicates whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="2a2db-142">Değer ise **Hayır**, cihaz bir karma Azure AD birleştirme işlemi gerçekleştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a2db-142">If the value is **NO**, the device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="2a2db-143">WorkplaceJoined: Hayır</span><span class="sxs-lookup"><span data-stu-id="2a2db-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="2a2db-144">Bu alan, bir kişisel cihaz olarak Azure AD ile cihazın kayıtlı olup olmadığını gösterir (olarak işaretlenmiş *çalışma alanına katılmış*).</span><span class="sxs-lookup"><span data-stu-id="2a2db-144">This field indicates whether the device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="2a2db-145">Bu değer olmalıdır **Hayır** de etki alanına katılmış bir bilgisayar için karma Azure AD alanına.</span><span class="sxs-lookup"><span data-stu-id="2a2db-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="2a2db-146">Değer ise **Evet**, karma Azure AD birleştirme tamamlanmadan önce bir iş veya Okul hesabı eklendi.</span><span class="sxs-lookup"><span data-stu-id="2a2db-146">If the value is **YES**, a work or school account was added prior to the completion of the hybrid Azure AD join.</span></span> <span data-ttu-id="2a2db-147">Bu durumda, hesap, Windows 10 (1607) Yıldönümü güncelleştirme sürümünü kullanırken dikkate alınmaz.</span><span class="sxs-lookup"><span data-stu-id="2a2db-147">In this case, the account is ignored when using the Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="2a2db-148">WamDefaultSet: Evet ve AzureADPrt: Evet</span><span class="sxs-lookup"><span data-stu-id="2a2db-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="2a2db-149">Bu alanlar kullanıcının Azure AD ile başarıyla kimliğinin olup olmadığını belirtmek için aygıt oturum açarken.</span><span class="sxs-lookup"><span data-stu-id="2a2db-149">These fields indicate whether the user has successfully authenticated to Azure AD when signing in to the device.</span></span> <span data-ttu-id="2a2db-150">Değerler ise **Hayır**, son olabilir:</span><span class="sxs-lookup"><span data-stu-id="2a2db-150">If the values are **NO**, it could be due:</span></span>

- <span data-ttu-id="2a2db-151">Hatalı depolama anahtar aygıt kaydı (denetimi yükseltilmiş çalışırken KeySignTest) ile ilişkili TPM (STK).</span><span class="sxs-lookup"><span data-stu-id="2a2db-151">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="2a2db-152">Alternatif oturum açma kimliği</span><span class="sxs-lookup"><span data-stu-id="2a2db-152">Alternate Login ID</span></span>

- <span data-ttu-id="2a2db-153">HTTP Proxy bulunamadı</span><span class="sxs-lookup"><span data-stu-id="2a2db-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a2db-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a2db-154">Next steps</span></span>

<span data-ttu-id="2a2db-155">Soruları için bkz: [aygıt yönetimi hakkında SSS](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="2a2db-155">For questions, see the [device management FAQ](device-management-faq.md)</span></span> 