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
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a>Logic apps ile switch deyimi içinde farklı eylemler gerçekleştirme

Bir iş akışı yazma, genellikle nesne veya ifade hello değere göre tootake farklı eylemler vardır. Örneğin, farklı bir HTTP isteği durum kodu hello göre logic app toobehave ya da bir e-posta içinde seçili bir seçenek isteyebilirsiniz.

Switch deyimi tooimplement bu senaryoları kullanabilirsiniz. Mantıksal uygulamanızı bir belirteç veya ifade değerlendirin ve hello hello durumuyla seçin aynı değeri tooexecute hello belirtilen eylemler. Yalnızca bir örnek hello switch deyimi eşleşmelidir.

> [!TIP]
> Tüm programlama dilleri gibi switch deyimleri yalnızca eşitlik işleçleri destekler. Diğer ilişkisel işleçleri gerekirse "büyüktür gibi", bir koşul deyimi kullanın.
> tooensure belirleyici yürütme davranışını durumlarda dinamik belirteçleri veya ifade yerine benzersiz ve statik bir değer içermelidir.

## <a name="prerequisites"></a>Ön koşullar

- Etkin bir Azure aboneliği. Etkin bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/), veya deneyin [Logic Apps için ücretsiz](https://tryappservice.azure.com/).
- [Mantıksal uygulamalar hakkındaki temel bilgileri](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a>Switch deyimi tooyour iş akışını Ekle

switch deyimi nasıl çalıştığını tooshow, bu örnek izleyiciler dosyaları tooDropbox karşıya bir mantıksal uygulama oluşturur. Merhaba yeni dosyaları karşıya zaman hello mantıksal uygulama seçen e-posta tooan onaylayan gönderir olup olmadığını tootransfer bu dosyaları tooSharePoint. Merhaba uygulama onaylayan seçer hello hello değere göre farklı eylemler gerçekleştiren bir anahtar deyimi kullanır.

1. Bir mantıksal uygulama oluşturun ve bu Tetikleyici seçin: **bir dosya oluşturulduğunda, Dropbox -**.

   ![Bir dosya tetikleyici oluşturulduğunda, Dropbox - kullanın](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. Bu eylemin Hello tetikleyici altında ekleyin: **Outlook.com - onay e-postası gönderme**

   > [!TIP]
   > Logic apps ayrıca bir Office 365 Outlook hesaptan gönderme onay e-posta senaryoları destekler.

   - Varolan bir bağlantıyı yoksa istenir toocreate biri.
   - Merhaba gerekli alanları doldurun. Örneğin, altında **için**, hello onaylayan e-posta göndermek için hello e-posta adresi belirtin.
   - Altında **kullanıcı seçenekleri**, girin `Approve, Reject`.

   ![Bağlantıyı yapılandırın](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. Switch deyimi ekleyin.

   - Seçin **+ yeni adım** > **... Daha fazla** > **anahtar durumu ekleme**. 
   - Merhaba üzerinde temel tooselect hello eylem tooperform istiyoruz artık `SelectedOptions` hello çıktı *onay e-posta Gönder* eylem. 
   Bu alan hello bulabilirsiniz **dinamik içerik eklemek** Seçici.
   - Kullanım *durum 1* hello onaylayan seçtiğinde toohandle `Approve`.
     - Onaylanırsa, çevrimiçi hello ile Merhaba özgün dosya tooSharePoint kopyalama [ **SharePoint Online - dosyası oluşturma** eylem](../connectors/connectors-create-api-sharepointonline.md).
     - Yeni bir dosya SharePoint üzerinde kullanılabilir olduğunu hello servis talebi toonotify kullanıcılar başka bir eylem ekleyin.
   - Kullanıcı seçtiğinde başka bir örneği toohandle eklemek `Reject`.
     - Reddedilirse, diğer onaylayanlar hello dosya reddedilir ve başka bir eylem gerekli değildir bildiren bir bildirim e-postası gönderin.
   - `SelectedOptions`Biz hello bırakabilirsiniz için yalnızca iki seçenek sunar **varsayılan** durum boş.

   ![Switch deyimi](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > Switch deyimi toplama toohello varsayılan durumda en az bir örnek gerekiyor.

4. Bu eylem ekleyerek hello özgün dosya karşıya tooDropbox Hello switch deyimi sonra silin: **Dropbox - dosya silinemiyor**

5. Mantıksal uygulamanızı kaydedin. Bir dosya tooDropbox karşıya yükleyerek uygulamanızı test edin. Kısa süre içinde bir onay e-posta alacaksınız. Bir seçenek belirleyin ve hello davranışı uyun.

   > [!TIP]
   > Nasıl çok denetleyin[mantıksal uygulamalarınızı izleme](logic-apps-monitor-your-logic-apps.md).

## <a name="understand-hello-code-behind-switch-statements"></a>Switch deyimleri arkasındaki Hello kodu anlama

Switch deyimi kullanarak bir mantıksal uygulama başarıyla oluşturuldu, hello kod tanımı hello switch deyimi arkasında bakalım.

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

* `"Switch"`Okunabilirlik için yeniden adlandırabilirsiniz hello switch deyimi Hello adıdır. 
* `"type": "Switch"`Merhaba eylem switch deyimi olduğunu gösterir. 
* `"expression"`Bu örnekte Hello onaylayanın seçili seçenektir ve daha sonra hello tanımında bildirilen her durumda karşı değerlendirilir. 
* `"cases"`herhangi bir sayıda durumları içerebilir. Her bir olay `"Case *"` okunabilirlik için yeniden adlandırabilirsiniz hello durumunun hello varsayılan addır. 
`"case"`anahtar ifadesi karşılaştırma kullanımları hello ve sabit ve benzersiz bir değer olmalıdır hello servis talebi etiket belirtir. Merhaba durumlarda hiçbiri hello anahtar ifadesi, Eylemler altında eşleşiyorsa `"default"` yürütülür.

## <a name="get-help"></a>Yardım alın

tooask sorular, soruları ve diğer Azure mantıksal uygulamaları kullanıcıların gittiğini, bkz: ziyaret hello [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Azure mantıksal uygulamaları ve bağlayıcıların geliştirmek, oy veya hello fikir gönderme [Azure Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Sonraki adımlar

- Nasıl çok öğrenin[koşulları ekleme](logic-apps-use-logic-app-features.md)
- Hakkında bilgi edinin [hata ve özel durum işleme](logic-apps-exception-handling.md)
- Daha fazla araştırmak [iş akışı dil özellikleri](logic-apps-author-definitions.md)