---
title: "HTTP üzerinden - Azure Logic Apps ile herhangi bir uç nokta iletişim | Microsoft Docs"
description: "İletişim kurabilir logic apps ile herhangi bir uç nokta HTTP üzerinden oluşturun."
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: d422a07a27ffa62a673bd2d471ae4fc837251dee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-http-action"></a><span data-ttu-id="15b68-103">HTTP eylem ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="15b68-103">Get started with the HTTP action</span></span>

<span data-ttu-id="15b68-104">HTTP eylem ile kuruluşunuz için iş akışları genişletmek ve herhangi bir uç nokta için HTTP üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="15b68-104">With the HTTP action, you can extend workflows for your organization and communicate to any endpoint over HTTP.</span></span>

<span data-ttu-id="15b68-105">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="15b68-105">You can:</span></span>

* <span data-ttu-id="15b68-106">Yönettiğiniz bir Web sitesi azaldığında (tetikleyici) etkinleştirme uygulama iş akışları mantığı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="15b68-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="15b68-107">Herhangi bir uç nokta, iş akışlarınızı diğer Hizmetleri içine genişletmek için HTTP üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="15b68-107">Communicate to any endpoint over HTTP to extend your workflows into other services.</span></span>

<span data-ttu-id="15b68-108">HTTP eylemi bir mantıksal uygulama kullanmaya başlamak için bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="15b68-108">To get started using the HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-trigger"></a><span data-ttu-id="15b68-109">HTTP tetikleyicisini kullanın</span><span class="sxs-lookup"><span data-stu-id="15b68-109">Use the HTTP trigger</span></span>
<span data-ttu-id="15b68-110">Bir tetikleyici bir mantıksal uygulama tanımlı iş akışını başlatmak için kullanılan bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="15b68-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="15b68-111">[Tetikleyiciler hakkında daha fazla bilgi](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15b68-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="15b68-112">Burada, örnek dizisi mantığı Uygulama Tasarımcısı'nda HTTP tetikleyicisi ayarlama konusunda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="15b68-112">Here’s an example sequence of how to set up the HTTP trigger in the Logic App Designer.</span></span>

1. <span data-ttu-id="15b68-113">HTTP tetikleyicisini mantıksal uygulamanızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="15b68-113">Add the HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="15b68-114">Sorgulamak istediğiniz HTTP uç noktası parametrelerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="15b68-114">Fill in the parameters for the HTTP endpoint that you want to poll.</span></span>
3. <span data-ttu-id="15b68-115">Ne sıklıkta yoklanacağını üzerinde yinelenme aralığını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="15b68-115">Modify the recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="15b68-116">Mantıksal uygulama artık her denetimi sırasında döndürülen herhangi bir içerik ile ateşlenir.</span><span class="sxs-lookup"><span data-stu-id="15b68-116">The logic app now fires with any content that is returned during each check.</span></span>

   ![HTTP tetikleyicisi](./media/connectors-native-http/using-trigger.png)

### <a name="how-the-http-trigger-works"></a><span data-ttu-id="15b68-118">HTTP tetikleyicisini nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="15b68-118">How the HTTP trigger works</span></span>

<span data-ttu-id="15b68-119">HTTP tetikleyicisini HTTP uç noktası için bir çağrı yinelenen bir aralıkta gönderir.</span><span class="sxs-lookup"><span data-stu-id="15b68-119">The HTTP trigger sends a call to HTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="15b68-120">Varsayılan olarak, 300'den düşük olduğu herhangi bir HTTP yanıt kodu çalıştırmak bir mantıksal uygulama neden olur.</span><span class="sxs-lookup"><span data-stu-id="15b68-120">By default, any HTTP response code that is lower than 300 causes a logic app to run.</span></span> <span data-ttu-id="15b68-121">Mantıksal uygulama yangın olup olmadığını belirlemek için kod görünümünde mantıksal uygulama düzenleyebilir ve HTTP çağrısından sonra değerlendiren bir koşul ekleyin.</span><span class="sxs-lookup"><span data-stu-id="15b68-121">To specify whether the logic app should fire, you can edit the logic app in code view, and add a condition that evaluates after the HTTP call.</span></span> <span data-ttu-id="15b68-122">Döndürülen durum kodu değerinden büyük veya eşit olduğunda tetiklenen bir HTTP tetikleyicisi bir örneği burada verilmiştir `400`.</span><span class="sxs-lookup"><span data-stu-id="15b68-122">Here's an example of an HTTP trigger that fires when the returned status code is greater than or equal to `400`.</span></span>

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

<span data-ttu-id="15b68-123">HTTP trigger parametreleri ilgili tam ayrıntılar bulunur [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="15b68-123">Full details about the HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-the-http-action"></a><span data-ttu-id="15b68-124">HTTP eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="15b68-124">Use the HTTP action</span></span>

<span data-ttu-id="15b68-125">Bir eylem, bir mantıksal uygulama içinde tanımlanan iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="15b68-125">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="15b68-126">[Eylemler hakkında daha fazla bilgi](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15b68-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="15b68-127">Seçin **yeni adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="15b68-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="15b68-128">Eylem arama kutusuna yazın **http** HTTP eylemler listesi.</span><span class="sxs-lookup"><span data-stu-id="15b68-128">In the action search box, type **http** to list the HTTP actions.</span></span>
   
    ![HTTP eylemi seçin](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="15b68-130">HTTP çağrısı için gerekli parametreleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="15b68-130">Add any required parameters for the HTTP call.</span></span>
   
    ![HTTP eylemi tamamlamak](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="15b68-132">Tasarımcı araç çubuğunda tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="15b68-132">On the designer toolbar, click **Save**.</span></span> <span data-ttu-id="15b68-133">Mantıksal uygulamanızı kaydedildi ve aynı anda (etkin) yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="15b68-133">Your logic app is saved and published (activated) at the same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="15b68-134">HTTP tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="15b68-134">HTTP trigger</span></span>
<span data-ttu-id="15b68-135">Aşağıda, bu bağlayıcıyı destekler tetikleyici için Ayrıntılar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="15b68-135">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="15b68-136">HTTP Bağlayıcısı bir tetikleyici vardır.</span><span class="sxs-lookup"><span data-stu-id="15b68-136">The HTTP connector has one trigger.</span></span>

| <span data-ttu-id="15b68-137">Tetikleyici</span><span class="sxs-lookup"><span data-stu-id="15b68-137">Trigger</span></span> | <span data-ttu-id="15b68-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="15b68-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="15b68-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="15b68-139">HTTP</span></span> |<span data-ttu-id="15b68-140">Bir HTTP çağrı yapar ve yanıt içeriği döndürür.</span><span class="sxs-lookup"><span data-stu-id="15b68-140">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="15b68-141">HTTP eylemi</span><span class="sxs-lookup"><span data-stu-id="15b68-141">HTTP action</span></span>
<span data-ttu-id="15b68-142">Aşağıda, bu bağlayıcıyı destekler eylemi için Ayrıntılar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="15b68-142">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="15b68-143">HTTP Bağlayıcısı olası eylem vardır.</span><span class="sxs-lookup"><span data-stu-id="15b68-143">The HTTP connector has one possible action.</span></span>

| <span data-ttu-id="15b68-144">Eylem</span><span class="sxs-lookup"><span data-stu-id="15b68-144">Action</span></span> | <span data-ttu-id="15b68-145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="15b68-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="15b68-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="15b68-146">HTTP</span></span> |<span data-ttu-id="15b68-147">Bir HTTP çağrı yapar ve yanıt içeriği döndürür.</span><span class="sxs-lookup"><span data-stu-id="15b68-147">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="15b68-148">HTTP ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="15b68-148">HTTP details</span></span>
<span data-ttu-id="15b68-149">Aşağıdaki tablolar, eylem ve eylem kullanımıyla ilişkili karşılık gelen çıkış ayrıntıları için gerekli ve isteğe bağlı giriş alanlarının açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="15b68-149">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="15b68-150">HTTP isteği</span><span class="sxs-lookup"><span data-stu-id="15b68-150">HTTP request</span></span>
<span data-ttu-id="15b68-151">HTTP giden isteğinde eylemi için girdi alanlarının verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="15b68-151">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="15b68-152">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="15b68-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="15b68-153">Görünen ad</span><span class="sxs-lookup"><span data-stu-id="15b68-153">Display name</span></span> | <span data-ttu-id="15b68-154">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="15b68-154">Property name</span></span> | <span data-ttu-id="15b68-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="15b68-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="15b68-156">Yöntemi *</span><span class="sxs-lookup"><span data-stu-id="15b68-156">Method*</span></span> |<span data-ttu-id="15b68-157">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="15b68-157">method</span></span> |<span data-ttu-id="15b68-158">Kullanılacak HTTP fiili</span><span class="sxs-lookup"><span data-stu-id="15b68-158">The HTTP verb to use</span></span> |
| <span data-ttu-id="15b68-159">URI *</span><span class="sxs-lookup"><span data-stu-id="15b68-159">URI*</span></span> |<span data-ttu-id="15b68-160">URI</span><span class="sxs-lookup"><span data-stu-id="15b68-160">uri</span></span> |<span data-ttu-id="15b68-161">HTTP isteği için URI</span><span class="sxs-lookup"><span data-stu-id="15b68-161">The URI for the HTTP request</span></span> |
| <span data-ttu-id="15b68-162">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="15b68-162">Headers</span></span> |<span data-ttu-id="15b68-163">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="15b68-163">headers</span></span> |<span data-ttu-id="15b68-164">HTTP üstbilgisi eklemek için bir JSON nesnesi</span><span class="sxs-lookup"><span data-stu-id="15b68-164">A JSON object of HTTP headers to include</span></span> |
| <span data-ttu-id="15b68-165">Gövde</span><span class="sxs-lookup"><span data-stu-id="15b68-165">Body</span></span> |<span data-ttu-id="15b68-166">Gövde</span><span class="sxs-lookup"><span data-stu-id="15b68-166">body</span></span> |<span data-ttu-id="15b68-167">HTTP istek gövdesi</span><span class="sxs-lookup"><span data-stu-id="15b68-167">The HTTP request body</span></span> |
| <span data-ttu-id="15b68-168">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="15b68-168">Authentication</span></span> |<span data-ttu-id="15b68-169">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="15b68-169">authentication</span></span> |<span data-ttu-id="15b68-170">İçinde ayrıntıları [kimlik doğrulaması](#authentication) bölümü</span><span class="sxs-lookup"><span data-stu-id="15b68-170">Details in the [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="15b68-171">Çıkış Ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="15b68-171">Output details</span></span>
<span data-ttu-id="15b68-172">HTTP yanıtı için çıkış ayrıntıları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="15b68-172">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="15b68-173">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="15b68-173">Property name</span></span> | <span data-ttu-id="15b68-174">Veri türü</span><span class="sxs-lookup"><span data-stu-id="15b68-174">Data type</span></span> | <span data-ttu-id="15b68-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="15b68-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="15b68-176">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="15b68-176">Headers</span></span> |<span data-ttu-id="15b68-177">Nesne</span><span class="sxs-lookup"><span data-stu-id="15b68-177">object</span></span> |<span data-ttu-id="15b68-178">Yanıt Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="15b68-178">Response headers</span></span> |
| <span data-ttu-id="15b68-179">Gövde</span><span class="sxs-lookup"><span data-stu-id="15b68-179">Body</span></span> |<span data-ttu-id="15b68-180">Nesne</span><span class="sxs-lookup"><span data-stu-id="15b68-180">object</span></span> |<span data-ttu-id="15b68-181">Yanıt nesnesi</span><span class="sxs-lookup"><span data-stu-id="15b68-181">Response object</span></span> |
| <span data-ttu-id="15b68-182">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="15b68-182">Status Code</span></span> |<span data-ttu-id="15b68-183">Int</span><span class="sxs-lookup"><span data-stu-id="15b68-183">int</span></span> |<span data-ttu-id="15b68-184">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="15b68-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="15b68-185">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="15b68-185">Authentication</span></span>
<span data-ttu-id="15b68-186">Logic Apps özelliği, farklı türlerde HTTP uç noktaları karşı kimlik doğrulama kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="15b68-186">The Logic Apps feature allows you to use different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="15b68-187">Bu kimlik doğrulaması ile kullanabileceğiniz **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, ve  **[HTTP Web kancası](connectors-native-webhook.md)**  bağlayıcılar.</span><span class="sxs-lookup"><span data-stu-id="15b68-187">You can use this authentication with the **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="15b68-188">Aşağıdaki kimlik doğrulama türlerini yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="15b68-188">The following types of authentication are configurable:</span></span>

* [<span data-ttu-id="15b68-189">Temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="15b68-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="15b68-190">İstemci sertifikası kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="15b68-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="15b68-191">Azure Active Directory (Azure AD) OAuth kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="15b68-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="15b68-192">Temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="15b68-192">Basic authentication</span></span>

<span data-ttu-id="15b68-193">Aşağıdaki kimlik doğrulama nesnesini temel kimlik doğrulaması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="15b68-193">The following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="15b68-194">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="15b68-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="15b68-195">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="15b68-195">Property name</span></span> | <span data-ttu-id="15b68-196">Veri türü</span><span class="sxs-lookup"><span data-stu-id="15b68-196">Data type</span></span> | <span data-ttu-id="15b68-197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="15b68-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="15b68-198">Türü *</span><span class="sxs-lookup"><span data-stu-id="15b68-198">Type*</span></span> |<span data-ttu-id="15b68-199">type</span><span class="sxs-lookup"><span data-stu-id="15b68-199">type</span></span> |<span data-ttu-id="15b68-200">Kimlik doğrulama türünü (olmalıdır `Basic` temel kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="15b68-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="15b68-201">Kullanıcı adı *</span><span class="sxs-lookup"><span data-stu-id="15b68-201">Username*</span></span> |<span data-ttu-id="15b68-202">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="15b68-202">username</span></span> |<span data-ttu-id="15b68-203">Kimlik doğrulaması için kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="15b68-203">User name to authenticate</span></span> |
| <span data-ttu-id="15b68-204">Parola *</span><span class="sxs-lookup"><span data-stu-id="15b68-204">Password*</span></span> |<span data-ttu-id="15b68-205">password</span><span class="sxs-lookup"><span data-stu-id="15b68-205">password</span></span> |<span data-ttu-id="15b68-206">Kimlik doğrulaması için parola</span><span class="sxs-lookup"><span data-stu-id="15b68-206">Password to authenticate</span></span> |

> [!TIP]
> <span data-ttu-id="15b68-207">Kullanım tanımından geri alınamaz bir parola kullanmak istiyorsanız bir `securestring` parametre ve `@parameters()`  
>  [iş akışı tanımı işlevi](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="15b68-207">If you want to use a password that cannot be retrieved from the definition, use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="15b68-208">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="15b68-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="15b68-209">İstemci sertifikası kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="15b68-209">Client certificate authentication</span></span>

<span data-ttu-id="15b68-210">Aşağıdaki kimlik doğrulama nesnesi için istemci sertifikası kimlik doğrulaması gereklidir.</span><span class="sxs-lookup"><span data-stu-id="15b68-210">The following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="15b68-211">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="15b68-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="15b68-212">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="15b68-212">Property name</span></span> | <span data-ttu-id="15b68-213">Veri türü</span><span class="sxs-lookup"><span data-stu-id="15b68-213">Data type</span></span> | <span data-ttu-id="15b68-214">Açıklama</span><span class="sxs-lookup"><span data-stu-id="15b68-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="15b68-215">Türü *</span><span class="sxs-lookup"><span data-stu-id="15b68-215">Type*</span></span> |<span data-ttu-id="15b68-216">type</span><span class="sxs-lookup"><span data-stu-id="15b68-216">type</span></span> |<span data-ttu-id="15b68-217">Kimlik doğrulaması türü (olmalıdır `ClientCertificate` SSL istemci sertifikaları için)</span><span class="sxs-lookup"><span data-stu-id="15b68-217">The type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="15b68-218">PFX *</span><span class="sxs-lookup"><span data-stu-id="15b68-218">PFX*</span></span> |<span data-ttu-id="15b68-219">PFX</span><span class="sxs-lookup"><span data-stu-id="15b68-219">pfx</span></span> |<span data-ttu-id="15b68-220">Kişisel bilgi değişimi (PFX) dosyası Base64 ile kodlanmış içeriği</span><span class="sxs-lookup"><span data-stu-id="15b68-220">The Base64-encoded contents of the Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="15b68-221">Parola *</span><span class="sxs-lookup"><span data-stu-id="15b68-221">Password*</span></span> |<span data-ttu-id="15b68-222">password</span><span class="sxs-lookup"><span data-stu-id="15b68-222">password</span></span> |<span data-ttu-id="15b68-223">PFX dosyası erişim için parola</span><span class="sxs-lookup"><span data-stu-id="15b68-223">The password to access the PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="15b68-224">Mantıksal uygulama kaydetme sonra tanımında okunamaz bir parametre kullanmak üzere kullanabileceğiniz bir `securestring` parametre ve `@parameters()`  
>  [iş akışı tanımı işlevi](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="15b68-224">To use a parameter that won't be readable in the definition after saving the logic app, you can use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="15b68-225">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="15b68-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="15b68-226">Azure AD OAuth kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="15b68-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="15b68-227">Aşağıdaki kimlik doğrulama nesnesini Azure AD OAuth kimlik doğrulaması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="15b68-227">The following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="15b68-228">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="15b68-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="15b68-229">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="15b68-229">Property name</span></span> | <span data-ttu-id="15b68-230">Veri türü</span><span class="sxs-lookup"><span data-stu-id="15b68-230">Data type</span></span> | <span data-ttu-id="15b68-231">Açıklama</span><span class="sxs-lookup"><span data-stu-id="15b68-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="15b68-232">Türü *</span><span class="sxs-lookup"><span data-stu-id="15b68-232">Type*</span></span> |<span data-ttu-id="15b68-233">type</span><span class="sxs-lookup"><span data-stu-id="15b68-233">type</span></span> |<span data-ttu-id="15b68-234">Kimlik doğrulaması türü (olmalıdır `ActiveDirectoryOAuth` Azure AD OAuth için)</span><span class="sxs-lookup"><span data-stu-id="15b68-234">The type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="15b68-235">Kiracı *</span><span class="sxs-lookup"><span data-stu-id="15b68-235">Tenant*</span></span> |<span data-ttu-id="15b68-236">Kiracı</span><span class="sxs-lookup"><span data-stu-id="15b68-236">tenant</span></span> |<span data-ttu-id="15b68-237">Azure AD kiracısı için Kiracı tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="15b68-237">The tenant identifier for the Azure AD tenant</span></span> |
| <span data-ttu-id="15b68-238">Hedef kitle *</span><span class="sxs-lookup"><span data-stu-id="15b68-238">Audience*</span></span> |<span data-ttu-id="15b68-239">Hedef kitle</span><span class="sxs-lookup"><span data-stu-id="15b68-239">audience</span></span> |<span data-ttu-id="15b68-240">Kaynak Yetkilendirme kullanmak istiyor.</span><span class="sxs-lookup"><span data-stu-id="15b68-240">The resource you are requesting authorization to use.</span></span> <span data-ttu-id="15b68-241">Örneğin, `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="15b68-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="15b68-242">İstemci kimliği *</span><span class="sxs-lookup"><span data-stu-id="15b68-242">Client ID*</span></span> |<span data-ttu-id="15b68-243">istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="15b68-243">clientId</span></span> |<span data-ttu-id="15b68-244">Azure AD uygulaması için istemci tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="15b68-244">The client identifier for the Azure AD application</span></span> |
| <span data-ttu-id="15b68-245">Gizli *</span><span class="sxs-lookup"><span data-stu-id="15b68-245">Secret*</span></span> |<span data-ttu-id="15b68-246">Gizli</span><span class="sxs-lookup"><span data-stu-id="15b68-246">secret</span></span> |<span data-ttu-id="15b68-247">Belirteç isteme istemci gizli anahtarı</span><span class="sxs-lookup"><span data-stu-id="15b68-247">The secret of the client that is requesting the token</span></span> |

> [!TIP]
> <span data-ttu-id="15b68-248">Kullanabileceğiniz bir `securestring` parametre ve `@parameters()` [iş akışı tanımı işlevi](http://aka.ms/logicappdocs) kaydettikten sonra tanımında okunamaz bir parametre kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="15b68-248">You can use a `securestring` parameter and the `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) to use a parameter that won't be readable in the definition after saving.</span></span>
> 
> 

<span data-ttu-id="15b68-249">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="15b68-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="15b68-250">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="15b68-250">Next steps</span></span>
<span data-ttu-id="15b68-251">Şimdi, platform deneyin ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="15b68-251">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="15b68-252">Logic Apps diğer kullanılabilir bağlayıcılar bakarak keşfedebilirsiniz bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="15b68-252">You can explore the other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

