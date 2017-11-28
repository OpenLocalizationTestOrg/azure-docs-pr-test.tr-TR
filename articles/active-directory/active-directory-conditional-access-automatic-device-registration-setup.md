---
title: "etki alanına katılmış Windows cihazlarının Azure Active Directory ile aaaHow tooconfigure otomatik kayıt | Microsoft Docs"
description: "Etki alanına katılmış Windows cihazları tooregister, Azure Active Directory ile otomatik olarak ve sessiz bir şekilde ayarlayın."
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
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="6cce1-103">Nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile</span><span class="sxs-lookup"><span data-stu-id="6cce1-103">How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="6cce1-104">toouse [Azure Active Directory cihaz temelli koşullu erişim](active-directory-conditional-access-azure-portal.md), bilgisayarlarınızı Azure Active Directory (Azure AD) ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-104">toouse [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6cce1-105">Hello kullanarak kuruluşunuzdaki kayıtlı aygıtların listesini alabilirsiniz [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) hello cmdlet'te [Azure Active Directory PowerShell Modülü](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="6cce1-105">You can get a list of registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="6cce1-106">Bu makale, kuruluşunuzda Azure AD ile etki alanına katılmış Windows cihazlarının hello otomatik kaydını yapılandırmak için ile Merhaba adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="6cce1-106">This article provides you with hello steps for configuring hello automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="6cce1-107">Hakkında daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="6cce1-107">For more information about:</span></span>

- <span data-ttu-id="6cce1-108">Koşullu erişim bkz [Azure Active Directory cihaz temelli koşullu erişim](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6cce1-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="6cce1-109">Windows 10 cihazları hello çalışma alanına ve Azure AD ile kaydolurken hello geliştirilmiş deneyimler görmek [hello kuruluş için Windows 10: cihazları iş için kullanmak](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6cce1-109">Windows 10 devices in hello workplace and hello enhanced experiences when registered with Azure AD, see [Windows 10 for hello enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="6cce1-110">Windows 10 Kurumsal E3 CSP içinde bkz hello [Windows 10 Kurumsal E3 CSP genel bakış](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="6cce1-110">Windows 10 Enterprise E3 in CSP, see hello [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="6cce1-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="6cce1-111">Before you begin</span></span>

<span data-ttu-id="6cce1-112">Ortamınızda Windows etki alanına katılmış cihazların Merhaba otomatik kayıt yapılandırmaya başlamadan önce kendiniz hello desteklenen senaryolar ve hello kısıtlamaları kazanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="6cce1-112">Before you start configuring hello automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="6cce1-113">Merhaba okunabilirliğini hello açıklamaları tooimprove, bu konuda terim aşağıdaki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="6cce1-113">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="6cce1-114">**Windows geçerli aygıtları** -Windows 10 veya Windows Server 2016 çalıştıran toodomain katılmış cihazlarda bu terimi anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-114">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="6cce1-115">**Windows alt düzey aygıtları** -bu terim tooall başvuruyor **desteklenen** çalışan Windows 10 ne Windows Server 2016 etki alanına katılmış Windows cihazları.</span><span class="sxs-lookup"><span data-stu-id="6cce1-115">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="6cce1-116">Geçerli Windows cihazları</span><span class="sxs-lookup"><span data-stu-id="6cce1-116">Windows current devices</span></span>

- <span data-ttu-id="6cce1-117">Merhaba Windows masaüstü işletim sistemi çalıştıran cihazlar için Windows 10 Anniversary güncelleştirme (sürüm 1607) kullanılmasını öneririz veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="6cce1-117">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="6cce1-118">Merhaba geçerli Windows cihazlarının kaydı **olan** parola karma eşitlemesi yapılandırmaları gibi Federasyon olmayan ortamlarda desteklenir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-118">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="6cce1-119">Windows alt düzey aygıtları</span><span class="sxs-lookup"><span data-stu-id="6cce1-119">Windows down-level devices</span></span>

- <span data-ttu-id="6cce1-120">Windows alt düzey aygıtları aşağıdaki hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="6cce1-120">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="6cce1-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="6cce1-121">Windows 8.1</span></span>
    - <span data-ttu-id="6cce1-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="6cce1-122">Windows 7</span></span>
    - <span data-ttu-id="6cce1-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="6cce1-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="6cce1-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="6cce1-124">Windows Server 2012</span></span>
    - <span data-ttu-id="6cce1-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="6cce1-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="6cce1-126">Merhaba Windows alt düzey cihazlarının kaydı **olan** sorunsuz çoklu oturum açma ile federe olmayan ortamlarda desteklenen [Azure Active Directory sorunsuz çoklu oturum açma](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="6cce1-126">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="6cce1-127">Merhaba Windows alt düzey cihazlarının kaydı **değil** dolaşım profilleri kullanarak cihazları için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-127">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="6cce1-128">Dolaşım profilleri veya ayarlarını FQDN'yi kullanıyorsanız, Windows 10 kullanın.</span><span class="sxs-lookup"><span data-stu-id="6cce1-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="6cce1-129">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6cce1-129">Prerequisites</span></span>

<span data-ttu-id="6cce1-130">Etki alanına katılmış cihazların kuruluşunuzdaki hello otomatik kaydı etkinleştirme başlamadan önce Azure AD güncel bir sürümünü çalıştırdığından emin toomake gerekir bağlanın.</span><span class="sxs-lookup"><span data-stu-id="6cce1-130">Before you start enabling hello auto-registration of domain-joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="6cce1-131">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="6cce1-131">Azure AD Connect:</span></span>

- <span data-ttu-id="6cce1-132">Şirket içi Active Directory (AD) ve Azure AD'de hello cihaz nesnesi hello bilgisayar hesabını arasındaki ilişkiyi Hello tutar.</span><span class="sxs-lookup"><span data-stu-id="6cce1-132">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="6cce1-133">Başka bir aygıt etkinleştirir ilgili özellikler gibi iş için Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="6cce1-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="6cce1-134">Yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="6cce1-134">Configuration steps</span></span>

<span data-ttu-id="6cce1-135">Bu konuda, tüm normal yapılandırma senaryoları için gerekli hello adımlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-135">This topic includes hello required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="6cce1-136">Aşağıdaki tablo tooget senaryonuz için gerekli olan hello adımlara genel bir bakış hello kullan:</span><span class="sxs-lookup"><span data-stu-id="6cce1-136">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="6cce1-137">Adımlar</span><span class="sxs-lookup"><span data-stu-id="6cce1-137">Steps</span></span>                                      | <span data-ttu-id="6cce1-138">Windows geçerli ve parola karma eşitlemesi</span><span class="sxs-lookup"><span data-stu-id="6cce1-138">Windows current and password hash sync</span></span> | <span data-ttu-id="6cce1-139">Windows geçerli ve Federasyon</span><span class="sxs-lookup"><span data-stu-id="6cce1-139">Windows current and federation</span></span> | <span data-ttu-id="6cce1-140">Alt düzey Windows</span><span class="sxs-lookup"><span data-stu-id="6cce1-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="6cce1-141">1. adım: hizmet bağlantı noktası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6cce1-141">Step 1: Configure service connection point</span></span> | ![İşaretli][1]                            | ![İşaretli][1]                    | ![İşaretli][1]        |
| <span data-ttu-id="6cce1-145">2. adım: talep verme kurma</span><span class="sxs-lookup"><span data-stu-id="6cce1-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![İşaretli][1]                    | ![İşaretli][1]        |
| <span data-ttu-id="6cce1-148">3. adım: Windows 10 cihazları etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="6cce1-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![İşaretli][1]        |
| <span data-ttu-id="6cce1-150">Adım 4: Denetimi dağıtımı ve dağıtım</span><span class="sxs-lookup"><span data-stu-id="6cce1-150">Step 4: Control deployment and rollout</span></span>     | ![İşaretli][1]                            | ![İşaretli][1]                    | ![İşaretli][1]        |
| <span data-ttu-id="6cce1-154">5. adım: kayıtlı cihazlar doğrulayın</span><span class="sxs-lookup"><span data-stu-id="6cce1-154">Step 5: Verify registered devices</span></span>          | ![İşaretli][1]                            | ![İşaretli][1]                    | ![İşaretli][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="6cce1-158">1. adım: hizmet bağlantı noktası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6cce1-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="6cce1-159">Merhaba hizmet bağlantı noktası (SCP) nesnesinin hello kayıt toodiscover sırasında Azure AD Kiracı bilgilerini cihazlar tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6cce1-159">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="6cce1-160">Şirket içi Active Directory (AD), etki alanına katılmış cihazların Merhaba otomatik kaydı için hello SCP nesnesi hello yapılandırma adlandırma bağlamı bölümünde hello bilgisayarın orman mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6cce1-160">In your on-premises Active Directory (AD), hello SCP object for hello auto-registration of domain-joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="6cce1-161">Her ormanda yalnızca bir yapılandırma adlandırma bağlamında yoktur.</span><span class="sxs-lookup"><span data-stu-id="6cce1-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="6cce1-162">Bir Çoklu orman Active Directory yapılandırması, etki alanına katılmış bilgisayarları içeren tüm ormanlarda hello hizmet bağlantı noktası mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6cce1-162">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="6cce1-163">Merhaba kullanabilirsiniz [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello yapılandırma adlandırma bağlamında ormanınızın.</span><span class="sxs-lookup"><span data-stu-id="6cce1-163">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="6cce1-164">Merhaba Active Directory etki alanı adına sahip bir orman için *fabrikam.com*, hello yapılandırma adlandırma bağlamında değil:</span><span class="sxs-lookup"><span data-stu-id="6cce1-164">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="6cce1-165">Ormanınıza hello otomatik kaydı etki alanına katılmış cihazlar için hello SCP nesnesi şu konumdadır:</span><span class="sxs-lookup"><span data-stu-id="6cce1-165">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="6cce1-166">Nasıl Azure AD Connect dağıttığınız bağlı olarak, hello SCP nesnesi zaten yapılandırılmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-166">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="6cce1-167">Hello nesne hello varlığını doğrulayın ve Windows PowerShell Betiği aşağıdaki hello kullanarak hello bulma değerleri alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6cce1-167">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="6cce1-168">Merhaba **$scp. Anahtar sözcükler** çıktı hello Azure AD Kiracı bilgileri, örneğin gösterir:</span><span class="sxs-lookup"><span data-stu-id="6cce1-168">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="6cce1-169">Merhaba hizmet bağlantı noktası mevcut değilse, bunu hello çalıştırarak oluşturabilirsiniz `Initialize-ADSyncDomainJoinedComputerSync` Azure AD Connect sunucunuzda cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="6cce1-169">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="6cce1-170">Kuruluş yönetici kimlik bilgileri gerekli toorun bu cmdlet'tir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-170">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="6cce1-171">Merhaba cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6cce1-171">hello cmdlet:</span></span>

- <span data-ttu-id="6cce1-172">Azure AD Connect bağlı hello Active Directory ormanındaki Hello hizmet bağlantı noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6cce1-172">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="6cce1-173">Toospecify hello gerektirir `AdConnectorAccount` parametresi.</span><span class="sxs-lookup"><span data-stu-id="6cce1-173">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="6cce1-174">Active Directory Bağlayıcısı hesabı Azure ad connect yapılandırılmış hello hesap budur.</span><span class="sxs-lookup"><span data-stu-id="6cce1-174">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="6cce1-175">Merhaba aşağıdaki komut dosyası hello cmdlet'ini kullanarak bir örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-175">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="6cce1-176">Bu komut `$aadAdminCred = Get-Credential` tootype bir kullanıcı adı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-176">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="6cce1-177">Merhaba kullanıcı asıl adı (UPN) biçiminde tooprovide hello kullanıcı adı gerekir (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="6cce1-177">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="6cce1-178">Merhaba `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6cce1-178">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="6cce1-179">Bir etki alanı denetleyicisinde çalışan Active Directory Web Hizmetleri dayanan hello Active Directory PowerShell modülü kullanır.</span><span class="sxs-lookup"><span data-stu-id="6cce1-179">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="6cce1-180">Active Directory Web Hizmetleri, Windows Server 2008 R2 çalıştıran etki alanı denetleyicilerinde ve üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="6cce1-181">Yalnızca hello tarafından desteklenen **MSOnline PowerShell modülü sürümü 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-181">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="6cce1-182">toodownload bu modül bu [bağlantı](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="6cce1-182">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="6cce1-183">Windows Server 2008 veya önceki sürümlerini çalıştıran etki alanı denetleyicileri için toocreate hello hizmet bağlantı noktası aşağıdaki hello komut dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="6cce1-183">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="6cce1-184">Bir Çoklu orman yapılandırması, komut dosyası toocreate hello hizmet bağlantı noktası bilgisayarları var olduğu her bir orman içinde aşağıdaki hello kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6cce1-184">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="6cce1-185">2. adım: talep verme kurma</span><span class="sxs-lookup"><span data-stu-id="6cce1-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="6cce1-186">Bir Federasyon Azure AD yapılandırma cihazlar Active Directory Federasyon Hizmetleri (AD FS) üzerinde kullanır veya 3. taraf bir Federasyon Hizmeti tooauthenticate tooAzure AD şirket içi.</span><span class="sxs-lookup"><span data-stu-id="6cce1-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="6cce1-187">Aygıtları tooget bir erişim belirteci tooregister hello Azure Active Directory cihaz kayıt Hizmeti'ne (Azure DRS) karşı kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="6cce1-187">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="6cce1-188">Windows hello şirket içi Federasyon Hizmeti tarafından barındırılan tümleşik Windows kimlik doğrulaması tooan etkin WS-Trust uç noktası (1.3 veya 2005 sürümler) kullanarak geçerli aygıtların kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="6cce1-188">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="6cce1-189">AD FS, ya da kullanırken **adfs/services/güven/13/windowstransport** veya **adfs/services/güven/2005/windowstransport** etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="6cce1-190">Ayrıca hello Web kimlik doğrulaması Proxy kullanıyorsanız, bu uç noktaya hello proxy üzerinden yayımlanan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6cce1-190">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="6cce1-191">Hangi uç noktalarının altında hello AD FS Yönetim Konsolu aracılığıyla özelliğinin etkinleştirilip etkinleştirilmediğini **hizmet > uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-191">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="6cce1-192">AD FS, şirket içi Federasyon Hizmeti olarak yoksa, WS-Trust 1.3 veya 2005 uç noktalarının ve bunlar hello meta veri değişimi dosya (MEX) yayımlanır desteklediğinden emin, satıcı toomake hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="6cce1-192">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="6cce1-193">Merhaba aşağıdaki talep için cihaz kayıt toocomplete Azure DRS tarafından alınan hello belirtecindeki mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-193">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="6cce1-194">Azure DRS Azure AD ile sonra Azure AD Connect tooassociate yeni oluşturulan hello cihaz nesnesi hello bilgisayar hesabı şirket tarafından kullanılan bu bilgilerin bazıları, bir cihaz nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6cce1-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="6cce1-195">Birden fazla doğrulanan etki alanı adı varsa, talep bilgisayarlar için aşağıdaki tooprovide hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6cce1-195">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="6cce1-196">Zaten bir İmmutableıd talep (örn., alternatif oturum açma kimliği) dağıttığınız bilgisayarlar için bir karşılık gelen talep tooprovide gerekir:</span><span class="sxs-lookup"><span data-stu-id="6cce1-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="6cce1-197">Aşağıdaki bölümlerde hello hakkında bilgiler yer:</span><span class="sxs-lookup"><span data-stu-id="6cce1-197">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="6cce1-198">Merhaba değerleri her talep olmalıdır</span><span class="sxs-lookup"><span data-stu-id="6cce1-198">hello values each claim should have</span></span>
- <span data-ttu-id="6cce1-199">Nasıl bir tanımı gibi AD FS'de görüneceği</span><span class="sxs-lookup"><span data-stu-id="6cce1-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="6cce1-200">Merhaba tanımı yardımcı olan tooverify hello değerleri mevcut olup olmadığını veya toocreate ihtiyacınız varsa, bunları.</span><span class="sxs-lookup"><span data-stu-id="6cce1-200">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="6cce1-201">Şirket içi Federasyon sunucunuz için AD FS kullanmıyorsanız, bu talepler satıcınızın yönergeleri toocreate hello uygun yapılandırma tooissue izleyin.</span><span class="sxs-lookup"><span data-stu-id="6cce1-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="6cce1-202">Sorunu hesap türü talep</span><span class="sxs-lookup"><span data-stu-id="6cce1-202">Issue account type claim</span></span>

<span data-ttu-id="6cce1-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Bu talep değerini içermelidir **DJ**, hello cihaz etki alanına katılmış bir bilgisayar olarak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6cce1-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="6cce1-204">AD FS'de şuna benzer bir verme dönüştürme kural ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6cce1-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="6cce1-205">Sorunu objectGUID hello bilgisayar hesabı şirket içinde</span><span class="sxs-lookup"><span data-stu-id="6cce1-205">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="6cce1-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Bu talep hello içermelidir **objectGUID** hello değerini şirket içi bilgisayar hesabı.</span><span class="sxs-lookup"><span data-stu-id="6cce1-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="6cce1-207">AD FS'de şuna benzer bir verme dönüştürme kural ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6cce1-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="6cce1-208">Sorunu objectSID hello bilgisayar hesabı şirket içinde</span><span class="sxs-lookup"><span data-stu-id="6cce1-208">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="6cce1-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Bu talep hello hello içermelidir **objectSID** hello değerini şirket içi bilgisayar hesabı.</span><span class="sxs-lookup"><span data-stu-id="6cce1-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="6cce1-210">AD FS'de şuna benzer bir verme dönüştürme kural ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6cce1-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="6cce1-211">Birden çok etki alanı adlarını Azure AD'de belirlediğinizde issuerID bilgisayar için sorun</span><span class="sxs-lookup"><span data-stu-id="6cce1-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="6cce1-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Bu talep hello hiçbirinin Tekdüzen Kaynak Tanımlayıcısı (URI) ile Merhaba bağlanmak etki alanı adları şirket içi Federasyon Hizmeti (AD FS veya 3. taraf) sertifika veren hello belirteci doğrulandı hello içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="6cce1-213">AD FS içinde sonra belirli bir sıraya Merhaba, olanları yukarıdaki olanları aşağıdaki hello gibi görünmesini verme dönüştürme kuralları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6cce1-213">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="6cce1-214">Lütfen gerekli kullanıcılar için bir kural tooexplicitly sorunu hello kural unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6cce1-214">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="6cce1-215">Merhaba kuralları'nda aşağıdaki kullanıcı ve bilgisayar kimlik doğrulaması tanımlama ilk bir kuralı eklenir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-215">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

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


<span data-ttu-id="6cce1-216">Yukarıdaki Hello talep kümesinde</span><span class="sxs-lookup"><span data-stu-id="6cce1-216">In hello claim above,</span></span>

- <span data-ttu-id="6cce1-217">`$<domain>`Merhaba AD FS hizmet URL'si</span><span class="sxs-lookup"><span data-stu-id="6cce1-217">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="6cce1-218">`<verified-domain-name>`tooreplace doğrulanmış etki alanı adlarınızı biri ile Azure AD içinde gereksinim duyduğunuz bir yer tutucudur</span><span class="sxs-lookup"><span data-stu-id="6cce1-218">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="6cce1-219">Doğrulanmış etki alanı adları hakkında daha fazla ayrıntı için bkz: [özel etki alanı adı tooAzure Active Directory eklemek](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="6cce1-219">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="6cce1-220">tooget doğrulanmış şirket etki alanlarının bir listesini, kullanabileceğiniz hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="6cce1-220">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="6cce1-222">Kullanıcılar için bir tane bulunduğunda (kimliği ayarlanmadan örneğin alternatif oturum açma) İmmutableıd bilgisayar için sorun</span><span class="sxs-lookup"><span data-stu-id="6cce1-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="6cce1-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**-Bu talep bilgisayarlar için geçerli bir değer içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="6cce1-224">AD FS içinde verme dönüştürme kural aşağıdaki gibi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6cce1-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="6cce1-225">Yardımcı betik toocreate hello AD FS verme dönüştürme kuralları</span><span class="sxs-lookup"><span data-stu-id="6cce1-225">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="6cce1-226">Merhaba aşağıdaki betiği hello verme hello oluşturulmasını ile yukarıda açıklanan kuralları dönüştürme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="6cce1-226">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

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

### <a name="remarks"></a><span data-ttu-id="6cce1-227">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="6cce1-227">Remarks</span></span> 

- <span data-ttu-id="6cce1-228">Bu komut dosyası hello kuralları toohello mevcut kurallar ekler.</span><span class="sxs-lookup"><span data-stu-id="6cce1-228">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="6cce1-229">Merhaba kuralları ayarlamak için çalışmıyor hello betik iki kez iki kez eklenir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-229">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="6cce1-230">Karşılık gelen hiçbir kural (koşullarda hello karşılık gelen) bu talepler için hello betiği yeniden çalıştırmadan önce var olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6cce1-230">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="6cce1-231">Merhaba değerini ayarlayın (hello Azure AD portalında veya hello Get-MsolDomains cmdlet'i aracılığıyla gösterildiği gibi) birden çok doğrulanmış etki alanı adı, varsa **$multipleVerifiedDomainNames** hello çok komut dosyası**$true**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-231">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="6cce1-232">Ayrıca Azure AD Connect veya başka yöntemler aracılığıyla oluşturulan tüm mevcut issuerid talep kaldırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6cce1-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="6cce1-233">Bu kural için örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="6cce1-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="6cce1-234">Zaten yayımlandı durumunda bir **İmmutableıd** hello değeri olarak ayarlayın, kullanıcı hesapları için talep **$immutableIDAlreadyIssuedforUsers** hello çok komut dosyası**$true**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-234">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="6cce1-235">Adım 3: Windows alt düzey aygıtları etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="6cce1-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="6cce1-236">Bazı etki alanına katılmış aygıtlarınız Windows cihazları sürümlerdeki, gerekir:</span><span class="sxs-lookup"><span data-stu-id="6cce1-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="6cce1-237">Bir ilke Azure AD tooenable kullanıcılar tooregister aygıtları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6cce1-237">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="6cce1-238">Şirket içi Federasyon Hizmeti tooissue talep toosupport yapılandırma **tümleşik Windows kimlik doğrulaması (IWA)** cihaz kaydı için.</span><span class="sxs-lookup"><span data-stu-id="6cce1-238">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="6cce1-239">Merhaba aygıt doğrulanırken tooavoid sertifika ister hello Azure AD cihaz kimlik doğrulama uç noktası toohello yerel Intranet bölgeler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6cce1-239">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="6cce1-240">İlke Azure AD tooenable kullanıcılar tooregister aygıtları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6cce1-240">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="6cce1-241">tooregister Windows alt düzey aygıtları toomake tooallow kullanıcılar Azure AD'de tooregister cihazları ayarlama bu hello ayarlandığından emin gerekir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-241">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="6cce1-242">Hello Azure portalı, bu ayarı altında bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6cce1-242">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="6cce1-243">Merhaba aşağıdaki İlkesi çok ayarlanmalıdır**tüm**: **kullanıcıları Azure AD ile cihazlarını kaydetme**</span><span class="sxs-lookup"><span data-stu-id="6cce1-243">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![Cihaz kaydetme](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="6cce1-245">Şirket içi Federasyon hizmetini yapılandır</span><span class="sxs-lookup"><span data-stu-id="6cce1-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="6cce1-246">Şirket içi Federasyon hizmetinizi veren hello desteklemelidir **authenticationmehod** ve **wiaormultiauthn** bir kimlik doğrulama alırken talep isteği toohello Azure AD bağlı olan taraf bulunduran bir resouce_params parametre gösterildiği gibi kodlanmış bir değeri olan aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="6cce1-246">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="6cce1-247">Böyle bir istek geldiğinde, hello şirket içi Federasyon Hizmeti tümleşik Windows kimlik doğrulaması kullanarak hello kullanıcı kimlik doğrulaması yapmalıdır ve başarı iki talep aşağıdaki hello kesmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6cce1-247">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="6cce1-248">AD FS içinde verme dönüştürme kural bu geçişleri üzerinden hello kimlik doğrulama yöntemi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-248">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="6cce1-249">**tooadd bu kural:**</span><span class="sxs-lookup"><span data-stu-id="6cce1-249">**tooadd this rule:**</span></span>

1. <span data-ttu-id="6cce1-250">Merhaba AD FS yönetim konsolunda çok Git`AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="6cce1-250">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="6cce1-251">Merhaba Microsoft Office 365 kimlik Platformu'na bağlı taraf güven nesnesi sağ tıklayın ve ardından **talep kurallarını Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-251">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="6cce1-252">Merhaba üzerinde **verme dönüştürme kuralları** sekmesine **Kuralı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-252">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="6cce1-253">Merhaba, **talep kuralı** şablonu listesinden **talepleri özel kural kullanarak Gönder**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-253">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="6cce1-254">Seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-254">Select **Next**.</span></span>
6. <span data-ttu-id="6cce1-255">Merhaba, **talep kuralı adı** kutusuna **kimlik doğrulama yöntemi talep kuralı**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-255">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="6cce1-256">Merhaba, **talep kuralı** kutusu, aşağıdaki kural türü hello:</span><span class="sxs-lookup"><span data-stu-id="6cce1-256">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="6cce1-257">Değiştirildikten sonra Federasyon sunucunuzda aşağıdaki hello PowerShell komutunu yazın  **\<RPObjectName\>**  hello bağlı olan taraf için nesne adı, Azure AD bağlı olan taraf güven nesnesi ile.</span><span class="sxs-lookup"><span data-stu-id="6cce1-257">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="6cce1-258">Bu nesne genellikle adlı **Microsoft Office 365 kimlik Platformu'na**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="6cce1-259">Hello Azure AD cihaz kimlik doğrulama uç noktası toohello yerel Intranet bölgeler ekleyin</span><span class="sxs-lookup"><span data-stu-id="6cce1-259">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="6cce1-260">tooAzure Internet Explorer'da URL toohello yerel Intranet bölgesine izleyen bir ilke tooyour etki alanına katılmış aygıtlar tooadd hello gönderebilir AD kaydı cihazları kullanıcıların kimliğini doğrularken tooavoid sertifika ister:</span><span class="sxs-lookup"><span data-stu-id="6cce1-260">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="6cce1-261">Adım 4: Denetimi dağıtımı ve dağıtım</span><span class="sxs-lookup"><span data-stu-id="6cce1-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="6cce1-262">Merhaba gerekli adımları tamamladıktan sonra etki alanına katılmış hazır tooautomatically kayıt Azure AD ile aygıtlardır.</span><span class="sxs-lookup"><span data-stu-id="6cce1-262">When you have completed hello required steps, domain-joined devices are ready tooautomatically register with Azure AD.</span></span> <span data-ttu-id="6cce1-263">Windows 10 Anniversary güncelleştirmesi ve Windows Server 2016 çalıştıran tüm etki alanına katılmış cihazlar otomatik olarak kayıt aygıt adresindeki Azure AD ile yeniden başlatın veya kullanıcı oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6cce1-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="6cce1-264">Yeni cihazların Merhaba etki alanına katılma işlemi tamamlandıktan sonra hello aygıt yeniden başlatıldığında Azure AD ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6cce1-264">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

<span data-ttu-id="6cce1-265">Daha önce çalışma alanına katılmış tooAzure AD (örneğin Intune) geçişi çok olan cihaz"*etki alanına katılmış, AAD kayıtlı*"; Ancak, gereken süre bu işlem toocomplete için toohello normal son tüm cihazlar arasında etki alanı ve kullanıcı etkinliğini akışı.</span><span class="sxs-lookup"><span data-stu-id="6cce1-265">Devices that were previously workplace-joined tooAzure AD (for example for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="6cce1-266">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="6cce1-266">Remarks</span></span>

- <span data-ttu-id="6cce1-267">Windows 10 ve Windows Server 2016 etki alanına katılmış bilgisayarlar otomatik kaydını bir Grup İlkesi nesnesi toocontrol hello sunumu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6cce1-267">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="6cce1-268">Windows 10 Kasım 2015 güncelleştirmesi otomatik olarak yazmaçlar Azure AD ile **yalnızca** hello sunum Grup İlkesi nesnesi ayarlarsanız.</span><span class="sxs-lookup"><span data-stu-id="6cce1-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="6cce1-269">dağıtabileceğiniz Windows alt düzey bilgisayarların toorollout hello otomatik kayıt, bir [Windows Installer paketi](#windows-installer-packages-for-non-windows-10-computers) seçtiğiniz toocomputers.</span><span class="sxs-lookup"><span data-stu-id="6cce1-269">toorollout hello automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="6cce1-270">Merhaba Grup İlkesi nesnesi tooWindows 8.1 etki alanına katılmış aygıtlar itme, kayıt denenecek; Ancak, hello kullanmanız önerilir [Windows Installer paketi](#windows-installer-packages-for-non-windows-10-computers) tooregister tüm Windows alt düzey cihazlar.</span><span class="sxs-lookup"><span data-stu-id="6cce1-270">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) tooregister all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="6cce1-271">Bir Grup İlkesi nesnesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6cce1-271">Create a Group Policy object</span></span> 

<span data-ttu-id="6cce1-272">toocontrol hello sunum otomatik kayıt geçerli bilgisayarların Windows hello dağıtmalısınız **etki alanına katılmış bilgisayarları cihaz olarak kaydetme** tooregister istediğiniz Grup İlkesi nesnesi toohello aygıtlar.</span><span class="sxs-lookup"><span data-stu-id="6cce1-272">toocontrol hello rollout of automatic registration of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="6cce1-273">Örneğin, hello İlkesi tooan kuruluş birimi ya da tooa güvenlik grubu dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6cce1-273">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="6cce1-274">**tooset hello İlkesi:**</span><span class="sxs-lookup"><span data-stu-id="6cce1-274">**tooset hello policy:**</span></span>

1. <span data-ttu-id="6cce1-275">Açık **Sunucu Yöneticisi'ni**ve çok Git`Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="6cce1-275">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="6cce1-276">Windows geçerli bilgisayarların tooactivate otomatik kaydı istediğiniz toohello etki alanı karşılık gelen toohello etki alanı düğümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="6cce1-276">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="6cce1-277">Sağ **Grup İlkesi nesneleri**ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="6cce1-278">Grup İlkesi nesnesi için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="6cce1-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="6cce1-279">Örneğin, *otomatik kayıt tooAzure AD*.</span><span class="sxs-lookup"><span data-stu-id="6cce1-279">For example, *Automatic Registration tooAzure AD*.</span></span> <span data-ttu-id="6cce1-280">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6cce1-280">Select **OK**.</span></span>
5. <span data-ttu-id="6cce1-281">Yeni Grup İlkesi nesneniz sağ tıklayın ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="6cce1-282">Çok Git**Bilgisayar Yapılandırması** > **ilkeleri** > **Yönetim Şablonları** > **Windows Bileşenleri** > **aygıt kaydı**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-282">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="6cce1-283">Sağ **etki alanına katılmış bilgisayarları cihaz olarak kaydetme**ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6cce1-284">Bu Grup İlkesi şablonu hello Grup İlkesi Yönetimi konsolunun önceki sürümlerden adlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="6cce1-284">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="6cce1-285">Merhaba konsol önceki bir sürümünü kullanıyorsanız, çok Git`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="6cce1-285">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="6cce1-286">Seçin **etkin**ve ardından **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="6cce1-287">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6cce1-287">Select **OK**.</span></span>
9. <span data-ttu-id="6cce1-288">Bağlantı hello Grup İlkesi nesnesi tooa konum.</span><span class="sxs-lookup"><span data-stu-id="6cce1-288">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="6cce1-289">Örneğin, tooa belirli bir kuruluş birimine bağlantı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6cce1-289">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="6cce1-290">Ayrıca Azure AD ile otomatik olarak kaydedilecek bilgisayarların tooa belirli bir güvenlik grubu bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6cce1-290">You also could link it tooa specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="6cce1-291">tooset Bu ilke tüm etki alanına katılmış Windows 10 ve Windows Server 2016 kuruluşunuzdaki bilgisayarların, bağlantı hello Grup İlkesi nesnesi toohello etki alanı için.</span><span class="sxs-lookup"><span data-stu-id="6cce1-291">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="6cce1-292">Windows 10 bilgisayarları için Windows Installer paketleri</span><span class="sxs-lookup"><span data-stu-id="6cce1-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="6cce1-293">tooregister etki alanına katılmış Windows alt düzey bilgisayarları Federasyon ortamında, indirin ve bu Windows Installer (.msi) paketi İndirme Merkezi'nden hello yükleyin [Microsoft çalışma alanına katılma için Windows 10 bilgisayarları](https://www.microsoft.com/en-us/download/details.aspx?id=53554) sayfası.</span><span class="sxs-lookup"><span data-stu-id="6cce1-293">tooregister domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="6cce1-294">Bir yazılım dağıtım sistemi gibi System Center Configuration Manager kullanılarak hello paketi dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6cce1-294">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="6cce1-295">Merhaba paketi destekler hello hello standart sessiz yükleme seçenekleriyle *sessiz* parametresi.</span><span class="sxs-lookup"><span data-stu-id="6cce1-295">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="6cce1-296">System Center Configuration Manager geçerli dalının hello özelliği tamamlandı tootrack kayıtlar gibi önceki sürümlerinden ek avantajlar sunar.</span><span class="sxs-lookup"><span data-stu-id="6cce1-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="6cce1-297">Daha fazla bilgi için bkz: [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="6cce1-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="6cce1-298">Hello yükleyici hello sistemde hello kullanıcının bağlamında çalışan zamanlanmış bir görev oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6cce1-298">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="6cce1-299">içinde tooWindows Hello kullanıcı oturum açtığında hello görevi tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-299">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="6cce1-300">Başlangıç görevi hello aygıt hello kullanıcı kimlik bilgileriyle tümleşik Windows kimlik doğrulaması kullanarak kimlik doğrulama sonra Azure AD ile sessizce kaydeder.</span><span class="sxs-lookup"><span data-stu-id="6cce1-300">hello task silently registers hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="6cce1-301">toosee hello zamanlanan görev hello aygıtta Git çok**Microsoft** > **çalışma alanına katılma**, ve ardından toohello Görev Zamanlayıcı Kitaplığı gidin.</span><span class="sxs-lookup"><span data-stu-id="6cce1-301">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="6cce1-302">5. adım: kayıtlı cihazlar doğrulayın</span><span class="sxs-lookup"><span data-stu-id="6cce1-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="6cce1-303">Hello kullanarak, kuruluşunuzda başarılı kayıtlı cihazlar denetleyebilirsiniz [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) hello cmdlet'te [Azure Active Directory PowerShell Modülü](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="6cce1-303">You can check successful registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="6cce1-304">Merhaba bu cmdlet'in çıktısı, Azure AD'de kayıtlı cihazları gösterir.</span><span class="sxs-lookup"><span data-stu-id="6cce1-304">hello output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="6cce1-305">tooget, tüm cihazların Merhaba kullanmak **-tüm** parametre ve filtre hello kullanarak bunları **deviceTrustType** özelliği.</span><span class="sxs-lookup"><span data-stu-id="6cce1-305">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="6cce1-306">Etki alanına katılmış aygıtlar değerine sahip **etki alanına katılmış**.</span><span class="sxs-lookup"><span data-stu-id="6cce1-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cce1-307">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6cce1-307">Next steps</span></span>

* [<span data-ttu-id="6cce1-308">Otomatik cihaz kaydı SSS</span><span class="sxs-lookup"><span data-stu-id="6cce1-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="6cce1-309">Birleştirilmiş bilgisayarlar tooAzure AD – Windows 10 ve Windows Server 2016 etki alanının otomatik kayıt sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="6cce1-309">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="6cce1-310">Birleştirilmiş bilgisayarlar tooAzure AD – Windows 10 etki alanının otomatik kayıt sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="6cce1-310">Troubleshooting auto-registration of domain joined computers tooAzure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="6cce1-311">Azure Active Directory koşullu erişimi</span><span class="sxs-lookup"><span data-stu-id="6cce1-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
