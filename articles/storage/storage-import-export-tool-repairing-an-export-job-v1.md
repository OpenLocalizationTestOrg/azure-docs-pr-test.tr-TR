---
title: "bir Azure içeri/dışarı aktarma dışarı aktarma işinin - v1 aaaRepairing | Microsoft Docs"
description: "Nasıl toorepair oluşturulmuş ve kullanarak çalışan bir dışarı aktarma işinin hello Azure içeri/dışarı aktarma bilgi hizmeti."
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
ms.openlocfilehash: 96c674fc7c697c37882fb2980c340303896ac6c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="532e5-103">Bir dışarı aktarma işini onarma</span><span class="sxs-lookup"><span data-stu-id="532e5-103">Repairing an export job</span></span>
<span data-ttu-id="532e5-104">Bir dışarı aktarma işi tamamlandıktan sonra Microsoft Azure içeri/dışarı aktarma aracı şirket içi hello çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="532e5-104">After an export job has completed, you can run hello Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="532e5-105">Hello Azure içeri/dışarı aktarma hizmeti oluşturamıyor tooexport olduğunu dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="532e5-105">Download any files that hello Azure Import/Export service was unable tooexport.</span></span>  
  
2.  <span data-ttu-id="532e5-106">Merhaba dosyaları hello sürücüye doğru şekilde aktarılmış doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="532e5-106">Validate that hello files on hello drive were correctly exported.</span></span>  
  
<span data-ttu-id="532e5-107">Bu işlev bağlantısı tooAzure depolama toouse olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="532e5-107">You must have connectivity tooAzure Storage toouse this functionality.</span></span>  
  
<span data-ttu-id="532e5-108">içe aktarma işi onarmak için hello komutu **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="532e5-108">hello command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="532e5-109">RepairExport parametreleri</span><span class="sxs-lookup"><span data-stu-id="532e5-109">RepairExport parameters</span></span>

<span data-ttu-id="532e5-110">Merhaba aşağıdaki parametreleri ile belirtilebilir **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="532e5-110">hello following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="532e5-111">Parametre</span><span class="sxs-lookup"><span data-stu-id="532e5-111">Parameter</span></span>|<span data-ttu-id="532e5-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="532e5-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="532e5-113">**/ r: < RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="532e5-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="532e5-114">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="532e5-114">Required.</span></span> <span data-ttu-id="532e5-115">Hello onarım hello ilerleyişini izler ve tooresume kesintiye uğramış bir onarım veren yolu toohello onarım dosyası.</span><span class="sxs-lookup"><span data-stu-id="532e5-115">Path toohello repair file, which tracks hello progress of hello repair, and allows you tooresume an interrupted repair.</span></span> <span data-ttu-id="532e5-116">Her bir sürücü bir ve yalnızca bir onarım dosyası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="532e5-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="532e5-117">Belirli bir sürücü için onarım başlattığınızda, henüz var olmayan hello yolu tooa onarım dosyasında geçer.</span><span class="sxs-lookup"><span data-stu-id="532e5-117">When you start a repair for a given drive, you will pass in hello path tooa repair file which does not yet exist.</span></span> <span data-ttu-id="532e5-118">tooresume kesintiye uğramış bir onarım, varolan bir onarma dosyasını hello adlarında geçirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="532e5-118">tooresume an interrupted repair, you should pass in hello name of an existing repair file.</span></span> <span data-ttu-id="532e5-119">Merhaba onarım dosya karşılık gelen toohello hedef sürücüde her zaman belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="532e5-119">hello repair file corresponding toohello target drive must always be specified.</span></span>|  
|<span data-ttu-id="532e5-120">**/ LOGDIR: < LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="532e5-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="532e5-121">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="532e5-121">Optional.</span></span> <span data-ttu-id="532e5-122">Merhaba günlük dosyası dizini.</span><span class="sxs-lookup"><span data-stu-id="532e5-122">hello log directory.</span></span> <span data-ttu-id="532e5-123">Ayrıntılı günlük dosyalarını toothis dizin yazılır.</span><span class="sxs-lookup"><span data-stu-id="532e5-123">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="532e5-124">Günlük dizini belirtilirse, hello geçerli dizin hello günlük dizini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="532e5-124">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="532e5-125">**/ d: < TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="532e5-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="532e5-126">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="532e5-126">Required.</span></span> <span data-ttu-id="532e5-127">Merhaba dizin toovalidate ve Onar.</span><span class="sxs-lookup"><span data-stu-id="532e5-127">hello directory toovalidate and repair.</span></span> <span data-ttu-id="532e5-128">Bu genellikle hello verme sürücüsünün kök dizinindeki hello olmakla birlikte, bir ağ dosya paylaşımına dışarı hello dosyalarının bir kopyasını da içeren.</span><span class="sxs-lookup"><span data-stu-id="532e5-128">This is usually hello root directory of hello export drive, but could also be a network file share containing a copy of hello exported files.</span></span>|  
|<span data-ttu-id="532e5-129">**/BK: < BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="532e5-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="532e5-130">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="532e5-130">Optional.</span></span> <span data-ttu-id="532e5-131">Bir şifrelenmiş dosyaların nerede hello dışarı depolanır hello aracı toounlock istiyorsanız hello BitLocker anahtar belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="532e5-131">You should specify hello BitLocker key if you want hello tool toounlock an encrypted where hello exported files are stored.</span></span>|  
|<span data-ttu-id="532e5-132">**/sn: < StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="532e5-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="532e5-133">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="532e5-133">Required.</span></span> <span data-ttu-id="532e5-134">Merhaba depolama hesabının adını Hello hello için iş verin.</span><span class="sxs-lookup"><span data-stu-id="532e5-134">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="532e5-135">**/SK: < StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="532e5-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="532e5-136">**Gerekli** bir kapsayıcı SAS varsa ve yalnızca belirtilmezse.</span><span class="sxs-lookup"><span data-stu-id="532e5-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="532e5-137">Merhaba hesap anahtarı hello depolama hesabı hello için iş verin.</span><span class="sxs-lookup"><span data-stu-id="532e5-137">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="532e5-138">**/csas: < ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="532e5-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="532e5-139">**Gerekli** hello depolama hesabı anahtarı belirtilmezse varsa ve yalnızca.</span><span class="sxs-lookup"><span data-stu-id="532e5-139">**Required** if and only if hello storage account key is not specified.</span></span> <span data-ttu-id="532e5-140">Merhaba kapsayıcı SAS hello hello dışa aktarma işi ile ilişkili BLOB'ları erişmek için.</span><span class="sxs-lookup"><span data-stu-id="532e5-140">hello container SAS for accessing hello blobs associated with hello export job.</span></span>|  
|<span data-ttu-id="532e5-141">**/ CopyLogFile: < DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="532e5-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="532e5-142">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="532e5-142">Required.</span></span> <span data-ttu-id="532e5-143">Merhaba yol toohello sürücü kopyalama günlük dosyası.</span><span class="sxs-lookup"><span data-stu-id="532e5-143">hello path toohello drive copy log file.</span></span> <span data-ttu-id="532e5-144">Merhaba dosya hello Windows Azure içeri/dışarı aktarma hizmeti tarafından oluşturulan ve hello işle ilişkili hello blob depolama biriminden indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="532e5-144">hello file is generated by hello Windows Azure Import/Export service and can be downloaded from hello blob storage associated with hello job.</span></span> <span data-ttu-id="532e5-145">Merhaba kopyalama günlük dosyası başarısız BLOB veya onarıldı toobe dosyaları hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="532e5-145">hello copy log file contains information about failed blobs or files which are toobe repaired.</span></span>|  
|<span data-ttu-id="532e5-146">**/ Manıfestfıle: < DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="532e5-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="532e5-147">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="532e5-147">Optional.</span></span> <span data-ttu-id="532e5-148">Merhaba yolu toohello verme sürücünün bildirim dosyası.</span><span class="sxs-lookup"><span data-stu-id="532e5-148">hello path toohello export drive's manifest file.</span></span> <span data-ttu-id="532e5-149">Bu dosya hello Windows Azure içeri/dışarı aktarma hizmeti tarafından oluşturulan ve hello verme sürücüsünde ve isteğe bağlı olarak hello işle ilişkili hello depolama hesabındaki blob içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="532e5-149">This file is generated by hello Windows Azure Import/Export service and stored on hello export drive, and optionally in a blob in hello storage account associated with hello job.</span></span><br /><br /> <span data-ttu-id="532e5-150">Merhaba hello verme sürücüde hello dosyaların içeriğini bu dosyada bulunan hello MD5 karma ile doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="532e5-150">hello content of hello files on hello export drive will be verified with hello MD5 hashes contained in this file.</span></span> <span data-ttu-id="532e5-151">Bozuk belirlendiği toobe tüm dosyalar indirildi ve yeniden toohello hedef dizinleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="532e5-151">Any files that are determined toobe corrupted will be downloaded and rewritten toohello target directories.</span></span>|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a><span data-ttu-id="532e5-152">RepairExport kullanarak modu toocorrect dışarı aktarma başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="532e5-152">Using RepairExport mode toocorrect failed exports</span></span>  
<span data-ttu-id="532e5-153">Tooexport başarısız hello Azure içeri/dışarı aktarma aracı toodownload dosyalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="532e5-153">You can use hello Azure Import/Export Tool toodownload files that failed tooexport.</span></span> <span data-ttu-id="532e5-154">Merhaba kopyalama günlük dosyası tooexport başarısız dosyaların bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="532e5-154">hello copy log file will contain a list of files that failed tooexport.</span></span>  
  
<span data-ttu-id="532e5-155">Merhaba dışa aktarma hatalarının olasılıklar aşağıdaki hello nedenler:</span><span class="sxs-lookup"><span data-stu-id="532e5-155">hello causes of export failures include hello following possibilities:</span></span>  
  
-   <span data-ttu-id="532e5-156">Bozuk sürücüler</span><span class="sxs-lookup"><span data-stu-id="532e5-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="532e5-157">Merhaba depolama hesabı anahtarı Hello aktarma işlemi sırasında değiştirildi</span><span class="sxs-lookup"><span data-stu-id="532e5-157">hello storage account key changed during hello transfer process</span></span>  
  
<span data-ttu-id="532e5-158">toorun hello aracında **RepairExport** modu, ilk ihtiyacınız hello dışa aktarılan dosyaları tooyour bilgisayar içeren tooconnect hello sürücü.</span><span class="sxs-lookup"><span data-stu-id="532e5-158">toorun hello tool in **RepairExport** mode, you first need tooconnect hello drive containing hello exported files tooyour computer.</span></span> <span data-ttu-id="532e5-159">Ardından, hello hello yolu toothat sürücünün ile Merhaba belirtilmesi Azure içeri/dışarı aktarma aracı çalıştırın `/d` parametresi.</span><span class="sxs-lookup"><span data-stu-id="532e5-159">Next, run hello Azure Import/Export Tool, specifying hello path toothat drive with hello `/d` parameter.</span></span> <span data-ttu-id="532e5-160">İndirdiğiniz toospecify hello yolu toohello sürücünün kopyalama günlük dosyası da gerekir.</span><span class="sxs-lookup"><span data-stu-id="532e5-160">You also need toospecify hello path toohello drive's copy log file that you downloaded.</span></span> <span data-ttu-id="532e5-161">Merhaba aşağıdaki aşağıdaki komut satırı örnek hello aracı toorepair tooexport başarısız herhangi bir dosya çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="532e5-161">hello following command line example below runs hello tool toorepair any files that failed tooexport:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="532e5-162">Merhaba, bu bir blok hello başarısız blob tooexport gösteren günlük dosya Kopyala örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="532e5-162">hello following is an example of a copy log file that shows that one block in hello blob failed tooexport:</span></span>  
  
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
  
<span data-ttu-id="532e5-163">Merhaba kopyalama günlük dosyası hello Windows Azure içeri/dışarı aktarma hizmeti hello verme sürücüde hello blob'un blokları toohello dosyası birini indirme uygulanırken bir hata oluştu gösterir.</span><span class="sxs-lookup"><span data-stu-id="532e5-163">hello copy log file indicates that a failure occurred while hello Windows Azure Import/Export service was downloading one of hello blob's blocks toohello file on hello export drive.</span></span> <span data-ttu-id="532e5-164">diğer bileşenleri başarıyla indirildi hello dosyasının hello ve hello dosya uzunluğunu doğru şekilde ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="532e5-164">hello other components of hello file downloaded successfully, and hello file length was correctly set.</span></span> <span data-ttu-id="532e5-165">Bu durumda, hello aracı hello sürücüde hello dosyasını açın, hello blok hello depolama hesabından karşıdan yükle ve toohello dosya aralık uzaklığı 65536 uzunluğu 65536 ile başlayarak yazma.</span><span class="sxs-lookup"><span data-stu-id="532e5-165">In this case, hello tool will open hello file on hello drive, download hello block from hello storage account, and write it toohello file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a><span data-ttu-id="532e5-166">RepairExport toovalidate sürücü içeriğini kullanma</span><span class="sxs-lookup"><span data-stu-id="532e5-166">Using RepairExport toovalidate drive contents</span></span>  
<span data-ttu-id="532e5-167">Azure içeri/dışarı aktarma ile Merhaba kullanabilirsiniz **RepairExport** hello sürücü seçeneği toovalidate Merhaba içeriğine doğru.</span><span class="sxs-lookup"><span data-stu-id="532e5-167">You can also use Azure Import/Export with hello **RepairExport** option toovalidate hello contents on hello drive are correct.</span></span> <span data-ttu-id="532e5-168">Merhaba bildirim dosyası her dışarı aktarma sürücüde MD5s hello hello sürücü içeriğini içerir.</span><span class="sxs-lookup"><span data-stu-id="532e5-168">hello manifest file on each export drive contains MD5s for hello contents of hello drive.</span></span>  
  
<span data-ttu-id="532e5-169">Hello Azure içeri/dışarı aktarma hizmeti ayrıca hello bildirim dosyaları tooa depolama hesabı hello dışa aktarma işlemi sırasında kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="532e5-169">hello Azure Import/Export service can also save hello manifest files tooa storage account during hello export process.</span></span> <span data-ttu-id="532e5-170">Merhaba hello bildirim dosyalarının konumu hello kullanılabilir [alma işi](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) hello iş tamamlandığında işlemi.</span><span class="sxs-lookup"><span data-stu-id="532e5-170">hello location of hello manifest files is available via hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when hello job has completed.</span></span> <span data-ttu-id="532e5-171">Bkz: [içeri/dışarı aktarma hizmeti bildirim dosyası biçimi](storage-import-export-file-format-metadata-and-properties.md) sürücü bildirim dosyası hello biçimi hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="532e5-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about hello format of a drive manifest file.</span></span>  
  
<span data-ttu-id="532e5-172">Merhaba aşağıdaki örnekte nasıl toorun hello Azure içeri/dışarı aktarma aracı ile Merhaba gösterir **/ManifestFile** ve **/CopyLogFile** Parametreler:</span><span class="sxs-lookup"><span data-stu-id="532e5-172">hello following example shows how toorun hello Azure Import/Export Tool with hello **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="532e5-173">Merhaba, bir bildirim dosyası örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="532e5-173">hello following is an example of a manifest file:</span></span>  
  
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
  
<span data-ttu-id="532e5-174">Sonlandırma hello Onarım işleminden sonra hello aracı hello bildirim dosyasında başvurulan her bir dosya üzerinden okuma ve hello MD5 karma ile Merhaba dosyanın bütünlüğünü doğrular.</span><span class="sxs-lookup"><span data-stu-id="532e5-174">After finishing hello repair process, hello tool will read through each file referenced in hello manifest file and verify hello file's integrity with hello MD5 hashes.</span></span> <span data-ttu-id="532e5-175">Yukarıdaki Hello bildirimi için bileşenleri aşağıdaki hello geçer.</span><span class="sxs-lookup"><span data-stu-id="532e5-175">For hello manifest above, it will go through hello following components.</span></span>  

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

<span data-ttu-id="532e5-176">Merhaba doğrulama başarısız olan herhangi bir bileşeni hello aracı tarafından indirilir ve yeniden yazılmıştır hello sürücüde dosya aynı toohello.</span><span class="sxs-lookup"><span data-stu-id="532e5-176">Any component failing hello verification will be downloaded by hello tool and rewritten toohello same file on hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="532e5-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="532e5-177">Next steps</span></span>
 
* [<span data-ttu-id="532e5-178">Kurulum hello Azure içeri/dışarı aktarma aracı</span><span class="sxs-lookup"><span data-stu-id="532e5-178">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="532e5-179">Sabit sürücüleri içeri aktarma işine hazırlama</span><span class="sxs-lookup"><span data-stu-id="532e5-179">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="532e5-180">Kopyalama günlük dosyalarıyla iş durumunu gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="532e5-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="532e5-181">Bir içeri aktarma işini onarma</span><span class="sxs-lookup"><span data-stu-id="532e5-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="532e5-182">Sorun giderme hello Azure içeri/dışarı aktarma aracı</span><span class="sxs-lookup"><span data-stu-id="532e5-182">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
