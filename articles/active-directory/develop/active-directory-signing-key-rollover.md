---
title: "Anahtar geçişi Azure AD'de aaaSigning | Microsoft Docs"
description: "Bu makalede, anahtar geçişi en iyi uygulamaları için Azure Active Directory imzalama hello anlatılmaktadır."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a>Azure Active Directory'de anahtar geçişi imzalama
Bu konuda, Azure Active Directory (Azure AD) toosign güvenlik belirteçlerinde kullanılan hello ortak anahtarları hakkında tooknow gerekenler açıklanmaktadır. Bu anahtarları rollover düzenli aralıklarla ve acil bir durumda uzatılabilir hemen önemli toonote olur. Azure AD kullanan tüm uygulamalar, mümkün tooprogrammatically tanıtıcı hello anahtarı geçiş işlemi veya düzenli el ile geçiş işlemi oluşturun. Hello anahtarları iş nasıl tooassess Merhaba rollover tooyour uygulaması etkisini nasıl hello ve nasıl toounderstand okuma devam tooupdate uygulamanızı veya düzenli el ile geçiş işlemi toohandle anahtar geçişi gerekirse oluşturun.

## <a name="overview-of-signing-keys-in-azure-ad"></a>Azure AD'de imzalama anahtarlarının genel bakış
Azure AD kullanır kendisi ve hello arasında endüstri standartları tooestablish güven üzerine kurulu ortak anahtar şifrelemesi kullanan uygulamaları. Pratikteki, bu yolu izleyerek hello çalışır: Azure AD genel ve özel bir anahtar çiftinden oluşur imzalama bir anahtar kullanır. Azure AD kimlik doğrulaması için kullandığı tooan uygulamada bir kullanıcı oturum açtığında, Azure AD hello kullanıcı hakkındaki bilgileri içeren bir güvenlik belirteci oluşturur. Bu belirteç geri toohello uygulama gönderilmeden önce özel anahtarını kullanarak Azure AD tarafından imzalanır. belirteç hello tooverify geçerli olduğundan ve Azure AD'den gerçekte kaynaklı, Merhaba uygulaması hello kiracının içinde yer alan Azure AD tarafından sunulan hello ortak anahtarı kullanılarak hello belirtecinin imzası doğrulama gerekir [Openıd Connect bulma belge](http://openid.net/specs/openid-connect-discovery-1_0.html) veya SAML/WS-Fed [Federasyon meta veri belgesi](active-directory-federation-metadata.md).

Güvenlik nedeniyle, Azure AD anahtar dökümünü düzenli aralıklarla ve acil bir hello durumda imzalama uzatılabilir hemen. Azure AD ile tümleşir herhangi bir uygulama bir anahtar geçişi olayı Hayır önemli ne sıklıkta oluşabilir toohandle hazırlıklı olmalıdır. Yoktur ve uygulamanızı toouse bir belirteç süresi dolan anahtar tooverify hello imza çalışır hello oturum açma isteği başarısız olur.

Her zaman birden fazla geçerli anahtar hello Openıd Connect bulma belge ve hello Federasyon meta veri belgesi mevcut değil. Uygulamanızı hazırlıklı olmalıdır toouse hello anahtarlardan herhangi birine belirtilen hello belgede bir anahtar yakında geri alınması beri başka değişimi olması ve benzeri.

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a>Nasıl uygulamanızı etkilenecek varsa tooassess ve onunla ilgili hangi toodo
Anahtar geçişi, uygulamanızın nasıl işlediğini uygulama veya hangi kimlik protokolü ve kitaplık kullanıldı hello türü gibi değişkenleri bağlıdır. Aşağıdaki hello bölümler Hello en yaygın uygulama türlerini hello anahtar geçişi tarafından etkilenen ve kılavuzluk nasıl tooupdate uygulama toosupport otomatik geçişi hello veya el ile Merhaba anahtarı güncelleştirme olup olmadığını değerlendirin.

* [Yerel istemci uygulamaları kaynaklara erişme](#nativeclient)
* [Web uygulamaları / API'leri kaynaklara erişme](#webclient)
* [Web uygulamaları / API'leri kaynakları koruma ve Azure App Services kullanılarak oluşturulmuş](#appservices)
* [Web uygulamaları / .NET OWIN Openıd Connect, WS-Fed veya WindowsAzureActiveDirectoryBearerAuthentication ara yazılımı kullanarak kaynakları koruma API'leri](#owin)
* [Web uygulamaları / .NET Core Openıd Connect veya JwtBearerAuthentication ara yazılımı kullanarak kaynakları koruma API'leri](#owincore)
* [Web uygulamaları / Node.js passport azure ad modülünü kullanarak kaynakları koruma API'leri](#passport)
* [Web uygulamaları / API'leri kaynakları koruma ve Visual Studio 2015 veya Visual Studio 2017 oluşturulmuş](#vs2015)
* [Kaynakları koruma ve Visual Studio 2013 ile oluşturulan web uygulamaları](#vs2013)
* [Kaynakları koruma ve Visual Studio 2013 ile oluşturulan web API'leri](#vs2013_webapi)
* [Kaynakları koruma ve Visual Studio 2012 ile oluşturulan web uygulamaları](#vs2012)
* [Kaynakları koruma ve Windows Identity Foundation'ı kullanarak 2008 o Visual Studio 2010 ile oluşturulan web uygulamaları](#vs2010)
* [Web uygulamaları / kaynakları koruma API'leri kullanarak diğer kitaplıkları veya el ile Merhaba hiçbirini uygulama protokolleri desteklenmez](#other)

Bu kılavuz **değil** için geçerlidir:

* Azure AD uygulama (özel dahil) galerisinden eklenen uygulamalar bakımından toosigning anahtarlarla ayrı yönergeler vardır. [Daha fazla bilgi.](../active-directory-sso-certs.md)
* Uygulama Ara sunucusu üzerinden yayımlanan uygulamalarla anahtarları imzalama hakkında tooworry yoksa şirket içi.

### <a name="nativeclient"></a>Yerel istemci uygulamaları kaynaklara erişme
Yalnızca (yani kaynaklarına erişen uygulamalar Microsoft Graph, KeyVault, Outlook API ve diğer Microsoft APIs) genellikle yalnızca bir belirteç elde ve toohello kaynak sahibi geçirin. O tüm kaynakları koruma değil, hello belirteci incelemek değil ve bu nedenle doğru şekilde imzalanmış tooensure gerekmez.

Yerel istemci uygulamaları, masaüstü veya mobil, bu kategoriye ve böylece hello rollover tarafından etkilenmez.

### <a name="webclient"></a>Web uygulamaları / API'leri kaynaklara erişme
Yalnızca (yani kaynaklarına erişen uygulamalar Microsoft Graph, KeyVault, Outlook API ve diğer Microsoft APIs) genellikle yalnızca bir belirteç elde ve toohello kaynak sahibi geçirin. O tüm kaynakları koruma değil, hello belirteci incelemek değil ve bu nedenle doğru şekilde imzalanmış tooensure gerekmez.

Web uygulamaları ve web hello yalnızca uygulama akışı kullanarak API'leri (istemci kimlik bilgileri / istemci sertifikası), bu kategoriye girer ve bu nedenle hello rollover tarafından etkilenmez.

### <a name="appservices"></a>Web uygulamaları / API'leri kaynakları koruma ve Azure App Services kullanılarak oluşturulmuş
Azure uygulama hizmetleri kimlik doğrulama / yetkilendirme (EasyAuth) işlevselliği zaten hello gerekli mantığı toohandle anahtar geçişi otomatik olarak.

### <a name="owin"></a>Web uygulamaları / .NET OWIN Openıd Connect, WS-Fed veya WindowsAzureActiveDirectoryBearerAuthentication ara yazılımı kullanarak kaynakları koruma API'leri
Uygulamanızı hello .NET OWIN Openıd Connect, WS-Fed veya WindowsAzureActiveDirectoryBearerAuthentication ara yazılımı kullanıyorsanız, zaten hello gerekli mantığı toohandle anahtar geçişi otomatik olarak içeriyor.

Uygulamanız herhangi birini herhangi parçacıkları uygulamanızın haline veya Startup.Auth.cs aşağıdaki hello bakarak kullandığını doğrulayın

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <a name="owincore"></a>Web uygulamaları / .NET Core Openıd Connect veya JwtBearerAuthentication ara yazılımı kullanarak kaynakları koruma API'leri
Uygulamanızı hello .NET Core OWIN Openıd Connect veya JwtBearerAuthentication ara yazılımı kullanıyorsanız, zaten hello gerekli mantığı toohandle anahtar geçişi otomatik olarak içeriyor.

Uygulamanız herhangi birini herhangi parçacıkları uygulamanızın haline veya Startup.Auth.cs aşağıdaki hello bakarak kullandığını doğrulayın

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <a name="passport"></a>Web uygulamaları / Node.js passport azure ad modülünü kullanarak kaynakları koruma API'leri
Uygulamanızı hello Node.js passport ad modülünü kullanıyorsanız, zaten hello gerekli mantığı toohandle anahtar geçişi otomatik olarak içeriyor.

Onaylayabilirsiniz uygulama passport-Uygulamanızın app.js parçacığında aşağıdaki hello arayarak ad

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <a name="vs2015"></a>Web uygulamaları / API'leri kaynakları koruma ve Visual Studio 2015 veya Visual Studio 2017 oluşturulmuş
Uygulamanızı Visual Studio 2015 ya da Visual Studio 2017 bir web uygulaması şablonu kullanılarak oluşturulan ve seçtiyseniz **iş ve Okul hesapları** hello gelen **kimlik doğrulamayı Değiştir** menüsünde, zaten Merhaba gerekli mantığı toohandle anahtar geçişi otomatik olarak sahiptir. OWIN Openıd Connect Hello Ara yazılımında katıştırılmış bu mantığı alır ve hello anahtarlarını hello Openıd Connect bulma belgesinden önbelleğe alır ve bunları düzenli aralıklarla yeniler.

Kimlik doğrulama tooyour çözüm elle eklediyseniz, uygulamanızın hello gerekli anahtar geçişi mantığı sahip olmayabilir. Toowrite gerekir, kendinize veya izleyin hello adımları [Web uygulamaları / diğer kitaplıkları'nı kullanarak veya el ile Merhaba hiçbirini uygulama API'leri Desteklenen protokoller.](#other).

### <a name="vs2013"></a>Kaynakları koruma ve Visual Studio 2013 ile oluşturulan web uygulamaları
Uygulamanızı Visual Studio 2013'te bir web uygulaması şablonu kullanılarak oluşturulan ve seçtiyseniz **Kurumsal hesaplar** hello gelen **kimlik doğrulamayı Değiştir** menüsünde hello gerekli zaten var mantığı toohandle rollover otomatik olarak anahtar. Bu mantık, kuruluşunuzun benzersiz tanımlayıcı ve iki veritabanı tablolardaki hello projeyle ilişkili anahtar bilgileri imzalama hello depolar. Merhaba bağlantı dizesi hello veritabanı için hello projenin Web.config dosyasında bulabilirsiniz.

Kimlik doğrulama tooyour çözüm elle eklediyseniz, uygulamanızın hello gerekli anahtar geçişi mantığı sahip olmayabilir. Toowrite gerekir, kendinize veya izleyin hello adımları [Web uygulamaları / diğer kitaplıkları'nı kullanarak veya el ile Merhaba hiçbirini uygulama API'leri Desteklenen protokoller.](#other).

Aşağıdaki adımları hello hello mantığı uygulamanızda düzgün çalıştığını doğrulamak yardımcı olur.

1. Visual Studio 2013'te hello çözümü açın ve üzerinde hello ardından **Sunucu Gezgini** hello sağ penceresi sekmesinde.
2. Genişletme **veri bağlantıları**, **DefaultConnection**ve ardından **tabloları**. Merhaba bulun **IssuingAuthorityKeys** tablo, sağ tıklatın ve ardından **Show Table Data**.
3. Merhaba, **IssuingAuthorityKeys** tablo, hello anahtar toohello parmak izi değeri karşılık gelen en az bir satır olacak. Merhaba tablodaki herhangi bir satır silin.
4. Sağ hello **kiracılar** tablo ve ardından **Show Table Data**.
5. Merhaba, **kiracılar** tablo, tooa benzersiz dizin Kiracı tanımlayıcısı karşılık gelen en az bir satır olacak. Merhaba tablodaki herhangi bir satır silin. Her iki hello hello satırlarda silmezseniz **kiracılar** tablo ve **IssuingAuthorityKeys** tablo, çalışma zamanında bir hata alırsınız.
6. Derleme ve hello uygulamayı çalıştırın. Tooyour hesabında oturum açtıktan sonra Merhaba uygulaması durdurabilirsiniz.
7. Toohello iade **Sunucu Gezgini** ve hello başlangıç değerleri bakmak **IssuingAuthorityKeys** ve **kiracılar** tablo. Bunlar otomatik olarak uygun bilgilerle hello Federasyon meta veri belgesi hello yeniden olduğunu fark edeceksiniz.

### <a name="vs2013"></a>Kaynakları koruma ve Visual Studio 2013 ile oluşturulan web API'leri
Bir web API uygulamasını hello Web API şablonu kullanarak Visual Studio 2013'oluşturduysanız ve ardından seçili **Kurumsal hesaplar** hello gelen **kimlik doğrulamayı Değiştir** menüsünde, zaten sahip hello Uygulamanızı gerekli mantığı.

Kimlik doğrulama el ile yapılandırdıysanız, hello toolearn aşağıda nasıl yönergeleri tooconfigure Web API tooautomatically anahtar bilgilerini güncelleştirin.

Merhaba aşağıdaki kod parçacığını nasıl tooget hello Federasyon meta veri belgesi son anahtarları hello ve hello kullan gösterir [JWT belirteci işleyicisi](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello belirteci. Hello kod parçacığını bir veritabanı, yapılandırma dosyası veya başka bir yerde olması gerekmediğini kendi gelecekteki kalıcı hello anahtar toovalidate mekanizma önbelleğe alma belirteçleri Azure AD'den kullanılacağını varsayar.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <a name="vs2012"></a>Kaynakları koruma ve Visual Studio 2012 ile oluşturulan web uygulamaları
Uygulamanızı Visual Studio 2012'de oluşturulduysa, büyük olasılıkla hello kimlik ve erişim aracı tooconfigure uygulamanızı kullanılır. Ayrıca hello kullanıyorsanız büyük olasılıkla [doğrulama verenin adı kayıt defteri (VINR)](https://msdn.microsoft.com/library/dn205067.aspx). Güvenilen kimlik sağlayıcıları (Azure AD) hakkında bilgi Hello VINR sorumludur ve onlar tarafından yayınlanan toovalidate belirteçleri hello anahtarları kullanılır. Merhaba VINR ayrıca kolay tooautomatically güncelleştirme hello anahtar bilgileri hello yapılandırması son hello ile güncel ise denetimi, bir dizinle ilişkili hello son Federasyon meta veri belgesi yükleyerek bir Web.config dosyasında depolanan kılar Belge ve güncelleştirme hello uygulama toouse hello yeni anahtarı gerekli.

Uygulamanızı hello kod örnekleri ya da Microsoft tarafından sağlanan izlenecek belgelerine herhangi birini kullanarak oluşturduysanız, hello anahtar geçişi mantığı zaten projenizde dahil edilir. Aşağıdaki hello kodu zaten projenizde var. fark edeceksiniz. Uygulamanız bu mantığı yoksa ve düzgün çalıştığını tooverify tooadd hello adımları izleyin.

1. İçinde **Çözüm Gezgini**, başvuru toohello ekleme **System.IdentityModel** hello uygun proje için derleme.
2. Açık hello **Global.asax.cs** dosya ve hello aşağıdaki yönergeleri kullanarak:
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. Yöntem toohello aşağıdaki hello eklemek **Global.asax.cs** dosyası:
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. Merhaba çağırma **RefreshValidationSettings()** hello yönteminde **Application_Start()** yönteminde **Global.asax.cs** gösterildiği gibi:
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

Bu adımları uyguladıktan sonra uygulamanızın Web.config hello hello Federasyon meta veri belgesi hello son anahtarları dahil olmak üzere, en son bilgilerle güncelleştirilir. Bu güncelleştirme, IIS, uygulama havuzu geri dönüştürme sayısı her zaman meydana gelir; Varsayılan olarak IIS, 29 saatte toorecycle uygulamaları ayarlanır.

Merhaba anahtar geçişi mantığı çalışma tooverify Hello adımları izleyin.

1. Uygulamanızı yukarıdaki, açık hello hello kodu kullandığını doğruladıktan sonra **Web.config** dosya ve toohello gidin  **<issuerNameRegistry>**  bloğu, özellikle birkaç satır aşağıdaki Merhaba aranıyor:
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. Merhaba,  **<add thumbprint=””>**  ayarı ile farklı bir karakterle değiştirerek hello parmak izi değerini değiştirin. Merhaba Kaydet **Web.config** dosya.
3. Merhaba uygulaması oluşturmak ve ardından çalıştırın. Merhaba oturum açma işlemini tamamlamak, uygulamanız başarıyla hello anahtarı, dizinin Federasyon meta verileri belgeden gerekli hello bilgilerini indirerek güncelleştiriyor. Oturum açma sorunları yaşıyorsanız, uygulamanızda hello değişiklikleri doğru hello okuyarak olduğundan emin olun [ekleme oturum açma tooYour Web uygulaması kullanarak Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) konusuna veya indiriliyor ve aşağıdaki kod örneği hello inceleniyor: [ Azure Active Directory için çok Kiracılı bulut uygulaması](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).

### <a name="vs2010"></a>Kaynakları koruma ve Visual Studio 2008 veya 2010 ile oluşturulan web uygulamaları ve Windows Identity Foundation (WIF) v1.0 .NET 3.5 için
Bir uygulama WIF v1.0 oluşturulduysa, uygulamanızın yapılandırma toouse yeni bir anahtar yok sağlanan mekanizması tooautomatically yenileme yoktur.

* *En kolay yolu* hello WIF hello son meta veri belgesi alabilir ve yapılandırmanızı güncelleştirmek SDK dahil hello FedUtil araçları kullanın.
* Merhaba System ad alanında bulunan WIF hello en yeni sürümünü içeren, uygulama too.NET 4.5, güncelleştirin. Merhaba sonra kullanabileceğiniz [doğrulama verenin adı kayıt defteri (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform otomatik olarak güncelleştirilmesini hello uygulamanın yapılandırma.
* Bu kılavuzu belge hello sonunda hello yönergeleri göredir el ile geçiş gerçekleştirin.

Toouse hello FedUtil tooupdate yapılandırmanızı yönergeler:

1. Merhaba WIF v1.0 SDK geliştirme makinenizde Visual Studio 2008 veya 2010 yüklü olduğunu doğrulayın. Yapabilecekleriniz [buradan indirin](https://www.microsoft.com/en-us/download/details.aspx?id=4451) henüz yüklemediyseniz.
2. Merhaba çözümü Visual Studio'da açın ve ardından hello geçerli projesine sağ tıklatın ve **güncelleştirme Federasyon meta verileri**. Bu seçenek kullanılabilir durumda değilse, FedUtil ve/veya hello WIF v1.0 SDK yüklenmedi.
3. Merhaba isteminden seçin **güncelleştirme** Federasyon meta verilerini güncelleştirme toobegin. Merhaba uygulaması barındırıldığı erişim toohello sunucu ortamınız varsa, isteğe bağlı olarak FedUtil'ın kullanabilirsiniz [otomatik meta veri güncelleştirme zamanlayıcı](https://msdn.microsoft.com/library/ee517272.aspx).
4. Tıklatın **son** toocomplete hello güncelleştirme işlemi.

### <a name="other"></a>Web uygulamaları / kaynakları koruma API'leri kullanarak diğer kitaplıkları veya el ile Merhaba hiçbirini uygulama protokolleri desteklenmez
Desteklenen hello protokollerden herhangi birini el ile uygulanan veya başka bir kitaplık kullanıyorsanız, tooreview hello kitaplığı gerekir veya anahtar Merhaba, uygulama tooensure hello Openıd Connect bulma belge veya hello alınıyor Federasyon meta veri belgesi. Bunun için tek yönlü toocheck toodo kodunuzu veya hello kitaplığın kod arama tüm çağrıları tooeither hello Openıd bulma belge veya hello Federasyon meta veri belgesi için ' dir.

Anahtarı depolanıyor yere veya sabit kodlanmış uygulamanızda el ile Merhaba anahtar ve buna göre tarafından gerçekleştirmek hello yönergeleri Bu kılavuzu belge hello sonunda göredir el ile bir rollover güncelleştirme alın. **Kesinlikle uygulama toosupport otomatik geçişi artırmak teşvik edilir** hello birini kullanarak yaklaşıyor anahat Bu makale tooavoid gelecekteki kesintilerini ve ek yükü içinde Azure AD, rollover tempoyla artırır veya varsa bir Acil Durum bant dışı geçişi.

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a>Nasıl tootest etkilenecek olan ise, uygulama toodetermine
Merhaba komut dosyaları indirip hello yönergelerini takip otomatik anahtar geçişi, uygulamanızın destekleyip desteklemediğini doğrulamak için [bu GitHub depo.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a>Nasıl tooperform uygulama, otomatik geçişi desteklemiyorsa, el ile geçiş
Uygulamanız varsa **değil** otomatik geçişi destekler, buna göre düzenli aralıklarla izleyiciler Azure AD imzalama işlemi anahtarları ve el ile geçiş işlemini gerçekleştirir tooestablish gerekir. [Bu GitHub deposunu](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) komut dosyası ve yönergeler içeren toodo bu.

