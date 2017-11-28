---
title: "aaaTroubleshooting karma Azure Active Directory'ye katılmış Windows 10 ve Windows Server 2016 cihazları | Microsoft Docs"
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
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="7b12b-103">Katılmış Windows 10 ve Windows Server 2016 cihazlarda karma Azure Active Directory sorun giderme</span><span class="sxs-lookup"><span data-stu-id="7b12b-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="7b12b-104">Bu konuda geçerli toohello istemcileri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="7b12b-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="7b12b-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="7b12b-105">Windows 10</span></span>
-   <span data-ttu-id="7b12b-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="7b12b-106">Windows Server 2016</span></span>

<span data-ttu-id="7b12b-107">Diğer Windows istemcileri için bkz: [sorun giderme karma Azure Active Directory birleştirilmiş alt düzey aygıtları](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="7b12b-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="7b12b-108">Bu konu, sahibi olduğunuzu varsayar [yapılandırılmış karma Azure Active Directory'ye katılmış cihazları](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello senaryolar:</span><span class="sxs-lookup"><span data-stu-id="7b12b-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="7b12b-109">Cihaz temelli koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="7b12b-109">Device-based conditional access</span></span>

- [<span data-ttu-id="7b12b-110">Kurumsal Dolaşım ayarları</span><span class="sxs-lookup"><span data-stu-id="7b12b-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="7b12b-111">İş İçin Windows Hello</span><span class="sxs-lookup"><span data-stu-id="7b12b-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="7b12b-112">Bu belge, nasıl tooresolve olası sorunları hakkında sorun giderme kılavuzu sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b12b-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 


<span data-ttu-id="7b12b-113">Windows 10 ve Windows Server 2016 için karma Azure Active Directory katılım destekler hello Windows 10 Kasım 2015 güncelleştirmesi ve üstü.</span><span class="sxs-lookup"><span data-stu-id="7b12b-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports hello Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="7b12b-114">Merhaba Yıldönümü güncelleştirme kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="7b12b-114">We recommend using hello Anniversary update.</span></span>

## <a name="step-1-retrieve-hello-join-status"></a><span data-ttu-id="7b12b-115">1. adım: hello birleşim durumu alma</span><span class="sxs-lookup"><span data-stu-id="7b12b-115">Step 1: Retrieve hello join status</span></span> 

<span data-ttu-id="7b12b-116">**tooretrieve hello birleşim durumu:**</span><span class="sxs-lookup"><span data-stu-id="7b12b-116">**tooretrieve hello join status:**</span></span>

1. <span data-ttu-id="7b12b-117">Bir yönetici olarak açın hello komut istemi</span><span class="sxs-lookup"><span data-stu-id="7b12b-117">Open hello command prompt as an administrator</span></span>

2. <span data-ttu-id="7b12b-118">Tür **dsregcmd/Status**</span><span class="sxs-lookup"><span data-stu-id="7b12b-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="7b12b-119">+----------------------------------------------------------------------+
   | Cihaz durumu |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="7b12b-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="7b12b-120">EnterpriseJoined: Cihaz kimliği yok: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 parmak izi: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform şifreleme sağlayıcısı TpmProtected: Evet KeySignTest:: Çalıştır yükseltilmiş tootest gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b12b-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="7b12b-121">IDP: login.windows.net Tenantıd: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/ msitsupp.microsoft.com/oauth2/Token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https:// Portal.Manage-Beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ JoinSrvVersion ==: 1.0 JoinSrvUrl: https:// enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs: enterpriseregistration.Windows.NET DomainJoined: Evet DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="7b12b-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="7b12b-122">+----------------------------------------------------------------------+
   | Kullanıcı durumunu |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="7b12b-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="7b12b-123">WamDefaultAuthority: kuruluşların WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (Azuread'i) AzureAdPrt: Evet</span><span class="sxs-lookup"><span data-stu-id="7b12b-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-hello-join-status"></a><span data-ttu-id="7b12b-124">2. adım: hello birleşim durumu değerlendirin</span><span class="sxs-lookup"><span data-stu-id="7b12b-124">Step 2: Evaluate hello join status</span></span> 

<span data-ttu-id="7b12b-125">Alanları aşağıdaki hello gözden geçirin ve hello beklenen değerler sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="7b12b-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="7b12b-126">AzureAdJoined: Evet</span><span class="sxs-lookup"><span data-stu-id="7b12b-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="7b12b-127">Bu alan hello aygıt ile Azure AD alanına katılıp katılmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7b12b-127">This field indicates whether hello device is joined with Azure AD.</span></span> <span data-ttu-id="7b12b-128">Merhaba değer ise **Hayır**, hello birleştirme tooAzure AD henüz tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="7b12b-128">If hello value is **NO**, hello join tooAzure AD has not completed yet.</span></span> 

<span data-ttu-id="7b12b-129">**Olası nedenler:**</span><span class="sxs-lookup"><span data-stu-id="7b12b-129">**Possible causes:**</span></span>

- <span data-ttu-id="7b12b-130">Bir birleştirme hello bilgisayarın kimlik doğrulaması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="7b12b-130">Authentication of hello computer for a join failed.</span></span>

- <span data-ttu-id="7b12b-131">Merhaba bilgisayar tarafından bulunan hello kuruluşta bir HTTP proxy yok</span><span class="sxs-lookup"><span data-stu-id="7b12b-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="7b12b-132">Merhaba bilgisayar kaydı için Azure AD tooauthenticate veya Azure DRS ulaşamıyor</span><span class="sxs-lookup"><span data-stu-id="7b12b-132">hello computer cannot reach Azure AD tooauthenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="7b12b-133">Merhaba bilgisayar hello kuruluşunuzun iç ağ veya VPN ile doğrudan görüş tooan olmayabilir şirket içi AD etki alanı denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="7b12b-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="7b12b-134">Merhaba bilgisayarda TPM varsa, hatalı durumda olabilir.</span><span class="sxs-lookup"><span data-stu-id="7b12b-134">If hello computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="7b12b-135">Olabilir yetersizliğini hello Hizmetleri'ndeki not ettiğiniz hello belgede daha önce tooverify yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b12b-135">There might be a misconfiguration in hello services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="7b12b-136">Ortak örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7b12b-136">Common examples are:</span></span>

    - <span data-ttu-id="7b12b-137">Federasyon sunucunuz etkin WS-Trust uç nokta yok</span><span class="sxs-lookup"><span data-stu-id="7b12b-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="7b12b-138">Federasyon sunucunuz bilgisayarlardan gelen kimlik doğrulama tümleşik Windows kimlik doğrulaması kullanarak ağınızda izin vermiyor.</span><span class="sxs-lookup"><span data-stu-id="7b12b-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="7b12b-139">Merhaba bilgisayar için ait olduğu hello AD ormanındaki Azure AD'de tooyour doğrulanmış etki alanı adına işaret hizmet bağlantı noktası nesnesi yok</span><span class="sxs-lookup"><span data-stu-id="7b12b-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="7b12b-140">DomainJoined: Evet</span><span class="sxs-lookup"><span data-stu-id="7b12b-140">DomainJoined : YES</span></span>  

<span data-ttu-id="7b12b-141">Bu alan hello aygıt alanına katılmış olup olmadığını tooan Active Directory veya şirket içi gösterir.</span><span class="sxs-lookup"><span data-stu-id="7b12b-141">This field indicates whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="7b12b-142">Merhaba değer ise **Hayır**, hello aygıt, bir karma Azure AD birleştirme gerçekleştiremez.</span><span class="sxs-lookup"><span data-stu-id="7b12b-142">If hello value is **NO**, hello device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="7b12b-143">WorkplaceJoined: Hayır</span><span class="sxs-lookup"><span data-stu-id="7b12b-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="7b12b-144">Bu alan bir kişisel cihaz olarak Azure AD ile Merhaba cihazın kayıtlı olup olmadığını belirtir (olarak işaretlenmiş *çalışma alanına katılmış*).</span><span class="sxs-lookup"><span data-stu-id="7b12b-144">This field indicates whether hello device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="7b12b-145">Bu değer olmalıdır **Hayır** de etki alanına katılmış bir bilgisayar için karma Azure AD alanına.</span><span class="sxs-lookup"><span data-stu-id="7b12b-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="7b12b-146">Merhaba değer ise **Evet**, bir iş veya Okul hesabı önceki toohello tamamlama hello karma Azure AD birleştirme eklendi.</span><span class="sxs-lookup"><span data-stu-id="7b12b-146">If hello value is **YES**, a work or school account was added prior toohello completion of hello hybrid Azure AD join.</span></span> <span data-ttu-id="7b12b-147">Bu durumda, hello hesap hello Yıldönümü güncelleştirme Windows 10 (1607) sürümünü kullanırken göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="7b12b-147">In this case, hello account is ignored when using hello Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="7b12b-148">WamDefaultSet: Evet ve AzureADPrt: Evet</span><span class="sxs-lookup"><span data-stu-id="7b12b-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="7b12b-149">Bu alanların hello kullanıcı başarıyla tooAzure AD doğrulaması olup olmadığını belirtmek toohello aygıtı imzalarken.</span><span class="sxs-lookup"><span data-stu-id="7b12b-149">These fields indicate whether hello user has successfully authenticated tooAzure AD when signing in toohello device.</span></span> <span data-ttu-id="7b12b-150">Merhaba değerler ise **Hayır**, son olabilir:</span><span class="sxs-lookup"><span data-stu-id="7b12b-150">If hello values are **NO**, it could be due:</span></span>

- <span data-ttu-id="7b12b-151">Hatalı depolama anahtar hello aygıt kaydı (KeySignTest yükseltilmiş çalışırken onay hello) ile ilişkili TPM (STK).</span><span class="sxs-lookup"><span data-stu-id="7b12b-151">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="7b12b-152">Alternatif oturum açma kimliği</span><span class="sxs-lookup"><span data-stu-id="7b12b-152">Alternate Login ID</span></span>

- <span data-ttu-id="7b12b-153">HTTP Proxy bulunamadı</span><span class="sxs-lookup"><span data-stu-id="7b12b-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b12b-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7b12b-154">Next steps</span></span>

<span data-ttu-id="7b12b-155">Merhaba soruları için bkz [aygıt yönetimi hakkında SSS](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="7b12b-155">For questions, see hello [device management FAQ](device-management-faq.md)</span></span> 
