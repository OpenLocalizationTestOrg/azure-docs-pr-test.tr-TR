---
title: "aaaAzure Notification Hubs - tanılama yönergeleri"
description: "Yönergeler, nasıl Azure Notification Hubs ile toodiagnose ortak sorunlar için."
services: notification-hubs
documentationcenter: Mobile
author: ysxu
manager: erikre
editor: 
ms.assetid: b5c89a2a-63b8-46d2-bbed-924f5a4cce61
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: NA
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: e374278f2bfdfad36ba091e8846059cd184c17ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs---diagnosis-guidelines"></a>Azure Notification Hubs - tanılama yönergeleri
## <a name="overview"></a>Genel Bakış
Merhaba en yaygın sorular yeterli yanıt Azure Notification Hubs müşterilerden biri neden kendi uygulama arka ucundan gönderilen bir bildirim görmüyorum çıkışı toofigure hello istemci aygıtında - görüntülenme nerede ve neden bildirimleri bırakılan ve nasıl toofix bu. Bu makalede hello neden bildirimleri bırakılan veya bitmeyen çeşitli nedenlerle hello cihazlarda ele alacağız. Biz çözümlemek ve hello kök nedenini anlamak yolu üzerinden arar. 

Öncelikle, nasıl Azure Notification Hubs bildirimleri toohello aygıtları iter kritik toounderstand olur.
![][0]

Tipik gönderme bildirim akışı selamlama iletisine hello gönderilen **uygulama arka uç** çok**Azure bildirim hub'ı (NH)** hangi sırayla mu katarak tüm hello kayıtlar üzerindeki bazı işleme Hesap hello etiketleri & Etiket ifadeleri toodetermine "hedefler" yani tooreceive hello anında iletme bildirimi gereken tüm hello kayıtlar yapılandırılmış. Bu kayıtlar herhangi birini veya tümünü bizim desteklenen platformlar - iOS, Google, Windows, Windows Phone yayılabilir Kindle ve Baidu Çin Android için. Merhaba hedefleri kurulan sonra NH sonra gönderim bildirimlerini çıkışı bölme kayıtlar, belirli bir toohello cihaz platformu birden çok toplu arasında **anında bildirim hizmeti (PNS)** -Örneğin, APNS için Apple, Google vb. için GCM. NH hello hello Klasik Azure portalı hello bildirim Hub'ı Yapılandır sayfasında kümesindeki hello kimlik bilgilerini ilgili PNS temel kimlik doğrulamasını. Merhaba PNS sonra hello bildirimleri toohello ilgili iletir **istemci cihazları**. Bu şekilde toodeliver anında iletme bildirimleri ve bildirim teslim hello son leg gerçekleşir hello platform PNS hello aygıt arasındaki Not önerilen hello platformudur. Bu nedenle dört ana bileşen - sahibiz *istemci*, *uygulama arka uç*, *Azure bildirim hub'ları (NH)* ve *anında bildirim Hizmetleri (PNS)* ve bunları herhangi biri kesiliyor bildirimleri neden olabilir. Bu mimarisi hakkında daha fazla bilgi edinilebilir [Notification Hubs'a genel bakış].

Bildirimleri hello ilk sırasında bir yapılandırma sorunu veya gösterebilir aşaması test/hazırlama burada tümünü veya bazılarını bildirimleri hello üretimde oluşabilir oluşabilir hatası toodeliver daha derin bazı uygulama belirten bırakılabilir veya desen sorunu Mesajlaşma. Merhaba bölümünde aşağıda bazıları, belirgin bulabilirsiniz yaygın toohello nadir türü ve diğerlerinin değil çok değişen çeşitli bırakılan bildirimler senaryolar ele alacağız. 

## <a name="azure-notifications-hub-mis-configuration"></a>Azure bildirim hub'ı yanlış yapılandırma
Azure bildirim hub'ları gereken tooauthenticate kendisini hello bağlamda hello geliştiricinin uygulama toobe mümkün toosuccessfully gönderme bildirimleri toohello, ilgili PNS. Bu bir geliştirici hesabını hello ilgili platformun (Google, Apple, Windows vb.) oluşturma ve hello portalında bildirim altında yapılandırılmış toobe gereken kimlik bilgilerini nereden uygulamasına kaydetme hello geliştirici tarafından mümkün hale getirilir Hub'ları yapılandırma bölümü. Bildirim yok, tooensure hello doğru kimlik bilgilerini hello bildirim Hub'ın hello uygulama ile eşleşen yapılandırılan platform özel Geliştirici hesabını altında oluşturulmalıdır ilk adım, üzerinden yapıyorsanız. Size bizim [Başlarken öğreticilerine alma] bu işlemi adım adım şekilde üzerinde yararlı toogo. Bazı sık karşılaşılan hatalı yapılandırmalar şunlardır:

1. **Genel**
   
    bir) yapma emin bildirim hub adınızı (olmadan, yazım hatalarını) olan Merhaba, aynı:
   
   * Burada hello istemciden kaydediyorsunuz, 
   * Burada hello arka ucundan bildirim gönderiyorsanız,  
   * Merhaba PNS kimlik yapılandırdığınız ve 
   * Yapılandırdığınız SAS kimlik bilgilerini istemci ve hello arka uç hello. 
     
     b) yapma emin hello istemci ve hello uygulama arka uç hello doğru SAS yapılandırma dizelerini kullanıyorsanız. Altın kural, hello kullanıyor olmanız gerekir **DefaultListenSharedAccessSignature** hello istemcide ve **DefaultFullSharedAccessSignature** (sağlayan izni toobe hello uygulama arka uç üzerinde mümkün toosend bildirim toohello NH)
2. **Apple anında iletilen bildirim servisi (APNS) yapılandırma**
   
    -Bir üretim için iki farklı hub korumalıdır ve test etmek için başka bir amaçla. Başka bir deyişle, sandbox ortamını tooa ayrı hub ve üretim tooa ayrı hub toouse kalacaklarını hello sertifika toouse kalacaklarını hello sertifikası karşıya yükleniyor. Farklı türde sertifikaları toohello tooupload çalışmayın şekliyle aynı hub hello satır aşağı bildirim hataları neden olabilir. Kendiniz Burada, yanlışlıkla yüklediğiniz sertifika toohello farklı türde bir konumda bulursanız, aynı hub toodelete hello hub ve yeni başlangıç önerilir. Herhangi bir nedenle olduğu varsa, mümkün toodelete hello hub sonra hello çok az olup olmadığı, hello hub'ından tüm hello varolan kayıtlarını silmeniz gerekir. 
3. **Google Cloud Messaging (GCM) yapılandırma** 
   
    bir) yapma emin, "Google bulut Mesajlaşma için Android" bulut projenizi altına etkinleştireceğiniz olduğunu. 
   
    ![][2]
   
    b) yapma emin hangi NH hello kimlik bilgileri elde tooauthenticate GCM ile birlikte kullanırken "Sunucu anahtarı" oluşturun. 
   
    ![][3]
   
    c) yapma emin "Proje kimliği" Merhaba panodan edinebilirsiniz tamamen sayısal bir varlık hello istemcide yapılandırdığınız:
   
    ![][1]

## <a name="application-issues"></a>Uygulama sorunları
1) **Etiketler / etiket ifadeleri**

Etiket veya etiket ifadeleri toosegment kitlenizi kullanıyorsanız, her zaman hello bildirimi gönderirken olduğunu gönderme aramanız belirtme hello etiketleri/etiket ifadeleri dayalı bulunan hiçbir hedef mümkündür. En iyi tooreview vardır, kayıtlar tooensure etiketler hangi eşleşme bildirimi gönderdiğinizde ve sonra bu kayıtları ile Merhaba istemcilerden yalnızca hello bildirim giriş doğrulayın. Örneğin Tüm NH, kayıtlarla ile yapıldığını etiketi "Siyaset" söyleyin ve "Spor" etiketi içeren bir bildirim gönderiyorsanız, tooany aygıt gönderilmez. Karmaşık bir durumda, size yalnızca kayıtlı "Etiketi A" veya "Etiketi B" ile ancak bildirimleri gönderilirken etiket ifadeleri ilgili olabilir "Etiketi A & & etiketi B" hedefleme. Hello ipuçları bölümüne otomatik olarak tanılamak, yolları sahiptirler hello etiketlerle birlikte, kayıtları gözden geçirebilirsiniz. 

2) **Şablon sorunları**

Şablonları kullanarak yeniden olun bölümünde anlatıldığı hello yönergeleri izleyerek [şablonu Kılavuzu]. 

3) **Geçersiz kayıtlar**

Doğru toowhich hello bildirimleri gönderilen toobe gereksinim geçerli hedefler hello bulunacak kaynaklanan hello bildirim hub'ı doğru yapılandırıldığından ve tüm etiketleri/etiket ifadeleri kullanılan varsayıldığında, paralel - her bir toplu iş birkaç işleme toplu işlemi kapatmak NH tetikler ileti tooa kayıt kümesine gönderme. 

> [!NOTE]
> Biz paralel işleme hello olduğundan, biz hangi hello bildirimleri teslim edilecek hello sipariş garanti etmez. 
> 
> 

Artık Azure bildirim hub'ı "konumundaki çoğu kez" ileti teslim modeli için optimize edilmiştir. Bu, böylece hiçbir bildirimleri birden çok kez tooa aygıt teslim biz devre dışı bırakma çoğaltma denemesi anlamına gelir. tooensure hello kayıtlar arayın ve yalnızca tek bir iletiyi emin olun gerçekte gönderen hello ileti toohello PNS önce cihaz tanımlayıcısı başına gönderilir. Her toplu toohello sırayla kabul PNS gönderilir ve hello kayıtları doğrulanıyor, o hello PNS bir toplu işlemde bir veya daha fazla hello kayıtlar hatayla algılar mümkündür gibi bir hata tooAzure NH döndürür ve böylece, bırakarak işlemeyi durdurur tamamen toplu. Bu, özellikle bir TCP akışı protokolünü kullanan APNS ile geçerlidir. Konumundaki-çoğu için bir kez iyileştirilmiş ancak bu durumda biz kaldırmak teslim bizim veritabanını ve ardından yeniden deneme bildirim teslimi hello rest toplu hello cihazlar için hataya neden olan kaydından hello.

Hello Azure Notification Hubs REST API'lerini kullanarak bir kayıt karşı hello başarısız teslim girişimi için hata bilgilerini elde edebilirsiniz: [başına ileti Telemetri: bildirim iletisi Telemetri almak](https://msdn.microsoft.com/library/azure/mt608135.aspx) ve [PNS geri bildirim](https://msdn.microsoft.com/library/azure/mt705560.aspx). Merhaba bkz [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) örneğin kod.

## <a name="pns-issues"></a>PNS sorunları
Merhaba bildirim iletisi tarafından alınan sonra kendi sorumluluk toodeliver hello bildirim toohello aygıt ise ilgili PNS hello. Azure bildirim hub'ları burada hello resim dışında ve denetimi olduğunda veya hello bildirim toohello aygıt teslim toobe edecekse yoktur. Hello platform Bildirim Hizmetleri oldukça sağlam olduğundan, bildirimleri tooreach hello cihazları birkaç saniye içinde PNS hello eğilimi gösterir. Merhaba PNS ancak azaltmadır, Azure Notification Hubs bir üstel geri alma stratejisi sonra uygulanır ve hello PNS için 30 dakikalık ulaşılamaz kalırsa sonra tooexpire yerleştirin ve bu iletileri kalıcı olarak bırakma İlkesi sunuyoruz. 

PNS toodeliver bir bildirim çalışır ancak hello cihaz çevrimdışıysa, hello bildirim sınırlı bir süre için PNS hello tarafından depolanır ve kullanılabilir hale geldiğinde toohello aygıt teslim. Belirli bir uygulama için yalnızca bir son bildirim depolanır. Merhaba aygıt çevrimdışı durumdayken birden fazla bildirim gönderiyorsanız, her bir yeni bildirim hello önceki bildirim toobe atılan neden olur. Yalnızca hello yeni bildirim tutmayı bu APNS bildirimleri birleştirmesi ve (hangi çöken bir anahtar kullanan) GCM daraltma başvurulan tooas davranıştır. Merhaba aygıt uzun bir süredir çevrimdışı kalırsa, bunun için depolanmakta herhangi bir bildirim atılır. Kaynak - [APNS Kılavuzu] & [GCM Kılavuzu]

Azure Notification Hubs ile - hello genel kullanarak bir HTTP üstbilgisi birleştirmesi anahtar geçirebilirsiniz `SendNotification` API (.NET SDK – örneğin `SendNotificationAsync`) de olarak geçirilen HTTP üstbilgileri aldığı olan toohello ilgili PNS. 

## <a name="self-diagnose-tips"></a>Kendi kendine tanılamak ipuçları
Merhaba burada inceleyeceğiz bildirim hub'ı sorunları çeşitli anlaşmaya toodiagnose ve kök neden:

### <a name="verify-credentials"></a>Kimlik bilgilerini doğrulama
1. **PNS Geliştirici Portalı**
   
    Merhaba ilgili PNS Geliştirici Portalı (APNS, GCM, WNS vb.) kullanarak doğrulama bizim [Başlarken öğreticilerine alma].
2. **Klasik Azure portalı**
   
    Toohello Yapılandır sekmesi tooreview gidin ve hello PNS Geliştirici Portalı'ndan elde edilenlerle hello kimlik bilgileriyle eşleşmesi. 
   
    ![][4]

### <a name="verify-registrations"></a>Kayıtlar doğrulayın
1. **Visual Studio**
   
    Geliştirme için Visual Studio kullanıyorsanız, ardından tooMicrosoft Azure ve görünüm bağlanabilir ve bildirimler hub'ının "Sunucu Gezgini'nden" dahil olmak üzere Azure hizmetlerinin bir demet yönetin. Bu, geliştirme ve test ortamınız için özellikle yararlıdır. 
   
    ![][9]
   
    Görüntüleyin ve hangi sorunsuz şekilde sınıflandırılır platform, yerel ya da şablon kayıt, etiketler, PNS tanımlayıcısı, hiçbir kayıt kimliği ve hello sona erme tarihi için tüm hello kayıtlar hub'ınızdaki yönetin. Bir kayıt deyin tooedit herhangi bir etiket istiyorsanız kullanışlıdır hello kolay bir şekilde - da düzenleyebilirsiniz. 
   
    ![][8]
   
   > [!NOTE]
   > Visual Studio işlevselliği tooedit kayıtlar yalnızca sınırlı sayıda kayıtlar ile geliştirme ve test sırasında kullanılmalıdır. Toplu olarak, kayıtlar gerek toofix ortaya varsa göz önünde bulundurun açıklanan hello içeri/dışarı aktarma kayıt işlevselliği burada - kullanarak [içeri/dışarı aktarma kayıtlar](https://msdn.microsoft.com/library/dn790624.aspx)
   > 
   > 
2. **Hizmet veri yolu Gezgini**
   
    Birçok müşteri explorer açıklanan ServiceBus burada - kullanmak [ServiceBus Explorer] görüntüleme ve kendi bildirim hub'ı yönetme. Açık kaynaklı proje code.microsoft.com - kullanılabilir olduğu [ServiceBus Explorer kodu]

### <a name="verify-message-notifications"></a>İleti bildirimlerini doğrulayın
1. **Klasik Azure Portalı**
   
    Herhangi bir hizmet arka uçtan yukarı gerek ve çalışan toohello "Hata ayıklama" sekmesini toosend test bildirimleri tooyour istemcileri gidebilirsiniz. 
   
    ![][7]
2. **Visual Studio**
   
    Visual Studio hello comforts test bildirimleri gönderebilirsiniz:
   
    ![][10]
   
    Daha fazla üzerinde hello Visual Studio bildirim hub'ı Azure explorer işlevsellik burada okuyabilirsiniz- 
   
   * [VS Sunucu Gezgini genel bakış]
   * [VS Sunucu Gezgini Blog Gönderisi - 1]
   * [VS Sunucu Gezgini Blog Gönderisi - 2]

### <a name="debug-failed-notifications-review-notification-outcome"></a>Hata ayıklama başarısız bildirimleri / bildirim sonucunu gözden geçirin
**EnableTestSend özelliği**

Bildirim hub'ları aracılığıyla bir bildirim gönderdiğinizde, başlangıçta, yalnızca NH toodo toofigure tüm hedefleri çıkış işleme için sıraya ve ardından sonunda NH toohello PNS gönderir. Bu, REST API veya hello istemci SDK birini kullanırken, hello ileti Merhaba, gönderme çağrı yalnızca anlamına gelir başarılı dönüşünü başarıyla bildirim Hub'sıraya alındı, anlamına gelir. NH sonunda toosend hello ileti tooPNS var olduğunda ne içine bir öngörü vermez. Bildiriminizin hello istemci cihazda ulaşan değil, NH toodeliver hello ileti tooPNS çalıştığında, bir sorun oluştu, örneğin hello yükü boyutu olasılığı PNS hello tarafından izin verilen hello sınırı aştı veya NH içinde yapılandırılmış hello kimlik bilgileri Geçersiz vb. tooget hello PNS hataları bir anlayış bir gösterdiğimizi adlı bir özellik [EnableTestSend özelliği]. Test iletileri hello portal ya da Visual Studio istemcisi ve bu nedenle, ayrıntılı toosee sağlar gönderdiğinizde, bu özelliği otomatik olarak etkin hata ayıklama bilgileri. Eklenen tooall istemci SDK'ları sonunda olur ve bu hello .NET SDK'sı şimdi kullanılabilir olduğunda hello örneği alma API'leri kullanabilirsiniz. toouse bu hello REST çağrısı ile yalnızca Ekle "test" Merhaba gönderme aramanız sonunda örneğin adlı bir sorgu dizesi parametresi 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

*Örnek (.NET SDK)*

.NET SDK'sı toosend yerel bildirim kullandığınız varsayın:

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

`result.State`olur yalnızca durum `Enqueued` hello yürütme ne herhangi bir anlayış olmadan hello sonunda tooyour itme oldu. Artık hello kullanarak `EnableTestSend` hello başlatılırken boolean özelliği `NotificationHubClient` ve hello bildirimi gönderirken hatalarla karşılaştı hello PNS hatalarla ilgili ayrıntılı durum elde edebilirsiniz. NH hello bildirim tooPNS toodetermine hello sonucunu sundu sonra yalnızca döndürmektir çünkü hello gönderme burada çağrısı ek zaman tooreturn olur. 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

*Örnek çıktı*

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    hello Token obtained from hello Token Provider is wrong

Bu ileti geçersiz kimlik bilgileri hello bildirim hub'yapılandırılmış olan veya hello hub ve hello hello kayıtları ile ilgili bir sorunu önerilen indirmelere ve bu kayıt toodelete olması hello göndermeden önce yeniden hello istemci izin gösterir İleti. 

> [!NOTE]
> Bu özellik Hello kullanımı yoğun bir şekilde kısıtlanan ve bu nedenle, yalnızca bu kayıtlar sınırlı sayıda ile geliştirme ve test ortamında kullanmalısınız unutmayın. Biz yalnızca hata ayıklama bildirimlerini too10 aygıtları gönderin. Biz de hata ayıklama gönderir toobe 10 dakika başına işlemenin sınırlaması vardır. 
> 
> 

### <a name="review-telemetry"></a>Telemetri gözden geçirin
1. **Klasik Azure portalını kullanın**
   
    Merhaba portal tooget, bildirim hub'ındaki tüm hello etkinliklerin hızlı bir genel bakış sağlar. 
   
    bir) Merhaba "Pano" sekmesinden platformu başına hatalarının yanı sıra hello kayıtlar, bildirimler birleşik bir görünümünü görüntüleyebilirsiniz. 
   
    ![][5]
   
    b), aynı zamanda birçok diğer platform belirli ölçümleri hello "İzleme" sekmesini tootake NH toosend hello bildirim toohello PNS çalıştığında döndürülen özellikle PNS belirli hataları daha derin göz ekleyebilirsiniz. 
   
    ![][6]
   
    c), hello inceleyerek başlamalısınız **gelen iletileri**, **kayıt işlemleri**, **başarılı bildirimler** ve tooper platform sekmesini tooreview hello gidin PNS belirli hataları. 
   
    d) varsa hello bildirim hub'ı hello kimlik doğrulama ayarlarıyla sonra yanlış PNS kimlik doğrulama hatası görürsünüz. Bir göstergesidir toocheck hello PNS kimlik budur. 

2) **Programlı erişim**

Daha fazla ayrıntı burada- 

* [Programsal Telemetri erişim]
* [API örnek üzerinden telemetri erişim] 

> [!NOTE]
> İlgili birkaç telemetri gibi özellikler **içeri/dışarı aktarma kayıtlar**, **API'leri aracılığıyla Telemetri erişim** vb. standart katmanında kullanılabilen yalnızca. Toouse çalışırsanız, boş veya temel katmana sonra kullanıyorsanız bu özellikleri hello doğrudan REST API kullanırken, hello SDK ve HTTP 403 (Yasak) kullanırken özel durum iletisi toothis etkisi alırsınız. Klasik Azure portalı tooStandard katmanı oluşturan taşıdığınızdan emin olun.  
> 
> 

<!-- IMAGES -->
[0]: ./media/notification-hubs-diagnosing/Architecture.png
[1]: ./media/notification-hubs-diagnosing/GCMConfigure.png
[2]: ./media/notification-hubs-diagnosing/GCMEnable.png
[3]: ./media/notification-hubs-diagnosing/GCMServerKey.png
[4]: ./media/notification-hubs-diagnosing/PortalConfigure.png
[5]: ./media/notification-hubs-diagnosing/PortalDashboard.png
[6]: ./media/notification-hubs-diagnosing/PortalMonitoring.png
[7]: ./media/notification-hubs-diagnosing/PortalTestNotification.png
[8]: ./media/notification-hubs-diagnosing/VSRegistrations.png
[9]: ./media/notification-hubs-diagnosing/VSServerExplorer.png
[10]: ./media/notification-hubs-diagnosing/VSTestNotification.png

<!-- LINKS -->
[Notification Hubs'a genel bakış]: notification-hubs-push-notification-overview.md
[Başlarken öğreticilerine alma]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[şablonu Kılavuzu]: https://msdn.microsoft.com/library/dn530748.aspx 
[APNS Kılavuzu]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4
[GCM Kılavuzu]: http://developer.android.com/google/gcm/adv.html
[Export/Import Registrations]: http://msdn.microsoft.com/library/dn790624.aspx
[ServiceBus Explorer]: http://msdn.microsoft.com/library/dn530751.aspx
[ServiceBus Explorer kodu]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a
[VS Sunucu Gezgini genel bakış]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx 
[VS Sunucu Gezgini Blog Gönderisi - 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs 
[VS Sunucu Gezgini Blog Gönderisi - 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ 
[EnableTestSend özelliği]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx
[Programsal Telemetri erişim]: http://msdn.microsoft.com/library/azure/dn458823.aspx
[API örnek üzerinden telemetri erişim]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel

