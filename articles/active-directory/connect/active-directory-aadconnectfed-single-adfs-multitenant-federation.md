---
title: "Birden çok Azure AD’yi tek bir AD FS ile birleştirme | Microsoft Docs"
description: "Bu belgede, birden çok Azure AD’yi tek bir AD FS ile nasıl birleştirebileceğinizi öğreneceksiniz."
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
ms.openlocfilehash: 436bf5905d2b203dc4cceea97f4fb90593df7111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="5b5c2-104">Azure AD’nin birden çok örneğini tek bir AD FS örneği ile birleştirme</span><span class="sxs-lookup"><span data-stu-id="5b5c2-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="5b5c2-105">Aralarında iki yönlü güven varsa, tek bir yüksek kullanılabilirlikli AD FS ormanı birden çok ormanı birleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="5b5c2-106">Bu birden çok orman, aynı Azure Active Directory’ye karşılık gelebilir veya gelmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-106">These multiple forests may or may not correspond to the same Azure Active Directory.</span></span> <span data-ttu-id="5b5c2-107">Bu makale, tek AD FS dağıtımı ile farklı Azure AD’ye eşitlenen birden çok orman arasında nasıl federasyon yapılandırabileceğinizle ilgili yönergeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-107">This article provides instructions on how to configure federation between a single AD FS deployment and more than one forests that sync to different Azure AD.</span></span>

![Tek AD FS ile çok kiracılı federasyon](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="5b5c2-109">Bu senaryoda cihaz geri yazma ve otomatik cihaz katılımı desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="5b5c2-110">Azure AD Connect tek bir Azure AD’deki etki alanları için federasyon yapılandırabildiğinden, bu senaryoda federasyon yapılandırmak için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-110">Azure AD Connect cannot be used to configure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="5b5c2-111">AD FS’yi birden çok Azure AD ile birleştirmek için uygulanması gereken adımlar</span><span class="sxs-lookup"><span data-stu-id="5b5c2-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="5b5c2-112">contoso.onmicrosoft.com adresli Azure Active Directory’deki contoso.com etki alanının zaten contoso.com’da şirket içi Active Directory ortamında yüklü şirket içi AD FS ile birleştirildiğini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with the AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="5b5c2-113">Fabrikam.com, fabrikam.onmicrosoft.com adresli Azure Active Directory’de bir etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="5b5c2-114">1. Adım: İki yönlü güven kurma</span><span class="sxs-lookup"><span data-stu-id="5b5c2-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="5b5c2-115">contoso.com’daki AD FS’nin fabrikam.com’da kullanıcıların kimliklerini doğrulayabilmesi için contoso.com ile fabrikam.com arasında iki yönlü bir güven gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-115">For AD FS in contoso.com to be able to authenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com.</span></span> <span data-ttu-id="5b5c2-116">İki yönlü güveni oluşturmak için bu [makaledeki](https://technet.microsoft.com/library/cc816590.aspx) kılavuzu izleyin.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-116">Follow the guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) to create the two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="5b5c2-117">2. Adım: contoso.com federasyon ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="5b5c2-117">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="5b5c2-118">AD FS ile birleştirilmiş tek bir etki alanı için ayarlanan varsayılan veren şudur: "http://ADFSServiceFQDN/adfs/services/trust". Örneğin, “http://fs.contoso.com/adfs/services/trust”.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-118">The default issuer set for a single domain federated to AD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="5b5c2-119">Azure Active Directory, federasyona eklenen her etki alanı için benzersiz bir veren gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-119">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="5b5c2-120">İki etki alanı aynı AD FS tarafından federasyona ekleneceğinden, AD FS’nin Azure Active Directory ile birleştirdiği her etki alanında benzersiz olması için veren değerinin değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-120">Since the same AD FS is going to federate two domains, the issuer value needs to be modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="5b5c2-121">AD FS sunucusunda Azure AD PowerShell’i açın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5b5c2-121">On the AD FS server, open Azure AD PowerShell and perform the following steps:</span></span>
 
<span data-ttu-id="5b5c2-122">contoso.com etki alanını içeren Azure Active Directory’ye bağlanın: Connect-MsolService contoso.com için federasyon ayarlarını güncelleştirin: Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="5b5c2-122">Connect to the Azure Active Directory that contains the domain contoso.com Connect-MsolService Update the federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="5b5c2-123">Etki alanı federasyon ayarındaki veren "http://contoso.com/adfs/services/trust" olarak değiştirilir ve Azure AD Bağlı Olan Taraf Güveni’nin UPN son ekine bağlı olarak doğru issuerId değerini vermesi için bir verme talebi kuralı eklenir.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-123">Issuer in the domain federation setting will be changed to "http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for the Azure AD Relying Party Trust to issue the correct issuerId value based on the UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="5b5c2-124">3. adım: fabrikam.com’u AD FS ile birleştirin</span><span class="sxs-lookup"><span data-stu-id="5b5c2-124">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="5b5c2-125">Azure AD powershell oturumunda şu adımları gerçekleştirin: fabrikam.com etki alanını içeren Azure Active Directory’ye bağlanın</span><span class="sxs-lookup"><span data-stu-id="5b5c2-125">In Azure AD powershell session perform the following steps: Connect to Azure Active Directory that contains the domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="5b5c2-126">fabrikam.com yönetilen etki alanını federasyon etki alanına dönüştürün:</span><span class="sxs-lookup"><span data-stu-id="5b5c2-126">Convert the fabrikam.com managed domain to federated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="5b5c2-127">Yukarıdaki işlem, fabrikam.com etki alanını aynı AD FS ile birleştirir.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-127">The above operation will federate the domain fabrikam.com with the same AD FS.</span></span> <span data-ttu-id="5b5c2-128">Her iki etki alanı için de Get-MsolDomainFederationSettings komutunu kullanarak etki alanı ayarlarını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b5c2-128">You can verify the domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b5c2-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5b5c2-129">Next steps</span></span>
[<span data-ttu-id="5b5c2-130">Azure Active Directory ile Active Directory’yi bağlama</span><span class="sxs-lookup"><span data-stu-id="5b5c2-130">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
