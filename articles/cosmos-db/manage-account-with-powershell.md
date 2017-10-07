---
title: "aaaAzure Cosmos DB Otomasyon - Powershell ile Yönetimi | Microsoft Docs"
description: "Kullanım Azure PowerShell'i Azure Cosmos DB hesaplarınızı yönetin."
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 3239fb815918a0e47bff69fcd1ab6562519e429b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a>PowerShell kullanarak bir Azure Cosmos DB hesabı oluşturma

Merhaba aşağıdaki kılavuz Azure Powershell kullanarak Azure Cosmos DB veritabanı hesaplarınızı komutları tooautomate yönetimini açıklar. Komutları toomanage hesabı anahtarları ve yük devretme öncelikleri'nde de içerir [bölgeli veritabanı hesaplarını][scaling-globally]. Veritabanı hesabını güncelleştirme toomodify tutarlılık ilkeleri ve Ekle/Kaldır bölgeler sağlar. Ya da kullanmak için platformlar arası yönetim Azure Cosmos DB hesabınızın [Azure CLI](cli-samples.md), hello [kaynak sağlayıcısı REST API][rp-rest-api], veya hello [Azure Portal](create-documentdb-dotnet.md#create-account).

## <a name="getting-started"></a>Başlarken

Merhaba yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma] [ powershell-install-configure] tooinstall ve tooyour Azure Resource Manager günlüğüne PowerShell'de hesap.

### <a name="notes"></a>Notlar

* Kullanıcı onayı gerektirmeden komutları aşağıdaki tooexecute hello isterseniz hello append `-Force` bayrak toohello komutu.
* Aşağıdaki komutları tüm hello zaman uyumlu.

## <a id="create-documentdb-account-powershell"></a>Bir Azure Cosmos DB hesabı oluşturma

Bu komut, toocreate Azure Cosmos DB veritabanı hesabı sağlar. Yeni veritabanı hesabınız ya da tek bölge yapılandırmak veya [bölgeli] [ scaling-globally] belirli bir ile [tutarlılık İlkesi](consistency-levels.md).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`Başlangıç konumu hello adını hello veritabanı hesabı bölgesi yazma. Bu konum gerekli toohave bir yük devretme öncelik değeri 0 değil. Veritabanı hesabı başına tam olarak bir yazma bölge olması gerekir.
* `<read-region-location>`Başlangıç konumu hello adını hello veritabanı hesabı bölgesi okuyun. Bu konum gerekli toohave 0'dan büyük bir yük devretme öncelik değeri değil. Veritabanı hesabı başına birden fazla okuma bölgeler olabilir.
* `<ip-range-filter>`İzin verilen veritabanı hesabı için istemci IP listesi hello olarak dahil CIDR form toobe Hello kümesi IP adresleri ve IP adres aralıklarını belirtir. IP adresleri/aralıklarına virgülle ayrılmış ve boşluk içermemelidir olması gerekir. Daha fazla bilgi için bkz: [Azure Cosmos DB güvenlik duvarı desteği](firewall-support.md)
* `<default-consistency-level>`Merhaba varsayılan tutarlılık düzeyi hello Azure Cosmos DB hesabı. Daha fazla bilgi için bkz: [Azure Cosmos veritabanı tutarlılık düzeylerini](consistency-levels.md).
* `<max-interval>`Sınırlanmış eskime durumu tutarlılığı ile kullanıldığında, bu değer izin hello süre miktarı (saniye cinsinden) eskime durumu temsil eder. Bu değer için kabul edilebilir aralık 1-100'dür.
* `<max-staleness-prefix>`Sınırlanmış eskime durumu tutarlılığı ile kullanıldığında, bu değer hello izin eski istek sayısını temsil eder. Bu değer için kabul edilebilir aralık 1 – 2,147,483,647 şeklindedir.
* `<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.
* `<resource-group-location>`hello Azure kaynak grubu toowhich hello yeni Azure Cosmos DB veritabanı hesabı Hello konumunu ait.
* `<database-account-name>`oluşturulan hello Azure Cosmos DB veritabanı hesabı toobe Hello adı. Yalnızca küçük harfler, rakamlar, hello kullanabileceği '-' karakteri ve 3-50 karakter arasında olmalıdır.

Örnek: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a>Notlar
* Merhaba önceki örnekte bir veritabanı hesabı ile iki bölgede oluşturur. Ayrıca, olası toocreate (Merhaba yazma bölge atanır ve bir yük devretme öncelik değeri 0 olan) bir bölge veya birden çok iki bölgede bir veritabanı hesabı unutulmamalıdır. Daha fazla bilgi için bkz: [bölgeli veritabanı hesaplarını][scaling-globally].
* Hello konumlarına bölgeler Azure Cosmos DB genel olarak kullanılabilir olması gerekir. Merhaba geçerli bölgelerin listesi hello üzerinde sağlanan [Azure bölgeleri sayfa](https://azure.microsoft.com/regions/#services).

## <a id="update-documentdb-account-powershell"></a>Bir DocumentDB veritabanı hesabı güncelleştirme

Bu komutu tooupdate sağlar, Azure Cosmos DB veritabanı hesabı özellikleri. Bu hangi hello veritabanı hesabı bulunmaktadır hello tutarlılık ilke ve hello konumları içerir.

> [!NOTE]
> Bu komut tooadd ve Kaldır bölgeler sağlar ancak toomodify yük devretme öncelikleri izin vermiyor. toomodify yük devretme öncelikleri görmek [aşağıda](#modify-failover-priority-powershell).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`Başlangıç konumu hello adını hello veritabanı hesabı bölgesi yazma. Bu konum gerekli toohave bir yük devretme öncelik değeri 0 değil. Veritabanı hesabı başına tam olarak bir yazma bölge olması gerekir.
* `<read-region-location>`Başlangıç konumu hello adını hello veritabanı hesabı bölgesi okuyun. Bu konum gerekli toohave 0'dan büyük bir yük devretme öncelik değeri değil. Veritabanı hesabı başına birden fazla okuma bölgeler olabilir.
* `<default-consistency-level>`Merhaba varsayılan tutarlılık düzeyi hello Azure Cosmos DB hesabı. Daha fazla bilgi için bkz: [Azure Cosmos veritabanı tutarlılık düzeylerini](consistency-levels.md).
* `<ip-range-filter>`İzin verilen veritabanı hesabı için istemci IP listesi hello olarak dahil CIDR form toobe Hello kümesi IP adresleri ve IP adres aralıklarını belirtir. IP adresleri/aralıklarına virgülle ayrılmış ve boşluk içermemelidir olması gerekir. Daha fazla bilgi için bkz: [Azure Cosmos DB güvenlik duvarı desteği](firewall-support.md)
* `<max-interval>`Sınırlanmış eskime durumu tutarlılığı ile kullanıldığında, bu değer izin hello süre miktarı (saniye cinsinden) eskime durumu temsil eder. Bu değer için kabul edilebilir aralık 1-100'dür.
* `<max-staleness-prefix>`Sınırlanmış eskime durumu tutarlılığı ile kullanıldığında, bu değer hello izin eski istek sayısını temsil eder. Bu değer için kabul edilebilir aralık 1 – 2,147,483,647 şeklindedir.
* `<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.
* `<resource-group-location>`hello Azure kaynak grubu toowhich hello yeni Azure Cosmos DB veritabanı hesabı Hello konumunu ait.
* `<database-account-name>`güncelleştirilmiş hello Azure Cosmos DB veritabanı hesabı toobe Hello adı.

Örnek: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <a id="delete-documentdb-account-powershell"></a>Bir DocumentDB veritabanı hesabı silme

Bu komut toodelete var olan bir Azure Cosmos DB veritabanı hesabını verir.

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* `<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.
* `<database-account-name>`hello Azure Cosmos DB veritabanı hesabı toobe silinmiş Hello adı.

Örnek:

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="get-documentdb-properties-powershell"></a>Bir DocumentDB veritabanı hesabı özelliklerini alır

Bu komut, var olan bir Azure Cosmos DB veritabanı hesabını tooget hello özelliklerini sağlar.

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.
* `<database-account-name>`hello Azure Cosmos DB veritabanı hesabı Hello adı.

Örnek:

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="update-tags-powershell"></a>Bir Azure Cosmos DB veritabanı hesabını güncelleştirme etiketleri

Merhaba aşağıdaki örnekte açıklanmaktadır nasıl tooset [Azure kaynak etiketleri] [ azure-resource-tags] Azure Cosmos DB için veritabanı hesabı.

> [!NOTE]
> Bu komut hello ile birleştirilebilir oluşturma veya güncelleştirme komutları hello ekleyerek `-Tags` bayrağı hello karşılık gelen bir parametre ile.

Örnek:

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <a id="list-account-keys-powershell"></a>Liste hesabı anahtarları

Bir Azure Cosmos DB hesabı oluşturduğunuzda, hello hizmeti hello Azure Cosmos DB hesap erişildiğinde, kimlik doğrulaması için kullanılan iki ana erişim tuşu oluşturur. İki erişim tuşu sağlayarak Azure Cosmos DB tooregenerate hello herhangi kesinti tooyour Azure Cosmos DB hesap anahtarlarla sağlar. Salt okunur işlemler kimlik doğrulaması için salt okunur anahtar de kullanılabilir. Var. iki okuma-yazma anahtarları (birincil ve ikincil) ve iki salt okunur anahtarları (birincil ve ikincil)

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.
* `<database-account-name>`hello Azure Cosmos DB veritabanı hesabı Hello adı.

Örnek:

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="list-connection-strings-powershell"></a>Liste bağlantı dizeleri

MongoDB hesapları için komutu aşağıdaki hello kullanarak MongoDB uygulama toohello veritabanı hesabınızı alınabilir bağlantı dizesi tooconnect hello.

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.
* `<database-account-name>`hello Azure Cosmos DB veritabanı hesabı Hello adı.

Örnek:

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="regenerate-account-key-powershell"></a>Hesap anahtarını yeniden oluşturma

Merhaba erişim anahtarları tooyour Azure Cosmos DB hesabı değiştirmelisiniz düzenli aralıklarla toohelp tutmak bağlantılarınızı daha güvenlidir. İki erişim tuşu tooenable atanır, toomaintain bağlantıları toohello bir erişim anahtarı kullanırken, yeniden Azure Cosmos DB hesap hello diğer erişim anahtarı.

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* `<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.
* `<database-account-name>`hello Azure Cosmos DB veritabanı hesabı Hello adı.
* `<key-kind>`Anahtarların hello dört türlerinden birini: ["Birincil" | " İkincil "|" PrimaryReadonly "|" Tooregenerate istediğiniz SecondaryReadonly"].

Örnek:

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <a id="modify-failover-priority-powershell"></a>Bir Azure Cosmos DB veritabanı hesabının yük devretme öncelik değiştirme

Bölgeli veritabanı hesapları için Azure Cosmos DB veritabanı hesabı hello çeşitli bölgelere mevcut hello hello yük devretme önceliğini değiştirebilirsiniz. Azure Cosmos DB veritabanı hesabınızda yük devretme hakkında daha fazla bilgi için bkz: [Azure Cosmos DB genel verilerle dağıtmak][distribute-data-globally].

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* `<write-region-location>`Başlangıç konumu hello adını hello veritabanı hesabı bölgesi yazma. Bu konum gerekli toohave bir yük devretme öncelik değeri 0 değil. Veritabanı hesabı başına tam olarak bir yazma bölge olması gerekir.
* `<read-region-location>`Başlangıç konumu hello adını hello veritabanı hesabı bölgesi okuyun. Bu konum gerekli toohave 0'dan büyük bir yük devretme öncelik değeri değil. Veritabanı hesabı başına birden fazla okuma bölgeler olabilir.
* `<resource-group-name>`Merhaba Hello adını [Azure kaynak grubu] [ azure-resource-groups] toowhich hello yeni Azure Cosmos DB veritabanı hesabı ait.
* `<database-account-name>`hello Azure Cosmos DB veritabanı hesabı Hello adı.

Örnek:

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a>Sonraki adımlar

* .NET kullanarak tooconnect bkz [bağlanma ve sorgu .NET ile](create-documentdb-dotnet.md).
* .NET Core kullanarak tooconnect bkz [Connect ve .NET Core sorguyla](create-documentdb-dotnet-core.md).
* Node.js kullanarak tooconnect bkz [Connect ve Node.js ve MongoDB uygulama sorguyla](create-mongodb-nodejs.md).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
