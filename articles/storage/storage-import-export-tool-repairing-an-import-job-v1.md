---
title: "Bir Azure içeri/dışarı aktarma alma işi - v1 onarma | Microsoft Docs"
description: "Oluşturulmuş ve Azure içeri/dışarı aktarma hizmeti kullanarak çalışan bir alma işi onarmak öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: b374eabcbafa6ffe64c639fb6c89be857ecfc221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="repairing-an-import-job"></a><span data-ttu-id="e8737-103">Bir içeri aktarma işini onarma</span><span class="sxs-lookup"><span data-stu-id="e8737-103">Repairing an import job</span></span>
<span data-ttu-id="e8737-104">Microsoft Azure içeri/dışarı aktarma hizmeti, bazı dosyalar veya, bir dosyanın parçalarını Windows Azure Blob hizmeti kopyalamak başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="e8737-104">The Microsoft Azure Import/Export service may fail to copy some of your files or parts of a file to the Windows Azure Blob service.</span></span> <span data-ttu-id="e8737-105">Hataları görmek için bazı nedenler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e8737-105">Some reasons for failures include:</span></span>  
  
-   <span data-ttu-id="e8737-106">Bozuk dosyaları</span><span class="sxs-lookup"><span data-stu-id="e8737-106">Corrupted files</span></span>  
  
-   <span data-ttu-id="e8737-107">Bozuk sürücüler</span><span class="sxs-lookup"><span data-stu-id="e8737-107">Damaged drives</span></span>  
  
-   <span data-ttu-id="e8737-108">Depolama hesabı anahtarı dosyası aktarılırken değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="e8737-108">The storage account key changed while the file was being transferred.</span></span>  
  
<span data-ttu-id="e8737-109">İşin kopya günlük dosyalarını içeri aktarmaya Microsoft Azure içeri/dışarı aktarma Aracı'nı çalıştırabilir ve içeri aktarma işlemini tamamlamak için Windows Azure depolama hesabınıza aracı eksik dosyaları (veya, bir dosyanın parçalarını) karşıya yükleyecek.</span><span class="sxs-lookup"><span data-stu-id="e8737-109">You can run the Microsoft Azure Import/Export Tool with the import job's copy log files, and the tool will upload the missing files (or parts of a file) to your Windows Azure storage account to complete import job.</span></span>  
  
## <a name="repairimport-parameters"></a><span data-ttu-id="e8737-110">RepairImport parametreleri</span><span class="sxs-lookup"><span data-stu-id="e8737-110">RepairImport parameters</span></span>

<span data-ttu-id="e8737-111">Aşağıdaki parametreleri ile belirtilen **RepairImport**:</span><span class="sxs-lookup"><span data-stu-id="e8737-111">The following parameters can be specified with **RepairImport**:</span></span> 
  
|||  
|-|-|  
|<span data-ttu-id="e8737-112">**/ r:**< RepairFile\></span><span class="sxs-lookup"><span data-stu-id="e8737-112">**/r:**<RepairFile\></span></span>|<span data-ttu-id="e8737-113">**Gerekli.**</span><span class="sxs-lookup"><span data-stu-id="e8737-113">**Required.**</span></span> <span data-ttu-id="e8737-114">Onarım ilerleyişini izler ve kesintiye uğramış bir onarım sürdürmek için veren onarım dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="e8737-114">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span></span> <span data-ttu-id="e8737-115">Her bir sürücü bir ve yalnızca bir onarım dosyası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8737-115">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="e8737-116">Belirli bir sürücü için onarım başlattığınızda, henüz var olmayan bir onarım dosya yolunda geçer.</span><span class="sxs-lookup"><span data-stu-id="e8737-116">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span></span> <span data-ttu-id="e8737-117">Kesintiye uğramış bir onarım sürdürmek için varolan bir onarma dosya adına geçirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="e8737-117">To resume an interrupted repair, you should pass in the name of an existing repair file.</span></span> <span data-ttu-id="e8737-118">Onarım dosya hedef sürücüye karşılık gelen her zaman belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8737-118">The repair file corresponding to the target drive must always be specified.</span></span>|  
|<span data-ttu-id="e8737-119">**/ LOGDIR:**< LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="e8737-119">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="e8737-120">**İsteğe bağlı.**</span><span class="sxs-lookup"><span data-stu-id="e8737-120">**Optional.**</span></span> <span data-ttu-id="e8737-121">Günlük dosyası dizini.</span><span class="sxs-lookup"><span data-stu-id="e8737-121">The log directory.</span></span> <span data-ttu-id="e8737-122">Bu dizin için ayrıntılı günlük dosyalarına yazılır.</span><span class="sxs-lookup"><span data-stu-id="e8737-122">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="e8737-123">Günlük dizini belirtilmezse, geçerli dizin günlük dizini olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e8737-123">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="e8737-124">**/ d:**< TargetDirectories\></span><span class="sxs-lookup"><span data-stu-id="e8737-124">**/d:**<TargetDirectories\></span></span>|<span data-ttu-id="e8737-125">**Gerekli.**</span><span class="sxs-lookup"><span data-stu-id="e8737-125">**Required.**</span></span> <span data-ttu-id="e8737-126">İçe aktarılan özgün dosyaları içeren bir veya daha çok noktalı virgülle ayrılmış dizinleri.</span><span class="sxs-lookup"><span data-stu-id="e8737-126">One or more semicolon-separated directories that contain the original files that were imported.</span></span> <span data-ttu-id="e8737-127">İçeri aktarma sürücü de kullanılabilir, ancak özgün dosyaları alternatif konumlara kullanılabilir, gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="e8737-127">The import drive may also be used, but is not required if alternate locations of original files are available.</span></span>|  
|<span data-ttu-id="e8737-128">**/BK:**< BitLockerKey\></span><span class="sxs-lookup"><span data-stu-id="e8737-128">**/bk:**<BitLockerKey\></span></span>|<span data-ttu-id="e8737-129">**İsteğe bağlı.**</span><span class="sxs-lookup"><span data-stu-id="e8737-129">**Optional.**</span></span> <span data-ttu-id="e8737-130">Özgün dosya kullanılabildiği şifrelenmiş sürücünün kilidini açmak için aracın istiyorsanız BitLocker anahtarını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8737-130">You should specify the BitLocker key if you want the tool to unlock an encrypted drive where the original files are available.</span></span>|  
|<span data-ttu-id="e8737-131">**/sn:**< StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="e8737-131">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="e8737-132">**Gerekli.**</span><span class="sxs-lookup"><span data-stu-id="e8737-132">**Required.**</span></span> <span data-ttu-id="e8737-133">İçe aktarma işi için depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="e8737-133">The name of the storage account for the import job.</span></span>|  
|<span data-ttu-id="e8737-134">**/SK:**< StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="e8737-134">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="e8737-135">**Gerekli** bir kapsayıcı SAS varsa ve yalnızca belirtilmezse.</span><span class="sxs-lookup"><span data-stu-id="e8737-135">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="e8737-136">İçe aktarma işi için depolama hesabı için hesap anahtarı.</span><span class="sxs-lookup"><span data-stu-id="e8737-136">The account key for the storage account for the import job.</span></span>|  
|<span data-ttu-id="e8737-137">**/csas:**< ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="e8737-137">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="e8737-138">**Gerekli** depolama hesabı anahtarı belirtilmezse varsa ve yalnızca.</span><span class="sxs-lookup"><span data-stu-id="e8737-138">**Required** if and only if the storage account key is not specified.</span></span> <span data-ttu-id="e8737-139">İçe aktarma işi ile ilişkili BLOB'ları erişmek için kapsayıcı SAS.</span><span class="sxs-lookup"><span data-stu-id="e8737-139">The container SAS for accessing the blobs associated with the import job.</span></span>|  
|<span data-ttu-id="e8737-140">**/ CopyLogFile:**< DriveCopyLogFile\></span><span class="sxs-lookup"><span data-stu-id="e8737-140">**/CopyLogFile:**<DriveCopyLogFile\></span></span>|<span data-ttu-id="e8737-141">**Gerekli.**</span><span class="sxs-lookup"><span data-stu-id="e8737-141">**Required.**</span></span> <span data-ttu-id="e8737-142">Sürücüyü Kopyala günlük dosyası (ya da ayrıntılı günlük veya hata günlüğü) yolu.</span><span class="sxs-lookup"><span data-stu-id="e8737-142">Path to the drive copy log file (either verbose log or error log).</span></span> <span data-ttu-id="e8737-143">Dosya Windows Azure içeri/dışarı aktarma hizmeti tarafından oluşturulan ve işle ilişkili blob depolama biriminden indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e8737-143">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span></span> <span data-ttu-id="e8737-144">Kopya günlük dosyası başarısız BLOB veya onarılması dosyaları hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="e8737-144">The copy log file contains information about failed blobs or files which are to be repaired.</span></span>|  
|<span data-ttu-id="e8737-145">**/ PathMapFile:**< DrivePathMapFile\></span><span class="sxs-lookup"><span data-stu-id="e8737-145">**/PathMapFile:**<DrivePathMapFile\></span></span>|<span data-ttu-id="e8737-146">**İsteğe bağlı.**</span><span class="sxs-lookup"><span data-stu-id="e8737-146">**Optional.**</span></span> <span data-ttu-id="e8737-147">Aldığınız aynı işlemde aynı ada sahip birden fazla dosya varsa belirsizlikleri çözümlemek için kullanılan bir metin dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="e8737-147">Path to a text file that can be used to resolve ambiguities if you have multiple files with the same name that you were importing in the same job.</span></span> <span data-ttu-id="e8737-148">İlk kez aracı çalıştırdığınızda, bu dosya tüm belirsiz adları ile doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8737-148">The first time the tool is run, it can populate this file with all of the ambiguous names.</span></span> <span data-ttu-id="e8737-149">Aracı'nın sonraki çalıştırır belirsizlikleri gidermek için bu dosyayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="e8737-149">Subsequent runs of the tool will use this file to resolve the ambiguities.</span></span>|  
  
## <a name="using-the-repairimport-command"></a><span data-ttu-id="e8737-150">RepairImport komutunu kullanma</span><span class="sxs-lookup"><span data-stu-id="e8737-150">Using the RepairImport command</span></span>  
<span data-ttu-id="e8737-151">İçeri aktarma verileri ağ üzerinden veri akış tarafından onarmak için alma kullanarak özgün dosyaları içeren dizinlerini belirt `/d` parametresi.</span><span class="sxs-lookup"><span data-stu-id="e8737-151">To repair import data by streaming the data over the network, you must specify the directories that contain the original files you were importing using the `/d` parameter.</span></span> <span data-ttu-id="e8737-152">Depolama hesabınızdan yüklediğiniz copy günlük dosyası da belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8737-152">You must also specify the copy log file that you downloaded from your storage account.</span></span> <span data-ttu-id="e8737-153">İçe aktarma işi kısmi hatalarıyla onarmak için tipik bir komut satırı şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="e8737-153">A typical command line to repair an import job with partial failures looks like:</span></span>  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
<span data-ttu-id="e8737-154">Kopya günlük dosyası örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e8737-154">The following is an example of a copy log file.</span></span> <span data-ttu-id="e8737-155">Bu durumda, bir alma işi sevk edilen sürücüde dosya 64 K parçası bozulmuş.</span><span class="sxs-lookup"><span data-stu-id="e8737-155">In this case, one 64K piece of a file was corrupted on the drive that was shipped for the import job.</span></span> <span data-ttu-id="e8737-156">Belirtilen tek hatası olduğundan iş bloblar geri kalanı başarıyla içeri aktarıldı.</span><span class="sxs-lookup"><span data-stu-id="e8737-156">Since this is the only failure indicated, the rest of the blobs in the job were successfully imported.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
<span data-ttu-id="e8737-157">Bu kopyalama günlük Azure içeri/dışarı aktarma aracı geçirildiğinde aracı eksik içeriği ağ üzerinden kopyalayarak bu dosya için alma işlemini bitirmek çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="e8737-157">When this copy log is passed to the Azure Import/Export Tool, the tool will try to finish the import for this file by copying the missing contents across the network.</span></span> <span data-ttu-id="e8737-158">Yukarıdaki örnekte aracı için özgün dosya görünür `\animals\koala.jpg` iki dizin içinde `C:\Users\bob\Pictures` ve `X:\BobBackup\photos`.</span><span class="sxs-lookup"><span data-stu-id="e8737-158">Following the example above, the tool will look for the original file `\animals\koala.jpg` within the two directories `C:\Users\bob\Pictures` and `X:\BobBackup\photos`.</span></span> <span data-ttu-id="e8737-159">Varsa dosyayı `C:\Users\bob\Pictures\animals\koala.jpg` yoksa, Azure içeri/dışarı aktarma aracı karşılık gelen blob veri eksik aralığını kopyalayacak `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.</span><span class="sxs-lookup"><span data-stu-id="e8737-159">If the file `C:\Users\bob\Pictures\animals\koala.jpg` exists, the Azure Import/Export Tool will copy the missing range of data to the corresponding blob `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.</span></span>  
  
## <a name="resolving-conflicts-when-using-repairimport"></a><span data-ttu-id="e8737-160">RepairImport kullanırken çakışmalarını çözme</span><span class="sxs-lookup"><span data-stu-id="e8737-160">Resolving conflicts when using RepairImport</span></span>  
<span data-ttu-id="e8737-161">Bazı durumlarda, aracı bulunamıyor veya gerekli dosya aşağıdaki nedenlerden birinden dolayı açmak mümkün olmayabilir: dosya bulunamadı, dosyanın erişilebilir değil, dosya adı belirsiz veya dosyanın içeriği artık doğru değil.</span><span class="sxs-lookup"><span data-stu-id="e8737-161">In some situations, the tool may not be able to find or open the necessary file for one of the following reasons: the file could not be found, the file is not accessible, the file name is ambiguous, or the content of the file is no longer correct.</span></span>  
  
<span data-ttu-id="e8737-162">Aracı bulmak çalışıyor belirsiz bir hata oluşabilir `\animals\koala.jpg` ve her ikisi de altında bu ada sahip bir dosya `C:\Users\bob\pictures` ve `X:\BobBackup\photos`.</span><span class="sxs-lookup"><span data-stu-id="e8737-162">An ambiguous error could occur if the tool is trying to locate `\animals\koala.jpg` and there is a file with that name under both `C:\Users\bob\pictures` and `X:\BobBackup\photos`.</span></span> <span data-ttu-id="e8737-163">Diğer bir deyişle, her ikisi de `C:\Users\bob\pictures\animals\koala.jpg` ve `X:\BobBackup\photos\animals\koala.jpg` alma işi sürücülerinde mevcut.</span><span class="sxs-lookup"><span data-stu-id="e8737-163">That is, both `C:\Users\bob\pictures\animals\koala.jpg` and `X:\BobBackup\photos\animals\koala.jpg` exist on the import job drives.</span></span>  
  
<span data-ttu-id="e8737-164">`/PathMapFile` Seçeneği, bu hataları gidermek ver.</span><span class="sxs-lookup"><span data-stu-id="e8737-164">The `/PathMapFile` option will allow you to resolve these errors.</span></span> <span data-ttu-id="e8737-165">Aracı'nı doğru şekilde belirlemek mümkün değildi dosyaların listesini dosyasını adını içeren belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8737-165">You can specify the name of the file which will contains the list of files that the tool was not able to correctly identify.</span></span> <span data-ttu-id="e8737-166">Doldurmak bir örnek komut satırı aşağıdadır `9WM35C2V_pathmap.txt`:</span><span class="sxs-lookup"><span data-stu-id="e8737-166">The following is an example command line that would populate `9WM35C2V_pathmap.txt`:</span></span>  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
<span data-ttu-id="e8737-167">Araç ardından sorunlu dosya yolları yazacak `9WM35C2V_pathmap.txt`, her satırda bir tane.</span><span class="sxs-lookup"><span data-stu-id="e8737-167">The tool will then write the problematic file paths to `9WM35C2V_pathmap.txt`, one on each line.</span></span> <span data-ttu-id="e8737-168">Örneğin, dosya, komutu çalıştırdıktan sonra aşağıdaki girdileri içerebilir:</span><span class="sxs-lookup"><span data-stu-id="e8737-168">For instance, the file may contain the following entries after running the command:</span></span>  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 <span data-ttu-id="e8737-169">Listedeki her dosya için araç kullanılabildiğinden emin olmak için dosyasını bulun ve açın denemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="e8737-169">For each file in the list, you should attempt to locate and open the file to ensure it is available to the tool.</span></span> <span data-ttu-id="e8737-170">Aracı açıkça bir dosyayı nerede bulacağını bildirir isterseniz, yol haritası değiştirebilir ve bir sekme karakteriyle ayrılmış aynı satırda her dosya yolunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e8737-170">If you wish to tell the tool explicitly where to find a file, you can modify the path map file and add the path to each file on the same line, separated by a tab character:</span></span>  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
<span data-ttu-id="e8737-171">Gerekli dosyaları aracı için kullanılabilir hale getirme veya yol haritası güncelleştirme sonra içeri aktarma işlemini tamamlamak için aracını çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8737-171">After making the necessary files available to the tool, or updating the path map file, you can rerun the tool to complete the import process.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="e8737-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e8737-172">Next steps</span></span>
 
* [<span data-ttu-id="e8737-173">Azure içeri/dışarı aktarma aracı ayarlama</span><span class="sxs-lookup"><span data-stu-id="e8737-173">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="e8737-174">Sabit sürücüleri içeri aktarma işine hazırlama</span><span class="sxs-lookup"><span data-stu-id="e8737-174">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="e8737-175">Kopyalama günlük dosyalarıyla iş durumunu gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="e8737-175">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="e8737-176">Bir dışarı aktarma işini onarma</span><span class="sxs-lookup"><span data-stu-id="e8737-176">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
* [<span data-ttu-id="e8737-177">Azure İçeri/Dışarı Aktarma Aracı ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="e8737-177">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
