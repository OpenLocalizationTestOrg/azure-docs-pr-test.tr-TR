---
title: ".NET kullanarak aaaConnecting tooMedia hizmetleri hesabı"
description: "Bu konuda gösterilir nasıl tooconnect tooMedia Hizmetleri kullanarak .NET."
services: media-services
documentationcenter: 
author: juliako
manager: erikre
editor: 
ms.assetid: a8412a29-59dc-44a0-ace0-be79a97dab63
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a23bd285f7cae17ae5831e1e50e73947afbb9a3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="2b1aa-103">TooMedia hizmetleri hesabı .NET için Media Services SDK'sını kullanarak bağlanma</span><span class="sxs-lookup"><span data-stu-id="2b1aa-103">Connecting tooMedia Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2b1aa-104">REST</span><span class="sxs-lookup"><span data-stu-id="2b1aa-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="2b1aa-105">.NET</span><span class="sxs-lookup"><span data-stu-id="2b1aa-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="2b1aa-106">Bu konuda nasıl tooobtain programlı bağlantı tooMicrosoft Azure Media Services ile programlamada hello Media Services SDK'sı için .NET açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services SDK for .NET.</span></span>

## <a name="connecting-toomedia-services"></a><span data-ttu-id="2b1aa-107">TooMedia Hizmetleri bağlanma</span><span class="sxs-lookup"><span data-stu-id="2b1aa-107">Connecting tooMedia Services</span></span>
<span data-ttu-id="2b1aa-108">tooconnect tooMedia Hizmetleri programlı olarak daha önce bir Azure hesabı ayarlamanız, Media Services, hesabında yapılandırılmış ve ardından Visual Studio projesini hello Media Services SDK ile geliştirme .NET için ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-108">tooconnect tooMedia Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with hello Media Services SDK for .NET.</span></span> <span data-ttu-id="2b1aa-109">Daha fazla bilgi için Kurulum geliştirme için .NET için Media Services SDK'sı hello ile bakın.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-109">For more information, see Setup for Development with hello Media Services SDK for .NET.</span></span>

<span data-ttu-id="2b1aa-110">Merhaba işleminin sonunda hello Media Services hesap kurulumu, gerekli hello aşağıdaki aldığınız bağlantı değerleri.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-110">At hello end of hello Media Services account setup process, you obtained hello following required connection values.</span></span> <span data-ttu-id="2b1aa-111">Bu toomake programlı bağlantılarını kullanmak tooMedia Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-111">Use these toomake programmatic connections tooMedia Services.</span></span>

* <span data-ttu-id="2b1aa-112">Media Services hesap adınız.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-112">Your Media Services account name.</span></span>
* <span data-ttu-id="2b1aa-113">Media Services hesabı anahtarınızı.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-113">Your Media Services account key.</span></span>

<span data-ttu-id="2b1aa-114">Bu değerleri, toofind toohello Azure Yönetimi portalı gidin, medya hizmeti hesabınızı seçin ve üzerinde hello "**ANAHTARLARI Yönet**" Merhaba portal penceresinin hello altındaki simgesine.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-114">toofind these values, go toohello Azure Managment Portal, select your Media Service account, and click on hello “**MANAGE KEYS**” icon on hello bottom of hello portal window.</span></span> <span data-ttu-id="2b1aa-115">Merhaba simgesi sonraki tooeach metin kutusu kopyaları hello değeri toohello sistem Pano'ya'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-115">Clicking on hello icon next tooeach text box copies hello value toohello system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="2b1aa-116">CloudMediaContext örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b1aa-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="2b1aa-117">gereksinim duyduğunuz toocreate Hizmetleri medya karşı programlama toostart bir **CloudMediaContext** hello sunucu bağlamı temsil eden örneği.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-117">toostart programming against Media Services you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="2b1aa-118">Merhaba **CloudMediaContext** işleri, varlıklar, dosyaları, erişim ilkeleri ve bulucular dahil olmak üzere başvuruları tooimportant koleksiyonları içerir.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-118">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="2b1aa-119">Merhaba **CloudMediaContext** sınıfı iş parçacığı içinde korumalı değil.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-119">hello **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="2b1aa-120">Yeni bir CloudMediaContext işlem kümesi veya iş parçacığı başına oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="2b1aa-121">CloudMediaContext beş Oluşturucusu aşırı yüklemeye sahip.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="2b1aa-122">Ele önerilen toouse oluşturucular olan **MediaServicesCredentials** bir parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-122">It is recommended toouse constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="2b1aa-123">Merhaba daha fazla bilgi için bkz: **yeniden erişim denetimi hizmeti belirteçleri** , izler.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-123">For more information, see hello **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="2b1aa-124">Merhaba aşağıdaki örnek hello genel CloudMediaContext(MediaServicesCredentials credentials) Oluşturucu kullanır:</span><span class="sxs-lookup"><span data-stu-id="2b1aa-124">hello following example uses hello public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="2b1aa-125">Erişim denetimi hizmeti belirteçleri yeniden kullanma</span><span class="sxs-lookup"><span data-stu-id="2b1aa-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="2b1aa-126">Bu bölümde, nasıl tooreuse erişim denetimi hizmeti MediaServicesCredentials bir parametre olarak geçirmesine CloudMediaContext oluşturucuları kullanarak belirteçleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-126">This section shows how tooreuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="2b1aa-127">[Azure Active Directory erişim denetimi](https://msdn.microsoft.com/library/hh147631.aspx) (erişim denetimi hizmeti veya ACS olarak da bilinir) olan tootheir web uygulamaları kimlik doğrulama ve yetki vererek kullanıcıların toogain erişim kolay bir yol sağlayan bulut tabanlı bir hizmet.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users toogain access tootheir web applications.</span></span> <span data-ttu-id="2b1aa-128">Microsoft Azure Media Services tooits Hizmetleri yine de bir ACS belirteci gerektirir OAuth protokolünün erişimi kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-128">Microsoft Azure Media Services controls access tooits services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="2b1aa-129">Media Services hello ACS belirteçleri bir yetkilendirme sunucusundan alır.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-129">Media Services receives hello ACS tokens from an authorization server.</span></span>

<span data-ttu-id="2b1aa-130">Merhaba Media Services SDK'sı ile geliştirirken, çünkü toonot anlaşma hello belirteçleri ile seçebilirsiniz SDK kod yöneticileri Merhaba, bunları.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-130">When developing with hello Media Services SDK, you can choose toonot deal with hello tokens because hello SDK code managers them for you.</span></span> <span data-ttu-id="2b1aa-131">Ancak, veren hello SDK tam olarak yönetmek hello ACS belirteçleri müşteri adayları toounnecessary belirteç isteklerini.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-131">However, letting hello SDK fully manage hello ACS tokens leads toounnecessary token requests.</span></span> <span data-ttu-id="2b1aa-132">Belirteçleri istediği zaman alır ve hello istemci ve sunucu kaynaklarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-132">Requesting tokens takes time and consumes hello client and server resources.</span></span> <span data-ttu-id="2b1aa-133">Ayrıca, Hello oranı çok yüksek ise hello ACS sunucu hello istekleri kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-133">Also, hello ACS server throttles hello requests if hello rate is too high.</span></span> <span data-ttu-id="2b1aa-134">Merhaba sınırı saniyede 30 istekler, bkz: [ACS Service sınırlamalar](https://msdn.microsoft.com/library/gg185909.aspx) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-134">hello limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="2b1aa-135">Media Services SDK'sı sürüm 3.0.0.0 Hello ile başlayarak, hello ACS belirteçleri yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-135">Starting with hello Media Services SDK version 3.0.0.0, you can reuse hello ACS tokens.</span></span> <span data-ttu-id="2b1aa-136">Merhaba **CloudMediaContext** ele oluşturucular **MediaServicesCredentials** paylaşım hello ACS belirteç birden çok bağlamları arasında bir parametre olarak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-136">hello **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing hello ACS tokens between multiple contexts.</span></span> <span data-ttu-id="2b1aa-137">Merhaba MediaServicesCredentials sınıfı hello Media Services kimlik bilgileri yalıtır.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-137">hello MediaServicesCredentials class encapsulates hello Media Services credentials.</span></span> <span data-ttu-id="2b1aa-138">Bir ACS belirteci kullanılabilir ise ve sona erme zamanı bilinen hello belirteci ile yeni bir MediaServicesCredentials örneği oluşturun ve CloudMediaContext toohello oluşturucusunun geçirin.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with hello token and pass it toohello constructor of CloudMediaContext.</span></span> <span data-ttu-id="2b1aa-139">Süreleri doluncaya her Media Services SDK'sı otomatik olarak hello Not belirteçleri yeniler.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-139">Note that hello Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="2b1aa-140">İki yolu vardır tooreuse ACS belirteçleri hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-140">There are two ways tooreuse ACS tokens, as shown in hello examples below.</span></span>

* <span data-ttu-id="2b1aa-141">Merhaba önbelleğe **MediaServicesCredentials** nesnesinde bellek (örneğin, bir statik sınıf değişkeni).</span><span class="sxs-lookup"><span data-stu-id="2b1aa-141">You can cache hello **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="2b1aa-142">Daha sonra önbelleğe hello nesne toohello CloudMediaContext Oluşturucusu geçirin.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-142">Then, pass hello cached object toohello CloudMediaContext constructor.</span></span> <span data-ttu-id="2b1aa-143">Merhaba MediaServicesCredentials nesne hala geçerliyse, yeniden kullanılabilir bir ACS belirteci içeriyor.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-143">hello MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="2b1aa-144">Media Services SDK'sı hello kimlik bilgilerini kullanarak toohello MediaServicesCredentials Oluşturucusu verilen Hello belirteci tarafından hello yenilenecek geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-144">If hello token is not valid, it will be refreshed by hello Media Services SDK using hello credentials given toohello MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="2b1aa-145">Bu hello Not **MediaServicesCredentials** nesne RefreshToken çağrılır hello sonra geçerli bir belirteci alır.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-145">Note that hello **MediaServicesCredentials** object gets a valid token after hello RefreshToken is called.</span></span> <span data-ttu-id="2b1aa-146">Merhaba **CloudMediaContext** çağrıları hello **RefreshToken** hello Oluşturucusu yöntemi.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-146">hello **CloudMediaContext** calls hello **RefreshToken** method in hello constructor.</span></span> <span data-ttu-id="2b1aa-147">Toosave hello simge değerlerini tooan harici depolama planlıyorsanız, hello belirteci verileri kaydetmeden önce hello TokenExpiration değeri geçerli olup olmadığını toocheck emin olun.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-147">If you are planning toosave hello token values tooan external storage, make sure toocheck whether hello TokenExpiration value is valid before saving hello token data.</span></span> <span data-ttu-id="2b1aa-148">Geçerli durumda değilse, önbelleğe alma önce RefreshToken çağırın.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="2b1aa-149">Merhaba AccessToken dize ve hello TokenExpiration değerleri de önbelleğe alabilir.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-149">You can also cache hello AccessToken string and hello TokenExpiration values.</span></span> <span data-ttu-id="2b1aa-150">Merhaba değerleri daha sonra yeni bir MediaServicesCredentials nesne önbelleğe hello belirteci verilerle kullanılan toocreate olabilir.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-150">hello values could later be used toocreate a new MediaServicesCredentials object with hello cached token data.</span></span>  <span data-ttu-id="2b1aa-151">Bu, özellikle burada hello belirteci güvenli bir şekilde birden çok bilgisayar veya işlemler arasında paylaşılabilir senaryoları için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-151">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="2b1aa-152">Merhaba aşağıdaki kod parçacıkları hello Bu örnekte tanımlanmamış SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage ve UpdateTokenDataInExternalStorageIfNeeded yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-152">hello following code snippets call hello SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="2b1aa-153">Bir dış depolama bu yöntemleri toostore, alma ve güncelleştirme belirteci verileri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-153">You could define these methods toostore, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="2b1aa-154">Simge değerlerini toocreate MediaServicesCredentials kaydedilmiş hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-154">Use hello saved token values toocreate MediaServicesCredentials.</span></span>

        var accessToken = "";
        var tokenExpiration = DateTime.UtcNow;

        // Retrieve saved token values.
        GetTokenDataFromExternalStorage(out accessToken, out tokenExpiration);

        // Create a new MediaServicesCredentials object using saved token values.
        MediaServicesCredentials credentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey)
        {
            AccessToken = accessToken,
            TokenExpiration = tokenExpiration
        };

        CloudMediaContext context2 = new CloudMediaContext(credentials);

    <span data-ttu-id="2b1aa-155">Merhaba belirteci hello Media Services SDK'sı tarafından güncelleştirildi durumda hello belirteci kopyalama güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-155">Update hello token copy in case hello token was updated by hello Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="2b1aa-156">Birden çok Media Services hesabı (örneğin, amaçları veya coğrafi dağıtım paylaşımı yükle) varsa hello System.Collections.Concurrent.ConcurrentDictionary koleksiyonu (hello kullanarak MediaServicesCredentials nesneleri önbelleğe alabilir ConcurrentDictionary koleksiyonu birden çok iş parçacığı tarafından eşzamanlı olarak erişilebilir anahtar/değer çiftlerinin iş parçacığı koleksiyonunu temsil eder).</span><span class="sxs-lookup"><span data-stu-id="2b1aa-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using hello System.Collections.Concurrent.ConcurrentDictionary collection (hello ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="2b1aa-157">Daha sonra hello GetOrAdd yöntemi tooget hello önbelleğe alınmış kimlik bilgilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-157">You can then use hello GetOrAdd method tooget hello cached credentials.</span></span> 
  
        // Declare a static class variable of hello ConcurrentDictionary type in which hello Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials toocreate a new CloudMediaContext object.
        static public CloudMediaContext CreateMediaServicesContext(string accountName, string accountKey)
        {
            CloudMediaContext cloudMediaContext;
            MediaServicesCredentials mediaServicesCredentials;

            mediaServicesCredentials = mediaServicesCredentialsCache.GetOrAdd(
                accountName,
                valueFactory => new MediaServicesCredentials(accountName, accountKey));

            cloudMediaContext = new CloudMediaContext(mediaServicesCredentials);

            return cloudMediaContext;
        }

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a><span data-ttu-id="2b1aa-158">Merhaba Kuzey Çin bölgede bulunan tooa Media Services hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="2b1aa-158">Connecting tooa Media Services account located in hello North China region</span></span>
<span data-ttu-id="2b1aa-159">Hesabınızı hello Kuzey Çin bölgede yer alıyorsa oluşturucudan hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="2b1aa-159">If your account is located in hello North China region, use hello following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="2b1aa-160">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2b1aa-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="2b1aa-161">Yapılandırmada bağlantı değerlerini depolama</span><span class="sxs-lookup"><span data-stu-id="2b1aa-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="2b1aa-162">Bir yüksek oranda önerilen uygulama toostore bağlantı değerleri, özellikle hassas hesap adı ve parola, yapılandırma gibi olur.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-162">It is a highly recommended practice toostore connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="2b1aa-163">Ayrıca, önerilen uygulama tooencrypt önemli yapılandırma verilerini vardır.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-163">Also, it is a recommended practice tooencrypt sensitive configuration data.</span></span> <span data-ttu-id="2b1aa-164">Merhaba tüm yapılandırma dosyası hello Windows şifreleme dosya sistemi (EFS) kullanarak şifreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-164">You can encrypt hello entire configuration file by using hello Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="2b1aa-165">tooenable hello dosyasını sağ tıklatın, bir dosyada EFS seçin **özellikleri**ve hello şifrelemeyi etkinleştirmek **Gelişmiş** Ayarlar sekmesi. Veya korumalı yapılandırmayı kullanarak bir yapılandırma dosyası seçili bölümlerini şifreleme için özel bir çözüm oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-165">tooenable EFS on a file, right-click hello file, select **Properties**, and enable encryption in hello **Advanced** settings tab. Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="2b1aa-166">Bkz: [korumalı yapılandırma kullanarak yapılandırma bilgilerini şifrelemek](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b1aa-166">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="2b1aa-167">Aşağıdaki App.config dosyasına hello gerekli hello bağlantı değerleri içerir.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-167">hello following App.config file contains hello required connection values.</span></span> <span data-ttu-id="2b1aa-168">Merhaba hello değerleri <appSettings> hello Media Services hesabı Kurulum işleminden aldığınız hello gerekli değerleri öğesidir.</span><span class="sxs-lookup"><span data-stu-id="2b1aa-168">hello values in hello <appSettings> element are hello required values that you got from hello Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="2b1aa-169">tooretrieve bağlantı değerleri yapılandırmadan kullanabileceğiniz hello **ConfigurationManager** sınıfı ve hello değerleri toofields kodunuzda atayın:</span><span class="sxs-lookup"><span data-stu-id="2b1aa-169">tooretrieve connection values from configuration, you can use hello **ConfigurationManager** class and then assign hello values toofields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="2b1aa-170">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="2b1aa-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2b1aa-171">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="2b1aa-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

