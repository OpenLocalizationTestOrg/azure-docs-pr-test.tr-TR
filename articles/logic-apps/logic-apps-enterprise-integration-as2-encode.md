---
title: "AS2 iletileri - Azure mantıksal uygulamaları kodla | Microsoft Docs"
description: "AS2 Kodlayıcı Kurumsal tümleştirme paketinde Azure Logic Apps için kullanma"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 7889bf9e4e02143b6bb4c797531afa54f8647ce5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="54515-103">Azure Logic Apps ile Kurumsal tümleştirme paketi için AS2 iletileri kodlama</span><span class="sxs-lookup"><span data-stu-id="54515-103">Encode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="54515-104">Güvenlik ve güvenilirlik aktaran iletileri sırasında kurmak için kodlama AS2 ileti Bağlayıcısı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="54515-104">To establish security and reliability while transmitting messages, use the Encode AS2 message connector.</span></span> <span data-ttu-id="54515-105">Bu bağlayıcı, dijital imza, şifreleme ve onayları aracılığıyla ileti Disposition bildirimler (hangi ayrıca inkar için desteklemek üzere müşteri adayları MDN), sağlar.</span><span class="sxs-lookup"><span data-stu-id="54515-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads to support for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="54515-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="54515-106">Before you start</span></span>

<span data-ttu-id="54515-107">Gereksinim duyduğunuz öğeleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="54515-107">Here's the items you need:</span></span>

* <span data-ttu-id="54515-108">Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="54515-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="54515-109">Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="54515-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="54515-110">Kodlama AS2 ileti bağlayıcıyı kullanmak üzere bir tümleştirme hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="54515-110">You must have an integration account to use the Encode AS2 message connector.</span></span>
* <span data-ttu-id="54515-111">En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış</span><span class="sxs-lookup"><span data-stu-id="54515-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="54515-112">Bir [AS2 sözleşmesi](logic-apps-enterprise-integration-as2.md) tümleştirme hesabınızda tanımlanan zaten</span><span class="sxs-lookup"><span data-stu-id="54515-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="54515-113">AS2 iletileri kodlama</span><span class="sxs-lookup"><span data-stu-id="54515-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="54515-114">[Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="54515-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="54515-115">Bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz kodlamak AS2 ileti bağlayıcı tetikleyiciler, sahip değil.</span><span class="sxs-lookup"><span data-stu-id="54515-115">The Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="54515-116">Mantıksal Uygulama Tasarımcısı'nda bir tetikleyici ekleyin ve ardından bir eylem mantıksal uygulamanızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="54515-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="54515-117">Arama kutusuna "AS2" filtreniz için girin.</span><span class="sxs-lookup"><span data-stu-id="54515-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="54515-118">Seçin **AS2 - kodlamak AS2 ileti**.</span><span class="sxs-lookup"><span data-stu-id="54515-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    !["AS2" için arama](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="54515-120">Tümleştirme hesabınıza daha önce herhangi bir bağlantısı oluşturmadıysanız, bu bağlantı artık oluşturmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="54515-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="54515-121">Bağlantınızı adlandırın ve bağlamak istediğiniz tümleştirme hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="54515-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![Tümleştirme hesabı bağlantısı oluşturma](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="54515-123">Bir yıldız işareti özelliklerle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="54515-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="54515-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="54515-124">Property</span></span> | <span data-ttu-id="54515-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="54515-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="54515-126">Bağlantı adı *</span><span class="sxs-lookup"><span data-stu-id="54515-126">Connection Name *</span></span> |<span data-ttu-id="54515-127">Bağlantınız için herhangi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="54515-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="54515-128">Tümleştirme hesabını *</span><span class="sxs-lookup"><span data-stu-id="54515-128">Integration Account *</span></span> |<span data-ttu-id="54515-129">Tümleştirme hesabınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="54515-129">Enter a name for your integration account.</span></span> <span data-ttu-id="54515-130">Tümleştirme hesabı ve mantığı uygulamanız aynı Azure konumuna olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="54515-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="54515-131">İşiniz bittiğinde, bağlantı bilgilerinizi bu örneğe benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="54515-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="54515-132">Bağlantınızı oluşturmayı tamamlamak için tercih **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="54515-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![Tümleştirme bağlantı ayrıntıları](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="54515-134">Bu örnekte gösterildiği gibi bağlantınızı oluşturulduktan sonra ayrıntılarını sağlamak **AS2-gelen**, **AS2-tanımlayıcıları** sözleşmenizde, yapılandırılan ve **gövde**, olduğu ileti yükü.</span><span class="sxs-lookup"><span data-stu-id="54515-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-To identifiers** as configured in your agreement, and **Body**, which is the message payload.</span></span>
   
    ![zorunlu alanlar sağlayın](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="54515-136">AS2 Kodlayıcı ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="54515-136">AS2 encoder details</span></span>

<span data-ttu-id="54515-137">Kodlama AS2 Bağlayıcısı'nı bu görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="54515-137">The Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="54515-138">AS2/HTTP üstbilgileri uygular</span><span class="sxs-lookup"><span data-stu-id="54515-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="54515-139">İletiler (yapılandırılmışsa) giden işaretleri</span><span class="sxs-lookup"><span data-stu-id="54515-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="54515-140">Giden iletileri şifreler (yapılandırıldıysa)</span><span class="sxs-lookup"><span data-stu-id="54515-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="54515-141">İletisi (yapılandırılmışsa) sıkıştırır</span><span class="sxs-lookup"><span data-stu-id="54515-141">Compresses the message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="54515-142">Bu örnek deneyin</span><span class="sxs-lookup"><span data-stu-id="54515-142">Try this sample</span></span>

<span data-ttu-id="54515-143">Bir tam olarak işlevsel mantığı uygulamasını ve örnek AS2 senaryoyu dağıtmaya denemek için bkz: [AS2 mantıksal uygulama şablonu ve senaryo](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="54515-143">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="54515-144">Swagger görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="54515-144">View the swagger</span></span>
<span data-ttu-id="54515-145">Bkz: [ayrıntıları swagger](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="54515-145">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="54515-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54515-146">Next steps</span></span>
[<span data-ttu-id="54515-147">Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="54515-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

