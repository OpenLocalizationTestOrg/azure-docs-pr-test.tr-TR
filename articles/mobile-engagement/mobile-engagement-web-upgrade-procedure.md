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
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="50693-103">Azure Mobile Engagement Web SDK yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="50693-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="50693-104">Web uygulamanıza hello Azure Mobile Engagement Web SDK önceki bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükselttiğinizde aşağıdaki tooconsider hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="50693-104">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your web application, you need tooconsider hello following points when you upgrade hello SDK.</span></span>

<span data-ttu-id="50693-105">Merhaba Mobile Engagement Web SDK birden fazla sürümünü atladıysanız hello yükseltme işlemi sırasında birçok yordamı toocomplete gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="50693-105">If you skipped multiple versions of hello Mobile Engagement Web SDK, you might need toocomplete several procedures during hello upgrade process.</span></span> <span data-ttu-id="50693-106">Örneğin, 1.4.0 geçirirseniz too1.6.0, ilk izleme hello yordamları tooupgrade 1.4.0 gelen too1.5.0.</span><span class="sxs-lookup"><span data-stu-id="50693-106">For example, if you migrate from 1.4.0 too1.6.0, first follow hello procedures tooupgrade from 1.4.0 too1.5.0.</span></span> <span data-ttu-id="50693-107">Ardından 1.5.0 hello yordamları tooupgrade izleyin too1.6.0.</span><span class="sxs-lookup"><span data-stu-id="50693-107">Then, follow hello procedures tooupgrade from 1.5.0 too1.6.0.</span></span>

<span data-ttu-id="50693-108">Yükseltme, hangi sürümü hello dosya azure-engagement.js önceki sürümünü hello dosyasının en son sürümünü hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="50693-108">Whichever version you upgrade from, replace any earlier version of hello file azure-engagement.js with hello latest version of hello file.</span></span>

## <a name="upgrade-from-121-too200"></a><span data-ttu-id="50693-109">1.2.1'den yükseltme too2.0.0</span><span class="sxs-lookup"><span data-stu-id="50693-109">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="50693-110">Bu bölümde, nasıl toomigrate Mobile Engagement Web SDK tümleştirmesi hello Capptain hizmetinden sunulan tooan Azure Mobile Engagement uygulaması Capptain SAS tarafından açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="50693-110">This section describes how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="50693-111">Önceki bir sürümden başvurun hello Capptain Web sitesi toofirst Lütfen geçiriyorsanız, too1.2.1 geçirmek ve hello yordamları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="50693-111">If you are migrating from an earlier version, please consult hello Capptain website toofirst migrate too1.2.1, and then apply hello following procedures.</span></span>

<span data-ttu-id="50693-112">Merhaba Mobile Engagement Web SDK'ın bu sürümü Samsung akıllı TV, Opera TV, webOS veya hello ulaşma özelliği desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="50693-112">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50693-113">Capptain ve Azure Mobile Engagement olan değil hello aynı hizmet.</span><span class="sxs-lookup"><span data-stu-id="50693-113">Capptain and Azure Mobile Engagement are not hello same service.</span></span> <span data-ttu-id="50693-114">Aşağıdaki yordamı hello yalnızca nasıl toomigrate hello istemci uygulamaları vurgular.</span><span class="sxs-lookup"><span data-stu-id="50693-114">hello following procedure highlights only how toomigrate hello client app.</span></span> <span data-ttu-id="50693-115">Geçirme hello Mobile Engagement Web SDK hello uygulama verilerinizi bir Capptain server tooa Mobile Engagement Sunucusu'ndan geçişi yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="50693-115">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="50693-116">JavaScript dosyaları</span><span class="sxs-lookup"><span data-stu-id="50693-116">JavaScript files</span></span>
<span data-ttu-id="50693-117">Değiştir hello dosya capptain-sdk.js hello ile azure engagement.js dosya ve komut dosyası içeri aktarmalar uygun şekilde güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="50693-117">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="50693-118">Capptain Reach Kaldır</span><span class="sxs-lookup"><span data-stu-id="50693-118">Remove Capptain Reach</span></span>
<span data-ttu-id="50693-119">Merhaba Mobile Engagement Web SDK'ın bu sürümü hello ulaşma özelliği desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="50693-119">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="50693-120">Uygulamanıza Capptain erişim'i bütünleştirdiyseniz tooremove gerekir.</span><span class="sxs-lookup"><span data-stu-id="50693-120">If you integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="50693-121">Merhaba ulaşmak CSS alma sayfanızdan kaldırın ve hello ilgili .css dosyasını (capptain-reach.css, varsayılan olarak) silin.</span><span class="sxs-lookup"><span data-stu-id="50693-121">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="50693-122">Reach kaynakları aşağıdaki hello Sil: hello Kapat görüntü (capptain-close.png, varsayılan olarak) ve hello marka simgesi (capptain bildirim-simgesi, varsayılan olarak).</span><span class="sxs-lookup"><span data-stu-id="50693-122">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="50693-123">Uygulama bildirimlerinin Hello ulaşmak UI kaldırın.</span><span class="sxs-lookup"><span data-stu-id="50693-123">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="50693-124">Merhaba varsayılan düzeni şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="50693-124">hello default layout looks like this:</span></span>

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

<span data-ttu-id="50693-125">Merhaba ulaşmak UI metin ve web duyuruları ve yoklamaları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="50693-125">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="50693-126">Merhaba varsayılan düzeni şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="50693-126">hello default layout looks like this:</span></span>

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

<span data-ttu-id="50693-127">Merhaba kaldırmak `reach` varsa, yapılandırmasından nesne.</span><span class="sxs-lookup"><span data-stu-id="50693-127">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="50693-128">Şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="50693-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="50693-129">Tüm diğer ulaşma özelleştirme, kategorileri gibi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="50693-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="50693-130">Kullanım dışı API'leri Kaldır</span><span class="sxs-lookup"><span data-stu-id="50693-130">Remove deprecated APIs</span></span>
<span data-ttu-id="50693-131">Bazı Capptain API'lerden hello Mobile Engagement Web SDK'SININ kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="50693-131">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="50693-132">API izleyen tüm çağrıları toohello kaldırın: `agent.connect`, `agent.disconnect`, `agent.pause`, ve `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="50693-132">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="50693-133">Geri aramalar Capptain yapılandırmasından aşağıdaki hello tüm örneklerini kaldırın: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, ve `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="50693-133">Remove any instances of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="50693-134">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="50693-134">Configuration</span></span>
<span data-ttu-id="50693-135">Mobile Engagement bir bağlantı dizesi tooconfigure SDK tanımlayıcıları, örneğin, hello uygulama tanımlayıcısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="50693-135">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="50693-136">Merhaba uygulama kimliği, bağlantı dizesi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="50693-136">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="50693-137">Merhaba SDK yapılandırma değişiklikleri için o hello genel nesne Not `capptain` çok`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="50693-137">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="50693-138">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="50693-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="50693-139">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="50693-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="50693-140">Merhaba bağlantı dizesi, uygulamanız için hello Azure Portal görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="50693-140">hello connection string for your application is displayed in hello Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="50693-141">JavaScript API'leri</span><span class="sxs-lookup"><span data-stu-id="50693-141">JavaScript APIs</span></span>
<span data-ttu-id="50693-142">Merhaba genel JavaScript nesne `window.capptain` adlandırıldı `window.azureEngagement` ancak hello kullanabilirsiniz `window.engagement` API çağrıları için diğer ad.</span><span class="sxs-lookup"><span data-stu-id="50693-142">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="50693-143">Merhaba diğer toodefine hello SDK yapılandırma kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="50693-143">You can't use hello alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="50693-144">Örneğin, `capptain.deviceId` hale `engagement.deviceId`, `capptain.agent.startActivity` hale `engagement.agent.startActivity`ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="50693-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

