---
title: "Azure Logic Apps ile Azure işlevleri için aaaCustom kod | Microsoft Docs"
description: "Oluşturma ve Azure Logic Apps ile Azure işlevleri için özel kod çalıştırma"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a>Ekleme ve logic apps için özel kod aracılığıyla Azure işlevleri çalıştırın

C# veya node.js logic apps içinde toorun özel parçacıkları, Azure işlevleri aracılığıyla özel işlevler oluşturabilirsiniz. 
[Azure işlevleri](../azure-functions/functions-overview.md) server ücretsiz Microsoft Azure ve bu görevleri gerçekleştirmek için yararlı olan bilgi işlem sunar:

* Gelişmiş Biçimlendirme veya logic apps alanların işlem
* Bir iş akışında hesaplamalar.
* C# veya node.js desteklenen işlevlere sahip Hello mantığı uygulama işlevini genişletme

## <a name="create-custom-functions-for-your-logic-apps"></a>Logic apps için özel işlevler oluştur

Bir işlev hello de hello Azure işlevleri portalından oluşturmanızı öneririz **Genel Web kancası - düğüm** veya **Genel Web kancası - C#** şablonları. Merhaba sonucu oluşturur otomatik doldurulan bir kabul eden bir şablonu `application/json` mantığı uygulamasından. Bu şablondan Oluştur işlevleri otomatik olarak algılanır ve hello mantığı Uygulama Tasarımcısı altında görünür **my bölgede Azure işlevleri.**

Merhaba hello üzerinde Azure portal'ın **tümleştir** bölmesini işlevinizi için şablonunuzu göstermek, **modu** çok ayarlamak**Web kancası** ve **Web kancası türü** çok ayarlanır**genel JSON**. 

Web kancası işlevleri bir isteğini kabul edin ve hello yöntemiyle uygulamasına geçirmek bir `data` değişkeni. Gibi noktalı gösterim kullanılarak yükünüzü hello özelliklerini erişebilirsiniz `data.function-name`. Örneğin, bir tarih saat değeri bir tarih dizeye dönüştürür basit bir JavaScript işlevi aşağıdaki örneğine hello gibi görünür:

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a>Mantığı uygulamalardan Azure işlevlerini çağırma

Aboneliğiniz ve mantığı Uygulama Tasarımcısı'nda toocall istediğinizi seçin hello işlevi toolist Merhaba kapsayıcılara tıklatın hello **Eylemler** menü ve arasından seçim **my bölgede Azure işlevleri**.

Merhaba işlevi seçtikten sonra olduğunuz bir giriş yükü nesne toospecify istedi. Mantıksal uygulama gönderir toohello işlevi hello ve bir JSON nesnesi olmalıdır selamlama iletisine nesnesidir. Örneğin, hello toopass istiyorsanız **son değişiklik** tarih Salesforce tetikleyiciden hello işlevi yükü aşağıdaki örnekte olduğu gibi görünebilir:

![Son değiştirilme tarihi][1]

## <a name="trigger-logic-apps-from-a-function"></a>Bir işlevden tetikleyici mantıksal uygulamalar

Bir işlev içinde bir mantıksal uygulama tetikleyebilir. Bkz: [Logic apps aranabilir uç noktalar olarak](logic-apps-http-endpoint.md). El ile tetikleyicisine sahip bir mantıksal uygulama oluşturun, sonra bir HTTP POST toohello el ile tetikleyici URL'si toohello mantıksal uygulama gönderilen istediğiniz hello yükü ile işlevinizin oluşturmak.

### <a name="create-a-function-from-logic-app-designer"></a>Mantıksal Uygulama Tasarımcısı'ndan bir işlev oluşturun

Merhaba Tasarımcısı'ndan bir node.js Web kancası işlevi de oluşturabilirsiniz. İlk olarak seçin **Azure işlevleri my bölgede** ve işlevinizi için bir kapsayıcı seçin. Henüz bir kapsayıcınız yoksa, hello gelen toocreate gerek [Azure işlevleri portalına](https://functions.azure.com/signin). Ardından **Yeni Oluştur**.  

toogenerate toocompute, istediğiniz hello verilerine dayalı bir şablon bir işlevdeki toopass planlama hello bağlam nesnesi belirtin. Bu nesne bir JSON nesnesi olmalıdır. Örneğin, FTP eylemin hello dosya içeriğinde geçirirseniz, hello bağlam yükü aşağıdaki gibi görünür:

![Bağlam yükü][2]

> [!NOTE]
> Bu nesne bir dize olarak cast değildi çünkü hello içerik doğrudan toohello JSON yükü eklenir. Ancak, Hello nesne (diğer bir deyişle, bir dize veya bir JSON nesnesi/dizi) bir JSON belirteci değilse hata oluşur. toocast hello nesnesi bir dize olarak, bu makaledeki hello ilk çizimde gösterildiği gibi teklifleri ekleyin.
> 

Merhaba Tasarımcısı sonra satır içi oluşturabileceğiniz bir işlevi şablon oluşturur. Değişkenleri hello işlevdeki toopass plan hello bağlamını temel alınarak önceden oluşturulur.

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
