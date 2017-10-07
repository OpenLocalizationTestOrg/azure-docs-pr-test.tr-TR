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
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="0c71e-104">AD FS kimlik doğrulaması ile iş Azure uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="0c71e-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="0c71e-105">Bu makale size nasıl gösterir toocreate bir ASP.NET MVC satır iş kolu uygulama [Azure App Service](../app-service/app-service-value-prop-what-is.md) bir şirket içi kullanılarak [Active Directory Federasyon Hizmetleri](http://technet.microsoft.com/library/hh831502.aspx) hello kimlik sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="0c71e-105">This article shows you how toocreate an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as hello identity provider.</span></span> <span data-ttu-id="0c71e-106">Bu senaryo, toocreate--iş kolu uygulamaları Azure App Service'te istiyor ancak kuruluşunuzun dizin veri toobe şirkete depolanan ihtiyaç çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-106">This scenario can work when you want toocreate line-of-business applications in Azure App Service but your organization requires directory data toobe stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="0c71e-107">Azure App Service için hello başka bir Kurumsal kimlik doğrulama ve yetkilendirme seçeneklerine genel bakış için bkz: [Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulama](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="0c71e-107">For an overview of hello different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="0c71e-108">Yapı</span><span class="sxs-lookup"><span data-stu-id="0c71e-108">What you will build</span></span>
<span data-ttu-id="0c71e-109">Azure App Service Web Apps temel bir ASP.NET uygulamasında özellikler aşağıdaki hello ile oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="0c71e-109">You will build a basic ASP.NET application in Azure App Service Web Apps with hello following features:</span></span>

* <span data-ttu-id="0c71e-110">AD FS karşı kullanıcıların kimliğini doğrular</span><span class="sxs-lookup"><span data-stu-id="0c71e-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="0c71e-111">Kullanan `[Authorize]` tooauthorize kullanıcılar farklı eylemler için</span><span class="sxs-lookup"><span data-stu-id="0c71e-111">Uses `[Authorize]` tooauthorize users for different actions</span></span>
* <span data-ttu-id="0c71e-112">Visual Studio'da hata ayıklama hem de tooApp hizmeti Web uygulamaları yayımlamak için statik yapılandırması (kez yapılandırma, hata ayıklama ve dilediğiniz zaman yayımlama)</span><span class="sxs-lookup"><span data-stu-id="0c71e-112">Static configuration for both debugging in Visual Studio and publishing tooApp Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="0c71e-113">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="0c71e-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="0c71e-114">Bu öğreticiyi toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="0c71e-114">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="0c71e-115">Şirket içi AD FS dağıtımı (Bu öğreticide kullanılan hello test laboratuvarı bir uçtan uca kılavuz için bkz: [Test laboratuvarı: Azure VM'de (yalnızca test için) AD FS ile tek başına STS](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="0c71e-115">An on-premises AD FS deployment (for an end-to-end walkthrough of hello test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="0c71e-116">AD FS Yönetimi'nde izinleri toocreate bağlı olan taraf güvenleri</span><span class="sxs-lookup"><span data-stu-id="0c71e-116">Permissions toocreate relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="0c71e-117">Visual Studio 2013 güncelleştirme 4 veya üstü</span><span class="sxs-lookup"><span data-stu-id="0c71e-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="0c71e-118">[Azure SDK 2.8.1 ile](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="0c71e-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="0c71e-119">Örnek uygulama için iş şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="0c71e-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="0c71e-120">Bu öğreticideki örnek uygulama Hello [WebApp WSFederation DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), hello Azure Active Directory ekibi tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0c71e-120">hello sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by hello Azure Active Directory team.</span></span> <span data-ttu-id="0c71e-121">AD FS WS-Federasyon desteklediğinden, kolaylıkla bir şablon toocreate satır iş kolu uygulamaları olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c71e-121">Since AD FS supports WS-Federation, you can use it as a template toocreate line-of-business applications with ease.</span></span> <span data-ttu-id="0c71e-122">Özellikler aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="0c71e-122">It has hello following features:</span></span>

* <span data-ttu-id="0c71e-123">Kullanan [WS-Federasyon](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate bir şirket içi AD FS dağıtımı</span><span class="sxs-lookup"><span data-stu-id="0c71e-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="0c71e-124">Oturum açma ve oturum kapatma işlevi</span><span class="sxs-lookup"><span data-stu-id="0c71e-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="0c71e-125">Kullanan [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (yerine Windows Identity Foundation), hangi olduğu hello ASP.NET ve kimlik doğrulama ve yetkilendirme için daha kolay tooset WIF daha ileride</span><span class="sxs-lookup"><span data-stu-id="0c71e-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is hello future of ASP.NET and much simpler tooset up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a><span data-ttu-id="0c71e-126">Merhaba örnek uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="0c71e-126">Set up hello sample application</span></span>
1. <span data-ttu-id="0c71e-127">Kopyalama veya hello örnek çözümü indirin [WebApp WSFederation DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour yerel dizin.</span><span class="sxs-lookup"><span data-stu-id="0c71e-127">Clone or download hello sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0c71e-128">Merhaba yönergeleri [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) nasıl yapacağınızı hello uygulamasının Azure Active Directory ile tooset.</span><span class="sxs-lookup"><span data-stu-id="0c71e-128">hello instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how tooset up hello application with Azure Active Directory.</span></span> <span data-ttu-id="0c71e-129">Ancak bu öğreticide, AD FS ile ayarlamak, bunun yerine burada hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="0c71e-129">But in this tutorial, you set it up with AD FS, so follow hello steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="0c71e-130">Merhaba çözümü açın ve ardından Controllers\AccountController.cs hello açın **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-130">Open hello solution, and then open Controllers\AccountController.cs in hello **Solution Explorer**.</span></span>
   
   <span data-ttu-id="0c71e-131">Merhaba kod yalnızca WS-Federasyon kullanarak bir kimlik doğrulama sınaması tooauthenticate hello kullanıcı sorunları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0c71e-131">You will see that hello code simply issues an authentication challenge tooauthenticate hello user using WS-Federation.</span></span> <span data-ttu-id="0c71e-132">Tüm kimlik doğrulaması App_Start\Startup.Auth.cs içinde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="0c71e-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="0c71e-133">App_Start\Startup.auth.cs açın.</span><span class="sxs-lookup"><span data-stu-id="0c71e-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="0c71e-134">Merhaba, `ConfigureAuth` yöntemi, Not hello satırı:</span><span class="sxs-lookup"><span data-stu-id="0c71e-134">In hello `ConfigureAuth` method, note hello line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="0c71e-135">Merhaba OWIN dünyasında bu parçacığı aslında hello tooconfigure WS-Federasyon kimlik doğrulaması ihtiyacınız minimum tam adıdır.</span><span class="sxs-lookup"><span data-stu-id="0c71e-135">In hello OWIN world, this snippet is really hello bare minimum you need tooconfigure WS-Federation authentication.</span></span> <span data-ttu-id="0c71e-136">Bu, çok daha kolaydır ve burada Web.config XML ile Merhaba yer dünyanın dört bir yanındaki eklenmiş WIF daha zarif olur.</span><span class="sxs-lookup"><span data-stu-id="0c71e-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over hello place.</span></span> <span data-ttu-id="0c71e-137">gereksinim duyduğunuz bilgileri hello bağlı olan tarafın (RP) yalnızca hello ADFS hizmetinizin meta veri dosyası tanımlayıcısı ve başlangıç URL'si.</span><span class="sxs-lookup"><span data-stu-id="0c71e-137">hello only information you need is hello relying party's (RP) identifier and hello URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="0c71e-138">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0c71e-138">Here's an example:</span></span>
   
   * <span data-ttu-id="0c71e-139">RP tanımlayıcısı:`https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="0c71e-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="0c71e-140">Meta veri adresi:`http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="0c71e-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="0c71e-141">App_Start\Startup.auth.cs içinde statik bir dize tanımları aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0c71e-141">In App_Start\Startup.Auth.cs, change hello following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="0c71e-142">Şimdi, Web.config dosyasında hello karşılık gelen değişiklikleri yapın. Merhaba Web.config açın ve uygulama ayarlarını aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0c71e-142">Now, make hello corresponding changes in Web.config. Open hello Web.config and modify hello following app settings:</span></span>  
   
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
   
   <span data-ttu-id="0c71e-143">İlgili ortamınıza bağlı hello anahtar değerlerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="0c71e-143">Fill in hello key values based on your respective environment.</span></span>
6. <span data-ttu-id="0c71e-144">Merhaba uygulama toomake hiçbir hata bulunmadığından emin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0c71e-144">Build hello application toomake sure there are no errors.</span></span>

<span data-ttu-id="0c71e-145">Bu kadar.</span><span class="sxs-lookup"><span data-stu-id="0c71e-145">That's it.</span></span> <span data-ttu-id="0c71e-146">Merhaba örnek uygulaması, AD FS ile hazır toowork sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="0c71e-146">Now hello sample application is ready toowork with AD FS.</span></span> <span data-ttu-id="0c71e-147">Yine tooconfigure AD FS daha sonra bu uygulamada RP güvenle gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-147">You still need tooconfigure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a><span data-ttu-id="0c71e-148">Merhaba örnek uygulama tooAzure App Service Web Apps dağıtma</span><span class="sxs-lookup"><span data-stu-id="0c71e-148">Deploy hello sample application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="0c71e-149">Burada, hello hata ayıklama ortamı korurken hello uygulama tooa web uygulaması App Service Web Apps yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="0c71e-149">Here, you publish hello application tooa web app in App Service Web Apps while preserving hello debug environment.</span></span> <span data-ttu-id="0c71e-150">AD FS ile RP güven olduğundan kimlik doğrulaması yine henüz çalışmıyor olması önce toopublish Merhaba uygulaması oluşturacağız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0c71e-150">Note that you're going toopublish hello application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="0c71e-151">Bunu, Bununla birlikte, artık, tooconfigure hello RP güven daha sonra kullanabileceğiniz hello web uygulaması URL'si olabilir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-151">However, if you do it now you can have hello web app URL that you can use tooconfigure hello RP trust later.</span></span>

1. <span data-ttu-id="0c71e-152">Projenize sağ tıklayın ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-152">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="0c71e-153">Seçin **Microsoft Azure uygulama hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-153">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="0c71e-154">İçinde tooAzure kaydolduysanız henüz tıklatın **oturum** ve, Azure aboneliği toosign hello Microsoft hesabını kullanın.</span><span class="sxs-lookup"><span data-stu-id="0c71e-154">If you haven't signed in tooAzure, click **Sign In** and use hello Microsoft account for your Azure subscription toosign in.</span></span>
4. <span data-ttu-id="0c71e-155">Oturum açtıktan sonra tıklatın **yeni** toocreate bir web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0c71e-155">Once signed in, click **New** toocreate a web app.</span></span>
5. <span data-ttu-id="0c71e-156">Tüm gerekli alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="0c71e-156">Fill in all required fields.</span></span> <span data-ttu-id="0c71e-157">Tooconnect tooon içi veri daha sonra bu web uygulaması için bir veritabanı oluşturmayın şekilde adımıdır.</span><span class="sxs-lookup"><span data-stu-id="0c71e-157">You are going tooconnect tooon-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="0c71e-158">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0c71e-158">Click **Create**.</span></span> <span data-ttu-id="0c71e-159">Merhaba web uygulaması oluşturulduktan sonra hello Web Yayımla iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="0c71e-159">Once hello web app is created, hello Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="0c71e-160">İçinde **hedef URL**, değiştirme **http** çok**https**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-160">In **Destination URL**, change **http** too**https**.</span></span> <span data-ttu-id="0c71e-161">Hello tüm URL'yi tooa metin düzenleyici daha sonra kullanmak için kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0c71e-161">Copy hello entire URL tooa text editor for later use.</span></span> <span data-ttu-id="0c71e-162">Ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-162">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="0c71e-163">Visual Studio'da açın **Web.Release.config** projenizdeki.</span><span class="sxs-lookup"><span data-stu-id="0c71e-163">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="0c71e-164">XML hello aşağıdaki hello Ekle `<configuration>` etiketi ve hello anahtar değeri, Yayımla web uygulamanızın URL'si ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0c71e-164">Insert hello following XML into hello `<configuration>` tag, and replace hello key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="0c71e-165">İşiniz bittiğinde, projenizdeki Visual Studio'da hata ayıklama ortamınız için bir tane yapılandırılmış iki RP tanımlayıcı sahip ve Azure'da hello için bir tane yayımlanan web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0c71e-165">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for hello published web app in Azure.</span></span> <span data-ttu-id="0c71e-166">Her iki AD FS ortamlarda hello bir RP güven ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="0c71e-166">You will set up an RP trust for each of hello two environments in AD FS.</span></span> <span data-ttu-id="0c71e-167">Hata ayıklama sırasında hello uygulamanın Web.config dosyasında kullanılan toomake ayarlardır, **hata ayıklama** AD FS ile yapılandırma çalışma.</span><span class="sxs-lookup"><span data-stu-id="0c71e-167">During debugging, hello app settings in Web.config are used toomake your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="0c71e-168">Ne zaman yayımlanan (varsayılan olarak, hello **sürüm** yapılandırma yayımlanır), dönüştürülmüş Web.config Web.Release.config hello uygulama ayarı değişiklikleri içeren yüklenir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-168">When it's published (by default, hello **Release** configuration is published), a transformed Web.config is uploaded that incorporates hello app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="0c71e-169">Tooattach hello yayımlanan web uygulamasına istiyorsanız hello bir kopyasını oluşturabilirsiniz (yani, kodunuzun hello yayımlanan web uygulamasında hata ayıklama simgeleri yüklemelisiniz) Azure toohello hata ayıklayıcı, hata ayıklama yapılandırması hata ayıklama Azure ancak kendi özel Web.config ile dönüştürme ( Örneğin Web.AzureDebug.config) Web.Release.config hello uygulama ayarlarını kullanır. Bu, toomaintain statik yapılandırması hello farklı ortamlar genelinde sağlar.</span><span class="sxs-lookup"><span data-stu-id="0c71e-169">If you want tooattach hello published web app in Azure toohello debugger (i.e. you must upload debug symbols of your code in hello published web app), you can create a clone of hello Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses hello app settings from Web.Release.config. This allows you toomaintain a static configuration across hello different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="0c71e-170">Bağlı olan taraf Güvenleri'ni AD FS Yönetimi'nde yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0c71e-170">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="0c71e-171">Şimdi örnek uygulamanızı kullanın ve gerçekte AD FS ile kimlik doğrulaması yapmak için önce AD FS Yönetimi RP güvende tooconfigure gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-171">Now you need tooconfigure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="0c71e-172">İki ayrı RP güvenleri tooset, hata ayıklama ortamınız için diğeri yayımlanan web uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-172">You will need tooset up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="0c71e-173">Her iki ortamınız için aşağıdaki adımları hello yineleyin emin olun.</span><span class="sxs-lookup"><span data-stu-id="0c71e-173">Make sure that you repeat hello following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="0c71e-174">AD FS sunucunuz üzerinde yönetim hakları tooAD FS sahip kimlik bilgileriyle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0c71e-174">On your AD FS server, log in with credentials that have management rights tooAD FS.</span></span>
2. <span data-ttu-id="0c71e-175">AD FS Yönetimi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="0c71e-175">Open AD FS Management.</span></span> <span data-ttu-id="0c71e-176">Sağ **AD FS\Trusted Relationships\Relying taraf güvenleri** seçip **bağlı olan taraf güveni Ekle**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-176">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="0c71e-177">Merhaba, **veri kaynağı Seç** sayfasında **hello bağlı olan taraf verilerini elle girin**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-177">In hello **Select Data Source** page, select **Enter data about hello relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="0c71e-178">Merhaba, **görünen adı belirt** sayfasında Merhaba uygulaması için bir görünen ad yazın ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-178">In hello **Specify Display Name** page, type a display name for hello application and click **Next**.</span></span>
5. <span data-ttu-id="0c71e-179">Merhaba, **protokolü seçin** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-179">In hello **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="0c71e-180">Merhaba, **sertifika Yapılandır** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-180">In hello **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0c71e-181">HTTPS zaten kullanıyor olmanız olduğundan, şifrelenen belirteçler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0c71e-181">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="0c71e-182">AD FS, bu sayfada gelen tooencrypt belirteçleri gerçekten istiyorsanız, kodunuzda belirteç şifre çözme mantığı de eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-182">If you really want tooencrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="0c71e-183">Daha fazla bilgi için bkz: [OWIN WS-Federasyon ara yazılım yapılandırma ve kabul belirteçlerini el ile şifrelenmiş](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c71e-183">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="0c71e-184">Hello sonraki adıma geçmeden önce Visual Studio projenizden tek parça bilgi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-184">Before you move onto hello next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="0c71e-185">Merhaba Proje Özellikleri'nde hello Not **SSL URL** hello uygulamasının.</span><span class="sxs-lookup"><span data-stu-id="0c71e-185">In hello project properties, note hello **SSL URL** of hello application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="0c71e-186">AD FS yönetimi, hello edilene **URL Yapılandır** hello sayfasının **bağlı olan taraf güveni Ekleme Sihirbazı**seçin **hello WS-Federasyon Edilgen Protokolü desteğini etkinleştir** ve Merhaba önceki adımda not ettiğiniz Hello Visual Studio projenizi SSL URL'sini yazın.</span><span class="sxs-lookup"><span data-stu-id="0c71e-186">Back in AD FS Management, in hello **Configure URL** page of hello **Add Relying Party Trust Wizard**, select **Enable support for hello WS-Federation Passive protocol** and type in hello SSL URL of your Visual Studio project that you noted in hello previous step.</span></span> <span data-ttu-id="0c71e-187">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0c71e-187">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="0c71e-188">Burada toosend hello istemci kimlik doğrulama işleminden sonra başarılı URL'yi belirtir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-188">URL specifies where toosend hello client after authentication succeeds.</span></span> <span data-ttu-id="0c71e-189">Merhaba hata ayıklama ortamı için olmalıdır <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="0c71e-189">For hello debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="0c71e-190">Merhaba yayımlanan web uygulaması için başlangıç web uygulaması URL'si olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c71e-190">For hello published web app, it should be hello web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="0c71e-191">Merhaba, **tanımlayıcıları yapılandırma** sayfasında, projenizin SSL URL zaten listelenmiş olduğunu doğrulayın ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-191">In hello **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="0c71e-192">Tıklatın **sonraki** tüm yolu toohello varsayılan seçimleri hello sihirbazıyla sonuna hello.</span><span class="sxs-lookup"><span data-stu-id="0c71e-192">Click **Next** all hello way toohello end of hello wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0c71e-193">İçinde App_Start\Startup.auth.cs Visual Studio projenizin karşı hello değerini bu tanımlayıcı eşleştirildiği <code>WsFederationAuthenticationOptions.Wtrealm</code> federe kimlik doğrulaması sırasında.</span><span class="sxs-lookup"><span data-stu-id="0c71e-193">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against hello value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="0c71e-194">Varsayılan olarak, hello uygulamanın URL hello önceki adımdaki RP tanımlayıcı olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-194">By default, hello application's URL from hello previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="0c71e-195">Şimdi, AD FS'de hello RP uygulaması projeniz için yapılandırma tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="0c71e-195">You have now finished configuring hello RP application for your project in AD FS.</span></span> <span data-ttu-id="0c71e-196">Ardından, bu uygulama toosend yapılandırın hello uygulamanızın gereksinim duyduğu talepleri.</span><span class="sxs-lookup"><span data-stu-id="0c71e-196">Next, you configure this application toosend hello claims needed by your application.</span></span> <span data-ttu-id="0c71e-197">Merhaba **talep kurallarını Düzenle** iletişim kutusu açıldığında varsayılan olarak, hello hello sihirbazın sonunda hemen başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="0c71e-197">hello **Edit Claim Rules** dialog is opened by default for you at hello end of hello wizard so you can start immediately.</span></span> <span data-ttu-id="0c71e-198">Yapılandıralım en az hello aşağıdaki talep (şemalarda parantez içinde):</span><span class="sxs-lookup"><span data-stu-id="0c71e-198">Let's configure at least hello following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="0c71e-199">ASP.NET toohydrate tarafından kullanılan adı (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="0c71e-199">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET toohydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="0c71e-200">Kullanıcı asıl adı (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - kullanılan toouniquely hello kuruluşunuzdaki kullanıcılar tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="0c71e-200">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used toouniquely identify users in hello organization.</span></span>
    * <span data-ttu-id="0c71e-201">Grup üyelikleri rolleri (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - olarak kullanılabileceğini `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize denetleyicileri/eylemler.</span><span class="sxs-lookup"><span data-stu-id="0c71e-201">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize controllers/actions.</span></span> <span data-ttu-id="0c71e-202">Gerçekte, bu yaklaşım değil olması hello çoğu kullanıcı rolü yetkilendirme için.</span><span class="sxs-lookup"><span data-stu-id="0c71e-202">In reality, this approach may not be hello most performant for role authorization.</span></span> <span data-ttu-id="0c71e-203">AD kullanıcıları güvenlik gruplarının toohundreds aitse, rol talepleri hello SAML belirteci yüzlerce haline gelir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-203">If your AD users belong toohundreds of security groups, they become hundreds of role claims in hello SAML token.</span></span> <span data-ttu-id="0c71e-204">Alternatif bir yaklaşım, tek bir rol talep koşullu hello kullanıcının üyelik belirli bir gruba bağlı olarak toosend ' dir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-204">An alternative approach is toosend a single role claim conditionally depending on hello user's membership in a particular group.</span></span> <span data-ttu-id="0c71e-205">Ancak, biz Bu öğretici için basit tut.</span><span class="sxs-lookup"><span data-stu-id="0c71e-205">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="0c71e-206">Kimliği (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) name - sahteciliğe karşı koruma doğrulama için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-206">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="0c71e-207">Merhaba nasıl toomake çalışır sahteciliğe karşı koruma doğrulama ile ilgili daha fazla bilgi için bkz **iş işlevsellik ekleyen** bölümünü [Azure Active Directory kimlik doğrulaması ile iş Azure uygulaması oluştur ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="0c71e-207">For more information on how toomake it work with anti-forgery validation, see hello **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="0c71e-208">Merhaba talep, türleri, uygulamanızın uygulamanızın gereksinimlerinize göre belirlenir için tooconfigure gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-208">hello claim types you need tooconfigure for your application is determined by your application's needs.</span></span> <span data-ttu-id="0c71e-209">Örneğin, Azure Active Directory uygulamaları (yani RP güvenleri) tarafından desteklenen talep Hello listesi için bkz [desteklenen belirteç ve talep türleri](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c71e-209">For hello list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="0c71e-210">Merhaba talep kurallarını Düzenle iletişim kutusunda tıklatın **Kuralı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-210">In hello Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="0c71e-211">Merhaba ekran görüntüsünde gösterildiği gibi Hello adı, UPN ve rol talepleri yapılandırmak ve tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-211">Configure hello name, UPN, and role claims as shown in hello screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="0c71e-212">Ardından, bir geçici ad kimliği talep hello adımları kullanarak gösterilen oluşturun [SAML onaylar adı tanımlayıcılarını](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c71e-212">Next, you create a transient name ID claim using hello steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="0c71e-213">Tıklatın **Kuralı Ekle** yeniden.</span><span class="sxs-lookup"><span data-stu-id="0c71e-213">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="0c71e-214">Seçin **talepleri özel kural kullanarak Gönder** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-214">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="0c71e-215">Hello içine yapıştırma hello aşağıdaki kural dil **özel kural** kutusu, ad hello kuralı **başına oturum tanımlayıcısı** tıklatıp **son**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-215">Paste hello following rule language into hello **Custom rule** box, name hello rule **Per Session Identifier** and click **Finish**.</span></span>  
    
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
    
    <span data-ttu-id="0c71e-216">Özel kural bu ekran görüntüsüne görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="0c71e-216">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="0c71e-217">Tıklatın **Kuralı Ekle** yeniden.</span><span class="sxs-lookup"><span data-stu-id="0c71e-217">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="0c71e-218">Seçin **gelen talebi Dönüştür** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-218">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="0c71e-219">İ (Merhaba özel kuralında oluşturulan hello talep türü kullanarak) hello ekran görüntüsü gösterildiği gibi Hello kuralı yapılandırmak ve **son**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-219">Configure hello rule as shown in hello screenshot (using hello claim type you created in hello custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="0c71e-220">Merhaba geçici ad kimliği talebi hello adımları hakkında ayrıntılı bilgi için bkz: [SAML onaylar adı tanımlayıcılarını](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c71e-220">For detailed information on hello steps for hello transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="0c71e-221">Tıklatın **Uygula** hello içinde **talep kurallarını Düzenle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0c71e-221">Click **Apply** in hello **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="0c71e-222">Merhaba ekran aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="0c71e-222">It should now look like hello following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="0c71e-223">Yeniden, hata ayıklama ortamı ve yayımlanan web uygulaması için bu adımları yineleyin emin olun.</span><span class="sxs-lookup"><span data-stu-id="0c71e-223">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="0c71e-224">Uygulamanız için federe kimlik doğrulamasını Sına</span><span class="sxs-lookup"><span data-stu-id="0c71e-224">Test federated authentication for your application</span></span>
<span data-ttu-id="0c71e-225">Uygulamanızın kimlik doğrulaması mantığı AD FS karşı hazır tootest şunlardır.</span><span class="sxs-lookup"><span data-stu-id="0c71e-225">You are ready tootest your application's authentication logic against AD FS.</span></span> <span data-ttu-id="0c71e-226">My AD FS laboratuar ortamında tooa test grubu içinde Active Directory (AD) ait bir test kullanıcısı sahibim.</span><span class="sxs-lookup"><span data-stu-id="0c71e-226">In my AD FS lab environment, I have a test user that belongs tooa test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="0c71e-227">hata ayıklayıcısında Merhaba, tüm yapmanız gereken toodo şimdi tootest kimlik doğrulaması türüdür `F5`.</span><span class="sxs-lookup"><span data-stu-id="0c71e-227">tootest authentication in hello debugger, all you need toodo now is type `F5`.</span></span> <span data-ttu-id="0c71e-228">Merhaba yayımlanan web uygulamasında tootest kimlik doğrulamasını istiyorsanız, toohello URL'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="0c71e-228">If you want tootest authentication in hello published web app, navigate toohello URL.</span></span>

<span data-ttu-id="0c71e-229">Merhaba web uygulaması yüklendikten sonra tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-229">After hello web application loads, click **Sign In**.</span></span> <span data-ttu-id="0c71e-230">AD FS tarafından seçilen hello kimlik doğrulama yöntemine bağlı olarak AD FS tarafından sunulan ya da bir oturum açma iletişim kutusu veya hello oturum açma sayfası artık almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-230">You should now get either a login dialog or hello login page served by AD FS, depending on hello authentication method chosen by AD FS.</span></span> <span data-ttu-id="0c71e-231">Internet Explorer 11 ne alıyorum aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-231">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="0c71e-232">Merhaba AD FS dağıtım hello AD etki alanındaki bir kullanıcının oturum oturum sonra yeniden hello giriş sayfası görmelisiniz **Hello <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="0c71e-232">Once you log in with a user in hello AD domain of hello AD FS deployment, you should now see hello homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="0c71e-233">Merhaba köşede.</span><span class="sxs-lookup"><span data-stu-id="0c71e-233">in hello corner.</span></span> <span data-ttu-id="0c71e-234">İşte ne alıyorum.</span><span class="sxs-lookup"><span data-stu-id="0c71e-234">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="0c71e-235">Şu ana kadar yol aşağıdaki hello başarılı:</span><span class="sxs-lookup"><span data-stu-id="0c71e-235">So far, you've succeeded in hello following ways:</span></span>

* <span data-ttu-id="0c71e-236">Uygulamanız başarıyla AD FS ulaştı ve eşleşen bir RP tanımlayıcı hello AD FS veritabanı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="0c71e-236">Your application has successfully reached AD FS and a matching RP identifier is found in hello AD FS database</span></span>
* <span data-ttu-id="0c71e-237">AD FS başarıyla bir AD kullanıcısının ve yeniden yönlendirme toohello uygulamanın giriş sayfası geri doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0c71e-237">AD FS has successfully authenticated an AD user and redirect you back toohello application's homepage</span></span>
* <span data-ttu-id="0c71e-238">Merhaba olgusu hello kullanıcı belirtildiği gibi başarıyla gönderilen hello adı olarak AD FS talep (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour uygulama adı, hello köşesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-238">AD FS as successfully sent hello name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour application, as indicated by hello fact that hello user name is displayed in hello corner.</span></span> 

<span data-ttu-id="0c71e-239">Merhaba adı talebi yoksa, görülen **Hello!**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-239">If hello name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="0c71e-240">Görünümler/paylaşılan bakarsanız\_LoginPartial.cshtml, bulduğunuz bunu kullandığını `User.Identity.Name` toodisplay hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="0c71e-240">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` toodisplay hello user name.</span></span> <span data-ttu-id="0c71e-241">Kullanıcı hello SAML belirtecinde kullanılabilir talep kimliği doğrulanmış Merhaba Hello adı, daha önce belirtildiği gibi ASP.NET bu özelliğiyle hydrates.</span><span class="sxs-lookup"><span data-stu-id="0c71e-241">As mentioned previously, if hello name claim of hello authenticated user is available in hello SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="0c71e-242">Tüm hello toosee, AD FS, bir kesme noktası Controllers\HomeController.cs içinde hello yerleştirme tarafından dizin eylem yöntemine gönderilen talepleri.</span><span class="sxs-lookup"><span data-stu-id="0c71e-242">toosee all hello claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in hello Index action method.</span></span> <span data-ttu-id="0c71e-243">Merhaba kullanıcının kimliği doğrulandıktan sonra hello incelemek `System.Security.Claims.Current.Claims` koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="0c71e-243">After hello user is authenticated, inspect hello `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="0c71e-244">Belirli denetleyicileri veya eylemler için Kullanıcıları yetkilendirmek</span><span class="sxs-lookup"><span data-stu-id="0c71e-244">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="0c71e-245">RP güven yapılandırmanıza grup üyeliklerini rol talepleri dahil olduğundan, artık doğrudan hello kullanabilmek için `[Authorize(Roles="...")]` decoration denetleyicileri ve eylemleri için.</span><span class="sxs-lookup"><span data-stu-id="0c71e-245">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in hello `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="0c71e-246">Merhaba Oluştur-okunur-güncelleştir-Sil (CRUD) desen ile bir iş kolu satır uygulamasında, her eylem belirli rolleri tooaccess yetki verebilir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-246">In a line-of-business application with hello Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles tooaccess each action.</span></span> <span data-ttu-id="0c71e-247">Şu an için yalnızca bu özellik hello varolan giriş denetleyicisinde çıkışı çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="0c71e-247">For now, you will just try out this feature on hello existing Home controller.</span></span>

1. <span data-ttu-id="0c71e-248">Controllers\HomeController.cs açın.</span><span class="sxs-lookup"><span data-stu-id="0c71e-248">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="0c71e-249">Merhaba tasarlamanız `About` ve `Contact` koddan, kimliği doğrulanmış kullanıcının güvenlik grup üyeliklerini kullanarak eylem yöntemleri benzer toohello.</span><span class="sxs-lookup"><span data-stu-id="0c71e-249">Decorate hello `About` and `Contact` action methods similar toohello following code, using security group memberships that your authenticated user has.</span></span>  
   
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
   
    <span data-ttu-id="0c71e-250">Ekledim beri **Test kullanıcısı** çok**Test grubu** my AD FS laboratuvar ortamında Test grubu tootest yetkilendirme üzerinde kullanmam `About`.</span><span class="sxs-lookup"><span data-stu-id="0c71e-250">Since I added **Test User** too**Test Group** in my AD FS lab environment, I'll use Test Group tootest authorization on `About`.</span></span> <span data-ttu-id="0c71e-251">İçin `Contact`, hello negatif durumunun test edeceksiniz **Domain Admins**, toowhich **Test kullanıcı** ait değil.</span><span class="sxs-lookup"><span data-stu-id="0c71e-251">For `Contact`, I'll test hello negative case of **Domain Admins**, toowhich **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="0c71e-252">Merhaba hata ayıklayıcı boyutlandırın `F5` ve oturum açın ve ardından **hakkında**.</span><span class="sxs-lookup"><span data-stu-id="0c71e-252">Start hello debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="0c71e-253">Merhaba şimdi görüntüleme `~/About/Index` , kimliği doğrulanmış kullanıcının bu eylemi için yetkili olup olmadığını başarıyla, sayfa.</span><span class="sxs-lookup"><span data-stu-id="0c71e-253">You should now be viewing hello `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="0c71e-254">Şimdi **kişi**, hangi my durumda yetki **Test kullanıcısı** hello eylemi için.</span><span class="sxs-lookup"><span data-stu-id="0c71e-254">Now click **Contact**, which in my case should not authorize **Test User** for hello action.</span></span> <span data-ttu-id="0c71e-255">Ancak, bu iletiyi sonunda gösterir yeniden yönlendirilen tooAD FS hello tarayıcısıdır:</span><span class="sxs-lookup"><span data-stu-id="0c71e-255">However, hello browser is redirected tooAD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="0c71e-256">Bu hatada Olay Görüntüleyicisi'nde hello AD FS sunucu araştırmak, bu özel durum iletisi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="0c71e-256">If you investigate this error in Event Viewer on hello AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="0c71e-257">Bu hatanın nedeni Hello bir kullanıcının rollerini yetkili olmadıkları zaman varsayılan olarak, MVC 401 Yetkisiz döndürmesidir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-257">hello reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="0c71e-258">Bir yeniden kimlik doğrulaması isteği tooyour kimlik sağlayıcısı'nı (AD FS) tetikler.</span><span class="sxs-lookup"><span data-stu-id="0c71e-258">This triggers a reauthentication request tooyour identity provider (AD FS).</span></span> <span data-ttu-id="0c71e-259">Merhaba kullanıcının kimliği zaten doğrulanmış olduğundan, AD FS toohello döndüren bir yeniden yönlendirme döngü oluşturma başka bir 401 sorunları aynı sayfa.</span><span class="sxs-lookup"><span data-stu-id="0c71e-259">Since hello user is already authenticated, AD FS returns toohello same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="0c71e-260">AuthorizeAttribute'nın geçersiz kılar `HandleUnauthorizedRequest` basit bir mantık tooshow yöntemiyle devam ediliyor hello yeniden yönlendirme döngüsü yerine mantıklı bir şey.</span><span class="sxs-lookup"><span data-stu-id="0c71e-260">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic tooshow something that makes sense instead of continuing hello redirect loop.</span></span>
5. <span data-ttu-id="0c71e-261">Merhaba projesinde AuthorizeAttribute.cs ve kod içine aşağıdaki Yapıştır hello adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0c71e-261">Create a file in hello project called AuthorizeAttribute.cs, and paste hello following code into it.</span></span>
   
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
   
    <span data-ttu-id="0c71e-262">Merhaba kimliği doğrulanmış ancak yetkisiz durumlarda kod gönderir (Yasak) HTTP 403 HTTP 401 (yetkisiz) yerine geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="0c71e-262">hello override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="0c71e-263">Merhaba hata ayıklayıcısı yeniden Çalıştır `F5`.</span><span class="sxs-lookup"><span data-stu-id="0c71e-263">Run hello debugger again with `F5`.</span></span> <span data-ttu-id="0c71e-264">Tıklatarak **kişi** şimdi (paragrafta barındırabilir) daha bilgilendirici bir hata iletisi gösterir:</span><span class="sxs-lookup"><span data-stu-id="0c71e-264">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="0c71e-265">Merhaba uygulama tooAzure App Service Web Apps yeniden yayımlamanız ve hello Canlı uygulamasının başlangıç davranışını sınayın.</span><span class="sxs-lookup"><span data-stu-id="0c71e-265">Publish hello application tooAzure App Service Web Apps again, and test hello behavior of hello live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a><span data-ttu-id="0c71e-266">Tooon içi verilere bağlanma</span><span class="sxs-lookup"><span data-stu-id="0c71e-266">Connect tooon-premises data</span></span>
<span data-ttu-id="0c71e-267">İş uygulamanızı Azure Active Directory yerine AD FS ile tooimplement istersiniz, bir kuruluşun veri kapalı içi tutma ile uyumluluk sorunlarını nedenidir.</span><span class="sxs-lookup"><span data-stu-id="0c71e-267">A reason that you would want tooimplement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="0c71e-268">Bu toouse izin verilmiyor beri web uygulamanızı azure'da şirket içi veritabanlarına erişim gerekir anlamına [SQL veritabanı](/services/sql-database/) hello web uygulamalarınız için veri katmanı olarak.</span><span class="sxs-lookup"><span data-stu-id="0c71e-268">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed toouse [SQL Database](/services/sql-database/) as hello data tier for your web apps.</span></span>

<span data-ttu-id="0c71e-269">Azure App Service Web Apps iki yaklaşım erişirken şirket içi veritabanlarıyla destekler: [karma bağlantılar](../biztalk-services/integration-hybrid-connection-overview.md) ve [sanal ağlar](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="0c71e-269">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="0c71e-270">Daha fazla bilgi için bkz: [kullanarak VNET tümleştirme ve karma bağlantılar Azure App Service Web Apps ile](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="0c71e-270">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="0c71e-271">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0c71e-271">Further resources</span></span>
* [<span data-ttu-id="0c71e-272">Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0c71e-272">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="0c71e-273">Azure Active Directory kimlik doğrulaması ile iş Azure uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="0c71e-273">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="0c71e-274">Visual Studio 2013'te Hello ASP.NET ile şirket içi Kurumsal kimlik doğrulama seçeneği (ADFS) kullanın</span><span class="sxs-lookup"><span data-stu-id="0c71e-274">Use hello On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="0c71e-275">Gelen VS2013 Web projesi WIF tooKatana geçirme</span><span class="sxs-lookup"><span data-stu-id="0c71e-275">Migrate a VS2013 Web Project From WIF tooKatana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="0c71e-276">Active Directory Federasyon Hizmetleri'ne Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0c71e-276">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="0c71e-277">WS-Federasyon 1.1 belirtimini</span><span class="sxs-lookup"><span data-stu-id="0c71e-277">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

