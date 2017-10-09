toocreate bir önbellek toohello içinde'ilk kez oturum [Azure portal](https://portal.azure.com), tıklatıp **yeni** > **veritabanları** > **Redis önbelleği**.

> [!NOTE]
> Azure hesabınız yoksa, yalnızca birkaç dakika içinde [Ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).
> 
> 

![Yeni önbellek](media/redis-cache-create/redis-cache-new-cache-menu.png)

> [!NOTE]
> Ayrıca toocreating hello Azure portalında önbelleğe alır, bunları Kaynak Yöneticisi'ni kullanarak da oluşturabilirsiniz şablonları, PowerShell veya Azure CLI.
> 
> * Resource Manager şablonları kullanarak önbellek a toocreate bkz [bir şablon kullanarak Redis önbelleği oluşturma](../articles/redis-cache/cache-redis-cache-arm-provision.md).
> * Azure PowerShell kullanarak önbellek toocreate bkz [Azure Redis önbelleğini Yönetme'Azure PowerShell ile](../articles/redis-cache/cache-howto-manage-redis-cache-powershell.md).
> * Azure CLI kullanarak önbellek toocreate bkz [nasıl toocreate ve hello Azure komut satırı arabirimi (Azure CLI) kullanarak Azure Redis önbelleği yönetmek](../articles/redis-cache/cache-manage-cli.md).
> 
> 

Merhaba, **yeni Redis önbelleği** dikey penceresinde hello hello önbelleği için istenen yapılandırmayı belirtin.

![Önbellek oluşturma](media/redis-cache-create/redis-cache-cache-create.png) 

* İçinde **Dns adı**, hello önbellek uç noktası için bir benzersiz önbellek adı toouse girin. Merhaba önbellek adı 1 ile 63 karakter arasında bir dize olması ve yalnızca rakam, harf ve hello içermelidir `-` karakter. Merhaba önbellek adı başlayamaz veya bitemez ile Merhaba `-` karakteri ve ardışık `-` karakterler geçerli değil.
* İçin **abonelik**, hello toouse hello önbelleği için istediğiniz Azure aboneliğini seçin. Hesabınızda yalnızca bir abonelik varsa, otomatik olarak seçilir ve hello **abonelik** açılan görüntülenmeyecek.
* **Kaynak grubu**’nda önbellek hesabınız için bir kaynak grubu seçin veya oluşturun. Daha fazla bilgi için bkz: [kullanarak kaynak gruplarını toomanage Azure kaynaklarınızı](../articles/azure-resource-manager/resource-group-overview.md). 
* Kullanım **konumu** toospecify hello coğrafi konum önbelleğiniz barındırılır. Merhaba en iyi performans için Microsoft hello hello önbelleği oluşturma önerir hello önbellek istemci uygulamasının aynı bölgede.
* Kullanım **fiyatlandırma katmanı** tooselect hello istenen önbellek boyutu ve özellikler.
* **Redis kümesi** toocreate önbellekleri birden çok Redis düğümünde 53 GB'a ve tooshard veri büyük sağlar. Daha fazla bilgi için bkz: [nasıl bir Premium Azure Redis önbelleği için kümeleri tooconfigure](../articles/redis-cache/cache-how-to-premium-clustering.md).
* **Redis kalıcılığı** , önbellek tooan Azure depolama hesabı hello özelliği toopersist sunar. Kalıcılığı yapılandırma ile ilgili yönergeler için bkz: [nasıl Premium Azure Redis önbelleği için kalıcılığı tooconfigure](../articles/redis-cache/cache-how-to-premium-persistence.md).
* **Sanal ağ** erişim tooyour önbellek tooonly kısıtlayarak belirtilen hello içindeki istemcilerle Gelişmiş Güvenlik ve yalıtım sağlar Azure sanal ağı. Alt ağlar, erişim denetimi ilkeleri ve diğer özellikleri toofurther erişim tooRedis kısıtlamak gibi vnet'in tüm hello özelliklerini kullanabilirsiniz. Daha fazla bilgi için bkz: [tooconfigure sanal ağ Premium Azure Redis önbelleği için nasıl destek](../articles/redis-cache/cache-how-to-premium-vnet.md).
* SSL olmayan erişim yeni önbellekler için varsayılan olarak devre dışı bırakılmıştır. tooenable hello SSL olmayan bağlantı noktası, onay **6379 (SSL şifreli) bağlantı noktasının engelini kaldırmak**.

Merhaba yeni önbellek seçenekleri yapılandırıldıktan sonra tıklatın **oluşturma**. Oluşturulan hello önbellek toobe birkaç dakika sürebilir. toocheck hello durumunu hello Sabitle hello ilerlemeyi izleyebilirsiniz. Merhaba önbellek oluşturulduktan sonra yeni önbelleğiniz bir **çalıştıran** durumu ve ile kullanım için hazır [varsayılan ayarları](../articles/redis-cache/cache-configure.md#default-redis-server-configuration).

![Önbellek oluşturuldu](media/redis-cache-create/redis-cache-cache-created.png)

