---
title: aaaDecode EDIFACT iletileri - Azure Logic Apps | Microsoft Docs
description: "EDI doğrulamak ve onayları hello EDIFACT ileti kod çözücü ile Azure Logic Apps için hello Kurumsal tümleştirme paketi oluştur"
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
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="e03f2-103">EDIFACT iletileri Enterprise Integration Pack Merhaba ile Azure mantıksal uygulamaları için kod çözme</span><span class="sxs-lookup"><span data-stu-id="e03f2-103">Decode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="e03f2-104">Hello kod çözme EDIFACT ileti bağlayıcısıyla EDI ve iş ortağı özgü özellikleri doğrulayın, işlemleri kümeleri içine etkileşimler bölme veya tüm etkileşimler korumak ve işlenen işlemler için ilgili kaynaklar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e03f2-104">With hello Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="e03f2-105">toouse bu bağlayıcı mantıksal uygulamanızı tetikleyici varolan hello bağlayıcı tooan eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e03f2-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e03f2-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e03f2-106">Before you start</span></span>

<span data-ttu-id="e03f2-107">Gereksinim duyduğunuz hello öğeleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e03f2-107">Here's hello items you need:</span></span>

* <span data-ttu-id="e03f2-108">Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="e03f2-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="e03f2-109">Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="e03f2-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="e03f2-110">Bir tümleştirme hesap toouse hello kod çözme EDIFACT ileti Bağlayıcısı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e03f2-110">You must have an integration account toouse hello Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="e03f2-111">En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış</span><span class="sxs-lookup"><span data-stu-id="e03f2-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="e03f2-112">Bir [EDIFACT sözleşmesi](logic-apps-enterprise-integration-edifact.md) tümleştirme hesabınızda tanımlanan zaten</span><span class="sxs-lookup"><span data-stu-id="e03f2-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="e03f2-113">EDIFACT iletileri kod çözme</span><span class="sxs-lookup"><span data-stu-id="e03f2-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="e03f2-114">[Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e03f2-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="e03f2-115">bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz hello kod çözme EDIFACT ileti bağlayıcı tetikleyiciler, sahip değil.</span><span class="sxs-lookup"><span data-stu-id="e03f2-115">hello Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="e03f2-116">Hello mantığı Uygulama Tasarımcısı, tetikleyici ekleyin ve sonra bir eylem tooyour mantıksal uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e03f2-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3. <span data-ttu-id="e03f2-117">Merhaba arama kutusuna "EDIFACT", filtre olarak girin.</span><span class="sxs-lookup"><span data-stu-id="e03f2-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="e03f2-118">Seçin **EDIFACT ileti kod çözme**.</span><span class="sxs-lookup"><span data-stu-id="e03f2-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![EDIFACT arama](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="e03f2-120">Tooyour tümleştirme hesabını daha önce herhangi bir bağlantısı oluşturmadıysanız, istenir toocreate şimdi bu bağlantı.</span><span class="sxs-lookup"><span data-stu-id="e03f2-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="e03f2-121">Bağlantınızı adlandırın ve hello tümleştirme hesabı tooconnect istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e03f2-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![Tümleştirme hesabı oluşturma](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="e03f2-123">Bir yıldız işareti özelliklerle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e03f2-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="e03f2-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="e03f2-124">Property</span></span> | <span data-ttu-id="e03f2-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="e03f2-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="e03f2-126">Bağlantı adı *</span><span class="sxs-lookup"><span data-stu-id="e03f2-126">Connection Name *</span></span> |<span data-ttu-id="e03f2-127">Bağlantınız için herhangi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="e03f2-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="e03f2-128">Tümleştirme hesabını *</span><span class="sxs-lookup"><span data-stu-id="e03f2-128">Integration Account *</span></span> |<span data-ttu-id="e03f2-129">Tümleştirme hesabınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="e03f2-129">Enter a name for your integration account.</span></span> <span data-ttu-id="e03f2-130">Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun aynı Azure konumu.</span><span class="sxs-lookup"><span data-stu-id="e03f2-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

4. <span data-ttu-id="e03f2-131">Bağlantınızı oluşturma toofinish bittiğinde, seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e03f2-131">When you're done toofinish creating your connection, choose **Create**.</span></span> <span data-ttu-id="e03f2-132">Bağlantı ayrıntıları benzer toothis örnek gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="e03f2-132">Your connection details should look similar toothis example:</span></span>

    ![Tümleştirme hesap ayrıntıları](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="e03f2-134">Bu örnekte gösterildiği gibi bağlantınızı oluşturulduktan sonra hello EDIFACT düz dosya ileti toodecode seçin.</span><span class="sxs-lookup"><span data-stu-id="e03f2-134">After your connection is created, as shown in this example, select hello EDIFACT flat file message toodecode.</span></span>

    ![oluşturulan tümleştirme hesap bağlantı](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="e03f2-136">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e03f2-136">For example:</span></span>

    ![Kod çözme için EDIFACT düz dosya iletiyi seçin](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="e03f2-138">EDIFACT kod çözücü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="e03f2-138">EDIFACT decoder details</span></span>

<span data-ttu-id="e03f2-139">Merhaba kod çözme EDIFACT connector, şu görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="e03f2-139">hello Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="e03f2-140">Ticari ortak sözleşmesi karşı hello Zarf doğrular.</span><span class="sxs-lookup"><span data-stu-id="e03f2-140">Validates hello envelope against trading partner agreement.</span></span>
* <span data-ttu-id="e03f2-141">Merhaba sözleşmesi hello gönderen Niteleyici Tanımlayıcısı ve alıcı niteleyicisi & tanımlayıcı eşleştirerek çözümler.</span><span class="sxs-lookup"><span data-stu-id="e03f2-141">Resolves hello agreement by matching hello sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="e03f2-142">Merhaba değişim ayarlarını yapılandırmayı alacağını birden fazla işlem hello anlaşmasına göre ait olduğunda bir değişim birden çok işlem halinde ayırır.</span><span class="sxs-lookup"><span data-stu-id="e03f2-142">Splits an interchange into multiple transactions when hello interchange has more than one transaction based on hello agreement's receive settings configuration.</span></span>
* <span data-ttu-id="e03f2-143">Merhaba değişim ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="e03f2-143">Disassembles hello interchange.</span></span>
* <span data-ttu-id="e03f2-144">EDI ve iş ortağı özgü özellikler de dahil olmak üzere doğrular:</span><span class="sxs-lookup"><span data-stu-id="e03f2-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="e03f2-145">Doğrulama hello değişim Zarf yapısı</span><span class="sxs-lookup"><span data-stu-id="e03f2-145">Validation of hello interchange envelope structure</span></span>
  * <span data-ttu-id="e03f2-146">Merhaba zarfının hello denetim şemasına karşılık şema doğrulaması</span><span class="sxs-lookup"><span data-stu-id="e03f2-146">Schema validation of hello envelope against hello control schema</span></span>
  * <span data-ttu-id="e03f2-147">Hello işlem kümesi veri öğeleri hello ileti şemasına karşılık şema doğrulaması</span><span class="sxs-lookup"><span data-stu-id="e03f2-147">Schema validation of hello transaction-set data elements against hello message schema</span></span>
  * <span data-ttu-id="e03f2-148">İşlem kümesi veri öğelerinde EDI doğrulamanın</span><span class="sxs-lookup"><span data-stu-id="e03f2-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="e03f2-149">Merhaba Değişim, Grup ve işlem kümesi denetim numaraları (yapılandırılmışsa) tekrarı olmayan olduğunu doğrular</span><span class="sxs-lookup"><span data-stu-id="e03f2-149">Verifies that hello interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="e03f2-150">Merhaba değiş tokuş denetim numarası önceden alınmış etkileşimler karşı denetler.</span><span class="sxs-lookup"><span data-stu-id="e03f2-150">Checks hello interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="e03f2-151">Merhaba Grup denetim numarası hello değişim diğer Grup denetimi numaraları karşı denetler.</span><span class="sxs-lookup"><span data-stu-id="e03f2-151">Checks hello group control number against other group control numbers in hello interchange.</span></span> 
  * <span data-ttu-id="e03f2-152">Bu gruptaki diğer işlem kümesi denetim numaraları karşı kontrol numarası Hello işlem ayarlamak denetler.</span><span class="sxs-lookup"><span data-stu-id="e03f2-152">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="e03f2-153">İşlem kümeleri içine Hello değişim böler veya hello tüm değişim korur:</span><span class="sxs-lookup"><span data-stu-id="e03f2-153">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="e03f2-154">Bölünmüş değişim işlem kümeleri - olarak askıya alma işlem kümeleri hatası: bölmelerini değişim hareket halinde ayarlar ve her işlem kümesi ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="e03f2-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="e03f2-155">Merhaba X12 kod çözme eylem çıkarır doğrulama çok başarısız işlem kümeleri`badMessages`ve işlemler kalan hello ayarlar çok çıkaran`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="e03f2-155">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="e03f2-156">Bölünmüş değişim işlem kümeleri - olarak askıya alma değişim hatası: bölmelerini değişim hareket halinde ayarlar ve her işlem kümesi ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="e03f2-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="e03f2-157">Bir veya daha fazla işlem hello değişim başarısız doğrulama ayarlarsa, tüm hello hareket ayarlar bu değişim çok hello X12 kod çözme eylem çıkarır`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="e03f2-157">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="e03f2-158">Değişim korumak - işlem kümeleri askıya alma hatası: Preserve hello değişim ve işlem hello tüm toplu değişim.</span><span class="sxs-lookup"><span data-stu-id="e03f2-158">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="e03f2-159">Merhaba X12 kod çözme eylem çıkarır doğrulama çok başarısız işlem kümeleri`badMessages`ve işlemler kalan hello ayarlar çok çıkaran`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="e03f2-159">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="e03f2-160">Değişim korumak - değişim askıya alma hatası: Preserve hello değişim ve işlem hello tüm toplu değişim.</span><span class="sxs-lookup"><span data-stu-id="e03f2-160">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="e03f2-161">Bir veya daha fazla işlem hello değişim başarısız doğrulama ayarlarsa, tüm hello hareket ayarlar bu değişim çok hello X12 kod çözme eylem çıkarır`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="e03f2-161">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
* <span data-ttu-id="e03f2-162">Teknik (Denetim) ve/veya işlev bildirim (yapılandırılmışsa) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e03f2-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="e03f2-163">Bir teknik bildirim veya hello CONTRL ACK hello tam alınan değişim söz dizimi kontrol hello sonuçlarını raporlar.</span><span class="sxs-lookup"><span data-stu-id="e03f2-163">A Technical Acknowledgment or hello CONTRL ACK reports hello results of a syntactical check of hello complete received interchange.</span></span>
  * <span data-ttu-id="e03f2-164">İşlev bildirimi kabul ettikten kabul edin veya alınan Değişim veya bir grup Reddet</span><span class="sxs-lookup"><span data-stu-id="e03f2-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="e03f2-165">Görünüm Swagger dosyası</span><span class="sxs-lookup"><span data-stu-id="e03f2-165">View Swagger file</span></span>
<span data-ttu-id="e03f2-166">tooview hello Swagger hello EDIFACT bağlayıcı ayrıntılarını görmek [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="e03f2-166">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e03f2-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e03f2-167">Next steps</span></span>
[<span data-ttu-id="e03f2-168">Merhaba Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="e03f2-168">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

