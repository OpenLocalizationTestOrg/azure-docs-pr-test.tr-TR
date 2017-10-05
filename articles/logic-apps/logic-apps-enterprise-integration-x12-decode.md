---
title: "X12 kod çözme iletileri - Azure Logic Apps | Microsoft Docs"
description: "EDI doğrulamak ve X12 ile onayları oluşturmak Azure Logic Apps için Kurumsal tümleştirme paketindeki ileti Kodlayıcısı"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 18719a8f49c74973947517161f7306c233a9323f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="fc48d-103">X12 kod çözme Azure Logic Apps Enterprise tümleştirme paketi ile iletileri</span><span class="sxs-lookup"><span data-stu-id="fc48d-103">Decode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="fc48d-104">Kod çözme X12 ileti bağlayıcısıyla, ticari ortak sözleşmesi karşı Zarf doğrulamak, EDI ve iş ortağı özgü özellikler doğrulamak, işlemleri kümeleri içine etkileşimler bölme veya tüm etkileşimler korumak ve ilgili kaynaklar oluştur işlenen işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="fc48d-104">With the Decode X12 message connector, you can validate the envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="fc48d-105">Bu bağlayıcıyı kullanmak için bağlayıcıyı mantıksal uygulamanızı varolan bir tetikleyicinin eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc48d-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="fc48d-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="fc48d-106">Before you start</span></span>

<span data-ttu-id="fc48d-107">Gereksinim duyduğunuz öğeleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fc48d-107">Here's the items you need:</span></span>

* <span data-ttu-id="fc48d-108">Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="fc48d-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="fc48d-109">Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="fc48d-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="fc48d-110">Kod çözme X12 ileti bağlayıcıyı kullanmak üzere bir tümleştirme hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc48d-110">You must have an integration account to use the Decode X12 message connector.</span></span>
* <span data-ttu-id="fc48d-111">En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış</span><span class="sxs-lookup"><span data-stu-id="fc48d-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="fc48d-112">Bir [X12 sözleşmesi](logic-apps-enterprise-integration-x12.md) tümleştirme hesabınızda tanımlanan zaten</span><span class="sxs-lookup"><span data-stu-id="fc48d-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="fc48d-113">X12 kod çözme iletileri</span><span class="sxs-lookup"><span data-stu-id="fc48d-113">Decode X12 messages</span></span>

1. <span data-ttu-id="fc48d-114">[Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="fc48d-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="fc48d-115">Bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz kod çözme X12 ileti bağlayıcı tetikleyiciler, sahip değil.</span><span class="sxs-lookup"><span data-stu-id="fc48d-115">The Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="fc48d-116">Mantıksal Uygulama Tasarımcısı'nda bir tetikleyici ekleyin ve ardından bir eylem mantıksal uygulamanızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fc48d-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="fc48d-117">Arama kutusuna "x12" filtreniz için girin.</span><span class="sxs-lookup"><span data-stu-id="fc48d-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="fc48d-118">Seçin **X12-X12 kod çözme ileti**.</span><span class="sxs-lookup"><span data-stu-id="fc48d-118">Select **X12 - Decode X12 message**.</span></span>
   
    !["X12" için arama](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="fc48d-120">Tümleştirme hesabınıza daha önce herhangi bir bağlantısı oluşturmadıysanız, bu bağlantı artık oluşturmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="fc48d-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="fc48d-121">Bağlantınızı adlandırın ve bağlamak istediğiniz tümleştirme hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="fc48d-121">Name your connection, and select the integration account that you want to connect.</span></span> 

    ![Hesap bağlantı ayrıntıları tümleştirme sağlar](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="fc48d-123">Bir yıldız işareti özelliklerle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fc48d-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="fc48d-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="fc48d-124">Property</span></span> | <span data-ttu-id="fc48d-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="fc48d-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="fc48d-126">Bağlantı adı *</span><span class="sxs-lookup"><span data-stu-id="fc48d-126">Connection Name *</span></span> |<span data-ttu-id="fc48d-127">Bağlantınız için herhangi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="fc48d-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="fc48d-128">Tümleştirme hesabını *</span><span class="sxs-lookup"><span data-stu-id="fc48d-128">Integration Account *</span></span> |<span data-ttu-id="fc48d-129">Tümleştirme hesabınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="fc48d-129">Enter a name for your integration account.</span></span> <span data-ttu-id="fc48d-130">Tümleştirme hesabı ve mantığı uygulamanız aynı Azure konumuna olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fc48d-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="fc48d-131">İşiniz bittiğinde, bağlantı bilgilerinizi bu örneğe benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="fc48d-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="fc48d-132">Bağlantınızı oluşturmayı tamamlamak için tercih **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="fc48d-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![Tümleştirme hesap bağlantı ayrıntıları](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="fc48d-134">Kod çözme için select X12 düz dosya ileti bu örnekte gösterildiği gibi bağlantınızı sonra oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fc48d-134">After your connection is created, as shown in this example, select the X12 flat file message to decode.</span></span>

    ![oluşturulan tümleştirme hesap bağlantı](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="fc48d-136">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fc48d-136">For example:</span></span>

    ![Kod çözme için dosya iletisi SELECT X12 düz](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="fc48d-138">X12 kod çözme ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="fc48d-138">X12 Decode details</span></span>

<span data-ttu-id="fc48d-139">X12 kod çözme bağlayıcı bu görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="fc48d-139">The X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="fc48d-140">Ticari ortak sözleşmesi karşı Zarf doğrular</span><span class="sxs-lookup"><span data-stu-id="fc48d-140">Validates the envelope against trading partner agreement</span></span>
* <span data-ttu-id="fc48d-141">EDI ve iş ortağı özgü özellikleri doğrular</span><span class="sxs-lookup"><span data-stu-id="fc48d-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="fc48d-142">EDI yapısal doğrulama ve genişletilmiş şema doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fc48d-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="fc48d-143">Değişim Zarf yapısını doğrulama.</span><span class="sxs-lookup"><span data-stu-id="fc48d-143">Validation of the structure of the interchange envelope.</span></span>
  * <span data-ttu-id="fc48d-144">Zarf denetim şemasına karşılık şema doğrulamasını.</span><span class="sxs-lookup"><span data-stu-id="fc48d-144">Schema validation of the envelope against the control schema.</span></span>
  * <span data-ttu-id="fc48d-145">Şema doğrulama ileti şemayla işlem kümesi veri öğelerinin.</span><span class="sxs-lookup"><span data-stu-id="fc48d-145">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="fc48d-146">İşlem kümesi veri öğelerinde EDI doğrulamanın</span><span class="sxs-lookup"><span data-stu-id="fc48d-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="fc48d-147">Değişim, Grup ve işlem kümesi denetim numaraları çoğaltmaları olmadığını doğrular</span><span class="sxs-lookup"><span data-stu-id="fc48d-147">Verifies that the interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="fc48d-148">Değişim kontrol numarası önceden alınmış etkileşimler karşı denetler.</span><span class="sxs-lookup"><span data-stu-id="fc48d-148">Checks the interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="fc48d-149">Grup denetim numarası değişim diğer Grup denetimi numaraları karşı denetler.</span><span class="sxs-lookup"><span data-stu-id="fc48d-149">Checks the group control number against other group control numbers in the interchange.</span></span>
  * <span data-ttu-id="fc48d-150">Bu gruptaki diğer işlem kümesi denetim numaraları karşı işlem kümesi denetim numarası denetler.</span><span class="sxs-lookup"><span data-stu-id="fc48d-150">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="fc48d-151">İşlem kümeleri içine değişim böler veya tüm değişim korur:</span><span class="sxs-lookup"><span data-stu-id="fc48d-151">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="fc48d-152">Bölünmüş değişim işlem kümeleri - olarak askıya alma işlem kümeleri hatası: bölmelerini değişim hareket halinde ayarlar ve her işlem kümesi ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="fc48d-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="fc48d-153">Kod çözme eylem çıkarır yalnızca bu işlem ayarlar X12 için doğrulama başarısız `badMessages`, kalan işlemler ayarlar için çıkış `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="fc48d-153">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="fc48d-154">Bölünmüş değişim işlem kümeleri - olarak askıya alma değişim hatası: bölmelerini değişim hareket halinde ayarlar ve her işlem kümesi ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="fc48d-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="fc48d-155">Bir veya daha fazla işlem değişim ayarlarsa doğrulama, kod çözme eylem çıkarır tüm işlem ayarlar bu değişim X12 başarısız `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="fc48d-155">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="fc48d-156">Değişim korumak - işlem kümeleri askıya alma hatası: değişim korumak ve tüm toplu değişim işlem.</span><span class="sxs-lookup"><span data-stu-id="fc48d-156">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="fc48d-157">Kod çözme eylem çıkarır yalnızca bu işlem ayarlar X12 için doğrulama başarısız `badMessages`, kalan işlemler ayarlar için çıkış `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="fc48d-157">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="fc48d-158">Değişim korumak - değişim askıya alma hatası: değişim korumak ve tüm toplu değişim işlem.</span><span class="sxs-lookup"><span data-stu-id="fc48d-158">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="fc48d-159">Bir veya daha fazla işlem değişim ayarlarsa doğrulama, kod çözme eylem çıkarır tüm işlem ayarlar bu değişim X12 başarısız `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="fc48d-159">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span> 
* <span data-ttu-id="fc48d-160">Teknik ve/veya işlevsel bir bildirim (yapılandırılmışsa) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fc48d-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="fc48d-161">Teknik bir bildirim başlığı doğrulama sonucu olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fc48d-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="fc48d-162">Teknik Bildirim bir değişim üstbilgisi ve adresi alıcı tarafından toplamı işlenmesini durumunu raporlar.</span><span class="sxs-lookup"><span data-stu-id="fc48d-162">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver.</span></span>
  * <span data-ttu-id="fc48d-163">İşlev bildirim gövde doğrulama sonucu olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fc48d-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="fc48d-164">İşlev bildirim alınan belge işlerken bir hatayla karşılaştı her hata raporları</span><span class="sxs-lookup"><span data-stu-id="fc48d-164">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="fc48d-165">Swagger görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="fc48d-165">View the swagger</span></span>
<span data-ttu-id="fc48d-166">Bkz: [ayrıntıları swagger](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="fc48d-166">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fc48d-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fc48d-167">Next steps</span></span>
[<span data-ttu-id="fc48d-168">Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="fc48d-168">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

