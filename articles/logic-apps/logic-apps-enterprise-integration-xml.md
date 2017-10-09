---
title: "XML ile aaaWorking iletiler, iş akışlarında - Azure Logic Apps | Microsoft Docs"
description: "İşlem, doğrulama, dönüştürme ve XML zenginleştirmek mantıksal uygulamalar ve iş tooscenarios kullanarak iletileri hello Kurumsal tümleştirme paketi"
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
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="16f40-103">Doğrulama ve XML dönüştürme, kodlama ve düz dosyalar kod çözme ve logic apps iletilerin özelliklerinde zenginleştirmek</span><span class="sxs-lookup"><span data-stu-id="16f40-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="16f40-104">Logic apps'ı kullanarak, gönderme ve alma hello özelliği tooprocess XML iletileri sahip.</span><span class="sxs-lookup"><span data-stu-id="16f40-104">Using logic apps, you have hello ability tooprocess XML messages that you send and receive.</span></span> <span data-ttu-id="16f40-105">Bu özellik Enterprise Integration Pack Merhaba ile dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="16f40-105">This feature is included with hello Enterprise Integration Pack.</span></span> <span data-ttu-id="16f40-106">Bu kullanıcılara bir BizTalk Server arka plana sahip hello Enterprise Integration Pack benzer yeteneklerini tootransform sağlar ve iletileri doğrulamak, düz dosyalarla ve bile XPath tooenrich kullanın veya belirli özellikleri iletiden ayıklar.</span><span class="sxs-lookup"><span data-stu-id="16f40-106">For those users with a BizTalk Server background, hello Enterprise Integration Pack gives you similar abilities tootransform and validate messages, work with flat files, and even use XPath tooenrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="16f40-107">Yeni toothis alanı olan kullanıcılar bu özellikler, iş akışı içinde iletileri işleminin nasıl genişletin.</span><span class="sxs-lookup"><span data-stu-id="16f40-107">For those users who are new toothis space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="16f40-108">İşletmeler için senaryoda ve hello Kurumsal tümleştirme paketi tooenhance kullanabilirsiniz belirli XML şemaları ile çalışma, örneğin, nasıl şirketiniz bu iletileri işler.</span><span class="sxs-lookup"><span data-stu-id="16f40-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use hello Enterprise Integration Pack tooenhance how your company processes these messages.</span></span> 

<span data-ttu-id="16f40-109">Merhaba Kurumsal tümleştirme paketi içerir:</span><span class="sxs-lookup"><span data-stu-id="16f40-109">hello Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="16f40-110">[XML doğrulaması](logic-apps-enterprise-integration-xml-validation.md "XML ileti doğrulama hakkında daha fazla bilgi") -gelen veya giden XML iletisine belirli bir şemaya karşı doğrulama.</span><span class="sxs-lookup"><span data-stu-id="16f40-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="16f40-111">[XML dönüştürme](../logic-apps/logic-apps-enterprise-integration-transform.md "XML ileti dönüşümleri ve eşlemeleri hakkında bilgi edinin") - Dönüştür veya XML iletisine, gereksinimleri veya bir iş ortağı hello gereksinimlerine göre özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="16f40-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or hello requirements of a partner.</span></span>
* <span data-ttu-id="16f40-112">[Düz dosya kodlama ve kod çözme düz dosya](logic-apps-enterprise-integration-flatfile.md "düz dosya kodlama/kod çözme hakkında bilgi edinin") - kodlamak veya düz dosyadır kodunu çözer.</span><span class="sxs-lookup"><span data-stu-id="16f40-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="16f40-113">Örneğin, SAP kabul eder ve düz dosya biçiminde IDOC dosyaları gönderir.</span><span class="sxs-lookup"><span data-stu-id="16f40-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="16f40-114">Birçok tümleştirme platformda Logic Apps dahil olmak üzere, XML iletileri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="16f40-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="16f40-115">Bu nedenle, kullandığı hello düz dosya Kodlayıcısı çok "XML dosyalarını tooflat dönüştürmeniz" bir mantıksal uygulama oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16f40-115">So, you can create a logic app that uses hello flat file encoder too"convert" XML files tooflat files.</span></span> 
* <span data-ttu-id="16f40-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - bir ileti zenginleştirmek ve belirli özellikler hello iletiden ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="16f40-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from hello message.</span></span> <span data-ttu-id="16f40-117">Kullanım hello özellikleri tooroute hello ileti tooa hedef veya aracı bir uç nokta ayıklanan sonra kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16f40-117">You can then use hello extracted properties tooroute hello message tooa destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="16f40-118">Deneyin</span><span class="sxs-lookup"><span data-stu-id="16f40-118">Try it out</span></span>
<span data-ttu-id="16f40-119">[Tam olarak işlevsel mantıksal uygulama dağıtma ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub örneği) Azure Logic Apps içinde hello XML özelliklerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="16f40-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using hello XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="16f40-120">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="16f40-120">Learn more</span></span>
[<span data-ttu-id="16f40-121">Merhaba Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="16f40-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")
