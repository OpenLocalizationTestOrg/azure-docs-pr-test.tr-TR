---
title: "Active Directory Sertifika tabanlı kimlik doğrulaması - aaaAzure Başlarken | Microsoft Docs"
description: "Bilgi nasıl ortamınızdaki tooconfigure sertifika tabanlı kimlik doğrulaması"
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a>Azure Active Directory'de sertifika tabanlı kimlik doğrulaması kullanmaya başlama

Sertifika tabanlı kimlik doğrulaması Azure Active Directory tarafından Windows, Android veya iOS aygıtında bir istemci sertifikası ile Exchange online hesabınızı bağlanırken kimlik doğrulaması toobe sağlar: 

- Microsoft Outlook ve Microsoft Word gibi Office mobil uygulamaları   

- Exchange ActiveSync (EAS) istemcileri 

Bu özelliği yapılandıran hello gerek tooenter bir kullanıcı adı ve parola birleşimi belirli mail ve Microsoft Office uygulamaları, mobil Cihazınızda içine ortadan kaldırır. 

Bu konuda:

- Merhaba sizinle tooconfigure adımları ve sertifika tabanlı kimlik doğrulaması kullanıcıları için Office 365 Kurumsal, iş, eğitim kiracılar kullanma ve US Government planları sağlar. Bu özellik, Office 365 Çin'de, US Government savunma ve US Government Federal planlarda Önizleme'de kullanılabilir. 

- Zaten sahip olduğunuz varsayılmaktadır bir [ortak anahtar altyapısı (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) ve [AD FS](connect/active-directory-aadconnectfed-whatis.md) yapılandırılmış.    


## <a name="requirements"></a>Gereksinimler

tooconfigure sertifika tabanlı kimlik doğrulaması, hello aşağıdakilerin doğru olması gerekir:  

- Sertifika tabanlı kimlik doğrulaması (CBA), yalnızca tarayıcı uygulamalarında veya modern kimlik doğrulaması (ADAL) kullanarak yerel istemciler için federe ortamlar için desteklenir. Merhaba tek özel durum Exchange ActiveSync (EAS), Federal hem yönetilen hesapları için kullanılabilecek EXO için kullanılır. 

- Azure Active Directory'de Hello kök sertifika yetkilisini ve ara sertifika yetkilileri yapılandırılması gerekir.  

- Her sertifika yetkilisi URL Internet'e yönelik başvurulan bir sertifika iptal listesini (CRL) olması gerekir.  

- Azure Active Directory içinde yapılandırılan en az bir sertifika yetkilisine sahip olmanız gerekir. Hello ilgili adımları bulabilirsiniz [hello sertifika yetkililerini](#step-2-configure-the-certificate-authorities) bölümü.  

- Exchange ActiveSync istemcileri için Exchange online ya da hello asıl adı veya adresi hello konu alternatif adı alanında RFC822 adı değerini hello hello kullanıcının yönlendirilebilir e-posta hello istemci sertifikası olması gerekir. Azure Active Directory hello RFC822 değer toohello Proxy adresi özniteliği hello dizininde eşler.  

- İstemci Cihazınızı istemci sertifikaları veren erişim tooat en az bir sertifika yetkilisi olması gerekir.  

- İstemci kimlik doğrulaması için bir istemci sertifikası tooyour istemci verilmiş olması gerekir.  




## <a name="step-1-select-your-device-platform"></a>1. adım: cihaz platformunuz seçin

İlk adım olarak, verdiğiniz hakkında hello cihaz platformu için tooreview hello aşağıdakilere sahip olmanız gerekir:

- Merhaba Office mobil uygulamaları desteği 
- Merhaba belirli uygulama gereksinimleri  

Merhaba, cihaz platformları aşağıdaki hello için bilgi mevcut ilgili:

- [Android](active-directory-certificate-based-authentication-android.md)
- [iOS](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a>2. adım: hello sertifika yetkililerini yapılandırma 

tooconfigure aşağıdaki hello Azure Active Directory'de her sertifika yetkilisi, sertifika yetkilileri karşıya yükle: 

* Merhaba hello sertifikasının ortak kısmını *.cer* biçimi 
* Merhaba URL'leri hello burada Internet'e sertifika iptal listelerinin (CRL'ler) bulunur

bir sertifika yetkilisi için Hello şeması şu şekilde görünür: 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

Merhaba yapılandırma için hello kullanabilirsiniz [Azure Active Directory PowerShell sürüm 2](/powershell/azure/install-adv2?view=azureadps-2.0):  

1. Windows PowerShell'i yönetici ayrıcalıklarıyla başlatın. 
2. Hello Azure AD modülünü yükleyin. Tooinstall sürüm gereksinim [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) ya da daha yüksek.  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

İlk Yapılandırma adım olarak, Kiracı ile tooestablish bağlantı gerekir. Bağlantı tooyour Kiracı var. hemen gözden geçirebilir, eklemek, silmek ve dizininizde tanımlanan hello güvenilen sertifika yetkilileri değiştirin. 

### <a name="connect"></a>Bağlan

tooestablish kullanım hello kiracınızın bağlantı [Connect-Azuread'i](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:

    Connect-AzureAD 


### <a name="retrieve"></a>Alma 

dizininizde, tanımlanan tooretrieve hello güvenilen sertifika yetkilileri kullanmak hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet'i. 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a>Ekle

toocreate bir güvenilen sertifika yetkilisi kullanma hello [yeni AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet'i ve kümesi hello **crlDistributionPoint** öznitelik tooa doğru değeri: 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a>Kaldır

tooremove bir güvenilen sertifika yetkilisi kullanma hello [Kaldır AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a>Modfiy

toomodify bir güvenilen sertifika yetkilisi kullanma hello [kümesi AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a>3. adım: iptal yapılandırma

bir istemci sertifikası, Azure Active Directory toorevoke hello URL'lerden iptal listesini (CRL) sertifika yetkilisi bilgilerinin bir parçası yüklenen ve önbelleğe alır hello sertifika getirir. Merhaba son zaman damgası yayımlama (**geçerlilik tarihi** özelliği) CRL kullanılır hello içinde tooensure hello CRL hala geçerlidir. Merhaba CRL hello listesinin bir parçası olan düzenli aralıklarla başvurulan toorevoke erişim toocertificates ' dir.

(Örneğin bir kullanıcının bir cihazı kaybederse) daha hızlı iptali gerekiyorsa, hello kullanıcının hello yetkilendirme belirteci geçersiz hale. tooinvalidate, hello yetkilendirme belirteci, ayarlanmış hello **StsRefreshTokenValidFrom** Windows PowerShell kullanarak belirli bir kullanıcı için alan. Merhaba güncelleştirmelisiniz **StsRefreshTokenValidFrom** toorevoke erişim için istediğiniz her bir kullanıcı için alan.

Merhaba iptal ederse tooensure, hello ayarlamalısınız **geçerlilik tarihi** hello CRL tooa Date tarafından belirlenen hello değerden **StsRefreshTokenValidFrom** ve söz konusu hello sertifikanın olduğundan emin olun Merhaba CRL.

Güncelleştirme ve ayarlama hello tarafından hello yetkilendirme belirteci geçersiz hale getiriliyor adımları anahat hello sürecini izleyerek hello **StsRefreshTokenValidFrom** alan. 

**tooconfigure iptal:** 

1. Yönetici kimlik bilgileri toohello MSOL hizmetiyle Bağlan: 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. Bir kullanıcı için geçerli StsRefreshTokensValidFrom değerini Hello Al: 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. Merhaba kullanıcı eşit toohello geçerli zaman damgası için yeni bir StsRefreshTokensValidFrom değeri yapılandırın: 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

Başlangıç tarihi, Ayarla hello gelecekte olmalıdır. Başlangıç tarihi hello gelecekteki değilse hello **StsRefreshTokensValidFrom** özelliği ayarlı değil. Başlangıç tarihi hello gelecekteki ise **StsRefreshTokensValidFrom** toohello geçerli saati (kümesi MsolUser komutu tarafından belirtilen başlangıç tarihi değil) ayarlanır. 


## <a name="step-4-test-your-configuration"></a>4. adım: Test yapılandırmanızı

### <a name="testing-your-certificate"></a>Sertifikanızı test etme

İlk Yapılandırma sınaması toosign içinde çok denemeniz gerektiğini[Outlook Web Access](https://outlook.office365.com) veya [SharePoint Online](https://microsoft.sharepoint.com) kullanarak, **-cihazdır**.

Oturum açma işleminiz başarılı olursa, ardından bunu biliyor:

- sağlanan tooyour test cihazı Hello kullanıcı sertifikası kaldırıldı
- AD FS düzgün yapılandırılmış  


### <a name="testing-office-mobile-applications"></a>Office mobil uygulamalarını test etme

**tootest sertifika tabanlı kimlik doğrulamasını mobil Office uygulamanızda:** 

1. Test aygıtınızda Office mobil uygulaması (örneğin, OneDrive) yükleyin.
3. Merhaba uygulaması başlatın. 
4. Kullanıcı adınızı girin ve ardından toouse istediğiniz hello kullanıcı sertifika seçin. 

Başarıyla oturum açmanız. 

### <a name="testing-exchange-activesync-client-applications"></a>Exchange ActiveSync istemci uygulamalarını test etme

Sertifika tabanlı kimlik doğrulaması, hello istemci sertifikasını içeren bir EAS profili aracılığıyla Exchange ActiveSync (EAS) tooaccess kullanılabilir toohello uygulamanın olması gerekir. 

Merhaba EAS profili bilgisinden hello içermelidir:

- kimlik doğrulaması için kullanılan kullanıcı sertifika toobe hello 

- Merhaba EAS uç noktası (örneğin, outlook.office365.com)

EAS profili yapılandırılan ve mobil cihaz Yönetimi (MDM) Intune gibi ya da el ile Merhaba sertifika hello hello cihazda EAS profili yerleştirmekten hello kullanımı üzerinden hello cihazın yerleştirilir.  

### <a name="testing-eas-client-applications-on-android"></a>Android'de test EAS istemci uygulamaları

**tootest sertifika kimlik doğrulaması:**  

1. EAS profili yukarıdaki hello gereksinimleri karşılayan hello yapılandırın.  
2. Merhaba uygulaması açın ve posta eşitliyor doğrulayın. 

