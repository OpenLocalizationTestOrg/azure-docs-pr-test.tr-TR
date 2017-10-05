---
title: "Azure Mobile Engagement Android SDK tümleştirmesi"
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
ms.openlocfilehash: 0282abbf44406cac89c13520bc2a4e375817ed1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-gcm-with-mobile-engagement"></a><span data-ttu-id="54d81-103">GCM mobil katılım ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="54d81-103">How to Integrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="54d81-104">Tümleştirme katılım nasıl Android belge üzerinde bu kılavuzu izlemeden önce açıklanan tümleştirme yordamı izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="54d81-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="54d81-105">Bu belge, yalnızca, zaten Reach modülünün ve Google Play aygıtları göndermek için plan tümleşik yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="54d81-105">This document is useful only if you already integrated the Reach module and plan to push Google Play devices.</span></span> <span data-ttu-id="54d81-106">Uygulamanızda Reach kampanyaları tümleştirmek için önce okuyun nasıl android'de Engagement Reach tümleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="54d81-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="54d81-107">Giriş</span><span class="sxs-lookup"><span data-stu-id="54d81-107">Introduction</span></span>
<span data-ttu-id="54d81-108">GCM tümleştirme uygulamanızı edilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="54d81-108">Integrating GCM allows your application to be pushed.</span></span>

<span data-ttu-id="54d81-109">SDK her zaman gönderilen GCM yüklerini içeren `azme` veri nesnesindeki anahtar.</span><span class="sxs-lookup"><span data-stu-id="54d81-109">GCM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="54d81-110">Böylece, uygulamanızda başka bir amaçla GCM kullanırsanız, bu anahtarı temel iter filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54d81-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54d81-111">Yalnızca Android 2.2 çalıştıran cihazlar veya üzeri yüklü ve Google sahip Google Play sahip etkin arka plan bağlantı GCM; kullanarak gönderilemez Ancak, bu kod cihazlarda (yalnızca hedefleri'ı kullanır) güvenli bir şekilde desteklenmeyen tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54d81-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="54d81-112">API anahtarıyla Google Cloud Messaging projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="54d81-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="54d81-113">SDK tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="54d81-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="54d81-114">Cihaz kayıtlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="54d81-114">Managing device registrations</span></span>
<span data-ttu-id="54d81-115">Her bir cihaz kayıt komutu Google sunucularına göndermesi gerekir, aksi halde bunlar ulaşılamıyor.</span><span class="sxs-lookup"><span data-stu-id="54d81-115">Each device must send a registration command to the Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="54d81-116">Bir cihaz da GCM bildirim (uygulama kaldırılırsa cihaz otomatik olarak kaydettirilmemiş) kaydını kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54d81-116">A device can also unregister from GCM notifications (the device is automatically unregistered if the application is uninstalled).</span></span>

<span data-ttu-id="54d81-117">Kullanmazsanız [Google Play SDK] veya, zaten kayıt hedefi kendiniz gönderme, otomatik olarak sizin için kaydedilecek katılım yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54d81-117">If you don't use [Google Play SDK] or you don't already send the registration intent yourself, you can make Engagement register the device automatically for you.</span></span>

<span data-ttu-id="54d81-118">Bu ayarı etkinleştirmek için aşağıdakileri ekleyin, `AndroidManifest.xml` içinde dosya `<application/>` etiketi:</span><span class="sxs-lookup"><span data-stu-id="54d81-118">To enable this, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget the \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="54d81-119">Katılım itme hizmetine kayıt kimliği iletişim kurmak ve bildirimlerin</span><span class="sxs-lookup"><span data-stu-id="54d81-119">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="54d81-120">Katılım itme hizmetini cihaza kayıt kimliğini iletişim kurmak ve kendi bildirimleri almak için aşağıdakileri ekleyin, `AndroidManifest.xml` içinde dosya `<application/>` (cihaz kayıtları kendiniz yönettiğiniz olsa bile) etiketi:</span><span class="sxs-lookup"><span data-stu-id="54d81-120">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you manage device registrations yourself):</span></span>

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

<span data-ttu-id="54d81-121">Aşağıdaki izinlere sahip olmak, `AndroidManifest.xml` (sonra `</application>` etiketi).</span><span class="sxs-lookup"><span data-stu-id="54d81-121">Ensure you have the following permissions in your `AndroidManifest.xml` (after the `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="54d81-122">GCM API Anahtarınıza Mobile Engagement erişimi verin</span><span class="sxs-lookup"><span data-stu-id="54d81-122">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="54d81-123">İzleyin [bu kılavuzda](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) GCM API anahtarınıza Mobile Engagement erişim vermek için.</span><span class="sxs-lookup"><span data-stu-id="54d81-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) to grant Mobile Engagement access to your GCM API Key.</span></span>

<span data-ttu-id="54d81-124">[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start</span><span class="sxs-lookup"><span data-stu-id="54d81-124">[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start</span></span>
