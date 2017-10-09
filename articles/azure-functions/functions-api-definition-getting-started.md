---
title: "Azure işlevleri OpenAPI meta verilerle başlatıldı aaaGetting | Microsoft Docs"
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
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="fdf36-103">OpenAPI 2.0 (Swagger) oluşturma (Önizleme) bir işlev uygulaması için meta veriler</span><span class="sxs-lookup"><span data-stu-id="fdf36-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="fdf36-104">Bu belgede Azure işlevlerini barındırılan basit bir API için OpenAPI tanımı oluşturma hello adım adım sürecinde size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="fdf36-104">This document guides you through hello step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="fdf36-105">OpenAPI (Swagger) nedir?</span><span class="sxs-lookup"><span data-stu-id="fdf36-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="fdf36-106">[Meta veri swagger](http://swagger.io/) hello işlevselliği tanımlayan bir dosyadır ve API'nizi modları işletim ve çeşitli diğer yazılımlar tarafından kullanılan REST API toobe barındıran bir işlev sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdf36-106">[Swagger Metadata](http://swagger.io/) is a file that defines hello functionality and operating modes of your API, and allows a function hosting a REST API toobe consumed by a wide variety of other software.</span></span> <span data-ttu-id="fdf36-107">Microsoft teklifleri ister PowerApps ve [API uygulamaları](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), gibi tooling 3 taraf geliştirici yanı sıra [Postman](https://www.getpostman.com/docs/importing_swagger) ve [pek çok daha fazla paket](http://swagger.io/tools/) tüm ile tüketilen, API toobe izin bir Swagger tanımı.</span><span class="sxs-lookup"><span data-stu-id="fdf36-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API toobe consumed with a Swagger definition.</span></span>

## <span data-ttu-id="fdf36-108"><a name="prepare-function"></a>Bir işlev ile basit bir API oluşturma</span><span class="sxs-lookup"><span data-stu-id="fdf36-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="fdf36-109">toocreate OpenAPI tanımı, ilk toocreate basit bir API işleviyle ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="fdf36-109">toocreate an OpenAPI definition, we first need toocreate a Function with a simple API.</span></span> <span data-ttu-id="fdf36-110">Bir işlev uygulaması üzerinde barındırılan bir API zaten varsa, düz toohello sonraki bölüme atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdf36-110">If you already have an API hosted on a Function App, you can skip straight toohello next section</span></span>
1. <span data-ttu-id="fdf36-111">Yeni bir işlev uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fdf36-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="fdf36-112">[Azure portal](https://portal.azure.com)  >  `+ New` > "İşlev uygulaması" için arama</span><span class="sxs-lookup"><span data-stu-id="fdf36-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="fdf36-113">Yeni işlev uygulamanız içinde yeni bir HTTP tetikleyicisi işlev oluştur</span><span class="sxs-lookup"><span data-stu-id="fdf36-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="fdf36-114">İşlevinizi tanımlama çok basit bir REST API'si ile önceden doldurulmuş haldedir kodudur.</span><span class="sxs-lookup"><span data-stu-id="fdf36-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="fdf36-115">"Hello {Giriş}" toohello işlevi hello gövdesinde veya bir sorgu parametresi olarak geçirilen herhangi bir dize döndürdü</span><span class="sxs-lookup"><span data-stu-id="fdf36-115">Any string passed toohello Function as a query parameter or in hello body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="fdf36-116">Toohello Git `Integrate` yeni HTTP tetikleyicisini işlevinizi sekmesi</span><span class="sxs-lookup"><span data-stu-id="fdf36-116">Go toohello `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="fdf36-117">İki durumlu `Allowed HTTP methods` çok`Selected methods`</span><span class="sxs-lookup"><span data-stu-id="fdf36-117">Toggle `Allowed HTTP methods` too`Selected methods`</span></span>
    1. <span data-ttu-id="fdf36-118">İçinde `Selected HTTP methods` her fiili POST dışında seçeneğinin işaretini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="fdf36-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="fdf36-119">![Seçili HTTP yöntemleri](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="fdf36-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="fdf36-120">Bu adım, daha sonra API tanımı basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="fdf36-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="fdf36-121"><a name="enable"></a>API tanımı desteğini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="fdf36-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="fdf36-122">Çok gidin`your function name` > `Platform Features` > `API Definition`
![tanım sekmesi](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="fdf36-122">Navigate too`your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="fdf36-123">Ayarlama `API Definition Source` çok`Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="fdf36-123">Set `API Definition Source` too`Function (preview)`</span></span>
    1. <span data-ttu-id="fdf36-124">Bu adım bir paketi bir uç nokta toohost işlevi uygulamanızın etki alanı, bir satır içi kopya hello OpenAPI dosyasından dahil olmak üzere, işlev uygulaması için OpenAPI seçeneklerini etkinleştirir [OpenAPI Düzenleyicisi](http://editor.swagger.io)ve bir hızlı başlangıç tanım Oluşturucu.</span><span class="sxs-lookup"><span data-stu-id="fdf36-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint toohost an OpenAPI file from your Function App's domain, an inline copy of hello [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="fdf36-125">![Etkin tanımı](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="fdf36-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="fdf36-126"><a name="create-definition"></a>Bir şablondan API tanımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fdf36-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="fdf36-127">Şuna tıklayın: `Generate API Definition template`</span><span class="sxs-lookup"><span data-stu-id="fdf36-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="fdf36-128">Bu adım işlevi uygulamanız HTTP tetikleyicisini işlevleri için tarar ve functions.json toogenerate OpenAPI belge hello bilgilerinizi kullanır.</span><span class="sxs-lookup"><span data-stu-id="fdf36-128">This step scans your Function App for HTTP Trigger functions and uses hello info in functions.json toogenerate an OpenAPI document.</span></span>
1. <span data-ttu-id="fdf36-129">Bir işlem nesnesi çok ekleme`paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="fdf36-129">Add an operation object too`paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="fdf36-130">tam bir OpenAPI Belge Anahattı Hello hızlı başlangıç OpenAPI belgedir. Daha fazla meta veri toobe işlemi nesneleri ve yanıt şablonlar gibi bir tam OpenAPI tanımı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fdf36-130">hello quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata toobe a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="fdf36-131">Hello örnek işlemi nesnesi aşağıdaki doldurulmuş bir bölüm oluşturur ve kullanır, bir parametre nesnesi ve yanıt nesnesi sahiptir.</span><span class="sxs-lookup"><span data-stu-id="fdf36-131">hello sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
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
    >  <span data-ttu-id="fdf36-132">x-ms-Özet bir görünen ad Logic Apps, akış ve PowerApps sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdf36-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="fdf36-133">Kullanıma [PowerApps için Swagger tanımı özelleştirme](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn daha fazla.</span><span class="sxs-lookup"><span data-stu-id="fdf36-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn more.</span></span>

1. <span data-ttu-id="fdf36-134">Tıklatın `save` toosave değişikliklerinizi ![şablonu tanımını ekleme](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="fdf36-134">Click `save` toosave your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="fdf36-135"><a name="use-definition"></a>API tanımı kullanma</span><span class="sxs-lookup"><span data-stu-id="fdf36-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="fdf36-136">Kopyalama, `API definition URL` ham OpenAPI belgenizi yeni bir tarayıcı sekmesi tooview yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="fdf36-136">Copy your `API definition URL` and paste it into a new browser tab tooview your raw OpenAPI document.</span></span>
1. <span data-ttu-id="fdf36-137">Test etme ve bu URL'yi kullanarak tümleştirme Araçlar OpenAPI belge tooany sayısı içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdf36-137">You can import your OpenAPI document tooany number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="fdf36-138">Çok sayıda Azure kullanarak OpenAPI belgenizi hello işlevi uygulama ayarlarınızı kaydedilmiş API tanımı URL'si mümkün tooautomatically alma kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="fdf36-138">Many Azure resources are able tooautomatically import your OpenAPI doc using hello API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="fdf36-139">Merhaba bir parçası olarak `Function` API tanımı kaynak, bu url, güncelleştiriyoruz.</span><span class="sxs-lookup"><span data-stu-id="fdf36-139">As a part of hello `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="fdf36-140"><a name="test-definition"></a>API tanımı Hello Swagger kullanıcı arabirimini tootest kullanma</span><span class="sxs-lookup"><span data-stu-id="fdf36-140"><a name="test-definition"></a>Using hello Swagger UI tootest your API definition</span></span>
<span data-ttu-id="fdf36-141">Karışık hello API tanımı Düzenleyicisi toohello UI görünümü içinde yerleşik araçlarını var. test.</span><span class="sxs-lookup"><span data-stu-id="fdf36-141">There are testing tools built in toohello UI view of hello imbedded API definition editor.</span></span> <span data-ttu-id="fdf36-142">API anahtarınızı ekleyin ve sonra hello `Try this operation` düğmesi her yöntemin altında.</span><span class="sxs-lookup"><span data-stu-id="fdf36-142">Add your API key, and then use hello `Try this operation` button under each method.</span></span> <span data-ttu-id="fdf36-143">API tanımı tooformat hello isteklerinizi Hello aracı kullanır ve başarılı yanıtları tanımınızı doğru olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdf36-143">hello tool will use your API Definition tooformat hello requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="fdf36-144">adımlar:</span><span class="sxs-lookup"><span data-stu-id="fdf36-144">Steps:</span></span>

1. <span data-ttu-id="fdf36-145">İşlev API anahtarınıza kopyalayın</span><span class="sxs-lookup"><span data-stu-id="fdf36-145">Copy your function API key</span></span>
    1. <span data-ttu-id="fdf36-146">Merhaba API anahtarı HTTP tetikleyicisi işlevinizi altında bulunabilir `function name` > `Keys` > `Function Keys` 
   ![işlev tuşu](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="fdf36-146">hello API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="fdf36-147">Toohello gidin `API Definition` sayfası.</span><span class="sxs-lookup"><span data-stu-id="fdf36-147">Navigate toohello `API Definition` page.</span></span>
    1. <span data-ttu-id="fdf36-148">Tıklatın `Authenticate` ve işlev API anahtar toohello güvenlik nesnenizin hello üstüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fdf36-148">Click `Authenticate` and add your Function API key toohello security object at hello top.</span></span>
  <span data-ttu-id="fdf36-149">![OpenAPI anahtarı](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="fdf36-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="fdf36-150">seçin`/api/yourfunctionroute` > `POST`</span><span class="sxs-lookup"><span data-stu-id="fdf36-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="fdf36-151">Tıklatın `Try it out` ve ad tootest girin</span><span class="sxs-lookup"><span data-stu-id="fdf36-151">Click `Try it out` and enter a name tootest</span></span>
1. <span data-ttu-id="fdf36-152">Başarı sonucu altında görmelisiniz `Pretty` 
 ![API tanımı test](./media/functions-api-definition-getting-started/definitionTest.png)</span><span class="sxs-lookup"><span data-stu-id="fdf36-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdf36-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fdf36-153">Next steps</span></span>
* [<span data-ttu-id="fdf36-154">OpenAPI tanımında işlevlerine genel bakış</span><span class="sxs-lookup"><span data-stu-id="fdf36-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="fdf36-155">Merhaba OpenAPI desteği hakkında daha fazla bilgi için tam belgelerini okuyun.</span><span class="sxs-lookup"><span data-stu-id="fdf36-155">Read hello full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="fdf36-156">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="fdf36-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="fdf36-157">İşlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için programcı başvurusu</span><span class="sxs-lookup"><span data-stu-id="fdf36-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="fdf36-158">Azure İşlevleri GitHub deposu</span><span class="sxs-lookup"><span data-stu-id="fdf36-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="fdf36-159">Merhaba işlevleri GitHub toogive bize hello API tanımı destek Önizleme geribildirim bakın!</span><span class="sxs-lookup"><span data-stu-id="fdf36-159">Check out hello Functions GitHub toogive us feedback on hello API definition support preview!</span></span> <span data-ttu-id="fdf36-160">GitHub sorunu güncelleştirilmiş toosee istediğiniz her şey için yapın.</span><span class="sxs-lookup"><span data-stu-id="fdf36-160">Make a GitHub issue for anything you'd like toosee updated.</span></span>
