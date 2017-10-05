---
title: "Azure içeri/dışarı aktarma için bir içeri aktarma işi oluşturma | Microsoft Docs"
description: "Microsoft Azure içeri/dışarı aktarma hizmeti için bir alma oluşturmayı öğrenin."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d373d2a0e601f2796719fc5efb8761f276ab24d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-import-job-for-the-azure-importexport-service"></a><span data-ttu-id="4ba7e-103">Azure içeri/dışarı aktarma hizmeti için bir alma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ba7e-103">Creating an import job for the Azure Import/Export service</span></span>

<span data-ttu-id="4ba7e-104">REST API kullanarak Microsoft Azure içeri/dışarı aktarma hizmeti için bir alma işi oluşturma, aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="4ba7e-104">Creating an import job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="4ba7e-105">Azure içeri/dışarı aktarma aracı olan sürücüleri hazırlanıyor.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-105">Preparing drives with the Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="4ba7e-106">Sürücü dağıtmayı konum alma.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-106">Obtaining the location to which to ship the drive.</span></span>

-   <span data-ttu-id="4ba7e-107">İçe aktarma işi oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-107">Creating the import job.</span></span>

-   <span data-ttu-id="4ba7e-108">Desteklenen taşıyıcı hizmeti üzerinden Microsoft'a sürücüleri aktarma.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-108">Shipping the drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="4ba7e-109">İçe aktarma işi ile sevkiyat ayrıntılarını güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-109">Updating the import job with the shipping details.</span></span>

 <span data-ttu-id="4ba7e-110">Bkz: [Blob depolama alanına veri aktarmak için Microsoft Azure içeri/dışarı aktarma hizmeti kullanılarak](storage-import-export-service.md) genel bir bakış içeri/dışarı aktarma hizmeti ve nasıl kullanılacağını gösteren bir öğretici için [Azure portal](https://portal.azure.com/) oluşturmak ve içeri aktarma yönetmek ve işleri vermek için.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-110">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure  portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-the-azure-importexport-tool"></a><span data-ttu-id="4ba7e-111">Azure içeri/dışarı aktarma aracı olan sürücüleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="4ba7e-111">Preparing drives with the Azure Import/Export Tool</span></span>

<span data-ttu-id="4ba7e-112">Sürücüleri içeri aktarma işi için hazırlamak üzere adımları portalı jobvia oluşturmak veya REST API aracılığıyla aynıdır.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-112">The steps to prepare drives for an import job are the same whether you create the jobvia the portal or via the REST API.</span></span>

<span data-ttu-id="4ba7e-113">Sürücü hazırlama kısa bir genel bakış aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="4ba7e-114">Başvurmak [Azure alma ExportTool başvurusu](storage-import-export-tool-how-to-v1.md) tam yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-114">Refer to the [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="4ba7e-115">Azure içeri/dışarı aktarma aracı indirebilirsiniz [burada](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="4ba7e-115">You can download the Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="4ba7e-116">Sürücünüz hazırlanıyor içerir:</span><span class="sxs-lookup"><span data-stu-id="4ba7e-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="4ba7e-117">İçeri aktarılacak veri tanımlama.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-117">Identifying the data to be imported.</span></span>

-   <span data-ttu-id="4ba7e-118">Windows Azure depolama alanındaki hedef BLOB'ları tanımlama.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-118">Identifying the destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="4ba7e-119">Bir veya daha fazla sabit sürücüler, verileri kopyalamak üzere Azure içeri/dışarı aktarma aracını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-119">Using the Azure Import/Export Tool to copy your data to one or more hard drives.</span></span>

 <span data-ttu-id="4ba7e-120">Hazırlandığını gibi Azure içeri/dışarı aktarma aracı ayrıca her sürücü için bir bildirim dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-120">The Azure Import/Export Tool will also generate a manifest file for each of the drives as it is prepared.</span></span> <span data-ttu-id="4ba7e-121">Bildirim dosyası içerir:</span><span class="sxs-lookup"><span data-stu-id="4ba7e-121">A manifest file contains:</span></span>

-   <span data-ttu-id="4ba7e-122">Karşıya yükleme ve bu dosyaların eşlemeleri BLOB'lar için yönelik tüm dosyaların listesi.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-122">An enumeration of all the files intended for upload and the mappings from these files to blobs.</span></span>

-   <span data-ttu-id="4ba7e-123">Her bir dosyanın parçalarını sağlama.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-123">Checksums of the segments of each file.</span></span>

-   <span data-ttu-id="4ba7e-124">Her bir blob ile ilişkilendirmek için özellikler ve meta verileri hakkında bilgiler.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-124">Information about the metadata and properties to associate with each blob.</span></span>

-   <span data-ttu-id="4ba7e-125">Karşıya yüklenen bir blob aynı adı taşıyan bir blob kapsayıcısında varsa yapılacak eylem listesi.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-125">A listing of the action to take if a blob that is being uploaded has the same name as an existing blob in the container.</span></span> <span data-ttu-id="4ba7e-126">Olası seçenekler: a) blob ile bu dosyanın üzerine, b) mevcut blob ve dosyayı karşıya yüklemeyi atlayın tutmak, c) bir sonek adına başka dosyalarla çakışmayacak şekilde ekleme.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-126">Possible options are: a) overwrite the blob with the file, b) keep the existing blob and skip uploading the file, c) append a suffix to the name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="4ba7e-127">Sevkiyat Konumunuz alma</span><span class="sxs-lookup"><span data-stu-id="4ba7e-127">Obtaining your shipping location</span></span>

<span data-ttu-id="4ba7e-128">Sevkiyat konumu ad ve adres çağırarak elde etmeniz alma işi oluşturmadan önce [listesi konumları](/rest/api/storageimportexport/listlocations) işlemi.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-128">Before creating an import job, you need to obtain a shipping location name and address by calling the [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="4ba7e-129">`List Locations`konumlar ve posta adresleri listesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="4ba7e-130">Döndürülen listeden bir konum seçin ve bu adresi, sabit sürücüler sevk.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-130">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="4ba7e-131">Aynı zamanda `Get Location` işlemi belirli bir konuma için teslimat adresi doğrudan elde edilir.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-131">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

 <span data-ttu-id="4ba7e-132">Sevkiyat konum elde etmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4ba7e-132">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="4ba7e-133">Konumun depolama hesabınızın adını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-133">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="4ba7e-134">Bu değer altında bulunabilir **konumu** depolama hesabının alanını **Pano** Azure portal ya da hizmet yönetimi API işlemi kullanarak için sorgulanan [depolama hesabı özellikleri Al](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="4ba7e-134">This value can be found under the **Location** field on the storage account's **Dashboard** in the Azure portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="4ba7e-135">Bu depolama hesabını çağırarak işlemek için konum almak `Get Location` işlemi.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-135">Retrieve the location that is available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="4ba7e-136">Varsa `AlternateLocations` özelliği konumun Konum içerir ve ardından bu konumu kullanmak uygundur.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-136">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="4ba7e-137">Aksi halde çağrı `Get Location` alternatif konumlar biriyle yeniden işlemi.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-137">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="4ba7e-138">Özgün konuma bakım için geçici olarak kapalı.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-138">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-import-job"></a><span data-ttu-id="4ba7e-139">İçe aktarma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ba7e-139">Creating the import job</span></span>
<span data-ttu-id="4ba7e-140">İçe aktarma işi oluşturmak için arama [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) işlemi.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-140">To create the import job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="4ba7e-141">Aşağıdaki bilgileri sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4ba7e-141">You will need to provide the following information:</span></span>

-   <span data-ttu-id="4ba7e-142">İş için bir ad.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-142">A name for the job.</span></span>

-   <span data-ttu-id="4ba7e-143">Depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-143">The storage account name.</span></span>

-   <span data-ttu-id="4ba7e-144">Önceki adımda elde edilen sevkiyat konum adı.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-144">The shipping location name, obtained from the previous step.</span></span>

-   <span data-ttu-id="4ba7e-145">İş türü (içe aktarma).</span><span class="sxs-lookup"><span data-stu-id="4ba7e-145">A job type (Import).</span></span>

-   <span data-ttu-id="4ba7e-146">Dönüş adresi alma işi tamamlandıktan sonra sürücüleri burada gönderilmelidir.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-146">The return address where the drives should be sent after the import job has completed.</span></span>

-   <span data-ttu-id="4ba7e-147">İş sürücülerin listesi.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-147">The list of drives in the job.</span></span> <span data-ttu-id="4ba7e-148">Her bir sürücü için sürücü hazırlık adımında edinilen aşağıdaki bilgileri içermelidir:</span><span class="sxs-lookup"><span data-stu-id="4ba7e-148">For each drive, you must include the following information that was obtained during the drive preparation step:</span></span>

    -   <span data-ttu-id="4ba7e-149">Sürücü Kimliği</span><span class="sxs-lookup"><span data-stu-id="4ba7e-149">The drive Id</span></span>

    -   <span data-ttu-id="4ba7e-150">BitLocker anahtar</span><span class="sxs-lookup"><span data-stu-id="4ba7e-150">The BitLocker key</span></span>

    -   <span data-ttu-id="4ba7e-151">Sabit sürücüde bildirim dosyası göreli yolu</span><span class="sxs-lookup"><span data-stu-id="4ba7e-151">The manifest file relative path on the hard drive</span></span>

    -   <span data-ttu-id="4ba7e-152">Bildirim dosyası MD5 karma Base16 kodlanmış</span><span class="sxs-lookup"><span data-stu-id="4ba7e-152">The Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="4ba7e-153">Sürücülerinizin aktarma</span><span class="sxs-lookup"><span data-stu-id="4ba7e-153">Shipping your drives</span></span>
<span data-ttu-id="4ba7e-154">Önceki adımda elde ettiğiniz adrese sürücülerinizin hazırlamalısınız ve paket izleme numarasıyla içeri/dışarı aktarma hizmeti sağlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-154">You must ship your drives to the address that you obtained from the previous step, and you must provide the Import/Export service with the tracking number of the package.</span></span>

> [!NOTE]
>  <span data-ttu-id="4ba7e-155">Sürücülerinizin paketiniz için bir izleme numarası sağlayacak bir desteklenen taşıyıcı hizmeti aracılığıyla hazırlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-import-job-with-your-shipping-information"></a><span data-ttu-id="4ba7e-156">İçe aktarma işi ile sevkiyat bilgilerinizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="4ba7e-156">Updating the import job with your shipping information</span></span>
<span data-ttu-id="4ba7e-157">İzleme numaranızın aldıktan sonra arama [güncelleştirme işi özellikleri](/api/storageimportexport/jobs#Jobs_Update) Sevkiyat taşıyıcı adı, iş için izleme numarası ve dönüş Sevkiyat taşıyıcı hesap numarası güncelleştirmek için güncelleştirme işlemi.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-157">After you have your tracking number, call the [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation to update the shipping carrier name, the tracking number for the job, and the carrier account number for return shipping.</span></span> <span data-ttu-id="4ba7e-158">İsteğe bağlı olarak, sürücüler ve sevkiyat tarihi de sayısını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ba7e-158">You can optionally specify the number of drives and the shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ba7e-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4ba7e-159">Next steps</span></span>

* [<span data-ttu-id="4ba7e-160">İçeri/dışarı aktarma hizmeti REST API'si kullanma</span><span class="sxs-lookup"><span data-stu-id="4ba7e-160">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
