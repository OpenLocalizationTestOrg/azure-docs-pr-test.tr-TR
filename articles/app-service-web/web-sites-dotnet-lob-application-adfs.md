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
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="40c98-104">AD FS kimlik doğrulaması ile iş Azure uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="40c98-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="40c98-105">Bu makalede, bir ASP.NET MVC satır iş kolu uygulamasının nasıl oluşturulacağını gösterir [Azure App Service](../app-service/app-service-value-prop-what-is.md) bir şirket içi kullanılarak [Active Directory Federasyon Hizmetleri](http://technet.microsoft.com/library/hh831502.aspx) kimlik sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="40c98-105">This article shows you how to create an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as the identity provider.</span></span> <span data-ttu-id="40c98-106">Bu senaryo, Azure App Service'te satır iş kolu uygulamaları oluşturmak istediğiniz ancak şirkete depolanacağı dizin verilerini, kuruluşunuza çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="40c98-106">This scenario can work when you want to create line-of-business applications in Azure App Service but your organization requires directory data to be stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="40c98-107">Azure uygulama hizmeti için başka bir Kurumsal kimlik doğrulama ve yetkilendirme seçeneklerine genel bakış için bkz: [Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulama](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="40c98-107">For an overview of the different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="40c98-108">Yapı</span><span class="sxs-lookup"><span data-stu-id="40c98-108">What you will build</span></span>
<span data-ttu-id="40c98-109">Azure App Service Web Apps aşağıdaki özelliklere sahip temel bir ASP.NET uygulamasına oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="40c98-109">You will build a basic ASP.NET application in Azure App Service Web Apps with the following features:</span></span>

* <span data-ttu-id="40c98-110">AD FS karşı kullanıcıların kimliğini doğrular</span><span class="sxs-lookup"><span data-stu-id="40c98-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="40c98-111">Kullanan `[Authorize]` farklı eylemler için Kullanıcıları yetkilendirmek için</span><span class="sxs-lookup"><span data-stu-id="40c98-111">Uses `[Authorize]` to authorize users for different actions</span></span>
* <span data-ttu-id="40c98-112">Visual Studio'da hata ayıklama hem de App Service Web Apps için yayımlama için statik yapılandırması (kez yapılandırma, hata ayıklama ve dilediğiniz zaman yayımlama)</span><span class="sxs-lookup"><span data-stu-id="40c98-112">Static configuration for both debugging in Visual Studio and publishing to App Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="40c98-113">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="40c98-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="40c98-114">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="40c98-114">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="40c98-115">Şirket içi AD FS dağıtımı (Bu öğreticide kullanılan test laboratuvarı bir uçtan uca kılavuz için bkz: [Test laboratuvarı: Azure VM'de (yalnızca test için) AD FS ile tek başına STS](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="40c98-115">An on-premises AD FS deployment (for an end-to-end walkthrough of the test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="40c98-116">AD FS Yönetimi'nde güvenleri bağlı olan oluşturma izni taraf</span><span class="sxs-lookup"><span data-stu-id="40c98-116">Permissions to create relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="40c98-117">Visual Studio 2013 güncelleştirme 4 veya üstü</span><span class="sxs-lookup"><span data-stu-id="40c98-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="40c98-118">[Azure SDK 2.8.1 ile](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="40c98-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="40c98-119">Örnek uygulama için iş şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="40c98-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="40c98-120">Bu öğreticideki örnek uygulama [WebApp WSFederation DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), Azure Active Directory ekibi tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="40c98-120">The sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by the Azure Active Directory team.</span></span> <span data-ttu-id="40c98-121">AD FS WS-Federasyon desteklediğinden, şablon olarak kolayca satır iş kolu uygulamaları oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c98-121">Since AD FS supports WS-Federation, you can use it as a template to create line-of-business applications with ease.</span></span> <span data-ttu-id="40c98-122">Aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="40c98-122">It has the following features:</span></span>

* <span data-ttu-id="40c98-123">Kullanan [WS-Federasyon](http://msdn.microsoft.com/library/bb498017.aspx) bir şirket içi ile kimlik doğrulaması için AD FS dağıtımı</span><span class="sxs-lookup"><span data-stu-id="40c98-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) to authenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="40c98-124">Oturum açma ve oturum kapatma işlevi</span><span class="sxs-lookup"><span data-stu-id="40c98-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="40c98-125">Kullanan [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (yerine Windows Identity Foundation), olan ASP.NET, gelecekteki ve kimlik doğrulaması ve yetkilendirme WIF daha ayarlamak çok daha kolaydır</span><span class="sxs-lookup"><span data-stu-id="40c98-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is the future of ASP.NET and much simpler to set up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-the-sample-application"></a><span data-ttu-id="40c98-126">Örnek uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="40c98-126">Set up the sample application</span></span>
1. <span data-ttu-id="40c98-127">Kopyalama veya örnek çözümü indirin [WebApp WSFederation DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) yerel dizininize.</span><span class="sxs-lookup"><span data-stu-id="40c98-127">Clone or download the sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) to your local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="40c98-128">Kısmındaki yönergeleri [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) uygulama Azure Active Directory ile ayarlama gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="40c98-128">The instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how to set up the application with Azure Active Directory.</span></span> <span data-ttu-id="40c98-129">Ancak bu öğreticide, AD FS ile ayarlamak, bunun yerine burada verilen adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="40c98-129">But in this tutorial, you set it up with AD FS, so follow the steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="40c98-130">Çözüm ve Controllers\AccountController.cs içinde açın **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="40c98-130">Open the solution, and then open Controllers\AccountController.cs in the **Solution Explorer**.</span></span>
   
   <span data-ttu-id="40c98-131">Kod yalnızca WS-Federasyon kullanarak kullanıcının kimliğini doğrulamak için bir kimlik doğrulaması sınaması sorunları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="40c98-131">You will see that the code simply issues an authentication challenge to authenticate the user using WS-Federation.</span></span> <span data-ttu-id="40c98-132">Tüm kimlik doğrulaması App_Start\Startup.Auth.cs içinde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="40c98-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="40c98-133">App_Start\Startup.auth.cs açın.</span><span class="sxs-lookup"><span data-stu-id="40c98-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="40c98-134">İçinde `ConfigureAuth` yöntemi, satıra dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="40c98-134">In the `ConfigureAuth` method, note the line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="40c98-135">OWIN dünyasında bu parçacığı gerçekten WS-Federasyon kimlik doğrulamasını yapılandırmak için gereken tam gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="40c98-135">In the OWIN world, this snippet is really the bare minimum you need to configure WS-Federation authentication.</span></span> <span data-ttu-id="40c98-136">Bu, çok daha kolaydır ve burada Web.config XML ile dünyanın dört bir yanındaki yer eklenmiş WIF daha zarif olur.</span><span class="sxs-lookup"><span data-stu-id="40c98-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over the place.</span></span> <span data-ttu-id="40c98-137">Gereksinim duyduğunuz yalnızca bağlı olan tarafın (RP) bilgilerdir tanımlayıcı ve AD FS hizmetinizin meta veri dosyası URL'si.</span><span class="sxs-lookup"><span data-stu-id="40c98-137">The only information you need is the relying party's (RP) identifier and the URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="40c98-138">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="40c98-138">Here's an example:</span></span>
   
   * <span data-ttu-id="40c98-139">RP tanımlayıcısı:`https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="40c98-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="40c98-140">Meta veri adresi:`http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="40c98-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="40c98-141">App_Start\Startup.auth.cs içinde aşağıdaki statik dize tanımları değiştirin:</span><span class="sxs-lookup"><span data-stu-id="40c98-141">In App_Start\Startup.Auth.cs, change the following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="40c98-142">Şimdi, Web.config dosyasında karşılık gelen değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="40c98-142">Now, make the corresponding changes in Web.config.</span></span> <span data-ttu-id="40c98-143">Web.config dosyasını açın ve aşağıdaki uygulama ayarları değiştirin:</span><span class="sxs-lookup"><span data-stu-id="40c98-143">Open the Web.config and modify the following app settings:</span></span>  
   
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
   
   <span data-ttu-id="40c98-144">İlgili ortamınıza bağlı anahtar değerlerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="40c98-144">Fill in the key values based on your respective environment.</span></span>
6. <span data-ttu-id="40c98-145">Hiçbir hata bulunmadığından emin olmak için uygulamayı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="40c98-145">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="40c98-146">Bu kadar.</span><span class="sxs-lookup"><span data-stu-id="40c98-146">That's it.</span></span> <span data-ttu-id="40c98-147">Şimdi örnek uygulama AD FS ile çalışmak hazırdır.</span><span class="sxs-lookup"><span data-stu-id="40c98-147">Now the sample application is ready to work with AD FS.</span></span> <span data-ttu-id="40c98-148">Hala bu uygulamayla AD FS'de daha sonra bir RP güven yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="40c98-148">You still need to configure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-the-sample-application-to-azure-app-service-web-apps"></a><span data-ttu-id="40c98-149">Azure App Service Web Apps için örnek uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="40c98-149">Deploy the sample application to Azure App Service Web Apps</span></span>
<span data-ttu-id="40c98-150">Burada, hata ayıklama ortamı korurken App Service Web Apps bir web uygulaması için uygulama yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="40c98-150">Here, you publish the application to a web app in App Service Web Apps while preserving the debug environment.</span></span> <span data-ttu-id="40c98-151">AD FS ile RP güven olduğundan kimlik doğrulaması yine henüz çalışmıyor olması önce uygulamayı yayımlamak için deneyeceğimiz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="40c98-151">Note that you're going to publish the application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="40c98-152">Bunu, Bununla birlikte, artık, RP güven daha sonra yapılandırmak için kullanabileceğiniz web uygulaması URL'si olabilir.</span><span class="sxs-lookup"><span data-stu-id="40c98-152">However, if you do it now you can have the web app URL that you can use to configure the RP trust later.</span></span>

1. <span data-ttu-id="40c98-153">Projenize sağ tıklayın ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="40c98-153">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="40c98-154">Seçin **Microsoft Azure uygulama hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="40c98-154">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="40c98-155">Azure'da oturum henüz yoksa, tıklatın **oturum** ve oturum açmak için Azure aboneliğiniz için Microsoft hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="40c98-155">If you haven't signed in to Azure, click **Sign In** and use the Microsoft account for your Azure subscription to sign in.</span></span>
4. <span data-ttu-id="40c98-156">Oturum açtıktan sonra tıklatın **yeni** bir web uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="40c98-156">Once signed in, click **New** to create a web app.</span></span>
5. <span data-ttu-id="40c98-157">Tüm gerekli alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="40c98-157">Fill in all required fields.</span></span> <span data-ttu-id="40c98-158">Şirket içi veri daha sonra bu web uygulaması için bir veritabanı oluşturmayın şekilde bağlanmak için adımıdır.</span><span class="sxs-lookup"><span data-stu-id="40c98-158">You are going to connect to on-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="40c98-159">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="40c98-159">Click **Create**.</span></span> <span data-ttu-id="40c98-160">Web uygulaması oluşturulduktan sonra Web Yayımla iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="40c98-160">Once the web app is created, the Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="40c98-161">İçinde **hedef URL**, değiştirme **http** için **https**.</span><span class="sxs-lookup"><span data-stu-id="40c98-161">In **Destination URL**, change **http** to **https**.</span></span> <span data-ttu-id="40c98-162">URL'nin tamamı daha sonra kullanmak için bir metin düzenleyicisine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="40c98-162">Copy the entire URL to a text editor for later use.</span></span> <span data-ttu-id="40c98-163">Ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="40c98-163">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="40c98-164">Visual Studio'da açın **Web.Release.config** projenizdeki.</span><span class="sxs-lookup"><span data-stu-id="40c98-164">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="40c98-165">Aşağıdaki XML öğesine Ekle `<configuration>` etiketi ve anahtar değeri, Yayımla web uygulamanızın URL'niz ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="40c98-165">Insert the following XML into the `<configuration>` tag, and replace the key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="40c98-166">İşiniz bittiğinde, projenizi, Visual Studio'da hata ayıklama ortamınız için diğeri Azure yayımlanan web uygulaması için yapılandırılmış iki RP tanımlayıcıları vardır.</span><span class="sxs-lookup"><span data-stu-id="40c98-166">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for the published web app in Azure.</span></span> <span data-ttu-id="40c98-167">Her iki AD FS ortamlarda bir RP güven ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="40c98-167">You will set up an RP trust for each of the two environments in AD FS.</span></span> <span data-ttu-id="40c98-168">Hata ayıklama sırasında Web.config uygulama ayarları yapmak için kullanılır, **hata ayıklama** AD FS ile yapılandırma çalışma.</span><span class="sxs-lookup"><span data-stu-id="40c98-168">During debugging, the app settings in Web.config are used to make your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="40c98-169">Ne zaman yayımlanan (varsayılan olarak, **sürüm** yapılandırma yayımlanır), dönüştürülmüş Web.config Web.Release.config uygulama ayarı değişiklikleri içeren yüklenir.</span><span class="sxs-lookup"><span data-stu-id="40c98-169">When it's published (by default, the **Release** configuration is published), a transformed Web.config is uploaded that incorporates the app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="40c98-170">Azure için yayımlanan web uygulaması eklemek isterseniz oluşturabileceğiniz Azure hata ayıklama için ancak kendi özel Web.config dönüştürmesi ile hata ayıklama yapılandırmasını bir kopyasını (örneğin, (yani, gerekir karşıya kodunuzun yayımlanan web uygulamasında hata ayıklama simgeleri) hata ayıklayıcı Web.AzureDebug.config) Web.Release.config uygulama ayarlarından kullanır.</span><span class="sxs-lookup"><span data-stu-id="40c98-170">If you want to attach the published web app in Azure to the debugger (i.e. you must upload debug symbols of your code in the published web app), you can create a clone of the Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses the app settings from Web.Release.config.</span></span> <span data-ttu-id="40c98-171">Bu statik yapılandırması farklı ortamlar genelinde korumanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="40c98-171">This allows you to maintain a static configuration across the different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="40c98-172">Bağlı olan taraf Güvenleri'ni AD FS Yönetimi'nde yapılandırın</span><span class="sxs-lookup"><span data-stu-id="40c98-172">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="40c98-173">Şimdi örnek uygulamanızı kullanın ve gerçekte AD FS ile kimlik doğrulaması yapmak için önce AD FS Yönetimi RP güvende yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="40c98-173">Now you need to configure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="40c98-174">İki ayrı RP güven, hata ayıklama ortamınız için diğeri yayımlanan web uygulamanız için ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="40c98-174">You will need to set up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="40c98-175">Aşağıdaki adımları hem de ortamlarınızın yinelemeniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="40c98-175">Make sure that you repeat the following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="40c98-176">AD FS sunucunuz üzerinde AD FS yönetim haklarına sahip kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="40c98-176">On your AD FS server, log in with credentials that have management rights to AD FS.</span></span>
2. <span data-ttu-id="40c98-177">AD FS Yönetimi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="40c98-177">Open AD FS Management.</span></span> <span data-ttu-id="40c98-178">Sağ **AD FS\Trusted Relationships\Relying taraf güvenleri** seçip **bağlı olan taraf güveni Ekle**.</span><span class="sxs-lookup"><span data-stu-id="40c98-178">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="40c98-179">İçinde **veri kaynağı Seç** sayfasında **bağlı olan taraf verilerini elle girin**.</span><span class="sxs-lookup"><span data-stu-id="40c98-179">In the **Select Data Source** page, select **Enter data about the relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="40c98-180">İçinde **görünen adı belirt** sayfasında, uygulama için bir görünen ad yazın ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="40c98-180">In the **Specify Display Name** page, type a display name for the application and click **Next**.</span></span>
5. <span data-ttu-id="40c98-181">İçinde **protokolü seçin** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="40c98-181">In the **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="40c98-182">İçinde **sertifika Yapılandır** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="40c98-182">In the **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="40c98-183">HTTPS zaten kullanıyor olmanız olduğundan, şifrelenen belirteçler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="40c98-183">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="40c98-184">Gerçekten AD FS, bu sayfada belirteçlerinden şifrelemek isterseniz, kodunuzda belirteç şifre çözme mantığı de eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="40c98-184">If you really want to encrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="40c98-185">Daha fazla bilgi için bkz: [OWIN WS-Federasyon ara yazılım yapılandırma ve kabul belirteçlerini el ile şifrelenmiş](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="40c98-185">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="40c98-186">Sonraki adıma geçmeden önce Visual Studio projenizden tek parça bilgi gerekir.</span><span class="sxs-lookup"><span data-stu-id="40c98-186">Before you move onto the next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="40c98-187">Proje Özellikleri'nde Not **SSL URL** uygulamanın.</span><span class="sxs-lookup"><span data-stu-id="40c98-187">In the project properties, note the **SSL URL** of the application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="40c98-188">AD FS Yönetimi'nde, yeniden **URL Yapılandır** sayfasında **bağlı olan taraf güveni Ekleme Sihirbazı**seçin **WS-Federasyon Edilgen Protokolü desteğini etkinleştir** ve yazın Önceki adımda not ettiğiniz Visual Studio projenizi SSL URL'si.</span><span class="sxs-lookup"><span data-stu-id="40c98-188">Back in AD FS Management, in the **Configure URL** page of the **Add Relying Party Trust Wizard**, select **Enable support for the WS-Federation Passive protocol** and type in the SSL URL of your Visual Studio project that you noted in the previous step.</span></span> <span data-ttu-id="40c98-189">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="40c98-189">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="40c98-190">URL, kimlik doğrulaması başarılı olduktan sonra istemcinin gönderileceği yeri belirtir.</span><span class="sxs-lookup"><span data-stu-id="40c98-190">URL specifies where to send the client after authentication succeeds.</span></span> <span data-ttu-id="40c98-191">Hata ayıklama ortamı için olmalıdır <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="40c98-191">For the debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="40c98-192">Yayımlanan web uygulaması için web uygulaması URL'si olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="40c98-192">For the published web app, it should be the web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="40c98-193">İçinde **tanımlayıcıları yapılandırma** sayfasında, projenizin SSL URL zaten listelenmiş olduğunu doğrulayın ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="40c98-193">In the **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="40c98-194">Tıklatın **sonraki** tüm varsayılan seçimleri sihirbazla sonuna.</span><span class="sxs-lookup"><span data-stu-id="40c98-194">Click **Next** all the way to the end of the wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="40c98-195">İçinde App_Start\Startup.auth.cs Visual Studio projenizin bu tanımlayıcı değeri karşı eşleştirildiği <code>WsFederationAuthenticationOptions.Wtrealm</code> federe kimlik doğrulaması sırasında.</span><span class="sxs-lookup"><span data-stu-id="40c98-195">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against the value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="40c98-196">Varsayılan olarak, önceki adımdan uygulamanın URL RP tanımlayıcı olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="40c98-196">By default, the application's URL from the previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="40c98-197">Artık, projenizi RP uygulaması için'de AD FS yapılandırma tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="40c98-197">You have now finished configuring the RP application for your project in AD FS.</span></span> <span data-ttu-id="40c98-198">Ardından, uygulamanızın gereksinim duyduğu talepleri göndermek için bu uygulamayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="40c98-198">Next, you configure this application to send the claims needed by your application.</span></span> <span data-ttu-id="40c98-199">**Talep kurallarını Düzenle** iletişim kutusu açıldığında varsayılan olarak, sihirbazın sonunda hemen başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="40c98-199">The **Edit Claim Rules** dialog is opened by default for you at the end of the wizard so you can start immediately.</span></span> <span data-ttu-id="40c98-200">En az (şemalarda parantez içinde) aşağıdaki talep yapılandıralım:</span><span class="sxs-lookup"><span data-stu-id="40c98-200">Let's configure at least the following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="40c98-201">Hydrate için ASP.NET tarafından kullanılan adı (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="40c98-201">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET to hydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="40c98-202">Kuruluşunuzdaki kullanıcılar benzersiz şekilde tanımlamak için kullanılan kullanıcı asıl adı (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) -.</span><span class="sxs-lookup"><span data-stu-id="40c98-202">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used to uniquely identify users in the organization.</span></span>
    * <span data-ttu-id="40c98-203">Grup üyelikleri rolleri (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - olarak kullanılabileceğini `[Authorize(Roles="role1, role2,...")]` denetleyicileri/Eylemler yetkilendirmek için düzenleme.</span><span class="sxs-lookup"><span data-stu-id="40c98-203">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration to authorize controllers/actions.</span></span> <span data-ttu-id="40c98-204">Gerçekte, bu yaklaşım, çoğu kullanıcı rolü yetkilendirme için olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="40c98-204">In reality, this approach may not be the most performant for role authorization.</span></span> <span data-ttu-id="40c98-205">AD kullanıcıları için güvenlik grupları yüzlerce aitse, rol talepleri SAML belirtecinde yüzlerce haline gelir.</span><span class="sxs-lookup"><span data-stu-id="40c98-205">If your AD users belong to hundreds of security groups, they become hundreds of role claims in the SAML token.</span></span> <span data-ttu-id="40c98-206">Alternatif bir yaklaşım, tek bir rol talep koşullu kullanıcının üyelik bağlı olarak belirli bir grubun göndermektir.</span><span class="sxs-lookup"><span data-stu-id="40c98-206">An alternative approach is to send a single role claim conditionally depending on the user's membership in a particular group.</span></span> <span data-ttu-id="40c98-207">Ancak, biz Bu öğretici için basit tut.</span><span class="sxs-lookup"><span data-stu-id="40c98-207">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="40c98-208">Kimliği (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) name - sahteciliğe karşı koruma doğrulama için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="40c98-208">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="40c98-209">Sahteciliğe karşı koruma doğrulama ile çalışması hakkında daha fazla bilgi için bkz: **iş işlevsellik ekleyen** bölümünü [ileAzureActiveDirectorykimlikdoğrulamasıişAzureuygulamasıoluştur](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="40c98-209">For more information on how to make it work with anti-forgery validation, see the **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="40c98-210">Uygulamanız için yapılandırmanız gereken talep türleri, uygulamanızın gereksinimlerine göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="40c98-210">The claim types you need to configure for your application is determined by your application's needs.</span></span> <span data-ttu-id="40c98-211">Örneğin, Azure Active Directory uygulamaları (yani RP güvenleri) tarafından desteklenen talep listesi için bkz: [desteklenen belirteç ve talep türleri](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="40c98-211">For the list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="40c98-212">Talep kurallarını Düzenle iletişim kutusunda tıklatın **Kuralı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="40c98-212">In the Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="40c98-213">Ad, UPN ve rol talepleri tıklatın ve ekran görüntüsü gösterildiği gibi yapılandırmak **son**.</span><span class="sxs-lookup"><span data-stu-id="40c98-213">Configure the name, UPN, and role claims as shown in the screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="40c98-214">Ardından, bir geçici ad kimliği talep adımları kullanarak gösterilen oluşturun [SAML onaylar adı tanımlayıcılarını](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="40c98-214">Next, you create a transient name ID claim using the steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="40c98-215">Tıklatın **Kuralı Ekle** yeniden.</span><span class="sxs-lookup"><span data-stu-id="40c98-215">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="40c98-216">Seçin **talepleri özel kural kullanarak Gönder** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="40c98-216">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="40c98-217">Aşağıdaki kural diline yapıştırın **özel kural** kutusunda, kuralın adını **başına oturum tanımlayıcısı** tıklatıp **son**.</span><span class="sxs-lookup"><span data-stu-id="40c98-217">Paste the following rule language into the **Custom rule** box, name the rule **Per Session Identifier** and click **Finish**.</span></span>  
    
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
    
    <span data-ttu-id="40c98-218">Özel kural bu ekran görüntüsüne görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="40c98-218">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="40c98-219">Tıklatın **Kuralı Ekle** yeniden.</span><span class="sxs-lookup"><span data-stu-id="40c98-219">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="40c98-220">Seçin **gelen talebi Dönüştür** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="40c98-220">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="40c98-221">Kural (talep türü, oluşturduğunuz özel kural kullanarak) ekran görüntüsü gösterildiği gibi yapılandırmak ve tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="40c98-221">Configure the rule as shown in the screenshot (using the claim type you created in the custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="40c98-222">Geçici ad kimliği talebi adımları hakkında ayrıntılı bilgi için bkz: [SAML onaylar adı tanımlayıcılarını](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="40c98-222">For detailed information on the steps for the transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="40c98-223">Tıklatın **Uygula** içinde **talep kurallarını Düzenle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="40c98-223">Click **Apply** in the **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="40c98-224">Aşağıdaki ekran görüntüsüne görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="40c98-224">It should now look like the following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="40c98-225">Yeniden, hata ayıklama ortamı ve yayımlanan web uygulaması için bu adımları yineleyin emin olun.</span><span class="sxs-lookup"><span data-stu-id="40c98-225">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="40c98-226">Uygulamanız için federe kimlik doğrulamasını Sına</span><span class="sxs-lookup"><span data-stu-id="40c98-226">Test federated authentication for your application</span></span>
<span data-ttu-id="40c98-227">Uygulamanızın kimlik doğrulaması mantığı AD FS karşı test etmek hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="40c98-227">You are ready to test your application's authentication logic against AD FS.</span></span> <span data-ttu-id="40c98-228">My AD FS laboratuvar ortamında test grubu içinde Active Directory (AD) ait bir test kullanıcısı sahibim.</span><span class="sxs-lookup"><span data-stu-id="40c98-228">In my AD FS lab environment, I have a test user that belongs to a test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="40c98-229">Hata ayıklayıcıda kimlik doğrulamasını sınamak için tüm yapmanız gereken şimdi türüdür `F5`.</span><span class="sxs-lookup"><span data-stu-id="40c98-229">To test authentication in the debugger, all you need to do now is type `F5`.</span></span> <span data-ttu-id="40c98-230">Yayımlanan web uygulaması kimlik doğrulama test etmek isterseniz, URL'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="40c98-230">If you want to test authentication in the published web app, navigate to the URL.</span></span>

<span data-ttu-id="40c98-231">Web uygulaması yüklendikten sonra tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="40c98-231">After the web application loads, click **Sign In**.</span></span> <span data-ttu-id="40c98-232">Şimdi bir oturum açma iletişim kutusu veya AD FS tarafından seçilen kimlik doğrulama yöntemine bağlı olarak AD FS tarafından sunulan oturum açma sayfasına almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="40c98-232">You should now get either a login dialog or the login page served by AD FS, depending on the authentication method chosen by AD FS.</span></span> <span data-ttu-id="40c98-233">Internet Explorer 11 ne alıyorum aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="40c98-233">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="40c98-234">AD FS dağıtımı, AD etki alanındaki bir kullanıcının oturum oturum sonra yeniden giriş sayfası görmelisiniz **Merhaba, <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="40c98-234">Once you log in with a user in the AD domain of the AD FS deployment, you should now see the homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="40c98-235">köşede.</span><span class="sxs-lookup"><span data-stu-id="40c98-235">in the corner.</span></span> <span data-ttu-id="40c98-236">İşte ne alıyorum.</span><span class="sxs-lookup"><span data-stu-id="40c98-236">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="40c98-237">Şu ana kadar aşağıdaki yollarla başarılı:</span><span class="sxs-lookup"><span data-stu-id="40c98-237">So far, you've succeeded in the following ways:</span></span>

* <span data-ttu-id="40c98-238">Uygulamanız başarıyla AD FS ulaştı ve eşleşen bir RP tanımlayıcı AD FS veritabanında bulunamadı</span><span class="sxs-lookup"><span data-stu-id="40c98-238">Your application has successfully reached AD FS and a matching RP identifier is found in the AD FS database</span></span>
* <span data-ttu-id="40c98-239">AD FS başarıyla bir AD kullanıcısının ve uygulamanın giriş sayfasına geri yönlendir doğrulaması</span><span class="sxs-lookup"><span data-stu-id="40c98-239">AD FS has successfully authenticated an AD user and redirect you back to the application's homepage</span></span>
* <span data-ttu-id="40c98-240">Olarak AD FS kullanıcı adı köşesinde görüntülenir olgu belirtildiği gibi uygulamanızın ad talebini (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) başarıyla gönderildi.</span><span class="sxs-lookup"><span data-stu-id="40c98-240">AD FS as successfully sent the name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) to your application, as indicated by the fact that the user name is displayed in the corner.</span></span> 

<span data-ttu-id="40c98-241">Adı talebi yoksa, görülen **Merhaba,!**.</span><span class="sxs-lookup"><span data-stu-id="40c98-241">If the name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="40c98-242">Görünümler/paylaşılan bakarsanız\_LoginPartial.cshtml, bulduğunuz bunu kullandığını `User.Identity.Name` kullanıcı adını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="40c98-242">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` to display the user name.</span></span> <span data-ttu-id="40c98-243">Kimliği doğrulanmış kullanıcının adı talebi SAML belirtecinde kullanılabiliyorsa, daha önce belirtildiği gibi ASP.NET bu özelliğiyle hydrates.</span><span class="sxs-lookup"><span data-stu-id="40c98-243">As mentioned previously, if the name claim of the authenticated user is available in the SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="40c98-244">AD FS tarafından gönderilen tüm talepler görmek için bir kesme noktası Controllers\HomeController.cs içinde dizin eylem yönteminde yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="40c98-244">To see all the claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in the Index action method.</span></span> <span data-ttu-id="40c98-245">Kullanıcının kimliği doğrulandıktan sonra incelemek `System.Security.Claims.Current.Claims` koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="40c98-245">After the user is authenticated, inspect the `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="40c98-246">Belirli denetleyicileri veya eylemler için Kullanıcıları yetkilendirmek</span><span class="sxs-lookup"><span data-stu-id="40c98-246">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="40c98-247">RP güven yapılandırmanıza grup üyeliklerini rol talepleri dahil olduğundan, artık doğrudan kullanabilmek için `[Authorize(Roles="...")]` decoration denetleyicileri ve eylemleri için.</span><span class="sxs-lookup"><span data-stu-id="40c98-247">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in the `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="40c98-248">Oluştur-okunur-güncelleştir-Sil (CRUD) desende bir iş kolu satır uygulamasında, her eylem erişmek için belirli rolleri yetki verebilir.</span><span class="sxs-lookup"><span data-stu-id="40c98-248">In a line-of-business application with the Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles to access each action.</span></span> <span data-ttu-id="40c98-249">Şu an için yalnızca bu özellik varolan giriş denetleyicisinde çıkışı çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="40c98-249">For now, you will just try out this feature on the existing Home controller.</span></span>

1. <span data-ttu-id="40c98-250">Controllers\HomeController.cs açın.</span><span class="sxs-lookup"><span data-stu-id="40c98-250">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="40c98-251">İşaretleme `About` ve `Contact` eylem yöntemleri güvenlik kullanarak aşağıdaki kodu, benzer Grup Kimliği doğrulanmış kullanıcı üyeliği.</span><span class="sxs-lookup"><span data-stu-id="40c98-251">Decorate the `About` and `Contact` action methods similar to the following code, using security group memberships that your authenticated user has.</span></span>  
   
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
   
    <span data-ttu-id="40c98-252">Ekledim beri **Test kullanıcı** için **Test grubu** my AD FS laboratuar ortamında ı Test grubu yetkilendirme üzerinde test etmek için kullanacağınız `About`.</span><span class="sxs-lookup"><span data-stu-id="40c98-252">Since I added **Test User** to **Test Group** in my AD FS lab environment, I'll use Test Group to test authorization on `About`.</span></span> <span data-ttu-id="40c98-253">İçin `Contact`, negatif durumunda test edeceksiniz **Domain Admins**, hangi **Test kullanıcı** ait değil.</span><span class="sxs-lookup"><span data-stu-id="40c98-253">For `Contact`, I'll test the negative case of **Domain Admins**, to which **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="40c98-254">Hata ayıklayıcı boyutlandırın `F5` ve oturum açın ve ardından **hakkında**.</span><span class="sxs-lookup"><span data-stu-id="40c98-254">Start the debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="40c98-255">Şimdi görüntüleme `~/About/Index` , kimliği doğrulanmış kullanıcının bu eylemi için yetkili olup olmadığını başarıyla, sayfa.</span><span class="sxs-lookup"><span data-stu-id="40c98-255">You should now be viewing the `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="40c98-256">Şimdi **kişi**, hangi my durumda yetki **Test kullanıcısı** eylemi için.</span><span class="sxs-lookup"><span data-stu-id="40c98-256">Now click **Contact**, which in my case should not authorize **Test User** for the action.</span></span> <span data-ttu-id="40c98-257">Ancak, tarayıcı sonunda bu iletiyi gösterir AD FS için yönlendirilir:</span><span class="sxs-lookup"><span data-stu-id="40c98-257">However, the browser is redirected to AD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="40c98-258">AD FS sunucusunda Olay Görüntüleyicisi'nde bu hatayı araştırmak, bu özel durum iletisi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="40c98-258">If you investigate this error in Event Viewer on the AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>The same client browser session has made '6' requests in the last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="40c98-259">Bu hatanın nedeni, bir kullanıcının rollerini yetkili olmadıkları zaman varsayılan olarak, MVC 401 Yetkisiz döndürdüğünden olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="40c98-259">The reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="40c98-260">Bu, kimlik sağlayıcısı (AD FS) için bir yeniden kimlik doğrulaması isteği tetikler.</span><span class="sxs-lookup"><span data-stu-id="40c98-260">This triggers a reauthentication request to your identity provider (AD FS).</span></span> <span data-ttu-id="40c98-261">Kullanıcının kimliği zaten doğrulanmış olduğundan, AD FS sonra başka bir 401 sorunları, aynı sayfasına yeniden yönlendirme döngü oluşturma döndürür.</span><span class="sxs-lookup"><span data-stu-id="40c98-261">Since the user is already authenticated, AD FS returns to the same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="40c98-262">AuthorizeAttribute'nın geçersiz kılar `HandleUnauthorizedRequest` yeniden yönlendirme döngü devam yerine anlamlı bir şey göstermek için basit bir mantık yöntemiyle.</span><span class="sxs-lookup"><span data-stu-id="40c98-262">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic to show something that makes sense instead of continuing the redirect loop.</span></span>
5. <span data-ttu-id="40c98-263">Projenin AuthorizeAttribute.cs adlı bir dosya oluşturun ve aşağıdaki kodu yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="40c98-263">Create a file in the project called AuthorizeAttribute.cs, and paste the following code into it.</span></span>
   
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
   
    <span data-ttu-id="40c98-264">Geçersiz kılma kodu kimliği doğrulanmış ancak yetkisiz durumlarda HTTP 401 (yetkisiz) yerine HTTP 403 (Yasak) gönderir.</span><span class="sxs-lookup"><span data-stu-id="40c98-264">The override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="40c98-265">Hata ayıklayıcıda yeniden çalıştırmak `F5`.</span><span class="sxs-lookup"><span data-stu-id="40c98-265">Run the debugger again with `F5`.</span></span> <span data-ttu-id="40c98-266">Tıklatarak **kişi** şimdi (paragrafta barındırabilir) daha bilgilendirici bir hata iletisi gösterir:</span><span class="sxs-lookup"><span data-stu-id="40c98-266">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="40c98-267">Azure App Service Web Apps uygulamayı yeniden yayımlama ve canlı uygulama davranışını sınayın.</span><span class="sxs-lookup"><span data-stu-id="40c98-267">Publish the application to Azure App Service Web Apps again, and test the behavior of the live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-to-on-premises-data"></a><span data-ttu-id="40c98-268">Şirket içi verilere bağlanma</span><span class="sxs-lookup"><span data-stu-id="40c98-268">Connect to on-premises data</span></span>
<span data-ttu-id="40c98-269">İş uygulamanızı Azure Active Directory yerine AD FS ile uygulamak istediğiniz bir kuruluş veri kapalı içi tutma ile uyumluluk sorunlarını nedenidir.</span><span class="sxs-lookup"><span data-stu-id="40c98-269">A reason that you would want to implement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="40c98-270">Bu kullanma izni yok olduğundan web uygulamanızı azure'da şirket içi veritabanlarına erişim gerekir anlamına [SQL veritabanı](/services/sql-database/) web uygulamalarınız için veri katmanı olarak.</span><span class="sxs-lookup"><span data-stu-id="40c98-270">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed to use [SQL Database](/services/sql-database/) as the data tier for your web apps.</span></span>

<span data-ttu-id="40c98-271">Azure App Service Web Apps iki yaklaşım erişirken şirket içi veritabanlarıyla destekler: [karma bağlantılar](../biztalk-services/integration-hybrid-connection-overview.md) ve [sanal ağlar](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="40c98-271">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="40c98-272">Daha fazla bilgi için bkz: [kullanarak VNET tümleştirme ve karma bağlantılar Azure App Service Web Apps ile](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="40c98-272">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="40c98-273">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="40c98-273">Further resources</span></span>
* [<span data-ttu-id="40c98-274">Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="40c98-274">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="40c98-275">Azure Active Directory kimlik doğrulaması ile iş Azure uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="40c98-275">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="40c98-276">Visual Studio 2013'te ASP.NET ile şirket içi Kurumsal kimlik doğrulama seçeneği (ADFS) kullanın</span><span class="sxs-lookup"><span data-stu-id="40c98-276">Use the On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="40c98-277">VS2013 Web projesi için Katana WIF geçirme</span><span class="sxs-lookup"><span data-stu-id="40c98-277">Migrate a VS2013 Web Project From WIF to Katana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="40c98-278">Active Directory Federasyon Hizmetleri'ne Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="40c98-278">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="40c98-279">WS-Federasyon 1.1 belirtimini</span><span class="sxs-lookup"><span data-stu-id="40c98-279">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

