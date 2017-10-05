---
title: "Azure Mobile Engagement Android SDK tümleştirmesi"
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
ms.openlocfilehash: 43987962ea2b7b825b88643d18b4db65f1f1670e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-adm-with-engagement"></a><span data-ttu-id="0435e-103">ADM katılım ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="0435e-103">How to Integrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0435e-104">Tümleştirme katılım nasıl Android belge üzerinde bu kılavuzu izlemeden önce açıklanan tümleştirme yordamı izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0435e-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="0435e-105">Bu belge, yalnızca, zaten Reach modülünün ve Amazon aygıtları göndermek için plan tümleşik yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="0435e-105">This document is useful only if you already integrated the Reach module and plan to push Amazon devices.</span></span> <span data-ttu-id="0435e-106">Uygulamanızda Reach kampanyaları tümleştirmek için önce okuyun nasıl android'de Engagement Reach tümleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0435e-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="0435e-107">Giriş</span><span class="sxs-lookup"><span data-stu-id="0435e-107">Introduction</span></span>
<span data-ttu-id="0435e-108">ADM tümleştirme uygulamanızı Amazon Android cihazları hedeflerken edilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="0435e-108">Integrating ADM allows your application to be pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="0435e-109">SDK her zaman gönderilen ADM yüklerini içeren `azme` veri nesnesindeki anahtar.</span><span class="sxs-lookup"><span data-stu-id="0435e-109">ADM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="0435e-110">Böylece, uygulamanızda başka bir amaçla ADM kullanırsanız, bu anahtarı temel iter filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0435e-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0435e-111">Android 4.0.3 çalıştıran yalnızca Amazon Kindle cihazlar veya Amazon Device Messaging; yukarıdaki desteklenir Ancak, bu kod diğer aygıtlarda güvenli bir şekilde tümleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="0435e-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-to-adm"></a><span data-ttu-id="0435e-112">ADM için kaydolun</span><span class="sxs-lookup"><span data-stu-id="0435e-112">Sign up to ADM</span></span>
<span data-ttu-id="0435e-113">Yapmadıysanız, Amazon hesabınızdaki ADM etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0435e-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="0435e-114">Yordamı, ayrıntılı: [ <https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="0435e-114">The procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="0435e-115">Yordamı tamamladığınızda, şunları alırsınız:</span><span class="sxs-lookup"><span data-stu-id="0435e-115">Upon completing the procedure, you get:</span></span>

* <span data-ttu-id="0435e-116">Aygıtlarınızı itme yapabilmek katılım için OAuth kimlik (istemci kimliği ve istemci gizli anahtarı).</span><span class="sxs-lookup"><span data-stu-id="0435e-116">OAuth credentials (a Client ID and a Client Secret) for Engagement to be able to push your devices.</span></span>
* <span data-ttu-id="0435e-117">Uygulamanıza tümleşik bir API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="0435e-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="0435e-118">SDK tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="0435e-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="0435e-119">Cihaz kayıtlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="0435e-119">Managing device registrations</span></span>
<span data-ttu-id="0435e-120">Her bir cihaz kayıt komutu ADM sunuculara göndermesi gerekir, aksi halde bunlar ulaşılamıyor.</span><span class="sxs-lookup"><span data-stu-id="0435e-120">Each device must send a registration command to the ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="0435e-121">Zaten kullanıyorsanız [ADM istemci Kitaplığı]ve zaten [ADM tümleşik] için android-sdk-adm-alma doğrudan gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0435e-121">If you already use the [ADM client library], and already have [integrated ADM] you can directly go to android-sdk-adm-receive.</span></span>

<span data-ttu-id="0435e-122">ADM henüz değil bütünleştirdiyseniz, katılım uygulamanızda etkinleştirmek için daha basit bir yol vardır:</span><span class="sxs-lookup"><span data-stu-id="0435e-122">If you have not integrated ADM yet, Engagement has a simpler way to enable it in your application:</span></span>

<span data-ttu-id="0435e-123">Düzenleme, `AndroidManifest.xml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="0435e-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="0435e-124">Amazon ad ekleme dosya şu şekilde başlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0435e-124">Add the Amazon namespace, the file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="0435e-125">İçinde `<application/>` etiketi, bu bölümde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0435e-125">Inside the `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="0435e-126">Amazon etiket ekledikten sonra proje derleme hedefi Android 2.1 ise bir derleme hatası olabilir.</span><span class="sxs-lookup"><span data-stu-id="0435e-126">After adding the amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="0435e-127">Kullanmak zorunda bir **Android 2.1 +** hedef yapı (endişelenmeyin, hala sahip bir `minSdkVersion` 4'e ayarlayın).</span><span class="sxs-lookup"><span data-stu-id="0435e-127">You have to use an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set to 4).</span></span>
* <span data-ttu-id="0435e-128">ADM API anahtarı izleyerek bir varlık tümleştirmek [bu yordamı].</span><span class="sxs-lookup"><span data-stu-id="0435e-128">Integrate the ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="0435e-129">Sonraki bölümlerde yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="0435e-129">Then follow the instructions of the next sections.</span></span>

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="0435e-130">Katılım itme hizmetine kayıt kimliği iletişim kurmak ve bildirimlerin</span><span class="sxs-lookup"><span data-stu-id="0435e-130">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="0435e-131">Katılım itme hizmetini cihaza kayıt kimliğini iletişim kurmak ve kendi bildirimleri almak için aşağıdakileri ekleyin, `AndroidManifest.xml` içinde dosya `<application/>` (ADM katılım olmadan kullanmak olsa bile) etiketi:</span><span class="sxs-lookup"><span data-stu-id="0435e-131">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you use ADM without Engagement):</span></span>

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

<span data-ttu-id="0435e-132">Aşağıdaki izinlere sahip olmak, `AndroidManifest.xml` (önce `</application>` etiketi).</span><span class="sxs-lookup"><span data-stu-id="0435e-132">Ensure you have the following permissions in your `AndroidManifest.xml` (before the `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="0435e-133">GRANT katılım OAuth kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="0435e-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="0435e-134">OAuth kimlik bilgilerinizi (istemci kimliği ve istemci gizli anahtarı) Engagement portalında gönderin.</span><span class="sxs-lookup"><span data-stu-id="0435e-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

<span data-ttu-id="0435e-135">[< https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span><span class="sxs-lookup"><span data-stu-id="0435e-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span></span>
<span data-ttu-id="0435e-136">[ADM istemci Kitaplığı]:https://developer.amazon.com/sdk/adm/setup.html</span><span class="sxs-lookup"><span data-stu-id="0435e-136">[ADM client library]:https://developer.amazon.com/sdk/adm/setup.html</span></span>
<span data-ttu-id="0435e-137">[ADM tümleşik]:https://developer.amazon.com/sdk/adm/integrating-app.html</span><span class="sxs-lookup"><span data-stu-id="0435e-137">[integrated ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span></span>
<span data-ttu-id="0435e-138">[bu yordamı]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span><span class="sxs-lookup"><span data-stu-id="0435e-138">[this procedure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span></span>
