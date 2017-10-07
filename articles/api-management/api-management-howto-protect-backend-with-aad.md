---
title: "Azure Active Directory ve API Management ile Web API arka uç aaaProtect | Microsoft Docs"
description: "Bilgi nasıl tooprotect Azure Active Directory ve API Management ile Web API arka uç."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="1e502-103">Nasıl tooprotect Azure Active Directory ve API Management ile Web API arka uç</span><span class="sxs-lookup"><span data-stu-id="1e502-103">How tooprotect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="1e502-104">Video gösterileri nasıl aşağıdaki hello toobuild bir Web API arka ucu ve Azure Active Directory ve API Management ile OAuth 2.0 protokolünü kullanarak koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e502-104">hello following video shows how toobuild a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="1e502-105">Ek bilgi için hello hello videoda adımlar ve bu makalede genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e502-105">This article provides an overview and additional information for hello steps in hello video.</span></span> <span data-ttu-id="1e502-106">Bu 24 dakikalık videoyu şunların nasıl yapıldığını gösterir için:</span><span class="sxs-lookup"><span data-stu-id="1e502-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="1e502-107">Bir Web API arka ucu oluşturmak ve aad'ye - 1: 30'da başlayan güvenli</span><span class="sxs-lookup"><span data-stu-id="1e502-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="1e502-108">API Management - 7:10 Başlangıç Hello API aktarın</span><span class="sxs-lookup"><span data-stu-id="1e502-108">Import hello API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="1e502-109">9:09 başlayan hello Geliştirici Portalı toocall hello API - yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1e502-109">Configure hello Developer portal toocall hello API - starting at 9:09</span></span>
* <span data-ttu-id="1e502-110">Bir masaüstü uygulaması toocall hello API - 18:08 başlayan yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1e502-110">Configure a desktop application toocall hello API - starting at 18:08</span></span>
* <span data-ttu-id="1e502-111">JWT doğrulama İlkesi toopre yapılandırma-20:47 başlayan isteklerini - yetkilendirmek</span><span class="sxs-lookup"><span data-stu-id="1e502-111">Configure a JWT validation policy toopre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="1e502-112">Azure AD dizini oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e502-112">Create an Azure AD directory</span></span>
<span data-ttu-id="1e502-113">Web API yedeklenen ilk olmalıdır Azure Active Directory'yi kullanarak toosecure bir AAD kiracısı.</span><span class="sxs-lookup"><span data-stu-id="1e502-113">toosecure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="1e502-114">Bu videoda adlı bir kiracı **APIMDemo** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e502-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="1e502-115">toocreate bir AAD kiracısı oturum açma toohello [Klasik Azure portalı](https://manage.windowsazure.com) tıklatıp **yeni**->**uygulama hizmetleri**->**etkin Dizin**->**Directory**->**özel Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="1e502-115">toocreate an AAD tenant, sign-in toohello [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="1e502-117">Bu örnekte adlı bir dizin **APIMDemo** adlı varsayılan etki alanı ile oluşturulan **DemoAPIM.onmicrosoft.com**. Bu dizin hello video kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e502-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**. This directory is used throughout hello video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="1e502-119">Azure Active Directory tarafından güvenliği sağlanan bir Web API hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e502-119">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="1e502-120">Bu adımda, Visual Studio 2013 kullanarak bir Web API arka uç oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1e502-120">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="1e502-121">Merhaba video, bu adım 1: 30'da başlar.</span><span class="sxs-lookup"><span data-stu-id="1e502-121">This step of hello video starts at 1:30.</span></span> <span data-ttu-id="1e502-122">Visual Studio tıklatın toocreate Web API arka uç projesi **dosya**->**yeni**->**proje**ve seçin **ASP.NET Web Uygulama** hello gelen **Web** şablonları listesi.</span><span class="sxs-lookup"><span data-stu-id="1e502-122">toocreate Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from hello **Web** templates list.</span></span> <span data-ttu-id="1e502-123">Bu video hello adlı projesi **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="1e502-123">In this video hello project is named **APIMAADDemo**.</span></span> <span data-ttu-id="1e502-124">Tıklatın **Tamam** toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="1e502-124">Click **OK** toocreate hello project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="1e502-126">Tıklatın **Web API** hello gelen **şablon listesini seçin** toocreate bir Web API projesi.</span><span class="sxs-lookup"><span data-stu-id="1e502-126">Click **Web API** from hello **Select a template list** toocreate a Web API project.</span></span> <span data-ttu-id="1e502-127">Azure Directory kimlik doğrulaması tooconfigure tıklatın **kimlik doğrulamayı Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="1e502-127">tooconfigure Azure Directory Authentication click **Change Authentication**.</span></span>

![Yeni Proje][api-management-new-project]

<span data-ttu-id="1e502-129">Tıklatın **Kurumsal hesaplar**ve hello belirtin **etki alanı** AAD kiracınızın.</span><span class="sxs-lookup"><span data-stu-id="1e502-129">Click **Organizational Accounts**, and specify hello **Domain** of your AAD tenant.</span></span> <span data-ttu-id="1e502-130">Bu örnek hello etki alanıdır **DemoAPIM.onmicrosoft.com**. dizininizin hello etki hello elde edilebilir **etki alanları** dizininizin sekmesi.</span><span class="sxs-lookup"><span data-stu-id="1e502-130">In this example hello domain is **DemoAPIM.onmicrosoft.com**. hello domain of your directory can be obtained from hello **Domains** tab of your directory.</span></span>

![Etki Alanları][api-management-aad-domains]

<span data-ttu-id="1e502-132">Hello istenen hello ayarlarını yapılandırma **kimlik doğrulamayı Değiştir** iletişim kutusu ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1e502-132">Configure hello desired settings in hello **Change Authentication** dialog box and click **OK**.</span></span>

![Kimlik doğrulamayı Değiştir][api-management-change-authentication]

<span data-ttu-id="1e502-134">Tıkladığınızda **Tamam** Visual Studio, Azure AD dizininizi uygulamanızla tooregister deneyecek ve Visual Studio tarafından istendiğinde toosign de olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e502-134">When you click **OK** Visual Studio will attempt tooregister your application with your Azure AD directory and you may be prompted toosign in by Visual Studio.</span></span> <span data-ttu-id="1e502-135">Dizininiz için bir yönetici hesabı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1e502-135">Sign in using an administrative account for your directory.</span></span>

![TooVisual Studio oturum][api-management-sign-in-vidual-studio]

<span data-ttu-id="1e502-137">Bu proje bir Azure Web API onay hello olarak tooconfigure kutusunda **hello buluttaki konağa** ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1e502-137">tooconfigure this project as an Azure Web API check hello box for **Host in hello cloud** and then click **OK**.</span></span>

![Yeni Proje][api-management-new-project-cloud]

<span data-ttu-id="1e502-139">İstendiğinde toosign tooAzure içinde olabilir ve ardından hello Web uygulaması yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e502-139">You may be prompted toosign in tooAzure, and then you can configure hello Web App.</span></span>

![Yapılandırma][api-management-configure-web-app]

<span data-ttu-id="1e502-141">Bu örnekte yeni bir **uygulama hizmeti planı** adlı **APIMAADDemo** belirtilir.</span><span class="sxs-lookup"><span data-stu-id="1e502-141">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="1e502-142">Tıklatın **Tamam** tooconfigure Web uygulaması hello ve başlangıç projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1e502-142">Click **OK** tooconfigure hello Web App and create hello project.</span></span>

## <a name="add-hello-code-toohello-web-api-project"></a><span data-ttu-id="1e502-143">Merhaba kod toohello Web API projesi ekleme</span><span class="sxs-lookup"><span data-stu-id="1e502-143">Add hello code toohello Web API project</span></span>
<span data-ttu-id="1e502-144">Merhaba video sonraki adımda Hello hello kod toohello Web API projesi ekler.</span><span class="sxs-lookup"><span data-stu-id="1e502-144">hello next step in hello video adds hello code toohello Web API project.</span></span> <span data-ttu-id="1e502-145">Bu adım 4:35 başlatır.</span><span class="sxs-lookup"><span data-stu-id="1e502-145">This step starts at 4:35.</span></span>

<span data-ttu-id="1e502-146">Bu örnekte Hello Web API'sini bir model ve bir denetleyici kullanarak bir temel hesaplayıcı hizmet uygular.</span><span class="sxs-lookup"><span data-stu-id="1e502-146">hello Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="1e502-147">tooadd hello modeli hello hizmeti için sağ **modelleri** içinde **Çözüm Gezgini** ve **Ekle**, **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="1e502-147">tooadd hello model for hello service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="1e502-148">Ad hello sınıfı `CalcInput` tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1e502-148">Name hello class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="1e502-149">Merhaba aşağıdakileri ekleyin `using` hello deyimi toohello üst `CalcInput.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="1e502-149">Add hello following `using` statement toohello top of hello `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="1e502-150">Oluşturulan hello sınıfı koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1e502-150">Replace hello generated class with hello following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="1e502-151">Sağ **denetleyicileri** içinde **Çözüm Gezgini** ve **Ekle**->**denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="1e502-151">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="1e502-152">Seçin **Web API 2 denetleyici - boş** tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1e502-152">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="1e502-153">Tür **CalcController** Merhaba Denetleyici adı ve'ı tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1e502-153">Type **CalcController** for hello Controller name and click **Add**.</span></span>

![Denetleyici ekleme][api-management-add-controller]

<span data-ttu-id="1e502-155">Merhaba aşağıdakileri ekleyin `using` hello deyimi toohello üst `CalcController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="1e502-155">Add hello following `using` statement toohello top of hello `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="1e502-156">Oluşturulan hello denetleyici sınıfını koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1e502-156">Replace hello generated controller class with hello following code.</span></span> <span data-ttu-id="1e502-157">Bu kod hello uygulayan `Add`, `Subtract`, `Multiply`, ve `Divide` hello temel hesaplayıcı API'si işlemleri.</span><span class="sxs-lookup"><span data-stu-id="1e502-157">This code implements hello `Add`, `Subtract`, `Multiply`, and `Divide` operations of hello Basic Calculator API.</span></span>

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

<span data-ttu-id="1e502-158">Tuşuna **F6** toobuild ve hello çözüm doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1e502-158">Press **F6** toobuild and verify hello solution.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="1e502-159">Yayımlama Hello proje tooAzure</span><span class="sxs-lookup"><span data-stu-id="1e502-159">Publish hello project tooAzure</span></span>
<span data-ttu-id="1e502-160">Bu adım hello Visual Studio yayımlanan tooAzure projesidir.</span><span class="sxs-lookup"><span data-stu-id="1e502-160">In this step hello Visual Studio project is published tooAzure.</span></span> <span data-ttu-id="1e502-161">Merhaba video, bu adım 5:45 başlatır.</span><span class="sxs-lookup"><span data-stu-id="1e502-161">This step of hello video starts at 5:45.</span></span>

<span data-ttu-id="1e502-162">toopublish proje tooAzure Merhaba, hello sağ **APIMAADDemo** seçin ve Visual Studio Proje **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="1e502-162">toopublish hello project tooAzure, right-click hello **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="1e502-163">Hello Hello varsayılan ayarları koruyun **Web'i Yayımla** iletişim kutusu ve tıklatın **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="1e502-163">Keep hello default settings in hello **Publish Web** dialog box and click **Publish**.</span></span>

![Web yayımlama][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a><span data-ttu-id="1e502-165">Azure AD toohello arka uç hizmeti uygulama izinleri</span><span class="sxs-lookup"><span data-stu-id="1e502-165">Grant permissions toohello Azure AD backend service application</span></span>
<span data-ttu-id="1e502-166">Yeni bir uygulama hello arka uç hizmeti için Azure AD dizininizi hello yapılandırma bölümü ve Web API projenizin yayımlama işlemi olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1e502-166">A new application for hello backend service is created in your Azure AD directory as part of hello configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="1e502-167">Merhaba video Bu adım 6:13 başlayan toohello Web API'si arka uç izinleri verilir.</span><span class="sxs-lookup"><span data-stu-id="1e502-167">In this step of hello video, starting at 6:13, permissions are granted toohello Web API backend.</span></span>

![Uygulama][api-management-aad-backend-app]

<span data-ttu-id="1e502-169">Merhaba uygulama tooconfigure hello gerekli izinleri Hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1e502-169">Click hello name of hello application tooconfigure hello required permissions.</span></span> <span data-ttu-id="1e502-170">Toohello gidin **yapılandırma** sekmesi ve toohello aşağı **izinleri tooother uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="1e502-170">Navigate toohello **Configure** tab and scroll down toohello **permissions tooother applications** section.</span></span> <span data-ttu-id="1e502-171">Merhaba tıklatın **uygulama izinleri** yanında aşağı açılan **Windows** **Azure Active Directory**, hello kutuyu **dizinverileriniokuma**, tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="1e502-171">Click hello **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check hello box for **Read directory data**, and click **Save**.</span></span>

![İzinleri ekleme][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="1e502-173">Varsa **Windows** **Azure Active Directory** olan izinleri tooother uygulamalar'ın altında listelenen değil, tıklatın **uygulama ekleme** ve hello listesinden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e502-173">If **Windows** **Azure Active Directory** is not listed under permissions tooother applications, click **Add application** and add it from hello list.</span></span>
> 
> 

<span data-ttu-id="1e502-174">Merhaba Not **uygulama kimliği URI'si** Azure AD uygulaması hello API Management Geliştirici Portalı için yapılandırıldığında, bir sonraki adımda kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="1e502-174">Make a note of hello **App Id URI** for use in a subsequent step when an Azure AD application is configured for hello API Management developer portal.</span></span>

![Uygulama Kimliği URI][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a><span data-ttu-id="1e502-176">API yönetime Hello Web API alma</span><span class="sxs-lookup"><span data-stu-id="1e502-176">Import hello Web API into API Management</span></span>
<span data-ttu-id="1e502-177">API hello Azure portalı erişilen hello API yayımcı portalında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="1e502-177">APIs are configured from hello API publisher portal, which is accessed through hello Azure Portal.</span></span> <span data-ttu-id="1e502-178">tooreach, tıklatın **yayımcı portalına** API Management hizmetinizin hello araç çubuğundan.</span><span class="sxs-lookup"><span data-stu-id="1e502-178">tooreach it, click **Publisher portal** from hello toolbar of your API Management service.</span></span> <span data-ttu-id="1e502-179">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [ilk API'nizi yönetme] [ Manage your first API] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="1e502-179">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API][Manage your first API] tutorial.</span></span>

![Yayımcı portalı][api-management-management-console]

<span data-ttu-id="1e502-181">İşlemleri olabilir [tooAPIs el ile eklenen](api-management-howto-add-operations.md), veya içeri aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="1e502-181">Operations can be [added tooAPIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="1e502-182">Bu videoda, Swagger biçiminde 6:40 başlangıç işlemleri alınır.</span><span class="sxs-lookup"><span data-stu-id="1e502-182">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="1e502-183">Adlı bir dosya oluşturun `calcapi.json` ile içeriği aşağıdaki ve tooyour bilgisayara kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1e502-183">Create a file named `calcapi.json` with following contents and save it tooyour computer.</span></span> <span data-ttu-id="1e502-184">Bu hello olun `host` özniteliği tooyour Web API'si arka uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="1e502-184">Ensure that hello `host` attribute points tooyour Web API backend.</span></span> <span data-ttu-id="1e502-185">Bu örnekte `"host": "apimaaddemo.azurewebsites.net"` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e502-185">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

<span data-ttu-id="1e502-186">tooimport hello hesaplayıcı API'sini, tıklatın **API'leri** hello gelen **API Management** sol hello ve ardından menüsünde **içeri aktarma API'si**.</span><span class="sxs-lookup"><span data-stu-id="1e502-186">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![API’yi İçeri Aktar düğmesi][api-management-import-api]

<span data-ttu-id="1e502-188">Aşağıdaki adımları tooconfigure hello hesaplayıcı API'si hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="1e502-188">Perform hello following steps tooconfigure hello calculator API.</span></span>

1. <span data-ttu-id="1e502-189">' I tıklatın **dosyasından**, toohello Gözat `calculator.json` dosyayı kaydedilmiş ve hello tıklayın **Swagger** radyo düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1e502-189">Click **From file**, browse toohello `calculator.json` file you saved, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="1e502-190">Tür **calc** hello içine **Web API'si URL soneki** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="1e502-190">Type **calc** into hello **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="1e502-191">Tıklatın hello **ürünler (isteğe bağlı)** kutusuna ve seçin **Starter**.</span><span class="sxs-lookup"><span data-stu-id="1e502-191">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="1e502-192">Tıklatın **kaydetmek** tooimport hello API.</span><span class="sxs-lookup"><span data-stu-id="1e502-192">Click **Save** tooimport hello API.</span></span>

![Yeni API ekle][api-management-import-new-api]

<span data-ttu-id="1e502-194">Merhaba API içeri aktarıldığında hello hello API için Özet sayfasında hello yayımcı Portalı'nda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1e502-194">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a><span data-ttu-id="1e502-195">Hello API hello Geliştirici portalından başarısız olan çağrı</span><span class="sxs-lookup"><span data-stu-id="1e502-195">Call hello API unsuccessfully from hello developer portal</span></span>
<span data-ttu-id="1e502-196">Bu noktada, hello API API yönetime içeri aktarıldı ancak hello arka uç hizmeti Azure AD kimlik doğrulaması ile korunduğu için henüz başarılı bir şekilde hello Geliştirici portalından çağrılamaz.</span><span class="sxs-lookup"><span data-stu-id="1e502-196">At this point, hello API has been imported into API Management, but cannot yet be called successfully from hello developer portal because hello backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="1e502-197">Bu 7: hello aşağıdaki adımları kullanarak 40 başlayan hello video gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1e502-197">This is demonstrated in hello video starting at 7:40 using hello following steps.</span></span>

<span data-ttu-id="1e502-198">Tıklatın **Geliştirici Portalı** hello sağ üst tarafındaki hello yayımcı portalı.</span><span class="sxs-lookup"><span data-stu-id="1e502-198">Click **Developer portal** from hello top-right side of hello publisher portal.</span></span>

![Geliştirici portalı][api-management-developer-portal-menu]

<span data-ttu-id="1e502-200">Tıklatın **API'leri** hello tıklatıp **hesaplayıcı** API.</span><span class="sxs-lookup"><span data-stu-id="1e502-200">Click **APIs** and click hello **Calculator** API.</span></span>

![Geliştirici portalı][api-management-dev-portal-apis]

<span data-ttu-id="1e502-202">Tıklatın **deneyin**.</span><span class="sxs-lookup"><span data-stu-id="1e502-202">Click **Try it**.</span></span>

![Deneyin][api-management-dev-portal-try-it]

<span data-ttu-id="1e502-204">Tıklatın **Gönder** ve Not hello yanıt durumu **401 Yetkisiz**.</span><span class="sxs-lookup"><span data-stu-id="1e502-204">Click **Send** and note hello response status of **401 Unauthorized**.</span></span>

![Gönder][api-management-dev-portal-send-401]

<span data-ttu-id="1e502-206">Merhaba istek yetkisiz çünkü Hello arka uç API'si Azure Active Directory tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="1e502-206">hello request is unauthorized because hello backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="1e502-207">Başarılı bir şekilde hello API çağırmadan önce hello Geliştirici Portalı OAuth 2.0 kullanan yapılandırılmış tooauthorize geliştiriciler olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e502-207">Before successfully calling hello API hello developer portal must be configured tooauthorize developers using OAuth 2.0.</span></span> <span data-ttu-id="1e502-208">Bu işlem hello aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1e502-208">This process is described in hello following sections.</span></span>

## <a name="register-hello-developer-portal-as-an-aad-application"></a><span data-ttu-id="1e502-209">Bir AAD uygulaması olarak kayıt hello Geliştirici Portalı</span><span class="sxs-lookup"><span data-stu-id="1e502-209">Register hello developer portal as an AAD application</span></span>
<span data-ttu-id="1e502-210">OAuth 2.0 kullanan hello Geliştirici Portalı tooauthorize geliştiriciler yapılandırmada hello ilk tooregister hello Geliştirici Portalı bir AAD uygulaması adımdır.</span><span class="sxs-lookup"><span data-stu-id="1e502-210">hello first step in configuring hello developer portal tooauthorize developers using OAuth 2.0 is tooregister hello developer portal as an AAD application.</span></span> <span data-ttu-id="1e502-211">Bu 8:27 hello videoda başlayarak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1e502-211">This is demonstrated starting at 8:27 in hello video.</span></span>

<span data-ttu-id="1e502-212">Bu örnekte bu videoda, ilk adımı hello toohello Azure AD kiracısı gidin **APIMDemo** toohello giderek **uygulamaları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="1e502-212">Navigate toohello Azure AD tenant from hello first step of this video, in this example **APIMDemo** and navigate toohello **Applications** tab.</span></span>

![Yeni uygulama][api-management-aad-new-application-devportal]

<span data-ttu-id="1e502-214">Merhaba tıklatın **Ekle** düğmesini toocreate yeni bir Azure Active Directory uygulaması ve seçin **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1e502-214">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Yeni uygulama][api-management-new-aad-application-menu]

<span data-ttu-id="1e502-216">Seçin **Web uygulaması ve/veya Web API**, bir ad girin ve hello İleri okuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1e502-216">Choose **Web application and/or Web API**, enter a name, and click hello next arrow.</span></span> <span data-ttu-id="1e502-217">Bu örnekte **APIMDeveloperPortal** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e502-217">In this example **APIMDeveloperPortal** is used.</span></span>

![Yeni uygulama][api-management-aad-new-application-devportal-1]

<span data-ttu-id="1e502-219">İçin **oturum açma URL'si** API Management hizmetiniz hello URL'sini girin ve ilave `/signin`.</span><span class="sxs-lookup"><span data-stu-id="1e502-219">For **Sign-on URL** enter hello URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="1e502-220">Bu örnekte `https://contoso5.portal.azure-api.net/signin` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e502-220">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="1e502-221">İçin **uygulama kimliği URL'si** API Management hizmetiniz hello URL'sini girin ve bazı benzersiz karakterler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e502-221">For **App Id URL** enter hello URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="1e502-222">Bunlar istenen herhangi bir karakter olabilir ve bu örnekte `https://contoso5.portal.azure-api.net/dp` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e502-222">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="1e502-223">Ne zaman hello istenen **uygulama özellikleri** olan yapılandırılmış, hello onay işareti toocreate hello uygulamaya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1e502-223">When hello  desired **App properties** are configured, click hello check mark toocreate hello application.</span></span>

![Yeni uygulama][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="1e502-225">Bir API Management OAuth 2.0 yetkilendirme sunucusu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1e502-225">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="1e502-226">Merhaba sonraki tooconfigure bir OAuth 2.0 yetkilendirme Sunucusu API Management adımdır.</span><span class="sxs-lookup"><span data-stu-id="1e502-226">hello next step is tooconfigure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="1e502-227">Bu adım 9:43 başlayan video hello gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1e502-227">This step is demonstrated in hello video starting at 9:43.</span></span>

<span data-ttu-id="1e502-228">Tıklatın **güvenlik** hello API Management menüden hello sol tarafta, **OAuth 2.0**ve ardından **yetkilendirme eklemek** sunucu.</span><span class="sxs-lookup"><span data-stu-id="1e502-228">Click **Security** from hello API Management menu on hello left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Yetkilendirme Sunucusu Ekle][api-management-add-authorization-server]

<span data-ttu-id="1e502-230">Hello bir ad ve isteğe bağlı bir açıklama girin **adı** ve **açıklama** alanları.</span><span class="sxs-lookup"><span data-stu-id="1e502-230">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> <span data-ttu-id="1e502-231">Bu alanlar hello API Management hizmet örneği içinde kullanılan tooidentify hello OAuth 2.0 yetkilendirme sunucusu olur.</span><span class="sxs-lookup"><span data-stu-id="1e502-231">These fields are used tooidentify hello OAuth 2.0 authorization server within hello API Management service instance.</span></span> <span data-ttu-id="1e502-232">Bu örnekte **yetkilendirme sunucusu demo** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e502-232">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="1e502-233">Daha sonra bir API için kimlik doğrulaması için kullanılan bir OAuth 2.0 server toobe belirttiğinizde, bu ad seçer.</span><span class="sxs-lookup"><span data-stu-id="1e502-233">Later when you specify an OAuth 2.0 server toobe used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="1e502-234">Hello için **istemci kayıt sayfası URL'si** bir yer tutucu değerini girin `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="1e502-234">For hello **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="1e502-235">Merhaba **istemci kayıt sayfası URL'si** toohello sayfasında, kullanıcıların noktaları toocreate kullanın ve kullanıcı hesaplarının yönetimini desteklemek için OAuth 2.0 sağlayıcıları kendi hesaplarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1e502-235">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="1e502-236">Bu örnekte, kullanıcıların değil oluşturun ve yer tutucu kullanılmak üzere kendi hesaplarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1e502-236">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Yetkilendirme Sunucusu Ekle][api-management-add-authorization-server-1]

<span data-ttu-id="1e502-238">Ardından, belirtin **yetkilendirme uç noktası URL'si** ve **belirteç uç nokta URL'si**.</span><span class="sxs-lookup"><span data-stu-id="1e502-238">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Yetkilendirme sunucusu][api-management-add-authorization-server-1a]

<span data-ttu-id="1e502-240">Bu değerleri hello alınabilir **uygulama uç noktaları** hello hello Geliştirici Portalı için oluşturulmuş AAD uygulaması sayfasında.</span><span class="sxs-lookup"><span data-stu-id="1e502-240">These values can be retrieved from hello **App Endpoints** page of hello AAD application you created for hello developer portal.</span></span> <span data-ttu-id="1e502-241">tooaccess hello uç noktaları gidin toohello **yapılandırma** sekmesinde Merhaba AAD uygulaması için **uç noktaları görüntülemek**.</span><span class="sxs-lookup"><span data-stu-id="1e502-241">tooaccess hello endpoints navigate toohello **Configure** tab for hello AAD application and click **View endpoints**.</span></span>

![Uygulama][api-management-aad-devportal-application]

![Uç noktalarını görüntüle][api-management-aad-view-endpoints]

<span data-ttu-id="1e502-244">Kopya hello **OAuth 2.0 yetkilendirme uç noktası** ve hello yapıştırma **yetkilendirme uç noktası URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="1e502-244">Copy hello **OAuth 2.0 authorization endpoint** and paste it into hello **Authorization endpoint URL** textbox.</span></span>

![Yetkilendirme Sunucusu Ekle][api-management-add-authorization-server-2]

<span data-ttu-id="1e502-246">Kopya hello **OAuth 2.0 belirteç uç noktası** ve hello yapıştırma **belirteç uç nokta URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="1e502-246">Copy hello **OAuth 2.0 token endpoint** and paste it into hello **Token endpoint URL** textbox.</span></span>

![Yetkilendirme Sunucusu Ekle][api-management-add-authorization-server-2a]

<span data-ttu-id="1e502-248">Ayrıca hello belirteç uç noktası, toopasting adlı bir ek gövde parametresini ekleyin **kaynak** ve hello hello değeri için kullanmak **uygulama kimliği URI'si** hello AAD uygulaması olan hello arka uç hizmeti için gelen Merhaba Visual Studio projesi yayımlandığında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1e502-248">In addition toopasting in hello token endpoint, add an additional body parameter named **resource** and for hello value use hello **App Id URI** from hello AAD application for hello backend service that was created when hello Visual Studio project was published.</span></span>

![Uygulama Kimliği URI][api-management-aad-sso-uri]

<span data-ttu-id="1e502-250">Ardından, hello istemci kimlik bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="1e502-250">Next, specify hello client credentials.</span></span> <span data-ttu-id="1e502-251">İstediğiniz hello kaynak hello kimlik bilgilerini bunlar tooaccess, bu durumda hello Geliştirici Portalı.</span><span class="sxs-lookup"><span data-stu-id="1e502-251">These are hello credentials for hello resource you want tooaccess, in this case hello developer portal.</span></span>

![İstemci kimlik bilgileri][api-management-client-credentials]

<span data-ttu-id="1e502-253">tooget hello **istemci kimliği**, toohello gidin **yapılandırma** hello hello Geliştirici Portalı ve kopyalama hello için AAD uygulama sekmesinde **istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="1e502-253">tooget hello **Client Id**, navigate toohello **Configure** tab of hello AAD application for hello developer portal and copy hello **Client Id**.</span></span>

<span data-ttu-id="1e502-254">tooget hello **gizli** hello tıklatın **seçin süresi** hello açılan **anahtarları** bölüm ve bir aralık belirtin.</span><span class="sxs-lookup"><span data-stu-id="1e502-254">tooget hello **Client Secret** click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="1e502-255">Bu örnekte, 1 yıl kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e502-255">In this example 1 year is used.</span></span>

![İstemci kimliği][api-management-aad-client-id]

<span data-ttu-id="1e502-257">Tıklatın **kaydetmek** toosave hello yapılandırma ve görüntü hello anahtarı.</span><span class="sxs-lookup"><span data-stu-id="1e502-257">Click **Save** toosave hello configuration and display hello key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1e502-258">Bu anahtarı not edin.</span><span class="sxs-lookup"><span data-stu-id="1e502-258">Make a note of this key.</span></span> <span data-ttu-id="1e502-259">Hello Azure Active Directory yapılandırması penceresini kapattığınızda hello anahtarı yeniden görüntülenemiyor.</span><span class="sxs-lookup"><span data-stu-id="1e502-259">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="1e502-260">Kopya hello anahtar toohello Pano, anahtar geri toohello yayımcı portalına hello hello anahtarı yapıştırın **gizli** metin kutusuna, tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="1e502-260">Copy hello key toohello clipboard, switch back toohello publisher portal, paste hello key into hello **Client Secret** textbox, and click **Save**.</span></span>

![Yetkilendirme Sunucusu Ekle][api-management-add-authorization-server-3]

<span data-ttu-id="1e502-262">Hemen hello istemci kimlik bilgileri aşağıdaki yetkilendirme kodu verme olur.</span><span class="sxs-lookup"><span data-stu-id="1e502-262">Immediately following hello client credentials is an authorization code grant.</span></span> <span data-ttu-id="1e502-263">Bu yetkilendirme kodu kopyalayın ve anahtar geri tooyour Azure AD Geliştirici Portalı uygulaması sayfasını yapılandırmak ve hello yetkilendirme verme hello yapıştırma **yanıt URL'si** alan öğesini tıklatıp **kaydetmek** yeniden.</span><span class="sxs-lookup"><span data-stu-id="1e502-263">Copy this authorization code and switch back tooyour Azure AD developer portal application configure page, and paste hello authorization grant into hello **Reply URL** field, and click **Save** again.</span></span>

![Yanıt URL'si][api-management-aad-reply-url]

<span data-ttu-id="1e502-265">Merhaba sonraki tooconfigure hello hello Geliştirici Portalı AAD uygulama izinlerini adımdır.</span><span class="sxs-lookup"><span data-stu-id="1e502-265">hello next step is tooconfigure hello permissions for hello developer portal AAD application.</span></span> <span data-ttu-id="1e502-266">Tıklatın **uygulama izinleri** ve hello kutuyu **dizin verilerini okuma**.</span><span class="sxs-lookup"><span data-stu-id="1e502-266">Click **Application Permissions** and check hello box for **Read directory data**.</span></span> <span data-ttu-id="1e502-267">Tıklatın **kaydetmek** bu değiştirin ve ardından toosave **uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="1e502-267">Click **Save** toosave this change, and then click **Add application**.</span></span>

![İzinleri ekleme][api-management-add-devportal-permissions]

<span data-ttu-id="1e502-269">Merhaba arama simgesine tıklayın türü **APIM** hello içine kutusundan başlayarak, seçin **APIMAADDemo**ve hello onay işareti toosave'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1e502-269">Click hello search icon, type **APIM** into hello Starting with box, select **APIMAADDemo**, and click hello check mark toosave.</span></span>

![İzinleri ekleme][api-management-aad-add-app-permissions]

<span data-ttu-id="1e502-271">Tıklatın **izinlere temsilci** için **APIMAADDemo** ve hello kutuyu **erişim APIMAADDemo**, tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="1e502-271">Click **Delegated Permissions** for **APIMAADDemo** and check hello box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="1e502-272">Bu hello Geliştirici Portalı Uygulama tooaccess hello arka uç hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e502-272">This allows hello developer portal application tooaccess hello backend service.</span></span>

![İzinleri ekleme][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a><span data-ttu-id="1e502-274">OAuth 2.0 kullanıcı yetkilendirme hello hesaplayıcı API'si için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1e502-274">Enable OAuth 2.0 user authorization for hello Calculator API</span></span>
<span data-ttu-id="1e502-275">Merhaba OAuth 2.0 sunucusu yapılandırılır, API'nizi hello güvenlik ayarlarını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e502-275">Now that hello OAuth 2.0 server is configured, you can specify it in hello security settings for your API.</span></span> <span data-ttu-id="1e502-276">Bu adım hello 14: 30'da başlayan video gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1e502-276">This step is demonstrated in hello video starting at 14:30.</span></span>

<span data-ttu-id="1e502-277">Tıklatın **API'leri** hello soldaki menüden ve tıklatın **hesaplayıcı** tooview ve ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1e502-277">Click **APIs** in hello left menu, and click  **Calculator** tooview and configure its settings.</span></span>

![Hesaplayıcı API'sini][api-management-calc-api]

<span data-ttu-id="1e502-279">Toohello gidin **güvenlik** sekmesinde, hello denetleyin **OAuth 2.0** onay kutusunu seçin hello istenen yetkilendirme hello sunucudan **yetkilendirme sunucusu** aşağı açılır ve'ı tıklatın **Kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="1e502-279">Navigate toohello **Security** tab, check hello **OAuth 2.0** checkbox, select hello desired authorization server from hello **Authorization server** drop-down, and click **Save**.</span></span>

![Hesaplayıcı API'sini][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a><span data-ttu-id="1e502-281">Merhaba hesaplayıcı API'si hello Geliştirici Portalı'ndan başarıyla çağırın</span><span class="sxs-lookup"><span data-stu-id="1e502-281">Successfully call hello Calculator API from hello developer portal</span></span>
<span data-ttu-id="1e502-282">Merhaba OAuth 2.0 yetkilendirme API hello üzerinde yapılandırılmış, işlemlerini başarıyla hello Geliştirici Merkezi'nden çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="1e502-282">Now that hello OAuth 2.0 authorization is configured on hello API, its operations can be successfully called from hello developer center.</span></span> <span data-ttu-id="1e502-283">Bu adım hello 15: 00'dan başlayarak video gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1e502-283">THis step is demonstrated in hello video starting at 15:00.</span></span>

<span data-ttu-id="1e502-284">Geri toohello gidin **iki tamsayı Ekle** işlemi hello hesap makinesi hizmetinin hello Geliştirici Portalı ve tıklatın **deneyin**.</span><span class="sxs-lookup"><span data-stu-id="1e502-284">Navigate back toohello **Add two integers** operation of hello calculator service in hello developer portal and click **Try it**.</span></span> <span data-ttu-id="1e502-285">Not hello yeni öğesini hello **yetkilendirme** eklediğiniz karşılık gelen toohello yetkilendirme sunucusu bölüm.</span><span class="sxs-lookup"><span data-stu-id="1e502-285">Note hello new item in hello **Authorization** section corresponding toohello authorization server you just added.</span></span>

![Hesaplayıcı API'sini][api-management-calc-authorization-server]

<span data-ttu-id="1e502-287">Seçin **yetkilendirme kodu** hello yetkilendirme açılan dan listesinde ve hello hesap toouse hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="1e502-287">Select **Authorization code** from hello authorization drop-down list and enter hello credentials of hello account toouse.</span></span> <span data-ttu-id="1e502-288">Merhaba hesabıyla oturum açmış istenebilir değil.</span><span class="sxs-lookup"><span data-stu-id="1e502-288">If you are already signed in with hello account you may not be prompted.</span></span>

![Hesaplayıcı API'sini][api-management-devportal-authorization-code]

<span data-ttu-id="1e502-290">Tıklatın **Gönder** ve Not hello **yanıt durumu** , **200 Tamam** ve hello yanıt içeriği hello işlemde hello sonucu.</span><span class="sxs-lookup"><span data-stu-id="1e502-290">Click **Send** and note hello **Response status** of **200 OK** and hello results of hello operation in hello response content.</span></span>

![Hesaplayıcı API'sini][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a><span data-ttu-id="1e502-292">Bir masaüstü uygulaması toocall hello API yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1e502-292">Configure a desktop application toocall hello API</span></span>
<span data-ttu-id="1e502-293">Sonraki yordamda hello video Hello 16: 30'da başlatılır ve basit masaüstü uygulaması toocall hello API yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="1e502-293">hello next procedure in hello video starts at 16:30 and configures a simple desktop application toocall hello API.</span></span> <span data-ttu-id="1e502-294">Merhaba ilk adımı tooregister hello masaüstü uygulaması, Azure AD ve erişim toohello dizin ve toohello arka uç hizmeti verin.</span><span class="sxs-lookup"><span data-stu-id="1e502-294">hello first step is tooregister hello desktop application in Azure AD and give it access toohello directory and toohello backend service.</span></span> <span data-ttu-id="1e502-295">18: 25'hello hesaplayıcı API'sini üzerinde bir işlemi çağırma Merhaba masaüstü uygulaması Tanıtımı yoktur.</span><span class="sxs-lookup"><span data-stu-id="1e502-295">At 18:25 there is a demonstration of hello desktop application calling an operation on hello calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a><span data-ttu-id="1e502-296">JWT doğrulama İlkesi toopre yapılandırma-isteklerini yetkilendirmek</span><span class="sxs-lookup"><span data-stu-id="1e502-296">Configure a JWT validation policy toopre-authorize requests</span></span>
<span data-ttu-id="1e502-297">Merhaba hello video son yordamda 20:48 başlar ve nasıl gösterir toouse hello [doğrulamak JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) İlkesi toopre-hello erişim belirteçleri her gelen istek doğrulayarak isteklerini yetkilendirmek.</span><span class="sxs-lookup"><span data-stu-id="1e502-297">hello final procedure in hello video starts at 20:48 and shows you how toouse hello [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy toopre-authorize requests by validating hello access tokens of each incoming request.</span></span> <span data-ttu-id="1e502-298">Merhaba isteği hello doğrulamak JWT ilke tarafından doğrulanmaz, hello isteği API Management tarafından engellenir ve toohello arka uç geçmedi.</span><span class="sxs-lookup"><span data-stu-id="1e502-298">If hello request is not validated by hello Validate JWT policy, hello request is blocked by API Management and is not passed along toohello backend.</span></span>

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

<span data-ttu-id="1e502-299">Yapılandırma ve bu ilkeyi kullanarak başka bir sunum için bkz: [bulut kapak bölüm 177: diğer API Management Özellikler](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too13:50 ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="1e502-299">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="1e502-300">Too15:00 hello İlkesi Düzenleyicisi'nde yapılandırılan toosee hello İlkesi sarma ve ardından yetkilendirme belirtecini too18:50 hem ile hem de hello olmadan hello Geliştirici Portalı'ndan bir işlem çağırma, bir örnek için gerekli.</span><span class="sxs-lookup"><span data-stu-id="1e502-300">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e502-301">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e502-301">Next steps</span></span>
* <span data-ttu-id="1e502-302">Daha fazla bilgi denetleyin [videolar](https://azure.microsoft.com/documentation/videos/index/?services=api-management) API Management hakkında.</span><span class="sxs-lookup"><span data-stu-id="1e502-302">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="1e502-303">Diğer yolları toosecure için arka uç hizmetinizin bkz [karşılıklı sertifika kimlik doğrulaması](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="1e502-303">For other ways toosecure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
