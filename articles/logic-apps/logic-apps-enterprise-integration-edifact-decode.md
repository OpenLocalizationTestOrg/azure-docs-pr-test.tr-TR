---
title: "EDIFACT iletileri - Azure Logic Apps kod çözme | Microsoft Docs"
description: "EDI doğrulamak ve onayları EDIFACT ileti kod çözücü ile Azure Logic Apps için Kurumsal tümleştirme paketi oluştur"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e3787b48037360bf6066ddce2bacba6842213b2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="4538d-103">EDIFACT iletileri Kurumsal tümleştirme paketi ile Azure mantıksal uygulamaları için kod çözme</span><span class="sxs-lookup"><span data-stu-id="4538d-103">Decode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="4538d-104">Kod çözme EDIFACT ileti bağlayıcısıyla EDI ve iş ortağı özgü özellikleri doğrulayın, işlemleri kümeleri içine etkileşimler bölme veya tüm etkileşimler korumak ve işlenen işlemler için ilgili kaynaklar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4538d-104">With the Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="4538d-105">Bu bağlayıcıyı kullanmak için bağlayıcıyı mantıksal uygulamanızı varolan bir tetikleyicinin eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4538d-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="4538d-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="4538d-106">Before you start</span></span>

<span data-ttu-id="4538d-107">Gereksinim duyduğunuz öğeleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="4538d-107">Here's the items you need:</span></span>

* <span data-ttu-id="4538d-108">Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="4538d-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="4538d-109">Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="4538d-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="4538d-110">Kod çözme EDIFACT ileti bağlayıcıyı kullanmak üzere bir tümleştirme hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4538d-110">You must have an integration account to use the Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="4538d-111">En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış</span><span class="sxs-lookup"><span data-stu-id="4538d-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="4538d-112">Bir [EDIFACT sözleşmesi](logic-apps-enterprise-integration-edifact.md) tümleştirme hesabınızda tanımlanan zaten</span><span class="sxs-lookup"><span data-stu-id="4538d-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="4538d-113">EDIFACT iletileri kod çözme</span><span class="sxs-lookup"><span data-stu-id="4538d-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="4538d-114">[Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4538d-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="4538d-115">Bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz kod çözme EDIFACT ileti bağlayıcı tetikleyiciler, sahip değil.</span><span class="sxs-lookup"><span data-stu-id="4538d-115">The Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="4538d-116">Mantıksal Uygulama Tasarımcısı'nda bir tetikleyici ekleyin ve ardından bir eylem mantıksal uygulamanızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4538d-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3. <span data-ttu-id="4538d-117">Arama kutusuna "EDIFACT", filtre olarak girin.</span><span class="sxs-lookup"><span data-stu-id="4538d-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="4538d-118">Seçin **EDIFACT ileti kod çözme**.</span><span class="sxs-lookup"><span data-stu-id="4538d-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![EDIFACT arama](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="4538d-120">Tümleştirme hesabınıza daha önce herhangi bir bağlantısı oluşturmadıysanız, bu bağlantı artık oluşturmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="4538d-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="4538d-121">Bağlantınızı adlandırın ve bağlamak istediğiniz tümleştirme hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="4538d-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![Tümleştirme hesabı oluşturma](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="4538d-123">Bir yıldız işareti özelliklerle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4538d-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="4538d-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="4538d-124">Property</span></span> | <span data-ttu-id="4538d-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="4538d-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="4538d-126">Bağlantı adı *</span><span class="sxs-lookup"><span data-stu-id="4538d-126">Connection Name *</span></span> |<span data-ttu-id="4538d-127">Bağlantınız için herhangi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="4538d-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="4538d-128">Tümleştirme hesabını *</span><span class="sxs-lookup"><span data-stu-id="4538d-128">Integration Account *</span></span> |<span data-ttu-id="4538d-129">Tümleştirme hesabınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="4538d-129">Enter a name for your integration account.</span></span> <span data-ttu-id="4538d-130">Tümleştirme hesabı ve mantığı uygulamanız aynı Azure konumuna olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4538d-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

4. <span data-ttu-id="4538d-131">İşiniz bittiğinde bağlantınızı oluşturmayı tamamlamak için seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4538d-131">When you're done to finish creating your connection, choose **Create**.</span></span> <span data-ttu-id="4538d-132">Bağlantı ayrıntıları bu örneğe benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="4538d-132">Your connection details should look similar to this example:</span></span>

    ![Tümleştirme hesap ayrıntıları](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="4538d-134">Bu örnekte gösterildiği gibi bağlantınızı oluşturulduktan sonra çözecek EDIFACT düz dosya iletiyi seçin.</span><span class="sxs-lookup"><span data-stu-id="4538d-134">After your connection is created, as shown in this example, select the EDIFACT flat file message to decode.</span></span>

    ![oluşturulan tümleştirme hesap bağlantı](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="4538d-136">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4538d-136">For example:</span></span>

    ![Kod çözme için EDIFACT düz dosya iletiyi seçin](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="4538d-138">EDIFACT kod çözücü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="4538d-138">EDIFACT decoder details</span></span>

<span data-ttu-id="4538d-139">Kod çözme EDIFACT connector, şu görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="4538d-139">The Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="4538d-140">Zarf ticari ortak sözleşmesi karşı doğrular.</span><span class="sxs-lookup"><span data-stu-id="4538d-140">Validates the envelope against trading partner agreement.</span></span>
* <span data-ttu-id="4538d-141">Anlaşmayı gönderen Niteleyici Tanımlayıcısı ve alıcı niteleyicisi & tanımlayıcı eşleştirerek çözümler.</span><span class="sxs-lookup"><span data-stu-id="4538d-141">Resolves the agreement by matching the sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="4538d-142">Değişim ayarlarını yapılandırmayı alacağını birden fazla işlem anlaşmasına göre ait olduğunda bir değişim birden çok işlem halinde ayırır.</span><span class="sxs-lookup"><span data-stu-id="4538d-142">Splits an interchange into multiple transactions when the interchange has more than one transaction based on the agreement's receive settings configuration.</span></span>
* <span data-ttu-id="4538d-143">Değişim ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="4538d-143">Disassembles the interchange.</span></span>
* <span data-ttu-id="4538d-144">EDI ve iş ortağı özgü özellikler de dahil olmak üzere doğrular:</span><span class="sxs-lookup"><span data-stu-id="4538d-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="4538d-145">Doğrulama değişim Zarf yapısı</span><span class="sxs-lookup"><span data-stu-id="4538d-145">Validation of the interchange envelope structure</span></span>
  * <span data-ttu-id="4538d-146">Zarf denetim şemasına karşılık şema doğrulaması</span><span class="sxs-lookup"><span data-stu-id="4538d-146">Schema validation of the envelope against the control schema</span></span>
  * <span data-ttu-id="4538d-147">Şema doğrulama ileti şemayla işlem kümesi veri öğelerinin</span><span class="sxs-lookup"><span data-stu-id="4538d-147">Schema validation of the transaction-set data elements against the message schema</span></span>
  * <span data-ttu-id="4538d-148">İşlem kümesi veri öğelerinde EDI doğrulamanın</span><span class="sxs-lookup"><span data-stu-id="4538d-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="4538d-149">Değişim, Grup ve işlem kümesi denetim numaraları (yapılandırılmışsa) tekrarı olmayan olduğunu doğrular</span><span class="sxs-lookup"><span data-stu-id="4538d-149">Verifies that the interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="4538d-150">Değişim kontrol numarası önceden alınmış etkileşimler karşı denetler.</span><span class="sxs-lookup"><span data-stu-id="4538d-150">Checks the interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="4538d-151">Grup denetim numarası değişim diğer Grup denetimi numaraları karşı denetler.</span><span class="sxs-lookup"><span data-stu-id="4538d-151">Checks the group control number against other group control numbers in the interchange.</span></span> 
  * <span data-ttu-id="4538d-152">Bu gruptaki diğer işlem kümesi denetim numaraları karşı işlem kümesi denetim numarası denetler.</span><span class="sxs-lookup"><span data-stu-id="4538d-152">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="4538d-153">İşlem kümeleri içine değişim böler veya tüm değişim korur:</span><span class="sxs-lookup"><span data-stu-id="4538d-153">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="4538d-154">Bölünmüş değişim işlem kümeleri - olarak askıya alma işlem kümeleri hatası: bölmelerini değişim hareket halinde ayarlar ve her işlem kümesi ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="4538d-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="4538d-155">Kod çözme eylem çıkarır yalnızca bu işlem ayarlar X12 için doğrulama başarısız `badMessages`, kalan işlemler ayarlar için çıkış `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="4538d-155">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="4538d-156">Bölünmüş değişim işlem kümeleri - olarak askıya alma değişim hatası: bölmelerini değişim hareket halinde ayarlar ve her işlem kümesi ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="4538d-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="4538d-157">Bir veya daha fazla işlem değişim ayarlarsa doğrulama, kod çözme eylem çıkarır tüm işlem ayarlar bu değişim X12 başarısız `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="4538d-157">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="4538d-158">Değişim korumak - işlem kümeleri askıya alma hatası: değişim korumak ve tüm toplu değişim işlem.</span><span class="sxs-lookup"><span data-stu-id="4538d-158">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="4538d-159">Kod çözme eylem çıkarır yalnızca bu işlem ayarlar X12 için doğrulama başarısız `badMessages`, kalan işlemler ayarlar için çıkış `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="4538d-159">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="4538d-160">Değişim korumak - değişim askıya alma hatası: değişim korumak ve tüm toplu değişim işlem.</span><span class="sxs-lookup"><span data-stu-id="4538d-160">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="4538d-161">Bir veya daha fazla işlem değişim ayarlarsa doğrulama, kod çözme eylem çıkarır tüm işlem ayarlar bu değişim X12 başarısız `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="4538d-161">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
* <span data-ttu-id="4538d-162">Teknik (Denetim) ve/veya işlev bildirim (yapılandırılmışsa) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4538d-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="4538d-163">Teknik bir bildirim veya CONTRL ACK tam alınan değişim söz dizimi kontrol sonuçlarını raporlar.</span><span class="sxs-lookup"><span data-stu-id="4538d-163">A Technical Acknowledgment or the CONTRL ACK reports the results of a syntactical check of the complete received interchange.</span></span>
  * <span data-ttu-id="4538d-164">İşlev bildirimi kabul ettikten kabul edin veya alınan Değişim veya bir grup Reddet</span><span class="sxs-lookup"><span data-stu-id="4538d-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="4538d-165">Görünüm Swagger dosyası</span><span class="sxs-lookup"><span data-stu-id="4538d-165">View Swagger file</span></span>
<span data-ttu-id="4538d-166">EDIFACT bağlayıcı Swagger ayrıntılarını görüntülemek için bkz: [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="4538d-166">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4538d-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4538d-167">Next steps</span></span>
[<span data-ttu-id="4538d-168">Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="4538d-168">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

