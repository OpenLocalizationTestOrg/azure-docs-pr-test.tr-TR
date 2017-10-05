---
title: ".NET kullanarak Media Services hesabına bağlanma"
description: "Bu konu, Media Services kullanarak .NET bağlanmak gösterilmiştir."
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
ms.openlocfilehash: 892932116934952265a21ab17aac3434b5760136
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="1bd7b-103">.NET için Media Services SDK'sını kullanarak Media Services hesabı bağlanma</span><span class="sxs-lookup"><span data-stu-id="1bd7b-103">Connecting to Media Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1bd7b-104">REST</span><span class="sxs-lookup"><span data-stu-id="1bd7b-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="1bd7b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="1bd7b-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="1bd7b-106">Bu konu, .NET için Media Services SDK'sı ile programlamada Microsoft Azure Media Services programlama bağlantı elde açıklar.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services SDK for .NET.</span></span>

## <a name="connecting-to-media-services"></a><span data-ttu-id="1bd7b-107">Media Services'e bağlanma</span><span class="sxs-lookup"><span data-stu-id="1bd7b-107">Connecting to Media Services</span></span>
<span data-ttu-id="1bd7b-108">Media Services'e program aracılığıyla bağlanmak için gerekir daha önce bir Azure hesabı ayarlamanız, Media Services, hesabında yapılandırılmış ve ardından Media Services SDK ile geliştirme için Visual Studio projesi için .NET ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-108">To connect to Media Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with the Media Services SDK for .NET.</span></span> <span data-ttu-id="1bd7b-109">Daha fazla bilgi için Kurulum geliştirme için Media Services SDK'sı ile .NET için bkz.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-109">For more information, see Setup for Development with the Media Services SDK for .NET.</span></span>

<span data-ttu-id="1bd7b-110">Media Services hesabı Kurulum işleminin sonunda aşağıdaki gerekli bağlantı değerleri alınır.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-110">At the end of the Media Services account setup process, you obtained the following required connection values.</span></span> <span data-ttu-id="1bd7b-111">Media Services'e program bağlantıları kurmak için bunları kullanın.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-111">Use these to make programmatic connections to Media Services.</span></span>

* <span data-ttu-id="1bd7b-112">Media Services hesap adınız.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-112">Your Media Services account name.</span></span>
* <span data-ttu-id="1bd7b-113">Media Services hesabı anahtarınızı.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-113">Your Media Services account key.</span></span>

<span data-ttu-id="1bd7b-114">Bu değerleri bulmaya Azure Yönetimi Portalı'na medya hizmeti hesabınızı seçin ve tıklayın Git "**ANAHTARLARI Yönet**" portal penceresinin en altındaki simgesi.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-114">To find these values, go to the Azure Managment Portal, select your Media Service account, and click on the “**MANAGE KEYS**” icon on the bottom of the portal window.</span></span> <span data-ttu-id="1bd7b-115">Her bir metin kutusunun yanındaki simgeye tıklandığında söz konusu değer sistem panosuna kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-115">Clicking on the icon next to each text box copies the value to the system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="1bd7b-116">CloudMediaContext örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="1bd7b-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="1bd7b-117">Media Services oluşturmanız karşı programlama başlatmak için bir **CloudMediaContext** sunucu bağlamı temsil eden örneği.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-117">To start programming against Media Services you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="1bd7b-118">**CloudMediaContext** işleri, varlıklar, dosyaları, erişim ilkeleri ve bulucular dahil olmak üzere önemli koleksiyonları başvurular içerir.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-118">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="1bd7b-119">**CloudMediaContext** sınıfı iş parçacığı içinde korumalı değil.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-119">The **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="1bd7b-120">Yeni bir CloudMediaContext işlem kümesi veya iş parçacığı başına oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="1bd7b-121">CloudMediaContext beş Oluşturucusu aşırı yüklemeye sahip.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="1bd7b-122">Ele oluşturucular kullanmak için önerilen **MediaServicesCredentials** bir parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-122">It is recommended to use constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="1bd7b-123">Daha fazla bilgi için bkz: **yeniden erişim denetimi hizmeti belirteçleri** , izler.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-123">For more information, see the **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="1bd7b-124">Aşağıdaki örnek, genel CloudMediaContext(MediaServicesCredentials credentials) Oluşturucu kullanır:</span><span class="sxs-lookup"><span data-stu-id="1bd7b-124">The following example uses the public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="1bd7b-125">Erişim denetimi hizmeti belirteçleri yeniden kullanma</span><span class="sxs-lookup"><span data-stu-id="1bd7b-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="1bd7b-126">Bu bölümde, erişim denetimi hizmeti belirteçleri MediaServicesCredentials bir parametre olarak geçirmesine CloudMediaContext oluşturucuları kullanarak tekrar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-126">This section shows how to reuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="1bd7b-127">[Azure Active Directory erişim denetimi](https://msdn.microsoft.com/library/hh147631.aspx) (erişim denetimi hizmeti veya ACS olarak da bilinir) olan web uygulamalarına erişmek için kimlik doğrulaması ve Kullanıcıları yetkilendirmek kolay bir yol sağlayan bulut tabanlı bir hizmet.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users to gain access to their web applications.</span></span> <span data-ttu-id="1bd7b-128">Microsoft Azure Media Services hizmetlerinin erişimi yine de bir ACS belirteci gerektirir OAuth protokolünün kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-128">Microsoft Azure Media Services controls access to its services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="1bd7b-129">Media Services ACS belirteçleri bir yetkilendirme sunucusundan alır.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-129">Media Services receives the ACS tokens from an authorization server.</span></span>

<span data-ttu-id="1bd7b-130">Media Services SDK'sı ile geliştirirken, SDK kod çünkü yöneticileri belirteçleri ile mücadele etmek değil seçebilirsiniz, bunları.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-130">When developing with the Media Services SDK, you can choose to not deal with the tokens because the SDK code managers them for you.</span></span> <span data-ttu-id="1bd7b-131">Ancak, tam olarak ACS belirteçlerini yönetin SDK izin vererek, gereksiz belirteç isteklerini yol açar.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-131">However, letting the SDK fully manage the ACS tokens leads to unnecessary token requests.</span></span> <span data-ttu-id="1bd7b-132">Belirteçleri istediği zaman alır ve istemci ve sunucu kaynaklarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-132">Requesting tokens takes time and consumes the client and server resources.</span></span> <span data-ttu-id="1bd7b-133">Ayrıca, oranı çok yüksekse, ACS sunucu istekleri kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-133">Also, the ACS server throttles the requests if the rate is too high.</span></span> <span data-ttu-id="1bd7b-134">Sınıra 30 saniye başına isteklerinin bkz. [ACS Service sınırlamalar](https://msdn.microsoft.com/library/gg185909.aspx) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-134">The limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="1bd7b-135">Media Services SDK sürüm 3.0.0.0 ile başlayarak, ACS belirteç yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-135">Starting with the Media Services SDK version 3.0.0.0, you can reuse the ACS tokens.</span></span> <span data-ttu-id="1bd7b-136">**CloudMediaContext** ele oluşturucular **MediaServicesCredentials** parametre olarak ACS belirteç birden çok bağlamları arasında paylaşımını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-136">The **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing the ACS tokens between multiple contexts.</span></span> <span data-ttu-id="1bd7b-137">MediaServicesCredentials sınıfı Media Services kimlik bilgileri yalıtır.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-137">The MediaServicesCredentials class encapsulates the Media Services credentials.</span></span> <span data-ttu-id="1bd7b-138">Bir ACS belirteci kullanılabilir ise ve sona erme zamanı bilinen belirteç ile yeni bir MediaServicesCredentials örneği oluşturun ve CloudMediaContext oluşturucuya geçirin.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with the token and pass it to the constructor of CloudMediaContext.</span></span> <span data-ttu-id="1bd7b-139">Not süreleri doluncaya her Media Services SDK'sı belirteçleri otomatik olarak yeniler.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-139">Note that the Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="1bd7b-140">Aşağıdaki örneklerde gösterildiği gibi ACS belirteçleri yeniden kullanmak için iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-140">There are two ways to reuse ACS tokens, as shown in the examples below.</span></span>

* <span data-ttu-id="1bd7b-141">Önbelleğe alabilir **MediaServicesCredentials** nesnesinde bellek (örneğin, bir statik sınıf değişkeni).</span><span class="sxs-lookup"><span data-stu-id="1bd7b-141">You can cache the **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="1bd7b-142">Daha sonra önbelleğe alınmış nesnenin CloudMediaContext oluşturucuya geçirin.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-142">Then, pass the cached object to the CloudMediaContext constructor.</span></span> <span data-ttu-id="1bd7b-143">MediaServicesCredentials nesne hala geçerliyse, yeniden kullanılabilir bir ACS belirteci içeriyor.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-143">The MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="1bd7b-144">Belirtecin geçerli değilse MediaServicesCredentials oluşturucuya verilen kimlik bilgilerini kullanarak Media Services SDK'sı tarafından yenilenecektir.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-144">If the token is not valid, it will be refreshed by the Media Services SDK using the credentials given to the MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="1bd7b-145">Unutmayın **MediaServicesCredentials** nesnesini RefreshToken çağrıldıktan sonra geçerli bir belirteci alır.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-145">Note that the **MediaServicesCredentials** object gets a valid token after the RefreshToken is called.</span></span> <span data-ttu-id="1bd7b-146">**CloudMediaContext** çağrıları **RefreshToken** oluşturucuda yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-146">The **CloudMediaContext** calls the **RefreshToken** method in the constructor.</span></span> <span data-ttu-id="1bd7b-147">Bir dış depolama birimine simge değerlerini kaydetmeyi planlıyorsanız, belirteç verileri kaydetmeden önce TokenExpiration değerinin geçerli olup olmadığını denetlemek emin olun.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-147">If you are planning to save the token values to an external storage, make sure to check whether the TokenExpiration value is valid before saving the token data.</span></span> <span data-ttu-id="1bd7b-148">Geçerli durumda değilse, önbelleğe alma önce RefreshToken çağırın.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use the cached credentials to create a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="1bd7b-149">AccessToken dize ve TokenExpiration değerleri de önbelleğe alabilir.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-149">You can also cache the AccessToken string and the TokenExpiration values.</span></span> <span data-ttu-id="1bd7b-150">Değerleri daha sonra önbelleğe alınan belirteç verilerle yeni bir MediaServicesCredentials nesnesi oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-150">The values could later be used to create a new MediaServicesCredentials object with the cached token data.</span></span>  <span data-ttu-id="1bd7b-151">Bu, özellikle burada belirteç güvenli bir şekilde birden çok bilgisayar veya işlemler arasında paylaşılabilir senaryoları için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-151">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="1bd7b-152">Aşağıdaki kod parçacıkları Bu örnekte tanımlanmamış SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage ve UpdateTokenDataInExternalStorageIfNeeded yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-152">The following code snippets call the SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="1bd7b-153">Bir dış depolama birimine belirteci verileri güncelleştirmek depolamak ve almak için bu yöntemleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-153">You could define these methods to store, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from the context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // The SaveTokenDataToExternalStorage method should check 
        // whether the TokenExpiration value is valid before saving the token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="1bd7b-154">Kaydedilen belirteç değerler MediaServicesCredentials oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-154">Use the saved token values to create MediaServicesCredentials.</span></span>

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

    <span data-ttu-id="1bd7b-155">Belirteç Media Services SDK'sı tarafından güncelleştirildi durumda belirteci kopyalama güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-155">Update the token copy in case the token was updated by the Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="1bd7b-156">Birden çok Media Services hesabı (örneğin, amaçları veya coğrafi dağıtım paylaşımı yükle) varsa (ConcurrentDictionary System.Collections.Concurrent.ConcurrentDictionary koleksiyonu kullanarak MediaServicesCredentials nesneleri önbelleğe alabilir koleksiyon birden çok iş parçacığı tarafından eşzamanlı olarak erişilebilir anahtar/değer çiftleri iş parçacığı koleksiyonu temsil eder).</span><span class="sxs-lookup"><span data-stu-id="1bd7b-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using the System.Collections.Concurrent.ConcurrentDictionary collection (the ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="1bd7b-157">Ardından, önbelleğe alınmış kimlik bilgilerini almak için GetOrAdd yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-157">You can then use the GetOrAdd method to get the cached credentials.</span></span> 
  
        // Declare a static class variable of the ConcurrentDictionary type in which the Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials to create a new CloudMediaContext object.
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

## <a name="connecting-to-a-media-services-account-located-in-the-north-china-region"></a><span data-ttu-id="1bd7b-158">Kuzey Çin bölgede bulunan bir Media Services hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="1bd7b-158">Connecting to a Media Services account located in the North China region</span></span>
<span data-ttu-id="1bd7b-159">Hesabınızı Kuzey Çin bölgede yer alıyorsa, aşağıdaki oluşturucuyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1bd7b-159">If your account is located in the North China region, use the following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="1bd7b-160">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1bd7b-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="1bd7b-161">Yapılandırmada bağlantı değerlerini depolama</span><span class="sxs-lookup"><span data-stu-id="1bd7b-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="1bd7b-162">Bağlantı değerleri, özellikle hassas hesap adı ve parola gibi yapılandırmasında depolamak için yüksek oranda önerilen bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-162">It is a highly recommended practice to store connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="1bd7b-163">Ayrıca, önemli yapılandırma verilerini şifrelemek önerilen yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-163">Also, it is a recommended practice to encrypt sensitive configuration data.</span></span> <span data-ttu-id="1bd7b-164">Tüm yapılandırma dosyasını Windows şifreleme dosya sistemi (EFS) kullanarak şifreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-164">You can encrypt the entire configuration file by using the Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="1bd7b-165">EFS dosya üzerinde etkinleştirmek için dosyaya sağ tıklayın, **özellikleri**ve şifreleme etkinleştirmek **Gelişmiş** Ayarlar sekmesi.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-165">To enable EFS on a file, right-click the file, select **Properties**, and enable encryption in the **Advanced** settings tab.</span></span> <span data-ttu-id="1bd7b-166">Veya korumalı yapılandırmayı kullanarak bir yapılandırma dosyası seçili bölümlerini şifreleme için özel bir çözüm oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-166">Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="1bd7b-167">Bkz: [korumalı yapılandırma kullanarak yapılandırma bilgilerini şifrelemek](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="1bd7b-167">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="1bd7b-168">Aşağıdaki App.config dosyası gerekli bağlantı değerleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-168">The following App.config file contains the required connection values.</span></span> <span data-ttu-id="1bd7b-169">Değerler <appSettings> Media Services hesabı Kurulum işleminden aldığınız gerekli değerleri öğesidir.</span><span class="sxs-lookup"><span data-stu-id="1bd7b-169">The values in the <appSettings> element are the required values that you got from the Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="1bd7b-170">Bağlantı değerleri yapılandırmasından almak için kullanabileceğiniz **ConfigurationManager** sınıfı ve kodunuzu alanlarına değerler atayın:</span><span class="sxs-lookup"><span data-stu-id="1bd7b-170">To retrieve connection values from configuration, you can use the **ConfigurationManager** class and then assign the values to fields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="1bd7b-171">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="1bd7b-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1bd7b-172">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="1bd7b-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

