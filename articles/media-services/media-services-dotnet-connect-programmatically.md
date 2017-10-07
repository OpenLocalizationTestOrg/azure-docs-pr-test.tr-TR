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
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a>TooMedia hizmetleri hesabı .NET için Media Services SDK'sını kullanarak bağlanma
> [!div class="op_single_selector"]
> * [REST](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

Bu konuda nasıl tooobtain programlı bağlantı tooMicrosoft Azure Media Services ile programlamada hello Media Services SDK'sı için .NET açıklanmaktadır.

## <a name="connecting-toomedia-services"></a>TooMedia Hizmetleri bağlanma
tooconnect tooMedia Hizmetleri programlı olarak daha önce bir Azure hesabı ayarlamanız, Media Services, hesabında yapılandırılmış ve ardından Visual Studio projesini hello Media Services SDK ile geliştirme .NET için ayarlamanız gerekir. Daha fazla bilgi için Kurulum geliştirme için .NET için Media Services SDK'sı hello ile bakın.

Merhaba işleminin sonunda hello Media Services hesap kurulumu, gerekli hello aşağıdaki aldığınız bağlantı değerleri. Bu toomake programlı bağlantılarını kullanmak tooMedia Hizmetleri.

* Media Services hesap adınız.
* Media Services hesabı anahtarınızı.

Bu değerleri, toofind toohello Azure Yönetimi portalı gidin, medya hizmeti hesabınızı seçin ve üzerinde hello "**ANAHTARLARI Yönet**" Merhaba portal penceresinin hello altındaki simgesine. Merhaba simgesi sonraki tooeach metin kutusu kopyaları hello değeri toohello sistem Pano'ya'yı tıklatın.

## <a name="creating-a-cloudmediacontext-instance"></a>CloudMediaContext örneği oluşturma
gereksinim duyduğunuz toocreate Hizmetleri medya karşı programlama toostart bir **CloudMediaContext** hello sunucu bağlamı temsil eden örneği. Merhaba **CloudMediaContext** işleri, varlıklar, dosyaları, erişim ilkeleri ve bulucular dahil olmak üzere başvuruları tooimportant koleksiyonları içerir.

> [!NOTE]
> Merhaba **CloudMediaContext** sınıfı iş parçacığı içinde korumalı değil. Yeni bir CloudMediaContext işlem kümesi veya iş parçacığı başına oluşturmanız gerekir.
> 
> 

CloudMediaContext beş Oluşturucusu aşırı yüklemeye sahip. Ele önerilen toouse oluşturucular olan **MediaServicesCredentials** bir parametre olarak. Merhaba daha fazla bilgi için bkz: **yeniden erişim denetimi hizmeti belirteçleri** , izler. 

Merhaba aşağıdaki örnek hello genel CloudMediaContext(MediaServicesCredentials credentials) Oluşturucu kullanır:

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a>Erişim denetimi hizmeti belirteçleri yeniden kullanma
Bu bölümde, nasıl tooreuse erişim denetimi hizmeti MediaServicesCredentials bir parametre olarak geçirmesine CloudMediaContext oluşturucuları kullanarak belirteçleri gösterir.

[Azure Active Directory erişim denetimi](https://msdn.microsoft.com/library/hh147631.aspx) (erişim denetimi hizmeti veya ACS olarak da bilinir) olan tootheir web uygulamaları kimlik doğrulama ve yetki vererek kullanıcıların toogain erişim kolay bir yol sağlayan bulut tabanlı bir hizmet. Microsoft Azure Media Services tooits Hizmetleri yine de bir ACS belirteci gerektirir OAuth protokolünün erişimi kontrol eder. Media Services hello ACS belirteçleri bir yetkilendirme sunucusundan alır.

Merhaba Media Services SDK'sı ile geliştirirken, çünkü toonot anlaşma hello belirteçleri ile seçebilirsiniz SDK kod yöneticileri Merhaba, bunları. Ancak, veren hello SDK tam olarak yönetmek hello ACS belirteçleri müşteri adayları toounnecessary belirteç isteklerini. Belirteçleri istediği zaman alır ve hello istemci ve sunucu kaynaklarını kullanır. Ayrıca, Hello oranı çok yüksek ise hello ACS sunucu hello istekleri kısıtlar. Merhaba sınırı saniyede 30 istekler, bkz: [ACS Service sınırlamalar](https://msdn.microsoft.com/library/gg185909.aspx) daha fazla ayrıntı için.

Media Services SDK'sı sürüm 3.0.0.0 Hello ile başlayarak, hello ACS belirteçleri yeniden kullanabilirsiniz. Merhaba **CloudMediaContext** ele oluşturucular **MediaServicesCredentials** paylaşım hello ACS belirteç birden çok bağlamları arasında bir parametre olarak etkinleştirin. Merhaba MediaServicesCredentials sınıfı hello Media Services kimlik bilgileri yalıtır. Bir ACS belirteci kullanılabilir ise ve sona erme zamanı bilinen hello belirteci ile yeni bir MediaServicesCredentials örneği oluşturun ve CloudMediaContext toohello oluşturucusunun geçirin. Süreleri doluncaya her Media Services SDK'sı otomatik olarak hello Not belirteçleri yeniler. İki yolu vardır tooreuse ACS belirteçleri hello aşağıdaki örnekte gösterildiği gibi.

* Merhaba önbelleğe **MediaServicesCredentials** nesnesinde bellek (örneğin, bir statik sınıf değişkeni). Daha sonra önbelleğe hello nesne toohello CloudMediaContext Oluşturucusu geçirin. Merhaba MediaServicesCredentials nesne hala geçerliyse, yeniden kullanılabilir bir ACS belirteci içeriyor. Media Services SDK'sı hello kimlik bilgilerini kullanarak toohello MediaServicesCredentials Oluşturucusu verilen Hello belirteci tarafından hello yenilenecek geçerli değil.
  
    Bu hello Not **MediaServicesCredentials** nesne RefreshToken çağrılır hello sonra geçerli bir belirteci alır. Merhaba **CloudMediaContext** çağrıları hello **RefreshToken** hello Oluşturucusu yöntemi. Toosave hello simge değerlerini tooan harici depolama planlıyorsanız, hello belirteci verileri kaydetmeden önce hello TokenExpiration değeri geçerli olup olmadığını toocheck emin olun. Geçerli durumda değilse, önbelleğe alma önce RefreshToken çağırın.
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* Merhaba AccessToken dize ve hello TokenExpiration değerleri de önbelleğe alabilir. Merhaba değerleri daha sonra yeni bir MediaServicesCredentials nesne önbelleğe hello belirteci verilerle kullanılan toocreate olabilir.  Bu, özellikle burada hello belirteci güvenli bir şekilde birden çok bilgisayar veya işlemler arasında paylaşılabilir senaryoları için kullanışlıdır.
  
    Merhaba aşağıdaki kod parçacıkları hello Bu örnekte tanımlanmamış SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage ve UpdateTokenDataInExternalStorageIfNeeded yöntemlerini çağırın. Bir dış depolama bu yöntemleri toostore, alma ve güncelleştirme belirteci verileri tanımlayabilirsiniz. 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    Simge değerlerini toocreate MediaServicesCredentials kaydedilmiş hello kullanın.

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

    Merhaba belirteci hello Media Services SDK'sı tarafından güncelleştirildi durumda hello belirteci kopyalama güncelleştirin. 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* Birden çok Media Services hesabı (örneğin, amaçları veya coğrafi dağıtım paylaşımı yükle) varsa hello System.Collections.Concurrent.ConcurrentDictionary koleksiyonu (hello kullanarak MediaServicesCredentials nesneleri önbelleğe alabilir ConcurrentDictionary koleksiyonu birden çok iş parçacığı tarafından eşzamanlı olarak erişilebilir anahtar/değer çiftlerinin iş parçacığı koleksiyonunu temsil eder). Daha sonra hello GetOrAdd yöntemi tooget hello önbelleğe alınmış kimlik bilgilerini kullanabilirsiniz. 
  
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

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a>Merhaba Kuzey Çin bölgede bulunan tooa Media Services hesabına bağlanma
Hesabınızı hello Kuzey Çin bölgede yer alıyorsa oluşturucudan hello kullanın:

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

Örneğin:

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a>Yapılandırmada bağlantı değerlerini depolama
Bir yüksek oranda önerilen uygulama toostore bağlantı değerleri, özellikle hassas hesap adı ve parola, yapılandırma gibi olur. Ayrıca, önerilen uygulama tooencrypt önemli yapılandırma verilerini vardır. Merhaba tüm yapılandırma dosyası hello Windows şifreleme dosya sistemi (EFS) kullanarak şifreleyebilirsiniz. tooenable hello dosyasını sağ tıklatın, bir dosyada EFS seçin **özellikleri**ve hello şifrelemeyi etkinleştirmek **Gelişmiş** Ayarlar sekmesi. Veya korumalı yapılandırmayı kullanarak bir yapılandırma dosyası seçili bölümlerini şifreleme için özel bir çözüm oluşturabilirsiniz. Bkz: [korumalı yapılandırma kullanarak yapılandırma bilgilerini şifrelemek](https://msdn.microsoft.com/library/53tyfkaw.aspx).

Aşağıdaki App.config dosyasına hello gerekli hello bağlantı değerleri içerir. Merhaba hello değerleri <appSettings> hello Media Services hesabı Kurulum işleminden aldığınız hello gerekli değerleri öğesidir.

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


tooretrieve bağlantı değerleri yapılandırmadan kullanabileceğiniz hello **ConfigurationManager** sınıfı ve hello değerleri toofields kodunuzda atayın:

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

