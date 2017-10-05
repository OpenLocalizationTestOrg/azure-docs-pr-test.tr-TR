---
title: "XML iletileri iş akışlarında - Azure Logic Apps ile çalışma | Microsoft Docs"
description: "İşlem, doğrulama, dönüştürme ve mantıksal uygulamalar ve iş XML iletileri zenginleştirmek-Kurumsal tümleştirme paketi kullanan senaryolar için"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 3fec4935f5317be4bf8c9e05f1c24a7c05381b1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="f18bd-103">Doğrulama ve XML dönüştürme, kodlama ve düz dosyalar kod çözme ve logic apps iletilerin özelliklerinde zenginleştirmek</span><span class="sxs-lookup"><span data-stu-id="f18bd-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="f18bd-104">Logic apps'ı kullanarak, gönderme ve alma işleminin XML iletileri yeteneğine sahip.</span><span class="sxs-lookup"><span data-stu-id="f18bd-104">Using logic apps, you have the ability to process XML messages that you send and receive.</span></span> <span data-ttu-id="f18bd-105">Bu özellik kuruluş tümleştirme paketi dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="f18bd-105">This feature is included with the Enterprise Integration Pack.</span></span> <span data-ttu-id="f18bd-106">BizTalk Server arka plana sahip olan kullanıcılar için Kurumsal tümleştirme paketi, dönüştürme ve iletileri doğrulamak için düz dosyalarla ve hatta zenginleştirmek veya belirli özellikleri iletiden ayıklamak için XPath kullanın benzer yetenekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="f18bd-106">For those users with a BizTalk Server background, the Enterprise Integration Pack gives you similar abilities to transform and validate messages, work with flat files, and even use XPath to enrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="f18bd-107">Bu alan için yeni kullanıcılar bu özellikler, iş akışı içinde iletileri işleminin nasıl genişletin.</span><span class="sxs-lookup"><span data-stu-id="f18bd-107">For those users who are new to this space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="f18bd-108">İşletmeler için senaryoda ve kurumsal tümleştirme paketi geliştirmek için kullanabileceğiniz sonra belirli XML şemaları ile çalışma, örneğin, nasıl şirketiniz bu iletileri işler.</span><span class="sxs-lookup"><span data-stu-id="f18bd-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use the Enterprise Integration Pack to enhance how your company processes these messages.</span></span> 

<span data-ttu-id="f18bd-109">Enterprise Integration Pack içerir:</span><span class="sxs-lookup"><span data-stu-id="f18bd-109">The Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="f18bd-110">[XML doğrulaması](logic-apps-enterprise-integration-xml-validation.md "XML ileti doğrulama hakkında daha fazla bilgi") -gelen veya giden XML iletisine belirli bir şemaya karşı doğrulama.</span><span class="sxs-lookup"><span data-stu-id="f18bd-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="f18bd-111">[XML dönüştürme](../logic-apps/logic-apps-enterprise-integration-transform.md "XML ileti dönüşümleri ve eşlemeleri hakkında bilgi edinin") - Dönüştür veya gereksinimlerinizi veya bir iş ortağı gereksinimlerine göre bir XML iletisini özelleştirme.</span><span class="sxs-lookup"><span data-stu-id="f18bd-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or the requirements of a partner.</span></span>
* <span data-ttu-id="f18bd-112">[Düz dosya kodlama ve kod çözme düz dosya](logic-apps-enterprise-integration-flatfile.md "düz dosya kodlama/kod çözme hakkında bilgi edinin") - kodlamak veya düz dosyadır kodunu çözer.</span><span class="sxs-lookup"><span data-stu-id="f18bd-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="f18bd-113">Örneğin, SAP kabul eder ve düz dosya biçiminde IDOC dosyaları gönderir.</span><span class="sxs-lookup"><span data-stu-id="f18bd-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="f18bd-114">Birçok tümleştirme platformda Logic Apps dahil olmak üzere, XML iletileri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f18bd-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="f18bd-115">Bu nedenle, "düz dosyalara XML dosyaları dönüştürmek için" düz dosya Kodlayıcısı kullanan bir mantıksal uygulama oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18bd-115">So, you can create a logic app that uses the flat file encoder to "convert" XML files to flat files.</span></span> 
* <span data-ttu-id="f18bd-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - bir ileti zenginleştirmek ve belirli özellikler iletiden ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="f18bd-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from the message.</span></span> <span data-ttu-id="f18bd-117">Sonra bir hedef veya aracı bir uç nokta ileti yönlendirmek için ayıklanan özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18bd-117">You can then use the extracted properties to route the message to a destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="f18bd-118">Deneyin</span><span class="sxs-lookup"><span data-stu-id="f18bd-118">Try it out</span></span>
<span data-ttu-id="f18bd-119">[Tam olarak işlevsel mantıksal uygulama dağıtma ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub örneği) XML özelliklerini Azure Logic Apps içinde kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f18bd-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using the XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="f18bd-120">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="f18bd-120">Learn more</span></span>
[<span data-ttu-id="f18bd-121">Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="f18bd-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")
