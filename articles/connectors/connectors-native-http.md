---
title: "HTTP - Azure Logic Apps üzerinden herhangi bir uç nokta ile aaaCommunicate | Microsoft Docs"
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
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a><span data-ttu-id="060c3-103">HTTP eylemi Hello ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="060c3-103">Get started with hello HTTP action</span></span>

<span data-ttu-id="060c3-104">Merhaba HTTP eylemi, kuruluşunuz için iş akışları genişletmek ve tooany uç noktası, HTTP iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="060c3-104">With hello HTTP action, you can extend workflows for your organization and communicate tooany endpoint over HTTP.</span></span>

<span data-ttu-id="060c3-105">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="060c3-105">You can:</span></span>

* <span data-ttu-id="060c3-106">Yönettiğiniz bir Web sitesi azaldığında (tetikleyici) etkinleştirme uygulama iş akışları mantığı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="060c3-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="060c3-107">Tooany uç nokta, iş akışlarınızı diğer Hizmetleri içine HTTP tooextend iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="060c3-107">Communicate tooany endpoint over HTTP tooextend your workflows into other services.</span></span>

<span data-ttu-id="060c3-108">bir mantıksal uygulama Hello HTTP eylem kullanmaya tooget bkz [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="060c3-108">tooget started using hello HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-trigger"></a><span data-ttu-id="060c3-109">Merhaba HTTP tetikleyicisi kullanın</span><span class="sxs-lookup"><span data-stu-id="060c3-109">Use hello HTTP trigger</span></span>
<span data-ttu-id="060c3-110">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="060c3-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="060c3-111">[Tetikleyiciler hakkında daha fazla bilgi](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="060c3-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="060c3-112">Burada, nasıl tooset hello HTTP yukarı tetiklemek hello mantığı Uygulama Tasarımcısı bir örnek sırası verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="060c3-112">Here’s an example sequence of how tooset up hello HTTP trigger in hello Logic App Designer.</span></span>

1. <span data-ttu-id="060c3-113">Merhaba HTTP tetikleyicisini mantıksal uygulamanızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="060c3-113">Add hello HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="060c3-114">Toopoll istediğiniz hello HTTP uç noktası için hello parametrelerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="060c3-114">Fill in hello parameters for hello HTTP endpoint that you want toopoll.</span></span>
3. <span data-ttu-id="060c3-115">Ne sıklıkta yoklanacağını üzerinde hello yinelenme aralığını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="060c3-115">Modify hello recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="060c3-116">Merhaba mantıksal uygulama artık her denetimi sırasında döndürülen herhangi bir içerik ile ateşlenir.</span><span class="sxs-lookup"><span data-stu-id="060c3-116">hello logic app now fires with any content that is returned during each check.</span></span>

   ![HTTP tetikleyicisi](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a><span data-ttu-id="060c3-118">Merhaba HTTP tetikleyicisini nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="060c3-118">How hello HTTP trigger works</span></span>

<span data-ttu-id="060c3-119">Merhaba HTTP tetikleyicisini çağrısı tooHTTP uç yinelenen bir aralıkta gönderir.</span><span class="sxs-lookup"><span data-stu-id="060c3-119">hello HTTP trigger sends a call tooHTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="060c3-120">Varsayılan olarak, 300'den düşük olduğu herhangi bir HTTP yanıt kodu mantığı uygulama toorun neden olur.</span><span class="sxs-lookup"><span data-stu-id="060c3-120">By default, any HTTP response code that is lower than 300 causes a logic app toorun.</span></span> <span data-ttu-id="060c3-121">toospecify hello mantıksal uygulama yangın olup olmadığını hello mantıksal uygulama kod görünümünde düzenleyin ve sonra hello HTTP çağrısıyla değerlendiren bir koşul ekleyin.</span><span class="sxs-lookup"><span data-stu-id="060c3-121">toospecify whether hello logic app should fire, you can edit hello logic app in code view, and add a condition that evaluates after hello HTTP call.</span></span> <span data-ttu-id="060c3-122">Merhaba çok eşit veya daha fazla durum kodu döndürdüğünde tetiklenen bir HTTP tetikleyicisi bir örneği burada verilmiştir`400`.</span><span class="sxs-lookup"><span data-stu-id="060c3-122">Here's an example of an HTTP trigger that fires when hello returned status code is greater than or equal too`400`.</span></span>

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

<span data-ttu-id="060c3-123">Merhaba HTTP trigger parametreleri ilgili tam ayrıntılar bulunur [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="060c3-123">Full details about hello HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-hello-http-action"></a><span data-ttu-id="060c3-124">Merhaba HTTP eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="060c3-124">Use hello HTTP action</span></span>

<span data-ttu-id="060c3-125">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="060c3-125">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="060c3-126">[Eylemler hakkında daha fazla bilgi](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="060c3-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="060c3-127">Seçin **yeni adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="060c3-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="060c3-128">Merhaba eylem arama kutusuna yazın **http** toolist hello HTTP eylemler.</span><span class="sxs-lookup"><span data-stu-id="060c3-128">In hello action search box, type **http** toolist hello HTTP actions.</span></span>
   
    ![Merhaba HTTP eylemi seçin](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="060c3-130">Merhaba HTTP çağrısı için gerekli parametreleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="060c3-130">Add any required parameters for hello HTTP call.</span></span>
   
    ![Tam hello HTTP eylemi](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="060c3-132">Merhaba designer araç çubuğundan, **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="060c3-132">On hello designer toolbar, click **Save**.</span></span> <span data-ttu-id="060c3-133">Mantıksal uygulamanızı kaydedilir ve hello (etkin) yayımlanan aynı anda.</span><span class="sxs-lookup"><span data-stu-id="060c3-133">Your logic app is saved and published (activated) at hello same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="060c3-134">HTTP tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="060c3-134">HTTP trigger</span></span>
<span data-ttu-id="060c3-135">Burada, bu bağlayıcıyı destekler hello tetikleyici hello ayrıntılarını bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="060c3-135">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="060c3-136">bir tetikleyici Hello HTTP bağlayıcısı vardır.</span><span class="sxs-lookup"><span data-stu-id="060c3-136">hello HTTP connector has one trigger.</span></span>

| <span data-ttu-id="060c3-137">Tetikleyici</span><span class="sxs-lookup"><span data-stu-id="060c3-137">Trigger</span></span> | <span data-ttu-id="060c3-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="060c3-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="060c3-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="060c3-139">HTTP</span></span> |<span data-ttu-id="060c3-140">Bir HTTP çağrı yapar ve hello yanıt içeriği döndürür.</span><span class="sxs-lookup"><span data-stu-id="060c3-140">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="060c3-141">HTTP eylemi</span><span class="sxs-lookup"><span data-stu-id="060c3-141">HTTP action</span></span>
<span data-ttu-id="060c3-142">Aşağıda, bu bağlayıcıyı destekler hello eylemin hello Ayrıntılar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="060c3-142">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="060c3-143">bir olası eylemin Hello HTTP bağlayıcısı vardır.</span><span class="sxs-lookup"><span data-stu-id="060c3-143">hello HTTP connector has one possible action.</span></span>

| <span data-ttu-id="060c3-144">Eylem</span><span class="sxs-lookup"><span data-stu-id="060c3-144">Action</span></span> | <span data-ttu-id="060c3-145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="060c3-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="060c3-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="060c3-146">HTTP</span></span> |<span data-ttu-id="060c3-147">Bir HTTP çağrı yapar ve hello yanıt içeriği döndürür.</span><span class="sxs-lookup"><span data-stu-id="060c3-147">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="060c3-148">HTTP ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="060c3-148">HTTP details</span></span>
<span data-ttu-id="060c3-149">Merhaba aşağıdaki tablolar hello gerekli ve isteğe bağlı giriş alanları hello eylem ve hello eylemini kullanarak ile ilişkili hello karşılık gelen çıkış ayrıntıları için açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="060c3-149">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="060c3-150">HTTP isteği</span><span class="sxs-lookup"><span data-stu-id="060c3-150">HTTP request</span></span>
<span data-ttu-id="060c3-151">Merhaba, HTTP giden isteğinde hello eylemi için girdi alanlarının verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="060c3-151">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="060c3-152">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="060c3-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="060c3-153">Görünen ad</span><span class="sxs-lookup"><span data-stu-id="060c3-153">Display name</span></span> | <span data-ttu-id="060c3-154">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="060c3-154">Property name</span></span> | <span data-ttu-id="060c3-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="060c3-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="060c3-156">Yöntemi *</span><span class="sxs-lookup"><span data-stu-id="060c3-156">Method*</span></span> |<span data-ttu-id="060c3-157">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="060c3-157">method</span></span> |<span data-ttu-id="060c3-158">Merhaba HTTP fiili toouse</span><span class="sxs-lookup"><span data-stu-id="060c3-158">hello HTTP verb toouse</span></span> |
| <span data-ttu-id="060c3-159">URI *</span><span class="sxs-lookup"><span data-stu-id="060c3-159">URI*</span></span> |<span data-ttu-id="060c3-160">URI</span><span class="sxs-lookup"><span data-stu-id="060c3-160">uri</span></span> |<span data-ttu-id="060c3-161">Merhaba URI hello HTTP isteği için</span><span class="sxs-lookup"><span data-stu-id="060c3-161">hello URI for hello HTTP request</span></span> |
| <span data-ttu-id="060c3-162">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="060c3-162">Headers</span></span> |<span data-ttu-id="060c3-163">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="060c3-163">headers</span></span> |<span data-ttu-id="060c3-164">HTTP üstbilgileri tooinclude JSON nesnesinin</span><span class="sxs-lookup"><span data-stu-id="060c3-164">A JSON object of HTTP headers tooinclude</span></span> |
| <span data-ttu-id="060c3-165">Gövde</span><span class="sxs-lookup"><span data-stu-id="060c3-165">Body</span></span> |<span data-ttu-id="060c3-166">Gövde</span><span class="sxs-lookup"><span data-stu-id="060c3-166">body</span></span> |<span data-ttu-id="060c3-167">Merhaba HTTP istek gövdesi</span><span class="sxs-lookup"><span data-stu-id="060c3-167">hello HTTP request body</span></span> |
| <span data-ttu-id="060c3-168">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="060c3-168">Authentication</span></span> |<span data-ttu-id="060c3-169">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="060c3-169">authentication</span></span> |<span data-ttu-id="060c3-170">Merhaba ayrıntılarında [kimlik doğrulaması](#authentication) bölümü</span><span class="sxs-lookup"><span data-stu-id="060c3-170">Details in hello [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="060c3-171">Çıkış Ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="060c3-171">Output details</span></span>
<span data-ttu-id="060c3-172">Merhaba, hello HTTP yanıtının çıkış ayrıntıları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="060c3-172">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="060c3-173">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="060c3-173">Property name</span></span> | <span data-ttu-id="060c3-174">Veri türü</span><span class="sxs-lookup"><span data-stu-id="060c3-174">Data type</span></span> | <span data-ttu-id="060c3-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="060c3-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="060c3-176">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="060c3-176">Headers</span></span> |<span data-ttu-id="060c3-177">Nesne</span><span class="sxs-lookup"><span data-stu-id="060c3-177">object</span></span> |<span data-ttu-id="060c3-178">Yanıt Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="060c3-178">Response headers</span></span> |
| <span data-ttu-id="060c3-179">Gövde</span><span class="sxs-lookup"><span data-stu-id="060c3-179">Body</span></span> |<span data-ttu-id="060c3-180">Nesne</span><span class="sxs-lookup"><span data-stu-id="060c3-180">object</span></span> |<span data-ttu-id="060c3-181">Yanıt nesnesi</span><span class="sxs-lookup"><span data-stu-id="060c3-181">Response object</span></span> |
| <span data-ttu-id="060c3-182">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="060c3-182">Status Code</span></span> |<span data-ttu-id="060c3-183">Int</span><span class="sxs-lookup"><span data-stu-id="060c3-183">int</span></span> |<span data-ttu-id="060c3-184">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="060c3-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="060c3-185">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="060c3-185">Authentication</span></span>
<span data-ttu-id="060c3-186">Merhaba Logic Apps özelliği toouse farklı tür HTTP uç noktaları karşı kimlik doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="060c3-186">hello Logic Apps feature allows you toouse different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="060c3-187">Bu kimlik doğrulama ile Merhaba kullanabilirsiniz **HTTP**, ** [HTTP + Swagger](connectors-native-http-swagger.md)**, ve ** [HTTP Web kancası](connectors-native-webhook.md) ** bağlayıcılar.</span><span class="sxs-lookup"><span data-stu-id="060c3-187">You can use this authentication with hello **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="060c3-188">şu kimlik doğrulama türlerini hello yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="060c3-188">hello following types of authentication are configurable:</span></span>

* [<span data-ttu-id="060c3-189">Temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="060c3-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="060c3-190">İstemci sertifikası kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="060c3-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="060c3-191">Azure Active Directory (Azure AD) OAuth kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="060c3-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="060c3-192">Temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="060c3-192">Basic authentication</span></span>

<span data-ttu-id="060c3-193">kimlik doğrulaması nesne aşağıdaki hello temel kimlik doğrulaması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="060c3-193">hello following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="060c3-194">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="060c3-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="060c3-195">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="060c3-195">Property name</span></span> | <span data-ttu-id="060c3-196">Veri türü</span><span class="sxs-lookup"><span data-stu-id="060c3-196">Data type</span></span> | <span data-ttu-id="060c3-197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="060c3-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="060c3-198">Türü *</span><span class="sxs-lookup"><span data-stu-id="060c3-198">Type*</span></span> |<span data-ttu-id="060c3-199">type</span><span class="sxs-lookup"><span data-stu-id="060c3-199">type</span></span> |<span data-ttu-id="060c3-200">Kimlik doğrulama türünü (olmalıdır `Basic` temel kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="060c3-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="060c3-201">Kullanıcı adı *</span><span class="sxs-lookup"><span data-stu-id="060c3-201">Username*</span></span> |<span data-ttu-id="060c3-202">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="060c3-202">username</span></span> |<span data-ttu-id="060c3-203">Kullanıcı adı tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="060c3-203">User name tooauthenticate</span></span> |
| <span data-ttu-id="060c3-204">Parola *</span><span class="sxs-lookup"><span data-stu-id="060c3-204">Password*</span></span> |<span data-ttu-id="060c3-205">password</span><span class="sxs-lookup"><span data-stu-id="060c3-205">password</span></span> |<span data-ttu-id="060c3-206">Parola tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="060c3-206">Password tooauthenticate</span></span> |

> [!TIP]
> <span data-ttu-id="060c3-207">Toouse hello tanımından geri alınamaz bir parola istiyorsanız kullanın bir `securestring` parametre ve hello `@parameters()`  
>  [iş akışı tanımı işlevi](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="060c3-207">If you want toouse a password that cannot be retrieved from hello definition, use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="060c3-208">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="060c3-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="060c3-209">İstemci sertifikası kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="060c3-209">Client certificate authentication</span></span>

<span data-ttu-id="060c3-210">Merhaba aşağıdaki kimlik doğrulama nesnesi için istemci sertifikası kimlik doğrulaması gereklidir.</span><span class="sxs-lookup"><span data-stu-id="060c3-210">hello following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="060c3-211">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="060c3-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="060c3-212">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="060c3-212">Property name</span></span> | <span data-ttu-id="060c3-213">Veri türü</span><span class="sxs-lookup"><span data-stu-id="060c3-213">Data type</span></span> | <span data-ttu-id="060c3-214">Açıklama</span><span class="sxs-lookup"><span data-stu-id="060c3-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="060c3-215">Türü *</span><span class="sxs-lookup"><span data-stu-id="060c3-215">Type*</span></span> |<span data-ttu-id="060c3-216">type</span><span class="sxs-lookup"><span data-stu-id="060c3-216">type</span></span> |<span data-ttu-id="060c3-217">Merhaba kimlik doğrulama türünü (olmalıdır `ClientCertificate` SSL istemci sertifikaları için)</span><span class="sxs-lookup"><span data-stu-id="060c3-217">hello type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="060c3-218">PFX *</span><span class="sxs-lookup"><span data-stu-id="060c3-218">PFX*</span></span> |<span data-ttu-id="060c3-219">PFX</span><span class="sxs-lookup"><span data-stu-id="060c3-219">pfx</span></span> |<span data-ttu-id="060c3-220">Merhaba Base64 ile kodlanmış içeriğini hello kişisel bilgi değişimi (PFX) dosyası</span><span class="sxs-lookup"><span data-stu-id="060c3-220">hello Base64-encoded contents of hello Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="060c3-221">Parola *</span><span class="sxs-lookup"><span data-stu-id="060c3-221">Password*</span></span> |<span data-ttu-id="060c3-222">password</span><span class="sxs-lookup"><span data-stu-id="060c3-222">password</span></span> |<span data-ttu-id="060c3-223">PFX dosyası Hello parola tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="060c3-223">hello password tooaccess hello PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="060c3-224">kullanabileceğiniz toouse hello mantıksal uygulama kaydetme sonra hello tanımında okunamaz bir parametre, bir `securestring` parametre ve hello `@parameters()`  
>  [iş akışı tanımı işlevi](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="060c3-224">toouse a parameter that won't be readable in hello definition after saving hello logic app, you can use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="060c3-225">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="060c3-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="060c3-226">Azure AD OAuth kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="060c3-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="060c3-227">kimlik doğrulaması nesne aşağıdaki hello Azure AD OAuth kimlik doğrulaması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="060c3-227">hello following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="060c3-228">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="060c3-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="060c3-229">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="060c3-229">Property name</span></span> | <span data-ttu-id="060c3-230">Veri türü</span><span class="sxs-lookup"><span data-stu-id="060c3-230">Data type</span></span> | <span data-ttu-id="060c3-231">Açıklama</span><span class="sxs-lookup"><span data-stu-id="060c3-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="060c3-232">Türü *</span><span class="sxs-lookup"><span data-stu-id="060c3-232">Type*</span></span> |<span data-ttu-id="060c3-233">type</span><span class="sxs-lookup"><span data-stu-id="060c3-233">type</span></span> |<span data-ttu-id="060c3-234">Merhaba kimlik doğrulama türünü (olmalıdır `ActiveDirectoryOAuth` Azure AD OAuth için)</span><span class="sxs-lookup"><span data-stu-id="060c3-234">hello type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="060c3-235">Kiracı *</span><span class="sxs-lookup"><span data-stu-id="060c3-235">Tenant*</span></span> |<span data-ttu-id="060c3-236">Kiracı</span><span class="sxs-lookup"><span data-stu-id="060c3-236">tenant</span></span> |<span data-ttu-id="060c3-237">hello Azure AD Kiracı için Hello Kiracı tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="060c3-237">hello tenant identifier for hello Azure AD tenant</span></span> |
| <span data-ttu-id="060c3-238">Hedef kitle *</span><span class="sxs-lookup"><span data-stu-id="060c3-238">Audience*</span></span> |<span data-ttu-id="060c3-239">Hedef kitle</span><span class="sxs-lookup"><span data-stu-id="060c3-239">audience</span></span> |<span data-ttu-id="060c3-240">Merhaba kaynak yetkilendirme toouse isteme.</span><span class="sxs-lookup"><span data-stu-id="060c3-240">hello resource you are requesting authorization toouse.</span></span> <span data-ttu-id="060c3-241">Örneğin, `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="060c3-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="060c3-242">İstemci kimliği *</span><span class="sxs-lookup"><span data-stu-id="060c3-242">Client ID*</span></span> |<span data-ttu-id="060c3-243">istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="060c3-243">clientId</span></span> |<span data-ttu-id="060c3-244">Merhaba Azure AD uygulaması için istemci tanımlayıcı hello</span><span class="sxs-lookup"><span data-stu-id="060c3-244">hello client identifier for hello Azure AD application</span></span> |
| <span data-ttu-id="060c3-245">Gizli *</span><span class="sxs-lookup"><span data-stu-id="060c3-245">Secret*</span></span> |<span data-ttu-id="060c3-246">Gizli</span><span class="sxs-lookup"><span data-stu-id="060c3-246">secret</span></span> |<span data-ttu-id="060c3-247">Merhaba belirteç isteme hello istemci Hello gizliliği</span><span class="sxs-lookup"><span data-stu-id="060c3-247">hello secret of hello client that is requesting hello token</span></span> |

> [!TIP]
> <span data-ttu-id="060c3-248">Kullanabileceğiniz bir `securestring` parametre ve hello `@parameters()` [iş akışı tanımı işlevi](http://aka.ms/logicappdocs) toouse kaydettikten sonra hello tanımında okunamaz bir parametre.</span><span class="sxs-lookup"><span data-stu-id="060c3-248">You can use a `securestring` parameter and hello `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) toouse a parameter that won't be readable in hello definition after saving.</span></span>
> 
> 

<span data-ttu-id="060c3-249">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="060c3-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="060c3-250">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="060c3-250">Next steps</span></span>
<span data-ttu-id="060c3-251">Şimdi, hello platform deneyin ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="060c3-251">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="060c3-252">Keşfedebilirsiniz bakarak Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="060c3-252">You can explore hello other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

