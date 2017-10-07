---
title: "aaaHow tooconfigure karma Azure Active Directory'ye katılmış cihazları | Microsoft Docs"
description: "Nasıl tooconfigure karma Azure Active Directory'ye katılmış cihazlarda öğrenin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: f97ea436eca2833d8a9843acd19e5c633bc0fc07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-hybrid-azure-active-directory-joined-devices"></a><span data-ttu-id="a71a3-103">Nasıl tooconfigure karma Azure Active Directory'ye katılmış cihazlarda</span><span class="sxs-lookup"><span data-stu-id="a71a3-103">How tooconfigure hybrid Azure Active Directory joined devices</span></span>

<span data-ttu-id="a71a3-104">Azure Active Directory'de (Azure AD) ile cihaz yönetimi, güvenlik ve uyumluluğa yönelik standartlarınızı karşılamak aygıtlardan kullanıcılarınızın kaynaklarınızı eriştiğiniz emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a71a3-104">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> <span data-ttu-id="a71a3-105">Daha fazla ayrıntı için bkz: [giriş toodevice Yönetimi Azure Active Directory'de](device-management-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a71a3-105">For more details, see [Introduction toodevice management in Azure Active Directory](device-management-introduction.md).</span></span>

<span data-ttu-id="a71a3-106">Bir şirket içi Active Directory ortamına sahip ve, etki alanına katılmış aygıtlar tooAzure AD toojoin istiyorsanız bunu karma Azure AD alanına katılmış cihazları yapılandırarak gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a71a3-106">If you have an on-premises Active Directory environment and you want toojoin your domain-joined devices tooAzure AD, you can accomplish this by configuring hybrid Azure AD joined devices.</span></span> <span data-ttu-id="a71a3-107">Merhaba konu sağlar, hello ile ilgili adımlar.</span><span class="sxs-lookup"><span data-stu-id="a71a3-107">hello topic provides you with hello related steps.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="a71a3-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="a71a3-108">Before you begin</span></span>

<span data-ttu-id="a71a3-109">Yapılandırmaya başlamadan önce ortamınızda karma Azure AD katılmış cihazlarda, kendiniz hello desteklenen senaryolar ve hello kısıtlamaları kazanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="a71a3-109">Before you start configuring hybrid Azure AD joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="a71a3-110">Merhaba okunabilirliğini hello açıklamaları tooimprove, bu konuda terim aşağıdaki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="a71a3-110">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="a71a3-111">**Windows geçerli aygıtları** -Windows 10 veya Windows Server 2016 çalıştıran toodomain katılmış cihazlarda bu terimi anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-111">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="a71a3-112">**Windows alt düzey aygıtları** -bu terim tooall başvuruyor **desteklenen** çalışan Windows 10 ne Windows Server 2016 etki alanına katılmış Windows cihazları.</span><span class="sxs-lookup"><span data-stu-id="a71a3-112">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="a71a3-113">Geçerli Windows cihazları</span><span class="sxs-lookup"><span data-stu-id="a71a3-113">Windows current devices</span></span>

- <span data-ttu-id="a71a3-114">Merhaba Windows masaüstü işletim sistemi çalıştıran cihazlar için Windows 10 Anniversary güncelleştirme (sürüm 1607) kullanılmasını öneririz veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="a71a3-114">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="a71a3-115">Merhaba geçerli Windows cihazlarının kaydı **olan** parola karma eşitlemesi yapılandırmaları gibi Federasyon olmayan ortamlarda desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-115">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="a71a3-116">Windows alt düzey aygıtları</span><span class="sxs-lookup"><span data-stu-id="a71a3-116">Windows down-level devices</span></span>

- <span data-ttu-id="a71a3-117">Windows alt düzey aygıtları aşağıdaki hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="a71a3-117">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="a71a3-118">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="a71a3-118">Windows 8.1</span></span>
    - <span data-ttu-id="a71a3-119">Windows 7</span><span class="sxs-lookup"><span data-stu-id="a71a3-119">Windows 7</span></span>
    - <span data-ttu-id="a71a3-120">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a71a3-120">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="a71a3-121">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a71a3-121">Windows Server 2012</span></span>
    - <span data-ttu-id="a71a3-122">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="a71a3-122">Windows Server 2008 R2</span></span>
- <span data-ttu-id="a71a3-123">Merhaba Windows alt düzey cihazlarının kaydı **olan** sorunsuz çoklu oturum açma ile federe olmayan ortamlarda desteklenen [Azure Active Directory sorunsuz çoklu oturum açma](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="a71a3-123">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="a71a3-124">Merhaba Windows alt düzey cihazlarının kaydı **değil** dolaşım profilleri kullanarak cihazları için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-124">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="a71a3-125">Dolaşım profilleri veya ayarlarını FQDN'yi kullanıyorsanız, Windows 10 kullanın.</span><span class="sxs-lookup"><span data-stu-id="a71a3-125">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="a71a3-126">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a71a3-126">Prerequisites</span></span>

<span data-ttu-id="a71a3-127">Karma Azure AD alanına katılmış cihazları, kuruluşunuzda etkinleştirme başlamadan önce Azure AD güncel bir sürümünü çalıştırdığından emin toomake gerekir bağlanın.</span><span class="sxs-lookup"><span data-stu-id="a71a3-127">Before you start enabling hybrid Azure AD joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="a71a3-128">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="a71a3-128">Azure AD Connect:</span></span>

- <span data-ttu-id="a71a3-129">Şirket içi Active Directory (AD) ve Azure AD'de hello cihaz nesnesi hello bilgisayar hesabını arasındaki ilişkiyi Hello tutar.</span><span class="sxs-lookup"><span data-stu-id="a71a3-129">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="a71a3-130">Başka bir aygıt etkinleştirir ilgili özellikler gibi iş için Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="a71a3-130">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="a71a3-131">Yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="a71a3-131">Configuration steps</span></span>

<span data-ttu-id="a71a3-132">Karma Azure AD alanına katılmış aygıtlar çeşitli Windows cihaz platformları için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a71a3-132">You can configure hybrid Azure AD joined devices for various types of Windows device platforms.</span></span> <span data-ttu-id="a71a3-133">Bu konuda, tüm normal yapılandırma senaryoları için gerekli hello adımlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-133">This topic includes hello required steps for all typical configuration scenarios.</span></span>  

<span data-ttu-id="a71a3-134">Aşağıdaki tablo tooget senaryonuz için gerekli olan hello adımlara genel bir bakış hello kullan:</span><span class="sxs-lookup"><span data-stu-id="a71a3-134">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="a71a3-135">Adımlar</span><span class="sxs-lookup"><span data-stu-id="a71a3-135">Steps</span></span>                                      | <span data-ttu-id="a71a3-136">Windows geçerli ve parola karma eşitlemesi</span><span class="sxs-lookup"><span data-stu-id="a71a3-136">Windows current and password hash sync</span></span> | <span data-ttu-id="a71a3-137">Windows geçerli ve Federasyon</span><span class="sxs-lookup"><span data-stu-id="a71a3-137">Windows current and federation</span></span> | <span data-ttu-id="a71a3-138">Alt düzey Windows</span><span class="sxs-lookup"><span data-stu-id="a71a3-138">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="a71a3-139">1. adım: hizmet bağlantı noktası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a71a3-139">Step 1: Configure service connection point</span></span> | ![İşaretli][1]                            | ![İşaretli][1]                    | ![İşaretli][1]        |
| <span data-ttu-id="a71a3-143">2. adım: talep verme kurma</span><span class="sxs-lookup"><span data-stu-id="a71a3-143">Step 2: Setup issuance of claims</span></span>           |                                        | ![İşaretli][1]                    | ![İşaretli][1]        |
| <span data-ttu-id="a71a3-146">3. adım: Windows 10 cihazları etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a71a3-146">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![İşaretli][1]        |
| <span data-ttu-id="a71a3-148">Adım 4: Denetimi dağıtımı ve dağıtım</span><span class="sxs-lookup"><span data-stu-id="a71a3-148">Step 4: Control deployment and rollout</span></span>     | ![İşaretli][1]                            | ![İşaretli][1]                    | ![İşaretli][1]        |
| <span data-ttu-id="a71a3-152">5. adım: alanına katılmamış aygıtlar doğrulayın</span><span class="sxs-lookup"><span data-stu-id="a71a3-152">Step 5: Verify joined devices</span></span>          | ![İşaretli][1]                            | ![İşaretli][1]                    | ![İşaretli][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="a71a3-156">1. adım: hizmet bağlantı noktası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a71a3-156">Step 1: Configure service connection point</span></span>

<span data-ttu-id="a71a3-157">Merhaba hizmet bağlantı noktası (SCP) nesnesinin hello kayıt toodiscover sırasında Azure AD Kiracı bilgilerini cihazlar tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a71a3-157">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="a71a3-158">Şirket içi Active Directory (AD), hello yapılandırma adlandırma bağlamı bölümünde hello bilgisayarın orman hello SCP nesnesi hello karma Azure AD alanına katılmış cihazlar için mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a71a3-158">In your on-premises Active Directory (AD), hello SCP object for hello hybrid Azure AD joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="a71a3-159">Her ormanda yalnızca bir yapılandırma adlandırma bağlamında yoktur.</span><span class="sxs-lookup"><span data-stu-id="a71a3-159">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="a71a3-160">Bir Çoklu orman Active Directory yapılandırması, etki alanına katılmış bilgisayarları içeren tüm ormanlarda hello hizmet bağlantı noktası mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a71a3-160">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="a71a3-161">Merhaba kullanabilirsiniz [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello yapılandırma adlandırma bağlamında ormanınızın.</span><span class="sxs-lookup"><span data-stu-id="a71a3-161">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="a71a3-162">Merhaba Active Directory etki alanı adına sahip bir orman için *fabrikam.com*, hello yapılandırma adlandırma bağlamında değil:</span><span class="sxs-lookup"><span data-stu-id="a71a3-162">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="a71a3-163">Ormanınıza hello otomatik kaydı etki alanına katılmış cihazlar için hello SCP nesnesi şu konumdadır:</span><span class="sxs-lookup"><span data-stu-id="a71a3-163">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="a71a3-164">Nasıl Azure AD Connect dağıttığınız bağlı olarak, hello SCP nesnesi zaten yapılandırılmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-164">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="a71a3-165">Hello nesne hello varlığını doğrulayın ve Windows PowerShell Betiği aşağıdaki hello kullanarak hello bulma değerleri alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a71a3-165">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="a71a3-166">Merhaba **$scp. Anahtar sözcükler** çıktı hello Azure AD Kiracı bilgileri, örneğin gösterir:</span><span class="sxs-lookup"><span data-stu-id="a71a3-166">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="a71a3-167">Merhaba hizmet bağlantı noktası mevcut değilse, bunu hello çalıştırarak oluşturabilirsiniz `Initialize-ADSyncDomainJoinedComputerSync` Azure AD Connect sunucunuzda cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a71a3-167">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="a71a3-168">Kuruluş yönetici kimlik bilgileri gerekli toorun bu cmdlet'tir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-168">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="a71a3-169">Merhaba cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a71a3-169">hello cmdlet:</span></span>

- <span data-ttu-id="a71a3-170">Azure AD Connect bağlı hello Active Directory ormanındaki Hello hizmet bağlantı noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a71a3-170">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="a71a3-171">Toospecify hello gerektirir `AdConnectorAccount` parametresi.</span><span class="sxs-lookup"><span data-stu-id="a71a3-171">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="a71a3-172">Active Directory Bağlayıcısı hesabı Azure ad connect yapılandırılmış hello hesap budur.</span><span class="sxs-lookup"><span data-stu-id="a71a3-172">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="a71a3-173">Merhaba aşağıdaki komut dosyası hello cmdlet'ini kullanarak bir örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-173">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="a71a3-174">Bu komut `$aadAdminCred = Get-Credential` tootype bir kullanıcı adı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-174">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="a71a3-175">Merhaba kullanıcı asıl adı (UPN) biçiminde tooprovide hello kullanıcı adı gerekir (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="a71a3-175">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="a71a3-176">Merhaba `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a71a3-176">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="a71a3-177">Bir etki alanı denetleyicisinde çalışan Active Directory Web Hizmetleri dayanan hello Active Directory PowerShell modülü kullanır.</span><span class="sxs-lookup"><span data-stu-id="a71a3-177">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="a71a3-178">Active Directory Web Hizmetleri, Windows Server 2008 R2 çalıştıran etki alanı denetleyicilerinde ve üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-178">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="a71a3-179">Yalnızca hello tarafından desteklenen **MSOnline PowerShell modülü sürümü 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-179">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="a71a3-180">toodownload bu modül bu [bağlantı](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="a71a3-180">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="a71a3-181">Windows Server 2008 veya önceki sürümlerini çalıştıran etki alanı denetleyicileri için toocreate hello hizmet bağlantı noktası aşağıdaki hello komut dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="a71a3-181">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="a71a3-182">Bir Çoklu orman yapılandırması, komut dosyası toocreate hello hizmet bağlantı noktası bilgisayarları var olduğu her bir orman içinde aşağıdaki hello kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a71a3-182">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="a71a3-183">2. adım: talep verme kurma</span><span class="sxs-lookup"><span data-stu-id="a71a3-183">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="a71a3-184">Bir Federasyon Azure AD yapılandırma cihazlar Active Directory Federasyon Hizmetleri (AD FS) üzerinde kullanır veya 3. taraf bir Federasyon Hizmeti tooauthenticate tooAzure AD şirket içi.</span><span class="sxs-lookup"><span data-stu-id="a71a3-184">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="a71a3-185">Aygıtları tooget bir erişim belirteci tooregister hello Azure Active Directory cihaz kayıt Hizmeti'ne (Azure DRS) karşı kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="a71a3-185">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="a71a3-186">Windows hello şirket içi Federasyon Hizmeti tarafından barındırılan tümleşik Windows kimlik doğrulaması tooan etkin WS-Trust uç noktası (1.3 veya 2005 sürümler) kullanarak geçerli aygıtların kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="a71a3-186">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="a71a3-187">AD FS, ya da kullanırken **adfs/services/güven/13/windowstransport** veya **adfs/services/güven/2005/windowstransport** etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-187">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="a71a3-188">Ayrıca hello Web kimlik doğrulaması Proxy kullanıyorsanız, bu uç noktaya hello proxy üzerinden yayımlanan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a71a3-188">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="a71a3-189">Hangi uç noktalarının altında hello AD FS Yönetim Konsolu aracılığıyla özelliğinin etkinleştirilip etkinleştirilmediğini **hizmet > uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-189">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="a71a3-190">AD FS, şirket içi Federasyon Hizmeti olarak yoksa, WS-Trust 1.3 veya 2005 uç noktalarının ve bunlar hello meta veri değişimi dosya (MEX) yayımlanır desteklediğinden emin, satıcı toomake hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="a71a3-190">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="a71a3-191">Merhaba aşağıdaki talep için cihaz kayıt toocomplete Azure DRS tarafından alınan hello belirtecindeki mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-191">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="a71a3-192">Azure DRS Azure AD ile sonra Azure AD Connect tooassociate yeni oluşturulan hello cihaz nesnesi hello bilgisayar hesabı şirket tarafından kullanılan bu bilgilerin bazıları, bir cihaz nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a71a3-192">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="a71a3-193">Birden fazla doğrulanan etki alanı adı varsa, talep bilgisayarlar için aşağıdaki tooprovide hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a71a3-193">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="a71a3-194">Zaten bir İmmutableıd talep (örn., alternatif oturum açma kimliği) dağıttığınız bilgisayarlar için bir karşılık gelen talep tooprovide gerekir:</span><span class="sxs-lookup"><span data-stu-id="a71a3-194">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="a71a3-195">Aşağıdaki bölümlerde hello hakkında bilgiler yer:</span><span class="sxs-lookup"><span data-stu-id="a71a3-195">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="a71a3-196">Merhaba değerleri her talep olmalıdır</span><span class="sxs-lookup"><span data-stu-id="a71a3-196">hello values each claim should have</span></span>
- <span data-ttu-id="a71a3-197">Nasıl bir tanımı gibi AD FS'de görüneceği</span><span class="sxs-lookup"><span data-stu-id="a71a3-197">How a definition would look like in AD FS</span></span>

<span data-ttu-id="a71a3-198">Merhaba tanımı yardımcı olan tooverify hello değerleri mevcut olup olmadığını veya toocreate ihtiyacınız varsa, bunları.</span><span class="sxs-lookup"><span data-stu-id="a71a3-198">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="a71a3-199">Şirket içi Federasyon sunucunuz için AD FS kullanmıyorsanız, bu talepler satıcınızın yönergeleri toocreate hello uygun yapılandırma tooissue izleyin.</span><span class="sxs-lookup"><span data-stu-id="a71a3-199">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="a71a3-200">Sorunu hesap türü talep</span><span class="sxs-lookup"><span data-stu-id="a71a3-200">Issue account type claim</span></span>

<span data-ttu-id="a71a3-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Bu talep değerini içermelidir **DJ**, hello cihaz etki alanına katılmış bir bilgisayar olarak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a71a3-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="a71a3-202">AD FS'de şuna benzer bir verme dönüştürme kural ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a71a3-202">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="a71a3-203">Sorunu objectGUID hello bilgisayar hesabı şirket içinde</span><span class="sxs-lookup"><span data-stu-id="a71a3-203">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="a71a3-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Bu talep hello içermelidir **objectGUID** hello değerini şirket içi bilgisayar hesabı.</span><span class="sxs-lookup"><span data-stu-id="a71a3-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="a71a3-205">AD FS'de şuna benzer bir verme dönüştürme kural ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a71a3-205">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="a71a3-206">Sorunu objectSID hello bilgisayar hesabı şirket içinde</span><span class="sxs-lookup"><span data-stu-id="a71a3-206">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="a71a3-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Bu talep hello hello içermelidir **objectSID** hello değerini şirket içi bilgisayar hesabı.</span><span class="sxs-lookup"><span data-stu-id="a71a3-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="a71a3-208">AD FS'de şuna benzer bir verme dönüştürme kural ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a71a3-208">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="a71a3-209">Birden çok etki alanı adlarını Azure AD'de belirlediğinizde issuerID bilgisayar için sorun</span><span class="sxs-lookup"><span data-stu-id="a71a3-209">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="a71a3-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Bu talep hello hiçbirinin Tekdüzen Kaynak Tanımlayıcısı (URI) ile Merhaba bağlanmak etki alanı adları şirket içi Federasyon Hizmeti (AD FS veya 3. taraf) sertifika veren hello belirteci doğrulandı hello içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="a71a3-211">AD FS içinde sonra belirli bir sıraya Merhaba, olanları yukarıdaki olanları aşağıdaki hello gibi görünmesini verme dönüştürme kuralları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a71a3-211">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="a71a3-212">Lütfen gerekli kullanıcılar için bir kural tooexplicitly sorunu hello kural unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a71a3-212">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="a71a3-213">Merhaba kuralları'nda aşağıdaki kullanıcı ve bilgisayar kimlik doğrulaması tanımlama ilk bir kuralı eklenir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-213">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


<span data-ttu-id="a71a3-214">Yukarıdaki Hello talep kümesinde</span><span class="sxs-lookup"><span data-stu-id="a71a3-214">In hello claim above,</span></span>

- <span data-ttu-id="a71a3-215">`$<domain>`Merhaba AD FS hizmet URL'si</span><span class="sxs-lookup"><span data-stu-id="a71a3-215">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="a71a3-216">`<verified-domain-name>`tooreplace doğrulanmış etki alanı adlarınızı biri ile Azure AD içinde gereksinim duyduğunuz bir yer tutucudur</span><span class="sxs-lookup"><span data-stu-id="a71a3-216">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="a71a3-217">Doğrulanmış etki alanı adları hakkında daha fazla ayrıntı için bkz: [özel etki alanı adı tooAzure Active Directory eklemek](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="a71a3-217">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="a71a3-218">tooget doğrulanmış şirket etki alanlarının bir listesini, kullanabileceğiniz hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a71a3-218">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="a71a3-220">Kullanıcılar için bir tane bulunduğunda (kimliği ayarlanmadan örneğin alternatif oturum açma) İmmutableıd bilgisayar için sorun</span><span class="sxs-lookup"><span data-stu-id="a71a3-220">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="a71a3-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**-Bu talep bilgisayarlar için geçerli bir değer içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="a71a3-222">AD FS içinde verme dönüştürme kural aşağıdaki gibi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a71a3-222">In AD FS, you can create an issuance transform rule as follows:</span></span>

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="a71a3-223">Yardımcı betik toocreate hello AD FS verme dönüştürme kuralları</span><span class="sxs-lookup"><span data-stu-id="a71a3-223">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="a71a3-224">Merhaba aşağıdaki betiği hello verme hello oluşturulmasını ile yukarıda açıklanan kuralları dönüştürme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a71a3-224">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a><span data-ttu-id="a71a3-225">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="a71a3-225">Remarks</span></span> 

- <span data-ttu-id="a71a3-226">Bu komut dosyası hello kuralları toohello mevcut kurallar ekler.</span><span class="sxs-lookup"><span data-stu-id="a71a3-226">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="a71a3-227">Merhaba kuralları ayarlamak için çalışmıyor hello betik iki kez iki kez eklenir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-227">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="a71a3-228">Karşılık gelen hiçbir kural (koşullarda hello karşılık gelen) bu talepler için hello betiği yeniden çalıştırmadan önce var olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a71a3-228">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="a71a3-229">Merhaba değerini ayarlayın (hello Azure AD portalında veya hello Get-MsolDomains cmdlet'i aracılığıyla gösterildiği gibi) birden çok doğrulanmış etki alanı adı, varsa **$multipleVerifiedDomainNames** hello çok komut dosyası**$true**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-229">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="a71a3-230">Ayrıca Azure AD Connect veya başka yöntemler aracılığıyla oluşturulan tüm mevcut issuerid talep kaldırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a71a3-230">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="a71a3-231">Bu kural için örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a71a3-231">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="a71a3-232">Zaten yayımlandı durumunda bir **İmmutableıd** hello değeri olarak ayarlayın, kullanıcı hesapları için talep **$immutableIDAlreadyIssuedforUsers** hello çok komut dosyası**$true**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-232">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="a71a3-233">Adım 3: Windows alt düzey aygıtları etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="a71a3-233">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="a71a3-234">Bazı etki alanına katılmış aygıtlarınız Windows cihazları sürümlerdeki, gerekir:</span><span class="sxs-lookup"><span data-stu-id="a71a3-234">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="a71a3-235">Bir ilke Azure AD tooenable kullanıcılar tooregister aygıtları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a71a3-235">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="a71a3-236">Şirket içi Federasyon Hizmeti tooissue talep toosupport yapılandırma **tümleşik Windows kimlik doğrulaması (IWA)** cihaz kaydı için.</span><span class="sxs-lookup"><span data-stu-id="a71a3-236">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="a71a3-237">Merhaba aygıt doğrulanırken tooavoid sertifika ister hello Azure AD cihaz kimlik doğrulama uç noktası toohello yerel Intranet bölgeler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a71a3-237">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="a71a3-238">İlke Azure AD tooenable kullanıcılar tooregister aygıtları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a71a3-238">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="a71a3-239">tooregister Windows alt düzey aygıtları toomake tooallow kullanıcılar Azure AD'de tooregister cihazları ayarlama bu hello ayarlandığından emin gerekir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-239">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="a71a3-240">Hello Azure portalı, bu ayarı altında bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a71a3-240">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="a71a3-241">Merhaba aşağıdaki İlkesi çok ayarlanmalıdır**tüm**: **kullanıcıları Azure AD ile cihazlarını kaydetme**</span><span class="sxs-lookup"><span data-stu-id="a71a3-241">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![Cihaz kaydetme](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="a71a3-243">Şirket içi Federasyon hizmetini yapılandır</span><span class="sxs-lookup"><span data-stu-id="a71a3-243">Configure on-premises federation service</span></span> 

<span data-ttu-id="a71a3-244">Şirket içi Federasyon hizmetinizi veren hello desteklemelidir **authenticationmehod** ve **wiaormultiauthn** bir kimlik doğrulama alırken talep isteği toohello Azure AD bağlı olan taraf bulunduran bir resouce_params parametre gösterildiği gibi kodlanmış bir değeri olan aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="a71a3-244">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="a71a3-245">Böyle bir istek geldiğinde, hello şirket içi Federasyon Hizmeti tümleşik Windows kimlik doğrulaması kullanarak hello kullanıcı kimlik doğrulaması yapmalıdır ve başarı iki talep aşağıdaki hello kesmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="a71a3-245">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="a71a3-246">AD FS içinde verme dönüştürme kural bu geçişleri üzerinden hello kimlik doğrulama yöntemi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-246">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="a71a3-247">**tooadd bu kural:**</span><span class="sxs-lookup"><span data-stu-id="a71a3-247">**tooadd this rule:**</span></span>

1. <span data-ttu-id="a71a3-248">Merhaba AD FS yönetim konsolunda çok Git`AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="a71a3-248">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="a71a3-249">Merhaba Microsoft Office 365 kimlik Platformu'na bağlı taraf güven nesnesi sağ tıklayın ve ardından **talep kurallarını Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-249">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="a71a3-250">Merhaba üzerinde **verme dönüştürme kuralları** sekmesine **Kuralı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-250">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="a71a3-251">Merhaba, **talep kuralı** şablonu listesinden **talepleri özel kural kullanarak Gönder**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-251">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="a71a3-252">Seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-252">Select **Next**.</span></span>
6. <span data-ttu-id="a71a3-253">Merhaba, **talep kuralı adı** kutusuna **kimlik doğrulama yöntemi talep kuralı**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-253">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="a71a3-254">Merhaba, **talep kuralı** kutusu, aşağıdaki kural türü hello:</span><span class="sxs-lookup"><span data-stu-id="a71a3-254">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="a71a3-255">Değiştirildikten sonra Federasyon sunucunuzda aşağıdaki hello PowerShell komutunu yazın  **\<RPObjectName\>**  hello bağlı olan taraf için nesne adı, Azure AD bağlı olan taraf güven nesnesi ile.</span><span class="sxs-lookup"><span data-stu-id="a71a3-255">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="a71a3-256">Bu nesne genellikle adlı **Microsoft Office 365 kimlik Platformu'na**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-256">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="a71a3-257">Hello Azure AD cihaz kimlik doğrulama uç noktası toohello yerel Intranet bölgeler ekleyin</span><span class="sxs-lookup"><span data-stu-id="a71a3-257">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="a71a3-258">tooAzure Internet Explorer'da URL toohello yerel Intranet bölgesine izleyen bir ilke tooyour etki alanına katılmış aygıtlar tooadd hello gönderebilir AD kaydı cihazları kullanıcıların kimliğini doğrularken tooavoid sertifika ister:</span><span class="sxs-lookup"><span data-stu-id="a71a3-258">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="a71a3-259">Adım 4: Denetimi dağıtımı ve dağıtım</span><span class="sxs-lookup"><span data-stu-id="a71a3-259">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="a71a3-260">Merhaba gerekli adımları tamamladıktan sonra hazır tooautomatically birleştirme Azure AD etki alanına katılmış aygıtlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a71a3-260">When you have completed hello required steps, domain-joined devices are ready tooautomatically join Azure AD:</span></span>

- <span data-ttu-id="a71a3-261">Windows 10 Anniversary güncelleştirmesi ve Windows Server 2016 çalıştıran tüm etki alanına katılmış cihazlar otomatik olarak kayıt aygıt adresindeki Azure AD ile yeniden başlatın veya kullanıcı oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a71a3-261">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> 

- <span data-ttu-id="a71a3-262">Yeni cihazların Merhaba etki alanına katılma işlemi tamamlandıktan sonra hello aygıt yeniden başlatıldığında Azure AD ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a71a3-262">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

- <span data-ttu-id="a71a3-263">Daha önce Azure AD olan cihaz kayıtlı (örneğin, Intune için) çok geçiş "*etki alanına katılmış, AAD kayıtlı*"; Ancak, gereken süre bu işlem toocomplete için toohello normal akışı nedeniyle tüm cihazlar arasında etki alanı ve kullanıcı etkinliğini.</span><span class="sxs-lookup"><span data-stu-id="a71a3-263">Devices that were previously Azure AD registered (for example, for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="a71a3-264">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="a71a3-264">Remarks</span></span>

- <span data-ttu-id="a71a3-265">Windows 10 ve Windows Server 2016 etki alanına katılmış bilgisayarlar otomatik kaydını bir Grup İlkesi nesnesi toocontrol hello sunumu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a71a3-265">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="a71a3-266">Windows 10 Kasım 2015 güncelleştirmesi otomatik olarak birleştiren Azure AD ile **yalnızca** hello sunum Grup İlkesi nesnesi ayarlarsanız.</span><span class="sxs-lookup"><span data-stu-id="a71a3-266">Windows 10 November 2015 Update automatically joins with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="a71a3-267">dağıtabileceğiniz toorollout Windows alt düzey bilgisayarların bir [Windows Installer paketi](#windows-installer-packages-for-non-windows-10-computers) seçtiğiniz toocomputers.</span><span class="sxs-lookup"><span data-stu-id="a71a3-267">toorollout of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="a71a3-268">Merhaba Grup İlkesi nesnesi tooWindows 8.1 etki alanına katılmış aygıtlar itme olursa, bir birleştirme denenir; Ancak, hello kullanmanız önerilir [Windows Installer paketi](#windows-installer-packages-for-non-windows-10-computers) toojoin tüm Windows alt düzey cihazlar.</span><span class="sxs-lookup"><span data-stu-id="a71a3-268">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, a join is attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toojoin all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="a71a3-269">Bir Grup İlkesi nesnesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a71a3-269">Create a Group Policy object</span></span> 

<span data-ttu-id="a71a3-270">toocontrol hello sunum geçerli bilgisayarların Windows hello dağıtmalısınız **etki alanına katılmış bilgisayarları cihaz olarak kaydetme** tooregister istediğiniz Grup İlkesi nesnesi toohello aygıtlar.</span><span class="sxs-lookup"><span data-stu-id="a71a3-270">toocontrol hello rollout of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="a71a3-271">Örneğin, hello İlkesi tooan kuruluş birimi ya da tooa güvenlik grubu dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a71a3-271">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="a71a3-272">**tooset hello İlkesi:**</span><span class="sxs-lookup"><span data-stu-id="a71a3-272">**tooset hello policy:**</span></span>

1. <span data-ttu-id="a71a3-273">Açık **Sunucu Yöneticisi'ni**ve çok Git`Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="a71a3-273">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="a71a3-274">Windows geçerli bilgisayarların tooactivate otomatik kaydı istediğiniz toohello etki alanı karşılık gelen toohello etki alanı düğümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="a71a3-274">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="a71a3-275">Sağ **Grup İlkesi nesneleri**ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-275">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="a71a3-276">Grup İlkesi nesnesi için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="a71a3-276">Type a name for your Group Policy object.</span></span> <span data-ttu-id="a71a3-277">Örneğin, * karma Azure AD birleştirme.</span><span class="sxs-lookup"><span data-stu-id="a71a3-277">For example, *Hybrid Azure AD join.</span></span> 
5. <span data-ttu-id="a71a3-278">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a71a3-278">Click **OK**.</span></span>
6. <span data-ttu-id="a71a3-279">Yeni Grup İlkesi nesneniz sağ tıklayın ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-279">Right-click your new Group Policy object, and then select **Edit**.</span></span>
7. <span data-ttu-id="a71a3-280">Çok Git**Bilgisayar Yapılandırması** > **ilkeleri** > **Yönetim Şablonları** > **Windows Bileşenleri** > **aygıt kaydı**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-280">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> 
8. <span data-ttu-id="a71a3-281">Sağ **etki alanına katılmış bilgisayarları cihaz olarak kaydetme**ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-281">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a71a3-282">Bu Grup İlkesi şablonu hello Grup İlkesi Yönetimi konsolunun önceki sürümlerden adlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="a71a3-282">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="a71a3-283">Merhaba konsol önceki bir sürümünü kullanıyorsanız, çok Git`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="a71a3-283">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="a71a3-284">Seçin **etkin**ve ardından **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-284">Select **Enabled**, and then click **Apply**.</span></span>
8. <span data-ttu-id="a71a3-285">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a71a3-285">Click **OK**.</span></span>
9. <span data-ttu-id="a71a3-286">Bağlantı hello Grup İlkesi nesnesi tooa konum.</span><span class="sxs-lookup"><span data-stu-id="a71a3-286">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="a71a3-287">Örneğin, tooa belirli bir kuruluş birimine bağlantı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a71a3-287">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="a71a3-288">Ayrıca otomatik olarak Azure AD ile katılmak bilgisayarları tooa belirli güvenlik grubunun bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a71a3-288">You also could link it tooa specific security group of computers that automatically join with Azure AD.</span></span> <span data-ttu-id="a71a3-289">tooset Bu ilke tüm etki alanına katılmış Windows 10 ve Windows Server 2016 kuruluşunuzdaki bilgisayarların, bağlantı hello Grup İlkesi nesnesi toohello etki alanı için.</span><span class="sxs-lookup"><span data-stu-id="a71a3-289">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="a71a3-290">Windows 10 bilgisayarları için Windows Installer paketleri</span><span class="sxs-lookup"><span data-stu-id="a71a3-290">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="a71a3-291">toojoin etki alanına katılmış Windows alt düzey bilgisayarları Federasyon ortamında, indirin ve bu Windows Installer (.msi) paketi İndirme Merkezi'nden hello yükleyin [Microsoft çalışma alanına katılma için Windows 10 bilgisayarları](https://www.microsoft.com/en-us/download/details.aspx?id=53554)sayfası.</span><span class="sxs-lookup"><span data-stu-id="a71a3-291">toojoin domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="a71a3-292">Bir yazılım dağıtım sistemi gibi System Center Configuration Manager kullanılarak hello paketi dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a71a3-292">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="a71a3-293">Merhaba paketi destekler hello hello standart sessiz yükleme seçenekleriyle *sessiz* parametresi.</span><span class="sxs-lookup"><span data-stu-id="a71a3-293">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="a71a3-294">System Center Configuration Manager geçerli dalının hello özelliği tamamlandı tootrack kayıtlar gibi önceki sürümlerinden ek avantajlar sunar.</span><span class="sxs-lookup"><span data-stu-id="a71a3-294">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="a71a3-295">Daha fazla bilgi için bkz: [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="a71a3-295">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="a71a3-296">Hello yükleyici hello sistemde hello kullanıcının bağlamında çalışan zamanlanmış bir görev oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a71a3-296">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="a71a3-297">içinde tooWindows Hello kullanıcı oturum açtığında hello görevi tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-297">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="a71a3-298">Merhaba görev sessizce hello aygıt hello kullanıcı kimlik bilgileriyle tümleşik Windows kimlik doğrulaması kullanarak kimlik doğrulama sonra Azure AD ile birleştirir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-298">hello task silently joins hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="a71a3-299">toosee hello zamanlanan görev hello aygıtta Git çok**Microsoft** > **çalışma alanına katılma**, ve ardından toohello Görev Zamanlayıcı Kitaplığı gidin.</span><span class="sxs-lookup"><span data-stu-id="a71a3-299">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-joined-devices"></a><span data-ttu-id="a71a3-300">5. adım: alanına katılmamış aygıtlar doğrulayın</span><span class="sxs-lookup"><span data-stu-id="a71a3-300">Step 5: Verify joined devices</span></span>

<span data-ttu-id="a71a3-301">Hello kullanarak, kuruluşunuzda başarılı alanına katılmamış aygıtlar denetleyebilirsiniz [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) hello cmdlet'te [Azure Active Directory PowerShell Modülü](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="a71a3-301">You can check successful joined devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="a71a3-302">Bu cmdlet Hello çıktısını, kayıtlı ve Azure AD ile birleşik olan cihazları gösterir.</span><span class="sxs-lookup"><span data-stu-id="a71a3-302">hello output of this cmdlet shows devices that are registered and joined with Azure AD.</span></span> <span data-ttu-id="a71a3-303">tooget, tüm cihazların Merhaba kullanmak **-tüm** parametre ve filtre hello kullanarak bunları **deviceTrustType** özelliği.</span><span class="sxs-lookup"><span data-stu-id="a71a3-303">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="a71a3-304">Etki alanına katılmış aygıtlar değerine sahip **etki alanına katılmış**.</span><span class="sxs-lookup"><span data-stu-id="a71a3-304">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a71a3-305">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a71a3-305">Next steps</span></span>

* [<span data-ttu-id="a71a3-306">Azure Active Directory'de giriş toodevice Yönetimi</span><span class="sxs-lookup"><span data-stu-id="a71a3-306">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
