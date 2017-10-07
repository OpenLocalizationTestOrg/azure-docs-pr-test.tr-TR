---
title: "AD FS kimlik doğrulaması iş Azure uygulamasıyla aaaCreate | Microsoft Docs"
description: "Nasıl toocreate satır iş kolu uygulamasını Azure App Service'te, kimlik doğrulamasını STS içi öğrenin. Bu öğretici, şirket içi STS hello gibi AD FS hedefler."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a>AD FS kimlik doğrulaması ile iş Azure uygulaması oluştur
Bu makale size nasıl gösterir toocreate bir ASP.NET MVC satır iş kolu uygulama [Azure App Service](../app-service/app-service-value-prop-what-is.md) bir şirket içi kullanılarak [Active Directory Federasyon Hizmetleri](http://technet.microsoft.com/library/hh831502.aspx) hello kimlik sağlayıcısı. Bu senaryo, toocreate--iş kolu uygulamaları Azure App Service'te istiyor ancak kuruluşunuzun dizin veri toobe şirkete depolanan ihtiyaç çalışabilir.

> [!NOTE]
> Azure App Service için hello başka bir Kurumsal kimlik doğrulama ve yetkilendirme seçeneklerine genel bakış için bkz: [Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulama](web-sites-authentication-authorization.md).
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Yapı
Azure App Service Web Apps temel bir ASP.NET uygulamasında özellikler aşağıdaki hello ile oluşturacak:

* AD FS karşı kullanıcıların kimliğini doğrular
* Kullanan `[Authorize]` tooauthorize kullanıcılar farklı eylemler için
* Visual Studio'da hata ayıklama hem de tooApp hizmeti Web uygulamaları yayımlamak için statik yapılandırması (kez yapılandırma, hata ayıklama ve dilediğiniz zaman yayımlama)  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Ne gerekiyor
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Bu öğreticiyi toocomplete hello:

* Şirket içi AD FS dağıtımı (Bu öğreticide kullanılan hello test laboratuvarı bir uçtan uca kılavuz için bkz: [Test laboratuvarı: Azure VM'de (yalnızca test için) AD FS ile tek başına STS](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))
* AD FS Yönetimi'nde izinleri toocreate bağlı olan taraf güvenleri
* Visual Studio 2013 güncelleştirme 4 veya üstü
* [Azure SDK 2.8.1 ile](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) veya daha yenisi

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a>Örnek uygulama için iş şablonu kullanın
Bu öğreticideki örnek uygulama Hello [WebApp WSFederation DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), hello Azure Active Directory ekibi tarafından oluşturulur. AD FS WS-Federasyon desteklediğinden, kolaylıkla bir şablon toocreate satır iş kolu uygulamaları olarak kullanabilirsiniz. Özellikler aşağıdaki hello sahiptir:

* Kullanan [WS-Federasyon](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate bir şirket içi AD FS dağıtımı
* Oturum açma ve oturum kapatma işlevi
* Kullanan [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (yerine Windows Identity Foundation), hangi olduğu hello ASP.NET ve kimlik doğrulama ve yetkilendirme için daha kolay tooset WIF daha ileride

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a>Merhaba örnek uygulama ayarlama
1. Kopyalama veya hello örnek çözümü indirin [WebApp WSFederation DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour yerel dizin.
   
   > [!NOTE]
   > Merhaba yönergeleri [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) nasıl yapacağınızı hello uygulamasının Azure Active Directory ile tooset. Ancak bu öğreticide, AD FS ile ayarlamak, bunun yerine burada hello adımları izleyin.
   > 
   > 
2. Merhaba çözümü açın ve ardından Controllers\AccountController.cs hello açın **Çözüm Gezgini**.
   
   Merhaba kod yalnızca WS-Federasyon kullanarak bir kimlik doğrulama sınaması tooauthenticate hello kullanıcı sorunları görürsünüz. Tüm kimlik doğrulaması App_Start\Startup.Auth.cs içinde yapılandırılır.
3. App_Start\Startup.auth.cs açın. Merhaba, `ConfigureAuth` yöntemi, Not hello satırı:
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   Merhaba OWIN dünyasında bu parçacığı aslında hello tooconfigure WS-Federasyon kimlik doğrulaması ihtiyacınız minimum tam adıdır. Bu, çok daha kolaydır ve burada Web.config XML ile Merhaba yer dünyanın dört bir yanındaki eklenmiş WIF daha zarif olur. gereksinim duyduğunuz bilgileri hello bağlı olan tarafın (RP) yalnızca hello ADFS hizmetinizin meta veri dosyası tanımlayıcısı ve başlangıç URL'si. Örnek aşağıda verilmiştir:
   
   * RP tanımlayıcısı:`https://contoso.com/MyLOBApp`
   * Meta veri adresi:`http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`
4. App_Start\Startup.auth.cs içinde statik bir dize tanımları aşağıdaki hello değiştirin:  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. Şimdi, Web.config dosyasında hello karşılık gelen değişiklikleri yapın. Merhaba Web.config açın ve uygulama ayarlarını aşağıdaki hello değiştirin:  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   İlgili ortamınıza bağlı hello anahtar değerlerini doldurun.
6. Merhaba uygulama toomake hiçbir hata bulunmadığından emin oluşturun.

Bu kadar. Merhaba örnek uygulaması, AD FS ile hazır toowork sunulmuştur. Yine tooconfigure AD FS daha sonra bu uygulamada RP güvenle gerekir.

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a>Merhaba örnek uygulama tooAzure App Service Web Apps dağıtma
Burada, hello hata ayıklama ortamı korurken hello uygulama tooa web uygulaması App Service Web Apps yayımlayın. AD FS ile RP güven olduğundan kimlik doğrulaması yine henüz çalışmıyor olması önce toopublish Merhaba uygulaması oluşturacağız unutmayın. Bunu, Bununla birlikte, artık, tooconfigure hello RP güven daha sonra kullanabileceğiniz hello web uygulaması URL'si olabilir.

1. Projenize sağ tıklayın ve seçin **Yayımla**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. Seçin **Microsoft Azure uygulama hizmeti**.
3. İçinde tooAzure kaydolduysanız henüz tıklatın **oturum** ve, Azure aboneliği toosign hello Microsoft hesabını kullanın.
4. Oturum açtıktan sonra tıklatın **yeni** toocreate bir web uygulaması.
5. Tüm gerekli alanları doldurun. Tooconnect tooon içi veri daha sonra bu web uygulaması için bir veritabanı oluşturmayın şekilde adımıdır.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. **Oluştur**'a tıklayın. Merhaba web uygulaması oluşturulduktan sonra hello Web Yayımla iletişim kutusu açılır.
7. İçinde **hedef URL**, değiştirme **http** çok**https**. Hello tüm URL'yi tooa metin düzenleyici daha sonra kullanmak için kopyalayın. Ardından **Yayımla**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. Visual Studio'da açın **Web.Release.config** projenizdeki. XML hello aşağıdaki hello Ekle `<configuration>` etiketi ve hello anahtar değeri, Yayımla web uygulamanızın URL'si ile değiştirin.  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

İşiniz bittiğinde, projenizdeki Visual Studio'da hata ayıklama ortamınız için bir tane yapılandırılmış iki RP tanımlayıcı sahip ve Azure'da hello için bir tane yayımlanan web uygulaması. Her iki AD FS ortamlarda hello bir RP güven ayarlarsınız. Hata ayıklama sırasında hello uygulamanın Web.config dosyasında kullanılan toomake ayarlardır, **hata ayıklama** AD FS ile yapılandırma çalışma. Ne zaman yayımlanan (varsayılan olarak, hello **sürüm** yapılandırma yayımlanır), dönüştürülmüş Web.config Web.Release.config hello uygulama ayarı değişiklikleri içeren yüklenir.

Tooattach hello yayımlanan web uygulamasına istiyorsanız hello bir kopyasını oluşturabilirsiniz (yani, kodunuzun hello yayımlanan web uygulamasında hata ayıklama simgeleri yüklemelisiniz) Azure toohello hata ayıklayıcı, hata ayıklama yapılandırması hata ayıklama Azure ancak kendi özel Web.config ile dönüştürme ( Örneğin Web.AzureDebug.config) Web.Release.config hello uygulama ayarlarını kullanır. Bu, toomaintain statik yapılandırması hello farklı ortamlar genelinde sağlar.

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a>Bağlı olan taraf Güvenleri'ni AD FS Yönetimi'nde yapılandırın
Şimdi örnek uygulamanızı kullanın ve gerçekte AD FS ile kimlik doğrulaması yapmak için önce AD FS Yönetimi RP güvende tooconfigure gerekir. İki ayrı RP güvenleri tooset, hata ayıklama ortamınız için diğeri yayımlanan web uygulamanız gerekir.

> [!NOTE]
> Her iki ortamınız için aşağıdaki adımları hello yineleyin emin olun.
> 
> 

1. AD FS sunucunuz üzerinde yönetim hakları tooAD FS sahip kimlik bilgileriyle oturum açın.
2. AD FS Yönetimi'ni açın. Sağ **AD FS\Trusted Relationships\Relying taraf güvenleri** seçip **bağlı olan taraf güveni Ekle**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. Merhaba, **veri kaynağı Seç** sayfasında **hello bağlı olan taraf verilerini elle girin**. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. Merhaba, **görünen adı belirt** sayfasında Merhaba uygulaması için bir görünen ad yazın ve tıklayın **sonraki**.
5. Merhaba, **protokolü seçin** sayfasında, **sonraki**.
6. Merhaba, **sertifika Yapılandır** sayfasında, **sonraki**.
   
   > [!NOTE]
   > HTTPS zaten kullanıyor olmanız olduğundan, şifrelenen belirteçler isteğe bağlıdır. AD FS, bu sayfada gelen tooencrypt belirteçleri gerçekten istiyorsanız, kodunuzda belirteç şifre çözme mantığı de eklemeniz gerekir. Daha fazla bilgi için bkz: [OWIN WS-Federasyon ara yazılım yapılandırma ve kabul belirteçlerini el ile şifrelenmiş](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).
   > 
   > 
7. Hello sonraki adıma geçmeden önce Visual Studio projenizden tek parça bilgi gerekir. Merhaba Proje Özellikleri'nde hello Not **SSL URL** hello uygulamasının. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. AD FS yönetimi, hello edilene **URL Yapılandır** hello sayfasının **bağlı olan taraf güveni Ekleme Sihirbazı**seçin **hello WS-Federasyon Edilgen Protokolü desteğini etkinleştir** ve Merhaba önceki adımda not ettiğiniz Hello Visual Studio projenizi SSL URL'sini yazın. Ardından **İleri**'ye tıklayın.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > Burada toosend hello istemci kimlik doğrulama işleminden sonra başarılı URL'yi belirtir. Merhaba hata ayıklama ortamı için olmalıdır <code>https://localhost:&lt;port&gt;/</code>. Merhaba yayımlanan web uygulaması için başlangıç web uygulaması URL'si olmalıdır.
   > 
   > 
9. Merhaba, **tanımlayıcıları yapılandırma** sayfasında, projenizin SSL URL zaten listelenmiş olduğunu doğrulayın ve tıklayın **sonraki**. Tıklatın **sonraki** tüm yolu toohello varsayılan seçimleri hello sihirbazıyla sonuna hello.
   
   > [!NOTE]
   > İçinde App_Start\Startup.auth.cs Visual Studio projenizin karşı hello değerini bu tanımlayıcı eşleştirildiği <code>WsFederationAuthenticationOptions.Wtrealm</code> federe kimlik doğrulaması sırasında. Varsayılan olarak, hello uygulamanın URL hello önceki adımdaki RP tanımlayıcı olarak eklenir.
   > 
   > 
10. Şimdi, AD FS'de hello RP uygulaması projeniz için yapılandırma tamamladınız. Ardından, bu uygulama toosend yapılandırın hello uygulamanızın gereksinim duyduğu talepleri. Merhaba **talep kurallarını Düzenle** iletişim kutusu açıldığında varsayılan olarak, hello hello sihirbazın sonunda hemen başlatmak için. Yapılandıralım en az hello aşağıdaki talep (şemalarda parantez içinde):
    
    * ASP.NET toohydrate tarafından kullanılan adı (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - `User.Identity.Name`.
    * Kullanıcı asıl adı (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - kullanılan toouniquely hello kuruluşunuzdaki kullanıcılar tanımlayın.
    * Grup üyelikleri rolleri (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - olarak kullanılabileceğini `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize denetleyicileri/eylemler. Gerçekte, bu yaklaşım değil olması hello çoğu kullanıcı rolü yetkilendirme için. AD kullanıcıları güvenlik gruplarının toohundreds aitse, rol talepleri hello SAML belirteci yüzlerce haline gelir. Alternatif bir yaklaşım, tek bir rol talep koşullu hello kullanıcının üyelik belirli bir gruba bağlı olarak toosend ' dir. Ancak, biz Bu öğretici için basit tut.
    * Kimliği (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) name - sahteciliğe karşı koruma doğrulama için kullanılabilir. Merhaba nasıl toomake çalışır sahteciliğe karşı koruma doğrulama ile ilgili daha fazla bilgi için bkz **iş işlevsellik ekleyen** bölümünü [Azure Active Directory kimlik doğrulaması ile iş Azure uygulaması oluştur ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).
    
    > [!NOTE]
    > Merhaba talep, türleri, uygulamanızın uygulamanızın gereksinimlerinize göre belirlenir için tooconfigure gerekir. Örneğin, Azure Active Directory uygulamaları (yani RP güvenleri) tarafından desteklenen talep Hello listesi için bkz [desteklenen belirteç ve talep türleri](http://msdn.microsoft.com/library/azure/dn195587.aspx).
    > 
    > 
11. Merhaba talep kurallarını Düzenle iletişim kutusunda tıklatın **Kuralı Ekle**.
12. Merhaba ekran görüntüsünde gösterildiği gibi Hello adı, UPN ve rol talepleri yapılandırmak ve tıklatın **son**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    Ardından, bir geçici ad kimliği talep hello adımları kullanarak gösterilen oluşturun [SAML onaylar adı tanımlayıcılarını](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
13. Tıklatın **Kuralı Ekle** yeniden.
14. Seçin **talepleri özel kural kullanarak Gönder** tıklatıp **sonraki**.
15. Hello içine yapıştırma hello aşağıdaki kural dil **özel kural** kutusu, ad hello kuralı **başına oturum tanımlayıcısı** tıklatıp **son**.  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    Özel kural bu ekran görüntüsüne görünmelidir:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. Tıklatın **Kuralı Ekle** yeniden.
17. Seçin **gelen talebi Dönüştür** tıklatıp **sonraki**.
18. İ (Merhaba özel kuralında oluşturulan hello talep türü kullanarak) hello ekran görüntüsü gösterildiği gibi Hello kuralı yapılandırmak ve **son**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    Merhaba geçici ad kimliği talebi hello adımları hakkında ayrıntılı bilgi için bkz: [SAML onaylar adı tanımlayıcılarını](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
19. Tıklatın **Uygula** hello içinde **talep kurallarını Düzenle** iletişim. Merhaba ekran aşağıdaki gibi görünmelidir:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > Yeniden, hata ayıklama ortamı ve yayımlanan web uygulaması için bu adımları yineleyin emin olun.
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a>Uygulamanız için federe kimlik doğrulamasını Sına
Uygulamanızın kimlik doğrulaması mantığı AD FS karşı hazır tootest şunlardır. My AD FS laboratuar ortamında tooa test grubu içinde Active Directory (AD) ait bir test kullanıcısı sahibim.

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

hata ayıklayıcısında Merhaba, tüm yapmanız gereken toodo şimdi tootest kimlik doğrulaması türüdür `F5`. Merhaba yayımlanan web uygulamasında tootest kimlik doğrulamasını istiyorsanız, toohello URL'ye gidin.

Merhaba web uygulaması yüklendikten sonra tıklatın **oturum**. AD FS tarafından seçilen hello kimlik doğrulama yöntemine bağlı olarak AD FS tarafından sunulan ya da bir oturum açma iletişim kutusu veya hello oturum açma sayfası artık almanız gerekir. Internet Explorer 11 ne alıyorum aşağıda verilmiştir.

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

Merhaba AD FS dağıtım hello AD etki alanındaki bir kullanıcının oturum oturum sonra yeniden hello giriş sayfası görmelisiniz **Hello <User Name>!** Merhaba köşede. İşte ne alıyorum.

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

Şu ana kadar yol aşağıdaki hello başarılı:

* Uygulamanız başarıyla AD FS ulaştı ve eşleşen bir RP tanımlayıcı hello AD FS veritabanı bulunamadı
* AD FS başarıyla bir AD kullanıcısının ve yeniden yönlendirme toohello uygulamanın giriş sayfası geri doğrulaması
* Merhaba olgusu hello kullanıcı belirtildiği gibi başarıyla gönderilen hello adı olarak AD FS talep (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour uygulama adı, hello köşesinde görüntülenir. 

Merhaba adı talebi yoksa, görülen **Hello!**. Görünümler/paylaşılan bakarsanız\_LoginPartial.cshtml, bulduğunuz bunu kullandığını `User.Identity.Name` toodisplay hello kullanıcı adı. Kullanıcı hello SAML belirtecinde kullanılabilir talep kimliği doğrulanmış Merhaba Hello adı, daha önce belirtildiği gibi ASP.NET bu özelliğiyle hydrates. Tüm hello toosee, AD FS, bir kesme noktası Controllers\HomeController.cs içinde hello yerleştirme tarafından dizin eylem yöntemine gönderilen talepleri. Merhaba kullanıcının kimliği doğrulandıktan sonra hello incelemek `System.Security.Claims.Current.Claims` koleksiyonu.

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a>Belirli denetleyicileri veya eylemler için Kullanıcıları yetkilendirmek
RP güven yapılandırmanıza grup üyeliklerini rol talepleri dahil olduğundan, artık doğrudan hello kullanabilmek için `[Authorize(Roles="...")]` decoration denetleyicileri ve eylemleri için. Merhaba Oluştur-okunur-güncelleştir-Sil (CRUD) desen ile bir iş kolu satır uygulamasında, her eylem belirli rolleri tooaccess yetki verebilir. Şu an için yalnızca bu özellik hello varolan giriş denetleyicisinde çıkışı çalışacaktır.

1. Controllers\HomeController.cs açın.
2. Merhaba tasarlamanız `About` ve `Contact` koddan, kimliği doğrulanmış kullanıcının güvenlik grup üyeliklerini kullanarak eylem yöntemleri benzer toohello.  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    Ekledim beri **Test kullanıcısı** çok**Test grubu** my AD FS laboratuvar ortamında Test grubu tootest yetkilendirme üzerinde kullanmam `About`. İçin `Contact`, hello negatif durumunun test edeceksiniz **Domain Admins**, toowhich **Test kullanıcı** ait değil.
3. Merhaba hata ayıklayıcı boyutlandırın `F5` ve oturum açın ve ardından **hakkında**. Merhaba şimdi görüntüleme `~/About/Index` , kimliği doğrulanmış kullanıcının bu eylemi için yetkili olup olmadığını başarıyla, sayfa.
4. Şimdi **kişi**, hangi my durumda yetki **Test kullanıcısı** hello eylemi için. Ancak, bu iletiyi sonunda gösterir yeniden yönlendirilen tooAD FS hello tarayıcısıdır:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    Bu hatada Olay Görüntüleyicisi'nde hello AD FS sunucu araştırmak, bu özel durum iletisi görüntülenir:  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    Bu hatanın nedeni Hello bir kullanıcının rollerini yetkili olmadıkları zaman varsayılan olarak, MVC 401 Yetkisiz döndürmesidir. Bir yeniden kimlik doğrulaması isteği tooyour kimlik sağlayıcısı'nı (AD FS) tetikler. Merhaba kullanıcının kimliği zaten doğrulanmış olduğundan, AD FS toohello döndüren bir yeniden yönlendirme döngü oluşturma başka bir 401 sorunları aynı sayfa. AuthorizeAttribute'nın geçersiz kılar `HandleUnauthorizedRequest` basit bir mantık tooshow yöntemiyle devam ediliyor hello yeniden yönlendirme döngüsü yerine mantıklı bir şey.
5. Merhaba projesinde AuthorizeAttribute.cs ve kod içine aşağıdaki Yapıştır hello adlı bir dosya oluşturun.
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    Merhaba kimliği doğrulanmış ancak yetkisiz durumlarda kod gönderir (Yasak) HTTP 403 HTTP 401 (yetkisiz) yerine geçersiz kılar.
6. Merhaba hata ayıklayıcısı yeniden Çalıştır `F5`. Tıklatarak **kişi** şimdi (paragrafta barındırabilir) daha bilgilendirici bir hata iletisi gösterir:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. Merhaba uygulama tooAzure App Service Web Apps yeniden yayımlamanız ve hello Canlı uygulamasının başlangıç davranışını sınayın.

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a>Tooon içi verilere bağlanma
İş uygulamanızı Azure Active Directory yerine AD FS ile tooimplement istersiniz, bir kuruluşun veri kapalı içi tutma ile uyumluluk sorunlarını nedenidir. Bu toouse izin verilmiyor beri web uygulamanızı azure'da şirket içi veritabanlarına erişim gerekir anlamına [SQL veritabanı](/services/sql-database/) hello web uygulamalarınız için veri katmanı olarak.

Azure App Service Web Apps iki yaklaşım erişirken şirket içi veritabanlarıyla destekler: [karma bağlantılar](../biztalk-services/integration-hybrid-connection-overview.md) ve [sanal ağlar](web-sites-integrate-with-vnet.md). Daha fazla bilgi için bkz: [kullanarak VNET tümleştirme ve karma bağlantılar Azure App Service Web Apps ile](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Ek kaynaklar
* [Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulaması](web-sites-authentication-authorization.md)
* [Azure Active Directory kimlik doğrulaması ile iş Azure uygulaması oluştur](web-sites-dotnet-lob-application-azure-ad.md)
* [Visual Studio 2013'te Hello ASP.NET ile şirket içi Kurumsal kimlik doğrulama seçeneği (ADFS) kullanın](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [Gelen VS2013 Web projesi WIF tooKatana geçirme](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [Active Directory Federasyon Hizmetleri'ne Genel Bakış](http://technet.microsoft.com/library/hh831502.aspx)
* [WS-Federasyon 1.1 belirtimini](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

