---
title: "Azure işlevleri OpenAPI meta verilerde | Microsoft Docs"
description: "Azure işlevleri OpenAPI desteği'ne genel bakış"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: e426e56bcac30c740e86d620dadf291fe31e3e10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a><span data-ttu-id="810f6-103">OpenAPI 2.0 meta verileri desteği Azure işlevlerinde (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="810f6-103">OpenAPI 2.0 metadata support in Azure Functions (preview)</span></span>
<span data-ttu-id="810f6-104">OpenAPI 2.0 (önceki adıyla Swagger) meta verileri desteği Azure işlevleri OpenAPI 2.0 tanımının bir işlev uygulaması içinde yazmak için kullanabileceğiniz bir önizleme özelliği değil.</span><span class="sxs-lookup"><span data-stu-id="810f6-104">OpenAPI 2.0 (formerly Swagger) metadata support in Azure Functions is a preview feature that you can use to write an OpenAPI 2.0 definition inside a function app.</span></span> <span data-ttu-id="810f6-105">Bu dosyayı işlev uygulaması kullanarak ardından barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="810f6-105">You can then host that file by using the function app.</span></span>

<span data-ttu-id="810f6-106">[OpenAPI meta veri](http://swagger.io/) çok çeşitli diğer yazılımlar tarafından kullanılması için bir REST API barındıran bir işlev sağlar.</span><span class="sxs-lookup"><span data-stu-id="810f6-106">[OpenAPI metadata](http://swagger.io/) allows a function that's hosting a REST API to be consumed by a wide variety of other software.</span></span> <span data-ttu-id="810f6-107">Bu yazılım Microsoft teklifleri PowerApps gibi içerir ve [Azure App Service API Apps özelliğini](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), üçüncü taraf geliştirici araçları ister [Postman](https://www.getpostman.com/docs/importing_swagger), ve [pek çok daha fazla paket](http://swagger.io/tools/).</span><span class="sxs-lookup"><span data-stu-id="810f6-107">This software includes Microsoft offerings like PowerApps and the [API Apps feature of Azure App Service](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), third-party developer tools like [Postman](https://www.getpostman.com/docs/importing_swagger), and [many more packages](http://swagger.io/tools/).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
><span data-ttu-id="810f6-108">İle başlayan öneririz [başlama Öğreticisi](./functions-api-definition-getting-started.md) ve belirli özellikler hakkında daha fazla bilgi edinmek için bu belgeye döndürüyor.</span><span class="sxs-lookup"><span data-stu-id="810f6-108">We recommend starting with the [getting started tutorial](./functions-api-definition-getting-started.md) and then returning to this document to learn more about specific features.</span></span>

## <span data-ttu-id="810f6-109"><a name="enable"></a>OpenAPI tanımı desteğini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="810f6-109"><a name="enable"></a>Enable OpenAPI definition support</span></span>
<span data-ttu-id="810f6-110">Tüm OpenAPI ayarları yapılandırabilirsiniz **API tanımı** işlevi uygulamanızın sayfa **Platform özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="810f6-110">You can configure all OpenAPI settings on the **API Definition** page in your function app's **Platform features**.</span></span>

<span data-ttu-id="810f6-111">Barındırılan bir OpenAPI tanımı ve hızlı başlangıç tanım oluşturulmasını etkinleştirmek için ayarlanmış **API tanımı kaynak** için **işlevi (Önizleme)**.</span><span class="sxs-lookup"><span data-stu-id="810f6-111">To enable the generation of a hosted OpenAPI definition and a quickstart definition, set **API definition source** to **Function (Preview)**.</span></span> <span data-ttu-id="810f6-112">**Dış URL** başka bir yerde barındırılan bir OpenAPI tanımı kullanmak, işlevi sağlar.</span><span class="sxs-lookup"><span data-stu-id="810f6-112">**External URL** allows your function to use an OpenAPI definition that's hosted elsewhere.</span></span>

## <span data-ttu-id="810f6-113"><a name="generate-definition"></a>İşlevin meta verilerini Swagger çatıyı oluştur</span><span class="sxs-lookup"><span data-stu-id="810f6-113"><a name="generate-definition"></a>Generate a Swagger skeleton from your function's metadata</span></span>
<span data-ttu-id="810f6-114">Bir şablonu ilk OpenAPI tanımınızı yazma başlamanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="810f6-114">A template can help you start writing your first OpenAPI definition.</span></span> <span data-ttu-id="810f6-115">Tanımı şablon özelliği bir seyrek OpenAPI tanımı tüm meta verilerin function.json dosyasında her bir HTTP tetikleyicisi işlevlerinizi için kullanarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="810f6-115">The definition template feature creates a sparse OpenAPI definition by using all the metadata in the function.json file for each of your HTTP trigger functions.</span></span> <span data-ttu-id="810f6-116">API öğesinden hakkında daha fazla bilgi doldurmanız gerekir [OpenAPI belirtimi](http://swagger.io/specification/), istek ve yanıt şablonlar gibi.</span><span class="sxs-lookup"><span data-stu-id="810f6-116">You'll need to fill in more information about your API from the [OpenAPI specification](http://swagger.io/specification/), such as request and response templates.</span></span>

<span data-ttu-id="810f6-117">Adım adım yönergeler için bkz: [başlama Öğreticisi](./functions-api-definition-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="810f6-117">For step-by-step instructions, see the [getting started tutorial](./functions-api-definition-getting-started.md).</span></span>

### <span data-ttu-id="810f6-118"><a name="templates"></a>Kullanılabilir şablonlar</span><span class="sxs-lookup"><span data-stu-id="810f6-118"><a name="templates"></a>Available templates</span></span>

|<span data-ttu-id="810f6-119">Ad</span><span class="sxs-lookup"><span data-stu-id="810f6-119">Name</span></span>| <span data-ttu-id="810f6-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="810f6-120">Description</span></span> |
|:-----|:-----|
|<span data-ttu-id="810f6-121">Oluşturulan tanımı</span><span class="sxs-lookup"><span data-stu-id="810f6-121">Generated Definition</span></span>|<span data-ttu-id="810f6-122">Bir işlevin varolan meta verilerini çıkarsanabileceği bilgi maksimum OpenAPI tanımıyla.</span><span class="sxs-lookup"><span data-stu-id="810f6-122">An OpenAPI definition with the maximum amount of information that can be inferred from the function's existing metadata.</span></span>|

### <span data-ttu-id="810f6-123"><a name="quickstart-details"></a>Oluşturulan tanımı'nda bulunan meta verileri</span><span class="sxs-lookup"><span data-stu-id="810f6-123"><a name="quickstart-details"></a>Included metadata in the generated definition</span></span>

<span data-ttu-id="810f6-124">Oluşturulan Swagger çatıyı eşlenmiş olarak aşağıdaki tabloda Azure portal ayarları ve function.json karşılık gelen verileri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="810f6-124">The following table represents the Azure portal settings and corresponding data in function.json as it is mapped to the generated Swagger skeleton.</span></span>

|<span data-ttu-id="810f6-125">Swagger.JSON</span><span class="sxs-lookup"><span data-stu-id="810f6-125">Swagger.json</span></span>|<span data-ttu-id="810f6-126">Portal UI</span><span class="sxs-lookup"><span data-stu-id="810f6-126">Portal UI</span></span>|<span data-ttu-id="810f6-127">Function.JSON</span><span class="sxs-lookup"><span data-stu-id="810f6-127">Function.json</span></span>|
|:----|:-----|:-----|
|[<span data-ttu-id="810f6-128">Ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="810f6-128">Host</span></span>](http://swagger.io/specification/#fixed-fields-15)|<span data-ttu-id="810f6-129">**İşlev uygulaması ayarları** > **App Service ayarlarını** > **genel bakış** > **URL'si**</span><span class="sxs-lookup"><span data-stu-id="810f6-129">**Function app settings** > **App Service settings** > **Overview** > **URL**</span></span>|<span data-ttu-id="810f6-130">*Mevcut değil*</span><span class="sxs-lookup"><span data-stu-id="810f6-130">*Not present*</span></span>
|[<span data-ttu-id="810f6-131">Yolları</span><span class="sxs-lookup"><span data-stu-id="810f6-131">Paths</span></span>](http://swagger.io/specification/#paths-object-29)|<span data-ttu-id="810f6-132">**Tümleştirme** > **seçili HTTP yöntemleri**</span><span class="sxs-lookup"><span data-stu-id="810f6-132">**Integrate** > **Selected HTTP methods**</span></span>|<span data-ttu-id="810f6-133">Bağlamaları: yol</span><span class="sxs-lookup"><span data-stu-id="810f6-133">Bindings: Route</span></span>
|[<span data-ttu-id="810f6-134">Yol öğesi</span><span class="sxs-lookup"><span data-stu-id="810f6-134">Path Item</span></span>](http://swagger.io/specification/#path-item-object-32)|<span data-ttu-id="810f6-135">**Tümleştirme** > **rota şablonu**</span><span class="sxs-lookup"><span data-stu-id="810f6-135">**Integrate** > **Route template**</span></span>|<span data-ttu-id="810f6-136">Bağlamaları: yöntemler</span><span class="sxs-lookup"><span data-stu-id="810f6-136">Bindings: Methods</span></span>
|[<span data-ttu-id="810f6-137">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="810f6-137">Security</span></span>](http://swagger.io/specification/#security-scheme-object-112)|<span data-ttu-id="810f6-138">**Anahtarları**</span><span class="sxs-lookup"><span data-stu-id="810f6-138">**Keys**</span></span>|<span data-ttu-id="810f6-139">*Mevcut değil*</span><span class="sxs-lookup"><span data-stu-id="810f6-139">*Not present*</span></span>|
|<span data-ttu-id="810f6-140">Operationıd *</span><span class="sxs-lookup"><span data-stu-id="810f6-140">operationID*</span></span>|<span data-ttu-id="810f6-141">**Rota + izin verilen fiiller**</span><span class="sxs-lookup"><span data-stu-id="810f6-141">**Route + Allowed verbs**</span></span>|<span data-ttu-id="810f6-142">Rota + izin verilen fiiller</span><span class="sxs-lookup"><span data-stu-id="810f6-142">Route + Allowed Verbs</span></span>|

<span data-ttu-id="810f6-143">\*İşlem kimliği, yalnızca PowerApps ve akış ile tümleştirmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="810f6-143">\*The operation ID is required only for integrating with PowerApps and Flow.</span></span>
> [!NOTE]
> <span data-ttu-id="810f6-144">X-ms-Özet uzantısı bir görünen ad mantıksal uygulamalar, PowerApps ve akış sağlar.</span><span class="sxs-lookup"><span data-stu-id="810f6-144">The x-ms-summary extension provides a display name in Logic Apps, PowerApps, and Flow.</span></span>
>
> <span data-ttu-id="810f6-145">Daha fazla bilgi için bkz: [PowerApps için Swagger tanımı özelleştirme](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).</span><span class="sxs-lookup"><span data-stu-id="810f6-145">To learn more, see [Customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).</span></span>

## <span data-ttu-id="810f6-146"><a name="CICD"></a>CI/CD bir API tanımı ayarlamak için kullanın</span><span class="sxs-lookup"><span data-stu-id="810f6-146"><a name="CICD"></a>Use CI/CD to set an API definition</span></span>

 <span data-ttu-id="810f6-147">API tanımı, API tanımı kaynak denetiminden değiştirmek kaynak denetimi etkinleştirmeden önce portalda barındırma etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="810f6-147">You must enable API definition hosting in the portal before you enable source control to modify your API definition from source control.</span></span> <span data-ttu-id="810f6-148">Bu yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="810f6-148">Follow these instructions:</span></span>

1. <span data-ttu-id="810f6-149">Gözat **API tanımı (Önizleme)** işlevi uygulama ayarları'nda.</span><span class="sxs-lookup"><span data-stu-id="810f6-149">Browse to **API Definition (preview)** in your function app settings.</span></span>
  1. <span data-ttu-id="810f6-150">Ayarlama **API tanımı kaynak** için **işlevi**.</span><span class="sxs-lookup"><span data-stu-id="810f6-150">Set **API definition source** to **Function**.</span></span>
  1. <span data-ttu-id="810f6-151">Tıklatın **oluşturmak API tanımı şablonu** ve ardından **kaydetmek** daha sonra değiştirmek için bir şablon tanımı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="810f6-151">Click **Generate API definition template** and then **Save** to create a template definition for modifying later.</span></span>
  1. <span data-ttu-id="810f6-152">API tanımı URL'si ve anahtar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="810f6-152">Note your API definition URL and key.</span></span>
1. <span data-ttu-id="810f6-153">[Sürekli Tümleştirme/sürekli dağıtım (CI/CD) ayarlayın.](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).</span><span class="sxs-lookup"><span data-stu-id="810f6-153">[Set up continuous integration/continuous deployment (CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).</span></span>
2. <span data-ttu-id="810f6-154">Swagger.JSON \site\wwwroot adresindeki kaynak denetiminde değiştirme\.azurefunctions\swagger\swagger.json.</span><span class="sxs-lookup"><span data-stu-id="810f6-154">Modify swagger.json in source control at \site\wwwroot\.azurefunctions\swagger\swagger.json.</span></span>

<span data-ttu-id="810f6-155">Şimdi, deponuzun swagger.json değişiklikleri işlevi uygulamanızı API tarafından barındırılan tanımı URL'si ve de not ettiğiniz anahtarı adım 1.c.</span><span class="sxs-lookup"><span data-stu-id="810f6-155">Now, changes to swagger.json in your repository are hosted by your function app at the API definition URL and key that you noted in step 1.c.</span></span>

## <a name="next-steps"></a><span data-ttu-id="810f6-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="810f6-156">Next steps</span></span>
* <span data-ttu-id="810f6-157">[Başlangıç Öğreticisi](functions-api-definition-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="810f6-157">[Getting started tutorial](functions-api-definition-getting-started.md).</span></span> <span data-ttu-id="810f6-158">Bir eylem OpenAPI tanımında görmek için izlenecek deneyin.</span><span class="sxs-lookup"><span data-stu-id="810f6-158">Try our walkthrough to see an OpenAPI definition in action.</span></span>
* <span data-ttu-id="810f6-159">[Azure işlevleri GitHub deposunu](https://github.com/Azure/Azure-Functions/).</span><span class="sxs-lookup"><span data-stu-id="810f6-159">[Azure Functions GitHub repository](https://github.com/Azure/Azure-Functions/).</span></span> <span data-ttu-id="810f6-160">API tanımı destek Önizleme'bize geri bildirim sağlamak için işlevleri depo göz atın.</span><span class="sxs-lookup"><span data-stu-id="810f6-160">Check out the Functions repository to give us feedback on the API definition support preview.</span></span> <span data-ttu-id="810f6-161">GitHub sorunu güncelleştirilmiş görmek istediğiniz her şey için yapın.</span><span class="sxs-lookup"><span data-stu-id="810f6-161">Make a GitHub issue for anything you want to see updated.</span></span>
* <span data-ttu-id="810f6-162">[Azure işlevleri Geliştirici Başvurusu](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="810f6-162">[Azure Functions developer reference](functions-reference.md).</span></span> <span data-ttu-id="810f6-163">İşlevlerin kodlanması ve tetikleyicilerin ve bağlamaların tanımlanması hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="810f6-163">Learn about coding functions and defining triggers and bindings.</span></span>
