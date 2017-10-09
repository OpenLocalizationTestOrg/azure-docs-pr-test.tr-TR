<span data-ttu-id="40d23-101">.NET uygulamaları hello kullanabileceğiniz **StackExchange.Redis** hello önbellek istemcisi uygulamalarının yapılandırmasını basitleştiren bir NuGet paketi kullanarak Visual Studio'da yapılandırılabilir önbellek istemcisi.</span><span class="sxs-lookup"><span data-stu-id="40d23-101">.NET applications can use hello **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies hello configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="40d23-102">Daha fazla bilgi için bkz: Merhaba [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github sayfası ve hello [StackExchange.Redis önbellek istemcisi belgeleri](http://github.com/StackExchange/StackExchange.Redis#documentation).</span><span class="sxs-lookup"><span data-stu-id="40d23-102">For more information, see hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  hello [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="40d23-103">tooconfigure Visual Studio'da hello StackExchange.Redis NuGet paketi kullanarak bir istemci uygulaması sağ hello projesinde **Çözüm Gezgini** ve **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="40d23-103">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, right-click hello project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![NuGet paketlerini yönetme](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="40d23-105">Tür **StackExchange.Redis** veya **StackExchange.Redis.StrongName** hello arama metin kutusuna hello sonuçlarından hello istediğiniz sürümü seçin ve tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="40d23-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into hello search text box, select hello desired version from hello results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="40d23-106">Toouse hello tanımlayıcı adlı bir sürümünü tercih ederseniz **StackExchange.Redis** istemci kitaplığı seçin **StackExchange.Redis.StrongName**; Aksi takdirde seçin **StackExchange.Redis**.</span><span class="sxs-lookup"><span data-stu-id="40d23-106">If you prefer toouse a strong-named version of hello **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![StackExchange.Redis NuGet paketi](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="40d23-108">Merhaba paketi indirir ve hello ekler NuGet derleme başvurularını hello StackExchange.Redis önbellek istemcisi ile istemci uygulaması tooaccess Azure Redis önbelleği için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="40d23-108">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="40d23-109">Daha önce proje toouse StackExchange.Redis yapılandırdıysanız, güncelleştirmeleri toohello hello paketinden denetleyebilirsiniz **NuGet Paket Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="40d23-109">If you have previously configured your project toouse StackExchange.Redis, you can check for updates toohello package from hello **NuGet Package Manager**.</span></span> <span data-ttu-id="40d23-110">için toocheck tıklatıp hello StackExchange.Redis NuGet paketi güncelleştirme yükleme sürümlerini **güncelleştirmeleri** hello hello içinde **NuGet Paket Yöneticisi** penceresi.</span><span class="sxs-lookup"><span data-stu-id="40d23-110">toocheck for and install updated versions of hello StackExchange.Redis NuGet package, click **Updates** in hello hello **NuGet Package Manager** window.</span></span> <span data-ttu-id="40d23-111">Bir güncelleştirme toohello StackExchange.Redis NuGet paketi kullanılabilir durumdaysa, proje toouse hello güncelleştirilmiş sürümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40d23-111">If an update toohello StackExchange.Redis NuGet package is available, you can update your project toouse hello updated version.</span></span>
> 
> 

<span data-ttu-id="40d23-112">Tıklatarak hello StackExchange.Redis NuGet paketi yükleyebilirsiniz **NuGet Paket Yöneticisi**, **Paket Yöneticisi Konsolu** hello gelen **Araçları** menü ve çalışan hello hello komutu aşağıdaki **Paket Yöneticisi Konsolu** penceresi.</span><span class="sxs-lookup"><span data-stu-id="40d23-112">You can also install hello StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu, and running hello following command from hello **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```
