---
title: "Karma yapılandırmak için Azure Active Directory'ye katılmış cihazlarda nasıl | Microsoft Docs"
description: "Karma Azure Active Directory'ye katılmış cihazları yapılandırmayı öğrenin."
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
ms.openlocfilehash: 4580075df9fce74664b22aa24065ba1885692384
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-hybrid-azure-active-directory-joined-devices"></a><span data-ttu-id="952da-103">Karma Azure Active Directory'ye katılmış cihazları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="952da-103">How to configure hybrid Azure Active Directory joined devices</span></span>

<span data-ttu-id="952da-104">Azure Active Directory'de (Azure AD) ile cihaz yönetimi, güvenlik ve uyumluluğa yönelik standartlarınızı karşılamak aygıtlardan kullanıcılarınızın kaynaklarınızı eriştiğiniz emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="952da-104">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> <span data-ttu-id="952da-105">Daha fazla ayrıntı için bkz: [Azure Active Directory'de cihaz yönetimine giriş](device-management-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="952da-105">For more details, see [Introduction to device management in Azure Active Directory](device-management-introduction.md).</span></span>

<span data-ttu-id="952da-106">Şirket içi Active Directory ortamında varsa ve Azure AD etki alanına katılmış cihazlarınızı katılmasını istediğiniz, bu karma Azure AD alanına katılmış cihazları yapılandırarak gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="952da-106">If you have an on-premises Active Directory environment and you want to join your domain-joined devices to Azure AD, you can accomplish this by configuring hybrid Azure AD joined devices.</span></span> <span data-ttu-id="952da-107">Konu ile ilgili adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="952da-107">The topic provides you with the related steps.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="952da-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="952da-108">Before you begin</span></span>

<span data-ttu-id="952da-109">Karma Azure AD alanına katılmış aygıtlar ortamınızda yapılandırmaya başlamadan önce kendiniz desteklenen senaryolar ve kısıtlamalar ile kazanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="952da-109">Before you start configuring hybrid Azure AD joined devices in your environment, you should familiarize yourself with the supported scenarios and the constraints.</span></span>  

<span data-ttu-id="952da-110">Açıklamaları okunabilirliğini artırmak için bu konuda aşağıdaki terim kullanır:</span><span class="sxs-lookup"><span data-stu-id="952da-110">To improve the readability of the descriptions, this topic uses the following term:</span></span> 

- <span data-ttu-id="952da-111">**Windows geçerli aygıtları** -Windows 10 veya Windows Server 2016 çalıştıran etki alanına katılmış cihazlar için bu terim başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="952da-111">**Windows current devices** - This term refers to domain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="952da-112">**Windows alt düzey aygıtları** -bu terim tümüne başvuruyor **desteklenen** çalışan Windows 10 ne Windows Server 2016 etki alanına katılmış Windows cihazları.</span><span class="sxs-lookup"><span data-stu-id="952da-112">**Windows down-level devices** - This term refers to all **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="952da-113">Geçerli Windows cihazları</span><span class="sxs-lookup"><span data-stu-id="952da-113">Windows current devices</span></span>

- <span data-ttu-id="952da-114">Windows masaüstü işletim sistemi çalıştıran cihazlar için Windows 10 Anniversary güncelleştirme (sürüm 1607) kullanılmasını öneririz veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="952da-114">For devices running the Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="952da-115">Geçerli Windows cihazlarının kaydı **olan** parola karma eşitlemesi yapılandırmaları gibi Federasyon olmayan ortamlarda desteklenir.</span><span class="sxs-lookup"><span data-stu-id="952da-115">The registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="952da-116">Windows alt düzey aygıtları</span><span class="sxs-lookup"><span data-stu-id="952da-116">Windows down-level devices</span></span>

- <span data-ttu-id="952da-117">Aşağıdaki Windows alt düzey aygıtları desteklenir:</span><span class="sxs-lookup"><span data-stu-id="952da-117">The following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="952da-118">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="952da-118">Windows 8.1</span></span>
    - <span data-ttu-id="952da-119">Windows 7</span><span class="sxs-lookup"><span data-stu-id="952da-119">Windows 7</span></span>
    - <span data-ttu-id="952da-120">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="952da-120">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="952da-121">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="952da-121">Windows Server 2012</span></span>
    - <span data-ttu-id="952da-122">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="952da-122">Windows Server 2008 R2</span></span>
- <span data-ttu-id="952da-123">Windows alt düzey aygıtları kaydını **olan** sorunsuz çoklu oturum açma ile federe olmayan ortamlarda desteklenen [Azure Active Directory sorunsuz çoklu oturum açma](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="952da-123">The registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="952da-124">Windows alt düzey aygıtları kaydını **değil** dolaşım profilleri kullanarak cihazları için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="952da-124">The registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="952da-125">Dolaşım profilleri veya ayarlarını FQDN'yi kullanıyorsanız, Windows 10 kullanın.</span><span class="sxs-lookup"><span data-stu-id="952da-125">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="952da-126">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="952da-126">Prerequisites</span></span>

<span data-ttu-id="952da-127">Karma Azure AD alanına katılmış cihazları, kuruluşunuzda etkinleştirmeye başlamadan önce Azure AD güncel bir sürümünü çalıştırdığından emin olmanız gerekir bağlanın.</span><span class="sxs-lookup"><span data-stu-id="952da-127">Before you start enabling hybrid Azure AD joined devices in your organization, you need to make sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="952da-128">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="952da-128">Azure AD Connect:</span></span>

- <span data-ttu-id="952da-129">Bilgisayar hesabında şirket içi Active Directory (AD) ve Azure AD cihaz nesne arasındaki ilişkiyi tutar.</span><span class="sxs-lookup"><span data-stu-id="952da-129">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span></span> 
- <span data-ttu-id="952da-130">Başka bir aygıt etkinleştirir ilgili özellikler gibi iş için Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="952da-130">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="952da-131">Yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="952da-131">Configuration steps</span></span>

<span data-ttu-id="952da-132">Karma Azure AD alanına katılmış aygıtlar çeşitli Windows cihaz platformları için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="952da-132">You can configure hybrid Azure AD joined devices for various types of Windows device platforms.</span></span> <span data-ttu-id="952da-133">Bu konu, tüm normal yapılandırma senaryoları için gerekli adımları içerir.</span><span class="sxs-lookup"><span data-stu-id="952da-133">This topic includes the required steps for all typical configuration scenarios.</span></span>  

<span data-ttu-id="952da-134">Senaryonuz için gerekli olan adımları özetini almak için aşağıdaki tabloyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="952da-134">Use the following table to get an overview of the steps that are required for your scenario:</span></span>  



| <span data-ttu-id="952da-135">Adımlar</span><span class="sxs-lookup"><span data-stu-id="952da-135">Steps</span></span>                                      | <span data-ttu-id="952da-136">Windows geçerli ve parola karma eşitlemesi</span><span class="sxs-lookup"><span data-stu-id="952da-136">Windows current and password hash sync</span></span> | <span data-ttu-id="952da-137">Windows geçerli ve Federasyon</span><span class="sxs-lookup"><span data-stu-id="952da-137">Windows current and federation</span></span> | <span data-ttu-id="952da-138">Alt düzey Windows</span><span class="sxs-lookup"><span data-stu-id="952da-138">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="952da-139">1. adım: hizmet bağlantı noktası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="952da-139">Step 1: Configure service connection point</span></span> | ![İşaretli][1]                            | ![İşaretli][1]                    | ![İşaretli][1]        |
| <span data-ttu-id="952da-143">2. adım: talep verme kurma</span><span class="sxs-lookup"><span data-stu-id="952da-143">Step 2: Setup issuance of claims</span></span>           |                                        | ![İşaretli][1]                    | ![İşaretli][1]        |
| <span data-ttu-id="952da-146">3. adım: Windows 10 cihazları etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="952da-146">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![İşaretli][1]        |
| <span data-ttu-id="952da-148">Adım 4: Denetimi dağıtımı ve dağıtım</span><span class="sxs-lookup"><span data-stu-id="952da-148">Step 4: Control deployment and rollout</span></span>     | ![İşaretli][1]                            | ![İşaretli][1]                    | ![İşaretli][1]        |
| <span data-ttu-id="952da-152">5. adım: alanına katılmamış aygıtlar doğrulayın</span><span class="sxs-lookup"><span data-stu-id="952da-152">Step 5: Verify joined devices</span></span>          | ![İşaretli][1]                            | ![İşaretli][1]                    | ![İşaretli][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="952da-156">1. adım: hizmet bağlantı noktası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="952da-156">Step 1: Configure service connection point</span></span>

<span data-ttu-id="952da-157">Hizmet bağlantı noktası (SCP) nesnesi, cihazlar tarafından kayıt sırasında Azure AD Kiracı bilgileri bulmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="952da-157">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span></span> <span data-ttu-id="952da-158">Şirket içi Active Directory (AD), SCP nesnesi karma Azure AD alanına katılmış cihazlar için adlandırma bağlamı bölüm bilgisayarın ormanın yapılandırmada mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="952da-158">In your on-premises Active Directory (AD), the SCP object for the hybrid Azure AD joined devices must exist in the configuration naming context partition of the computer's forest.</span></span> <span data-ttu-id="952da-159">Her ormanda yalnızca bir yapılandırma adlandırma bağlamında yoktur.</span><span class="sxs-lookup"><span data-stu-id="952da-159">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="952da-160">Bir Çoklu orman Active Directory yapılandırması, hizmet bağlantı noktası etki alanına katılmış bilgisayarları içeren tüm ormanlarda mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="952da-160">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="952da-161">Kullanabileceğiniz [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) ormanınızın yapılandırma adlandırma bağlamında almak üzere.</span><span class="sxs-lookup"><span data-stu-id="952da-161">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span></span>  

<span data-ttu-id="952da-162">Active Directory etki alanı adına sahip bir orman için *fabrikam.com*, yapılandırma adlandırma bağlamında değil:</span><span class="sxs-lookup"><span data-stu-id="952da-162">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="952da-163">Ormanınıza etki alanına katılmış cihazların otomatik kayıt için SCP nesnesi şu konumdadır:</span><span class="sxs-lookup"><span data-stu-id="952da-163">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="952da-164">Nasıl Azure AD Connect dağıttığınız bağlı olarak, SCP nesnesi zaten yapılandırılmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="952da-164">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span></span>
<span data-ttu-id="952da-165">Nesne varlığını doğrulayın ve aşağıdaki Windows PowerShell Betiği kullanılarak bulma değerleri alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="952da-165">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="952da-166">**$Scp. Anahtar sözcükler** çıktı Azure AD Kiracı bilgileri örneğin gösterir:</span><span class="sxs-lookup"><span data-stu-id="952da-166">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="952da-167">Hizmet bağlantı noktası mevcut değilse, bunu çalıştırarak oluşturabilirsiniz `Initialize-ADSyncDomainJoinedComputerSync` Azure AD Connect sunucunuzda cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="952da-167">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="952da-168">Kuruluş yönetici kimlik bilgileri, bu cmdlet'i çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="952da-168">Enterprise admin credential is required to run this cmdlet.</span></span>  
<span data-ttu-id="952da-169">Cmdlet:</span><span class="sxs-lookup"><span data-stu-id="952da-169">The cmdlet:</span></span>

- <span data-ttu-id="952da-170">Azure AD Connect bağlı Active Directory ormanındaki hizmet bağlantı noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="952da-170">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="952da-171">Belirtmenizi gerektirir `AdConnectorAccount` parametresi.</span><span class="sxs-lookup"><span data-stu-id="952da-171">Requires you to specify the `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="952da-172">Active Directory Bağlayıcısı hesabı Azure ad connect yapılandırılan hesap budur.</span><span class="sxs-lookup"><span data-stu-id="952da-172">This is the account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="952da-173">Aşağıdaki komut dosyası cmdlet'ini kullanarak bir örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="952da-173">The following script shows an example for using the cmdlet.</span></span> <span data-ttu-id="952da-174">Bu komut `$aadAdminCred = Get-Credential` bir kullanıcı adı yazın gerektirir.</span><span class="sxs-lookup"><span data-stu-id="952da-174">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span></span> <span data-ttu-id="952da-175">Kullanıcı asıl adı (UPN) biçiminde kullanıcı adı sağlamanız gerekir (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="952da-175">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="952da-176">`Initialize-ADSyncDomainJoinedComputerSync` Cmdlet:</span><span class="sxs-lookup"><span data-stu-id="952da-176">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="952da-177">Bir etki alanı denetleyicisinde çalışan Active Directory Web Hizmetleri dayanan Active Directory PowerShell modülü kullanır.</span><span class="sxs-lookup"><span data-stu-id="952da-177">Uses the Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="952da-178">Active Directory Web Hizmetleri, Windows Server 2008 R2 çalıştıran etki alanı denetleyicilerinde ve üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="952da-178">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="952da-179">Yalnızca tarafından desteklenen **MSOnline PowerShell modülü sürümü 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="952da-179">Is only supported by the **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="952da-180">Bu modül indirmek için bunu kullanın [bağlantı](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="952da-180">To download this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="952da-181">Windows Server 2008 veya önceki sürümlerini çalıştıran etki alanı denetleyicileri için hizmet bağlantı noktası oluşturmak için aşağıdaki komut dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="952da-181">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span></span>

<span data-ttu-id="952da-182">Bir Çoklu orman yapılandırması, hizmet bağlantı noktası bilgisayarları var olduğu her ormanda oluşturmak için aşağıdaki komut dosyasını kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="952da-182">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="952da-183">2. adım: talep verme kurma</span><span class="sxs-lookup"><span data-stu-id="952da-183">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="952da-184">Bir Federasyon Azure AD yapılandırma cihazlar Active Directory Federasyon Hizmetleri (AD FS) üzerinde kullanır veya 3. taraf bir Federasyon Hizmeti için Azure AD kimlik doğrulaması yapmak için şirket içi.</span><span class="sxs-lookup"><span data-stu-id="952da-184">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span></span> <span data-ttu-id="952da-185">Cihazların Azure Active Directory cihaz kayıt Hizmeti'ne karşı (Azure DRS) kaydetmek için bir erişim belirteci almak için kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="952da-185">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="952da-186">Windows geçerli cihazlar şirket içi Federasyon Hizmeti tarafından barındırılan tümleşik Windows kimlik etkin bir WS-Trust uç (1.3 veya 2005 sürümleri) kullanarak kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="952da-186">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="952da-187">AD FS, ya da kullanırken **adfs/services/güven/13/windowstransport** veya **adfs/services/güven/2005/windowstransport** etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="952da-187">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="952da-188">Ayrıca Web kimlik doğrulaması Proxy kullanıyorsanız, bu uç noktası proxy yayımlanır emin olun.</span><span class="sxs-lookup"><span data-stu-id="952da-188">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span></span> <span data-ttu-id="952da-189">Hangi uç noktalarının altında AD FS Yönetim Konsolu aracılığıyla özelliğinin etkinleştirilip etkinleştirilmediğini **hizmet > uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="952da-189">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="952da-190">AD FS, şirket içi Federasyon Hizmeti olarak yoksa, WS-Trust 1.3 veya 2005 uç noktalarının ve bunlar meta veri değişimi dosyası (MEX) aracılığıyla yayımlanır destekledikleri emin olmak için satıcınızın yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="952da-190">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="952da-191">Aşağıdaki talep tamamlanması, cihaz kaydı için Azure DRS'tarafından alınan belirteç bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="952da-191">The following claims must exist in the token received by Azure DRS for device registration to complete.</span></span> <span data-ttu-id="952da-192">Azure DRS Azure AD ile sonra yeni oluşturulan cihaz nesnesi bilgisayar hesabı ile şirket içi ilişkilendirmek için Azure AD Connect tarafından kullanılan bu bilgilerin bazıları, bir cihaz nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="952da-192">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="952da-193">Birden fazla doğrulanan etki alanı adı varsa, bilgisayarlar için aşağıdaki talep sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="952da-193">If you have more than one verified domain name, you need to provide the following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="952da-194">Zaten bir İmmutableıd talep (örn., alternatif oturum açma kimliği) dağıttığınız, bilgisayarlar için karşılık gelen bir talep sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="952da-194">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="952da-195">Aşağıdaki bölümlerde hakkında bilgiler yer:</span><span class="sxs-lookup"><span data-stu-id="952da-195">In the following sections, you find information about:</span></span>
 
- <span data-ttu-id="952da-196">Değerlerin her talep olmalıdır</span><span class="sxs-lookup"><span data-stu-id="952da-196">The values each claim should have</span></span>
- <span data-ttu-id="952da-197">Nasıl bir tanımı gibi AD FS'de görüneceği</span><span class="sxs-lookup"><span data-stu-id="952da-197">How a definition would look like in AD FS</span></span>

<span data-ttu-id="952da-198">Tanımı, değerleri mevcut olup olmadığını veya bunları oluşturmanız gerekiyorsa doğrulamak için yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="952da-198">The definition helps you to verify whether the values are present or if you need to create them.</span></span>

> [!NOTE]
> <span data-ttu-id="952da-199">Şirket içi Federasyon sunucunuz için AD FS kullanmıyorsanız, bu talepleri vermek için uygun bir yapılandırma oluşturmak için satıcınızın yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="952da-199">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="952da-200">Sorunu hesap türü talep</span><span class="sxs-lookup"><span data-stu-id="952da-200">Issue account type claim</span></span>

<span data-ttu-id="952da-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Bu talep değerini içermelidir **DJ**, cihaz etki alanına katılmış bir bilgisayar olarak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="952da-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span></span> <span data-ttu-id="952da-202">AD FS'de şuna benzer bir verme dönüştürme kural ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="952da-202">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a><span data-ttu-id="952da-203">Bilgisayar hesabı içi objectGUID sorun</span><span class="sxs-lookup"><span data-stu-id="952da-203">Issue objectGUID of the computer account on-premises</span></span>

<span data-ttu-id="952da-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Bu talebi içermelidir **objectGUID** şirket içi bilgisayar hesabı değeri.</span><span class="sxs-lookup"><span data-stu-id="952da-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span></span> <span data-ttu-id="952da-205">AD FS'de şuna benzer bir verme dönüştürme kural ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="952da-205">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a><span data-ttu-id="952da-206">Bilgisayar hesabı içi objectSID sorun</span><span class="sxs-lookup"><span data-stu-id="952da-206">Issue objectSID of the computer account on-premises</span></span>

<span data-ttu-id="952da-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Bu talebi içermelidir **objectSID** şirket içi bilgisayar hesabı değeri.</span><span class="sxs-lookup"><span data-stu-id="952da-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the the **objectSid** value of the on-premises computer account.</span></span> <span data-ttu-id="952da-208">AD FS'de şuna benzer bir verme dönüştürme kural ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="952da-208">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="952da-209">Birden çok etki alanı adlarını Azure AD'de belirlediğinizde issuerID bilgisayar için sorun</span><span class="sxs-lookup"><span data-stu-id="952da-209">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="952da-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Herhangi bir şirket içi Federasyon Hizmeti ile (AD FS veya 3. taraf) bağlanma doğrulanmış etki alanı adlarını Tekdüzen Kaynak Tanımlayıcısı (URI) Bu talebi içermelidir belirteç veren.</span><span class="sxs-lookup"><span data-stu-id="952da-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span></span> <span data-ttu-id="952da-211">' De AD FS, yukarıdaki olanlardan sonra olanları belirli sırayla görüneceği verme dönüştürme kuralları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="952da-211">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span></span> <span data-ttu-id="952da-212">Lütfen açıkça kullanıcılar için kuralı vermek için bir kural gerekli olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="952da-212">Please note that one rule to explicitly issue the rule for users is necessary.</span></span> <span data-ttu-id="952da-213">Aşağıdaki kuralları, kullanıcı ve bilgisayar kimlik doğrulaması tanımlama ilk bir kuralı eklenir.</span><span class="sxs-lookup"><span data-stu-id="952da-213">In the rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with the value User when its not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
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


<span data-ttu-id="952da-214">Yukarıdaki talep</span><span class="sxs-lookup"><span data-stu-id="952da-214">In the claim above,</span></span>

- <span data-ttu-id="952da-215">`$<domain>`AD FS hizmet URL'si</span><span class="sxs-lookup"><span data-stu-id="952da-215">`$<domain>` is the AD FS service URL</span></span>
- <span data-ttu-id="952da-216">`<verified-domain-name>`Azure AD'de doğrulanmış etki alanı adlarınızı biri ile değiştirmek için gereken bir yer tutucudur</span><span class="sxs-lookup"><span data-stu-id="952da-216">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="952da-217">Doğrulanmış etki alanı adları hakkında daha fazla ayrıntı için bkz: [bir özel etki alanı adını Azure Active Directory'ye ekleme](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="952da-217">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="952da-218">Doğrulanmış şirket etki alanlarının bir listesini almak için kullanabileceğiniz [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="952da-218">To get a list of your verified company domains, you can use the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="952da-220">Kullanıcılar için bir tane bulunduğunda (kimliği ayarlanmadan örneğin alternatif oturum açma) İmmutableıd bilgisayar için sorun</span><span class="sxs-lookup"><span data-stu-id="952da-220">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="952da-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**-Bu talep bilgisayarlar için geçerli bir değer içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="952da-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="952da-222">AD FS içinde verme dönüştürme kural aşağıdaki gibi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="952da-222">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a><span data-ttu-id="952da-223">AD FS verme dönüştürme kuralları oluşturmak için yardımcı kod</span><span class="sxs-lookup"><span data-stu-id="952da-223">Helper script to create the AD FS issuance transform rules</span></span>

<span data-ttu-id="952da-224">Aşağıdaki komut dosyası, yukarıda açıklanan kuralları dönüştürme verme oluşturulmasını ile yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="952da-224">The following script helps you with the creation of the issuance transform rules described above.</span></span>

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
    $rule4 = '@RuleName = "Issue account type with the value User when it is not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
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

### <a name="remarks"></a><span data-ttu-id="952da-225">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="952da-225">Remarks</span></span> 

- <span data-ttu-id="952da-226">Bu komut dosyası kuralları için varolan kuralları ekler.</span><span class="sxs-lookup"><span data-stu-id="952da-226">This script appends the rules to the existing rules.</span></span> <span data-ttu-id="952da-227">Komut dosyası iki kez çalıştırmayın kuralları iki kez eklenebilir olduğundan.</span><span class="sxs-lookup"><span data-stu-id="952da-227">Do not run the script twice because the set of rules would be added twice.</span></span> <span data-ttu-id="952da-228">Karşılık gelen hiçbir kural bu talepleri (karşılık gelen koşullarda) için komut dosyası yeniden çalıştırmadan önce var olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="952da-228">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span></span>

- <span data-ttu-id="952da-229">(Azure AD portalı veya Get-MsolDomains cmdlet'i aracılığıyla gösterildiği gibi) birden çok doğrulanmış etki alanı adı varsa, değerini ayarlamak **$multipleVerifiedDomainNames** betikteki **$true**.</span><span class="sxs-lookup"><span data-stu-id="952da-229">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span></span> <span data-ttu-id="952da-230">Ayrıca Azure AD Connect veya başka yöntemler aracılığıyla oluşturulan tüm mevcut issuerid talep kaldırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="952da-230">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="952da-231">Bu kural için örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="952da-231">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="952da-232">Zaten yayımlandı durumunda bir **İmmutableıd** kullanıcı hesapları için talep, değerini **$immutableIDAlreadyIssuedforUsers** betikteki **$true**.</span><span class="sxs-lookup"><span data-stu-id="952da-232">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$immutableIDAlreadyIssuedforUsers** in the script to **$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="952da-233">Adım 3: Windows alt düzey aygıtları etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="952da-233">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="952da-234">Bazı etki alanına katılmış aygıtlarınız Windows cihazları sürümlerdeki, gerekir:</span><span class="sxs-lookup"><span data-stu-id="952da-234">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="952da-235">Kullanıcıların aygıtlarını kaydetmesini sağlamak için Azure AD içinde bir ilke ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="952da-235">Set a policy in Azure AD to enable users to register devices.</span></span>
 
- <span data-ttu-id="952da-236">Şirket içi Federasyon hizmetini desteklemek için bir talep yapılandırma **tümleşik Windows kimlik doğrulaması (IWA)** cihaz kaydı için.</span><span class="sxs-lookup"><span data-stu-id="952da-236">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="952da-237">Azure AD cihaz kimlik doğrulama uç noktası cihaz doğrulanırken sertifika istemleri önlemek için yerel Intranet bölgesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="952da-237">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span></span>

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a><span data-ttu-id="952da-238">Kullanıcıların aygıtlarını kaydetmesini sağlamak için Azure AD'de ilkesini ayarlama</span><span class="sxs-lookup"><span data-stu-id="952da-238">Set policy in Azure AD to enable users to register devices</span></span>

<span data-ttu-id="952da-239">Windows alt düzey cihazları kaydetmek için kullanıcıların Azure AD'de cihazları kaydetmek izin vermek için ayarı ayarlandığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="952da-239">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span></span> <span data-ttu-id="952da-240">Azure Portal'da, bu ayarı altında bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="952da-240">In the Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="952da-241">Aşağıdaki ilke ayarlamak **tüm**: **kullanıcıları Azure AD ile cihazlarını kaydetme**</span><span class="sxs-lookup"><span data-stu-id="952da-241">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![Cihaz kaydetme](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="952da-243">Şirket içi Federasyon hizmetini yapılandır</span><span class="sxs-lookup"><span data-stu-id="952da-243">Configure on-premises federation service</span></span> 

<span data-ttu-id="952da-244">Şirket içi Federasyon hizmetinizi veren desteklemelidir **authenticationmehod** ve **wiaormultiauthn** aşağıda gösterildiği gibi kodlanmış bir değer resouce_params parametresiyle tutan Azure AD bağlı olan taraf için kimlik doğrulama isteği alırken talepleri:</span><span class="sxs-lookup"><span data-stu-id="952da-244">Your on-premises federation service must support issuing the **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="952da-245">Böyle bir istek geldiğinde, şirket içi Federasyon Hizmeti tümleşik Windows kimlik doğrulaması kullanarak kullanıcı kimlik doğrulaması yapmalıdır ve başarılı üzerinde aşağıdaki iki talep kesmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="952da-245">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="952da-246">AD FS'de kimlik doğrulama yöntemini geçişleri üzerinden bir verme dönüştürme kuralı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="952da-246">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span></span>  

<span data-ttu-id="952da-247">**Bu kural eklemek için:**</span><span class="sxs-lookup"><span data-stu-id="952da-247">**To add this rule:**</span></span>

1. <span data-ttu-id="952da-248">AD FS yönetim konsolunda Git `AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="952da-248">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="952da-249">Microsoft Office 365 kimlik Platformu'na bağlı taraf güven nesnesi sağ tıklayın ve ardından **talep kurallarını Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="952da-249">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="952da-250">Üzerinde **verme dönüştürme kuralları** sekmesine **Kuralı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="952da-250">On the **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="952da-251">İçinde **talep kuralı** şablonu listesinden **talepleri özel kural kullanarak Gönder**.</span><span class="sxs-lookup"><span data-stu-id="952da-251">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="952da-252">Seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="952da-252">Select **Next**.</span></span>
6. <span data-ttu-id="952da-253">İçinde **talep kuralı adı** kutusuna **kimlik doğrulama yöntemi talep kuralı**.</span><span class="sxs-lookup"><span data-stu-id="952da-253">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="952da-254">İçinde **talep kuralı** kutusunda, aşağıdaki kural yazın:</span><span class="sxs-lookup"><span data-stu-id="952da-254">In the **Claim rule** box, type the following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="952da-255">Değiştirildikten sonra Federasyon sunucunuzda aşağıdaki PowerShell komutunu yazın  **\<RPObjectName\>**  adıyla bağlı olan taraf nesnesi, Azure AD bağlı olan taraf güven nesnesi.</span><span class="sxs-lookup"><span data-stu-id="952da-255">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="952da-256">Bu nesne genellikle adlı **Microsoft Office 365 kimlik Platformu'na**.</span><span class="sxs-lookup"><span data-stu-id="952da-256">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a><span data-ttu-id="952da-257">Azure AD cihaz kimlik doğrulama uç noktası yerel Intranet bölgesine ekleyin</span><span class="sxs-lookup"><span data-stu-id="952da-257">Add the Azure AD device authentication end-point to the Local Intranet zones</span></span>

<span data-ttu-id="952da-258">Sertifika önlemek için kayıt aygıtları kullanıcılar yerel Intranet bölgesine Internet Explorer'da aşağıdaki URL'yi eklemek için etki alanına katılmış cihazlar için bir ilke itme Azure AD kimlik doğrulaması sırasında ister:</span><span class="sxs-lookup"><span data-stu-id="952da-258">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="952da-259">Adım 4: Denetimi dağıtımı ve dağıtım</span><span class="sxs-lookup"><span data-stu-id="952da-259">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="952da-260">Gerekli adımları tamamladıktan sonra etki alanına katılmış cihazları otomatik olarak Azure AD katılım hazırsınız:</span><span class="sxs-lookup"><span data-stu-id="952da-260">When you have completed the required steps, domain-joined devices are ready to automatically join Azure AD:</span></span>

- <span data-ttu-id="952da-261">Windows 10 Anniversary güncelleştirmesi ve Windows Server 2016 çalıştıran tüm etki alanına katılmış cihazlar otomatik olarak kayıt aygıt adresindeki Azure AD ile yeniden başlatın veya kullanıcı oturum açma.</span><span class="sxs-lookup"><span data-stu-id="952da-261">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> 

- <span data-ttu-id="952da-262">Yeni cihazların etki alanına katılma işlemi tamamlandıktan sonra aygıt yeniden başlatıldığında Azure AD ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="952da-262">New devices register with Azure AD when the device restarts after the domain join operation is completed.</span></span>

- <span data-ttu-id="952da-263">Daha önce Azure AD olan cihaz kayıtlı (örneğin, Intune için) için geçiş "*etki alanına katılmış, AAD kayıtlı*"; Ancak, etki alanının normal akıştaki nedeniyle tüm cihazlar arasında tamamlamak bu işlem biraz zaman alabilir ve kullanıcı etkinliği.</span><span class="sxs-lookup"><span data-stu-id="952da-263">Devices that were previously Azure AD registered (for example, for Intune) transition to “*Domain Joined, AAD Registered*”; however it takes some time for this process to complete across all devices due to the normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="952da-264">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="952da-264">Remarks</span></span>

- <span data-ttu-id="952da-265">Windows 10 ve Windows Server 2016 etki alanına katılmış bilgisayarlar otomatik kaydını piyasaya sürümü denetlemek için Grup İlkesi nesnesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="952da-265">You can use a Group Policy object to control the rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="952da-266">Windows 10 Kasım 2015 güncelleştirmesi otomatik olarak birleştiren Azure AD ile **yalnızca** sunum Grup İlkesi nesnesi ayarlarsanız.</span><span class="sxs-lookup"><span data-stu-id="952da-266">Windows 10 November 2015 Update automatically joins with Azure AD **only** if the rollout Group Policy object is set.</span></span>

- <span data-ttu-id="952da-267">Kullanıcılarınıza Windows alt düzey bilgisayarların, dağıttığınız bir [Windows Installer paketi](#windows-installer-packages-for-non-windows-10-computers) seçtiğiniz bilgisayarlara.</span><span class="sxs-lookup"><span data-stu-id="952da-267">To rollout of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to computers that you select.</span></span>

- <span data-ttu-id="952da-268">Windows 8.1 etki alanına katılmış cihazlar için Grup İlkesi nesnesini itme olursa, bir birleştirme denenir; Ancak, kullanmanız önerilir [Windows Installer paketi](#windows-installer-packages-for-non-windows-10-computers) tüm Windows alt düzey aygıtları katılmak için.</span><span class="sxs-lookup"><span data-stu-id="952da-268">If you push the Group Policy object to Windows 8.1 domain-joined devices, a join is attempted; however it is recommended that you use the [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to join all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="952da-269">Bir Grup İlkesi nesnesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="952da-269">Create a Group Policy object</span></span> 

<span data-ttu-id="952da-270">Windows geçerli bilgisayarların piyasaya sürümü denetlemek için dağıtmanız **etki alanına katılmış bilgisayarları cihaz olarak kaydetme** kaydetmek istediğiniz aygıtları için Grup İlkesi nesnesi.</span><span class="sxs-lookup"><span data-stu-id="952da-270">To control the rollout of Windows current computers, you should deploy the **Register domain-joined computers as devices** Group Policy object to the devices you want to register.</span></span> <span data-ttu-id="952da-271">Örneğin, bir kuruluş birimi veya bir güvenlik grubu için ilke dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="952da-271">For example, you can deploy the policy to an organizational unit or to a security group.</span></span>

<span data-ttu-id="952da-272">**İlke ayarlamak için:**</span><span class="sxs-lookup"><span data-stu-id="952da-272">**To set the policy:**</span></span>

1. <span data-ttu-id="952da-273">Açık **Sunucu Yöneticisi'ni**ve ardından `Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="952da-273">Open **Server Manager**, and then go to `Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="952da-274">Otomatik kaydı Windows geçerli bilgisayarların etkinleştirmek istediğiniz etki alanı için karşılık gelen etki alanı düğümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="952da-274">Go to the domain node that corresponds to the domain where you want to activate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="952da-275">Sağ **Grup İlkesi nesneleri**ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="952da-275">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="952da-276">Grup İlkesi nesnesi için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="952da-276">Type a name for your Group Policy object.</span></span> <span data-ttu-id="952da-277">Örneğin, * karma Azure AD birleştirme.</span><span class="sxs-lookup"><span data-stu-id="952da-277">For example, *Hybrid Azure AD join.</span></span> 
5. <span data-ttu-id="952da-278">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="952da-278">Click **OK**.</span></span>
6. <span data-ttu-id="952da-279">Yeni Grup İlkesi nesneniz sağ tıklayın ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="952da-279">Right-click your new Group Policy object, and then select **Edit**.</span></span>
7. <span data-ttu-id="952da-280">Git **Bilgisayar Yapılandırması** > **ilkeleri** > **Yönetim Şablonları** > **Windows bileşenleri** > **aygıt kaydı**.</span><span class="sxs-lookup"><span data-stu-id="952da-280">Go to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> 
8. <span data-ttu-id="952da-281">Sağ **etki alanına katılmış bilgisayarları cihaz olarak kaydetme**ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="952da-281">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="952da-282">Bu Grup İlkesi şablonu, Grup İlkesi Yönetimi konsolunun önceki sürümlerden adlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="952da-282">This Group Policy template has been renamed from earlier versions of the Group Policy Management console.</span></span> <span data-ttu-id="952da-283">Konsol önceki bir sürümünü kullanıyorsanız, Git `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="952da-283">If you are using an earlier version of the console, go to `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="952da-284">Seçin **etkin**ve ardından **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="952da-284">Select **Enabled**, and then click **Apply**.</span></span>
8. <span data-ttu-id="952da-285">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="952da-285">Click **OK**.</span></span>
9. <span data-ttu-id="952da-286">Grup İlkesi nesnesini, bir konumla bağlayın.</span><span class="sxs-lookup"><span data-stu-id="952da-286">Link the Group Policy object to a location of your choice.</span></span> <span data-ttu-id="952da-287">Örneğin, belirli bir kuruluş birimine olarak bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="952da-287">For example, you can link it to a specific organizational unit.</span></span> <span data-ttu-id="952da-288">Otomatik olarak Azure AD ile katılmak bilgisayarları belirli güvenlik grubuna da bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="952da-288">You also could link it to a specific security group of computers that automatically join with Azure AD.</span></span> <span data-ttu-id="952da-289">Bu ilke tüm etki alanına katılmış Windows 10 ve Windows Server 2016 kuruluşunuzdaki bilgisayarlara atamak için Grup İlkesi nesnesini etki alanına bağlayın.</span><span class="sxs-lookup"><span data-stu-id="952da-289">To set this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link the Group Policy object to the domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="952da-290">Windows 10 bilgisayarları için Windows Installer paketleri</span><span class="sxs-lookup"><span data-stu-id="952da-290">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="952da-291">Federasyon ortamında Windows alt düzey bilgisayarları etki alanına katılmış katılmak için indirin ve bu Windows Installer (.msi) paketi İndirme Merkezi'nden yüklemek [Windows 10 bilgisayarlar için Microsoft çalışma alanına katılma](https://www.microsoft.com/en-us/download/details.aspx?id=53554) Sayfa.</span><span class="sxs-lookup"><span data-stu-id="952da-291">To join domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="952da-292">Paketi, System Center Configuration Manager gibi yazılım dağıtım sistemi kullanarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="952da-292">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="952da-293">Paket ile standart sessiz yükleme seçeneklerini destekler *sessiz* parametresi.</span><span class="sxs-lookup"><span data-stu-id="952da-293">The package supports the standard silent install options with the *quiet* parameter.</span></span> <span data-ttu-id="952da-294">System Center Configuration Manager geçerli dalının tamamlanmış kayıtlar izleme yeteneği gibi önceki sürümlerinden ek avantajlar sunar.</span><span class="sxs-lookup"><span data-stu-id="952da-294">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span></span> <span data-ttu-id="952da-295">Daha fazla bilgi için bkz: [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="952da-295">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="952da-296">Yükleyici sistemde kullanıcının bağlamında çalışan zamanlanmış bir görev oluşturur.</span><span class="sxs-lookup"><span data-stu-id="952da-296">The installer creates a scheduled task on the system that runs in the user’s context.</span></span> <span data-ttu-id="952da-297">Kullanıcı Windows açtığında görevi tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="952da-297">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="952da-298">Görev sessizce aygıt tümleşik Windows kimlik doğrulaması kullanarak kimlik doğrulama sonra Azure AD kullanıcı kimlik bilgileri ile birleştirir.</span><span class="sxs-lookup"><span data-stu-id="952da-298">The task silently joins the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="952da-299">Aygıtta zamanlanmış görev görmek için Git **Microsoft** > **çalışma alanına katılma**ve Görev Zamanlayıcı Kitaplığı'na gidin.</span><span class="sxs-lookup"><span data-stu-id="952da-299">To see the scheduled task, in the device, go to **Microsoft** > **Workplace Join**, and then go to the Task Scheduler library.</span></span>

## <a name="step-5-verify-joined-devices"></a><span data-ttu-id="952da-300">5. adım: alanına katılmamış aygıtlar doğrulayın</span><span class="sxs-lookup"><span data-stu-id="952da-300">Step 5: Verify joined devices</span></span>

<span data-ttu-id="952da-301">Kullanarak, kuruluşunuzda başarılı alanına katılmamış aygıtlar denetleyebilirsiniz [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet'te [Azure Active Directory PowerShell Modülü](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="952da-301">You can check successful joined devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="952da-302">Bu cmdlet'in çıktısı, kayıtlı ve Azure AD ile birleştirilmiş cihazları gösterir.</span><span class="sxs-lookup"><span data-stu-id="952da-302">The output of this cmdlet shows devices that are registered and joined with Azure AD.</span></span> <span data-ttu-id="952da-303">Tüm cihazlar almak için kullanın **-tüm** parametresi ve bunları filtre kullanarak **deviceTrustType** özelliği.</span><span class="sxs-lookup"><span data-stu-id="952da-303">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span></span> <span data-ttu-id="952da-304">Etki alanına katılmış aygıtlar değerine sahip **etki alanına katılmış**.</span><span class="sxs-lookup"><span data-stu-id="952da-304">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="952da-305">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="952da-305">Next steps</span></span>

* [<span data-ttu-id="952da-306">Azure Active Directory'de cihaz yönetimine giriş</span><span class="sxs-lookup"><span data-stu-id="952da-306">Introduction to device management in Azure Active Directory</span></span>](device-management-introduction.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
