---
title: "Dışa aktarma işi için Azure içeri/dışarı aktarma oluşturun | Microsoft Docs"
description: "Microsoft Azure içeri/dışarı aktarma hizmeti için bir dışarı aktarma işinin oluşturmayı öğrenin."
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
ms.openlocfilehash: bdeac373aa8270bd9de8f135ec7166d744fd83ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-export-job-for-the-azure-importexport-service"></a><span data-ttu-id="6bfd8-103">Azure içeri/dışarı aktarma hizmeti için bir dışa aktarma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6bfd8-103">Creating an export job for the Azure Import/Export service</span></span>
<span data-ttu-id="6bfd8-104">REST API kullanarak Microsoft Azure içeri/dışarı aktarma hizmeti için bir dışarı aktarma işinin oluşturma, aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="6bfd8-104">Creating an export job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="6bfd8-105">BLOB'ları dışarı aktarmak için seçme.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-105">Selecting the blobs to export.</span></span>

-   <span data-ttu-id="6bfd8-106">Bir sevkiyat konum alma.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="6bfd8-107">Dışarı aktarma işinin oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-107">Creating the export job.</span></span>

-   <span data-ttu-id="6bfd8-108">Microsoft'a boş sürücülerinizin desteklenen taşıyıcı hizmeti üzerinden aktarma.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-108">Shipping your empty drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="6bfd8-109">Dışarı aktarma işinin paket bilgilerle güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-109">Updating the export job with the package information.</span></span>

-   <span data-ttu-id="6bfd8-110">Sürücüleri Microsoft'tan geri alınıyor.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-110">Receiving the drives back from Microsoft.</span></span>

 <span data-ttu-id="6bfd8-111">Bkz: [Blob depolama alanına veri aktarmak için Windows Azure içeri/dışarı aktarma hizmetini kullanarak](storage-import-export-service.md) genel bir bakış içeri/dışarı aktarma hizmeti ve nasıl kullanılacağını gösteren bir öğretici için [Azure portal](https://portal.azure.com/) oluşturmak ve içeri aktarma yönetmek ve işleri vermek için.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-111">See [Using the Windows Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="selecting-blobs-to-export"></a><span data-ttu-id="6bfd8-112">BLOB'ları dışarı aktarmak için seçme</span><span class="sxs-lookup"><span data-stu-id="6bfd8-112">Selecting blobs to export</span></span>
 <span data-ttu-id="6bfd8-113">Dışarı aktarma işini oluşturmak için depolama hesabınızdan dışarı aktarmak istediğiniz BLOB'ları listesini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-113">To create an export job, you will need to provide a list of blobs that you want to export from your storage account.</span></span> <span data-ttu-id="6bfd8-114">BLOB'ları dışarı seçmek için birkaç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="6bfd8-114">There are a few ways to select blobs to be exported:</span></span>

-   <span data-ttu-id="6bfd8-115">Tek bir blob ve tüm alt anlık görüntü seçmek için göreli blob yolu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-115">You can use a relative blob path to select a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="6bfd8-116">Kendi anlık görüntüleri hariç olmak üzere tek bir blob seçmek için göreli blob yolu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-116">You can use a relative blob path to select a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="6bfd8-117">Tek bir anlık görüntü seçmek için göreli blob yolu ve bir anlık görüntü saati kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-117">You can use a relative blob path and a snapshot time to select a single snapshot.</span></span>

-   <span data-ttu-id="6bfd8-118">Bir blob öneki tüm BLOB'ları ve anlık görüntüleri verilen önekiyle seçmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-118">You can use a blob prefix to select all blobs and snapshots with the given prefix.</span></span>

-   <span data-ttu-id="6bfd8-119">Tüm BLOB'ları ve anlık görüntü depolama hesabındaki dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-119">You can export all blobs and snapshots in the storage account.</span></span>

 <span data-ttu-id="6bfd8-120">BLOB'ları dışarı aktarmak için belirtme hakkında daha fazla bilgi için bkz: [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) işlemi.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-120">For more information about specifying blobs to export, see the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="6bfd8-121">Sevkiyat Konumunuz alma</span><span class="sxs-lookup"><span data-stu-id="6bfd8-121">Obtaining your shipping location</span></span>
<span data-ttu-id="6bfd8-122">Sevkiyat konumu ad ve adres çağırarak elde etmeniz bir dışarı aktarma işinin oluşturmadan önce [alma konumu](https://portal.azure.com) veya [listesi konumları](/rest/api/storageimportexport/listlocations) işlemi.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-122">Before creating an export job, you need to obtain a shipping location name and address by calling the [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="6bfd8-123">`List Locations`konumlar ve posta adresleri listesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="6bfd8-124">Döndürülen listeden bir konum seçin ve bu adresi, sabit sürücüler sevk.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-124">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="6bfd8-125">Aynı zamanda `Get Location` işlemi belirli bir konuma için teslimat adresi doğrudan elde edilir.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-125">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

<span data-ttu-id="6bfd8-126">Sevkiyat konum elde etmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6bfd8-126">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="6bfd8-127">Konumun depolama hesabınızın adını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-127">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="6bfd8-128">Bu değer altında bulunabilir **konumu** depolama hesabının alanını **Pano** Klasik portal ya da hizmet yönetimi API işlemi kullanarak için sorgulanan içinde [depolama hesabı özellikleri Al](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="6bfd8-128">This value can be found under the **Location** field on the storage account's **Dashboard** in the classic portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="6bfd8-129">Bu depolama hesabını çağırarak işlemek için kullanılabilecek konumu almak `Get Location` işlemi.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-129">Retrieve the location that are available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="6bfd8-130">Varsa `AlternateLocations` özelliği konumun Konum içerir ve ardından bu konumu kullanmak uygundur.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-130">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="6bfd8-131">Aksi halde çağrı `Get Location` alternatif konumlar biriyle yeniden işlemi.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-131">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="6bfd8-132">Özgün konuma bakım için geçici olarak kapalı.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-132">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-export-job"></a><span data-ttu-id="6bfd8-133">Dışa aktarma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6bfd8-133">Creating the export job</span></span>
 <span data-ttu-id="6bfd8-134">Dışarı aktarma işini oluşturmak için arama [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) işlemi.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-134">To create the export job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="6bfd8-135">Aşağıdaki bilgileri sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6bfd8-135">You will need to provide the following information:</span></span>

-   <span data-ttu-id="6bfd8-136">İş için bir ad.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-136">A name for the job.</span></span>

-   <span data-ttu-id="6bfd8-137">Depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-137">The storage account name.</span></span>

-   <span data-ttu-id="6bfd8-138">Önceki adımda elde sevkiyat konum adı.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-138">The shipping location name, obtained in the previous step.</span></span>

-   <span data-ttu-id="6bfd8-139">İş türü (verme).</span><span class="sxs-lookup"><span data-stu-id="6bfd8-139">A job type (Export).</span></span>

-   <span data-ttu-id="6bfd8-140">Dönüş adresi dışa aktarma işi tamamlandıktan sonra sürücüleri burada gönderilmelidir.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-140">The return address where the drives should be sent after the export job has completed.</span></span>

-   <span data-ttu-id="6bfd8-141">Dışa aktarılacak BLOB'lar (veya blob önekler) listesi.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-141">The list of blobs (or blob prefixes) to be exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="6bfd8-142">Sürücülerinizin aktarma</span><span class="sxs-lookup"><span data-stu-id="6bfd8-142">Shipping your drives</span></span>
 <span data-ttu-id="6bfd8-143">Ardından, Azure içeri/dışarı aktarma aracı göndermek istediğiniz sürücü sayısını belirlemek için verilecek seçtiğiniz BLOB'ları ve disk boyutu göre kullanın.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-143">Next, use the Azure Import/Export Tool to determine the number of drives you need to send, based on the blobs you have selected to be exported and the drive size.</span></span> <span data-ttu-id="6bfd8-144">Bkz: [Azure içeri/dışarı aktarma aracı başvurusu](storage-import-export-tool-how-to-v1.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-144">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="6bfd8-145">Tek bir paket sürücüleri paketini ve bunları önceki adımda elde adrese gönderme.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-145">Package the drives in a single package and ship them to the address obtained in the earlier step.</span></span> <span data-ttu-id="6bfd8-146">Paketinizin bir sonraki adım için izleme sayısını not edin.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-146">Note the tracking number of your package for the next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="6bfd8-147">Sürücülerinizin paketiniz için bir izleme numarası sağlayacak bir desteklenen taşıyıcı hizmeti aracılığıyla hazırlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-export-job-with-your-package-information"></a><span data-ttu-id="6bfd8-148">Dışarı aktarma işinin paket bilgilerinizi ile güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="6bfd8-148">Updating the export job with your package information</span></span>
 <span data-ttu-id="6bfd8-149">İzleme numaranızın aldıktan sonra arama [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) taşıyıcı adı ve iş numaralı izleme işlemi için güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-149">After you have your tracking number, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation to updated the carrier name and tracking number for the job.</span></span> <span data-ttu-id="6bfd8-150">İsteğe bağlı olarak, sürücüler, dönüş adresi ve sevkiyat tarihi de sayısını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-150">You can optionally specify the number of drives, the return address, and the shipping date as well.</span></span>

## <a name="receiving-the-package"></a><span data-ttu-id="6bfd8-151">Paket alma</span><span class="sxs-lookup"><span data-stu-id="6bfd8-151">Receiving the package</span></span>
 <span data-ttu-id="6bfd8-152">Sürücülerinizin dışarı aktarma işini işlendikten sonra size, şifrelenmiş verilerle döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-152">After your export job has been processed, your drives will be returned to you with your encrypted data.</span></span> <span data-ttu-id="6bfd8-153">Çağırarak her sürücüleri için BitLocker anahtarını alabilir [alma işi](/rest/api/storageimportexport/jobs#Jobs_Get) işlemi.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-153">You can retrieve the BitLocker key for each of the drives by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="6bfd8-154">Ardından anahtar kullanılarak sürücünün kilidini açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-154">You can then unlock the drive using the key.</span></span> <span data-ttu-id="6bfd8-155">Her sürücüde sürücü bildirim dosyası, her dosya için özgün blob adresi yanı sıra, sürücü dosyaları listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="6bfd8-155">The drive manifest file on each drive contains the list of files on the drive, as well as the original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bfd8-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6bfd8-156">Next steps</span></span>

* [<span data-ttu-id="6bfd8-157">İçeri/dışarı aktarma hizmeti REST API'si kullanma</span><span class="sxs-lookup"><span data-stu-id="6bfd8-157">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
