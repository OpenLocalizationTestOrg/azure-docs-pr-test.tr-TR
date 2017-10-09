.NET uygulamaları hello kullanabileceğiniz **StackExchange.Redis** hello önbellek istemcisi uygulamalarının yapılandırmasını basitleştiren bir NuGet paketi kullanarak Visual Studio'da yapılandırılabilir önbellek istemcisi. 

> [!NOTE]
> Daha fazla bilgi için bkz: Merhaba [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github sayfası ve hello [StackExchange.Redis önbellek istemcisi belgeleri](http://github.com/StackExchange/StackExchange.Redis#documentation).
> 
> 

tooconfigure Visual Studio'da hello StackExchange.Redis NuGet paketi kullanarak bir istemci uygulaması sağ hello projesinde **Çözüm Gezgini** ve **NuGet paketlerini Yönet**. 

![NuGet paketlerini yönetme](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

Tür **StackExchange.Redis** veya **StackExchange.Redis.StrongName** hello arama metin kutusuna hello sonuçlarından hello istediğiniz sürümü seçin ve tıklatın **yükleme**.

> [!NOTE]
> Toouse hello tanımlayıcı adlı bir sürümünü tercih ederseniz **StackExchange.Redis** istemci kitaplığı seçin **StackExchange.Redis.StrongName**; Aksi takdirde seçin **StackExchange.Redis**.
> 
> 

![StackExchange.Redis NuGet paketi](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

Merhaba paketi indirir ve hello ekler NuGet derleme başvurularını hello StackExchange.Redis önbellek istemcisi ile istemci uygulaması tooaccess Azure Redis önbelleği için gereklidir.

> [!NOTE]
> Daha önce proje toouse StackExchange.Redis yapılandırdıysanız, güncelleştirmeleri toohello hello paketinden denetleyebilirsiniz **NuGet Paket Yöneticisi**. için toocheck tıklatıp hello StackExchange.Redis NuGet paketi güncelleştirme yükleme sürümlerini **güncelleştirmeleri** hello hello içinde **NuGet Paket Yöneticisi** penceresi. Bir güncelleştirme toohello StackExchange.Redis NuGet paketi kullanılabilir durumdaysa, proje toouse hello güncelleştirilmiş sürümünü güncelleştirebilirsiniz.
> 
> 

Tıklatarak hello StackExchange.Redis NuGet paketi yükleyebilirsiniz **NuGet Paket Yöneticisi**, **Paket Yöneticisi Konsolu** hello gelen **Araçları** menü ve çalışan hello hello komutu aşağıdaki **Paket Yöneticisi Konsolu** penceresi.
    
```
Install-Package StackExchange.Redis
```
