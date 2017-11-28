---
title: "aaaTroubleshooting hello otomatik kaydı Azure AD etki alanına katılmış bilgisayarları Windows 10 ve Windows Server 2016 için | Microsoft Docs"
description: "Sorun giderme Hello otomatik kaydı Azure AD etki alanı bilgisayarları Windows 10 ve Windows Server 2016 için katıldı."
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
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="4f653-103">Birleştirilmiş bilgisayarlar tooAzure AD – Windows 10 ve Windows Server 2016 etki alanının otomatik kayıt sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="4f653-103">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="4f653-104">Bu konuda geçerli toohello istemcileri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="4f653-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="4f653-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="4f653-105">Windows 10</span></span>
-   <span data-ttu-id="4f653-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="4f653-106">Windows Server 2016</span></span>

<span data-ttu-id="4f653-107">Diğer Windows istemcileri için bkz: [Windows alt düzey istemciler için birleştirilmiş bilgisayarlar tooAzure AD otomatik kaydı etki alanının sorun giderme](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="4f653-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="4f653-108">Bu konu, etki alanına katılmış aygıtlar otomatik kaydı nda olarak açıklanan yapılandırmış olduğunuz varsayılır, [nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile](active-directory-device-registration-get-started.md) Aşağıdaki senaryolar toosupport hello:</span><span class="sxs-lookup"><span data-stu-id="4f653-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello following scenarios:</span></span>

- [<span data-ttu-id="4f653-109">Cihaz temelli koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="4f653-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="4f653-110">Kurumsal Dolaşım ayarları</span><span class="sxs-lookup"><span data-stu-id="4f653-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="4f653-111">İş İçin Windows Hello</span><span class="sxs-lookup"><span data-stu-id="4f653-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="4f653-112">Bu belge, nasıl tooresolve olası sorunları hakkında sorun giderme kılavuzu sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f653-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 

<span data-ttu-id="4f653-113">Merhaba kayıt hello Windows'da desteklenen 10 Kasım 2015 güncelleştirmesi ve üstü.</span><span class="sxs-lookup"><span data-stu-id="4f653-113">hello registration is supported in hello Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="4f653-114">Yukarıdaki hello senaryoları etkinleştirmek için hello Yıldönümü güncelleştirme kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="4f653-114">We recommend using hello Anniversary Update for enabling hello scenarios above.</span></span>

## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="4f653-115">1. adım: hello kayıt durumunu alma</span><span class="sxs-lookup"><span data-stu-id="4f653-115">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="4f653-116">**tooretrieve hello kayıt durumu:**</span><span class="sxs-lookup"><span data-stu-id="4f653-116">**tooretrieve hello registration status:**</span></span>

1. <span data-ttu-id="4f653-117">Merhaba komut istemini yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="4f653-117">Open hello command prompt as an administrator.</span></span>

2. <span data-ttu-id="4f653-118">Tür **dsregcmd/Status**</span><span class="sxs-lookup"><span data-stu-id="4f653-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="4f653-119">+----------------------------------------------------------------------+
   | Cihaz durumu |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="4f653-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="4f653-120">EnterpriseJoined: Cihaz kimliği yok: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 parmak izi: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform şifreleme sağlayıcısı TpmProtected: Evet KeySignTest:: Çalıştır yükseltilmiş tootest gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f653-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="4f653-121">IDP: login.windows.net Tenantıd: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ JoinSrvVersion ==: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: Evet DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="4f653-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="4f653-122">+----------------------------------------------------------------------+
   | Kullanıcı durumunu |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="4f653-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="4f653-123">WamDefaultAuthority: kuruluşların WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (Azuread'i) AzureAdPrt: Evet</span><span class="sxs-lookup"><span data-stu-id="4f653-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="4f653-124">2. adım: hello kayıt durumunu değerlendirme</span><span class="sxs-lookup"><span data-stu-id="4f653-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="4f653-125">Alanları aşağıdaki hello gözden geçirin ve hello beklenen değerler sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="4f653-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="4f653-126">AzureAdJoined: Evet</span><span class="sxs-lookup"><span data-stu-id="4f653-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="4f653-127">Bu alan, Azure AD ile Merhaba cihazın kayıtlı olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4f653-127">This field shows whether hello device is registered with Azure AD.</span></span> <span data-ttu-id="4f653-128">Merhaba değeri 'Hayır' gösteriliyorsa, kayıt tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="4f653-128">If hello value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="4f653-129">**Olası nedenler:**</span><span class="sxs-lookup"><span data-stu-id="4f653-129">**Possible causes:**</span></span>

- <span data-ttu-id="4f653-130">Merhaba bilgisayarın kayıt için kimlik doğrulaması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="4f653-130">Authentication of hello computer for registration failed.</span></span>

- <span data-ttu-id="4f653-131">Merhaba bilgisayar tarafından bulunan hello kuruluşta bir HTTP proxy yok</span><span class="sxs-lookup"><span data-stu-id="4f653-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="4f653-132">Merhaba bilgisayar kimlik doğrulaması için Azure AD veya Azure DRS kaydı için ulaşamıyor</span><span class="sxs-lookup"><span data-stu-id="4f653-132">hello computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="4f653-133">Merhaba bilgisayar hello kuruluşunuzun iç ağ veya VPN ile doğrudan görüş tooan olmayabilir şirket içi AD etki alanı denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="4f653-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="4f653-134">Merhaba bilgisayarda TPM varsa, hatalı durumda olabilir.</span><span class="sxs-lookup"><span data-stu-id="4f653-134">If hello computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="4f653-135">Olabilir yetersizliğini Hizmetleri'ndeki not ettiğiniz hello belgede daha önce tooverify yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f653-135">There may be a misconfiguration in services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="4f653-136">Ortak örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4f653-136">Common examples are:</span></span>

    - <span data-ttu-id="4f653-137">Federasyon sunucunuz etkin WS-Trust uç nokta yok</span><span class="sxs-lookup"><span data-stu-id="4f653-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="4f653-138">Federasyon sunucunuz bilgisayarlardan gelen kimlik doğrulama tümleşik Windows kimlik doğrulaması kullanarak ağınızda izin vermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="4f653-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="4f653-139">Merhaba bilgisayar için ait olduğu hello AD ormanındaki Azure AD'de tooyour doğrulanmış etki alanı adına işaret hizmet bağlantı noktası nesnesi yok</span><span class="sxs-lookup"><span data-stu-id="4f653-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="4f653-140">DomainJoined: Evet</span><span class="sxs-lookup"><span data-stu-id="4f653-140">DomainJoined : YES</span></span>  

<span data-ttu-id="4f653-141">Bu alan hello aygıt birleştirilmiş tooan şirket içi Active Directory olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4f653-141">This field shows whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="4f653-142">Merhaba değeri olarak gösteriliyorsa **Hayır**, hello aygıt olamaz otomatik kaydını Azure AD ile.</span><span class="sxs-lookup"><span data-stu-id="4f653-142">If hello value shows as **NO**, hello device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="4f653-143">İlk olarak bu hello aygıt birleştirmeler toohello Active Directory, Azure AD ile kaydedebilmek için şirket içi denetleyin.</span><span class="sxs-lookup"><span data-stu-id="4f653-143">Check first that hello device joins toohello on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="4f653-144">Lütfen hello bilgisayar tooAzure AD doğrudan katılmak için arıyorsanız, Azure Active Directory katılım yetenekleriyle ilgili tooLearn gidin.</span><span class="sxs-lookup"><span data-stu-id="4f653-144">If you are looking for joining hello computer tooAzure AD directly, please go tooLearn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="4f653-145">WorkplaceJoined: Hayır</span><span class="sxs-lookup"><span data-stu-id="4f653-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="4f653-146">Bu alan hello aygıt Azure AD ile ancak ('Çalışma alanına katılmış ' işaretli) bir kişisel cihaz olarak kayıtlı olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4f653-146">This field shows whether hello device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="4f653-147">Ancak bu değer, Azure AD ile kayıtlı bir etki alanına katılmış bilgisayar için 'Hayır' göstermesi gerekir, bu anlamına gelir Evet olarak gösteriliyorsa eklenen önceki toohello bilgisayar Tamamlanıyor kaydı bir iş veya Okul hesabı idi.</span><span class="sxs-lookup"><span data-stu-id="4f653-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior toohello computer completing registration.</span></span> <span data-ttu-id="4f653-148">Bu durumda hello hesap hello Yıldönümü güncelleştirme Windows 10 (zaman içinde hello WinVer komutu çalıştıran hello 'Run' veya bir komut istemi penceresinde 1607) sürümünü kullanıyorsanız yoksayılacak.</span><span class="sxs-lookup"><span data-stu-id="4f653-148">In this case hello account will be ignored if using hello Anniversary Update version of Windows 10 (1607 when running hello WinVer command in hello ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="4f653-149">WamDefaultSet: Evet ve AzureADPrt: Evet</span><span class="sxs-lookup"><span data-stu-id="4f653-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="4f653-150">Bu alanlar hello kullanıcı toohello aygıtı imzalama sırasında tooAzure AD başarıyla doğrulaması gösterir.</span><span class="sxs-lookup"><span data-stu-id="4f653-150">These fields show that hello user has successfully authenticated tooAzure AD upon signing in toohello device.</span></span> <span data-ttu-id="4f653-151">Bunlar gösterirse 'Hayır' hello olası nedenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4f653-151">If they show ‘NO’ hello following are possible causes:</span></span>

- <span data-ttu-id="4f653-152">Hatalı depolama anahtar hello aygıt kaydı (KeySignTest yükseltilmiş çalışırken onay hello) ile ilişkili TPM (STK).</span><span class="sxs-lookup"><span data-stu-id="4f653-152">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="4f653-153">Alternatif oturum açma kimliği</span><span class="sxs-lookup"><span data-stu-id="4f653-153">Alternate Login ID</span></span>

- <span data-ttu-id="4f653-154">HTTP Proxy bulunamadı</span><span class="sxs-lookup"><span data-stu-id="4f653-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f653-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4f653-155">Next steps</span></span>

<span data-ttu-id="4f653-156">Daha fazla bilgi için bkz: Merhaba [otomatik cihaz kaydı SSS](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="4f653-156">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
