---
title: "aaaSchema güncelleştirmeleri Haziran-1-2016 - Azure Logic Apps | Microsoft Docs"
description: "Şema sürümü 2016-06-01 Azure Logic Apps için JSON tanımları oluşturma"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: b0347fbbd692a93b63a2f8b741402a225450b35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="37b0e-103">Şema güncelleştirmeleri Azure Logic Apps için - 1 Haziran 2016</span><span class="sxs-lookup"><span data-stu-id="37b0e-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="37b0e-104">Bu yeni şema ve API sürümü Azure mantıksal uygulamaları için daha fazla mantıksal uygulamalar olun anahtar iyileştirmeler içerir güvenilir ve kolay toouse:</span><span class="sxs-lookup"><span data-stu-id="37b0e-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

* <span data-ttu-id="37b0e-105">[Kapsamları](#scopes) grup veya eylemler Eylemler koleksiyonu olarak iç içe sağlar.</span><span class="sxs-lookup"><span data-stu-id="37b0e-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="37b0e-106">[Koşullar ve döngüler](#conditions-loops) birinci sınıf Eylemler sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="37b0e-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="37b0e-107">Eylemler ile Merhaba çalıştırmak için daha kesin sıralama `runAfter` özelliğini değiştirme`dependsOn`</span><span class="sxs-lookup"><span data-stu-id="37b0e-107">More precise ordering for running actions with hello `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="37b0e-108">mantıksal uygulamalarınızı hello 1 Ağustos 2015 tooupgrade Önizleme şema toohello 1 Haziran 2016 şema [hello yükseltme bölümü denetleyin](##upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="37b0e-108">tooupgrade your logic apps from hello August 1, 2015 preview schema toohello June 1, 2016 schema, [check out hello upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="37b0e-109">Kapsamları</span><span class="sxs-lookup"><span data-stu-id="37b0e-109">Scopes</span></span>

<span data-ttu-id="37b0e-110">Bu şemayı Grup eylem birlikte veya iç içe Eylemler birbirine içinde izin kapsamları içerir.</span><span class="sxs-lookup"><span data-stu-id="37b0e-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="37b0e-111">Örneğin, bir koşul başka bir koşul içerebilir.</span><span class="sxs-lookup"><span data-stu-id="37b0e-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="37b0e-112">Daha fazla bilgi edinmek [kapsam sözdizimi](../logic-apps/logic-apps-loops-and-scopes.md), ya da bu temel kapsam örnek gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="37b0e-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="37b0e-113">Koşullar ve döngüler değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="37b0e-113">Conditions and loops changes</span></span>

<span data-ttu-id="37b0e-114">Önceki şemada, tek bir eylemle ilişkili parametreler sürümleri, koşulları ve döngüleri yoktu.</span><span class="sxs-lookup"><span data-stu-id="37b0e-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="37b0e-115">Koşullar ve döngüler şimdi eylem türleri olarak görünmesi için bu sınırlama, bu şemayı kaldırır.</span><span class="sxs-lookup"><span data-stu-id="37b0e-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="37b0e-116">Daha fazla bilgi edinmek [döngüler ve kapsamları](../logic-apps/logic-apps-loops-and-scopes.md), veya bir koşul eylemi temel bu örneğin gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="37b0e-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a><span data-ttu-id="37b0e-117">'runAfter' özelliği</span><span class="sxs-lookup"><span data-stu-id="37b0e-117">'runAfter' property</span></span>

<span data-ttu-id="37b0e-118">Merhaba `runAfter` özelliğini değiştirir `dependsOn`, Eylemler için Çalıştır hello sırası belirttiğinizde daha yüksek duyarlılık önceki Eylemler hello durumlarına dayalı sağlanması.</span><span class="sxs-lookup"><span data-stu-id="37b0e-118">hello `runAfter` property replaces `dependsOn`, providing more precision when you specify hello run order for actions based on hello status of previous actions.</span></span>

<span data-ttu-id="37b0e-119">Merhaba `dependsOn` özelliği "Merhaba eylem çalıştırıldığı ve başarılı olup ile" eşanlamlı, kaç kez olsun, hello önceki eylemi başarılı olup üzerinde temel tooexecute bir eylem başarısız oldu veya atlandı istedik.</span><span class="sxs-lookup"><span data-stu-id="37b0e-119">hello `dependsOn` property was synonymous with "hello action ran and was successful", no matter how many times you wanted tooexecute an action, based on whether hello previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="37b0e-120">Merhaba `runAfter` özelliği, tüm hello sonra hello nesne çalıştığı eylem adları belirten bir nesne olarak bu esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="37b0e-120">hello `runAfter` property provides that flexibility as an object that specifies all hello action names after which hello object runs.</span></span> <span data-ttu-id="37b0e-121">Bu özellik ayrıca bir dizi Tetikleyicileri kabul edilebilir durumları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="37b0e-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="37b0e-122">Adım A başarılı ve ayrıca sonraki adım B başarılı veya başarısız sonra toorun istediyseniz, örneğin, size bu oluşturmak `runAfter` özelliği:</span><span class="sxs-lookup"><span data-stu-id="37b0e-122">For example, if you wanted toorun after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="37b0e-123">Şemanızı yükseltme</span><span class="sxs-lookup"><span data-stu-id="37b0e-123">Upgrade your schema</span></span>

<span data-ttu-id="37b0e-124">Toohello yükseltme yeni şema yalnızca birkaç adım alır.</span><span class="sxs-lookup"><span data-stu-id="37b0e-124">Upgrading toohello new schema only takes a few steps.</span></span> <span data-ttu-id="37b0e-125">Merhaba yükseltme işlemi hello yükseltme komut dosyası çalıştırarak içeren yeni bir mantıksal uygulama kaydetme ve isterseniz, büyük olasılıkla hello önceki mantıksal uygulama üzerine.</span><span class="sxs-lookup"><span data-stu-id="37b0e-125">hello upgrade process includes running hello upgrade script, saving as a new logic app, and if you want, possibly overwriting hello previous logic app.</span></span>

1. <span data-ttu-id="37b0e-126">Hello Azure portal'de, mantıksal uygulamanızı açın.</span><span class="sxs-lookup"><span data-stu-id="37b0e-126">In hello Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="37b0e-127">Çok Git**genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="37b0e-127">Go too**Overview**.</span></span> <span data-ttu-id="37b0e-128">Merhaba mantığı uygulama araç çubuğunda seçin **Şemayı Güncelleştir**.</span><span class="sxs-lookup"><span data-stu-id="37b0e-128">On hello logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Şemayı Güncelleştir'i seçin][1]
   
    <span data-ttu-id="37b0e-130">Merhaba yükseltilmiş tanımı, kopyalamak ve gerekirse, bir kaynak tanımı yapıştırma döndürülür.</span><span class="sxs-lookup"><span data-stu-id="37b0e-130">hello upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="37b0e-131">Ancak, biz **tavsiye** seçtiğiniz **Kaydet** toomake tüm bağlantı başvuruları hello geçerli olduğundan emin yükseltilmiş mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="37b0e-131">However, we **strongly recommend** you choose **Save As** toomake sure that all connection references are valid in hello upgraded logic app.</span></span>

3. <span data-ttu-id="37b0e-132">Merhaba yükseltme dikey araç çubuğunda seçin **Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="37b0e-132">In hello upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="37b0e-133">Merhaba mantığı adını ve durumunu girin.</span><span class="sxs-lookup"><span data-stu-id="37b0e-133">Enter hello logic name and status.</span></span> <span data-ttu-id="37b0e-134">toodeploy yükseltilmiş mantıksal uygulamanızı seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="37b0e-134">toodeploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="37b0e-135">Yükseltilen mantıksal uygulamanızı beklendiği gibi çalıştığını onaylayın.</span><span class="sxs-lookup"><span data-stu-id="37b0e-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="37b0e-136">El ile veya istek tetikleyicisi kullanıyorsanız, yeni mantıksal uygulamanızı hello geri çağırma URL'si değiştirir.</span><span class="sxs-lookup"><span data-stu-id="37b0e-136">If you are using a manual or request trigger, hello callback URL changes in your new logic app.</span></span> <span data-ttu-id="37b0e-137">Test hello yeni URL toomake emin hello uçtan uca deneyimi çalışır.</span><span class="sxs-lookup"><span data-stu-id="37b0e-137">Test hello new URL toomake sure hello end-to-end experience works.</span></span> <span data-ttu-id="37b0e-138">toopreserve önceki URL'ler, var olan mantıksal uygulamanızı kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37b0e-138">toopreserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="37b0e-139">*İsteğe bağlı* toooverwrite hello yeni şema sürüm ile hello araç, önceki mantıksal uygulamanızı seçin **kopya**, sonraki çok**Şemayı Güncelleştir**.</span><span class="sxs-lookup"><span data-stu-id="37b0e-139">*Optional* toooverwrite your previous logic app with hello new schema version, on hello toolbar, choose **Clone**, next too**Update Schema**.</span></span> <span data-ttu-id="37b0e-140">Bu adım yalnızca istiyorsanız tookeep hello aynı kaynak kimliği veya istek tetikleyici URL'si mantıksal uygulamanızı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="37b0e-140">This step is necessary only if you want tookeep hello same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="37b0e-141">Yükseltme Aracı notları</span><span class="sxs-lookup"><span data-stu-id="37b0e-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="37b0e-142">Eşleme koşulları</span><span class="sxs-lookup"><span data-stu-id="37b0e-142">Mapping conditions</span></span>

<span data-ttu-id="37b0e-143">Yükseltme hello tanımında true ve false şube Eylemler birlikte gruplandırma kapsamı olarak en iyi çaba hello araç haline getirir.</span><span class="sxs-lookup"><span data-stu-id="37b0e-143">In hello upgraded definition, hello tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="37b0e-144">Özellikle, hello Tasarımcı desenini `@equals(actions('a').status, 'Skipped')` olarak görünmesi gereken bir `else` eylem.</span><span class="sxs-lookup"><span data-stu-id="37b0e-144">Specifically, hello designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="37b0e-145">Ancak, Hello aracı tanınmayan desenleri algılarsa, hello aracı hello true ve false şube hello için ayrı koşullar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37b0e-145">However, if hello tool detects unrecognizable patterns, hello tool might create separate conditions for both hello true and hello false branch.</span></span> <span data-ttu-id="37b0e-146">Gerekirse, yükseltme işleminin ardından, Eylemler eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37b0e-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="37b0e-147">'foreach' döngü koşuluna sahip</span><span class="sxs-lookup"><span data-stu-id="37b0e-147">'foreach' loop with condition</span></span>

<span data-ttu-id="37b0e-148">Hello yeni şemada hello filtre eylemi tooreplicate hello desenini kullanabileceğiniz bir `foreach` döngü her öğe, bir koşul ile ancak yükseltme yaptığınızda bu değişiklik otomatik olarak gerçekleştirilmesi.</span><span class="sxs-lookup"><span data-stu-id="37b0e-148">In hello new schema, you can use hello filter action tooreplicate hello pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="37b0e-149">Merhaba koşul hello foreach döngüsü hello koşulu ile eşleşen öğe yalnızca bir dizi döndürmek için önce bir filtre eylemi olur ve bu diziyi hello foreach eyleme geçirilir.</span><span class="sxs-lookup"><span data-stu-id="37b0e-149">hello condition becomes a filter action before hello foreach loop for returning only an array of items that match hello condition, and that array is passed into hello foreach action.</span></span> <span data-ttu-id="37b0e-150">Bir örnek için bkz: [döngüler ve kapsamları](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="37b0e-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="37b0e-151">Kaynak etiketleri</span><span class="sxs-lookup"><span data-stu-id="37b0e-151">Resource tags</span></span>

<span data-ttu-id="37b0e-152">Yükseltmeden sonra yükseltme hello iş akışı için sıfırlamanız gerekir böylece kaynak etiketleri kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="37b0e-152">After you upgrade, resource tags are removed, so you must reset them for hello upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="37b0e-153">Diğer değişiklikler</span><span class="sxs-lookup"><span data-stu-id="37b0e-153">Other changes</span></span>

### <a name="renamed-manual-trigger-toorequest-trigger"></a><span data-ttu-id="37b0e-154">'Manual' tetikleyici too'request yeniden adlandırılmış ' tetikleyici</span><span class="sxs-lookup"><span data-stu-id="37b0e-154">Renamed 'manual' trigger too'request' trigger</span></span>

<span data-ttu-id="37b0e-155">Merhaba `manual` tetikleyici türü kullanım ve çok yeniden adlandırılmış`request` türüyle `http`.</span><span class="sxs-lookup"><span data-stu-id="37b0e-155">hello `manual` trigger type was deprecated and renamed too`request` with type `http`.</span></span> <span data-ttu-id="37b0e-156">Tetikleyici hello düzeni Hello tür kullanılan toobuild için bu değişiklik, daha fazla tutarlılık oluşturur.</span><span class="sxs-lookup"><span data-stu-id="37b0e-156">This change creates more consistency for hello kind of pattern that hello trigger is used toobuild.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="37b0e-157">Yeni 'filtre' eylemi</span><span class="sxs-lookup"><span data-stu-id="37b0e-157">New 'filter' action</span></span>

<span data-ttu-id="37b0e-158">toofilter tooa küçük hello yeni öğeler kümesi aşağı uzun bir diziye `filter` türü bir dizi ve koşulu kabul eder, her öğe için hello koşulu değerlendirir ve hello koşul toplantı öğelerle bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="37b0e-158">toofilter a large array down tooa smaller set of items, hello new `filter` type accepts an array and a condition, evaluates hello condition for each item, and returns an array with items meeting hello condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="37b0e-159">'Foreach' ve 'kadar' Eylemler kısıtlamalar</span><span class="sxs-lookup"><span data-stu-id="37b0e-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="37b0e-160">Merhaba `foreach` ve `until` döngü kısıtlı tooa tek eylem şunlardır.</span><span class="sxs-lookup"><span data-stu-id="37b0e-160">hello `foreach` and `until` loop are restricted tooa single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="37b0e-161">Eylemler için yeni 'trackedProperties'</span><span class="sxs-lookup"><span data-stu-id="37b0e-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="37b0e-162">Eylemler şimdi adlı bir ek özellik sahip `trackedProperties`, eşdüzey toohello olduğu `runAfter` ve `type` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="37b0e-162">Actions can now have an additional property called `trackedProperties`, which is sibling toohello `runAfter` and `type` properties.</span></span> <span data-ttu-id="37b0e-163">Bu nesne belirli eylem girişleri belirtir veya iş akışının bir parçası gösterilen hello Azure tanılama telemetri tooinclude istediğiniz çıkarır.</span><span class="sxs-lookup"><span data-stu-id="37b0e-163">This object specifies certain action inputs or outputs that you want tooinclude in hello Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="37b0e-164">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="37b0e-164">For example:</span></span>

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="37b0e-165">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="37b0e-165">Next Steps</span></span>
* [<span data-ttu-id="37b0e-166">Logic apps için iş akışı tanımları oluşturma</span><span class="sxs-lookup"><span data-stu-id="37b0e-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="37b0e-167">Mantıksal uygulamalar için dağıtım şablonlar oluşturma</span><span class="sxs-lookup"><span data-stu-id="37b0e-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
