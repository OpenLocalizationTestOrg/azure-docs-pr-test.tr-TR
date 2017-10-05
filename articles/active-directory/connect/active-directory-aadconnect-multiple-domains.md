---
title: "Azure AD Connect birden çok etki alanı"
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
ms.openlocfilehash: 8e3f496c2868cc3430e0efd47805aec2205168aa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="43123-103">Azure AD ile Federasyon için Çoklu Etki Alanı Desteği</span><span class="sxs-lookup"><span data-stu-id="43123-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="43123-104">Aşağıdaki belgeler Office 365 veya Azure AD etki alanları ile federasyonunu zaman birden çok üst düzey etki alanları ve alt etki alanlarını kullanma hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="43123-104">The following documentation provides guidance on how to use multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="43123-105">Birden çok üst düzey etki alanı desteği</span><span class="sxs-lookup"><span data-stu-id="43123-105">Multiple top-level domain support</span></span>
<span data-ttu-id="43123-106">Birden çok federasyonunu, üst düzey etki alanlarının Azure AD ile bir üst düzey etki alanı ile federasyonunu kullanılırken gerekli değildir bazı ek yapılandırma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="43123-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="43123-107">Bir etki alanı Azure AD ile Federasyon olduğunda, çeşitli özellikleri etki alanı Azure ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="43123-107">When a domain is federated with Azure AD, several properties are set on the domain in Azure.</span></span>  <span data-ttu-id="43123-108">Bir önemli IssuerUri adrestir.</span><span class="sxs-lookup"><span data-stu-id="43123-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="43123-109">Azure AD tarafından belirteci ile ilişkili etki alanını tanımlamak için kullanılan bir URI budur.</span><span class="sxs-lookup"><span data-stu-id="43123-109">This is a URI that is used by Azure AD to identify the domain that the token is associated with.</span></span>  <span data-ttu-id="43123-110">URI, herhangi bir şey ancak geçerli bir URI olmalıdır çözümlemek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="43123-110">The URI doesn’t need to resolve to anything but it must be a valid URI.</span></span>  <span data-ttu-id="43123-111">Varsayılan olarak, Azure AD bu Federasyon Hizmeti tanımlayıcısı değerine, şirket içi AD FS ayarlar yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="43123-111">By default, Azure AD sets this to the value of the federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="43123-112">Federasyon Hizmeti tanımlayıcısı bir Federasyon Hizmeti benzersiz olarak tanımlayan bir URI değil.</span><span class="sxs-lookup"><span data-stu-id="43123-112">The federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="43123-113">Federasyon Hizmeti AD FS bu işlevler güvenlik belirteci hizmeti örneğidir.</span><span class="sxs-lookup"><span data-stu-id="43123-113">The federation service is an instance of AD FS that functions as the security token service.</span></span> 
> 
> 

<span data-ttu-id="43123-114">PowerShell komutunu kullanarak görünümü IssuerUri yapabilecekleriniz `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span><span class="sxs-lookup"><span data-stu-id="43123-114">You can vew IssuerUri by using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="43123-116">Birden çok üst düzey etki alanı eklemek istediğinizde bir sorun ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="43123-116">A problem arises when we want to add more than one top-level domain.</span></span>  <span data-ttu-id="43123-117">Örneğin, Kurulum Federasyon Azure AD arasında sahip düşünelim ve şirket içi ortamınıza.</span><span class="sxs-lookup"><span data-stu-id="43123-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="43123-118">Bu belge için bmcontoso.com kullanıyorum.</span><span class="sxs-lookup"><span data-stu-id="43123-118">For this document I am using bmcontoso.com.</span></span>  <span data-ttu-id="43123-119">İkinci, üst düzey etki alanı eklemiş olduğunuz artık bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="43123-119">Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Etki Alanları](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="43123-121">Biz birleştirilecek bizim bmfabrikam.com etki alanı dönüştürmeye çalıştığınızda, biz hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="43123-121">When we attempt to convert our bmfabrikam.com domain to be federated, we receive an error.</span></span>  <span data-ttu-id="43123-122">Bunun nedeni, Azure AD'de birden fazla etki alanı için aynı değeri sağlamak IssuerUri özelliğe izin vermeyen bir kısıtlaması vardır.</span><span class="sxs-lookup"><span data-stu-id="43123-122">The reason for this is, Azure AD has a constraint that does not allow the IssuerUri property to have the same value for more than one domain.</span></span>  

![Federasyon hata](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="43123-124">SupportMultipleDomain parametresi</span><span class="sxs-lookup"><span data-stu-id="43123-124">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="43123-125">Geçici çözüm için bu, hangi kullanılarak yapılabilir farklı bir IssuerUri eklemek ihtiyacımız `-SupportMultipleDomain` parametresi.</span><span class="sxs-lookup"><span data-stu-id="43123-125">To workaround this, we need to add a different IssuerUri which can be done by using the `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="43123-126">Bu parametre, aşağıdaki cmdlet ile birlikte kullanılır:</span><span class="sxs-lookup"><span data-stu-id="43123-126">This parameter is used with the following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="43123-127">Bu parametre, Azure AD etki alanı adını temel alarak IssuerUri yapılandırın yapar.</span><span class="sxs-lookup"><span data-stu-id="43123-127">This parameter makes Azure AD configure the IssuerUri so that it is based on the name of the domain.</span></span>  <span data-ttu-id="43123-128">Bu dizinlerde Azure AD içinde benzersiz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="43123-128">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="43123-129">Parametresini kullanarak başarıyla tamamlamak için PowerShell komutunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="43123-129">Using the parameter allows the PowerShell command to complete successfully.</span></span>

![Federasyon hata](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="43123-131">Bizim yeni bmfabrikam.com etki alanı ayarında aramanız aşağıdakileri görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="43123-131">Looking at the settings of our new bmfabrikam.com domain you can see the following:</span></span>

![Federasyon hata](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="43123-133">Unutmayın `-SupportMultipleDomain` hangi adfs.bmcontoso.com bizim Federasyon Hizmeti'ne işaret edecek şekilde yapılandırılmış olan diğer uç noktalardan değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="43123-133">Note that `-SupportMultipleDomain` does not change the other endpoints which are still configured to point to our federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="43123-134">Başka bir şey, `-SupportMultipleDomain` yapar, uygun veren değeriyle AD FS sistem için Azure AD yayınlanan belirteçleri içerir güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="43123-134">Another thing that `-SupportMultipleDomain` does is that it ensures that the AD FS system includes the proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="43123-135">Bunu kullanıcıların UPN etki alanı kısmı alma ve bu etki alanında IssuerUri, yani https://{upn soneki olarak ayarlayarak yapar} / adfs/services/güven.</span><span class="sxs-lookup"><span data-stu-id="43123-135">It does this by taking the domain portion of the users UPN and setting this as the domain in the IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="43123-136">Bu nedenle Azure ad kimlik doğrulaması sırasında veya kullanıcı belirteci IssuerUri öğesinde, Office 365, Azure AD etki alanını bulmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="43123-136">Thus during authentication to Azure AD or Office 365, the IssuerUri element in the user’s token is used to locate the domain in Azure AD.</span></span>  <span data-ttu-id="43123-137">Kimlik doğrulaması başarısız olur bir eşleşme bulunamazsa.</span><span class="sxs-lookup"><span data-stu-id="43123-137">If a match cannot be found the authentication will fail.</span></span> 

<span data-ttu-id="43123-138">Örneğin, bir kullanıcının UPN ise bsimon@bmcontoso.com, belirteç AD FS sorunları IssuerUri öğesinde http://bmcontoso.com/adfs/services/trust için ayarlanacak.</span><span class="sxs-lookup"><span data-stu-id="43123-138">For example, if a user’s UPN is bsimon@bmcontoso.com, the IssuerUri element in the token AD FS issues will be set to http://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="43123-139">Bu Azure AD yapılandırma ile eşleşir ve kimlik doğrulama başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="43123-139">This will match the Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="43123-140">Bu mantığı uygular özelleştirilmiş talep kuralı verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="43123-140">The following is the customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="43123-141">Yeni Ekle veya zaten Dönüştür girişimi etki alanları eklendiğinde - SupportMultipleDomain anahtar kullanabilmek için Kurulum başlangıçta desteklemek için federasyon güven olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="43123-141">In order to use the -SupportMultipleDomain switch when attempting to add new or convert already added domains, you need to have setup your federated trust to support them originally.</span></span>  
> 
> 

## <a name="how-to-update-the-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="43123-142">AD FS ile Azure AD arasında güven güncelleştirmek nasıl</span><span class="sxs-lookup"><span data-stu-id="43123-142">How to update the trust between AD FS and Azure AD</span></span>
<span data-ttu-id="43123-143">AD FS ile Azure AD Örneğinize arasında federe güven Kurulum belirtilmedi, bu güven yeniden oluşturmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="43123-143">If you did not setup the federated trust between AD FS and your instance of Azure AD, you may need to re-create this trust.</span></span>  <span data-ttu-id="43123-144">Kurulum olmadan başlangıçta olduğu zaman, bunun nedeni `-SupportMultipleDomain` parametresi IssuerUri varsayılan değer olan ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="43123-144">This is because, when it is originally setup without the `-SupportMultipleDomain` parameter, the IssuerUri is set with the default value.</span></span>  <span data-ttu-id="43123-145">Aşağıdaki ekran görüntüsünde IssuerUri https://adfs.bmcontoso.com/adfs/services/trust için ayarlandığını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43123-145">In the screenshot below you can see the IssuerUri is set to https://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="43123-146">Bunu şimdi, Azure AD portalında yeni bir etki alanı başarıyla eklediniz ve kullanarak dönüştürmeyi denemeden `Convert-MsolDomaintoFederated -DomainName <your domain>`, biz aşağıdaki hatayı alıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="43123-146">So now, if we have successfully added an new domain in the Azure AD portal and then attempt to convert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get the following error.</span></span>

![Federasyon hata](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="43123-148">Eklemeyi denediğinizde `-SupportMultipleDomain` anahtar biz aşağıdaki hatayı alırsınız:</span><span class="sxs-lookup"><span data-stu-id="43123-148">If you try to add the `-SupportMultipleDomain` switch we will receive the following error:</span></span>

![Federasyon hata](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="43123-150">Çalıştırmayı denerseniz `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` özgün etki alanında da bir hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="43123-150">Simply trying to run `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on the original domain will also result in an error.</span></span>

![Federasyon hata](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="43123-152">Ek bir üst düzey etki alanı eklemek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="43123-152">Use the steps below to add an additional top-level domain.</span></span>  <span data-ttu-id="43123-153">Bir etki alanı eklemiş ve kullanmaz `-SupportMultipleDomain` kaldırma ve özgün etki alanınızın güncelleştirme için adımlara parametre Başlat.</span><span class="sxs-lookup"><span data-stu-id="43123-153">If you have already added a domain and did not use the `-SupportMultipleDomain` parameter start with the steps for removing and updating your original domain.</span></span>  <span data-ttu-id="43123-154">Henüz bir üst düzey etki alanı eklemediyseniz PowerShell Azure AD Connect kullanarak bir etki alanı ekleme adımları başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43123-154">If you have not added a top-level domain yet you can start with the steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="43123-155">Microsoft Online güven kaldırın ve özgün etki alanınızın güncelleştirmek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="43123-155">Use the following steps to remove the Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="43123-156">AD FS federasyon sunucunuzda açık **AD FS yönetimi.**</span><span class="sxs-lookup"><span data-stu-id="43123-156">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="43123-157">Sol bölmede, genişletin **güven ilişkileri** ve **bağlı olan taraf güvenleri**</span><span class="sxs-lookup"><span data-stu-id="43123-157">On the left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="43123-158">Sağ tarafta silme **Microsoft Office 365 kimlik Platformu'na** girişi.</span><span class="sxs-lookup"><span data-stu-id="43123-158">On the right, delete the **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="43123-159">![Microsoft çevrimiçi kaldırma](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="43123-159">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="43123-160">Sahip bir makinede [Azure Active Directory için Windows PowerShell Modülü](https://msdn.microsoft.com/library/azure/jj151815.aspx) yüklü aşağıdaki komutu çalıştırın: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="43123-160">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="43123-161">Kullanıcı adı ve parola genel yöneticinin ile federasyonunu Azure AD etki alanını girin</span><span class="sxs-lookup"><span data-stu-id="43123-161">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="43123-162">PowerShell'de girin`Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="43123-162">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="43123-163">PowerShell'de girin `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="43123-163">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="43123-164">Özgün etki alanı için budur.</span><span class="sxs-lookup"><span data-stu-id="43123-164">This is for the original domain.</span></span>  <span data-ttu-id="43123-165">Bu nedenle bu olacaktır yukarıdaki etki alanlarını kullanma:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="43123-165">So using the above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="43123-166">PowerShell kullanarak yeni üst düzey etki alanı eklemek için aşağıdaki adımları kullanın</span><span class="sxs-lookup"><span data-stu-id="43123-166">Use the following steps to add the new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="43123-167">Sahip bir makinede [Azure Active Directory için Windows PowerShell Modülü](https://msdn.microsoft.com/library/azure/jj151815.aspx) yüklü aşağıdaki komutu çalıştırın: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="43123-167">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="43123-168">Kullanıcı adı ve parola genel yöneticinin ile federasyonunu Azure AD etki alanını girin</span><span class="sxs-lookup"><span data-stu-id="43123-168">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="43123-169">PowerShell'de girin`Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="43123-169">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="43123-170">PowerShell'de girin`New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="43123-170">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="43123-171">Azure AD Connect'i kullanarak yeni üst düzey etki alanı eklemek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="43123-171">Use the following steps to add the new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="43123-172">Azure AD Connect masaüstünden başlatmak veya Başlat menüsü</span><span class="sxs-lookup"><span data-stu-id="43123-172">Launch Azure AD Connect from the desktop or start menu</span></span>
2. <span data-ttu-id="43123-173">"Ek Azure AD etki alanı Ekle" seçin ![ek bir ekleme Azure AD etki alanı](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="43123-173">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="43123-174">Azure AD girin ve Active Directory kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="43123-174">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="43123-175">Federasyon için yapılandırmak istediğiniz ikinci etki alanını seçin.</span><span class="sxs-lookup"><span data-stu-id="43123-175">Select the second domain you wish to configure for federation.</span></span>
   <span data-ttu-id="43123-176">![Ek bir ekleme Azure AD etki alanı](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="43123-176">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="43123-177">Yükle'yi tıklatın</span><span class="sxs-lookup"><span data-stu-id="43123-177">Click Install</span></span>

### <a name="verify-the-new-top-level-domain"></a><span data-ttu-id="43123-178">Yeni üst düzey etki alanını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="43123-178">Verify the new top-level domain</span></span>
<span data-ttu-id="43123-179">PowerShell komutunu kullanarak `Get-MsolDomainFederationSettings -DomainName <your domain>`güncelleştirilmiş IssuerUri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43123-179">By using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view the updated IssuerUri.</span></span>  <span data-ttu-id="43123-180">Aşağıdaki ekran görüntüsünde ayarlar bizim özgün etki alanı http://bmcontoso.com/adfs/services/trust üzerinde güncelleştirildi Federasyon gösterir.</span><span class="sxs-lookup"><span data-stu-id="43123-180">The screenshot below shows the federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="43123-182">Bizim yeni bir etki alanı üzerinde IssuerUri https://bmfabrikam.com/adfs/services/trust için ayarlayın</span><span class="sxs-lookup"><span data-stu-id="43123-182">And the IssuerUri on our new domain has been set to https://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="43123-184">Alt etki alanları desteği</span><span class="sxs-lookup"><span data-stu-id="43123-184">Support for Sub-domains</span></span>
<span data-ttu-id="43123-185">İşlenen şekilde Azure AD etki alanları nedeniyle bir alt etki alanı eklediğinizde, üst öğesinin ayarlarını devralır.</span><span class="sxs-lookup"><span data-stu-id="43123-185">When you add a sub-domain, because of the way Azure AD handled domains, it will inherit the settings of the parent.</span></span>  <span data-ttu-id="43123-186">Bu, IssuerUri Üst eşleşmesi gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="43123-186">This means that the IssuerUri needs to match the parents.</span></span>

<span data-ttu-id="43123-187">Bu nedenle deyin ı bmcontoso.com varsa ve corp.bmcontoso.com eklemek örneğin olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="43123-187">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.</span></span>  <span data-ttu-id="43123-188">Bir kullanıcıdan corp.bmcontoso.com IssuerUri olması gerekir yani **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="43123-188">This means that the IssuerUri for a user from corp.bmcontoso.com will need to be **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="43123-189">Yukarıda Azure AD için uygulanan standart kural oluşturacağını ancak bir veren belirteciyle **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="43123-189">However the standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="43123-190">değeri gerekli etki alanı eşleşmez ve kimlik doğrulaması başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="43123-190">which will not match the domain's required value and authentication will fail.</span></span>

### <a name="how-to-enable-support-for-sub-domains"></a><span data-ttu-id="43123-191">Alt etki alanları desteği etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="43123-191">How To enable support for sub-domains</span></span>
<span data-ttu-id="43123-192">AD FS bu sorunu çözmek için Microsoft Online bağlı olan taraf güveni güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="43123-192">In order to work around this the AD FS relying party trust for Microsoft Online needs to be updated.</span></span>  <span data-ttu-id="43123-193">Bunu yapmak için tüm alt etki alanlarından kullanıcı UPN soneki kapalı özel veren değeriyle oluşturulurken şeritler böylece özel talep kuralı yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="43123-193">To do this, you must configure a custom claim rule so that it strips off any sub-domains from the user’s UPN suffix when constructing the custom Issuer value.</span></span> 

<span data-ttu-id="43123-194">Aşağıdaki talep bunu yapın:</span><span class="sxs-lookup"><span data-stu-id="43123-194">The following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="43123-195">Normal ifade son sayısı, kök etki alanında yok kaç üst etki alanları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="43123-195">The last number in the regular expression set the how many parent domains there is in your root domain.</span></span> <span data-ttu-id="43123-196">Burada i sahip bmcontoso.com şekilde iki üst etki alanı gerekli.</span><span class="sxs-lookup"><span data-stu-id="43123-196">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="43123-197">Etki alanları üç ana durumunda tutulması gerçekleştirilen (örn: corp.bmcontoso.com), sayı üç olabilirdi sonra.</span><span class="sxs-lookup"><span data-stu-id="43123-197">If three parent domains were to be kept (i.e.: corp.bmcontoso.com), then the number would have been three.</span></span> <span data-ttu-id="43123-198">Eventualy bir aralık gösterilen, eşleşme her zaman maksimum etki alanlarının eşleşmesi için yapılır.</span><span class="sxs-lookup"><span data-stu-id="43123-198">Eventualy a range can be indicated, the match will always be made to match the maximum of domains.</span></span> <span data-ttu-id="43123-199">"{2,3}" iki ila üç etki alanları eşleşir (örn: bmfabrikam.com ve corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="43123-199">"{2,3}" will match two to three domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="43123-200">Alt etki alanlarını desteklemek için bir özel talep eklemek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="43123-200">Use the following steps to add a custom claim to support sub-domains.</span></span>

1. <span data-ttu-id="43123-201">Açık AD FS Yönetimi</span><span class="sxs-lookup"><span data-stu-id="43123-201">Open AD FS Management</span></span>
2. <span data-ttu-id="43123-202">Microsoft çevrimiçi RP güven sağ tıklayın ve düzenlemek talep kurallarını seçin</span><span class="sxs-lookup"><span data-stu-id="43123-202">Right click the Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="43123-203">Üçüncü talep kuralı seçin ve Değiştir ![düzenleme talep](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="43123-203">Select the third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="43123-204">Geçerli talep değiştirin:</span><span class="sxs-lookup"><span data-stu-id="43123-204">Replace the current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Talep değiştirin](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="43123-206">Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="43123-206">Click Ok.</span></span>  <span data-ttu-id="43123-207">Uygula'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="43123-207">Click Apply.</span></span>  <span data-ttu-id="43123-208">Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="43123-208">Click Ok.</span></span>  <span data-ttu-id="43123-209">AD FS Yönetimi'ni kapatın.</span><span class="sxs-lookup"><span data-stu-id="43123-209">Close AD FS Management.</span></span>

