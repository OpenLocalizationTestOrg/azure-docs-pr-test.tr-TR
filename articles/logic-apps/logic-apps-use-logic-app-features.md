---
title: "aaaAdd koşulları ve iş akışları - Azure Logic Apps başlatın | Microsoft Docs"
description: "İş akışları Azure Logic Apps içinde koşullu mantık, Tetikleyiciler, Eylemler ve parametreleri ekleyerek çalışma şeklini denetler."
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a>Logic Apps özelliklerini kullanma

İçinde bir [önceki konu](../logic-apps/logic-apps-create-a-logic-app.md), ilk mantıksal uygulamanızı oluşturuldu. toocontrol mantığı uygulamanızın iş akışı için logic app toorun farklı yollarını belirtin ve nasıl çok veri dizileri, koleksiyonlar ve toplu işlem. Bu öğeleri mantığı uygulama akışınızda içerebilir:

* Koşullar ve [switch ifadeleri](../logic-apps/logic-apps-switch-case.md) belirli koşulların karşılanıp karşılanmadığını bağlı olarak farklı eylemler çalıştırmak mantıksal uygulamanızı sağlar.

* [Döngüler](../logic-apps/logic-apps-loops-and-scopes.md) adımları tekrar tekrar çalıştırmak mantıksal uygulamanızı sağlar. Kullandığınızda Örneğin, Eylemler bir dizi yineleyebilirsiniz bir **For_each** döngü. Ya da kullanırken bir koşul yerine getirilene kadar Eylemler yineleyebilirsiniz bir **kadar** döngü.

* [Kapsamları](../logic-apps/logic-apps-loops-and-scopes.md) let gruplandırma Eylemler dizisi birlikte, örneğin, tooimplement özel durum işleme.

* [Debatching](../logic-apps/logic-apps-loops-and-scopes.md) hello kullandığınızda bir dizi öğeleri için ayrı iş akışlarını başlatmak mantıksal uygulamanızı sağlar **SplitOn** komutu.

Bu konu, mantıksal uygulamanızı oluşturmaya yönelik diğer kavramları sunar:

* Görünüm tooedit var olan bir mantıksal uygulama kodu
* Bir iş akışı başlatma seçenekleri

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a>Koşullar: yalnızca bir koşul yerine getirdikten sonra adımları çalıştırın

toohave adımları yalnızca veri belirli ölçütleri karşıladığında Çalıştır mantıksal uygulamanızı belirli alanlar veya değerler karşı hello akışındaki verileri karşılaştıran bir koşulu ekleyebilirsiniz.

Örneğin, bir Web sitesinin RSS akışı gönderileri için çok fazla e-posta gönderen bir mantıksal uygulama olduğunu varsayalım. Yalnızca yeni hello duyurduğumuzda mantıksal uygulamanızı e-posta gönderir. böylece bir koşul tooa belirli kategori ait ekleyebilirsiniz.

1. Merhaba, [Azure portal](https://portal.azure.com), bulma ve mantığı Uygulama Tasarımcısı'nda mantıksal uygulamanızı açın.

2. İstediğiniz koşulu toohello iş akışı konum ekleyin. 

   Merhaba mantığı uygulama iş akışında, var olan adımları arasında tooadd hello koşul işaretçisini hello hello ok tooadd hello koşul istediğiniz. 
   Merhaba seçin **artı** (**+**), ardından **bir koşul eklemek**. Örneğin:

   ![Koşul toologic uygulama Ekle](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > Merhaba, geçerli iş akışınızı sonunda tooadd bir koşul istiyorsanız, mantıksal uygulamanızı toohello sonuna gidin ve seçin **+ yeni adım**.

3. Şimdi hello koşul tanımlayın. Merhaba kaynak alan tooevaluate, hello işlemi tooperform ve hello hedef değer veya alan istediğinizi belirtin. tooadd var olan alanları tooyour koşul hello seçin **Ekle dinamik içerik listesi**.

   Örneğin:

   ![Koşul temel modunda düzenleme](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   Merhaba tam koşul şöyledir:

   ![Tam koşul](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > kodda, toodefine hello koşulu seçin **Gelişmiş modda Düzenle**. Örneğin:
   > 
   > ![Kod koşulunda Düzenle](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. Altında **Evet IF** ve **IF Hayır**, hello koşula uyulup uyulmadığını dayalı hello adımları tooperform ekleyin.

   Örneğin:

   ![Evet ve hiçbir yol koşulu](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > Var olan eylemler hello sürükleyin **Evet IF** ve **IF Hayır** yolları.

5. İşiniz bittiğinde, mantıksal uygulamanızı kaydedin.

Şimdi yalnızca hello gönderileri koşulunuz karşıladığında e-postaları alın.

## <a name="repeat-actions-over-a-list-with-foreach"></a>Eylemler forEach ile bir liste üzerinden yineleme

Merhaba forEach döngüsü üzerinde bir dizi toorepeat bir eylem belirtir. Bir dizi değil hello akış başarısız olur. Örneğin, iletileri dizisini çıkarır action1 varsa ve her iletinin toosend istiyorsanız, eylemin hello özelliklerinde bu forEach deyimi içerebilir:`forEach : "@action('action1').outputs.messages"`

## <a name="edit-hello-code-definition-for-a-logic-app"></a>Bir mantıksal uygulama için Hello kodu tanımını düzenleme

Merhaba mantığı Uygulama Tasarımcısı sahip olsa da, bir mantıksal uygulama tanımlayan hello kodu doğrudan düzenleyebilirsiniz.

1. Merhaba komut çubuğunda seçin **kod görünümü**.

    Bir tam Düzenleyicisi'ni açar ve düzenlediğiniz hello tanımını gösterir.

    ![Kod Görünümü](media/logic-apps-use-logic-app-features/codeview.png)

    Merhaba Metin Düzenleyicisi'nde kopyalayın ve herhangi bir sayıda hello içinde eylemler yapıştırın aynı mantıksal uygulama ya da mantıksal uygulamalar arasında. 
    Ayrıca kolayca eklemenize veya tüm bölümleri hello tanımından kaldırın ve ayrıca tanımları başkalarıyla paylaşabilirsiniz.

2. Yaptığınız düzenlemeleri toosave seçin **kaydetmek**.

## <a name="parameters"></a>Parametreler

Bazı Logic Apps özellikleri yalnızca kod görünümünde, örneğin, parametreleri sağlanır. Parametreleri kolay tooreuse değerleri mantıksal uygulamanızı boyunca kolaylaştırır. Örneğin, çeşitli eylemler kullanmak istediğiniz bir e-posta adresi varsa, bu e-posta adresi parametre olarak tanımlamanız gerekir.

Büyük olasılıkla toochange çok olmayan değerler çekmek için iyi parametreleridir. Bunlar, özellikle farklı ortamlarda toooverride parametreleri gerektiğinde kullanışlıdır. ortamında, temel toooverride parametreleri nasıl görürüm toolearn [Yazar mantıksal uygulama tanımları](../logic-apps/logic-apps-author-definitions.md) ve [REST API belgeleri](https://docs.microsoft.com/rest/api/logic).

Bu örnekte gösterilir nasıl tooupdate var olan mantıksal uygulamanızı böylece hello sorgu dönem için parametreleri kullanabilirsiniz.

1. Kod Görünümü'nde hello bulur `parameters : {}` nesne ve ekleme bir `currentFeedUrl` nesnesi:

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. Toohello Git `When_a_feed-item_is_published` eylem, Bul hello `queries` bölümünde ve hello sorgu değerle değiştirin:`"feedUrl": "#@{parameters('currentFeedUrl')}"` 

    toojoin iki veya daha fazla dizeleri hello de kullanabilirsiniz `concat` işlevi. 
    Örneğin, `"@concat('#',parameters('currentFeedUrl'))"` works hello aynı hello yukarıdaki.

3.  İşiniz bittiğinde seçin **kaydetmek**. 

    Merhaba Web sitesinin RSS hello yoluyla farklı bir URL geçirerek akışı değiştirebileceğiniz artık `currentFeedURL` nesnesi.

Daha fazla bilgi edinmek [nasıl tooauthor mantıksal uygulama tanımları](../logic-apps/logic-apps-author-definitions.md).

## <a name="start-logic-app-workflows"></a>Mantıksal uygulama iş akışlarını başlatmak

Mantıksal uygulamanızı tanımlanan hello iş akışını başlatmak için farklı seçeneğiniz vardır. Her zaman bir iş akışı isteğe bağlı hello başlatabilirsiniz [Azure portal].

### <a name="recurrence-triggers"></a>Yineleme Tetikleyicileri

Bir yineleme tetikleyici, belirttiğiniz bir zaman aralığında çalışır. Koşullu mantık Hello tetikleyicisine sahip olduğunda hello tetikleyici hello iş akışı toorun gerekip gerekmediğini belirler. Tetikleyici hello iş akışı döndürerek çalışmalı gösteren bir `200` durum kodu. Merhaba tetikleyici döndürür Hello iş akışı toorun gerek yoktur, bir `202` durum kodu.

### <a name="callback-using-rest-apis"></a>REST API'lerini kullanarak geri çağırma

toostart bir iş akışı, bir mantıksal uygulama uç noktası Hizmetleri çağırabilirsiniz. Bu tür bir mantıksal uygulama isteğe bağlı, toostart seçin **Şimdi Çalıştır** hello komut çubuğunda. Bkz: [Tetikleyiciler olarak uygulama uç noktaları mantığı çağırarak iş akışlarını başlatmak](../logic-apps/logic-apps-http-endpoint.md). 

<!-- Shared links -->
[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a>Sonraki adımlar

* [Switch deyimleri](../logic-apps/logic-apps-switch-case.md) 
* [Döngüler, kapsamlar ve ayırma](../logic-apps/logic-apps-loops-and-scopes.md)
* [Mantıksal uygulama tanımları yazma](../logic-apps/logic-apps-author-definitions.md)