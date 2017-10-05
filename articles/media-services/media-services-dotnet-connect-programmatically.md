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
# <a name="connecting-to-media-services-account-using-media-services-sdk-for-net"></a>.NET için Media Services SDK'sını kullanarak Media Services hesabı bağlanma
> [!div class="op_single_selector"]
> * [REST](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

Bu konu, .NET için Media Services SDK'sı ile programlamada Microsoft Azure Media Services programlama bağlantı elde açıklar.

## <a name="connecting-to-media-services"></a>Media Services'e bağlanma
Media Services'e program aracılığıyla bağlanmak için gerekir daha önce bir Azure hesabı ayarlamanız, Media Services, hesabında yapılandırılmış ve ardından Media Services SDK ile geliştirme için Visual Studio projesi için .NET ayarlayın. Daha fazla bilgi için Kurulum geliştirme için Media Services SDK'sı ile .NET için bkz.

Media Services hesabı Kurulum işleminin sonunda aşağıdaki gerekli bağlantı değerleri alınır. Media Services'e program bağlantıları kurmak için bunları kullanın.

* Media Services hesap adınız.
* Media Services hesabı anahtarınızı.

Bu değerleri bulmaya Azure Yönetimi Portalı'na medya hizmeti hesabınızı seçin ve tıklayın Git "**ANAHTARLARI Yönet**" portal penceresinin en altındaki simgesi. Her bir metin kutusunun yanındaki simgeye tıklandığında söz konusu değer sistem panosuna kopyalanır.

## <a name="creating-a-cloudmediacontext-instance"></a>CloudMediaContext örneği oluşturma
Media Services oluşturmanız karşı programlama başlatmak için bir **CloudMediaContext** sunucu bağlamı temsil eden örneği. **CloudMediaContext** işleri, varlıklar, dosyaları, erişim ilkeleri ve bulucular dahil olmak üzere önemli koleksiyonları başvurular içerir.

> [!NOTE]
> **CloudMediaContext** sınıfı iş parçacığı içinde korumalı değil. Yeni bir CloudMediaContext işlem kümesi veya iş parçacığı başına oluşturmanız gerekir.
> 
> 

CloudMediaContext beş Oluşturucusu aşırı yüklemeye sahip. Ele oluşturucular kullanmak için önerilen **MediaServicesCredentials** bir parametre olarak. Daha fazla bilgi için bkz: **yeniden erişim denetimi hizmeti belirteçleri** , izler. 

Aşağıdaki örnek, genel CloudMediaContext(MediaServicesCredentials credentials) Oluşturucu kullanır:

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a>Erişim denetimi hizmeti belirteçleri yeniden kullanma
Bu bölümde, erişim denetimi hizmeti belirteçleri MediaServicesCredentials bir parametre olarak geçirmesine CloudMediaContext oluşturucuları kullanarak tekrar gösterilmektedir.

[Azure Active Directory erişim denetimi](https://msdn.microsoft.com/library/hh147631.aspx) (erişim denetimi hizmeti veya ACS olarak da bilinir) olan web uygulamalarına erişmek için kimlik doğrulaması ve Kullanıcıları yetkilendirmek kolay bir yol sağlayan bulut tabanlı bir hizmet. Microsoft Azure Media Services hizmetlerinin erişimi yine de bir ACS belirteci gerektirir OAuth protokolünün kontrol eder. Media Services ACS belirteçleri bir yetkilendirme sunucusundan alır.

Media Services SDK'sı ile geliştirirken, SDK kod çünkü yöneticileri belirteçleri ile mücadele etmek değil seçebilirsiniz, bunları. Ancak, tam olarak ACS belirteçlerini yönetin SDK izin vererek, gereksiz belirteç isteklerini yol açar. Belirteçleri istediği zaman alır ve istemci ve sunucu kaynaklarını kullanır. Ayrıca, oranı çok yüksekse, ACS sunucu istekleri kısıtlar. Sınıra 30 saniye başına isteklerinin bkz. [ACS Service sınırlamalar](https://msdn.microsoft.com/library/gg185909.aspx) daha fazla ayrıntı için.

Media Services SDK sürüm 3.0.0.0 ile başlayarak, ACS belirteç yeniden kullanabilirsiniz. **CloudMediaContext** ele oluşturucular **MediaServicesCredentials** parametre olarak ACS belirteç birden çok bağlamları arasında paylaşımını etkinleştirin. MediaServicesCredentials sınıfı Media Services kimlik bilgileri yalıtır. Bir ACS belirteci kullanılabilir ise ve sona erme zamanı bilinen belirteç ile yeni bir MediaServicesCredentials örneği oluşturun ve CloudMediaContext oluşturucuya geçirin. Not süreleri doluncaya her Media Services SDK'sı belirteçleri otomatik olarak yeniler. Aşağıdaki örneklerde gösterildiği gibi ACS belirteçleri yeniden kullanmak için iki yolu vardır.

* Önbelleğe alabilir **MediaServicesCredentials** nesnesinde bellek (örneğin, bir statik sınıf değişkeni). Daha sonra önbelleğe alınmış nesnenin CloudMediaContext oluşturucuya geçirin. MediaServicesCredentials nesne hala geçerliyse, yeniden kullanılabilir bir ACS belirteci içeriyor. Belirtecin geçerli değilse MediaServicesCredentials oluşturucuya verilen kimlik bilgilerini kullanarak Media Services SDK'sı tarafından yenilenecektir.
  
    Unutmayın **MediaServicesCredentials** nesnesini RefreshToken çağrıldıktan sonra geçerli bir belirteci alır. **CloudMediaContext** çağrıları **RefreshToken** oluşturucuda yöntemi. Bir dış depolama birimine simge değerlerini kaydetmeyi planlıyorsanız, belirteç verileri kaydetmeden önce TokenExpiration değerinin geçerli olup olmadığını denetlemek emin olun. Geçerli durumda değilse, önbelleğe alma önce RefreshToken çağırın.
  
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use the cached credentials to create a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* AccessToken dize ve TokenExpiration değerleri de önbelleğe alabilir. Değerleri daha sonra önbelleğe alınan belirteç verilerle yeni bir MediaServicesCredentials nesnesi oluşturmak için kullanılabilir.  Bu, özellikle burada belirteç güvenli bir şekilde birden çok bilgisayar veya işlemler arasında paylaşılabilir senaryoları için kullanışlıdır.
  
    Aşağıdaki kod parçacıkları Bu örnekte tanımlanmamış SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage ve UpdateTokenDataInExternalStorageIfNeeded yöntemlerini çağırın. Bir dış depolama birimine belirteci verileri güncelleştirmek depolamak ve almak için bu yöntemleri tanımlayabilirsiniz. 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from the context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // The SaveTokenDataToExternalStorage method should check 
        // whether the TokenExpiration value is valid before saving the token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    Kaydedilen belirteç değerler MediaServicesCredentials oluşturmak için kullanın.

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

    Belirteç Media Services SDK'sı tarafından güncelleştirildi durumda belirteci kopyalama güncelleştirin. 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* Birden çok Media Services hesabı (örneğin, amaçları veya coğrafi dağıtım paylaşımı yükle) varsa (ConcurrentDictionary System.Collections.Concurrent.ConcurrentDictionary koleksiyonu kullanarak MediaServicesCredentials nesneleri önbelleğe alabilir koleksiyon birden çok iş parçacığı tarafından eşzamanlı olarak erişilebilir anahtar/değer çiftleri iş parçacığı koleksiyonu temsil eder). Ardından, önbelleğe alınmış kimlik bilgilerini almak için GetOrAdd yöntemi kullanabilirsiniz. 
  
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

## <a name="connecting-to-a-media-services-account-located-in-the-north-china-region"></a>Kuzey Çin bölgede bulunan bir Media Services hesabına bağlanma
Hesabınızı Kuzey Çin bölgede yer alıyorsa, aşağıdaki oluşturucuyu kullanın:

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

Örneğin:

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a>Yapılandırmada bağlantı değerlerini depolama
Bağlantı değerleri, özellikle hassas hesap adı ve parola gibi yapılandırmasında depolamak için yüksek oranda önerilen bir yöntemdir. Ayrıca, önemli yapılandırma verilerini şifrelemek önerilen yöntemdir. Tüm yapılandırma dosyasını Windows şifreleme dosya sistemi (EFS) kullanarak şifreleyebilirsiniz. EFS dosya üzerinde etkinleştirmek için dosyaya sağ tıklayın, **özellikleri**ve şifreleme etkinleştirmek **Gelişmiş** Ayarlar sekmesi. Veya korumalı yapılandırmayı kullanarak bir yapılandırma dosyası seçili bölümlerini şifreleme için özel bir çözüm oluşturabilirsiniz. Bkz: [korumalı yapılandırma kullanarak yapılandırma bilgilerini şifrelemek](https://msdn.microsoft.com/library/53tyfkaw.aspx).

Aşağıdaki App.config dosyası gerekli bağlantı değerleri içerir. Değerler <appSettings> Media Services hesabı Kurulum işleminden aldığınız gerekli değerleri öğesidir.

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


Bağlantı değerleri yapılandırmasından almak için kullanabileceğiniz **ConfigurationManager** sınıfı ve kodunuzu alanlarına değerler atayın:

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

