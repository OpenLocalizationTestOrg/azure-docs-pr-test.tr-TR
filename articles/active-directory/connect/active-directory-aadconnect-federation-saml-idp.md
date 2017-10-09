---
title: "Azure AD Connect: SAML 2.0 kimlik sağlayıcısı için çoklu oturum açma kullanın | Microsoft Docs"
description: "Bu konu, çoklu oturum açma için SAML 2.0 uyumlu IDP kullanarak açıklar."
services: active-directory
author: billmath
manager: femila
ms.custom: it-pro
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f9653dc44fb284a9b3c1988f623c33f27ae148cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#  <a name="use-a-saml-20-identity-provider-idp-for-single-sign-on"></a>Çoklu oturum açma için SAML 2.0 kimlik sağlayıcısı (IDP) kullanın

Bu konu, bilgiler içerir hello güvenlik belirteci hizmeti (STS) tercih edilen olarak SAML 2.0 kullanımına uyumlu SP Lite profili kimlik sağlayıcısı dayalı / kimlik sağlayıcısı. Zaten bir kullanıcı dizini ve SAML 2.0 kullanarak erişilen şirket içi depolama parola olduğu bu yararlı olur. Bu olan bir kullanıcı dizini, oturum açma 365 tooOffice ve diğer Azure AD güvenli kaynaklar için kullanılabilir. SAML 2.0 SP-profili hello üzerinde yaygın olarak dayanır Lite Hello güvenlik onaylama işlemi biçimlendirme dili (SAML) federe kimlik standart tooprovide bir oturum açma ve öznitelik exchange framework kullanılır.

>[!NOTE]
>3. taraf için Azure AD ile kullanmak için test Idps hello listesini [Azure AD Federasyonu uyumluluk listesi](active-directory-aadconnect-federation-compatibility.md)

Microsoft Office 365 gibi bir Microsoft bulut hizmeti hello tümleştirilmesi olarak bu oturum açma deneyimini destekler, düzgün şekilde yapılandırılmış, SAML 2.0 ile IDP profiline dayalı. SAML 2.0 kimlik sağlayıcısı üçüncü taraf ürünleri olan ve bu nedenle Microsoft destek hello dağıtımı için yapılandırma, bunları ilgili en iyi uygulamaları sorunlarını giderme sağlamaz. Bir kez düzgün yapılandırıldığından hello tümleşme hello SAML 2.0 kimlik sağlayıcısı için uygun yapılandırma hello aşağıdaki daha ayrıntılı olarak açıklanan Microsoft bağlantı Çözümleyicisi aracını kullanarak test. SAML 2.0 SP-Lite profili tabanlı kimlik sağlayıcınızı hakkında daha fazla bilgi için onu sağlanan hello kuruluş isteyin.

>[!IMPORTANT]
>Bu, sınırlı sayıda istemciyle yalnızca bu senaryoda oturum açma SAML 2.0 kimlik sağlayıcısı ile kullanılabilir içerir:

>- Outlook Web Access ve SharePoint Online gibi Web tabanlı istemciler
- Temel kimlik doğrulaması ve IMAP, POP, Active Sync, MAPI, gibi desteklenen bir Exchange erişim yöntemi kullanan e-posta zengin istemcileri vb. (Merhaba uç noktasıdır dağıtılan gerekli toobe Gelişmiş istemci Protokolü) gibi:
    - Outlook 2013/Microsoft Outlook 2010/Outlook 2016, Apple iPhone (çeşitli iOS sürümleri)
    - Çeşitli Google Android cihazları
    - Windows Phone 7, Windows Phone 7,8 ve Windows Phone 8.0
    - Windows 8 posta istemcisi ve Windows 8.1 posta istemcisi
    - Windows 10 posta istemcisi

Diğer tüm istemcileri, bu senaryoda oturum açma, SAML 2.0 kimlik sağlayıcısı ile kullanılamaz. Örneğin, hello Lync 2010 masaüstü istemcisi için çoklu oturum açmayı yapılandırılmış, SAML 2.0 kimlik sağlayıcısı ile Merhaba hizmete mümkün toologin değil.

## <a name="azure-ad-saml-20-protocol-requirements"></a>Azure AD SAML 2.0 protokolü gereksinimleri
Bu konu, ayrıntılı gereksinimler hello iletişim kuralı ve ileti SAML 2.0 kimlik sağlayıcısı ile oturum açma Azure AD tooenable tooone toofederate ya da daha fazla Microsoft bulut hizmetlerine (örneğin, Office 365) uygulamalıdır biçimlendirme içerir. Bu senaryoda kullanılan bir Microsoft bulut hizmeti için Hello SAML 2.0 bağlı olan taraf (SP-STS) Azure AD ' dir.

Kimlik sağlayıcısı çıkış örnek izlemeleri mümkün olduğunca sağlanan benzer toohello olarak mesajlarının, SAML 2.0 olun önerilir. Ayrıca, mümkün olduğunda sağlanan hello Azure AD meta verilerden belirli öznitelik değerlerini kullanın. Çıktı iletilerinizi mutluluk olduktan sonra aşağıda açıklandığı gibi Microsoft bağlantı Çözümleyicisi'ni hello ile test edebilirsiniz.

Hello Azure AD meta verileri bu URL'den indirilebilir: [https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml](http://https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml).
Office 365 Çin özgü örneğini Çin kullanarak müşteriler hello için Federasyon uç noktası aşağıdaki hello kullanılmalıdır: [https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml](https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml).

## <a name="saml-protocol-requirements"></a>SAML protokolü gereksinimleri
Bu bölüm ayrıntıları nasıl hello istek ve yanıt iletisi çiftleridir sipariş toohelp, tooformat bir araya iletilerinizi doğru.

Azure AD, aşağıda listelenen bazı belirli gereksinimleri ile Merhaba SAML 2.0 SP Lite profili kullanan kimlik sağlayıcıları ile yapılandırılmış toowork olabilir. Otomatik ve el ile test birlikte Merhaba örnek SAML istek ve yanıt iletileri kullanan, tooachieve birlikte çalışabilirlik Azure AD ile çalışabilirsiniz.

## <a name="signature-block-requirements"></a>İmza bloğu gereksinimleri
SAML yanıtını Hello içinde ileti hello imza düğümü hello dijital imza selamlama iletisine kendisi için ilgili bilgiler içerir. Merhaba imza bloğunu hello gereksinimlerine sahiptir:

1. Merhaba onaylama düğüm imzalanmalıdır.
2.  Merhaba RSA sha1 algoritması DigestMethod hello olarak kullanılmalıdır. Diğer dijital imza algoritması kabul edilmedi.
   `<ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>`
3.  Merhaba XML belgesi de kaydolabilirsiniz. 
4.  Merhaba dönüştürme algoritması örnek aşağıdaki hello başlangıç değerleri aynı olması gerekir.`<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
       <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>`
9.  Merhaba SignatureMethod'a algoritması örnek aşağıdaki hello eşleşmesi gerekir:`<ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>`

## <a name="supported-bindings"></a>Desteklenen bağlamaları
Bağlamaları değil hello aktarım ilgili gerekli iletişimleri parametreleri. hello gereksinimleri aşağıdaki toohello bağlamaları Uygula

1. HTTPS gerekli hello Aktarım ' dir.
2.  Azure AD oturum açma sırasında belirteci gönderimi için HTTP POST gerektirir
3.  Azure AD hello oturum kapatma iletisi toohello kimlik sağlayıcısı için HTTP POST hello kimlik doğrulama isteği toohello kimlik sağlayıcısı ve yeniden yönlendirme için kullanır.

## <a name="required-attributes"></a>Gerekli öznitelikler
Bu tablo belirli öznitelikler için gereksinimleri hello SAML 2.0 iletisinde gösterir.
 
|Öznitelik|Açıklama|
| ----- | ----- |
|NameID|Bu onaylama Hello değerini gerekir olması hello hello Azure AD kullanıcının İmmutableıd aynıdır. Too64 alfa sayısal karakterler olabilir. Güvenli olmayan HTML karakterler kodlanmış olmalıdır, örneğin "+" karakter ".2B" gösterilir.|
|IDPEmail|Merhaba kullanıcı asıl adı (UPN) listelenen hello sahip bir öğe adı IDPEmail bu hello SAML yanıt hello kullanıcının UserPrincipalName (UPN) Azure AD/Office 365'te aynıdır. Merhaba UPN e-posta adresi biçimindedir. Windows Office 365 (Azure Active Directory) UPN değeri.|
|Veren|Gerekli toobe hello kimlik sağlayıcısı URI'sini budur. Merhaba veren hello örnek iletilerden yeniden kullanmamalısınız. Veren eşleşmelidir, Azure AD kiracılar hello birden çok üst düzey etki alanı varsa, etki alanı başına yapılandırılmış URI ayarı hello belirtildi.|

>[!IMPORTANT]
>Şu anda Azure AD destekleyen SAML 2.0:urn:oasis:names:tc:SAML:2.0:nameid NameID biçimi URI aşağıdaki hello-biçimi: kalıcı.

## <a name="sample-saml-request-and-response-messages"></a>Örnek SAML istek ve yanıt iletileri
Bir istek ve yanıt iletisi çifti hello oturum açma ileti değişimi için gösterilir.
Azure AD tooa örnek SAML 2.0 kimlik sağlayıcısı'ndan gönderilen bir örnek istek iletisi budur. Merhaba örnek SAML 2.0 kimlik sağlayıcısı Active Directory Federasyon Hizmetleri (AD FS) toouse SAML-P Protokolü yapılandırıldı. Birlikte çalışabilirlik sınaması diğer SAML 2.0 kimlik sağlayıcıları ile tamamlandı.

    `<samlp:AuthnRequest xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_7171b0b2-19f2-4ba2-8f94-24b5e56b7f1e" IssueInstant="2014-01-30T16:18:35Z" Version="2.0" AssertionConsumerServiceIndex="0" >
    <saml:Issuer>urn:federation:MicrosoftOnline</saml:Issuer>
    <samlp:NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
    </samlp:AuthnRequest>`

Merhaba örnek SAML 2.0 uyumlu kimlik sağlayıcısı tooAzure AD gönderilen bir örnek yanıt iletisi budur / Office 365.

    `<samlp:Response ID="_592c022f-e85e-4d23-b55b-9141c95cd2a5" Version="2.0" IssueInstant="2014-01-31T15:36:31.357Z" Destination="https://login.microsoftonline.com/login.srf" Consent="urn:oasis:names:tc:SAML:2.0:consent:unspecified" InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
    </samlp:Status>
    <Assertion ID="_7e3c1bcd-f180-4f78-83e1-7680920793aa" IssueInstant="2014-01-31T15:36:31.279Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
        <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
        <ds:Reference URI="#_7e3c1bcd-f180-4f78-83e1-7680920793aa">
          <ds:Transforms>
            <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
            <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
          </ds:Transforms>
          <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
          <ds:DigestValue>CBn/5YqbheaJP425c0pHva9PhNY=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
      <ds:SignatureValue>TciWMyHW2ZODrh/2xrvp5ggmcHBFEd9vrp6DYXp+hZWJzmXMmzwmwS8KNRJKy8H7XqBsdELA1Msqi8I3TmWdnoIRfM/ZAyUppo8suMu6Zw+boE32hoQRnX9EWN/f0vH6zA/YKTzrjca6JQ8gAV1ErwvRWDpyMcwdYCiWALv9ScbkAcebOE1s1JctZ5RBXggdZWrYi72X+I4i6WgyZcIGai/rZ4v2otoWAEHS0y1yh1qT7NDPpl/McDaTGkNU6C+8VfjD78DrUXEcAfKvPgKlKrOMZnD1lCGsViimGY+LSuIdY45MLmyaa5UT4KWph6dA==</ds:SignatureValue>
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
        <ds:X509Data>
          <ds:X509Certificate>MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyhBREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDTE1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9ybWVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/+3ZWxd9T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEMb2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcCAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvyJOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBySx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==</ds:X509Certificate>
        </ds:X509Data>
      </KeyInfo>
    </ds:Signature>
    <Subject>
      <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">ABCDEG1234567890</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" NotOnOrAfter="2014-01-31T15:41:31.357Z" Recipient="https://login.microsoftonline.com/login.srf" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2014-01-31T15:36:31.263Z" NotOnOrAfter="2014-01-31T16:36:31.263Z">
      <AudienceRestriction>
        <Audience>urn:federation:MicrosoftOnline</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="IDPEmail">
        <AttributeValue>administrator@contoso.com</AttributeValue>
      </Attribute>
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2014-01-31T15:36:30.200Z" SessionIndex="_7e3c1bcd-f180-4f78-83e1-7680920793aa">
      <AuthnContext>
        <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
    </Assertion>
    </samlp:Response>`

## <a name="configure-your-saml-20-compliant-identity-provider"></a>SAML 2.0 uyumlu kimlik sağlayıcısı yapılandırma
Bu konu, tooconfigure (Office 365 gibi), SAML 2.0 kimlik sağlayıcısı toofederate Azure AD tooenable tek oturum açma erişimini tooone veya daha fazla Microsoft bulut hizmetleri nasıl yönergeler içerir hello SAML 2.0 protokolü kullanarak. Merhaba SAML 2.0 bağlı olan taraf Bu senaryoda kullanılan bir Microsoft bulut hizmeti için Azure AD olur.

## <a name="add-azure-ad-metadata"></a>Azure AD meta verileri ekleme
SAML 2.0 kimlik sağlayıcısı hello Azure AD bağlı olan taraf hakkında tooadhere tooinformation gerekir. Azure AD https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml konumundaki meta verilerini yayımlar.

Her zaman en son Azure AD hello meta SAML 2.0 kimlik sağlayıcısı yapılandırırken içe olduğunu önerilir. Azure AD hello kimlik sağlayıcısından meta verileri okumaz unutmayın.

## <a name="add-azure-ad-as-a-relying-party"></a>Azure AD bağlı olan taraf Ekle
SAML 2.0 kimlik sağlayıcısı ve Azure AD arasındaki tooenable iletişimi var. Bu yapılandırma, belirli bir kimlik sağlayıcısı bağımlı olur ve bunun için toodocumentation başvurmalıdır. Genelde hello bağlı olan taraf kimliği toohello ayarlanan hello Azure AD meta verilerden hello Entityıd aynıdır.

>[!NOTE]
>SAML 2.0 kimlik sağlayıcısı sunucunuzda Hello saati eşitlenmiş tooan doğru zaman kaynağı olduğundan emin olun. Yanlış bir saatin, federe oturum açma bilgileri toofail neden olabilir.

## <a name="install-windows-powershell-for-sign-on-with-saml-20-identity-provider"></a>SAML 2.0 kimlik sağlayıcısı ile oturum açma için Windows PowerShell yükleme
Azure AD oturum açma ile kullanım için SAML 2.0 kimlik sağlayıcınız yapılandırdıktan sonra hello sonraki toodownload ve yükleme hello Azure Active Directory için Windows PowerShell modülü adımdır. Bir kez yüklendikten sonra bu cmdlet'leri tooconfigure Federasyon etki alanı Azure AD etki alanlarınızı kullanır.

Hello Azure Active Directory için Windows PowerShell modülü, Azure AD'de Kuruluş verilerinizde yönetmeye yönelik bir yüklemedir. Bu modül, PowerShell cmdlet'leri tooWindows kümesi yükler; Bu cmdlet tooset tek oturum açma erişimini tooAzure AD yukarı çalıştırın ve sırayla hello tooall bulut hizmetlerini abone olduğunuz. Toodownload ve yükleme cmdlet'lerini nasıl hello hakkında yönergeler için bkz: [http://technet.microsoft.com/library/jj151815.aspx](http://technet.microsoft.com/library/jj151815.aspx)

## <a name="set-up-a-trust-between-your-saml-identity-provider-and-azure-ad"></a>SAML kimlik sağlayıcısı ve Azure AD arasında güven oluşturma
Azure AD etki alanı üzerinde Federasyon yapılandırmadan önce özel bir etki alanı yapılandırılmış olması gerekir. Microsoft tarafından sağlanan hello varsayılan etki alanını birleştiremeyiz. Microsoft'tan Hello varsayılan etki alanı "onmicrosoft.com" ile sona erer.
Bir dizi cmdlet'leri hello Windows PowerShell komut satırı arabirimi tooadd çalıştırmadan veya etki alanları için çoklu oturum açma Dönüştür.

SAML 2.0 kimlik sağlayıcısı kullanarak toofederate aşağıdakilerden birini yapmalısınız istediğiniz her bir Azure Active Directory etki alanı bir tek oturum açma etki alanı veya dönüştürülmüş toobe tek bir oturum açma etki standart bir etki alanından eklenmesi. SAML 2.0 kimlik sağlayıcısı ve Azure AD arasında güven ekleme veya bir etki alanı dönüştürme ayarlar.

Merhaba aşağıdaki yordam, SAML 2.0 SP-Lite kullanarak bir var olan standart bir etki alanı tooa Federasyon etki alanını dönüştürme konusunda size yol gösterir. Etki alanınızı too2 saat bu adımı sonra kullanıcıları etkiler kesinti yaşayabilirsiniz unutmayın.

## <a name="configuring-a-domain-in-your-azure-ad-directory-for-federation"></a>Federasyon için Azure AD dizininizdeki bir etki alanını yapılandırma


1. Tooyour Azure AD dizini bir kiracı yönetici olarak bağlanın: bağlanmak MsolService.
2.  İstenen Office 365 etki alanı toouse Federasyon SAML 2.0 ile yapılandırın:`$dom = "contoso.com" $BrandName - "Sample SAML 2.0 IDP" $LogOnUrl = "https://WS2012R2-0.contoso.com/passiveLogon" $LogOffUrl = "https://WS2012R2-0.contoso.com/passiveLogOff" $ecpUrl = "https://WS2012R2-0.contoso.com/PAOS" $MyURI = "urn:uri:MySamlp2IDP" $MySigningCert = @" MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyh BREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDT E1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9yb WVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/kupQ VcjKuKLitVDbssFyqbDTjP7WRjlVMWAHBI3kgNT7oE362Gf2WMJFf1b0HcrsgLin7daRXpq4Qi6OA57 sW1YFMj3sqyuTP0eZV3S4+ZbDVob6amsZIdIwxaLP9Zfywg2bLsGnVldB0+XKedZwDbCLCVg+3ZWxd9 T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEM b2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcC AwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9 eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+ CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvy JOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBy Sx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==" "@ $uri = "http://WS2012R2-0.contoso.com/adfs/services/trust" $Protocol = "SAMLP" Set-MsolDomainAuthentication -DomainName $dom -FederationBrandName $dom -Authentication Federated -PassiveLogOnUri $MyURI -ActiveLogOnUri $ecpUrl -SigningCertificate $MySigningCert -IssuerUri $uri -LogOffUri $url -PreferredAuthenticationProtocol $Protocol` 

3.  Sertifika base64 kodlu dize IDP meta veri dosyanızdan imzalama hello elde edebilirsiniz. Bu konum örneği sağlanmış olan ancak biraz uygulamanız göre farklılık gösterebilir.

    `<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol"> <KeyDescriptor use="signing"> <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#"> <X509Data> <X509Certificate>MIIC5jCCAc6gAwIBAgIQLnaxUPzay6ZJsC8HVv/QfTANBgkqhkiG9w0BAQsFADAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwHhcNMTMxMTA0MTgxMzMyWhcNMTQxMTA0MTgxMzMyWjAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCwMdVLTr5YTSRp+ccbSpuuFeXMfABD9mVCi2wtkRwC30TIyPdORz642MkurdxdPCWjwgJ0HW6TvXwcO9afH3OC5V//wEGDoNcI8PV4enCzTYFe/h//w51uqyv48Fbb3lEXs+aVl8155OAj2sO9IX64OJWKey82GQWK3g7LfhWWpp17j5bKpSd9DBH5pvrV+Q1ESU3mx71TEOvikHGCZYitEPywNeVMLRKrevdWI3FAhFjcCSO6nWDiMqCqiTDYOURXIcHVYTSof1YotkJ4tG6mP5Kpjzd4VQvnR7Pjb47nhIYG6iZ3mR1F85Ns9+hBWukQWNN2hcD/uGdPXhpdMVpBAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAK7h7jF7wPzhZ1dPl4e+XMAr8I7TNbhgEU3+oxKyW/IioQbvZVw1mYVCbGq9Rsw4KE06eSMybqHln3w5EeBbLS0MEkApqHY+p68iRpguqa+W7UHKXXQVgPMCpqxMFKonX6VlSQOR64FgpBme2uG+LJ8reTgypEKspQIN0WvtPWmiq4zAwBp08hAacgv868c0MM4WbOYU0rzMIR6Q+ceGVRImlCwZ5b7XKp4mJZ9hlaRjeuyVrDuzBkzROSurX1OXoci08yJvhbtiBJLf3uPOJHrhjKRwIt2TnzS9ElgFZlJiDIA26Athe73n43CT0af2IG6yC7e6sK4L3NEXJrwwUZk=</X509Certificate> </X509Data> </KeyInfo> </KeyDescriptor>` 

"Set-MsolDomainAuthentication" hakkında daha fazla bilgi için bkz: [http://technet.microsoft.com/library/dn194112.aspx](http://technet.microsoft.com/library/dn194112.aspx).

>[!NOTE]
>Kullanım çalıştırmanız gerekir "$ecpUrl"https://WS2012R2-0.contoso.com/PAOS"=" Kimlik sağlayıcısı için ECP uzantı ayarlarsanız. Exchange Online istemciler, Outlook Web uygulaması (OWA) hariç Bel etkin uç noktası bir POST tabanlı. SAML 2.0 STS bir etkin uç noktası bir etkin uç noktası benzer tooShibboleth's ECP uygulaması uyguluyorsa hello Exchange Online hizmeti ile bu zengin istemciler toointeract mümkün olabilir.

Federasyon yapılandırıldıktan sonra geri çok "Federasyon olmayan" (veya "yönetilen"), ancak bu değişikliği tootwo saatleri toocomplete alır ve bulut için yeni rastgele parolaları atama tooeach oturum açma kullanıcı tabanlı gerektirir geçiş yapabilirsiniz. Yeniden geçiş yapmayı çok "yönetilen" olabilir ayarlarınızda hata bazı senaryolar tooreset gerekli. Etki alanı dönüştürme hakkında daha fazla bilgi için bkz: [http://msdn.microsoft.com/library/windowsazure/dn194122.aspx](http://msdn.microsoft.com/library/windowsazure/dn194122.aspx).

## <a name="provision-user-principals-tooazure-ad--office-365"></a>Kullanıcı ilkeleri tooAzure AD sağlamak / Office 365
Kullanıcıların tooOffice 365 kimlik doğrulama gerçekleştirmeden önce Azure AD toohello onaylama hello SAML 2.0 içinde karşılık gelen sorumluları talep kullanıcıyla hazırlamanız gerekir. Bu kullanıcı ilkeleri tooAzure AD önceden bilinmiyorsa sonra bunlar federe oturum açma için kullanılamaz. Azure AD Connect veya Windows PowerShell kullanılan tooprovision kullanıcı ilkeleri olabilir.

Azure AD Connect kullanılan tooprovision sorumluları tooyour Azure AD dizininizi hello şirket içi Active Directory etki alanlarında olabilir. Daha ayrıntılı bilgi için bkz: [şirket içi dizinlerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).

Windows PowerShell de yeni kullanıcılar tooAzure AD ekleme kullanılan tooautomate olabilir ve hello şirket içi dizininden toosynchronize değiştirir. toouse hello hello indirmesi Windows PowerShell cmdlet'leri [Azure Active Directory modülleri](https://docs.microsoft.com/powershell/azure/install-adv2?view=azureadps-2.0).

Bu yordam gösterir nasıl tooadd tek kullanıcı tooAzure AD.


1. Tooyour Azure AD dizini bir kiracı yönetici olarak bağlanın: bağlanmak MsolService.
2.  Yeni bir kullanıcı asıl oluşturun:` New-MsolUser
        -UserPrincipalName elwoodf1@contoso.com
        -ImmutableId ABCDEFG1234567890
        -DisplayName "Elwood Folk"
        -FirstName Elwood 
        -LastName Folk 
        -AlternateEmailAddresses "Elwood.Folk@contoso.com" 
        -LicenseAssignment "samlp2test:ENTERPRISEPACK" 
        -UsageLocation "US" ` 

"Yeni-MsolUser" kullanıma, hakkında daha fazla bilgi için [http://technet.microsoft.com/library/dn194096.aspx](http://technet.microsoft.com/library/dn194096.aspx)

>[!NOTE]
>Merhaba "UserPrinciplName" değeri "IDPEmail" için SAML 2.0 talep ve Başlangıç "değeri"NameID"değerinizi gönderilen hello değeriyle eşleşmelidir İmmutableıd" göndereceğiniz hello değeriyle eşleşmelidir.

## <a name="verify-single-sign-on-with-your-saml-20-idp"></a>Çoklu oturum açma ile SAML 2.0 IDP doğrulayın
Merhaba yönetici olarak doğrulayın ve çoklu oturum açma (Ayrıca çağrılan Kimlik Federasyonu) yönetmek önce hello bilgileri gözden geçirin ve çoklu oturum açma, SAML 2.0 SP-Lite tabanlı kimlik sağlayıcısı ile yedekleme makaleleri tooset aşağıdaki hello hello adımları gerçekleştirin:


1.  Hello Azure AD SAML 2.0 protokolü gereksinimleri gözden geçirdikten
2.  SAML 2.0 kimlik sağlayıcısı yapılandırmış olduğunuz
3.  SAML 2.0 kimlik sağlayıcısı ile çoklu oturum açma için Windows PowerShell yükleme
4.  SAML 2.0 kimlik sağlayıcısı ve Azure AD arasında güven oluşturma
5.  Bir bilinen test kullanıcı asıl tooAzure Active Directory (Office 365), Windows PowerShell veya Azure AD Connect ile sağlandı.
6.  Dizin eşitleme kullanarak yapılandırma [Azure AD Connect](active-directory-aadconnect.md).

Çoklu oturum açma SAML 2.0 SP-tabanlı Lite kimliğinizi sağlayıcısı ile kurduktan sonra düzgün çalıştığını doğrulamanız gerekir.

>[!NOTE]
>Eklenirken bir yerine bir etki alanı dönüştürülürse too24 saatleri tooset çoklu oturum açma Yukarı Yukarı sürebilir.
Çoklu oturum açmayı doğrulamak için önce Active Directory eşitleme kurulumunun tamamlanması, dizinlerinizi eşitleyin ve eşitlenmiş kullanıcıları etkinleştirme gerekir.

### <a name="use-hello-tool-tooverify-that-single-sign-on-has-been-set-up-correctly"></a>Çoklu oturum açmayı kullanmak hello aracı tooverify doğru olarak ayarlanmış
tooverify, çoklu oturum açma doğru olarak ayarlanmış olan, şirket kimlik bilgilerinizle toohello bulut hizmetindeki mümkün toosign olduğunu yordamı tooconfirm aşağıdaki hello gerçekleştirebilirsiniz.

Microsoft bir aracı sağlanan dayalı kimlik sağlayıcısı, SAML 2.0 tootest kullanabilirsiniz. Merhaba çalıştırmadan önce kimlik sağlayıcınız ile bir Azure AD Kiracı toofederate yapılandırılmış gerekir aracı test edin.

>[!NOTE]
>Merhaba bağlantı Çözümleyicisi'ni Internet Explorer 10 veya üstünü gerektirir.



1. İndirme hello bağlantı Çözümleyicisi'ni, [https://testconnectivity.microsoft.com/?tabid=Client](https://testconnectivity.microsoft.com/?tabid=Client).
2.  Şimdi Yükle toobegin indirme ve hello aracı Yükleme'yi tıklatın.
3.  "I Office 365, Azure veya Azure Active Directory kullanan diğer hizmetler ile Federasyon ayarlayamazsınız" seçin.
4.  Merhaba aracı yüklenmiş ve çalışıyor olduğundan sonra hello bağlantı tanılama penceresinde göreceksiniz. Merhaba aracı Federasyon bağlantınızı test aracılığıyla adım.
5.  Merhaba bağlantı Çözümleyicisi'ni, toologon, SAML 2.0 IDP açın, test ettiğiniz hello kullanıcı asıl adı için hello kimlik bilgilerini girin: ![SAML](media/active-directory-aadconnect-federation-saml-idp/saml1.png)
6.  Federasyon Merhaba oturum açma penceresi SAML 2.0 kimlik sağlayıcınız ile Federasyon yapılandırılmış toobe olan hello Azure AD kiracısı için bir hesap adı ve parola girmelisiniz sınayın. Merhaba aracı toosign bileşenini bu kimlik bilgilerini kullanarak çalışır ve hello oturum açma girişimi sırasında gerçekleştirilen testleri ayrıntılı sonuçlarını çıkış olarak sağlanacaktır.
![SAML](media/active-directory-aadconnect-federation-saml-idp/saml2.png)
7. Bu pencere sınama başarısız sonucunu gösterir. Ayrıntılı sonuçları gerçekleştirildiği her test hello sonuçlarıyla ilgili bilgileri gösterir İnceleme tıklayarak. Merhaba sonuçları toodisk sipariş tooshare kaydedebilirsiniz bunları.
 
>[!NOTE]
>Merhaba bağlantı Çözümleyicisi'ni da etkin hello WS * kullanarak Federasyon test-tabanlı ve ECP/PAOS protokoller. Bunlar kullanmıyorsanız aşağıdaki hata hello göz ardı edebilirsiniz: Test hello oturum açma, kimlik sağlayıcısının etkin Federasyon endpoint kullanarak etkin akış.

### <a name="manually-verify-that-single-sign-on-has-been-set-up-correctly"></a>Bu çoklu oturum açma doğru olarak ayarlanmış olan el ile doğrulayın
El ile doğrulama SAML 2.0 kimlik sağlayıcısı, birçok senaryoda düzgün çalıştığını tooensure yapabileceğiniz ek adımları sağlar.
Çoklu oturum açmayı tooverify doğru olarak ayarlanmış, hello aşağıdaki tam adımlar:


1. Etki alanına katılmış bir bilgisayar üzerinde tooyour bulut Hizmeti'nde aynı oturum açma için şirket kimlik bilgilerinizi kullanın adınız hello kullanarak oturum açın.
2.  Merhaba parola kutusunun içine tıklayın. Çoklu oturum açma ayarlandığından, hello parola kutusu gölgeli olacaktır ve iletiden hello görürsünüz: "konumunda ın gerekli toosign sunulmuştur <your company>."
3.  Merhaba tıklatın adresinde oturum açın <your company> bağlantı. İçinde mümkün toosign varsa, ardından çoklu oturum açma ayarlanmış olması.

## <a name="next-steps"></a>Sonraki Adımlar


- [Active Directory Federasyon Hizmetleri Yönetimi ve Azure AD Connect ile özelleştirme](active-directory-aadconnect-federation-management.md)
- [Azure AD federasyonu uyumluluk listesi](active-directory-aadconnect-federation-compatibility.md)
- [Azure AD Connect özel yüklemesi](active-directory-aadconnect-get-started-custom.md)
