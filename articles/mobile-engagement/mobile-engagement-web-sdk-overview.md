---
title: "Azure Mobile Engagement Web SDK genel bakış | Microsoft Docs"
description: "En son güncelleştirmeleri ve Azure Mobile Engagement için Web SDK'sı için yordamlar"
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
ms.openlocfilehash: 770a83131a3e661771db50b22ce7de25b2d541cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="584f7-103">Azure Mobile Engagement Web SDK</span><span class="sxs-lookup"><span data-stu-id="584f7-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="584f7-104">Bir web uygulamasını Azure Mobile Engagement tümleştirme hakkında tüm ayrıntılar için buradan başlayın.</span><span class="sxs-lookup"><span data-stu-id="584f7-104">Start here for all the details about how to integrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="584f7-105">İsterseniz, kendi web uygulaması ile çalışmaya başlama önce bir denemelisiniz bkz bizim [15 dakikalık Öğreticisi](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="584f7-105">If you'd like to give it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="584f7-106">Tümleştirme yordamları</span><span class="sxs-lookup"><span data-stu-id="584f7-106">Integration procedures</span></span>
1. <span data-ttu-id="584f7-107">Bilgi [web uygulamanızı Mobile Engagement tümleştirme](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="584f7-107">Learn [how to integrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="584f7-108">Etiket planı uygulama için bilgi [API web uygulamanızda etiketleme Gelişmiş Mobile Engagement kullanmayı](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="584f7-108">For tag plan implementation, learn [how to use the advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="584f7-109">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="584f7-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="584f7-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="584f7-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="584f7-111">Özel (Safari) gözatma sabit kilitlenme.</span><span class="sxs-lookup"><span data-stu-id="584f7-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="584f7-112">Sabit kilitlenme tarayıcılarında tanımlama bilgileri devre dışı ile.</span><span class="sxs-lookup"><span data-stu-id="584f7-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="584f7-113">Tüm sürümler için lütfen bkz. [tamamlamak sürüm notları](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="584f7-113">For all versions, please see the [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="584f7-114">Yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="584f7-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-to-200"></a><span data-ttu-id="584f7-115">1.2.1 2.0.0 için yükseltme</span><span class="sxs-lookup"><span data-stu-id="584f7-115">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="584f7-116">Aşağıdaki bölümlerde, nasıl Azure Mobile Engagement uygulamayı Capptain SAS tarafından sunulan Capptain hizmetinden bir Mobile Engagement Web SDK tümleştirmesi geçirileceği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="584f7-116">The following sections describe how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="584f7-117">1.2.1'den önceki bir sürümden geçiriyorsanız, Lütfen 1.2.1 için ilk geçirmek için Capptain Web sitesine bakın ve ardından aşağıdaki yordamları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="584f7-117">If you are migrating from a version earlier than 1.2.1, please consult the Capptain website to migrate to 1.2.1 first, and then apply the following procedures.</span></span>

<span data-ttu-id="584f7-118">Mobile Engagement Web SDK'ın bu sürümü Samsung akıllı TV, Opera TV, webOS veya Reach özelliğini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="584f7-118">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="584f7-119">Aynı hizmeti Capptain ve Azure Mobile Engagement değildir ve aşağıdaki yordamları istemci uygulaması yalnızca nasıl geçirileceği vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="584f7-119">Capptain and Azure Mobile Engagement are not the same service, and the following procedures highlight only how to migrate the client app.</span></span> <span data-ttu-id="584f7-120">Mobile Engagement Web SDK uygulamasında geçirme verilerinizi Capptain sunucusundan bir Mobile Engagement sunucuya geçişi yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="584f7-120">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="584f7-121">JavaScript dosyaları</span><span class="sxs-lookup"><span data-stu-id="584f7-121">JavaScript files</span></span>
<span data-ttu-id="584f7-122">Dosya capptain sdk.js dosya azure engagement.js ile değiştirin ve ardından komut dosyasını içeri aktarmalar uygun şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="584f7-122">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="584f7-123">Capptain Reach Kaldır</span><span class="sxs-lookup"><span data-stu-id="584f7-123">Remove Capptain Reach</span></span>
<span data-ttu-id="584f7-124">Mobile Engagement Web SDK'ın bu sürümü ulaşma özelliği desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="584f7-124">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="584f7-125">Uygulamanıza Capptain ulaşma bütünleştirdiyseniz kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="584f7-125">If you have integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="584f7-126">CSS ulaşmak alma sayfanızdan kaldırın ve ilgili .css dosyasını (capptain-reach.css, varsayılan olarak) silin.</span><span class="sxs-lookup"><span data-stu-id="584f7-126">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="584f7-127">Aşağıdaki ulaşma kaynakları silin: Kapat görüntünün (capptain-close.png, varsayılan olarak) ve marka simgesi (capptain bildirim-simgesi, varsayılan olarak).</span><span class="sxs-lookup"><span data-stu-id="584f7-127">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="584f7-128">Uygulama bildirimleri için ulaşmak UI kaldırın.</span><span class="sxs-lookup"><span data-stu-id="584f7-128">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="584f7-129">Varsayılan düzen şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="584f7-129">The default layout looks like this:</span></span>

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

<span data-ttu-id="584f7-130">Metin ve web duyuruları ve yoklamaları ulaşmak UI kaldırın.</span><span class="sxs-lookup"><span data-stu-id="584f7-130">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="584f7-131">Varsayılan düzen şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="584f7-131">The default layout looks like this:</span></span>

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

<span data-ttu-id="584f7-132">Kaldırma `reach` varsa, yapılandırmasından nesne.</span><span class="sxs-lookup"><span data-stu-id="584f7-132">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="584f7-133">Şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="584f7-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="584f7-134">Tüm diğer ulaşma özelleştirme, kategorileri gibi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="584f7-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="584f7-135">Kullanım dışı API'leri Kaldır</span><span class="sxs-lookup"><span data-stu-id="584f7-135">Remove deprecated APIs</span></span>
<span data-ttu-id="584f7-136">Bazı Capptain API'lerden Mobile Engagement Web SDK'ın kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="584f7-136">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="584f7-137">Aşağıdaki API'leri tüm çağrıları kaldırın: `agent.connect`, `agent.disconnect`, `agent.pause`, ve `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="584f7-137">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="584f7-138">Aşağıdaki geri çağırmaları hiçbirini Capptain yapılandırmasından kaldırın: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, ve `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="584f7-138">Remove any of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="584f7-139">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="584f7-139">Configuration</span></span>
<span data-ttu-id="584f7-140">Mobile Engagement SDK'sı tanımlayıcıları, örneğin, uygulama tanımlayıcısı yapılandırmak için bir bağlantı dizesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="584f7-140">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="584f7-141">Uygulama kimliği, bağlantı dizesi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="584f7-141">Replace the application ID with your connection string.</span></span> <span data-ttu-id="584f7-142">SDK yapılandırması için genel nesne değişiklikleri Not `capptain` için `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="584f7-142">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="584f7-143">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="584f7-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="584f7-144">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="584f7-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="584f7-145">Bağlantı dizesi, uygulamanız için Azure Portalı'nda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="584f7-145">The connection string for your application is displayed in the Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="584f7-146">JavaScript API'leri</span><span class="sxs-lookup"><span data-stu-id="584f7-146">JavaScript APIs</span></span>
<span data-ttu-id="584f7-147">Genel JavaScript nesne `window.capptain` adlandırıldı `window.azureEngagement`, ancak kullanabilirsiniz `window.engagement` API çağrıları için diğer ad.</span><span class="sxs-lookup"><span data-stu-id="584f7-147">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="584f7-148">SDK yapılandırmasını tanımlamak için bu diğer ad kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="584f7-148">You can't use this alias to define the SDK configuration.</span></span>

<span data-ttu-id="584f7-149">Örneğin, `capptain.deviceId` hale `engagement.deviceId`, `capptain.agent.startActivity` hale `engagement.agent.startActivity`ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="584f7-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="584f7-150">Lütfen okuyun, uygulamasına Azure Mobile Engagement Web SDK önceki bir sürümü zaten bütünleştirdiyseniz [yükseltme yordamları](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="584f7-150">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

