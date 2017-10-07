---
title: "aaaCall, tetikleyin veya HTTP uç noktaları - Azure Logic Apps ile iş akışı iç içe | Microsoft Docs"
description: "HTTP uç noktaları toocall, tetikleyici veya iç içe iş akışları için Azure Logic Apps ayarlamanız"
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
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="a1a0d-104">HTTP uç noktaları logic apps içinde iş akışlarıyla iç içe veya, tetikleyici çağırın</span><span class="sxs-lookup"><span data-stu-id="a1a0d-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="a1a0d-105">Böylece tetiklemek veya mantıksal uygulamalarınızı bir URL yoluyla çağrı logic apps Tetikleyicileri olarak zaman uyumlu HTTP uç noktaları yerel getirebilir.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="a1a0d-106">Ayrıca, iş akışları aranabilir uç noktaları desenini kullanarak logic apps içinde yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="a1a0d-107">toocreate HTTP uç noktaları, gelen istekleri mantıksal uygulamalarınızı alabilmesi tetikler ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-107">toocreate HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="a1a0d-108">İstek</span><span class="sxs-lookup"><span data-stu-id="a1a0d-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="a1a0d-109">API bağlantı Web kancası</span><span class="sxs-lookup"><span data-stu-id="a1a0d-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="a1a0d-110">HTTP Web kancası</span><span class="sxs-lookup"><span data-stu-id="a1a0d-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="a1a0d-111">Örneklerde hello kullansa da **isteği** tetikleyici, kullanabileceğiniz herhangi birini hello listelenen HTTP tetikleyiciler ve tüm ilkeler, toohello özdeş diğer tetikleyici türleri uygulanır..</span><span class="sxs-lookup"><span data-stu-id="a1a0d-111">Although our examples use hello **Request** trigger, you can use any of hello listed HTTP triggers, and all principles identically apply toohello other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="a1a0d-112">Mantıksal uygulamanız için bir HTTP uç nokta ayarlama</span><span class="sxs-lookup"><span data-stu-id="a1a0d-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="a1a0d-113">bir HTTP uç noktası toocreate gelen istekleri alabilen tetikleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-113">toocreate an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="a1a0d-114">İçinde toohello oturum [Azure portal](https://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="a1a0d-114">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="a1a0d-115">Tooyour mantıksal uygulama gidin ve mantığı Uygulama Tasarımcısı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-115">Go tooyour logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="a1a0d-116">Gelen istekleri almak mantıksal uygulamanızı sağlayan bir tetikleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="a1a0d-117">Örneğin, hello ekleyin **isteği** tetikleyici tooyour mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-117">For example, add hello **Request** trigger tooyour logic app.</span></span>

3.  <span data-ttu-id="a1a0d-118">Altında **iste gövde JSON şeması**, isteğe bağlı olarak bir JSON şeması hello tetikleyici tooreceive beklediğiniz hello için Yükü (veri) girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for hello payload (data) that you expect hello trigger tooreceive.</span></span>

    <span data-ttu-id="a1a0d-119">Merhaba Tasarımcısı mantıksal uygulamanızı tooconsume, ayrıştırma ve hello tetikleyici, iş akışı aracılığıyla geçişi veriler kullanabileceğiniz belirteçleri oluşturmak için bu şemayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-119">hello designer uses this schema for generating tokens that your logic app can use tooconsume, parse, and pass data from hello trigger through your workflow.</span></span> 
    <span data-ttu-id="a1a0d-120">Hakkında daha fazla bilgi [JSON şemaları oluşturulan belirteçleri](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="a1a0d-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="a1a0d-121">Bu örnekte, hello Tasarımcısı'nda gösterilen hello şema girin:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-121">For this example, enter hello schema shown in hello designer:</span></span>

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

    ![Merhaba isteği Eylem Ekle][1]

    > [!TIP]
    > 
    > <span data-ttu-id="a1a0d-123">Örnek bir JSON yükü için bir şema gibi bir araçtan oluşturabileceğiniz [jsonschema.net](http://jsonschema.net/), veya hello **isteği** seçerek tetikleyici **kullanım örnek yükü toogenerate şeması**.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in hello **Request** trigger by choosing **Use sample payload toogenerate schema**.</span></span> 
    > <span data-ttu-id="a1a0d-124">Örnek yükünüzü girin ve seçin **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="a1a0d-125">Örneğin, bu örnek yükü:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="a1a0d-126">Bu şemayı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-126">generates this schema:</span></span>

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

4.  <span data-ttu-id="a1a0d-127">Mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-127">Save your logic app.</span></span> <span data-ttu-id="a1a0d-128">Altında **HTTP POST toothis URL**, artık bu örnek gibi bir oluşturulan geri çağırma URL'si bulmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-128">Under **HTTP POST toothis URL**, you should now find a generated callback URL, like this example:</span></span>

    ![Uç noktası için oluşturulan geri çağırma URL'si](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="a1a0d-130">Bu URL'yi bir paylaşılan erişim imzası (SAS) anahtarı kimlik doğrulaması için kullanılan hello sorgu parametrelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-130">This URL contains a Shared Access Signature (SAS) key in hello query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="a1a0d-131">Hello Azure portal, mantığı uygulama genel bakış gelen hello HTTP uç noktası URL'si de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-131">You can also get hello HTTP endpoint URL from your logic app overview in hello Azure portal.</span></span> <span data-ttu-id="a1a0d-132">Altında **tetikleyici geçmişi**, tetikleyici seçin:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-132">Under **Trigger History**, select your trigger:</span></span>

    ![Azure Portalı'ndan HTTP uç noktasının URL'sini alın][2]

    <span data-ttu-id="a1a0d-134">Veya bu çağrı yaparak hello URL alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-134">Or you can get hello URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a><span data-ttu-id="a1a0d-135">Tetikleyicinizin Hello HTTP yöntemini değiştirme</span><span class="sxs-lookup"><span data-stu-id="a1a0d-135">Change hello HTTP method for your trigger</span></span>

<span data-ttu-id="a1a0d-136">Varsayılan olarak, hello **isteği** tetikleyici bir HTTP POST isteği bekliyor, ancak farklı bir HTTP yöntemini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-136">By default, hello **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="a1a0d-137">Yalnızca bir yöntem türü belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="a1a0d-138">Üzerinde **isteği** tetikleyin, seçin **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="a1a0d-139">Açık hello **yöntemi** listesi.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-139">Open hello **Method** list.</span></span> <span data-ttu-id="a1a0d-140">Bu örnek için select **almak** böylece HTTP uç noktanın URL'sini daha sonra test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a1a0d-141">Herhangi bir HTTP yöntemini seçin veya özel bir yöntem için kendi mantıksal uygulama belirtin.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![HTTP yöntemini değiştirme](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="a1a0d-143">HTTP uç nokta URL'nizi aracılığıyla parametreleri kabul et</span><span class="sxs-lookup"><span data-stu-id="a1a0d-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="a1a0d-144">HTTP uç noktası URL'si tooaccept parametrelerinizi istediğinizde, tetikleyicinin göreli yol özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-144">When you want your HTTP endpoint URL tooaccept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="a1a0d-145">Üzerinde **isteği** tetikleyin, seçin **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="a1a0d-146">Altında **yöntemi**, istek toouse istediğiniz hello HTTP yöntemini belirtin.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-146">Under **Method**, specify hello HTTP method that you want your request toouse.</span></span> <span data-ttu-id="a1a0d-147">Bu örnekte, hello seçin **almak** böylece HTTP uç noktanın URL'sini test, yapmadıysanız yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-147">For this example, select hello **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="a1a0d-148">Tetikleyici için göreli bir yol belirttiğinizde, tetikleyici için bir HTTP yöntemini de açıkça belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="a1a0d-149">Altında **göreli yol**, URL'niz, örneğin, kabul etmelidir hello parametresi için göreli yol hello belirtin `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-149">Under **Relative path**, specify hello relative path for hello parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Merhaba HTTP yöntemi ve parametresi için göreli yolunu belirtin](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="a1a0d-151">toouse parametresi Merhaba, ekleme bir **yanıt** eylem tooyour mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-151">toouse hello parameter, add a **Response** action tooyour logic app.</span></span> <span data-ttu-id="a1a0d-152">(Seçin, tetikleyici altında **yeni adım** > **Eylem Ekle** > **yanıt**)</span><span class="sxs-lookup"><span data-stu-id="a1a0d-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="a1a0d-153">Yanıt 's **gövde**, hello belirteci, tetikleyicinin göreli yolda belirtilen hello parametresi için içerir.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-153">In your response's **Body**, include hello token for hello parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="a1a0d-154">Örneğin, tooreturn `Hello {customerID}`, yanıtın güncelleştirme **gövde** ile `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-154">For example, tooreturn `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="a1a0d-155">Merhaba dinamik içerik listesinde görünür ve hello Göster `customerID` , tooselect için belirteç.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-155">hello dynamic content list should appear and show hello `customerID` token for you tooselect.</span></span>

    ![Parametre tooresponse gövde ekleme](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="a1a0d-157">**Gövde** bu örnekteki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-157">Your **Body** should look like this example:</span></span>

    ![Yanıt gövdesi parametresi](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="a1a0d-159">Mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-159">Save your logic app.</span></span> 

    <span data-ttu-id="a1a0d-160">HTTP uç nokta URL'nizi şimdi hello göreli yol, örneğin içerir:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-160">Your HTTP endpoint URL now includes hello relative path, for example:</span></span> 

    <span data-ttu-id="a1a0d-161">HTTPS & # 58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="a1a0d-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="a1a0d-162">HTTP uç noktası, kopyalama ve yapıştırma güncelleştirilmiş URL başka bir tarayıcı penceresine hello ancak Değiştir tootest `{customerID}` ile `123456`, ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-162">tootest your HTTP endpoint, copy and paste hello updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="a1a0d-163">Tarayıcınız bu metin göstermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="a1a0d-164">Mantıksal uygulamanız için JSON şemaları üretilen belirteçleri</span><span class="sxs-lookup"><span data-stu-id="a1a0d-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="a1a0d-165">Bir JSON şeması sağladığınız zaman, **isteği** tetikleyin, hello mantığı Uygulama Tasarımcısı belirteçleri özellikleri için bu şemada oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-165">When you provide a JSON schema in your **Request** trigger, hello Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="a1a0d-166">Mantıksal uygulama akışı aracılığıyla veri geçirme daha sonra bu belirteçleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="a1a0d-167">Merhaba eklerseniz, bu örneğin `title` ve `name` özellikleri tooyour JSON şeması, kendi belirteçleri daha sonraki iş akışı adımlarda kullanılabilir toouse sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-167">For this example, if you add hello `title` and `name` properties tooyour JSON schema, their tokens are now available toouse in later workflow steps.</span></span> 

<span data-ttu-id="a1a0d-168">Merhaba tam JSON şeması şöyledir:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-168">Here is hello complete JSON schema:</span></span>

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

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="a1a0d-169">Logic apps iç içe geçmiş iş akışları oluşturmak</span><span class="sxs-lookup"><span data-stu-id="a1a0d-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="a1a0d-170">İstekleri alabilen diğer mantıksal uygulamalar ekleyerek mantıksal uygulamanızı iş akışları yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="a1a0d-171">tooinclude bu mantığı uygulamalar ekleme hello **Azure Logic Apps - Logic Apps iş akışı seçin** eylem tooyour tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-171">tooinclude these logic apps, add hello **Azure Logic Apps - Choose a Logic Apps workflow** action tooyour trigger.</span></span> <span data-ttu-id="a1a0d-172">Daha sonra uygun mantığı uygulamalardan seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-172">You can then select from eligible logic apps.</span></span>

![Başka bir mantıksal uygulama Ekle](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="a1a0d-174">HTTP uç noktaları aracılığıyla logic apps tetiklemek veya çağırın</span><span class="sxs-lookup"><span data-stu-id="a1a0d-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="a1a0d-175">HTTP uç noktanızı oluşturduktan sonra mantıksal uygulamanızı aracılığıyla tetikleyebilir bir `POST` yöntemi toohello tam URL.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method toohello full URL.</span></span> <span data-ttu-id="a1a0d-176">Logic apps doğrudan erişimli uç noktaları için yerleşik destek vardır.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="a1a0d-177">Gelen istek başvuru içeriği</span><span class="sxs-lookup"><span data-stu-id="a1a0d-177">Reference content from an incoming request</span></span>

<span data-ttu-id="a1a0d-178">Merhaba içerik türü kullanıcının ise `application/json`, hello gelen istekte özelliklerine başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-178">If hello content's type is `application/json`, you can reference properties from hello incoming request.</span></span> <span data-ttu-id="a1a0d-179">Aksi takdirde, içerik tooother API'leri geçirebilirsiniz tek bir ikili birim olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-179">Otherwise, content is treated as a single binary unit that you can pass tooother APIs.</span></span> <span data-ttu-id="a1a0d-180">tooreference hello iş akışı içinde bu içerik, o içeriği dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-180">tooreference this content inside hello workflow, you must convert that content.</span></span> <span data-ttu-id="a1a0d-181">Örneğin, geçirdiğiniz `application/xml` içerik, kullanabileceğiniz `@xpath()` bir XPath ayıklama için veya `@json()` XML tooJSON dönüştürmek için.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML tooJSON.</span></span> <span data-ttu-id="a1a0d-182">Hakkında bilgi edinin [içerik türleriyle çalışma](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="a1a0d-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="a1a0d-183">tooget hello hello kullanabileceğiniz gelen isteğinden, çıktı `@triggerOutputs()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-183">tooget hello output from an incoming request, you can use hello `@triggerOutputs()` function.</span></span> <span data-ttu-id="a1a0d-184">Merhaba çıktı aşağıdaki örnekte olduğu gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-184">hello output might look like this example:</span></span>

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

<span data-ttu-id="a1a0d-185">tooaccess hello `body` özelliği özellikle kullanabileceğiniz hello `@triggerBody()` kısayol.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-185">tooaccess hello `body` property specifically, you can use hello `@triggerBody()` shortcut.</span></span> 

## <a name="respond-toorequests"></a><span data-ttu-id="a1a0d-186">Toorequests yanıt</span><span class="sxs-lookup"><span data-stu-id="a1a0d-186">Respond toorequests</span></span>

<span data-ttu-id="a1a0d-187">Bir mantıksal uygulama içerik toohello çağıran döndürerek Başlat toorespond toocertain istekleri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-187">You might want toorespond toocertain requests that start a logic app by returning content toohello caller.</span></span> <span data-ttu-id="a1a0d-188">tooconstruct hello durum kodu, başlığı ve yanıt için gövde hello kullanabilir **yanıt** eylem.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-188">tooconstruct hello status code, header, and body for your response, you can use hello **Response** action.</span></span> <span data-ttu-id="a1a0d-189">Bu eylem yalnızca sonunda Merhaba, iş akışı mantığı uygulamanıza herhangi bir yerde görünebilir.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-189">This action can appear anywhere in your logic app, not just at hello end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="a1a0d-190">Mantıksal uygulamanızı içermiyorsa bir **yanıt**, hello HTTP uç noktası yanıt *hemen* ile bir **202 kabul edilen** durumu.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-190">If your logic app doesn't include a **Response**, hello HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="a1a0d-191">Ayrıca, hello özgün istek tooget hello yanıt için hello yanıt için gereken tüm adımları içinde hello bitmesi gereken [istek zaman aşımı sınırı](./logic-apps-limits-and-config.md) hello iş akışı iç içe geçmiş mantıksal uygulama olarak gerektirmediği sürece.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-191">Also, for hello original request tooget hello response, all steps required for hello response must finish within hello [request timeout limit](./logic-apps-limits-and-config.md) unless you call hello workflow as a nested logic app.</span></span> <span data-ttu-id="a1a0d-192">Bu sınırı içinde yanıt meydana gelirse hello gelen istek zaman aşımına uğradı ve hello HTTP yanıtı alır **408 istemci zaman aşımı**.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-192">If no response happens within this limit, hello incoming request times out and receives hello HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="a1a0d-193">İç içe geçmiş logic apps için hello üst mantıksal uygulama toowait yanıt ne kadar zaman gerekli olduğuna bakılmaksızın, tamamlanana kadar devam eder.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-193">For nested logic apps, hello parent logic app continues toowait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-hello-response"></a><span data-ttu-id="a1a0d-194">Yapı hello yanıt</span><span class="sxs-lookup"><span data-stu-id="a1a0d-194">Construct hello response</span></span>

<span data-ttu-id="a1a0d-195">Merhaba yanıt gövdesi içinde birden fazla üst bilgi ve içerik herhangi bir türde içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-195">You can include more than one header and any type of content in hello response body.</span></span> <span data-ttu-id="a1a0d-196">Bizim örnek yanıt hello yanıt içerik türü var. hello üstbilgisini belirtir `application/json`.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-196">In our example response, hello header specifies that hello response has content type `application/json`.</span></span> <span data-ttu-id="a1a0d-197">ve hello gövdesinde `title` ve `name`bağlı olarak daha önce hello için güncelleştirilmiş hello JSON şeması **isteği** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-197">and hello body contains `title` and `name`, based on hello JSON schema updated previously for hello **Request** trigger.</span></span>

![HTTP yanıtının eylem][3]

<span data-ttu-id="a1a0d-199">Yanıtları bu özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-199">Responses have these properties:</span></span>

| <span data-ttu-id="a1a0d-200">Özellik</span><span class="sxs-lookup"><span data-stu-id="a1a0d-200">Property</span></span> | <span data-ttu-id="a1a0d-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a1a0d-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a1a0d-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="a1a0d-202">statusCode</span></span> |<span data-ttu-id="a1a0d-203">Yanıt veren toohello gelen istek için Hello HTTP durum kodu belirtir.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-203">Specifies hello HTTP status code for responding toohello incoming request.</span></span> <span data-ttu-id="a1a0d-204">Bu kod 2xx, 4xx veya 5xx ile başlayan tüm geçerli durum kodu olabilir.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="a1a0d-205">Ancak, 3xx durum kodları izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="a1a0d-206">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="a1a0d-206">headers</span></span> |<span data-ttu-id="a1a0d-207">Herhangi bir sayıda üstbilgileri tooinclude hello yanıt olarak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-207">Defines any number of headers tooinclude in hello response.</span></span> |
| <span data-ttu-id="a1a0d-208">Gövde</span><span class="sxs-lookup"><span data-stu-id="a1a0d-208">body</span></span> |<span data-ttu-id="a1a0d-209">Bir dize olabilir bir gövde nesnesi, JSON nesnesi veya bir önceki adımda başvurulan bile ikili içerik belirtir.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="a1a0d-210">Gibi görünüyor şimdi hello için hangi hello JSON şeması işte **yanıt** eylem:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-210">Here's what hello JSON schema looks like now for hello **Response** action:</span></span>

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
> <span data-ttu-id="a1a0d-211">Merhaba mantığı Uygulama Tasarımcısı üzerinde mantıksal uygulamanızı tooview hello tam JSON tanımını seçin **kod görünümü**.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-211">tooview hello complete JSON definition for your logic app, on hello Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="a1a0d-212">Soru-Cevap</span><span class="sxs-lookup"><span data-stu-id="a1a0d-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="a1a0d-213">S: ne hakkında URL güvenlik?</span><span class="sxs-lookup"><span data-stu-id="a1a0d-213">Q: What about URL security?</span></span>

<span data-ttu-id="a1a0d-214">Y: azure güvenli bir şekilde bir paylaşılan erişim imzası (SAS) kullanarak logic app geri çağırma URL'leri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="a1a0d-215">Bu imza sorgu parametresi olarak geçtiği ve mantıksal uygulamanızı tetikleyebilir önce doğrulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="a1a0d-216">Azure mantıksal uygulama, hello Tetikleyici adı ve gerçekleştirilir hello işlemi başına gizli bir anahtar benzersiz bir birleşimini kullanarak hello imza oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-216">Azure generates hello signature using a unique combination of a secret key per logic app, hello trigger name, and hello operation that's performed.</span></span> <span data-ttu-id="a1a0d-217">Bu nedenle birisi erişim toohello gizli mantığı uygulama anahtarı olmadığı sürece, geçerli bir imzası oluşturulamaz.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-217">So unless someone has access toohello secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a1a0d-218">Üretim ve güvenli sistemler için mantıksal uygulamanızı doğrudan hello tarayıcıdan çünkü çağırma karşı önerilir:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-218">For production and secure systems, we strongly recommend against calling your logic app directly from hello browser because:</span></span>
   > 
   > * <span data-ttu-id="a1a0d-219">Merhaba paylaşılan erişim anahtarı hello URL'de görünür.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-219">hello shared access key appears in hello URL.</span></span>
   > * <span data-ttu-id="a1a0d-220">Mantıksal uygulama müşterileri arasında güvenli içerik ilkeleri tooshared etki alanları nedeniyle yönetemez.</span><span class="sxs-lookup"><span data-stu-id="a1a0d-220">You can't manage secure content policies due tooshared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="a1a0d-221">S: daha fazla HTTP uç noktaları yapılandırabilir?</span><span class="sxs-lookup"><span data-stu-id="a1a0d-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="a1a0d-222">A: Evet HTTP uç noktaları aracılığıyla daha gelişmiş yapılandırma desteği [ **API Management**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="a1a0d-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="a1a0d-223">Tooconsistently yönetmek için mantıksal uygulamalar dahil olmak üzere tüm Apı'lerinizi, bu hizmet ayrıca hello özelliği sunar, özel etki alanı adlarını ayarlama, daha fazla kimlik doğrulama yöntemleri ve daha fazla bilgi, örneğin kullanın:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-223">This service also offers hello capability for you tooconsistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="a1a0d-224">Değişiklik hello istek yöntemi</span><span class="sxs-lookup"><span data-stu-id="a1a0d-224">Change hello request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="a1a0d-225">Merhaba URL kesimleri hello isteğinin değiştirme</span><span class="sxs-lookup"><span data-stu-id="a1a0d-225">Change hello URL segments of hello request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="a1a0d-226">Merhaba, API Management etki alanlarında ayarlama [Azure portal](https://portal.azure.com/ "Azure portalı")</span><span class="sxs-lookup"><span data-stu-id="a1a0d-226">Set up your API Management domains in hello [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="a1a0d-227">Temel kimlik doğrulaması için ilke toocheck ayarlama</span><span class="sxs-lookup"><span data-stu-id="a1a0d-227">Set up policy toocheck for Basic authentication</span></span>

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a><span data-ttu-id="a1a0d-228">S: Merhaba şema hello 1 Aralık 2014 Önizlemesi'nden geçirilen ne değiştirilir?</span><span class="sxs-lookup"><span data-stu-id="a1a0d-228">Q: What changed when hello schema migrated from hello December 1, 2014 preview?</span></span>

<span data-ttu-id="a1a0d-229">A: Bu değişiklikler hakkında bir özeti aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a1a0d-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="a1a0d-230">1 Aralık 2014 Önizleme</span><span class="sxs-lookup"><span data-stu-id="a1a0d-230">December 1, 2014 preview</span></span> | <span data-ttu-id="a1a0d-231">1 Haziran 2016</span><span class="sxs-lookup"><span data-stu-id="a1a0d-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="a1a0d-232">Tıklatın **HTTP dinleyicisi** API uygulaması</span><span class="sxs-lookup"><span data-stu-id="a1a0d-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="a1a0d-233">Tıklatın **el ile tetikleyici** (hiçbir API uygulaması gereklidir)</span><span class="sxs-lookup"><span data-stu-id="a1a0d-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="a1a0d-234">HTTP dinleyicisi ayarı "*yanıt otomatik olarak gönderir*"</span><span class="sxs-lookup"><span data-stu-id="a1a0d-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="a1a0d-235">Ya da dahil bir **yanıt** eylemin hello iş akışı tanımı yer almıyor</span><span class="sxs-lookup"><span data-stu-id="a1a0d-235">Either include a **Response** action or not in hello workflow definition</span></span> |
| <span data-ttu-id="a1a0d-236">Temel veya OAuth kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a1a0d-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="a1a0d-237">API Yönetimi</span><span class="sxs-lookup"><span data-stu-id="a1a0d-237">via API Management</span></span> |
| <span data-ttu-id="a1a0d-238">HTTP yöntemini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a1a0d-238">Configure HTTP method</span></span> |<span data-ttu-id="a1a0d-239">Altında **Gelişmiş Seçenekleri Göster**, bir HTTP yöntemini seçin</span><span class="sxs-lookup"><span data-stu-id="a1a0d-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="a1a0d-240">Göreli yolunu Yapılandır</span><span class="sxs-lookup"><span data-stu-id="a1a0d-240">Configure relative path</span></span> |<span data-ttu-id="a1a0d-241">Altında **Gelişmiş Seçenekleri Göster**, göreli bir yol ekleme</span><span class="sxs-lookup"><span data-stu-id="a1a0d-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="a1a0d-242">Başvuru hello gelen gövdesi aracılığıyla`@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="a1a0d-242">Reference hello incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="a1a0d-243">Aracılığıyla başvurusu`@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="a1a0d-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="a1a0d-244">**HTTP yanıt gönderme** hello HTTP dinleyicisi eylemi</span><span class="sxs-lookup"><span data-stu-id="a1a0d-244">**Send HTTP response** action on hello HTTP Listener</span></span> |<span data-ttu-id="a1a0d-245">Tıklatın **yanıt tooHTTP isteği** (hiçbir API uygulaması gereklidir)</span><span class="sxs-lookup"><span data-stu-id="a1a0d-245">Click **Respond tooHTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="a1a0d-246">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="a1a0d-246">Get help</span></span>

<span data-ttu-id="a1a0d-247">tooask sorular soruları ve hangi diğer Azure mantığı kullanıcılar gittiğini, uygulamaların ziyaret hello öğrenin [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="a1a0d-247">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="a1a0d-248">toohelp Azure mantıksal uygulamaları ve bağlayıcıların geliştirmek, oy veya hello fikir gönderme [Azure Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="a1a0d-248">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1a0d-249">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a1a0d-249">Next steps</span></span>

* [<span data-ttu-id="a1a0d-250">Mantıksal uygulama tanımları yazma</span><span class="sxs-lookup"><span data-stu-id="a1a0d-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="a1a0d-251">Hataları ve özel durumları işleme</span><span class="sxs-lookup"><span data-stu-id="a1a0d-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
