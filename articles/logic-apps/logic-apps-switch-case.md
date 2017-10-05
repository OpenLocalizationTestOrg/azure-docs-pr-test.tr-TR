---
title: "Azure Logic Apps içinde deyimi farklı eylemler için geçiş | Microsoft Docs"
description: "Switch deyimi kullanarak ifade değerlerine göre logic apps gerçekleştirmek için farklı eylemleri seçin"
services: logic-apps
keywords: Switch deyimi
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 338b6a5b549d7bf81186550295608438ac4aee32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="e670c-104">Logic apps ile switch deyimi içinde farklı eylemler gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="e670c-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="e670c-105">Bir iş akışı yazma, genellikle nesne veya ifade değere göre farklı eylemleri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e670c-105">When authoring a workflow, you often have to take different actions based on the value of an object or expression.</span></span> <span data-ttu-id="e670c-106">Örneğin, farklı bir HTTP isteğinin ya da bir e-posta içinde seçili bir seçenek durum kodunu göre davranmasına mantıksal uygulamanızı isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e670c-106">For example, you might want your logic app to behave differently based on the status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="e670c-107">Bu senaryolar uygulamak için bir anahtar ifadesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e670c-107">You can use a switch statement to implement these scenarios.</span></span> <span data-ttu-id="e670c-108">Mantıksal uygulamanızı bir belirteç veya ifade değerlendirin ve belirtilen eylemleri yürütmek için aynı değere sahip bir servis talebi seçin.</span><span class="sxs-lookup"><span data-stu-id="e670c-108">Your logic app can evaluate a token or expression, and choose the case with the same value to execute the specified actions.</span></span> <span data-ttu-id="e670c-109">Switch deyimi yalnızca bir örnek eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="e670c-109">Only one case should match the switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="e670c-110">Tüm programlama dilleri gibi switch deyimleri yalnızca eşitlik işleçleri destekler.</span><span class="sxs-lookup"><span data-stu-id="e670c-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="e670c-111">Diğer ilişkisel işleçleri gerekirse "büyüktür gibi", bir koşul deyimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="e670c-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="e670c-112">Belirleyici yürütme davranışı sağlamak için durumlarda dinamik belirteçleri veya ifade yerine benzersiz ve statik bir değer içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e670c-112">To ensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e670c-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e670c-113">Prerequisites</span></span>

- <span data-ttu-id="e670c-114">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="e670c-114">An active Azure subscription.</span></span> <span data-ttu-id="e670c-115">Etkin bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/), veya deneyin [Logic Apps için ücretsiz](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e670c-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="e670c-116">Mantıksal uygulamalar hakkındaki temel bilgileri</span><span class="sxs-lookup"><span data-stu-id="e670c-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-to-your-workflow"></a><span data-ttu-id="e670c-117">Switch deyimi akışınıza ekleme</span><span class="sxs-lookup"><span data-stu-id="e670c-117">Add a switch statement to your workflow</span></span>

<span data-ttu-id="e670c-118">Switch deyimi nasıl çalıştığını göstermek için bu örnek için Dropbox karşıya yüklenen dosyaların izler bir mantıksal uygulama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e670c-118">To show how a switch statement works, this example creates a logic app that monitors files uploaded to Dropbox.</span></span> <span data-ttu-id="e670c-119">Yeni dosyalar yüklenirken mantıksal uygulama aktarılmayacağını SharePoint'e bu dosyaları seçen onaylayıcı e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="e670c-119">When the new files are uploaded, the logic app sends email to an approver who chooses whether to transfer those files to SharePoint.</span></span> <span data-ttu-id="e670c-120">Uygulama onaylayan seçtiği değere göre farklı eylemler gerçekleştiren bir anahtar deyimi kullanır.</span><span class="sxs-lookup"><span data-stu-id="e670c-120">The app uses a switch statement that performs different actions based on the value that the approver selects.</span></span>

1. <span data-ttu-id="e670c-121">Bir mantıksal uygulama oluşturun ve bu Tetikleyici seçin: **bir dosya oluşturulduğunda, Dropbox -**.</span><span class="sxs-lookup"><span data-stu-id="e670c-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Bir dosya tetikleyici oluşturulduğunda, Dropbox - kullanın](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="e670c-123">Bu eylem tetikleyici altında ekleyin: **Outlook.com - onay e-postası gönderme**</span><span class="sxs-lookup"><span data-stu-id="e670c-123">Under the trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="e670c-124">Logic apps ayrıca bir Office 365 Outlook hesaptan gönderme onay e-posta senaryoları destekler.</span><span class="sxs-lookup"><span data-stu-id="e670c-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="e670c-125">Varolan bir bağlantıyı sahip değilseniz, birini oluşturmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="e670c-125">If you don't have an existing connection, you're prompted to create one.</span></span>
   - <span data-ttu-id="e670c-126">Gerekli alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="e670c-126">Fill in the required fields.</span></span> <span data-ttu-id="e670c-127">Örneğin, altında **için**, onaylayan e-posta göndermek için e-posta adresi belirtin.</span><span class="sxs-lookup"><span data-stu-id="e670c-127">For example, under **To**, specify the email address for sending the approver email.</span></span>
   - <span data-ttu-id="e670c-128">Altında **kullanıcı seçenekleri**, girin `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="e670c-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Bağlantıyı yapılandırın](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="e670c-130">Switch deyimi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e670c-130">Add a switch statement.</span></span>

   - <span data-ttu-id="e670c-131">Seçin **+ yeni adım** > **... Daha fazla** > **anahtar durumu ekleme**.</span><span class="sxs-lookup"><span data-stu-id="e670c-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="e670c-132">Gerçekleştirilecek eylemi seçin istiyoruz artık temel `SelectedOptions` çıktısı *onay e-posta Gönder* eylem.</span><span class="sxs-lookup"><span data-stu-id="e670c-132">Now we want to select the action to perform based on the `SelectedOptions` output from the *Send approval email* action.</span></span> 
   <span data-ttu-id="e670c-133">Bu alanda bulabileceğiniz **dinamik içerik eklemek** Seçici.</span><span class="sxs-lookup"><span data-stu-id="e670c-133">You can find this field in the **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="e670c-134">Kullanım *durum 1* onaylayan seçtiğinde işlemek için `Approve`.</span><span class="sxs-lookup"><span data-stu-id="e670c-134">Use *Case 1* to handle when the approver selects `Approve`.</span></span>
     - <span data-ttu-id="e670c-135">SharePoint Online ile onaylanırsa, özgün dosya kopyalama [ **SharePoint Online - dosyası oluşturma** eylem](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="e670c-135">If approved, copy the original file to SharePoint Online with the [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="e670c-136">Yeni bir dosya SharePoint üzerinde kullanılabilir olduğunu kullanıcılara bildirmek için durum içindeki başka bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e670c-136">Add another action within the case to notify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="e670c-137">Kullanıcı seçtiğinde işlemek için başka bir örneği eklemek `Reject`.</span><span class="sxs-lookup"><span data-stu-id="e670c-137">Add another case to handle when user selects `Reject`.</span></span>
     - <span data-ttu-id="e670c-138">Reddedilirse, diğer onaylayanlar dosya reddedilir ve başka bir eylem gerekli değildir bildiren bir bildirim e-postası gönderin.</span><span class="sxs-lookup"><span data-stu-id="e670c-138">If rejected, send a notification email informing other approvers that the file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="e670c-139">`SelectedOptions`Biz bırakabilirsiniz, bu nedenle yalnızca iki seçenek sunar **varsayılan** durum boş.</span><span class="sxs-lookup"><span data-stu-id="e670c-139">`SelectedOptions` provides only two options, so we can leave the **Default** case empty.</span></span>

   ![Switch deyimi](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="e670c-141">Switch deyimi varsayılan durumda yanı sıra en az bir örnek gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="e670c-141">A switch statement needs at least one case in addition to the default case.</span></span>

4. <span data-ttu-id="e670c-142">Switch deyimi sonra bu eylem ekleyerek Dropbox'a karşıya özgün dosyayı silmektir: **Dropbox - dosya silinemiyor**</span><span class="sxs-lookup"><span data-stu-id="e670c-142">After the switch statement, delete the original file uploaded to Dropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="e670c-143">Mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e670c-143">Save your logic app.</span></span> <span data-ttu-id="e670c-144">Dropbox için bir dosyayı karşıya yükleyerek uygulamanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e670c-144">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="e670c-145">Kısa süre içinde bir onay e-posta alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e670c-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="e670c-146">Bir seçenek belirleyin ve davranışı uyun.</span><span class="sxs-lookup"><span data-stu-id="e670c-146">Select an option, and observe the behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="e670c-147">Nasıl yapılır kullanıma [mantıksal uygulamalarınızı izleme](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="e670c-147">Check out how to [monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-the-code-behind-switch-statements"></a><span data-ttu-id="e670c-148">Switch deyimleri arka plan kodu anlama</span><span class="sxs-lookup"><span data-stu-id="e670c-148">Understand the code behind switch statements</span></span>

<span data-ttu-id="e670c-149">Switch deyimi kullanarak bir mantıksal uygulama başarıyla oluşturuldu, switch deyimi arkasındaki kod tanımı bakalım.</span><span class="sxs-lookup"><span data-stu-id="e670c-149">Now that you successfully created a logic app using a switch statement, let's look at the code definition behind the switch statement.</span></span>

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* <span data-ttu-id="e670c-150">`"Switch"`Okunabilirlik için yeniden adlandırabilirsiniz switch deyimi adıdır.</span><span class="sxs-lookup"><span data-stu-id="e670c-150">`"Switch"` is the name of the switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="e670c-151">`"type": "Switch"`Eylem switch deyimi olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="e670c-151">`"type": "Switch"` indicates that the action is a switch statement.</span></span> 
* <span data-ttu-id="e670c-152">`"expression"`Bu örnekte onaylayanın seçili seçenektir ve tanımı içinde bildirilen her durumda karşı değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="e670c-152">`"expression"` is the approver's selected option in this example and is evaluated against each case declared later in the definition.</span></span> 
* <span data-ttu-id="e670c-153">`"cases"`herhangi bir sayıda durumları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="e670c-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="e670c-154">Her bir olay `"Case *"` okunabilirlik için yeniden adlandırabilirsiniz durumunun varsayılan addır.</span><span class="sxs-lookup"><span data-stu-id="e670c-154">For each case, `"Case *"` is the default name of the case, which you can rename for readability.</span></span> 
<span data-ttu-id="e670c-155">`"case"`anahtar ifadesi karşılaştırma için kullanır, servis talebi etiketini belirtir ve sabit ve benzersiz bir değer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e670c-155">`"case"` specifies the case label, which the switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="e670c-156">Örneklerin hiçbiri anahtar ifadesi, Eylemler altında eşleşiyorsa `"default"` yürütülür.</span><span class="sxs-lookup"><span data-stu-id="e670c-156">If none of the cases match the switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="e670c-157">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="e670c-157">Get help</span></span>

<span data-ttu-id="e670c-158">Sorular sormak, soruları yanıtlamak ve diğer Azure Logic Apps kullanıcılarının neler yaptığını görmek için [Azure Logic Apps forumunu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="e670c-158">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="e670c-159">Azure Logic Apps ve bağlayıcıları geliştirmeye yardımcı olmak için, [Azure Logic Apps kullanıcı geri bildirim sitesinde](http://aka.ms/logicapps-wish) oy kullanın veya fikirlerinizi paylaşın.</span><span class="sxs-lookup"><span data-stu-id="e670c-159">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e670c-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e670c-160">Next steps</span></span>

- <span data-ttu-id="e670c-161">Bilgi edinmek için nasıl [koşulları ekleme](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="e670c-161">Learn how to [add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="e670c-162">Hakkında bilgi edinin [hata ve özel durum işleme](logic-apps-exception-handling.md)</span><span class="sxs-lookup"><span data-stu-id="e670c-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="e670c-163">Daha fazla araştırmak [iş akışı dil özellikleri](logic-apps-author-definitions.md)</span><span class="sxs-lookup"><span data-stu-id="e670c-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>