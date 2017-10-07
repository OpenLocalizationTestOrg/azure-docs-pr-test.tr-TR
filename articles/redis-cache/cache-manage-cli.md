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
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="30a61-103">Nasıl toocreate ve hello Azure komut satırı arabirimi (Azure CLI) kullanarak Azure Redis önbelleği yönetme</span><span class="sxs-lookup"><span data-stu-id="30a61-103">How toocreate and manage Azure Redis Cache using hello Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="30a61-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="30a61-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="30a61-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="30a61-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="30a61-106">Hello Azure CLI mükemmel şekilde toomanage Azure altyapınızı herhangi bir platform değil.</span><span class="sxs-lookup"><span data-stu-id="30a61-106">hello Azure CLI is a great way toomanage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="30a61-107">Bu makale size nasıl gösterir toocreate ve Azure Redis önbelleği örneklerinizi hello Azure CLI kullanarak yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30a61-107">This article shows you how toocreate and manage your Azure Redis Cache instances using hello Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="30a61-108">Bu makale, Azure CLI önceki sürümü tooa geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="30a61-108">This article applies tooa previous version of Azure CLI.</span></span> <span data-ttu-id="30a61-109">Merhaba en son Azure CLI 2.0 örnek komut dosyaları için bkz: [CLI Azure Redis önbelleği örnekleri](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="30a61-109">For hello latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="30a61-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="30a61-110">Prerequisites</span></span>
<span data-ttu-id="30a61-111">toocreate ve Azure CLI kullanarak Azure Redis önbelleği örnekleri yönetebilir, hello aşağıdaki adımları tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="30a61-111">toocreate and manage Azure Redis Cache instances using Azure CLI, you must complete hello following steps.</span></span>

* <span data-ttu-id="30a61-112">Bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="30a61-112">You must have an Azure account.</span></span> <span data-ttu-id="30a61-113">Yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika sonra.</span><span class="sxs-lookup"><span data-stu-id="30a61-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="30a61-114">[Hello Azure CLI yükleme](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="30a61-114">[Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="30a61-115">Kişisel bir Azure hesabı veya bir iş ile Azure CLI yüklemenizi bağlanmak veya Okul Azure hesabı ve oturum açın hello hello kullanarak Azure CLI `azure login` komutu.</span><span class="sxs-lookup"><span data-stu-id="30a61-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from hello Azure CLI using hello `azure login` command.</span></span> <span data-ttu-id="30a61-116">toounderstand Merhaba farklar ve seçin, bkz: [hello Azure komut satırı arabirimi (Azure CLI) tooan Azure aboneliğine bağlanma](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="30a61-116">toounderstand hello differences and choose, see [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="30a61-117">Komutları aşağıdaki hello birini çalıştırmadan önce hello çalıştırarak hello Azure CLI Resource Manager moduna geçin `azure config mode arm` komutu.</span><span class="sxs-lookup"><span data-stu-id="30a61-117">Before running any of hello following commands, switch hello Azure CLI into Resource Manager mode by running hello `azure config mode arm` command.</span></span> <span data-ttu-id="30a61-118">Daha fazla bilgi için bkz: [hello Azure CLI toomanage Azure kullanmak kaynaklar ve kaynak grupları](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="30a61-118">For more information, see [Use hello Azure CLI toomanage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="30a61-119">Redis önbelleği özellikleri</span><span class="sxs-lookup"><span data-stu-id="30a61-119">Redis Cache properties</span></span>
<span data-ttu-id="30a61-120">Merhaba aşağıdaki özellikleri oluşturma ve Redis önbelleği örnekleri güncelleştirme olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="30a61-120">hello following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="30a61-121">Özellik</span><span class="sxs-lookup"><span data-stu-id="30a61-121">Property</span></span> | <span data-ttu-id="30a61-122">Anahtar</span><span class="sxs-lookup"><span data-stu-id="30a61-122">Switch</span></span> | <span data-ttu-id="30a61-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="30a61-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="30a61-124">ad</span><span class="sxs-lookup"><span data-stu-id="30a61-124">name</span></span> |<span data-ttu-id="30a61-125">-n,--adı</span><span class="sxs-lookup"><span data-stu-id="30a61-125">-n, --name</span></span> |<span data-ttu-id="30a61-126">Merhaba Redis önbelleği adı.</span><span class="sxs-lookup"><span data-stu-id="30a61-126">Name of hello Redis Cache.</span></span> |
| <span data-ttu-id="30a61-127">kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="30a61-127">resource group</span></span> |<span data-ttu-id="30a61-128">-g,--kaynak-grubu</span><span class="sxs-lookup"><span data-stu-id="30a61-128">-g, --resource-group</span></span> |<span data-ttu-id="30a61-129">Merhaba kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="30a61-129">Name of hello Resource Group.</span></span> |
| <span data-ttu-id="30a61-130">location</span><span class="sxs-lookup"><span data-stu-id="30a61-130">location</span></span> |<span data-ttu-id="30a61-131">-l,--konum</span><span class="sxs-lookup"><span data-stu-id="30a61-131">-l, --location</span></span> |<span data-ttu-id="30a61-132">Konum toocreate önbelleği.</span><span class="sxs-lookup"><span data-stu-id="30a61-132">Location toocreate cache.</span></span> |
| <span data-ttu-id="30a61-133">Boyutu</span><span class="sxs-lookup"><span data-stu-id="30a61-133">size</span></span> |<span data-ttu-id="30a61-134">-z,--boyutu</span><span class="sxs-lookup"><span data-stu-id="30a61-134">-z, --size</span></span> |<span data-ttu-id="30a61-135">Merhaba Redis önbelleği boyutu.</span><span class="sxs-lookup"><span data-stu-id="30a61-135">Size of hello Redis Cache.</span></span> <span data-ttu-id="30a61-136">Geçerli değerler: [C0 C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="30a61-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="30a61-137">SKU</span><span class="sxs-lookup"><span data-stu-id="30a61-137">sku</span></span> |<span data-ttu-id="30a61-138">-x,--sku</span><span class="sxs-lookup"><span data-stu-id="30a61-138">-x, --sku</span></span> |<span data-ttu-id="30a61-139">SKU redis.</span><span class="sxs-lookup"><span data-stu-id="30a61-139">Redis SKU.</span></span> <span data-ttu-id="30a61-140">Şunlardan biri olmalıdır: [temel, standart, Premium]</span><span class="sxs-lookup"><span data-stu-id="30a61-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="30a61-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="30a61-141">EnableNonSslPort</span></span> |<span data-ttu-id="30a61-142">-e,--enable-olmayan-ssl-bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="30a61-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="30a61-143">Merhaba Redis önbelleği EnableNonSslPort özelliği.</span><span class="sxs-lookup"><span data-stu-id="30a61-143">EnableNonSslPort property of hello Redis Cache.</span></span> <span data-ttu-id="30a61-144">Bu bayrak önbelleğiniz için tooenable hello olmayan SSL bağlantı noktası istiyorsanız ekleyin</span><span class="sxs-lookup"><span data-stu-id="30a61-144">Add this flag if you want tooenable hello Non SSL Port for your cache</span></span> |
| <span data-ttu-id="30a61-145">Yapılandırma redis</span><span class="sxs-lookup"><span data-stu-id="30a61-145">Redis Configuration</span></span> |<span data-ttu-id="30a61-146">-c,--redis-yapılandırma</span><span class="sxs-lookup"><span data-stu-id="30a61-146">-c, --redis-configuration</span></span> |<span data-ttu-id="30a61-147">Yapılandırma redis.</span><span class="sxs-lookup"><span data-stu-id="30a61-147">Redis Configuration.</span></span> <span data-ttu-id="30a61-148">Yapılandırma anahtarları ve değerleri burada biçimlendirilmiş JSON dizesi girin.</span><span class="sxs-lookup"><span data-stu-id="30a61-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="30a61-149">Biçim: "{" ":""," ":" "}"</span><span class="sxs-lookup"><span data-stu-id="30a61-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="30a61-150">Yapılandırma redis</span><span class="sxs-lookup"><span data-stu-id="30a61-150">Redis Configuration</span></span> |<span data-ttu-id="30a61-151">-f,--redis yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="30a61-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="30a61-152">Yapılandırma redis.</span><span class="sxs-lookup"><span data-stu-id="30a61-152">Redis Configuration.</span></span> <span data-ttu-id="30a61-153">Yapılandırma anahtarları ve değerleri burada içeren bir dosyayı Hello yolunu girin.</span><span class="sxs-lookup"><span data-stu-id="30a61-153">Enter hello path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="30a61-154">Merhaba dosyası girişi için biçimi: {"": "","": ""}</span><span class="sxs-lookup"><span data-stu-id="30a61-154">Format for hello file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="30a61-155">Parça sayısı</span><span class="sxs-lookup"><span data-stu-id="30a61-155">Shard Count</span></span> |<span data-ttu-id="30a61-156">-r,--parça sayısı</span><span class="sxs-lookup"><span data-stu-id="30a61-156">-r, --shard-count</span></span> |<span data-ttu-id="30a61-157">Kümeleme ile Premium küme önbellekteki parça toocreate sayısı.</span><span class="sxs-lookup"><span data-stu-id="30a61-157">Number of Shards toocreate on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="30a61-158">Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="30a61-158">Virtual Network</span></span> |<span data-ttu-id="30a61-159">-v,--sanal ağ</span><span class="sxs-lookup"><span data-stu-id="30a61-159">-v, --virtual-network</span></span> |<span data-ttu-id="30a61-160">Önbelleğiniz bir VNET içindeki barındırma belirttiğinde hello tam ARM kaynak Kimliğini hello sanal ağ toodeploy hello redis Önbelleği'nde.</span><span class="sxs-lookup"><span data-stu-id="30a61-160">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="30a61-161">Örnek Biçim: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="30a61-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="30a61-162">Anahtar türü</span><span class="sxs-lookup"><span data-stu-id="30a61-162">key type</span></span> |<span data-ttu-id="30a61-163">-t,--anahtar türü</span><span class="sxs-lookup"><span data-stu-id="30a61-163">-t, --key-type</span></span> |<span data-ttu-id="30a61-164">Anahtar toorenew türü.</span><span class="sxs-lookup"><span data-stu-id="30a61-164">Type of key toorenew.</span></span> <span data-ttu-id="30a61-165">Geçerli değerler: [birincil, ikincil]</span><span class="sxs-lookup"><span data-stu-id="30a61-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="30a61-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="30a61-166">StaticIP</span></span> |<span data-ttu-id="30a61-167">-p,--statik IP < statik IP ></span><span class="sxs-lookup"><span data-stu-id="30a61-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="30a61-168">Önbelleğinizi bir VNET içindeki barındırdığında hello alt hello önbelleği için benzersiz bir IP adresi belirtir.</span><span class="sxs-lookup"><span data-stu-id="30a61-168">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="30a61-169">Sağlanmazsa, bir sizin için hello alt ağdan seçilir.</span><span class="sxs-lookup"><span data-stu-id="30a61-169">If not provided, one is chosen for you from hello subnet.</span></span> |
| <span data-ttu-id="30a61-170">Alt ağ</span><span class="sxs-lookup"><span data-stu-id="30a61-170">Subnet</span></span> |<span data-ttu-id="30a61-171">t,--alt ağ<subnet></span><span class="sxs-lookup"><span data-stu-id="30a61-171">t, --subnet <subnet></span></span> |<span data-ttu-id="30a61-172">Önbelleğiniz bir VNET içindeki barındırdığında hangi toodeploy hello Önbelleği'nde hello alt hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="30a61-172">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> |
| <span data-ttu-id="30a61-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="30a61-173">VirtualNetwork</span></span> |<span data-ttu-id="30a61-174">-v,--sanal ağ < sanal ağ ></span><span class="sxs-lookup"><span data-stu-id="30a61-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="30a61-175">Önbelleğiniz bir VNET içindeki barındırma belirttiğinde hello tam ARM kaynak Kimliğini hello sanal ağ toodeploy hello redis Önbelleği'nde.</span><span class="sxs-lookup"><span data-stu-id="30a61-175">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="30a61-176">Örnek Biçim: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="30a61-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="30a61-177">Abonelik</span><span class="sxs-lookup"><span data-stu-id="30a61-177">Subscription</span></span> |<span data-ttu-id="30a61-178">-s,--abonelik</span><span class="sxs-lookup"><span data-stu-id="30a61-178">-s, --subscription</span></span> |<span data-ttu-id="30a61-179">Merhaba abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="30a61-179">hello subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="30a61-180">Tüm Redis önbelleği komutları bakın</span><span class="sxs-lookup"><span data-stu-id="30a61-180">See all Redis Cache commands</span></span>
<span data-ttu-id="30a61-181">toosee tüm Redis önbelleği komutları ve bunların parametrelerini kullanmak hello `azure rediscache -h` komutu.</span><span class="sxs-lookup"><span data-stu-id="30a61-181">toosee all Redis Cache commands and their parameters, use hello `azure rediscache -h` command.</span></span>

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

## <a name="create-a-redis-cache"></a><span data-ttu-id="30a61-182">Redis Cache oluşturma</span><span class="sxs-lookup"><span data-stu-id="30a61-182">Create a Redis Cache</span></span>
<span data-ttu-id="30a61-183">toocreate bir Redis önbelleği hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="30a61-183">toocreate a Redis Cache, use hello following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="30a61-184">Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache create -h` komutu.</span><span class="sxs-lookup"><span data-stu-id="30a61-184">For more information about this command, run hello `azure rediscache create -h` command.</span></span>

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

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="30a61-185">Varolan bir Redis önbelleği Sil</span><span class="sxs-lookup"><span data-stu-id="30a61-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="30a61-186">toodelete bir Redis önbelleği hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="30a61-186">toodelete a Redis Cache, use hello following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="30a61-187">Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache delete -h` komutu.</span><span class="sxs-lookup"><span data-stu-id="30a61-187">For more information about this command, run hello `azure rediscache delete -h` command.</span></span>

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

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="30a61-188">Abonelik veya kaynak grubu içindeki tüm Redis önbellekleri listesi</span><span class="sxs-lookup"><span data-stu-id="30a61-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="30a61-189">Abonelik veya kaynak grubu içindeki tüm Redis önbellekleri toolist kullanmak hello komutu:</span><span class="sxs-lookup"><span data-stu-id="30a61-189">toolist all Redis Caches within your Subscription or Resource Group, use hello following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="30a61-190">Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache list -h` komutu.</span><span class="sxs-lookup"><span data-stu-id="30a61-190">For more information about this command, run hello `azure rediscache list -h` command.</span></span>

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

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="30a61-191">Varolan bir Redis önbelleği özelliklerini göster</span><span class="sxs-lookup"><span data-stu-id="30a61-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="30a61-192">bir varolan Redis önbelleği, tooshow özelliklerini hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="30a61-192">tooshow properties of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="30a61-193">Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache show -h` komutu.</span><span class="sxs-lookup"><span data-stu-id="30a61-193">For more information about this command, run hello `azure rediscache show -h` command.</span></span>

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

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="30a61-194">Varolan bir Redis önbelleği ayarlarını değiştir</span><span class="sxs-lookup"><span data-stu-id="30a61-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="30a61-195">toochange ayarlarını bir varolan Redis önbelleği, komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="30a61-195">toochange settings of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="30a61-196">Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache set -h` komutu.</span><span class="sxs-lookup"><span data-stu-id="30a61-196">For more information about this command, run hello `azure rediscache set -h` command.</span></span>

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

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="30a61-197">Varolan bir Redis önbelleği için Hello kimlik doğrulama anahtarı yenileme</span><span class="sxs-lookup"><span data-stu-id="30a61-197">Renew hello authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="30a61-198">bir varolan Redis önbelleği için komutu aşağıdaki kullanım hello toorenew hello kimlik doğrulama anahtarı:</span><span class="sxs-lookup"><span data-stu-id="30a61-198">toorenew hello authentication key for an existing Redis Cache, use hello following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="30a61-199">Belirtin `Primary` veya `Secondary` için `key-type`.</span><span class="sxs-lookup"><span data-stu-id="30a61-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="30a61-200">Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache renew-key -h` komutu.</span><span class="sxs-lookup"><span data-stu-id="30a61-200">For more information about this command, run hello `azure rediscache renew-key -h` command.</span></span>

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

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="30a61-201">Varolan bir Redis önbelleği listesi birincil ve ikincil anahtarları</span><span class="sxs-lookup"><span data-stu-id="30a61-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="30a61-202">bir varolan Redis önbelleği, toolist birincil ve ikincil anahtarları hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="30a61-202">toolist Primary and Secondary keys of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="30a61-203">Bu komut hakkında daha fazla bilgi için hello çalıştırmak `azure rediscache list-keys -h` komutu.</span><span class="sxs-lookup"><span data-stu-id="30a61-203">For more information about this command, run hello `azure rediscache list-keys -h` command.</span></span>

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
