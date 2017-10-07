---
title: "aaaAzure Mobile Engagement Android SDK tümleştirmesi"
description: "En son güncelleştirmeler ve yordamlar için Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a><span data-ttu-id="0eb87-103">Nasıl tooIntegrate ADM engagement</span><span class="sxs-lookup"><span data-stu-id="0eb87-103">How tooIntegrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0eb87-104">TooIntegrate android'de katılım nasıl belge bu kılavuzu izlemeden önce hello açıklanan hello tümleştirme yordamı izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0eb87-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="0eb87-105">Bu belge, yalnızca hello Reach modülü ve planı toopush Amazon cihazları zaten bütünleştirdiyseniz yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="0eb87-105">This document is useful only if you already integrated hello Reach module and plan toopush Amazon devices.</span></span> <span data-ttu-id="0eb87-106">Lütfen ilk nasıl okuyun, uygulamanızda toointegrate Reach kampanyaları tooIntegrate Engagement Reach android'de.</span><span class="sxs-lookup"><span data-stu-id="0eb87-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="0eb87-107">Giriş</span><span class="sxs-lookup"><span data-stu-id="0eb87-107">Introduction</span></span>
<span data-ttu-id="0eb87-108">ADM tümleştirme Amazon Android cihazları hedeflerken gönderilir, uygulama toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="0eb87-108">Integrating ADM allows your application toobe pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="0eb87-109">ADM yüklerini toohello SDK her zaman gönderilen içeren hello `azme` hello veri nesnesindeki anahtar.</span><span class="sxs-lookup"><span data-stu-id="0eb87-109">ADM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="0eb87-110">Böylece, uygulamanızda başka bir amaçla ADM kullanırsanız, bu anahtarı temel iter filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0eb87-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0eb87-111">Android 4.0.3 çalıştıran yalnızca Amazon Kindle cihazlar veya Amazon Device Messaging; yukarıdaki desteklenir Ancak, bu kod diğer aygıtlarda güvenli bir şekilde tümleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="0eb87-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-tooadm"></a><span data-ttu-id="0eb87-112">TooADM oturum</span><span class="sxs-lookup"><span data-stu-id="0eb87-112">Sign up tooADM</span></span>
<span data-ttu-id="0eb87-113">Yapmadıysanız, Amazon hesabınızdaki ADM etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0eb87-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="0eb87-114">Merhaba yordamı ayrıntılı adresindeki: [ <https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="0eb87-114">hello procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="0eb87-115">Merhaba yordamı tamamladıktan sonra alın:</span><span class="sxs-lookup"><span data-stu-id="0eb87-115">Upon completing hello procedure, you get:</span></span>

* <span data-ttu-id="0eb87-116">OAuth (istemci kimliği ve istemci parolasını) katılım toobe mümkün toopush için cihazlarınızı kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="0eb87-116">OAuth credentials (a Client ID and a Client Secret) for Engagement toobe able toopush your devices.</span></span>
* <span data-ttu-id="0eb87-117">Uygulamanıza tümleşik bir API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="0eb87-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="0eb87-118">SDK tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="0eb87-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="0eb87-119">Cihaz kayıtlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="0eb87-119">Managing device registrations</span></span>
<span data-ttu-id="0eb87-120">Her bir cihaz kayıt komutu toohello ADM sunucuları göndermesi gerekir, aksi halde bunlar ulaşılamıyor.</span><span class="sxs-lookup"><span data-stu-id="0eb87-120">Each device must send a registration command toohello ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="0eb87-121">Merhaba zaten kullanıyorsanız [ADM istemci Kitaplığı]ve zaten [ADM tümleşik] tooandroid-sdk-adm-alma doğrudan gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0eb87-121">If you already use hello [ADM client library], and already have [integrated ADM] you can directly go tooandroid-sdk-adm-receive.</span></span>

<span data-ttu-id="0eb87-122">ADM entegre edilemez henüz katılım daha basit bir şekilde tooenable sahip değilse, uygulamanızın içinde:</span><span class="sxs-lookup"><span data-stu-id="0eb87-122">If you have not integrated ADM yet, Engagement has a simpler way tooenable it in your application:</span></span>

<span data-ttu-id="0eb87-123">Düzenleme, `AndroidManifest.xml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="0eb87-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="0eb87-124">Amazon ad Merhaba, hello dosya şu şekilde başlaması gereken ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0eb87-124">Add hello Amazon namespace, hello file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="0eb87-125">İç hello `<application/>` etiketi, bu bölümde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0eb87-125">Inside hello `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="0eb87-126">Proje derleme hedefi Android 2.1 ise hello amazon etiketi eklendikten sonra bir derleme hatası olabilir.</span><span class="sxs-lookup"><span data-stu-id="0eb87-126">After adding hello amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="0eb87-127">Toouse sahip bir **Android 2.1 +** hedef yapı (endişelenmeyin, hala sahip bir `minSdkVersion` too4 ayarlayın).</span><span class="sxs-lookup"><span data-stu-id="0eb87-127">You have toouse an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set too4).</span></span>
* <span data-ttu-id="0eb87-128">Merhaba ADM API anahtarı izleyerek bir varlık tümleştirmek [bu yordamı].</span><span class="sxs-lookup"><span data-stu-id="0eb87-128">Integrate hello ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="0eb87-129">Ardından hello sonraki bölümleri hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="0eb87-129">Then follow hello instructions of hello next sections.</span></span>

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="0eb87-130">Kayıt Kimliği toohello katılım gönderme hizmeti iletişim ve bildirimlerin</span><span class="sxs-lookup"><span data-stu-id="0eb87-130">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="0eb87-131">Sipariş toocommunicate hello kayıt kimliğinde hello aygıt toohello katılım anında hizmet ve kendi bildirimleri almak, tooyour aşağıdaki hello eklemeniz `AndroidManifest.xml` hello içinde dosya `<application/>` (ADM katılım olmadan kullanmak olsa bile) etiketi:</span><span class="sxs-lookup"><span data-stu-id="0eb87-131">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you use ADM without Engagement):</span></span>

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

<span data-ttu-id="0eb87-132">Aşağıdaki izinleri de hello olduğundan emin olun, `AndroidManifest.xml` (Merhaba önce `</application>` etiketi).</span><span class="sxs-lookup"><span data-stu-id="0eb87-132">Ensure you have hello following permissions in your `AndroidManifest.xml` (before hello `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="0eb87-133">GRANT katılım OAuth kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="0eb87-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="0eb87-134">OAuth kimlik bilgilerinizi (istemci kimliği ve istemci gizli anahtarı) Engagement portalında gönderin.</span><span class="sxs-lookup"><span data-stu-id="0eb87-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

[< https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[ADM istemci Kitaplığı]:https://developer.amazon.com/sdk/adm/setup.html
[ADM tümleşik]:https://developer.amazon.com/sdk/adm/integrating-app.html
[bu yordamı]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
