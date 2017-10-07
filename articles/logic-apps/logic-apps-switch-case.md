---
title: "Azure Logic Apps farklı eylemler için aaaSwitch bildirimi | Microsoft Docs"
description: "Switch deyimi kullanarak ifade değerlerine göre logic apps farklı eylemler tooperform seçin"
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
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="d6ecc-104">Logic apps ile switch deyimi içinde farklı eylemler gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="d6ecc-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="d6ecc-105">Bir iş akışı yazma, genellikle nesne veya ifade hello değere göre tootake farklı eylemler vardır.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-105">When authoring a workflow, you often have tootake different actions based on hello value of an object or expression.</span></span> <span data-ttu-id="d6ecc-106">Örneğin, farklı bir HTTP isteği durum kodu hello göre logic app toobehave ya da bir e-posta içinde seçili bir seçenek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-106">For example, you might want your logic app toobehave differently based on hello status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="d6ecc-107">Switch deyimi tooimplement bu senaryoları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-107">You can use a switch statement tooimplement these scenarios.</span></span> <span data-ttu-id="d6ecc-108">Mantıksal uygulamanızı bir belirteç veya ifade değerlendirin ve hello hello durumuyla seçin aynı değeri tooexecute hello belirtilen eylemler.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-108">Your logic app can evaluate a token or expression, and choose hello case with hello same value tooexecute hello specified actions.</span></span> <span data-ttu-id="d6ecc-109">Yalnızca bir örnek hello switch deyimi eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-109">Only one case should match hello switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="d6ecc-110">Tüm programlama dilleri gibi switch deyimleri yalnızca eşitlik işleçleri destekler.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="d6ecc-111">Diğer ilişkisel işleçleri gerekirse "büyüktür gibi", bir koşul deyimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="d6ecc-112">tooensure belirleyici yürütme davranışını durumlarda dinamik belirteçleri veya ifade yerine benzersiz ve statik bir değer içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-112">tooensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6ecc-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d6ecc-113">Prerequisites</span></span>

- <span data-ttu-id="d6ecc-114">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-114">An active Azure subscription.</span></span> <span data-ttu-id="d6ecc-115">Etkin bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/), veya deneyin [Logic Apps için ücretsiz](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d6ecc-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="d6ecc-116">Mantıksal uygulamalar hakkındaki temel bilgileri</span><span class="sxs-lookup"><span data-stu-id="d6ecc-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a><span data-ttu-id="d6ecc-117">Switch deyimi tooyour iş akışını Ekle</span><span class="sxs-lookup"><span data-stu-id="d6ecc-117">Add a switch statement tooyour workflow</span></span>

<span data-ttu-id="d6ecc-118">switch deyimi nasıl çalıştığını tooshow, bu örnek izleyiciler dosyaları tooDropbox karşıya bir mantıksal uygulama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-118">tooshow how a switch statement works, this example creates a logic app that monitors files uploaded tooDropbox.</span></span> <span data-ttu-id="d6ecc-119">Merhaba yeni dosyaları karşıya zaman hello mantıksal uygulama seçen e-posta tooan onaylayan gönderir olup olmadığını tootransfer bu dosyaları tooSharePoint.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-119">When hello new files are uploaded, hello logic app sends email tooan approver who chooses whether tootransfer those files tooSharePoint.</span></span> <span data-ttu-id="d6ecc-120">Merhaba uygulama onaylayan seçer hello hello değere göre farklı eylemler gerçekleştiren bir anahtar deyimi kullanır.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-120">hello app uses a switch statement that performs different actions based on hello value that hello approver selects.</span></span>

1. <span data-ttu-id="d6ecc-121">Bir mantıksal uygulama oluşturun ve bu Tetikleyici seçin: **bir dosya oluşturulduğunda, Dropbox -**.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Bir dosya tetikleyici oluşturulduğunda, Dropbox - kullanın](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="d6ecc-123">Bu eylemin Hello tetikleyici altında ekleyin: **Outlook.com - onay e-postası gönderme**</span><span class="sxs-lookup"><span data-stu-id="d6ecc-123">Under hello trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="d6ecc-124">Logic apps ayrıca bir Office 365 Outlook hesaptan gönderme onay e-posta senaryoları destekler.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="d6ecc-125">Varolan bir bağlantıyı yoksa istenir toocreate biri.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-125">If you don't have an existing connection, you're prompted toocreate one.</span></span>
   - <span data-ttu-id="d6ecc-126">Merhaba gerekli alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-126">Fill in hello required fields.</span></span> <span data-ttu-id="d6ecc-127">Örneğin, altında **için**, hello onaylayan e-posta göndermek için hello e-posta adresi belirtin.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-127">For example, under **To**, specify hello email address for sending hello approver email.</span></span>
   - <span data-ttu-id="d6ecc-128">Altında **kullanıcı seçenekleri**, girin `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Bağlantıyı yapılandırın](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="d6ecc-130">Switch deyimi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-130">Add a switch statement.</span></span>

   - <span data-ttu-id="d6ecc-131">Seçin **+ yeni adım** > **... Daha fazla** > **anahtar durumu ekleme**.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="d6ecc-132">Merhaba üzerinde temel tooselect hello eylem tooperform istiyoruz artık `SelectedOptions` hello çıktı *onay e-posta Gönder* eylem.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-132">Now we want tooselect hello action tooperform based on hello `SelectedOptions` output from hello *Send approval email* action.</span></span> 
   <span data-ttu-id="d6ecc-133">Bu alan hello bulabilirsiniz **dinamik içerik eklemek** Seçici.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-133">You can find this field in hello **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="d6ecc-134">Kullanım *durum 1* hello onaylayan seçtiğinde toohandle `Approve`.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-134">Use *Case 1* toohandle when hello approver selects `Approve`.</span></span>
     - <span data-ttu-id="d6ecc-135">Onaylanırsa, çevrimiçi hello ile Merhaba özgün dosya tooSharePoint kopyalama [ **SharePoint Online - dosyası oluşturma** eylem](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="d6ecc-135">If approved, copy hello original file tooSharePoint Online with hello [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="d6ecc-136">Yeni bir dosya SharePoint üzerinde kullanılabilir olduğunu hello servis talebi toonotify kullanıcılar başka bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-136">Add another action within hello case toonotify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="d6ecc-137">Kullanıcı seçtiğinde başka bir örneği toohandle eklemek `Reject`.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-137">Add another case toohandle when user selects `Reject`.</span></span>
     - <span data-ttu-id="d6ecc-138">Reddedilirse, diğer onaylayanlar hello dosya reddedilir ve başka bir eylem gerekli değildir bildiren bir bildirim e-postası gönderin.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-138">If rejected, send a notification email informing other approvers that hello file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="d6ecc-139">`SelectedOptions`Biz hello bırakabilirsiniz için yalnızca iki seçenek sunar **varsayılan** durum boş.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-139">`SelectedOptions` provides only two options, so we can leave hello **Default** case empty.</span></span>

   ![Switch deyimi](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="d6ecc-141">Switch deyimi toplama toohello varsayılan durumda en az bir örnek gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-141">A switch statement needs at least one case in addition toohello default case.</span></span>

4. <span data-ttu-id="d6ecc-142">Bu eylem ekleyerek hello özgün dosya karşıya tooDropbox Hello switch deyimi sonra silin: **Dropbox - dosya silinemiyor**</span><span class="sxs-lookup"><span data-stu-id="d6ecc-142">After hello switch statement, delete hello original file uploaded tooDropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="d6ecc-143">Mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-143">Save your logic app.</span></span> <span data-ttu-id="d6ecc-144">Bir dosya tooDropbox karşıya yükleyerek uygulamanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-144">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="d6ecc-145">Kısa süre içinde bir onay e-posta alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="d6ecc-146">Bir seçenek belirleyin ve hello davranışı uyun.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-146">Select an option, and observe hello behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="d6ecc-147">Nasıl çok denetleyin[mantıksal uygulamalarınızı izleme](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d6ecc-147">Check out how too[monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-hello-code-behind-switch-statements"></a><span data-ttu-id="d6ecc-148">Switch deyimleri arkasındaki Hello kodu anlama</span><span class="sxs-lookup"><span data-stu-id="d6ecc-148">Understand hello code behind switch statements</span></span>

<span data-ttu-id="d6ecc-149">Switch deyimi kullanarak bir mantıksal uygulama başarıyla oluşturuldu, hello kod tanımı hello switch deyimi arkasında bakalım.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-149">Now that you successfully created a logic app using a switch statement, let's look at hello code definition behind hello switch statement.</span></span>

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

* <span data-ttu-id="d6ecc-150">`"Switch"`Okunabilirlik için yeniden adlandırabilirsiniz hello switch deyimi Hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-150">`"Switch"` is hello name of hello switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="d6ecc-151">`"type": "Switch"`Merhaba eylem switch deyimi olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-151">`"type": "Switch"` indicates that hello action is a switch statement.</span></span> 
* <span data-ttu-id="d6ecc-152">`"expression"`Bu örnekte Hello onaylayanın seçili seçenektir ve daha sonra hello tanımında bildirilen her durumda karşı değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-152">`"expression"` is hello approver's selected option in this example and is evaluated against each case declared later in hello definition.</span></span> 
* <span data-ttu-id="d6ecc-153">`"cases"`herhangi bir sayıda durumları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="d6ecc-154">Her bir olay `"Case *"` okunabilirlik için yeniden adlandırabilirsiniz hello durumunun hello varsayılan addır.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-154">For each case, `"Case *"` is hello default name of hello case, which you can rename for readability.</span></span> 
<span data-ttu-id="d6ecc-155">`"case"`anahtar ifadesi karşılaştırma kullanımları hello ve sabit ve benzersiz bir değer olmalıdır hello servis talebi etiket belirtir.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-155">`"case"` specifies hello case label, which hello switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="d6ecc-156">Merhaba durumlarda hiçbiri hello anahtar ifadesi, Eylemler altında eşleşiyorsa `"default"` yürütülür.</span><span class="sxs-lookup"><span data-stu-id="d6ecc-156">If none of hello cases match hello switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="d6ecc-157">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="d6ecc-157">Get help</span></span>

<span data-ttu-id="d6ecc-158">tooask sorular, soruları ve diğer Azure mantıksal uygulamaları kullanıcıların gittiğini, bkz: ziyaret hello [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="d6ecc-158">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="d6ecc-159">toohelp Azure mantıksal uygulamaları ve bağlayıcıların geliştirmek, oy veya hello fikir gönderme [Azure Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="d6ecc-159">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6ecc-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d6ecc-160">Next steps</span></span>

- <span data-ttu-id="d6ecc-161">Nasıl çok öğrenin[koşulları ekleme](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="d6ecc-161">Learn how too[add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="d6ecc-162">Hakkında bilgi edinin [hata ve özel durum işleme](logic-apps-exception-handling.md)</span><span class="sxs-lookup"><span data-stu-id="d6ecc-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="d6ecc-163">Daha fazla araştırmak [iş akışı dil özellikleri](logic-apps-author-definitions.md)</span><span class="sxs-lookup"><span data-stu-id="d6ecc-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>