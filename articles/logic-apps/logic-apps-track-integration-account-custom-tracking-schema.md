---
title: "B2B için şemalar izleme aaaCustom izleme - Azure Logic Apps | Microsoft Docs"
description: "Özel İzleme şemaları toomonitor B2B iletileri Azure tümleştirme hesabınızda işlemlerdeki oluşturun."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="bf7bd-103">İş akışını tam, uçtan uca izleme toomonitor etkinleştir</span><span class="sxs-lookup"><span data-stu-id="bf7bd-103">Enable tracking toomonitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="bf7bd-104">İzleme AS2 veya X12 gibi iş iş akışınızı farklı kısımlarını iletileri için etkinleştirebileceğiniz olduğunu izleme yerleşik yoktur.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="bf7bd-105">Bir mantıksal uygulama, BizTalk Server, SQL Server veya başka bir katmanında içeren iş akışları oluşturduğunuzda, hello başına toohello sonundan akışınızı olayları kaydeder özel izleme işlevini etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from hello beginning toohello end of your workflow.</span></span> 

<span data-ttu-id="bf7bd-106">Bu konu, mantıksal uygulamanızı dışında hello katmanlarında kullanabilirsiniz özel kod sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-106">This topic provides custom code that you can use in hello layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="bf7bd-107">Özel İzleme şeması</span><span class="sxs-lookup"><span data-stu-id="bf7bd-107">Custom tracking schema</span></span>
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| <span data-ttu-id="bf7bd-108">Özellik</span><span class="sxs-lookup"><span data-stu-id="bf7bd-108">Property</span></span> | <span data-ttu-id="bf7bd-109">Tür</span><span class="sxs-lookup"><span data-stu-id="bf7bd-109">Type</span></span> | <span data-ttu-id="bf7bd-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf7bd-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bf7bd-111">Kaynak türü</span><span class="sxs-lookup"><span data-stu-id="bf7bd-111">sourceType</span></span> |   | <span data-ttu-id="bf7bd-112">Çalıştırma hello kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-112">Type of hello run source.</span></span> <span data-ttu-id="bf7bd-113">İzin verilen değerler **Microsoft.Logic/workflows** ve **özel**.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="bf7bd-114">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-114">(Mandatory)</span></span> |
| <span data-ttu-id="bf7bd-115">Kaynak</span><span class="sxs-lookup"><span data-stu-id="bf7bd-115">Source</span></span> |   | <span data-ttu-id="bf7bd-116">Merhaba kaynak türü ise **Microsoft.Logic/workflows**, hello kaynak bilgileri, bu şemayı toofollow gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-116">If hello source type is **Microsoft.Logic/workflows**, hello source information needs toofollow this schema.</span></span> <span data-ttu-id="bf7bd-117">Merhaba kaynak türü ise **özel**, hello schema bir JToken'dır.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-117">If hello source type is **custom**, hello schema is a JToken.</span></span> <span data-ttu-id="bf7bd-118">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-118">(Mandatory)</span></span> |
| <span data-ttu-id="bf7bd-119">SistemKimliği</span><span class="sxs-lookup"><span data-stu-id="bf7bd-119">systemId</span></span> | <span data-ttu-id="bf7bd-120">Dize</span><span class="sxs-lookup"><span data-stu-id="bf7bd-120">String</span></span> | <span data-ttu-id="bf7bd-121">Mantıksal uygulama sistem kimliği</span><span class="sxs-lookup"><span data-stu-id="bf7bd-121">Logic app system ID.</span></span> <span data-ttu-id="bf7bd-122">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-122">(Mandatory)</span></span> |
| <span data-ttu-id="bf7bd-123">çalıştırma kodu</span><span class="sxs-lookup"><span data-stu-id="bf7bd-123">runId</span></span> | <span data-ttu-id="bf7bd-124">Dize</span><span class="sxs-lookup"><span data-stu-id="bf7bd-124">String</span></span> | <span data-ttu-id="bf7bd-125">Mantıksal uygulama kimliği çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bf7bd-125">Logic app run ID.</span></span> <span data-ttu-id="bf7bd-126">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-126">(Mandatory)</span></span> |
| <span data-ttu-id="bf7bd-127">operationName</span><span class="sxs-lookup"><span data-stu-id="bf7bd-127">operationName</span></span> | <span data-ttu-id="bf7bd-128">Dize</span><span class="sxs-lookup"><span data-stu-id="bf7bd-128">String</span></span> | <span data-ttu-id="bf7bd-129">Merhaba işlemi (örneğin, eylem veya tetikleyici) adı.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-129">Name of hello operation (for example, action or trigger).</span></span> <span data-ttu-id="bf7bd-130">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-130">(Mandatory)</span></span> |
| <span data-ttu-id="bf7bd-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="bf7bd-131">repeatItemScopeName</span></span> | <span data-ttu-id="bf7bd-132">Dize</span><span class="sxs-lookup"><span data-stu-id="bf7bd-132">String</span></span> | <span data-ttu-id="bf7bd-133">Öğe adı Hello eylem içinde ise yineleyin bir `foreach` / `until` döngü.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-133">Repeat item name if hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="bf7bd-134">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-134">(Mandatory)</span></span> |
| <span data-ttu-id="bf7bd-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="bf7bd-135">repeatItemIndex</span></span> | <span data-ttu-id="bf7bd-136">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="bf7bd-136">Integer</span></span> | <span data-ttu-id="bf7bd-137">Merhaba eylem içinde olup olmadığını bir `foreach` / `until` döngü.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-137">Whether hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="bf7bd-138">Merhaba yinelenen öğe dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-138">Indicates hello repeated item index.</span></span> <span data-ttu-id="bf7bd-139">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-139">(Mandatory)</span></span> |
| <span data-ttu-id="bf7bd-140">İzleme kodu</span><span class="sxs-lookup"><span data-stu-id="bf7bd-140">trackingId</span></span> | <span data-ttu-id="bf7bd-141">Dize</span><span class="sxs-lookup"><span data-stu-id="bf7bd-141">String</span></span> | <span data-ttu-id="bf7bd-142">İzleme kimliği, toocorrelate Merhaba iletileri.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-142">Tracking ID, toocorrelate hello messages.</span></span> <span data-ttu-id="bf7bd-143">(İsteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-143">(Optional)</span></span> |
| <span data-ttu-id="bf7bd-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="bf7bd-144">correlationId</span></span> | <span data-ttu-id="bf7bd-145">Dize</span><span class="sxs-lookup"><span data-stu-id="bf7bd-145">String</span></span> | <span data-ttu-id="bf7bd-146">Bağıntı kimliği, toocorrelate Merhaba iletileri.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-146">Correlation ID, toocorrelate hello messages.</span></span> <span data-ttu-id="bf7bd-147">(İsteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-147">(Optional)</span></span> |
| <span data-ttu-id="bf7bd-148">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="bf7bd-148">clientRequestId</span></span> | <span data-ttu-id="bf7bd-149">Dize</span><span class="sxs-lookup"><span data-stu-id="bf7bd-149">String</span></span> | <span data-ttu-id="bf7bd-150">İstemci toocorrelate iletileri doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-150">Client can populate it toocorrelate messages.</span></span> <span data-ttu-id="bf7bd-151">(İsteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-151">(Optional)</span></span> |
| <span data-ttu-id="bf7bd-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="bf7bd-152">eventLevel</span></span> |   | <span data-ttu-id="bf7bd-153">Merhaba olay düzeyi.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-153">Level of hello event.</span></span> <span data-ttu-id="bf7bd-154">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-154">(Mandatory)</span></span> |
| <span data-ttu-id="bf7bd-155">EventTime</span><span class="sxs-lookup"><span data-stu-id="bf7bd-155">eventTime</span></span> |   | <span data-ttu-id="bf7bd-156">YYYY-AA-DDTHH:MM:SS.00000Z UTC biçiminde hello olay zamanı.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-156">Time of hello event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="bf7bd-157">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-157">(Mandatory)</span></span> |
| <span data-ttu-id="bf7bd-158">RecordType</span><span class="sxs-lookup"><span data-stu-id="bf7bd-158">recordType</span></span> |   | <span data-ttu-id="bf7bd-159">Merhaba İzle kayıt türü.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-159">Type of hello track record.</span></span> <span data-ttu-id="bf7bd-160">Değer izin verilen **özel**.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-160">Allowed value is **custom**.</span></span> <span data-ttu-id="bf7bd-161">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-161">(Mandatory)</span></span> |
| <span data-ttu-id="bf7bd-162">Kayıt</span><span class="sxs-lookup"><span data-stu-id="bf7bd-162">record</span></span> |   | <span data-ttu-id="bf7bd-163">Özel bir kayıt türü.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-163">Custom record type.</span></span> <span data-ttu-id="bf7bd-164">İzin verilen JToken biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="bf7bd-164">Allowed format is JToken.</span></span> <span data-ttu-id="bf7bd-165">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="bf7bd-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="bf7bd-166">B2B Protokolü izleme şemaları</span><span class="sxs-lookup"><span data-stu-id="bf7bd-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="bf7bd-167">B2B Protokolü şemaları izleme hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="bf7bd-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="bf7bd-168">AS2 izleme şemaları</span><span class="sxs-lookup"><span data-stu-id="bf7bd-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="bf7bd-169">X12 izleme şemaları</span><span class="sxs-lookup"><span data-stu-id="bf7bd-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="bf7bd-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bf7bd-170">Next steps</span></span>
* <span data-ttu-id="bf7bd-171">Daha fazla bilgi edinmek [B2B iletileri izleme](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="bf7bd-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="bf7bd-172">Hakkında bilgi edinin [hello Operations Management Suite portalına B2B iletilerinde izleme](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="bf7bd-172">Learn about [tracking B2B messages in hello Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="bf7bd-173">Merhaba hakkında daha fazla bilgi [Kurumsal tümleştirme paketi](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bf7bd-173">Learn more about hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
