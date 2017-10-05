---
title: "Hdınsight için ek Azure depolama hesapları ekleme | Microsoft Docs"
description: "Ek Azure depolama hesapları olan bir Hdınsight kümesine eklemeyi öğrenin."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 0853e8605e07c28867676e9c13b89263ade67c88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="add-additional-storage-accounts-to-hdinsight"></a><span data-ttu-id="f729b-103">Hdınsight için ek depolama hesapları ekleme</span><span class="sxs-lookup"><span data-stu-id="f729b-103">Add additional storage accounts to HDInsight</span></span>

<span data-ttu-id="f729b-104">Hdınsight için ek Azure depolama hesapları eklemek için betik eylemleri kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f729b-104">Learn how to use script actions to add additional Azure storage accounts to HDInsight.</span></span> <span data-ttu-id="f729b-105">Bu belgede yer alan adımlar bir depolama hesabı olan bir Linux tabanlı Hdınsight kümesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f729b-105">The steps in this document add a storage account to an existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f729b-106">Bu belgedeki oluşturulduktan sonra ek depolama alanı bir kümeye ekleme hakkındaki bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="f729b-106">The information in this document is about adding additional storage to a cluster after it has been created.</span></span> <span data-ttu-id="f729b-107">Küme oluşturma sırasında depolama hesapları ekleme hakkında daha fazla bilgi için bkz: [Hdınsight Hadoop, Spark, Kafka ve daha fazla ile kümelerde ayarlama](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="f729b-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="f729b-108">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="f729b-108">How it works</span></span>

<span data-ttu-id="f729b-109">Bu betiği aşağıdaki parametreleri alır:</span><span class="sxs-lookup"><span data-stu-id="f729b-109">This script takes the following parameters:</span></span>

* <span data-ttu-id="f729b-110">__Azure depolama hesabı adı__: Hdınsight kümesine eklemek için depolama hesabının adı.</span><span class="sxs-lookup"><span data-stu-id="f729b-110">__Azure storage account name__: The name of the storage account to add to the HDInsight cluster.</span></span> <span data-ttu-id="f729b-111">Hdınsight, komut dosyasını çalıştırdıktan sonra okuma ve bu depolama hesabında depolanan verileri yazma.</span><span class="sxs-lookup"><span data-stu-id="f729b-111">After running the script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="f729b-112">__Azure depolama hesabı anahtarı__: depolama hesabına erişim izni veren bir anahtar.</span><span class="sxs-lookup"><span data-stu-id="f729b-112">__Azure storage account key__: A key that grants access to the storage account.</span></span>

* <span data-ttu-id="f729b-113">__-p__ (isteğe bağlı): belirtilmişse, anahtarı şifrelenmemiş ve düz metin olarak core-site.xml dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="f729b-113">__-p__ (optional): If specified, the key is not encrypted and is stored in the core-site.xml file as plain text.</span></span>

<span data-ttu-id="f729b-114">İşleme sırasında komut aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="f729b-114">During processing, the script performs the following actions:</span></span>

* <span data-ttu-id="f729b-115">Depolama hesabı küme için core-site.xml yapılandırmasının zaten varsa, komut dosyası çıkar ve başka hiçbir eylem gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f729b-115">If the storage account already exists in the core-site.xml configuration for the cluster, the script exits and no further actions are performed.</span></span>

* <span data-ttu-id="f729b-116">Depolama hesabı var ve anahtarı kullanılarak erişilebilir doğrular.</span><span class="sxs-lookup"><span data-stu-id="f729b-116">Verifies that the storage account exists and can be accessed using the key.</span></span>

* <span data-ttu-id="f729b-117">Küme kimlik bilgilerini kullanarak anahtarı şifreleyen.</span><span class="sxs-lookup"><span data-stu-id="f729b-117">Encrypts the key using the cluster credential.</span></span>

* <span data-ttu-id="f729b-118">Depolama hesabı core-site.xml dosyasına ekler.</span><span class="sxs-lookup"><span data-stu-id="f729b-118">Adds the storage account to the core-site.xml file.</span></span>

* <span data-ttu-id="f729b-119">Durdurur ve Oozie, YARN, MapReduce2 ve HDFS hizmetleri yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="f729b-119">Stops and restarts the Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="f729b-120">Durdurma ve bu hizmetleri başlatma yeni depolama hesabı kullanmak üzere sağlar.</span><span class="sxs-lookup"><span data-stu-id="f729b-120">Stopping and starting these services allows them to use the new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="f729b-121">Hdınsight kümesi farklı bir konumda bir depolama hesabıyla desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="f729b-121">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="the-script"></a><span data-ttu-id="f729b-122">Komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f729b-122">The script</span></span>

<span data-ttu-id="f729b-123">__Komut dosyası konumu__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="f729b-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="f729b-124">__Gereksinimleri__:</span><span class="sxs-lookup"><span data-stu-id="f729b-124">__Requirements__:</span></span>

* <span data-ttu-id="f729b-125">Komut dosyası üzerinde uygulanması gereken __baş düğümler__.</span><span class="sxs-lookup"><span data-stu-id="f729b-125">The script must be applied on the __Head nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="f729b-126">Betik kullanmak için</span><span class="sxs-lookup"><span data-stu-id="f729b-126">To use the script</span></span>

<span data-ttu-id="f729b-127">Bu komut, Azure portalı, Azure PowerShell veya Azure CLI 1.0 kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f729b-127">This script can be used from the Azure portal, Azure PowerShell, or the Azure CLI 1.0.</span></span> <span data-ttu-id="f729b-128">Daha fazla bilgi için bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) belge.</span><span class="sxs-lookup"><span data-stu-id="f729b-128">For more information, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f729b-129">Özelleştirme belgede sağlanan adımları kullanarak, bu komut dosyasını uygulamak için aşağıdaki bilgileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="f729b-129">When using the steps provided in the customization document, use the following information to apply this script:</span></span>
>
> * <span data-ttu-id="f729b-130">Tüm örnek betik eylemi URI bu komut dosyası (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh) için URI ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f729b-130">Replace any example script action URI with the URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="f729b-131">Kümeye eklenecek depolama hesabı anahtarı ve Azure depolama hesabı adı ile örnek parametreleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f729b-131">Replace any example parameters with the Azure storage account name and key of the storage account to be added to the cluster.</span></span> <span data-ttu-id="f729b-132">Azure portalını kullanıyorsanız, bu parametreler boşlukla ayrılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f729b-132">If using the Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="f729b-133">Bu komut dosyası olarak işaretlemek gerekmez __kalıcı__, doğrudan bir küme için Ambari yapılandırmasını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="f729b-133">You do not need to mark this script as __Persisted__, as it directly updates the Ambari configuration for the cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="f729b-134">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="f729b-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="f729b-135">Azure portalından veya Araçlar görüntülenmeyen depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="f729b-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="f729b-136">Hdınsight kümesi Azure portalında görüntülerken seçme __depolama hesapları__ altında girdisi __özellikleri__ bu betik eylemi eklenen depolama hesaplarına görüntülemez.</span><span class="sxs-lookup"><span data-stu-id="f729b-136">When viewing the HDInsight cluster in the Azure portal, selecting the __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="f729b-137">Azure PowerShell ve Azure CLI ek depolama alanı hesabı ya da görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="f729b-137">Azure PowerShell and Azure CLI do not display the additional storage account either.</span></span>

<span data-ttu-id="f729b-138">Komut dosyası küme için core-site.xml yapılandırmasının yalnızca değiştirdiğinden depolama bilgiler görüntülenmiyor.</span><span class="sxs-lookup"><span data-stu-id="f729b-138">The storage information isn't displayed because the script only modifies the core-site.xml configuration for the cluster.</span></span> <span data-ttu-id="f729b-139">Bu bilgiler Azure management API'leri kullanarak küme bilgi alınırken kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="f729b-139">This information is not used when retrieving the cluster information using Azure management APIs.</span></span>

<span data-ttu-id="f729b-140">Bu komut dosyasını kullanarak kümeye eklenen depolama hesabı bilgilerini görüntülemek için Ambari REST API kullanın.</span><span class="sxs-lookup"><span data-stu-id="f729b-140">To view storage account information added to the cluster using this script, use the Ambari REST API.</span></span> <span data-ttu-id="f729b-141">Kümeniz için bu bilgileri almak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="f729b-141">Use the following commands to retrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter the cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="f729b-142">Ayarlama `$clusterName` Hdınsight kümesinin adı.</span><span class="sxs-lookup"><span data-stu-id="f729b-142">Set `$clusterName` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="f729b-143">Ayarlama `$storageAccountName` depolama hesabının adı.</span><span class="sxs-lookup"><span data-stu-id="f729b-143">Set `$storageAccountName` to the name of the storage account.</span></span> <span data-ttu-id="f729b-144">İstendiğinde, küme oturum açma (Yönetici) ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="f729b-144">When prompted, enter the cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="f729b-145">Ayarlama `$PASSWORD` küme oturum açma (Yönetici) hesap parolası için.</span><span class="sxs-lookup"><span data-stu-id="f729b-145">Set `$PASSWORD` to the cluster login (admin) account password.</span></span> <span data-ttu-id="f729b-146">Ayarlama `$CLUSTERNAME` Hdınsight kümesinin adı.</span><span class="sxs-lookup"><span data-stu-id="f729b-146">Set `$CLUSTERNAME` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="f729b-147">Ayarlama `$STORAGEACCOUNTNAME` depolama hesabının adı.</span><span class="sxs-lookup"><span data-stu-id="f729b-147">Set `$STORAGEACCOUNTNAME` to the name of the storage account.</span></span>
>
> <span data-ttu-id="f729b-148">Bu örnekte [curl (http://curl.haxx.se/)](http://curl.haxx.se/) ve [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) almak ve JSON verilerini ayrıştırılamadı.</span><span class="sxs-lookup"><span data-stu-id="f729b-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) to retrieve and parse JSON data.</span></span>

<span data-ttu-id="f729b-149">Bu komut, kullanırken değiştirin __CLUSTERNAME__ Hdınsight kümesi adı.</span><span class="sxs-lookup"><span data-stu-id="f729b-149">When using this command, replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="f729b-150">Değiştir __parola__ küme için HTTP oturum açma parolası ile.</span><span class="sxs-lookup"><span data-stu-id="f729b-150">Replace __PASSWORD__ with the HTTP login password for the cluster.</span></span> <span data-ttu-id="f729b-151">Değiştir __STORAGEACCOUNT__ betik eylemi kullanarak eklenen depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="f729b-151">Replace __STORAGEACCOUNT__ with the name of the storage account added using script action.</span></span> <span data-ttu-id="f729b-152">Bu komuttan döndürülen bilgi için aşağıdaki metni benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="f729b-152">Information returned from this command appears similar to the following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="f729b-153">Bu metin, depolama hesabına erişmek için kullanılan şifreli bir anahtar örneğidir.</span><span class="sxs-lookup"><span data-stu-id="f729b-153">This text is an example of an encrypted key, which is used to access the storage account.</span></span>

### <a name="unable-to-access-storage-after-changing-key"></a><span data-ttu-id="f729b-154">Depolama anahtarı değiştirdikten sonra erişilemiyor</span><span class="sxs-lookup"><span data-stu-id="f729b-154">Unable to access storage after changing key</span></span>

<span data-ttu-id="f729b-155">Bir depolama hesabı anahtarı değiştirirseniz, Hdınsight depolama hesabı artık erişemez.</span><span class="sxs-lookup"><span data-stu-id="f729b-155">If you change the key for a storage account, HDInsight can no longer access the storage account.</span></span> <span data-ttu-id="f729b-156">Hdınsight, küme için core-site.xml anahtar önbelleğe alınmış bir kopyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="f729b-156">HDInsight uses a cached copy of key in the core-site.xml for the cluster.</span></span> <span data-ttu-id="f729b-157">Önbelleğe alınan bu kopyayı yeni anahtarı eşleşecek şekilde güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f729b-157">This cached copy must be updated to match the new key.</span></span>

<span data-ttu-id="f729b-158">Betik eylemi yeniden çalıştıran mu __değil__ anahtar depolama hesabı için bir giriş zaten var olup olmadığını görmek için komut dosyasını denetler gibi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f729b-158">Running the script action again does __not__ update the key, as the script checks to see if an entry for the storage account already exists.</span></span> <span data-ttu-id="f729b-159">Bir giriş zaten varsa, herhangi bir değişiklik yapmaz.</span><span class="sxs-lookup"><span data-stu-id="f729b-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="f729b-160">Bu sorunu gidermek için depolama hesabı için varolan bir girişi kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f729b-160">To work around this problem, you must remove the existing entry for the storage account.</span></span> <span data-ttu-id="f729b-161">Varolan bir girişi kaldırmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="f729b-161">Use the following steps to remove the existing entry:</span></span>

1. <span data-ttu-id="f729b-162">Bir web tarayıcısında Hdınsight kümeniz için Ambari Web kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="f729b-162">In a web browser, open the Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="f729b-163">URI https://CLUSTERNAME.azurehdinsight.net ' dir.</span><span class="sxs-lookup"><span data-stu-id="f729b-163">The URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="f729b-164">__CLUSTERNAME__ değerini kümenizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f729b-164">Replace __CLUSTERNAME__ with the name of your cluster.</span></span>

    <span data-ttu-id="f729b-165">İstendiğinde, kümeniz için HTTP oturum açma kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="f729b-165">When prompted, enter the HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="f729b-166">Sayfanın sol Hizmetleri listesinden seçin __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="f729b-166">From the list of services on the left of the page, select __HDFS__.</span></span> <span data-ttu-id="f729b-167">Ardından __yapılandırmalar__ sayfasının ortasında sekmesi.</span><span class="sxs-lookup"><span data-stu-id="f729b-167">Then select the __Configs__ tab in the center of the page.</span></span>

3. <span data-ttu-id="f729b-168">İçinde __filtre...__  değeri alanına, __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="f729b-168">In the __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="f729b-169">Bu kümeye eklenen herhangi bir ek depolama alanı hesabı girişlerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f729b-169">This returns entries for any additional storage accounts that have been added to the cluster.</span></span> <span data-ttu-id="f729b-170">İki tür giriş vardır; __keyprovider__ ve __anahtar__.</span><span class="sxs-lookup"><span data-stu-id="f729b-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="f729b-171">Her ikisi de anahtar adının bir parçası olarak depolama hesabı adını içerir.</span><span class="sxs-lookup"><span data-stu-id="f729b-171">Both contain the name of the storage account as part of the key name.</span></span>

    <span data-ttu-id="f729b-172">Aşağıdaki örnek girişlerdir adlı bir depolama hesabı için __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="f729b-172">The following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="f729b-173">Gereksinim kaldırmak için depolama hesabı için anahtarlar tanımladıktan sonra kırmızı kullanmak '-' silmek için giriş sağındaki simgesi.</span><span class="sxs-lookup"><span data-stu-id="f729b-173">After you have identified the keys for the storage account you need to remove, use the red '-' icon to the right of the entry to delete it.</span></span> <span data-ttu-id="f729b-174">Ardından __kaydetmek__ yaptığınız değişiklikleri kaydetmek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f729b-174">Then use the __Save__ button to save your changes.</span></span>

5. <span data-ttu-id="f729b-175">Değişiklikler kaydedildikten sonra depolama hesabı ve yeni anahtar değeri kümeye eklemek için betik eylemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="f729b-175">After changes have been saved, use the script action to add the storage account and new key value to the cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="f729b-176">Düşük performans</span><span class="sxs-lookup"><span data-stu-id="f729b-176">Poor performance</span></span>

<span data-ttu-id="f729b-177">Hdınsight kümesi farklı bir bölgede depolama hesabı ise, düşük performans karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f729b-177">If the storage account is in a different region than the HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="f729b-178">Farklı bir bölgeye verilere ağ trafiğini bölgesel Azure veri merkezinin dışındaki ve gecikme getirebilir ortak Internet üzerinden gönderir.</span><span class="sxs-lookup"><span data-stu-id="f729b-178">Accessing data in a different region sends network traffic outside the regional Azure data center and across the public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="f729b-179">Hdınsight kümesi farklı bir bölgede bir depolama hesabı kullanılması desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="f729b-179">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="f729b-180">Ek ücretlere</span><span class="sxs-lookup"><span data-stu-id="f729b-180">Additional charges</span></span>

<span data-ttu-id="f729b-181">Hdınsight kümesi farklı bir bölgede depolama hesabı ise, Azure faturalama hakkında ek çıkış ücretlerini fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f729b-181">If the storage account is in a different region than the HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="f729b-182">Verileri bir bölgesel veri merkezi ayrıldığında bir çıkış ücret uygulanır.</span><span class="sxs-lookup"><span data-stu-id="f729b-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="f729b-183">Farklı bir bölgede başka bir Azure veri merkezi için trafiği hedefleyen olsa bile bu ücretsiz olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="f729b-183">This charge is applied even if the traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="f729b-184">Hdınsight kümesi farklı bir bölgede bir depolama hesabı kullanılması desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="f729b-184">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f729b-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f729b-185">Next steps</span></span>

<span data-ttu-id="f729b-186">Ek depolama hesapları olan bir Hdınsight kümesine ekleme öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="f729b-186">You have learned how to add additional storage accounts to an existing HDInsight cluster.</span></span> <span data-ttu-id="f729b-187">Betik eylemleri hakkında daha fazla bilgi için bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="f729b-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
