---
title: "Bir Azure içeri/dışarı aktarma dışarı aktarma işinin - v1 onarma | Microsoft Docs"
description: "Oluşturulmuş ve Azure içeri/dışarı aktarma hizmeti kullanarak çalışan bir dışarı aktarma işinin onarmak öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 30ca0f8d06cb1927c19e66035ff485db0fc09e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="df6a2-103">Bir dışarı aktarma işini onarma</span><span class="sxs-lookup"><span data-stu-id="df6a2-103">Repairing an export job</span></span>
<span data-ttu-id="df6a2-104">Bir dışarı aktarma işi tamamlandıktan sonra Microsoft Azure içeri/dışarı aktarma aracı şirket içi çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="df6a2-104">After an export job has completed, you can run the Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="df6a2-105">Azure içeri/dışarı aktarma hizmeti veremedi dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="df6a2-105">Download any files that the Azure Import/Export service was unable to export.</span></span>  
  
2.  <span data-ttu-id="df6a2-106">Sürücüdeki dosyalar doğru aktarılmış doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="df6a2-106">Validate that the files on the drive were correctly exported.</span></span>  
  
<span data-ttu-id="df6a2-107">Bu işlevselliği kullanmak için Azure Storage bağlantısı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="df6a2-107">You must have connectivity to Azure Storage to use this functionality.</span></span>  
  
<span data-ttu-id="df6a2-108">İçe aktarma işi onarmak için komut **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="df6a2-108">The command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="df6a2-109">RepairExport parametreleri</span><span class="sxs-lookup"><span data-stu-id="df6a2-109">RepairExport parameters</span></span>

<span data-ttu-id="df6a2-110">Aşağıdaki parametreleri ile belirtilen **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="df6a2-110">The following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="df6a2-111">Parametre</span><span class="sxs-lookup"><span data-stu-id="df6a2-111">Parameter</span></span>|<span data-ttu-id="df6a2-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="df6a2-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="df6a2-113">**/ r: < RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="df6a2-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="df6a2-114">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="df6a2-114">Required.</span></span> <span data-ttu-id="df6a2-115">Onarım ilerleyişini izler ve kesintiye uğramış bir onarım sürdürmek için veren onarım dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="df6a2-115">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span></span> <span data-ttu-id="df6a2-116">Her bir sürücü bir ve yalnızca bir onarım dosyası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="df6a2-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="df6a2-117">Belirli bir sürücü için onarım başlattığınızda, henüz var olmayan bir onarım dosya yolunda geçer.</span><span class="sxs-lookup"><span data-stu-id="df6a2-117">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span></span> <span data-ttu-id="df6a2-118">Kesintiye uğramış bir onarım sürdürmek için varolan bir onarma dosya adına geçirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="df6a2-118">To resume an interrupted repair, you should pass in the name of an existing repair file.</span></span> <span data-ttu-id="df6a2-119">Onarım dosya hedef sürücüye karşılık gelen her zaman belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="df6a2-119">The repair file corresponding to the target drive must always be specified.</span></span>|  
|<span data-ttu-id="df6a2-120">**/ LOGDIR: < LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="df6a2-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="df6a2-121">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="df6a2-121">Optional.</span></span> <span data-ttu-id="df6a2-122">Günlük dosyası dizini.</span><span class="sxs-lookup"><span data-stu-id="df6a2-122">The log directory.</span></span> <span data-ttu-id="df6a2-123">Bu dizin için ayrıntılı günlük dosyalarına yazılır.</span><span class="sxs-lookup"><span data-stu-id="df6a2-123">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="df6a2-124">Günlük dizini belirtilmezse, geçerli dizin günlük dizini olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="df6a2-124">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="df6a2-125">**/ d: < TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="df6a2-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="df6a2-126">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="df6a2-126">Required.</span></span> <span data-ttu-id="df6a2-127">Doğrulama ve onarmak için dizin.</span><span class="sxs-lookup"><span data-stu-id="df6a2-127">The directory to validate and repair.</span></span> <span data-ttu-id="df6a2-128">Bu genellikle verme sürücüsünün kök dizinindeki olmakla birlikte, bir ağ dosya paylaşımı dışa aktarılan dosyaların bir kopyasını da içeren.</span><span class="sxs-lookup"><span data-stu-id="df6a2-128">This is usually the root directory of the export drive, but could also be a network file share containing a copy of the exported files.</span></span>|  
|<span data-ttu-id="df6a2-129">**/BK: < BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="df6a2-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="df6a2-130">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="df6a2-130">Optional.</span></span> <span data-ttu-id="df6a2-131">Bir şifrelenmiş dışa aktarılan dosyaların depolandığı kilidini açmak için aracın istiyorsanız BitLocker anahtarını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="df6a2-131">You should specify the BitLocker key if you want the tool to unlock an encrypted where the exported files are stored.</span></span>|  
|<span data-ttu-id="df6a2-132">**/sn: < StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="df6a2-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="df6a2-133">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="df6a2-133">Required.</span></span> <span data-ttu-id="df6a2-134">Dışa aktarma işi için depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="df6a2-134">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="df6a2-135">**/SK: < StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="df6a2-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="df6a2-136">**Gerekli** bir kapsayıcı SAS varsa ve yalnızca belirtilmezse.</span><span class="sxs-lookup"><span data-stu-id="df6a2-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="df6a2-137">Dışa aktarma işi için depolama hesabı için hesap anahtarı.</span><span class="sxs-lookup"><span data-stu-id="df6a2-137">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="df6a2-138">**/csas: < ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="df6a2-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="df6a2-139">**Gerekli** depolama hesabı anahtarı belirtilmezse varsa ve yalnızca.</span><span class="sxs-lookup"><span data-stu-id="df6a2-139">**Required** if and only if the storage account key is not specified.</span></span> <span data-ttu-id="df6a2-140">Dışa aktarma işi ile ilişkili BLOB'ları erişmek için kapsayıcı SAS.</span><span class="sxs-lookup"><span data-stu-id="df6a2-140">The container SAS for accessing the blobs associated with the export job.</span></span>|  
|<span data-ttu-id="df6a2-141">**/ CopyLogFile: < DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="df6a2-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="df6a2-142">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="df6a2-142">Required.</span></span> <span data-ttu-id="df6a2-143">Sürücüyü Kopyala günlük dosyası yolu.</span><span class="sxs-lookup"><span data-stu-id="df6a2-143">The path to the drive copy log file.</span></span> <span data-ttu-id="df6a2-144">Dosya Windows Azure içeri/dışarı aktarma hizmeti tarafından oluşturulan ve işle ilişkili blob depolama biriminden indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="df6a2-144">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span></span> <span data-ttu-id="df6a2-145">Kopya günlük dosyası başarısız BLOB veya onarılması dosyaları hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="df6a2-145">The copy log file contains information about failed blobs or files which are to be repaired.</span></span>|  
|<span data-ttu-id="df6a2-146">**/ Manıfestfıle: < DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="df6a2-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="df6a2-147">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="df6a2-147">Optional.</span></span> <span data-ttu-id="df6a2-148">Dışarı aktarma sürücünün bildirim dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="df6a2-148">The path to the export drive's manifest file.</span></span> <span data-ttu-id="df6a2-149">Bu dosya Windows Azure içeri/dışarı aktarma hizmeti tarafından oluşturulan ve dışarı aktarma sürücü ve isteğe bağlı olarak işle ilişkili depolama hesabındaki blob depolanır.</span><span class="sxs-lookup"><span data-stu-id="df6a2-149">This file is generated by the Windows Azure Import/Export service and stored on the export drive, and optionally in a blob in the storage account associated with the job.</span></span><br /><br /> <span data-ttu-id="df6a2-150">Dosyaları dışarı aktarma sürücüde içeriğini bu dosyada bulunan MD5 karma ile doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="df6a2-150">The content of the files on the export drive will be verified with the MD5 hashes contained in this file.</span></span> <span data-ttu-id="df6a2-151">Bozuk olduğu belirlenir herhangi bir dosya indirilir ve hedef dizinleri yeniden yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="df6a2-151">Any files that are determined to be corrupted will be downloaded and rewritten to the target directories.</span></span>|  
  
## <a name="using-repairexport-mode-to-correct-failed-exports"></a><span data-ttu-id="df6a2-152">Başarısız dışarı aktarmaları düzeltmek için RepairExport modunu kullanma</span><span class="sxs-lookup"><span data-stu-id="df6a2-152">Using RepairExport mode to correct failed exports</span></span>  
<span data-ttu-id="df6a2-153">Dışarı aktarılamadı dosyalarını indirmek için Azure içeri/dışarı aktarma aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df6a2-153">You can use the Azure Import/Export Tool to download files that failed to export.</span></span> <span data-ttu-id="df6a2-154">Dosya Kopyala günlük dışarı aktarılamadı dosyaların bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="df6a2-154">The copy log file will contain a list of files that failed to export.</span></span>  
  
<span data-ttu-id="df6a2-155">Dışarı aktarma hatalarının nedenlerini aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="df6a2-155">The causes of export failures include the following possibilities:</span></span>  
  
-   <span data-ttu-id="df6a2-156">Bozuk sürücüler</span><span class="sxs-lookup"><span data-stu-id="df6a2-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="df6a2-157">Aktarma işlemi sırasında değiştirilmiş depolama hesabı anahtarı</span><span class="sxs-lookup"><span data-stu-id="df6a2-157">The storage account key changed during the transfer process</span></span>  
  
<span data-ttu-id="df6a2-158">Aracı çalıştırmak için **RepairExport** modu, ilk ihtiyacınız bilgisayarınıza dışa aktarılan dosyaları içeren sürücü bağlanmak.</span><span class="sxs-lookup"><span data-stu-id="df6a2-158">To run the tool in **RepairExport** mode, you first need to connect the drive containing the exported files to your computer.</span></span> <span data-ttu-id="df6a2-159">Ardından, bu sürücüyle yolunu belirtme Azure içeri/dışarı aktarma aracı çalıştırın `/d` parametresi.</span><span class="sxs-lookup"><span data-stu-id="df6a2-159">Next, run the Azure Import/Export Tool, specifying the path to that drive with the `/d` parameter.</span></span> <span data-ttu-id="df6a2-160">Ayrıca indirdiğiniz sürücünün kopyalama günlük dosyası yolunu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="df6a2-160">You also need to specify the path to the drive's copy log file that you downloaded.</span></span> <span data-ttu-id="df6a2-161">Aşağıdaki komut satırı örnek dışarı aktarılamadı dosyalarını onarmak için aracını çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="df6a2-161">The following command line example below runs the tool to repair any files that failed to export:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="df6a2-162">Blob içinde bir bloğu gösterir kopyalama günlük dosyası örneği dışarı aktarılamadı verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="df6a2-162">The following is an example of a copy log file that shows that one block in the blob failed to export:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="df6a2-163">Windows Azure içeri/dışarı aktarma hizmeti blob'un blokları birini verme sürücüsündeki dosyanın indirilmesi edildi uygulanırken bir hata oluştu kopyalama günlük dosyasında belirtilir.</span><span class="sxs-lookup"><span data-stu-id="df6a2-163">The copy log file indicates that a failure occurred while the Windows Azure Import/Export service was downloading one of the blob's blocks to the file on the export drive.</span></span> <span data-ttu-id="df6a2-164">Dosyanın diğer bileşenleri başarıyla indirildi ve dosya uzunluğunu doğru şekilde ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="df6a2-164">The other components of the file downloaded successfully, and the file length was correctly set.</span></span> <span data-ttu-id="df6a2-165">Bu durumda, araç sürücüde dosyasını açın, blok depolama hesabından karşıdan yükle ve uzaklık 65536 uzunluğu 65536 ile başlayarak dosya aralığına yazma.</span><span class="sxs-lookup"><span data-stu-id="df6a2-165">In this case, the tool will open the file on the drive, download the block from the storage account, and write it to the file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-to-validate-drive-contents"></a><span data-ttu-id="df6a2-166">Sürücü içeriklerini doğrulamak için RepairExport kullanma</span><span class="sxs-lookup"><span data-stu-id="df6a2-166">Using RepairExport to validate drive contents</span></span>  
<span data-ttu-id="df6a2-167">Azure içeri/dışarı aktarma ile de kullanabileceğiniz **RepairExport** sürücüde içeriklerini doğrulamak için seçeneği doğru.</span><span class="sxs-lookup"><span data-stu-id="df6a2-167">You can also use Azure Import/Export with the **RepairExport** option to validate the contents on the drive are correct.</span></span> <span data-ttu-id="df6a2-168">Bildirim dosyası her dışarı aktarma sürücüde sürücü içeriğini için MD5s içerir.</span><span class="sxs-lookup"><span data-stu-id="df6a2-168">The manifest file on each export drive contains MD5s for the contents of the drive.</span></span>  
  
<span data-ttu-id="df6a2-169">Azure içeri/dışarı aktarma hizmeti de bildirim dosyaları bir depolama hesabı için dışa aktarma işlemi sırasında kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df6a2-169">The Azure Import/Export service can also save the manifest files to a storage account during the export process.</span></span> <span data-ttu-id="df6a2-170">Bildirim dosyalarının konumunu aracılığıyla kullanılabilir [alma işi](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) iş tamamlandığında işlemi.</span><span class="sxs-lookup"><span data-stu-id="df6a2-170">The location of the manifest files is available via the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when the job has completed.</span></span> <span data-ttu-id="df6a2-171">Bkz: [içeri/dışarı aktarma hizmeti bildirim dosyası biçimi](storage-import-export-file-format-metadata-and-properties.md) sürücü bildirim dosyası biçimi hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="df6a2-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about the format of a drive manifest file.</span></span>  
  
<span data-ttu-id="df6a2-172">Aşağıdaki örnek, Azure içeri/dışarı aktarma aracı ile çalıştırmak gösterilmiştir **/ManifestFile** ve **/CopyLogFile** Parametreler:</span><span class="sxs-lookup"><span data-stu-id="df6a2-172">The following example shows how to run the Azure Import/Export Tool with the **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="df6a2-173">Bildirim dosyası örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="df6a2-173">The following is an example of a manifest file:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
<span data-ttu-id="df6a2-174">Onarım işlemi bittikten sonra aracı bildirim dosyasında başvurulan her bir dosya aracılığıyla okuma ve MD5 karma ile dosya bütünlüğünü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="df6a2-174">After finishing the repair process, the tool will read through each file referenced in the manifest file and verify the file's integrity with the MD5 hashes.</span></span> <span data-ttu-id="df6a2-175">Listesi için aşağıdaki bileşenleri geçer.</span><span class="sxs-lookup"><span data-stu-id="df6a2-175">For the manifest above, it will go through the following components.</span></span>  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

<span data-ttu-id="df6a2-176">Doğrulama başarısız olan herhangi bir bileşeni aracı tarafından indirilir ve sürücüde aynı dosyaya yeniden yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="df6a2-176">Any component failing the verification will be downloaded by the tool and rewritten to the same file on the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="df6a2-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="df6a2-177">Next steps</span></span>
 
* [<span data-ttu-id="df6a2-178">Azure içeri/dışarı aktarma aracı ayarlama</span><span class="sxs-lookup"><span data-stu-id="df6a2-178">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="df6a2-179">Sabit sürücüleri içeri aktarma işine hazırlama</span><span class="sxs-lookup"><span data-stu-id="df6a2-179">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="df6a2-180">Kopyalama günlük dosyalarıyla iş durumunu gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="df6a2-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="df6a2-181">Bir içeri aktarma işini onarma</span><span class="sxs-lookup"><span data-stu-id="df6a2-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="df6a2-182">Azure İçeri/Dışarı Aktarma Aracı ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="df6a2-182">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
