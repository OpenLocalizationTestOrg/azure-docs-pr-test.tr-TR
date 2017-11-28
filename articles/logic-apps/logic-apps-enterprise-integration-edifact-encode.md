---
title: "EDIFACT iletileri - Azure mantıksal uygulamaları kodla | Microsoft Docs"
description: "EDI doğrulamak ve XML Azure Logic Apps için EDIFACT ileti Kodlayıcı Kurumsal tümleştirme paketi oluştur"
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
ms.openlocfilehash: b8d577326d23ec45cb4a9ec0e450ebf7afd945f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="e8613-103">Azure Logic Apps ile Kurumsal tümleştirme paketi için EDIFACT iletileri kodlama</span><span class="sxs-lookup"><span data-stu-id="e8613-103">Encode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="e8613-104">Kodlama EDIFACT ileti bağlayıcısıyla EDI ve iş ortağı özgü özellikler doğrulamak, her işlem kümesi için bir XML belgesi oluşturmak ve teknik bir bildirim, işlevsel bildirim ya da her ikisini de isteyin.</span><span class="sxs-lookup"><span data-stu-id="e8613-104">With the Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="e8613-105">Bu bağlayıcıyı kullanmak için bağlayıcıyı mantıksal uygulamanızı varolan bir tetikleyicinin eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8613-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e8613-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e8613-106">Before you start</span></span>

<span data-ttu-id="e8613-107">Gereksinim duyduğunuz öğeleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e8613-107">Here's the items you need:</span></span>

* <span data-ttu-id="e8613-108">Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="e8613-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="e8613-109">Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="e8613-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="e8613-110">Kodlama EDIFACT ileti bağlayıcıyı kullanmak üzere bir tümleştirme hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8613-110">You must have an integration account to use the Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="e8613-111">En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış</span><span class="sxs-lookup"><span data-stu-id="e8613-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="e8613-112">Bir [EDIFACT sözleşmesi](logic-apps-enterprise-integration-edifact.md) tümleştirme hesabınızda tanımlanan zaten</span><span class="sxs-lookup"><span data-stu-id="e8613-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="e8613-113">EDIFACT iletileri kodlama</span><span class="sxs-lookup"><span data-stu-id="e8613-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="e8613-114">[Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e8613-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="e8613-115">Bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz kodlamak EDIFACT ileti bağlayıcı tetikleyiciler, sahip değil.</span><span class="sxs-lookup"><span data-stu-id="e8613-115">The Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="e8613-116">Mantıksal Uygulama Tasarımcısı'nda bir tetikleyici ekleyin ve ardından bir eylem mantıksal uygulamanızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e8613-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="e8613-117">Arama kutusuna "EDIFACT", filtre olarak girin.</span><span class="sxs-lookup"><span data-stu-id="e8613-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="e8613-118">Şunlardan birini seçin **EDIFACT iletiyle kodlamak anlaşma adı** veya **EDIFACT iletisi kimlikleri tarafından kodla**.</span><span class="sxs-lookup"><span data-stu-id="e8613-118">Select either **Encode EDIFACT Message by agreement name** or **Encode to EDIFACT message by identities**.</span></span>
   
    ![EDIFACT arama](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="e8613-120">Tümleştirme hesabınıza daha önce herhangi bir bağlantısı oluşturmadıysanız, bu bağlantı artık oluşturmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="e8613-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="e8613-121">Bağlantınızı adlandırın ve bağlamak istediğiniz tümleştirme hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="e8613-121">Name your connection, and select the integration account that you want to connect.</span></span>

    ![Tümleştirme hesap bağlantısı oluşturma](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="e8613-123">Bir yıldız işareti özelliklerle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e8613-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="e8613-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="e8613-124">Property</span></span> | <span data-ttu-id="e8613-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="e8613-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="e8613-126">Bağlantı adı *</span><span class="sxs-lookup"><span data-stu-id="e8613-126">Connection Name *</span></span> |<span data-ttu-id="e8613-127">Bağlantınız için herhangi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="e8613-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="e8613-128">Tümleştirme hesabını *</span><span class="sxs-lookup"><span data-stu-id="e8613-128">Integration Account *</span></span> |<span data-ttu-id="e8613-129">Tümleştirme hesabınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="e8613-129">Enter a name for your integration account.</span></span> <span data-ttu-id="e8613-130">Tümleştirme hesabı ve mantığı uygulamanız aynı Azure konumuna olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e8613-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="e8613-131">İşiniz bittiğinde, bağlantı bilgilerinizi bu örneğe benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="e8613-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="e8613-132">Bağlantınızı oluşturmayı tamamlamak için tercih **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e8613-132">To finish creating your connection, choose **Create**.</span></span>

    ![Tümleştirme hesap bağlantı ayrıntıları](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="e8613-134">Bağlantınızı şimdi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e8613-134">Your connection is now created.</span></span>

    ![oluşturulan tümleştirme hesap bağlantı](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="e8613-136">Anlaşma adı tarafından EDIFACT ileti kodlama</span><span class="sxs-lookup"><span data-stu-id="e8613-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="e8613-137">Anlaşma adı tarafından EDIFACT iletileri kodlamak seçerseniz, açık **adı, EDIFACT sözleşmesi** listesinde, girin veya EDIFACT sözleşmesi adınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="e8613-137">If you chose to encode EDIFACT messages by agreement name, open the **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="e8613-138">Kodlanacak XML ileti girin.</span><span class="sxs-lookup"><span data-stu-id="e8613-138">Enter the XML message to encode.</span></span>

![EDIFACT sözleşmesi adını ve kodlamak için XML iletisini girin](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="e8613-140">EDIFACT iletisi kimlikleri tarafından kodlama</span><span class="sxs-lookup"><span data-stu-id="e8613-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="e8613-141">EDIFACT iletileri tarafından kimlikleri kodlamak seçerseniz, gönderen tanımlayıcısı, gönderen Niteleyici, alıcı tanımlayıcısı ve EDIFACT sözleşmenizde yapılandırılan alıcı niteleyici girin.</span><span class="sxs-lookup"><span data-stu-id="e8613-141">If you choose to encode EDIFACT messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="e8613-142">Kodlanacak XML iletiyi seçin.</span><span class="sxs-lookup"><span data-stu-id="e8613-142">Select the XML message to encode.</span></span>

![Göndereni ve alıcısı için kimlikleri sağlamak için kodlamak için XML ileti seçin](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="e8613-144">EDIFACT kodlamak ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="e8613-144">EDIFACT Encode details</span></span>

<span data-ttu-id="e8613-145">Kodlama EDIFACT connector, şu görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="e8613-145">The Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="e8613-146">Gönderen niteleyicisi & tanımlayıcısı ve alıcı niteleyicisi ve tanımlayıcısı eşleştirerek anlaşmayı çözümleyin</span><span class="sxs-lookup"><span data-stu-id="e8613-146">Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="e8613-147">EDI işlem değişim kümelerinde XML olarak kodlanmış iletileri dönüştürme EDI değişim serileştirir.</span><span class="sxs-lookup"><span data-stu-id="e8613-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="e8613-148">İşlem kümesi üstbilgi ve toplamı kesimleri uygular</span><span class="sxs-lookup"><span data-stu-id="e8613-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="e8613-149">Bir değişim denetim sayısı, Grup denetim numarası ve her giden değişim için bir işlem kümesi denetim sayı oluşturur</span><span class="sxs-lookup"><span data-stu-id="e8613-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="e8613-150">Ayırıcılar yükü veri değiştirir</span><span class="sxs-lookup"><span data-stu-id="e8613-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="e8613-151">EDI ve iş ortağı özgü özellikleri doğrular</span><span class="sxs-lookup"><span data-stu-id="e8613-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="e8613-152">Şema doğrulama ileti şemayla işlem kümesi veri öğelerinin.</span><span class="sxs-lookup"><span data-stu-id="e8613-152">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="e8613-153">EDI, üzerinde işlem kümesi veri öğeleri doğrulamanın.</span><span class="sxs-lookup"><span data-stu-id="e8613-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="e8613-154">İşlem kümesi veri öğeleri üzerinde Genişletilmiş doğrulamanın</span><span class="sxs-lookup"><span data-stu-id="e8613-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="e8613-155">Her işlem kümesi için bir XML belgesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e8613-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="e8613-156">Teknik ve/veya işlevsel bir bildirim (yapılandırılmışsa) ister.</span><span class="sxs-lookup"><span data-stu-id="e8613-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="e8613-157">Teknik bir bildirim CONTRL ileti bir değişim alınmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e8613-157">As a technical acknowledgment, the CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="e8613-158">İşlevsel bir bildirim CONTRL ileti, kabul veya alınan Değişim, Grup veya ileti reddine hataları veya desteklenmeyen işlevlerin listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e8613-158">As a functional acknowledgment, the CONTRL message indicates acceptance or rejection of the received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="e8613-159">Görünüm Swagger dosyası</span><span class="sxs-lookup"><span data-stu-id="e8613-159">View Swagger file</span></span>
<span data-ttu-id="e8613-160">EDIFACT bağlayıcı Swagger ayrıntılarını görüntülemek için bkz: [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="e8613-160">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8613-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e8613-161">Next steps</span></span>
[<span data-ttu-id="e8613-162">Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="e8613-162">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

