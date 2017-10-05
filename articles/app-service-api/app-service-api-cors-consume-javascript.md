---
title: "App Service’de CORS desteği | Microsoft Belgeleri"
description: "Azure App Service’de CORS desteğini kullanmayı öğrenin."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: f8373cf5b2e06e6c71bce51cd9e9d5123eea7cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="f9464-103">CORS kullanarak JavaScript’ten bir API uygulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="f9464-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="f9464-104">App Service, JavaScript istemcilerinin API uygulamalarında barındırılan API’lere etki alanları arası çağrılar yapmasını sağlayan [Çıkış Noktaları Arası Kaynak Paylaşımı (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) için yerleşik destek sunar.</span><span class="sxs-lookup"><span data-stu-id="f9464-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients to make cross-domain calls to APIs that are hosted in API apps.</span></span> <span data-ttu-id="f9464-105">App Service, API’nizde herhangi bir kod yazmak zorunda kalmadan API’nize CORS erişimini yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9464-105">App Service lets you configure CORS access to your API without writing any code in your API.</span></span>

<span data-ttu-id="f9464-106">Bu makale iki bölüm içerir:</span><span class="sxs-lookup"><span data-stu-id="f9464-106">This article contains two sections:</span></span>

* <span data-ttu-id="f9464-107">[CORS yapılandırma](#corsconfig) bölümünde herhangi bir API uygulaması, web uygulaması veya mobil uygulama için CORS’nin nasıl yapılandırılacağı genel olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f9464-107">The [How to configure CORS](#corsconfig) section explains in general how to configure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="f9464-108">.NET, Node.js ve Java dahil App Service tarafından desteklenen tüm çerçeveler için eşit oranda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f9464-108">It applies equally to all frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="f9464-109">Makale, [.NET kullanmaya başlarken öğreticilerine devam etme](#tutorialstart) bölümünden başlayarak, [ilk API Apps kullanmaya başlarken öğreticisinde](app-service-api-dotnet-get-started.md) yaptıklarınızın üzerine ekleme yaparak CORS desteğini gösteren bir öğreticidir.</span><span class="sxs-lookup"><span data-stu-id="f9464-109">Starting with the [Continuing the .NET getting-started tutorials](#tutorialstart) section, the article is a tutorial that demonstrates CORS support by building on what you did in [the first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="f9464-110"><a id="corsconfig"></a> Azure Uygulama Hizmeti’nde CORS’yi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f9464-110"><a id="corsconfig"></a> How to configure CORS in Azure App Service</span></span>
<span data-ttu-id="f9464-111">CORS’yi Azure portalında veya [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) araçlarını kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9464-111">You can configure CORS in the Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-the-azure-portal"></a><span data-ttu-id="f9464-112">CORS’yi Azure portalında yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f9464-112">Configure CORS in the Azure portal</span></span>
1. <span data-ttu-id="f9464-113">Bir tarayıcıda [Azure portalına](https://portal.azure.com/) gidin.</span><span class="sxs-lookup"><span data-stu-id="f9464-113">In a browser go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f9464-114">**App Services**’e ve ardından API uygulamanızın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-114">Click **App Services**, and then click the name of your API app.</span></span>
   
    ![Portalda API uygulamasını seçin](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="f9464-116">**API uygulaması** dikey penceresinin sağ tarafında açılan **Ayarlar** dikey penceresinde, **API** bölümünü bulun ve ardından **CORS**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-116">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![Ayarlar dikey penceresinden CORS’yi seçin](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="f9464-118">Metin kutusunda JavaScript çağrılarının alınmasına izin vermek istediğiniz URL’yi veya URL'leri girin.</span><span class="sxs-lookup"><span data-stu-id="f9464-118">In the text box enter the URL or URLs that you want to allow JavaScript calls to come from.</span></span>

    <span data-ttu-id="f9464-119">Örneğin, JavaScript uygulamanızı todolistangular adlı bir web uygulamasına dağıttıysanız, "https://todolistangular.azurewebsites.net" girin.</span><span class="sxs-lookup"><span data-stu-id="f9464-119">For example, if you deployed your JavaScript application to a web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="f9464-120">Alternatif olarak, tüm kaynak etki alanlarının kabul edildiğini belirtmek için bir yıldız işareti (*) girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9464-120">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="f9464-121">**Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-121">Click **Save**.</span></span>
   
   ![Kaydet’e tıklayın.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="f9464-123">**Kaydet**’e tıkladıktan sonra, API uygulaması belirtilen URL’lerden JavaScript çağrılarını kabul eder.</span><span class="sxs-lookup"><span data-stu-id="f9464-123">After you click **Save**, the API app will accept JavaScript calls from the specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="f9464-124">Azure Resource Manager araçlarını kullanarak CORS’yi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f9464-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="f9464-125">CORS’yi [Azure PowerShell](/powershell/azureps-cmdlets-docs) ve [Azure CLI](../cli-install-nodejs.md) gibi komut satırı araçlarında [Azure Resource Manager şablonlarını](../azure-resource-manager/resource-group-authoring-templates.md) kullanarak da yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9464-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and the [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="f9464-126">CORS özelliğini ayarlayan bir Azure Resource Manager şablonu örneği için, [bu öğreticinin örnek uygulamasının deposundaki azuredeploy.json dosyasını](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json) açın.</span><span class="sxs-lookup"><span data-stu-id="f9464-126">For an example of an Azure Resource Manager template that sets the CORS property, open the [azuredeploy.json file in the repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="f9464-127">Aşağıdaki gibi görünen şablon bölümünü bulun:</span><span class="sxs-lookup"><span data-stu-id="f9464-127">Find the section of the template that looks like the following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="f9464-128"><a id="tutorialstart"></a> .NET’i kullanmaya başlama eğiticisinin devamı</span><span class="sxs-lookup"><span data-stu-id="f9464-128"><a id="tutorialstart"></a> Continuing the .NET getting-started tutorial</span></span>
<span data-ttu-id="f9464-129">API uygulamaları için Node.js ve Java kullanmaya başlama serisini takip ediyorsanız, kullanmaya başlama serisini tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="f9464-129">If you are following the Node.js or Java getting-started series for API apps, you have completed the getting started series.</span></span> <span data-ttu-id="f9464-130">API Apps hakkında daha fazla bilgi edinmenizi sağlayacak öneriler için [Sonraki adımlar](#next-steps) bölümüne geçin.</span><span class="sxs-lookup"><span data-stu-id="f9464-130">Skip to the [Next steps](#next-steps) section to find suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="f9464-131">Bu makalenin sonraki bölümleri .NET kullanmaya başlarken serisinin devamıdır ve [ilk öğreticiyi](app-service-api-dotnet-get-started.md) tamamladığınız varsayılır.</span><span class="sxs-lookup"><span data-stu-id="f9464-131">The remainder of this article is a continuation of the .NET getting-started series and assumes that you successfully completed [the first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-the-todolistangular-project-to-a-new-web-app"></a><span data-ttu-id="f9464-132">ToDoListAngular projesini yeni bir web uygulamasına dağıtma</span><span class="sxs-lookup"><span data-stu-id="f9464-132">Deploy the ToDoListAngular project to a new web app</span></span>
<span data-ttu-id="f9464-133">[İlk öğreticide](app-service-api-dotnet-get-started.md), bir orta katman API uygulaması ve bir veri katmanı API uygulaması oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="f9464-133">In [the first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="f9464-134">Bu öğreticide, orta katman API uygulamasını çağıran bir tek sayfalı uygulama (SPA) web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f9464-134">In this tutorial you create a single-page application (SPA) web app that calls the middle tier API app.</span></span> <span data-ttu-id="f9464-135">SPA’nın çalışması için, CORS orta katman API uygulaması üzerinde etkin hale getirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="f9464-135">For the SPA to work you have to enable CORS on the middle tier API app.</span></span> 

<span data-ttu-id="f9464-136">[ToDoList örnek uygulamasında](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), ToDoListAngular projesi orta katman ToDoListAPI Web API projesini çağıran basit bir AngularJS istemcisidir.</span><span class="sxs-lookup"><span data-stu-id="f9464-136">In the [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), the ToDoListAngular project is a simple AngularJS client that calls the middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="f9464-137">*app/scripts/todoListSvc.js* dosyasındaki JavaScript kodu, AngularJS HTTP sağlayıcısını kullanarak API’yi çağırır.</span><span class="sxs-lookup"><span data-stu-id="f9464-137">The JavaScript code in the *app/scripts/todoListSvc.js* file calls the API by using the AngularJS HTTP provider.</span></span> 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-the-todolistangular-project"></a><span data-ttu-id="f9464-138">ToDoListAngular projesi için yeni bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9464-138">Create a new web app for the ToDoListAngular project</span></span>
<span data-ttu-id="f9464-139">Yeni bir App Service web uygulaması oluşturma ve buna bir proje dağıtma yordamı, [serideki ilk öğreticide bir API uygulaması oluşturma ve dağıtma için](app-service-api-dotnet-get-started.md#createapiapp) yer alan yordama benzer.</span><span class="sxs-lookup"><span data-stu-id="f9464-139">The procedure to create a new App Service web app and deploy a project to it is similar to what you saw for [creating and deploying an API app in the first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="f9464-140">Tek farkı uygulama türünün **API Uygulaması** yerine **Web Uygulaması** olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="f9464-140">The only difference is that the app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="f9464-141">İletişim kutularının ekran görüntüleri için bkz.</span><span class="sxs-lookup"><span data-stu-id="f9464-141">For screen shots of the dialogs, see</span></span> 

1. <span data-ttu-id="f9464-142">**Çözüm Gezgini**’nde ToDoListAngular projesine sağ tıklayın ve ardından **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-142">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="f9464-143">**Web’de Yayımla** sihirbazının **Profil** sekmesinde, **Microsoft Azure App Service**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-143">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="f9464-144">**App Service** iletişim kutusunda **Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-144">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="f9464-145">**App Service Oluştur** iletişim kutusunun **Barındırma** sekmesinde, *azurewebsites.net* etki alanında benzersiz bir **Web Uygulaması Adı** girin.</span><span class="sxs-lookup"><span data-stu-id="f9464-145">In the **Hosting** tab of the **Create App Service** dialog box, enter a **Web App Name** that is unique in the *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="f9464-146">Çalışmak istediğiniz Azure **Aboneliğini** seçin.</span><span class="sxs-lookup"><span data-stu-id="f9464-146">Choose the Azure **Subscription** you want to work with.</span></span>
6. <span data-ttu-id="f9464-147">**Kaynak Grubu** açılan listesinde, önceden oluşturduğunuz kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="f9464-147">In the **Resource Group** drop-down list, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="f9464-148">**App Service Planı** açılır listesinde, önceden oluşturduğunuz planı seçin.</span><span class="sxs-lookup"><span data-stu-id="f9464-148">In the **App Service Plan** drop-down list, choose the same plan you created earlier.</span></span> 
8. <span data-ttu-id="f9464-149">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-149">Click **Create**.</span></span>
   
    <span data-ttu-id="f9464-150">Visual Studio web uygulamasını oluşturur, bunun için bir yayımlama profili oluşturur ve **Web’i Yayımla** sihirbazının **Bağlantı** adımını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f9464-150">Visual Studio creates the web app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="f9464-151">Henüz **Yayımla**’ya tıklamayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="f9464-152">Aşağıdaki bölümde, App Service’de çalışan orta katman API uygulamasını çağırmak için yeni web uygulamasını yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="f9464-152">In the following section, you configure the new web app to call the middle tier API app that is running in App Service.</span></span> 

### <a name="set-the-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="f9464-153">Web uygulaması ayarları içinde orta katman URL'yi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f9464-153">Set the middle tier URL in web app settings</span></span>
1. <span data-ttu-id="f9464-154">[Azure portalına](https://portal.azure.com/) gidin ve ardından TodoListAngular (ön uç) projesini barındırmak için oluşturduğunuz **Web Uygulaması** dikey penceresine gidin.</span><span class="sxs-lookup"><span data-stu-id="f9464-154">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **Web App** blade for the web app that you created to host the TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="f9464-155">**Ayarlar > Uygulama Ayarları**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="f9464-156">**Uygulama Ayarları** bölümünde, aşağıdaki anahtar ve değeri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f9464-156">In the **App settings** section, add the following key and value:</span></span>
   
   | <span data-ttu-id="f9464-157">Anahtar</span><span class="sxs-lookup"><span data-stu-id="f9464-157">Key</span></span> | <span data-ttu-id="f9464-158">Değer</span><span class="sxs-lookup"><span data-stu-id="f9464-158">Value</span></span> | <span data-ttu-id="f9464-159">Örnek</span><span class="sxs-lookup"><span data-stu-id="f9464-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="f9464-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="f9464-160">toDoListAPIURL</span></span> |<span data-ttu-id="f9464-161">https://{orta katman API uygulamanızın adı}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="f9464-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="f9464-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="f9464-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="f9464-163">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-163">Click **Save**.</span></span>
   
    <span data-ttu-id="f9464-164">Kod Azure içinde çalıştığında, bu değer *Web.config* dosyasındaki localhost URL’sini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="f9464-164">When the code runs in Azure, this value overrides the localhost URL that is in the *Web.config* file.</span></span> 
   
    <span data-ttu-id="f9464-165">Ayar değerini alan kod *index.cshtml* içindedir:</span><span class="sxs-lookup"><span data-stu-id="f9464-165">The code that gets the setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="f9464-166">*todoListSvc.js* içindeki kod şu ayarı kullanır:</span><span class="sxs-lookup"><span data-stu-id="f9464-166">The code in *todoListSvc.js* uses the setting:</span></span>
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-the-todolistangular-web-project-to-the-new-web-app"></a><span data-ttu-id="f9464-167">ToDoListAngular web projesini yeni web uygulamasına dağıtma</span><span class="sxs-lookup"><span data-stu-id="f9464-167">Deploy the ToDoListAngular web project to the new web app</span></span>
* <span data-ttu-id="f9464-168">Visual Studio’da, **Web’i Yayımla** sihirbazının **Bağlantı** adımında, **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-168">In Visual Studio, in the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="f9464-169">Visual Studio, ToDoListAngular projesini yeni web uygulamasına dağıtır ve web uygulaması URL'sini bir tarayıcı penceresinde açar.</span><span class="sxs-lookup"><span data-stu-id="f9464-169">Visual Studio deploys the ToDoListAngular project to the new web app and opens a browser to the URL of the web app.</span></span> 

### <a name="test-the-application-without-cors-enabled"></a><span data-ttu-id="f9464-170">CORS’yi etkinleştirmeden uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="f9464-170">Test the application without CORS enabled</span></span>
1. <span data-ttu-id="f9464-171">Tarayıcınızda Geliştirici Araçları’nda Konsol penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="f9464-171">In your browser Developer Tools, open the Console window.</span></span>
2. <span data-ttu-id="f9464-172">AngularJS kullanıcı arabirimini gösteren tarayıcı penceresinde **Yapılacaklar Listesi** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-172">In the browser window that displays the AngularJS UI, click the **To Do List** link.</span></span>
   
    <span data-ttu-id="f9464-173">JavaScript kodu orta katman API uygulamasını çağırmayı dener ancak ön uç arka uçtan farklı bir etki alanında çalıştığından başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="f9464-173">The JavaScript code tries to call the middle tier API app, but the call fails because the front end is running in a different domain than the back end.</span></span> <span data-ttu-id="f9464-174">Tarayıcının Geliştirici Araçları Konsol penceresi bir çıkış noktaları arası hata iletisi gösterir.</span><span class="sxs-lookup"><span data-stu-id="f9464-174">The browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Çıkış noktaları arası hata iletisi](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-the-middle-tier-api-app"></a><span data-ttu-id="f9464-176">CORS’yi orta katman API uygulaması için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f9464-176">Configure CORS for the middle tier API app</span></span>
<span data-ttu-id="f9464-177">Bu bölümde, Azure’da orta katman ToDoListAPI API uygulaması için CORS ayarını yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="f9464-177">In this section, you configure the CORS setting in Azure for the middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="f9464-178">Bu ayar, orta katman API uygulamasının ToDoListAngular projesi için oluşturduğunuz web uygulamasından JavaScript çağrılarını almasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9464-178">This setting will allow the middle tier API app to receive JavaScript calls from the web app that you created for the ToDoListAngular project.</span></span>

1. <span data-ttu-id="f9464-179">Bir tarayıcıda [Azure portalına](https://portal.azure.com/) gidin.</span><span class="sxs-lookup"><span data-stu-id="f9464-179">In a browser, go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f9464-180">**App Services**’e ve ardından ToDoListAPI (orta katman) API uygulamasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-180">Click **App Services**, and then click the ToDoListAPI (middle tier) API app.</span></span>
   
    ![Portalda API uygulamasını seçin](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="f9464-182">**API uygulaması** dikey penceresinin sağ tarafında açılan **Ayarlar** dikey penceresinde, **API** bölümünü bulun ve ardından **CORS**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-182">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![Portalda CORS’yi seçme](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="f9464-184">Metin kutusunda, ToDoListAngular (ön uç) web uygulamasının URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="f9464-184">In the text box, enter the URL for the ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="f9464-185">Örneğin, ToDoListAngular projesini todolistangular0121 adlı bir web uygulamasına dağıttıysanız, `https://todolistangular0121.azurewebsites.net` URL’sinden gelen çağrılara izin verin.</span><span class="sxs-lookup"><span data-stu-id="f9464-185">For example, if you deployed the ToDoListAngular project to a web app named todolistangular0121, allow calls from the URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="f9464-186">Alternatif olarak, tüm kaynak etki alanlarının kabul edildiğini belirtmek için bir yıldız işareti (*) girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9464-186">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="f9464-187">**Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9464-187">Click **Save**.</span></span>
   
   ![Kaydet’e tıklayın.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="f9464-189">**Kaydet**’e tıkladıktan sonra, API uygulaması belirtilen URL’den JavaScript çağrılarını kabul eder.</span><span class="sxs-lookup"><span data-stu-id="f9464-189">After you click **Save**, the API app will accept JavaScript calls from the specified URL.</span></span> <span data-ttu-id="f9464-190">Bu ekran görüntüsünde, ToDoListAPI0223 API uygulaması ToDoListAngular web uygulamasından gelen JavaScript istemci çağrılarını kabul eder.</span><span class="sxs-lookup"><span data-stu-id="f9464-190">In this screen shot, the ToDoListAPI0223 API app will accept JavaScript client calls from the ToDoListAngular web app.</span></span>

### <a name="test-the-application-with-cors-enabled"></a><span data-ttu-id="f9464-191">CORS’yi etkinleştirerek uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="f9464-191">Test the application with CORS enabled</span></span>
* <span data-ttu-id="f9464-192">Web uygulamasının HTTPS URL'sini bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="f9464-192">Open a browser to the HTTPS URL of the web app.</span></span> 
  
    <span data-ttu-id="f9464-193">Bu sefer uygulama yapılacaklar öğelerini görüntülemenize, eklemenize, düzenlemenize ve silmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9464-193">This time the application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![Örnek uygulamanın Yapılacaklar Listesi sayfası](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="f9464-195">App Service CORS ile Web API CORS karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="f9464-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="f9464-196">Bir Web API projesinde, API’nizin hangi etki alanlarından JavaScript çağrılarını kabul edeceğini kodla belirtmek için [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet paketini yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9464-196">In a Web API project, you can install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package to specify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="f9464-197">Web API CORS desteği App Service CORS desteğinden daha esnektir.</span><span class="sxs-lookup"><span data-stu-id="f9464-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="f9464-198">Örneğin, kodda farklı eylem yöntemleri için farklı kabul edilen çıkış noktaları belirtebilirken, App Service CORS’de bir API uygulamasının tüm yöntemleri için bir kabul edilen çıkış noktası kümesi belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9464-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="f9464-199">Web API CORS ve App Service CORS’yi aynı API uygulamasında kullanmayı denemeyin.</span><span class="sxs-lookup"><span data-stu-id="f9464-199">Don't try to use both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="f9464-200">App Service CORS öncelik kazanır ve Web API CORS’nin hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="f9464-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="f9464-201">Örneğin, App Service içinde bir çıkış noktası etki alanını etkinleştirir ve Web API kodunuzdaki tüm çıkış noktası etki alanlarını etkinleştirirseniz, Azure API uygulamanız yalnızca Azure içinde belirtilen etki alanı çağrılarını kabul eder.</span><span class="sxs-lookup"><span data-stu-id="f9464-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from the domain you specified in Azure.</span></span>
> 
> 

### <a name="how-to-enable-cors-in-web-api-code"></a><span data-ttu-id="f9464-202">Web API kodunda CORS’yi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f9464-202">How to enable CORS in Web API code</span></span>
<span data-ttu-id="f9464-203">Aşağıdaki adımlarda Web API CORS desteğini etkinleştirme işlemi özetlenir.</span><span class="sxs-lookup"><span data-stu-id="f9464-203">The following steps summarize the process for enabling Web API CORS support.</span></span> <span data-ttu-id="f9464-204">Daha fazla bilgi için bkz. [ASP.NET Web API 2’de Çıkış Noktaları Arası İstekleri Etkinleştirme](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span><span class="sxs-lookup"><span data-stu-id="f9464-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="f9464-205">Bir Web API projesinde, [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f9464-205">In a Web API project, install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="f9464-206">**WebApiConfig** sınıfının **Register** yöntemine aşağıdaki örnekteki gibi bir `config.EnableCors()` kod satırı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f9464-206">Include a `config.EnableCors()` line of code in the **Register** method of the **WebApiConfig** class, as in the following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // The following line enables you to control CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. <span data-ttu-id="f9464-207">Web API denetleyicinizde, `System.Web.Http.Cors` ad alanı için bir `using` bildirimi ekleyin ve denetleyici sınıfına veya tek tek eylem yöntemlerine `EnableCors` özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f9464-207">In your Web API controller, add a `using` statement for the `System.Web.Http.Cors` namespace, and add the `EnableCors` attribute to the controller class or to individual action methods.</span></span> <span data-ttu-id="f9464-208">Aşağıdaki örnekte, CORS desteği tüm denetleyiciye uygulanır.</span><span class="sxs-lookup"><span data-stu-id="f9464-208">In the following example, CORS support applies to the entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="f9464-209">API Apps ile Azure API Management kullanma</span><span class="sxs-lookup"><span data-stu-id="f9464-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="f9464-210">Bir API uygulamasıyla Azure API Management kullanıyorsanız, CORS’yi API uygulamasında değil API Management içinde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f9464-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in the API app.</span></span> <span data-ttu-id="f9464-211">Daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="f9464-211">For more information, see the following resources:</span></span>

* [<span data-ttu-id="f9464-212">Azure API Management’a Genel Bakış (video: CORS 12:10’da başlar)</span><span class="sxs-lookup"><span data-stu-id="f9464-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="f9464-213">API Management etki alanları arası ilkeler</span><span class="sxs-lookup"><span data-stu-id="f9464-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="f9464-214">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="f9464-214">Troubleshooting</span></span>
<span data-ttu-id="f9464-215">Bu öğreticiyi izlerken bir sorunla karşılaşırsanız, bazı sorun giderme fikirlerini burada bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9464-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="f9464-216">[Visual Studio 2015 için .NET için Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003)’nin en yeni sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f9464-216">Make sure that you're using the latest version of the [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="f9464-217">CORS ayarında `https` değerini girdiğinizden ve ön uç web uygulamasını çalıştırmak için `https` kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f9464-217">Make sure that you entered `https` in the CORS setting, and make sure that you're using `https` to run the front-end web app.</span></span>
* <span data-ttu-id="f9464-218">CORS ayarını ön uç web uygulamasında değil orta katman API uygulamasında girdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f9464-218">Make sure that you entered the CORS setting in the middle tier API app, not in the front-end web app.</span></span>
* <span data-ttu-id="f9464-219">CORS’yi hem uygulama kodunda hem de Azure App Service içinde yapılandırıyorsanız, App Service CORS ayarının uygulama kodunda yaptığınız ayarları geçersiz kılacağına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f9464-219">If you're configuring CORS in both application code and Azure App Service, note that the App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="f9464-220">Sorun gidermeyi basitleştiren Visual Studio özellikleri hakkında daha fazla bilgi için bkz. [Visual Studio’da Azure App Service uygulamalarıyla ilgili sorunları giderme](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f9464-220">To learn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9464-221">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f9464-221">Next steps</span></span>
<span data-ttu-id="f9464-222">Bu makalede, istemci JavaScript kodunun farklı bir etki alanındaki bir API’yi çağırması için App Service CORS desteğini nasıl etkinleştireceğinizi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="f9464-222">In this article, you saw how to enable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="f9464-223">API uygulamaları hakkında daha fazla bilgi için, [App Service’de kimlik doğrulamasına giriş](../app-service/app-service-authentication-overview.md) bölümünü okuyun ve ardından [API uygulamaları için kullanıcı kimlik doğrulamaları](app-service-api-dotnet-user-principal-auth.md) öğreticisine gidin.</span><span class="sxs-lookup"><span data-stu-id="f9464-223">To learn more about API apps, read the [introduction to authentication in App Service](../app-service/app-service-authentication-overview.md), and then go to the [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

