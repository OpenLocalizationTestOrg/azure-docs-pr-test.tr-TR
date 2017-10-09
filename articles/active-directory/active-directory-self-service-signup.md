---
title: "aaaWhat Azure için Self Servis kaydolma mi? | Microsoft Belgeleri"
description: "Azure için bir genel bakış Self Servis kaydolma toomanage hello nasıl kaydolma işlemini ve nasıl tootake üzerinden bir DNS etki alanı adı."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: dbf3b59e3807e98f7bf39f3d5591fcde01667323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-self-service-signup-for-azure"></a>Azure için Self Servis kaydolma nedir?
Bu konu hello Self Servis kaydolma işlemini açıklar ve nasıl tootake üzerinden bir DNS etki alanı adı.  

## <a name="why-use-self-service-signup"></a>Self Servis kaydolmanın neden kullanılır?
* Get müşteriler tooservices daha hızlı istedikleri.
* E-posta tabanlı teklifleri için bir hizmet oluşturun.
* Hızlı bir şekilde kolay unutmayın iş e-posta benzersizse kullanan toocreate kimlikleri kullanıcıların e-posta tabanlı kaydolma akışları oluşturun.
* Yönetilmeyen Azure dizinler yönetilen dizinlere daha sonra yapılabilir ve diğer hizmetler için yeniden kullanılabilir.

## <a name="terms-and-definitions"></a>Terimleri ve tanımları
* **Self Servis kaydolma**: Bu, bir kullanıcı için bir bulut hizmeti kaydolduğunda ve bunlar için Azure Active Directory (Azure AD) otomatik olarak oluşturulan bir kimlik tabanlı sahip kendi e-posta etki hello yöntemdir.
* **Yönetilmeyen Azure directory**: Bu kimliğe oluşturulduğu hello dizindir. Yönetilmeyen bir dizin yok genel yönetici olan bir dizindir.
* **Kullanıcı e-posta doğrulandı**: Azure AD'de kullanıcı hesabı türü budur. Self Servis Teklif için kaydolan sonra otomatik olarak oluşturulan bir kimliğe sahip bir kullanıcı bir e-posta doğrulanmış kullanıcı olarak bilinir. Bir e-posta doğrulanan kullanıcı ile creationmethod etiketli bir dizin normal üyesidir EmailVerified =.

## <a name="user-experience"></a>Kullanıcı deneyimi
Örneğin, bir kullanıcı, e-posta düşünelim Dan@BellowsCollege.com e-posta yoluyla hassas dosyalar alır. Merhaba dosyaları Azure Rights Management (Azure RMS) tarafından korunmuş. Ancak Can'ın kuruluş, Körüğü üniversitenin, Azure RMS için kaydolmuş değil veya Active Directory RMS dağıtıldığını. Bu durumda, Dan ücretsiz abonelik tooRMS için sipariş tooread korumalı hello dosyalarında kişiler için kaydolabilirsiniz.

Dan BellowsCollege.com toosign sunarak bu Self Servisi için bir e-posta adresi ile Merhaba ilk kullanıcı ise, ardından bir yönetilmeyen dizin Azure AD'de BellowsCollege.com için oluşturulur. Merhaba BellowsCollege.com etki alanındaki diğer kullanıcıların bu teklifi veya benzer bir Self Servis sunumu için kaydolursanız, bunlar ayrıca hello oluşturulan e-posta doğrulanan kullanıcı hesapları aynı yönetilmeyen sahip olur Azure dizin.

## <a name="admin-experience"></a>Yönetici deneyimi
Yönetilmeyen bir Azure directory hello DNS etki alanı adına sahip bir yönetici devralır veya sahipliği kanıtlayan sonra hello dizin birleştirin. hello Yöneticisi deneyimi daha ayrıntılı Hello sonraki bölümlerde açıklanmaktadır, ancak bir özeti aşağıda verilmiştir:

* Yönetilmeyen bir Azure dizin üzerinde alırken, yalnızca hello hello yönetilmeyen dizinin genel Yöneticisi haline gelir. Bazen, bir iç devralma da denir.
* Yönetilmeyen bir Azure dizini birleştirme, hello yönetilmeyen tooyour yönetilen Azure dizin hello DNS etki alanı adını eklemek ve kullanıcıların kaynaklara eşlenmesini oluşturulur böylece kullanıcılar tooaccess Hizmetleri kesintisiz devam edebilirsiniz. Bazen, bir dış devralma da denir.

## <a name="what-gets-created-in-azure-active-directory"></a>Azure Active Directory'de oluşturulan?
#### <a name="directory"></a>Dizin
* Merhaba etki alanı için bir Azure Active Directory dizin oluşturulduğunda, etki alanı başına bir dizin.
* hiçbir genel yönetici Hello Azure AD dizinine sahip

#### <a name="users"></a>Kullanıcılar
* Kaydolan her kullanıcı için hello Azure AD dizininde bir kullanıcı nesnesi oluşturulur.
* Her kullanıcı nesnesi harici olarak işaretlenir.
* Her kullanıcı bunlar kaydolup erişim toohello hizmeti verilir.

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a>Ne ı talep Self Servis Azure AD olduğum bir etki alanı için dizin?
Self Servis Azure AD talep etki alanı doğrulama gerçekleştirerek dizin. Etki alanı doğrulama kendi hello etki alanı DNS kayıtları oluşturarak kanıtlar.

İki yolu toodo Azure AD dizini, DNS devralma vardır:

* İç devralma (yönetici yönetilmeyen Azure directory bulur ve yönetilen bir dizin tooturn istediği)
* Dış devralma (yönetici tooadd yeni bir etki alanı tootheir yönetilen Azure dizin çalışır)

Bir kullanıcı Self Servis kaydolma gerçekleştirilen veya yeni bir etki alanı tooan mevcut yönetilen dizin ekleme sonra yönetilmeyen bir dizin üzerinde aldığı bir etki alanı kendi doğrulanırken ilginizi çekebilir. Örneğin, contoso.com adlı bir etki alanına sahip ve tooadd contoso.co.uk veya contoso.uk adlı yeni bir etki alanı istiyor.

## <a name="what-is-domain-takeover"></a>Etki alanı devralma nedir?
Bu bölümde ele alınmaktadır nasıl toovalidate bir etki alanına sahip

### <a name="what-is-domain-validation-and-why-is-it-used"></a>Etki alanı doğrulama nedir ve neden kullanılır?
Bir dizin üzerinde sıralı tooperform işlemler Azure AD hello DNS etki alanı sahipliğini doğrulamanız gerektirir.  Doğrulama hello etki alanının, tooclaim başlangıç dizini ve ya da hello Self Servis tooa yönetilen dizin yükseltmek veya var olan içine birleştirme hello Self Servis directory directory yönetilen sağlar.

## <a name="examples-of-domain-validation"></a>Etki alanı doğrulama örnekleri
Bir dizinin DNS devralma iki yolu toodo vardır:

* İç devralma (örneğin, bir yönetici bir Self Servis, yönetilmeyen dizin bulur ve yönetilen bir dizin tooturn istediği)
* Dış devralma (örneğin, bir yönetici tooadd yeni bir etki alanı tooa yönetilen dizin çalışır)

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-toobe-a-managed-directory"></a>İç devralma - Self Servis, yönetilmeyen dizin toobe yönetilen bir dizin Yükselt
İç devralma yaptığınızda hello dizin yönetilmeyen dizin tooa yönetilen dizininden dönüştürülen. Merhaba DNS bölgesinde MX kaydı veya bir TXT kaydı oluşturduğunuz toocomplete DNS etki alanı adı doğrulaması, gerekir. Bu eylem:

* Merhaba etki alanına ait olduğunu doğrular
* Yönetilen hello dizin yapar
* Genel yönetici hello dizininin hello yapar

Merhaba Okul kullanıcıların self servis teklifleri için sürümüne kaydolduğunuzdan Körüğü üniversitenin BT yöneticilerinden bulur varsayalım. Hello kayıtlı gibi hello DNS sahibinin adı BellowsCollege.com, hello BT yöneticisi azure'da hello DNS adının sahipliği doğrulamak ve hello yönetilmeyen dizin üzerinde gerçekleştirin. Merhaba dizin sonra yönetilen bir dizin olur ve hello BT yöneticisi hello BellowsCollege.com dizin hello genel Yönetici rolüne atanır.

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a>Dış devralma - mevcut bir yönetilen dizin bir Self Servis dizin birleştirme
Bir dış devralma içinde yönetilen bir dizin zaten var ve tüm kullanıcılar ve directory yönetilen bir yönetilmeyen dizin toojoin gruplarından istediğiniz yerine dizinleri kendi iki ayrı.

Yönetilen bir dizin Yöneticisi, olarak bir etki alanına eklemek ve bu etki alanı toohave kendisiyle ilişkili bir yönetilmeyen dizini olur.

Örneğin, bir BT yöneticisiyseniz ve Contoso.com, kayıtlı tooyour kuruluşunuzun bir etki alanı adı zaten yönetilen bir dizin varsa varsayalım. Kuruluşunuzdaki kullanıcıların Self Servis oturum oluşturan bir sunum için e-posta etki alanı adını kullanarak gerçekleştirdiğiniz Bul user@contoso.co.uk, kuruluşunuzun sahip olduğu başka bir etki alanı adı değil. Bu kullanıcıların hesaplarını contoso.co.uk için yönetilmeyen bir dizindeki şu anda yok.

Mevcut yönetilen BT dizininize contoso.com hello yönetilmeyen dizin contoso.co.uk için birleştirmek için toomanage iki ayrı dizini, istemezsiniz.

Dış devralma aşağıdaki iç devralma aynı DNS doğrulama süreci hello.  Fark edilmesini: kullanıcıların ve hizmetlerin açmayla toohello BT olan yönetilen bir dizin.

#### <a name="whats-hello-impact-of-performing-an-external-takeover"></a>Bir dış devralma gerçekleştirmenin etkisini hello nedir?
Kullanıcıların tooaccess Hizmetleri kesintiye uğramadan devam edebilmek için bir dış devralma ile kullanıcıların kaynaklara eşlenmesini oluşturulur. Kişiler için RMS dahil olmak üzere birçok uygulama, kullanıcıların kaynaklara eşlenmesini hello iyi işlemek ve kullanıcıların tooaccess değişiklik olmadan bu hizmetlerin devam edebilirsiniz. Bir uygulama kullanıcıların kaynaklara eşlenmesini hello etkili bir şekilde işlemez, dış devralma zayıf bir deneyim açıkça engellenen tooprevent kullanıcılardan olması olabilir.

#### <a name="directory-takeover-support-by-service"></a>Dizin hizmeti tarafından devralma desteği
Şu anda aşağıdaki hello destek devralma Hizmetleri:

* RMS

Hizmetleri aşağıdaki hello yakında devralma destekleyecek:

* PowerBI

Merhaba aşağıdaki olmayan ve bir dış devralma sonra ek yönetim eylemi toomigrate kullanıcı verilerini gerektirir.

* SharePoint/OneDrive

## <a name="how-tooperform-a-dns-domain-name-takeover"></a>Nasıl tooperform bir DNS etki alanı adı devralma
Nasıl için birkaç seçeneğiniz tooperform bir etki alanı doğrulama (ve isterseniz bir devralma yapın):

1. Azure Yönetim Portalı

   Bir etki alanı ekleme yaparak bir devralma tetiklenir.  Merhaba etki alanı için bir dizin zaten varsa, bir dış devralma hello seçeneği tooperform sahip olacaksınız.

   İçinde toohello kimlik bilgilerinizi kullanarak Azure portalında oturum açın.  Tooyour varolan dizinine gidin ve ardından çok**etki alanı Ekle**.
2. Office 365

   Merhaba hello seçeneklerini kullanabilirsiniz [etki alanlarını yönetme](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) Office 365 toowork etki alanları ve DNS kayıtları sayfasında. Bkz: [Office 365'te etki alanınızı doğrulayın](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/).
3. Windows PowerShell

   Aşağıdaki adımları hello gerekli tooperform Windows PowerShell kullanarak bir doğrulama ' dir.

   | Adım | Cmdlet toouse |
   | --- | --- |
   | Bir kimlik bilgisi nesnesi oluşturun |Get-Credential |
   | TooAzure AD connect |Connect-MsolService |
   | etki alanlarının bir listesini alma |Get-MsolDomain |
   | Bir challenge oluşturma |Get-MsolDomainVerificationDns |
   | DNS kaydı oluşturma |DNS sunucunuzda bunu |
   | Merhaba sınama doğrulayın |Confirm-MsolEmailVerifiedDomain |

Örneğin:

1. TooAzure AD connect kullanılan toorespond toohello Self Servis sunumu olan hello kimlik bilgilerini kullanarak:

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. Etki alanlarının bir listesini alın:

    Get-MsolDomain
3. Ardından hello Get-MsolDomainVerificationDns cmdlet'i toocreate bir sınama çalıştırın:

    Get-MsolDomainVerificationDns – DomainName *your_domain_name* – modu DnsTxtRecord

    Örneğin:

    Get-MsolDomainVerificationDns – DomainName contoso.com – modu DnsTxtRecord
4. Bu komuttan döndürülen hello değerini (Merhaba Çekişme) kopyalayın.

    Örneğin:

    MS 32DD01B82C05D27151EA9AE93C5890787F0E65D9 =
5. Ortak DNS ad alanında hello önceki adımda kopyaladığınız hello değeri içeren bir DNS txt kaydı oluşturun.

    Hello adı bu kaydına hello üst etki alanının adını Merhaba, hello DNS rolü Windows Server kullanarak bu kaynak kaydı oluşturun, böylece hello kayıt adını boş bırakın ve yalnızca hello değeri hello metin kutusuna yapıştırın
6. Merhaba Onayla MsolDomain cmdlet tooverify hello sınama çalıştırın:

    Onayla MsolEmailVerifiedDomain - DomainName *your_domain_name*

    Örneğin:

    Onayla MsolEmailVerifiedDomain - DomainName contoso.com

Başarılı bir sınama toohello sormadan bir hata döndürür.

## <a name="how-do-i-control-self-service-settings"></a>Self Servis ayarları nasıl denetlerim?
Yöneticilere iki Self Servis denetimleri bugün sahip. Bunlar denetleyebilirsiniz:

* Olsun veya olmasın kullanıcılar e-posta yoluyla hello dizin birleştirebilirsiniz.
* Desteklemediğini kullanıcıların kendilerini uygulamalar ve hizmetler için lisans verebilirsiniz.

### <a name="how-can-i-control-these-capabilities"></a>Bu özelliklerin nasıl kontrol edebilir mi?
Bir yönetici bu Azure AD cmdlet Set-MsolCompanySettings parametreleri kullanarak şu olanakları yapılandırabilirsiniz:

* **AllowEmailVerifiedUsers** bir kullanıcı oluşturabilir veya yönetilmeyen bir directory katılım olup olmadığını denetler. Çok bu parametreyi ayarlarsanız $false, Hayır e-posta doğrulandı kullanıcıları hello dizin birleştirebilirsiniz.
* **AllowAdHocSubscriptions** tooperform Self Servis kaydolma kullanıcıların hello olanağını denetler. Bu parametreyi çok ayarlarsanız $false, hiçbir kullanıcı Self Servis kaydolma da gerçekleştirebilirsiniz.

### <a name="how-do-hello-controls-work-together"></a>Merhaba denetimleri birlikte nasıl çalışır?
Bu parametrelerden kullanılabilir Self Servis üzerinde daha kesin denetim birlikte toodefine kaydolun. Bu kullanıcılar Azure AD'de bir hesabınız zaten varsa komutu aşağıdaki hello kullanıcılar tooperform Self Servis kaydolma, ancak yalnızca örneğin, izin verir (diğer bir deyişle, oluşturulan bir e-posta doğrulandı hesap toobe gereken kullanıcıları Self Servis oturum yukarı gerçekleştiremezsiniz):

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

Merhaba aşağıdaki akış çizelgesi bu parametreler için tüm hello farklı birleşimler ve başlangıç dizini ve Self Servis kaydolma elde edilen koşullarını hello açıklanmaktadır.

![][1]

Daha fazla bilgi ve bu parametreleri toouse nasıl görürüm örnekleri [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).

## <a name="see-also"></a>Ayrıca Bkz.
* [Nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Cmdlet Başvurusu](/powershell/azure/get-started-azureps)
* [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
