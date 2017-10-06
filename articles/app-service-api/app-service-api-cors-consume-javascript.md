---
title: "aaaCORS desteği App Service'te | Microsoft Docs"
description: "Nasıl toouse CORS desteği Azure Azure App Service'te öğrenin."
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
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="81262-103">CORS kullanarak JavaScript’ten bir API uygulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="81262-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="81262-104">Uygulama hizmeti için yerleşik destek sunar [arası kaynak kaynak paylaşımı (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), JavaScript istemcilerinin toomake etki alanları arası sağlayan API uygulamalarında barındırılan tooAPIs çağırır.</span><span class="sxs-lookup"><span data-stu-id="81262-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients toomake cross-domain calls tooAPIs that are hosted in API apps.</span></span> <span data-ttu-id="81262-105">App Service CORS erişim tooyour API API'nizi hiçbir kod yazmadan yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="81262-105">App Service lets you configure CORS access tooyour API without writing any code in your API.</span></span>

<span data-ttu-id="81262-106">Bu makale iki bölüm içerir:</span><span class="sxs-lookup"><span data-stu-id="81262-106">This article contains two sections:</span></span>

* <span data-ttu-id="81262-107">Merhaba [nasıl tooconfigure CORS](#corsconfig) bölümde açıklanmıştır genel nasıl tooconfigure CORS herhangi bir API uygulaması, web uygulaması veya mobil uygulama.</span><span class="sxs-lookup"><span data-stu-id="81262-107">hello [How tooconfigure CORS](#corsconfig) section explains in general how tooconfigure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="81262-108">Ayrıca .NET, Node.js ve Java dahil App Service tarafından desteklenen tooall çerçeveleri eşit oranda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="81262-108">It applies equally tooall frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="81262-109">Merhaba ile başlayan [hello .NET kullanmaya Başlarken öğreticilerine devam etme](#tutorialstart) bölümünde hello makaledir CORS desteği yaptıklarınızın üzerine ekleme yaparak gösteren bir eğitim [hello ilk API Apps başlangıç öğreticisinde ](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="81262-109">Starting with hello [Continuing hello .NET getting-started tutorials](#tutorialstart) section, hello article is a tutorial that demonstrates CORS support by building on what you did in [hello first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="81262-110"><a id="corsconfig"></a>Nasıl tooconfigure Azure App Service'de CORS</span><span class="sxs-lookup"><span data-stu-id="81262-110"><a id="corsconfig"></a> How tooconfigure CORS in Azure App Service</span></span>
<span data-ttu-id="81262-111">Hello Azure portal veya kullanarak CORS'yi yapılandırın [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) araçları.</span><span class="sxs-lookup"><span data-stu-id="81262-111">You can configure CORS in hello Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-hello-azure-portal"></a><span data-ttu-id="81262-112">Hello Azure portal CORS'yi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="81262-112">Configure CORS in hello Azure portal</span></span>
1. <span data-ttu-id="81262-113">Bir tarayıcıda toohello Git [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="81262-113">In a browser go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="81262-114">Tıklatın **uygulama hizmetleri**ve ardından API uygulamanızın hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81262-114">Click **App Services**, and then click hello name of your API app.</span></span>
   
    ![Portalda API uygulamasını seçin](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="81262-116">Merhaba, **ayarları** hello toohello sağındaki açılan dikey **API uygulaması** dikey penceresinde, Bul hello **API** bölümünde ve ardından **CORS**.</span><span class="sxs-lookup"><span data-stu-id="81262-116">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Ayarlar dikey penceresinden CORS’yi seçin](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="81262-118">Merhaba metin kutusuna hello URL veya tooallow JavaScript çağrılarını toocome gelen istediğiniz URL'leri girin.</span><span class="sxs-lookup"><span data-stu-id="81262-118">In hello text box enter hello URL or URLs that you want tooallow JavaScript calls toocome from.</span></span>

    <span data-ttu-id="81262-119">Örneğin, todolistangular adlı, JavaScript uygulama tooa web uygulamasına dağıttıysanız, "https://todolistangular.azurewebsites.net" girin.</span><span class="sxs-lookup"><span data-stu-id="81262-119">For example, if you deployed your JavaScript application tooa web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="81262-120">Alternatif olarak, tüm kaynak etki alanlarının kabul edildiğini bir yıldız işareti (*) toospecify girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81262-120">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="81262-121">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81262-121">Click **Save**.</span></span>
   
   ![Kaydet’e tıklayın.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="81262-123">Tıklattıktan sonra **kaydetmek**, hello API uygulaması JavaScript kabul hello gelen çağrıları belirtilen URL.</span><span class="sxs-lookup"><span data-stu-id="81262-123">After you click **Save**, hello API app will accept JavaScript calls from hello specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="81262-124">Azure Resource Manager araçlarını kullanarak CORS’yi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="81262-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="81262-125">Kullanarak bir API uygulaması için CORS yapılandırabilirsiniz [Azure Resource Manager şablonları](../azure-resource-manager/resource-group-authoring-templates.md) gibi komut satırı araçlarında [Azure PowerShell](/powershell/azureps-cmdlets-docs) ve hello [Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="81262-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and hello [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="81262-126">Merhaba hello CORS özelliğini ayarlayan bir Azure Resource Manager şablonu örneği için açık [Bu öğreticinin örnek uygulamasının için hello deposundaki azuredeploy.json dosyasını](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="81262-126">For an example of an Azure Resource Manager template that sets hello CORS property, open hello [azuredeploy.json file in hello repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="81262-127">Merhaba aşağıdaki örneğine hello gibi görünüyor hello şablon bölümünü bulun:</span><span class="sxs-lookup"><span data-stu-id="81262-127">Find hello section of hello template that looks like hello following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="81262-128"><a id="tutorialstart"></a>Merhaba .NET kullanmaya Başlarken Öğreticisine devam etme</span><span class="sxs-lookup"><span data-stu-id="81262-128"><a id="tutorialstart"></a> Continuing hello .NET getting-started tutorial</span></span>
<span data-ttu-id="81262-129">Merhaba Node.js ve Java kullanmaya başlama serisini API uygulamaları için takip ediyorsanız, kullanmaya başlama serisini alma tamamlanmış hello sahip.</span><span class="sxs-lookup"><span data-stu-id="81262-129">If you are following hello Node.js or Java getting-started series for API apps, you have completed hello getting started series.</span></span> <span data-ttu-id="81262-130">Toohello atla [sonraki adımlar](#next-steps) bölümünde API uygulamaları hakkında daha fazla öğrenme toofind yönelik öneriler.</span><span class="sxs-lookup"><span data-stu-id="81262-130">Skip toohello [Next steps](#next-steps) section toofind suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="81262-131">Merhaba bu makalenin sonraki bölümlerinde hello .NET kullanmaya Başlarken serisinin devamıdır ve başarıyla tamamlandığını varsayar [hello ilk öğreticide](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="81262-131">hello remainder of this article is a continuation of hello .NET getting-started series and assumes that you successfully completed [hello first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a><span data-ttu-id="81262-132">Merhaba ToDoListAngular projesi tooa yeni web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="81262-132">Deploy hello ToDoListAngular project tooa new web app</span></span>
<span data-ttu-id="81262-133">İçinde [hello ilk öğreticide](app-service-api-dotnet-get-started.md), orta katman API uygulamasını ve veri katmanı API uygulaması oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="81262-133">In [hello first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="81262-134">Bu öğreticide, çağrıları hello orta katman API uygulamasını bir tek sayfalı uygulama (SPA) web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81262-134">In this tutorial you create a single-page application (SPA) web app that calls hello middle tier API app.</span></span> <span data-ttu-id="81262-135">Merhaba SPA toowork tooenable CORS hello orta katman API uygulaması sahip.</span><span class="sxs-lookup"><span data-stu-id="81262-135">For hello SPA toowork you have tooenable CORS on hello middle tier API app.</span></span> 

<span data-ttu-id="81262-136">Merhaba, [ToDoList örnek uygulamasında](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular projedir hello orta katman Todolistapı Web API projesini çağıran basit bir AngularJS istemci.</span><span class="sxs-lookup"><span data-stu-id="81262-136">In hello [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular project is a simple AngularJS client that calls hello middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="81262-137">JavaScript kodu hello hello *app/scripts/todoListSvc.js* dosya hello AngularJS HTTP sağlayıcısını kullanarak hello API çağırır.</span><span class="sxs-lookup"><span data-stu-id="81262-137">hello JavaScript code in hello *app/scripts/todoListSvc.js* file calls hello API by using hello AngularJS HTTP provider.</span></span> 

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

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a><span data-ttu-id="81262-138">Merhaba ToDoListAngular projesi için yeni bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="81262-138">Create a new web app for hello ToDoListAngular project</span></span>
<span data-ttu-id="81262-139">Merhaba yordamı toocreate yeni bir App Service web uygulaması ve proje dağıtma tooit olduğu için gördüğünüz benzer toowhat [oluşturma ve hello bu serideki ilk öğreticide bir API uygulamasına dağıtma](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="81262-139">hello procedure toocreate a new App Service web app and deploy a project tooit is similar toowhat you saw for [creating and deploying an API app in hello first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="81262-140">Bu hello uygulama türü farktır yalnızca Hello: **Web uygulaması** yerine **API uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="81262-140">hello only difference is that hello app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="81262-141">Merhaba iletişim kutularının ekran görüntüleri için bkz:</span><span class="sxs-lookup"><span data-stu-id="81262-141">For screen shots of hello dialogs, see</span></span> 

1. <span data-ttu-id="81262-142">İçinde **Çözüm Gezgini**hello ToDoListAngular projesine sağ tıklayın ve ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="81262-142">In **Solution Explorer**, right-click hello ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="81262-143">Merhaba, **profil** hello sekmesinde **Web'i Yayımla** Sihirbazı'nı tıklatın **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="81262-143">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="81262-144">Merhaba, **uygulama hizmeti** iletişim kutusu, tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="81262-144">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="81262-145">Merhaba, **barındırma** hello sekmesinde **App Service Oluştur** iletişim kutusuna bir **Web uygulaması adı** hello benzersiz *azurewebsites.net* etki alanı.</span><span class="sxs-lookup"><span data-stu-id="81262-145">In hello **Hosting** tab of hello **Create App Service** dialog box, enter a **Web App Name** that is unique in hello *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="81262-146">Hello Azure'ı seçin **abonelik** ile toowork istiyor.</span><span class="sxs-lookup"><span data-stu-id="81262-146">Choose hello Azure **Subscription** you want toowork with.</span></span>
6. <span data-ttu-id="81262-147">Merhaba, **kaynak grubu** aşağı açılan listesinde, hello seçin daha önce oluşturduğunuz aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="81262-147">In hello **Resource Group** drop-down list, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="81262-148">Merhaba, **uygulama hizmeti planı** aşağı açılan listesinde, hello seçin önceden oluşturduğunuz planı.</span><span class="sxs-lookup"><span data-stu-id="81262-148">In hello **App Service Plan** drop-down list, choose hello same plan you created earlier.</span></span> 
8. <span data-ttu-id="81262-149">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81262-149">Click **Create**.</span></span>
   
    <span data-ttu-id="81262-150">Visual Studio hello web uygulamasını oluşturur, bunun için bir yayımlama profili oluşturur ve görüntüler hello **bağlantı** hello adımında **Web'i Yayımla** Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="81262-150">Visual Studio creates hello web app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="81262-151">Henüz **Yayımla**’ya tıklamayın.</span><span class="sxs-lookup"><span data-stu-id="81262-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="81262-152">Bölümden hello, App Service'te çalışan hello yeni web uygulaması toocall hello orta katman API uygulamasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="81262-152">In hello following section, you configure hello new web app toocall hello middle tier API app that is running in App Service.</span></span> 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="81262-153">Web uygulaması ayarları içinde Hello orta katman URL'yi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="81262-153">Set hello middle tier URL in web app settings</span></span>
1. <span data-ttu-id="81262-154">Toohello Git [Azure portal](https://portal.azure.com/)ve ardından toohello gidin **Web uygulaması** toohost hello TodoListAngular (ön uç) projesini oluşturulan hello web uygulaması dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="81262-154">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **Web App** blade for hello web app that you created toohost hello TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="81262-155">**Ayarlar > Uygulama Ayarları**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81262-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="81262-156">Merhaba, **uygulama ayarları** bölümünde, hello aşağıdakileri ekleyin anahtar ve değer:</span><span class="sxs-lookup"><span data-stu-id="81262-156">In hello **App settings** section, add hello following key and value:</span></span>
   
   | <span data-ttu-id="81262-157">Anahtar</span><span class="sxs-lookup"><span data-stu-id="81262-157">Key</span></span> | <span data-ttu-id="81262-158">Değer</span><span class="sxs-lookup"><span data-stu-id="81262-158">Value</span></span> | <span data-ttu-id="81262-159">Örnek</span><span class="sxs-lookup"><span data-stu-id="81262-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="81262-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="81262-160">toDoListAPIURL</span></span> |<span data-ttu-id="81262-161">https://{orta katman API uygulamanızın adı}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="81262-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="81262-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="81262-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="81262-163">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81262-163">Click **Save**.</span></span>
   
    <span data-ttu-id="81262-164">Merhaba kod Azure içinde çalıştığında, bu değer hello olduğu hello localhost URL'sini geçersiz kılar *Web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="81262-164">When hello code runs in Azure, this value overrides hello localhost URL that is in hello *Web.config* file.</span></span> 
   
    <span data-ttu-id="81262-165">Merhaba ayar değerini hello kodu içinde *Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="81262-165">hello code that gets hello setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="81262-166">Merhaba kodda *todoListSvc.js* hello ayarı kullanır:</span><span class="sxs-lookup"><span data-stu-id="81262-166">hello code in *todoListSvc.js* uses hello setting:</span></span>
   
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

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a><span data-ttu-id="81262-167">Merhaba ToDoListAngular web projesi toohello yeni web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="81262-167">Deploy hello ToDoListAngular web project toohello new web app</span></span>
* <span data-ttu-id="81262-168">Visual Studio'da, hello **bağlantı** hello adımında **Web'i Yayımla** Sihirbazı'nı tıklatın **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="81262-168">In Visual Studio, in hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="81262-169">Visual Studio hello ToDoListAngular projesi toohello yeni web uygulamasına dağıtır ve hello web uygulamasının bir tarayıcı toohello URL'sini açar.</span><span class="sxs-lookup"><span data-stu-id="81262-169">Visual Studio deploys hello ToDoListAngular project toohello new web app and opens a browser toohello URL of hello web app.</span></span> 

### <a name="test-hello-application-without-cors-enabled"></a><span data-ttu-id="81262-170">CORS'yi etkinleştirmeden Hello uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="81262-170">Test hello application without CORS enabled</span></span>
1. <span data-ttu-id="81262-171">Tarayıcınızda geliştirici araçları hello konsol penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="81262-171">In your browser Developer Tools, open hello Console window.</span></span>
2. <span data-ttu-id="81262-172">Merhaba AngularJS kullanıcı arabirimini görüntüleyen hello tarayıcı penceresinde hello tıklatın **tooDo listesi** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="81262-172">In hello browser window that displays hello AngularJS UI, click hello **tooDo List** link.</span></span>
   
    <span data-ttu-id="81262-173">Merhaba JavaScript kodu toocall hello orta katman API uygulaması çalışır ancak hello ön uç geri hello farklı bir etki alanında son çalıştığından hello çağrı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="81262-173">hello JavaScript code tries toocall hello middle tier API app, but hello call fails because hello front end is running in a different domain than hello back end.</span></span> <span data-ttu-id="81262-174">Merhaba tarayıcının geliştirici araçları konsol penceresi bir çıkış noktaları arası hata iletisi gösterir.</span><span class="sxs-lookup"><span data-stu-id="81262-174">hello browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Çıkış noktaları arası hata iletisi](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a><span data-ttu-id="81262-176">Merhaba orta katman API uygulaması CORS'yi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="81262-176">Configure CORS for hello middle tier API app</span></span>
<span data-ttu-id="81262-177">Bu bölümde, hello orta katman Todolistapı API uygulaması azure'da hello CORS ayarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="81262-177">In this section, you configure hello CORS setting in Azure for hello middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="81262-178">Bu ayar hello orta katman API uygulaması tooreceive JavaScript çağrılarını hello ToDoListAngular projesi için oluşturduğunuz web uygulamasından hello izin verir.</span><span class="sxs-lookup"><span data-stu-id="81262-178">This setting will allow hello middle tier API app tooreceive JavaScript calls from hello web app that you created for hello ToDoListAngular project.</span></span>

1. <span data-ttu-id="81262-179">Bir tarayıcıda toohello Git [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="81262-179">In a browser, go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="81262-180">Tıklatın **uygulama hizmetleri**ve ardından Todolistapı (orta katman) API hello uygulama tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81262-180">Click **App Services**, and then click hello ToDoListAPI (middle tier) API app.</span></span>
   
    ![Portalda API uygulamasını seçin](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="81262-182">Merhaba, **ayarları** hello toohello sağındaki açılan dikey **API uygulaması** dikey penceresinde, Bul hello **API** bölümünde ve ardından **CORS**.</span><span class="sxs-lookup"><span data-stu-id="81262-182">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Portalda CORS’yi seçme](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="81262-184">Merhaba metin kutusuna hello ToDoListAngular (ön uç) web uygulaması için hello URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="81262-184">In hello text box, enter hello URL for hello ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="81262-185">Örneğin, todolistangular0121 adlı hello ToDoListAngular projesi tooa web uygulamasına dağıttıysanız, hello URL'den çağrılarına izin vermek `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="81262-185">For example, if you deployed hello ToDoListAngular project tooa web app named todolistangular0121, allow calls from hello URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="81262-186">Alternatif olarak, tüm kaynak etki alanlarının kabul edildiğini bir yıldız işareti (*) toospecify girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81262-186">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="81262-187">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81262-187">Click **Save**.</span></span>
   
   ![Kaydet’e tıklayın.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="81262-189">Tıklattıktan sonra **kaydetmek**, hello API uygulaması JavaScript kabul hello gelen çağrıları belirtilen URL.</span><span class="sxs-lookup"><span data-stu-id="81262-189">After you click **Save**, hello API app will accept JavaScript calls from hello specified URL.</span></span> <span data-ttu-id="81262-190">Bu ekran görüntüsünde hello Todolistapı0223 API uygulaması hello ToDoListAngular web uygulamasından JavaScript istemci çağrılarını kabul eder.</span><span class="sxs-lookup"><span data-stu-id="81262-190">In this screen shot, hello ToDoListAPI0223 API app will accept JavaScript client calls from hello ToDoListAngular web app.</span></span>

### <a name="test-hello-application-with-cors-enabled"></a><span data-ttu-id="81262-191">CORS'yi Hello uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="81262-191">Test hello application with CORS enabled</span></span>
* <span data-ttu-id="81262-192">Bir tarayıcı toohello hello web uygulamasının HTTPS URL'sini açın.</span><span class="sxs-lookup"><span data-stu-id="81262-192">Open a browser toohello HTTPS URL of hello web app.</span></span> 
  
    <span data-ttu-id="81262-193">Bu zaman hello uygulaması, görüntülemek, ekleme, düzenleme ve yapılacaklar öğelerini silme sağlar.</span><span class="sxs-lookup"><span data-stu-id="81262-193">This time hello application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![örnek uygulaması tooDo liste sayfası](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="81262-195">App Service CORS ile Web API CORS karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="81262-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="81262-196">Bir Web API projesinde hello yükleyebilirsiniz [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet paketi toospecify kodu JavaScript API'nizi kabul edeceği hangi etki alanlarının çağırır.</span><span class="sxs-lookup"><span data-stu-id="81262-196">In a Web API project, you can install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package toospecify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="81262-197">Web API CORS desteği App Service CORS desteğinden daha esnektir.</span><span class="sxs-lookup"><span data-stu-id="81262-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="81262-198">Örneğin, kodda farklı eylem yöntemleri için farklı kabul edilen çıkış noktaları belirtebilirken, App Service CORS’de bir API uygulamasının tüm yöntemleri için bir kabul edilen çıkış noktası kümesi belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81262-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="81262-199">Toouse denemeyin Web API CORS ve App Service CORS bir API uygulamasında.</span><span class="sxs-lookup"><span data-stu-id="81262-199">Don't try toouse both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="81262-200">App Service CORS öncelik kazanır ve Web API CORS’nin hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="81262-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="81262-201">Örneğin, App Service'te bir kaynak etki alanı etkinleştirirseniz ve Web API kodunuzdaki tüm çıkış noktası etki alanlarını etkinleştirmek, Azure API uygulamanız yalnızca Azure içinde belirtilen hello etki alanından çağrılarını kabul eder.</span><span class="sxs-lookup"><span data-stu-id="81262-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from hello domain you specified in Azure.</span></span>
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a><span data-ttu-id="81262-202">Nasıl Web API kodunda CORS'yi tooenable</span><span class="sxs-lookup"><span data-stu-id="81262-202">How tooenable CORS in Web API code</span></span>
<span data-ttu-id="81262-203">Aşağıdaki adımları hello Web API CORS desteğini etkinleştirme hello işlemi özetlenir.</span><span class="sxs-lookup"><span data-stu-id="81262-203">hello following steps summarize hello process for enabling Web API CORS support.</span></span> <span data-ttu-id="81262-204">Daha fazla bilgi için bkz. [ASP.NET Web API 2’de Çıkış Noktaları Arası İstekleri Etkinleştirme](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span><span class="sxs-lookup"><span data-stu-id="81262-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="81262-205">Bir Web API projesinde hello yüklemek [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="81262-205">In a Web API project, install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="81262-206">Dahil bir `config.EnableCors()` hello kod satırı **kaydetmek** hello yöntemi **WebApiConfig** aşağıdaki örneğine hello olduğu gibi sınıfı.</span><span class="sxs-lookup"><span data-stu-id="81262-206">Include a `config.EnableCors()` line of code in hello **Register** method of hello **WebApiConfig** class, as in hello following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
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
3. <span data-ttu-id="81262-207">Web API denetleyicinizde eklemek bir `using` hello bildirimi `System.Web.Http.Cors` ad alanı ve hello ekleyin `EnableCors` özniteliği toohello denetleyici sınıfı veya tooindividual eylem yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="81262-207">In your Web API controller, add a `using` statement for hello `System.Web.Http.Cors` namespace, and add hello `EnableCors` attribute toohello controller class or tooindividual action methods.</span></span> <span data-ttu-id="81262-208">Aşağıdaki örneğine hello CORS desteğini toohello tüm denetleyiciye uygulanır.</span><span class="sxs-lookup"><span data-stu-id="81262-208">In hello following example, CORS support applies toohello entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="81262-209">API Apps ile Azure API Management kullanma</span><span class="sxs-lookup"><span data-stu-id="81262-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="81262-210">Bir API uygulamasıyla Azure API Management kullanıyorsanız, CORS'yi API Management yerine hello API uygulamasında yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="81262-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in hello API app.</span></span> <span data-ttu-id="81262-211">Daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="81262-211">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="81262-212">Azure API Management’a Genel Bakış (video: CORS 12:10’da başlar)</span><span class="sxs-lookup"><span data-stu-id="81262-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="81262-213">API Management etki alanları arası ilkeler</span><span class="sxs-lookup"><span data-stu-id="81262-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="81262-214">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="81262-214">Troubleshooting</span></span>
<span data-ttu-id="81262-215">Bu öğreticiyi izlerken bir sorunla karşılaşırsanız, bazı sorun giderme fikirlerini burada bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81262-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="81262-216">Merhaba hello en son sürümünü kullandığınızdan emin olun [Visual Studio 2015 için .NET için Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="81262-216">Make sure that you're using hello latest version of hello [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="81262-217">Girdiğinizden emin olun `https` hello CORS ayarını ve kullandığınızdan emin olun `https` toorun hello ön uç web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="81262-217">Make sure that you entered `https` in hello CORS setting, and make sure that you're using `https` toorun hello front-end web app.</span></span>
* <span data-ttu-id="81262-218">Hello CORS ayarını girdiğiniz hello orta katman API uygulaması, hello ön uç web uygulamasında değil olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="81262-218">Make sure that you entered hello CORS setting in hello middle tier API app, not in hello front-end web app.</span></span>
* <span data-ttu-id="81262-219">CORS'yi hem uygulama kodunda hem de Azure App Service içinde yapılandırıyorsanız hello App Service CORS ayarının uygulama kodunda yaptığınız ne olursa olsun kılar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="81262-219">If you're configuring CORS in both application code and Azure App Service, note that hello App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="81262-220">Daha fazla sorun gidermeyi basitleştiren Visual Studio özellikleri hakkında toolearn bkz [Visual Studio'daki sorun giderme Azure uygulama hizmetinde uygulamaları](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="81262-220">toolearn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="81262-221">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="81262-221">Next steps</span></span>
<span data-ttu-id="81262-222">Bu makalede, nasıl tooenable App Service CORS desteği böylece istemci JavaScript kodunun farklı bir etki alanında bir API çağrısı gördünüz.</span><span class="sxs-lookup"><span data-stu-id="81262-222">In this article, you saw how tooenable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="81262-223">toolearn hello okuma API uygulamaları hakkında daha fazla [App Service'te giriş tooauthentication](../app-service/app-service-authentication-overview.md), ve toohello Git [API uygulamaları için kullanıcı kimlik doğrulaması](app-service-api-dotnet-user-principal-auth.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="81262-223">toolearn more about API apps, read hello [introduction tooauthentication in App Service](../app-service/app-service-authentication-overview.md), and then go toohello [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

