---
title: "aaaAzure Mobile Engagement Web SDK yükseltme yordamları | Microsoft Docs"
description: "en son güncelleştirmeler ve yordamlar hello Web SDK'sı için Azure Mobile Engagement için hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a20529b4-ec8d-4503-8ae9-09b5f0846d5b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: a2df65904c6b56584ce6588ed26a9b79f3aa27ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a>Azure Mobile Engagement Web SDK yükseltme yordamları
Web uygulamanıza hello Azure Mobile Engagement Web SDK önceki bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükselttiğinizde aşağıdaki tooconsider hello gerekir.

Merhaba Mobile Engagement Web SDK birden fazla sürümünü atladıysanız hello yükseltme işlemi sırasında birçok yordamı toocomplete gerekebilir. Örneğin, 1.4.0 geçirirseniz too1.6.0, ilk izleme hello yordamları tooupgrade 1.4.0 gelen too1.5.0. Ardından 1.5.0 hello yordamları tooupgrade izleyin too1.6.0.

Yükseltme, hangi sürümü hello dosya azure-engagement.js önceki sürümünü hello dosyasının en son sürümünü hello ile değiştirin.

## <a name="upgrade-from-121-too200"></a>1.2.1'den yükseltme too2.0.0
Bu bölümde, nasıl toomigrate Mobile Engagement Web SDK tümleştirmesi hello Capptain hizmetinden sunulan tooan Azure Mobile Engagement uygulaması Capptain SAS tarafından açıklanmaktadır. Önceki bir sürümden başvurun hello Capptain Web sitesi toofirst Lütfen geçiriyorsanız, too1.2.1 geçirmek ve hello yordamları uygulayın.

Merhaba Mobile Engagement Web SDK'ın bu sürümü Samsung akıllı TV, Opera TV, webOS veya hello ulaşma özelliği desteklemiyor.

> [!IMPORTANT]
> Capptain ve Azure Mobile Engagement olan değil hello aynı hizmet. Aşağıdaki yordamı hello yalnızca nasıl toomigrate hello istemci uygulamaları vurgular. Geçirme hello Mobile Engagement Web SDK hello uygulama verilerinizi bir Capptain server tooa Mobile Engagement Sunucusu'ndan geçişi yapılmaz.
> 
> 

### <a name="javascript-files"></a>JavaScript dosyaları
Değiştir hello dosya capptain-sdk.js hello ile azure engagement.js dosya ve komut dosyası içeri aktarmalar uygun şekilde güncelleştirilir.

### <a name="remove-capptain-reach"></a>Capptain Reach Kaldır
Merhaba Mobile Engagement Web SDK'ın bu sürümü hello ulaşma özelliği desteklemiyor. Uygulamanıza Capptain erişim'i bütünleştirdiyseniz tooremove gerekir.

Merhaba ulaşmak CSS alma sayfanızdan kaldırın ve hello ilgili .css dosyasını (capptain-reach.css, varsayılan olarak) silin.

Reach kaynakları aşağıdaki hello Sil: hello Kapat görüntü (capptain-close.png, varsayılan olarak) ve hello marka simgesi (capptain bildirim-simgesi, varsayılan olarak).

Uygulama bildirimlerinin Hello ulaşmak UI kaldırın. Merhaba varsayılan düzeni şöyle görünür:

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

Merhaba ulaşmak UI metin ve web duyuruları ve yoklamaları kaldırın. Merhaba varsayılan düzeni şöyle görünür:

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

Merhaba kaldırmak `reach` varsa, yapılandırmasından nesne. Şöyle görünür:

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

Tüm diğer ulaşma özelleştirme, kategorileri gibi kaldırın.

### <a name="remove-deprecated-apis"></a>Kullanım dışı API'leri Kaldır
Bazı Capptain API'lerden hello Mobile Engagement Web SDK'SININ kullanım dışı bırakılmıştır.

API izleyen tüm çağrıları toohello kaldırın: `agent.connect`, `agent.disconnect`, `agent.pause`, ve `agent.sendMessageToDevice`.

Geri aramalar Capptain yapılandırmasından aşağıdaki hello tüm örneklerini kaldırın: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, ve `onPushMessageReceived`.

### <a name="configuration"></a>Yapılandırma
Mobile Engagement bir bağlantı dizesi tooconfigure SDK tanımlayıcıları, örneğin, hello uygulama tanımlayıcısı kullanır.

Merhaba uygulama kimliği, bağlantı dizesi ile değiştirin. Merhaba SDK yapılandırma değişiklikleri için o hello genel nesne Not `capptain` çok`azureEngagement`.

Geçişten önce:

    window.capptain = {
      appId: ...,
      [...]
    };

Geçişten sonra:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

Merhaba bağlantı dizesi, uygulamanız için hello Azure Portal görüntülenir.

### <a name="javascript-apis"></a>JavaScript API'leri
Merhaba genel JavaScript nesne `window.capptain` adlandırıldı `window.azureEngagement` ancak hello kullanabilirsiniz `window.engagement` API çağrıları için diğer ad. Merhaba diğer toodefine hello SDK yapılandırma kullanamazsınız.

Örneğin, `capptain.deviceId` hale `engagement.deviceId`, `capptain.agent.startActivity` hale `engagement.agent.startActivity`ve benzeri.

