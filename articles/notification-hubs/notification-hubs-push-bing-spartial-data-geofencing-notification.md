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
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="1f860-104">Azure Notification Hubs ve Bing Uzamsal Veri ile bölge sınırlamalı anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="1f860-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="1f860-105">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f860-105">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="1f860-106">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f860-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1f860-107">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span><span class="sxs-lookup"><span data-stu-id="1f860-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="1f860-108">Bu öğreticide, nasıl toodeliver konum temelli anında iletme bildirimleri ile Azure Notification Hubs ve Bing uzamsal gelen bir evrensel Windows Platform uygulaması içinde kullanılan veri öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="1f860-108">In this tutorial, you will learn how toodeliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f860-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1f860-109">Prerequisites</span></span>
<span data-ttu-id="1f860-110">Öncelikle, tüm hello yazılım ve hizmet önkoşullarına sahip olduğunuzdan emin toomake gerekir:</span><span class="sxs-lookup"><span data-stu-id="1f860-110">First and foremost, you need toomake sure that you have all hello software and service pre-requisites:</span></span>

* <span data-ttu-id="1f860-111">[Visual Studio 2015 Güncelleştirmesi 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) veya üzeri ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) da geçerli olur).</span><span class="sxs-lookup"><span data-stu-id="1f860-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="1f860-112">En son sürümünü hello [Azure SDK'sı](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1f860-112">Latest version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="1f860-113">[Bing Haritalar Geliştirme Merkezi hesabı](https://www.bingmapsportal.com/) (ücretsiz bir tane oluşturabilir ve Microsoft hesabınızla ilişkilendirebilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="1f860-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="1f860-114">Başlarken</span><span class="sxs-lookup"><span data-stu-id="1f860-114">Getting Started</span></span>
<span data-ttu-id="1f860-115">Başlangıç projesi oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="1f860-115">Let’s start by creating hello project.</span></span> <span data-ttu-id="1f860-116">Visual Studio'da **Boş Uygulama (Evrensel Windows)** türü yeni bir proje başlatın.</span><span class="sxs-lookup"><span data-stu-id="1f860-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="1f860-117">Merhaba proje oluşturmayı tamamladıktan sonra hello uygulama kendisi için hello donanımınız olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f860-117">Once hello project creation is complete, you should have hello harness for hello app itself.</span></span> <span data-ttu-id="1f860-118">Şimdi hello bölge sınırlama altyapısı için her şeyi ayarlayalım.</span><span class="sxs-lookup"><span data-stu-id="1f860-118">Now let’s set up everything for hello geo-fencing infrastructure.</span></span> <span data-ttu-id="1f860-119">Biz bu için Bing Hizmetleri giderek toouse olduğundan, bize tooquery belirli konum çerçevelerini sağlayan ortak bir REST API uç noktası vardır:</span><span class="sxs-lookup"><span data-stu-id="1f860-119">Because we are going toouse Bing services for this, there is a public REST API endpoint that allows us tooquery specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="1f860-120">Toospecify gerekir hello parametreleri tooget onu çalışma:</span><span class="sxs-lookup"><span data-stu-id="1f860-120">You will need toospecify hello following parameters tooget it working:</span></span>

* <span data-ttu-id="1f860-121">**Veri Kaynağı Kimliği** ve **Veri Kaynağı Adı**: Veri kaynakları, Bing Haritalar API'sinde konumlar ve çalışma saatleri gibi kümelenmiş çeşitli meta veriler içerir.</span><span class="sxs-lookup"><span data-stu-id="1f860-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="1f860-122">Burada, bunlar hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f860-122">You can read more about those here.</span></span> 
* <span data-ttu-id="1f860-123">**Varlık adı** – hello istediğiniz toouse bir başvuru noktası olarak hello bildirimi varlığı.</span><span class="sxs-lookup"><span data-stu-id="1f860-123">**Entity Name** – hello entity you want toouse as a reference point for hello notification.</span></span> 
* <span data-ttu-id="1f860-124">**Bing Haritalar API'si anahtarı** – bu hello Bing Geliştirme Merkezi hesabı oluşturduğunuzda, daha önce aldığınız hello anahtardır.</span><span class="sxs-lookup"><span data-stu-id="1f860-124">**Bing Maps API Key** – this is hello key that you obtained earlier when you created hello Bing Dev Center account.</span></span>

<span data-ttu-id="1f860-125">Şimdi derin Dalış hello kurulumunu her yukarıdaki hello öğeler için yapın.</span><span class="sxs-lookup"><span data-stu-id="1f860-125">Let’s do a deep-dive on hello setup for each of hello elements above.</span></span>

## <a name="setting-up-hello-data-source"></a><span data-ttu-id="1f860-126">Merhaba veri kaynağını ayarlama</span><span class="sxs-lookup"><span data-stu-id="1f860-126">Setting up hello data source</span></span>
<span data-ttu-id="1f860-127">Merhaba Bing Haritalar geliştirme Merkezi'nde yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f860-127">You can do it in hello Bing Maps Dev Center.</span></span> <span data-ttu-id="1f860-128">Yalnızca tıklayın **veri kaynakları** hello üst gezinti çubuğu ve select içinde **veri kaynaklarını yönet**.</span><span class="sxs-lookup"><span data-stu-id="1f860-128">Simply click on **Data sources** in hello top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="1f860-129">Önce Bing Haritalar API'si ile çalışmadıysanız büyük olasılıkla olmayacaktır herhangi bir veri kaynağı mevcut, böylece yalnızca karşıya yükleme veri tooa veri kaynağında'ı tıklatarak yeni bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f860-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data tooa data source.</span></span> <span data-ttu-id="1f860-130">Tüm hello gerekli alanları doldurduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="1f860-130">Make sure you fill out all hello required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="1f860-131">Merak ediyor olabilirsiniz hello veri dosyası nedir ve neleri karşıya yüklemeniz?</span><span class="sxs-lookup"><span data-stu-id="1f860-131">You might be wondering – what is hello data file and what should you be uploading?</span></span> <span data-ttu-id="1f860-132">Bu test Hello amaçları doğrultusunda, biz yalnızca, bir alanı hello San Francisco rıhtımının çerçeve hello kanal tabanlı örneği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1f860-132">For hello purposes of this test, we can just use hello sample pipe-based that frames an area of hello San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="1f860-133">Yukarıdaki Hello bu varlığı temsil eder:</span><span class="sxs-lookup"><span data-stu-id="1f860-133">hello above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="1f860-134">Yalnızca kopyalayın ve yukarıdaki hello dizeyi yeni bir dosyaya yapıştırın ve olarak kaydedin **NotificationHubsGeofence.pipe**ve hello Bing geliştirme Merkezi'ne yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1f860-134">Simply copy and paste hello string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in hello Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="1f860-135">İstendiğinde toospecify hello için yeni bir anahtar olabilir **ana anahtar** hello farklı **sorgu anahtarını**.</span><span class="sxs-lookup"><span data-stu-id="1f860-135">You might be prompted toospecify a new key for hello **Master Key** that is different from hello **Query Key**.</span></span> <span data-ttu-id="1f860-136">Yalnızca hello Pano ve yenileme hello veri kaynağını karşıya yükleme sayfasını aracılığıyla yeni bir anahtar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1f860-136">Simply create a new key through hello dashboard and refresh hello data source upload page.</span></span>
> 
> 

<span data-ttu-id="1f860-137">Merhaba veri dosyasını karşıya yükledikten sonra toomake hello veri kaynağını yayımladığınızdan emin gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f860-137">Once you upload hello data file, you will need toomake sure that you publish hello data source.</span></span> 

<span data-ttu-id="1f860-138">Çok Git**veri kaynaklarını yönet**, tıpkı yaptığımız, hello listede veri kaynağınızı bulun ve tıklayın **Yayımla** hello içinde **Eylemler** sütun.</span><span class="sxs-lookup"><span data-stu-id="1f860-138">Go too**Manage Data Sources**, just like we did above, find your data source in hello list and click on **Publish** in hello **Actions** column.</span></span> <span data-ttu-id="1f860-139">İçinde bir bit hello veri kaynağınızı görmeniz gerekir **yayımlanan veri kaynakları** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="1f860-139">In a bit, you should see your data source in hello **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="1f860-140">Tıklatırsanız **Düzenle**, size bir bakışta mümkün toosee size sunulan içinde hangi konumları olacaktır:</span><span class="sxs-lookup"><span data-stu-id="1f860-140">If you click **Edit**, you will be able toosee at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="1f860-141">Bu noktada, hello portal göstermez oluşturduğumuz hello yerleştirecek sınırları hello – tüm ihtiyacımız olan belirtilen hello hello doğru yakın çevrede konumdur bir onay.</span><span class="sxs-lookup"><span data-stu-id="1f860-141">At this point, hello portal does not show you hello boundaries for hello geofence that we created – all we need is a confirmation that hello location specified is in hello right vicinity.</span></span>

<span data-ttu-id="1f860-142">Şimdi hello veri kaynağı için tüm hello gereksinimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="1f860-142">Now you have all hello requirements for hello data source.</span></span> <span data-ttu-id="1f860-143">Merhaba istek URL'si, hello Bing Haritalar Geliştirme Merkezi hello API çağrısı için tooget hello ayrıntıları tıklatın **veri kaynakları** seçip **veri kaynağı bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="1f860-143">tooget hello details on hello request URL for hello API call, in hello Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="1f860-144">Merhaba **sorgu URL** burada aradığımız şey değil.</span><span class="sxs-lookup"><span data-stu-id="1f860-144">hello **Query URL** is what we’re after here.</span></span> <span data-ttu-id="1f860-145">Bu hello cihaz şu anda bir konum hello sınırlar içinde olsun veya olmasın göre biz sorguları toocheck yürütebilir hello uç noktadır.</span><span class="sxs-lookup"><span data-stu-id="1f860-145">This is hello endpoint against which we can execute queries toocheck whether hello device is currently within hello boundaries of a location or not.</span></span> <span data-ttu-id="1f860-146">Bu iletişim kutusunda, yalnızca bir GET çağrısı hello sorgu URL'ye karşı şu parametreler eklenmiş hello ile tooexecute ihtiyacımız tooperform:</span><span class="sxs-lookup"><span data-stu-id="1f860-146">tooperform this check, we simply need tooexecute a GET call against hello query URL, with hello following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="1f860-147">Böylece biz hello aygıttan almak ve hello bölge sınırı içinde olup olmadığını Bing Haritalar hello hesaplamaları toosee otomatik olarak gerçekleştirecek bir hedef noktaya belirlediniz.</span><span class="sxs-lookup"><span data-stu-id="1f860-147">That way you're specifying a target point that we obtain from hello device and Bing Maps will automatically perform hello calculations toosee whether it is within hello geofence.</span></span> <span data-ttu-id="1f860-148">Bir tarayıcı (veya cURL) aracılığıyla hello isteği yürüttükten sonra standart bir JSON yanıtı alırsınız:</span><span class="sxs-lookup"><span data-stu-id="1f860-148">Once you execute hello request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="1f860-149">Bu yanıt yalnızca başlangıç noktası gerçekten sınırları belirlenmiş hello içinde olduğunda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="1f860-149">This response only happens when hello point is actually within hello designated boundaries.</span></span> <span data-ttu-id="1f860-150">Değilse boş bir **sonuçlar** demeti alırsınız:</span><span class="sxs-lookup"><span data-stu-id="1f860-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a><span data-ttu-id="1f860-151">Merhaba UWP uygulamasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="1f860-151">Setting up hello UWP application</span></span>
<span data-ttu-id="1f860-152">Biz hello veri kaynağı hazır sahip olduğunuza göre biz daha önce önyüklemesini yaptığımız UWP uygulaması hello üzerinde çalışmaya başlayabiliriz.</span><span class="sxs-lookup"><span data-stu-id="1f860-152">Now that we have hello data source ready, we can start working on hello UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="1f860-153">Öncelikle, uygulamamız için konum hizmetlerini etkinleştirmemiz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f860-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="1f860-154">toodo Bu, çift tıklatıldığında `Package.appxmanifest` dosyasını **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="1f860-154">toodo this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="1f860-155">Açılan hello paket özellikleri sekmesinde tıklayın **yetenekleri** ve seçtiğinizden emin olun **konumu**:</span><span class="sxs-lookup"><span data-stu-id="1f860-155">In hello package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="1f860-156">Merhaba konum özelliği bildirildiğine göre çözümünüz adlı yeni bir klasör oluşturun `Core`ve içerdiği, adlı yeni bir dosya ekleyin `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="1f860-156">As hello location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="1f860-157">Merhaba `LocationHelper` sınıfının kendisi oldukça temel bu noktada – tüm izin bize hello sistem API'si aracılığıyla tooobtain hello kullanıcı konumu:</span><span class="sxs-lookup"><span data-stu-id="1f860-157">hello `LocationHelper` class itself is fairly basic at this point – all it does is allow us tooobtain hello user location through hello system API:</span></span>

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

<span data-ttu-id="1f860-158">Merhaba resmi UWP uygulamalarında kullanıcının konumunu alma hakkında daha fazla hello okuyabilirsiniz [MSDN belgesi](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f860-158">You can read more about getting hello user’s location in UWP apps in hello official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="1f860-159">Merhaba konum almanın çalışıp, toocheck ana sayfanızın kod tarafını hello açın (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="1f860-159">toocheck that hello location acquisition is actually working, open hello code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="1f860-160">Hello için yeni bir olay işleyicisi oluşturun `Loaded` hello olayda `MainPage` Oluşturucusu:</span><span class="sxs-lookup"><span data-stu-id="1f860-160">Create a new event handler for hello `Loaded` event in hello `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="1f860-161">Merhaba olay işleyicisi Hello uygulaması aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="1f860-161">hello implementation of hello event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="1f860-162">Biz hello işleyiciyi zaman uyumsuz olarak dikkat `GetCurrentLocation` bildirdiğimize ve bu nedenle bir zaman uyumsuz bağlamında yürütülen toobe gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1f860-162">Notice that we declared hello handler as async because `GetCurrentLocation` is awaitable, and therefore requires toobe executed in an async context.</span></span> <span data-ttu-id="1f860-163">Ayrıca, belirli koşullar altında biz null bir konumla bitirebilirsiniz olduğundan (örneğin hello konum hizmetleri devre dışı bırakılır veya hello uygulama izinleri tooaccess konumu reddedildi), null denetimi ile düzgün şekilde işlenir emin toomake ihtiyacımız.</span><span class="sxs-lookup"><span data-stu-id="1f860-163">Also, because under certain circumstances we might end up with a null location (e.g. hello location services are disabled or hello application was denied permissions tooaccess location), we need toomake sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="1f860-164">Merhaba uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1f860-164">Run hello application.</span></span> <span data-ttu-id="1f860-165">Konum erişimine izin verdiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="1f860-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="1f860-166">Uygulama başlatır'bir kez hello, mümkün toosee hello hello koordinatlarında olmalıdır **çıkış** penceresi:</span><span class="sxs-lookup"><span data-stu-id="1f860-166">Once hello application launches, you should be able toosee hello coordinates in hello **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="1f860-167">Şimdi konum almanın çalıştığını düşünüyorsanız, ücretsiz tooremove hello test olay işleyicisini için yüklenen biz artık kullanıyor olmaz çünkü bildirin.</span><span class="sxs-lookup"><span data-stu-id="1f860-167">Now you know that location acquisition works – feel free tooremove hello test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="1f860-168">Merhaba sonraki toocapture konum değişikliklerinin adımdır.</span><span class="sxs-lookup"><span data-stu-id="1f860-168">hello next step is toocapture location changes.</span></span> <span data-ttu-id="1f860-169">Bunun için geri toohello edelim `LocationHelper` sınıfı ve hello olay işleyicisi ekleme `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="1f860-169">For that, let’s go back toohello `LocationHelper` class and add hello event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="1f860-170">Merhaba uygulama hello konum koordinatlarını hello gösterir **çıkış** penceresi:</span><span class="sxs-lookup"><span data-stu-id="1f860-170">hello implementation will show hello location coordinates in hello **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a><span data-ttu-id="1f860-171">Merhaba arka ucu ayarlama</span><span class="sxs-lookup"><span data-stu-id="1f860-171">Setting up hello backend</span></span>
<span data-ttu-id="1f860-172">Merhaba karşıdan [github'dan .NET arka ucu örneği](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="1f860-172">Download hello [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="1f860-173">Merhaba indirme işlemi tamamlandıktan sonra hello açmak `NotifyUsers` klasörünü ve ardından hello `NotifyUsers.sln` dosya.</span><span class="sxs-lookup"><span data-stu-id="1f860-173">Once hello download completes, open hello `NotifyUsers` folder, and subsequently – hello `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="1f860-174">Set hello `AppBackend` projesi hello olarak **başlangıç projesi** ve başlatın.</span><span class="sxs-lookup"><span data-stu-id="1f860-174">Set hello `AppBackend` project as hello **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="1f860-175">Merhaba proje zaten yapılandırılmış toosend anında iletme bildirimleri tootarget aygıtları, toodo yalnızca iki şey – ihtiyacımız şekilde hello sağ bağlantı dizesi hello bildirim hub'ı takas ve sınır kimliği toosend hello yalnızca hello değiştiğinde bildirimi ekleme Kullanıcı hello bölge sınırı içinde değil.</span><span class="sxs-lookup"><span data-stu-id="1f860-175">hello project is already configured toosend push notifications tootarget devices, so we’ll need toodo only two things – swap out hello right connection string for hello notification hub and add boundary identification toosend hello notification only when hello user is within hello geofence.</span></span>

<span data-ttu-id="1f860-176">tooconfigure hello bağlantı dizesinde, hello `Models` Klasör Aç `Notifications.cs`.</span><span class="sxs-lookup"><span data-stu-id="1f860-176">tooconfigure hello connection string, in hello `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="1f860-177">Merhaba `NotificationHubClient.CreateClientFromConnectionString` işlevi hello alabileceğiniz bildirim hub'ınız hakkında hello bilgi içermelidir [Azure Portal](https://portal.azure.com) (Merhaba içinde Ara **erişim ilkeleri** dikey penceresinde  **Ayarları**).</span><span class="sxs-lookup"><span data-stu-id="1f860-177">hello `NotificationHubClient.CreateClientFromConnectionString` function should contain hello information about your notification hub that you can get in hello [Azure Portal](https://portal.azure.com) (look inside hello **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="1f860-178">Merhaba güncelleştirilmiş yapılandırma dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1f860-178">Save hello updated configuration file.</span></span>

<span data-ttu-id="1f860-179">Şimdi toocreate bir model hello Bing Haritalar API'si sonucu için ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="1f860-179">Now we need toocreate a model for hello Bing Maps API result.</span></span> <span data-ttu-id="1f860-180">Merhaba sağ tıklatın, en kolay yolu toodo hello `Models` klasörünü **Ekle** > **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="1f860-180">hello easiest way toodo that is right-click on hello `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="1f860-181">Bunu, `GeofenceBoundary.cs` olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="1f860-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="1f860-182">Bunu yaptıktan sonra hello ilk bölümünde ve Visual Studio kullanımda konuştuğumuz hello API yanıt hello JSON kopyalama **Düzenle** > **Özel Yapıştır** > **JSON Yapıştır Sınıflar olarak**.</span><span class="sxs-lookup"><span data-stu-id="1f860-182">Once done, copy hello JSON from hello API response that we discussed in hello first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="1f860-183">Tam olarak istendiği gibi Biz bu hello nesne emin oluruz serisi kaldırılacak.</span><span class="sxs-lookup"><span data-stu-id="1f860-183">That way we ensure that hello object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="1f860-184">Elde edilen sınıf kümeniz şuna benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="1f860-184">Your resulting class set should resemble this:</span></span>

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

<span data-ttu-id="1f860-185">Ardından `Controllers` > `NotificationsController.cs` öğesini açın.</span><span class="sxs-lookup"><span data-stu-id="1f860-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="1f860-186">Tootweak hello Post çağrısı tooaccount hello hedef enlemini ve boylamını gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f860-186">We need tootweak hello Post call tooaccount for hello target longitude and latitude.</span></span> <span data-ttu-id="1f860-187">Bunun için iki dizeleri toohello işlev imzası – eklemeniz yeterlidir `latitude` ve `longitude`.</span><span class="sxs-lookup"><span data-stu-id="1f860-187">For that, simply add two strings toohello function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="1f860-188">Adlı hello projesi içinde yeni bir sınıf oluşturun `ApiHelper.cs` – tooconnect tooBing toocheck nokta sınır kesişimlerini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="1f860-188">Create a new class within hello project called `ApiHelper.cs` – we’ll use it tooconnect tooBing toocheck point boundary intersections.</span></span> <span data-ttu-id="1f860-189">Aşağıdaki şekilde bir `IsPointWithinBounds` işlevini uygulayın:</span><span class="sxs-lookup"><span data-stu-id="1f860-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

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
> <span data-ttu-id="1f860-190">Daha önce Bing Geliştirme Merkezi (aynı toohello API anahtarı geçerlidir) hello aldığınız hello sorgu URL'si ile emin toosubstitute hello API uç noktası olun.</span><span class="sxs-lookup"><span data-stu-id="1f860-190">Make sure toosubstitute hello API endpoint with hello query URL that you obtained earlier from hello Bing Dev Center (same applies toohello API key).</span></span> 
> 
> 

<span data-ttu-id="1f860-191">Sonuçları toohello sorgusu varsa, döndürürüz belirtilen noktası hello anlamına hello yerleştirecek hello sınırları içinde olduğundan `true`.</span><span class="sxs-lookup"><span data-stu-id="1f860-191">If there are results toohello query, that means that hello specified point is within hello boundaries of hello geofence, so we return `true`.</span></span> <span data-ttu-id="1f860-192">Hiç sonuç yoksa Bing bize döndürürüz hello noktası hello arama çerçevesi dışında olduğunu belirtiyor `false`.</span><span class="sxs-lookup"><span data-stu-id="1f860-192">If there are no results, Bing is telling us that hello point is outside hello lookup frame, so we return `false`.</span></span>

<span data-ttu-id="1f860-193">Geri `NotificationsController.cs`, hello switch deyimi hemen önce bir denetim oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1f860-193">Back in `NotificationsController.cs`, create a check right before hello switch statement:</span></span>

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

<span data-ttu-id="1f860-194">Bu şekilde hello bildirim yalnızca başlangıç noktası hello sınırlar içinde olduğunda gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1f860-194">That way, hello notification is only sent when hello point is within hello boundaries.</span></span>

## <a name="testing-push-notifications-in-hello-uwp-app"></a><span data-ttu-id="1f860-195">Merhaba UWP uygulamasında anında iletme bildirimlerini test etme</span><span class="sxs-lookup"><span data-stu-id="1f860-195">Testing push notifications in hello UWP app</span></span>
<span data-ttu-id="1f860-196">Toohello UWP uygulamasında geri dönerseniz, biz artık mümkün tootest bildirimleri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f860-196">Going back toohello UWP app, we should now be able tootest notifications.</span></span> <span data-ttu-id="1f860-197">Merhaba içinde `LocationHelper` sınıfı, yeni bir işlev oluşturun `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="1f860-197">Within hello `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

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
> <span data-ttu-id="1f860-198">Merhaba takas `POST_URL` hello önceki bölümde oluşturduğumuz dağıtılmış web uygulamanızın toohello konumu.</span><span class="sxs-lookup"><span data-stu-id="1f860-198">Swap hello `POST_URL` toohello location of your deployed web application that we created in hello previous section.</span></span> <span data-ttu-id="1f860-199">İsteğe bağlı olarak şu an için Tamam toorun olan yerel olarak, ancak genel bir sürümü dağıtma üzerinde çalışırken, toohost gerekir dış sağlayıcı ile.</span><span class="sxs-lookup"><span data-stu-id="1f860-199">For now, it’s OK toorun it locally, but as you work on deploying a public version, you will need toohost it with an external provider.</span></span>
> 
> 

<span data-ttu-id="1f860-200">Şimdi biz hello UWP uygulamasında anında iletme bildirimleri için kayıt emin olalım.</span><span class="sxs-lookup"><span data-stu-id="1f860-200">Let’s now make sure that we register hello UWP app for push notifications.</span></span> <span data-ttu-id="1f860-201">Visual Studio'da tıklayın **proje** > **depolamak** > **uygulama hello deposuyla ilişkilendirmek**.</span><span class="sxs-lookup"><span data-stu-id="1f860-201">In Visual Studio, click on **Project** > **Store** > **Associate app with hello store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="1f860-202">Tooyour Geliştirici hesabında oturum sonra var olan bir uygulama seçin veya yeni bir tane oluşturun ve hello paketi Bununla ilişkilendirin emin olun.</span><span class="sxs-lookup"><span data-stu-id="1f860-202">Once you sign in tooyour developer account, make sure you select an existing app or create a new one and associate hello package with it.</span></span> 

<span data-ttu-id="1f860-203">Toohello Geliştirici Merkezi ve yeni oluşturduğunuz açık hello uygulama gidin.</span><span class="sxs-lookup"><span data-stu-id="1f860-203">Go toohello Dev Center and open hello app that you just created.</span></span> <span data-ttu-id="1f860-204">**Hizmetler** > **Anında İletme Bildirimleri** > **Live Services sitesine** tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1f860-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="1f860-205">Merhaba sitesinde hello not edin **uygulama gizli anahtarı** ve hello **paket SID'si**.</span><span class="sxs-lookup"><span data-stu-id="1f860-205">On hello site, take note of hello **Application Secret** and hello **Package SID**.</span></span> <span data-ttu-id="1f860-206">İhtiyacınız olacak hem hello Azure Portal-bildirim hub'ınızı açın, üzerinde **ayarları** > **Bildirim Hizmetleri** > **Windows (WNS)**ve gerekli hello alanlara hello bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="1f860-206">You will need both in hello Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter hello information in hello required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="1f860-207">**Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1f860-207">Click on **Save**.</span></span>

<span data-ttu-id="1f860-208">**Çözüm Gezgini**'nde **Başvurular**'a sağ tıklayın ve **NuGet Paketlerini Yönet**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="1f860-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="1f860-209">Tooadd başvuru toohello ihtiyacımız **Microsoft Azure Service Bus yönetilen kitaplık** – yalnızca arama `WindowsAzure.Messaging.Managed` ve tooyour proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1f860-209">We will need tooadd a reference toohello **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it tooyour project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="1f860-210">Test amacıyla, hello oluşturabilir `MainPage_Loaded` olay işleyicisini yeniden, bu kod parçacığını tooit ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1f860-210">For testing purposes, we can create hello `MainPage_Loaded` event handler once again, and add this code snippet tooit:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="1f860-211">Yukarıdaki Hello hello bildirim hub'hello uygulama kaydeder.</span><span class="sxs-lookup"><span data-stu-id="1f860-211">hello above registers hello app with hello notification hub.</span></span> <span data-ttu-id="1f860-212">Hazır toogo olduğunuz!</span><span class="sxs-lookup"><span data-stu-id="1f860-212">You are ready toogo!</span></span> 

<span data-ttu-id="1f860-213">İçinde `LocationHelper`, hello içinde `Geolocator_PositionChanged` işleyicisi hello konumu hello bölge sınırının içine zorla sokar test kodu parçası ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1f860-213">In `LocationHelper`, inside hello `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put hello location inside hello geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="1f860-214">(Hangi hello sınırlar içinde hello şu anda olmayabilir) hello gerçek koordinatları geçirmediğimiz olmayan ve önceden tanımlanmış test değerleri için biz güncelleştirme üzerinde bir bildirim görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="1f860-214">Because we are not passing hello real coordinates (which might not be within hello boundaries at hello moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="1f860-215">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="1f860-215">What’s next?</span></span>
<span data-ttu-id="1f860-216">Birkaç ek toohello toomake hello çözümün üretime hazır olduğundan emin yukarıda toofollow gerekebilecek adım vardır.</span><span class="sxs-lookup"><span data-stu-id="1f860-216">There are a couple of steps that you might need toofollow in addition toohello above toomake sure that hello solution is production-ready.</span></span>

<span data-ttu-id="1f860-217">Öncelikle, bölge sınırlarının dinamik olduğundan tooensure gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1f860-217">First and foremost, you might need tooensure that geofences are dynamic.</span></span> <span data-ttu-id="1f860-218">Bu sipariş toobe mümkün tooupload yeni sınırları içinde hello varolan bir veri kaynağını hello Bing API'si ile bazı ek çalışmalar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1f860-218">This will require some extra work with hello Bing API in order toobe able tooupload new boundaries within hello existing data source.</span></span> <span data-ttu-id="1f860-219">Merhaba başvurun [Bing uzamsal Veri Hizmetleri API belgelerine](https://msdn.microsoft.com/library/ff701734.aspx) hello konu hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="1f860-219">Consult hello [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on hello subject.</span></span>

<span data-ttu-id="1f860-220">İkinci olarak, çalışma tooensure hello teslim toohello doğru katılımcılara yapıldığından olarak tootarget isteyebilirsiniz aracılığıyla bunları [etiketleme](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="1f860-220">Second, as you are working tooensure that hello delivery is done toohello right participants, you might want tootarget them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="1f860-221">Yukarıda gösterilen hello çözümü hesabınıza hello bölge sınırlaması toosystem özgü özellikleri sınır değil için çok çeşitli hedef platformlara sahip neden olabileceğiniz bir senaryo açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1f860-221">hello solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit hello geofencing toosystem-specific capabilities.</span></span> <span data-ttu-id="1f860-222">Bununla hello Evrensel Windows platformu sunar yetenekleri çok[bölge sınırlarının sağ out-of--box algılamak](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="1f860-222">That said, hello Universal Windows Platform offers capabilities too[detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="1f860-223">Notification Hubs özellikleri hakkında daha ayrıntılı bilgi için [belge portalımıza](https://azure.microsoft.com/documentation/services/notification-hubs/) göz atın.</span><span class="sxs-lookup"><span data-stu-id="1f860-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

