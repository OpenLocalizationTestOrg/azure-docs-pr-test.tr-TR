---
title: "AS2 iletileri - Azure Logic Apps kod çözme | Microsoft Docs"
description: "Azure mantıksal uygulamaları için Kurumsal tümleştirme paketinde AS2 kod çözücü kullanma"
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
ms.openlocfilehash: a7920b2509fe368c6f7d55e17fe0bf0020c4562c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="e1e1a-103">AS2 iletileri Kurumsal tümleştirme paketi ile Azure mantıksal uygulamaları için kod çözme</span><span class="sxs-lookup"><span data-stu-id="e1e1a-103">Decode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span> 

<span data-ttu-id="e1e1a-104">Güvenlik ve güvenilirlik aktaran iletileri sırasında kurmak için kod çözme AS2 ileti Bağlayıcısı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-104">To establish security and reliability while transmitting messages, use the Decode AS2 message connector.</span></span> <span data-ttu-id="e1e1a-105">Bu bağlayıcı, dijital imza, şifre çözme ve onayları ileti Disposition bildirimler (MDN) aracılığıyla sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e1e1a-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e1e1a-106">Before you start</span></span>

<span data-ttu-id="e1e1a-107">Gereksinim duyduğunuz öğeleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e1e1a-107">Here's the items you need:</span></span>

* <span data-ttu-id="e1e1a-108">Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="e1e1a-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="e1e1a-109">Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="e1e1a-110">Kod çözme AS2 ileti bağlayıcıyı kullanmak üzere bir tümleştirme hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-110">You must have an integration account to use the Decode AS2 message connector.</span></span>
* <span data-ttu-id="e1e1a-111">En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış</span><span class="sxs-lookup"><span data-stu-id="e1e1a-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="e1e1a-112">Bir [AS2 sözleşmesi](logic-apps-enterprise-integration-as2.md) tümleştirme hesabınızda tanımlanan zaten</span><span class="sxs-lookup"><span data-stu-id="e1e1a-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="e1e1a-113">AS2 iletileri kod çözme</span><span class="sxs-lookup"><span data-stu-id="e1e1a-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="e1e1a-114">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e1e1a-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="e1e1a-115">Bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz kod çözme AS2 ileti bağlayıcı tetikleyiciler, sahip değil.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-115">The Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="e1e1a-116">Mantıksal Uygulama Tasarımcısı'nda bir tetikleyici ekleyin ve ardından bir eylem mantıksal uygulamanızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="e1e1a-117">Arama kutusuna "AS2" filtreniz için girin.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="e1e1a-118">Seçin **AS2 - kod çözme AS2 ileti**.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    !["AS2" için arama](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="e1e1a-120">Tümleştirme hesabınıza daha önce herhangi bir bağlantısı oluşturmadıysanız, bu bağlantı artık oluşturmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="e1e1a-121">Bağlantınızı adlandırın ve bağlamak istediğiniz tümleştirme hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![Tümleştirme bağlantısı oluşturma](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="e1e1a-123">Bir yıldız işareti özelliklerle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="e1e1a-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="e1e1a-124">Property</span></span> | <span data-ttu-id="e1e1a-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="e1e1a-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="e1e1a-126">Bağlantı adı *</span><span class="sxs-lookup"><span data-stu-id="e1e1a-126">Connection Name *</span></span> |<span data-ttu-id="e1e1a-127">Bağlantınız için herhangi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="e1e1a-128">Tümleştirme hesabını *</span><span class="sxs-lookup"><span data-stu-id="e1e1a-128">Integration Account *</span></span> |<span data-ttu-id="e1e1a-129">Tümleştirme hesabınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-129">Enter a name for your integration account.</span></span> <span data-ttu-id="e1e1a-130">Tümleştirme hesabı ve mantığı uygulamanız aynı Azure konumuna olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="e1e1a-131">İşiniz bittiğinde, bağlantı bilgilerinizi bu örneğe benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="e1e1a-132">Bağlantınızı oluşturmayı tamamlamak için tercih **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-132">To finish creating your connection, choose **Create**.</span></span>

    ![Tümleştirme bağlantı ayrıntıları](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="e1e1a-134">Bu örnekte gösterildiği gibi bağlantınızı oluşturulduktan sonra Seç **gövde** ve **üstbilgileri** isteği çıkışları gelen.</span><span class="sxs-lookup"><span data-stu-id="e1e1a-134">After your connection is created, as shown in this example, select **Body** and **Headers** from the Request outputs.</span></span>
   
    ![oluşturulan tümleştirme bağlantı](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="e1e1a-136">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e1e1a-136">For example:</span></span>

    ![Gövde ve üstbilgileri isteği çıkışlarından seçin](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="e1e1a-138">AS2 decoder ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="e1e1a-138">AS2 decoder details</span></span>

<span data-ttu-id="e1e1a-139">Kod çözme AS2 Bağlayıcısı'nı bu görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="e1e1a-139">The Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="e1e1a-140">AS2/HTTP üstbilgileri işler</span><span class="sxs-lookup"><span data-stu-id="e1e1a-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="e1e1a-141">(Yapılandırılmışsa) imzayı doğrular</span><span class="sxs-lookup"><span data-stu-id="e1e1a-141">Verifies the signature (if configured)</span></span>
* <span data-ttu-id="e1e1a-142">İletilerin şifresini çözer (yapılandırıldıysa)</span><span class="sxs-lookup"><span data-stu-id="e1e1a-142">Decrypts the messages (if configured)</span></span>
* <span data-ttu-id="e1e1a-143">İletisi (yapılandırılmışsa) açar</span><span class="sxs-lookup"><span data-stu-id="e1e1a-143">Decompresses the message (if configured)</span></span>
* <span data-ttu-id="e1e1a-144">Alınan MDN özgün giden iletiyle çözümler</span><span class="sxs-lookup"><span data-stu-id="e1e1a-144">Reconciles a received MDN with the original outbound message</span></span>
* <span data-ttu-id="e1e1a-145">Güncelleştirmeleri ve takası veritabanındaki kayıtları karşılık gelen</span><span class="sxs-lookup"><span data-stu-id="e1e1a-145">Updates and correlates records in the non-repudiation database</span></span>
* <span data-ttu-id="e1e1a-146">AS2 durumu raporlama için kayıtları Yazar</span><span class="sxs-lookup"><span data-stu-id="e1e1a-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="e1e1a-147">Base64 kodlu çıkış yükü dosyalarla</span><span class="sxs-lookup"><span data-stu-id="e1e1a-147">The output payload contents are base64 encoded</span></span>
* <span data-ttu-id="e1e1a-148">Bir MDN gereklidir ve olup MDN zaman uyumlu veya zaman uyumsuz yapılandırmaya AS2 sözleşmesi göre belirler</span><span class="sxs-lookup"><span data-stu-id="e1e1a-148">Determines whether an MDN is required, and whether the MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="e1e1a-149">(Sözleşmesi yapılandırmalarını temel alan) zaman uyumlu veya zaman uyumsuz bir MDN oluşturur</span><span class="sxs-lookup"><span data-stu-id="e1e1a-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="e1e1a-150">Bağıntı belirteçleri ve özellikler üzerinde MDN ayarlar</span><span class="sxs-lookup"><span data-stu-id="e1e1a-150">Sets the correlation tokens and properties on the MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="e1e1a-151">Bu örnek deneyin</span><span class="sxs-lookup"><span data-stu-id="e1e1a-151">Try this sample</span></span>

<span data-ttu-id="e1e1a-152">Bir tam olarak işlevsel mantığı uygulamasını ve örnek AS2 senaryoyu dağıtmaya denemek için bkz: [AS2 mantıksal uygulama şablonu ve senaryo](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="e1e1a-152">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="e1e1a-153">Swagger görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="e1e1a-153">View the swagger</span></span>
<span data-ttu-id="e1e1a-154">Bkz: [ayrıntıları swagger](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="e1e1a-154">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e1e1a-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e1e1a-155">Next steps</span></span>
[<span data-ttu-id="e1e1a-156">Enterprise Integration Pack hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="e1e1a-156">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

