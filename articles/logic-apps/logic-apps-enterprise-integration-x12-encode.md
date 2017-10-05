---
title: X12 kodlamak iletileri - Azure Logic Apps | Microsoft Docs
description: "EDI doğrulamak ve XML ile kodlanmış Dönüştür X12 iletilerle ileti Kodlayıcısı Kurumsal tümleştirme paketi ile Azure mantıksal uygulamaları için"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 29d19364b9a98e351c95f13e68a2e63b9f6439f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="f33e0-103">X12 kodlamak Azure Logic Apps Enterprise tümleştirme paketi ile iletileri</span><span class="sxs-lookup"><span data-stu-id="f33e0-103">Encode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="f33e0-104">Kodla X12 ileti bağlayıcısıyla EDI ve iş ortağı özgü özellikler doğrulamak, XML olarak kodlanmış iletileri değiş tokuş EDI işlem kümelerinde dönüştürmek ve teknik bir bildirim, işlevsel bildirim ya da her ikisini de isteyin.</span><span class="sxs-lookup"><span data-stu-id="f33e0-104">With the Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in the interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="f33e0-105">Bu bağlayıcıyı kullanmak için bağlayıcıyı mantıksal uygulamanızı varolan bir tetikleyicinin eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f33e0-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="f33e0-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="f33e0-106">Before you start</span></span>

<span data-ttu-id="f33e0-107">Gereksinim duyduğunuz öğeleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f33e0-107">Here's the items you need:</span></span>

* <span data-ttu-id="f33e0-108">Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="f33e0-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="f33e0-109">Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="f33e0-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="f33e0-110">Kodla X12 ileti bağlayıcıyı kullanmak üzere bir tümleştirme hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f33e0-110">You must have an integration account to use the Encode X12 message connector.</span></span>
* <span data-ttu-id="f33e0-111">En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış</span><span class="sxs-lookup"><span data-stu-id="f33e0-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="f33e0-112">Bir [X12 sözleşmesi](logic-apps-enterprise-integration-x12.md) tümleştirme hesabınızda tanımlanan zaten</span><span class="sxs-lookup"><span data-stu-id="f33e0-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="f33e0-113">X12 kodlamak iletileri</span><span class="sxs-lookup"><span data-stu-id="f33e0-113">Encode X12 messages</span></span>

1. <span data-ttu-id="f33e0-114">[Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f33e0-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="f33e0-115">Bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz kodla X12 ileti bağlayıcı tetikleyiciler, sahip değil.</span><span class="sxs-lookup"><span data-stu-id="f33e0-115">The Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="f33e0-116">Mantıksal Uygulama Tasarımcısı'nda bir tetikleyici ekleyin ve ardından bir eylem mantıksal uygulamanızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f33e0-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="f33e0-117">Arama kutusuna "x12" filtreniz için girin.</span><span class="sxs-lookup"><span data-stu-id="f33e0-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="f33e0-118">Şunlardan birini seçin **X12-kodlamak için X12 ileti anlaşma adı tarafından** veya **X12-kodlamak için X12 kimlikleri ileti**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-118">Select either **X12 - Encode to X12 message by agreement name** or **X12 - Encode to X12 message by identities**.</span></span>
   
    !["X12" için arama](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="f33e0-120">Tümleştirme hesabınıza daha önce herhangi bir bağlantısı oluşturmadıysanız, bu bağlantı artık oluşturmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="f33e0-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="f33e0-121">Bağlantınızı adlandırın ve bağlamak istediğiniz tümleştirme hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="f33e0-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![Tümleştirme hesap bağlantı](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="f33e0-123">Bir yıldız işareti özelliklerle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f33e0-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="f33e0-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="f33e0-124">Property</span></span> | <span data-ttu-id="f33e0-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="f33e0-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="f33e0-126">Bağlantı adı *</span><span class="sxs-lookup"><span data-stu-id="f33e0-126">Connection Name *</span></span> |<span data-ttu-id="f33e0-127">Bağlantınız için herhangi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="f33e0-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="f33e0-128">Tümleştirme hesabını *</span><span class="sxs-lookup"><span data-stu-id="f33e0-128">Integration Account *</span></span> |<span data-ttu-id="f33e0-129">Tümleştirme hesabınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="f33e0-129">Enter a name for your integration account.</span></span> <span data-ttu-id="f33e0-130">Tümleştirme hesabı ve mantığı uygulamanız aynı Azure konumuna olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f33e0-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="f33e0-131">İşiniz bittiğinde, bağlantı bilgilerinizi bu örneğe benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="f33e0-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="f33e0-132">Bağlantınızı oluşturmayı tamamlamak için tercih **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-132">To finish creating your connection, choose **Create**.</span></span>

    ![oluşturulan tümleştirme hesap bağlantı](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="f33e0-134">Bağlantınızı şimdi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f33e0-134">Your connection is now created.</span></span>

    ![Tümleştirme hesap bağlantı ayrıntıları](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="f33e0-136">X12 kodlamak iletileri göre anlaşma adı</span><span class="sxs-lookup"><span data-stu-id="f33e0-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="f33e0-137">X12 kodlamak seçerseniz iletileri anlaşma adı ile açmak **X12 adını anlaşma** listesinde, girin veya mevcut X12 seçin anlaşma.</span><span class="sxs-lookup"><span data-stu-id="f33e0-137">If you chose to encode X12 messages by agreement name, open the **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="f33e0-138">Kodlanacak XML ileti girin.</span><span class="sxs-lookup"><span data-stu-id="f33e0-138">Enter the XML message to encode.</span></span>

![X12 girin anlaşma adı ve kodlamak için XML iletisi](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="f33e0-140">X12 kodlamak kimlikleri iletileri</span><span class="sxs-lookup"><span data-stu-id="f33e0-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="f33e0-141">X12 kodlamak seçerseniz iletileri kimlikleri göre gönderen tanımlayıcısı, gönderen Niteleyici, alıcı tanımlayıcısı ve alıcı Niteleyici, X12 yapılandırıldığı gibi girin anlaşma.</span><span class="sxs-lookup"><span data-stu-id="f33e0-141">If you choose to encode X12 messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="f33e0-142">Kodlanacak XML iletiyi seçin.</span><span class="sxs-lookup"><span data-stu-id="f33e0-142">Select the XML message to encode.</span></span>
   
![Göndereni ve alıcısı için kimlikleri sağlamak için kodlamak için XML ileti seçin](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="f33e0-144">X12 kodlamak ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="f33e0-144">X12 Encode details</span></span>

<span data-ttu-id="f33e0-145">X12 kodla bağlayıcı bu görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="f33e0-145">The X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="f33e0-146">Eşleşen göndereni ve alıcısı bağlam özellikleri tarafından sözleşmesi çözünürlüğü.</span><span class="sxs-lookup"><span data-stu-id="f33e0-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="f33e0-147">EDI işlem değişim kümelerinde XML olarak kodlanmış iletileri dönüştürme EDI değişim serileştirir.</span><span class="sxs-lookup"><span data-stu-id="f33e0-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="f33e0-148">İşlem kümesi üstbilgi ve toplamı kesimleri uygular</span><span class="sxs-lookup"><span data-stu-id="f33e0-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="f33e0-149">Bir değişim denetim sayısı, Grup denetim numarası ve her giden değişim için bir işlem kümesi denetim sayı oluşturur</span><span class="sxs-lookup"><span data-stu-id="f33e0-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="f33e0-150">Ayırıcılar yükü veri değiştirir</span><span class="sxs-lookup"><span data-stu-id="f33e0-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="f33e0-151">EDI ve iş ortağı özgü özellikleri doğrular</span><span class="sxs-lookup"><span data-stu-id="f33e0-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="f33e0-152">Şema doğrulama ileti şema karşı işlem kümesi veri öğelerinin</span><span class="sxs-lookup"><span data-stu-id="f33e0-152">Schema validation of the transaction-set data elements against the message Schema</span></span>
  * <span data-ttu-id="f33e0-153">EDI, üzerinde işlem kümesi veri öğeleri doğrulamanın.</span><span class="sxs-lookup"><span data-stu-id="f33e0-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="f33e0-154">İşlem kümesi veri öğeleri üzerinde Genişletilmiş doğrulamanın</span><span class="sxs-lookup"><span data-stu-id="f33e0-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="f33e0-155">Teknik ve/veya işlevsel bir bildirim (yapılandırılmışsa) ister.</span><span class="sxs-lookup"><span data-stu-id="f33e0-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="f33e0-156">Teknik bir bildirim başlığı doğrulama sonucu olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f33e0-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="f33e0-157">Teknik Bildirim bir değişim üstbilgisi ve adresi alıcı tarafından toplamı işlenmesini durumunu raporlar</span><span class="sxs-lookup"><span data-stu-id="f33e0-157">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver</span></span>
  * <span data-ttu-id="f33e0-158">İşlev bildirim gövde doğrulama sonucu olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f33e0-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="f33e0-159">İşlev bildirim alınan belge işlerken bir hatayla karşılaştı her hata raporları</span><span class="sxs-lookup"><span data-stu-id="f33e0-159">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="f33e0-160">Swagger görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="f33e0-160">View the swagger</span></span>
<span data-ttu-id="f33e0-161">Bkz: [ayrıntıları swagger](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="f33e0-161">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f33e0-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f33e0-162">Next steps</span></span>
[<span data-ttu-id="f33e0-163">Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="f33e0-163">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

