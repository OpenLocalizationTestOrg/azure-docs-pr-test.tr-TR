---
title: "Çağrı, tetikleyici veya HTTP uç noktaları - Azure Logic Apps ile iş akışı iç içe | Microsoft Docs"
description: "Çağrı, tetikleyici veya iş akışları için Azure Logic Apps iç içe için HTTP uç noktaları ayarlama"
services: logic-apps
keywords: "İş akışları, HTTP uç noktaları"
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: c92692db23ac59f67890e26cce6b2d3272e8901d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="34605-104">HTTP uç noktaları logic apps içinde iş akışlarıyla iç içe veya, tetikleyici çağırın</span><span class="sxs-lookup"><span data-stu-id="34605-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="34605-105">Böylece tetiklemek veya mantıksal uygulamalarınızı bir URL yoluyla çağrı logic apps Tetikleyicileri olarak zaman uyumlu HTTP uç noktaları yerel getirebilir.</span><span class="sxs-lookup"><span data-stu-id="34605-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="34605-106">Ayrıca, iş akışları aranabilir uç noktaları desenini kullanarak logic apps içinde yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34605-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="34605-107">HTTP uç noktaları oluşturmak için mantıksal uygulamalarınızı gelen istekleri alabilmesi tetikler ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34605-107">To create HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="34605-108">İstek</span><span class="sxs-lookup"><span data-stu-id="34605-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="34605-109">API bağlantı Web kancası</span><span class="sxs-lookup"><span data-stu-id="34605-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="34605-110">HTTP Web kancası</span><span class="sxs-lookup"><span data-stu-id="34605-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="34605-111">Örneklerde kullansa da **isteği** tetikleyici, listelenen HTTP Tetikleyicileri birini kullanabilirsiniz ve tüm ilkeler özdeş diğer tetikleyici türlerine uygulanır.</span><span class="sxs-lookup"><span data-stu-id="34605-111">Although our examples use the **Request** trigger, you can use any of the listed HTTP triggers, and all principles identically apply to the other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="34605-112">Mantıksal uygulamanız için bir HTTP uç nokta ayarlama</span><span class="sxs-lookup"><span data-stu-id="34605-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="34605-113">Bir HTTP uç noktası oluşturmak için gelen istekleri alabilen tetikleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34605-113">To create an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="34605-114">[Azure portalı](https://portal.azure.com "Azure portalı") oturumunu açın.</span><span class="sxs-lookup"><span data-stu-id="34605-114">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="34605-115">Mantıksal uygulamanızı gidin ve mantığı Uygulama Tasarımcısı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="34605-115">Go to your logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="34605-116">Gelen istekleri almak mantıksal uygulamanızı sağlayan bir tetikleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34605-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="34605-117">Örneğin, ekleyin **isteği** mantıksal uygulamanızı tetikleyiciye.</span><span class="sxs-lookup"><span data-stu-id="34605-117">For example, add the **Request** trigger to your logic app.</span></span>

3.  <span data-ttu-id="34605-118">Altında **iste gövde JSON şeması**, isteğe bağlı olarak bir JSON şeması almak için tetikleyici beklediğiniz için Yükü (veri) girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34605-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for the payload (data) that you expect the trigger to receive.</span></span>

    <span data-ttu-id="34605-119">Tasarımcı mantıksal uygulamanızı kullanmak, ayrıştırma ve tetikleyici, iş akışı aracılığıyla veri geçirmek için kullanabileceğiniz belirteçleri oluşturmak için bu şemayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="34605-119">The designer uses this schema for generating tokens that your logic app can use to consume, parse, and pass data from the trigger through your workflow.</span></span> 
    <span data-ttu-id="34605-120">Hakkında daha fazla bilgi [JSON şemaları oluşturulan belirteçleri](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="34605-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="34605-121">Bu örnekte, Tasarımcısı'nda gösterilen şema girin:</span><span class="sxs-lookup"><span data-stu-id="34605-121">For this example, enter the schema shown in the designer:</span></span>

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![İstek Eylem Ekle][1]

    > [!TIP]
    > 
    > <span data-ttu-id="34605-123">Örnek bir JSON yükü için bir şema gibi bir araçtan oluşturabileceğiniz [jsonschema.net](http://jsonschema.net/), veya **isteği** seçerek tetikleyici **şema üretmek için kullanım örnek yük**.</span><span class="sxs-lookup"><span data-stu-id="34605-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in the **Request** trigger by choosing **Use sample payload to generate schema**.</span></span> 
    > <span data-ttu-id="34605-124">Örnek yükünüzü girin ve seçin **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="34605-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="34605-125">Örneğin, bu örnek yükü:</span><span class="sxs-lookup"><span data-stu-id="34605-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="34605-126">Bu şemayı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="34605-126">generates this schema:</span></span>

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  <span data-ttu-id="34605-127">Mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="34605-127">Save your logic app.</span></span> <span data-ttu-id="34605-128">Altında **bu URL için HTTP POST**, artık bu örnek gibi bir oluşturulan geri çağırma URL'si bulmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="34605-128">Under **HTTP POST to this URL**, you should now find a generated callback URL, like this example:</span></span>

    ![Uç noktası için oluşturulan geri çağırma URL'si](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="34605-130">Bu URL'yi bir paylaşılan erişim imzası (SAS) anahtarı kimlik doğrulaması için kullanılan sorgu parametrelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="34605-130">This URL contains a Shared Access Signature (SAS) key in the query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="34605-131">Azure portalında, mantığı uygulama genel bakış gelen HTTP uç noktası URL'si de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34605-131">You can also get the HTTP endpoint URL from your logic app overview in the Azure portal.</span></span> <span data-ttu-id="34605-132">Altında **tetikleyici geçmişi**, tetikleyici seçin:</span><span class="sxs-lookup"><span data-stu-id="34605-132">Under **Trigger History**, select your trigger:</span></span>

    ![Azure Portalı'ndan HTTP uç noktasının URL'sini alın][2]

    <span data-ttu-id="34605-134">Veya bu çağrı yaparak URL'yi elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34605-134">Or you can get the URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-the-http-method-for-your-trigger"></a><span data-ttu-id="34605-135">Tetikleyicinizin HTTP yöntemini değiştirme</span><span class="sxs-lookup"><span data-stu-id="34605-135">Change the HTTP method for your trigger</span></span>

<span data-ttu-id="34605-136">Varsayılan olarak, **isteği** tetikleyici bir HTTP POST isteği bekliyor, ancak farklı bir HTTP yöntemini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34605-136">By default, the **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="34605-137">Yalnızca bir yöntem türü belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34605-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="34605-138">Üzerinde **isteği** tetikleyin, seçin **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="34605-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="34605-139">Açık **yöntemi** listesi.</span><span class="sxs-lookup"><span data-stu-id="34605-139">Open the **Method** list.</span></span> <span data-ttu-id="34605-140">Bu örnek için select **almak** böylece HTTP uç noktanın URL'sini daha sonra test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34605-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="34605-141">Herhangi bir HTTP yöntemini seçin veya özel bir yöntem için kendi mantıksal uygulama belirtin.</span><span class="sxs-lookup"><span data-stu-id="34605-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![HTTP yöntemini değiştirme](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="34605-143">HTTP uç nokta URL'nizi aracılığıyla parametreleri kabul et</span><span class="sxs-lookup"><span data-stu-id="34605-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="34605-144">Parametreler kabul etmek için HTTP uç nokta URL'nizi istediğinizde, tetikleyicinin göreli yol özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="34605-144">When you want your HTTP endpoint URL to accept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="34605-145">Üzerinde **isteği** tetikleyin, seçin **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="34605-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="34605-146">Altında **yöntemi**, isteğiniz kullanmak istediğiniz HTTP yöntemini belirtin.</span><span class="sxs-lookup"><span data-stu-id="34605-146">Under **Method**, specify the HTTP method that you want your request to use.</span></span> <span data-ttu-id="34605-147">Bu örnek için select **almak** böylece HTTP uç noktanın URL'sini test, yapmadıysanız yöntemi.</span><span class="sxs-lookup"><span data-stu-id="34605-147">For this example, select the **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="34605-148">Tetikleyici için göreli bir yol belirttiğinizde, tetikleyici için bir HTTP yöntemini de açıkça belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="34605-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="34605-149">Altında **göreli yol**, URL'niz, örneğin, kabul etmelidir parametresi göreli yolunu belirtin `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="34605-149">Under **Relative path**, specify the relative path for the parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Parametre için göreli yolu ve HTTP yöntemini belirtin](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="34605-151">Parametre kullanmak için ekleyin bir **yanıt** mantığı uygulamanıza eylem.</span><span class="sxs-lookup"><span data-stu-id="34605-151">To use the parameter, add a **Response** action to your logic app.</span></span> <span data-ttu-id="34605-152">(Seçin, tetikleyici altında **yeni adım** > **Eylem Ekle** > **yanıt**)</span><span class="sxs-lookup"><span data-stu-id="34605-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="34605-153">Yanıt 's **gövde**, belirtecin, tetikleyicinin göreli yolda belirtilen parametresi için içerir.</span><span class="sxs-lookup"><span data-stu-id="34605-153">In your response's **Body**, include the token for the parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="34605-154">Örneğin, döndürülecek `Hello {customerID}`, yanıtın güncelleştirme **gövde** ile `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="34605-154">For example, to return `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="34605-155">Dinamik içerik listesi görüntülenir ve Göster `customerID` seçebilmeniz için belirteç.</span><span class="sxs-lookup"><span data-stu-id="34605-155">The dynamic content list should appear and show the `customerID` token for you to select.</span></span>

    ![Yanıt gövdesi için parametre ekleme](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="34605-157">**Gövde** bu örnekteki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="34605-157">Your **Body** should look like this example:</span></span>

    ![Yanıt gövdesi parametresi](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="34605-159">Mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="34605-159">Save your logic app.</span></span> 

    <span data-ttu-id="34605-160">HTTP uç nokta URL'nizi şimdi Örneğin, göreli yol içerir:</span><span class="sxs-lookup"><span data-stu-id="34605-160">Your HTTP endpoint URL now includes the relative path, for example:</span></span> 

    <span data-ttu-id="34605-161">HTTPS & # 58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="34605-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="34605-162">HTTP uç noktanızı sınamak için kopyalamak ve güncelleştirilmiş URL başka bir tarayıcı penceresine yapıştırın, ancak yerine `{customerID}` ile `123456`, ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="34605-162">To test your HTTP endpoint, copy and paste the updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="34605-163">Tarayıcınız bu metin göstermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="34605-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="34605-164">Mantıksal uygulamanız için JSON şemaları üretilen belirteçleri</span><span class="sxs-lookup"><span data-stu-id="34605-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="34605-165">Bir JSON şeması sağladığınız zaman, **isteği** tetikleyici, mantığı Uygulama Tasarımcısı'nı bu şemada özellikleri için belirteçleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="34605-165">When you provide a JSON schema in your **Request** trigger, the Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="34605-166">Mantıksal uygulama akışı aracılığıyla veri geçirme daha sonra bu belirteçleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34605-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="34605-167">Bu örneğin eklerseniz, `title` ve `name` özellikleri JSON şeması için kendi belirteçleri şimdi sonraki iş akışı adımlarda kullanmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="34605-167">For this example, if you add the `title` and `name` properties to your JSON schema, their tokens are now available to use in later workflow steps.</span></span> 

<span data-ttu-id="34605-168">Tam JSON şeması şöyledir:</span><span class="sxs-lookup"><span data-stu-id="34605-168">Here is the complete JSON schema:</span></span>

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="34605-169">Logic apps iç içe geçmiş iş akışları oluşturmak</span><span class="sxs-lookup"><span data-stu-id="34605-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="34605-170">İstekleri alabilen diğer mantıksal uygulamalar ekleyerek mantıksal uygulamanızı iş akışları yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34605-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="34605-171">Bu mantıksal uygulamalar dahil etmek için ekleyin **Azure Logic Apps - Logic Apps iş akışı seçin** , tetikleyici için eylem.</span><span class="sxs-lookup"><span data-stu-id="34605-171">To include these logic apps, add the **Azure Logic Apps - Choose a Logic Apps workflow** action to your trigger.</span></span> <span data-ttu-id="34605-172">Daha sonra uygun mantığı uygulamalardan seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34605-172">You can then select from eligible logic apps.</span></span>

![Başka bir mantıksal uygulama Ekle](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="34605-174">HTTP uç noktaları aracılığıyla logic apps tetiklemek veya çağırın</span><span class="sxs-lookup"><span data-stu-id="34605-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="34605-175">HTTP uç noktanızı oluşturduktan sonra mantıksal uygulamanızı aracılığıyla tetikleyebilir bir `POST` yöntemi tam URL.</span><span class="sxs-lookup"><span data-stu-id="34605-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method to the full URL.</span></span> <span data-ttu-id="34605-176">Logic apps doğrudan erişimli uç noktaları için yerleşik destek vardır.</span><span class="sxs-lookup"><span data-stu-id="34605-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="34605-177">Gelen istek başvuru içeriği</span><span class="sxs-lookup"><span data-stu-id="34605-177">Reference content from an incoming request</span></span>

<span data-ttu-id="34605-178">İçeriğin türü ise `application/json`, gelen istekte özelliklerine başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34605-178">If the content's type is `application/json`, you can reference properties from the incoming request.</span></span> <span data-ttu-id="34605-179">Aksi takdirde, içeriği diğer API'leri geçirebilirsiniz tek bir ikili birim olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="34605-179">Otherwise, content is treated as a single binary unit that you can pass to other APIs.</span></span> <span data-ttu-id="34605-180">Bu içerik iş akışı içinde başvurmak için bu içeriği dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="34605-180">To reference this content inside the workflow, you must convert that content.</span></span> <span data-ttu-id="34605-181">Örneğin, geçirdiğiniz `application/xml` içerik, kullanabileceğiniz `@xpath()` bir XPath ayıklama için veya `@json()` XML JSON değerine dönüştürmek için.</span><span class="sxs-lookup"><span data-stu-id="34605-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML to JSON.</span></span> <span data-ttu-id="34605-182">Hakkında bilgi edinin [içerik türleriyle çalışma](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="34605-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="34605-183">Gelen bir istekte çıkış almak için kullanabileceğiniz `@triggerOutputs()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="34605-183">To get the output from an incoming request, you can use the `@triggerOutputs()` function.</span></span> <span data-ttu-id="34605-184">Çıktı aşağıdaki örnekte olduğu gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="34605-184">The output might look like this example:</span></span>

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

<span data-ttu-id="34605-185">Erişim için `body` özelliği özellikle kullanabileceğiniz `@triggerBody()` kısayol.</span><span class="sxs-lookup"><span data-stu-id="34605-185">To access the `body` property specifically, you can use the `@triggerBody()` shortcut.</span></span> 

## <a name="respond-to-requests"></a><span data-ttu-id="34605-186">İsteklerine yanıt</span><span class="sxs-lookup"><span data-stu-id="34605-186">Respond to requests</span></span>

<span data-ttu-id="34605-187">Bir mantıksal uygulama çağırana içerik döndürerek Başlat belirli isteklere yanıt verecek şekilde isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34605-187">You might want to respond to certain requests that start a logic app by returning content to the caller.</span></span> <span data-ttu-id="34605-188">Durum kodu, başlığı ve yanıt için gövde oluşturmak için kullanabileceğiniz **yanıt** eylem.</span><span class="sxs-lookup"><span data-stu-id="34605-188">To construct the status code, header, and body for your response, you can use the **Response** action.</span></span> <span data-ttu-id="34605-189">Bu eylem yalnızca, iş akışınızı sonunda mantıksal uygulamanızı herhangi bir yere görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="34605-189">This action can appear anywhere in your logic app, not just at the end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="34605-190">Mantıksal uygulamanızı içermiyorsa bir **yanıt**, HTTP uç noktası yanıt *hemen* ile bir **202 kabul edilen** durumu.</span><span class="sxs-lookup"><span data-stu-id="34605-190">If your logic app doesn't include a **Response**, the HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="34605-191">Ayrıca, özgün istek yanıt almak için yanıt için gereken tüm adımları içinde bitmesi gereken [istek zaman aşımı sınırı](./logic-apps-limits-and-config.md) iş akışı iç içe geçmiş mantıksal uygulama olarak gerektirmediği sürece.</span><span class="sxs-lookup"><span data-stu-id="34605-191">Also, for the original request to get the response, all steps required for the response must finish within the [request timeout limit](./logic-apps-limits-and-config.md) unless you call the workflow as a nested logic app.</span></span> <span data-ttu-id="34605-192">Yanıt bu sınırı içinde olursa, gelen istek zaman aşımına uğradı ve HTTP yanıtı alır **408 istemci zaman aşımı**.</span><span class="sxs-lookup"><span data-stu-id="34605-192">If no response happens within this limit, the incoming request times out and receives the HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="34605-193">İç içe geçmiş logic apps için üst mantıksal uygulama yanıt ne kadar zaman gerekli olduğuna bakılmaksızın, tamamlanana kadar beklemeye devam eder.</span><span class="sxs-lookup"><span data-stu-id="34605-193">For nested logic apps, the parent logic app continues to wait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-the-response"></a><span data-ttu-id="34605-194">Yapı yanıt</span><span class="sxs-lookup"><span data-stu-id="34605-194">Construct the response</span></span>

<span data-ttu-id="34605-195">Yanıt gövdesi içinde birden fazla üst bilgi ve içerik herhangi bir türde içerebilir.</span><span class="sxs-lookup"><span data-stu-id="34605-195">You can include more than one header and any type of content in the response body.</span></span> <span data-ttu-id="34605-196">Yanıtın içerik türü var. bizim örnek yanıt üstbilgisini belirtir `application/json`.</span><span class="sxs-lookup"><span data-stu-id="34605-196">In our example response, the header specifies that the response has content type `application/json`.</span></span> <span data-ttu-id="34605-197">ve gövde içeren `title` ve `name`bağlı için daha önce güncelleştirilmiş JSON şeması olarak **isteği** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="34605-197">and the body contains `title` and `name`, based on the JSON schema updated previously for the **Request** trigger.</span></span>

![HTTP yanıtının eylem][3]

<span data-ttu-id="34605-199">Yanıtları bu özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="34605-199">Responses have these properties:</span></span>

| <span data-ttu-id="34605-200">Özellik</span><span class="sxs-lookup"><span data-stu-id="34605-200">Property</span></span> | <span data-ttu-id="34605-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34605-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="34605-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="34605-202">statusCode</span></span> |<span data-ttu-id="34605-203">Gelen istek için yanıt için HTTP durum kodu belirtir.</span><span class="sxs-lookup"><span data-stu-id="34605-203">Specifies the HTTP status code for responding to the incoming request.</span></span> <span data-ttu-id="34605-204">Bu kod 2xx, 4xx veya 5xx ile başlayan tüm geçerli durum kodu olabilir.</span><span class="sxs-lookup"><span data-stu-id="34605-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="34605-205">Ancak, 3xx durum kodları izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="34605-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="34605-206">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="34605-206">headers</span></span> |<span data-ttu-id="34605-207">Yanıta eklenecek üstbilgi herhangi bir sayıda tanımlar.</span><span class="sxs-lookup"><span data-stu-id="34605-207">Defines any number of headers to include in the response.</span></span> |
| <span data-ttu-id="34605-208">Gövde</span><span class="sxs-lookup"><span data-stu-id="34605-208">body</span></span> |<span data-ttu-id="34605-209">Bir dize olabilir bir gövde nesnesi, JSON nesnesi veya bir önceki adımda başvurulan bile ikili içerik belirtir.</span><span class="sxs-lookup"><span data-stu-id="34605-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="34605-210">İşte JSON şeması nasıl şimdi göründüğünü **yanıt** eylem:</span><span class="sxs-lookup"><span data-stu-id="34605-210">Here's what the JSON schema looks like now for the **Response** action:</span></span>

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> <span data-ttu-id="34605-211">Mantıksal uygulamanız için tam JSON tanımını mantığı uygulama Designer'ı görüntülemek için seçin **kod görünümü**.</span><span class="sxs-lookup"><span data-stu-id="34605-211">To view the complete JSON definition for your logic app, on the Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="34605-212">Soru-Cevap</span><span class="sxs-lookup"><span data-stu-id="34605-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="34605-213">S: ne hakkında URL güvenlik?</span><span class="sxs-lookup"><span data-stu-id="34605-213">Q: What about URL security?</span></span>

<span data-ttu-id="34605-214">Y: azure güvenli bir şekilde bir paylaşılan erişim imzası (SAS) kullanarak logic app geri çağırma URL'leri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="34605-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="34605-215">Bu imza sorgu parametresi olarak geçtiği ve mantıksal uygulamanızı tetikleyebilir önce doğrulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34605-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="34605-216">Azure mantıksal uygulama, tetikleyici adı ve gerçekleştirilir işlemi başına gizli bir anahtar benzersiz bir birleşimini kullanarak imza oluşturur.</span><span class="sxs-lookup"><span data-stu-id="34605-216">Azure generates the signature using a unique combination of a secret key per logic app, the trigger name, and the operation that's performed.</span></span> <span data-ttu-id="34605-217">Bu nedenle birisi gizli mantığı uygulama anahtarı erişimi sürece, geçerli bir imzası oluşturulamaz.</span><span class="sxs-lookup"><span data-stu-id="34605-217">So unless someone has access to the secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="34605-218">Üretim ve güvenli sistemler için mantıksal uygulamanızı doğrudan tarayıcıdan çünkü çağırma karşı önerilir:</span><span class="sxs-lookup"><span data-stu-id="34605-218">For production and secure systems, we strongly recommend against calling your logic app directly from the browser because:</span></span>
   > 
   > * <span data-ttu-id="34605-219">Paylaşılan erişim anahtarı URL'de görünür.</span><span class="sxs-lookup"><span data-stu-id="34605-219">The shared access key appears in the URL.</span></span>
   > * <span data-ttu-id="34605-220">Mantıksal uygulama müşterileri arasında paylaşılan etki alanları nedeniyle güvenli içerik ilkeleri yönetemez.</span><span class="sxs-lookup"><span data-stu-id="34605-220">You can't manage secure content policies due to shared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="34605-221">S: daha fazla HTTP uç noktaları yapılandırabilir?</span><span class="sxs-lookup"><span data-stu-id="34605-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="34605-222">A: Evet HTTP uç noktaları aracılığıyla daha gelişmiş yapılandırma desteği [ **API Management**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="34605-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="34605-223">Bu hizmet, tutarlı bir şekilde mantıksal uygulamalar dahil olmak üzere tüm Apı'lerinizi, yönetme, özel etki alanı adlarını ayarlama, daha fazla kimlik doğrulama yöntemleri ve daha fazla bilgi, örneğin kullanmak özelliği de sunar:</span><span class="sxs-lookup"><span data-stu-id="34605-223">This service also offers the capability for you to consistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="34605-224">Değişiklik isteği yöntemi</span><span class="sxs-lookup"><span data-stu-id="34605-224">Change the request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="34605-225">İsteğin URL kesimleri değiştirme</span><span class="sxs-lookup"><span data-stu-id="34605-225">Change the URL segments of the request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="34605-226">API Management alanlarında ayarlama [Azure portal](https://portal.azure.com/ "Azure portalı")</span><span class="sxs-lookup"><span data-stu-id="34605-226">Set up your API Management domains in the [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="34605-227">Temel kimlik doğrulaması için denetlenecek ilkesini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="34605-227">Set up policy to check for Basic authentication</span></span>

#### <a name="q-what-changed-when-the-schema-migrated-from-the-december-1-2014-preview"></a><span data-ttu-id="34605-228">S: şema 1 Aralık 2014 Önizlemesi'nden geçirilen ne değiştirilir?</span><span class="sxs-lookup"><span data-stu-id="34605-228">Q: What changed when the schema migrated from the December 1, 2014 preview?</span></span>

<span data-ttu-id="34605-229">A: Bu değişiklikler hakkında bir özeti aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="34605-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="34605-230">1 Aralık 2014 Önizleme</span><span class="sxs-lookup"><span data-stu-id="34605-230">December 1, 2014 preview</span></span> | <span data-ttu-id="34605-231">1 Haziran 2016</span><span class="sxs-lookup"><span data-stu-id="34605-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="34605-232">Tıklatın **HTTP dinleyicisi** API uygulaması</span><span class="sxs-lookup"><span data-stu-id="34605-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="34605-233">Tıklatın **el ile tetikleyici** (hiçbir API uygulaması gereklidir)</span><span class="sxs-lookup"><span data-stu-id="34605-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="34605-234">HTTP dinleyicisi ayarı "*yanıt otomatik olarak gönderir*"</span><span class="sxs-lookup"><span data-stu-id="34605-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="34605-235">Ya da dahil bir **yanıt** eylem veya iş akışı tanımı içinde değil</span><span class="sxs-lookup"><span data-stu-id="34605-235">Either include a **Response** action or not in the workflow definition</span></span> |
| <span data-ttu-id="34605-236">Temel veya OAuth kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34605-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="34605-237">API Yönetimi</span><span class="sxs-lookup"><span data-stu-id="34605-237">via API Management</span></span> |
| <span data-ttu-id="34605-238">HTTP yöntemini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34605-238">Configure HTTP method</span></span> |<span data-ttu-id="34605-239">Altında **Gelişmiş Seçenekleri Göster**, bir HTTP yöntemini seçin</span><span class="sxs-lookup"><span data-stu-id="34605-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="34605-240">Göreli yolunu Yapılandır</span><span class="sxs-lookup"><span data-stu-id="34605-240">Configure relative path</span></span> |<span data-ttu-id="34605-241">Altında **Gelişmiş Seçenekleri Göster**, göreli bir yol ekleme</span><span class="sxs-lookup"><span data-stu-id="34605-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="34605-242">Üzerinden gelen gövde başvurusu`@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="34605-242">Reference the incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="34605-243">Aracılığıyla başvurusu`@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="34605-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="34605-244">**HTTP yanıt gönderme** HTTP dinleyicisi eylemi</span><span class="sxs-lookup"><span data-stu-id="34605-244">**Send HTTP response** action on the HTTP Listener</span></span> |<span data-ttu-id="34605-245">Tıklatın **HTTP isteğine yanıt** (hiçbir API uygulaması gereklidir)</span><span class="sxs-lookup"><span data-stu-id="34605-245">Click **Respond to HTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="34605-246">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="34605-246">Get help</span></span>

<span data-ttu-id="34605-247">Sorular sormak, soruları yanıtlamak ve diğer Azure Logic Apps kullanıcılarının neler yaptığını öğrenmek için [Azure Logic Apps forumunu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="34605-247">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="34605-248">Azure Logic Apps ve bağlayıcıları geliştirmeye yardımcı olmak için, [Azure Logic Apps kullanıcı geri bildirim sitesinde](http://aka.ms/logicapps-wish) oy kullanın veya fikirlerinizi paylaşın.</span><span class="sxs-lookup"><span data-stu-id="34605-248">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34605-249">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34605-249">Next steps</span></span>

* [<span data-ttu-id="34605-250">Mantıksal uygulama tanımları yazma</span><span class="sxs-lookup"><span data-stu-id="34605-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="34605-251">Hataları ve özel durumları işleme</span><span class="sxs-lookup"><span data-stu-id="34605-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
