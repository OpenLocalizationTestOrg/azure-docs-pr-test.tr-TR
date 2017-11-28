---
title: "aaaUse istek ve yanıt eylemleri | Microsoft Docs"
description: "Merhaba istek ve yanıt tetikleyici ve bir Azure mantıksal uygulama eylemde genel bakış"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a><span data-ttu-id="32c21-103">Merhaba istek ve yanıt bileşenleriyle çalışmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="32c21-103">Get started with hello request and response components</span></span>
<span data-ttu-id="32c21-104">Merhaba istek ve yanıt bileşenlerinde ile bir mantıksal uygulama, gerçek zamanlı tooevents yanıt verebilir.</span><span class="sxs-lookup"><span data-stu-id="32c21-104">With hello request and response components in a logic app, you can respond in real time tooevents.</span></span>

<span data-ttu-id="32c21-105">Örneğin, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="32c21-105">For example, you can:</span></span>

* <span data-ttu-id="32c21-106">Bir mantıksal uygulama yoluyla şirket içi veritabanından verilerle tooan HTTP isteğine yanıt.</span><span class="sxs-lookup"><span data-stu-id="32c21-106">Respond tooan HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="32c21-107">Bir mantıksal uygulama bir dış Web kancası olaydan tetikler.</span><span class="sxs-lookup"><span data-stu-id="32c21-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="32c21-108">İstek ve yanıt eylemi başka bir mantıksal uygulama içinde ile bir mantıksal uygulama çağırın.</span><span class="sxs-lookup"><span data-stu-id="32c21-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="32c21-109">bir mantıksal uygulama Hello istek ve yanıt eylemleri kullanmaya tooget bkz [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="32c21-109">tooget started using hello request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-request-trigger"></a><span data-ttu-id="32c21-110">Merhaba HTTP isteği tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="32c21-110">Use hello HTTP Request trigger</span></span>
<span data-ttu-id="32c21-111">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="32c21-111">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="32c21-112">[Tetikleyiciler hakkında daha fazla bilgi](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32c21-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="32c21-113">Burada, örnek dizisi nasıl tooset oluşturan bir HTTP isteği hello mantığı Uygulama Tasarımcısı verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="32c21-113">Here’s an example sequence of how tooset up an HTTP request in hello Logic App Designer.</span></span>

1. <span data-ttu-id="32c21-114">Merhaba tetikleyici eklemek **isteği - olduğunda bir HTTP isteği alındığında** mantığı uygulamanıza.</span><span class="sxs-lookup"><span data-stu-id="32c21-114">Add hello trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="32c21-115">İsteğe bağlı olarak bir JSON şeması sağlayın (gibi bir araç kullanarak [JSONSchema.net](http://jsonschema.net)) hello istek gövdesi için.</span><span class="sxs-lookup"><span data-stu-id="32c21-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for hello request body.</span></span> <span data-ttu-id="32c21-116">Bu özellikler için hello Tasarımcı toogenerate belirteçleri hello HTTP istek sağlar.</span><span class="sxs-lookup"><span data-stu-id="32c21-116">This allows hello designer toogenerate tokens for properties in hello HTTP request.</span></span>
2. <span data-ttu-id="32c21-117">Başka bir eylem ekleyebilirsiniz, böylece hello mantıksal uygulama kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32c21-117">Add another action so that you can save hello logic app.</span></span>
3. <span data-ttu-id="32c21-118">Merhaba mantıksal uygulama kaydedildikten sonra hello isteği kartından hello HTTP istek URL'si elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32c21-118">After saving hello logic app, you can get hello HTTP request URL from hello request card.</span></span>
4. <span data-ttu-id="32c21-119">Bir HTTP POST (gibi bir araç kullanabilirsiniz [Postman](https://www.getpostman.com/)) toohello URL Tetikleyicileri hello mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="32c21-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) toohello URL triggers hello logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="32c21-120">Bir yanıt eylemi tanımlarsanız olmayan bir `202 ACCEPTED` yanıt toohello çağıran hemen döndürülür.</span><span class="sxs-lookup"><span data-stu-id="32c21-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span> <span data-ttu-id="32c21-121">Merhaba yanıt eylem toocustomize yanıt kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32c21-121">You can use hello response action toocustomize a response.</span></span>
> 
> 

![Yanıt tetikleyici](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a><span data-ttu-id="32c21-123">Merhaba HTTP yanıtının eylem kullanın</span><span class="sxs-lookup"><span data-stu-id="32c21-123">Use hello HTTP Response action</span></span>
<span data-ttu-id="32c21-124">Merhaba HTTP yanıtının eylem, yalnızca bir HTTP isteğiyle tetiklenen bir iş akışında kullanıldığında geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="32c21-124">hello HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="32c21-125">Bir yanıt eylemi tanımlarsanız olmayan bir `202 ACCEPTED` yanıt toohello çağıran hemen döndürülür.</span><span class="sxs-lookup"><span data-stu-id="32c21-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span>  <span data-ttu-id="32c21-126">Merhaba iş akışı içindeki tüm adımda bir yanıt eylemi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32c21-126">You can add a response action at any step within hello workflow.</span></span> <span data-ttu-id="32c21-127">Merhaba mantıksal uygulama yalnızca hello gelen istek açık bir yanıt için bir dakika için tutar.</span><span class="sxs-lookup"><span data-stu-id="32c21-127">hello logic app only keeps hello incoming request open for one minute for a response.</span></span>  <span data-ttu-id="32c21-128">Bir yanıt hello akışından gönderilen (ve bir yanıt eylemi hello tanımında varsa) dakika sonra bir `504 GATEWAY TIMEOUT` toohello arayan döndürülür.</span><span class="sxs-lookup"><span data-stu-id="32c21-128">After one minute, if no response was sent from hello workflow (and a response action exists in hello definition), a `504 GATEWAY TIMEOUT` is returned toohello caller.</span></span>

<span data-ttu-id="32c21-129">İşte nasıl tooadd bir HTTP yanıtının eylem:</span><span class="sxs-lookup"><span data-stu-id="32c21-129">Here's how tooadd an HTTP Response action:</span></span>

1. <span data-ttu-id="32c21-130">Select hello **yeni adım** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32c21-130">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="32c21-131">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="32c21-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="32c21-132">Merhaba eylem arama kutusuna yazın **yanıt** toolist hello yanıt eylem.</span><span class="sxs-lookup"><span data-stu-id="32c21-132">In hello action search box, type **response** toolist hello Response action.</span></span>
   
    ![Merhaba yanıt eylemi seçin](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="32c21-134">Merhaba HTTP yanıt iletisi için gerekli olan parametreleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="32c21-134">Add in any parameters that are required for hello HTTP response message.</span></span>
   
    ![Tam hello yanıt eylemi](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="32c21-136">Merhaba sol üst köşesindeki hello araç toosave ve, logic app kazandırır hem'ı tıklatın ve yayımlama (etkinleştirin).</span><span class="sxs-lookup"><span data-stu-id="32c21-136">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="32c21-137">Tetikleyici isteği</span><span class="sxs-lookup"><span data-stu-id="32c21-137">Request trigger</span></span>
<span data-ttu-id="32c21-138">Burada, bu bağlayıcıyı destekler hello tetikleyici hello ayrıntılarını bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="32c21-138">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="32c21-139">Bir tek istek tetikleyici yoktur.</span><span class="sxs-lookup"><span data-stu-id="32c21-139">There is a single request trigger.</span></span>

| <span data-ttu-id="32c21-140">Tetikleyici</span><span class="sxs-lookup"><span data-stu-id="32c21-140">Trigger</span></span> | <span data-ttu-id="32c21-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="32c21-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="32c21-142">İstek</span><span class="sxs-lookup"><span data-stu-id="32c21-142">Request</span></span> |<span data-ttu-id="32c21-143">Bir HTTP isteği alındığında gerçekleşir</span><span class="sxs-lookup"><span data-stu-id="32c21-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="32c21-144">Yanıt eylemi</span><span class="sxs-lookup"><span data-stu-id="32c21-144">Response action</span></span>
<span data-ttu-id="32c21-145">Aşağıda, bu bağlayıcıyı destekler hello eylemin hello Ayrıntılar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="32c21-145">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="32c21-146">Bir istek tetikleyicisini eşlik yükleyen yalnızca kullanılabilir tek yanıt eylemi yok.</span><span class="sxs-lookup"><span data-stu-id="32c21-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="32c21-147">Eylem</span><span class="sxs-lookup"><span data-stu-id="32c21-147">Action</span></span> | <span data-ttu-id="32c21-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="32c21-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="32c21-149">Yanıt</span><span class="sxs-lookup"><span data-stu-id="32c21-149">Response</span></span> |<span data-ttu-id="32c21-150">HTTP isteğinin yanıtı toohello bağıntılı döndürür</span><span class="sxs-lookup"><span data-stu-id="32c21-150">Returns a response toohello correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="32c21-151">Tetikleyici ve eylem ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="32c21-151">Trigger and action details</span></span>
<span data-ttu-id="32c21-152">Merhaba aşağıdaki tablolarda hello tetikleyici ve eylem için girdi alanlarının hello açıklar ve karşılık gelen çıkış ayrıntıları hello.</span><span class="sxs-lookup"><span data-stu-id="32c21-152">hello following tables describe hello input fields for hello trigger and action, and hello corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="32c21-153">Tetikleyici isteği</span><span class="sxs-lookup"><span data-stu-id="32c21-153">Request trigger</span></span>
<span data-ttu-id="32c21-154">Merhaba, bir gelen HTTP istek hello tetikleyici için giriş alanını aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="32c21-154">hello following is an input field for hello trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="32c21-155">Görünen ad</span><span class="sxs-lookup"><span data-stu-id="32c21-155">Display name</span></span> | <span data-ttu-id="32c21-156">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="32c21-156">Property name</span></span> | <span data-ttu-id="32c21-157">Açıklama</span><span class="sxs-lookup"><span data-stu-id="32c21-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="32c21-158">JSON şeması</span><span class="sxs-lookup"><span data-stu-id="32c21-158">JSON Schema</span></span> |<span data-ttu-id="32c21-159">Şema</span><span class="sxs-lookup"><span data-stu-id="32c21-159">schema</span></span> |<span data-ttu-id="32c21-160">Merhaba HTTP isteği gövdesinin Hello JSON şeması</span><span class="sxs-lookup"><span data-stu-id="32c21-160">hello JSON schema of hello HTTP request body</span></span> |

<br>

<span data-ttu-id="32c21-161">**Çıkış Ayrıntıları**</span><span class="sxs-lookup"><span data-stu-id="32c21-161">**Output details**</span></span>

<span data-ttu-id="32c21-162">Merhaba, hello istek için çıkış ayrıntıları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="32c21-162">hello following are output details for hello request.</span></span>

| <span data-ttu-id="32c21-163">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="32c21-163">Property name</span></span> | <span data-ttu-id="32c21-164">Veri türü</span><span class="sxs-lookup"><span data-stu-id="32c21-164">Data type</span></span> | <span data-ttu-id="32c21-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="32c21-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="32c21-166">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="32c21-166">Headers</span></span> |<span data-ttu-id="32c21-167">Nesne</span><span class="sxs-lookup"><span data-stu-id="32c21-167">object</span></span> |<span data-ttu-id="32c21-168">İstek üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="32c21-168">Request headers</span></span> |
| <span data-ttu-id="32c21-169">Gövde</span><span class="sxs-lookup"><span data-stu-id="32c21-169">Body</span></span> |<span data-ttu-id="32c21-170">Nesne</span><span class="sxs-lookup"><span data-stu-id="32c21-170">object</span></span> |<span data-ttu-id="32c21-171">İstek nesnesi</span><span class="sxs-lookup"><span data-stu-id="32c21-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="32c21-172">Yanıt eylemi</span><span class="sxs-lookup"><span data-stu-id="32c21-172">Response action</span></span>
<span data-ttu-id="32c21-173">Merhaba, hello HTTP yanıtının eylem için girdi alanlarının verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="32c21-173">hello following are input fields for hello HTTP Response action.</span></span> <span data-ttu-id="32c21-174">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="32c21-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="32c21-175">Görünen ad</span><span class="sxs-lookup"><span data-stu-id="32c21-175">Display name</span></span> | <span data-ttu-id="32c21-176">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="32c21-176">Property name</span></span> | <span data-ttu-id="32c21-177">Açıklama</span><span class="sxs-lookup"><span data-stu-id="32c21-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="32c21-178">Durum kodu *</span><span class="sxs-lookup"><span data-stu-id="32c21-178">Status Code*</span></span> |<span data-ttu-id="32c21-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="32c21-179">statusCode</span></span> |<span data-ttu-id="32c21-180">Merhaba HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="32c21-180">hello HTTP status code</span></span> |
| <span data-ttu-id="32c21-181">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="32c21-181">Headers</span></span> |<span data-ttu-id="32c21-182">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="32c21-182">headers</span></span> |<span data-ttu-id="32c21-183">Tüm yanıt üstbilgileri tooinclude JSON nesnesinin</span><span class="sxs-lookup"><span data-stu-id="32c21-183">A JSON object of any response headers tooinclude</span></span> |
| <span data-ttu-id="32c21-184">Gövde</span><span class="sxs-lookup"><span data-stu-id="32c21-184">Body</span></span> |<span data-ttu-id="32c21-185">Gövde</span><span class="sxs-lookup"><span data-stu-id="32c21-185">body</span></span> |<span data-ttu-id="32c21-186">Merhaba yanıt gövdesi</span><span class="sxs-lookup"><span data-stu-id="32c21-186">hello response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="32c21-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="32c21-187">Next steps</span></span>
<span data-ttu-id="32c21-188">Şimdi, hello platform deneyin ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="32c21-188">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="32c21-189">Keşfedebilirsiniz bakarak logic apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="32c21-189">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

