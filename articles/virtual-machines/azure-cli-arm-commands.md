---
title: "aaaAzure CLI komutları Kaynak Yöneticisi modunda | Microsoft Docs"
description: "Azure komut satırı arabirimi (CLI) toomanage kaynakları hello Resource Manager dağıtım modelinde komutları"
services: virtual-machines-linux,virtual-machines-windows,virtual-network,mobile-services,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: be37da5b-72fe-41a1-9fa0-8937b69464ec
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: danlep
ms.openlocfilehash: 49539655f7b24511e219f982819bcb59c9305d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-commands-in-resource-manager-mode"></a><span data-ttu-id="5c418-103">Kaynak Yöneticisi modunda Azure CLI komutları</span><span class="sxs-lookup"><span data-stu-id="5c418-103">Azure CLI commands in Resource Manager mode</span></span>
<span data-ttu-id="5c418-104">Seçenekler, genellikle yaptığınız Azure komut satırı arabirimi (CLI) komutları için toocreate kullanın ve hello Azure Resource Manager dağıtım modelinde Azure kaynaklarınızı yönetmek ve bu makalede sözdizimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c418-104">This article provides syntax and options for Azure command-line interface (CLI) commands you'd commonly use toocreate and manage Azure resources in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="5c418-105">Bu komutlar, Resource Manager (arm) modunda hello CLI çalıştırarak erişin.</span><span class="sxs-lookup"><span data-stu-id="5c418-105">You access these commands by running hello CLI in Resource Manager (arm) mode.</span></span> <span data-ttu-id="5c418-106">Bu tam bir başvuru değildir ve CLI Sürüm biraz farklı komutları ya da parametreleri gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="5c418-106">This is not a complete reference, and your CLI version may show slightly different commands or parameters.</span></span> <span data-ttu-id="5c418-107">Azure kaynakları ve kaynak gruplarını genel bir bakış için bkz: [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c418-107">For a general overview of Azure resources and resource groups, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="5c418-108">Bu makalede Resource Manager modunu komutları hello Azure CLI gösterilmektedir bazen Azure CLI 1.0 çağrılır.</span><span class="sxs-lookup"><span data-stu-id="5c418-108">This article shows Resource Manager mode commands in hello Azure CLI, sometimes called Azure CLI 1.0.</span></span> <span data-ttu-id="5c418-109">toowork hello Resource Manager modelinde hello de deneyebilirsiniz [Azure CLI 2.0](/cli/azure/install-az-cli2), bizim İleri nesil birden çok platform CLI.</span><span class="sxs-lookup"><span data-stu-id="5c418-109">toowork in hello Resource Manager model, you can also try hello [Azure CLI 2.0](/cli/azure/install-az-cli2), our next generation multi-platform CLI.</span></span>
><span data-ttu-id="5c418-110">Merhaba hakkında daha fazla bilgi [eski ve yeni Azure CLIs](/cli/azure/old-and-new-clis).</span><span class="sxs-lookup"><span data-stu-id="5c418-110">Find out more about hello [old and new Azure CLIs](/cli/azure/old-and-new-clis).</span></span>
>

<span data-ttu-id="5c418-111">tooget başlatıldı, ilk [hello Azure CLI yükleme](../cli-install-nodejs.md) ve [tooyour Azure aboneliğine bağlanma](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="5c418-111">tooget started, first [install hello Azure CLI](../cli-install-nodejs.md) and [connect tooyour Azure subscription](../xplat-cli-connect.md).</span></span>

<span data-ttu-id="5c418-112">Geçerli komut söz dizimi ve Kaynak Yöneticisi modunda hello komut satırı seçenekleri için yazın `azure help` veya, belirli bir komutla ilgili Yardım toodisplay `azure help [command]`.</span><span class="sxs-lookup"><span data-stu-id="5c418-112">For current command syntax and options at hello command line in Resource Manager mode, type `azure help` or, toodisplay help for a specific command, `azure help [command]`.</span></span> <span data-ttu-id="5c418-113">Ayrıca CLI örnekleri oluşturma ve belirli Azure hizmetleri yönetmek için hello belgelerinde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c418-113">Also find CLI examples in hello documentation for creating and managing specific Azure services.</span></span>

<span data-ttu-id="5c418-114">İsteğe bağlı parametreler köşeli ayraç içinde gösterilir (örneğin, `[parameter]`).</span><span class="sxs-lookup"><span data-stu-id="5c418-114">Optional parameters are shown in square brackets (for example, `[parameter]`).</span></span> <span data-ttu-id="5c418-115">Diğer tüm parametreleri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5c418-115">All other parameters are required.</span></span>

<span data-ttu-id="5c418-116">Belgelenen toplama toocommand özgü isteğe bağlı parametreler, bunlar kullanılan toodisplay olabilir üç isteğe bağlı parametreler ayrıntılı çıktı isteği seçeneklerini ve durum kodları gibi.</span><span class="sxs-lookup"><span data-stu-id="5c418-116">In addition toocommand-specific optional parameters documented here, there are three optional parameters that can be used toodisplay detailed output such as request options and status codes.</span></span> <span data-ttu-id="5c418-117">Merhaba `-v` parametresi sağlar ayrıntılı çıktı ve hello `-vv` parametresi sağlar bile daha ayrıntılı ayrıntılı çıktı.</span><span class="sxs-lookup"><span data-stu-id="5c418-117">hello `-v` parameter provides verbose output, and hello `-vv` parameter provides even more detailed verbose output.</span></span> <span data-ttu-id="5c418-118">Merhaba `--json` seçeneği ham json biçiminde hello sonuç çıkarır.</span><span class="sxs-lookup"><span data-stu-id="5c418-118">hello `--json` option outputs hello result in raw json format.</span></span>

## <a name="setting-hello-resource-manager-mode"></a><span data-ttu-id="5c418-119">Merhaba Resource Manager modunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="5c418-119">Setting hello Resource Manager mode</span></span>
<span data-ttu-id="5c418-120">Komut tooenable Azure CLI Resource Manager modunu komutlarını aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="5c418-120">Use hello following command tooenable Azure CLI Resource Manager mode commands.</span></span>

    azure config mode arm

> [!NOTE]
> <span data-ttu-id="5c418-121">Merhaba CLI Azure Resource Manager moduna ve Azure hizmet yönetimi modu karşılıklı olarak birbirini dışlar.</span><span class="sxs-lookup"><span data-stu-id="5c418-121">hello CLI's Azure Resource Manager mode and Azure Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="5c418-122">Diğer bir deyişle, bir modunda oluşturulan kaynakları hello yönetilemez diğer modu.</span><span class="sxs-lookup"><span data-stu-id="5c418-122">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
> 
> 

## <a name="azure-account-manage-your-account-information"></a><span data-ttu-id="5c418-123">Azure hesabı: hesap bilgilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="5c418-123">azure account: Manage your account information</span></span>
<span data-ttu-id="5c418-124">Azure abonelik bilgilerinizi hello aracı tooconnect tooyour hesabı tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5c418-124">Your Azure subscription information is used by hello tool tooconnect tooyour account.</span></span>

<span data-ttu-id="5c418-125">**İçeri aktarılan hello abonelikleri listeler**</span><span class="sxs-lookup"><span data-stu-id="5c418-125">**List hello imported subscriptions**</span></span>

    account list [options]

<span data-ttu-id="5c418-126">**Bir aboneliği hakkında ayrıntıları göster**</span><span class="sxs-lookup"><span data-stu-id="5c418-126">**Show details about a subscription**</span></span>  

    account show [options] [subscriptionNameOrId]

<span data-ttu-id="5c418-127">**Merhaba geçerli abonelik ayarlayın**</span><span class="sxs-lookup"><span data-stu-id="5c418-127">**Set hello current subscription**</span></span>

    account set [options] <subscriptionNameOrId>

<span data-ttu-id="5c418-128">**Bir abonelik veya ortam kaldırmak veya tüm depolanan hello hesabı ve ortam bilgilerini temizleyin**</span><span class="sxs-lookup"><span data-stu-id="5c418-128">**Remove a subscription or environment, or clear all of hello stored account and environment info**</span></span>  

    account clear [options]

<span data-ttu-id="5c418-129">**Hesap ortamınızı toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-129">**Commands toomanage your account environment**</span></span>  

    account env list [options]
    account env show [options] [environment]
    account env add [options] [environment]
    account env set [options] [environment]
    account env delete [options] [environment]

## <a name="azure-ad-commands-toodisplay-active-directory-objects"></a><span data-ttu-id="5c418-130">Azure ad: komutları toodisplay Active Directory nesneleri</span><span class="sxs-lookup"><span data-stu-id="5c418-130">azure ad: Commands toodisplay Active Directory objects</span></span>
<span data-ttu-id="5c418-131">**Komutları toodisplay active directory uygulamaları**</span><span class="sxs-lookup"><span data-stu-id="5c418-131">**Commands toodisplay active directory applications**</span></span>

    ad app create [options]
    ad app delete [options] <object-id>

<span data-ttu-id="5c418-132">**Komutları toodisplay active directory grupları**</span><span class="sxs-lookup"><span data-stu-id="5c418-132">**Commands toodisplay active directory groups**</span></span>

    ad group list [options]
    ad group show [options]

<span data-ttu-id="5c418-133">**Bir active directory alt grubu veya üye bilgisi tooprovide komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-133">**Commands tooprovide an active directory sub group or member info**</span></span>

    ad group member list [options] [objectId]

<span data-ttu-id="5c418-134">**Komutları toodisplay active directory hizmet asıl adı**</span><span class="sxs-lookup"><span data-stu-id="5c418-134">**Commands toodisplay active directory service principals**</span></span>

    ad sp list [options]
    ad sp show [options]
    ad sp create [options] <application-id>
    ad sp delete [options] <object-id>

<span data-ttu-id="5c418-135">**Komutları toodisplay active directory kullanıcıları**</span><span class="sxs-lookup"><span data-stu-id="5c418-135">**Commands toodisplay active directory users**</span></span>

    ad user list [options]
    ad user show [options]

## <a name="azure-availset-commands-toomanage-your-availability-sets"></a><span data-ttu-id="5c418-136">Azure availset: komutları toomanage, kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="5c418-136">azure availset: commands toomanage your availability sets</span></span>
<span data-ttu-id="5c418-137">**Kullanılabilirlik bir kaynak grubu içindeki kümesi oluşturur**</span><span class="sxs-lookup"><span data-stu-id="5c418-137">**Creates an availability set within a resource group**</span></span>

    availset create [options] <resource-group> <name> <location> [tags]

<span data-ttu-id="5c418-138">**Bir kaynak grubu içinde kullanılabilirlik kümeleri listeleri hello**</span><span class="sxs-lookup"><span data-stu-id="5c418-138">**Lists hello availability sets within a resource group**</span></span>

    availset list [options] <resource-group>

<span data-ttu-id="5c418-139">**Bir kaynak grubu içindeki bir kullanılabilirlik alır**</span><span class="sxs-lookup"><span data-stu-id="5c418-139">**Gets one availability set within a resource group**</span></span>

    availset show [options] <resource-group> <name>

<span data-ttu-id="5c418-140">**Bir kaynak grubu içindeki bir kullanılabilirlik siler**</span><span class="sxs-lookup"><span data-stu-id="5c418-140">**Deletes one availability set within a resource group**</span></span>

    availset delete [options] <resource-group> <name>

## <a name="azure-config-commands-toomanage-your-local-settings"></a><span data-ttu-id="5c418-141">Azure config: yerel ayarlarınızı toomanage komutları</span><span class="sxs-lookup"><span data-stu-id="5c418-141">azure config: commands toomanage your local settings</span></span>
<span data-ttu-id="5c418-142">**Liste Azure CLI yapılandırma ayarları**</span><span class="sxs-lookup"><span data-stu-id="5c418-142">**List Azure CLI configuration settings**</span></span>

    config list [options]

<span data-ttu-id="5c418-143">**Bir yapılandırma ayarı Sil**</span><span class="sxs-lookup"><span data-stu-id="5c418-143">**Delete a config setting**</span></span>

    config delete [options] <name>

<span data-ttu-id="5c418-144">**Bir yapılandırma ayarı güncelleştir**</span><span class="sxs-lookup"><span data-stu-id="5c418-144">**Update a config setting**</span></span>

    config set <name> <value>

<span data-ttu-id="5c418-145">**Ayarlar hello Azure CLI moduna tooeither çalışma `arm` veya`asm`**</span><span class="sxs-lookup"><span data-stu-id="5c418-145">**Sets hello Azure CLI working mode tooeither `arm` or `asm`**</span></span>

    config mode [options] <modename>


## <a name="azure-feature-commands-toomanage-account-features"></a><span data-ttu-id="5c418-146">Azure özellik: toomanage hesabı özellikleri komutları</span><span class="sxs-lookup"><span data-stu-id="5c418-146">azure feature: commands toomanage account features</span></span>
<span data-ttu-id="5c418-147">**Aboneliğiniz için kullanılabilir tüm özellikler listesi**</span><span class="sxs-lookup"><span data-stu-id="5c418-147">**List all features available for your subscription**</span></span>

    feature list [options]

<span data-ttu-id="5c418-148">**Bir özellik gösterir**</span><span class="sxs-lookup"><span data-stu-id="5c418-148">**Shows a feature**</span></span>

    feature show [options] <providerName> <featureName>

<span data-ttu-id="5c418-149">**Bir kaynak sağlayıcısının Önizleme uygulanan bir özellik kaydeder**</span><span class="sxs-lookup"><span data-stu-id="5c418-149">**Registers a previewed feature of a resource provider**</span></span>

    feature register [options] <providerName> <featureName>

## <a name="azure-group-commands-toomanage-your-resource-groups"></a><span data-ttu-id="5c418-150">Azure Grup: kaynak gruplarınızı toomanage komutları</span><span class="sxs-lookup"><span data-stu-id="5c418-150">azure group: Commands toomanage your resource groups</span></span>
<span data-ttu-id="5c418-151">**Bir kaynak grubu oluşturur**</span><span class="sxs-lookup"><span data-stu-id="5c418-151">**Creates a resource group**</span></span>

    group create [options] <name> <location>

<span data-ttu-id="5c418-152">**Etiketler tooa kaynak grubunu Ayarla**</span><span class="sxs-lookup"><span data-stu-id="5c418-152">**Set tags tooa resource group**</span></span>

    group set [options] <name> <tags>

<span data-ttu-id="5c418-153">**Bir kaynak grubu siler**</span><span class="sxs-lookup"><span data-stu-id="5c418-153">**Deletes a resource group**</span></span>

    group delete [options] <name>

<span data-ttu-id="5c418-154">**Aboneliğiniz için Hello kaynak gruplarını listeler**</span><span class="sxs-lookup"><span data-stu-id="5c418-154">**Lists hello resource groups for your subscription**</span></span>

    group list [options]

<span data-ttu-id="5c418-155">**Aboneliğiniz için bir kaynak grubu gösterir**</span><span class="sxs-lookup"><span data-stu-id="5c418-155">**Shows a resource group for your subscription**</span></span>

    group show [options] <name>

<span data-ttu-id="5c418-156">**Komutları toomanage kaynak grubu günlükleri**</span><span class="sxs-lookup"><span data-stu-id="5c418-156">**Commands toomanage resource group logs**</span></span>

    group log show [options] [name]

<span data-ttu-id="5c418-157">**Bir kaynak grubu dağıtımınızda toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-157">**Commands toomanage your deployment in a resource group**</span></span>

    group deployment create [options] [resource-group] [name]
    group deployment list [options] <resource-group> [state]
    group deployment show [options] <resource-group> [deployment-name]
    group deployment stop [options] <resource-group> [deployment-name]

<span data-ttu-id="5c418-158">**Yerel veya galeri kaynak grubu şablonunuz toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-158">**Commands toomanage your local or gallery resource group template**</span></span>

    group template list [options]
    group template show [options] <name>
    group template download [options] [name] [file]
    group template validate [options] <resource-group>

## <a name="azure-hdinsight-commands-toomanage-your-hdinsight-clusters"></a><span data-ttu-id="5c418-159">Azure hdınsight: Hdınsight kümelerinizi toomanage komutları</span><span class="sxs-lookup"><span data-stu-id="5c418-159">azure hdinsight: Commands toomanage your HDInsight clusters</span></span>
<span data-ttu-id="5c418-160">**Komutları toocreate veya tooa küme yapılandırma dosyası ekleme**</span><span class="sxs-lookup"><span data-stu-id="5c418-160">**Commands toocreate or add tooa cluster configuration file**</span></span>

    hdinsight config create [options] <configFilePath> <overwrite>
    hdinsight config add-config-values [options] <configFilePath>
    hdinsight config add-script-action [options] <configFilePath>

<span data-ttu-id="5c418-161">Örnek: bir küme oluştururken, bir komut dosyası eylemi toorun içeren bir yapılandırma dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c418-161">Example: Create a configuration file that contains a script action toorun when creating a cluster.</span></span>

    hdinsight config create "C:\myFiles\configFile.config"
    hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <scriptActionURI> --name myScriptAction --parameters "-param value"

<span data-ttu-id="5c418-162">**Bir kaynak grubu bir kümede toocreate komutu**</span><span class="sxs-lookup"><span data-stu-id="5c418-162">**Command toocreate a cluster in a resource group**</span></span>

    hdinsight cluster create [options] <clusterName>

<span data-ttu-id="5c418-163">Örnek: Linux kümesinde bir Storm oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c418-163">Example: Create a Storm on Linux cluster</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Storm --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="5c418-164">Örnek: bir betik eylemi ile bir küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c418-164">Example: Create a cluster with a script action</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Hadoop --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 –configurationPath "C:\myFiles\configFile.config" myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="5c418-165">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-165">Parameter options:</span></span>

    -h, --help                                                 output usage information
    -v, --verbose                                              use verbose output
    -vv                                                        more verbose with debug output
    --json                                                     use json output
    -g --resource-group <resource-group>                       hello name of hello resource group
    -c, --clusterName <clusterName>                            HDInsight cluster name
    -l, --location <location>                                  Data center location for hello cluster
    -y, --osType <osType>                                      HDInsight cluster operating system
    'Windows' or 'Linux'
    --version <version>                                        HDInsight cluster version
    --clusterType <clusterType>                                HDInsight cluster type.
    Hadoop | HBase | Spark | Storm
    --defaultStorageAccountName <storageAccountName>           Storage account url toouse for default HDInsight storage
    --defaultStorageAccountKey <storageAccountKey>             Key toohello storage account toouse for default HDInsight storage
    --defaultStorageContainer <storageContainer>               Container in hello storage account toouse for HDInsight default storage
    --headNodeSize <headNodeSize>                              (Optional) Head node size for hello cluster
    --workerNodeCount <workerNodeCount>                        Number of worker nodes toouse for hello cluster
    --workerNodeSize <workerNodeSize>                          (Optional) Worker node size for hello cluster)
    --zookeeperNodeSize <zookeeperNodeSize>                    (Optional) Zookeeper node size for hello cluster
    --userName <userName>                                      Cluster username
    --password <password>                                      Cluster password
    --sshUserName <sshUserName>                                SSH username (only for Linux clusters)
    --sshPassword <sshPassword>                                SSH password (only for Linux clusters)
    --sshPublicKey <sshPublicKey>                              SSH public key (only for Linux clusters)
    --rdpUserName <rdpUserName>                                RDP username (only for Windows clusters)
    --rdpPassword <rdpPassword>                                RDP password (only for Windows clusters)
    --rdpAccessExpiry <rdpAccessExpiry>                        RDP access expiry.
    For example 12/12/2015 (only for Windows clusters)
    --virtualNetworkId <virtualNetworkId>                      (Optional) Virtual network ID for hello cluster.
    Value is a GUID for Windows cluster and ARM resource ID for Linux cluster)
    --subnetName <subnetName>                                  (Optional) Subnet for hello cluster
    --additionalStorageAccounts <additionalStorageAccounts>    (Optional) Additional storage accounts.
    Can be multiple.
    In hello format of 'accountName#accountKey'.
    For example, --additionalStorageAccounts "acc1#key1;acc2#key2"
    --hiveMetastoreServerName <hiveMetastoreServerName>        (Optional) SQL Server name for hello external metastore for Hive
    --hiveMetastoreDatabaseName <hiveMetastoreDatabaseName>    (Optional) Database name for hello external metastore for Hive
    --hiveMetastoreUserName <hiveMetastoreUserName>            (Optional) Database username for hello external metastore for Hive
    --hiveMetastorePassword <hiveMetastorePassword>            (Optional) Database password for hello external metastore for Hive
    --oozieMetastoreServerName <oozieMetastoreServerName>      (Optional) SQL Server name for hello external metastore for Oozie
    --oozieMetastoreDatabaseName <oozieMetastoreDatabaseName>  (Optional) Database name for hello external metastore for Oozie
    --oozieMetastoreUserName <oozieMetastoreUserName>          (Optional) Database username for hello external metastore for Oozie
    --oozieMetastorePassword <oozieMetastorePassword>          (Optional) Database password for hello external metastore for Oozie
    --configurationPath <configurationPath>                    (Optional) HDInsight cluster configuration file path
    -s, --subscription <id>                                    hello subscription id
    --tags <tags>                                              Tags tooset toohello cluster.
    Can be multiple.
    In hello format of 'name=value'.
    Name is required and value is optional.
    For example, --tags tag1=value1;tag2


<span data-ttu-id="5c418-166">**Bir küme toodelete komutu**</span><span class="sxs-lookup"><span data-stu-id="5c418-166">**Command toodelete a cluster**</span></span>

    hdinsight cluster delete [options] <clusterName>

<span data-ttu-id="5c418-167">**Komut tooshow küme ayrıntıları**</span><span class="sxs-lookup"><span data-stu-id="5c418-167">**Command tooshow cluster details**</span></span>

    hdinsight cluster show [options] <clusterName>

<span data-ttu-id="5c418-168">**Tüm komut toolist (sağladıysanız bir belirli bir kaynak grubunda) kümeleri**</span><span class="sxs-lookup"><span data-stu-id="5c418-168">**Command toolist all clusters (in a specific resource group, if provided)**</span></span>

    hdinsight cluster list [options]

<span data-ttu-id="5c418-169">**Bir küme tooresize komutu**</span><span class="sxs-lookup"><span data-stu-id="5c418-169">**Command tooresize a cluster**</span></span>

    hdinsight cluster resize [options] <clusterName> <targetInstanceCount>

<span data-ttu-id="5c418-170">**Bir küme için tooenable HTTP erişimi komutu**</span><span class="sxs-lookup"><span data-stu-id="5c418-170">**Command tooenable HTTP access for a cluster**</span></span>

    hdinsight cluster enable-http-access [options] <clusterName> <userName> <password>

<span data-ttu-id="5c418-171">**Bir küme için toodisable HTTP erişimi komutu**</span><span class="sxs-lookup"><span data-stu-id="5c418-171">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-http-access [options] <clusterName>

<span data-ttu-id="5c418-172">**Bir küme için komut tooenable RDP erişim**</span><span class="sxs-lookup"><span data-stu-id="5c418-172">**Command tooenable RDP access for a cluster**</span></span>

    hdinsight cluster enable-rdp-access [options] <clusterName> <rdpUserName> <rdpPassword> <rdpExpiryDate>

<span data-ttu-id="5c418-173">**Bir küme için toodisable HTTP erişimi komutu**</span><span class="sxs-lookup"><span data-stu-id="5c418-173">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-rdp-access [options] <clusterName>

## <a name="azure-insights-commands-related-toomonitoring-insights-events-alert-rules-autoscale-settings-metrics"></a><span data-ttu-id="5c418-174">Azure Öngörüler: komutları ilgili toomonitoring Öngörüler (olaylar, uyarı kuralları, otomatik ölçeklendirme ayarları, ölçümleri)</span><span class="sxs-lookup"><span data-stu-id="5c418-174">azure insights: Commands related toomonitoring Insights (events, alert rules, autoscale settings, metrics)</span></span>
<span data-ttu-id="5c418-175">**Abonelik, bir correlationıd değeri, bir kaynak grubu, kaynak veya kaynak sağlayıcısı için işlem günlüklerini alma**</span><span class="sxs-lookup"><span data-stu-id="5c418-175">**Retrieve operation logs for a subscription, a correlationId, a resource group, resource, or resource provider**</span></span>

    insights logs list [options]

## <a name="azure-location-commands-tooget-hello-available-locations-for-all-resource-types"></a><span data-ttu-id="5c418-176">Azure konumu: komutları tooget hello tüm kaynak türleri için kullanılabilir konumları</span><span class="sxs-lookup"><span data-stu-id="5c418-176">azure location: Commands tooget hello available locations for all resource types</span></span>
<span data-ttu-id="5c418-177">**Liste hello kullanılabilir konumları**</span><span class="sxs-lookup"><span data-stu-id="5c418-177">**List hello available locations**</span></span>

    location list [options]

## <a name="azure-network-commands-toomanage-network-resources"></a><span data-ttu-id="5c418-178">Azure ağı: komutları toomanage ağ kaynakları</span><span class="sxs-lookup"><span data-stu-id="5c418-178">azure network: Commands toomanage network resources</span></span>
<span data-ttu-id="5c418-179">**Komutları toomanage sanal ağlar**</span><span class="sxs-lookup"><span data-stu-id="5c418-179">**Commands toomanage virtual networks**</span></span>

    network vnet create [options] <resource-group> <name> <location>
<span data-ttu-id="5c418-180">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5c418-180">Creates a virtual network.</span></span> <span data-ttu-id="5c418-181">Hello bir sanal ağ oluşturuyoruz aşağıdaki örnekte kaynak grubu myresourcegroup hello Batı ABD bölgesindeki newvnet adlı.</span><span class="sxs-lookup"><span data-stu-id="5c418-181">In hello following example we create a virtual network named newvnet for resource group myresourcegroup in hello West US region.</span></span>

    azure network vnet create myresourcegroup newvnet "west us"
    info:    Executing command network vnet create
    + Looking up virtual network "newvnet"
    + Creating virtual network "newvnet"
     Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet create command OK


<span data-ttu-id="5c418-182">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-182">Parameter options:</span></span>

     -h, --help                                 output usage information
     -v, --verbose                              use verbose output
    --json                                     use json output
     -g, --resource-group <resource-group>      hello name of hello resource group
     -n, --name <name>                          hello name of hello virtual network
     -l, --location <location>                  hello location
     -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network
      For example -a 10.0.0.0/24,10.0.1.0/24.
      Default value is 10.0.0.0/8

    -d, --dns-servers <dns-servers>            hello comma separated list of DNS servers IP addresses
     -t, --tags <tags>                          hello tags set on this virtual network.
      Can be multiple. In hello format of "name=value".
      Name is required and value is optional.
      For example, -t tag1=value1;tag2
     -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet set [options] <resource-group> <name>

<span data-ttu-id="5c418-183">Bir kaynak grubu içinde bir sanal ağ yapılandırmasını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5c418-183">Updates a virtual network configuration within a resource group.</span></span>

    azure network vnet set myresourcegroup newvnet

    info:    Executing command network vnet set
    + Looking up virtual network "newvnet"
    + Updating virtual network "newvnet"
    + Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet set command OK

<span data-ttu-id="5c418-184">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-184">Parameter options:</span></span>

       -h, --help                                 output usage information
       -v, --verbose                              use verbose output
       --json                                     use json output
       -g, --resource-group <resource-group>      hello name of hello resource group
       -n, --name <name>                          hello name of hello virtual network
       -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network.
        For example -a 10.0.0.0/24,10.0.1.0/24.
        This list will be appended toohello current list of address prefixes.
        hello address prefixes in this list should not overlap between them.
        hello address prefixes in this list should not overlap with existing address prefixes in hello vnet.

       -d, --dns-servers [dns-servers]            hello comma separated list of DNS servers IP addresses.
        This list will be appended toohello current list of DNS server IP addresses.

       -t, --tags <tags>                          hello tags set on this virtual network.
        Can be multiple. In hello format of "name=value".
        Name is required and value is optional. For example, -t tag1=value1;tag2.
        This list will be appended toohello current list of tags

       --no-tags                                  remove all existing tags
       -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet list [options] <resource-group>

<span data-ttu-id="5c418-185">Merhaba komut bir kaynak grubundaki tüm sanal ağları listeler.</span><span class="sxs-lookup"><span data-stu-id="5c418-185">hello command lists all virtual networks in a resource group.</span></span>

    C:\>azure network vnet list myresourcegroup

    info:    Executing command network vnet list
    + Listing virtual networks
        data:    ID
       Name      Location  Address prefixes  DNS servers
    data:    -------------------------------------------------------------------
    ------  --------  --------  ----------------  -----------
    data:    /subscriptions/###############################/resourceGroups/
    wvnet   newvnet   westus    10.0.0.0/8
    info:    network vnet list command OK

<span data-ttu-id="5c418-186">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-186">Parameter options:</span></span>

      -h, --help                             output usage information
      -v, --verbose                          use verbose output
      --json                                 use json output
      -g, --resource-group <resource-group>  hello name of hello resource group
      -s, --subscription <subscription>      hello subscription identifier

<BR>

    network vnet show [options] <resource-group> <name>
<span data-ttu-id="5c418-187">Merhaba komut bir kaynak grubunda hello sanal ağ özellikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="5c418-187">hello command shows hello virtual network properties in a resource group.</span></span>

    azure network vnet show -g myresourcegroup -n newvnet

    info:    Executing command network vnet show
    + Looking up virtual network "newvnet"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet show command OK
<BR>

    network vnet delete [options] <resource-group> <name>
<span data-ttu-id="5c418-188">Merhaba komutu, bir sanal ağ kaldırır.</span><span class="sxs-lookup"><span data-stu-id="5c418-188">hello command removes a virtual network.</span></span>

    azure network vnet delete myresourcegroup newvnetX

    info:    Executing command network vnet delete
    + Looking up virtual network "newvnetX"
    Delete virtual network newvnetX? [y/n] y
    + Deleting virtual network "newvnetX"
    info:    network vnet delete command OK

<span data-ttu-id="5c418-189">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-189">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello virtual network
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="5c418-190">**Komutları toomanage sanal ağ alt ağları**</span><span class="sxs-lookup"><span data-stu-id="5c418-190">**Commands toomanage virtual network subnets**</span></span>

    network vnet subnet create [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="5c418-191">Başka bir alt tooan varolan sanal ağ ekler.</span><span class="sxs-lookup"><span data-stu-id="5c418-191">Adds another subnet tooan existing virtual network.</span></span>

    azure network vnet subnet create -g myresourcegroup --vnet-name newvnet -n subnet --address-prefix 10.0.1.0/24

    info:    Executing command network vnet subnet create
    + Looking up hello subnet "subnet"
    + Creating subnet "subnet"
    + Looking up hello subnet "subnet"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Name:                      subnet
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet create command OK

<span data-ttu-id="5c418-192">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-192">Parameter options:</span></span>

     -h, --help                                                       output usage information
     -v, --verbose                                                    use verbose output
         --json                                                           use json output
     -g, --resource-group <resource-group>                            hello name of hello resource group
     -e, --vnet-name <vnet-name>                                      hello name of hello virtual network
     -n, --name <name>                                                hello name of hello subnet
     -a, --address-prefix <address-prefix>                            hello address prefix
     -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
           e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
     -o, --network-security-group-name <network-security-group-name>  hello network security group name
     -s, --subscription <subscription>                                hello subscription identifier

<BR>

    network vnet subnet set [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="5c418-193">Bir kaynak grubu içindeki belirli bir sanal ağ alt ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5c418-193">Sets a specific virtual network subnet within a resource group.</span></span>

    C:\>azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet list [options] <resource-group> <vnet-name>

<span data-ttu-id="5c418-194">Bir kaynak grubu içindeki belirli bir sanal ağı için tüm hello sanal ağ alt ağları listeler.</span><span class="sxs-lookup"><span data-stu-id="5c418-194">Lists all hello virtual network subnets for a specific virtual network within a resource group.</span></span>

    azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet show [options] <resource-group> <vnet-name> <name>
<span data-ttu-id="5c418-195">Sanal ağ alt ağı özelliklerini görüntüler</span><span class="sxs-lookup"><span data-stu-id="5c418-195">Displays virtual network subnet properties</span></span>

    azure network vnet subnet show -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet show
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft
    .Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet show command OK

<span data-ttu-id="5c418-196">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-196">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -e, --vnet-name <vnet-name>            hello name of hello virtual network
    -n, --name <name>                      hello name of hello subnet
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network vnet subnet delete [options] <resource-group> <vnet-name> <subnet-name>
<span data-ttu-id="5c418-197">Bir alt ağ, var olan bir sanal ağdan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="5c418-197">Removes a subnet from an existing virtual network.</span></span>

    azure network vnet subnet delete -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet delete
    + Looking up hello subnet "subnet1"
    Delete subnet "subnet1"? [y/n] y
    + Deleting subnet "subnet1"
    info:    network vnet subnet delete command OK

<span data-ttu-id="5c418-198">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-198">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -e, --vnet-name <vnet-name>            hello name of hello virtual network
     -n, --name <name>                      hello subnet name
     -s, --subscription <subscription>      hello subscription identifier
     -q, --quiet                            quiet mode, do not ask for delete confirmation

<span data-ttu-id="5c418-199">**Komutları toomanage yük Dengeleyiciler**</span><span class="sxs-lookup"><span data-stu-id="5c418-199">**Commands toomanage load balancers**</span></span>

    network lb create [options] <resource-group> <name> <location>
<span data-ttu-id="5c418-200">Bir yük dengeleyici kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5c418-200">Creates a load balancer set.</span></span>

    azure network lb create -g myresourcegroup -n mylb -l westus

    info:    Executing command network lb create
    + Looking up hello load balancer "mylb"
    + Creating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb create command OK

<span data-ttu-id="5c418-201">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-201">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -l, --location <location>              hello location
    -t, --tags <tags>                      hello list of tags.
     Can be multiple. In hello format of "name=value".
     Name is required and value is optional. For example, -t tag1=value1;tag2
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb list [options] <resource-group>
<span data-ttu-id="5c418-202">Yük Dengeleyici kaynaklar bir kaynak grubu içinde listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="5c418-202">Lists Load balancer resources within a resource group.</span></span>

    azure network lb list myresourcegroup

    info:    Executing command network lb list
    + Getting hello load balancers
    data:    Name  Location
    data:    ----  --------
    data:    mylb  westus
    info:    network lb list command OK

<span data-ttu-id="5c418-203">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-203">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb show [options] <resource-group> <name>

<span data-ttu-id="5c418-204">Yük Dengeleyici bilgileri bir kaynak grubu içindeki belirli yük dengeleyicinin görüntüler</span><span class="sxs-lookup"><span data-stu-id="5c418-204">Displays load balancer information of a specific load balancer within a resource group</span></span>

    azure network lb show myresourcegroup mylb -v

    info:    Executing command network lb show
    verbose: Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb show command OK

<span data-ttu-id="5c418-205">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-205">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb delete [options] <resource-group> <name>

<span data-ttu-id="5c418-206">Yük Dengeleyici kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="5c418-206">Delete load balancer resources.</span></span>

    azure network lb delete  myresourcegroup mylb

    info:    Executing command network lb delete
    + Looking up hello load balancer "mylb"
    Delete load balancer "mylb"? [y/n] y
    + Deleting load balancer "mylb"
    info:    network lb delete command OK

<span data-ttu-id="5c418-207">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-207">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello load balancer
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="5c418-208">**Bir yük dengeleyicinin toomanage araştırmalar komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-208">**Commands toomanage probes of a load balancer**</span></span>

    network lb probe create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="5c418-209">Sistem durumu için Hello araştırma yapılandırma hello yük dengeleyicisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c418-209">Create hello probe configuration for health status in hello load balancer.</span></span> <span data-ttu-id="5c418-210">Bu komut göz toorun tutun, ön uç IP Kaynak (komut "azure ağ ön uç-IP" tooassign bir IP adresi tooload dengeleyici kullanıma), yük dengeleyici gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5c418-210">Keep in mind toorun this command, your load balancer requires a frontend-ip resource (Check out command "azure network frontend-ip" tooassign an ip address tooload balancer).</span></span>

    azure network lb probe create -g myresourcegroup --lb-name mylb -n mylbprobe --protocol tcp --port 80 -i 300

    info:    Executing command network lb probe create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe create command OK

<span data-ttu-id="5c418-211">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-211">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -p, --protocol <protocol>              hello probe protocol
    -o, --port <port>                      hello probe port
    -f, --path <path>                      hello probe path
    -i, --interval <interval>              hello probe interval in seconds
    -c, --count <count>                    hello number of probes
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb probe set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="5c418-212">Var olan bir yük dengeleyici araştırması için yeni değerleri ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5c418-212">Updates an existing load balancer probe with new values for it.</span></span>

    azure network lb probe set -g myresourcegroup -l mylb -n mylbprobe -p mylbprobe1 -p TCP -o 443 -i 300

    info:    Executing command network lb probe set
        + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe set command OK

<span data-ttu-id="5c418-213">Parametre seçenekleri</span><span class="sxs-lookup"><span data-stu-id="5c418-213">Parameter options</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -e, --new-probe-name <new-probe-name>  hello new name of hello probe
    -p, --protocol <protocol>              hello new value for probe protocol
    -o, --port <port>                      hello new value for probe port
    -f, --path <path>                      hello new value for probe path
    -i, --interval <interval>              hello new value for probe interval in seconds
    -c, --count <count>                    hello new value for number of probes
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb probe list [options] <resource-group> <lb-name>

<span data-ttu-id="5c418-214">Bir yük dengeleyici küme Hello araştırma özelliklerini listeleyin.</span><span class="sxs-lookup"><span data-stu-id="5c418-214">List hello probe properties for a load balancer set.</span></span>

    C:\>azure network lb probe list -g myresourcegroup -l mylb

    info:    Executing command network lb probe list
    + Looking up hello load balancer "mylb"
    data:    Name       Protocol  Port  Path  Interval  Count
    data:    ---------  --------  ----  ----  --------  -----
    data:    mylbprobe  Tcp       443         300       2
    info:    network lb probe list command OK

<span data-ttu-id="5c418-215">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-215">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier


    network lb probe delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="5c418-216">Merhaba yük dengeleyici için oluşturulan hello araştırma kaldırır.</span><span class="sxs-lookup"><span data-stu-id="5c418-216">Removes hello probe created for hello load balancer.</span></span>

    azure network lb probe delete -g myresourcegroup -l mylb -n mylbprobe

    info:    Executing command network lb probe delete
    + Looking up hello load balancer "mylb"
    Delete a probe "mylbprobe?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb probe delete command OK

<span data-ttu-id="5c418-217">**Komutları toomanage ön uç IP yapılandırmaları bir yük dengeleyici**</span><span class="sxs-lookup"><span data-stu-id="5c418-217">**Commands toomanage frontend ip configurations of a load balancer**</span></span>

    network lb frontend-ip create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="5c418-218">Yük Dengeleyici küme var olan bir ön uç IP yapılandırması tooan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5c418-218">Creates a frontend IP configuration tooan existing load balancer set.</span></span>

    azure network lb frontend-ip create -g myresourcegroup --lb-name mylb -n myfrontendip -o Dynamic -e subnet -m newvnet

    info:    Executing command network lb frontend-ip create
    + Looking up hello load balancer "mylb"
    + Looking up hello subnet "subnet"
    + Creating frontend IP configuration "myfrontendip"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/Myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    /frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:           10.0.1.4
    data:    Subnet:                       id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Public IP address:
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip create command OK

<BR>

    network lb frontend-ip set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="5c418-219">Güncelleştirmeleri mevcut bir ön uç aşağıdaki IP.hello komutu yapılandırmasını myfrontendip adlı mypubip5 tooan var olan yük dengeleyici ön uç IP adı verilen bir ortak IP ekler.</span><span class="sxs-lookup"><span data-stu-id="5c418-219">Updates an existing configuration of a frontend IP.hello command below adds a public IP called mypubip5 tooan existing load balancer frontend IP named myfrontendip.</span></span>

    azure network lb frontend-ip set -g myresourcegroup --lb-name mylb -n myfrontendip -i mypubip5

    info:    Executing command network lb frontend-ip set
    + Looking up hello load balancer "mylb"
    + Looking up hello public ip "mypubip5"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:
    data:    Subnet:
    data:    Public IP address:            id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mypubip5
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip set command OK

<span data-ttu-id="5c418-220">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-220">Parameter options:</span></span>

    -h, --help                                                         output usage information
    -v, --verbose                                                      use verbose output
    --json                                                             use json output
    -g, --resource-group <resource-group>                              hello name of hello resource group
    -l, --lb-name <lb-name>                                            hello name of hello load balancer
    -n, --name <name>                                                  hello name of hello frontend ip configuration
    -a, --private-ip-address <private-ip-address>                      hello private ip address
    -o, --private-ip-allocation-method <private-ip-allocation-method>  hello private ip allocation method [Static, Dynamic]
    -u, --public-ip-id <public-ip-id>                                  hello public ip identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -i, --public-ip-name <public-ip-name>                              hello public ip name.
    This public ip must exist in hello same resource group as hello lb.
    Please use public-ip-id if that is not hello case.
    -b, --subnet-id <subnet-id>                                        hello subnet id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/VirtualNetworks/<vnet-name>/subnets/<subnet-name>
    -e, --subnet-name <subnet-name>                                    hello subnet name
    -m, --vnet-name <vnet-name>                                        hello virtual network name.
    This virtual network must exist in hello same resource group as hello lb.
    Please use subnet-id if that is not hello case.
    -s, --subscription <subscription>                                  hello subscription identifier

<BR>

    network lb frontend-ip list [options] <resource-group> <lb-name>

<span data-ttu-id="5c418-221">Merhaba yük dengeleyici için yapılandırılan tüm hello ön uç IP kaynakları listeler.</span><span class="sxs-lookup"><span data-stu-id="5c418-221">Lists all hello frontend IP resources configured for hello load balancer.</span></span>

    azure network lb frontend-ip list -g myresourcegroup -l mylb

    info:    Executing command network lb frontend-ip list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Private IP allocation method  Subnet
    data:    -----------  ------------------  ----------------------------  ------
    data:    myprivateip  Succeeded           Dynamic
    info:    network lb frontend-ip list command OK

<span data-ttu-id="5c418-222">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-222">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb frontend-ip delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="5c418-223">Merhaba ön uç IP ilişkili nesne tooload dengeleyici siler</span><span class="sxs-lookup"><span data-stu-id="5c418-223">Deletes hello frontend IP object associated tooload balancer</span></span>

    network lb frontend-ip delete -g myresourcegroup -l mylb -n myfrontendip
    info:    Executing command network lb frontend-ip delete
    + Looking up hello load balancer "mylb"
    Delete frontend ip configuration "myfrontendip"? [y/n] y
    + Updating load balancer "mylb"

<span data-ttu-id="5c418-224">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-224">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello frontend ip configuration
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="5c418-225">**Bir yük dengeleyicinin toomanage arka uç adres havuzlarında komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-225">**Commands toomanage backend address pools of a load balancer**</span></span>

    network lb address-pool create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="5c418-226">Bir yük dengeleyici için bir arka uç adres havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c418-226">Create a backend address pool for a load balancer.</span></span>

    azure network lb address-pool create -g myresourcegroup --lb-name mylb -n myaddresspool

    info:    Executing command network lb address-pool create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourgroup/providers/Microso.Network/loadBalancers/mylb/backendAddressPools/myaddresspool
    data:    Name:                      myaddresspool
    data:    Type:                      Microsoft.Network/loadBalancers/backendAddressPools
    data:    Provisioning state:        Succeeded
    data:    Backend IP configurations:
    data:    Load balancing rules:
    data:
    info:    network lb address-pool create command OK

<span data-ttu-id="5c418-227">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-227">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb address-pool list [options] <resource-group> <lb-name>

<span data-ttu-id="5c418-228">Belirli bir kaynak grubunun için arka uç IP adresi havuzu aralığı listesi</span><span class="sxs-lookup"><span data-stu-id="5c418-228">List backend IP address pool range for a specific resource group</span></span>

    azure network lb address-pool list -g myresourcegroup -l mylb

    info:    Executing command network lb address-pool list
    + Looking up hello load balancer "mylb"
    data:    Name           Provisioning state
    data:    -------------  ------------------
    data:    mybackendpool  Succeeded
    info:    network lb address-pool list command OK

<span data-ttu-id="5c418-229">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-229">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -l, --lb-name <lb-name>                hello name of hello load balancer
     -s, --subscription <subscription>      hello subscription identifier

<BR>
    <span data-ttu-id="5c418-230">Ağ lb adres havuzu silme [Seçenekler] < resource-group >< lb-adı ><name></span><span class="sxs-lookup"><span data-stu-id="5c418-230">network lb address-pool delete [options] <resource-group> <lb-name> <name></span></span>

<span data-ttu-id="5c418-231">Merhaba arka uç IP havuzu aralığı kaynağı yük dengeleyiciden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="5c418-231">Removes hello backend IP pool range resource from load balancer.</span></span>

    azure network lb address-pool delete -g myresourcegroup -l mylb -n mybackendpool

    info:    Executing command network lb address-pool delete
    + Looking up hello load balancer "mylb"
    Delete backend address pool "mybackendpool"? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb address-pool delete command OK

<span data-ttu-id="5c418-232">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-232">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="5c418-233">**Toomanage yük dengeleyici kuralları komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-233">**Commands toomanage load balancer rules**</span></span>

    network lb rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="5c418-234">Yük Dengeleyici kuralları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c418-234">Create load balancer rules.</span></span>

<span data-ttu-id="5c418-235">Merhaba yük dengeleyici ve hello arka uç adres havuzu aralığı tooreceive hello gelen ağ trafiğini hello ön uç noktasının yapılandırma yük dengeleyici kuralı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c418-235">You can create a load balancer rule configuring hello frontend endpoint for hello load balancer and hello backend address pool range tooreceive hello incoming network traffic.</span></span> <span data-ttu-id="5c418-236">Ayarlar ayrıca hello ön uç IP uç noktası için ve bağlantı noktaları hello arka uç adres havuzu aralığının içerir.</span><span class="sxs-lookup"><span data-stu-id="5c418-236">Settings also include hello ports for frontend IP endpoint and ports for hello backend address pool range.</span></span>

<span data-ttu-id="5c418-237">Merhaba aşağıdaki örnekte nasıl toocreate bir yük dengeleyici kuralı, hello ön uç nokta tooport 80 dinleme gösterir TCP ve Yük Dengeleme ağ trafiğini tooport 8080 hello arka uç adres havuzu aralığının gönderme.</span><span class="sxs-lookup"><span data-stu-id="5c418-237">hello following example shows how toocreate a load balancer rule,  hello frontend endpoint listening tooport 80 TCP and load balancing network traffic sending tooport 8080 for hello backend address pool range.</span></span>

    azure network lb rule create -g myresourcegroup -l mylb -n mylbrule -p tcp -f 80 -b 8080 -i 10


    info:    Executing command network lb rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mylbrule
    data:    Name:                      mylbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule create command OK

<BR>

    network lb rule set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="5c418-238">Belirli bir kaynak grubundaki mevcut bir yük dengeleyici kuralını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5c418-238">Updates an existing load balancer rule set in a specific resource group.</span></span> <span data-ttu-id="5c418-239">Aşağıdaki örneğine hello biz mylbrule toomynewlbrule hello kural adı değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="5c418-239">In hello following example, we changed hello rule name from mylbrule toomynewlbrule.</span></span>

    azure network lb rule set -g myresourcegroup -l mylb -n mylbrule -r mynewlbrule -p tcp -f 80 -b 8080 -i 10 -t myfrontendip -o mybackendpool

    info:    Executing command network lb rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mynewlbrule
    data:    Name:                      mynewlbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule set command OK

<span data-ttu-id="5c418-240">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-240">Parameter options:</span></span>

    -h, --help                                         output usage information
    -v, --verbose                                      use verbose output
    --json                                             use json output
    -g, --resource-group <resource-group>              hello name of hello resource group
    -l, --lb-name <lb-name>                            hello name of hello load balancer
    -n, --name <name>                                  hello name of hello rule
    -r, --new-rule-name <new-rule-name>                new rule name
    -p, --protocol <protocol>                          hello rule protocol
    -f, --frontend-port <frontend-port>                hello frontend port
    -b, --backend-port <backend-port>                  hello backend port
    -e, --enable-floating-ip <enable-floating-ip>      enable floating point ip
    -i, --idle-timeout <idle-timeout>                  hello idle timeout in minutes
    -a, --probe-name [probe-name]                      hello name of hello probe defined in hello same load balancer
    -t, --frontend-ip-name <frontend-ip-name>          hello name of hello frontend ip configuration in hello same load balancer
    -o, --backend-address-pool <backend-address-pool>  name of hello backend address pool defined in hello same load balancer
    -s, --subscription <subscription>                  hello subscription identifier


    network lb rule list [options] <resource-group> <lb-name>

<span data-ttu-id="5c418-241">Yük Dengeleyici kuralları belirli bir kaynak grubunun bir yük dengeleyicisi için yapılandırılan tüm listeler.</span><span class="sxs-lookup"><span data-stu-id="5c418-241">Lists all load balancer rules configured for a load balancer in a specific resource group.</span></span>

    azure network lb rule list -g myresourcegroup -l mylb

    info:    Executing command network lb rule list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend address pool  Probe data

    data:    mynewlbrule  Succeeded           Tcp       80             8080          false               10                       /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    info:    network lb rule list command OK

<span data-ttu-id="5c418-242">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-242">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

    network lb rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="5c418-243">Yük Dengeleyici kuralı siler.</span><span class="sxs-lookup"><span data-stu-id="5c418-243">Deletes a load balancer rule.</span></span>

    azure network lb rule delete -g myresourcegroup -l mylb -n mynewlbrule

    info:    Executing command network lb rule delete
    + Looking up hello load balancer "mylb"
    Delete load balancing rule mynewlbrule? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb rule delete command OK

<span data-ttu-id="5c418-244">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-244">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="5c418-245">**Komutları toomanage yük dengeleyici gelen NAT kuralları**</span><span class="sxs-lookup"><span data-stu-id="5c418-245">**Commands toomanage load balancer inbound NAT rules**</span></span>

    network lb inbound-nat-rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="5c418-246">Yük Dengeleyici gelen NAT kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5c418-246">Creates an inbound NAT rule for load balancer.</span></span>

<span data-ttu-id="5c418-247">Hello aşağıdaki örnek bir NAT kuralı (hangi hello "azure ağ ön uç-IP" komutunu kullanarak daha önce tanımlandı) ön uç IP dinleme bağlantı noktasına gelen ve giden bağlantı noktası ile bu hello yük dengeleyici oluşturduğumuz toosend hello ağ trafiğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="5c418-247">In hello following example  we created a NAT rule from frontend IP (which was previously defined using hello "azure network frontend-ip" command) with an inbound listening port and outbound port that hello load balancer uses toosend hello network traffic.</span></span>

    azure network lb inbound-nat-rule create -g myresourcegroup -l mylb -n myinboundnat -p tcp -f 80 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              80
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule create command OK

<span data-ttu-id="5c418-248">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-248">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id <vm-id>                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.This VM must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case.
    this parameter will be ignored if --vm-id is specified
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule set [options] <resource-group> <lb-name> <name>
<span data-ttu-id="5c418-249">Mevcut bir gelen nat kuralını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5c418-249">Updates an existing inbound nat rule.</span></span> <span data-ttu-id="5c418-250">Aşağıdaki örneğine hello sabit hello değiştirdik gelen dinleme bağlantı noktası 80 too81 gelen.</span><span class="sxs-lookup"><span data-stu-id="5c418-250">In hello following example, we changed hello inbound listening port from 80 too81.</span></span>

    azure network lb inbound-nat-rule set -g group-1 -l mylb -n myinboundnat -p tcp -f 81 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              81
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule set command OK

<span data-ttu-id="5c418-251">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-251">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id [vm-id]                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.
    This virtual machine must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule list [options] <resource-group> <lb-name>

<span data-ttu-id="5c418-252">Yük Dengeleyici için tüm gelen nat kuralları listeler.</span><span class="sxs-lookup"><span data-stu-id="5c418-252">Lists all inbound nat rules for load balancer.</span></span>

    azure network lb inbound-nat-rule list -g myresourcegroup -l mylb

    info:    Executing command network lb inbound-nat-rule list
    + Looking up hello load balancer "mylb"
    data:    Name          Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend IP configuration
    data:    ------------  ------------------  --------  -------------  ------------  ------------------  -----------------------  ---
    ---------------------
    data:    myinboundnat  Succeeded           Tcp       81             8080          false               4

    info:    network lb inbound-nat-rule list command OK

<span data-ttu-id="5c418-253">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-253">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb inbound-nat-rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="5c418-254">Belirli bir kaynak grubunun hello yük dengeleyicisi NAT kuralını siler.</span><span class="sxs-lookup"><span data-stu-id="5c418-254">Deletes NAT rule for hello load balancer in a specific resource group.</span></span>

    azure network lb inbound-nat-rule delete -g myresourcegroup -l mylb -n myinboundnat

    info:    Executing command network lb inbound-nat-rule delete
    + Looking up hello load balancer "mylb"
    Delete inbound NAT rule "myinboundnat?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb inbound-nat-rule delete command OK

<span data-ttu-id="5c418-255">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-255">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello inbound NAT rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="5c418-256">**Komutları toomanage genel IP adresleri**</span><span class="sxs-lookup"><span data-stu-id="5c418-256">**Commands toomanage public ip addresses**</span></span>

    network public-ip create [options] <resource-group> <name> <location>
<span data-ttu-id="5c418-257">Genel IP kaynağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5c418-257">Creates a public ip resource.</span></span> <span data-ttu-id="5c418-258">Hello genel IP kaynağı oluşturacak ve tooa etki alanı adı ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="5c418-258">You will create hello public ip resource and associate tooa domain name.</span></span>

    azure network public-ip create -g myresourcegroup -n mytestpublicip1 -l eastus -d azureclitest -a "Dynamic"
    info:    Executing command network public-ip create
    + Looking up hello public ip "mytestpublicip1"
    + Creating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Dynamic
    data:    Idle timeout:         4
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip create command OK


<span data-ttu-id="5c418-259">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-259">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -l, --location <location>                    hello location
    -d, --domain-name-label <domain-name-label>  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn <reverse-fqdn>            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>            hello subscription identifier
<br>

    network public-ip set [options] <resource-group> <name>
<span data-ttu-id="5c418-260">Varolan bir genel IP kaynağı Hello özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5c418-260">Updates hello properties of an existing public ip resource.</span></span> <span data-ttu-id="5c418-261">Aşağıdaki örneğine hello biz dinamik tooStatic hello genel IP adresi değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="5c418-261">In hello following example we changed hello public IP address from Dynamic tooStatic.</span></span>

    azure network public-ip set -g group-1 -n mytestpublicip1 -d azureclitest -a "Static"
    info:    Executing command network public-ip set
    + Looking up hello public ip "mytestpublicip1"
    + Updating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip set command OK

<span data-ttu-id="5c418-262">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-262">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -d, --domain-name-label [domain-name-label]  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn [reverse-fqdn]            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    --no-tags                                    remove all existing tags
    -s, --subscription <subscription>            hello subscription identifier

<br>
    <span data-ttu-id="5c418-263">ağ ortak IP listesi [Seçenekler] < resource-group > bir kaynak grubu içinde bulunan tüm genel IP kaynakları listeler.</span><span class="sxs-lookup"><span data-stu-id="5c418-263">network public-ip list [options] <resource-group> Lists all public IP resources within a resource group.</span></span>

    azure network public-ip list -g myresourcegroup

    info:    Executing command network public-ip list
    + Getting hello public ip addresses
    data:    Name             Location  Allocation  IP Address    Idle timeout  DNS Name
    data:    ---------------  --------  ----------  ------------  ------------  -------------------------------------------
    data:    mypubip5         westus    Dynamic                   4             "domain name".westus.cloudapp.azure.com
    data:    myPublicIP       eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip   eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip1  eastus   Static (Static IP address) 4             azureclitest.eastus.cloudapp.azure.com

<span data-ttu-id="5c418-264">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-264">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>
    <span data-ttu-id="5c418-265">Ağ ve genel IP < resource-group > [Seçenekler] Göster<name></span><span class="sxs-lookup"><span data-stu-id="5c418-265">network public-ip show [options] <resource-group> <name></span></span>

<span data-ttu-id="5c418-266">Bir kaynak grubu içindeki ortak IP kaynak için genel IP özelliklerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5c418-266">Displays public ip properties for a public ip resource within a resource group.</span></span>

    azure network public-ip show -g myresourcegroup -n mytestpublicip

    info:    Executing command network public-ip show
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip
    data:    Name:                 mytestpublicip
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip show command OK

<span data-ttu-id="5c418-267">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-267">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -s, --subscription <subscription>      hello subscription identifier


    network public-ip delete [options] <resource-group> <name>

<span data-ttu-id="5c418-268">Genel IP kaynağı siler.</span><span class="sxs-lookup"><span data-stu-id="5c418-268">Deletes public ip resource.</span></span>

    azure network public-ip delete -g group-1 -n mypublicipname
    info:    Executing command network public-ip delete
    + Looking up hello public ip "mypublicipname"
    Delete public ip address "mypublicipname"? [y/n] y
    + Deleting public ip address "mypublicipname"
    info:    network public-ip delete command OK

<span data-ttu-id="5c418-269">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-269">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="5c418-270">**Komutları toomanage ağ arabirimleri**</span><span class="sxs-lookup"><span data-stu-id="5c418-270">**Commands toomanage network interfaces**</span></span>

    network nic create [options] <resource-group> <name> <location>
<span data-ttu-id="5c418-271">Veya sanal makine tooa ilişkilendirmek için yük Dengeleyiciler kullanılabilir ağ arabirimi (NIC) adlı bir kaynak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5c418-271">Creates a resource called network interface (NIC) which can be used for load balancers or associate tooa Virtual Machine.</span></span>

    azure network nic create -g myresourcegroup -l eastus -n testnic1 --subnet-name subnet-1 --subnet-vnet-name myvnet

    info:    Executing command network nic create
    + Looking up hello network interface "testnic1"
    + Looking up hello subnet "subnet-1"
    + Creating network interface "testnic1"
    + Looking up hello network interface "testnic1"
    data:    Id:                     /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/networkInterfaces/testnic1
    data:    Name:                   testnic1
    data:    Type:                   Microsoft.Network/networkInterfaces
    data:    Location:               eastus
    data:    Provisioning state:     Succeeded
    data:    IP configurations:
    data:       Name:                         NIC-config
    data:       Provisioning state:           Succeeded
    data:       Private IP address:           10.0.0.5
    data:       Private IP Allocation Method: Dynamic
    data:       Subnet:                       /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/virtualNetworks/myVNET/subnets/Subnet-1

<span data-ttu-id="5c418-272">Parametre seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="5c418-272">Parameter options:</span></span>

    -h, --help                                                       output usage information
    -v, --verbose                                                    use verbose output
    --json                                                           use json output
    -g, --resource-group <resource-group>                            hello name of hello resource group
    -n, --name <name>                                                hello name of hello network interface
    -l, --location <location>                                        hello location
    -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
    -o, --network-security-group-name <network-security-group-name>  hello network security group name.
    This network security group must exist in hello same resource group as hello nic.
    Please use network-security-group-id if that is not hello case.
    -i, --public-ip-id <public-ip-id>                                hello public IP identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -p, --public-ip-name <public-ip-name>                            hello public IP name.
    This public ip must exist in hello same resource group as hello nic.
    Please use public-ip-id if that is not hello case.
    -a, --private-ip-address <private-ip-address>                    hello private IP address
    -u, --subnet-id <subnet-id>                                      hello subnet identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<vnet-name>/subnets/<subnet-name>
    --subnet-name <subnet-name>                                  hello subnet name
    -m, --subnet-vnet-name <subnet-vnet-name>                        hello vnet name under which subnet-name exists
    -t, --tags <tags>                                                hello comma seperated list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>                                hello subscription identifier
    data:
    info:    network nic create command OK

<BR>

    network nic set [options] <resource-group> <name>

    network nic list [options] <resource-group>
    network nic show [options] <resource-group> <name>
    network nic delete [options] <resource-group> <name>

<span data-ttu-id="5c418-273">**Komutları toomanage ağ güvenlik grupları**</span><span class="sxs-lookup"><span data-stu-id="5c418-273">**Commands toomanage network security groups**</span></span>

    network nsg create [options] <resource-group> <name> <location>
    network nsg set [options] <resource-group> <name>
    network nsg list [options] <resource-group>
    network nsg show [options] <resource-group> <name>
    network nsg delete [options] <resource-group> <name>

<span data-ttu-id="5c418-274">**Komutları toomanage ağ güvenlik grubu kuralları**</span><span class="sxs-lookup"><span data-stu-id="5c418-274">**Commands toomanage network security group rules**</span></span>

    network nsg rule create [options] <resource-group> <nsg-name> <name>
    network nsg rule set [options] <resource-group> <nsg-name> <name>
    network nsg rule list [options] <resource-group> <nsg-name>
    network nsg rule show [options] <resource-group> <nsg-name> <name>
    network nsg rule delete [options] <resource-group> <nsg-name> <name>

<span data-ttu-id="5c418-275">**Komutları toomanage trafik Yöneticisi profili**</span><span class="sxs-lookup"><span data-stu-id="5c418-275">**Commands toomanage traffic manager profile**</span></span>

    network traffic-manager profile create [options] <resource-group> <name>
    network traffic-manager profile set [options] <resource-group> <name>
    network traffic-manager profile list [options] <resource-group>
    network traffic-manager profile show [options] <resource-group> <name>
    network traffic-manager profile delete [options] <resource-group> <name>
    network traffic-manager profile is-dns-available [options] <resource-group> <relative-dns-name>

<span data-ttu-id="5c418-276">**Komutları toomanage trafik Yöneticisi uç noktaları**</span><span class="sxs-lookup"><span data-stu-id="5c418-276">**Commands toomanage traffic manager endpoints**</span></span>

    network traffic-manager profile endpoint create [options] <resource-group> <profile-name> <name> <endpoint-location>
    network traffic-manager profile endpoint set [options] <resource-group> <profile-name> <name>
    network traffic-manager profile endpoint delete [options] <resource-group> <profile-name> <name>

<span data-ttu-id="5c418-277">**Komutları toomanage sanal ağ geçitleri**</span><span class="sxs-lookup"><span data-stu-id="5c418-277">**Commands toomanage virtual network gateways**</span></span>

    network gateway list [options] <resource-group>

## <a name="azure-provider-commands-toomanage-resource-provider-registrations"></a><span data-ttu-id="5c418-278">Azure sağlayıcısı: komutları toomanage kaynak sağlayıcısı kayıtlar</span><span class="sxs-lookup"><span data-stu-id="5c418-278">azure provider: Commands toomanage resource provider registrations</span></span>
<span data-ttu-id="5c418-279">**Kaynak Yöneticisi'nde şu anda kayıtlı sağlayıcı listesi**</span><span class="sxs-lookup"><span data-stu-id="5c418-279">**List currently registered providers in Resource Manager**</span></span>

    provider list [options]

<span data-ttu-id="5c418-280">**Sağlayıcı ad alanı hello hakkında ayrıntıları göster istendi**</span><span class="sxs-lookup"><span data-stu-id="5c418-280">**Show details about hello requested provider namespace**</span></span>

    provider show [options] <namespace>

<span data-ttu-id="5c418-281">**Sağlayıcı hello aboneliğiniz ile kaydeder**</span><span class="sxs-lookup"><span data-stu-id="5c418-281">**Register provider with hello subscription**</span></span>

    provider register [options] <namespace>

<span data-ttu-id="5c418-282">**Merhaba aboneliğiyle Sağlayıcısı kaydı**</span><span class="sxs-lookup"><span data-stu-id="5c418-282">**Unregister provider with hello subscription**</span></span>

    provider unregister [options] <namespace>

## <a name="azure-resource-commands-toomanage-your-resources"></a><span data-ttu-id="5c418-283">Azure kaynak: toomanage kaynaklarınızı komutları</span><span class="sxs-lookup"><span data-stu-id="5c418-283">azure resource: Commands toomanage your resources</span></span>
<span data-ttu-id="5c418-284">**Bir kaynak içinde bir kaynak grubu oluşturur**</span><span class="sxs-lookup"><span data-stu-id="5c418-284">**Creates a resource in a resource group**</span></span>

    resource create [options] <resource-group> <name> <resource-type> <location> <api-version>

<span data-ttu-id="5c418-285">**Kaynak şablonları veya parametreleri olmadan bir kaynak grubunda güncelleştirir**</span><span class="sxs-lookup"><span data-stu-id="5c418-285">**Updates a resource in a resource group without any templates or parameters**</span></span>

    resource set [options] <resource-group> <name> <resource-type> <properties> <api-version>

<span data-ttu-id="5c418-286">**Listeleri hello kaynakları**</span><span class="sxs-lookup"><span data-stu-id="5c418-286">**Lists hello resources**</span></span>

    resource list [options] [resource-group]

<span data-ttu-id="5c418-287">**Bir kaynak içinde bir kaynak grubuna veya aboneliğe alır**</span><span class="sxs-lookup"><span data-stu-id="5c418-287">**Gets one resource within a resource group or subscription**</span></span>

    resource show [options] <resource-group> <name> <resource-type> <api-version>

<span data-ttu-id="5c418-288">**Kaynak bir kaynak grubunda siler**</span><span class="sxs-lookup"><span data-stu-id="5c418-288">**Deletes a resource in a resource group**</span></span>

    resource delete [options] <resource-group> <name> <resource-type> <api-version>

## <a name="azure-role-commands-toomanage-your-azure-roles"></a><span data-ttu-id="5c418-289">Azure rol: Azure rollerinizi toomanage komutları</span><span class="sxs-lookup"><span data-stu-id="5c418-289">azure role: Commands toomanage your Azure roles</span></span>
<span data-ttu-id="5c418-290">**Tüm kullanılabilir rol tanımlarını Al**</span><span class="sxs-lookup"><span data-stu-id="5c418-290">**Get all available role definitions**</span></span>

    role list [options]

<span data-ttu-id="5c418-291">**Kullanılabilir rol tanımı Al**</span><span class="sxs-lookup"><span data-stu-id="5c418-291">**Get an available role definition**</span></span>

    role show [options] [name]

<span data-ttu-id="5c418-292">**Rol atamalarınızı toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-292">**Commands toomanage your role assignment**</span></span>

    role assignment create [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment list [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment delete [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]

## <a name="azure-storage-commands-toomanage-your-storage-objects"></a><span data-ttu-id="5c418-293">Azure Depolama: depolama nesnelerinizi toomanage komutları</span><span class="sxs-lookup"><span data-stu-id="5c418-293">azure storage: Commands toomanage your Storage objects</span></span>
<span data-ttu-id="5c418-294">**Depolama hesaplarınızı toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-294">**Commands toomanage your Storage accounts**</span></span>

    storage account list [options]
    storage account show [options] <name>
    storage account create [options] <name>
    storage account set [options] <name>
    storage account delete [options] <name>

<span data-ttu-id="5c418-295">**Depolama hesabı anahtarlarını toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-295">**Commands toomanage your Storage account keys**</span></span>

    storage account keys list [options] <name>
    storage account keys renew [options] <name>

<span data-ttu-id="5c418-296">**Depolama bağlantı dizenizi tooshow komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-296">**Commands tooshow your Storage connection string**</span></span>

    storage account connectionstring show [options] <name>

<span data-ttu-id="5c418-297">**Depolama kapsayıcıları toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-297">**Commands toomanage your Storage containers**</span></span>

    storage container list [options] [prefix]
    storage container show [options] [container]
    storage container create [options] [container]
    storage container delete [options] [container]
    storage container set [options] [container]

<span data-ttu-id="5c418-298">**Depolama kapsayıcısı toomanage paylaşılan erişim imzalarını komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-298">**Commands toomanage shared access signatures of your Storage container**</span></span>

    storage container sas create [options] [container] [permissions] [expiry]

<span data-ttu-id="5c418-299">**Erişim ilkeleri, depolama kapsayıcısının komutları toomanage depolanan**</span><span class="sxs-lookup"><span data-stu-id="5c418-299">**Commands toomanage stored access policies of your Storage container**</span></span>

    storage container policy create [options] [container] [name]
    storage container policy show [options] [container] [name]
    storage container policy list [options] [container]
    storage container policy set [options] [container] [name]
    storage container policy delete [options] [container] [name]

<span data-ttu-id="5c418-300">**Depolama bloblarınızın toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-300">**Commands toomanage your Storage blobs**</span></span>

    storage blob list [options] [container] [prefix]
    storage blob show [options] [container] [blob]
    storage blob delete [options] [container] [blob]
    storage blob upload [options] [file] [container] [blob]
    storage blob download [options] [container] [blob] [destination]

<span data-ttu-id="5c418-301">**Blob kopyalama işlemleri toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-301">**Commands toomanage your blob copy operations**</span></span>

    storage blob copy start [options] [sourceUri] [destContainer]
    storage blob copy show [options] [container] [blob]
    storage blob copy stop [options] [container] [blob] [copyid]

<span data-ttu-id="5c418-302">**Depolama blobu komutları toomanage paylaşılan erişim imzası**</span><span class="sxs-lookup"><span data-stu-id="5c418-302">**Commands toomanage shared access signature of your Storage blob**</span></span>

    storage blob sas create [options] [container] [blob] [permissions] [expiry]

<span data-ttu-id="5c418-303">**Depolama dosya paylaşımlarını toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-303">**Commands toomanage your Storage file shares**</span></span>

    storage share create [options] [share]
    storage share show [options] [share]
    storage share delete [options] [share]
    storage share list [options] [prefix]

<span data-ttu-id="5c418-304">**Depolama dosyalarınızı toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-304">**Commands toomanage your Storage files**</span></span>

    storage file list [options] [share] [path]
    storage file delete [options] [share] [path]
    storage file upload [options] [source] [share] [path]
    storage file download [options] [share] [path] [destination]

<span data-ttu-id="5c418-305">**Depolama dosya dizininize toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-305">**Commands toomanage your Storage file directory**</span></span>

    storage directory create [options] [share] [path]
    storage directory delete [options] [share] [path]

<span data-ttu-id="5c418-306">**Depolama kuyrukları toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-306">**Commands toomanage your Storage queues**</span></span>

    storage queue create [options] [queue]
    storage queue list [options] [prefix]
    storage queue show [options] [queue]
    storage queue delete [options] [queue]

<span data-ttu-id="5c418-307">**Depolama kuyruğu, komutları toomanage paylaşılan erişim imzaları**</span><span class="sxs-lookup"><span data-stu-id="5c418-307">**Commands toomanage shared access signatures of your Storage queue**</span></span>

    storage queue sas create [options] [queue] [permissions] [expiry]

<span data-ttu-id="5c418-308">**Erişim ilkeleri, depolama kuyruğu komutları toomanage depolanan**</span><span class="sxs-lookup"><span data-stu-id="5c418-308">**Commands toomanage stored access policies of your Storage queue**</span></span>

    storage queue policy create [options] [queue] [name]
    storage queue policy show [options] [queue] [name]
    storage queue policy list [options] [queue]
    storage queue policy set [options] [queue] [name]
    storage queue policy delete [options] [queue] [name]

<span data-ttu-id="5c418-309">**Depolama günlüğe kaydetme özellikleri toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-309">**Commands toomanage your Storage logging properties**</span></span>

    storage logging show [options]
    storage logging set [options]

<span data-ttu-id="5c418-310">**Depolama ölçümleri özelliklerinizi toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-310">**Commands toomanage your Storage metrics properties**</span></span>

    storage metrics show [options]
    storage metrics set [options]

<span data-ttu-id="5c418-311">**Depolama tabloları toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-311">**Commands toomanage your Storage tables**</span></span>

    storage table create [options] [table]
    storage table list [options] [prefix]
    storage table show [options] [table]
    storage table delete [options] [table]

<span data-ttu-id="5c418-312">**Depolama tablonuzun toomanage paylaşılan erişim imzaları komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-312">**Commands toomanage shared access signatures of your Storage table**</span></span>

    storage table sas create [options] [table] [permissions] [expiry]

<span data-ttu-id="5c418-313">**Erişim ilkeleri depolama tablonuzun komutları toomanage depolanan**</span><span class="sxs-lookup"><span data-stu-id="5c418-313">**Commands toomanage stored access policies of your Storage table**</span></span>

    storage table policy create [options] [table] [name]
    storage table policy show [options] [table] [name]
    storage table policy list [options] [table]
    storage table policy set [options] [table] [name]
    storage table policy delete [options] [table] [name]

## <a name="azure-tag-commands-toomanage-your-resource-manager-tag"></a><span data-ttu-id="5c418-314">Azure etiketi: resource manager etiketi toomanage komutları</span><span class="sxs-lookup"><span data-stu-id="5c418-314">azure tag: Commands toomanage your resource manager tag</span></span>
<span data-ttu-id="5c418-315">**Etiket ekleme**</span><span class="sxs-lookup"><span data-stu-id="5c418-315">**Add a tag**</span></span>

    tag create [options] <name> <value>

<span data-ttu-id="5c418-316">**Tüm bir etiket veya bir etiket değeri kaldırma**</span><span class="sxs-lookup"><span data-stu-id="5c418-316">**Remove an entire tag or a tag value**</span></span>

    tag delete [options] <name> <value>

<span data-ttu-id="5c418-317">**Merhaba etiket bilgilerini listeler**</span><span class="sxs-lookup"><span data-stu-id="5c418-317">**Lists hello tag information**</span></span>

    tag list [options]

<span data-ttu-id="5c418-318">**Bir etiketi Al**</span><span class="sxs-lookup"><span data-stu-id="5c418-318">**Get a tag**</span></span>

    tag show [options] [name]

## <a name="azure-vm-commands-toomanage-your-azure-virtual-machines"></a><span data-ttu-id="5c418-319">Azure vm: Azure sanal makinelerinizi toomanage komutları</span><span class="sxs-lookup"><span data-stu-id="5c418-319">azure vm: Commands toomanage your Azure Virtual Machines</span></span>
<span data-ttu-id="5c418-320">**Bir VM oluşturma**</span><span class="sxs-lookup"><span data-stu-id="5c418-320">**Create a VM**</span></span>

    vm create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="5c418-321">**Varsayılan kaynaklar ile bir VM oluşturma**</span><span class="sxs-lookup"><span data-stu-id="5c418-321">**Create a VM with default resources**</span></span>

    vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password

> [!TIP]
> <span data-ttu-id="5c418-322">CLI Sürüm 0.10 ile başlayarak, "UbuntuLTS" veya "Win2012R2Datacenter" Merhaba gibi kısa bir diğer ad sağlayabilir `image-urn` bazı yaygın Market görüntüleri için.</span><span class="sxs-lookup"><span data-stu-id="5c418-322">Starting with CLI version 0.10, you can provide a short alias such as "UbuntuLTS" or "Win2012R2Datacenter" as hello `image-urn` for some popular Marketplace images.</span></span> <span data-ttu-id="5c418-323">Çalıştırma `azure help vm quick-create` seçenekleri için.</span><span class="sxs-lookup"><span data-stu-id="5c418-323">Run `azure help vm quick-create` for options.</span></span> <span data-ttu-id="5c418-324">Ayrıca, 0,10, sürümünden başlayarak `azure vm quick-create` hello seçili bölgede kullanılabiliyorsa, varsayılan olarak premium depolama kullanır.</span><span class="sxs-lookup"><span data-stu-id="5c418-324">Additionally, starting with version 0.10, `azure vm quick-create` uses premium storage by default if it's available in hello selected region.</span></span>
> 
> 

<span data-ttu-id="5c418-325">**Bir hesap içinde listesi hello sanal makineler**</span><span class="sxs-lookup"><span data-stu-id="5c418-325">**List hello virtual machines within an account**</span></span>

    vm list [options]

<span data-ttu-id="5c418-326">**Bir kaynak grubu içinde bir sanal makine Al**</span><span class="sxs-lookup"><span data-stu-id="5c418-326">**Get one virtual machine within a resource group**</span></span>

    vm show [options] <resource-group> <name>

<span data-ttu-id="5c418-327">**Bir kaynak grubu içinde bir sanal makineyi Sil**</span><span class="sxs-lookup"><span data-stu-id="5c418-327">**Delete one virtual machine within a resource group**</span></span>

    vm delete [options] <resource-group> <name>

<span data-ttu-id="5c418-328">**Bir kaynak grubu içinde bir sanal makine kapatma**</span><span class="sxs-lookup"><span data-stu-id="5c418-328">**Shutdown one virtual machine within a resource group**</span></span>

    vm stop [options] <resource-group> <name>

<span data-ttu-id="5c418-329">**Bir kaynak grubu içinde bir sanal makineyi yeniden başlatın**</span><span class="sxs-lookup"><span data-stu-id="5c418-329">**Restart one virtual machine within a resource group**</span></span>

    vm restart [options] <resource-group> <name>

<span data-ttu-id="5c418-330">**Bir kaynak grubu içinde bir sanal makineyi Başlat**</span><span class="sxs-lookup"><span data-stu-id="5c418-330">**Start one virtual machine within a resource group**</span></span>

    vm start [options] <resource-group> <name>

<span data-ttu-id="5c418-331">**Bir kaynak grubu ve sürümler hello içinde bir sanal makine kapatma işlem kaynakları**</span><span class="sxs-lookup"><span data-stu-id="5c418-331">**Shutdown one virtual machine within a resource group and releases hello compute resources**</span></span>

    vm deallocate [options] <resource-group> <name>

<span data-ttu-id="5c418-332">**Kullanılabilir sanal makine boyutlarını Listele**</span><span class="sxs-lookup"><span data-stu-id="5c418-332">**List available virtual machine sizes**</span></span>

    vm sizes [options]

<span data-ttu-id="5c418-333">**Merhaba işletim sistemi görüntüsü olarak VM veya VM görüntüsü yakalama**</span><span class="sxs-lookup"><span data-stu-id="5c418-333">**Capture hello VM as OS Image or VM Image**</span></span>

    vm capture [options] <resource-group> <name> <vhd-name-prefix>

<span data-ttu-id="5c418-334">**Merhaba VM tooGeneralized Hello durumunu ayarla**</span><span class="sxs-lookup"><span data-stu-id="5c418-334">**Set hello state of hello VM tooGeneralized**</span></span>

    vm generalize [options] <resource-group> <name>

<span data-ttu-id="5c418-335">**Merhaba VM örnek görünümünü Al**</span><span class="sxs-lookup"><span data-stu-id="5c418-335">**Get instance view of hello VM**</span></span>

    vm get-instance-view [options] <resource-group> <name>

<span data-ttu-id="5c418-336">**Bir sanal makine ve tooreset hello Yöneticisi veya sudo yetkilisi hello hesabının parolasını tooreset Uzak Masaüstü erişimi veya SSH ayarlarını etkinleştir**</span><span class="sxs-lookup"><span data-stu-id="5c418-336">**Enable you tooreset Remote Desktop Access or SSH settings on a Virtual Machine and tooreset hello password for hello account that has administrator or sudo authority**</span></span>

    vm reset-access [options] <resource-group> <name>

<span data-ttu-id="5c418-337">**VM yeni verilerle güncelleştirin**</span><span class="sxs-lookup"><span data-stu-id="5c418-337">**Update VM with new data**</span></span>

    vm set [options] <resource-group> <name>

<span data-ttu-id="5c418-338">**Sanal makine veri diski toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-338">**Commands toomanage your Virtual Machine data disks**</span></span>

    vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]
    vm disk detach [options] <resource-group> <vm-name> <lun>
    vm disk attach [options] <resource-group> <vm-name> [vhd-url]

<span data-ttu-id="5c418-339">**Komutları toomanage VM kaynak uzantıları**</span><span class="sxs-lookup"><span data-stu-id="5c418-339">**Commands toomanage VM resource extensions**</span></span>

    vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>
    vm extension get [options] <resource-group> <vm-name>

<span data-ttu-id="5c418-340">**Docker sanal makineniz toomanage komutları**</span><span class="sxs-lookup"><span data-stu-id="5c418-340">**Commands toomanage your Docker Virtual Machine**</span></span>

    vm docker create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="5c418-341">**Komutları toomanage VM görüntüleri**</span><span class="sxs-lookup"><span data-stu-id="5c418-341">**Commands toomanage VM images**</span></span>

    vm image list-publishers [options] <location>
    vm image list-offers [options] <location> <publisher>
    vm image list-skus [options] <location> <publisher> <offer>
    vm image list [options] <location> <publisher> [offer] [sku]
