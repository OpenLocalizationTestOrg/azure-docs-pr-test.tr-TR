---
title: aaaHow toouse Notification Hubs ile Python
description: "Bilgi nasıl toouse Azure Notification Hubs bir Python arka uçtan."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 5640dd4a-a91e-4aa0-a833-93615bde49b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: python
ms.devlang: php
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 21d5aaf7fc24c9936fac8e0a8de640c66c51ab0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-python"></a>Nasıl toouse python'dan bildirim hub'ları
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Bir Java/PHP/Python/Ruby arka ucunu tüm bildirim hub'ları özelliklere erişebilir hello MSDN konuda açıklandığı gibi hello bildirim hub'ı REST arabirimini kullanarak [bildirim hub'ları REST API'leri](http://msdn.microsoft.com/library/dn223264.aspx).

> [!NOTE]
> Bu hello bildirim gönderir Python içinde uygulamak için bir örnek başvuru uygulaması ve hello bildirimler Hub Python SDK resmi olarak desteklenen değil.
> 
> Bu örnek, Python 3.4 kullanılarak yazılır.
> 
> 

Bu konudaki gösteriyoruz nasıl yapılır:

* REST istemcisi Python Notification Hubs özellikleri için oluşturun.
* Merhaba Python arabirimi toohello bildirim hub'ı REST API'lerini kullanarak bildirimleri gönderin. 
* Hata ayıklama/eğitim amaçla hello HTTP REST istek/yanıt dökümünü alın. 

Merhaba izleyebilirsiniz [Get öğreticisinde](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) hello arka uç bölümü Python içinde uygulama tercih ettiğiniz mobil platformunuz için.

> [!NOTE]
> yalnızca sınırlı toosend bildirim hello örnek Hello kapsamı olan ve herhangi bir kayıt yönetim yapmaz.
> 
> 

## <a name="client-interface"></a>İstemci arabirimi
Merhaba ana istemci arabirimi hello kullanılabilir aynı yöntemleri hello sağlayabilir [.NET Notification Hubs SDK'sı](http://msdn.microsoft.com/library/jj933431.aspx). Bu, toodirectly sağlayacak tüm hello öğreticiler ve bu site şu anda kullanılabilir örnekleri Çevir ve hello hello topluluğu tarafından katkısı Internet.

Hello kullanılabilir tüm hello kod Bul [Python REST sarmalayıcı örnek].

Örneğin, toocreate bir istemci:

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

toosend Windows bildirim kutlayın:

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a>Uygulama
Zaten yaptıysanız Lütfen izleyin bizim [Get öğreticisinde] yukarı tooimplement hello arka uç olduğu toohello son bölümü.

Tüm Ayrıntılar tooimplement tam REST sarmalayıcı bulunabilir hello [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). Bu bölümde biz hello Python uygulaması hello ana adım gerekli tooaccess bildirim hub'ları REST uç noktalarını tanımlamak ve bildirimleri gönderme

1. Merhaba bağlantı dizesini ayrıştırma
2. Merhaba yetkilendirme belirteci oluştur
3. HTTP REST API kullanarak bildirim gönderme

### <a name="parse-hello-connection-string"></a>Merhaba bağlantı dizesini ayrıştırma
Merhaba ana sınıfı oluşturucusu hello bağlantı dizesini ayrıştırmak için hello istemci uygulama şöyledir:

    class NotificationHub:
        API_VERSION = "?api-version=2013-10"
        DEBUG_SEND = "&test"

        def __init__(self, connection_string=None, hub_name=None, debug=0):
            self.HubName = hub_name
            self.Debug = debug

            # Parse connection string
            parts = connection_string.split(';')
            if len(parts) != 3:
                raise Exception("Invalid ConnectionString.")

            for part in parts:
                if part.startswith('Endpoint'):
                    self.Endpoint = 'https' + part[11:]
                if part.startswith('SharedAccessKeyName'):
                    self.SasKeyName = part[20:]
                if part.startswith('SharedAccessKey'):
                    self.SasKeyValue = part[16:]


### <a name="create-security-token"></a>Güvenlik belirteci oluşturma
Merhaba güvenlik belirteci oluşturma Hello ayrıntılarını kullanılabilir [burada](http://msdn.microsoft.com/library/dn495627.aspx).
Merhaba aşağıdaki yöntemlerden sahip eklenen toobe toohello **NotificationHub** hello hello geçerli istek ve hello bağlantı dizesinden ayıklanan hello kimlik URI'sini temel sınıf toocreate hello simgesi.

    @staticmethod
    def get_expiry():
        # By default returns an expiration of 5 minutes (=300 seconds) from now
        return int(round(time.time() + 300))

    @staticmethod
    def encode_base64(data):
        return base64.b64encode(data)

    def sign_string(self, to_sign):
        key = self.SasKeyValue.encode('utf-8')
        to_sign = to_sign.encode('utf-8')
        signed_hmac_sha256 = hmac.HMAC(key, to_sign, hashlib.sha256)
        digest = signed_hmac_sha256.digest()
        encoded_digest = self.encode_base64(digest)
        return encoded_digest

    def generate_sas_token(self):
        target_uri = self.Endpoint + self.HubName
        my_uri = urllib.parse.quote(target_uri, '').lower()
        expiry = str(self.get_expiry())
        to_sign = my_uri + '\n' + expiry
        signature = urllib.parse.quote(self.sign_string(to_sign))
        auth_format = 'SharedAccessSignature sig={0}&se={1}&skn={2}&sr={3}'
        sas_token = auth_format.format(signature, expiry, self.SasKeyName, my_uri)
        return sas_token

### <a name="send-a-notification-using-http-rest-api"></a>HTTP REST API kullanarak bildirim gönderme
Birincisi, let tanımlamak bir bildirim temsil eden sınıf.

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of hello following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

Bu sınıf, bir yerel bildirim gövdesi veya bir şablon bildirim biçimi (yerel platform veya şablon) ve platforma özgü özellikleri (örneğin, Apple sona erme özelliği ve WNS üstbilgileri) içeren bir dizi üstbilgileri durumunda özellikler kümesi için bir kapsayıcıdır.

Lütfen toohello bakın [bildirim hub'ları REST API belgelerine](http://msdn.microsoft.com/library/dn495827.aspx) ve tüm kullanılabilir seçenekleri hello için belirli bildirim platformları biçimleri hello.

Bu sınıf ile biz hello gönderme hello içinde bildirim yöntemleri yazabilirsiniz artık **NotificationHub** sınıfı.

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about hello PNS send notification outcome
            url += self.DEBUG_SEND
            print("--- REQUEST ---")
            print("URI: " + url)
            print("Headers: " + json.dumps(headers, sort_keys=True, indent=4, separators=(' ', ': ')))
            print("--- END REQUEST ---\n")

        connection.request('POST', url, payload, headers)
        response = connection.getresponse()

        if self.Debug > 0:
            # print out detailed response information for debugging purpose
            print("\n\n--- RESPONSE ---")
            print(str(response.status) + " " + response.reason)
            print(response.msg)
            print(response.read())
            print("--- END RESPONSE ---")

        elif response.status != 201:
            # Successful outcome of send message is HTTP 201 - Created
            raise Exception(
                "Error sending notification. Received HTTP code " + str(response.status) + " " + response.reason)

        connection.close()

    def send_notification(self, notification, tag_or_tag_expression=None):
        url = self.Endpoint + self.HubName + '/messages' + self.API_VERSION

        json_platforms = ['template', 'apple', 'gcm', 'adm', 'baidu']

        if any(x in notification.format for x in json_platforms):
            content_type = "application/json"
            payload_to_send = json.dumps(notification.payload)
        else:
            content_type = "application/xml"
            payload_to_send = notification.payload

        headers = {
            'Content-type': content_type,
            'Authorization': self.generate_sas_token(),
            'ServiceBusNotification-Format': notification.format
        }

        if isinstance(tag_or_tag_expression, set):
            tag_list = ' || '.join(tag_or_tag_expression)
        else:
            tag_list = tag_or_tag_expression

        # add hello tags/tag expressions toohello headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers toohello headers collection that hello user may have added
        if notification.headers is not None:
            headers.update(notification.headers)

        self.make_http_request(url, payload_to_send, headers)

    def send_apple_notification(self, payload, tags=""):
        nh = Notification("apple", payload)
        self.send_notification(nh, tags)

    def send_gcm_notification(self, payload, tags=""):
        nh = Notification("gcm", payload)
        self.send_notification(nh, tags)

    def send_adm_notification(self, payload, tags=""):
        nh = Notification("adm", payload)
        self.send_notification(nh, tags)

    def send_baidu_notification(self, payload, tags=""):
        nh = Notification("baidu", payload)
        self.send_notification(nh, tags)

    def send_mpns_notification(self, payload, tags=""):
        nh = Notification("windowsphone", payload)

        if "<wp:Toast>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'toast', 'X-NotificationClass': '2'}
        elif "<wp:Tile>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'tile', 'X-NotificationClass': '1'}

        self.send_notification(nh, tags)

    def send_windows_notification(self, payload, tags=""):
        nh = Notification("windows", payload)

        if "<toast>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/toast'}
        elif "<tile>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/tile'}
        elif "<badge>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/badge'}

        self.send_notification(nh, tags)

    def send_template_notification(self, properties, tags=""):
        nh = Notification("template", properties)
        self.send_notification(nh, tags)

Merhaba yöntemleri yukarıda bir HTTP POST isteği toohello /messages uç noktasını, bildirim hub ' ınızı hello doğru gövde ve üstbilgileri toosend hello bildirim gönderin.

### <a name="using-debug-property-tooenable-detailed-logging"></a>Hata ayıklama özelliği tooenable kullanarak ayrıntılı günlük kaydı
Merhaba bildirim hub'ı başlatılırken hata ayıklama özelliğini etkinleştirme hello HTTP ilgili ayrıntılı günlük kaydı bilgileri ayrıntılı bir bildirim iletisi yanı sıra istek ve yanıt döküm sonucu Gönder yazacaksınız. Son olarak adlandırılan bu özellik eklediğimiz [bildirim hub'ları TestSend özelliği](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) hello bildirim gönderme sonucunu hakkında ayrıntılı bilgiler döndürür. toouse, - hello aşağıdakileri kullanarak başlatılamadı:

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

Merhaba bildirim hub'ı gönderme isteği HTTP URL'si, "test" sorgu dizesi ile sonuç olarak eklenmiş. 

## <a name="complete-tutorial"></a>Tam başlangıç Öğreticisi
Şimdi bir Python arka ucunu hello bildirim göndererek hello Başlarken Öğreticisi tamamlayabilirsiniz.

Bildirim hub'ları istemciniz başlatılamıyor (hello belirtildiği gibi hello bağlantı dizenizi ve hub adı yerine [Get öğreticisinde]):

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

Ardından, hedef mobil platforma bağlı olarak hello gönderme kodu ekleyin. Bu örnek ayrıca hello platform örneğin send_windows_notification windows için temel bildirimleri gönderme daha yüksek düzey yöntemleri tooenable ekler; (için apple) send_apple_notification vs. 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Windows mağazası ve Windows Phone 8.1 (Silverlight olmayan)
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 ve 8.1 Silverlight
    hub.send_mpns_notification(toast)

### <a name="ios"></a>iOS
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a>Android
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a>Kindle Fire
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a>Baidu
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

Python kodunuzu çalıştıran hedef aygıtınızda görünen bir bildirim üretir.

## <a name="examples"></a>Örnekler:
### <a name="enabling-debug-property"></a>Hata ayıklama özelliğini etkinleştirme
Göreceğiniz sonra hello NotificationHub başlatılırken hata ayıklama bayrağı etkinleştirdiğinizde, HTTP istek ve yanıt döküm yanı sıra NotificationOutcome burada hangi HTTP üstbilgileri hello istekte geçirilir ve hangi HTTP anlayabileceği hello aşağıdaki gibi ayrıntılı yanıt, bildirim hub'ı hello alındı:![][1]

Bildirim hub'ı sonuç ayrıntılı örneğin görürsünüz 

* Merhaba ileti başarıyla toohello anında iletilen bildirim servisi gönderildiğinde. 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* Varsa herhangi bir anında bildirim hedefi bulunamadı sonra büyük olasılıkla toosee hello aşağıdaki (gösteren bazı hello kayıtlar sahip olduğundan toodeliver hello bildirim büyük olasılıkla bulunan herhangi bir kayıt olan hello yanıt kalacaklarını eşleşmeyen etiketler)
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a>Bildirim bildirim tooWindows yayını
Bir yayın bildirim bildirim tooWindows istemci gönderirken gönderilen hello üstbilgileri dikkat edin. 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a>Bir etiketi (veya etiket ifadesi) belirterek bildirim gönder
Toohello HTTP isteği eklenen bildirimi hello etiketleri HTTP üstbilgisi (Merhaba aşağıdaki örnekte, biz hello bildirim yalnızca tooregistrations 'Spor' yükü gönderiyor)

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a>Birden çok etiket belirtme bildirim gönder
Birden çok etiket gönderildiğinde hello etiketleri HTTP üstbilgisi nasıl değiştiğine dikkat edin. 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a>Şablonlu bildirim
Biçim HTTP üstbilgisi değişiklikleri hello ve yükü gövde hello dikkat edin hello HTTP istek gövdesi bir parçası olarak gönderilir:

**İstemci tarafı - kayıtlı şablonu**

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

**Sunucu tarafı - Hello yükü gönderme**

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a>Sonraki Adımlar
Bu konuda size nasıl basit bir Python toocreate REST gösterdi istemci bildirim hub'ları için. Buradan şunları yapabilirsiniz:

* Merhaba tam karşıdan [Python REST sarmalayıcı örnek], yukarıdaki tüm hello kodunu içerir.
* Bildirim hub'ları özelliği hello etiketleme hakkında bilgi almaya devam etmek [çiğnemekten haber Öğreticisi]
* Hello bildirim hub'ları şablonları özelliği hakkında bilgi almaya devam etmek [yerelleştirme haber Öğreticisi]

<!-- URLs -->
[Python REST sarmalayıcı örnek]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python
[Get öğreticisinde]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[çiğnemekten haber Öğreticisi]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/
[yerelleştirme haber Öğreticisi]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

