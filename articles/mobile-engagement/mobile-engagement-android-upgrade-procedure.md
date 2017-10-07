---
title: "aaaAzure Mobile Engagement Android SDK tümleştirmesi"
description: "En son güncelleştirmeler ve yordamlar için Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a>Yükseltme yordamları
Uygulamanıza bizim SDK daha eski bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükseltirken aşağıdaki tooconsider hello sahip.

Merhaba SDK çeşitli sürümleri eksik birkaç yordamları toofollow olabilir. 1.4.0 geçirirseniz örneğin hello izleyin toofirst sahip too1.6.0 "1.4.0 gelen too1.5.0" yordamı sonra hello "1.5.0 gelen too1.6.0" yordamı.

Yükseltme, seçtiğiniz hello sürüm tooreplace hello sahip `mobile-engagement-VERSION.jar` hello yeni bir tane ile.

## <a name="from-420-too421"></a>4.2.0 gelen too4.2.1
Bu adım gerçekte herhangi bir hello SDK sürümünde yapılabilir, ulaşma etkinlikleri tümleştirdiğinizde güvenlik geliştirme olur.

Şimdi eklemelisiniz `exported="false"` tooall ulaşma etkinlikler.

Reach etkinlikleri şimdi şöyle görünmelidir, `AndroidManifest.xml`:

            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

## <a name="from-400-too410"></a>4.0.0 gelen too4.1.0
Merhaba SDK şimdi tanıtıcı yeni izni modelden Android M.

Konum özelliklerini kullanmak veya büyük resmi bildirimleri okuyun [Bu bölümde](mobile-engagement-android-integrate-engagement.md#android-m-permissions).

Ayrıca toohello yeni izni modeli şimdi konum özelliklerini çalışma zamanında yapılandırma destekliyoruz.
Biz yine hello bildirimi parametreleri konumu için uyumludur, ancak artık kullanılmıyor. Kaldır hello aşağıdaki toouse çalışma zamanı yapılandırması, bölümler, ``AndroidManifest.xml``:

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

okuyup [bu güncelleştirilmiş yordamı](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse çalışma zamanı yapılandırma yerine.

## <a name="from-300-too400"></a>3.0.0 gelen too4.0.0
### <a name="native-push"></a>Yerel gönderim
İtme kampanya herhangi bir türde hello yerel gönderim kimlik bilgilerini yapılandırmak için yerel gönderim (GCM/ADM) şimdi de için uygulama içi Bildirimlerde kullanılır.

Aksi halde zaten Lütfen izleyin [bu yordamı](mobile-engagement-android-integrate-engagement-reach.md#native-push).

### <a name="androidmanifestxml"></a>AndroidManifest.xml
Reach tümleştirme değiştirildi ``AndroidManifest.xml``.

Bu değiştirin:

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

Tarafından

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>
    <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
      <intent-filter>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
      </intent-filter>
    </receiver>

Yapıldığında büyük olasılıkla yükleme ekran şimdi duyuru (metin/web içerik ile) ya da bir yoklama tıklatın.
Tooadd bu bu Kampanyalar toowork 4.0.0 içinde olan:

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a>Kaynaklar
Merhaba yeni katıştırmak `res/layout/engagement_loading.xml` projenize dosya.

## <a name="from-240-too300"></a>2.4.0 gelen too3.0.0
Merhaba toomigrate'nın Azure Mobile Engagement tarafından desteklenen bir uygulamaya bir SDK tümleştirmesi hello Capptain hizmet gelen Capptain SAS tarafından nasıl sunulan açıklanmıştır. Önceki bir sürümünden geçiş yapıyorsanız, lütfen hello Capptain web sitesi toomigrate too2.4.0 ilk bakın ve hello aşağıdaki yordamı uygulayın.

> [!IMPORTANT]
> Capptain ve Mobile Engagement değil hello aynı hizmetler ve nasıl toomigrate hello istemci uygulamasını yalnızca vurgular verilen yordamı hello. Geçirme hello SDK hello uygulama verilerinizi hello Capptain sunucuları toohello Mobile Engagement sunucularından geçişi YAPILMAZ.
> 
> 

### <a name="jar-file"></a>JAR dosyasını
Değiştir `capptain.jar` tarafından `mobile-engagement-VERSION.jar` içinde `libs` klasörü.

### <a name="resource-files"></a>Kaynak dosyaları
Bizim sağladığımız her kaynak dosyası (önüne `capptain_`) sahip toobe yerine yenilerini hello tarafından (önekine sahip `engagement_`).

Bu dosyaları özelleştirdiyseniz, toore sahip-özelleştirme hello yeni dosyalarda uygulamak **hello kaynak dosyalarında tüm hello tanımlayıcıları da yeniden adlandırıldığı**.

### <a name="application-id"></a>Uygulama Kimliği
Şimdi katılım bir bağlantı dizesi tooconfigure hello SDK tanımlayıcıları hello uygulama tanımlayıcısı gibi kullanır.

Toouse sahip `EngagementAgent.init` Başlatıcısı etkinliklerinizi şöyle yöntemi:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

Merhaba bağlantı dizesi, uygulamanız için Azure portalında görüntülenir.

Lütfen herhangi bir çağrısına çok kaldırın`CapptainAgent.configure` olarak `EngagementAgent.init` o yöntemi değiştirir.

Merhaba `appId` artık kullanılarak yapılandırılabilir `AndroidManifest.xml`.

Lütfen bu bölümünden kaldırın, `AndroidManifest.xml` , varsa:

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a>Java API’si
Her çağrı tooany Java sınıfı bizim SDK'sının yeniden adlandırılmış toobe; yine de sahip istiyor musunuz? Örneğin, `CapptainAgent.getInstance(this)` kaydedilmelidir `EngagementAgent.getInstance(this)`, `extends CapptainActivity` kaydedilmelidir `extends EngagementActivity` vb....

Varsayılan aracı tercih dosyalarını ile tümleşik hello varsayılan dosya adı şimdi varsa, `engagement.agent` ve başlangıç anahtarı `engagement:agent`.

Web duyuruları oluştururken hello Javascript bağlayıcı sunulmuştur `engagementReachContent`.

### <a name="androidmanifestxml"></a>AndroidManifest.xml
Çok sayıda değişiklik vardır oldu, hello hizmeti artık paylaşılmayan ve alıcıları çok değildir verilebilir artık.

Merhaba hizmet bildirimi artık daha kolaydır; Merhaba hedefi filtre ve içindeki tüm meta veri kaldırıp eklemek `exportable=false`.

Ayrıca, yeniden adlandırılmış toouse katılım gereken her şey vardır.

Şimdi gibi görünüyor:

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

Tooenable test günlüklerinin istediğinizde hello meta verileri artık bırakıldı toohello uygulama etiketi taşınır ve yeniden adlandırıldı:

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

Tüm diğer meta verileri yalnızca yeniden adlandırıldığı, hello tam listesi (kullandığınız Elbette yeniden adlandırma yalnızca hello olanlar) aşağıdadır:

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

Google Play ve SmartAd izleme kaldırıldı SDK'dan yalnızca tooremove bu değişikliği gerekir:

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

Merhaba ulaşma etkinlikleri şöyle bildirilir:

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

Özel erişim etkinlikler varsa, yalnızca toochange hello hedefi Eylemler toomatch ya da ihtiyacınız `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` veya `com.microsoft.azure.engagement.reach.intent.action.POLL`.

Merhaba yayın alıcıları yeniden adlandırıldığı artı şimdi eklediğimiz `exported=false`. Merhaba yeni belirtimi (kullandığınız Elbette yeniden adlandırma yalnızca hello olanlar) hello alıcılarla hello tam listesi aşağıdadır:

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

Bu bölümde tooremove alacak şekilde alıcı izleme kaldırıldı:

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

Uygulamanıza hello Hello bildirimi alıcı yayın Not **EngagementMessageReceiver** hello değişti `AndroidManifest.xml`. Bu hello API toosend ekleme ve kaldırma rasgele XMPP rasgele XMPP varlıklardan iletileri olduğundan ve API toosend hello ve cihazlar arasında iletilerini kaldırıldı. Ayrıca bu nedenle, gelen geri aramalar aşağıdaki toodelete hello vardır, **EngagementMessageReceiver** uygulama:

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

ve

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

üzerinde herhangi bir çağrısına silme **EngagementAgent** için:

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

ve

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a>Proguard
Proguard yapılandırma rebranding, kuralları şimdi gibi aradığınız hello tarafından etkilenebilir:

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

