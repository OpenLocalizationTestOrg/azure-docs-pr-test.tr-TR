---
title: "Azure işlevleri OpenAPI meta veriler ile çalışmaya başlama | Microsoft Docs"
description: "Başlarken OpenAPI desteğiyle Azure işlevleri"
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
ms.openlocfilehash: 9b861aacf31e17866293732dc2323f56014c1877
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="25db9-103">OpenAPI 2.0 (Swagger) oluşturma (Önizleme) bir işlev uygulaması için meta veriler</span><span class="sxs-lookup"><span data-stu-id="25db9-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="25db9-104">Bu belgede Azure işlevlerini barındırılan basit bir API için OpenAPI tanımı oluşturma adım adım sürecinde size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="25db9-104">This document guides you through the step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="25db9-105">OpenAPI (Swagger) nedir?</span><span class="sxs-lookup"><span data-stu-id="25db9-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="25db9-106">[Meta veri swagger](http://swagger.io/) işlevsellik ve API'nizi işletim modlarını tanımlar ve çeşitli diğer yazılımlar tarafından kullanılması için bir REST API barındırma işlevi sağlayan bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="25db9-106">[Swagger Metadata](http://swagger.io/) is a file that defines the functionality and operating modes of your API, and allows a function hosting a REST API to be consumed by a wide variety of other software.</span></span> <span data-ttu-id="25db9-107">Microsoft teklifleri ister PowerApps ve [API uygulamaları](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), gibi tooling 3 taraf geliştirici yanı sıra [Postman](https://www.getpostman.com/docs/importing_swagger) ve [pek çok daha fazla paket](http://swagger.io/tools/) tüm bir Swagger tanımı tüketilmesi API'nizi izin.</span><span class="sxs-lookup"><span data-stu-id="25db9-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API to be consumed with a Swagger definition.</span></span>

## <span data-ttu-id="25db9-108"><a name="prepare-function"></a>Bir işlev ile basit bir API oluşturma</span><span class="sxs-lookup"><span data-stu-id="25db9-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="25db9-109">OpenAPI tanımı oluşturmak için önce bir işlevi basit bir API oluşturmak ihtiyacımız.</span><span class="sxs-lookup"><span data-stu-id="25db9-109">To create an OpenAPI definition, we first need to create a Function with a simple API.</span></span> <span data-ttu-id="25db9-110">Bir işlev uygulaması üzerinde barındırılan bir API zaten varsa, doğrudan bir sonraki bölüme atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25db9-110">If you already have an API hosted on a Function App, you can skip straight to the next section</span></span>
1. <span data-ttu-id="25db9-111">Yeni bir işlev uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="25db9-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="25db9-112">[Azure portal](https://portal.azure.com)  >  `+ New` > "İşlev uygulaması" için arama</span><span class="sxs-lookup"><span data-stu-id="25db9-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="25db9-113">Yeni işlev uygulamanız içinde yeni bir HTTP tetikleyicisi işlev oluştur</span><span class="sxs-lookup"><span data-stu-id="25db9-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="25db9-114">İşlevinizi tanımlama çok basit bir REST API'si ile önceden doldurulmuş haldedir kodudur.</span><span class="sxs-lookup"><span data-stu-id="25db9-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="25db9-115">"Hello {Giriş}" sorgu parametresi olarak veya gövdedeki işleve herhangi bir dize döndürdü</span><span class="sxs-lookup"><span data-stu-id="25db9-115">Any string passed to the Function as a query parameter or in the body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="25db9-116">Git `Integrate` yeni HTTP tetikleyicisini işlevinizi sekmesi</span><span class="sxs-lookup"><span data-stu-id="25db9-116">Go to the `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="25db9-117">İki durumlu `Allowed HTTP methods` için`Selected methods`</span><span class="sxs-lookup"><span data-stu-id="25db9-117">Toggle `Allowed HTTP methods` to `Selected methods`</span></span>
    1. <span data-ttu-id="25db9-118">İçinde `Selected HTTP methods` her fiili POST dışında seçeneğinin işaretini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="25db9-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="25db9-119">![Seçili HTTP yöntemleri](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="25db9-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="25db9-120">Bu adım, daha sonra API tanımı basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="25db9-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="25db9-121"><a name="enable"></a>API tanımı desteğini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="25db9-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="25db9-122">Gidin `your function name`  >  `Platform Features`  >  `API Definition` 
 ![tanım sekmesi](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="25db9-122">Navigate to `your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="25db9-123">Ayarlama `API Definition Source` için`Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="25db9-123">Set `API Definition Source` to `Function (preview)`</span></span>
    1. <span data-ttu-id="25db9-124">Bu adım bir paketi işlevi uygulamanızın etki alanı, bir satır içi kopyasını OpenAPI dosyasından barındırmak için bir uç nokta da dahil olmak üzere, işlev uygulaması için OpenAPI seçeneklerini etkinleştirir [OpenAPI Düzenleyicisi](http://editor.swagger.io)ve bir hızlı başlangıç tanım Oluşturucu.</span><span class="sxs-lookup"><span data-stu-id="25db9-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint to host an OpenAPI file from your Function App's domain, an inline copy of the [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="25db9-125">![Etkin tanımı](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="25db9-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="25db9-126"><a name="create-definition"></a>Bir şablondan API tanımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="25db9-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="25db9-127">Şuna tıklayın: `Generate API Definition template`</span><span class="sxs-lookup"><span data-stu-id="25db9-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="25db9-128">Bu adım işlevi uygulamanız HTTP tetikleyicisini işlevleri için tarar ve OpenAPI belge oluşturmak için functions.json bilgilerinizi kullanır.</span><span class="sxs-lookup"><span data-stu-id="25db9-128">This step scans your Function App for HTTP Trigger functions and uses the info in functions.json to generate an OpenAPI document.</span></span>
1. <span data-ttu-id="25db9-129">İşlemi nesneye ekleme`paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="25db9-129">Add an operation object to `paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="25db9-130">Hızlı Başlangıç OpenAPI tam OpenAPI Belge Anahattı belgedir. Daha fazla meta veri işlemi nesneleri ve yanıt şablonlar gibi bir tam OpenAPI tanımı olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="25db9-130">The quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata to be a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="25db9-131">Aşağıdaki örnek işlemi nesnesi doldurulmuş bir bölüm oluşturur ve kullanır, bir parametre nesnesi ve yanıt nesnesi vardır.</span><span class="sxs-lookup"><span data-stu-id="25db9-131">The sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  <span data-ttu-id="25db9-132">x-ms-Özet bir görünen ad Logic Apps, akış ve PowerApps sağlar.</span><span class="sxs-lookup"><span data-stu-id="25db9-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="25db9-133">Kullanıma [PowerApps için Swagger tanımı özelleştirme](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="25db9-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) to learn more.</span></span>

1. <span data-ttu-id="25db9-134">Tıklatın `save` yaptığınız değişiklikleri kaydetmek için ![şablonu tanımını ekleme](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="25db9-134">Click `save` to save your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="25db9-135"><a name="use-definition"></a>API tanımı kullanma</span><span class="sxs-lookup"><span data-stu-id="25db9-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="25db9-136">Kopyalama, `API definition URL` ham OpenAPI belgeyi görüntülemek için yeni bir tarayıcı sekmesi yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="25db9-136">Copy your `API definition URL` and paste it into a new browser tab to view your raw OpenAPI document.</span></span>
1. <span data-ttu-id="25db9-137">Herhangi bir sayıda test etmek ve bu URL'yi kullanarak tümleştirme için Araçlar OpenAPI belgenizi aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25db9-137">You can import your OpenAPI document to any number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="25db9-138">Çok sayıda Azure kaynaklarını OpenAPI belgenizi işlevi uygulama ayarlarınızı kaydedilmiş API tanımı URL'si kullanarak otomatik olarak içeri aktaramıyor.</span><span class="sxs-lookup"><span data-stu-id="25db9-138">Many Azure resources are able to automatically import your OpenAPI doc using the API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="25db9-139">Bir parçası olarak `Function` API tanımı kaynak, bu url, güncelleştiriyoruz.</span><span class="sxs-lookup"><span data-stu-id="25db9-139">As a part of the `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="25db9-140"><a name="test-definition"></a>API tanımı test etmek için Swagger kullanıcı arabirimini kullanma</span><span class="sxs-lookup"><span data-stu-id="25db9-140"><a name="test-definition"></a>Using the Swagger UI to test your API definition</span></span>
<span data-ttu-id="25db9-141">Karışık API tanımı Düzenleyicisi'ni UI görünümüne yerleşik araçlar vardır test.</span><span class="sxs-lookup"><span data-stu-id="25db9-141">There are testing tools built in to the UI view of the imbedded API definition editor.</span></span> <span data-ttu-id="25db9-142">API anahtarınızı ekleyin ve ardından `Try this operation` düğmesi her yöntemin altında.</span><span class="sxs-lookup"><span data-stu-id="25db9-142">Add your API key, and then use the `Try this operation` button under each method.</span></span> <span data-ttu-id="25db9-143">Araç API tanımı istekleri biçimlendirmek için kullanır ve başarılı yanıtları tanımınızı doğru olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="25db9-143">The tool will use your API Definition to format the requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="25db9-144">adımlar:</span><span class="sxs-lookup"><span data-stu-id="25db9-144">Steps:</span></span>

1. <span data-ttu-id="25db9-145">İşlev API anahtarınıza kopyalayın</span><span class="sxs-lookup"><span data-stu-id="25db9-145">Copy your function API key</span></span>
    1. <span data-ttu-id="25db9-146">API anahtarını HTTP tetikleyicisi işlevinizi altında bulunabilir `function name` > `Keys` > `Function Keys` 
   ![işlev tuşu](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="25db9-146">The API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="25db9-147">Gidin `API Definition` sayfası.</span><span class="sxs-lookup"><span data-stu-id="25db9-147">Navigate to the `API Definition` page.</span></span>
    1. <span data-ttu-id="25db9-148">Tıklatın `Authenticate` ve üst güvenlik nesnesine işlevi API anahtarınızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="25db9-148">Click `Authenticate` and add your Function API key to the security object at the top.</span></span>
  <span data-ttu-id="25db9-149">![OpenAPI anahtarı](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="25db9-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="25db9-150">seçin`/api/yourfunctionroute` > `POST`</span><span class="sxs-lookup"><span data-stu-id="25db9-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="25db9-151">Tıklatın `Try it out` ve test etmek için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="25db9-151">Click `Try it out` and enter a name to test</span></span>
1. <span data-ttu-id="25db9-152">Başarı sonucu altında görmelisiniz `Pretty` 
 ![API tanımı test](./media/functions-api-definition-getting-started/definitionTest.png)</span><span class="sxs-lookup"><span data-stu-id="25db9-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="25db9-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="25db9-153">Next steps</span></span>
* [<span data-ttu-id="25db9-154">OpenAPI tanımında işlevlerine genel bakış</span><span class="sxs-lookup"><span data-stu-id="25db9-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="25db9-155">OpenAPI desteği hakkında daha fazla bilgi için tam belgelerini okuyun.</span><span class="sxs-lookup"><span data-stu-id="25db9-155">Read the full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="25db9-156">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="25db9-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="25db9-157">İşlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için programcı başvurusu</span><span class="sxs-lookup"><span data-stu-id="25db9-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="25db9-158">Azure İşlevleri GitHub deposu</span><span class="sxs-lookup"><span data-stu-id="25db9-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="25db9-159">API tanımı destek Önizleme'bize geri bildirim sağlamak için bu işlevler GitHub göz atın!</span><span class="sxs-lookup"><span data-stu-id="25db9-159">Check out the Functions GitHub to give us feedback on the API definition support preview!</span></span> <span data-ttu-id="25db9-160">GitHub sorunu görmek için güncelleştirilmiş istediğiniz her şey için yapın.</span><span class="sxs-lookup"><span data-stu-id="25db9-160">Make a GitHub issue for anything you'd like to see updated.</span></span>
