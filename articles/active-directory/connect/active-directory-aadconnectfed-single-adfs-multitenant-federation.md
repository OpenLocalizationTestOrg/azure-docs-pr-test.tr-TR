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
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a>Azure AD’nin birden çok örneğini tek bir AD FS örneği ile birleştirme

Aralarında iki yönlü güven varsa, tek bir yüksek kullanılabilirlikli AD FS ormanı birden çok ormanı birleştirebilir. Bu birden çok ormanı olabilir veya toohello karşılık gelmeyebilir aynı Azure Active Directory. Bu makalede, tek bir AD FS dağıtımı ile birden fazla arasındaki tooconfigure Federasyon, Azure AD eşitleme toodifferent nasıl ormanlar yönergeler sağlar.

![Tek AD FS ile çok kiracılı federasyon](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> Bu senaryoda cihaz geri yazma ve otomatik cihaz katılımı desteklenmez.

> [!NOTE]
> Azure AD Connect Azure AD Connect Federasyon etki alanları için tek bir Azure AD içinde yapılandırabilirsiniz Bu senaryoda kullanılan tooconfigure Federasyon olamaz.

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a>AD FS’yi birden çok Azure AD ile birleştirmek için uygulanması gereken adımlar

Azure Active Directory contoso.onmicrosoft.com bir etki alanı contoso.com zaten hello AD FS contoso.com şirket içi Active Directory ortamında yüklü şirket içinde Federasyon göz önünde bulundurun. Fabrikam.com, fabrikam.onmicrosoft.com adresli Azure Active Directory’de bir etki alanıdır.

##<a name="step-1-establish-a-two-way-trust"></a>1. Adım: İki yönlü güven kurma
 
Contoso.com toobe mümkün tooauthenticate kullanıcılar fabrikam.com içinde AD FS için contoso.com ve fabrikam.com arasında iki yönlü bir güven gereklidir. Bu kılavuz Hello izleyin [makale](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello iki yönlü güven.
 
##<a name="step-2-modify-contosocom-federation-settings"></a>2. Adım: contoso.com federasyon ayarlarını değiştirme 
 
hello varsayılan veren bir Federasyon tek bir etki alanı tooAD FS "http://ADFSServiceFQDN/adfs/services/trust", örneğin, "http://fs.contoso.com/adfs/services/trust" için ayarlayın. Azure Active Directory, federasyona eklenen her etki alanı için benzersiz bir veren gerektirir. Merhaba aynı AD FS toofederate iki etki alanı geçiyor olduğundan, Azure Active Directory ile AD FS federates her etki alanı için benzersiz şekilde değiştirilebilir toobe hello veren değeriyle gerekir. 
 
Merhaba AD FS sunucusunda Azure AD PowerShell'i açın ve hello aşağıdaki adımları gerçekleştirin:
 
Toohello contoso.com güncelleştirme MsolFederatedDomain - DomainName contoso.com hello etki alanı contoso.com Bağlan MsolService güncelleştirme hello Federasyon ayarlarını içeren Azure Active Directory connect – SupportMultipleDomain
 
Merhaba etki alanı Federasyon ayarını veren değiştirilmesi "http://contoso.com/adfs/services/trust" ve bir verme kuralı eklenecek hello Azure AD bağlı olan taraf güveni tooissue hello issuerId değerine göre hello UPN soneki üzerinde doğru için çok talep.
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a>3. adım: fabrikam.com’u AD FS ile birleştirin
 
Azure AD PowerShell'de oturum hello aşağıdaki adımları gerçekleştirin: tooAzure hello etki alanı fabrikam.com içeren Active Directory Connect

    Connect-MsolService
Merhaba fabrikam.com yönetilen etki alanı toofederated Dönüştür:

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
Merhaba işlemi yukarıda hello etki alanı fabrikam.com hello aynı AD FS ile birleştirmek. Merhaba etki alanı ayarları her iki etki alanı için Get-MsolDomainFederationSettings kullanarak doğrulayabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
[Azure Active Directory ile Active Directory’yi bağlama](active-directory-aadconnect.md)
