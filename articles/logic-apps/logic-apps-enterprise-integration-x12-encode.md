---
title: aaaEncode X12 iletileri - Azure Logic Apps | Microsoft Docs
description: "EDI doğrulamak ve XML ile kodlanmış Dönüştür X12 iletilerle ileti Kodlayıcısı hello Kurumsal tümleştirme paketi ile Azure mantıksal uygulamaları için"
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
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="8eb97-103">X12 kodlamak hello Kurumsal tümleştirme paketi ile Azure Logic Apps için iletileri</span><span class="sxs-lookup"><span data-stu-id="8eb97-103">Encode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="8eb97-104">Merhaba kodla X12 ileti bağlayıcısıyla EDI ve iş ortağı özgü özellikler doğrulamak, XML olarak kodlanmış iletileri EDI işlem hello değişim kümelerinde dönüştürmek ve teknik bir bildirim, işlevsel bildirim ya da her ikisini de isteyin.</span><span class="sxs-lookup"><span data-stu-id="8eb97-104">With hello Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in hello interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="8eb97-105">toouse bu bağlayıcı mantıksal uygulamanızı tetikleyici varolan hello bağlayıcı tooan eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8eb97-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="8eb97-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="8eb97-106">Before you start</span></span>

<span data-ttu-id="8eb97-107">Gereksinim duyduğunuz hello öğeleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="8eb97-107">Here's hello items you need:</span></span>

* <span data-ttu-id="8eb97-108">Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="8eb97-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="8eb97-109">Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="8eb97-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="8eb97-110">Bir tümleştirme hesap toouse hello kodla X12 ileti Bağlayıcısı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8eb97-110">You must have an integration account toouse hello Encode X12 message connector.</span></span>
* <span data-ttu-id="8eb97-111">En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış</span><span class="sxs-lookup"><span data-stu-id="8eb97-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="8eb97-112">Bir [X12 sözleşmesi](logic-apps-enterprise-integration-x12.md) tümleştirme hesabınızda tanımlanan zaten</span><span class="sxs-lookup"><span data-stu-id="8eb97-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="8eb97-113">X12 kodlamak iletileri</span><span class="sxs-lookup"><span data-stu-id="8eb97-113">Encode X12 messages</span></span>

1. <span data-ttu-id="8eb97-114">[Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8eb97-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="8eb97-115">bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz hello kodla X12 ileti bağlayıcı tetikleyiciler, sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8eb97-115">hello Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="8eb97-116">Hello mantığı Uygulama Tasarımcısı, tetikleyici ekleyin ve sonra bir eylem tooyour mantıksal uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8eb97-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="8eb97-117">Merhaba arama kutusuna "x12" filtreniz için girin.</span><span class="sxs-lookup"><span data-stu-id="8eb97-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="8eb97-118">Şunlardan birini seçin **X12-tooX12 ileti sözleşmesi adıyla kodlamak** veya **X12-tooX12 iletisi kimlikleri tarafından kodla**.</span><span class="sxs-lookup"><span data-stu-id="8eb97-118">Select either **X12 - Encode tooX12 message by agreement name** or **X12 - Encode tooX12 message by identities**.</span></span>
   
    !["X12" için arama](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="8eb97-120">Tooyour tümleştirme hesabını daha önce herhangi bir bağlantısı oluşturmadıysanız, istenir toocreate şimdi bu bağlantı.</span><span class="sxs-lookup"><span data-stu-id="8eb97-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="8eb97-121">Bağlantınızı adlandırın ve hello tümleştirme hesabı tooconnect istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="8eb97-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![Tümleştirme hesap bağlantı](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="8eb97-123">Bir yıldız işareti özelliklerle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8eb97-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="8eb97-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="8eb97-124">Property</span></span> | <span data-ttu-id="8eb97-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="8eb97-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="8eb97-126">Bağlantı adı *</span><span class="sxs-lookup"><span data-stu-id="8eb97-126">Connection Name *</span></span> |<span data-ttu-id="8eb97-127">Bağlantınız için herhangi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="8eb97-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="8eb97-128">Tümleştirme hesabını *</span><span class="sxs-lookup"><span data-stu-id="8eb97-128">Integration Account *</span></span> |<span data-ttu-id="8eb97-129">Tümleştirme hesabınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="8eb97-129">Enter a name for your integration account.</span></span> <span data-ttu-id="8eb97-130">Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun aynı Azure konumu.</span><span class="sxs-lookup"><span data-stu-id="8eb97-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="8eb97-131">İşiniz bittiğinde, bağlantı ayrıntılarınızı benzer toothis örnek görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="8eb97-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="8eb97-132">bağlantı oluşturma toofinish seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="8eb97-132">toofinish creating your connection, choose **Create**.</span></span>

    ![oluşturulan tümleştirme hesap bağlantı](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="8eb97-134">Bağlantınızı şimdi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8eb97-134">Your connection is now created.</span></span>

    ![Tümleştirme hesap bağlantı ayrıntıları](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="8eb97-136">X12 kodlamak iletileri göre anlaşma adı</span><span class="sxs-lookup"><span data-stu-id="8eb97-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="8eb97-137">Anlaşma adı tarafından tooencode X12 iletileri seçerseniz hello açmak **X12 adını anlaşma** listesinde, girin veya mevcut X12 seçin anlaşma.</span><span class="sxs-lookup"><span data-stu-id="8eb97-137">If you chose tooencode X12 messages by agreement name, open hello **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="8eb97-138">Merhaba XML ileti tooencode girin.</span><span class="sxs-lookup"><span data-stu-id="8eb97-138">Enter hello XML message tooencode.</span></span>

![X12 girin adı ve XML tooencode ileti sözleşmesi](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="8eb97-140">X12 kodlamak kimlikleri iletileri</span><span class="sxs-lookup"><span data-stu-id="8eb97-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="8eb97-141">Kimlikleri tarafından tooencode X12 iletileri seçerseniz hello gönderen tanımlayıcısı, gönderen Niteleyici, alıcı tanımlayıcısı ve alıcı Niteleyici, X12 yapılandırıldığı gibi girin anlaşma.</span><span class="sxs-lookup"><span data-stu-id="8eb97-141">If you choose tooencode X12 messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="8eb97-142">Merhaba XML ileti tooencode seçin.</span><span class="sxs-lookup"><span data-stu-id="8eb97-142">Select hello XML message tooencode.</span></span>
   
![Göndereni ve alıcısı için kimlikleri sağlamak için XML ileti tooencode seçin](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="8eb97-144">X12 kodlamak ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="8eb97-144">X12 Encode details</span></span>

<span data-ttu-id="8eb97-145">Merhaba X12 kodla connector, şu görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="8eb97-145">hello X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="8eb97-146">Eşleşen göndereni ve alıcısı bağlam özellikleri tarafından sözleşmesi çözünürlüğü.</span><span class="sxs-lookup"><span data-stu-id="8eb97-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="8eb97-147">EDI işlem hello değişim kümelerinde XML olarak kodlanmış iletileri dönüştürme hello EDI değişim serileştirir.</span><span class="sxs-lookup"><span data-stu-id="8eb97-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="8eb97-148">İşlem kümesi üstbilgi ve toplamı kesimleri uygular</span><span class="sxs-lookup"><span data-stu-id="8eb97-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="8eb97-149">Bir değişim denetim sayısı, Grup denetim numarası ve her giden değişim için bir işlem kümesi denetim sayı oluşturur</span><span class="sxs-lookup"><span data-stu-id="8eb97-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="8eb97-150">Ayırıcı hello yükü veri olarak değiştirir</span><span class="sxs-lookup"><span data-stu-id="8eb97-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="8eb97-151">EDI ve iş ortağı özgü özellikleri doğrular</span><span class="sxs-lookup"><span data-stu-id="8eb97-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="8eb97-152">Selamlama iletisine şema karşı hello işlem kümesi veri öğelerinin şema doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8eb97-152">Schema validation of hello transaction-set data elements against hello message Schema</span></span>
  * <span data-ttu-id="8eb97-153">EDI, üzerinde işlem kümesi veri öğeleri doğrulamanın.</span><span class="sxs-lookup"><span data-stu-id="8eb97-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="8eb97-154">İşlem kümesi veri öğeleri üzerinde Genişletilmiş doğrulamanın</span><span class="sxs-lookup"><span data-stu-id="8eb97-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="8eb97-155">Teknik ve/veya işlevsel bir bildirim (yapılandırılmışsa) ister.</span><span class="sxs-lookup"><span data-stu-id="8eb97-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="8eb97-156">Teknik bir bildirim başlığı doğrulama sonucu olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8eb97-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="8eb97-157">Merhaba Teknik Bildirim hello bir değişim üstbilgi ve toplamı hello adresi alıcı tarafından işlenmesini hello durumunu raporlar</span><span class="sxs-lookup"><span data-stu-id="8eb97-157">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver</span></span>
  * <span data-ttu-id="8eb97-158">İşlev bildirim gövde doğrulama sonucu olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8eb97-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="8eb97-159">Merhaba işlevsel bildirim belge hello işleme alınan karşılaştı her hata raporları</span><span class="sxs-lookup"><span data-stu-id="8eb97-159">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="8eb97-160">Görünüm hello swagger</span><span class="sxs-lookup"><span data-stu-id="8eb97-160">View hello swagger</span></span>
<span data-ttu-id="8eb97-161">Merhaba bkz [ayrıntıları swagger](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="8eb97-161">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8eb97-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8eb97-162">Next steps</span></span>
[<span data-ttu-id="8eb97-163">Merhaba Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="8eb97-163">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

