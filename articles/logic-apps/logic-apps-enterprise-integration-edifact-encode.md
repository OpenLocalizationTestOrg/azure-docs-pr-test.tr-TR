---
title: aaaEncode EDIFACT iletileri - Azure Logic Apps | Microsoft Docs
description: "EDI doğrulamak ve Azure Logic Apps için EDIFACT ileti Kodlayıcısı hello Kurumsal tümleştirme paketi ile birlikte XML oluştur"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="f5e5c-103">EDIFACT iletileri için Azure Logic Apps Enterprise Integration Pack Merhaba ile kodlayın.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-103">Encode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="f5e5c-104">Merhaba kodlamak EDIFACT ileti bağlayıcısıyla EDI ve iş ortağı özgü özellikler doğrulamak, her işlem kümesi için bir XML belgesi oluşturmak ve teknik bir bildirim, işlevsel bildirim ya da her ikisini de isteyin.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-104">With hello Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="f5e5c-105">toouse bu bağlayıcı mantıksal uygulamanızı tetikleyici varolan hello bağlayıcı tooan eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="f5e5c-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="f5e5c-106">Before you start</span></span>

<span data-ttu-id="f5e5c-107">Gereksinim duyduğunuz hello öğeleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f5e5c-107">Here's hello items you need:</span></span>

* <span data-ttu-id="f5e5c-108">Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="f5e5c-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="f5e5c-109">Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="f5e5c-110">Bir tümleştirme hesap toouse hello kodlamak EDIFACT ileti Bağlayıcısı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-110">You must have an integration account toouse hello Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="f5e5c-111">En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış</span><span class="sxs-lookup"><span data-stu-id="f5e5c-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="f5e5c-112">Bir [EDIFACT sözleşmesi](logic-apps-enterprise-integration-edifact.md) tümleştirme hesabınızda tanımlanan zaten</span><span class="sxs-lookup"><span data-stu-id="f5e5c-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="f5e5c-113">EDIFACT iletileri kodlama</span><span class="sxs-lookup"><span data-stu-id="f5e5c-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="f5e5c-114">[Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f5e5c-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="f5e5c-115">bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz hello kodlamak EDIFACT ileti bağlayıcı tetikleyiciler, sahip değil.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-115">hello Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="f5e5c-116">Hello mantığı Uygulama Tasarımcısı, tetikleyici ekleyin ve sonra bir eylem tooyour mantıksal uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="f5e5c-117">Merhaba arama kutusuna "EDIFACT", filtre olarak girin.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="f5e5c-118">Şunlardan birini seçin **EDIFACT iletiyle kodlamak anlaşma adı** veya **kodla tooEDIFACT iletisi kimlikleri tarafından**.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-118">Select either **Encode EDIFACT Message by agreement name** or **Encode tooEDIFACT message by identities**.</span></span>
   
    ![EDIFACT arama](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="f5e5c-120">Tooyour tümleştirme hesabını daha önce herhangi bir bağlantısı oluşturmadıysanız, istenir toocreate şimdi bu bağlantı.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="f5e5c-121">Bağlantınızı adlandırın ve hello tümleştirme hesabı tooconnect istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>

    ![Tümleştirme hesap bağlantısı oluşturma](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="f5e5c-123">Bir yıldız işareti özelliklerle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="f5e5c-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="f5e5c-124">Property</span></span> | <span data-ttu-id="f5e5c-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="f5e5c-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="f5e5c-126">Bağlantı adı *</span><span class="sxs-lookup"><span data-stu-id="f5e5c-126">Connection Name *</span></span> |<span data-ttu-id="f5e5c-127">Bağlantınız için herhangi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="f5e5c-128">Tümleştirme hesabını *</span><span class="sxs-lookup"><span data-stu-id="f5e5c-128">Integration Account *</span></span> |<span data-ttu-id="f5e5c-129">Tümleştirme hesabınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-129">Enter a name for your integration account.</span></span> <span data-ttu-id="f5e5c-130">Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun aynı Azure konumu.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="f5e5c-131">İşiniz bittiğinde, bağlantı ayrıntılarınızı benzer toothis örnek görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="f5e5c-132">bağlantı oluşturma toofinish seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-132">toofinish creating your connection, choose **Create**.</span></span>

    ![Tümleştirme hesap bağlantı ayrıntıları](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="f5e5c-134">Bağlantınızı şimdi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-134">Your connection is now created.</span></span>

    ![oluşturulan tümleştirme hesap bağlantı](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="f5e5c-136">Anlaşma adı tarafından EDIFACT ileti kodlama</span><span class="sxs-lookup"><span data-stu-id="f5e5c-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="f5e5c-137">Anlaşma adı tarafından EDIFACT iletileri tooencode seçerseniz, hello açmak **adı, EDIFACT sözleşmesi** listesinde, girin veya EDIFACT sözleşmesi adınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-137">If you chose tooencode EDIFACT messages by agreement name, open hello **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="f5e5c-138">Merhaba XML ileti tooencode girin.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-138">Enter hello XML message tooencode.</span></span>

![EDIFACT sözleşmesi adını ve XML ileti tooencode girin](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="f5e5c-140">EDIFACT iletisi kimlikleri tarafından kodlama</span><span class="sxs-lookup"><span data-stu-id="f5e5c-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="f5e5c-141">Tarafından kimlikleri EDIFACT iletileri tooencode seçerseniz, hello gönderen tanımlayıcısı, gönderen Niteleyici, alıcı tanımlayıcısı ve EDIFACT sözleşmenizde yapılandırılan alıcı niteleyici girin.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-141">If you choose tooencode EDIFACT messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="f5e5c-142">Merhaba XML ileti tooencode seçin.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-142">Select hello XML message tooencode.</span></span>

![Göndereni ve alıcısı için kimlikleri sağlamak için XML ileti tooencode seçin](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="f5e5c-144">EDIFACT kodlamak ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="f5e5c-144">EDIFACT Encode details</span></span>

<span data-ttu-id="f5e5c-145">Hello kodlamak EDIFACT connector, şu görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="f5e5c-145">hello Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="f5e5c-146">Merhaba gönderen niteleyicisi & tanımlayıcısı ve alıcı niteleyicisi ve tanımlayıcısı eşleştirerek Hello sözleşmesi çözümleyin</span><span class="sxs-lookup"><span data-stu-id="f5e5c-146">Resolve hello agreement by matching hello sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="f5e5c-147">EDI işlem hello değişim kümelerinde XML olarak kodlanmış iletileri dönüştürme hello EDI değişim serileştirir.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="f5e5c-148">İşlem kümesi üstbilgi ve toplamı kesimleri uygular</span><span class="sxs-lookup"><span data-stu-id="f5e5c-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="f5e5c-149">Bir değişim denetim sayısı, Grup denetim numarası ve her giden değişim için bir işlem kümesi denetim sayı oluşturur</span><span class="sxs-lookup"><span data-stu-id="f5e5c-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="f5e5c-150">Ayırıcı hello yükü veri olarak değiştirir</span><span class="sxs-lookup"><span data-stu-id="f5e5c-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="f5e5c-151">EDI ve iş ortağı özgü özellikleri doğrular</span><span class="sxs-lookup"><span data-stu-id="f5e5c-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="f5e5c-152">Merhaba işlem kümesi veri öğeleri hello ileti şemasına karşılık şema doğrulamasını.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-152">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="f5e5c-153">EDI, üzerinde işlem kümesi veri öğeleri doğrulamanın.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="f5e5c-154">İşlem kümesi veri öğeleri üzerinde Genişletilmiş doğrulamanın</span><span class="sxs-lookup"><span data-stu-id="f5e5c-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="f5e5c-155">Her işlem kümesi için bir XML belgesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="f5e5c-156">Teknik ve/veya işlevsel bir bildirim (yapılandırılmışsa) ister.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="f5e5c-157">Teknik bir bildirim hello CONTRL ileti bir değişim alınmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-157">As a technical acknowledgment, hello CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="f5e5c-158">İşlevsel bir bildirim hello CONTRL ileti, kabul veya alınan hello Değişim, Grup veya ileti reddine hataları veya desteklenmeyen işlevlerin listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f5e5c-158">As a functional acknowledgment, hello CONTRL message indicates acceptance or rejection of hello received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="f5e5c-159">Görünüm Swagger dosyası</span><span class="sxs-lookup"><span data-stu-id="f5e5c-159">View Swagger file</span></span>
<span data-ttu-id="f5e5c-160">tooview hello Swagger hello EDIFACT bağlayıcı ayrıntılarını görmek [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="f5e5c-160">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5e5c-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f5e5c-161">Next steps</span></span>
[<span data-ttu-id="f5e5c-162">Merhaba Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="f5e5c-162">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

