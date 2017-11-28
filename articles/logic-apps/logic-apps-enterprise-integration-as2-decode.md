---
title: aaaDecode AS2 iletileri - Azure Logic Apps | Microsoft Docs
description: "Nasıl toouse hello AS2 Çözücü'hello Kurumsal tümleştirme paketi de Azure mantıksal uygulamaları için"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="b7cda-103">AS2 iletileri Enterprise Integration Pack Merhaba ile Azure mantıksal uygulamaları için kod çözme</span><span class="sxs-lookup"><span data-stu-id="b7cda-103">Decode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span> 

<span data-ttu-id="b7cda-104">tooestablish güvenlik ve güvenilirlik iletileri aktarımı sırasında hello kod çözme AS2 ileti bağlayıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7cda-104">tooestablish security and reliability while transmitting messages, use hello Decode AS2 message connector.</span></span> <span data-ttu-id="b7cda-105">Bu bağlayıcı, dijital imza, şifre çözme ve onayları ileti Disposition bildirimler (MDN) aracılığıyla sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7cda-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="b7cda-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b7cda-106">Before you start</span></span>

<span data-ttu-id="b7cda-107">Gereksinim duyduğunuz hello öğeleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b7cda-107">Here's hello items you need:</span></span>

* <span data-ttu-id="b7cda-108">Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="b7cda-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="b7cda-109">Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="b7cda-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="b7cda-110">Bir tümleştirme hesap toouse hello kod çözme AS2 ileti Bağlayıcısı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7cda-110">You must have an integration account toouse hello Decode AS2 message connector.</span></span>
* <span data-ttu-id="b7cda-111">En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış</span><span class="sxs-lookup"><span data-stu-id="b7cda-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="b7cda-112">Bir [AS2 sözleşmesi](logic-apps-enterprise-integration-as2.md) tümleştirme hesabınızda tanımlanan zaten</span><span class="sxs-lookup"><span data-stu-id="b7cda-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="b7cda-113">AS2 iletileri kod çözme</span><span class="sxs-lookup"><span data-stu-id="b7cda-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="b7cda-114">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b7cda-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="b7cda-115">bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz hello kod çözme AS2 ileti bağlayıcı tetikleyiciler, sahip değil.</span><span class="sxs-lookup"><span data-stu-id="b7cda-115">hello Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="b7cda-116">Hello mantığı Uygulama Tasarımcısı, tetikleyici ekleyin ve sonra bir eylem tooyour mantıksal uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b7cda-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="b7cda-117">Merhaba arama kutusuna "AS2" filtreniz için girin.</span><span class="sxs-lookup"><span data-stu-id="b7cda-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="b7cda-118">Seçin **AS2 - kod çözme AS2 ileti**.</span><span class="sxs-lookup"><span data-stu-id="b7cda-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    !["AS2" için arama](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="b7cda-120">Tooyour tümleştirme hesabını daha önce herhangi bir bağlantısı oluşturmadıysanız, istenir toocreate şimdi bu bağlantı.</span><span class="sxs-lookup"><span data-stu-id="b7cda-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="b7cda-121">Bağlantınızı adlandırın ve hello tümleştirme hesabı tooconnect istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="b7cda-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![Tümleştirme bağlantısı oluşturma](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="b7cda-123">Bir yıldız işareti özelliklerle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b7cda-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="b7cda-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="b7cda-124">Property</span></span> | <span data-ttu-id="b7cda-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="b7cda-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="b7cda-126">Bağlantı adı *</span><span class="sxs-lookup"><span data-stu-id="b7cda-126">Connection Name *</span></span> |<span data-ttu-id="b7cda-127">Bağlantınız için herhangi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="b7cda-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="b7cda-128">Tümleştirme hesabını *</span><span class="sxs-lookup"><span data-stu-id="b7cda-128">Integration Account *</span></span> |<span data-ttu-id="b7cda-129">Tümleştirme hesabınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="b7cda-129">Enter a name for your integration account.</span></span> <span data-ttu-id="b7cda-130">Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun aynı Azure konumu.</span><span class="sxs-lookup"><span data-stu-id="b7cda-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="b7cda-131">İşiniz bittiğinde, bağlantı ayrıntılarınızı benzer toothis örnek görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="b7cda-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="b7cda-132">bağlantı oluşturma toofinish seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="b7cda-132">toofinish creating your connection, choose **Create**.</span></span>

    ![Tümleştirme bağlantı ayrıntıları](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="b7cda-134">Bu örnekte gösterildiği gibi bağlantınızı oluşturulduktan sonra Seç **gövde** ve **üstbilgileri** çıkışları hello istek.</span><span class="sxs-lookup"><span data-stu-id="b7cda-134">After your connection is created, as shown in this example, select **Body** and **Headers** from hello Request outputs.</span></span>
   
    ![oluşturulan tümleştirme bağlantı](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="b7cda-136">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b7cda-136">For example:</span></span>

    ![Gövde ve üstbilgileri isteği çıkışlarından seçin](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="b7cda-138">AS2 decoder ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="b7cda-138">AS2 decoder details</span></span>

<span data-ttu-id="b7cda-139">Merhaba kod çözme AS2 Bağlayıcısı, şu görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="b7cda-139">hello Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="b7cda-140">AS2/HTTP üstbilgileri işler</span><span class="sxs-lookup"><span data-stu-id="b7cda-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="b7cda-141">(Yapılandırılmışsa) Hello imzayı doğrular</span><span class="sxs-lookup"><span data-stu-id="b7cda-141">Verifies hello signature (if configured)</span></span>
* <span data-ttu-id="b7cda-142">Merhaba iletileri (yapılandırılmışsa) şifresini çözer.</span><span class="sxs-lookup"><span data-stu-id="b7cda-142">Decrypts hello messages (if configured)</span></span>
* <span data-ttu-id="b7cda-143">Merhaba iletisi (yapılandırılmışsa) açar</span><span class="sxs-lookup"><span data-stu-id="b7cda-143">Decompresses hello message (if configured)</span></span>
* <span data-ttu-id="b7cda-144">Alınan MDN hello özgün giden iletiyle çözümler</span><span class="sxs-lookup"><span data-stu-id="b7cda-144">Reconciles a received MDN with hello original outbound message</span></span>
* <span data-ttu-id="b7cda-145">Güncelleştirmeleri ve hello takası veritabanındaki kayıtları karşılık gelen</span><span class="sxs-lookup"><span data-stu-id="b7cda-145">Updates and correlates records in hello non-repudiation database</span></span>
* <span data-ttu-id="b7cda-146">AS2 durumu raporlama için kayıtları Yazar</span><span class="sxs-lookup"><span data-stu-id="b7cda-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="b7cda-147">Merhaba çıkış yükü içeriği base64 ile kodlanmış olan</span><span class="sxs-lookup"><span data-stu-id="b7cda-147">hello output payload contents are base64 encoded</span></span>
* <span data-ttu-id="b7cda-148">Bir MDN gereklidir ve olup hello MDN zaman uyumlu olması gerekir veya AS2 sözleşmesi zaman uyumsuz yapılandırmasını temel alarak belirler</span><span class="sxs-lookup"><span data-stu-id="b7cda-148">Determines whether an MDN is required, and whether hello MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="b7cda-149">(Sözleşmesi yapılandırmalarını temel alan) zaman uyumlu veya zaman uyumsuz bir MDN oluşturur</span><span class="sxs-lookup"><span data-stu-id="b7cda-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="b7cda-150">Merhaba MDN üzerinde Hello bağıntı belirteçleri ve özelliklerini ayarlar</span><span class="sxs-lookup"><span data-stu-id="b7cda-150">Sets hello correlation tokens and properties on hello MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="b7cda-151">Bu örnek deneyin</span><span class="sxs-lookup"><span data-stu-id="b7cda-151">Try this sample</span></span>

<span data-ttu-id="b7cda-152">bir tam olarak işlevsel mantığı uygulamasını ve örnek AS2 senaryo dağıtma tootry bkz hello [AS2 mantıksal uygulama şablonu ve senaryo](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="b7cda-152">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="b7cda-153">Görünüm hello swagger</span><span class="sxs-lookup"><span data-stu-id="b7cda-153">View hello swagger</span></span>
<span data-ttu-id="b7cda-154">Merhaba bkz [ayrıntıları swagger](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="b7cda-154">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b7cda-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b7cda-155">Next steps</span></span>
[<span data-ttu-id="b7cda-156">Merhaba Enterprise Integration Pack hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="b7cda-156">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

