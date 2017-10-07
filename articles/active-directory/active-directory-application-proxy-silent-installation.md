---
title: "aaaSilent Azure AD uygulama ara sunucusu Bağlayıcısı yükleme | Microsoft Docs"
description: "Nasıl tooperform Azure AD uygulama ara sunucusu Bağlayıcısı tooprovide güvenli uzaktan erişim tooyour katılımsız yüklemesi uygulamaları şirket içi kapsar."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3aa1c7f2-fb2a-4693-abd5-95bb53700cbb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ce796ff45a65ba7d5f0f63c02085bdc6af494548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a>Hello Azure AD uygulama ara sunucusu Bağlayıcısı gerek kalmadan sessiz yükleme
Bir yükleme komut dosyası toomultiple Windows sunucuları veya etkin kullanıcı arabirimi yok tooWindows sunucuları toobe mümkün toosend istiyor. Bu konu, katılımsız yükleme ve kaydetme, Azure AD uygulama ara sunucusu Bağlayıcısı etkinleştiren bir Windows PowerShell betik oluşturmanıza yardımcı olur.

Bu özellik, aşağıdakileri yapmak istediğinizde yararlıdır:

* Merhaba bağlayıcı makinelere RDP toohello makine yapamadığında veya hiç kullanıcı Arabirimi katman ile yükleyin.
* Yükleme ve aynı anda birçok bağlayıcılar kaydedin.
* Merhaba Bağlayıcısı yükleme ve başka bir yordamının parçası olarak kayıt tümleştirin.
* Merhaba bağlayıcı BITS içerir ancak kaydedilmemiş standart sunucu görüntüsünü oluşturun.

Uygulama proxy'si hello bağlayıcı ağınızdaki adlı ince bir Windows Server hizmetini yükleyerek çalışır. Merhaba uygulama Proxy Bağlayıcısı toowork için bir genel yönetici ve parola kullanarak Azure AD diziniyle kayıtlı toobe içeriyor. Normalde bu bilgileri açılan iletişim kutusunda Bağlayıcısı yüklemesi sırasında girilir. Ancak, Windows PowerShell toocreate bir kimlik bilgisi nesnesi tooenter kayıt bilgilerinizi kullanabilirsiniz. Veya, kendi belirteç oluşturmak ve tooenter kullanmanızı kayıt bilgilerinizi.

## <a name="install-hello-connector"></a>Merhaba bağlayıcısını yükleme
Merhaba bağlayıcı MSI'lerini hello bağlayıcı gibi kaydettirmeden yükleyin:

1. Bir komut istemi açın.
2. Hangi hello, sessiz yükleme /q anlamına gelir komutu aşağıdaki hello Çalıştır - hello yükleme tooaccept hello son kullanıcı lisans sözleşmesi ister değil.
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a>Merhaba bağlayıcı Azure AD ile kaydetme
Tooregister hello bağlayıcı kullanabileceğiniz iki yöntem vardır:

* Bir Windows PowerShell kimlik bilgisi nesnesi kullanarak hello bağlayıcı kaydetme
* Çevrimdışı oluşturan bir belirteç kullanarak hello bağlayıcı kaydetme

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a>Bir Windows PowerShell kimlik bilgisi nesnesi kullanarak hello bağlayıcı kaydetme
1. Şu komutu çalıştırarak Hello Windows PowerShell kimlik bilgilerini nesnesi oluşturun. Değiştir  *\<kullanıcıadı\>*  ve  *\<parola\>*  hello kullanıcı adı ve parola dizininiz için:
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. Çok Git**C:\Program Files\Microsoft AAD uygulama Proxy Bağlayıcısı** ve kimlik bilgileri, oluşturduğunuz nesne hello PowerShell kullanarak hello komut dosyasını çalıştırın. Değiştir *$cred* hello PowerShell hello adı ile oluşturduğunuz kimlik bilgilerini nesnesi:
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a>Çevrimdışı oluşturan bir belirteç kullanarak hello bağlayıcı kaydetme
1. Merhaba kod parçacığında Hello değerleri kullanarak hello Authenticationcontext'i sınıfını kullanarak çevrimdışı bir belirteç oluşturur:

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// hello AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// hello application ID of hello connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// hello reply address of hello connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// hello AppIdUri of hello registration service in AAD
        /// </summary>
        static readonly Uri RegistrationServiceAppIdUri = new Uri("https://proxy.cloudwebappproxy.net/registerapp");

        #endregion

        #region private members
        private string token;
        private string tenantID;
        #endregion

        public void GetAuthenticationToken()
        {
            AuthenticationContext authContext = new AuthenticationContext(AadAuthenticationEndpoint.AbsoluteUri);

            AuthenticationResult authResult = authContext.AcquireToken(RegistrationServiceAppIdUri.AbsoluteUri,
                ConnectorAppId,
                ConnectorRedirectAddress,
                PromptBehavior.Always);

            if (authResult == null || string.IsNullOrEmpty(authResult.AccessToken) || string.IsNullOrEmpty(authResult.TenantId))
            {
                Trace.TraceError("Authentication result, token or tenant id returned are null");
                throw new InvalidOperationException("Authentication result, token or tenant id returned are null");
            }

            token = authResult.AccessToken;
            tenantID = authResult.TenantId;
        }


2. Merhaba belirteci olduktan sonra hello belirteci kullanarak bir SecureString oluşturun:

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. Windows PowerShell komutunu aşağıdaki, değiştirme çalıştırma hello \<GUID Kiracı\> , dizin kimliği:

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a>Sonraki adımlar 
* [Kendi etki alanı adınızı kullanarak uygulama yayımlama](active-directory-application-proxy-custom-domains.md)
* [Çoklu oturum açmayı etkinleştirme](active-directory-application-proxy-sso-using-kcd.md)
* [Uygulama Ara sunucusu ile ilgili sorunları giderme](active-directory-application-proxy-troubleshoot.md)


