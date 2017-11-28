---
title: aaaEncode AS2 iletileri - Azure Logic Apps | Microsoft Docs
description: "Nasıl toouse hello AS2 Kodlayıcısı hello Kurumsal tümleştirme paketi ile Azure mantıksal uygulamaları için"
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
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="2e29b-103">AS2 iletileri için Azure Logic Apps Enterprise Integration Pack Merhaba ile kodlayın.</span><span class="sxs-lookup"><span data-stu-id="2e29b-103">Encode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="2e29b-104">tooestablish güvenlik ve güvenilirlik iletileri aktarımı sırasında hello kodlamak AS2 ileti bağlayıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e29b-104">tooestablish security and reliability while transmitting messages, use hello Encode AS2 message connector.</span></span> <span data-ttu-id="2e29b-105">Bu bağlayıcı, dijital imza, şifreleme ve onayları aracılığıyla ileti Disposition bildirimler (hangi toosupport inkar için de müşteri adayları MDN), sağlar.</span><span class="sxs-lookup"><span data-stu-id="2e29b-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads toosupport for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="2e29b-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="2e29b-106">Before you start</span></span>

<span data-ttu-id="2e29b-107">Gereksinim duyduğunuz hello öğeleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="2e29b-107">Here's hello items you need:</span></span>

* <span data-ttu-id="2e29b-108">Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="2e29b-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="2e29b-109">Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="2e29b-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="2e29b-110">Bir tümleştirme hesap toouse hello kodlamak AS2 ileti Bağlayıcısı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e29b-110">You must have an integration account toouse hello Encode AS2 message connector.</span></span>
* <span data-ttu-id="2e29b-111">En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış</span><span class="sxs-lookup"><span data-stu-id="2e29b-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="2e29b-112">Bir [AS2 sözleşmesi](logic-apps-enterprise-integration-as2.md) tümleştirme hesabınızda tanımlanan zaten</span><span class="sxs-lookup"><span data-stu-id="2e29b-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="2e29b-113">AS2 iletileri kodlama</span><span class="sxs-lookup"><span data-stu-id="2e29b-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="2e29b-114">[Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2e29b-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="2e29b-115">bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz hello kodlamak AS2 ileti bağlayıcı tetikleyiciler, sahip değil.</span><span class="sxs-lookup"><span data-stu-id="2e29b-115">hello Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="2e29b-116">Hello mantığı Uygulama Tasarımcısı, tetikleyici ekleyin ve sonra bir eylem tooyour mantıksal uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2e29b-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="2e29b-117">Merhaba arama kutusuna "AS2" filtreniz için girin.</span><span class="sxs-lookup"><span data-stu-id="2e29b-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="2e29b-118">Seçin **AS2 - kodlamak AS2 ileti**.</span><span class="sxs-lookup"><span data-stu-id="2e29b-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    !["AS2" için arama](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="2e29b-120">Tooyour tümleştirme hesabını daha önce herhangi bir bağlantısı oluşturmadıysanız, istenir toocreate şimdi bu bağlantı.</span><span class="sxs-lookup"><span data-stu-id="2e29b-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="2e29b-121">Bağlantınızı adlandırın ve hello tümleştirme hesabı tooconnect istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="2e29b-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![bağlantı toointegration hesabı oluşturma](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="2e29b-123">Bir yıldız işareti özelliklerle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2e29b-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="2e29b-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="2e29b-124">Property</span></span> | <span data-ttu-id="2e29b-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="2e29b-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="2e29b-126">Bağlantı adı *</span><span class="sxs-lookup"><span data-stu-id="2e29b-126">Connection Name *</span></span> |<span data-ttu-id="2e29b-127">Bağlantınız için herhangi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="2e29b-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="2e29b-128">Tümleştirme hesabını *</span><span class="sxs-lookup"><span data-stu-id="2e29b-128">Integration Account *</span></span> |<span data-ttu-id="2e29b-129">Tümleştirme hesabınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="2e29b-129">Enter a name for your integration account.</span></span> <span data-ttu-id="2e29b-130">Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun aynı Azure konumu.</span><span class="sxs-lookup"><span data-stu-id="2e29b-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="2e29b-131">İşiniz bittiğinde, bağlantı ayrıntılarınızı benzer toothis örnek görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="2e29b-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="2e29b-132">bağlantı oluşturma toofinish seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="2e29b-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![Tümleştirme bağlantı ayrıntıları](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="2e29b-134">Bu örnekte gösterildiği gibi bağlantınızı oluşturulduktan sonra ayrıntılarını sağlamak **AS2-gelen**, **AS2 tooidentifiers** sözleşmenizde, yapılandırılan ve **gövde**, olduğu Merhaba ileti yükü.</span><span class="sxs-lookup"><span data-stu-id="2e29b-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-tooidentifiers** as configured in your agreement, and **Body**, which is hello message payload.</span></span>
   
    ![zorunlu alanlar sağlayın](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="2e29b-136">AS2 Kodlayıcı ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="2e29b-136">AS2 encoder details</span></span>

<span data-ttu-id="2e29b-137">Merhaba kodlamak AS2 Bağlayıcısı, şu görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="2e29b-137">hello Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="2e29b-138">AS2/HTTP üstbilgileri uygular</span><span class="sxs-lookup"><span data-stu-id="2e29b-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="2e29b-139">İletiler (yapılandırılmışsa) giden işaretleri</span><span class="sxs-lookup"><span data-stu-id="2e29b-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="2e29b-140">Giden iletileri şifreler (yapılandırıldıysa)</span><span class="sxs-lookup"><span data-stu-id="2e29b-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="2e29b-141">Merhaba iletisi (yapılandırılmışsa) sıkıştırır</span><span class="sxs-lookup"><span data-stu-id="2e29b-141">Compresses hello message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="2e29b-142">Bu örnek deneyin</span><span class="sxs-lookup"><span data-stu-id="2e29b-142">Try this sample</span></span>

<span data-ttu-id="2e29b-143">bir tam olarak işlevsel mantığı uygulamasını ve örnek AS2 senaryo dağıtma tootry bkz hello [AS2 mantıksal uygulama şablonu ve senaryo](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="2e29b-143">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="2e29b-144">Görünüm hello swagger</span><span class="sxs-lookup"><span data-stu-id="2e29b-144">View hello swagger</span></span>
<span data-ttu-id="2e29b-145">Merhaba bkz [ayrıntıları swagger](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="2e29b-145">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2e29b-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2e29b-146">Next steps</span></span>
[<span data-ttu-id="2e29b-147">Merhaba Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="2e29b-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

