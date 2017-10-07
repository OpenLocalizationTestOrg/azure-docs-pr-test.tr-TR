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
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a>Şema güncelleştirmeleri Azure Logic Apps için - 1 Haziran 2016

Bu yeni şema ve API sürümü Azure mantıksal uygulamaları için daha fazla mantıksal uygulamalar olun anahtar iyileştirmeler içerir güvenilir ve kolay toouse:

* [Kapsamları](#scopes) grup veya eylemler Eylemler koleksiyonu olarak iç içe sağlar.
* [Koşullar ve döngüler](#conditions-loops) birinci sınıf Eylemler sunulmuştur.
* Eylemler ile Merhaba çalıştırmak için daha kesin sıralama `runAfter` özelliğini değiştirme`dependsOn`

mantıksal uygulamalarınızı hello 1 Ağustos 2015 tooupgrade Önizleme şema toohello 1 Haziran 2016 şema [hello yükseltme bölümü denetleyin](##upgrade-your-schema).

<a name="scopes"></a>
## <a name="scopes"></a>Kapsamları

Bu şemayı Grup eylem birlikte veya iç içe Eylemler birbirine içinde izin kapsamları içerir. Örneğin, bir koşul başka bir koşul içerebilir. Daha fazla bilgi edinmek [kapsam sözdizimi](../logic-apps/logic-apps-loops-and-scopes.md), ya da bu temel kapsam örnek gözden geçirin:

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
## <a name="conditions-and-loops-changes"></a>Koşullar ve döngüler değişiklikleri

Önceki şemada, tek bir eylemle ilişkili parametreler sürümleri, koşulları ve döngüleri yoktu. Koşullar ve döngüler şimdi eylem türleri olarak görünmesi için bu sınırlama, bu şemayı kaldırır. Daha fazla bilgi edinmek [döngüler ve kapsamları](../logic-apps/logic-apps-loops-and-scopes.md), veya bir koşul eylemi temel bu örneğin gözden geçirin:

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
## <a name="runafter-property"></a>'runAfter' özelliği

Merhaba `runAfter` özelliğini değiştirir `dependsOn`, Eylemler için Çalıştır hello sırası belirttiğinizde daha yüksek duyarlılık önceki Eylemler hello durumlarına dayalı sağlanması.

Merhaba `dependsOn` özelliği "Merhaba eylem çalıştırıldığı ve başarılı olup ile" eşanlamlı, kaç kez olsun, hello önceki eylemi başarılı olup üzerinde temel tooexecute bir eylem başarısız oldu veya atlandı istedik. Merhaba `runAfter` özelliği, tüm hello sonra hello nesne çalıştığı eylem adları belirten bir nesne olarak bu esneklik sağlar. Bu özellik ayrıca bir dizi Tetikleyicileri kabul edilebilir durumları tanımlar. Adım A başarılı ve ayrıca sonraki adım B başarılı veya başarısız sonra toorun istediyseniz, örneğin, size bu oluşturmak `runAfter` özelliği:

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a>Şemanızı yükseltme

Toohello yükseltme yeni şema yalnızca birkaç adım alır. Merhaba yükseltme işlemi hello yükseltme komut dosyası çalıştırarak içeren yeni bir mantıksal uygulama kaydetme ve isterseniz, büyük olasılıkla hello önceki mantıksal uygulama üzerine.

1. Hello Azure portal'de, mantıksal uygulamanızı açın.

2. Çok Git**genel bakış**. Merhaba mantığı uygulama araç çubuğunda seçin **Şemayı Güncelleştir**.
   
    ![Şemayı Güncelleştir'i seçin][1]
   
    Merhaba yükseltilmiş tanımı, kopyalamak ve gerekirse, bir kaynak tanımı yapıştırma döndürülür. 
    Ancak, biz **tavsiye** seçtiğiniz **Kaydet** toomake tüm bağlantı başvuruları hello geçerli olduğundan emin yükseltilmiş mantıksal uygulama.

3. Merhaba yükseltme dikey araç çubuğunda seçin **Kaydet**.

4. Merhaba mantığı adını ve durumunu girin. toodeploy yükseltilmiş mantıksal uygulamanızı seçin **oluşturma**.

5. Yükseltilen mantıksal uygulamanızı beklendiği gibi çalıştığını onaylayın.
   
   > [!NOTE]
   > El ile veya istek tetikleyicisi kullanıyorsanız, yeni mantıksal uygulamanızı hello geri çağırma URL'si değiştirir. Test hello yeni URL toomake emin hello uçtan uca deneyimi çalışır. toopreserve önceki URL'ler, var olan mantıksal uygulamanızı kopyalayabilirsiniz.

6. *İsteğe bağlı* toooverwrite hello yeni şema sürüm ile hello araç, önceki mantıksal uygulamanızı seçin **kopya**, sonraki çok**Şemayı Güncelleştir**. Bu adım yalnızca istiyorsanız tookeep hello aynı kaynak kimliği veya istek tetikleyici URL'si mantıksal uygulamanızı gereklidir.

### <a name="upgrade-tool-notes"></a>Yükseltme Aracı notları

#### <a name="mapping-conditions"></a>Eşleme koşulları

Yükseltme hello tanımında true ve false şube Eylemler birlikte gruplandırma kapsamı olarak en iyi çaba hello araç haline getirir. Özellikle, hello Tasarımcı desenini `@equals(actions('a').status, 'Skipped')` olarak görünmesi gereken bir `else` eylem. Ancak, Hello aracı tanınmayan desenleri algılarsa, hello aracı hello true ve false şube hello için ayrı koşullar oluşturabilirsiniz. Gerekirse, yükseltme işleminin ardından, Eylemler eşleyebilirsiniz.

#### <a name="foreach-loop-with-condition"></a>'foreach' döngü koşuluna sahip

Hello yeni şemada hello filtre eylemi tooreplicate hello desenini kullanabileceğiniz bir `foreach` döngü her öğe, bir koşul ile ancak yükseltme yaptığınızda bu değişiklik otomatik olarak gerçekleştirilmesi. Merhaba koşul hello foreach döngüsü hello koşulu ile eşleşen öğe yalnızca bir dizi döndürmek için önce bir filtre eylemi olur ve bu diziyi hello foreach eyleme geçirilir. Bir örnek için bkz: [döngüler ve kapsamları](../logic-apps/logic-apps-loops-and-scopes.md).

#### <a name="resource-tags"></a>Kaynak etiketleri

Yükseltmeden sonra yükseltme hello iş akışı için sıfırlamanız gerekir böylece kaynak etiketleri kaldırılır.

## <a name="other-changes"></a>Diğer değişiklikler

### <a name="renamed-manual-trigger-toorequest-trigger"></a>'Manual' tetikleyici too'request yeniden adlandırılmış ' tetikleyici

Merhaba `manual` tetikleyici türü kullanım ve çok yeniden adlandırılmış`request` türüyle `http`. Tetikleyici hello düzeni Hello tür kullanılan toobuild için bu değişiklik, daha fazla tutarlılık oluşturur.

### <a name="new-filter-action"></a>Yeni 'filtre' eylemi

toofilter tooa küçük hello yeni öğeler kümesi aşağı uzun bir diziye `filter` türü bir dizi ve koşulu kabul eder, her öğe için hello koşulu değerlendirir ve hello koşul toplantı öğelerle bir dizi döndürür.

### <a name="restrictions-for-foreach-and-until-actions"></a>'Foreach' ve 'kadar' Eylemler kısıtlamalar

Merhaba `foreach` ve `until` döngü kısıtlı tooa tek eylem şunlardır.

### <a name="new-trackedproperties-for-actions"></a>Eylemler için yeni 'trackedProperties'

Eylemler şimdi adlı bir ek özellik sahip `trackedProperties`, eşdüzey toohello olduğu `runAfter` ve `type` özellikleri. Bu nesne belirli eylem girişleri belirtir veya iş akışının bir parçası gösterilen hello Azure tanılama telemetri tooinclude istediğiniz çıkarır. Örneğin:

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

## <a name="next-steps"></a>Sonraki Adımlar
* [Logic apps için iş akışı tanımları oluşturma](../logic-apps/logic-apps-author-definitions.md)
* [Mantıksal uygulamalar için dağıtım şablonlar oluşturma](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
