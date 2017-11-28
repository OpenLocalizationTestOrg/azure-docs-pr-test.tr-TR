---
title: "PHP ile bildirim hub'ları kullanma"
description: "Bir PHP arka ucunu Azure bildirim hub'ları kullanmayı öğrenin."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 0156f994-96d0-4878-b07b-49b7be4fd856
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: php
ms.devlang: php
ms.topic: article
ms.date: 06/07/2016
ms.author: yuaxu
ms.openlocfilehash: c27b6308ff528224a0398e0ff40537db05417bb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-php"></a><span data-ttu-id="c71ed-103">Php'den Notification Hubs kullanma</span><span class="sxs-lookup"><span data-stu-id="c71ed-103">How to use Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="c71ed-104">Bir PHP/Java/Ruby MSDN konusunda açıklandığı gibi bildirim hub'ı REST arabirimini kullanarak uç tüm bildirim hub'ları özellikleri erişebileceğiniz [bildirim hub'ları REST API'leri](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="c71ed-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="c71ed-105">Bu konudaki gösteriyoruz nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="c71ed-105">In this topic we show how to:</span></span>

* <span data-ttu-id="c71ed-106">PHP Notification Hubs özellikleri için bir REST istemci oluşturun;</span><span class="sxs-lookup"><span data-stu-id="c71ed-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="c71ed-107">İzleyin [Get öğreticisinde](notification-hubs-ios-apple-push-notification-apns-get-started.md) seçim için mobil platformda, arka uç bölümü PHP ile uygulama.</span><span class="sxs-lookup"><span data-stu-id="c71ed-107">Follow the [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing the back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="c71ed-108">İstemci arabirimi</span><span class="sxs-lookup"><span data-stu-id="c71ed-108">Client interface</span></span>
<span data-ttu-id="c71ed-109">Ana istemci arabirimi bulunan aynı yöntemleri sağlayabilir [.NET Notification Hubs SDK'sı](http://msdn.microsoft.com/library/jj933431.aspx), bu öğreticiler ve bu site şu anda kullanılabilir örnekleri doğrudan Çevir olanak sağlar ve katkıda bulunan Internet üzerindeki topluluğu.</span><span class="sxs-lookup"><span data-stu-id="c71ed-109">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="c71ed-110">Kullanılabilir tüm kod Bul [PHP REST sarmalayıcı örnek].</span><span class="sxs-lookup"><span data-stu-id="c71ed-110">You can find all the code available in the [PHP REST wrapper sample].</span></span>

<span data-ttu-id="c71ed-111">Örneğin, bir istemci oluşturmak için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="c71ed-111">For example, to create a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="c71ed-112">Bir iOS yerel bildirim göndermek için:</span><span class="sxs-lookup"><span data-stu-id="c71ed-112">To send an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="c71ed-113">Uygulama</span><span class="sxs-lookup"><span data-stu-id="c71ed-113">Implementation</span></span>
<span data-ttu-id="c71ed-114">Zaten yaptıysanız Lütfen izleyin bizim [Get öğreticisinde] son uç uygulamak için sahip olduğu bölüm yukarı.</span><span class="sxs-lookup"><span data-stu-id="c71ed-114">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>
<span data-ttu-id="c71ed-115">Ayrıca, isterseniz koddan kullanabilirsiniz [PHP REST sarmalayıcı örnek] ve doğrudan gitmek [öğreticiye](#complete-tutorial) bölümü.</span><span class="sxs-lookup"><span data-stu-id="c71ed-115">Also, if you want you can use the code from the [PHP REST wrapper sample] and go directly to the [Complete the tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="c71ed-116">Tam bir REST sarmalayıcı uygulamak için tüm ayrıntıları bulunabilir [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="c71ed-116">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="c71ed-117">Bu bölümde biz PHP uygulaması bildirim hub'ları REST uç noktalarını erişmek için gerekli ana adım anlatmaktadır:</span><span class="sxs-lookup"><span data-stu-id="c71ed-117">In this section we will describe the PHP implementation of the main steps required to access Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="c71ed-118">Bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="c71ed-118">Parse the connection string</span></span>
2. <span data-ttu-id="c71ed-119">Yetkilendirme belirteci oluştur</span><span class="sxs-lookup"><span data-stu-id="c71ed-119">Generate the authorization token</span></span>
3. <span data-ttu-id="c71ed-120">HTTP çağrısı yapmak</span><span class="sxs-lookup"><span data-stu-id="c71ed-120">Perform the HTTP call</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="c71ed-121">Bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="c71ed-121">Parse the connection string</span></span>
<span data-ttu-id="c71ed-122">İstemci, bağlantı dizesini ayrıştırmak için olan Oluşturucusu uygulama ana sınıfı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="c71ed-122">Here is the main class implementing the client, whose constructor that parses the connection string:</span></span>

    class NotificationHub {
        const API_VERSION = "?api-version=2013-10";

        private $endpoint;
        private $hubPath;
        private $sasKeyName;
        private $sasKeyValue;

        function __construct($connectionString, $hubPath) {
            $this->hubPath = $hubPath;

            $this->parseConnectionString($connectionString);
        }

        private function parseConnectionString($connectionString) {
            $parts = explode(";", $connectionString);
            if (sizeof($parts) != 3) {
                throw new Exception("Error parsing connection string: " . $connectionString);
            }

            foreach ($parts as $part) {
                if (strpos($part, "Endpoint") === 0) {
                    $this->endpoint = "https" . substr($part, 11);
                } else if (strpos($part, "SharedAccessKeyName") === 0) {
                    $this->sasKeyName = substr($part, 20);
                } else if (strpos($part, "SharedAccessKey") === 0) {
                    $this->sasKeyValue = substr($part, 16);
                }
            }
        }
    }


### <a name="create-security-token"></a><span data-ttu-id="c71ed-123">Güvenlik belirteci oluşturma</span><span class="sxs-lookup"><span data-stu-id="c71ed-123">Create security token</span></span>
<span data-ttu-id="c71ed-124">Güvenlik belirteci oluşturma ayrıntılarını kullanılabilir [burada](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="c71ed-124">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="c71ed-125">Eklenecek aşağıdaki yöntemi sahip **NotificationHub** geçerli istek ve kimlik bilgileri bağlantı dizesinden ayıklanan URI'sini temel belirteç oluşturmak için sınıfı.</span><span class="sxs-lookup"><span data-stu-id="c71ed-125">The following method has to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

    private function generateSasToken($uri) {
        $targetUri = strtolower(rawurlencode(strtolower($uri)));

        $expires = time();
        $expiresInMins = 60;
        $expires = $expires + $expiresInMins * 60;
        $toSign = $targetUri . "\n" . $expires;

        $signature = rawurlencode(base64_encode(hash_hmac('sha256', $toSign, $this->sasKeyValue, TRUE)));

        $token = "SharedAccessSignature sr=" . $targetUri . "&sig="
                    . $signature . "&se=" . $expires . "&skn=" . $this->sasKeyName;

        return $token;
    }

### <a name="send-a-notification"></a><span data-ttu-id="c71ed-126">Bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="c71ed-126">Send a notification</span></span>
<span data-ttu-id="c71ed-127">İlk olarak, bir bildirim temsil eden bir sınıf bize tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c71ed-127">First, let us define a class representing a notification.</span></span>

    class Notification {
        public $format;
        public $payload;

        # array with keynames for headers
        # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
        # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
        public $headers;

        function __construct($format, $payload) {
            if (!in_array($format, ["template", "apple", "windows", "gcm", "windowsphone"])) {
                throw new Exception('Invalid format: ' . $format);
            }

            $this->format = $format;
            $this->payload = $payload;
        }
    }

<span data-ttu-id="c71ed-128">Bu sınıf bir yerel bildirim gövdesi veya bir şablon bildirim durumunun özellikleri kümesi ve biçimini (yerel platform veya şablon) ve (örneğin, Apple sona erme özelliği ve WNS platforma özgü özellikleri içeren bir üstbilgi kümesi için bir kapsayıcıdır üst bilgiler).</span><span class="sxs-lookup"><span data-stu-id="c71ed-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="c71ed-129">Lütfen [bildirim hub'ları REST API belgelerine](http://msdn.microsoft.com/library/dn495827.aspx) ve kullanabileceğiniz tüm seçenekler için belirli bildirim platformları biçimleri.</span><span class="sxs-lookup"><span data-stu-id="c71ed-129">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="c71ed-130">Bu sınıfla çağrılmak, biz Şimdi Gönder içinde bildirim yöntemleri yazabilirsiniz **NotificationHub** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="c71ed-130">Armed with this class, we can now write the send notification methods inside of the **NotificationHub** class.</span></span>

    public function sendNotification($notification, $tagsOrTagExpression="") {
        if (is_array($tagsOrTagExpression)) {
            $tagExpression = implode(" || ", $tagsOrTagExpression);
        } else {
            $tagExpression = $tagsOrTagExpression;
        }

        # build uri
        $uri = $this->endpoint . $this->hubPath . "/messages" . NotificationHub::API_VERSION;
        $ch = curl_init($uri);

        if (in_array($notification->format, ["template", "apple", "gcm"])) {
            $contentType = "application/json";
        } else {
            $contentType = "application/xml";
        }

        $token = $this->generateSasToken($uri);

        $headers = [
            'Authorization: '.$token,
            'Content-Type: '.$contentType,
            'ServiceBusNotification-Format: '.$notification->format
        ];

        if ("" !== $tagExpression) {
            $headers[] = 'ServiceBusNotification-Tags: '.$tagExpression;
        }

        # add headers for other platforms
        if (is_array($notification->headers)) {
            $headers = array_merge($headers, $notification->headers);
        }

        curl_setopt_array($ch, array(
            CURLOPT_POST => TRUE,
            CURLOPT_RETURNTRANSFER => TRUE,
            CURLOPT_SSL_VERIFYPEER => FALSE,
            CURLOPT_HTTPHEADER => $headers,
            CURLOPT_POSTFIELDS => $notification->payload
        ));

        // Send the request
        $response = curl_exec($ch);

        // Check for errors
        if($response === FALSE){
            throw new Exception(curl_error($ch));
        }

        $info = curl_getinfo($ch);

        if ($info['http_code'] <> 201) {
            throw new Exception('Error sending notificaiton: '. $info['http_code'] . ' msg: ' . $response);
        }
    } 

<span data-ttu-id="c71ed-131">Yukarıdaki yöntemler, bildirim hub ' ınızı doğru gövde ve bildirim göndermek için üstbilgiler /messages uç noktası bir HTTP POST isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="c71ed-131">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

## <span data-ttu-id="c71ed-132"><a name="complete-tutorial"></a>Öğreticiyi Tamamla</span><span class="sxs-lookup"><span data-stu-id="c71ed-132"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="c71ed-133">Şimdi bir PHP arka ucunu bildirim göndererek Başlarken Öğreticisi tamamlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c71ed-133">Now you can complete the Get Started tutorial by sending the notification from a PHP back-end.</span></span>

<span data-ttu-id="c71ed-134">Bildirim hub'ları istemciniz başlatılamıyor (belirtildiği gibi bağlantı dizenizi ve hub adı yerine [Get öğreticisinde]):</span><span class="sxs-lookup"><span data-stu-id="c71ed-134">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="c71ed-135">Ardından, hedef mobil platforma bağlı olarak gönderme kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c71ed-135">Then add the send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="c71ed-136">Windows mağazası ve Windows Phone 8.1 (Silverlight olmayan)</span><span class="sxs-lookup"><span data-stu-id="c71ed-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="c71ed-137">iOS</span><span class="sxs-lookup"><span data-stu-id="c71ed-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="c71ed-138">Android</span><span class="sxs-lookup"><span data-stu-id="c71ed-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="c71ed-139">Windows Phone 8.0 ve 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="c71ed-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    $toast = '<?xml version="1.0" encoding="utf-8"?>' .
                '<wp:Notification xmlns:wp="WPNotification">' .
                   '<wp:Toast>' .
                        '<wp:Text1>Hello from PHP!</wp:Text1>' .
                   '</wp:Toast> ' .
                '</wp:Notification>';
    $notification = new Notification("windowsphone", $toast);
    $notification->headers[] = 'X-WindowsPhone-Target : toast';
    $notification->headers[] = 'X-NotificationClass : 2';
    $hub->sendNotification($notification, null);


### <a name="kindle-fire"></a><span data-ttu-id="c71ed-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="c71ed-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="c71ed-141">PHP kodunuzu çalıştırmaya şimdi, hedef cihazda görünen bir bildirim üretir.</span><span class="sxs-lookup"><span data-stu-id="c71ed-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c71ed-142">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c71ed-142">Next Steps</span></span>
<span data-ttu-id="c71ed-143">Bu konuda size bildirim hub'ları için basit bir Java REST istemcisi nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c71ed-143">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="c71ed-144">Buradan şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c71ed-144">From here you can:</span></span>

* <span data-ttu-id="c71ed-145">Tam karşıdan [PHP REST sarmalayıcı örnek], yukarıdaki tüm kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="c71ed-145">Download the full [PHP REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="c71ed-146">Bildirim hub'ları özelliği [çiğnemekten haber öğreticide] etiketleme hakkında bilgi almaya devam etmek</span><span class="sxs-lookup"><span data-stu-id="c71ed-146">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="c71ed-147">Bildirimleri bireysel kullanıcılara [kullanıcılara bildirme öğreticide] İtme hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="c71ed-147">Learn about pushing notifications to individual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="c71ed-148">Daha fazla bilgi için Ayrıca bkz. [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="c71ed-148">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="c71ed-149">[PHP REST sarmalayıcı örnek]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php</span><span class="sxs-lookup"><span data-stu-id="c71ed-149">[PHP REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php</span></span>
<span data-ttu-id="c71ed-150">[Get öğreticisinde]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/</span><span class="sxs-lookup"><span data-stu-id="c71ed-150">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/</span></span>

