---
title: "aaaCreate bir dışa aktarma işi için Azure içeri/dışarı aktarma | Microsoft Docs"
description: "Nasıl toocreate bir dışa aktarma işi Merhaba Microsoft Azure içeri/dışarı aktarma hizmeti hakkında bilgi edinin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a><span data-ttu-id="4aad6-103">Hello Azure içeri/dışarı aktarma hizmeti için bir dışa aktarma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4aad6-103">Creating an export job for hello Azure Import/Export service</span></span>
<span data-ttu-id="4aad6-104">Bir dışarı aktarma işinin hello REST API kullanarak hello Microsoft Azure içeri/dışarı aktarma hizmeti oluşturma hello aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="4aad6-104">Creating an export job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="4aad6-105">Merhaba seçerek tooexport BLOB '.</span><span class="sxs-lookup"><span data-stu-id="4aad6-105">Selecting hello blobs tooexport.</span></span>

-   <span data-ttu-id="4aad6-106">Bir sevkiyat konum alma.</span><span class="sxs-lookup"><span data-stu-id="4aad6-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="4aad6-107">Merhaba dışarı aktarma işini oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="4aad6-107">Creating hello export job.</span></span>

-   <span data-ttu-id="4aad6-108">Boş sürücüleri tooMicrosoft desteklenen taşıyıcı hizmeti üzerinden aktarma.</span><span class="sxs-lookup"><span data-stu-id="4aad6-108">Shipping your empty drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="4aad6-109">Merhaba dışarı aktarma işini hello paket bilgilerle güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="4aad6-109">Updating hello export job with hello package information.</span></span>

-   <span data-ttu-id="4aad6-110">Microsoft'tan geri alma hello sürücüler.</span><span class="sxs-lookup"><span data-stu-id="4aad6-110">Receiving hello drives back from Microsoft.</span></span>

 <span data-ttu-id="4aad6-111">Bkz: [hello Windows Azure içeri/dışarı aktarma hizmeti tooTransfer veri tooBlob depolama kullanarak](storage-import-export-service.md) genel bir bakış hello içeri/dışarı aktarma hizmeti ve gösteren bir öğretici için nasıl toouse hello [Azure portal](https://portal.azure.com/) toocreate alma yönetmek ve işleri dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="4aad6-111">See [Using hello Windows Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="selecting-blobs-tooexport"></a><span data-ttu-id="4aad6-112">BLOB'ları tooexport seçme</span><span class="sxs-lookup"><span data-stu-id="4aad6-112">Selecting blobs tooexport</span></span>
 <span data-ttu-id="4aad6-113">bir dışarı aktarma işinin toocreate, tooprovide BLOB storage hesabınızdan tooexport istediğiniz listesini gerekir.</span><span class="sxs-lookup"><span data-stu-id="4aad6-113">toocreate an export job, you will need tooprovide a list of blobs that you want tooexport from your storage account.</span></span> <span data-ttu-id="4aad6-114">Birkaç yolu vardır tooselect BLOB'ların verilen toobe:</span><span class="sxs-lookup"><span data-stu-id="4aad6-114">There are a few ways tooselect blobs toobe exported:</span></span>

-   <span data-ttu-id="4aad6-115">Tek bir blob ve tüm alt anlık görüntü göreli blob yolu tooselect kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4aad6-115">You can use a relative blob path tooselect a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="4aad6-116">Kendi anlık görüntüleri hariç olmak üzere tek bir blob göreli blob yolu tooselect kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4aad6-116">You can use a relative blob path tooselect a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="4aad6-117">Göreli blob yolu ve bir anlık görüntü saati tooselect bir anlık görüntüsü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4aad6-117">You can use a relative blob path and a snapshot time tooselect a single snapshot.</span></span>

-   <span data-ttu-id="4aad6-118">Bir blob öneki tooselect öneki verilen hello ile tüm BLOB'ları ve anlık görüntüleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4aad6-118">You can use a blob prefix tooselect all blobs and snapshots with hello given prefix.</span></span>

-   <span data-ttu-id="4aad6-119">Tüm BLOB'ları ve anlık görüntüleri hello depolama hesabındaki dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4aad6-119">You can export all blobs and snapshots in hello storage account.</span></span>

 <span data-ttu-id="4aad6-120">Merhaba BLOB'ların tooexport belirtme hakkında daha fazla bilgi için bkz: [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) işlemi.</span><span class="sxs-lookup"><span data-stu-id="4aad6-120">For more information about specifying blobs tooexport, see hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="4aad6-121">Sevkiyat Konumunuz alma</span><span class="sxs-lookup"><span data-stu-id="4aad6-121">Obtaining your shipping location</span></span>
<span data-ttu-id="4aad6-122">Bir dışarı aktarma işinin oluşturmadan önce tooobtain sevkiyat konum adı ve adres tarafından arama hello ihtiyacınız [alma konumu](https://portal.azure.com) veya [listesi konumları](/rest/api/storageimportexport/listlocations) işlemi.</span><span class="sxs-lookup"><span data-stu-id="4aad6-122">Before creating an export job, you need tooobtain a shipping location name and address by calling hello [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="4aad6-123">`List Locations`konumlar ve posta adresleri listesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="4aad6-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="4aad6-124">Liste döndürülen hello bir konum seçin ve sabit sürücüler toothat adresinizi sevk.</span><span class="sxs-lookup"><span data-stu-id="4aad6-124">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="4aad6-125">Merhaba de kullanabilirsiniz `Get Location` belirli bir konuma adresini doğrudan aktarma işlemi tooobtain hello.</span><span class="sxs-lookup"><span data-stu-id="4aad6-125">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

<span data-ttu-id="4aad6-126">Tooobtain hello sevkiyat konumu Hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4aad6-126">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="4aad6-127">Merhaba hello konumun depolama hesabınızın adını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="4aad6-127">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="4aad6-128">Bu değer hello altında bulunabilir **konumu** hello depolama hesabının alanını **Pano** hello Klasik portal ya da hello Hizmet Yönetimi API işlemi kullanarak için sorgulanan içinde [Al Depolama hesabı özellikleri](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="4aad6-128">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello classic portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="4aad6-129">Kullanılabilir tooprocess olan hello konum bu depolama hesabı tarafından arama hello almak `Get Location` işlemi.</span><span class="sxs-lookup"><span data-stu-id="4aad6-129">Retrieve hello location that are available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="4aad6-130">Merhaba, `AlternateLocations` özelliği hello konumunun hello konumu kendisini içeren sonra kesebilirsiniz toouse olduğu bu konumu.</span><span class="sxs-lookup"><span data-stu-id="4aad6-130">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="4aad6-131">Aksi takdirde hello çağrı `Get Location` hello alternatif konumlar biriyle yeniden işlemi.</span><span class="sxs-lookup"><span data-stu-id="4aad6-131">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="4aad6-132">Merhaba özgün konumuna bakım için geçici olarak kapalı.</span><span class="sxs-lookup"><span data-stu-id="4aad6-132">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-export-job"></a><span data-ttu-id="4aad6-133">Merhaba dışa aktarma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4aad6-133">Creating hello export job</span></span>
 <span data-ttu-id="4aad6-134">toocreate hello dışarı aktarma işini, çağrı hello [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) işlemi.</span><span class="sxs-lookup"><span data-stu-id="4aad6-134">toocreate hello export job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="4aad6-135">Aşağıdaki bilgilerle tooprovide hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4aad6-135">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="4aad6-136">Merhaba işi için bir ad.</span><span class="sxs-lookup"><span data-stu-id="4aad6-136">A name for hello job.</span></span>

-   <span data-ttu-id="4aad6-137">Merhaba depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="4aad6-137">hello storage account name.</span></span>

-   <span data-ttu-id="4aad6-138">Merhaba sevkiyat Hello önceki adımda elde konum adı.</span><span class="sxs-lookup"><span data-stu-id="4aad6-138">hello shipping location name, obtained in hello previous step.</span></span>

-   <span data-ttu-id="4aad6-139">İş türü (verme).</span><span class="sxs-lookup"><span data-stu-id="4aad6-139">A job type (Export).</span></span>

-   <span data-ttu-id="4aad6-140">Merhaba dönüş adresi Hello dışa aktarma işi tamamlandıktan sonra hello sürücüleri burada gönderilmelidir.</span><span class="sxs-lookup"><span data-stu-id="4aad6-140">hello return address where hello drives should be sent after hello export job has completed.</span></span>

-   <span data-ttu-id="4aad6-141">Merhaba BLOB'lar (veya blob önekler) listesini toobe verildi.</span><span class="sxs-lookup"><span data-stu-id="4aad6-141">hello list of blobs (or blob prefixes) toobe exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="4aad6-142">Sürücülerinizin aktarma</span><span class="sxs-lookup"><span data-stu-id="4aad6-142">Shipping your drives</span></span>
 <span data-ttu-id="4aad6-143">Ardından, hello Azure içeri/dışarı aktarma aracı toodetermine hello dışarı toobe seçtiğiniz hello BLOB'ları üzerinde temel toosend, gereksinim duyduğunuz sürücü sayısı kullanın ve disk boyutu hello.</span><span class="sxs-lookup"><span data-stu-id="4aad6-143">Next, use hello Azure Import/Export Tool toodetermine hello number of drives you need toosend, based on hello blobs you have selected toobe exported and hello drive size.</span></span> <span data-ttu-id="4aad6-144">Merhaba bkz [Azure içeri/dışarı aktarma aracı başvurusu](storage-import-export-tool-how-to-v1.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="4aad6-144">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="4aad6-145">Tek bir paket hello sürücü paketini ve toohello sevk hello elde edilen adresi önceki adım.</span><span class="sxs-lookup"><span data-stu-id="4aad6-145">Package hello drives in a single package and ship them toohello address obtained in hello earlier step.</span></span> <span data-ttu-id="4aad6-146">Merhaba sonraki adımınız, paket sayısı izleme hello unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4aad6-146">Note hello tracking number of your package for hello next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="4aad6-147">Sürücülerinizin paketiniz için bir izleme numarası sağlayacak bir desteklenen taşıyıcı hizmeti aracılığıyla hazırlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="4aad6-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-export-job-with-your-package-information"></a><span data-ttu-id="4aad6-148">Paket bilgilerinizle Hello dışarı aktarma işini güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="4aad6-148">Updating hello export job with your package information</span></span>
 <span data-ttu-id="4aad6-149">İzleme numaranızın aldıktan sonra hello çağrısı [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) işlem tooupdated hello taşıyıcı adı ve izleme hello proje numarası.</span><span class="sxs-lookup"><span data-stu-id="4aad6-149">After you have your tracking number, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation tooupdated hello carrier name and tracking number for hello job.</span></span> <span data-ttu-id="4aad6-150">İsteğe bağlı olarak, sürücüler, hello dönüş adresi ve hello sevkiyat tarihi de hello sayısını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4aad6-150">You can optionally specify hello number of drives, hello return address, and hello shipping date as well.</span></span>

## <a name="receiving-hello-package"></a><span data-ttu-id="4aad6-151">Merhaba paket alma</span><span class="sxs-lookup"><span data-stu-id="4aad6-151">Receiving hello package</span></span>
 <span data-ttu-id="4aad6-152">Dışarı aktarma işini işlendikten sonra sürücülerinizin tooyou şifrelenmiş verilerinizi ile döndürülür.</span><span class="sxs-lookup"><span data-stu-id="4aad6-152">After your export job has been processed, your drives will be returned tooyou with your encrypted data.</span></span> <span data-ttu-id="4aad6-153">Her çağırma hello hello sürücüleriyle hello BitLocker anahtarını alabilir [alma işi](/rest/api/storageimportexport/jobs#Jobs_Get) işlemi.</span><span class="sxs-lookup"><span data-stu-id="4aad6-153">You can retrieve hello BitLocker key for each of hello drives by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="4aad6-154">Ardından hello sürücü hello anahtarını kullanarak kilidini açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4aad6-154">You can then unlock hello drive using hello key.</span></span> <span data-ttu-id="4aad6-155">Merhaba sürücü bildirim dosyası her sürücüde hello özgün blob adresi yanı sıra hello sürücü dosyalarını her dosya için hello listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="4aad6-155">hello drive manifest file on each drive contains hello list of files on hello drive, as well as hello original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4aad6-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4aad6-156">Next steps</span></span>

* [<span data-ttu-id="4aad6-157">Merhaba içeri/dışarı aktarma hizmeti REST API'si kullanma</span><span class="sxs-lookup"><span data-stu-id="4aad6-157">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
