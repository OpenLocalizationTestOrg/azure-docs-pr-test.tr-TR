---
title: "Azure PowerShell ile Azure Redis önbelleği aaaManage | Microsoft Docs"
description: "Bilgi nasıl tooperform yönetim görevlerini Azure PowerShell kullanarak Azure Redis önbelleği için."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a>Azure PowerShell ile Azure Redis önbelleği Yönet
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Azure CLI](cache-manage-cli.md)
> 
> 

Bu konu nasıl tooperform ortak oluşturmak gibi görevleri gösterir, güncelleştirme ve Azure Redis önbelleği örneklerinizi nasıl ölçeklendirin tooregenerate erişim anahtarlarını ve nasıl tooview önbellekleri hakkında bilgi. Azure Redis önbelleği PowerShell cmdlet'lerinin tam listesi için bkz: [Azure Redis önbelleği cmdlet'leri](https://msdn.microsoft.com/library/azure/mt634513.aspx).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

Merhaba Klasik dağıtım modeli hakkında daha fazla bilgi için bkz: [Azure Resource Manager ve klasik dağıtım: dağıtım modellerini anlama ve hello kaynaklarınızın durumunu](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).

## <a name="prerequisites"></a>Ön koşullar
Azure PowerShell'i zaten yüklediyseniz, Azure PowerShell sürümü 1.0.0 olmalıdır veya sonraki bir sürümü. Bu komutla hello Azure PowerShell komut isteminde yüklediğiniz Azure PowerShell hello sürümü kontrol edebilirsiniz.

    Get-Module azure | format-table version


İlk olarak, bu komutla tooAzure olarak oturum açmalısınız.

    Login-AzureRmAccount

Merhaba Microsoft Azure oturum açma iletişim kutusunda Azure hesabınızı ve kendi parolasını Hello e-posta adresini belirtin.

Ardından, birden çok Azure aboneliğiniz varsa, Azure aboneliğinizin tooset gerekir. toosee geçerli aboneliklerinizi listesini bu komutu çalıştırın.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

toospecify hello abonelik, komutu aşağıdaki hello çalıştırın. Aşağıdaki örneğine hello hello abonelik adıdır `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

Azure Resource Manager ile Windows PowerShell kullanabilmeniz için önce hello aşağıdaki gerekir:

* Windows PowerShell sürüm 3.0 veya 4.0. Windows PowerShell, türü toofind hello sürümü:`$PSVersionTable` ve hello değerini doğrulayın `PSVersion` 3.0 veya 4.0. tooinstall uyumlu bir sürümde bkz [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) veya [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

tooget ayrıntılı hello Get-Help cmdlet'ini kullanın Bu öğreticide gördüğünüz herhangi bir cmdlet için Yardım.

    Get-Help <cmdlet-name> -Detailed

Örneğin, tooget yardımını hello `New-AzureRmRedisCache` cmdlet, türü:

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a>Nasıl tooconnect tooother Bulutlar
Varsayılan hello Azure tarafından ortamıdır `AzureCloud`, hangi hello genel Azure bulut örneği temsil eder. tooconnect tooa farklı bir örnek, kullanım hello `Add-AzureRmAccount` hello komutunu `-Environment` veya -`EnvironmentName` komut satırı anahtarıyla hello istenen ortama veya ortam adı.

Merhaba çalıştırmak kullanılabilir ortamları toosee hello listesi `Get-AzureRmEnvironment` cmdlet'i.

### <a name="tooconnect-toohello-azure-government-cloud"></a>tooconnect toohello Azure Bulutu
tooconnect toohello Azure Bulutu komutları aşağıdaki hello birini kullanın.

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

or

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

toocreate hello Azure Bulutu önbelleğinde hello aşağıdaki konumlardan birini kullanın.

* ABD hükümeti Virginia
* ABD hükümeti Iowa

Hello Azure Bulutu hakkında daha fazla bilgi için bkz: [Microsoft Azure kamu](https://azure.microsoft.com/features/gov/) ve [Microsoft Azure kamu Geliştirici Kılavuzu](../azure-government-developer-guide.md).

### <a name="tooconnect-toohello-azure-china-cloud"></a>tooconnect toohello Azure Çin bulut
tooconnect toohello Azure Çin bulut komutları aşağıdaki hello birini kullanın.

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

or

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

toocreate hello Azure Çin bulut önbelleğinde hello aşağıdaki konumlardan birini kullanın.

* Çin Doğu
* Çin Kuzey

Hello Azure Çin bulut hakkında daha fazla bilgi için bkz: [AzureChinaCloud Azure Çin'de 21Vianet tarafından işletilen](http://www.windowsazure.cn/).

### <a name="tooconnect-toomicrosoft-azure-germany"></a>tooconnect tooMicrosoft Azure Almanya
tooconnect tooMicrosoft Azure Almanya komutları aşağıdaki hello birini kullanın.

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


or

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

Microsoft Azure Almanya, önbellekte toocreate hello aşağıdaki konumlardan birini kullanın.

* Almanya Orta
* Almanya Kuzeydoğu

Microsoft Azure Almanya hakkında daha fazla bilgi için bkz: [Microsoft Azure Almanya](https://azure.microsoft.com/overview/clouds/germany/).

### <a name="properties-used-for-azure-redis-cache-powershell"></a>Azure Redis önbelleği PowerShell için kullanılan özellikleri
Aşağıdaki tablonun hello özellikleri ve açıklamaları oluştururken ve Azure PowerShell kullanarak Azure Redis önbelleği örneklerinizi yönetme yaygın olarak kullanılan parametreleri içerir.

| Parametre | Açıklama | Varsayılan |
| --- | --- | --- |
| Ad |Merhaba önbellek adı | |
| Konum |Merhaba önbellek konumu | |
| resourceGroupName |Hangi toocreate hello önbelleğinde kaynak grubu adı | |
| Boyut |Merhaba önbellek boyutunu Hello. Geçerli değerler: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5 GB, 6 GB, 13 GB, 26 GB, 53 GB'a |1 GB |
| ShardCount |premium önbelleği kümeleme özelliği etkinleştirilmiş oluştururken parça toocreate Hello sayısı. Geçerli değerler: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 | |
| SKU |Merhaba hello önbellek SKU'su belirtir. Geçerli değerler: temel, standart ve Premium |Standart |
| RedisConfiguration |Redis yapılandırma ayarlarını belirtir. Merhaba aşağıdaki her ayarlama hakkında daha fazla bilgi için bkz: [RedisConfiguration özellikleri](#redisconfiguration-properties) tablo. | |
| EnableNonSslPort |Merhaba SSL olmayan bağlantı noktası etkinleştirilip etkinleştirilmeyeceğini gösterir. |False |
| MaxMemoryPolicy |Bu parametre kullanım dışı - RedisConfiguration kullanın. | |
| StaticIP |Önbelleğinizi bir VNET içindeki barındırdığında hello alt hello önbelleği için benzersiz bir IP adresi belirtir. Sağlanmazsa, bir sizin için hello alt ağdan seçilir. | |
| Alt ağ |Önbelleğiniz bir VNET içindeki barındırdığında hangi toodeploy hello Önbelleği'nde hello alt hello adını belirtir. | |
| VirtualNetwork |Önbelleğinizi bir VNET içindeki barındırma belirttiğinde hello kaynak Kimliğini VNET hangi toodeploy hello önbelleğinde hello. | |
| keyType |Hangi erişim tuşu belirtir erişim tuşları yenilenirken tooregenerate. Geçerli değerler: birincil, ikincil | |

### <a name="redisconfiguration-properties"></a>RedisConfiguration özellikleri
| Özellik | Açıklama | Fiyatlandırma katmanları |
| --- | --- | --- |
| RDB yedekleme etkin |Olup olmadığını [Redis veri kalıcılığını](cache-how-to-premium-persistence.md) etkin |Yalnızca Premium |
| RDB depolama bağlantı dizesi |Merhaba bağlantı dizesi toohello depolama hesabı için [Redis veri kalıcılığını](cache-how-to-premium-persistence.md) |Yalnızca Premium |
| RDB yedekleme sıklığı |Merhaba yedekleme sıklığına [Redis veri kalıcılığını](cache-how-to-premium-persistence.md) |Yalnızca Premium |
| maxmemory-ayrılmış |Merhaba yapılandırır [ayrılan bellek](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) önbellek olmayan işlemler için |Standart ve Premium |
| maxmemory İlkesi |Merhaba yapılandırır [çıkarma İlkesi](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) hello önbelleği |Tüm fiyatlandırma katmanlarına |
| bildirim-keyspace-olayları |Yapılandırır [keyspace bildirimleri](cache-configure.md#keyspace-notifications-advanced-settings) |Standart ve Premium |
| max ziplist girişlerini karma |Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri |Standart ve Premium |
| karma-max-ziplist-değer |Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri |Standart ve Premium |
| max intset girişlerini ayarlama |Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri |Standart ve Premium |
| max ziplist girişlerini zset |Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri |Standart ve Premium |
| max ziplist değeri zset |Yapılandırır [belleği en iyi duruma getirme](http://redis.io/topics/memory-optimization) küçük toplam veri türleri |Standart ve Premium |
| veritabanları |Veritabanı Hello sayısını yapılandırır. Bu özellik yalnızca önbellek oluşturma sırasında yapılandırılabilir. |Standart ve Premium |

## <a name="toocreate-a-redis-cache"></a>toocreate bir Redis önbelleği
Yeni Azure Redis önbelleği örnekleri hello kullanarak oluşturulur [yeni AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet'i.

> [!IMPORTANT]
> Merhaba hello Azure portal kullanarak bir abonelikte Redis önbelleği oluşturma ilk kez hello portal hello kaydeder `Microsoft.Cache` Bu abonelik için ad alanı. Dener toocreate hello ilk Redis önbelleği PowerShell kullanarak bir abonelikte, komutu aşağıdaki hello kullanarak bu ad önce kaydetmeniz gerekir; Aksi takdirde cmdlet'leri gibi `New-AzureRmRedisCache` ve `Get-AzureRmRedisCache` başarısız.
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

toosee listesini kullanılabilir parametreleri ve açıklamaları için `New-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

toocreate bir önbellek varsayılan parametrelerle hello aşağıdaki komutu çalıştırın.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

`ResourceGroupName`, `Name`, ve `Location` Gerekli Parametreler, ancak hello rest isteğe bağlıdır ve varsayılan değerlere sahip. Merhaba önceki komutunu çalıştırarak hello belirtilen adını, konumunu ve devre dışı hello SSL olmayan bağlantı noktası ile boyutu 1 GB olan kaynak grubu ile bir standart SKU Azure Redis önbelleği örneği oluşturur.

toocreate premium önbelleği P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), dosya boyutu belirtin P3 (26 GB - 260 GB), ya da P4 (53 GB'a - 530 GB). kümeleme, tooenable belirtin hello kullanarak bir parça sayısı `ShardCount` parametresi. Merhaba aşağıdaki örnek P1 premium önbelleği ile 3 parça oluşturur. P1 premium önbelleği 6 GB boyutunda ve üç parça toplam boyutu hello belirtilen beri 18 GB (3 x 6 GB).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

Merhaba toospecify değerlerini `RedisConfiguration` parametresi hello değerlerini içine alın `{}` anahtar/değer çiftleri ister `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`. Merhaba aşağıdaki örnekte bir standart 1 GB önbellek ile oluşturur `allkeys-random` ile yapılandırılmış maxmemory İlkesi ve keyspace bildirimleri `KEA`. Daha fazla bilgi için bkz: [Keyspace bildirimleri (Gelişmiş ayarları)](cache-configure.md#keyspace-notifications-advanced-settings) ve [bellek ilkeleri](cache-configure.md#memory-policies).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a>önbelleği oluşturma sırasında ayarı tooconfigure hello veritabanları
Merhaba `databases` ayarı yalnızca önbellek oluşturma sırasında yapılandırılabilir. Merhaba aşağıdaki örnekte oluşturur premium P3 (26 GB) önbellek hello kullanarak 48 veritabanlarıyla [yeni AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet'i.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

Merhaba hakkında daha fazla bilgi için `databases` özelliği, bkz: [Azure Redis önbelleği varsayılan sunucu yapılandırma](cache-configure.md#default-redis-server-configuration). Hello kullanarak önbellek oluşturma hakkında daha fazla bilgi için [yeni AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet'in önceki hello bkz [toocreate bir Redis önbelleği](#to-create-a-redis-cache) bölümü.

## <a name="tooupdate-a-redis-cache"></a>tooupdate Redis önbelleği
Azure Redis önbelleği örnekleri hello kullanarak güncel [kümesi AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet'i.

toosee listesini kullanılabilir parametreleri ve açıklamaları için `Set-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Merhaba `Set-AzureRmRedisCache` cmdlet gibi kullanılan tooupdate özellikler olabilir `Size`, `Sku`, `EnableNonSslPort`ve hello `RedisConfiguration` değerleri. 

Merhaba hello Redis önbelleği için maxmemory İlkesi güncelleştirmeleri hello aşağıdaki komutu myCache adlı.

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a>tooscale Redis önbelleği
`Set-AzureRmRedisCache`bir Azure Redis önbelleği örneği hello zaman kullanılan tooscale olabilir `Size`, `Sku`, veya `ShardCount` özellikleri değiştirilemez. 

> [!NOTE]
> PowerShell kullanarak önbellek ölçeklendirme aynı sınırlar konu toohello olduğunu ve Azure portalında bir önbellekten ölçeklendirme olarak yönergeleri hello. Tooa kısıtlamaları aşağıdaki hello ile fiyatlandırma katmanı farklı ölçeklendirebilirsiniz.
> 
> * Bir daha yüksek fiyatlandırma katmanı tooa fiyatlandırma katmanı alt ölçeklendirme olamaz.
> * Ölçeklendirme olamaz bir **Premium** tooa aşağı önbellek **standart** veya **temel** önbelleği.
> * Ölçeklendirme olamaz bir **standart** tooa aşağı önbellek **temel** önbelleği.
> * Ölçeklendirme yapılabilir bir **temel** tooa önbelleğe **standart** önbellek ancak hello hello boyutta değiştiremiyor aynı anda. Farklı bir boyut gerekiyorsa, bir sonraki ölçeklendirme işlemi istenen toohello boyutu yapabilirsiniz.
> * Ölçeklendirme olamaz bir **temel** doğrudan tooa önbelleğe **Premium** önbelleği. Ölçeklendirme gerekir **temel** çok**standart** bir ölçeklendirme işlemi ve ardından gelen **standart** çok**Premium** , sonraki ölçeklendirme işlem.
> * Büyük bir değerden toohello aşağı ölçeklendirme olamaz **C0 (250 MB)** boyutu.
> 
> Daha fazla bilgi için bkz: [nasıl tooScale Azure Redis önbelleği](cache-how-to-scale.md).
> 
> 

Merhaba aşağıdaki örnekte nasıl tooscale bir önbellek adlı gösterir `myCache` tooa 2,5 GB önbellek. Bu komut bir temel veya standart bir önbellek için çalıştığını unutmayın.

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Bu komutu verildikten sonra hello önbellek hello durumu döndürülür (benzer toocalling `Get-AzureRmRedisCache`). Bu hello Not `ProvisioningState` olan `Scaling`.

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

Merhaba ölçeklendirme işlemi tamamlandıktan sonra hello `ProvisioningState` çok değişiklikleri`Succeeded`. Toomake temel tooStandard değiştirme ve ardından hello boyutunu değiştirme gibi sonraki bir ölçeklendirme işlemi gerekiyorsa hello önceki işlem tamamlanana veya bir hata benzer toohello aşağıdaki aldığınız kadar beklemeniz gerekir.

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a>Redis önbelleği hakkında tooget bilgi
Hello kullanarak önbellek hakkında bilgi alabilir [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet'i.

toosee listesini kullanılabilir parametreleri ve açıklamaları için `Get-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Merhaba geçerli Abonelikteki tüm önbellekleri tooreturn bilgilerini çalıştırmak `Get-AzureRmRedisCache` hiçbir parametre olmadan.

    Get-AzureRmRedisCache

belirli bir kaynak grubundaki tüm önbellekleri tooreturn bilgilerini çalıştırmak `Get-AzureRmRedisCache` hello ile `ResourceGroupName` parametresi.

    Get-AzureRmRedisCache -ResourceGroupName myGroup

belirli bir önbelleği hakkında tooreturn bilgi çalıştırmak `Get-AzureRmRedisCache` hello ile `Name` hello önbellek ve hello hello adını içeren parametre `ResourceGroupName` hello kaynak grubu, önbellek içeren parametresiyle.

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a>Redis önbelleği tooretrieve hello erişim tuşları
tooretrieve hello erişim tuşları önbelleğiniz için kullanabileceğiniz hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet'i.

toosee listesini kullanılabilir parametreleri ve açıklamaları için `Get-AzureRmRedisCacheKey`çalıştırın hello aşağıdaki komutu.

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

tooretrieve hello anahtarları önbelleğiniz için arama hello `Get-AzureRmRedisCacheKey` cmdlet'i ve önbelleğiniz hello adını geçişinde hello hello önbellek içeren hello kaynak grubunun adı.

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a>Redis önbelleği için tooregenerate erişim tuşları
tooregenerate hello erişim tuşları önbelleğiniz için kullanabileceğiniz hello [yeni AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet'i.

toosee listesini kullanılabilir parametreleri ve açıklamaları için `New-AzureRmRedisCacheKey`çalıştırın hello aşağıdaki komutu.

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Çağrı hello önbelleğiniz için tooregenerate hello birincil veya ikincil anahtarı `New-AzureRmRedisCacheKey` cmdlet hello geçişinde adı, kaynak grubu ve belirtin `Primary` veya `Secondary` hello için `KeyType` parametresi. Aşağıdaki örneğine hello, önbellek için hello ikincil erişim anahtarını yeniden oluşturur.

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a>toodelete Redis önbelleği
toodelete bir Redis önbelleği kullanma hello [Kaldır AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet'i.

toosee listesini kullanılabilir parametreleri ve açıklamaları için `Remove-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Adlandırılmış önbellek örneği aşağıdaki hello hello `myCache` kaldırılır.

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a>tooimport Redis önbelleği
Hello kullanarak bir Azure Redis önbelleği örneğine verileri içeri aktarabilirsiniz `Import-AzureRmRedisCache` cmdlet'i.

> [!IMPORTANT]
> İçeri/dışarı aktarma için kullanılabilir yalnızca [premium katmanı](cache-premium-tier-intro.md) önbelleğe alır. İçeri/dışarı aktarma hakkında daha fazla bilgi için bkz: [içeri ve dışarı aktarma Azure Redis önbelleği verilerde](cache-how-to-import-export-data.md).
> 
> 

toosee listesini kullanılabilir parametreleri ve açıklamaları için `Import-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Merhaba aşağıdaki komutu verileri Azure Redis önbelleğine hello SAS URI tarafından belirtilen hello blob alır.

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a>tooexport Redis önbelleği
Hello kullanarak bir Azure Redis önbelleği örnekten verileri dışarı aktarabilirsiniz `Export-AzureRmRedisCache` cmdlet'i.

> [!IMPORTANT]
> İçeri/dışarı aktarma için kullanılabilir yalnızca [premium katmanı](cache-premium-tier-intro.md) önbelleğe alır. İçeri/dışarı aktarma hakkında daha fazla bilgi için bkz: [içeri ve dışarı aktarma Azure Redis önbelleği verilerde](cache-how-to-import-export-data.md).
> 
> 

toosee listesini kullanılabilir parametreleri ve açıklamaları için `Export-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Merhaba aşağıdaki komutu veri hello SAS URI tarafından belirtilen hello kapsayıcısı uygulamasına Azure Redis önbelleği örneğinden dışa aktarır.

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a>tooreboot Redis önbelleği
Azure Redis önbelleği örneğinizi hello kullanarak yeniden `Reset-AzureRmRedisCache` cmdlet'i.

> [!IMPORTANT]
> Yeniden başlatma için kullanılabilir yalnızca [premium katmanı](cache-premium-tier-intro.md) önbelleğe alır. Önbelleğinizi yeniden başlatma hakkında daha fazla bilgi için bkz: [önbelleğe yönetim - yeniden başlatma](cache-administration.md#reboot).
> 
> 

toosee listesini kullanılabilir parametreleri ve açıklamaları için `Reset-AzureRmRedisCache`çalıştırın hello aşağıdaki komutu.

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Merhaba aşağıdaki komutu yeniden belirtilen Merhaba, her iki düğüm önbelleği.

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a>Sonraki adımlar
Azure ile Windows PowerShell'i kullanma hakkında daha fazla toolearn kaynakları aşağıdaki hello bakın:

* [MSDN'deki Azure Redis önbelleği cmdlet belgeleri](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* [Azure Resource Manager cmdlet'lerini](http://go.microsoft.com/fwlink/?LinkID=394765): hello Azure Resource Manager modülünde toouse hello cmdlet'leri hakkında bilgi edinme.
* [Azure kaynaklarınızı grupları toomanage kaynağı kullanan](../azure-resource-manager/resource-group-template-deploy-portal.md): öğrenin nasıl toocreate ve hello Azure portalında bulunan kaynak gruplarını yönetin.
* [Azure blogu](http://blogs.msdn.com/windowsazure): Azure yeni özellikler hakkında bilgi edinin.
* [Windows PowerShell Web günlüğü](http://blogs.msdn.com/powershell): Windows PowerShell'de yeni özellikler hakkında bilgi edinin.
* ["Hey, betik yazarı!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Windows PowerShell topluluk hello gerçek ipuçları ve püf noktaları alın.

