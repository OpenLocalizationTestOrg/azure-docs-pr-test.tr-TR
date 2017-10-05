---
title: "Özel İzleme şemaları B2B izleme - Azure Logic Apps | Microsoft Docs"
description: "B2B iletilerden Azure tümleştirme hesabınızda işlemleri izlemek için özel izleme şemalarını oluşturun."
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
ms.openlocfilehash: b71a4938dde2a71f1ce29403af7aa9101358d64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-tracking-to-monitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="74385-103">İş akışını tam, uçtan uca izlemek izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="74385-103">Enable tracking to monitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="74385-104">İzleme AS2 veya X12 gibi iş iş akışınızı farklı kısımlarını iletileri için etkinleştirebileceğiniz olduğunu izleme yerleşik yoktur.</span><span class="sxs-lookup"><span data-stu-id="74385-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="74385-105">Başlangıçtan itibaren akışınıza sonuna olayları kaydeder özel izleme etkinleştirebilirsiniz sonra iş akışları oluşturduğunuzda bir mantıksal uygulama, BizTalk Server, SQL Server veya diğer herhangi bir katman içerir.</span><span class="sxs-lookup"><span data-stu-id="74385-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from the beginning to the end of your workflow.</span></span> 

<span data-ttu-id="74385-106">Bu konu, mantıksal uygulamanızı dışında Katmanlar kullanabilirsiniz özel kod sağlar.</span><span class="sxs-lookup"><span data-stu-id="74385-106">This topic provides custom code that you can use in the layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="74385-107">Özel İzleme şeması</span><span class="sxs-lookup"><span data-stu-id="74385-107">Custom tracking schema</span></span>
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

| <span data-ttu-id="74385-108">Özellik</span><span class="sxs-lookup"><span data-stu-id="74385-108">Property</span></span> | <span data-ttu-id="74385-109">Tür</span><span class="sxs-lookup"><span data-stu-id="74385-109">Type</span></span> | <span data-ttu-id="74385-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="74385-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="74385-111">Kaynak türü</span><span class="sxs-lookup"><span data-stu-id="74385-111">sourceType</span></span> |   | <span data-ttu-id="74385-112">Çalışma kaynağının türü.</span><span class="sxs-lookup"><span data-stu-id="74385-112">Type of the run source.</span></span> <span data-ttu-id="74385-113">İzin verilen değerler **Microsoft.Logic/workflows** ve **özel**.</span><span class="sxs-lookup"><span data-stu-id="74385-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="74385-114">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="74385-114">(Mandatory)</span></span> |
| <span data-ttu-id="74385-115">Kaynak</span><span class="sxs-lookup"><span data-stu-id="74385-115">Source</span></span> |   | <span data-ttu-id="74385-116">Kaynak türü ise **Microsoft.Logic/workflows**, kaynak bilgilerini bu şemayı izlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="74385-116">If the source type is **Microsoft.Logic/workflows**, the source information needs to follow this schema.</span></span> <span data-ttu-id="74385-117">Kaynak türü ise **özel**, şemanın bir JToken olduğu.</span><span class="sxs-lookup"><span data-stu-id="74385-117">If the source type is **custom**, the schema is a JToken.</span></span> <span data-ttu-id="74385-118">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="74385-118">(Mandatory)</span></span> |
| <span data-ttu-id="74385-119">SistemKimliği</span><span class="sxs-lookup"><span data-stu-id="74385-119">systemId</span></span> | <span data-ttu-id="74385-120">Dize</span><span class="sxs-lookup"><span data-stu-id="74385-120">String</span></span> | <span data-ttu-id="74385-121">Mantıksal uygulama sistem kimliği</span><span class="sxs-lookup"><span data-stu-id="74385-121">Logic app system ID.</span></span> <span data-ttu-id="74385-122">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="74385-122">(Mandatory)</span></span> |
| <span data-ttu-id="74385-123">çalıştırma kodu</span><span class="sxs-lookup"><span data-stu-id="74385-123">runId</span></span> | <span data-ttu-id="74385-124">Dize</span><span class="sxs-lookup"><span data-stu-id="74385-124">String</span></span> | <span data-ttu-id="74385-125">Mantıksal uygulama kimliği çalıştırın</span><span class="sxs-lookup"><span data-stu-id="74385-125">Logic app run ID.</span></span> <span data-ttu-id="74385-126">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="74385-126">(Mandatory)</span></span> |
| <span data-ttu-id="74385-127">operationName</span><span class="sxs-lookup"><span data-stu-id="74385-127">operationName</span></span> | <span data-ttu-id="74385-128">Dize</span><span class="sxs-lookup"><span data-stu-id="74385-128">String</span></span> | <span data-ttu-id="74385-129">(Örneğin, eylem veya tetikleyici) işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="74385-129">Name of the operation (for example, action or trigger).</span></span> <span data-ttu-id="74385-130">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="74385-130">(Mandatory)</span></span> |
| <span data-ttu-id="74385-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="74385-131">repeatItemScopeName</span></span> | <span data-ttu-id="74385-132">Dize</span><span class="sxs-lookup"><span data-stu-id="74385-132">String</span></span> | <span data-ttu-id="74385-133">Eylem içinde olduğunda öğe adı yineleyin bir `foreach` / `until` döngü.</span><span class="sxs-lookup"><span data-stu-id="74385-133">Repeat item name if the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="74385-134">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="74385-134">(Mandatory)</span></span> |
| <span data-ttu-id="74385-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="74385-135">repeatItemIndex</span></span> | <span data-ttu-id="74385-136">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="74385-136">Integer</span></span> | <span data-ttu-id="74385-137">Eylem içinde olup olmadığını bir `foreach` / `until` döngü.</span><span class="sxs-lookup"><span data-stu-id="74385-137">Whether the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="74385-138">Yinelenen öğe dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="74385-138">Indicates the repeated item index.</span></span> <span data-ttu-id="74385-139">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="74385-139">(Mandatory)</span></span> |
| <span data-ttu-id="74385-140">İzleme kodu</span><span class="sxs-lookup"><span data-stu-id="74385-140">trackingId</span></span> | <span data-ttu-id="74385-141">Dize</span><span class="sxs-lookup"><span data-stu-id="74385-141">String</span></span> | <span data-ttu-id="74385-142">İletileri ilişkilendirmek için izleme kimliği.</span><span class="sxs-lookup"><span data-stu-id="74385-142">Tracking ID, to correlate the messages.</span></span> <span data-ttu-id="74385-143">(İsteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="74385-143">(Optional)</span></span> |
| <span data-ttu-id="74385-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="74385-144">correlationId</span></span> | <span data-ttu-id="74385-145">Dize</span><span class="sxs-lookup"><span data-stu-id="74385-145">String</span></span> | <span data-ttu-id="74385-146">Bağıntı kimliği, iletileri ilişkilendirmek için.</span><span class="sxs-lookup"><span data-stu-id="74385-146">Correlation ID, to correlate the messages.</span></span> <span data-ttu-id="74385-147">(İsteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="74385-147">(Optional)</span></span> |
| <span data-ttu-id="74385-148">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="74385-148">clientRequestId</span></span> | <span data-ttu-id="74385-149">Dize</span><span class="sxs-lookup"><span data-stu-id="74385-149">String</span></span> | <span data-ttu-id="74385-150">İstemci iletileri ilişkilendirmek için doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74385-150">Client can populate it to correlate messages.</span></span> <span data-ttu-id="74385-151">(İsteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="74385-151">(Optional)</span></span> |
| <span data-ttu-id="74385-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="74385-152">eventLevel</span></span> |   | <span data-ttu-id="74385-153">Olay düzeyi.</span><span class="sxs-lookup"><span data-stu-id="74385-153">Level of the event.</span></span> <span data-ttu-id="74385-154">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="74385-154">(Mandatory)</span></span> |
| <span data-ttu-id="74385-155">EventTime</span><span class="sxs-lookup"><span data-stu-id="74385-155">eventTime</span></span> |   | <span data-ttu-id="74385-156">UTC biçiminde YYYY-AA-DDTHH:MM:SS.00000Z olay zamanı.</span><span class="sxs-lookup"><span data-stu-id="74385-156">Time of the event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="74385-157">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="74385-157">(Mandatory)</span></span> |
| <span data-ttu-id="74385-158">RecordType</span><span class="sxs-lookup"><span data-stu-id="74385-158">recordType</span></span> |   | <span data-ttu-id="74385-159">İzleme kayıt türü.</span><span class="sxs-lookup"><span data-stu-id="74385-159">Type of the track record.</span></span> <span data-ttu-id="74385-160">Değer izin verilen **özel**.</span><span class="sxs-lookup"><span data-stu-id="74385-160">Allowed value is **custom**.</span></span> <span data-ttu-id="74385-161">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="74385-161">(Mandatory)</span></span> |
| <span data-ttu-id="74385-162">Kayıt</span><span class="sxs-lookup"><span data-stu-id="74385-162">record</span></span> |   | <span data-ttu-id="74385-163">Özel bir kayıt türü.</span><span class="sxs-lookup"><span data-stu-id="74385-163">Custom record type.</span></span> <span data-ttu-id="74385-164">İzin verilen JToken biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="74385-164">Allowed format is JToken.</span></span> <span data-ttu-id="74385-165">(Zorunlu)</span><span class="sxs-lookup"><span data-stu-id="74385-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="74385-166">B2B Protokolü izleme şemaları</span><span class="sxs-lookup"><span data-stu-id="74385-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="74385-167">B2B Protokolü şemaları izleme hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="74385-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="74385-168">AS2 izleme şemaları</span><span class="sxs-lookup"><span data-stu-id="74385-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="74385-169">X12 izleme şemaları</span><span class="sxs-lookup"><span data-stu-id="74385-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="74385-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="74385-170">Next steps</span></span>
* <span data-ttu-id="74385-171">Daha fazla bilgi edinmek [B2B iletileri izleme](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="74385-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="74385-172">Hakkında bilgi edinin [Operations Management Suite portalına B2B iletilerinde izleme](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="74385-172">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="74385-173">Daha fazla bilgi edinmek [Kurumsal tümleştirme paketi](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74385-173">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
