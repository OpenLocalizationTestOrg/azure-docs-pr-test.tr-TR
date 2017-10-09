---
title: "aaaRead NSG akış günlükleri | Microsoft Docs"
description: "Bu makalede nasıl tooparse NSG akış günlükleri gösterir"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: gwallace
ms.openlocfilehash: b4f0f64639c7b2a6b4db50e54d15056bfd809e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="read-nsg-flow-logs"></a><span data-ttu-id="c0305-103">Okuma NSG akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="c0305-103">Read NSG flow logs</span></span>

<span data-ttu-id="c0305-104">Tooread NSG akışı girişlerini PowerShell ile nasıl oturum öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c0305-104">Learn how tooread NSG flow logs entries with PowerShell.</span></span>

<span data-ttu-id="c0305-105">NSG akış günlükleri, bir depolama hesabında depolanır [blok blobları](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span><span class="sxs-lookup"><span data-stu-id="c0305-105">NSG flow logs are stored in a storage account in [block blobs](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span></span> <span data-ttu-id="c0305-106">Blok blobları, daha küçük bloklarını yapılır.</span><span class="sxs-lookup"><span data-stu-id="c0305-106">Block blobs are made up of smaller blocks.</span></span> <span data-ttu-id="c0305-107">Her günlük saatte oluşturulan ayrı blok blob ' dir.</span><span class="sxs-lookup"><span data-stu-id="c0305-107">Each log is a separate block blob that is generated every hour.</span></span> <span data-ttu-id="c0305-108">Yeni günlükler saatte oluşturulan, hello günlükleri yeni girişlerle birkaç dakikada hello en son verilerle güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c0305-108">New logs are generated every hour, hello logs are updated with new entries every few minutes with hello latest data.</span></span> <span data-ttu-id="c0305-109">Bu makalede hello tooread bölümlerini günlüklerini nasıl gerçekleştiğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c0305-109">In this article you learn how tooread portions of hello flow logs.</span></span>

## <a name="scenario"></a><span data-ttu-id="c0305-110">Senaryo</span><span class="sxs-lookup"><span data-stu-id="c0305-110">Scenario</span></span>

<span data-ttu-id="c0305-111">Senaryo aşağıdaki hello bir depolama hesabında depolanan bir örnek akış günlüğü vardır.</span><span class="sxs-lookup"><span data-stu-id="c0305-111">In hello following scenario, you have an example flow log that is stored in a storage account.</span></span> <span data-ttu-id="c0305-112">nasıl seçmeli olarak hello son olayları NSG akış günlüklerine okuyabilirsiniz adım.</span><span class="sxs-lookup"><span data-stu-id="c0305-112">we step through how you can selectively read hello latest events in NSG flow logs.</span></span> <span data-ttu-id="c0305-113">Bu makalede PowerShell kullanacağız, ancak hello makalesinde açıklanan hello kavramları sınırlı toohello programlama dili olup olmadığı ve Azure depolama API'leri hello tarafından desteklenen geçerli tooall diller</span><span class="sxs-lookup"><span data-stu-id="c0305-113">In this article we will use PowerShell, however, hello concepts discussed in hello article are not limited toohello programming language and are applicable tooall languages supported by hello Azure Storage APIs</span></span>

## <a name="setup"></a><span data-ttu-id="c0305-114">Kurulum</span><span class="sxs-lookup"><span data-stu-id="c0305-114">Setup</span></span>

<span data-ttu-id="c0305-115">Başlamadan önce ağ güvenlik grubu akış hesabınızda bir veya daha çok ağ güvenlik grupları etkin günlüğü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0305-115">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="c0305-116">Akış günlükleri ağ güvenliği etkinleştirme yönergeleri için aşağıdaki makaleye bakın toohello bakın: [ağ güvenlik grupları için giriş tooflow günlüğü](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0305-116">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="retrieve-hello-block-list"></a><span data-ttu-id="c0305-117">Merhaba blok listesini alma</span><span class="sxs-lookup"><span data-stu-id="c0305-117">Retrieve hello block list</span></span>

<span data-ttu-id="c0305-118">tooquery hello NSG akış oturum hello içinde blob ve liste hello blok hello değişkenleri PowerShell ayarlar aşağıdaki hello [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) blok blobu.</span><span class="sxs-lookup"><span data-stu-id="c0305-118">hello following PowerShell sets up hello variables needed tooquery hello NSG flow log blob and list hello blocks within hello [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) block blob.</span></span> <span data-ttu-id="c0305-119">Merhaba betik toocontain ortamınız için geçerli değerler güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c0305-119">Update hello script toocontain valid values for your environment.</span></span>

```powershell
# hello SubscriptionID toouse
$subscriptionId = "00000000-0000-0000-0000-000000000000"

# Resource group that contains hello Network Security Group
$resourceGroupName = "<resourceGroupName>"

# hello name of hello Network Security Group
$nsgName = "NSGName"

# hello storage account name that contains hello NSG logs
$storageAccountName = "<storageAccountName>" 

# hello date and time for hello log toobe queried, logs are stored in hour intervals.
[datetime]$logtime = "06/16/2017 20:00"

# Retrieve hello primary storage account key tooaccess hello NSG logs
$StorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName).Value[0]

# Setup a new storage context toobe used tooquery hello logs
$ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

# Container name used by NSG flow logs
$ContainerName = "insights-logs-networksecuritygroupflowevent"

# Name of hello blob that contains hello NSG flow log
$BlobName = "resourceId=/SUBSCRIPTIONS/${subscriptionId}/RESOURCEGROUPS/${resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/${nsgName}/y=$($logtime.Year)/m=$(($logtime).ToString("MM"))/d=$(($logtime).ToString("dd"))/h=$(($logtime).ToString("HH"))/m=00/PT1H.json"

# Gets hello storage blog
$Blob = Get-AzureStorageBlob -Context $ctx -Container $ContainerName -Blob $BlobName

# Gets hello block blog of type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from hello storage blob
$CloudBlockBlob = [Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob] $Blob.ICloudBlob

# Stores hello block list in a variable from hello block blob.
$blockList = $CloudBlockBlob.DownloadBlockList()
```

<span data-ttu-id="c0305-120">Merhaba `$blockList` değişkeni hello blob hello blokları listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="c0305-120">hello `$blockList` variable returns a list of hello blocks in hello blob.</span></span> <span data-ttu-id="c0305-121">Her blok blobu en az iki blokları içerir.</span><span class="sxs-lookup"><span data-stu-id="c0305-121">Each block blob contains at least two blocks.</span></span>  <span data-ttu-id="c0305-122">Merhaba ilk Blok uzunluğu olan `21` bayt bu bloğu hello json günlüğünün köşeli açma hello içerir.</span><span class="sxs-lookup"><span data-stu-id="c0305-122">hello first block has a length of `21` bytes, this block contains hello opening brackets of hello json log.</span></span> <span data-ttu-id="c0305-123">Merhaba diğer blok hello kapanış köşeli ve uzunluğuna sahip `9` bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c0305-123">hello other block is hello closing brackets and has a length of `9` bytes.</span></span>  <span data-ttu-id="c0305-124">Gördüğünüz gibi örnek günlük aşağıdaki hello yedi girişleri, içinde her bir girişe olan içeriyor.</span><span class="sxs-lookup"><span data-stu-id="c0305-124">As you can see hello following example log has seven entries in it, each being an individual entry.</span></span> <span data-ttu-id="c0305-125">Tüm yeni girişler hello günlüğüne toohello sona hello son blok hemen önce eklenir.</span><span class="sxs-lookup"><span data-stu-id="c0305-125">All new entries in hello log are added toohello end right before hello final block.</span></span>

```
Name                                         Length Committed
----                                         ------ ---------
ZDk5MTk5N2FkNGE0MmY5MTk5ZWViYjA0YmZhODRhYzY=     21      True
NzQxNDA5MTRhNDUzMGI2M2Y1MDMyOWZlN2QwNDZiYzQ=   2685      True
ODdjM2UyMWY3NzFhZTU3MmVlMmU5MDNlOWEwNWE3YWY=   2586      True
ZDU2MjA3OGQ2ZDU3MjczMWQ4MTRmYWNhYjAzOGJkMTg=   2688      True
ZmM3ZWJjMGQ0ZDA1ODJlOWMyODhlOWE3MDI1MGJhMTc=   2775      True
ZGVkYTc4MzQzNjEyMzlmZWE5MmRiNjc1OWE5OTc0OTQ=   2676      True
ZmY2MjUzYTIwYWIyOGU1OTA2ZDY1OWYzNmY2NmU4ZTY=   2777      True
Mzk1YzQwM2U0ZWY1ZDRhOWFlMTNhYjQ3OGVhYmUzNjk=   2675      True
ZjAyZTliYWE3OTI1YWZmYjFmMWI0MjJhNzMxZTI4MDM=      9      True
```

## <a name="read-hello-block-blob"></a><span data-ttu-id="c0305-126">Okuma hello blok blobu</span><span class="sxs-lookup"><span data-stu-id="c0305-126">Read hello block blob</span></span>

<span data-ttu-id="c0305-127">Tooread hello sonraki ihtiyacımız `$blocklist` değişken tooretrieve hello veri.</span><span class="sxs-lookup"><span data-stu-id="c0305-127">Next we need tooread hello `$blocklist` variable tooretrieve hello data.</span></span> <span data-ttu-id="c0305-128">Bu örnekte, biz hello engelleme yineleme her bloğundan hello bayt okuma ve bir dizi yazı.</span><span class="sxs-lookup"><span data-stu-id="c0305-128">In this example we iterate through hello blocklist, read hello bytes from each block and story them in an array.</span></span> <span data-ttu-id="c0305-129">Merhaba kullanırız [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) yöntemi tooretrieve hello veri.</span><span class="sxs-lookup"><span data-stu-id="c0305-129">We use hello [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) method tooretrieve hello data.</span></span>

```powershell
# Set hello size of hello byte array toohello largest block
$maxvalue = ($blocklist | measure Length -Maximum).Maximum

# Create an array toostore values in
$valuearray = @()

# Define hello starting index tootrack hello current block being read
$index = 0

# Loop through each block in hello block list
for($i=0; $i -lt $blocklist.count; $i++)
{

# Create a byte array object toostory hello bytes from hello block
$downloadArray = New-Object -TypeName byte[] -ArgumentList $maxvalue

# Download hello data into hello ByteArray, starting with hello current index, for hello number of bytes in hello current block. Index is increased by 3 when reading tooremove preceding comma.
$CloudBlockBlob.DownloadRangeToByteArray($downloadArray,0,$index+3,$($blockList[$i].Length-1)) | Out-Null

# Increment hello index by adding hello current block length toohello previous index
$index = $index + $blockList[$i].Length

# Retrieve hello string from hello byte array

$value = [System.Text.Encoding]::ASCII.GetString($downloadArray)

# Add hello log entry toohello value array
$valuearray += $value
}
```

<span data-ttu-id="c0305-130">Şimdi hello `$valuearray` dizi blokların hello dize değerini içeriyor.</span><span class="sxs-lookup"><span data-stu-id="c0305-130">Now hello `$valuearray` array contains hello string value of each block.</span></span> <span data-ttu-id="c0305-131">tooverify hello girdisi, get hello ikinci toohello son değer çalıştırarak hello dizisinden `$valuearray[$valuearray.Length-2]`.</span><span class="sxs-lookup"><span data-stu-id="c0305-131">tooverify hello entry, get hello second toohello last value from hello array by running `$valuearray[$valuearray.Length-2]`.</span></span> <span data-ttu-id="c0305-132">Merhaba son yalnızca hello kapanış ayracı değerdir istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0305-132">We do not want hello last value is just hello closing bracket.</span></span>

<span data-ttu-id="c0305-133">Bu değer Hello sonuçları aşağıdaki örneğine hello gösterilir:</span><span class="sxs-lookup"><span data-stu-id="c0305-133">hello results of this value are shown in hello following example:</span></span>

```json
        {
             "time": "2017-06-16T20:59:43.7340000Z",
             "systemId": "5f4d02d3-a7d0-4ed4-9ce8-c0ae9377951c",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/CONTOSORG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/CONTOSONSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_AllowInternetOutBound","flows":[{"mac":"000D3A18077E","flowTuples":["1497646722,10.0.0.4,168.62.32.14,44904,443,T,O,A","1497646722,10.0.0.4,52.240.48.24,45218,443,T,O,A","1497646725,10.
0.0.4,168.62.32.14,44910,443,T,O,A","1497646725,10.0.0.4,52.240.48.24,45224,443,T,O,A","1497646728,10.0.0.4,168.62.32.14,44916,443,T,O,A","1497646728,10.0.0.4,52.240.48.24,45230,443,T,O,A","1497646732,10.0.0.4,168.62.32.14,44922,443,T,O,A","14976
46732,10.0.0.4,52.240.48.24,45236,443,T,O,A","1497646735,10.0.0.4,168.62.32.14,44928,443,T,O,A","1497646735,10.0.0.4,52.240.48.24,45242,443,T,O,A","1497646738,10.0.0.4,168.62.32.14,44934,443,T,O,A","1497646738,10.0.0.4,52.240.48.24,45248,443,T,O,
A","1497646742,10.0.0.4,168.62.32.14,44942,443,T,O,A","1497646742,10.0.0.4,52.240.48.24,45256,443,T,O,A","1497646745,10.0.0.4,168.62.32.14,44948,443,T,O,A","1497646745,10.0.0.4,52.240.48.24,45262,443,T,O,A","1497646749,10.0.0.4,168.62.32.14,44954
,443,T,O,A","1497646749,10.0.0.4,52.240.48.24,45268,443,T,O,A","1497646753,10.0.0.4,168.62.32.14,44960,443,T,O,A","1497646753,10.0.0.4,52.240.48.24,45274,443,T,O,A","1497646756,10.0.0.4,168.62.32.14,44966,443,T,O,A","1497646756,10.0.0.4,52.240.48
.24,45280,443,T,O,A","1497646759,10.0.0.4,168.62.32.14,44972,443,T,O,A","1497646759,10.0.0.4,52.240.48.24,45286,443,T,O,A","1497646763,10.0.0.4,168.62.32.14,44978,443,T,O,A","1497646763,10.0.0.4,52.240.48.24,45292,443,T,O,A","1497646766,10.0.0.4,
168.62.32.14,44984,443,T,O,A","1497646766,10.0.0.4,52.240.48.24,45298,443,T,O,A","1497646769,10.0.0.4,168.62.32.14,44990,443,T,O,A","1497646769,10.0.0.4,52.240.48.24,45304,443,T,O,A","1497646773,10.0.0.4,168.62.32.14,44996,443,T,O,A","1497646773,
10.0.0.4,52.240.48.24,45310,443,T,O,A","1497646776,10.0.0.4,168.62.32.14,45002,443,T,O,A","1497646776,10.0.0.4,52.240.48.24,45316,443,T,O,A","1497646779,10.0.0.4,168.62.32.14,45008,443,T,O,A","1497646779,10.0.0.4,52.240.48.24,45322,443,T,O,A"]}]}
,{"rule":"DefaultRule_DenyAllInBound","flows":[]},{"rule":"UserRule_ssh-rule","flows":[]},{"rule":"UserRule_web-rule","flows":[{"mac":"000D3A18077E","flowTuples":["1497646738,13.82.225.93,10.0.0.4,1180,80,T,I,A","1497646750,13.82.225.93,10.0.0.4,
1184,80,T,I,A","1497646768,13.82.225.93,10.0.0.4,1181,80,T,I,A","1497646780,13.82.225.93,10.0.0.4,1336,80,T,I,A"]}]}]}
        }
```

<span data-ttu-id="c0305-134">Bu senaryo tooparse hello tüm günlük gerek kalmadan tooread girişleri NSG günlüklerini nasıl gerçekleştiğini bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="c0305-134">This scenario is an example of how tooread entries in NSG flow logs without having tooparse hello entire log.</span></span> <span data-ttu-id="c0305-135">Merhaba blok Kimliğini kullanarak veya hello blok blobu depolanan blokları hello uzunluğu izleme yazıldığı şekilde hello günlüğünde yeni girişleri okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="c0305-135">You can read new entries in hello log as they are written by using hello block ID or by tracking hello length of blocks stored in hello block blob.</span></span> <span data-ttu-id="c0305-136">Bu, yeni girişler yalnızca hello tooread sağlar.</span><span class="sxs-lookup"><span data-stu-id="c0305-136">This allows you tooread only hello new entries.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c0305-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c0305-137">Next steps</span></span>

<span data-ttu-id="c0305-138">Ziyaret [açık kaynaklı Araçları'nı kullanarak Azure Ağ İzleyicisi NSG akış günlükleri görselleştirmek](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) toolearn diğer yolları tooview NSG hakkında daha fazla akış günlükleri.</span><span class="sxs-lookup"><span data-stu-id="c0305-138">Visit [visualize Azure Network Watcher NSG flow logs using open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) toolearn more about other ways tooview NSG flow logs.</span></span>

<span data-ttu-id="c0305-139">toolearn depolama BLOB'ları hakkında daha fazla ziyaret edin: [Azure işlevleri Blob Depolama bağlamaları](../azure-functions/functions-bindings-storage-blob.md)</span><span class="sxs-lookup"><span data-stu-id="c0305-139">toolearn more about storage blobs visit: [Azure Functions Blob storage bindings](../azure-functions/functions-bindings-storage-blob.md)</span></span>
