---
title: "Azure bildirim hub'ları ve Node.js ile aaaSending anında iletme bildirimleri"
description: "Nasıl toouse bildirim hub'ları toosend anında iletme bildirimleri bir Node.js uygulamasından öğrenin."
keywords: "anında iletme bildirimi, anında iletme notifications,node.js itme ios anında iletme"
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a>Azure bildirim hub'ları ve Node.js ile anında iletme bildirimleri gönderme
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a>Genel Bakış
> [!IMPORTANT]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).
> 
> 

Bu kılavuz size nasıl toosend anında iletme bildirimleri hello Yardım Azure bildirim hub'larını doğrudan bir Node.js uygulamasından gösterir. 

anında iletme bildirimleri tooapplications platformlar aşağıdaki hello üzerinde gönderme kapsamdaki hello senaryolar şunlardır:

* Android
* iOS
* Windows Phone
* Evrensel Windows platformu 

Bildirim hub'ları hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next) bölümü.

## <a name="what-are-notification-hubs"></a>Bildirim Hub'ları nedir?
Azure bildirim hub'ları, anında iletme bildirimleri toomobile aygıtları göndermek için kullanımı kolay, çok platformlu, ölçeklenebilir bir altyapı sunar. Merhaba hello hizmet altyapısı hakkında daha fazla bilgi için bkz: [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) sayfası.

## <a name="create-a-nodejs-application"></a>Bir Node.js uygulaması oluşturma
Bu öğreticide Hello ilk adımı, yeni ve boş bir Node.js uygulaması oluşturmaktır. Bir Node.js uygulaması oluşturma ile ilgili yönergeler için bkz: [oluşturma ve bir Node.js uygulaması tooAzure Web sitesi dağıtma][nodejswebsite], [Node.js bulut hizmeti] [ Node.js Cloud Service] Windows PowerShell kullanarak veya [Web sitesini WebMatrix ile].

## <a name="configure-your-application-toouse-notification-hubs"></a>Uygulamanızı tooUse bildirim hub'ları yapılandırma
Azure Notification Hubs toouse, gereksinim duyduğunuz toodownload ve kullanım hello Node.js [azure paketi](https://www.npmjs.com/package/azure), hello anında iletme bildirimi REST Hizmetleri ile iletişim yardımcı kitaplıklar yerleşik bir kümesini içerir.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Düğüm paketi Yöneticisi (NPM) tooobtain hello paketini kullanın
1. Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (Linux) ve boş uygulamanızı oluşturulduğu toohello klasörüne gidin .
2. Tür **npm yükleme azure sb** hello komut penceresinde.
3. Merhaba el ile çalıştırabilirsiniz **ls** veya **dir** komutu tooverify, bir **düğümü\_modülleri** klasörü oluşturuldu. Bu klasör içinde hello bulur **azure** tooaccess ihtiyacınız hello kitaplıklarını içeren paket hello bildirim hub'ı.

> [!NOTE]
> Merhaba resmi üzerinde NPM yükleme hakkında daha fazla bilgi edinebilirsiniz [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm). 
> 
> 

### <a name="import-hello-module"></a>İçeri aktarma hello Modülü
Bir metin düzenleyicisi kullanarak eklemek hello toohello üstündeki aşağıdaki hello **server.js** hello uygulama dosyası:

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a>Azure bildirim hub'ı bağlantısı kurma
Merhaba **NotificationHubService** nesne notification hubs ile çalışmanıza olanak sağlar. Merhaba aşağıdaki kod oluşturur bir **NotificationHubService** hello nofication hub'ı adlı nesne **hubname**. Merhaba hello yukarıya yakın eklemek **server.js** hello deyimi tooimport hello azure modülü sonra dosyayı:

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

Merhaba bağlantı **connectionstring** değeri hello elde edilebilir [Azure Portal] hello aşağıdaki adımları gerçekleştirerek:

1. Merhaba sol gezinti bölmesinde **Gözat**.
2. Seçin **bildirim hub'ları**ve ardından Bul hello hub hello örnek toouse istiyor. Toohello başvurabilir [Windows mağazası Başlarken Öğreticisi](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) yeni bir bildirim hub'ı oluşturma yardıma gereksinim duyarsanız.
3. Seçin **ayarları**.
4. Tıklayın **erişim ilkeleri**. Her iki paylaşılan ve tam erişim bağlantı dizeleri görürsünüz.

![Azure Portal - bildirim hub'ları](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> Hello kullanarak hello bağlantı dizesini de alabilirsiniz **Get-AzureSbNamespace** tarafından sağlanan cmdlet [Azure PowerShell](/powershell/azureps-cmdlets-docs) veya hello **azure sb ad alanı göster** komutunu Merhaba [Azure komut satırı arabirimi (Azure CLI)](../cli-install-nodejs.md).
> 
> 

## <a name="general-architecture"></a>Genel mimari
Merhaba **NotificationHubService** nesne anında iletme bildirimleri toospecific cihazları ve uygulamaları göndermek için nesne örnekleri aşağıdaki hello gösterir:

* **Android** -hello kullan **GcmService** şu adresten edinilebilir nesne **notificationHubService.gcm**
* **iOS** -hello kullan **ApnsService** adresindeki erişilebilir olan nesne, **notificationHubService.apns**
* **Windows Phone** -hello kullan **MpnsService** şu adresten edinilebilir nesne **notificationHubService.mpns**
* **Evrensel Windows platformu** -hello kullan **WnsService** şu adresten edinilebilir nesne **notificationHubService.wns**

### <a name="how-to-send-push-notifications-tooandroid-applications"></a>Nasıl yapılır: anında iletme bildirimleri tooAndroid uygulamaları gönderir
Merhaba **GcmService** nesnesi sağlar bir **Gönder** kullanılan toosend anında iletme bildirimleri tooAndroid uygulamaları kullanılabilecek yöntemi. Merhaba **Gönder** yöntemi şu parametreler hello kabul eder:

* **Etiketler** -etiketi tanımlayıcı hello. Hiçbir etiketi sağlanırsa, tooall istemcileri hello bildirim gönderilir.
* **Yükü** -ileti JSON veya ham dize yükü hello.
* **Geri çağırma** -hello geri çağırma işlevi.

Merhaba hello yük biçimi hakkında daha fazla bilgi için bkz: **yükü** hello bölümünü [uygulama GCM Server](http://developer.android.com/google/gcm/server.html#payload) belge.

Merhaba aşağıdaki kod kullanır hello **GcmService** hello tarafından kullanıma sunulan örneği **NotificationHubService** toosend anında iletme bildirimi tooall istemciler kayıtlı.

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a>Nasıl yapılır: anında iletme bildirimleri tooiOS uygulamaları gönderir
Yukarıda açıklanan Android uygulamalarında olduğu gibi aynı hello **ApnsService** nesnesi sağlar bir **Gönder** kullanılan toosend anında iletme bildirimleri tooiOS uygulamaları kullanılabilecek yöntemi. Merhaba **Gönder** yöntemi şu parametreler hello kabul eder:

* **Etiketler** -etiketi tanımlayıcı hello. Hiçbir etiketi sağlanırsa, tooall istemcileri hello bildirim gönderilir.
* **Yükü** - ileti JSON hello veya dize yükü.
* **Geri çağırma** -hello geri çağırma işlevi.

Daha fazla bilgi hello yük biçimi için hello bkz **bildirim yükü** hello bölümünü [yerel ve anında iletilen bildirim Programlama Kılavuzu](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) belge.

Merhaba aşağıdaki kod kullanır hello **ApnsService** hello tarafından kullanıma sunulan örneği **NotificationHubService** toosend bir uyarı iletisi tooall istemciler:

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a>Nasıl yapılır: anında iletme bildirimleri tooWindows Phone uygulamaları Gönder
Merhaba **MpnsService** nesne sağlayan bir **Gönder** kullanılan toosend anında iletme bildirimleri tooWindows Phone uygulamaları olabilir yöntemi. Merhaba **Gönder** yöntemi şu parametreler hello kabul eder:

* **Etiketler** -etiketi tanımlayıcı hello. Hiçbir etiketi sağlanırsa, tooall istemcileri hello bildirim gönderilir.
* **Yükü** -ileti XML yükü hello.
* **TargetName**  -  `toast` bildirimleri için. `token`Döşeme bildirimleri için.
* **NotificationClass** -hello hello bildirim önceliğini. Merhaba bkz **HTTP üstbilgi öğelerini** hello bölümünü [anında iletme bildirimleri bir sunucudan](http://msdn.microsoft.com/library/hh221551.aspx) belge için geçerli değerler.
* **Seçenekler** - isteğe bağlı istek üstbilgileri.
* **Geri çağırma** -hello geri çağırma işlevi.

Geçerli bir listesi için **TargetName**, **NotificationClass** ve başlık seçeneklerini denetleme hello [anında iletme bildirimleri bir sunucudan](http://msdn.microsoft.com/library/hh221551.aspx) sayfası.

Aşağıdaki örnek kod hello kullanan hello **MpnsService** hello tarafından kullanıma sunulan örneği **NotificationHubService** toosend anında bildirim:

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a>Nasıl yapılır: anında iletme bildirimleri tooUniversal Windows Platformu (UWP) uygulamaları gönderir
Merhaba **WnsService** nesne sağlayan bir **Gönder** kullanılan toosend anında iletme bildirimleri tooUniversal Windows platformu uygulamaları kullanılabilecek yöntemi.  Merhaba **Gönder** yöntemi şu parametreler hello kabul eder:

* **Etiketler** -etiketi tanımlayıcı hello. Hiçbir etiketi sağlanırsa, kayıtlı tooall istemcileri hello bildirim gönderilir.
* **Yükü** -hello XML ileti yükü.
* **Tür** -hello bildirim türü.
* **Seçenekler** - isteğe bağlı istek üstbilgileri.
* **Geri çağırma** -hello geri çağırma işlevi.

Geçerli türler ve istek üstbilgileri listesi için bkz: [anında bildirim hizmeti istek ve yanıt üstbilgileri](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).

Merhaba aşağıdaki kod kullanır hello **WnsService** hello tarafından kullanıma sunulan örneği **NotificationHubService** toosend bir bildirim anında iletme bildirimi tooa UWP uygulaması:

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a>Sonraki Adımlar
Merhaba örnek parçacıkları yukarıdaki, tooeasily yapı hizmeti altyapı toodeliver anında iletme bildirimleri tooa çeşitli aygıtlar izin verir. Node.js ile bildirim hub'ları kullanarak hello temellerini öğrendiğinize göre bu özellikleri daha fazla nasıl genişletebileceğini hakkında daha fazla bu bağlantılar toolearn izleyin.

* Bkz. MSDN başvurusunu hello [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).
* Merhaba ziyaret [düğümü için Azure SDK] daha fazla örnekleri ve uygulama ayrıntıları için github'da depo.

[düğümü için Azure SDK]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[Web sitesini WebMatrix ile]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Azure Portal]: https://portal.azure.com
