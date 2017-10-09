---
title: "aaaFederating tek AD FS ile birden çok Azure AD | Microsoft Docs"
description: "Bu belgede, öğreneceksiniz nasıl toofederate tek bir AD FS ile birden çok Azure AD."
keywords: "federasyon, ADFS, AD FS, birden çok kiracı, tek AD FS, bir ADFS, çok kiracılı federasyon, çok ormanlı adfs, aad bağlantısı, federasyon oluşturma, kiracılar arası federasyon"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="12b3b-104">Azure AD’nin birden çok örneğini tek bir AD FS örneği ile birleştirme</span><span class="sxs-lookup"><span data-stu-id="12b3b-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="12b3b-105">Aralarında iki yönlü güven varsa, tek bir yüksek kullanılabilirlikli AD FS ormanı birden çok ormanı birleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="12b3b-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="12b3b-106">Bu birden çok ormanı olabilir veya toohello karşılık gelmeyebilir aynı Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="12b3b-106">These multiple forests may or may not correspond toohello same Azure Active Directory.</span></span> <span data-ttu-id="12b3b-107">Bu makalede, tek bir AD FS dağıtımı ile birden fazla arasındaki tooconfigure Federasyon, Azure AD eşitleme toodifferent nasıl ormanlar yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="12b3b-107">This article provides instructions on how tooconfigure federation between a single AD FS deployment and more than one forests that sync toodifferent Azure AD.</span></span>

![Tek AD FS ile çok kiracılı federasyon](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="12b3b-109">Bu senaryoda cihaz geri yazma ve otomatik cihaz katılımı desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="12b3b-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="12b3b-110">Azure AD Connect Azure AD Connect Federasyon etki alanları için tek bir Azure AD içinde yapılandırabilirsiniz Bu senaryoda kullanılan tooconfigure Federasyon olamaz.</span><span class="sxs-lookup"><span data-stu-id="12b3b-110">Azure AD Connect cannot be used tooconfigure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="12b3b-111">AD FS’yi birden çok Azure AD ile birleştirmek için uygulanması gereken adımlar</span><span class="sxs-lookup"><span data-stu-id="12b3b-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="12b3b-112">Azure Active Directory contoso.onmicrosoft.com bir etki alanı contoso.com zaten hello AD FS contoso.com şirket içi Active Directory ortamında yüklü şirket içinde Federasyon göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="12b3b-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with hello AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="12b3b-113">Fabrikam.com, fabrikam.onmicrosoft.com adresli Azure Active Directory’de bir etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="12b3b-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="12b3b-114">1. Adım: İki yönlü güven kurma</span><span class="sxs-lookup"><span data-stu-id="12b3b-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="12b3b-115">Contoso.com toobe mümkün tooauthenticate kullanıcılar fabrikam.com içinde AD FS için contoso.com ve fabrikam.com arasında iki yönlü bir güven gereklidir. Bu kılavuz Hello izleyin [makale](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello iki yönlü güven.</span><span class="sxs-lookup"><span data-stu-id="12b3b-115">For AD FS in contoso.com toobe able tooauthenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com. Follow hello guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="12b3b-116">2. Adım: contoso.com federasyon ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="12b3b-116">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="12b3b-117">hello varsayılan veren bir Federasyon tek bir etki alanı tooAD FS "http://ADFSServiceFQDN/adfs/services/trust", örneğin, "http://fs.contoso.com/adfs/services/trust" için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="12b3b-117">hello default issuer set for a single domain federated tooAD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="12b3b-118">Azure Active Directory, federasyona eklenen her etki alanı için benzersiz bir veren gerektirir.</span><span class="sxs-lookup"><span data-stu-id="12b3b-118">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="12b3b-119">Merhaba aynı AD FS toofederate iki etki alanı geçiyor olduğundan, Azure Active Directory ile AD FS federates her etki alanı için benzersiz şekilde değiştirilebilir toobe hello veren değeriyle gerekir.</span><span class="sxs-lookup"><span data-stu-id="12b3b-119">Since hello same AD FS is going toofederate two domains, hello issuer value needs toobe modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="12b3b-120">Merhaba AD FS sunucusunda Azure AD PowerShell'i açın ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="12b3b-120">On hello AD FS server, open Azure AD PowerShell and perform hello following steps:</span></span>
 
<span data-ttu-id="12b3b-121">Toohello contoso.com güncelleştirme MsolFederatedDomain - DomainName contoso.com hello etki alanı contoso.com Bağlan MsolService güncelleştirme hello Federasyon ayarlarını içeren Azure Active Directory connect – SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="12b3b-121">Connect toohello Azure Active Directory that contains hello domain contoso.com Connect-MsolService Update hello federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="12b3b-122">Merhaba etki alanı Federasyon ayarını veren değiştirilmesi "http://contoso.com/adfs/services/trust" ve bir verme kuralı eklenecek hello Azure AD bağlı olan taraf güveni tooissue hello issuerId değerine göre hello UPN soneki üzerinde doğru için çok talep.</span><span class="sxs-lookup"><span data-stu-id="12b3b-122">Issuer in hello domain federation setting will be changed too"http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for hello Azure AD Relying Party Trust tooissue hello correct issuerId value based on hello UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="12b3b-123">3. adım: fabrikam.com’u AD FS ile birleştirin</span><span class="sxs-lookup"><span data-stu-id="12b3b-123">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="12b3b-124">Azure AD PowerShell'de oturum hello aşağıdaki adımları gerçekleştirin: tooAzure hello etki alanı fabrikam.com içeren Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="12b3b-124">In Azure AD powershell session perform hello following steps: Connect tooAzure Active Directory that contains hello domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="12b3b-125">Merhaba fabrikam.com yönetilen etki alanı toofederated Dönüştür:</span><span class="sxs-lookup"><span data-stu-id="12b3b-125">Convert hello fabrikam.com managed domain toofederated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="12b3b-126">Merhaba işlemi yukarıda hello etki alanı fabrikam.com hello aynı AD FS ile birleştirmek.</span><span class="sxs-lookup"><span data-stu-id="12b3b-126">hello above operation will federate hello domain fabrikam.com with hello same AD FS.</span></span> <span data-ttu-id="12b3b-127">Merhaba etki alanı ayarları her iki etki alanı için Get-MsolDomainFederationSettings kullanarak doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12b3b-127">You can verify hello domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12b3b-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="12b3b-128">Next steps</span></span>
[<span data-ttu-id="12b3b-129">Azure Active Directory ile Active Directory’yi bağlama</span><span class="sxs-lookup"><span data-stu-id="12b3b-129">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
