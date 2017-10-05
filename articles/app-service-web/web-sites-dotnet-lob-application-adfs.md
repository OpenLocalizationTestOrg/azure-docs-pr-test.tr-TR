---
title: "AD FS kimlik doğrulaması ile bir iş Azure uygulaması oluşturma | Microsoft Docs"
description: "Azure uygulama hizmetinde şirket içi STS ile kimliğini doğrulayan bir satır iş kolu uygulaması oluşturmayı öğrenin. Bu öğretici, şirket içi STS olarak AD FS hedefler."
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
ms.openlocfilehash: f9a8984400378d154a504af8a41609900128d052
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a>AD FS kimlik doğrulaması ile iş Azure uygulaması oluştur
Bu makalede, bir ASP.NET MVC satır iş kolu uygulamasının nasıl oluşturulacağını gösterir [Azure App Service](../app-service/app-service-value-prop-what-is.md) bir şirket içi kullanılarak [Active Directory Federasyon Hizmetleri](http://technet.microsoft.com/library/hh831502.aspx) kimlik sağlayıcısı. Bu senaryo, Azure App Service'te satır iş kolu uygulamaları oluşturmak istediğiniz ancak şirkete depolanacağı dizin verilerini, kuruluşunuza çalışabilir.

> [!NOTE]
> Azure uygulama hizmeti için başka bir Kurumsal kimlik doğrulama ve yetkilendirme seçeneklerine genel bakış için bkz: [Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulama](web-sites-authentication-authorization.md).
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Yapı
Azure App Service Web Apps aşağıdaki özelliklere sahip temel bir ASP.NET uygulamasına oluşturacak:

* AD FS karşı kullanıcıların kimliğini doğrular
* Kullanan `[Authorize]` farklı eylemler için Kullanıcıları yetkilendirmek için
* Visual Studio'da hata ayıklama hem de App Service Web Apps için yayımlama için statik yapılandırması (kez yapılandırma, hata ayıklama ve dilediğiniz zaman yayımlama)  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Ne gerekiyor
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:

* Şirket içi AD FS dağıtımı (Bu öğreticide kullanılan test laboratuvarı bir uçtan uca kılavuz için bkz: [Test laboratuvarı: Azure VM'de (yalnızca test için) AD FS ile tek başına STS](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))
* AD FS Yönetimi'nde güvenleri bağlı olan oluşturma izni taraf
* Visual Studio 2013 güncelleştirme 4 veya üstü
* [Azure SDK 2.8.1 ile](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) veya daha yenisi

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a>Örnek uygulama için iş şablonu kullanın
Bu öğreticideki örnek uygulama [WebApp WSFederation DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), Azure Active Directory ekibi tarafından oluşturulur. AD FS WS-Federasyon desteklediğinden, şablon olarak kolayca satır iş kolu uygulamaları oluşturmak için kullanabilirsiniz. Aşağıdaki özelliklere sahiptir:

* Kullanan [WS-Federasyon](http://msdn.microsoft.com/library/bb498017.aspx) bir şirket içi ile kimlik doğrulaması için AD FS dağıtımı
* Oturum açma ve oturum kapatma işlevi
* Kullanan [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (yerine Windows Identity Foundation), olan ASP.NET, gelecekteki ve kimlik doğrulaması ve yetkilendirme WIF daha ayarlamak çok daha kolaydır

<a name="bkmk_setup"></a>

## <a name="set-up-the-sample-application"></a>Örnek uygulama ayarlama
1. Kopyalama veya örnek çözümü indirin [WebApp WSFederation DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) yerel dizininize.
   
   > [!NOTE]
   > Kısmındaki yönergeleri [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) uygulama Azure Active Directory ile ayarlama gösterilmektedir. Ancak bu öğreticide, AD FS ile ayarlamak, bunun yerine burada verilen adımları izleyin.
   > 
   > 
2. Çözüm ve Controllers\AccountController.cs içinde açın **Çözüm Gezgini**.
   
   Kod yalnızca WS-Federasyon kullanarak kullanıcının kimliğini doğrulamak için bir kimlik doğrulaması sınaması sorunları görürsünüz. Tüm kimlik doğrulaması App_Start\Startup.Auth.cs içinde yapılandırılır.
3. App_Start\Startup.auth.cs açın. İçinde `ConfigureAuth` yöntemi, satıra dikkat edin:
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   OWIN dünyasında bu parçacığı gerçekten WS-Federasyon kimlik doğrulamasını yapılandırmak için gereken tam gereksinimdir. Bu, çok daha kolaydır ve burada Web.config XML ile dünyanın dört bir yanındaki yer eklenmiş WIF daha zarif olur. Gereksinim duyduğunuz yalnızca bağlı olan tarafın (RP) bilgilerdir tanımlayıcı ve AD FS hizmetinizin meta veri dosyası URL'si. Örnek aşağıda verilmiştir:
   
   * RP tanımlayıcısı:`https://contoso.com/MyLOBApp`
   * Meta veri adresi:`http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`
4. App_Start\Startup.auth.cs içinde aşağıdaki statik dize tanımları değiştirin:  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. Şimdi, Web.config dosyasında karşılık gelen değişiklikleri yapın. Web.config dosyasını açın ve aşağıdaki uygulama ayarları değiştirin:  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter the App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter the relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter the FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   İlgili ortamınıza bağlı anahtar değerlerini doldurun.
6. Hiçbir hata bulunmadığından emin olmak için uygulamayı oluşturun.

Bu kadar. Şimdi örnek uygulama AD FS ile çalışmak hazırdır. Hala bu uygulamayla AD FS'de daha sonra bir RP güven yapılandırmanız gerekir.

<a name="bkmk_deploy"></a>

## <a name="deploy-the-sample-application-to-azure-app-service-web-apps"></a>Azure App Service Web Apps için örnek uygulama dağıtma
Burada, hata ayıklama ortamı korurken App Service Web Apps bir web uygulaması için uygulama yayımlayın. AD FS ile RP güven olduğundan kimlik doğrulaması yine henüz çalışmıyor olması önce uygulamayı yayımlamak için deneyeceğimiz unutmayın. Bunu, Bununla birlikte, artık, RP güven daha sonra yapılandırmak için kullanabileceğiniz web uygulaması URL'si olabilir.

1. Projenize sağ tıklayın ve seçin **Yayımla**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. Seçin **Microsoft Azure uygulama hizmeti**.
3. Azure'da oturum henüz yoksa, tıklatın **oturum** ve oturum açmak için Azure aboneliğiniz için Microsoft hesabı kullanın.
4. Oturum açtıktan sonra tıklatın **yeni** bir web uygulaması oluşturma.
5. Tüm gerekli alanları doldurun. Şirket içi veri daha sonra bu web uygulaması için bir veritabanı oluşturmayın şekilde bağlanmak için adımıdır.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. **Oluştur**'a tıklayın. Web uygulaması oluşturulduktan sonra Web Yayımla iletişim kutusu açılır.
7. İçinde **hedef URL**, değiştirme **http** için **https**. URL'nin tamamı daha sonra kullanmak için bir metin düzenleyicisine kopyalayın. Ardından **Yayımla**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. Visual Studio'da açın **Web.Release.config** projenizdeki. Aşağıdaki XML öğesine Ekle `<configuration>` etiketi ve anahtar değeri, Yayımla web uygulamanızın URL'niz ile değiştirin.  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

İşiniz bittiğinde, projenizi, Visual Studio'da hata ayıklama ortamınız için diğeri Azure yayımlanan web uygulaması için yapılandırılmış iki RP tanımlayıcıları vardır. Her iki AD FS ortamlarda bir RP güven ayarlarsınız. Hata ayıklama sırasında Web.config uygulama ayarları yapmak için kullanılır, **hata ayıklama** AD FS ile yapılandırma çalışma. Ne zaman yayımlanan (varsayılan olarak, **sürüm** yapılandırma yayımlanır), dönüştürülmüş Web.config Web.Release.config uygulama ayarı değişiklikleri içeren yüklenir.

Azure için yayımlanan web uygulaması eklemek isterseniz oluşturabileceğiniz Azure hata ayıklama için ancak kendi özel Web.config dönüştürmesi ile hata ayıklama yapılandırmasını bir kopyasını (örneğin, (yani, gerekir karşıya kodunuzun yayımlanan web uygulamasında hata ayıklama simgeleri) hata ayıklayıcı Web.AzureDebug.config) Web.Release.config uygulama ayarlarından kullanır. Bu statik yapılandırması farklı ortamlar genelinde korumanıza olanak sağlar.

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a>Bağlı olan taraf Güvenleri'ni AD FS Yönetimi'nde yapılandırın
Şimdi örnek uygulamanızı kullanın ve gerçekte AD FS ile kimlik doğrulaması yapmak için önce AD FS Yönetimi RP güvende yapılandırmanız gerekir. İki ayrı RP güven, hata ayıklama ortamınız için diğeri yayımlanan web uygulamanız için ayarlamanız gerekir.

> [!NOTE]
> Aşağıdaki adımları hem de ortamlarınızın yinelemeniz emin olun.
> 
> 

1. AD FS sunucunuz üzerinde AD FS yönetim haklarına sahip kimlik bilgilerinizle oturum açın.
2. AD FS Yönetimi'ni açın. Sağ **AD FS\Trusted Relationships\Relying taraf güvenleri** seçip **bağlı olan taraf güveni Ekle**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. İçinde **veri kaynağı Seç** sayfasında **bağlı olan taraf verilerini elle girin**. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. İçinde **görünen adı belirt** sayfasında, uygulama için bir görünen ad yazın ve tıklayın **sonraki**.
5. İçinde **protokolü seçin** sayfasında, **sonraki**.
6. İçinde **sertifika Yapılandır** sayfasında, **sonraki**.
   
   > [!NOTE]
   > HTTPS zaten kullanıyor olmanız olduğundan, şifrelenen belirteçler isteğe bağlıdır. Gerçekten AD FS, bu sayfada belirteçlerinden şifrelemek isterseniz, kodunuzda belirteç şifre çözme mantığı de eklemeniz gerekir. Daha fazla bilgi için bkz: [OWIN WS-Federasyon ara yazılım yapılandırma ve kabul belirteçlerini el ile şifrelenmiş](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).
   > 
   > 
7. Sonraki adıma geçmeden önce Visual Studio projenizden tek parça bilgi gerekir. Proje Özellikleri'nde Not **SSL URL** uygulamanın. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. AD FS Yönetimi'nde, yeniden **URL Yapılandır** sayfasında **bağlı olan taraf güveni Ekleme Sihirbazı**seçin **WS-Federasyon Edilgen Protokolü desteğini etkinleştir** ve yazın Önceki adımda not ettiğiniz Visual Studio projenizi SSL URL'si. Ardından **İleri**'ye tıklayın.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > URL, kimlik doğrulaması başarılı olduktan sonra istemcinin gönderileceği yeri belirtir. Hata ayıklama ortamı için olmalıdır <code>https://localhost:&lt;port&gt;/</code>. Yayımlanan web uygulaması için web uygulaması URL'si olmalıdır.
   > 
   > 
9. İçinde **tanımlayıcıları yapılandırma** sayfasında, projenizin SSL URL zaten listelenmiş olduğunu doğrulayın ve tıklayın **sonraki**. Tıklatın **sonraki** tüm varsayılan seçimleri sihirbazla sonuna.
   
   > [!NOTE]
   > İçinde App_Start\Startup.auth.cs Visual Studio projenizin bu tanımlayıcı değeri karşı eşleştirildiği <code>WsFederationAuthenticationOptions.Wtrealm</code> federe kimlik doğrulaması sırasında. Varsayılan olarak, önceki adımdan uygulamanın URL RP tanımlayıcı olarak eklenir.
   > 
   > 
10. Artık, projenizi RP uygulaması için'de AD FS yapılandırma tamamladınız. Ardından, uygulamanızın gereksinim duyduğu talepleri göndermek için bu uygulamayı yapılandırın. **Talep kurallarını Düzenle** iletişim kutusu açıldığında varsayılan olarak, sihirbazın sonunda hemen başlatmak için. En az (şemalarda parantez içinde) aşağıdaki talep yapılandıralım:
    
    * Hydrate için ASP.NET tarafından kullanılan adı (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - `User.Identity.Name`.
    * Kuruluşunuzdaki kullanıcılar benzersiz şekilde tanımlamak için kullanılan kullanıcı asıl adı (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) -.
    * Grup üyelikleri rolleri (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - olarak kullanılabileceğini `[Authorize(Roles="role1, role2,...")]` denetleyicileri/Eylemler yetkilendirmek için düzenleme. Gerçekte, bu yaklaşım, çoğu kullanıcı rolü yetkilendirme için olmayabilir. AD kullanıcıları için güvenlik grupları yüzlerce aitse, rol talepleri SAML belirtecinde yüzlerce haline gelir. Alternatif bir yaklaşım, tek bir rol talep koşullu kullanıcının üyelik bağlı olarak belirli bir grubun göndermektir. Ancak, biz Bu öğretici için basit tut.
    * Kimliği (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) name - sahteciliğe karşı koruma doğrulama için kullanılabilir. Sahteciliğe karşı koruma doğrulama ile çalışması hakkında daha fazla bilgi için bkz: **iş işlevsellik ekleyen** bölümünü [ileAzureActiveDirectorykimlikdoğrulamasıişAzureuygulamasıoluştur](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).
    
    > [!NOTE]
    > Uygulamanız için yapılandırmanız gereken talep türleri, uygulamanızın gereksinimlerine göre belirlenir. Örneğin, Azure Active Directory uygulamaları (yani RP güvenleri) tarafından desteklenen talep listesi için bkz: [desteklenen belirteç ve talep türleri](http://msdn.microsoft.com/library/azure/dn195587.aspx).
    > 
    > 
11. Talep kurallarını Düzenle iletişim kutusunda tıklatın **Kuralı Ekle**.
12. Ad, UPN ve rol talepleri tıklatın ve ekran görüntüsü gösterildiği gibi yapılandırmak **son**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    Ardından, bir geçici ad kimliği talep adımları kullanarak gösterilen oluşturun [SAML onaylar adı tanımlayıcılarını](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
13. Tıklatın **Kuralı Ekle** yeniden.
14. Seçin **talepleri özel kural kullanarak Gönder** tıklatıp **sonraki**.
15. Aşağıdaki kural diline yapıştırın **özel kural** kutusunda, kuralın adını **başına oturum tanımlayıcısı** tıklatıp **son**.  
    
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
18. Kural (talep türü, oluşturduğunuz özel kural kullanarak) ekran görüntüsü gösterildiği gibi yapılandırmak ve tıklatın **son**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    Geçici ad kimliği talebi adımları hakkında ayrıntılı bilgi için bkz: [SAML onaylar adı tanımlayıcılarını](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
19. Tıklatın **Uygula** içinde **talep kurallarını Düzenle** iletişim. Aşağıdaki ekran görüntüsüne görünmelidir:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > Yeniden, hata ayıklama ortamı ve yayımlanan web uygulaması için bu adımları yineleyin emin olun.
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a>Uygulamanız için federe kimlik doğrulamasını Sına
Uygulamanızın kimlik doğrulaması mantığı AD FS karşı test etmek hazır olursunuz. My AD FS laboratuvar ortamında test grubu içinde Active Directory (AD) ait bir test kullanıcısı sahibim.

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

Hata ayıklayıcıda kimlik doğrulamasını sınamak için tüm yapmanız gereken şimdi türüdür `F5`. Yayımlanan web uygulaması kimlik doğrulama test etmek isterseniz, URL'ye gidin.

Web uygulaması yüklendikten sonra tıklatın **oturum**. Şimdi bir oturum açma iletişim kutusu veya AD FS tarafından seçilen kimlik doğrulama yöntemine bağlı olarak AD FS tarafından sunulan oturum açma sayfasına almanız gerekir. Internet Explorer 11 ne alıyorum aşağıda verilmiştir.

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

AD FS dağıtımı, AD etki alanındaki bir kullanıcının oturum oturum sonra yeniden giriş sayfası görmelisiniz **Merhaba, <User Name>!** köşede. İşte ne alıyorum.

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

Şu ana kadar aşağıdaki yollarla başarılı:

* Uygulamanız başarıyla AD FS ulaştı ve eşleşen bir RP tanımlayıcı AD FS veritabanında bulunamadı
* AD FS başarıyla bir AD kullanıcısının ve uygulamanın giriş sayfasına geri yönlendir doğrulaması
* Olarak AD FS kullanıcı adı köşesinde görüntülenir olgu belirtildiği gibi uygulamanızın ad talebini (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) başarıyla gönderildi. 

Adı talebi yoksa, görülen **Merhaba,!**. Görünümler/paylaşılan bakarsanız\_LoginPartial.cshtml, bulduğunuz bunu kullandığını `User.Identity.Name` kullanıcı adını görüntülemek için. Kimliği doğrulanmış kullanıcının adı talebi SAML belirtecinde kullanılabiliyorsa, daha önce belirtildiği gibi ASP.NET bu özelliğiyle hydrates. AD FS tarafından gönderilen tüm talepler görmek için bir kesme noktası Controllers\HomeController.cs içinde dizin eylem yönteminde yerleştirin. Kullanıcının kimliği doğrulandıktan sonra incelemek `System.Security.Claims.Current.Claims` koleksiyonu.

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a>Belirli denetleyicileri veya eylemler için Kullanıcıları yetkilendirmek
RP güven yapılandırmanıza grup üyeliklerini rol talepleri dahil olduğundan, artık doğrudan kullanabilmek için `[Authorize(Roles="...")]` decoration denetleyicileri ve eylemleri için. Oluştur-okunur-güncelleştir-Sil (CRUD) desende bir iş kolu satır uygulamasında, her eylem erişmek için belirli rolleri yetki verebilir. Şu an için yalnızca bu özellik varolan giriş denetleyicisinde çıkışı çalışacaktır.

1. Controllers\HomeController.cs açın.
2. İşaretleme `About` ve `Contact` eylem yöntemleri güvenlik kullanarak aşağıdaki kodu, benzer Grup Kimliği doğrulanmış kullanıcı üyeliği.  
   
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
   
    Ekledim beri **Test kullanıcı** için **Test grubu** my AD FS laboratuar ortamında ı Test grubu yetkilendirme üzerinde test etmek için kullanacağınız `About`. İçin `Contact`, negatif durumunda test edeceksiniz **Domain Admins**, hangi **Test kullanıcı** ait değil.
3. Hata ayıklayıcı boyutlandırın `F5` ve oturum açın ve ardından **hakkında**. Şimdi görüntüleme `~/About/Index` , kimliği doğrulanmış kullanıcının bu eylemi için yetkili olup olmadığını başarıyla, sayfa.
4. Şimdi **kişi**, hangi my durumda yetki **Test kullanıcısı** eylemi için. Ancak, tarayıcı sonunda bu iletiyi gösterir AD FS için yönlendirilir:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    AD FS sunucusunda Olay Görüntüleyicisi'nde bu hatayı araştırmak, bu özel durum iletisi görüntülenir:  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>The same client browser session has made '6' requests in the last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    Bu hatanın nedeni, bir kullanıcının rollerini yetkili olmadıkları zaman varsayılan olarak, MVC 401 Yetkisiz döndürdüğünden olmasıdır. Bu, kimlik sağlayıcısı (AD FS) için bir yeniden kimlik doğrulaması isteği tetikler. Kullanıcının kimliği zaten doğrulanmış olduğundan, AD FS sonra başka bir 401 sorunları, aynı sayfasına yeniden yönlendirme döngü oluşturma döndürür. AuthorizeAttribute'nın geçersiz kılar `HandleUnauthorizedRequest` yeniden yönlendirme döngü devam yerine anlamlı bir şey göstermek için basit bir mantık yöntemiyle.
5. Projenin AuthorizeAttribute.cs adlı bir dosya oluşturun ve aşağıdaki kodu yapıştırın.
   
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
   
    Geçersiz kılma kodu kimliği doğrulanmış ancak yetkisiz durumlarda HTTP 401 (yetkisiz) yerine HTTP 403 (Yasak) gönderir.
6. Hata ayıklayıcıda yeniden çalıştırmak `F5`. Tıklatarak **kişi** şimdi (paragrafta barındırabilir) daha bilgilendirici bir hata iletisi gösterir:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. Azure App Service Web Apps uygulamayı yeniden yayımlama ve canlı uygulama davranışını sınayın.

<a name="bkmk_data"></a>

## <a name="connect-to-on-premises-data"></a>Şirket içi verilere bağlanma
İş uygulamanızı Azure Active Directory yerine AD FS ile uygulamak istediğiniz bir kuruluş veri kapalı içi tutma ile uyumluluk sorunlarını nedenidir. Bu kullanma izni yok olduğundan web uygulamanızı azure'da şirket içi veritabanlarına erişim gerekir anlamına [SQL veritabanı](/services/sql-database/) web uygulamalarınız için veri katmanı olarak.

Azure App Service Web Apps iki yaklaşım erişirken şirket içi veritabanlarıyla destekler: [karma bağlantılar](../biztalk-services/integration-hybrid-connection-overview.md) ve [sanal ağlar](web-sites-integrate-with-vnet.md). Daha fazla bilgi için bkz: [kullanarak VNET tümleştirme ve karma bağlantılar Azure App Service Web Apps ile](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Ek kaynaklar
* [Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulaması](web-sites-authentication-authorization.md)
* [Azure Active Directory kimlik doğrulaması ile iş Azure uygulaması oluştur](web-sites-dotnet-lob-application-azure-ad.md)
* [Visual Studio 2013'te ASP.NET ile şirket içi Kurumsal kimlik doğrulama seçeneği (ADFS) kullanın](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [VS2013 Web projesi için Katana WIF geçirme](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [Active Directory Federasyon Hizmetleri'ne Genel Bakış](http://technet.microsoft.com/library/hh831502.aspx)
* [WS-Federasyon 1.1 belirtimini](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

