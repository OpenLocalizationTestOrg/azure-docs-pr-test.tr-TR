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
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a>Nasıl tooIntegrate Mobile Engagement ile GCM
> [!IMPORTANT]
> TooIntegrate android'de katılım nasıl belge bu kılavuzu izlemeden önce hello açıklanan hello tümleştirme yordamı izlemeniz gerekir.
> 
> Bu belge, yalnızca, zaten tümleşik hello modülü ve planı toopush Google Play cihazlara ulaşmak yararlıdır. Lütfen ilk nasıl okuyun, uygulamanızda toointegrate Reach kampanyaları tooIntegrate Engagement Reach android'de.
> 
> 

## <a name="introduction"></a>Giriş
GCM tümleştirme gönderilir, uygulama toobe sağlar.

Toohello SDK her zaman gönderilen GCM yüklerini içeren hello `azme` hello veri nesnesindeki anahtar. Böylece, uygulamanızda başka bir amaçla GCM kullanırsanız, bu anahtarı temel iter filtreleyebilirsiniz.

> [!IMPORTANT]
> Yalnızca Android 2.2 çalıştıran cihazlar veya üzeri yüklü ve Google sahip Google Play sahip etkin arka plan bağlantı GCM; kullanarak gönderilemez Ancak, bu kod cihazlarda (yalnızca hedefleri'ı kullanır) güvenli bir şekilde desteklenmeyen tümleştirebilirsiniz.
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a>API anahtarıyla Google Cloud Messaging projesi oluşturma
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a>SDK tümleştirmesi
### <a name="managing-device-registrations"></a>Cihaz kayıtlarını yönetme
Her bir cihaz kayıt komutu toohello Google sunucularına göndermesi gerekir, aksi halde bunlar ulaşılamıyor.

Bir cihaz da GCM bildirimleri (Merhaba uygulaması kaldırılırsa hello cihaz otomatik olarak kaydettirilmemiş) kaydını kaldırabilirsiniz.

Kullanmazsanız [Google Play SDK] veya, zaten hello kayıt hedefi kendiniz gönderme, hello aygıt sizin için otomatik olarak kaydedilecek katılım yapabilirsiniz.

tooenable bunu tooyour aşağıdaki hello eklemek `AndroidManifest.xml` hello içinde dosya `<application/>` etiketi:

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Kayıt Kimliği toohello katılım gönderme hizmeti iletişim ve bildirimlerin
Sipariş toocommunicate hello kayıt kimliğinde hello aygıt toohello katılım anında hizmet ve kendi bildirimleri almak, tooyour aşağıdaki hello eklemeniz `AndroidManifest.xml` hello içinde dosya `<application/>` (cihaz kayıtları kendiniz yönettiğiniz olsa bile) etiketi:

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

Aşağıdaki izinleri de hello olduğundan emin olun, `AndroidManifest.xml` (Merhaba sonra `</application>` etiketi).

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>GRANT Mobile Engagement erişimi tooyour GCM API anahtarı
İzleyin [bu kılavuzda](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement erişimi tooyour GCM API anahtarı.

[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start
