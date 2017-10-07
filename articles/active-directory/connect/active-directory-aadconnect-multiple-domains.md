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
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a>Azure AD ile Federasyon için Çoklu Etki Alanı Desteği
Merhaba aşağıdaki belgeleri rehberlik sağlar toouse birden çok üst düzey etki alanları ve Office 365 veya Azure AD etki alanlarıyla federasyonunu alt etki alanları.

## <a name="multiple-top-level-domain-support"></a>Birden çok üst düzey etki alanı desteği
Birden çok federasyonunu, üst düzey etki alanlarının Azure AD ile bir üst düzey etki alanı ile federasyonunu kullanılırken gerekli değildir bazı ek yapılandırma gerektirir.

Bir etki alanı Azure AD ile Federasyon olduğunda, çeşitli özellikler Azure hello etki alanına ayarlanır.  Bir önemli IssuerUri adrestir.  Kullanılan URI budur Azure AD tooidentify tarafından belirteci hello hello etki alanı ile ilişkili.  Merhaba URI tooresolve tooanything gerek yoktur, ancak geçerli bir URI olmalıdır.  Varsayılan olarak, Azure AD hello Federasyon Hizmeti tanımlayıcısı bu toohello değerini, şirket içi AD FS ayarlar yapılandırma.

> [!NOTE]
> Merhaba Federasyon Hizmeti tanımlayıcısı bir Federasyon Hizmeti benzersiz olarak tanımlayan bir URI değil.  Merhaba Federasyon Hizmeti AD FS bu işlevleri hello güvenlik belirteci hizmeti örneğidir. 
> 
> 

Merhaba PowerShell komutunu kullanarak görünümü IssuerUri yapabilecekleriniz `Get-MsolDomainFederationSettings -DomainName <your domain>`.

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Birden çok üst düzey etki alanı tooadd istiyoruz olduğunda bir sorun ortaya çıkar.  Örneğin, Kurulum Federasyon Azure AD arasında sahip düşünelim ve şirket içi ortamınıza.  Bu belge için bmcontoso.com kullanıyorum.  İkinci, üst düzey etki alanı eklemiş olduğunuz artık bmfabrikam.com.

![Etki Alanları](./media/active-directory-multiple-domains/domains.png)

Biz bizim bmfabrikam.com etki alanı toobe federe tooconvert denediğinizde, biz hata alırsınız.  Merhaba Bunun nedeni, Azure AD hello birden fazla etki alanı için aynı değeri IssuerUri özelliği toohave hello izin vermeyen bir kısıtlamaya sahip.  

![Federasyon hata](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a>SupportMultipleDomain parametresi
tooworkaround bunu tooadd hangi hello kullanılarak yapılabilir farklı bir IssuerUri ihtiyacımız `-SupportMultipleDomain` parametresi.  Bu parametre cmdlet'leri aşağıdaki hello ile kullanılır:

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

Bu parametreyi hello hello etki alanı adını temel alarak şekilde hello IssuerUri yapılandırmak Azure AD yapar.  Bu dizinlerde Azure AD içinde benzersiz olacaktır.  Merhaba parametresini kullanarak hello PowerShell komut toocomplete başarıyla sağlar.

![Federasyon hata](./media/active-directory-multiple-domains/convert.png)

Bizim yeni bmfabrikam.com etki alanının Hello ayarları aramanız hello aşağıdakileri görebilirsiniz:

![Federasyon hata](./media/active-directory-multiple-domains/settings.png)

Unutmayın `-SupportMultipleDomain` hello değiştirmez olan diğer uç noktaları toopoint tooour Federasyon Hizmeti üzerinde adfs.bmcontoso.com halen yapılandırılıyor.

Başka bir şey, `-SupportMultipleDomain` yapar, hello uygun veren değeriyle hello AD FS sistem için Azure AD yayınlanan belirteçleri içerir güvence altına alır. Bunu alma hello kullanıcıların UPN hello etki alanı bölümü ve bu hello etki alanında hello IssuerUri, yani https://{upn soneki olarak ayarlayarak yapar} / adfs/services/güven. 

Bu nedenle kimlik doğrulaması tooAzure AD ya da Office 365 sırasında hello IssuerUri hello kullanıcının belirteci kullanılan toolocate hello etki alanı Azure AD'de öğedir.  Bir eşleşme hello kimlik doğrulaması başarısız olur bulunamazsa. 

Örneğin, bir kullanıcının UPN ise bsimon@bmcontoso.com, hello IssuerUri hello belirteci AD FS sorunları öğesinde toohttp://bmcontoso.com/adfs/services/trust ayarlanacaktır. Bu hello Azure AD yapılandırma ile eşleşir ve kimlik doğrulama başarılı olur.

Merhaba, bu mantığı uygular hello özelleştirilmiş talep kuralı aşağıdadır:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> Sipariş toouse - SupportMultipleDomain tooadd yeni çalışırken geçiş veya zaten Dönüştür hello eklenen etki alanlarını, toohave gerek federe güven toosupport Kurulum bunları başlangıçta.  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a>Tooupdate hello nasıl güven AD FS ile Azure AD arasında
AD FS ile Azure AD Örneğinize arasında hello federe güven Kurulum belirtilmedi, toore gerekebilir-bu güven oluşturun.  Kurulum hello olmadan başlangıçta olduğu zaman, bunun nedeni `-SupportMultipleDomain` parametresi hello IssuerUri hello varsayılan değeri ile ayarlanır.  Hello hello IssuerUri toohttps://adfs.bmcontoso.com/adfs/services/trust ayarlanır ekran görüntüsü aşağıda görebilirsiniz.

Bunu şimdi biz hello Azure AD Portalı'nda yeni bir etki alanı başarıyla eklediniz ve ardından tooconvert çalışırsanız kullanarak `Convert-MsolDomaintoFederated -DomainName <your domain>`, biz aşağıdaki hata hello alın.

![Federasyon hata](./media/active-directory-multiple-domains/trust1.png)

Tooadd hello çalışırsanız `-SupportMultipleDomain` anahtar biz hello aşağıdaki hata alırsınız:

![Federasyon hata](./media/active-directory-multiple-domains/trust2.png)

Yalnızca toorun çalışırken `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` hello üzerinde özgün etki alanı ayrıca bir hatayla sonuçlanır.

![Federasyon hata](./media/active-directory-multiple-domains/trust3.png)

Merhaba tooadd ek bir üst düzey etki alanı adımları kullanın.  Bir etki alanı eklemiş ve hello kullanmadı `-SupportMultipleDomain` kaldırma ve özgün etki alanınızın güncelleştirme için hello adımlara parametre Başlat.  Henüz bir üst düzey etki alanı eklemediyseniz PowerShell Azure AD Connect kullanarak bir etki alanı eklemek için hello adımlara başlatabilirsiniz.

Aşağıdaki adımları tooremove hello Microsoft Online güven hello kullanın ve özgün etki alanınızın güncelleştirin.

1. AD FS federasyon sunucunuzda açık **AD FS yönetimi.** 
2. Merhaba solda genişletin **güven ilişkileri** ve **bağlı olan taraf güvenleri**
3. Merhaba sağ Hello üzerinde silme **Microsoft Office 365 kimlik Platformu'na** girişi.
   ![Microsoft çevrimiçi kaldırma](./media/active-directory-multiple-domains/trust4.png)
4. Sahip bir makinede [Azure Active Directory için Windows PowerShell Modülü](https://msdn.microsoft.com/library/azure/jj151815.aspx) yüklü hello aşağıdaki komutu çalıştırın: `$cred=Get-Credential`.  
5. Hello Azure AD etki alanı ile federasyonunu Hello kullanıcı genel Yönetici adını ve parolasını girin
6. PowerShell'de girin`Connect-MsolService -Credential $cred`
7. PowerShell'de girin `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.  Merhaba özgün etki alanı için budur.  Bunu etki alanları bu olacaktır hello kullanarak:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`

PowerShell kullanarak tooadd hello yeni üst düzey etki alanı kullanım hello aşağıdaki adımları

1. Sahip bir makinede [Azure Active Directory için Windows PowerShell Modülü](https://msdn.microsoft.com/library/azure/jj151815.aspx) yüklü hello aşağıdaki komutu çalıştırın: `$cred=Get-Credential`.  
2. Hello Azure AD etki alanı ile federasyonunu Hello kullanıcı genel Yönetici adını ve parolasını girin
3. PowerShell'de girin`Connect-MsolService -Credential $cred`
4. PowerShell'de girin`New-MsolFederatedDomain –SupportMultipleDomain –DomainName`

Azure AD Connect'i kullanarak adımları tooadd hello yeni üst düzey etki alanı aşağıdaki hello kullanın.

1. Azure AD Connect hello masaüstünden başlatmak veya Başlat menüsü
2. "Ek Azure AD etki alanı Ekle" seçin ![ek bir ekleme Azure AD etki alanı](./media/active-directory-multiple-domains/add1.png)
3. Azure AD girin ve Active Directory kimlik bilgileri
4. Federasyon tooconfigure istediğiniz hello ikinci etki alanını seçin.
   ![Ek bir ekleme Azure AD etki alanı](./media/active-directory-multiple-domains/add2.png)
5. Yükle'yi tıklatın

### <a name="verify-hello-new-top-level-domain"></a>Merhaba yeni üst düzey etki alanını doğrulayın
Merhaba PowerShell komutunu kullanarak `Get-MsolDomainFederationSettings -DomainName <your domain>`görüntüleyebileceğiniz hello IssuerUri güncelleştirildi.  Merhaba Federasyon ayarlar bizim özgün etki alanı http://bmcontoso.com/adfs/services/trust üzerinde güncelleştirildi Hello ekran görüntüsü aşağıda gösterir

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Merhaba, yeni bir etki alanı üzerinde IssuerUri toohttps://bmfabrikam.com/adfs/services/trust ayarlayın

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a>Alt etki alanları desteği
Bir alt etki alanı eklediğinizde, hello nedeniyle şekilde Azure AD etki alanları ele, hello üst öğesinin hello ayarlarını devralır.  Başka bir deyişle, bu hello IssuerUri toomatch hello üst gerekiyor.

Bu nedenle deyin ı bmcontoso.com varsa ve corp.bmcontoso.com eklemek örneğin olanak sağlar.  Corp.bmcontoso.com kullanıcıdan toobe gerekir bu anlamına gelir, hello IssuerUri **http://bmcontoso.com/adfs/services/trust.**  Azure AD için yukarıdaki Hello standart kural uygulanmadı ancak bir veren belirteciyle oluşturacak **http://corp.bmcontoso.com/adfs/services/trust.** Merhaba etki alanının gerekli değer eşleşmez ve kimlik doğrulaması başarısız olur.

### <a name="how-tooenable-support-for-sub-domains"></a>Tooenable alt etki alanları için nasıl destekler
Sipariş toowork bu hello geçici olarak AD FS bağlı olan taraf güveni için Microsoft Online güncelleştirilmiş toobe gerekir.  toodo Bu, bir özel talep kuralı, tüm alt etki alanlarından hello kullanıcının UPN soneki kapalı hello özel veren değeriyle oluşturulurken şeritler şekilde yapılandırmalısınız. 

Talep aşağıdaki hello bunu yapın:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
Merhaba numaraya hello normal ifadede hello kök etki alanında yok kaç üst etki alanları ayarlayın. Burada i sahip bmcontoso.com şekilde iki üst etki alanı gerekli. Üç tutulan toobe olan etki alanları üst varsa (örneğin: corp.bmcontoso.com), hello numarası üç olabilirdi sonra. Eventualy bir aralık belirtilebilir, hello eşleşme toomatch hello maksimum etki alanlarının her zaman yapılmayacak. "{2,3}" iki toothree etki alanı eşleşir (örn: bmfabrikam.com ve corp.bmcontoso.com).

Aşağıdaki adımları tooadd hello bir özel talep toosupport alt etki alanlarını kullanın.

1. Açık AD FS Yönetimi
2. Merhaba Microsoft çevrimiçi RP güven sağ tıklayın ve düzenlemek talep kurallarını seçin
3. Merhaba üçüncü talep kuralı seçin ve Değiştir ![düzenleme talep](./media/active-directory-multiple-domains/sub1.png)
4. Merhaba geçerli talep değiştirin:
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Talep değiştirin](./media/active-directory-multiple-domains/sub2.png)

5. Tamam'ı tıklatın.  Uygula'yı tıklatın.  Tamam'ı tıklatın.  AD FS Yönetimi'ni kapatın.

