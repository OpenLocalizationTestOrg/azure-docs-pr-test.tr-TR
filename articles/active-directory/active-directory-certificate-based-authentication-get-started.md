---
title: "Active Directory Sertifika tabanlı kimlik doğrulaması - aaaAzure Başlarken | Microsoft Docs"
description: "Bilgi nasıl ortamınızdaki tooconfigure sertifika tabanlı kimlik doğrulaması"
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="71789-103">Azure Active Directory'de sertifika tabanlı kimlik doğrulaması kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="71789-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="71789-104">Sertifika tabanlı kimlik doğrulaması Azure Active Directory tarafından Windows, Android veya iOS aygıtında bir istemci sertifikası ile Exchange online hesabınızı bağlanırken kimlik doğrulaması toobe sağlar:</span><span class="sxs-lookup"><span data-stu-id="71789-104">Certificate-based authentication enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="71789-105">Microsoft Outlook ve Microsoft Word gibi Office mobil uygulamaları</span><span class="sxs-lookup"><span data-stu-id="71789-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="71789-106">Exchange ActiveSync (EAS) istemcileri</span><span class="sxs-lookup"><span data-stu-id="71789-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="71789-107">Bu özelliği yapılandıran hello gerek tooenter bir kullanıcı adı ve parola birleşimi belirli mail ve Microsoft Office uygulamaları, mobil Cihazınızda içine ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="71789-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="71789-108">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="71789-108">This topic:</span></span>

- <span data-ttu-id="71789-109">Merhaba sizinle tooconfigure adımları ve sertifika tabanlı kimlik doğrulaması kullanıcıları için Office 365 Kurumsal, iş, eğitim kiracılar kullanma ve US Government planları sağlar.</span><span class="sxs-lookup"><span data-stu-id="71789-109">Provides you with hello steps tooconfigure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="71789-110">Bu özellik, Office 365 Çin'de, US Government savunma ve US Government Federal planlarda Önizleme'de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="71789-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="71789-111">Zaten sahip olduğunuz varsayılmaktadır bir [ortak anahtar altyapısı (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) ve [AD FS](connect/active-directory-aadconnectfed-whatis.md) yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="71789-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="71789-112">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="71789-112">Requirements</span></span>

<span data-ttu-id="71789-113">tooconfigure sertifika tabanlı kimlik doğrulaması, hello aşağıdakilerin doğru olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="71789-113">tooconfigure certificate-based authentication, hello following must be true:</span></span>  

- <span data-ttu-id="71789-114">Sertifika tabanlı kimlik doğrulaması (CBA), yalnızca tarayıcı uygulamalarında veya modern kimlik doğrulaması (ADAL) kullanarak yerel istemciler için federe ortamlar için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="71789-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="71789-115">Merhaba tek özel durum Exchange ActiveSync (EAS), Federal hem yönetilen hesapları için kullanılabilecek EXO için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="71789-115">hello one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="71789-116">Azure Active Directory'de Hello kök sertifika yetkilisini ve ara sertifika yetkilileri yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="71789-116">hello root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="71789-117">Her sertifika yetkilisi URL Internet'e yönelik başvurulan bir sertifika iptal listesini (CRL) olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="71789-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="71789-118">Azure Active Directory içinde yapılandırılan en az bir sertifika yetkilisine sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="71789-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="71789-119">Hello ilgili adımları bulabilirsiniz [hello sertifika yetkililerini](#step-2-configure-the-certificate-authorities) bölümü.</span><span class="sxs-lookup"><span data-stu-id="71789-119">You can find related steps in hello [Configure hello certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="71789-120">Exchange ActiveSync istemcileri için Exchange online ya da hello asıl adı veya adresi hello konu alternatif adı alanında RFC822 adı değerini hello hello kullanıcının yönlendirilebilir e-posta hello istemci sertifikası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="71789-120">For Exchange ActiveSync clients, hello client certificate must have hello user’s routable email address in Exchange online in either hello Principal Name or hello RFC822 Name value of hello Subject Alternative Name field.</span></span> <span data-ttu-id="71789-121">Azure Active Directory hello RFC822 değer toohello Proxy adresi özniteliği hello dizininde eşler.</span><span class="sxs-lookup"><span data-stu-id="71789-121">Azure Active Directory maps hello RFC822 value toohello Proxy Address attribute in hello directory.</span></span>  

- <span data-ttu-id="71789-122">İstemci Cihazınızı istemci sertifikaları veren erişim tooat en az bir sertifika yetkilisi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="71789-122">Your client device must have access tooat least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="71789-123">İstemci kimlik doğrulaması için bir istemci sertifikası tooyour istemci verilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="71789-123">A client certificate for client authentication must have been issued tooyour client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="71789-124">1. adım: cihaz platformunuz seçin</span><span class="sxs-lookup"><span data-stu-id="71789-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="71789-125">İlk adım olarak, verdiğiniz hakkında hello cihaz platformu için tooreview hello aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="71789-125">As a first step, for hello device platform you care about, you need tooreview hello following:</span></span>

- <span data-ttu-id="71789-126">Merhaba Office mobil uygulamaları desteği</span><span class="sxs-lookup"><span data-stu-id="71789-126">hello Office mobile applications support</span></span> 
- <span data-ttu-id="71789-127">Merhaba belirli uygulama gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="71789-127">hello specific implementation requirements</span></span>  

<span data-ttu-id="71789-128">Merhaba, cihaz platformları aşağıdaki hello için bilgi mevcut ilgili:</span><span class="sxs-lookup"><span data-stu-id="71789-128">hello related information exists for hello following device platforms:</span></span>

- [<span data-ttu-id="71789-129">Android</span><span class="sxs-lookup"><span data-stu-id="71789-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="71789-130">iOS</span><span class="sxs-lookup"><span data-stu-id="71789-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a><span data-ttu-id="71789-131">2. adım: hello sertifika yetkililerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="71789-131">Step 2: Configure hello certificate authorities</span></span> 

<span data-ttu-id="71789-132">tooconfigure aşağıdaki hello Azure Active Directory'de her sertifika yetkilisi, sertifika yetkilileri karşıya yükle:</span><span class="sxs-lookup"><span data-stu-id="71789-132">tooconfigure your certificate authorities in Azure Active Directory, for each certificate authority, upload hello following:</span></span> 

* <span data-ttu-id="71789-133">Merhaba hello sertifikasının ortak kısmını *.cer* biçimi</span><span class="sxs-lookup"><span data-stu-id="71789-133">hello public portion of hello certificate, in *.cer* format</span></span> 
* <span data-ttu-id="71789-134">Merhaba URL'leri hello burada Internet'e sertifika iptal listelerinin (CRL'ler) bulunur</span><span class="sxs-lookup"><span data-stu-id="71789-134">hello Internet facing URLs where hello Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="71789-135">bir sertifika yetkilisi için Hello şeması şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="71789-135">hello schema for a certificate authority looks as follows:</span></span> 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

<span data-ttu-id="71789-136">Merhaba yapılandırma için hello kullanabilirsiniz [Azure Active Directory PowerShell sürüm 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="71789-136">For hello configuration, you can use hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="71789-137">Windows PowerShell'i yönetici ayrıcalıklarıyla başlatın.</span><span class="sxs-lookup"><span data-stu-id="71789-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="71789-138">Hello Azure AD modülünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="71789-138">Install hello Azure AD module.</span></span> <span data-ttu-id="71789-139">Tooinstall sürüm gereksinim [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="71789-139">You need tooinstall Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="71789-140">İlk Yapılandırma adım olarak, Kiracı ile tooestablish bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="71789-140">As a first configuration step, you need tooestablish a connection with your tenant.</span></span> <span data-ttu-id="71789-141">Bağlantı tooyour Kiracı var. hemen gözden geçirebilir, eklemek, silmek ve dizininizde tanımlanan hello güvenilen sertifika yetkilileri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="71789-141">As soon as a connection tooyour tenant exists, you can review, add, delete and modify hello trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="71789-142">Bağlan</span><span class="sxs-lookup"><span data-stu-id="71789-142">Connect</span></span>

<span data-ttu-id="71789-143">tooestablish kullanım hello kiracınızın bağlantı [Connect-Azuread'i](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="71789-143">tooestablish a connection with your tenant, use hello [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="71789-144">Alma</span><span class="sxs-lookup"><span data-stu-id="71789-144">Retrieve</span></span> 

<span data-ttu-id="71789-145">dizininizde, tanımlanan tooretrieve hello güvenilen sertifika yetkilileri kullanmak hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="71789-145">tooretrieve hello trusted certificate authorities that are defined in your directory, use hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="71789-146">Ekle</span><span class="sxs-lookup"><span data-stu-id="71789-146">Add</span></span>

<span data-ttu-id="71789-147">toocreate bir güvenilen sertifika yetkilisi kullanma hello [yeni AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet'i ve kümesi hello **crlDistributionPoint** öznitelik tooa doğru değeri:</span><span class="sxs-lookup"><span data-stu-id="71789-147">toocreate a trusted certificate authority, use hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set hello **crlDistributionPoint** attribute tooa correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="71789-148">Kaldır</span><span class="sxs-lookup"><span data-stu-id="71789-148">Remove</span></span>

<span data-ttu-id="71789-149">tooremove bir güvenilen sertifika yetkilisi kullanma hello [Kaldır AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="71789-149">tooremove a trusted certificate authority, use hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="71789-150">Modfiy</span><span class="sxs-lookup"><span data-stu-id="71789-150">Modfiy</span></span>

<span data-ttu-id="71789-151">toomodify bir güvenilen sertifika yetkilisi kullanma hello [kümesi AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="71789-151">toomodify a trusted certificate authority, use hello [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="71789-152">3. adım: iptal yapılandırma</span><span class="sxs-lookup"><span data-stu-id="71789-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="71789-153">bir istemci sertifikası, Azure Active Directory toorevoke hello URL'lerden iptal listesini (CRL) sertifika yetkilisi bilgilerinin bir parçası yüklenen ve önbelleğe alır hello sertifika getirir.</span><span class="sxs-lookup"><span data-stu-id="71789-153">toorevoke a client certificate, Azure Active Directory fetches hello certificate revocation list (CRL) from hello URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="71789-154">Merhaba son zaman damgası yayımlama (**geçerlilik tarihi** özelliği) CRL kullanılır hello içinde tooensure hello CRL hala geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="71789-154">hello last publish timestamp (**Effective Date** property) in hello CRL is used tooensure hello CRL is still valid.</span></span> <span data-ttu-id="71789-155">Merhaba CRL hello listesinin bir parçası olan düzenli aralıklarla başvurulan toorevoke erişim toocertificates ' dir.</span><span class="sxs-lookup"><span data-stu-id="71789-155">hello CRL is periodically referenced toorevoke access toocertificates that are a part of hello list.</span></span>

<span data-ttu-id="71789-156">(Örneğin bir kullanıcının bir cihazı kaybederse) daha hızlı iptali gerekiyorsa, hello kullanıcının hello yetkilendirme belirteci geçersiz hale.</span><span class="sxs-lookup"><span data-stu-id="71789-156">If a more instant revocation is required (for example, if a user loses a device), hello authorization token of hello user can be invalidated.</span></span> <span data-ttu-id="71789-157">tooinvalidate, hello yetkilendirme belirteci, ayarlanmış hello **StsRefreshTokenValidFrom** Windows PowerShell kullanarak belirli bir kullanıcı için alan.</span><span class="sxs-lookup"><span data-stu-id="71789-157">tooinvalidate hello authorization token, set hello **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="71789-158">Merhaba güncelleştirmelisiniz **StsRefreshTokenValidFrom** toorevoke erişim için istediğiniz her bir kullanıcı için alan.</span><span class="sxs-lookup"><span data-stu-id="71789-158">You must update hello **StsRefreshTokenValidFrom** field for each user you want toorevoke access for.</span></span>

<span data-ttu-id="71789-159">Merhaba iptal ederse tooensure, hello ayarlamalısınız **geçerlilik tarihi** hello CRL tooa Date tarafından belirlenen hello değerden **StsRefreshTokenValidFrom** ve söz konusu hello sertifikanın olduğundan emin olun Merhaba CRL.</span><span class="sxs-lookup"><span data-stu-id="71789-159">tooensure that hello revocation persists, you must set hello **Effective Date** of hello CRL tooa date after hello value set by **StsRefreshTokenValidFrom** and ensure hello certificate in question is in hello CRL.</span></span>

<span data-ttu-id="71789-160">Güncelleştirme ve ayarlama hello tarafından hello yetkilendirme belirteci geçersiz hale getiriliyor adımları anahat hello sürecini izleyerek hello **StsRefreshTokenValidFrom** alan.</span><span class="sxs-lookup"><span data-stu-id="71789-160">hello following steps outline hello process for updating and invalidating hello authorization token by setting hello **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="71789-161">**tooconfigure iptal:**</span><span class="sxs-lookup"><span data-stu-id="71789-161">**tooconfigure revocation:**</span></span> 

1. <span data-ttu-id="71789-162">Yönetici kimlik bilgileri toohello MSOL hizmetiyle Bağlan:</span><span class="sxs-lookup"><span data-stu-id="71789-162">Connect with admin credentials toohello MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="71789-163">Bir kullanıcı için geçerli StsRefreshTokensValidFrom değerini Hello Al:</span><span class="sxs-lookup"><span data-stu-id="71789-163">Retrieve hello current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="71789-164">Merhaba kullanıcı eşit toohello geçerli zaman damgası için yeni bir StsRefreshTokensValidFrom değeri yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="71789-164">Configure a new StsRefreshTokensValidFrom value for hello user equal toohello current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="71789-165">Başlangıç tarihi, Ayarla hello gelecekte olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="71789-165">hello date you set must be in hello future.</span></span> <span data-ttu-id="71789-166">Başlangıç tarihi hello gelecekteki değilse hello **StsRefreshTokensValidFrom** özelliği ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="71789-166">If hello date is not in hello future, hello **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="71789-167">Başlangıç tarihi hello gelecekteki ise **StsRefreshTokensValidFrom** toohello geçerli saati (kümesi MsolUser komutu tarafından belirtilen başlangıç tarihi değil) ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="71789-167">If hello date is in hello future, **StsRefreshTokensValidFrom** is set toohello current time (not hello date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="71789-168">4. adım: Test yapılandırmanızı</span><span class="sxs-lookup"><span data-stu-id="71789-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="71789-169">Sertifikanızı test etme</span><span class="sxs-lookup"><span data-stu-id="71789-169">Testing your certificate</span></span>

<span data-ttu-id="71789-170">İlk Yapılandırma sınaması toosign içinde çok denemeniz gerektiğini[Outlook Web Access](https://outlook.office365.com) veya [SharePoint Online](https://microsoft.sharepoint.com) kullanarak, **-cihazdır**.</span><span class="sxs-lookup"><span data-stu-id="71789-170">As a first configuration test, you should try toosign in too[Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="71789-171">Oturum açma işleminiz başarılı olursa, ardından bunu biliyor:</span><span class="sxs-lookup"><span data-stu-id="71789-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="71789-172">sağlanan tooyour test cihazı Hello kullanıcı sertifikası kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="71789-172">hello user certificate has been provisioned tooyour test device</span></span>
- <span data-ttu-id="71789-173">AD FS düzgün yapılandırılmış</span><span class="sxs-lookup"><span data-stu-id="71789-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="71789-174">Office mobil uygulamalarını test etme</span><span class="sxs-lookup"><span data-stu-id="71789-174">Testing Office mobile applications</span></span>

<span data-ttu-id="71789-175">**tootest sertifika tabanlı kimlik doğrulamasını mobil Office uygulamanızda:**</span><span class="sxs-lookup"><span data-stu-id="71789-175">**tootest certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="71789-176">Test aygıtınızda Office mobil uygulaması (örneğin, OneDrive) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="71789-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="71789-177">Merhaba uygulaması başlatın.</span><span class="sxs-lookup"><span data-stu-id="71789-177">Launch hello application.</span></span> 
4. <span data-ttu-id="71789-178">Kullanıcı adınızı girin ve ardından toouse istediğiniz hello kullanıcı sertifika seçin.</span><span class="sxs-lookup"><span data-stu-id="71789-178">Enter your user name, and then select hello user certificate you want toouse.</span></span> 

<span data-ttu-id="71789-179">Başarıyla oturum açmanız.</span><span class="sxs-lookup"><span data-stu-id="71789-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="71789-180">Exchange ActiveSync istemci uygulamalarını test etme</span><span class="sxs-lookup"><span data-stu-id="71789-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="71789-181">Sertifika tabanlı kimlik doğrulaması, hello istemci sertifikasını içeren bir EAS profili aracılığıyla Exchange ActiveSync (EAS) tooaccess kullanılabilir toohello uygulamanın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="71789-181">tooaccess Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing hello client certificate must be available toohello application.</span></span> 

<span data-ttu-id="71789-182">Merhaba EAS profili bilgisinden hello içermelidir:</span><span class="sxs-lookup"><span data-stu-id="71789-182">hello EAS profile must contain hello following information:</span></span>

- <span data-ttu-id="71789-183">kimlik doğrulaması için kullanılan kullanıcı sertifika toobe hello</span><span class="sxs-lookup"><span data-stu-id="71789-183">hello user certificate toobe used for authentication</span></span> 

- <span data-ttu-id="71789-184">Merhaba EAS uç noktası (örneğin, outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="71789-184">hello EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="71789-185">EAS profili yapılandırılan ve mobil cihaz Yönetimi (MDM) Intune gibi ya da el ile Merhaba sertifika hello hello cihazda EAS profili yerleştirmekten hello kullanımı üzerinden hello cihazın yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="71789-185">An EAS profile can be configured and placed on hello device through hello utilization of Mobile device management (MDM) such as Intune or by manually placing hello certificate in hello EAS profile on hello device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="71789-186">Android'de test EAS istemci uygulamaları</span><span class="sxs-lookup"><span data-stu-id="71789-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="71789-187">**tootest sertifika kimlik doğrulaması:**</span><span class="sxs-lookup"><span data-stu-id="71789-187">**tootest certificate authentication:**</span></span>  

1. <span data-ttu-id="71789-188">EAS profili yukarıdaki hello gereksinimleri karşılayan hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="71789-188">Configure an EAS profile in hello application that satisfies hello requirements above.</span></span>  
2. <span data-ttu-id="71789-189">Merhaba uygulaması açın ve posta eşitliyor doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="71789-189">Open hello application, and verify that mail is synchronizing.</span></span> 

