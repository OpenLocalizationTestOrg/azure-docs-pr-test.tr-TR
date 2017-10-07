---
title: "Connect aaaAzure AD birden çok etki alanı"
description: "Bu belgede ayarlama ve O365 ve Azure AD ile birden çok üst düzey etki alanlarını yapılandırma açıklanmaktadır."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="914b3-103">Azure AD ile Federasyon için Çoklu Etki Alanı Desteği</span><span class="sxs-lookup"><span data-stu-id="914b3-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="914b3-104">Merhaba aşağıdaki belgeleri rehberlik sağlar toouse birden çok üst düzey etki alanları ve Office 365 veya Azure AD etki alanlarıyla federasyonunu alt etki alanları.</span><span class="sxs-lookup"><span data-stu-id="914b3-104">hello following documentation provides guidance on how toouse multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="914b3-105">Birden çok üst düzey etki alanı desteği</span><span class="sxs-lookup"><span data-stu-id="914b3-105">Multiple top-level domain support</span></span>
<span data-ttu-id="914b3-106">Birden çok federasyonunu, üst düzey etki alanlarının Azure AD ile bir üst düzey etki alanı ile federasyonunu kullanılırken gerekli değildir bazı ek yapılandırma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="914b3-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="914b3-107">Bir etki alanı Azure AD ile Federasyon olduğunda, çeşitli özellikler Azure hello etki alanına ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="914b3-107">When a domain is federated with Azure AD, several properties are set on hello domain in Azure.</span></span>  <span data-ttu-id="914b3-108">Bir önemli IssuerUri adrestir.</span><span class="sxs-lookup"><span data-stu-id="914b3-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="914b3-109">Kullanılan URI budur Azure AD tooidentify tarafından belirteci hello hello etki alanı ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="914b3-109">This is a URI that is used by Azure AD tooidentify hello domain that hello token is associated with.</span></span>  <span data-ttu-id="914b3-110">Merhaba URI tooresolve tooanything gerek yoktur, ancak geçerli bir URI olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="914b3-110">hello URI doesn’t need tooresolve tooanything but it must be a valid URI.</span></span>  <span data-ttu-id="914b3-111">Varsayılan olarak, Azure AD hello Federasyon Hizmeti tanımlayıcısı bu toohello değerini, şirket içi AD FS ayarlar yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="914b3-111">By default, Azure AD sets this toohello value of hello federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="914b3-112">Merhaba Federasyon Hizmeti tanımlayıcısı bir Federasyon Hizmeti benzersiz olarak tanımlayan bir URI değil.</span><span class="sxs-lookup"><span data-stu-id="914b3-112">hello federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="914b3-113">Merhaba Federasyon Hizmeti AD FS bu işlevleri hello güvenlik belirteci hizmeti örneğidir.</span><span class="sxs-lookup"><span data-stu-id="914b3-113">hello federation service is an instance of AD FS that functions as hello security token service.</span></span> 
> 
> 

<span data-ttu-id="914b3-114">Merhaba PowerShell komutunu kullanarak görünümü IssuerUri yapabilecekleriniz `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span><span class="sxs-lookup"><span data-stu-id="914b3-114">You can vew IssuerUri by using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="914b3-116">Birden çok üst düzey etki alanı tooadd istiyoruz olduğunda bir sorun ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="914b3-116">A problem arises when we want tooadd more than one top-level domain.</span></span>  <span data-ttu-id="914b3-117">Örneğin, Kurulum Federasyon Azure AD arasında sahip düşünelim ve şirket içi ortamınıza.</span><span class="sxs-lookup"><span data-stu-id="914b3-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="914b3-118">Bu belge için bmcontoso.com kullanıyorum.  İkinci, üst düzey etki alanı eklemiş olduğunuz artık bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="914b3-118">For this document I am using bmcontoso.com.  Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Etki Alanları](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="914b3-120">Biz bizim bmfabrikam.com etki alanı toobe federe tooconvert denediğinizde, biz hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="914b3-120">When we attempt tooconvert our bmfabrikam.com domain toobe federated, we receive an error.</span></span>  <span data-ttu-id="914b3-121">Merhaba Bunun nedeni, Azure AD hello birden fazla etki alanı için aynı değeri IssuerUri özelliği toohave hello izin vermeyen bir kısıtlamaya sahip.</span><span class="sxs-lookup"><span data-stu-id="914b3-121">hello reason for this is, Azure AD has a constraint that does not allow hello IssuerUri property toohave hello same value for more than one domain.</span></span>  

![Federasyon hata](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="914b3-123">SupportMultipleDomain parametresi</span><span class="sxs-lookup"><span data-stu-id="914b3-123">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="914b3-124">tooworkaround bunu tooadd hangi hello kullanılarak yapılabilir farklı bir IssuerUri ihtiyacımız `-SupportMultipleDomain` parametresi.</span><span class="sxs-lookup"><span data-stu-id="914b3-124">tooworkaround this, we need tooadd a different IssuerUri which can be done by using hello `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="914b3-125">Bu parametre cmdlet'leri aşağıdaki hello ile kullanılır:</span><span class="sxs-lookup"><span data-stu-id="914b3-125">This parameter is used with hello following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="914b3-126">Bu parametreyi hello hello etki alanı adını temel alarak şekilde hello IssuerUri yapılandırmak Azure AD yapar.</span><span class="sxs-lookup"><span data-stu-id="914b3-126">This parameter makes Azure AD configure hello IssuerUri so that it is based on hello name of hello domain.</span></span>  <span data-ttu-id="914b3-127">Bu dizinlerde Azure AD içinde benzersiz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="914b3-127">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="914b3-128">Merhaba parametresini kullanarak hello PowerShell komut toocomplete başarıyla sağlar.</span><span class="sxs-lookup"><span data-stu-id="914b3-128">Using hello parameter allows hello PowerShell command toocomplete successfully.</span></span>

![Federasyon hata](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="914b3-130">Bizim yeni bmfabrikam.com etki alanının Hello ayarları aramanız hello aşağıdakileri görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="914b3-130">Looking at hello settings of our new bmfabrikam.com domain you can see hello following:</span></span>

![Federasyon hata](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="914b3-132">Unutmayın `-SupportMultipleDomain` hello değiştirmez olan diğer uç noktaları toopoint tooour Federasyon Hizmeti üzerinde adfs.bmcontoso.com halen yapılandırılıyor.</span><span class="sxs-lookup"><span data-stu-id="914b3-132">Note that `-SupportMultipleDomain` does not change hello other endpoints which are still configured toopoint tooour federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="914b3-133">Başka bir şey, `-SupportMultipleDomain` yapar, hello uygun veren değeriyle hello AD FS sistem için Azure AD yayınlanan belirteçleri içerir güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="914b3-133">Another thing that `-SupportMultipleDomain` does is that it ensures that hello AD FS system includes hello proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="914b3-134">Bunu alma hello kullanıcıların UPN hello etki alanı bölümü ve bu hello etki alanında hello IssuerUri, yani https://{upn soneki olarak ayarlayarak yapar} / adfs/services/güven.</span><span class="sxs-lookup"><span data-stu-id="914b3-134">It does this by taking hello domain portion of hello users UPN and setting this as hello domain in hello IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="914b3-135">Bu nedenle kimlik doğrulaması tooAzure AD ya da Office 365 sırasında hello IssuerUri hello kullanıcının belirteci kullanılan toolocate hello etki alanı Azure AD'de öğedir.</span><span class="sxs-lookup"><span data-stu-id="914b3-135">Thus during authentication tooAzure AD or Office 365, hello IssuerUri element in hello user’s token is used toolocate hello domain in Azure AD.</span></span>  <span data-ttu-id="914b3-136">Bir eşleşme hello kimlik doğrulaması başarısız olur bulunamazsa.</span><span class="sxs-lookup"><span data-stu-id="914b3-136">If a match cannot be found hello authentication will fail.</span></span> 

<span data-ttu-id="914b3-137">Örneğin, bir kullanıcının UPN ise bsimon@bmcontoso.com, hello IssuerUri hello belirteci AD FS sorunları öğesinde toohttp://bmcontoso.com/adfs/services/trust ayarlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="914b3-137">For example, if a user’s UPN is bsimon@bmcontoso.com, hello IssuerUri element in hello token AD FS issues will be set toohttp://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="914b3-138">Bu hello Azure AD yapılandırma ile eşleşir ve kimlik doğrulama başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="914b3-138">This will match hello Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="914b3-139">Merhaba, bu mantığı uygular hello özelleştirilmiş talep kuralı aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="914b3-139">hello following is hello customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="914b3-140">Sipariş toouse - SupportMultipleDomain tooadd yeni çalışırken geçiş veya zaten Dönüştür hello eklenen etki alanlarını, toohave gerek federe güven toosupport Kurulum bunları başlangıçta.</span><span class="sxs-lookup"><span data-stu-id="914b3-140">In order toouse hello -SupportMultipleDomain switch when attempting tooadd new or convert already added domains, you need toohave setup your federated trust toosupport them originally.</span></span>  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="914b3-141">Tooupdate hello nasıl güven AD FS ile Azure AD arasında</span><span class="sxs-lookup"><span data-stu-id="914b3-141">How tooupdate hello trust between AD FS and Azure AD</span></span>
<span data-ttu-id="914b3-142">AD FS ile Azure AD Örneğinize arasında hello federe güven Kurulum belirtilmedi, toore gerekebilir-bu güven oluşturun.</span><span class="sxs-lookup"><span data-stu-id="914b3-142">If you did not setup hello federated trust between AD FS and your instance of Azure AD, you may need toore-create this trust.</span></span>  <span data-ttu-id="914b3-143">Kurulum hello olmadan başlangıçta olduğu zaman, bunun nedeni `-SupportMultipleDomain` parametresi hello IssuerUri hello varsayılan değeri ile ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="914b3-143">This is because, when it is originally setup without hello `-SupportMultipleDomain` parameter, hello IssuerUri is set with hello default value.</span></span>  <span data-ttu-id="914b3-144">Hello hello IssuerUri toohttps://adfs.bmcontoso.com/adfs/services/trust ayarlanır ekran görüntüsü aşağıda görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="914b3-144">In hello screenshot below you can see hello IssuerUri is set toohttps://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="914b3-145">Bunu şimdi biz hello Azure AD Portalı'nda yeni bir etki alanı başarıyla eklediniz ve ardından tooconvert çalışırsanız kullanarak `Convert-MsolDomaintoFederated -DomainName <your domain>`, biz aşağıdaki hata hello alın.</span><span class="sxs-lookup"><span data-stu-id="914b3-145">So now, if we have successfully added an new domain in hello Azure AD portal and then attempt tooconvert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get hello following error.</span></span>

![Federasyon hata](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="914b3-147">Tooadd hello çalışırsanız `-SupportMultipleDomain` anahtar biz hello aşağıdaki hata alırsınız:</span><span class="sxs-lookup"><span data-stu-id="914b3-147">If you try tooadd hello `-SupportMultipleDomain` switch we will receive hello following error:</span></span>

![Federasyon hata](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="914b3-149">Yalnızca toorun çalışırken `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` hello üzerinde özgün etki alanı ayrıca bir hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="914b3-149">Simply trying toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on hello original domain will also result in an error.</span></span>

![Federasyon hata](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="914b3-151">Merhaba tooadd ek bir üst düzey etki alanı adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="914b3-151">Use hello steps below tooadd an additional top-level domain.</span></span>  <span data-ttu-id="914b3-152">Bir etki alanı eklemiş ve hello kullanmadı `-SupportMultipleDomain` kaldırma ve özgün etki alanınızın güncelleştirme için hello adımlara parametre Başlat.</span><span class="sxs-lookup"><span data-stu-id="914b3-152">If you have already added a domain and did not use hello `-SupportMultipleDomain` parameter start with hello steps for removing and updating your original domain.</span></span>  <span data-ttu-id="914b3-153">Henüz bir üst düzey etki alanı eklemediyseniz PowerShell Azure AD Connect kullanarak bir etki alanı eklemek için hello adımlara başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="914b3-153">If you have not added a top-level domain yet you can start with hello steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="914b3-154">Aşağıdaki adımları tooremove hello Microsoft Online güven hello kullanın ve özgün etki alanınızın güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="914b3-154">Use hello following steps tooremove hello Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="914b3-155">AD FS federasyon sunucunuzda açık **AD FS yönetimi.**</span><span class="sxs-lookup"><span data-stu-id="914b3-155">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="914b3-156">Merhaba solda genişletin **güven ilişkileri** ve **bağlı olan taraf güvenleri**</span><span class="sxs-lookup"><span data-stu-id="914b3-156">On hello left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="914b3-157">Merhaba sağ Hello üzerinde silme **Microsoft Office 365 kimlik Platformu'na** girişi.</span><span class="sxs-lookup"><span data-stu-id="914b3-157">On hello right, delete hello **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="914b3-158">![Microsoft çevrimiçi kaldırma](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="914b3-158">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="914b3-159">Sahip bir makinede [Azure Active Directory için Windows PowerShell Modülü](https://msdn.microsoft.com/library/azure/jj151815.aspx) yüklü hello aşağıdaki komutu çalıştırın: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="914b3-159">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="914b3-160">Hello Azure AD etki alanı ile federasyonunu Hello kullanıcı genel Yönetici adını ve parolasını girin</span><span class="sxs-lookup"><span data-stu-id="914b3-160">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="914b3-161">PowerShell'de girin`Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="914b3-161">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="914b3-162">PowerShell'de girin `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="914b3-162">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="914b3-163">Merhaba özgün etki alanı için budur.</span><span class="sxs-lookup"><span data-stu-id="914b3-163">This is for hello original domain.</span></span>  <span data-ttu-id="914b3-164">Bunu etki alanları bu olacaktır hello kullanarak:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="914b3-164">So using hello above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="914b3-165">PowerShell kullanarak tooadd hello yeni üst düzey etki alanı kullanım hello aşağıdaki adımları</span><span class="sxs-lookup"><span data-stu-id="914b3-165">Use hello following steps tooadd hello new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="914b3-166">Sahip bir makinede [Azure Active Directory için Windows PowerShell Modülü](https://msdn.microsoft.com/library/azure/jj151815.aspx) yüklü hello aşağıdaki komutu çalıştırın: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="914b3-166">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="914b3-167">Hello Azure AD etki alanı ile federasyonunu Hello kullanıcı genel Yönetici adını ve parolasını girin</span><span class="sxs-lookup"><span data-stu-id="914b3-167">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="914b3-168">PowerShell'de girin`Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="914b3-168">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="914b3-169">PowerShell'de girin`New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="914b3-169">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="914b3-170">Azure AD Connect'i kullanarak adımları tooadd hello yeni üst düzey etki alanı aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="914b3-170">Use hello following steps tooadd hello new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="914b3-171">Azure AD Connect hello masaüstünden başlatmak veya Başlat menüsü</span><span class="sxs-lookup"><span data-stu-id="914b3-171">Launch Azure AD Connect from hello desktop or start menu</span></span>
2. <span data-ttu-id="914b3-172">"Ek Azure AD etki alanı Ekle" seçin ![ek bir ekleme Azure AD etki alanı](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="914b3-172">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="914b3-173">Azure AD girin ve Active Directory kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="914b3-173">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="914b3-174">Federasyon tooconfigure istediğiniz hello ikinci etki alanını seçin.</span><span class="sxs-lookup"><span data-stu-id="914b3-174">Select hello second domain you wish tooconfigure for federation.</span></span>
   <span data-ttu-id="914b3-175">![Ek bir ekleme Azure AD etki alanı](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="914b3-175">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="914b3-176">Yükle'yi tıklatın</span><span class="sxs-lookup"><span data-stu-id="914b3-176">Click Install</span></span>

### <a name="verify-hello-new-top-level-domain"></a><span data-ttu-id="914b3-177">Merhaba yeni üst düzey etki alanını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="914b3-177">Verify hello new top-level domain</span></span>
<span data-ttu-id="914b3-178">Merhaba PowerShell komutunu kullanarak `Get-MsolDomainFederationSettings -DomainName <your domain>`görüntüleyebileceğiniz hello IssuerUri güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="914b3-178">By using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view hello updated IssuerUri.</span></span>  <span data-ttu-id="914b3-179">Merhaba Federasyon ayarlar bizim özgün etki alanı http://bmcontoso.com/adfs/services/trust üzerinde güncelleştirildi Hello ekran görüntüsü aşağıda gösterir</span><span class="sxs-lookup"><span data-stu-id="914b3-179">hello screenshot below shows hello federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="914b3-181">Merhaba, yeni bir etki alanı üzerinde IssuerUri toohttps://bmfabrikam.com/adfs/services/trust ayarlayın</span><span class="sxs-lookup"><span data-stu-id="914b3-181">And hello IssuerUri on our new domain has been set toohttps://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="914b3-183">Alt etki alanları desteği</span><span class="sxs-lookup"><span data-stu-id="914b3-183">Support for Sub-domains</span></span>
<span data-ttu-id="914b3-184">Bir alt etki alanı eklediğinizde, hello nedeniyle şekilde Azure AD etki alanları ele, hello üst öğesinin hello ayarlarını devralır.</span><span class="sxs-lookup"><span data-stu-id="914b3-184">When you add a sub-domain, because of hello way Azure AD handled domains, it will inherit hello settings of hello parent.</span></span>  <span data-ttu-id="914b3-185">Başka bir deyişle, bu hello IssuerUri toomatch hello üst gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="914b3-185">This means that hello IssuerUri needs toomatch hello parents.</span></span>

<span data-ttu-id="914b3-186">Bu nedenle deyin ı bmcontoso.com varsa ve corp.bmcontoso.com eklemek örneğin olanak sağlar.  Corp.bmcontoso.com kullanıcıdan toobe gerekir bu anlamına gelir, hello IssuerUri **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="914b3-186">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.  This means that hello IssuerUri for a user from corp.bmcontoso.com will need toobe **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="914b3-187">Azure AD için yukarıdaki Hello standart kural uygulanmadı ancak bir veren belirteciyle oluşturacak **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="914b3-187">However hello standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="914b3-188">Merhaba etki alanının gerekli değer eşleşmez ve kimlik doğrulaması başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="914b3-188">which will not match hello domain's required value and authentication will fail.</span></span>

### <a name="how-tooenable-support-for-sub-domains"></a><span data-ttu-id="914b3-189">Tooenable alt etki alanları için nasıl destekler</span><span class="sxs-lookup"><span data-stu-id="914b3-189">How tooenable support for sub-domains</span></span>
<span data-ttu-id="914b3-190">Sipariş toowork bu hello geçici olarak AD FS bağlı olan taraf güveni için Microsoft Online güncelleştirilmiş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="914b3-190">In order toowork around this hello AD FS relying party trust for Microsoft Online needs toobe updated.</span></span>  <span data-ttu-id="914b3-191">toodo Bu, bir özel talep kuralı, tüm alt etki alanlarından hello kullanıcının UPN soneki kapalı hello özel veren değeriyle oluşturulurken şeritler şekilde yapılandırmalısınız.</span><span class="sxs-lookup"><span data-stu-id="914b3-191">toodo this, you must configure a custom claim rule so that it strips off any sub-domains from hello user’s UPN suffix when constructing hello custom Issuer value.</span></span> 

<span data-ttu-id="914b3-192">Talep aşağıdaki hello bunu yapın:</span><span class="sxs-lookup"><span data-stu-id="914b3-192">hello following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="914b3-193">Merhaba numaraya hello normal ifadede hello kök etki alanında yok kaç üst etki alanları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="914b3-193">hello last number in hello regular expression set hello how many parent domains there is in your root domain.</span></span> <span data-ttu-id="914b3-194">Burada i sahip bmcontoso.com şekilde iki üst etki alanı gerekli.</span><span class="sxs-lookup"><span data-stu-id="914b3-194">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="914b3-195">Üç tutulan toobe olan etki alanları üst varsa (örneğin: corp.bmcontoso.com), hello numarası üç olabilirdi sonra.</span><span class="sxs-lookup"><span data-stu-id="914b3-195">If three parent domains were toobe kept (i.e.: corp.bmcontoso.com), then hello number would have been three.</span></span> <span data-ttu-id="914b3-196">Eventualy bir aralık belirtilebilir, hello eşleşme toomatch hello maksimum etki alanlarının her zaman yapılmayacak.</span><span class="sxs-lookup"><span data-stu-id="914b3-196">Eventualy a range can be indicated, hello match will always be made toomatch hello maximum of domains.</span></span> <span data-ttu-id="914b3-197">"{2,3}" iki toothree etki alanı eşleşir (örn: bmfabrikam.com ve corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="914b3-197">"{2,3}" will match two toothree domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="914b3-198">Aşağıdaki adımları tooadd hello bir özel talep toosupport alt etki alanlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="914b3-198">Use hello following steps tooadd a custom claim toosupport sub-domains.</span></span>

1. <span data-ttu-id="914b3-199">Açık AD FS Yönetimi</span><span class="sxs-lookup"><span data-stu-id="914b3-199">Open AD FS Management</span></span>
2. <span data-ttu-id="914b3-200">Merhaba Microsoft çevrimiçi RP güven sağ tıklayın ve düzenlemek talep kurallarını seçin</span><span class="sxs-lookup"><span data-stu-id="914b3-200">Right click hello Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="914b3-201">Merhaba üçüncü talep kuralı seçin ve Değiştir ![düzenleme talep](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="914b3-201">Select hello third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="914b3-202">Merhaba geçerli talep değiştirin:</span><span class="sxs-lookup"><span data-stu-id="914b3-202">Replace hello current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Talep değiştirin](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="914b3-204">Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="914b3-204">Click Ok.</span></span>  <span data-ttu-id="914b3-205">Uygula'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="914b3-205">Click Apply.</span></span>  <span data-ttu-id="914b3-206">Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="914b3-206">Click Ok.</span></span>  <span data-ttu-id="914b3-207">AD FS Yönetimi'ni kapatın.</span><span class="sxs-lookup"><span data-stu-id="914b3-207">Close AD FS Management.</span></span>

