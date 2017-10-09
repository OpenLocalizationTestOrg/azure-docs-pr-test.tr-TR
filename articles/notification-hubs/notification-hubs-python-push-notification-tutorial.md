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
# <a name="how-toouse-notification-hubs-from-python"></a><span data-ttu-id="6abb0-103">Nasıl toouse python'dan bildirim hub'ları</span><span class="sxs-lookup"><span data-stu-id="6abb0-103">How toouse Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="6abb0-104">Bir Java/PHP/Python/Ruby arka ucunu tüm bildirim hub'ları özelliklere erişebilir hello MSDN konuda açıklandığı gibi hello bildirim hub'ı REST arabirimini kullanarak [bildirim hub'ları REST API'leri](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="6abb0-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="6abb0-105">Bu hello bildirim gönderir Python içinde uygulamak için bir örnek başvuru uygulaması ve hello bildirimler Hub Python SDK resmi olarak desteklenen değil.</span><span class="sxs-lookup"><span data-stu-id="6abb0-105">This is a sample reference implementation for implementing hello notification sends in Python and is not hello officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="6abb0-106">Bu örnek, Python 3.4 kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="6abb0-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="6abb0-107">Bu konudaki gösteriyoruz nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="6abb0-107">In this topic we show how to:</span></span>

* <span data-ttu-id="6abb0-108">REST istemcisi Python Notification Hubs özellikleri için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6abb0-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="6abb0-109">Merhaba Python arabirimi toohello bildirim hub'ı REST API'lerini kullanarak bildirimleri gönderin.</span><span class="sxs-lookup"><span data-stu-id="6abb0-109">Send notifications using hello Python interface toohello Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="6abb0-110">Hata ayıklama/eğitim amaçla hello HTTP REST istek/yanıt dökümünü alın.</span><span class="sxs-lookup"><span data-stu-id="6abb0-110">Get a dump of hello HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="6abb0-111">Merhaba izleyebilirsiniz [Get öğreticisinde](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) hello arka uç bölümü Python içinde uygulama tercih ettiğiniz mobil platformunuz için.</span><span class="sxs-lookup"><span data-stu-id="6abb0-111">You can follow hello [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing hello back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="6abb0-112">yalnızca sınırlı toosend bildirim hello örnek Hello kapsamı olan ve herhangi bir kayıt yönetim yapmaz.</span><span class="sxs-lookup"><span data-stu-id="6abb0-112">hello scope of hello sample is only limited toosend notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="6abb0-113">İstemci arabirimi</span><span class="sxs-lookup"><span data-stu-id="6abb0-113">Client interface</span></span>
<span data-ttu-id="6abb0-114">Merhaba ana istemci arabirimi hello kullanılabilir aynı yöntemleri hello sağlayabilir [.NET Notification Hubs SDK'sı](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="6abb0-114">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="6abb0-115">Bu, toodirectly sağlayacak tüm hello öğreticiler ve bu site şu anda kullanılabilir örnekleri Çevir ve hello hello topluluğu tarafından katkısı Internet.</span><span class="sxs-lookup"><span data-stu-id="6abb0-115">This will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="6abb0-116">Hello kullanılabilir tüm hello kod Bul [Python REST sarmalayıcı örnek].</span><span class="sxs-lookup"><span data-stu-id="6abb0-116">You can find all hello code available in hello [Python REST wrapper sample].</span></span>

<span data-ttu-id="6abb0-117">Örneğin, toocreate bir istemci:</span><span class="sxs-lookup"><span data-stu-id="6abb0-117">For example, toocreate a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="6abb0-118">toosend Windows bildirim kutlayın:</span><span class="sxs-lookup"><span data-stu-id="6abb0-118">toosend a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="6abb0-119">Uygulama</span><span class="sxs-lookup"><span data-stu-id="6abb0-119">Implementation</span></span>
<span data-ttu-id="6abb0-120">Zaten yaptıysanız Lütfen izleyin bizim [Get öğreticisinde] yukarı tooimplement hello arka uç olduğu toohello son bölümü.</span><span class="sxs-lookup"><span data-stu-id="6abb0-120">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>

<span data-ttu-id="6abb0-121">Tüm Ayrıntılar tooimplement tam REST sarmalayıcı bulunabilir hello [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="6abb0-121">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="6abb0-122">Bu bölümde biz hello Python uygulaması hello ana adım gerekli tooaccess bildirim hub'ları REST uç noktalarını tanımlamak ve bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="6abb0-122">In this section we will describe hello Python implementation of hello main steps required tooaccess Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="6abb0-123">Merhaba bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="6abb0-123">Parse hello connection string</span></span>
2. <span data-ttu-id="6abb0-124">Merhaba yetkilendirme belirteci oluştur</span><span class="sxs-lookup"><span data-stu-id="6abb0-124">Generate hello authorization token</span></span>
3. <span data-ttu-id="6abb0-125">HTTP REST API kullanarak bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="6abb0-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="6abb0-126">Merhaba bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="6abb0-126">Parse hello connection string</span></span>
<span data-ttu-id="6abb0-127">Merhaba ana sınıfı oluşturucusu hello bağlantı dizesini ayrıştırmak için hello istemci uygulama şöyledir:</span><span class="sxs-lookup"><span data-stu-id="6abb0-127">Here is hello main class implementing hello client, whose constructor parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="6abb0-128">Güvenlik belirteci oluşturma</span><span class="sxs-lookup"><span data-stu-id="6abb0-128">Create security token</span></span>
<span data-ttu-id="6abb0-129">Merhaba güvenlik belirteci oluşturma Hello ayrıntılarını kullanılabilir [burada](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="6abb0-129">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="6abb0-130">Merhaba aşağıdaki yöntemlerden sahip eklenen toobe toohello **NotificationHub** hello hello geçerli istek ve hello bağlantı dizesinden ayıklanan hello kimlik URI'sini temel sınıf toocreate hello simgesi.</span><span class="sxs-lookup"><span data-stu-id="6abb0-130">hello following methods have toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="6abb0-131">HTTP REST API kullanarak bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="6abb0-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="6abb0-132">Birincisi, let tanımlamak bir bildirim temsil eden sınıf.</span><span class="sxs-lookup"><span data-stu-id="6abb0-132">First, let use define a class representing a notification.</span></span>

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

<span data-ttu-id="6abb0-133">Bu sınıf, bir yerel bildirim gövdesi veya bir şablon bildirim biçimi (yerel platform veya şablon) ve platforma özgü özellikleri (örneğin, Apple sona erme özelliği ve WNS üstbilgileri) içeren bir dizi üstbilgileri durumunda özellikler kümesi için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="6abb0-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="6abb0-134">Lütfen toohello bakın [bildirim hub'ları REST API belgelerine](http://msdn.microsoft.com/library/dn495827.aspx) ve tüm kullanılabilir seçenekleri hello için belirli bildirim platformları biçimleri hello.</span><span class="sxs-lookup"><span data-stu-id="6abb0-134">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="6abb0-135">Bu sınıf ile biz hello gönderme hello içinde bildirim yöntemleri yazabilirsiniz artık **NotificationHub** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="6abb0-135">Now with this class, we can write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

<span data-ttu-id="6abb0-136">Merhaba yöntemleri yukarıda bir HTTP POST isteği toohello /messages uç noktasını, bildirim hub ' ınızı hello doğru gövde ve üstbilgileri toosend hello bildirim gönderin.</span><span class="sxs-lookup"><span data-stu-id="6abb0-136">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

### <a name="using-debug-property-tooenable-detailed-logging"></a><span data-ttu-id="6abb0-137">Hata ayıklama özelliği tooenable kullanarak ayrıntılı günlük kaydı</span><span class="sxs-lookup"><span data-stu-id="6abb0-137">Using debug property tooenable detailed logging</span></span>
<span data-ttu-id="6abb0-138">Merhaba bildirim hub'ı başlatılırken hata ayıklama özelliğini etkinleştirme hello HTTP ilgili ayrıntılı günlük kaydı bilgileri ayrıntılı bir bildirim iletisi yanı sıra istek ve yanıt döküm sonucu Gönder yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="6abb0-138">Enabling debug property while initializing hello Notification Hub will write out detailed logging information about hello HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="6abb0-139">Son olarak adlandırılan bu özellik eklediğimiz [bildirim hub'ları TestSend özelliği](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) hello bildirim gönderme sonucunu hakkında ayrıntılı bilgiler döndürür.</span><span class="sxs-lookup"><span data-stu-id="6abb0-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about hello notification send outcome.</span></span> <span data-ttu-id="6abb0-140">toouse, - hello aşağıdakileri kullanarak başlatılamadı:</span><span class="sxs-lookup"><span data-stu-id="6abb0-140">toouse it - initialize using hello following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="6abb0-141">Merhaba bildirim hub'ı gönderme isteği HTTP URL'si, "test" sorgu dizesi ile sonuç olarak eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="6abb0-141">hello Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="6abb0-142"><a name="complete-tutorial"></a>Tam başlangıç Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="6abb0-142"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="6abb0-143">Şimdi bir Python arka ucunu hello bildirim göndererek hello Başlarken Öğreticisi tamamlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6abb0-143">Now you can complete hello Get Started tutorial by sending hello notification from a Python back-end.</span></span>

<span data-ttu-id="6abb0-144">Bildirim hub'ları istemciniz başlatılamıyor (hello belirtildiği gibi hello bağlantı dizenizi ve hub adı yerine [Get öğreticisinde]):</span><span class="sxs-lookup"><span data-stu-id="6abb0-144">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="6abb0-145">Ardından, hedef mobil platforma bağlı olarak hello gönderme kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6abb0-145">Then add hello send code depending on your target mobile platform.</span></span> <span data-ttu-id="6abb0-146">Bu örnek ayrıca hello platform örneğin send_windows_notification windows için temel bildirimleri gönderme daha yüksek düzey yöntemleri tooenable ekler; (için apple) send_apple_notification vs.</span><span class="sxs-lookup"><span data-stu-id="6abb0-146">This sample also adds higher level methods tooenable sending notifications based on hello platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="6abb0-147">Windows mağazası ve Windows Phone 8.1 (Silverlight olmayan)</span><span class="sxs-lookup"><span data-stu-id="6abb0-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="6abb0-148">Windows Phone 8.0 ve 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="6abb0-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="6abb0-149">iOS</span><span class="sxs-lookup"><span data-stu-id="6abb0-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="6abb0-150">Android</span><span class="sxs-lookup"><span data-stu-id="6abb0-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="6abb0-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="6abb0-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="6abb0-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="6abb0-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="6abb0-153">Python kodunuzu çalıştıran hedef aygıtınızda görünen bir bildirim üretir.</span><span class="sxs-lookup"><span data-stu-id="6abb0-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="6abb0-154">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="6abb0-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="6abb0-155">Hata ayıklama özelliğini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="6abb0-155">Enabling debug property</span></span>
<span data-ttu-id="6abb0-156">Göreceğiniz sonra hello NotificationHub başlatılırken hata ayıklama bayrağı etkinleştirdiğinizde, HTTP istek ve yanıt döküm yanı sıra NotificationOutcome burada hangi HTTP üstbilgileri hello istekte geçirilir ve hangi HTTP anlayabileceği hello aşağıdaki gibi ayrıntılı yanıt, bildirim hub'ı hello alındı:![][1]</span><span class="sxs-lookup"><span data-stu-id="6abb0-156">When you enable debug flag while initializing hello NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like hello following where you can understand what HTTP headers are passed in hello request and what HTTP response was received from hello Notification Hub: ![][1]</span></span>

<span data-ttu-id="6abb0-157">Bildirim hub'ı sonuç ayrıntılı örneğin görürsünüz</span><span class="sxs-lookup"><span data-stu-id="6abb0-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="6abb0-158">Merhaba ileti başarıyla toohello anında iletilen bildirim servisi gönderildiğinde.</span><span class="sxs-lookup"><span data-stu-id="6abb0-158">when hello message is successfully sent toohello Push Notification Service.</span></span> 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* <span data-ttu-id="6abb0-159">Varsa herhangi bir anında bildirim hedefi bulunamadı sonra büyük olasılıkla toosee hello aşağıdaki (gösteren bazı hello kayıtlar sahip olduğundan toodeliver hello bildirim büyük olasılıkla bulunan herhangi bir kayıt olan hello yanıt kalacaklarını eşleşmeyen etiketler)</span><span class="sxs-lookup"><span data-stu-id="6abb0-159">If there were no targets found for any push notification then you are likely going toosee hello following in hello response (which indicates that there were no registrations found toodeliver hello notification probably because hello registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a><span data-ttu-id="6abb0-160">Bildirim bildirim tooWindows yayını</span><span class="sxs-lookup"><span data-stu-id="6abb0-160">Broadcast toast notification tooWindows</span></span>
<span data-ttu-id="6abb0-161">Bir yayın bildirim bildirim tooWindows istemci gönderirken gönderilen hello üstbilgileri dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6abb0-161">Notice hello headers that get sent out when you are sending a broadcast toast notification tooWindows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="6abb0-162">Bir etiketi (veya etiket ifadesi) belirterek bildirim gönder</span><span class="sxs-lookup"><span data-stu-id="6abb0-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="6abb0-163">Toohello HTTP isteği eklenen bildirimi hello etiketleri HTTP üstbilgisi (Merhaba aşağıdaki örnekte, biz hello bildirim yalnızca tooregistrations 'Spor' yükü gönderiyor)</span><span class="sxs-lookup"><span data-stu-id="6abb0-163">Notice hello Tags HTTP header which gets added toohello HTTP request (in hello example below, we are sending hello notification only tooregistrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="6abb0-164">Birden çok etiket belirtme bildirim gönder</span><span class="sxs-lookup"><span data-stu-id="6abb0-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="6abb0-165">Birden çok etiket gönderildiğinde hello etiketleri HTTP üstbilgisi nasıl değiştiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6abb0-165">Notice how hello Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="6abb0-166">Şablonlu bildirim</span><span class="sxs-lookup"><span data-stu-id="6abb0-166">Templated notification</span></span>
<span data-ttu-id="6abb0-167">Biçim HTTP üstbilgisi değişiklikleri hello ve yükü gövde hello dikkat edin hello HTTP istek gövdesi bir parçası olarak gönderilir:</span><span class="sxs-lookup"><span data-stu-id="6abb0-167">Notice that hello Format HTTP header changes and hello payload body is sent as part of hello HTTP request body:</span></span>

<span data-ttu-id="6abb0-168">**İstemci tarafı - kayıtlı şablonu**</span><span class="sxs-lookup"><span data-stu-id="6abb0-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="6abb0-169">**Sunucu tarafı - Hello yükü gönderme**</span><span class="sxs-lookup"><span data-stu-id="6abb0-169">**Server side - sending hello payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="6abb0-170">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="6abb0-170">Next Steps</span></span>
<span data-ttu-id="6abb0-171">Bu konuda size nasıl basit bir Python toocreate REST gösterdi istemci bildirim hub'ları için.</span><span class="sxs-lookup"><span data-stu-id="6abb0-171">In this topic we showed how toocreate a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="6abb0-172">Buradan şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6abb0-172">From here you can:</span></span>

* <span data-ttu-id="6abb0-173">Merhaba tam karşıdan [Python REST sarmalayıcı örnek], yukarıdaki tüm hello kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="6abb0-173">Download hello full [Python REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="6abb0-174">Bildirim hub'ları özelliği hello etiketleme hakkında bilgi almaya devam etmek [çiğnemekten haber Öğreticisi]</span><span class="sxs-lookup"><span data-stu-id="6abb0-174">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="6abb0-175">Hello bildirim hub'ları şablonları özelliği hakkında bilgi almaya devam etmek [yerelleştirme haber Öğreticisi]</span><span class="sxs-lookup"><span data-stu-id="6abb0-175">Continue learning about Notification Hubs Templates feature in hello [Localizing News tutorial]</span></span>

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

