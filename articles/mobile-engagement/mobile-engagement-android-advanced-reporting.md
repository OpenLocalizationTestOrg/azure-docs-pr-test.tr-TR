---
title: "Raporlama seçenekleri için Azure Mobile Engagement Android SDK aaaAdvanced"
description: "Nasıl toodo raporlama toocapture analizi için Azure Mobile Engagement Android SDK Gelişmiş açıklar"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a>Gelişmiş Android katılım ile raporlama
> [!div class="op_single_selector"]
> * [Evrensel Windows](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

Bu konuda, Android uygulamanızdaki ek raporlama senaryolar açıklanmaktadır. Hello oluşturulan bu seçenekleri toohello uygulaması uygulayabilirsiniz [Başlarken](mobile-engagement-android-get-started.md) Öğreticisi.

## <a name="prerequisites"></a>Ön koşullar
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

Başlangıç Öğreticisi, tamamlandı kasıtlı olarak doğrudan ve basit ancak Gelişmiş seçebileceğiniz seçenekleri.

## <a name="modifying-your-activity-classes"></a>Değiştirme, `Activity` sınıfları
Merhaba, [Başlarken Öğreticisi](mobile-engagement-android-get-started.md), tüm toodo sahip olan toomake, `*Activity` alt sınıfların devral hello karşılık gelen `Engagement*Activity` sınıfları. Örneğin, eski etkinliklerinizi Genişletilmiş `ListActivity`, genişletme yapacağı `EngagementListActivity`.

> [!IMPORTANT]
> Kullanırken `EngagementListActivity` veya `EngagementExpandableListActivity`, emin olun herhangi bir çağrıda çok`requestWindowFeature(...);` hello çağrısından önce çok yapılan`super.onCreate(...);`, aksi halde bir kilitlenme oluşur.
> 
> 

Bu sınıfların hello bulabilirsiniz `src` klasörünü ve bunları projenize kopyalayabilirsiniz. Merhaba sınıflardır ayrıca hello **JavaDoc**.

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Alternatif yöntem: çağrı `startActivity()` ve `endActivity()` el ile
Olamaz ya da toooverload istiyor musunuz, `Activity` sınıfları, bunun yerine başlatabilir ve hello çağırarak etkinliklerinizi bitiş `EngagementAgent`'s doğrudan yöntemleri.

> [!IMPORTANT]
> Merhaba Android SDK hiçbir zaman hello çağırır `endActivity()` Merhaba uygulaması kapalı olduğunda bile yöntemi (Android, uygulamaları hiçbir zaman kapalı). Bu nedenle, olan *yüksek oranda* toocall hello önerilen `startActivity()` hello yönteminde `onResume` , geri çağırma *tüm* etkinlikleri ve hello `endActivity()` hello yönteminde `onPause()` geri arama, *tüm* etkinliklerinizi. Bu hello tek yolu toobe oturumları sızdırılmaz emin olur. Bir oturum sızmasını varsa (bir oturum bekleyen olduğu sürece hello hizmet bağlı kalır bu yana) hello katılım hizmet hiçbir zaman hello katılım arka ucundan bağlantısını keser.
> 
> 

Örnek aşağıda verilmiştir:

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

Bu örnekte, benzer toohello `EngagementActivity` sınıfı ve kaynak kodu hello sağlanan türevleri `src` klasör.

## <a name="using-applicationoncreate"></a>Application.onCreate() kullanma
Yerleştirdiğiniz içinde herhangi bir kod `Application.onCreate()` ve başka bir uygulamada geri aramalar hello katılım hizmeti dahil olmak üzere tüm uygulama işlemleri için çalıştırılır. Gereksiz bellek ayırma ve hello Engagement'ın işlemdeki iş parçacıklarını gibi istenmeyen yan etkileri olabilir veya yinelenen yayın alıcıları veya hizmetleri.

Geçersiz kılarsanız `Application.onCreate()`, aşağıdaki kod parçacığını hello başında hello ekleme öneririz, `Application.onCreate()` işlevi:

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

Yapabileceğiniz hello aynı şeyi `Application.onTerminate()`, `Application.onLowMemory()`, ve `Application.onConfigurationChanged(...)`.

Ayrıca genişletebilirsiniz `EngagementApplication` genişletme yerine `Application`: geri çağırma hello `Application.onCreate()` işlem denetimi ve çağrıları hello `Application.onApplicationProcessCreate()` hello geçerli işlem hello bir barındırma hello katılım hizmeti değil ise, hello aynı kuralları için yalnızca uygulama diğer geri aramalar hello.

## <a name="tags-in-hello-androidmanifestxml-file"></a>Merhaba AndroidManifest.xml dosyasında etiketleri
Merhaba hizmet etiketine hello AndroidManifest.xml dosyasında hello `android:label` özniteliği verir toochoose hello hello katılım hizmet adını tooend kullanıcıların telefonlarını hello "Çalışan hizmetleri" ekranında göründüğü gibi. Bu öznitelik çok ayar önerilen`"<Your application name>Service"` (örneğin, `"AcmeFunGameService"`).

Belirten hello `android:process` özniteliği (katılım aynı işlemi, uygulamanızın ana/kullanıcı Arabirimi iş parçacığı potansiyel olarak daha az yanıt getirir hello çalıştıran) kendi işleminde katılım hizmeti çalıştığında bu hello sağlar.

## <a name="building-with-proguard"></a>ProGuard ile oluşturma
Uygulama paketinizi ProGuard ile yapılandırdıysanız, bazı sınıfları tookeep gerekir. Yapılandırma parçacığını aşağıdaki hello kullanabilirsiniz:

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
