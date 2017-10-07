---
title: "Azure Notification Hubs ve Bing uzamsal veri ile aaaGeo korumalı anında iletme bildirimleri | Microsoft Docs"
description: "Bu öğreticide, nasıl toodeliver konum temelli anında iletme bildirimleri Azure Notification Hubs ve Bing uzamsal veri ile öğreneceksiniz."
services: notification-hubs
documentationcenter: windows
keywords: "anında iletme bildirimi, anında iletme bildirimi"
author: dend
manager: yuaxu
editor: dend
ms.assetid: f41beea1-0d62-4418-9ffc-c9d70607a1b7
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/31/2016
ms.author: dendeli
ms.openlocfilehash: d6efe473537f2159240c53e780741f12619c045d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a>Azure Notification Hubs ve Bing Uzamsal Veri ile bölge sınırlamalı anında iletme bildirimleri
> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).
> 
> 

Bu öğreticide, nasıl toodeliver konum temelli anında iletme bildirimleri ile Azure Notification Hubs ve Bing uzamsal gelen bir evrensel Windows Platform uygulaması içinde kullanılan veri öğreneceksiniz.

## <a name="prerequisites"></a>Ön koşullar
Öncelikle, tüm hello yazılım ve hizmet önkoşullarına sahip olduğunuzdan emin toomake gerekir:

* [Visual Studio 2015 Güncelleştirmesi 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) veya üzeri ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) da geçerli olur). 
* En son sürümünü hello [Azure SDK'sı](https://azure.microsoft.com/downloads/). 
* [Bing Haritalar Geliştirme Merkezi hesabı](https://www.bingmapsportal.com/) (ücretsiz bir tane oluşturabilir ve Microsoft hesabınızla ilişkilendirebilirsiniz). 

## <a name="getting-started"></a>Başlarken
Başlangıç projesi oluşturarak başlayalım. Visual Studio'da **Boş Uygulama (Evrensel Windows)** türü yeni bir proje başlatın.

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

Merhaba proje oluşturmayı tamamladıktan sonra hello uygulama kendisi için hello donanımınız olması gerekir. Şimdi hello bölge sınırlama altyapısı için her şeyi ayarlayalım. Biz bu için Bing Hizmetleri giderek toouse olduğundan, bize tooquery belirli konum çerçevelerini sağlayan ortak bir REST API uç noktası vardır:

    http://spatial.virtualearth.net/REST/v1/data/

Toospecify gerekir hello parametreleri tooget onu çalışma:

* **Veri Kaynağı Kimliği** ve **Veri Kaynağı Adı**: Veri kaynakları, Bing Haritalar API'sinde konumlar ve çalışma saatleri gibi kümelenmiş çeşitli meta veriler içerir. Burada, bunlar hakkında daha fazla bilgi edinebilirsiniz. 
* **Varlık adı** – hello istediğiniz toouse bir başvuru noktası olarak hello bildirimi varlığı. 
* **Bing Haritalar API'si anahtarı** – bu hello Bing Geliştirme Merkezi hesabı oluşturduğunuzda, daha önce aldığınız hello anahtardır.

Şimdi derin Dalış hello kurulumunu her yukarıdaki hello öğeler için yapın.

## <a name="setting-up-hello-data-source"></a>Merhaba veri kaynağını ayarlama
Merhaba Bing Haritalar geliştirme Merkezi'nde yapabilirsiniz. Yalnızca tıklayın **veri kaynakları** hello üst gezinti çubuğu ve select içinde **veri kaynaklarını yönet**.

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

Önce Bing Haritalar API'si ile çalışmadıysanız büyük olasılıkla olmayacaktır herhangi bir veri kaynağı mevcut, böylece yalnızca karşıya yükleme veri tooa veri kaynağında'ı tıklatarak yeni bir tane oluşturabilirsiniz. Tüm hello gerekli alanları doldurduğunuzdan emin olun:

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

Merak ediyor olabilirsiniz hello veri dosyası nedir ve neleri karşıya yüklemeniz? Bu test Hello amaçları doğrultusunda, biz yalnızca, bir alanı hello San Francisco rıhtımının çerçeve hello kanal tabanlı örneği kullanabilirsiniz:

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

Yukarıdaki Hello bu varlığı temsil eder:

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

Yalnızca kopyalayın ve yukarıdaki hello dizeyi yeni bir dosyaya yapıştırın ve olarak kaydedin **NotificationHubsGeofence.pipe**ve hello Bing geliştirme Merkezi'ne yükleyin.

> [!NOTE]
> İstendiğinde toospecify hello için yeni bir anahtar olabilir **ana anahtar** hello farklı **sorgu anahtarını**. Yalnızca hello Pano ve yenileme hello veri kaynağını karşıya yükleme sayfasını aracılığıyla yeni bir anahtar oluşturun.
> 
> 

Merhaba veri dosyasını karşıya yükledikten sonra toomake hello veri kaynağını yayımladığınızdan emin gerekir. 

Çok Git**veri kaynaklarını yönet**, tıpkı yaptığımız, hello listede veri kaynağınızı bulun ve tıklayın **Yayımla** hello içinde **Eylemler** sütun. İçinde bir bit hello veri kaynağınızı görmeniz gerekir **yayımlanan veri kaynakları** sekmesi:

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

Tıklatırsanız **Düzenle**, size bir bakışta mümkün toosee size sunulan içinde hangi konumları olacaktır:

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

Bu noktada, hello portal göstermez oluşturduğumuz hello yerleştirecek sınırları hello – tüm ihtiyacımız olan belirtilen hello hello doğru yakın çevrede konumdur bir onay.

Şimdi hello veri kaynağı için tüm hello gereksinimleri vardır. Merhaba istek URL'si, hello Bing Haritalar Geliştirme Merkezi hello API çağrısı için tooget hello ayrıntıları tıklatın **veri kaynakları** seçip **veri kaynağı bilgileri**.

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

Merhaba **sorgu URL** burada aradığımız şey değil. Bu hello cihaz şu anda bir konum hello sınırlar içinde olsun veya olmasın göre biz sorguları toocheck yürütebilir hello uç noktadır. Bu iletişim kutusunda, yalnızca bir GET çağrısı hello sorgu URL'ye karşı şu parametreler eklenmiş hello ile tooexecute ihtiyacımız tooperform:

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

Böylece biz hello aygıttan almak ve hello bölge sınırı içinde olup olmadığını Bing Haritalar hello hesaplamaları toosee otomatik olarak gerçekleştirecek bir hedef noktaya belirlediniz. Bir tarayıcı (veya cURL) aracılığıyla hello isteği yürüttükten sonra standart bir JSON yanıtı alırsınız:

![](./media/notification-hubs-geofence/bing-maps-json.png)

Bu yanıt yalnızca başlangıç noktası gerçekten sınırları belirlenmiş hello içinde olduğunda gerçekleşir. Değilse boş bir **sonuçlar** demeti alırsınız:

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a>Merhaba UWP uygulamasını ayarlama
Biz hello veri kaynağı hazır sahip olduğunuza göre biz daha önce önyüklemesini yaptığımız UWP uygulaması hello üzerinde çalışmaya başlayabiliriz.

Öncelikle, uygulamamız için konum hizmetlerini etkinleştirmemiz gerekir. toodo Bu, çift tıklatıldığında `Package.appxmanifest` dosyasını **Çözüm Gezgini**.

![](./media/notification-hubs-geofence/vs-package-manifest.png)

Açılan hello paket özellikleri sekmesinde tıklayın **yetenekleri** ve seçtiğinizden emin olun **konumu**:

![](./media/notification-hubs-geofence/vs-package-location.png)

Merhaba konum özelliği bildirildiğine göre çözümünüz adlı yeni bir klasör oluşturun `Core`ve içerdiği, adlı yeni bir dosya ekleyin `LocationHelper.cs`:

![](./media/notification-hubs-geofence/vs-location-helper.png)

Merhaba `LocationHelper` sınıfının kendisi oldukça temel bu noktada – tüm izin bize hello sistem API'si aracılığıyla tooobtain hello kullanıcı konumu:

    using System;
    using System.Threading.Tasks;
    using Windows.Devices.Geolocation;

    namespace NotificationHubs.Geofence.Core
    {
        public class LocationHelper
        {
            private static readonly uint AppDesiredAccuracyInMeters = 10;

            public async static Task<Geoposition> GetCurrentLocation()
            {
                var accessStatus = await Geolocator.RequestAccessAsync();
                switch (accessStatus)
                {
                    case GeolocationAccessStatus.Allowed:
                        {
                            Geolocator geolocator = new Geolocator { DesiredAccuracyInMeters = AppDesiredAccuracyInMeters };

                            return await geolocator.GetGeopositionAsync();
                        }
                    default:
                        {
                            return null;
                        }
                }
            }

        }
    }

Merhaba resmi UWP uygulamalarında kullanıcının konumunu alma hakkında daha fazla hello okuyabilirsiniz [MSDN belgesi](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).

Merhaba konum almanın çalışıp, toocheck ana sayfanızın kod tarafını hello açın (`MainPage.xaml.cs`). Hello için yeni bir olay işleyicisi oluşturun `Loaded` hello olayda `MainPage` Oluşturucusu:

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

Merhaba olay işleyicisi Hello uygulaması aşağıdaki gibidir:

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

Biz hello işleyiciyi zaman uyumsuz olarak dikkat `GetCurrentLocation` bildirdiğimize ve bu nedenle bir zaman uyumsuz bağlamında yürütülen toobe gerektirir. Ayrıca, belirli koşullar altında biz null bir konumla bitirebilirsiniz olduğundan (örneğin hello konum hizmetleri devre dışı bırakılır veya hello uygulama izinleri tooaccess konumu reddedildi), null denetimi ile düzgün şekilde işlenir emin toomake ihtiyacımız.

Merhaba uygulamayı çalıştırın. Konum erişimine izin verdiğinizden emin olun:

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

Uygulama başlatır'bir kez hello, mümkün toosee hello hello koordinatlarında olmalıdır **çıkış** penceresi:

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

Şimdi konum almanın çalıştığını düşünüyorsanız, ücretsiz tooremove hello test olay işleyicisini için yüklenen biz artık kullanıyor olmaz çünkü bildirin.

Merhaba sonraki toocapture konum değişikliklerinin adımdır. Bunun için geri toohello edelim `LocationHelper` sınıfı ve hello olay işleyicisi ekleme `PositionChanged`:

    geolocator.PositionChanged += Geolocator_PositionChanged;

Merhaba uygulama hello konum koordinatlarını hello gösterir **çıkış** penceresi:

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a>Merhaba arka ucu ayarlama
Merhaba karşıdan [github'dan .NET arka ucu örneği](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). Merhaba indirme işlemi tamamlandıktan sonra hello açmak `NotifyUsers` klasörünü ve ardından hello `NotifyUsers.sln` dosya.

Set hello `AppBackend` projesi hello olarak **başlangıç projesi** ve başlatın.

![](./media/notification-hubs-geofence/vs-startup-project.png)

Merhaba proje zaten yapılandırılmış toosend anında iletme bildirimleri tootarget aygıtları, toodo yalnızca iki şey – ihtiyacımız şekilde hello sağ bağlantı dizesi hello bildirim hub'ı takas ve sınır kimliği toosend hello yalnızca hello değiştiğinde bildirimi ekleme Kullanıcı hello bölge sınırı içinde değil.

tooconfigure hello bağlantı dizesinde, hello `Models` Klasör Aç `Notifications.cs`. Merhaba `NotificationHubClient.CreateClientFromConnectionString` işlevi hello alabileceğiniz bildirim hub'ınız hakkında hello bilgi içermelidir [Azure Portal](https://portal.azure.com) (Merhaba içinde Ara **erişim ilkeleri** dikey penceresinde  **Ayarları**). Merhaba güncelleştirilmiş yapılandırma dosyasını kaydedin.

Şimdi toocreate bir model hello Bing Haritalar API'si sonucu için ihtiyacımız var. Merhaba sağ tıklatın, en kolay yolu toodo hello `Models` klasörünü **Ekle** > **sınıfı**. Bunu, `GeofenceBoundary.cs` olarak adlandırın. Bunu yaptıktan sonra hello ilk bölümünde ve Visual Studio kullanımda konuştuğumuz hello API yanıt hello JSON kopyalama **Düzenle** > **Özel Yapıştır** > **JSON Yapıştır Sınıflar olarak**. 

Tam olarak istendiği gibi Biz bu hello nesne emin oluruz serisi kaldırılacak. Elde edilen sınıf kümeniz şuna benzemelidir:

    namespace AppBackend.Models
    {
        public class Rootobject
        {
            public D d { get; set; }
        }

        public class D
        {
            public string __copyright { get; set; }
            public Result[] results { get; set; }
        }

        public class Result
        {
            public __Metadata __metadata { get; set; }
            public string EntityID { get; set; }
            public string Name { get; set; }
            public float Longitude { get; set; }
            public float Latitude { get; set; }
            public string Boundary { get; set; }
            public string Confidence { get; set; }
            public string Locality { get; set; }
            public string AddressLine { get; set; }
            public string AdminDistrict { get; set; }
            public string CountryRegion { get; set; }
            public string PostalCode { get; set; }
        }

        public class __Metadata
        {
            public string uri { get; set; }
        }
    }

Ardından `Controllers` > `NotificationsController.cs` öğesini açın. Tootweak hello Post çağrısı tooaccount hello hedef enlemini ve boylamını gerekir. Bunun için iki dizeleri toohello işlev imzası – eklemeniz yeterlidir `latitude` ve `longitude`.

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

Adlı hello projesi içinde yeni bir sınıf oluşturun `ApiHelper.cs` – tooconnect tooBing toocheck nokta sınır kesişimlerini kullanacağız. Aşağıdaki şekilde bir `IsPointWithinBounds` işlevini uygulayın:

    public class ApiHelper
    {
        public static readonly string ApiEndpoint = "{YOUR_QUERY_ENDPOINT}?spatialFilter=intersects(%27POINT%20({0}%20{1})%27)&$format=json&key={2}";
        public static readonly string ApiKey = "{YOUR_API_KEY}";

        public static bool IsPointWithinBounds(string longitude,string latitude)
        {
            var json = new WebClient().DownloadString(string.Format(ApiEndpoint, longitude, latitude, ApiKey));
            var result = JsonConvert.DeserializeObject<Rootobject>(json);
            if (result.d.results != null && result.d.results.Count() > 0)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    }

> [!NOTE]
> Daha önce Bing Geliştirme Merkezi (aynı toohello API anahtarı geçerlidir) hello aldığınız hello sorgu URL'si ile emin toosubstitute hello API uç noktası olun. 
> 
> 

Sonuçları toohello sorgusu varsa, döndürürüz belirtilen noktası hello anlamına hello yerleştirecek hello sınırları içinde olduğundan `true`. Hiç sonuç yoksa Bing bize döndürürüz hello noktası hello arama çerçevesi dışında olduğunu belirtiyor `false`.

Geri `NotificationsController.cs`, hello switch deyimi hemen önce bir denetim oluşturun:

    if (ApiHelper.IsPointWithinBounds(longitude, latitude))
    {
        switch (pns.ToLower())
        {
            case "wns":
                //// Windows 8.1 / Windows Phone 8.1
                var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                // Windows 10 specific Action Center support
                toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                break;
        }
    }

Bu şekilde hello bildirim yalnızca başlangıç noktası hello sınırlar içinde olduğunda gönderilir.

## <a name="testing-push-notifications-in-hello-uwp-app"></a>Merhaba UWP uygulamasında anında iletme bildirimlerini test etme
Toohello UWP uygulamasında geri dönerseniz, biz artık mümkün tootest bildirimleri olması gerekir. Merhaba içinde `LocationHelper` sınıfı, yeni bir işlev oluşturun `SendLocationToBackend`:

    public static async Task SendLocationToBackend(string pns, string userTag, string message, string latitude, string longitude)
    {
        var POST_URL = "http://localhost:8741/api/notifications?pns=" +
            pns + "&to_tag=" + userTag + "&latitude=" + latitude + "&longitude=" + longitude;

        using (var httpClient = new HttpClient())
        {
            try
            {
                await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                    System.Text.Encoding.UTF8, "application/json"));
            }
            catch (Exception ex)
            {
                Debug.WriteLine(ex.Message);
            }
        }
    }

> [!NOTE]
> Merhaba takas `POST_URL` hello önceki bölümde oluşturduğumuz dağıtılmış web uygulamanızın toohello konumu. İsteğe bağlı olarak şu an için Tamam toorun olan yerel olarak, ancak genel bir sürümü dağıtma üzerinde çalışırken, toohost gerekir dış sağlayıcı ile.
> 
> 

Şimdi biz hello UWP uygulamasında anında iletme bildirimleri için kayıt emin olalım. Visual Studio'da tıklayın **proje** > **depolamak** > **uygulama hello deposuyla ilişkilendirmek**.

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

Tooyour Geliştirici hesabında oturum sonra var olan bir uygulama seçin veya yeni bir tane oluşturun ve hello paketi Bununla ilişkilendirin emin olun. 

Toohello Geliştirici Merkezi ve yeni oluşturduğunuz açık hello uygulama gidin. **Hizmetler** > **Anında İletme Bildirimleri** > **Live Services sitesine** tıklayın.

![](./media/notification-hubs-geofence/ms-live-services.png)

Merhaba sitesinde hello not edin **uygulama gizli anahtarı** ve hello **paket SID'si**. İhtiyacınız olacak hem hello Azure Portal-bildirim hub'ınızı açın, üzerinde **ayarları** > **Bildirim Hizmetleri** > **Windows (WNS)**ve gerekli hello alanlara hello bilgileri girin.

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

**Kaydet**'e tıklayın.

**Çözüm Gezgini**'nde **Başvurular**'a sağ tıklayın ve **NuGet Paketlerini Yönet**'i seçin. Tooadd başvuru toohello ihtiyacımız **Microsoft Azure Service Bus yönetilen kitaplık** – yalnızca arama `WindowsAzure.Messaging.Managed` ve tooyour proje ekleyin.

![](./media/notification-hubs-geofence/vs-nuget.png)

Test amacıyla, hello oluşturabilir `MainPage_Loaded` olay işleyicisini yeniden, bu kod parçacığını tooit ekleyin:

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

Yukarıdaki Hello hello bildirim hub'hello uygulama kaydeder. Hazır toogo olduğunuz! 

İçinde `LocationHelper`, hello içinde `Geolocator_PositionChanged` işleyicisi hello konumu hello bölge sınırının içine zorla sokar test kodu parçası ekleyebilirsiniz:

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

(Hangi hello sınırlar içinde hello şu anda olmayabilir) hello gerçek koordinatları geçirmediğimiz olmayan ve önceden tanımlanmış test değerleri için biz güncelleştirme üzerinde bir bildirim görürsünüz:

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a>Sırada ne var?
Birkaç ek toohello toomake hello çözümün üretime hazır olduğundan emin yukarıda toofollow gerekebilecek adım vardır.

Öncelikle, bölge sınırlarının dinamik olduğundan tooensure gerekebilir. Bu sipariş toobe mümkün tooupload yeni sınırları içinde hello varolan bir veri kaynağını hello Bing API'si ile bazı ek çalışmalar gerektirir. Merhaba başvurun [Bing uzamsal Veri Hizmetleri API belgelerine](https://msdn.microsoft.com/library/ff701734.aspx) hello konu hakkında daha fazla ayrıntı için.

İkinci olarak, çalışma tooensure hello teslim toohello doğru katılımcılara yapıldığından olarak tootarget isteyebilirsiniz aracılığıyla bunları [etiketleme](notification-hubs-tags-segment-push-message.md).

Yukarıda gösterilen hello çözümü hesabınıza hello bölge sınırlaması toosystem özgü özellikleri sınır değil için çok çeşitli hedef platformlara sahip neden olabileceğiniz bir senaryo açıklanmaktadır. Bununla hello Evrensel Windows platformu sunar yetenekleri çok[bölge sınırlarının sağ out-of--box algılamak](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).

Notification Hubs özellikleri hakkında daha ayrıntılı bilgi için [belge portalımıza](https://azure.microsoft.com/documentation/services/notification-hubs/) göz atın.

