---
title: "Depolama çalışırken sonra aaaUpdate Media Services erişim anahtarları | Microsoft Docs"
description: "Bu makaleler nasıl tooupdate Media Services'ı depolama çalışırken sonra erişim anahtarları hakkında rehberlik sağlar."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="80807-103">Depolama erişim tuşlarını çalışırken sonra güncelleştirme medya Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="80807-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="80807-104">Yeni bir Azure Media Services (AMS) hesabı oluşturduğunuzda, bir Azure depolama hesabı başka bir deyişle tooselect toostore medya içeriğinizi kullanılan de istenir.</span><span class="sxs-lookup"><span data-stu-id="80807-104">When you create a new Azure Media Services (AMS) account, you are also asked tooselect an Azure Storage account that is used toostore your media content.</span></span> <span data-ttu-id="80807-105">Birden fazla depolama hesapları tooyour Media Services hesabı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80807-105">You can add more than one storage accounts tooyour Media Services account.</span></span> <span data-ttu-id="80807-106">Bu konuda gösterilmektedir nasıl toorotate depolama anahtarları.</span><span class="sxs-lookup"><span data-stu-id="80807-106">This topic shows how toorotate storage keys.</span></span> <span data-ttu-id="80807-107">Aynı zamanda, nasıl tooa medya hesabı tooadd depolama hesaplarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="80807-107">It also shows how tooadd storage accounts tooa media account.</span></span> 

<span data-ttu-id="80807-108">Bu konuda açıklanan tooperform hello Eylemler, kullanıyor [ARM API'leri](https://docs.microsoft.com/rest/api/media/mediaservice) ve [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="80807-108">tooperform hello actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="80807-109">Daha fazla bilgi için bkz: [nasıl toomanage Azure PowerShell ve Resource Manager kaynaklarıyla](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="80807-109">For more information, see [How toomanage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="80807-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="80807-110">Overview</span></span>

<span data-ttu-id="80807-111">Yeni bir depolama hesabı oluşturduğunuzda Azure kullanılan tooauthenticate olan iki 512 bit depolama erişim tuşu oluşturur erişim tooyour depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="80807-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used tooauthenticate access tooyour storage account.</span></span> <span data-ttu-id="80807-112">Depolama bağlantılarınızı tooperiodically önerilen daha güvenli yeniden oluşturun ve depolama erişim anahtarınızı döndürme tookeep.</span><span class="sxs-lookup"><span data-stu-id="80807-112">tookeep your storage connections more secure, it is recommended tooperiodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="80807-113">Sipariş tooenable kullanarak, toomaintain bağlantıları toohello depolama hesabına erişim anahtarı hello yeniden oluşturmak diğer erişim tuşu iki erişim tuşu (birincil ve ikincil) sağlanır.</span><span class="sxs-lookup"><span data-stu-id="80807-113">Two access keys (primary and secondary) are provided in order tooenable you toomaintain connections toohello storage account using one access key while you regenerate hello other access key.</span></span> <span data-ttu-id="80807-114">Bu yordamı, "çalışırken erişim tuşları" olarak da adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="80807-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="80807-115">Media Services tooit sağlanan bir depolama anahtarı bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="80807-115">Media Services depends on a storage key provided tooit.</span></span> <span data-ttu-id="80807-116">Özellikle, kullanılan toostream veya varlıklarınızı karşıdan hello bulucular hello belirtilen depolama erişim tuşu üzerinde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="80807-116">Specifically, hello locators that are used toostream or download your assets depend on hello specified storage access key.</span></span> <span data-ttu-id="80807-117">AMS hesabı oluşturduğunuzda, bir bağımlılık hello birincil depolama erişim tuşu üzerinde varsayılan olarak alır ancak bir kullanıcı olarak AMS sahip hello depolama anahtarı güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80807-117">When an AMS account is created it takes a dependency on hello primary storage access key by default but as a user you can update hello storage key that AMS has.</span></span> <span data-ttu-id="80807-118">Bu konuda açıklanan adımları izleyerek hangi anahtar toouse toolet Media Services bilmeniz emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="80807-118">You must make sure toolet Media Services know which key toouse by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="80807-119">Birden çok depolama hesabınız yoksa, bu yordamı her bir depolama hesabıyla gerçekleştirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="80807-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="80807-120">Depolama anahtarları döndürme hello sipariş sabit değildir.</span><span class="sxs-lookup"><span data-stu-id="80807-120">hello order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="80807-121">Hello ikincil anahtar ilk döndürün ve birincil anahtar veya bunun tersini de hello.</span><span class="sxs-lookup"><span data-stu-id="80807-121">You can rotate hello secondary key first and then hello primary key or vice versa.</span></span>
>
> <span data-ttu-id="80807-122">Adımları yürütmeden önce bu konuda yapma emin tootest bir üretim hesabı bunları bir üretim öncesi hesabında açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="80807-122">Before executing steps described in this topic on a production account, make sure tootest them on a pre-production account.</span></span>
>

## <a name="steps-toorotate-storage-keys"></a><span data-ttu-id="80807-123">Adımları toorotate depolama anahtarları</span><span class="sxs-lookup"><span data-stu-id="80807-123">Steps toorotate storage keys</span></span> 
 
 1. <span data-ttu-id="80807-124">Değişiklik hello depolama hesabının birincil anahtarını hello powershell cmdlet'i aracılığıyla veya [Azure](https://portal.azure.com/) portal.</span><span class="sxs-lookup"><span data-stu-id="80807-124">Change hello storage account Primary key through hello powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="80807-125">Uygun parametreleri tooforce medya hesap toopick depolama hesabı anahtarlarını yukarı eşitleme AzureRmMediaServiceStorageKeys cmdlet'ini çağırın</span><span class="sxs-lookup"><span data-stu-id="80807-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params tooforce media account toopick up storage account keys</span></span>
 
    <span data-ttu-id="80807-126">Aşağıdaki örnek hello nasıl toosync toostorage hesapları anahtarları gösterir.</span><span class="sxs-lookup"><span data-stu-id="80807-126">hello following example shows how toosync keys toostorage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="80807-127">Bir saat ya da bunu bekleyin.</span><span class="sxs-lookup"><span data-stu-id="80807-127">Wait an hour or so.</span></span> <span data-ttu-id="80807-128">Merhaba akış senaryoları çalıştığınız doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="80807-128">Verify hello streaming scenarios are working.</span></span>
 4. <span data-ttu-id="80807-129">Depolama hesabının ikincil anahtarını hello powershell cmdlet veya Azure portal aracılığıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="80807-129">Change storage account secondary key through hello powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="80807-130">Eşitleme AzureRmMediaServiceStorageKeys powershell uygun parametreleri tooforce medya hesap toopick yeni depolama hesabı anahtarları ayarlama ile çağırın.</span><span class="sxs-lookup"><span data-stu-id="80807-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params tooforce media account toopick up new storage account keys.</span></span> 
 6. <span data-ttu-id="80807-131">Bir saat ya da bunu bekleyin.</span><span class="sxs-lookup"><span data-stu-id="80807-131">Wait an hour or so.</span></span> <span data-ttu-id="80807-132">Merhaba akış senaryoları çalıştığınız doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="80807-132">Verify hello streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="80807-133">Powershell cmdlet örneği</span><span class="sxs-lookup"><span data-stu-id="80807-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="80807-134">Merhaba aşağıdaki örnekte nasıl tooget depolama hesabı hello ve hello AMS hesabıyla eşitleme gösterir.</span><span class="sxs-lookup"><span data-stu-id="80807-134">hello following example demonstrates how tooget hello storage account and sync it with hello AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a><span data-ttu-id="80807-135">Tooyour AMS hesabının adımları tooadd depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="80807-135">Steps tooadd storage accounts tooyour AMS account</span></span>

<span data-ttu-id="80807-136">Merhaba aşağıdaki konu tooyour AMS hesabının nasıl tooadd depolama hesaplarını gösterir: [birden çok depolama hesapları tooa Media Services hesabı ekleme](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="80807-136">hello following topic shows how tooadd storage accounts tooyour AMS account: [Attach multiple storage accounts tooa Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="80807-137">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="80807-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="80807-138">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="80807-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="80807-139">İlgili kaynaklar</span><span class="sxs-lookup"><span data-stu-id="80807-139">Acknowledgments</span></span>
<span data-ttu-id="80807-140">Bu belge oluşturma doğrultusunda katkıda bulunan kişiler aşağıdaki tooacknowledge hello isteriz: Cenk Dingiloglu, Milan Gada Seva Titov.</span><span class="sxs-lookup"><span data-stu-id="80807-140">We would like tooacknowledge hello following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
