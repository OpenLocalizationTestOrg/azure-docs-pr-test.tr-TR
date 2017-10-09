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
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="3a236-103">Azure Mobile Engagement Web SDK</span><span class="sxs-lookup"><span data-stu-id="3a236-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="3a236-104">Tüm hakkında ayrıntılı bilgi hello için buradan başlayın toointegrate Azure Mobile Engagement bir web uygulamasında.</span><span class="sxs-lookup"><span data-stu-id="3a236-104">Start here for all hello details about how toointegrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="3a236-105">Toogive isterseniz kendi web uygulaması ile çalışmaya başlama önce bir try bkz bizim [15 dakikalık Öğreticisi](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3a236-105">If you'd like toogive it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="3a236-106">Tümleştirme yordamları</span><span class="sxs-lookup"><span data-stu-id="3a236-106">Integration procedures</span></span>
1. <span data-ttu-id="3a236-107">Bilgi [nasıl toointegrate Mobile Engagement web uygulamanızda](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="3a236-107">Learn [how toointegrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="3a236-108">Etiket planı uygulama için bilgi [nasıl toouse hello Mobile Engagement web uygulamanızda API etiketleme Gelişmiş](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="3a236-108">For tag plan implementation, learn [how toouse hello advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="3a236-109">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="3a236-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="3a236-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="3a236-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="3a236-111">Özel (Safari) gözatma sabit kilitlenme.</span><span class="sxs-lookup"><span data-stu-id="3a236-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="3a236-112">Sabit kilitlenme tarayıcılarında tanımlama bilgileri devre dışı ile.</span><span class="sxs-lookup"><span data-stu-id="3a236-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="3a236-113">Tüm sürümler için lütfen hello bakın [tamamlamak sürüm notları](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="3a236-113">For all versions, please see hello [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="3a236-114">Yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="3a236-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-too200"></a><span data-ttu-id="3a236-115">1.2.1'den yükseltme too2.0.0</span><span class="sxs-lookup"><span data-stu-id="3a236-115">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="3a236-116">Merhaba aşağıdaki bölümlerde nasıl toomigrate Mobile Engagement Web SDK tümleştirmesi hello Capptain hizmetinden sunulan tooan Azure Mobile Engagement uygulaması Capptain SAS tarafından açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3a236-116">hello following sections describe how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="3a236-117">Geçiş daha önceki bir sürüm 1.2.1, daha Lütfen hello Capptain Web sitesi toomigrate too1.2.1 ilk bakın ve hello yordamları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="3a236-117">If you are migrating from a version earlier than 1.2.1, please consult hello Capptain website toomigrate too1.2.1 first, and then apply hello following procedures.</span></span>

<span data-ttu-id="3a236-118">Merhaba Mobile Engagement Web SDK'ın bu sürümü Samsung akıllı TV, Opera TV, webOS veya hello ulaşma özelliği desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="3a236-118">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a236-119">Capptain ve Azure Mobile Engagement olan değil hello aynı hizmet ve yalnızca nasıl toomigrate hello istemci uygulaması yordamları izleyerek hello vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="3a236-119">Capptain and Azure Mobile Engagement are not hello same service, and hello following procedures highlight only how toomigrate hello client app.</span></span> <span data-ttu-id="3a236-120">Geçirme hello Mobile Engagement Web SDK hello uygulama verilerinizi bir Capptain server tooa Mobile Engagement Sunucusu'ndan geçişi yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="3a236-120">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="3a236-121">JavaScript dosyaları</span><span class="sxs-lookup"><span data-stu-id="3a236-121">JavaScript files</span></span>
<span data-ttu-id="3a236-122">Değiştir hello dosya capptain-sdk.js hello ile azure engagement.js dosya ve komut dosyası içeri aktarmalar uygun şekilde güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3a236-122">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="3a236-123">Capptain Reach Kaldır</span><span class="sxs-lookup"><span data-stu-id="3a236-123">Remove Capptain Reach</span></span>
<span data-ttu-id="3a236-124">Merhaba Mobile Engagement Web SDK'ın bu sürümü hello ulaşma özelliği desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="3a236-124">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="3a236-125">Uygulamanıza Capptain ulaşma bütünleştirdiyseniz tooremove gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a236-125">If you have integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="3a236-126">Merhaba ulaşmak CSS alma sayfanızdan kaldırın ve hello ilgili .css dosyasını (capptain-reach.css, varsayılan olarak) silin.</span><span class="sxs-lookup"><span data-stu-id="3a236-126">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="3a236-127">Reach kaynakları aşağıdaki hello Sil: hello Kapat görüntü (capptain-close.png, varsayılan olarak) ve hello marka simgesi (capptain bildirim-simgesi, varsayılan olarak).</span><span class="sxs-lookup"><span data-stu-id="3a236-127">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="3a236-128">Uygulama bildirimlerinin Hello ulaşmak UI kaldırın.</span><span class="sxs-lookup"><span data-stu-id="3a236-128">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="3a236-129">Merhaba varsayılan düzeni şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="3a236-129">hello default layout looks like this:</span></span>

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

<span data-ttu-id="3a236-130">Merhaba ulaşmak UI metin ve web duyuruları ve yoklamaları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="3a236-130">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="3a236-131">Merhaba varsayılan düzeni şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="3a236-131">hello default layout looks like this:</span></span>

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

<span data-ttu-id="3a236-132">Merhaba kaldırmak `reach` varsa, yapılandırmasından nesne.</span><span class="sxs-lookup"><span data-stu-id="3a236-132">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="3a236-133">Şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="3a236-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="3a236-134">Tüm diğer ulaşma özelleştirme, kategorileri gibi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="3a236-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="3a236-135">Kullanım dışı API'leri Kaldır</span><span class="sxs-lookup"><span data-stu-id="3a236-135">Remove deprecated APIs</span></span>
<span data-ttu-id="3a236-136">Bazı Capptain API'lerden hello Mobile Engagement Web SDK'SININ kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="3a236-136">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="3a236-137">API izleyen tüm çağrıları toohello kaldırın: `agent.connect`, `agent.disconnect`, `agent.pause`, ve `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="3a236-137">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="3a236-138">Geri aramalar Capptain yapılandırmasından aşağıdaki hello birini kaldırın: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, ve `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="3a236-138">Remove any of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="3a236-139">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3a236-139">Configuration</span></span>
<span data-ttu-id="3a236-140">Mobile Engagement bir bağlantı dizesi tooconfigure SDK tanımlayıcıları, örneğin, hello uygulama tanımlayıcısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="3a236-140">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="3a236-141">Merhaba uygulama kimliği, bağlantı dizesi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3a236-141">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="3a236-142">Merhaba SDK yapılandırma değişiklikleri için o hello genel nesne Not `capptain` çok`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="3a236-142">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="3a236-143">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="3a236-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="3a236-144">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="3a236-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="3a236-145">Merhaba bağlantı dizesi, uygulamanız için hello Azure portalında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3a236-145">hello connection string for your application is displayed in hello Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="3a236-146">JavaScript API'leri</span><span class="sxs-lookup"><span data-stu-id="3a236-146">JavaScript APIs</span></span>
<span data-ttu-id="3a236-147">Merhaba genel JavaScript nesne `window.capptain` adlandırıldı `window.azureEngagement`, ancak hello kullanabilirsiniz `window.engagement` API çağrıları için diğer ad.</span><span class="sxs-lookup"><span data-stu-id="3a236-147">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="3a236-148">Bu diğer ad toodefine hello SDK yapılandırma kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="3a236-148">You can't use this alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="3a236-149">Örneğin, `capptain.deviceId` hale `engagement.deviceId`, `capptain.agent.startActivity` hale `engagement.agent.startActivity`ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="3a236-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="3a236-150">Lütfen okuyun uygulamanıza hello Azure Mobile Engagement Web SDK önceki bir sürümü zaten bütünleştirdiyseniz [yükseltme yordamları](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="3a236-150">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

