---
title: "aaaAzure Mobile Engagement Web SDK genel bakış | Microsoft Docs"
description: "en son güncelleştirmeler ve yordamlar hello Web SDK'sı için Azure Mobile Engagement için hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 5bbc2fda-0f3f-43d0-a73d-0f2c0f8dc25b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 10/18/2016
ms.author: piyushjo
ms.openlocfilehash: 9e60a232b5eb2c41c405041a88e09d7137563513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a>Azure Mobile Engagement Web SDK
Tüm hakkında ayrıntılı bilgi hello için buradan başlayın toointegrate Azure Mobile Engagement bir web uygulamasında. Toogive isterseniz kendi web uygulaması ile çalışmaya başlama önce bir try bkz bizim [15 dakikalık Öğreticisi](mobile-engagement-web-app-get-started.md).

## <a name="integration-procedures"></a>Tümleştirme yordamları
1. Bilgi [nasıl toointegrate Mobile Engagement web uygulamanızda](mobile-engagement-web-integrate-engagement.md).
2. Etiket planı uygulama için bilgi [nasıl toouse hello Mobile Engagement web uygulamanızda API etiketleme Gelişmiş](mobile-engagement-web-use-engagement-api.md).

## <a name="release-notes"></a>Sürüm notları
### <a name="202-10182016"></a>2.0.2 (10/18/2016)
* Özel (Safari) gözatma sabit kilitlenme.
* Sabit kilitlenme tarayıcılarında tanımlama bilgileri devre dışı ile.

Tüm sürümler için lütfen hello bakın [tamamlamak sürüm notları](mobile-engagement-web-release-notes.md).

## <a name="upgrade-procedures"></a>Yükseltme yordamları
### <a name="upgrade-from-121-too200"></a>1.2.1'den yükseltme too2.0.0
Merhaba aşağıdaki bölümlerde nasıl toomigrate Mobile Engagement Web SDK tümleştirmesi hello Capptain hizmetinden sunulan tooan Azure Mobile Engagement uygulaması Capptain SAS tarafından açıklanmaktadır. Geçiş daha önceki bir sürüm 1.2.1, daha Lütfen hello Capptain Web sitesi toomigrate too1.2.1 ilk bakın ve hello yordamları uygulayın.

Merhaba Mobile Engagement Web SDK'ın bu sürümü Samsung akıllı TV, Opera TV, webOS veya hello ulaşma özelliği desteklemiyor.

> [!IMPORTANT]
> Capptain ve Azure Mobile Engagement olan değil hello aynı hizmet ve yalnızca nasıl toomigrate hello istemci uygulaması yordamları izleyerek hello vurgulayın. Geçirme hello Mobile Engagement Web SDK hello uygulama verilerinizi bir Capptain server tooa Mobile Engagement Sunucusu'ndan geçişi yapılmaz.
> 
> 

#### <a name="javascript-files"></a>JavaScript dosyaları
Değiştir hello dosya capptain-sdk.js hello ile azure engagement.js dosya ve komut dosyası içeri aktarmalar uygun şekilde güncelleştirilir.

#### <a name="remove-capptain-reach"></a>Capptain Reach Kaldır
Merhaba Mobile Engagement Web SDK'ın bu sürümü hello ulaşma özelliği desteklemiyor. Uygulamanıza Capptain ulaşma bütünleştirdiyseniz tooremove gerekir.

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

#### <a name="remove-deprecated-apis"></a>Kullanım dışı API'leri Kaldır
Bazı Capptain API'lerden hello Mobile Engagement Web SDK'SININ kullanım dışı bırakılmıştır.

API izleyen tüm çağrıları toohello kaldırın: `agent.connect`, `agent.disconnect`, `agent.pause`, ve `agent.sendMessageToDevice`.

Geri aramalar Capptain yapılandırmasından aşağıdaki hello birini kaldırın: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, ve `onPushMessageReceived`.

#### <a name="configuration"></a>Yapılandırma
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

Merhaba bağlantı dizesi, uygulamanız için hello Azure portalında görüntülenir.

#### <a name="javascript-apis"></a>JavaScript API'leri
Merhaba genel JavaScript nesne `window.capptain` adlandırıldı `window.azureEngagement`, ancak hello kullanabilirsiniz `window.engagement` API çağrıları için diğer ad. Bu diğer ad toodefine hello SDK yapılandırma kullanamazsınız.

Örneğin, `capptain.deviceId` hale `engagement.deviceId`, `capptain.agent.startActivity` hale `engagement.agent.startActivity`ve benzeri.

Lütfen okuyun uygulamanıza hello Azure Mobile Engagement Web SDK önceki bir sürümü zaten bütünleştirdiyseniz [yükseltme yordamları](mobile-engagement-web-upgrade-procedure.md).

