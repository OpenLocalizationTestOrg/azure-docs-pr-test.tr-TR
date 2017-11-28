---
title: "aaaCreate içe aktarma işi için Azure içeri/dışarı aktarma | Microsoft Docs"
description: "Bilgi nasıl toocreate hello Microsoft Azure içeri/dışarı aktarma hizmeti için bir alma."
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
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a><span data-ttu-id="5eb31-103">Hello Azure içeri/dışarı aktarma hizmeti için bir içeri aktarma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5eb31-103">Creating an import job for hello Azure Import/Export service</span></span>

<span data-ttu-id="5eb31-104">İçe aktarma işi hello REST API kullanarak hello Microsoft Azure içeri/dışarı aktarma hizmeti oluşturma hello aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="5eb31-104">Creating an import job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="5eb31-105">Hello Azure içeri/dışarı aktarma aracı olan sürücüleri hazırlanıyor.</span><span class="sxs-lookup"><span data-stu-id="5eb31-105">Preparing drives with hello Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="5eb31-106">Başlangıç konumu toowhich tooship hello sürücü alma.</span><span class="sxs-lookup"><span data-stu-id="5eb31-106">Obtaining hello location toowhich tooship hello drive.</span></span>

-   <span data-ttu-id="5eb31-107">Merhaba alma işi oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="5eb31-107">Creating hello import job.</span></span>

-   <span data-ttu-id="5eb31-108">Merhaba sevkiyat tooMicrosoft desteklenen taşıyıcı hizmeti sürücüleri.</span><span class="sxs-lookup"><span data-stu-id="5eb31-108">Shipping hello drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="5eb31-109">Merhaba içe aktarma işi ile Sevkiyat ayrıntıları hello güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="5eb31-109">Updating hello import job with hello shipping details.</span></span>

 <span data-ttu-id="5eb31-110">Bkz: [hello Microsoft Azure içeri/dışarı aktarma hizmeti tooTransfer veri tooBlob depolama kullanarak](storage-import-export-service.md) genel bir bakış hello içeri/dışarı aktarma hizmeti ve gösteren bir öğretici için nasıl toouse hello [Azure portal](https://portal.azure.com/) toocreate alma yönetmek ve işleri dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="5eb31-110">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure  portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a><span data-ttu-id="5eb31-111">Hello Azure içeri/dışarı aktarma aracı olan sürücüleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="5eb31-111">Preparing drives with hello Azure Import/Export Tool</span></span>

<span data-ttu-id="5eb31-112">Merhaba adımları tooprepare sürücüler içeri aktarma işi için olan hello aynı olup olmadığını oluşturduğunuz jobvia hello portal hello veya REST API aracılığıyla hello.</span><span class="sxs-lookup"><span data-stu-id="5eb31-112">hello steps tooprepare drives for an import job are hello same whether you create hello jobvia hello portal or via hello REST API.</span></span>

<span data-ttu-id="5eb31-113">Sürücü hazırlama kısa bir genel bakış aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="5eb31-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="5eb31-114">Toohello başvuran [Azure alma ExportTool başvurusu](storage-import-export-tool-how-to-v1.md) tam yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="5eb31-114">Refer toohello [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="5eb31-115">Hello Azure içeri/dışarı aktarma aracı indirebilirsiniz [burada](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="5eb31-115">You can download hello Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="5eb31-116">Sürücünüz hazırlanıyor içerir:</span><span class="sxs-lookup"><span data-stu-id="5eb31-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="5eb31-117">Merhaba veri toobe alınan tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="5eb31-117">Identifying hello data toobe imported.</span></span>

-   <span data-ttu-id="5eb31-118">Windows Azure depolama alanında Hello hedef BLOB'ları tanımlama.</span><span class="sxs-lookup"><span data-stu-id="5eb31-118">Identifying hello destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="5eb31-119">Hello Azure içeri/dışarı aktarma aracı toocopy veri tooone ya da daha fazla sabit disk sürücüler kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="5eb31-119">Using hello Azure Import/Export Tool toocopy your data tooone or more hard drives.</span></span>

 <span data-ttu-id="5eb31-120">hazırlandığını gibi hello Azure içeri/dışarı aktarma aracı ayrıca her hello sürücüleri için bir bildirim dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5eb31-120">hello Azure Import/Export Tool will also generate a manifest file for each of hello drives as it is prepared.</span></span> <span data-ttu-id="5eb31-121">Bildirim dosyası içerir:</span><span class="sxs-lookup"><span data-stu-id="5eb31-121">A manifest file contains:</span></span>

-   <span data-ttu-id="5eb31-122">Karşıya yükleme ve bu dosyaları tooblobs hello eşlemelerini yönelik tüm hello dosyaları numaralandırması.</span><span class="sxs-lookup"><span data-stu-id="5eb31-122">An enumeration of all hello files intended for upload and hello mappings from these files tooblobs.</span></span>

-   <span data-ttu-id="5eb31-123">Her bir dosyanın parçalarını hello sağlama.</span><span class="sxs-lookup"><span data-stu-id="5eb31-123">Checksums of hello segments of each file.</span></span>

-   <span data-ttu-id="5eb31-124">Her bir blob ile Merhaba meta verileri ve özellikleri tooassociate hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5eb31-124">Information about hello metadata and properties tooassociate with each blob.</span></span>

-   <span data-ttu-id="5eb31-125">Karşıya yüklenen bir blob hello varsa bir hello eylem tootake listeleme aynı hello kapsayıcısındaki bir blob olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="5eb31-125">A listing of hello action tootake if a blob that is being uploaded has hello same name as an existing blob in hello container.</span></span> <span data-ttu-id="5eb31-126">Olası seçenekler: a) hello blob ile Merhaba dosyanın üzerine, (b) hello mevcut blob ve hello dosyayı karşıya yüklemeyi atlayın tutmak, c) toohello sonek başka dosyalarla çakışmadığından emin Ekle.</span><span class="sxs-lookup"><span data-stu-id="5eb31-126">Possible options are: a) overwrite hello blob with hello file, b) keep hello existing blob and skip uploading hello file, c) append a suffix toohello name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="5eb31-127">Sevkiyat Konumunuz alma</span><span class="sxs-lookup"><span data-stu-id="5eb31-127">Obtaining your shipping location</span></span>

<span data-ttu-id="5eb31-128">İçe aktarma işi oluşturmadan önce tooobtain sevkiyat konum adı ve adres tarafından arama hello ihtiyacınız [listesi konumları](/rest/api/storageimportexport/listlocations) işlemi.</span><span class="sxs-lookup"><span data-stu-id="5eb31-128">Before creating an import job, you need tooobtain a shipping location name and address by calling hello [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="5eb31-129">`List Locations`konumlar ve posta adresleri listesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="5eb31-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="5eb31-130">Liste döndürülen hello bir konum seçin ve sabit sürücüler toothat adresinizi sevk.</span><span class="sxs-lookup"><span data-stu-id="5eb31-130">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="5eb31-131">Merhaba de kullanabilirsiniz `Get Location` belirli bir konuma adresini doğrudan aktarma işlemi tooobtain hello.</span><span class="sxs-lookup"><span data-stu-id="5eb31-131">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

 <span data-ttu-id="5eb31-132">Tooobtain hello sevkiyat konumu Hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="5eb31-132">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="5eb31-133">Merhaba hello konumun depolama hesabınızın adını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="5eb31-133">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="5eb31-134">Bu değer hello altında bulunabilir **konumu** hello depolama hesabının alanını **Pano** hello Azure portal veya hello Hizmet Yönetimi API işlemi kullanarak için sorgulanan içinde [depolama Al Hesap özellikleri](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="5eb31-134">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello Azure portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="5eb31-135">Kullanılabilir tooprocess hello konuma göre arama hello bu depolama hesabı almak `Get Location` işlemi.</span><span class="sxs-lookup"><span data-stu-id="5eb31-135">Retrieve hello location that is available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="5eb31-136">Merhaba, `AlternateLocations` özelliği hello konumunun hello konumu kendisini içeren sonra kesebilirsiniz toouse olduğu bu konumu.</span><span class="sxs-lookup"><span data-stu-id="5eb31-136">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="5eb31-137">Aksi takdirde hello çağrı `Get Location` hello alternatif konumlar biriyle yeniden işlemi.</span><span class="sxs-lookup"><span data-stu-id="5eb31-137">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="5eb31-138">Merhaba özgün konumuna bakım için geçici olarak kapalı.</span><span class="sxs-lookup"><span data-stu-id="5eb31-138">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-import-job"></a><span data-ttu-id="5eb31-139">Merhaba alma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5eb31-139">Creating hello import job</span></span>
<span data-ttu-id="5eb31-140">toocreate hello alma işi, çağrı hello [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) işlemi.</span><span class="sxs-lookup"><span data-stu-id="5eb31-140">toocreate hello import job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="5eb31-141">Aşağıdaki bilgilerle tooprovide hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5eb31-141">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="5eb31-142">Merhaba işi için bir ad.</span><span class="sxs-lookup"><span data-stu-id="5eb31-142">A name for hello job.</span></span>

-   <span data-ttu-id="5eb31-143">Merhaba depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="5eb31-143">hello storage account name.</span></span>

-   <span data-ttu-id="5eb31-144">Merhaba sevkiyat Hello önceki adımda elde edilen konum adı.</span><span class="sxs-lookup"><span data-stu-id="5eb31-144">hello shipping location name, obtained from hello previous step.</span></span>

-   <span data-ttu-id="5eb31-145">İş türü (içe aktarma).</span><span class="sxs-lookup"><span data-stu-id="5eb31-145">A job type (Import).</span></span>

-   <span data-ttu-id="5eb31-146">Merhaba dönüş adresi Hello alma işi tamamlandıktan sonra hello sürücüleri burada gönderilmelidir.</span><span class="sxs-lookup"><span data-stu-id="5eb31-146">hello return address where hello drives should be sent after hello import job has completed.</span></span>

-   <span data-ttu-id="5eb31-147">Merhaba işteki sürücülerin listesini Hello.</span><span class="sxs-lookup"><span data-stu-id="5eb31-147">hello list of drives in hello job.</span></span> <span data-ttu-id="5eb31-148">Her bir sürücü için hello sürücü hazırlık adımı sırasında edinilen bilgisinden hello şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="5eb31-148">For each drive, you must include hello following information that was obtained during hello drive preparation step:</span></span>

    -   <span data-ttu-id="5eb31-149">Merhaba sürücü kimliği</span><span class="sxs-lookup"><span data-stu-id="5eb31-149">hello drive Id</span></span>

    -   <span data-ttu-id="5eb31-150">Merhaba BitLocker anahtarı</span><span class="sxs-lookup"><span data-stu-id="5eb31-150">hello BitLocker key</span></span>

    -   <span data-ttu-id="5eb31-151">Merhaba bildirim dosyası göreli yolda hello sabit sürücü</span><span class="sxs-lookup"><span data-stu-id="5eb31-151">hello manifest file relative path on hello hard drive</span></span>

    -   <span data-ttu-id="5eb31-152">bildirim dosyası MD5 karma değeri Hello Base16 kodlanmış</span><span class="sxs-lookup"><span data-stu-id="5eb31-152">hello Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="5eb31-153">Sürücülerinizin aktarma</span><span class="sxs-lookup"><span data-stu-id="5eb31-153">Shipping your drives</span></span>
<span data-ttu-id="5eb31-154">Merhaba önceki adımda elde ettiğiniz sürücüleri toohello adresinizi hazırlamalısınız ve hello içeri/dışarı aktarma hizmeti ile Merhaba paket sayısı izleme hello sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5eb31-154">You must ship your drives toohello address that you obtained from hello previous step, and you must provide hello Import/Export service with hello tracking number of hello package.</span></span>

> [!NOTE]
>  <span data-ttu-id="5eb31-155">Sürücülerinizin paketiniz için bir izleme numarası sağlayacak bir desteklenen taşıyıcı hizmeti aracılığıyla hazırlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="5eb31-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-import-job-with-your-shipping-information"></a><span data-ttu-id="5eb31-156">Merhaba içe aktarma işi ile sevkiyat bilgilerinizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="5eb31-156">Updating hello import job with your shipping information</span></span>
<span data-ttu-id="5eb31-157">İzleme numaranızın aldıktan sonra hello çağrısı [güncelleştirme işi özellikleri](/api/storageimportexport/jobs#Jobs_Update) taşıyıcı adı, hello izleme numarası hello işi için ve hello taşıyıcı hesap numarası dönüş sevkiyat aktarma işlemi tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="5eb31-157">After you have your tracking number, call hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation tooupdate hello shipping carrier name, hello tracking number for hello job, and hello carrier account number for return shipping.</span></span> <span data-ttu-id="5eb31-158">İsteğe bağlı olarak, sürücüler ve tarihi de sevkiyat hello hello sayısını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5eb31-158">You can optionally specify hello number of drives and hello shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5eb31-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5eb31-159">Next steps</span></span>

* [<span data-ttu-id="5eb31-160">Merhaba içeri/dışarı aktarma hizmeti REST API'si kullanma</span><span class="sxs-lookup"><span data-stu-id="5eb31-160">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
