---
title: "Azure CLI kullanarak Azure Redis önbelleği aaaManage | Microsoft Docs"
description: "Nasıl tooinstall hello Azure CLI herhangi bir platformda nasıl bilgi toouse, tooconnect tooyour Azure hesabı ve nasıl toocreate ve Redis önbelleği hello Azure CLI ' yönetebilirsiniz."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a>Nasıl toocreate ve hello Azure komut satırı arabirimi (Azure CLI) kullanarak Azure Redis önbelleği yönetme
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Azure CLI](cache-manage-cli.md)
>
>

Hello Azure CLI mükemmel şekilde toomanage Azure altyapınızı herhangi bir platform değil. Bu makale size nasıl gösterir toocreate ve Azure Redis önbelleği örneklerinizi hello Azure CLI kullanarak yönetebilirsiniz.

> [!NOTE]
> Bu makale, Azure CLI önceki sürümü tooa geçerlidir. Merhaba en son Azure CLI 2.0 örnek komut dosyaları için bkz: [CLI Azure Redis önbelleği örnekleri](cli-samples.md).
> 
> 

## <a name="prerequisites"></a>Ön koşullar
toocreate ve Azure CLI kullanarak Azure Redis önbelleği örnekleri yönetebilir, hello aşağıdaki adımları tamamlamanız gerekir.

* Bir Azure hesabınızın olması gerekir. Yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika sonra.
* [Hello Azure CLI yükleme](../cli-install-nodejs.md).
* Kişisel bir Azure hesabı veya bir iş ile Azure CLI yüklemenizi bağlanmak veya Okul Azure hesabı ve oturum açın hello hello kullanarak Azure CLI `azure login` komutu. toounderstand Merhaba farklar ve seçin, bkz: [hello Azure komut satırı arabirimi (Azure CLI) tooan Azure aboneliğine bağlanma](../xplat-cli-connect.md).
* Komutları aşağıdaki hello birini çalıştırmadan önce hello çalıştırarak hello Azure CLI Resource Manager moduna geçin `azure config mode arm` komutu. Daha fazla bilgi için bkz: [hello Azure CLI toomanage Azure kullanmak kaynaklar ve kaynak grupları](../xplat-cli-azure-resource-manager.md).

## <a name="redis-cache-properties"></a>Redis önbelleği özellikleri
Merhaba aşağıdaki özellikleri oluşturma ve Redis önbelleği örnekleri güncelleştirme olduğunda kullanılır.

| Özellik | Anahtar | Açıklama |
| --- | --- | --- |
| ad |-n,--adı |Merhaba Redis önbelleği adı. |
| kaynak grubu |-g,--kaynak-grubu |Merhaba kaynak grubunun adı. |
| location |-l,--konum |Konum toocreate önbelleği. |
| Boyutu |-z,--boyutu |Merhaba Redis önbelleği boyutu. Geçerli değerler: [C0 C1, C2, C3, C4, C5, C6, P1, P2, P3, P4] |
| SKU |-x,--sku |SKU redis. Şunlardan biri olmalıdır: [temel, standart, Premium] |
| EnableNonSslPort |-e,--enable-olmayan-ssl-bağlantı noktası |Merhaba Redis önbelleği EnableNonSslPort özelliği. Bu bayrak önbelleğiniz için tooenable hello olmayan SSL bağlantı noktası istiyorsanız ekleyin |
| Yapılandırma redis |-c,--redis-yapılandırma |Yapılandırma redis. Yapılandırma anahtarları ve değerleri burada biçimlendirilmiş JSON dizesi girin. Biçim: "{" ":""," ":" "}" |
| Yapılandırma redis |-f,--redis yapılandırma dosyası |Yapılandırma redis. Yapılandırma anahtarları ve değerleri burada içeren bir dosyayı Hello yolunu girin. Merhaba dosyası girişi için biçimi: {"": "","": ""} |
| Parça sayısı |-r,--parça sayısı |Kümeleme ile Premium küme önbellekteki parça toocreate sayısı. |
| Sanal Ağ |-v,--sanal ağ |Önbelleğiniz bir VNET içindeki barındırma belirttiğinde hello tam ARM kaynak Kimliğini hello sanal ağ toodeploy hello redis Önbelleği'nde. Örnek Biçim: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| Anahtar türü |-t,--anahtar türü |Anahtar toorenew türü. Geçerli değerler: [birincil, ikincil] |
| StaticIP |-p,--statik IP < statik IP > |Önbelleğinizi bir VNET içindeki barındırdığında hello alt hello önbelleği için benzersiz bir IP adresi belirtir. Sağlanmazsa, bir sizin için hello alt ağdan seçilir. |
| Alt ağ |t,--alt ağ<subnet> |Önbelleğiniz bir VNET içindeki barındırdığında hangi toodeploy hello Önbelleği'nde hello alt hello adını belirtir. |
| VirtualNetwork |-v,--sanal ağ < sanal ağ > |Önbelleğiniz bir VNET içindeki barındırma belirttiğinde hello tam ARM kaynak Kimliğini hello sanal ağ toodeploy hello redis Önbelleği'nde. Örnek Biçim: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| Abonelik |-s,--abonelik |Merhaba abonelik tanımlayıcısı. |

## <a name="see-all-redis-cache-commands"></a>Tüm Redis önbelleği komutları bakın
toosee tüm Redis önbelleği komutları ve bunların parametrelerini kullanmak hello `azure rediscache -h` komutu.

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a>Redis Cache oluşturma
toocreate bir Redis önbelleği hello aşağıdaki komutu kullanın:

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache create -h` komutu.

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a>Varolan bir Redis önbelleği Sil
toodelete bir Redis önbelleği hello aşağıdaki komutu kullanın:

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache delete -h` komutu.

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a>Abonelik veya kaynak grubu içindeki tüm Redis önbellekleri listesi
Abonelik veya kaynak grubu içindeki tüm Redis önbellekleri toolist kullanmak hello komutu:

    azure rediscache list [options]

Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache list -h` komutu.

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a>Varolan bir Redis önbelleği özelliklerini göster
bir varolan Redis önbelleği, tooshow özelliklerini hello aşağıdaki komutu kullanın:

    azure rediscache show [--name <name> --resource-group <resource-group>]

Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache show -h` komutu.

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a>Varolan bir Redis önbelleği ayarlarını değiştir
toochange ayarlarını bir varolan Redis önbelleği, komutu aşağıdaki hello kullan:

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache set -h` komutu.

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a>Varolan bir Redis önbelleği için Hello kimlik doğrulama anahtarı yenileme
bir varolan Redis önbelleği için komutu aşağıdaki kullanım hello toorenew hello kimlik doğrulama anahtarı:

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

Belirtin `Primary` veya `Secondary` için `key-type`.

Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache renew-key -h` komutu.

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a>Varolan bir Redis önbelleği listesi birincil ve ikincil anahtarları
bir varolan Redis önbelleği, toolist birincil ve ikincil anahtarları hello aşağıdaki komutu kullanın:

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache list-keys -h` komutu.

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
