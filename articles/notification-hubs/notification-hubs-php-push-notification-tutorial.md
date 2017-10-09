---
title: "aaaHow toouse PHP ile bildirim hub'ları"
description: "Bilgi nasıl toouse Azure Notification Hubs bir PHP arka uçtan."
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
ms.openlocfilehash: 6cd426286a684006a07867fcf44a8ff71be7efa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-php"></a><span data-ttu-id="10076-103">Nasıl toouse php'den Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="10076-103">How toouse Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="10076-104">Bir PHP/Java/Ruby arka ucunu tüm bildirim hub'ları özelliklere erişebilir hello MSDN konuda açıklandığı gibi hello bildirim hub'ı REST arabirimini kullanarak [bildirim hub'ları REST API'leri](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="10076-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="10076-105">Bu konudaki gösteriyoruz nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="10076-105">In this topic we show how to:</span></span>

* <span data-ttu-id="10076-106">PHP Notification Hubs özellikleri için bir REST istemci oluşturun;</span><span class="sxs-lookup"><span data-stu-id="10076-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="10076-107">Merhaba izleyin [Get öğreticisinde](notification-hubs-ios-apple-push-notification-apns-get-started.md) hello arka uç bölümü PHP ile uygulama tercih ettiğiniz mobil platformunuz için.</span><span class="sxs-lookup"><span data-stu-id="10076-107">Follow hello [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing hello back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="10076-108">İstemci arabirimi</span><span class="sxs-lookup"><span data-stu-id="10076-108">Client interface</span></span>
<span data-ttu-id="10076-109">Merhaba ana istemci arabirimi hello kullanılabilir aynı yöntemleri hello sağlayabilir [.NET Notification Hubs SDK'sı](http://msdn.microsoft.com/library/jj933431.aspx), bu, olanak tanır toodirectly Çevir tüm hello öğreticiler ve bu site şu anda kullanılabilir örnekleri ve Merhaba hello topluluğu tarafından katkıda Internet.</span><span class="sxs-lookup"><span data-stu-id="10076-109">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="10076-110">Hello kullanılabilir tüm hello kod Bul [PHP REST sarmalayıcı örnek].</span><span class="sxs-lookup"><span data-stu-id="10076-110">You can find all hello code available in hello [PHP REST wrapper sample].</span></span>

<span data-ttu-id="10076-111">Örneğin, toocreate bir istemci:</span><span class="sxs-lookup"><span data-stu-id="10076-111">For example, toocreate a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="10076-112">toosend bir iOS yerel bildirimi:</span><span class="sxs-lookup"><span data-stu-id="10076-112">toosend an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="10076-113">Uygulama</span><span class="sxs-lookup"><span data-stu-id="10076-113">Implementation</span></span>
<span data-ttu-id="10076-114">Zaten yaptıysanız Lütfen izleyin bizim [Get öğreticisinde] yukarı tooimplement hello arka uç olduğu toohello son bölümü.</span><span class="sxs-lookup"><span data-stu-id="10076-114">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>
<span data-ttu-id="10076-115">Ayrıca, isterseniz hello hello koddan kullanabilirsiniz [PHP REST sarmalayıcı örnek] ve doğrudan toohello Git [tam hello öğretici](#complete-tutorial) bölümü.</span><span class="sxs-lookup"><span data-stu-id="10076-115">Also, if you want you can use hello code from hello [PHP REST wrapper sample] and go directly toohello [Complete hello tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="10076-116">Tüm Ayrıntılar tooimplement tam REST sarmalayıcı bulunabilir hello [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="10076-116">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="10076-117">Bu bölümde biz hello ana adım gerekli tooaccess bildirim hub'ları REST uç noktalarını hello PHP uygulaması anlatmaktadır:</span><span class="sxs-lookup"><span data-stu-id="10076-117">In this section we will describe hello PHP implementation of hello main steps required tooaccess Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="10076-118">Merhaba bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="10076-118">Parse hello connection string</span></span>
2. <span data-ttu-id="10076-119">Merhaba yetkilendirme belirteci oluştur</span><span class="sxs-lookup"><span data-stu-id="10076-119">Generate hello authorization token</span></span>
3. <span data-ttu-id="10076-120">Merhaba HTTP çağrısı yapmak</span><span class="sxs-lookup"><span data-stu-id="10076-120">Perform hello HTTP call</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="10076-121">Merhaba bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="10076-121">Parse hello connection string</span></span>
<span data-ttu-id="10076-122">Merhaba ana sınıfı uygulama hello istemci, hello bağlantı dizesini ayrıştırmak için olan Oluşturucusu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="10076-122">Here is hello main class implementing hello client, whose constructor that parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="10076-123">Güvenlik belirteci oluşturma</span><span class="sxs-lookup"><span data-stu-id="10076-123">Create security token</span></span>
<span data-ttu-id="10076-124">Merhaba güvenlik belirteci oluşturma Hello ayrıntılarını kullanılabilir [burada](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="10076-124">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="10076-125">Merhaba aşağıdaki yöntemi sahip eklenen toobe toohello **NotificationHub** hello hello geçerli istek ve hello bağlantı dizesinden ayıklanan hello kimlik URI'sini temel sınıf toocreate hello simgesi.</span><span class="sxs-lookup"><span data-stu-id="10076-125">hello following method has toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification"></a><span data-ttu-id="10076-126">Bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="10076-126">Send a notification</span></span>
<span data-ttu-id="10076-127">İlk olarak, bir bildirim temsil eden bir sınıf bize tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="10076-127">First, let us define a class representing a notification.</span></span>

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

<span data-ttu-id="10076-128">Bu sınıf bir yerel bildirim gövdesi veya bir şablon bildirim durumunun özellikleri kümesi ve biçimini (yerel platform veya şablon) ve (örneğin, Apple sona erme özelliği ve WNS platforma özgü özellikleri içeren bir üstbilgi kümesi için bir kapsayıcıdır üst bilgiler).</span><span class="sxs-lookup"><span data-stu-id="10076-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="10076-129">Lütfen toohello bakın [bildirim hub'ları REST API belgelerine](http://msdn.microsoft.com/library/dn495827.aspx) ve tüm kullanılabilir seçenekleri hello için belirli bildirim platformları biçimleri hello.</span><span class="sxs-lookup"><span data-stu-id="10076-129">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="10076-130">Bu sınıfla çağrılmak, biz şimdi hello gönderme hello içinde bildirim yöntemleri yazabilirsiniz **NotificationHub** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="10076-130">Armed with this class, we can now write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

        // Send hello request
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

<span data-ttu-id="10076-131">Merhaba yöntemleri yukarıda bir HTTP POST isteği toohello /messages uç noktasını, bildirim hub ' ınızı hello doğru gövde ve üstbilgileri toosend hello bildirim gönderin.</span><span class="sxs-lookup"><span data-stu-id="10076-131">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

## <span data-ttu-id="10076-132"><a name="complete-tutorial"></a>Tam başlangıç Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="10076-132"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="10076-133">Şimdi bir PHP arka ucunu hello bildirim göndererek hello Başlarken Öğreticisi tamamlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10076-133">Now you can complete hello Get Started tutorial by sending hello notification from a PHP back-end.</span></span>

<span data-ttu-id="10076-134">Bildirim hub'ları istemciniz başlatılamıyor (hello belirtildiği gibi hello bağlantı dizenizi ve hub adı yerine [Get öğreticisinde]):</span><span class="sxs-lookup"><span data-stu-id="10076-134">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="10076-135">Ardından, hedef mobil platforma bağlı olarak hello gönderme kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="10076-135">Then add hello send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="10076-136">Windows mağazası ve Windows Phone 8.1 (Silverlight olmayan)</span><span class="sxs-lookup"><span data-stu-id="10076-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="10076-137">iOS</span><span class="sxs-lookup"><span data-stu-id="10076-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="10076-138">Android</span><span class="sxs-lookup"><span data-stu-id="10076-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="10076-139">Windows Phone 8.0 ve 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="10076-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
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


### <a name="kindle-fire"></a><span data-ttu-id="10076-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="10076-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="10076-141">PHP kodunuzu çalıştırmaya şimdi, hedef cihazda görünen bir bildirim üretir.</span><span class="sxs-lookup"><span data-stu-id="10076-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10076-142">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="10076-142">Next Steps</span></span>
<span data-ttu-id="10076-143">Bu konuda size nasıl basit bir Java toocreate REST gösterdi istemci bildirim hub'ları için.</span><span class="sxs-lookup"><span data-stu-id="10076-143">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="10076-144">Buradan şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="10076-144">From here you can:</span></span>

* <span data-ttu-id="10076-145">Merhaba tam karşıdan [PHP REST sarmalayıcı örnek], yukarıdaki tüm hello kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="10076-145">Download hello full [PHP REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="10076-146">Bildirim hub'ları hello [çiğnemekten haber öğretici] özelliği etiketleme hakkında bilgi almaya devam etmek</span><span class="sxs-lookup"><span data-stu-id="10076-146">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="10076-147">[Kullanıcılara bildirme öğreticide] bildirimleri tooindividual kullanıcılar Ftp'den hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="10076-147">Learn about pushing notifications tooindividual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="10076-148">Daha fazla bilgi için hello Ayrıca bkz. [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="10076-148">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[PHP REST sarmalayıcı örnek]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[Get öğreticisinde]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

