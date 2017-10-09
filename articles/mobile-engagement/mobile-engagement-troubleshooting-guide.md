---
title: "aaaAzure Mobile Engagement sorun giderme kılavuzları"
description: "Azure Mobile Engagement için sorun giderme kılavuzu"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 31134a29-a513-4e5e-b626-f6cf6fe04769
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: dd69bfd7019907c3e1da8df590db3b5f61606173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---troubleshooting-guide"></a>Azure Mobile Engagement - Sorun Giderme Kılavuzu
## <a name="introduction"></a>Giriş
sorun giderme kılavuzu izleyerek hello nedenlerini bazı yaygın olarak görülen sorunlar ve tootroubleshoot kendi etkinleştirmek anlamanıza yardımcı olur. 

## <a name="general"></a>Genel
Genel olarak, her zaman hello aşağıdakilerden emin olmalısınız:

1. Tüm hello adımlarında açıklandığı gibi tümleştirme için gereken ilerlemiş sağlamak bizim [başlama öğreticileri](mobile-engagement-windows-store-dotnet-get-started.md)
2. Merhaba hello platform SDK'ları en son sürümünü kullanıyorsunuz. 
3. Bazı sorunlar yalnızca belirli tooemulator olduğundan gerçek bir cihaza hem bir öykünücü sınayın. 
4. Tüm sınırları/belgelenen kısıtlamaları Mobile Engagement gelen basarsa değil [burada](../azure-subscription-service-limits.md)
5. Mümkün değilse tooconnect toohello Mobile Engagement arka uç veya sürekli olarak yüklenen olmayan verileri görmesini hizmet sonra devam eden hizmet olay denetleyerek emin [burada](https://azure.microsoft.com/status/)

## <a name="monitor-issues"></a>'İzleyici' sorunları
### <a name="i-am-not-seeing-my-device-showing-up-on-hello-monitor-tab"></a>Merhaba monitör sekmesinde gösteren cihazımı görüyorum değil
İzleyici sekmesi hello aygıtları bağlı tooyour Mobile Engagement platformu gerçek zamanlı olarak gösterir. Bir öykünücü ve cihaz ayıkladığınız, burada en az bir oturum görmeniz gerekir. Ardından Hello uygulama dağıtılıyorsa hello ölçer yansıtacak gerçek zamanlı bağlı toohello platformu olan hello aygıtları etkin oturumları görürsünüz. 

Ardından, aygıtınızı hello monitör sekmesinde görmüyorsanız büyük olasılıkla bir SDK tümleştirme sorunu olduğunu. Bazı ortak adımlar tootake tootroubleshoot aşağıdaki gibidir:

1. Merhaba mobil uygulamasında hello doğru bağlantı dizesini kullanarak ve hello SDK anahtarları bölümüne ve değil hello API anahtarları bölümüne olduğundan emin olun. Merhaba bağlantı dizesi, mobil uygulama toohello örneğiniz hello monitör sekmesinde Cihazınızı yazısını görürsünüz hello Mobile Engagement uygulaması bağlanır. 
2. Windows platformu - sayfanızı hello kılıyorsa için `OnNavigatedTo` yöntemi, yapma emin toocall `base.OnNavigatedTo(e)`.
3. Mevcut mobil uygulamaya Mobile Engagement tümleştirme sonra size herhangi bir adım tümleştirme adımları Gelişmiş hello bakarak eksik değil olduğunu sağlayabilirsiniz [burada](mobile-engagement-windows-store-integrate-engagement.md)
4. Gönderdiğiniz en az bir ekran/etkinlik EngagementActivity hello sayfasıyla çalıştığınızı hello açıklandığı gibi hello platformu bağlı olarak geçersiz kılarak olun [başlama öğreticileri](mobile-engagement-windows-store-dotnet-get-started.md).

### <a name="i-am-seeing-hello-monitor-tab-showing-a-session-even-when-i-have-disconnected-or-closed-my-app-emulator"></a>Bir oturum gösteren hello İzleyici sekmesi görüyorum bile zaman ı bağlantısı kesilmiş veya Uygulamam kapalı / öykünücüsü.
Bu noktada olduğunuz hello yalnızca bir bağlı toohello platform ve bir öykünücü tooopen hello uygulama kullanıyorsanız sonra bu tooemulator quirks olasıdır. Genel olarak, size geri hello uygulama oturumu toodisconnect hello öykünücüsü toohello giriş ekranında başarıyla geldiğini tooensure gerekir. Ayrıca, Windows platformunda, Visual Studio ile hata ayıklama sırasında Visual Studio'da, toohello gidin tooensure gerekebilir **yaşam döngüsü olayları** menü çubuğu ve tıklayarak **askıya alma** tooreally kapatın Merhaba oturumu. Bkz: [Windows öğretici](mobile-engagement-windows-store-dotnet-get-started.md) Ayrıntılar için. 

## <a name="analytics-issues"></a>'Analytics' sorunları
### <a name="i-am-not-seeing-any-data-refreshed-data-on-analytics-tab"></a>Herhangi bir veri görmüyorum / Analytics sekmesinde verilerin yenilenmesi
Analiz verileri düzenli olarak hesaplanır ve bu yenileme 24 saatten fazla sürebilir. Bu verileri gerçek zamanlı değildir ve bu 24 saatlik süre içinde yenilenir görürsünüz.
Lütfen ancak, en az bir ekran veya etkinlik toohello platform arka uç tarafından ya da geçersiz kılma en az bir sayfayla gönderdiğinizden emin olmak `EngagementActivity` veya çağırma `SendActivity` explcitly. 

### <a name="i-am-seeing-incorrectly-captured-datetime-for-a-device-on-hello-analytics-tab"></a>Bir aygıt için yanlış yakalanan tarih/saat hello Analytics sekmesinde görüyorum
Merhaba süre analiz için hello kullanıcı cihaz ayarları hello tarihinden temel alır. Bu nedenle bu hello olun aygıtın hello tarih doğru olarak ayarlanmış. 

## <a name="segment-issues"></a>'Segment' sorunları
### <a name="i-created-a-segment-and-it-is-showing-up-as-greyed-out-or-not-showing-any-data"></a>Bir segment oluşturup ve devre dışı olarak gösteren veya tüm veriler gösterilmiyor
Segment oluşturma hello şu anda gerçek zamanlı değildir. Merhaba aynı hello analiz verileri toplanır ve 24 saatten fazla sürebilir şekilde zaman hesaplanır. Daha sonra yeniden Buraya, ancak bu sırada Ayrıca hangi hello kesimleri oluşturan hello temelinde hello veri, mobil uygulamalarınızın gerçekten gönderiyor emin olmalısınız. Örneğin bir olay 'foo' herhangi bir mobil aygıtı tarafından gönderilen değil sonra EventName ile oluşturulan bir kesim için herhangi bir segment veri olmayacaktır olması söylediğinizde foo hello ölçüt olarak =. SDK tümleştirmesi tooensure de denetlemelisiniz mobil uygulamanızı hello veri doğru gönderiyor. 

## <a name="reach-or-push-notifications-issues"></a>'Ulaşmak' ya da anında iletme bildirimleri sorunları
### <a name="my-push-messages-are-not-being-delivered"></a>My anında iletileri teslim edilmiyor
1. Tüm hello bileşenleri - mobil uygulama, SDK'sı ve hello hizmet doğru şekilde bağlandığını ve mümkün toodeliver anında iletme bildirimleri olduğunu bildirimleri tooa test cihaz ilk tooensure göndermeyi deneyin. 
2. Her zaman hello basit 'uygulamasının, çıkış bildirim' ilk değil zamanlanan bir kampanya göndermek ve ya da belirtilen tüm hedef kitle ölçütünün sahiptir. Yeniden bildirim bağlantısının düzgün çalıştığını tooprove budur. 
3. Karşılaştığınız sorunları da iyi bir ise uygulama bildirimleri teslim ilk önce bir uygulama bildirim göndererek tootry adım. 
4. Bu hello 'Yerel gönderim' mobil uygulamanız için doğru bir şekilde yapılandırıldığından emin olun. Merhaba platformuna bağlı olarak, ya da anahtarları (Android, Windows) veya sertifikaları (iOS) içerir. Bkz: [kullanıcı arabirimi - ayarlar](mobile-engagement-user-interface-settings.md)
5. Bildirimler ayrıca tarafından hello önlenebilir uygulama dışı kullanıcı mobil işletim sistemi bu nedenle bu emin hello aracılığıyla hello durumda değil. 
6. Hello ayarı bulunamadı sağlamak *yoksay hedef kitle, anında iletme toousers hello API üzerinden gönderilecek* hello seçeneğinde **kampanya** bölümünde bir Reach kampanya bu durum, bu itme güvence altına alır çünkü bildirimleri Yalnızca API gönderilebilir. 
7. WIFI ve telefon işleci ağ tooeliminate hello ağ bağlantı sorunlarının olası bir kaynak olarak üzerinden bağlanan her iki bir aygıt ile anında iletme kampanyanızı test ettiğinizden emin olun.
8. Merhaba sistem olun tarih aygıt/öykünücüsü üzerinde olduğundan doğru eşitlenmemiş herhangi bir aygıt ile Merhaba anında iletilen bildirim hizmetin özelliği toodeliver bildirimleri çalışmasını engeller. 

Daha fazla platforma aşağıdaki yönergeleri sorunlarını giderme:

1. **iOS** 
   
   * Merhaba sertifikaların geçerli ve süresi dolmamış iOS anında iletme bildirimleri için olduğundan emin olun. 
   * Doğru şekilde yapılandırdığınızdan emin olun bir *üretim* Mobile Engagement uygulamanız sertifikada. 
   * Üzerinde test ettiğinizden emin olun bir *gerçek, fiziksel aygıt.* Merhaba iOS simülatörü anında iletme iletileri işleyemez.
   * Bu hello paket tanımlayıcısı hello mobil uygulamasında doğru yapılandırıldığından emin olun. Merhaba yönergelere bakın [burada](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)
   * Test ederken "Geçici" dağıtım mobil sağlama profilinizde kullanın. "Hata ayıklama" kullanarak uygulamanızı derlenmiş ise mümkün tooreceive bildirim olmaz
2. **Android**
   
   * \N karakterin ardından mobil uygulamanızın AndroidManifest.xml dosyasında hello doğru proje numarası belirttiğinizden emin olun. 
     
           <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
   * Eksik olmayan veya tüm izinleri hello Android derleme bildirimi dosyasında yanlış yapılandırdığınızdan emin olun 
   * Merhaba proje numarası tooyour istemci uygulaması eklemekte olduğunuz aynı hello GCM Server anahtarını burada aldığınız hesap hello olduğundan emin olun. Hello iki arasında bir uyuşmazlık, gönderim çıkmasını önler. 
   * Sistem alıyorsanız bildirimleri ancak değil hello gözden uygulama [bildirimler bölümü için bir simge belirtin](mobile-engagement-android-get-started.md) olarak olasılıkla hello doğru simge hello Android derleme bildirimi dosyasında belirtiyorsanız değil. 
   * Bir BigPicture bildirim göndererek, ardından olması durumunda emin olun, dış görüntü sunucularına sahip sonra toobe mümkün toosupport HTTP ihtiyaç duydukları "GET" ve "HEAD".
3. **Windows**
   
   * Geçerli bir Windows mağazası uygulaması ile ilişkili hello uygulama emin olun. Visual Studio'da - hello proje tıklayın ve "Uygulama mağazası ile ilişkilendirme" seçeneğini seçip hello Windows mağazası oluşturulan select hello uygulaması tooright sahip olur. Bu Windows mağazası uygulaması hello yerel gönderim kimlik bilgilerini tooconfigure hello Mobile Engagement portalında burada aldığınız gelen hello aynı olmalıdır.
   * App anında iletme bildirimleri ancak olmayan uygulama bildirimlerle alıyorsanız `EngagementOverlay` sonra tümleştirme sayfanızda bir kök kılavuz öğesi olduğundan emin olun. EngagementOverlay hello görünümlerde, xaml dosyası tooadd iki web sayfanızda bulduğu ilk "Kılavuz" öğesini kullanır. Burada web görünümleri ayarlanacak toolocate istiyorsanız, bu gibi tooensure sahip olur ancak "EngagementGrid" adlı bir kılavuz tanımlayabilirsiniz yeterli yükseklik yoktur ve genişliği hello için sonraki iki web hello bildirim göster ve aşağıdaki hello görünümler uygulama içi bildirim olarak Duyurusu:
     
           <Grid x:Name="EngagementGrid"></Grid>

### <a name="i-created-a-push-notificationannouncement-campaign-and-even-after-it-sent-me-hello-notification-it-is-showing-as-active-what-does-it-mean"></a>Bir anında iletme bildirimi/duyuru oluşturulan/kampanya ve hatta Bunu bana hello bildirim gönderdikten sonra 'Etkin' olarak gösteriyor. Ne anlama geliyor?
Merhaba **kampanya** Mobile Engagement içinde oluşturulan yeni aygıtları tooyour mobil katılım platform bağlandıkları, uzun süre çalışan bir anında iletme bildirimi anlamı olduğundan, bunlar otomatik olarak hello bildirim gönderilir şekilde çağrılır Merhaba kampanya ayarladığınız hello ölçütü karşılayan sürece, burada yapılandırın. Tek bir çekim tek bildirim kurulu değil budur. Hello üzerinde tıklatın toomanually olacaktır **son** düğmesini tooterminate hello kampanya böylece daha fazla bildirim göndermez. 

### <a name="i-created-a-push-campaign-and-i-am-receiving-notifications-successfully-however-whenever-i-open-up-hello-app-i-get-hello-same-notification-even-when-i-had-actioned-it-before"></a>Anında iletme kampanya oluşturulan ve bildirimler başarıyla ancak hello uygulamasını açtığınızda, hello elde alıyorum bile ı işleme alınan varken aynı bildirim önce?
Test sırasında büyük olasılıkla toohappen ve Öykünücüler veya TestFlight gibi bazı test Framework'te kullanıyorsanız budur. Neler olduğuna dair örneği çalıştıran her uygulamanın olduğundan yeni bir cihaz kimliği alınırken ve hello Mobile Engagement platformu tootreat neden tooour arka uç göndermeden, işte bunu yeni bir cihaz ve hello bildirim göndererek olarak. 

## <a name="getting-support"></a>Destek alma
Kendiniz oluşturulamıyor tooresolve hello sorun varsa şunları yapabilirsiniz:

1. İş parçacıklarında hello varolan StackOverflow Forumunda sorununuz için arama ve [MSDN Forumu](https://social.msdn.microsoft.com/Forums/windows/en-US/home?forum=azuremobileengagement) ve değil sonra var. bir soru sorun. 
2. Üzerinde sonra ekleme/oy hello istek için eksik bir özellik bulursanız bizim [UserVoice Forumu](https://feedback.azure.com/forums/285737-mobile-engagement/)
3. Microsoft destek açık bir destek olayını aşağıdaki ayrıntılara hello sağlayarak varsa: 
   * Azure abonelik kimliği
   * Platform (örn. iOS, Android vb.)
   * Uygulama Kimliği
   * Kampanya kimliği (için anında iletme bildirimi sorunları)
   * Cihaz Kimliği
   * Mobile Engagement SDK'sı sürüm (örneğin Android SDK v2.1.0)
   * Hata ayrıntılarını tam hata iletisi ve senaryosu

