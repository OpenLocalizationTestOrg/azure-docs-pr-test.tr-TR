---
title: "aaaUse Azure anahtar Kasası'nı bir Web uygulaması | Microsoft Docs"
description: "Bu öğretici toohelp nasıl toouse Azure anahtar kasası bir web uygulamasından öğrenin kullanın."
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a>Bir Web uygulamasından Azure anahtar kasası kullanın
## <a name="introduction"></a>Giriş
Bu öğretici toohelp toouse Azure anahtar kasası nasıl Azure web uygulamasından öğrenin kullanın. Bu, böylece web uygulamanızda kullanılabilir gizli bir Azure anahtar Kasası'erişme hello işlemi açıklanmaktadır.

**Zaman toocomplete tahmini:** 15 dakika

Azure Anahtar Kasası genel bakış bilgileri için bkz. [Azure Anahtar Kasası nedir?](key-vault-whatis.md)

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğreticiyi izleyerek hello olması gerekir:

* Azure anahtar Kasası'nda bir URI tooa gizlilik
* Azure Active Directory ile erişim tooyour anahtar kasası sahip kayıtlı bir istemci kimliği ve bir web uygulaması için bir istemci parolası
* Bir web uygulamasıdır. Biz gösteren bir Web uygulaması olarak azure'da dağıtılan bir ASP.NET MVC uygulaması için başlangıç adımları.

> [!NOTE]
> Listelenen hello adımları tamamladınız gereklidir [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md) , böylece Bu öğretici için URI tooa gizli ve hello istemci kimliği ve istemci parolası için bir web uygulaması hello.
> 
> 

Merhaba anahtar kasası erişecek Merhaba web uygulaması, Azure Active Directory'de kayıtlı ve erişim tooyour anahtar kasası belirtilen hello bir ' dir. Merhaba durum bu değilse, tooRegister hello Başlarken Öğreticisi uygulamada geri dönün ve listelenen hello adımları yineleyin.

Bu öğretici, Azure üzerinde web uygulamaları oluşturmak, hello temellerini anlamak web geliştiricileri için tasarlanmıştır. Azure Web Apps hakkında daha fazla bilgi için bkz: [Web Apps'e genel bakış](../app-service-web/app-service-web-overview.md).

## <a id="packages"></a>Nuget paketleri ekleme
Yüklü toohave web uygulamanız gereken iki paket vardır.

* Active Directory Authentication Library - Azure Active Directory ile etkileşim ve kullanıcı kimliği yönetmek için yöntemler içerir
* Azure anahtar kasası Library - Azure anahtar kasası ile etkileşim için yöntemler içerir

Bu paketleri her ikisi de kullanılarak yüklenebilir hello Install-Package komutunu kullanarak Paket Yöneticisi konsolu hello.

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <a id="webconfig"></a>Web.Config değiştirme
Toobe eklenen toohello web.config dosyasında aşağıdaki gibi gereken üç uygulama ayarlarını vardır.

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


Uygulamanızı Azure Web uygulaması olarak toohost yapmayacağınız, hello gerçek ClientID, istemci gizli anahtarı ve gizli anahtar URI'sini değerleri toohello web.config eklemeniz gerekir. Aksi takdirde hello Azure Portal için ek bir güvenlik düzeyi içinde hello gerçek değerler biz alacağınız çünkü bu kukla değerleri bırakın.

## <a id="gettoken"></a>Yöntem tooGet bir erişim belirteci Ekle
Sipariş toouse hello anahtar kasası API'sini bir erişim belirteci gerekir. Merhaba anahtar kasası istemci işleme toohello anahtar kasası API ancak gereksinim toosupply çağrıları hello erişim belirteci alan bir işlev ile.  

Merhaba kod tooget bir erişim belirteci Azure Active Directory'den aşağıdadır. Bu kodu, uygulamanızda herhangi bir yere gidebilirsiniz. I tooadd bir yardımcı programları veya EncryptionHelper sınıfı gibi.  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> Bir istemci kimliği ve istemci parolası hello en kolay yolu tooauthenticate Azure AD uygulaması kullanmaktır. Ve web uygulamanızı kullanarak ayrılması görevlerini ve anahtar yönetimi üzerinde daha fazla denetim sağlar. Ancak, yapılandırma ayarlarınızı tooprotect istediğiniz hello gizli koyma olarak olarak riskli olabilecek bazı yapılandırma ayarlarınızın hello gizli koyma kullanır. Azure AD uygulaması toouse bir istemci kimliği ve istemci kimliği ve istemci parolası tooauthenticate yerine sertifikanın nasıl hello üzerinde bir tartışma için aşağıya bakın.
> 
> 

## <a id="appstart"></a>Uygulama başlangıç Hello gizli alma
Şimdi biz toocall hello anahtar kasası API kod ve hello gizli almak. toouse ihtiyacınız önce çağırılır sürece hello aşağıdaki kodu her yerden yerleştirilebileceği onu. I bu kodu hello uygulama başlatma olayı hello Global.asax başlangıç kez çalışır ve gizli hello uygulama için kullanılabilir hale getirir hello koymak.

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <a id="portalsettings"></a>Uygulama ayarları hello Azure portalı (isteğe bağlı) Ekle
Bir Azure Web uygulaması varsa hello Azure Portal hello gerçek değerler hello AppSettings için artık ekleyebilirsiniz. Bunu yaparak hello gerçek değerler hello web.config dosyasında olmaz ancak ayrı bir erişim denetimi özelliklerinden sahip olduğu Portal hello korumalı. Bu değerler, web.config dosyanızda girdiğiniz hello değerleri için değiştirilecektir. Merhaba adları olan Merhaba, aynı olduğundan emin olun.

![Azure Portalı'nda görüntülenen uygulama ayarları][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a>Bir istemci parolası yerine bir sertifika ile kimlik doğrulaması
Başka bir şekilde tooauthenticate Azure AD uygulaması bir istemci kimliği ve bir sertifika bir istemci kimliği ve istemci parolası yerine kullanmaktır. Aşağıdaki adımları toouse Azure Web uygulaması sertifikada hello:

1. Alma veya bir sertifika oluşturun
2. Merhaba sertifika bir Azure AD uygulama ile ilişkilendirme
3. Kod tooyour Web uygulaması toouse hello sertifika Ekle
4. Sertifika tooyour Web uygulaması Ekle

**Alma veya bir sertifika oluşturmak** bizim amacıyla bir test sertifikası yapacağız. Birkaç sertifika bir geliştirici komut istemi toocreate kullanabileceğiniz komutlar şunlardır. Oluşturulan hello sertifika dosyaları istediğiniz dizin toowhere değiştirin.  Ayrıca, başlangıç ve bitiş tarihi başlangıç sertifikanın hello hello geçerli tarih artı 1 yıl kullanın.

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

Merhaba bitiş tarihi ve hello .pfx hello parolasını not edin (Bu örnekte: 07/31/2016 ve test123). Bunları aşağıdaki gerekir.

Bir test sertifikası oluşturma hakkında daha fazla bilgi için bkz: [nasıl yapılır: bilgisayarınızı kendi Test sertifikası oluşturma](https://msdn.microsoft.com/library/ff699202.aspx)

**Azure AD uygulaması ile ilişkilendirme hello sertifika** bir sertifikanız, tooassociate gereken Azure AD uygulaması ile. Şu anda hello Azure portalı, bu iş akışı desteklemiyor; Bu PowerShell aracılığıyla tamamlanabilir. Aşağıdaki komutları tooassoicate hello Merhaba Azure AD uygulaması sertifikayla hello çalıştırın:

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

Bu komutları çalıştırdıktan sonra Azure AD'de Merhaba uygulaması görebilirsiniz. Arama yaparken, "Şirketimin sahip olduğu uygulamalar" seçin "uygulamaları Şirketim kullandığından yerine" Merhaba arama iletişim kutusunda emin olun.

Azure AD uygulama nesneleri ve ServicePrincipal nesneleri hakkında daha fazla toolearn bakın [uygulama ve hizmet sorumlusu nesneleri](../active-directory/active-directory-application-objects.md)

**Kod tooyour Web uygulaması toouse hello sertifika Ekle** artık kod tooyour Web uygulaması tooaccess hello cert ve kimlik doğrulaması için kullanmak ekleyeceğiz.

İlk kod tooaccess hello cert yoktur.

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


Bu hello StoreLocation LocalMachine yerine Currentuser'a olduğuna dikkat edin. Bir test sertifikası kullanıyoruz yöntemi ve biz 'false' toohello sağladığı bulunamıyor.

Sonraki hello CertificateHelper kullanır ve kimlik doğrulaması için gerekli olan bir ClientAssertionCertificate oluşturan kodudur.

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


Merhaba yeni kod tooget hello erişim belirteci aşağıdadır. Merhaba GetToken yöntemi yukarıdaki değiştirir. I kolaylık sağlamak için farklı bir ad verilen.

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

I tüm bu kod, kullanım kolaylığı için my Web uygulaması projenin yardımcı programları sınıfı yerleştirin.

Merhaba son kod hello uygulama_başlatma yönteminin değişikliktir. İlk toocall hello GetCert() yöntemi tooload hello ClientAssertionCertificate gerekir. Ve biz Biz yeni KeyVaultClient oluştururken sağladığınız hello geri çağırma yöntemini değiştirin. Bu size yukarıda vardı hello kod değiştirir unutmayın.

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


**Web uygulaması hello Azure Portal aracılığıyla bir sertifika tooyour ekleme** sertifika tooyour Web uygulaması ekleme olan basit bir işlemdir. İlk olarak, toohello Azure Portal gidin ve tooyour Web uygulamasına gidin. Hello ayarları dikey penceresinde, Web uygulamanız için "özel etki alanları ve SSL" Merhaba giriş'i tıklatın. Merhaba üzerinde açılan dikey mümkün tooupload hello KVWebApp.pfx yukarıda oluşturduğunuz sertifika olması, hello pfx hello parolasını anımsamasını emin olun.

![Hello Azure Portal sertifika tooa Web uygulaması ekleme][2]

Merhaba toodo gereken son tooadd bir uygulama ayarı tooyour hello adını Web sitesi olan bir Web uygulaması şeydir\_yük\_SERTİFİKALARI ve değerini *. Bu, tüm sertifikaların yüklü olduğundan güvence altına alır. Tooload yalnızca hello sertifikalar istediyseniz karşıya yüklediğiniz sonra virgülle ayrılmış bir liste kendi parmak izleri girebilirsiniz.

Sertifika tooa Web uygulaması ekleme hakkında daha fazla toolearn bakın [kullanarak sertifikaları Azure Web siteleri uygulamalarında](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)

**Sertifika tooKey kasası gizlilik olarak ekleme** , sertifika toohello Web App service doğrudan yüklemek yerine, anahtar kasası gizli olarak depolayın ve buradan dağıtın. Bu blog gönderisine aşağıdaki hello özetlenen iki adımlı bir işlemdir [anahtar kasası aracılığıyla Azure Web uygulaması sertifikası dağıtma](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)

## <a id="next"></a>Sonraki adımlar
Programlama başvuruları için bkz: [Azure anahtar kasası C# istemci API Başvurusu](https://msdn.microsoft.com/library/azure/dn903628.aspx).

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
