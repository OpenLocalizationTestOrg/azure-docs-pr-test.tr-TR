---
title: "Bir Web uygulamasından Azure anahtar kasası kullanan | Microsoft Docs"
description: "Bir web uygulamasından Azure anahtar kasası kullanmayı öğrenmenize yardımcı olmak için bu öğreticiyi kullanın."
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
ms.openlocfilehash: d095bcfe37baefa90cf79bb48bff3f703ce1dad7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a>Bir Web uygulamasından Azure anahtar kasası kullanın
## <a name="introduction"></a>Giriş
Azure web uygulamasından Azure anahtar kasası kullanmayı öğrenmenize yardımcı olmak için bu öğreticiyi kullanın. Bu, böylece web uygulamanızda kullanılabilir gizli bir Azure anahtar Kasası'erişme işlemi açıklanmaktadır.

**Tahmini tamamlanma süresi:** 15 dakika

Azure Anahtar Kasası genel bakış bilgileri için bkz. [Azure Anahtar Kasası nedir?](key-vault-whatis.md)

## <a name="prerequisites"></a>Önkoşullar
Bu öğreticiyi tamamlamak için aşağıdakilere sahip olmanız gerekir:

* Azure anahtar Kasası'nda bir gizlilik için bir URI
* Bir istemci kimliği ve bir web uygulaması için bir gizli anahtar kasanızı erişimi Azure Active Directory'ye kayıtlı
* Bir web uygulamasıdır. Biz gösteren Azure Web uygulaması olarak dağıtılmış bir ASP.NET MVC uygulaması için adımları.

> [!NOTE]
> Listelenen adımları tamamladınız gereklidir [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md) Bu öğretici için böylece bir web uygulaması için bir gizlilik ve istemci kimliği ve istemci parolası URI sahip.
> 
> 

Anahtar kasası erişecek web uygulamasını Azure Active Directory'de kayıtlı ve anahtar Kasası'na erişim verildi adrestir. Bu durumda değilse, bir kasaya Başlarken Öğreticisi uygulamada geri dönün ve listelenen adımları yineleyin.

Bu öğretici, Azure üzerinde web uygulamaları oluşturma temelleri anlamak web geliştiricileri için tasarlanmıştır. Azure Web Apps hakkında daha fazla bilgi için bkz: [Web Apps'e genel bakış](../app-service-web/app-service-web-overview.md).

## <a id="packages"></a>Nuget paketleri ekleme
Yüklü web uygulamanız gereken iki paket vardır.

* Active Directory Authentication Library - Azure Active Directory ile etkileşim ve kullanıcı kimliği yönetmek için yöntemler içerir
* Azure anahtar kasası Library - Azure anahtar kasası ile etkileşim için yöntemler içerir

Bu paketleri her ikisi de Install-Package komutunu kullanarak Paket Yöneticisi konsolu kullanılarak yüklenebilir.

    // this is currently the latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <a id="webconfig"></a>Web.Config değiştirme
Web.config dosyasında aşağıdaki gibi eklenmesi gereken üç uygulama ayarlarını vardır.

    <!-- ClientId and ClientSecret refer to the web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is the URI for the secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


Uygulamanızı Azure Web uygulaması olarak barındırmak için yapmayacağınız, web.config dosyasına gerçek ClientID, istemci gizli anahtarı ve gizli anahtar URI'sini değerleri eklemeniz gerekir. Aksi takdirde ek bir güvenlik düzeyi için Azure Portalı'nda gerçek değerler biz alacağınız çünkü bu kukla değerleri bırakın.

## <a id="gettoken"></a>Bir erişim belirteci almak için bir yöntem ekleyin
Anahtar kasası API kullanmak için bir erişim belirteci gerekir. Anahtar kasası istemci anahtar kasası API çağrılarını işler, ancak erişim belirtecini alır işleviyle sağlamanız gerekir.  

Azure Active Directory'den bir erişim belirteci alma kodu verilmiştir. Bu kodu, uygulamanızda herhangi bir yere gidebilirsiniz. Bir yardımcı programları veya EncryptionHelper sınıfı eklemek ister.  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property to hold the secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //the method that will be provided to the KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed to obtain the JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> Bir istemci kimliği ve istemci gizli anahtarı kullanarak, Azure AD uygulaması kimliğini doğrulamak için kolay bir yoludur. Ve web uygulamanızı kullanarak ayrılması görevlerini ve anahtar yönetimi üzerinde daha fazla denetim sağlar. Ancak, yapılandırma ayarlarınızda korumak istediğiniz gizli koyma olarak olarak riskli olabilecek bazı yapılandırma ayarlarınızın istemci gizli anahtarı koyma kullanır. Bir istemci kimliği ve sertifika istemci kimliği ve istemci parolası yerine Azure AD uygulaması kimliğini doğrulamak için nasıl kullanılacağı hakkında tartışma için aşağıya bakın.
> 
> 

## <a id="appstart"></a>Uygulama başlangıç gizli anahtarı alma
Şimdi anahtar kasası API çağrısı ve gizli anahtarı almak için kod gerekir. Aşağıdaki kod herhangi bir yere kullanmaya ihtiyacım önce çağırılır sürece koyabilirsiniz. Böylece gizli uygulama için kullanılabilir hale getirir ve Başlat'bir kez çalıştırılır t bu kodu Global.asax uygulama başlatma olayı koymak.

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class to hold the secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <a id="portalsettings"></a>Uygulama ayarları (isteğe bağlı) Azure portalında ekleme
Bir Azure Web uygulaması varsa, Azure Portal'da AppSettings için gerçek değerler artık ekleyebilirsiniz. Bunu yaparak, gerçek değerler Web.Config'de olmaz ancak ayrı bir erişim denetimi özelliklerinden sahip olduğu Portal korumalı. Bu değerler, web.config dosyanızda girdiğiniz değerleri için değiştirilecektir. Adları aynı olduğundan emin olun.

![Azure Portalı'nda görüntülenen uygulama ayarları][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a>Bir istemci parolası yerine bir sertifika ile kimlik doğrulaması
Azure AD uygulaması kimliğini doğrulamak için başka bir istemci kimliği ve istemci parolası yerine bir istemci kimliği ve bir sertifika kullanarak yoludur. Bir Azure Web uygulamasında bir sertifika kullanmak için adımları şunlardır:

1. Alma veya bir sertifika oluşturun
2. Sertifika bir Azure AD uygulama ile ilişkilendirme
3. Sertifikayı kullanmak üzere Web uygulamanıza kod ekleme
4. Web uygulamanız için bir sertifika Ekle

**Alma veya bir sertifika oluşturmak** bizim amacıyla bir test sertifikası yapacağız. Burada, birkaç Geliştirici Komut İstemi'nde bir sertifika oluşturmak için kullanabileceğiniz komutlar bulunmaktadır. Oluşturulan sertifika dosyaları istediğiniz dizini değiştirin.  Ayrıca, başlangıç ve bitiş tarihi sertifikanın için geçerli tarih artı 1 yıl kullanın.

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

Bitiş tarihi ve .pfx için parolayı not edin (Bu örnekte: 07/31/2016 ve test123). Bunları aşağıdaki gerekir.

Bir test sertifikası oluşturma hakkında daha fazla bilgi için bkz: [nasıl yapılır: bilgisayarınızı kendi Test sertifikası oluşturma](https://msdn.microsoft.com/library/ff699202.aspx)

**Sertifika bir Azure AD uygulama ile ilişkilendirme** sertifika sahip olduğunuza göre Azure AD uygulaması ile ilişkilendirmeniz gerekir. Şu anda Azure Portalı'nı bu iş akışı desteklemiyor; Bu PowerShell aracılığıyla tamamlanabilir. Aşağıdaki komutları assoicate için sertifika ile Azure AD uygulaması çalıştırın:

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get the thumbprint to use in your app settings
    $x509.Thumbprint

Bu komutları çalıştırdıktan sonra Azure AD'de uygulama görebilirsiniz. Arama yaparken, "Şirketimin sahip olduğu uygulamalar" "Uygulamaları Şirketim kullanıyor yerine" arama iletişim kutusunda seçtiğiniz emin olun.

Azure AD uygulama nesneleri ve ServicePrincipal nesneleri hakkında daha fazla bilgi için bkz: [uygulama ve hizmet sorumlusu nesneleri](../active-directory/active-directory-application-objects.md)

**Web uygulamanız için sertifikayı kullanmak üzere kod eklemek** şimdi biz cert erişmek ve kimlik doğrulaması için kullanmak üzere Web uygulamanız için kod ekleyeceksiniz.

İlk cert erişmek için kod yoktur.

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since the test root isn't installed.
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


StoreLocation Currentuser'a LocalMachine yerine olduğuna dikkat edin. Ve bir test sertifikası kullanıyoruz çünkü biz bulma yöntemine ' false' sağlamış olursunuz olduğunu.

Sonraki CertificateHelper kullanır ve kimlik doğrulaması için gerekli olan bir ClientAssertionCertificate oluşturan kodudur.

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


Erişim belirteci almak için yeni kod aşağıdaki gibidir. GetToken yöntemi yukarıdaki değiştirir. I kolaylık sağlamak için farklı bir ad verilen.

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

I tüm bu kod, kullanım kolaylığı için my Web uygulaması projenin yardımcı programları sınıfı yerleştirin.

En son kod değişikliği Application_Start yöntemidir. İlk olarak kimliğinizi ClientAssertionCertificate yüklemek için GetCert() yöntemini çağırmak gerekiyor. Ve biz Biz yeni KeyVaultClient oluştururken sağladığınız geri çağırma yöntemi değiştirebilirsiniz. Bu size yukarıda vardı kod değiştirir unutmayın.

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


**Web uygulamanızı Azure Portal aracılığıyla bir sertifika eklemek** bir sertifika, Web uygulamanızın ekleme olan basit bir işlemdir. İlk olarak, Azure Portalı'na gidin ve Web uygulamanıza gidin. "Özel etki alanları ve SSL" girişini ayarları dikey penceresinde, Web uygulamanız için tıklatın. Açılan dikey penceresinde KVWebApp.pfx yukarıda oluşturduğunuz sertifikayı karşıya yüklemek için pfx parolasını anımsamasını emin olun.

![Azure portalında bir Web uygulaması için bir sertifika ekleme][2]

Bir uygulama ayarı adı Web sitesi sahip, Web uygulamanızın eklemek için yapmanız gereken son şey.\_yük\_SERTİFİKALARI ve değerini *. Bu, tüm sertifikaların yüklü olduğundan güvence altına alır. Karşıya yüklediğiniz sertifikalar yüklemek istiyorsanız, virgülle ayrılmış bir liste kendi parmak izleri girebilirsiniz.

Bir Web uygulaması için bir sertifika ekleme hakkında daha fazla bilgi edinmek için [kullanarak sertifikaları Azure Web siteleri uygulamalarında](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)

**Anahtar kasasına gizli olarak bir sertifika eklemek** sertifikanızı Web App Service'e doğrudan yüklemek yerine, anahtar kasası gizli olarak depolayın ve buradan dağıtın. Bu aşağıdaki blog postasına özetlenen iki adımlı bir işlemdir [anahtar kasası aracılığıyla Azure Web uygulaması sertifikası dağıtma](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)

## <a id="next"></a>Sonraki adımlar
Programlama başvuruları için bkz: [Azure anahtar kasası C# istemci API Başvurusu](https://msdn.microsoft.com/library/azure/dn903628.aspx).

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
