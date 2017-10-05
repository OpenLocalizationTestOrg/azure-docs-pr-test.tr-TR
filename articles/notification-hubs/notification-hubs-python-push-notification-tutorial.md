---
title: "Bildirim hub'ları Python ile kullanma"
description: "Bir Python arka ucunu Azure bildirim hub'ları kullanmayı öğrenin."
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
ms.openlocfilehash: 9ceedb9940759427fc8cec74a1307e42472563a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-python"></a><span data-ttu-id="cff42-103">Python'dan bildirim hub'ları kullanma</span><span class="sxs-lookup"><span data-stu-id="cff42-103">How to use Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="cff42-104">Bir Java/PHP/Python/Ruby MSDN konusunda açıklandığı gibi bildirim hub'ı REST arabirimini kullanarak uç tüm bildirim hub'ları özellikleri erişebileceğiniz [bildirim hub'ları REST API'leri](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="cff42-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="cff42-105">Bu bildirim gönderir Python içinde uygulamak için bir örnek başvuru uygulamasıdır ve resmi olarak desteklenen bildirim hub'ı Python SDK'sı değil.</span><span class="sxs-lookup"><span data-stu-id="cff42-105">This is a sample reference implementation for implementing the notification sends in Python and is not the officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="cff42-106">Bu örnek, Python 3.4 kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="cff42-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="cff42-107">Bu konudaki gösteriyoruz nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="cff42-107">In this topic we show how to:</span></span>

* <span data-ttu-id="cff42-108">REST istemcisi Python Notification Hubs özellikleri için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cff42-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="cff42-109">Bildirim hub'ı REST API'lerine Python arabirimi kullanarak bildirimleri gönderin.</span><span class="sxs-lookup"><span data-stu-id="cff42-109">Send notifications using the Python interface to the Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="cff42-110">Bir HTTP REST istek/yanıt dökümü için hata ayıklama/eğitim amaçlı alın.</span><span class="sxs-lookup"><span data-stu-id="cff42-110">Get a dump of the HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="cff42-111">İzleyebileceğiniz [Get öğreticisinde](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) seçim için mobil platformda, arka uç bölümü Python içinde uygulama.</span><span class="sxs-lookup"><span data-stu-id="cff42-111">You can follow the [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing the back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="cff42-112">Örnek kapsamını yalnızca bildirimleri göndermek için sınırlı ve herhangi bir kayıt yönetim yapmaz.</span><span class="sxs-lookup"><span data-stu-id="cff42-112">The scope of the sample is only limited to send notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="cff42-113">İstemci arabirimi</span><span class="sxs-lookup"><span data-stu-id="cff42-113">Client interface</span></span>
<span data-ttu-id="cff42-114">Ana istemci arabirimi bulunan aynı yöntemleri sağlayabilir [.NET Notification Hubs SDK'sı](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="cff42-114">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="cff42-115">Bu öğreticiler ve bu site şu anda kullanılabilir örnekleri doğrudan Çevir olanak sağlar ve Internet üzerindeki topluluk tarafından katkısı.</span><span class="sxs-lookup"><span data-stu-id="cff42-115">This will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="cff42-116">Kullanılabilir tüm kod Bul [Python REST sarmalayıcı örnek].</span><span class="sxs-lookup"><span data-stu-id="cff42-116">You can find all the code available in the [Python REST wrapper sample].</span></span>

<span data-ttu-id="cff42-117">Örneğin, bir istemci oluşturmak için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="cff42-117">For example, to create a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="cff42-118">Windows bildirim göndermek için:</span><span class="sxs-lookup"><span data-stu-id="cff42-118">To send a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="cff42-119">Uygulama</span><span class="sxs-lookup"><span data-stu-id="cff42-119">Implementation</span></span>
<span data-ttu-id="cff42-120">Zaten yaptıysanız Lütfen izleyin bizim [Get öğreticisinde] son uç uygulamak için sahip olduğu bölüm yukarı.</span><span class="sxs-lookup"><span data-stu-id="cff42-120">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>

<span data-ttu-id="cff42-121">Tam bir REST sarmalayıcı uygulamak için tüm ayrıntıları bulunabilir [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="cff42-121">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="cff42-122">Bu bölümde biz Python uygulaması bildirim hub'ları REST uç noktalarını erişmek ve bildirimleri göndermek için gerekli ana adımlar açıklanmıştır</span><span class="sxs-lookup"><span data-stu-id="cff42-122">In this section we will describe the Python implementation of the main steps required to access Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="cff42-123">Bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="cff42-123">Parse the connection string</span></span>
2. <span data-ttu-id="cff42-124">Yetkilendirme belirteci oluştur</span><span class="sxs-lookup"><span data-stu-id="cff42-124">Generate the authorization token</span></span>
3. <span data-ttu-id="cff42-125">HTTP REST API kullanarak bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="cff42-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="cff42-126">Bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="cff42-126">Parse the connection string</span></span>
<span data-ttu-id="cff42-127">Oluşturucusu bağlantı dizesini ayrıştırmak için bir istemci uygulama ana sınıfı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="cff42-127">Here is the main class implementing the client, whose constructor parses the connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="cff42-128">Güvenlik belirteci oluşturma</span><span class="sxs-lookup"><span data-stu-id="cff42-128">Create security token</span></span>
<span data-ttu-id="cff42-129">Güvenlik belirteci oluşturma ayrıntılarını kullanılabilir [burada](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="cff42-129">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="cff42-130">Aşağıdaki yöntemlerden eklenecek zorunda **NotificationHub** geçerli istek ve kimlik bilgileri bağlantı dizesinden ayıklanan URI'sini temel belirteç oluşturmak için sınıfı.</span><span class="sxs-lookup"><span data-stu-id="cff42-130">The following methods have to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="cff42-131">HTTP REST API kullanarak bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="cff42-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="cff42-132">Birincisi, let tanımlamak bir bildirim temsil eden sınıf.</span><span class="sxs-lookup"><span data-stu-id="cff42-132">First, let use define a class representing a notification.</span></span>

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of the following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

<span data-ttu-id="cff42-133">Bu sınıf, bir yerel bildirim gövdesi veya bir şablon bildirim biçimi (yerel platform veya şablon) ve platforma özgü özellikleri (örneğin, Apple sona erme özelliği ve WNS üstbilgileri) içeren bir dizi üstbilgileri durumunda özellikler kümesi için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="cff42-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="cff42-134">Lütfen [bildirim hub'ları REST API belgelerine](http://msdn.microsoft.com/library/dn495827.aspx) ve kullanabileceğiniz tüm seçenekler için belirli bildirim platformları biçimleri.</span><span class="sxs-lookup"><span data-stu-id="cff42-134">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="cff42-135">Bu sınıf ile biz Gönder içinde bildirim yöntemleri yazabilirsiniz artık **NotificationHub** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="cff42-135">Now with this class, we can write the send notification methods inside of the **NotificationHub** class.</span></span>

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about the PNS send notification outcome
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

        # add the tags/tag expressions to the headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers to the headers collection that the user may have added
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

<span data-ttu-id="cff42-136">Yukarıdaki yöntemler, bildirim hub ' ınızı doğru gövde ve bildirim göndermek için üstbilgiler /messages uç noktası bir HTTP POST isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="cff42-136">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

### <a name="using-debug-property-to-enable-detailed-logging"></a><span data-ttu-id="cff42-137">Ayrıntılı günlük kaydını etkinleştirmek için hata ayıklama özelliğini kullanma</span><span class="sxs-lookup"><span data-stu-id="cff42-137">Using debug property to enable detailed logging</span></span>
<span data-ttu-id="cff42-138">HTTP isteğiyle ilgili ayrıntılı günlük kaydı bilgileri bildirim hub'ı başlatılırken hata ayıklama özelliğini etkinleştirme yazılır ve ayrıntılı bir bildirim iletisi yanı sıra yanıt döküm sonucunu gönderin.</span><span class="sxs-lookup"><span data-stu-id="cff42-138">Enabling debug property while initializing the Notification Hub will write out detailed logging information about the HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="cff42-139">Son olarak adlandırılan bu özellik eklediğimiz [bildirim hub'ları TestSend özelliği](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) bildirim gönderme sonucunu hakkında ayrıntılı bilgiler döndürür.</span><span class="sxs-lookup"><span data-stu-id="cff42-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about the notification send outcome.</span></span> <span data-ttu-id="cff42-140">-Kullanmak için aşağıdakileri kullanarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="cff42-140">To use it - initialize using the following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="cff42-141">Bildirim hub'ı İsteği Gönder HTTP URL'si, "test" sorgu dizesi ile sonuç olarak eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="cff42-141">The Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="cff42-142"><a name="complete-tutorial"></a>Öğreticiyi Tamamla</span><span class="sxs-lookup"><span data-stu-id="cff42-142"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="cff42-143">Şimdi bir Python arka ucunu bildirim göndererek Başlarken Öğreticisi tamamlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cff42-143">Now you can complete the Get Started tutorial by sending the notification from a Python back-end.</span></span>

<span data-ttu-id="cff42-144">Bildirim hub'ları istemciniz başlatılamıyor (belirtildiği gibi bağlantı dizenizi ve hub adı yerine [Get öğreticisinde]):</span><span class="sxs-lookup"><span data-stu-id="cff42-144">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="cff42-145">Ardından, hedef mobil platforma bağlı olarak gönderme kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cff42-145">Then add the send code depending on your target mobile platform.</span></span> <span data-ttu-id="cff42-146">Bu örnek ayrıca örneğin send_windows_notification Windows platform göre gönderen bildirimlerini etkinleştirmek için daha yüksek düzey yöntemleri ekler; (için apple) send_apple_notification vs.</span><span class="sxs-lookup"><span data-stu-id="cff42-146">This sample also adds higher level methods to enable sending notifications based on the platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="cff42-147">Windows mağazası ve Windows Phone 8.1 (Silverlight olmayan)</span><span class="sxs-lookup"><span data-stu-id="cff42-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="cff42-148">Windows Phone 8.0 ve 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="cff42-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="cff42-149">iOS</span><span class="sxs-lookup"><span data-stu-id="cff42-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="cff42-150">Android</span><span class="sxs-lookup"><span data-stu-id="cff42-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="cff42-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="cff42-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="cff42-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="cff42-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="cff42-153">Python kodunuzu çalıştıran hedef aygıtınızda görünen bir bildirim üretir.</span><span class="sxs-lookup"><span data-stu-id="cff42-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="cff42-154">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="cff42-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="cff42-155">Hata ayıklama özelliğini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="cff42-155">Enabling debug property</span></span>
<span data-ttu-id="cff42-156">Hata ayıklama bayrağı hangi HTTP üstbilgileri istekte geçirilir ve hangi HTTP yanıtı bildirim Hub'ından alınan burada anlamak aşağıdaki gibi NotificationOutcome yanı sıra ayrıntılı HTTP isteği ve yanıt döküm görür NotificationHub başlatılırken etkinleştirdiğinizde:![][1]</span><span class="sxs-lookup"><span data-stu-id="cff42-156">When you enable debug flag while initializing the NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like the following where you can understand what HTTP headers are passed in the request and what HTTP response was received from the Notification Hub: ![][1]</span></span>

<span data-ttu-id="cff42-157">Bildirim hub'ı sonuç ayrıntılı örneğin görürsünüz</span><span class="sxs-lookup"><span data-stu-id="cff42-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="cff42-158">ileti başarıyla için anında iletilen bildirim servisi gönderildiğinde.</span><span class="sxs-lookup"><span data-stu-id="cff42-158">when the message is successfully sent to the Push Notification Service.</span></span> 
  
        <Outcome>The Notification was successfully sent to the Push Notification System</Outcome>
* <span data-ttu-id="cff42-159">Herhangi bir anında bildirim bulunan hiçbir hedef olsaydı sonra büyük olasılıkla aşağıdaki (hangi kayıtları eşleşmeyen bazı etiketler olduğundan bildirim büyük olasılıkla teslim etmek için bulunan herhangi bir kayıt olduğunu gösterir) yanıt görmek için olmaz</span><span class="sxs-lookup"><span data-stu-id="cff42-159">If there were no targets found for any push notification then you are likely going to see the following in the response (which indicates that there were no registrations found to deliver the notification probably because the registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-to-windows"></a><span data-ttu-id="cff42-160">Windows bildirim yayını</span><span class="sxs-lookup"><span data-stu-id="cff42-160">Broadcast toast notification to Windows</span></span>
<span data-ttu-id="cff42-161">Windows İstemcisi için yayın bildirim gönderirken gönderilen üstbilgileri dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="cff42-161">Notice the headers that get sent out when you are sending a broadcast toast notification to Windows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="cff42-162">Bir etiketi (veya etiket ifadesi) belirterek bildirim gönder</span><span class="sxs-lookup"><span data-stu-id="cff42-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="cff42-163">HTTP isteği eklenen etiketleri HTTP üstbilgisi dikkat edin (aşağıdaki örnekte, biz bildirim yalnızca 'Spor' yükü kayıtlarla gönderme)</span><span class="sxs-lookup"><span data-stu-id="cff42-163">Notice the Tags HTTP header which gets added to the HTTP request (in the example below, we are sending the notification only to registrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="cff42-164">Birden çok etiket belirtme bildirim gönder</span><span class="sxs-lookup"><span data-stu-id="cff42-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="cff42-165">Birden çok etiket gönderildiğinde etiketleri HTTP üstbilgisi nasıl değiştiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="cff42-165">Notice how the Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="cff42-166">Şablonlu bildirim</span><span class="sxs-lookup"><span data-stu-id="cff42-166">Templated notification</span></span>
<span data-ttu-id="cff42-167">Biçim HTTP üstbilgisi değişiklikleri dikkat edin ve yük gövde HTTP isteği gövdesinin bir parçası olarak gönderilir:</span><span class="sxs-lookup"><span data-stu-id="cff42-167">Notice that the Format HTTP header changes and the payload body is sent as part of the HTTP request body:</span></span>

<span data-ttu-id="cff42-168">**İstemci tarafı - kayıtlı şablonu**</span><span class="sxs-lookup"><span data-stu-id="cff42-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="cff42-169">**Sunucu tarafı - yükü gönderme**</span><span class="sxs-lookup"><span data-stu-id="cff42-169">**Server side - sending the payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="cff42-170">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="cff42-170">Next Steps</span></span>
<span data-ttu-id="cff42-171">Bu konuda size bildirim hub'ları için basit bir Python REST istemcisi nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="cff42-171">In this topic we showed how to create a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="cff42-172">Buradan şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cff42-172">From here you can:</span></span>

* <span data-ttu-id="cff42-173">Tam karşıdan [Python REST sarmalayıcı örnek], yukarıdaki tüm kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="cff42-173">Download the full [Python REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="cff42-174">Bildirim hub'ları özelliği etiketleme hakkında bilgi almaya devam etmek [çiğnemekten haber Öğreticisi]</span><span class="sxs-lookup"><span data-stu-id="cff42-174">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="cff42-175">Bildirim hub'ları şablonları özelliği hakkında bilgi almaya devam etmek [yerelleştirme haber Öğreticisi]</span><span class="sxs-lookup"><span data-stu-id="cff42-175">Continue learning about Notification Hubs Templates feature in the [Localizing News tutorial]</span></span>

<!-- URLs -->
<span data-ttu-id="cff42-176">[Python REST sarmalayıcı örnek]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span><span class="sxs-lookup"><span data-stu-id="cff42-176">[Python REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span></span>
<span data-ttu-id="cff42-177">[Get öğreticisinde]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="cff42-177">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="cff42-178">[çiğnemekten haber Öğreticisi]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="cff42-178">[Breaking News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span></span>
<span data-ttu-id="cff42-179">[yerelleştirme haber Öğreticisi]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="cff42-179">[Localizing News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

