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
# <a name="how-toointegrate-adm-with-engagement"></a>Nasıl tooIntegrate ADM engagement
> [!IMPORTANT]
> TooIntegrate android'de katılım nasıl belge bu kılavuzu izlemeden önce hello açıklanan hello tümleştirme yordamı izlemeniz gerekir.
> 
> Bu belge, yalnızca hello Reach modülü ve planı toopush Amazon cihazları zaten bütünleştirdiyseniz yararlıdır. Lütfen ilk nasıl okuyun, uygulamanızda toointegrate Reach kampanyaları tooIntegrate Engagement Reach android'de.
> 
> 

## <a name="introduction"></a>Giriş
ADM tümleştirme Amazon Android cihazları hedeflerken gönderilir, uygulama toobe sağlar.

ADM yüklerini toohello SDK her zaman gönderilen içeren hello `azme` hello veri nesnesindeki anahtar. Böylece, uygulamanızda başka bir amaçla ADM kullanırsanız, bu anahtarı temel iter filtreleyebilirsiniz.

> [!IMPORTANT]
> Android 4.0.3 çalıştıran yalnızca Amazon Kindle cihazlar veya Amazon Device Messaging; yukarıdaki desteklenir Ancak, bu kod diğer aygıtlarda güvenli bir şekilde tümleştirilebilir.
> 
> 

## <a name="sign-up-tooadm"></a>TooADM oturum
Yapmadıysanız, Amazon hesabınızdaki ADM etkinleştirmeniz gerekir.

Merhaba yordamı ayrıntılı adresindeki: [ <https://developer.amazon.com/sdk/adm/credentials.html>].

Merhaba yordamı tamamladıktan sonra alın:

* OAuth (istemci kimliği ve istemci parolasını) katılım toobe mümkün toopush için cihazlarınızı kimlik bilgileri.
* Uygulamanıza tümleşik bir API anahtarı.

## <a name="sdk-integration"></a>SDK tümleştirmesi
### <a name="managing-device-registrations"></a>Cihaz kayıtlarını yönetme
Her bir cihaz kayıt komutu toohello ADM sunucuları göndermesi gerekir, aksi halde bunlar ulaşılamıyor.

Merhaba zaten kullanıyorsanız [ADM istemci Kitaplığı]ve zaten [ADM tümleşik] tooandroid-sdk-adm-alma doğrudan gidebilirsiniz.

ADM entegre edilemez henüz katılım daha basit bir şekilde tooenable sahip değilse, uygulamanızın içinde:

Düzenleme, `AndroidManifest.xml` dosyası:

* Amazon ad Merhaba, hello dosya şu şekilde başlaması gereken ekleyin:
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* İç hello `<application/>` etiketi, bu bölümde ekleyin:
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* Proje derleme hedefi Android 2.1 ise hello amazon etiketi eklendikten sonra bir derleme hatası olabilir. Toouse sahip bir **Android 2.1 +** hedef yapı (endişelenmeyin, hala sahip bir `minSdkVersion` too4 ayarlayın).
* Merhaba ADM API anahtarı izleyerek bir varlık tümleştirmek [bu yordamı].

Ardından hello sonraki bölümleri hello yönergeleri izleyin.

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Kayıt Kimliği toohello katılım gönderme hizmeti iletişim ve bildirimlerin
Sipariş toocommunicate hello kayıt kimliğinde hello aygıt toohello katılım anında hizmet ve kendi bildirimleri almak, tooyour aşağıdaki hello eklemeniz `AndroidManifest.xml` hello içinde dosya `<application/>` (ADM katılım olmadan kullanmak olsa bile) etiketi:

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

Aşağıdaki izinleri de hello olduğundan emin olun, `AndroidManifest.xml` (Merhaba önce `</application>` etiketi).

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a>GRANT katılım OAuth kimlik bilgileri
OAuth kimlik bilgilerinizi (istemci kimliği ve istemci gizli anahtarı) Engagement portalında gönderin.

[< https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[ADM istemci Kitaplığı]:https://developer.amazon.com/sdk/adm/setup.html
[ADM tümleşik]:https://developer.amazon.com/sdk/adm/integrating-app.html
[bu yordamı]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
