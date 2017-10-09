---
title: aaaDecode X12 iletileri - Azure Logic Apps | Microsoft Docs
description: "EDI doğrulamak ve onayları hello X12 ileti kod çözücü ile Azure Logic Apps için hello Kurumsal tümleştirme paketi oluştur"
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
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="e27bc-103">X12 kod çözme hello Kurumsal tümleştirme paketi ile Azure Logic Apps için iletileri</span><span class="sxs-lookup"><span data-stu-id="e27bc-103">Decode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="e27bc-104">Hello kod çözme X12 ileti bağlayıcısıyla, hello Zarf ticari ortak sözleşmesi karşı doğrulamak, EDI ve iş ortağı özgü özellikler doğrulamak, işlemleri kümeleri içine etkileşimler bölme veya tüm etkileşimler korumak ve Oluştur işlenen işlemler için bildirimler.</span><span class="sxs-lookup"><span data-stu-id="e27bc-104">With hello Decode X12 message connector, you can validate hello envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="e27bc-105">toouse bu bağlayıcı mantıksal uygulamanızı tetikleyici varolan hello bağlayıcı tooan eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e27bc-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e27bc-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e27bc-106">Before you start</span></span>

<span data-ttu-id="e27bc-107">Gereksinim duyduğunuz hello öğeleri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e27bc-107">Here's hello items you need:</span></span>

* <span data-ttu-id="e27bc-108">Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="e27bc-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="e27bc-109">Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="e27bc-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="e27bc-110">Bir tümleştirme hesap toouse hello kod çözme X12 ileti Bağlayıcısı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e27bc-110">You must have an integration account toouse hello Decode X12 message connector.</span></span>
* <span data-ttu-id="e27bc-111">En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış</span><span class="sxs-lookup"><span data-stu-id="e27bc-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="e27bc-112">Bir [X12 sözleşmesi](logic-apps-enterprise-integration-x12.md) tümleştirme hesabınızda tanımlanan zaten</span><span class="sxs-lookup"><span data-stu-id="e27bc-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="e27bc-113">X12 kod çözme iletileri</span><span class="sxs-lookup"><span data-stu-id="e27bc-113">Decode X12 messages</span></span>

1. <span data-ttu-id="e27bc-114">[Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e27bc-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="e27bc-115">bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz hello kod çözme X12 ileti bağlayıcı tetikleyiciler, sahip değil.</span><span class="sxs-lookup"><span data-stu-id="e27bc-115">hello Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="e27bc-116">Hello mantığı Uygulama Tasarımcısı, tetikleyici ekleyin ve sonra bir eylem tooyour mantıksal uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e27bc-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="e27bc-117">Merhaba arama kutusuna "x12" filtreniz için girin.</span><span class="sxs-lookup"><span data-stu-id="e27bc-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="e27bc-118">Seçin **X12-X12 kod çözme ileti**.</span><span class="sxs-lookup"><span data-stu-id="e27bc-118">Select **X12 - Decode X12 message**.</span></span>
   
    !["X12" için arama](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="e27bc-120">Tooyour tümleştirme hesabını daha önce herhangi bir bağlantısı oluşturmadıysanız, istenir toocreate şimdi bu bağlantı.</span><span class="sxs-lookup"><span data-stu-id="e27bc-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="e27bc-121">Bağlantınızı adlandırın ve hello tümleştirme hesabı tooconnect istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e27bc-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 

    ![Hesap bağlantı ayrıntıları tümleştirme sağlar](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="e27bc-123">Bir yıldız işareti özelliklerle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e27bc-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="e27bc-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="e27bc-124">Property</span></span> | <span data-ttu-id="e27bc-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="e27bc-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="e27bc-126">Bağlantı adı *</span><span class="sxs-lookup"><span data-stu-id="e27bc-126">Connection Name *</span></span> |<span data-ttu-id="e27bc-127">Bağlantınız için herhangi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="e27bc-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="e27bc-128">Tümleştirme hesabını *</span><span class="sxs-lookup"><span data-stu-id="e27bc-128">Integration Account *</span></span> |<span data-ttu-id="e27bc-129">Tümleştirme hesabınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="e27bc-129">Enter a name for your integration account.</span></span> <span data-ttu-id="e27bc-130">Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun aynı Azure konumu.</span><span class="sxs-lookup"><span data-stu-id="e27bc-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="e27bc-131">İşiniz bittiğinde, bağlantı ayrıntılarınızı benzer toothis örnek görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="e27bc-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="e27bc-132">bağlantı oluşturma toofinish seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e27bc-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![Tümleştirme hesap bağlantı ayrıntıları](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="e27bc-134">Bu örnekte gösterildiği gibi bağlantınızı oluşturulduktan sonra hello X12 düz dosya ileti toodecode seçin.</span><span class="sxs-lookup"><span data-stu-id="e27bc-134">After your connection is created, as shown in this example, select hello X12 flat file message toodecode.</span></span>

    ![oluşturulan tümleştirme hesap bağlantı](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="e27bc-136">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e27bc-136">For example:</span></span>

    ![Kod çözme için dosya iletisi SELECT X12 düz](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="e27bc-138">X12 kod çözme ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="e27bc-138">X12 Decode details</span></span>

<span data-ttu-id="e27bc-139">Merhaba X12 kod çözme connector, şu görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="e27bc-139">hello X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="e27bc-140">Ticari ortak sözleşmesi karşı hello Zarf doğrular</span><span class="sxs-lookup"><span data-stu-id="e27bc-140">Validates hello envelope against trading partner agreement</span></span>
* <span data-ttu-id="e27bc-141">EDI ve iş ortağı özgü özellikleri doğrular</span><span class="sxs-lookup"><span data-stu-id="e27bc-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="e27bc-142">EDI yapısal doğrulama ve genişletilmiş şema doğrulaması</span><span class="sxs-lookup"><span data-stu-id="e27bc-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="e27bc-143">Merhaba değişim Zarf hello yapısını doğrulama.</span><span class="sxs-lookup"><span data-stu-id="e27bc-143">Validation of hello structure of hello interchange envelope.</span></span>
  * <span data-ttu-id="e27bc-144">Merhaba zarfının hello denetim şemasına karşılık şema doğrulamasını.</span><span class="sxs-lookup"><span data-stu-id="e27bc-144">Schema validation of hello envelope against hello control schema.</span></span>
  * <span data-ttu-id="e27bc-145">Merhaba işlem kümesi veri öğeleri hello ileti şemasına karşılık şema doğrulamasını.</span><span class="sxs-lookup"><span data-stu-id="e27bc-145">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="e27bc-146">İşlem kümesi veri öğelerinde EDI doğrulamanın</span><span class="sxs-lookup"><span data-stu-id="e27bc-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="e27bc-147">Merhaba Değişim, Grup ve işlem kümesi denetim numaraları çoğaltmaları olmadığını doğrular</span><span class="sxs-lookup"><span data-stu-id="e27bc-147">Verifies that hello interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="e27bc-148">Merhaba değiş tokuş denetim numarası önceden alınmış etkileşimler karşı denetler.</span><span class="sxs-lookup"><span data-stu-id="e27bc-148">Checks hello interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="e27bc-149">Merhaba Grup denetim numarası hello değişim diğer Grup denetimi numaraları karşı denetler.</span><span class="sxs-lookup"><span data-stu-id="e27bc-149">Checks hello group control number against other group control numbers in hello interchange.</span></span>
  * <span data-ttu-id="e27bc-150">Bu gruptaki diğer işlem kümesi denetim numaraları karşı kontrol numarası Hello işlem ayarlamak denetler.</span><span class="sxs-lookup"><span data-stu-id="e27bc-150">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="e27bc-151">İşlem kümeleri içine Hello değişim böler veya hello tüm değişim korur:</span><span class="sxs-lookup"><span data-stu-id="e27bc-151">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="e27bc-152">Bölünmüş değişim işlem kümeleri - olarak askıya alma işlem kümeleri hatası: bölmelerini değişim hareket halinde ayarlar ve her işlem kümesi ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="e27bc-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="e27bc-153">Merhaba X12 kod çözme eylem çıkarır doğrulama çok başarısız işlem kümeleri`badMessages`ve işlemler kalan hello ayarlar çok çıkaran`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="e27bc-153">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="e27bc-154">Bölünmüş değişim işlem kümeleri - olarak askıya alma değişim hatası: bölmelerini değişim hareket halinde ayarlar ve her işlem kümesi ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="e27bc-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="e27bc-155">Bir veya daha fazla işlem hello değişim başarısız doğrulama ayarlarsa, tüm hello hareket ayarlar bu değişim çok hello X12 kod çözme eylem çıkarır`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="e27bc-155">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="e27bc-156">Değişim korumak - işlem kümeleri askıya alma hatası: Preserve hello değişim ve işlem hello tüm toplu değişim.</span><span class="sxs-lookup"><span data-stu-id="e27bc-156">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="e27bc-157">Merhaba X12 kod çözme eylem çıkarır doğrulama çok başarısız işlem kümeleri`badMessages`ve işlemler kalan hello ayarlar çok çıkaran`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="e27bc-157">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="e27bc-158">Değişim korumak - değişim askıya alma hatası: Preserve hello değişim ve işlem hello tüm toplu değişim.</span><span class="sxs-lookup"><span data-stu-id="e27bc-158">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="e27bc-159">Bir veya daha fazla işlem hello değişim başarısız doğrulama ayarlarsa, tüm hello hareket ayarlar bu değişim çok hello X12 kod çözme eylem çıkarır`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="e27bc-159">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span> 
* <span data-ttu-id="e27bc-160">Teknik ve/veya işlevsel bir bildirim (yapılandırılmışsa) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e27bc-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="e27bc-161">Teknik bir bildirim başlığı doğrulama sonucu olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e27bc-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="e27bc-162">Merhaba Teknik Bildirim hello bir değişim üstbilgi ve toplamı hello adresi alıcı tarafından işlenmesini hello durumunu raporlar.</span><span class="sxs-lookup"><span data-stu-id="e27bc-162">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver.</span></span>
  * <span data-ttu-id="e27bc-163">İşlev bildirim gövde doğrulama sonucu olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e27bc-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="e27bc-164">Merhaba işlevsel bildirim belge hello işleme alınan karşılaştı her hata raporları</span><span class="sxs-lookup"><span data-stu-id="e27bc-164">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="e27bc-165">Görünüm hello swagger</span><span class="sxs-lookup"><span data-stu-id="e27bc-165">View hello swagger</span></span>
<span data-ttu-id="e27bc-166">Merhaba bkz [ayrıntıları swagger](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="e27bc-166">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e27bc-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e27bc-167">Next steps</span></span>
[<span data-ttu-id="e27bc-168">Merhaba Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="e27bc-168">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

