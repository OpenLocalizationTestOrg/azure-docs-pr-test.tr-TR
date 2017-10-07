---
title: "aaaAzure Mobile Engagement Android SDK tümleştirmesi"
description: "En son güncelleştirmeler ve yordamlar için Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: e81230cbc99a209f2909cc163c4e566df67dc828
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a><span data-ttu-id="c0f77-103">Nasıl tooIntegrate Mobile Engagement ile GCM</span><span class="sxs-lookup"><span data-stu-id="c0f77-103">How tooIntegrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c0f77-104">TooIntegrate android'de katılım nasıl belge bu kılavuzu izlemeden önce hello açıklanan hello tümleştirme yordamı izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0f77-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="c0f77-105">Bu belge, yalnızca, zaten tümleşik hello modülü ve planı toopush Google Play cihazlara ulaşmak yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="c0f77-105">This document is useful only if you already integrated hello Reach module and plan toopush Google Play devices.</span></span> <span data-ttu-id="c0f77-106">Lütfen ilk nasıl okuyun, uygulamanızda toointegrate Reach kampanyaları tooIntegrate Engagement Reach android'de.</span><span class="sxs-lookup"><span data-stu-id="c0f77-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="c0f77-107">Giriş</span><span class="sxs-lookup"><span data-stu-id="c0f77-107">Introduction</span></span>
<span data-ttu-id="c0f77-108">GCM tümleştirme gönderilir, uygulama toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="c0f77-108">Integrating GCM allows your application toobe pushed.</span></span>

<span data-ttu-id="c0f77-109">Toohello SDK her zaman gönderilen GCM yüklerini içeren hello `azme` hello veri nesnesindeki anahtar.</span><span class="sxs-lookup"><span data-stu-id="c0f77-109">GCM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="c0f77-110">Böylece, uygulamanızda başka bir amaçla GCM kullanırsanız, bu anahtarı temel iter filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f77-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0f77-111">Yalnızca Android 2.2 çalıştıran cihazlar veya üzeri yüklü ve Google sahip Google Play sahip etkin arka plan bağlantı GCM; kullanarak gönderilemez Ancak, bu kod cihazlarda (yalnızca hedefleri'ı kullanır) güvenli bir şekilde desteklenmeyen tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f77-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="c0f77-112">API anahtarıyla Google Cloud Messaging projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0f77-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="c0f77-113">SDK tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="c0f77-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="c0f77-114">Cihaz kayıtlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="c0f77-114">Managing device registrations</span></span>
<span data-ttu-id="c0f77-115">Her bir cihaz kayıt komutu toohello Google sunucularına göndermesi gerekir, aksi halde bunlar ulaşılamıyor.</span><span class="sxs-lookup"><span data-stu-id="c0f77-115">Each device must send a registration command toohello Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="c0f77-116">Bir cihaz da GCM bildirimleri (Merhaba uygulaması kaldırılırsa hello cihaz otomatik olarak kaydettirilmemiş) kaydını kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f77-116">A device can also unregister from GCM notifications (hello device is automatically unregistered if hello application is uninstalled).</span></span>

<span data-ttu-id="c0f77-117">Kullanmazsanız [Google Play SDK] veya, zaten hello kayıt hedefi kendiniz gönderme, hello aygıt sizin için otomatik olarak kaydedilecek katılım yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f77-117">If you don't use [Google Play SDK] or you don't already send hello registration intent yourself, you can make Engagement register hello device automatically for you.</span></span>

<span data-ttu-id="c0f77-118">tooenable bunu tooyour aşağıdaki hello eklemek `AndroidManifest.xml` hello içinde dosya `<application/>` etiketi:</span><span class="sxs-lookup"><span data-stu-id="c0f77-118">tooenable this, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="c0f77-119">Kayıt Kimliği toohello katılım gönderme hizmeti iletişim ve bildirimlerin</span><span class="sxs-lookup"><span data-stu-id="c0f77-119">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="c0f77-120">Sipariş toocommunicate hello kayıt kimliğinde hello aygıt toohello katılım anında hizmet ve kendi bildirimleri almak, tooyour aşağıdaki hello eklemeniz `AndroidManifest.xml` hello içinde dosya `<application/>` (cihaz kayıtları kendiniz yönettiğiniz olsa bile) etiketi:</span><span class="sxs-lookup"><span data-stu-id="c0f77-120">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you manage device registrations yourself):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

<span data-ttu-id="c0f77-121">Aşağıdaki izinleri de hello olduğundan emin olun, `AndroidManifest.xml` (Merhaba sonra `</application>` etiketi).</span><span class="sxs-lookup"><span data-stu-id="c0f77-121">Ensure you have hello following permissions in your `AndroidManifest.xml` (after hello `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="c0f77-122">GRANT Mobile Engagement erişimi tooyour GCM API anahtarı</span><span class="sxs-lookup"><span data-stu-id="c0f77-122">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="c0f77-123">İzleyin [bu kılavuzda](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement erişimi tooyour GCM API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="c0f77-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement access tooyour GCM API Key.</span></span>

[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start
