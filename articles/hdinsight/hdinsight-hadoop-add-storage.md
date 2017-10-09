---
title: "aaaAdd ek Azure depolama hesapları tooHDInsight | Microsoft Docs"
description: "Nasıl tooan olan bir Hdınsight kümesine tooadd ek Azure depolama hesapları hakkında bilgi edinin."
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
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a><span data-ttu-id="472c2-103">Ek depolama hesapları tooHDInsight Ekle</span><span class="sxs-lookup"><span data-stu-id="472c2-103">Add additional storage accounts tooHDInsight</span></span>

<span data-ttu-id="472c2-104">Nasıl tooHDInsight toouse betik eylemleri tooadd ek Azure depolama hesapları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="472c2-104">Learn how toouse script actions tooadd additional Azure storage accounts tooHDInsight.</span></span> <span data-ttu-id="472c2-105">Merhaba bu belgedeki adımlar bir depolama hesabı tooan varolan Linux tabanlı Hdınsight kümesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="472c2-105">hello steps in this document add a storage account tooan existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="472c2-106">Merhaba bu belgedeki oluşturulduktan sonra ek depolama alanı tooa küme ekleme hakkında bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="472c2-106">hello information in this document is about adding additional storage tooa cluster after it has been created.</span></span> <span data-ttu-id="472c2-107">Küme oluşturma sırasında depolama hesapları ekleme hakkında daha fazla bilgi için bkz: [Hdınsight Hadoop, Spark, Kafka ve daha fazla ile kümelerde ayarlama](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="472c2-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="472c2-108">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="472c2-108">How it works</span></span>

<span data-ttu-id="472c2-109">Bu komut dosyası şu parametreler hello alır:</span><span class="sxs-lookup"><span data-stu-id="472c2-109">This script takes hello following parameters:</span></span>

* <span data-ttu-id="472c2-110">__Azure depolama hesabı adı__: hello depolama hesabı tooadd toohello Hdınsight kümesi hello adı.</span><span class="sxs-lookup"><span data-stu-id="472c2-110">__Azure storage account name__: hello name of hello storage account tooadd toohello HDInsight cluster.</span></span> <span data-ttu-id="472c2-111">Hdınsight, Hello komut dosyasını çalıştırdıktan sonra okuma ve bu depolama hesabında depolanan verileri yazma.</span><span class="sxs-lookup"><span data-stu-id="472c2-111">After running hello script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="472c2-112">__Azure depolama hesabı anahtarı__: bir anahtar, veren erişim toohello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="472c2-112">__Azure storage account key__: A key that grants access toohello storage account.</span></span>

* <span data-ttu-id="472c2-113">__-p__ (isteğe bağlı): belirtilmişse hello anahtarı şifrelenmemiş ve düz metin olarak hello core-site.xml dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="472c2-113">__-p__ (optional): If specified, hello key is not encrypted and is stored in hello core-site.xml file as plain text.</span></span>

<span data-ttu-id="472c2-114">İşleme sırasında hello betik hello aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="472c2-114">During processing, hello script performs hello following actions:</span></span>

* <span data-ttu-id="472c2-115">Merhaba depolama hesabı hello core-site.xml yapılandırmasında hello küme zaten varsa, hello betik çıkar ve başka hiçbir eylem gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="472c2-115">If hello storage account already exists in hello core-site.xml configuration for hello cluster, hello script exits and no further actions are performed.</span></span>

* <span data-ttu-id="472c2-116">Merhaba depolama hesabı var ve başlangıç anahtarı kullanılarak erişilebilir doğrular.</span><span class="sxs-lookup"><span data-stu-id="472c2-116">Verifies that hello storage account exists and can be accessed using hello key.</span></span>

* <span data-ttu-id="472c2-117">Başlangıç anahtarı Hello küme kimlik bilgilerini kullanarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="472c2-117">Encrypts hello key using hello cluster credential.</span></span>

* <span data-ttu-id="472c2-118">Merhaba depolama hesabı toohello core-site.xml dosyasının ekler.</span><span class="sxs-lookup"><span data-stu-id="472c2-118">Adds hello storage account toohello core-site.xml file.</span></span>

* <span data-ttu-id="472c2-119">Durdurur ve hello Oozie, YARN, MapReduce2 ve HDFS hizmetleri yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="472c2-119">Stops and restarts hello Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="472c2-120">Durdurma ve bu hizmetleri başlatma toouse hello yeni depolama hesabı sağlar.</span><span class="sxs-lookup"><span data-stu-id="472c2-120">Stopping and starting these services allows them toouse hello new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="472c2-121">Merhaba Hdınsight kümesi farklı bir konumda bir depolama hesabıyla desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="472c2-121">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="hello-script"></a><span data-ttu-id="472c2-122">Merhaba komut dosyası</span><span class="sxs-lookup"><span data-stu-id="472c2-122">hello script</span></span>

<span data-ttu-id="472c2-123">__Komut dosyası konumu__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="472c2-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="472c2-124">__Gereksinimleri__:</span><span class="sxs-lookup"><span data-stu-id="472c2-124">__Requirements__:</span></span>

* <span data-ttu-id="472c2-125">Merhaba üzerinde Hello betik uygulanan __baş düğümler__.</span><span class="sxs-lookup"><span data-stu-id="472c2-125">hello script must be applied on hello __Head nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="472c2-126">toouse hello komut dosyası</span><span class="sxs-lookup"><span data-stu-id="472c2-126">toouse hello script</span></span>

<span data-ttu-id="472c2-127">Bu komut dosyası veya Azure CLI 1.0 hello hello Azure portal, Azure PowerShell kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="472c2-127">This script can be used from hello Azure portal, Azure PowerShell, or hello Azure CLI 1.0.</span></span> <span data-ttu-id="472c2-128">Daha fazla bilgi için bkz: Merhaba [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) belge.</span><span class="sxs-lookup"><span data-stu-id="472c2-128">For more information, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="472c2-129">Merhaba özelleştirme belgede sağlanan hello adımları kullanırken, bilgi tooapply aşağıdaki hello bu komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="472c2-129">When using hello steps provided in hello customization document, use hello following information tooapply this script:</span></span>
>
> * <span data-ttu-id="472c2-130">Bu komut dosyası (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh) için URI hello herhangi örnek betik eylemi URI değiştirin.</span><span class="sxs-lookup"><span data-stu-id="472c2-130">Replace any example script action URI with hello URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="472c2-131">Örnek parametreleri hello Azure depolama hesabı adı ve hello depolama hesabı toobe eklenen toohello kümesinin anahtarı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="472c2-131">Replace any example parameters with hello Azure storage account name and key of hello storage account toobe added toohello cluster.</span></span> <span data-ttu-id="472c2-132">Azure portal kullanarak Merhaba, bu parametreler boşlukla ayrılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="472c2-132">If using hello Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="472c2-133">Bu komut dosyası olarak toomark gerekmez __kalıcı__, doğrudan hello Ambari yapılandırma hello kümesi için güncelleştirmeler.</span><span class="sxs-lookup"><span data-stu-id="472c2-133">You do not need toomark this script as __Persisted__, as it directly updates hello Ambari configuration for hello cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="472c2-134">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="472c2-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="472c2-135">Azure portalından veya Araçlar görüntülenmeyen depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="472c2-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="472c2-136">Görüntüleme hello Hdınsight küme hello Azure portal, hello seçme __depolama hesapları__ altında girdisi __özellikleri__ bu betik eylemi eklenen depolama hesaplarına görüntülemez.</span><span class="sxs-lookup"><span data-stu-id="472c2-136">When viewing hello HDInsight cluster in hello Azure portal, selecting hello __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="472c2-137">Azure PowerShell ve Azure CLI hello ek depolama alanı hesabı ya da görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="472c2-137">Azure PowerShell and Azure CLI do not display hello additional storage account either.</span></span>

<span data-ttu-id="472c2-138">Merhaba betik hello core-site.xml yapılandırma hello kümesi için yalnızca değiştirdiğinden hello depolama bilgiler görüntülenmiyor.</span><span class="sxs-lookup"><span data-stu-id="472c2-138">hello storage information isn't displayed because hello script only modifies hello core-site.xml configuration for hello cluster.</span></span> <span data-ttu-id="472c2-139">Bu bilgiler, Azure yönetim API'leri kullanılarak hello küme bilgilerini alırken kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="472c2-139">This information is not used when retrieving hello cluster information using Azure management APIs.</span></span>

<span data-ttu-id="472c2-140">Bu komut, kullanım hello Ambari REST API kullanarak toohello küme tooview depolama hesabı bilgilerini eklendi.</span><span class="sxs-lookup"><span data-stu-id="472c2-140">tooview storage account information added toohello cluster using this script, use hello Ambari REST API.</span></span> <span data-ttu-id="472c2-141">Aşağıdaki komutları tooretrieve hello kümeniz için bu bilgileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="472c2-141">Use hello following commands tooretrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="472c2-142">Ayarlama `$clusterName` hello Hdınsight kümesi toohello adı.</span><span class="sxs-lookup"><span data-stu-id="472c2-142">Set `$clusterName` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="472c2-143">Ayarlama `$storageAccountName` hello depolama hesabının toohello adı.</span><span class="sxs-lookup"><span data-stu-id="472c2-143">Set `$storageAccountName` toohello name of hello storage account.</span></span> <span data-ttu-id="472c2-144">İstendiğinde, hello küme oturum açma (Yönetici) ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="472c2-144">When prompted, enter hello cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="472c2-145">Ayarlama `$PASSWORD` toohello küme oturum açma (Yönetici) hesap parolası.</span><span class="sxs-lookup"><span data-stu-id="472c2-145">Set `$PASSWORD` toohello cluster login (admin) account password.</span></span> <span data-ttu-id="472c2-146">Ayarlama `$CLUSTERNAME` hello Hdınsight kümesi toohello adı.</span><span class="sxs-lookup"><span data-stu-id="472c2-146">Set `$CLUSTERNAME` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="472c2-147">Ayarlama `$STORAGEACCOUNTNAME` hello depolama hesabının toohello adı.</span><span class="sxs-lookup"><span data-stu-id="472c2-147">Set `$STORAGEACCOUNTNAME` toohello name of hello storage account.</span></span>
>
> <span data-ttu-id="472c2-148">Bu örnekte [curl (http://curl.haxx.se/)](http://curl.haxx.se/) ve [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve ve parse JSON verileri.</span><span class="sxs-lookup"><span data-stu-id="472c2-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve and parse JSON data.</span></span>

<span data-ttu-id="472c2-149">Bu komut, kullanırken değiştirin __CLUSTERNAME__ hello Hdınsight kümesi hello adı.</span><span class="sxs-lookup"><span data-stu-id="472c2-149">When using this command, replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="472c2-150">Değiştir __parola__ hello küme oturum açma parolasını hello HTTP ile.</span><span class="sxs-lookup"><span data-stu-id="472c2-150">Replace __PASSWORD__ with hello HTTP login password for hello cluster.</span></span> <span data-ttu-id="472c2-151">Değiştir __STORAGEACCOUNT__ hello adıyla hello depolama hesabı betik eylemi kullanarak eklendi.</span><span class="sxs-lookup"><span data-stu-id="472c2-151">Replace __STORAGEACCOUNT__ with hello name of hello storage account added using script action.</span></span> <span data-ttu-id="472c2-152">Bu komuttan döndürülen bilgi metnini izleyen benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="472c2-152">Information returned from this command appears similar toohello following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="472c2-153">Bu metin kullanılan şifreli bir anahtar örneğidir tooaccess hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="472c2-153">This text is an example of an encrypted key, which is used tooaccess hello storage account.</span></span>

### <a name="unable-tooaccess-storage-after-changing-key"></a><span data-ttu-id="472c2-154">Anahtar değiştirdikten sonra oluşturulamıyor tooaccess depolama</span><span class="sxs-lookup"><span data-stu-id="472c2-154">Unable tooaccess storage after changing key</span></span>

<span data-ttu-id="472c2-155">Bir depolama hesabının hello anahtarı değiştirirseniz, Hdınsight hello depolama hesabı artık erişemez.</span><span class="sxs-lookup"><span data-stu-id="472c2-155">If you change hello key for a storage account, HDInsight can no longer access hello storage account.</span></span> <span data-ttu-id="472c2-156">Hdınsight anahtarı önbelleğe alınmış bir kopyasını hello core-site.xml hello küme için kullanır.</span><span class="sxs-lookup"><span data-stu-id="472c2-156">HDInsight uses a cached copy of key in hello core-site.xml for hello cluster.</span></span> <span data-ttu-id="472c2-157">Önbelleğe alınan bu kopya güncelleştirilmiş toomatch hello yeni anahtarı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="472c2-157">This cached copy must be updated toomatch hello new key.</span></span>

<span data-ttu-id="472c2-158">Merhaba betik eylemi yeniden çalıştıran mu __değil__ hello depolama hesabı için bir giriş zaten varsa hello betik toosee denetler gibi hello anahtar güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="472c2-158">Running hello script action again does __not__ update hello key, as hello script checks toosee if an entry for hello storage account already exists.</span></span> <span data-ttu-id="472c2-159">Bir giriş zaten varsa, herhangi bir değişiklik yapmaz.</span><span class="sxs-lookup"><span data-stu-id="472c2-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="472c2-160">Bu soruna geçici bir çözüm toowork, varolan bir girişi hello hello depolama hesabı için kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="472c2-160">toowork around this problem, you must remove hello existing entry for hello storage account.</span></span> <span data-ttu-id="472c2-161">Aşağıdaki adımları tooremove hello varolan bir girişi hello kullan:</span><span class="sxs-lookup"><span data-stu-id="472c2-161">Use hello following steps tooremove hello existing entry:</span></span>

1. <span data-ttu-id="472c2-162">Bir web tarayıcısında Hdınsight kümenizin hello Ambari Web kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="472c2-162">In a web browser, open hello Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="472c2-163">Merhaba URI https://CLUSTERNAME.azurehdinsight.net ' dir.</span><span class="sxs-lookup"><span data-stu-id="472c2-163">hello URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="472c2-164">Değiştir __CLUSTERNAME__ kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="472c2-164">Replace __CLUSTERNAME__ with hello name of your cluster.</span></span>

    <span data-ttu-id="472c2-165">İstendiğinde, kümeniz için hello HTTP oturum açma kullanıcısı ve parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="472c2-165">When prompted, enter hello HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="472c2-166">Merhaba hello sayfasının hello soldaki hizmetlerin listesinden __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="472c2-166">From hello list of services on hello left of hello page, select __HDFS__.</span></span> <span data-ttu-id="472c2-167">Merhaba seçip __yapılandırmalar__ hello sayfasının hello Center'da sekmesi.</span><span class="sxs-lookup"><span data-stu-id="472c2-167">Then select hello __Configs__ tab in hello center of hello page.</span></span>

3. <span data-ttu-id="472c2-168">Merhaba, __filtre...__  değeri alanına, __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="472c2-168">In hello __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="472c2-169">Bu toohello kümeye eklenmiş herhangi bir ek depolama alanı hesabı girişlerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="472c2-169">This returns entries for any additional storage accounts that have been added toohello cluster.</span></span> <span data-ttu-id="472c2-170">İki tür giriş vardır; __keyprovider__ ve __anahtar__.</span><span class="sxs-lookup"><span data-stu-id="472c2-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="472c2-171">Her ikisi de hello depolama hesabı hello anahtar adının bir parçası olarak hello adını içerir.</span><span class="sxs-lookup"><span data-stu-id="472c2-171">Both contain hello name of hello storage account as part of hello key name.</span></span>

    <span data-ttu-id="472c2-172">Merhaba adlı bir depolama hesabı örnek girdileri verilmiştir __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="472c2-172">hello following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="472c2-173">Merhaba kırmızı tooremove ihtiyacınız hello depolama hesabı için hello anahtarları tanımladıktan sonra kullanmak '-' hello girişi toodelete sağında simgesi toohello.</span><span class="sxs-lookup"><span data-stu-id="472c2-173">After you have identified hello keys for hello storage account you need tooremove, use hello red '-' icon toohello right of hello entry toodelete it.</span></span> <span data-ttu-id="472c2-174">Hello kullan __kaydetmek__ toosave değişikliklerinizi düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="472c2-174">Then use hello __Save__ button toosave your changes.</span></span>

5. <span data-ttu-id="472c2-175">Değişiklikler kaydedildikten sonra hello betik eylemi tooadd hello depolama hesabı ve yeni anahtar değeri toohello küme kullanın.</span><span class="sxs-lookup"><span data-stu-id="472c2-175">After changes have been saved, use hello script action tooadd hello storage account and new key value toohello cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="472c2-176">Düşük performans</span><span class="sxs-lookup"><span data-stu-id="472c2-176">Poor performance</span></span>

<span data-ttu-id="472c2-177">Merhaba depolama hesabı hello Hdınsight kümesi farklı bir bölgede ise, düşük performans karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="472c2-177">If hello storage account is in a different region than hello HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="472c2-178">Bir farklı bir bölgeye gönderir ve ağ trafiğini hello bölgesel Azure veri merkezi dışında çapraz erişilirken verilerde gecikme getirebilir genel internet hello.</span><span class="sxs-lookup"><span data-stu-id="472c2-178">Accessing data in a different region sends network traffic outside hello regional Azure data center and across hello public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="472c2-179">Merhaba Hdınsight kümesi farklı bir bölgede bir depolama hesabı kullanılması desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="472c2-179">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="472c2-180">Ek ücretlere</span><span class="sxs-lookup"><span data-stu-id="472c2-180">Additional charges</span></span>

<span data-ttu-id="472c2-181">Merhaba depolama hesabı Hdınsight kümesi hello daha farklı bir bölgede ise, Azure faturalama hakkında ek çıkış ücretlerini fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="472c2-181">If hello storage account is in a different region than hello HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="472c2-182">Verileri bir bölgesel veri merkezi ayrıldığında bir çıkış ücret uygulanır.</span><span class="sxs-lookup"><span data-stu-id="472c2-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="472c2-183">Merhaba trafik farklı bir bölgede başka bir Azure veri merkezi için hedeflenen olsa bile bu ücretsiz olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="472c2-183">This charge is applied even if hello traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="472c2-184">Merhaba Hdınsight kümesi farklı bir bölgede bir depolama hesabı kullanılması desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="472c2-184">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="472c2-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="472c2-185">Next steps</span></span>

<span data-ttu-id="472c2-186">Nasıl tooan olan bir Hdınsight kümesine tooadd ek depolama hesapları öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="472c2-186">You have learned how tooadd additional storage accounts tooan existing HDInsight cluster.</span></span> <span data-ttu-id="472c2-187">Betik eylemleri hakkında daha fazla bilgi için bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="472c2-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
