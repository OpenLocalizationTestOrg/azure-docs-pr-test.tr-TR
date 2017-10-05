---
title: "Kopyalama veya Windows Azure Storage ile AzCopy için veri taşıma | Microsoft Docs"
description: "AzCopy üzerinde bir Windows yardımcı programı taşımak veya için veya blob, tablo ve dosya içeriği veri kopyalamak için kullanın. Verileri Azure depolama birimine yerel dosyalarından kopyalamak veya içinde veya depolama hesapları arasında veri kopyalama. Kolayca verilerinizi Azure depolama alanına geçiş."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: 9806697747b2409d4bd0ae19dc0b9fe01f500dc0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-data-with-the-azcopy-on-windows"></a><span data-ttu-id="c728b-105">Windows AzCopy ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="c728b-105">Transfer data with the AzCopy on Windows</span></span>
<span data-ttu-id="c728b-106">AzCopy en uygun performans ile basit komutları kullanarak Microsoft Azure Blob, dosya ve tablo depolama gelen ve giden veri kopyalamak için tasarlanmış bir komut satırı yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="c728b-106">AzCopy is a command-line utility designed for copying data to and from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="c728b-107">Verileri bir nesneden diğerine depolama hesabınızda veya depolama hesapları arasında kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c728b-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="c728b-108">İndirebilirsiniz AzCopy iki sürümü vardır.</span><span class="sxs-lookup"><span data-stu-id="c728b-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="c728b-109">AzCopy Windows .NET Framework ile oluşturulur ve Windows stili komut satırı seçenekleri sunar.</span><span class="sxs-lookup"><span data-stu-id="c728b-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="c728b-110">[Linux üzerinde AzCopy](storage-use-azcopy-linux.md) çekirdek, POSIX stili komut satırı seçenekleri sunan Linux platformlar hedefler ile .NET Framework yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="c728b-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="c728b-111">Bu makalede Windows AzCopy kapsar.</span><span class="sxs-lookup"><span data-stu-id="c728b-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="c728b-112">AzCopy yükleyip</span><span class="sxs-lookup"><span data-stu-id="c728b-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="c728b-113">Windows üzerinde AzCopy</span><span class="sxs-lookup"><span data-stu-id="c728b-113">AzCopy on Windows</span></span>
<span data-ttu-id="c728b-114">Karşıdan [AzCopy Windows en son sürümünü](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="c728b-114">Download the [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="c728b-115">Windows yükleme</span><span class="sxs-lookup"><span data-stu-id="c728b-115">Installation on Windows</span></span>
<span data-ttu-id="c728b-116">Windows Installer kullanarak AzCopy yükledikten sonra bir komut penceresi açın ve bilgisayarınızda - AzCopy yükleme dizinine gidin nerede `AzCopy.exe` yürütülebilir bulunur.</span><span class="sxs-lookup"><span data-stu-id="c728b-116">After installing AzCopy on Windows using the installer, open a command window and navigate to the AzCopy installation directory on your computer - where the `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="c728b-117">İsterseniz, AzCopy yükleme konumu sistem yoluna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c728b-117">If desired, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="c728b-118">AzCopy varsayılan olarak, yüklü `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` veya `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="c728b-118">By default, AzCopy is installed to `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="c728b-119">İlk AzCopy komut yazma</span><span class="sxs-lookup"><span data-stu-id="c728b-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="c728b-120">AzCopy komutları temel sözdizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="c728b-120">The basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="c728b-121">Aşağıdaki örnekler, çeşitli veri ve Microsoft Azure BLOB'ları, dosyaları ve tablolardan kopyalama için senaryolarda göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="c728b-121">The following examples demonstrate a variety of scenarios for copying data to and from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="c728b-122">Başvurmak [AzCopy parametreleri](#azcopy-parameters) her örnekte kullanılan parametreleri ayrıntılı bir açıklaması için bölüm.</span><span class="sxs-lookup"><span data-stu-id="c728b-122">Refer to the [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="c728b-123">BLOB: karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="c728b-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="c728b-124">Tek blob indirin</span><span class="sxs-lookup"><span data-stu-id="c728b-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="c728b-125">Klasör unutmayın `C:\myfolder` yok, AzCopy oluşturur ve indirme `abc.txt ` yeni klasöre.</span><span class="sxs-lookup"><span data-stu-id="c728b-125">Note that if the folder `C:\myfolder` does not exist, AzCopy creates it and download `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="c728b-126">Tek blob ikincil bölge ' indirin</span><span class="sxs-lookup"><span data-stu-id="c728b-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="c728b-127">Okuma erişimli coğrafi olarak yedekli depolama etkin olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="c728b-128">Tüm BLOB'ları indirme</span><span class="sxs-lookup"><span data-stu-id="c728b-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="c728b-129">Aşağıdaki BLOB'ları belirtilen kapsayıcıda bulunan varsayın:</span><span class="sxs-lookup"><span data-stu-id="c728b-129">Assume the following blobs reside in the specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="c728b-130">Dizin yükleme işleminden sonra `C:\myfolder` aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="c728b-130">After the download operation, the directory `C:\myfolder` includes the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="c728b-131">Seçeneği belirtmezseniz, `/S`, blob yok indirilir.</span><span class="sxs-lookup"><span data-stu-id="c728b-131">If you do not specify option `/S`, no blobs are downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="c728b-132">BLOB'lar ile belirtilen bir önek indirin</span><span class="sxs-lookup"><span data-stu-id="c728b-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="c728b-133">Aşağıdaki BLOB'ları belirtilen kapsayıcıda bulunan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="c728b-133">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="c728b-134">Önek ile başlayan tüm BLOB'lar `a` yüklenir:</span><span class="sxs-lookup"><span data-stu-id="c728b-134">All blobs beginning with the prefix `a` are downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="c728b-135">Klasör yükleme işleminden sonra `C:\myfolder` aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="c728b-135">After the download operation, the folder `C:\myfolder` includes the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="c728b-136">Önek blob adı ilk bölümü forms bir sanal dizin geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c728b-136">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="c728b-137">Yüklenmez şekilde yukarıda gösterilen örnekte, sanal dizin belirtilen bir önek eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="c728b-137">In the example shown above, the virtual directory does not match the specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="c728b-138">Ayrıca, varsa seçeneği `\S` belirtilmezse, AzCopy BLOB indirmek değil.</span><span class="sxs-lookup"><span data-stu-id="c728b-138">In addition, if the option `\S` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="c728b-139">Kaynak BLOB olarak aynı olmalıdır dışarı aktarılan dosyaların son değiştirme zamanı ayarlama</span><span class="sxs-lookup"><span data-stu-id="c728b-139">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="c728b-140">Son değiştiren bunların zamana dayalı indirme işlemi de BLOB'lar hariç tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c728b-140">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="c728b-141">Son değişiklik zamanı BLOB'lar dışlamak istiyorsanız, örneğin, aynı veya daha yeni hedef dosya eklemektir `/XN` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="c728b-141">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="c728b-142">Ya da son değişiklik zamanı BLOB'lar hariç tutmak istediğiniz ise, aynı veya daha eski hedef dosya ekleme `/XO` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="c728b-142">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="c728b-143">BLOB: karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="c728b-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="c728b-144">Tek dosya karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="c728b-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="c728b-145">Belirtilen hedef kapsayıcı mevcut değilse, AzCopy oluşturur ve dosyayı içine yükler.</span><span class="sxs-lookup"><span data-stu-id="c728b-145">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="c728b-146">Sanal dizin için tek dosya karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="c728b-146">Upload single file to virtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="c728b-147">Belirtilen sanal dizin yoksa, AzCopy sanal dizin adını eklemek için dosyayı yükler (*örneğin*, `vd/abc.txt` Yukarıdaki örnekteki).</span><span class="sxs-lookup"><span data-stu-id="c728b-147">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in its name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="c728b-148">Tüm dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="c728b-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="c728b-149">Seçeneğini belirterek `/S` belirtilen dizin içeriğini tüm alt klasörleri ve bunların dosyaları da karşıya anlamı Blob Depolama yinelemeli olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="c728b-149">Specifying option `/S` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="c728b-150">Örneğin, aşağıdaki dosyaları klasöründe bulunan varsayın `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="c728b-150">For instance, assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="c728b-151">Karşıya yükleme işleminden sonra kapsayıcı aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="c728b-151">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="c728b-152">Seçeneği belirtmezseniz, `/S`, AzCopy yinelemeli olarak karşıya değil.</span><span class="sxs-lookup"><span data-stu-id="c728b-152">If you do not specify option `/S`, AzCopy does not upload recursively.</span></span> <span data-ttu-id="c728b-153">Karşıya yükleme işleminden sonra kapsayıcı aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="c728b-153">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="c728b-154">Belirtilen desenle eşleşen dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="c728b-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="c728b-155">Aşağıdaki dosyaları klasöründe bulunan varsayın `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="c728b-155">Assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="c728b-156">Karşıya yükleme işleminden sonra kapsayıcı aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="c728b-156">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="c728b-157">Seçeneği belirtmezseniz, `/S`, AzCopy yalnızca sanal bir dizinde bulunan değilsiniz BLOB'ları yükler:</span><span class="sxs-lookup"><span data-stu-id="c728b-157">If you do not specify option `/S`, AzCopy only uploads blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="c728b-158">Hedef blob MIME içerik türünü belirtin</span><span class="sxs-lookup"><span data-stu-id="c728b-158">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="c728b-159">Varsayılan olarak, içerik türü için bir hedef blob AzCopy ayarlar `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="c728b-159">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="c728b-160">3.1.0 sürümünden başlayarak, içerik türü seçeneği açıkça belirtebilirsiniz `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="c728b-160">Beginning with version 3.1.0, you can explicitly specify the content type via the option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="c728b-161">Bu sözdiziminin bir karşıya yükleme işleminde tüm BLOB'lar için içerik türünü ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c728b-161">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="c728b-162">Belirtirseniz `/SetContentType` olmayan bir değer, AzCopy her bir blob veya dosyanın içerik türü dosya uzantısını göre ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c728b-162">If you specify `/SetContentType` without a value, AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="c728b-163">BLOB: kopyalama</span><span class="sxs-lookup"><span data-stu-id="c728b-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="c728b-164">Depolama hesabı içinde tek blob kopyalama</span><span class="sxs-lookup"><span data-stu-id="c728b-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="c728b-165">Bir depolama hesabındaki blob kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c728b-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="c728b-166">Tek blob depolama hesapları arasında kopyalama</span><span class="sxs-lookup"><span data-stu-id="c728b-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="c728b-167">Bir blob depolama hesapları arasında kopyaladığınızda, bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c728b-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="c728b-168">Birincil bölge ikincil bölge'den blob'a tek kopyalama</span><span class="sxs-lookup"><span data-stu-id="c728b-168">Copy single blob from secondary region to primary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="c728b-169">Okuma erişimli coğrafi olarak yedekli depolama etkin olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="c728b-170">Depolama hesapları arasında tek blob ve onun anlık görüntüleri kopyalama</span><span class="sxs-lookup"><span data-stu-id="c728b-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="c728b-171">Kopyalama işleminden sonra hedef kapsayıcı blob ve onun anlık görüntülerini içerir.</span><span class="sxs-lookup"><span data-stu-id="c728b-171">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="c728b-172">Kapsayıcı, blob yukarıdaki örnekte iki anlık görüntülere sahip olduğu varsayılarak, aşağıdaki blob ve anlık görüntüleri içerir:</span><span class="sxs-lookup"><span data-stu-id="c728b-172">Assuming the blob in the example above has two snapshots, the container includes the following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="c728b-173">Zaman uyumlu olarak depolama hesapları arasında BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="c728b-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="c728b-174">AzCopy varsayılan olarak, iki depolama uç noktaları arasında verileri zaman uyumsuz olarak kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c728b-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="c728b-175">Bu nedenle, kopyalama işlemi nasıl bakımından hiçbir SLA hızlı sahip yedek bant genişliğini kapasite kullanarak arka blob kopyalanır ve kopyalama tamamlandı başarısız oldu veya kadar AzCopy kopya durumunu düzenli olarak denetler. çalışır.</span><span class="sxs-lookup"><span data-stu-id="c728b-175">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied, and AzCopy periodically checks the copy status until the copying is completed or failed.</span></span>

<span data-ttu-id="c728b-176">`/SyncCopy` Seçeneği sağlar kopyalama işlemi tutarlı hızı alır.</span><span class="sxs-lookup"><span data-stu-id="c728b-176">The `/SyncCopy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="c728b-177">AzCopy zaman uyumlu kopyası yerel bellek için belirtilen kaynak kopyalamak için BLOB'ları karşıdan yükleyip ardından Blob Depolama hedefe karşıya yükleme gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="c728b-177">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="c728b-178">`/SyncCopy`zaman uyumsuz kopyaya karşılaştırıldığında ek çıkışı maliyeti oluşturabilir, çıkışı maliyeti önlemek için kaynak depolama hesabınız ile aynı bölgede olan Azure VM'deki bu seçeneği kullanmak için önerilen yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="c728b-178">`/SyncCopy` might generate additional egress cost compared to asynchronous copy, the recommended approach is to use this option in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="c728b-179">Dosya: karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="c728b-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="c728b-180">Tek dosya indirme</span><span class="sxs-lookup"><span data-stu-id="c728b-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="c728b-181">Belirtilen kaynak bir Azure dosya paylaşımıdır sonra ya da tam dosya adını belirtmeniz gerekir (*örneğin* `abc.txt`) tek bir dosya indirme veya seçenek belirtmek için `/S` paylaşımı yinelemeli olarak tüm dosyaları indirmek için.</span><span class="sxs-lookup"><span data-stu-id="c728b-181">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `/S` to download all files in the share recursively.</span></span> <span data-ttu-id="c728b-182">Bir dosya düzeni ve seçenek belirtmek çalışırken `/S` birlikte hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="c728b-182">Attempting to specify both a file pattern and option `/S` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="c728b-183">Tüm dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="c728b-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="c728b-184">Boş klasörleri indirilmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-184">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="c728b-185">Dosya: karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="c728b-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="c728b-186">Tek dosya karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="c728b-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="c728b-187">Tüm dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="c728b-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="c728b-188">Boş klasörleri değil karşıya unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-188">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="c728b-189">Belirtilen desenle eşleşen dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="c728b-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="c728b-190">Dosya: kopyalama</span><span class="sxs-lookup"><span data-stu-id="c728b-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="c728b-191">Dosya paylaşımlarında kopyalayın</span><span class="sxs-lookup"><span data-stu-id="c728b-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="c728b-192">Dosya paylaşımlarında bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c728b-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="c728b-193">BLOB dosya paylaşımından kopyalayın</span><span class="sxs-lookup"><span data-stu-id="c728b-193">Copy from file share to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="c728b-194">Dosya blob öğesine dosya paylaşımından kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c728b-194">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="c728b-195">BLOB üzerinden dosya paylaşımına kopyalayın</span><span class="sxs-lookup"><span data-stu-id="c728b-195">Copy from blob to file share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="c728b-196">Dosya Paylaşımı için blobundan bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c728b-196">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="c728b-197">Zaman uyumlu olarak dosyaları kopyalayın</span><span class="sxs-lookup"><span data-stu-id="c728b-197">Synchronously copy files</span></span>
<span data-ttu-id="c728b-198">Belirleyebileceğiniz `/SyncCopy` dosya depolama dosya depolama alanına, Blob Depolama birimine dosya depolama ve File Storage için Blob depolama biriminden verileri zaman uyumlu olarak kopyalamak için seçenek, AzCopy bu veri kaynağını yerel belleğe yükleyerek yapar ve hedefe yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c728b-198">You can specify the `/SyncCopy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously, AzCopy does this by downloading the source data to local memory and upload it again to destination.</span></span> <span data-ttu-id="c728b-199">Standart çıkış maliyet geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c728b-199">Standard egress cost applies.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="c728b-200">Dosya depolama biriminden Blob depolama alanına kopyalama işlemi sırasında varsayılan blob türü blok blobu, kullanıcı seçeneği belirtebilirsiniz `/BlobType:page` hedef blob türünü değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c728b-200">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="c728b-201">Unutmayın `/SyncCopy` zaman uyumsuz kopyaya karşılaştırma maliyet ek çıkış oluşturabilir, Azure VM'deki çıkışı maliyeti önlemek için kaynak depolama hesabınız ile aynı bölgede olan bu seçeneği kullanmak için önerilen yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="c728b-201">Note that `/SyncCopy` might generate additional egress cost comparing to asynchronous copy, the recommended approach is to use this option in the Azure VM which is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="c728b-202">Tablo: dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="c728b-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="c728b-203">Dışarı aktarma tablosu</span><span class="sxs-lookup"><span data-stu-id="c728b-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="c728b-204">AzCopy bildirim dosyası belirtilen hedef klasöre yazar.</span><span class="sxs-lookup"><span data-stu-id="c728b-204">AzCopy writes a manifest file to the specified destination folder.</span></span> <span data-ttu-id="c728b-205">Bildirim dosyası alma işleminde gerekli veri dosyalarını bulmak ve veri doğrulama gerçekleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c728b-205">The manifest file is used in the import process to locate the necessary data files and perform data validation.</span></span> <span data-ttu-id="c728b-206">Bildirim dosyası, varsayılan olarak aşağıdaki adlandırma kuralını kullanır:</span><span class="sxs-lookup"><span data-stu-id="c728b-206">The manifest file uses the following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="c728b-207">Kullanıcı ayrıca seçeneğini belirtin `/Manifest:<manifest file name>` yayılma dosyası adı ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="c728b-207">User can also specify the option `/Manifest:<manifest file name>` to set the manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="c728b-208">Birden çok dosyalarına bölünmüş dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="c728b-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="c728b-209">AzCopy kullanan bir *birim dizin* birden çok dosya ayırt etmek için bölünmüş veri dosya adları.</span><span class="sxs-lookup"><span data-stu-id="c728b-209">AzCopy uses a *volume index* in the split data file names to distinguish multiple files.</span></span> <span data-ttu-id="c728b-210">Birim dizini iki bölümden oluşur bir *bölüm anahtarı aralığının dizin* ve *bölünmüş dosya dizini*.</span><span class="sxs-lookup"><span data-stu-id="c728b-210">The volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="c728b-211">Her iki dizinleri sıfır tabanlı.</span><span class="sxs-lookup"><span data-stu-id="c728b-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="c728b-212">Kullanıcı seçeneği belirlemezse bölüm anahtarı aralığının dizini 0'dır `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="c728b-212">The partition key range index is 0 if the user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="c728b-213">Örneğin, AzCopy seçeneği kullanıcının belirttiği sonra iki veri dosyalarını oluşturur düşünelim `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="c728b-213">For instance, suppose AzCopy generates two data files after the user specifies option `/SplitSize`.</span></span> <span data-ttu-id="c728b-214">Sonuçta elde edilen veri dosya adları olabilir:</span><span class="sxs-lookup"><span data-stu-id="c728b-214">The resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="c728b-215">Mümkün olan en düşük değer seçenek için Not `/SplitSize` 32 MB'dir.</span><span class="sxs-lookup"><span data-stu-id="c728b-215">Note that the minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="c728b-216">Belirtilen hedef Blob Depolama alanı ise, kendi boyutları blob boyutu sınırlaması (200 GB) ulaştığında AzCopy veri dosyasını ayırır, bakılmaksızın olup seçeneği `/SplitSize` kullanıcı tarafından belirtilen.</span><span class="sxs-lookup"><span data-stu-id="c728b-216">If the specified destination is Blob storage, AzCopy splits the data file once its sizes reaches the blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by the user.</span></span>

### <a name="export-table-to-json-or-csv-data-file-format"></a><span data-ttu-id="c728b-217">Tablo verme JSON veya CSV veri dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="c728b-217">Export table to JSON or CSV data file format</span></span>
<span data-ttu-id="c728b-218">Varsayılan olarak AzCopy tablolar JSON veri dosyalarını dışarı aktarır.</span><span class="sxs-lookup"><span data-stu-id="c728b-218">AzCopy by default exports tables to JSON data files.</span></span> <span data-ttu-id="c728b-219">Seçeneğini belirtebilirsiniz `/PayloadFormat:JSON|CSV` tablolar JSON veya CSV dışarı aktarmak için.</span><span class="sxs-lookup"><span data-stu-id="c728b-219">You can specify the option `/PayloadFormat:JSON|CSV` to export the tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="c728b-220">AzCopy CSV yük biçimi belirtirken, aynı zamanda dosya uzantısına sahip bir şema dosyası oluşturur. `.schema.csv` her veri dosyası için.</span><span class="sxs-lookup"><span data-stu-id="c728b-220">When specifying the CSV payload format, AzCopy also generates a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="c728b-221">Tablo varlıkları eşzamanlı olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="c728b-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="c728b-222">AzCopy başlatır kullanıcı seçeneği belirttiğinde varlıklar dışarı aktarmak için eşzamanlı işlem `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="c728b-222">AzCopy starts concurrent operations to export entities when the user specifies option `/PKRS`.</span></span> <span data-ttu-id="c728b-223">Her bir işlemin bir bölüm anahtarı aralığının dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="c728b-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="c728b-224">Eşzamanlı işlem sayısını da seçeneği tarafından denetlendiğini unutmayın `/NC`.</span><span class="sxs-lookup"><span data-stu-id="c728b-224">Note that the number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="c728b-225">AzCopy kullandığı Çekirdek İşlemci sayısı varsayılan değer olarak `/NC` tablo varlıkları kopyalarken olsa bile `/NC` belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="c728b-225">AzCopy uses the number of core processors as the default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="c728b-226">Kullanıcı seçeneği belirttiğinde `/PKRS`, AzCopy kullanan iki değerden daha küçük - bölüm anahtar aralıklarına karşı örtük veya açık olarak belirtilen eşzamanlı operasyonlar - çok başlatmak için eşzamanlı işlem sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="c728b-226">When the user specifies option `/PKRS`, AzCopy uses the smaller of the two values - partition key ranges versus implicitly or explicitly specified concurrent operations - to determine the number of concurrent operations to start.</span></span> <span data-ttu-id="c728b-227">Daha fazla ayrıntı için yazın `AzCopy /?:NC` komut satırında.</span><span class="sxs-lookup"><span data-stu-id="c728b-227">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="export-table-to-blob"></a><span data-ttu-id="c728b-228">BLOB tabloyu dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="c728b-228">Export table to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="c728b-229">AzCopy bir JSON veri dosyası adlandırma kuralı aşağıdaki ile blob kapsayıcısı içinde oluşturur:</span><span class="sxs-lookup"><span data-stu-id="c728b-229">AzCopy generates a JSON data file into the blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="c728b-230">Oluşturulan JSON veri dosyası en küçük meta verileri için yük biçimi izler.</span><span class="sxs-lookup"><span data-stu-id="c728b-230">The generated JSON data file follows the payload format for minimal metadata.</span></span> <span data-ttu-id="c728b-231">Bu yük biçimi hakkında daha fazla bilgi için bkz: [tablo hizmeti işlemleri için yük biçimi](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="c728b-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="c728b-232">Tablolar için BLOB'ları dışarı aktarılırken AzCopy tablo varlıkları yerel geçici veri dosyalarını indirir ve ardından bu varlıkların blob yükler olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-232">Note that when exporting tables to blobs, AzCopy downloads the Table entities to local temporary data files and then uploads those entities to the blob.</span></span> <span data-ttu-id="c728b-233">Bu geçici veri dosyalarını varsayılan yolu ile günlük dosyası klasöre yerleştirilir "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>" olarak seçeneği belirtebilirsiniz/değişiklik günlüğü için [günlük dosyası klasörü] Z: dosya klasör konumu ve böylece geçici veri dosyaları konumunu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c728b-233">These temporary data files are put into the journal file folder with the default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] to change the journal file folder location and thus change the temporary data files location.</span></span> <span data-ttu-id="c728b-234">Blob için karşıya sonra yerel disk geçici veri dosyasında hemen silinir rağmen dosyalarının boyutu, tablo varlıklarınızı boyutu ve seçeneği /SplitSize ile belirtilen boyutu tarafından belirlenir geçici verileri Lütfen elinizde yeterince yerel sağlayın silinmeden önce bu geçici veri dosyalarını depolamak için disk alanı.</span><span class="sxs-lookup"><span data-stu-id="c728b-234">The temporary data files' size is decided by your table entities' size and the size you specified with the option /SplitSize, although the temporary data file in local disk is deleted instantly once it has been uploaded to the blob, please make sure you have enough local disk space to store these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="c728b-235">Tablo: alma</span><span class="sxs-lookup"><span data-stu-id="c728b-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="c728b-236">Alma tablosu</span><span class="sxs-lookup"><span data-stu-id="c728b-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="c728b-237">Seçenek `/EntityOperation` tabloya varlıklar ekleme gösterir.</span><span class="sxs-lookup"><span data-stu-id="c728b-237">The option `/EntityOperation` indicates how to insert entities into the table.</span></span> <span data-ttu-id="c728b-238">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c728b-238">Possible values are:</span></span>

* <span data-ttu-id="c728b-239">`InsertOrSkip`: Var olan bir varlığı atlar veya tabloda mevcut değilse yeni bir varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="c728b-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="c728b-240">`InsertOrMerge`: Birleştirir var olan bir varlığı veya tabloda mevcut değilse yeni bir varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="c728b-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="c728b-241">`InsertOrReplace`: Var olan bir varlığı değiştirir veya tabloda mevcut değilse yeni bir varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="c728b-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="c728b-242">Seçeneği belirtemezsiniz Not `/PKRS` alma senaryoda.</span><span class="sxs-lookup"><span data-stu-id="c728b-242">Note that you cannot specify option `/PKRS` in the import scenario.</span></span> <span data-ttu-id="c728b-243">İçinde belirtmelisiniz seçeneği verme senaryo aksine `/PKRS` tablo içeri aktardığınızda eşzamanlı işlem başlatmak için AzCopy eşzamanlı operasyonlar varsayılan olarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="c728b-243">Unlike the export scenario, in which you must specify option `/PKRS` to start concurrent operations, AzCopy starts concurrent operations by default when you import a table.</span></span> <span data-ttu-id="c728b-244">Varsayılan eşzamanlı işlemleri başlatıldı çekirdekli işlemciler sayıya eşit sayısıdır; Bununla birlikte, eşzamanlı seçeneğiyle farklı sayıda belirtebilirsiniz `/NC`.</span><span class="sxs-lookup"><span data-stu-id="c728b-244">The default number of concurrent operations started is equal to the number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="c728b-245">Daha fazla ayrıntı için yazın `AzCopy /?:NC` komut satırında.</span><span class="sxs-lookup"><span data-stu-id="c728b-245">For more details, type `AzCopy /?:NC` at the command line.</span></span>

<span data-ttu-id="c728b-246">AzCopy yalnızca JSON değil CSV içe aktarma desteklediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="c728b-247">AzCopy değil kullanıcı tarafından oluşturulan JSON öğesinden tablo içeri aktarmalar destekler ve dosyaları bildirimi.</span><span class="sxs-lookup"><span data-stu-id="c728b-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="c728b-248">Bu dosyaların her ikisinin bir AzCopy tablo verme etki alanından gelmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c728b-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="c728b-249">Hatalarını önlemek için lütfen dışarı aktarılan JSON değiştirmeyin veya bildirim dosyası.</span><span class="sxs-lookup"><span data-stu-id="c728b-249">To avoid errors, please do not modify the exported JSON or manifest file.</span></span>

### <a name="import-entities-to-table-using-blobs"></a><span data-ttu-id="c728b-250">BLOB'ları kullanarak tablo varlıkları İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="c728b-250">Import entities to table using blobs</span></span>
<span data-ttu-id="c728b-251">Bir Blob kapsayıcısını içeren aşağıdaki varsayalım: Azure tablo ve eşlik eden bildirim dosyasını temsil eden bir JSON dosyası.</span><span class="sxs-lookup"><span data-stu-id="c728b-251">Assume a Blob container contains the following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="c728b-252">Bu blob kapsayıcısında bildirim dosyası kullanarak bir tabloya varlıkları içeri aktarmak için aşağıdaki komutu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c728b-252">You can run the following command to import entities into a table using the manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="c728b-253">Diğer AzCopy özellikleri</span><span class="sxs-lookup"><span data-stu-id="c728b-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="c728b-254">Hedefte mevcut olmayan veri Kopyala</span><span class="sxs-lookup"><span data-stu-id="c728b-254">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="c728b-255">`/XO` Ve `/XN` parametreleri, sırasıyla kopyalanmasını daha eski veya yeni kaynak kaynakları hariç tut izin verir.</span><span class="sxs-lookup"><span data-stu-id="c728b-255">The `/XO` and `/XN` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="c728b-256">Yalnızca hedef yoksa kaynak kaynakları kopyalamak isterseniz, AzCopy komut parametrelerinin her ikisini de belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c728b-256">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="c728b-257">Kaynak veya hedef tablo olduğunda bu desteklenmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-257">Note that this is not supported when either the source or destination is a table.</span></span>

### <a name="use-a-response-file-to-specify-command-line-parameters"></a><span data-ttu-id="c728b-258">Komut satırı parametrelerini belirtmek için bir yanıt dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="c728b-258">Use a response file to specify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="c728b-259">AzCopy komut satırı parametreleri bir yanıt dosyası içerebilir.</span><span class="sxs-lookup"><span data-stu-id="c728b-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="c728b-260">Komut satırında belirtilmiş gibi AzCopy dosyasının içeriğiyle doğrudan bir değiştirme gerçekleştirme dosyasındaki parametreleri işler.</span><span class="sxs-lookup"><span data-stu-id="c728b-260">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="c728b-261">Adlı bir yanıt dosyası varsayın `copyoperation.txt`, aşağıdaki satırları içeren.</span><span class="sxs-lookup"><span data-stu-id="c728b-261">Assume a response file named `copyoperation.txt`, that contains the following lines.</span></span> <span data-ttu-id="c728b-262">Tek bir satıra her AzCopy parametresi belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="c728b-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="c728b-263">veya satırları ayrı:</span><span class="sxs-lookup"><span data-stu-id="c728b-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="c728b-264">AzCopy bozulursa parametresi iki satır arasında bölmek için aşağıda gösterildiği gibi `/sourcekey` parametre:</span><span class="sxs-lookup"><span data-stu-id="c728b-264">AzCopy fails if you split the parameter across two lines, as shown here for the `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-to-specify-command-line-parameters"></a><span data-ttu-id="c728b-265">Komut satırı parametrelerini belirtmek için birden çok yanıt dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="c728b-265">Use multiple response files to specify command-line parameters</span></span>
<span data-ttu-id="c728b-266">Adlı bir yanıt dosyası varsayın `source.txt` kaynak kapsayıcı belirtir:</span><span class="sxs-lookup"><span data-stu-id="c728b-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="c728b-267">Ve adlı bir yanıt dosyası `dest.txt` bir hedef klasör dosya sistemindeki belirtir:</span><span class="sxs-lookup"><span data-stu-id="c728b-267">And a response file named `dest.txt` that specifies a destination folder in the file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="c728b-268">Ve adlı bir yanıt dosyası `options.txt` AzCopy seçeneklerini belirtir:</span><span class="sxs-lookup"><span data-stu-id="c728b-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="c728b-269">Bu yanıt dosyaları ile AzCopy çağırmak için her biri bir dizinde bulunan `C:\responsefiles`, bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="c728b-269">To call AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="c728b-270">Tüm Bireysel parametreleri komut satırında eklenirse gibi AzCopy bu komut işler:</span><span class="sxs-lookup"><span data-stu-id="c728b-270">AzCopy processes this command just as it would if you included all of the individual parameters on the command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="c728b-271">Paylaşılan erişim imzası (SAS) belirtin</span><span class="sxs-lookup"><span data-stu-id="c728b-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="c728b-272">Ayrıca, bir SAS kapsayıcısında URI belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c728b-272">You can also specify a SAS on the container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="c728b-273">Günlük dosyası klasörü</span><span class="sxs-lookup"><span data-stu-id="c728b-273">Journal file folder</span></span>
<span data-ttu-id="c728b-274">AzCopy için bir komut sorun her zaman varsayılan klasöründe bir günlük dosyası var olup var veya bu seçeneği belirtilen bir klasörde varolup denetler.</span><span class="sxs-lookup"><span data-stu-id="c728b-274">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="c728b-275">Günlük dosyası her iki yerde mevcut değilse, AzCopy işlemi yeni olarak değerlendirir ve yeni bir günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c728b-275">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="c728b-276">Günlük dosyası mevcut değilse, AzCopy girdiğiniz komut satırı günlük dosyası komut satırında eşleşip eşleşmediğini denetler.</span><span class="sxs-lookup"><span data-stu-id="c728b-276">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="c728b-277">İki komut satırları eşleşirse, AzCopy tamamlanmamış işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="c728b-277">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="c728b-278">Bunlar eşleşmiyorsa ya da yeni bir işlemi başlatmak için ya da geçerli işlemi iptal etmek için günlük dosyasının üzerine istenir.</span><span class="sxs-lookup"><span data-stu-id="c728b-278">If they do not match, you are prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="c728b-279">Varsayılan konumu için günlük dosyası kullanmak istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="c728b-279">If you want to use the default location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="c728b-280">Seçeneği unutursanız `/Z`, veya seçeneğini belirtin `/Z` klasör yolu, yukarıda gösterildiği gibi AzCopy günlük dosyası olan varsayılan konumda oluşturur `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="c728b-280">If you omit option `/Z`, or specify option `/Z` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="c728b-281">Günlük dosyası zaten varsa, AzCopy günlük dosyasına dayalı işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="c728b-281">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="c728b-282">Günlük dosyası için özel bir konum belirtmek istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="c728b-282">If you want to specify a custom location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="c728b-283">Zaten yoksa, bu örnek günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c728b-283">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="c728b-284">Mevcut değilse, AzCopy günlük dosyasına dayalı işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="c728b-284">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="c728b-285">AzCopy çalışmaya devam etmesini istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="c728b-285">If you want to resume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="c728b-286">Bu örnek tamamlamak için başarısız olan son işlem sürdürür.</span><span class="sxs-lookup"><span data-stu-id="c728b-286">This example resumes the last operation, which may have failed to complete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="c728b-287">Bir günlük dosyası oluşturur</span><span class="sxs-lookup"><span data-stu-id="c728b-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="c728b-288">Seçeneğini belirtirseniz `/V` ayrıntılı günlük dosya yoluna sağlamadan sonra AzCopy günlük dosyası olan varsayılan konumda oluşturur `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="c728b-288">If you specify option `/V` without providing a file path to the verbose log, then AzCopy creates the log file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="c728b-289">Aksi takdirde, özel bir konumda bir günlük dosyası oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c728b-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="c728b-290">Seçenek aşağıdaki göreli bir yol belirtirseniz, unutmayın `/V`, gibi `/V:test/azcopy1.log`, ayrıntılı günlük adlı bir alt klasör içinde geçerli çalışma dizininde oluşturulduktan sonra `test`.</span><span class="sxs-lookup"><span data-stu-id="c728b-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then the verbose log is created in the current working directory within a subfolder named `test`.</span></span>

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="c728b-291">Başlatmak için eşzamanlı işlem sayısını belirtin</span><span class="sxs-lookup"><span data-stu-id="c728b-291">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="c728b-292">Seçenek `/NC` eşzamanlı kopyalama işlemlerinin sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-292">Option `/NC` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="c728b-293">Varsayılan olarak, belirli bir sayıda veri aktarımı verimliliğini artırmak için eşzamanlı işlem AzCopy başlatır.</span><span class="sxs-lookup"><span data-stu-id="c728b-293">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="c728b-294">Tablo işlemleri için eşzamanlı işlem sayısını elinizde işlemci sayısına eşittir.</span><span class="sxs-lookup"><span data-stu-id="c728b-294">For Table operations, the number of concurrent operations is equal to the number of processors you have.</span></span> <span data-ttu-id="c728b-295">BLOB ve dosya işlemleri, eşzamanlı işlem sayısını için sahip olduğunuz işlemcilerin sayısı 8 kat eşit.</span><span class="sxs-lookup"><span data-stu-id="c728b-295">For Blob and File operations, the number of concurrent operations is equal 8 times the number of processors you have.</span></span> <span data-ttu-id="c728b-296">Düşük bant genişlikli ağ üzerinden AzCopy çalıştırıyorsanız, daha düşük bir sayı /NC tarafından kaynak rekabet nedeniyle başarısız olmaması için belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c728b-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC to avoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="c728b-297">AzCopy Azure Storage öykünücüsüne karşı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c728b-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="c728b-298">AzCopy karşı çalıştırabilirsiniz [Azure Storage öykünücüsü](storage-use-emulator.md) BLOB'lar için:</span><span class="sxs-lookup"><span data-stu-id="c728b-298">You can run AzCopy against the [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="c728b-299">ve tabloları:</span><span class="sxs-lookup"><span data-stu-id="c728b-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="c728b-300">AzCopy parametreleri</span><span class="sxs-lookup"><span data-stu-id="c728b-300">AzCopy Parameters</span></span>
<span data-ttu-id="c728b-301">AzCopy için Parametreler aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c728b-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="c728b-302">Yardım için komut satırından aşağıdaki komutlardan birini, AzCopy kullanarak da yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c728b-302">You can also type one of the following commands from the command line for help in using AzCopy:</span></span>

* <span data-ttu-id="c728b-303">AzCopy için ayrıntılı komut satırı Yardım için:`AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="c728b-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="c728b-304">Herhangi bir AzCopy parametre ile ilgili ayrıntılı yardım için:`AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="c728b-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="c728b-305">Komut satırı örnekleri için:`AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="c728b-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="c728b-306">/ Kaynak: "kaynak"</span><span class="sxs-lookup"><span data-stu-id="c728b-306">/Source:"source"</span></span>
<span data-ttu-id="c728b-307">Kopyalanacak kaynak verileri belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-307">Specifies the source data from which to copy.</span></span> <span data-ttu-id="c728b-308">Kaynak dosya sistemi dizini, bir blob kapsayıcı, blob sanal dizin, bir depolama dosya paylaşımı, bir depolama dosyası dizini veya bir Azure tablosu olabilir.</span><span class="sxs-lookup"><span data-stu-id="c728b-308">The source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="c728b-309">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="c728b-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="c728b-310">/ Taşınmaya: "hedef"</span><span class="sxs-lookup"><span data-stu-id="c728b-310">/Dest:"destination"</span></span>
<span data-ttu-id="c728b-311">Kopyalamak için hedef belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-311">Specifies the destination to copy to.</span></span> <span data-ttu-id="c728b-312">Hedef dosya sistemi dizini, bir blob kapsayıcı, blob sanal dizin, bir depolama dosya paylaşımı, bir depolama dosyası dizini veya bir Azure tablosu olabilir.</span><span class="sxs-lookup"><span data-stu-id="c728b-312">The destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="c728b-313">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="c728b-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="c728b-314">/ Desen: "dosya deseni"</span><span class="sxs-lookup"><span data-stu-id="c728b-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="c728b-315">Kopyalamak için hangi dosyaların gösteren bir dosya düzeni belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-315">Specifies a file pattern that indicates which files to copy.</span></span> <span data-ttu-id="c728b-316">/Pattern parametresi davranışını kaynak verilerin konumu ve yinelemeli modu seçeneği varlığını tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="c728b-316">The behavior of the /Pattern parameter is determined by the location of the source data, and the presence of the recursive mode option.</span></span> <span data-ttu-id="c728b-317">/S. seçeneği belirtilen Özyinelemeli modu</span><span class="sxs-lookup"><span data-stu-id="c728b-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="c728b-318">Belirtilen kaynak dosya sisteminde bir dizin ise, standart joker karakterler yürürlükte olan ve dizin içindeki dosyaları sağlanan dosya desen eşleştirme.</span><span class="sxs-lookup"><span data-stu-id="c728b-318">If the specified source is a directory in the file system, then standard wildcards are in effect, and the file pattern provided is matched against files within the directory.</span></span> <span data-ttu-id="c728b-319">/S Belirtilen seçeneği sonra AzCopy de karşı dizini altındaki tüm alt klasörlerdeki tüm dosyaları belirtilen desenle eşleşiyorsa.</span><span class="sxs-lookup"><span data-stu-id="c728b-319">If option /S is specified, then AzCopy also matches the specified pattern against all files in any subfolders beneath the directory.</span></span>

<span data-ttu-id="c728b-320">Belirtilen kaynak blob kapsayıcısı veya sanal dizin ise, joker karakter uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="c728b-320">If the specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="c728b-321">Seçenek sonra AzCopy /S belirtilirse, belirtilen dosya düzeni blob önek olarak yorumlar varsa.</span><span class="sxs-lookup"><span data-stu-id="c728b-321">If option /S is specified, then AzCopy interprets the specified file pattern as a blob prefix.</span></span> <span data-ttu-id="c728b-322">/S belirtilmezse, seçeneği sonra AzCopy tam blob adlarıyla dosya desen eşleşirse.</span><span class="sxs-lookup"><span data-stu-id="c728b-322">If option /S is not specified, then AzCopy matches the file pattern against exact blob names.</span></span>

<span data-ttu-id="c728b-323">Belirtilen kaynak bir Azure dosya paylaşımıdır sonra gerekir ya da tek bir dosya kopyalamak için tam dosya adını (örneğin abc.txt) belirtin veya seçeneğini belirtin /S paylaşımı yinelemeli olarak tüm dosyaları kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-323">If the specified source is an Azure file share, then you must either specify the exact file name, (e.g. abc.txt) to copy a single file, or specify option /S to copy all files in the share recursively.</span></span> <span data-ttu-id="c728b-324">Her iki bir dosya düzeni ve seçeneği /S birlikte sonuçlar hata belirleyin çalışılıyor.</span><span class="sxs-lookup"><span data-stu-id="c728b-324">Attempting to specify both a file pattern and option /S together results in an error.</span></span>

<span data-ttu-id="c728b-325">AzCopy / Source bir blob kapsayıcısı veya blob sanal dizin ve büyük küçük harf duyarsız tüm diğer durumlarda eşleşen kullanması durumunda büyük küçük harfe duyarlı eşleşen kullanır.</span><span class="sxs-lookup"><span data-stu-id="c728b-325">AzCopy uses case-sensitive matching when the /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all the other cases.</span></span>

<span data-ttu-id="c728b-326">Hiçbir dosya deseni belirtildiğinde kullanılan varsayılan dosya Düzen *.*</span><span class="sxs-lookup"><span data-stu-id="c728b-326">The default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="c728b-327">bir dosya sistemi konumu veya bir Azure depolama konumu için boş bir önek.</span><span class="sxs-lookup"><span data-stu-id="c728b-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="c728b-328">Birden çok dosya desenlerinin belirtilmesi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="c728b-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="c728b-329">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="c728b-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="c728b-330">/ DestKey: "depolama anahtar"</span><span class="sxs-lookup"><span data-stu-id="c728b-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="c728b-331">Hedef kaynak için depolama hesabı anahtar belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-331">Specifies the storage account key for the destination resource.</span></span>

<span data-ttu-id="c728b-332">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="c728b-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="c728b-333">/ DestSAS: "sas belirteci"</span><span class="sxs-lookup"><span data-stu-id="c728b-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="c728b-334">(Eğer varsa) hedef için okuma ve yazma izinlerine sahip paylaşılan erişim imzası (SAS) belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for the destination (if applicable).</span></span> <span data-ttu-id="c728b-335">İçerdiğinden özel komut satırı karakter çift tırnak işareti ile SAS koyun.</span><span class="sxs-lookup"><span data-stu-id="c728b-335">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="c728b-336">Hedef kaynak, bir blob kapsayıcısını, dosya paylaşımı veya tablo ise, bu seçenek SAS belirteci tarafından izlenen ya da belirtebilirsiniz veya hedef blob kapsayıcısını, dosya paylaşımı veya tablonun URI, bu seçeneği olmadan bir parçası olarak SAS belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c728b-336">If the destination resource is a blob container, file share or table, you can either specify this option followed by the SAS token, or you can specify the SAS as part of the destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="c728b-337">Kaynak ve hedef hem de blob'ları varsa, hedef blob aynı kaynak blob depolama hesabı içinde bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c728b-337">If the source and destination are both blobs, then the destination blob must reside within the same storage account as the source blob.</span></span>

<span data-ttu-id="c728b-338">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="c728b-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="c728b-339">/ SourceKey: "depolama anahtar"</span><span class="sxs-lookup"><span data-stu-id="c728b-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="c728b-340">Kaynak kaynak için depolama hesabı anahtar belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-340">Specifies the storage account key for the source resource.</span></span>

<span data-ttu-id="c728b-341">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="c728b-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="c728b-342">/ SourceSAS: "sas belirteci"</span><span class="sxs-lookup"><span data-stu-id="c728b-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="c728b-343">Kaynak için okuma ve liste izinlerine sahip paylaşılan erişim imzası (varsa) belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-343">Specifies a Shared Access Signature with READ and LIST permissions for the source (if applicable).</span></span> <span data-ttu-id="c728b-344">İçerdiğinden özel komut satırı karakter çift tırnak işareti ile SAS koyun.</span><span class="sxs-lookup"><span data-stu-id="c728b-344">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="c728b-345">Bir blob kapsayıcısını kaynak kaynak ise ve bir anahtar ya da SAS sağlanan blob kapsayıcısında anonim erişim okuyun.</span><span class="sxs-lookup"><span data-stu-id="c728b-345">If the source resource is a blob container, and neither a key nor a SAS is provided, then the blob container is read via anonymous access.</span></span>

<span data-ttu-id="c728b-346">Kaynak dosya paylaşımı veya tablo ise, bir anahtar veya bir SAS sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c728b-346">If the source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="c728b-347">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="c728b-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="c728b-348">/ S</span><span class="sxs-lookup"><span data-stu-id="c728b-348">/S</span></span>
<span data-ttu-id="c728b-349">Kopyalama işlemleri için özyinelemeli modunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="c728b-350">Özyinelemeli modunda AzCopy tüm BLOB'ları veya alt klasörler de dahil olmak üzere belirtilen dosya desenle eşleşen dosyaları kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c728b-350">In recursive mode, AzCopy copies all blobs or files that match the specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="c728b-351">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="c728b-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="c728b-352">/ BlobType: "blok" | "Sayfa" | "Ekle"</span><span class="sxs-lookup"><span data-stu-id="c728b-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="c728b-353">Hedef blob blok blobu, bir sayfa blob'u ya da bir ek blobu olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-353">Specifies whether the destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="c728b-354">Bu seçenek yalnızca bir blob karşıya yüklenirken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c728b-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="c728b-355">Aksi takdirde bir hata oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c728b-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="c728b-356">Hedef blob ise ve bu seçenek, varsayılan olarak, belirtilmemiş bir blok blobu AzCopy oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c728b-356">If the destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="c728b-357">**Uygulanabilir:** BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="c728b-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="c728b-358">/ CheckMD5</span><span class="sxs-lookup"><span data-stu-id="c728b-358">/CheckMD5</span></span>
<span data-ttu-id="c728b-359">Karşıdan yüklenen veriler için MD5 karma değeri hesaplar ve MD5 karma değeri blob içinde depolanan veya hesaplanan karma dosyanın içeriği MD5 özelliği eşleşen doğrular.</span><span class="sxs-lookup"><span data-stu-id="c728b-359">Calculates an MD5 hash for downloaded data and verifies that the MD5 hash stored in the blob or file's Content-MD5 property matches the calculated hash.</span></span> <span data-ttu-id="c728b-360">MD5 denetimi verilerini yüklerken gerçekleştirmek için bu seçeneği belirtmeniz gerekir böylece MD5 onay varsayılan olarak kapalıdır.</span><span class="sxs-lookup"><span data-stu-id="c728b-360">The MD5 check is turned off by default, so you must specify this option to perform the MD5 check when downloading data.</span></span>

<span data-ttu-id="c728b-361">Azure Storage blob veya dosya için depolanan MD5 karma değeri güncel olduğunu garanti etmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-361">Note that Azure Storage doesn't guarantee that the MD5 hash stored for the blob or file is up-to-date.</span></span> <span data-ttu-id="c728b-362">Blob veya dosya değiştirildiğinde MD5 güncelleştirmesi istemcinin sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="c728b-362">It is client's responsibility to update the MD5 whenever the blob or file is modified.</span></span>

<span data-ttu-id="c728b-363">AzCopy hizmete karşıya sonra bir Azure blob veya dosya için Content-MD5 özelliği her zaman ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c728b-363">AzCopy always sets the Content-MD5 property for an Azure blob or file after uploading it to the service.</span></span>  

<span data-ttu-id="c728b-364">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="c728b-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="c728b-365">/ Anlık görüntü</span><span class="sxs-lookup"><span data-stu-id="c728b-365">/Snapshot</span></span>
<span data-ttu-id="c728b-366">Anlık görüntüler aktarmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="c728b-366">Indicates whether to transfer snapshots.</span></span> <span data-ttu-id="c728b-367">Bu seçenek, yalnızca kaynak blob olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c728b-367">This option is only valid when the source is a blob.</span></span>

<span data-ttu-id="c728b-368">Aktarılan blob anlık görüntüler şu biçimde adlandırılır: blob adı (anlık görüntü-time) .extension</span><span class="sxs-lookup"><span data-stu-id="c728b-368">The transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="c728b-369">Varsayılan olarak, anlık görüntüleri kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="c728b-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="c728b-370">**Uygulanabilir:** BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="c728b-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="c728b-371">/ V: [verbose-günlük dosyası]</span><span class="sxs-lookup"><span data-stu-id="c728b-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="c728b-372">Bir günlük dosyasına çıkarır ayrıntılı durum iletileri.</span><span class="sxs-lookup"><span data-stu-id="c728b-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="c728b-373">Varsayılan olarak, içinde AzCopyVerbose.log adlı ayrıntılı günlük dosyası `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="c728b-373">By default, the verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="c728b-374">Varolan bir dosya konumu için bu seçeneği belirtirseniz, ayrıntılı günlük bu dosyaya eklenir.</span><span class="sxs-lookup"><span data-stu-id="c728b-374">If you specify an existing file location for this option, the verbose log is appended to that file.</span></span>  

<span data-ttu-id="c728b-375">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="c728b-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="c728b-376">/ Z: [günlük dosyası klasörü]</span><span class="sxs-lookup"><span data-stu-id="c728b-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="c728b-377">Bir işlemi sürdürme bir günlük dosyası klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="c728b-378">AzCopy her zaman bir işlem yarıda kesildi durumunda sürdürme destekler.</span><span class="sxs-lookup"><span data-stu-id="c728b-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="c728b-379">Bu seçenek belirtilmezse ya da bir klasör yolu belirtilen AzCopy günlük dosyası % LocalAppData%\Microsoft\Azure\AzCopy olan varsayılan konumda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c728b-379">If this option is not specified, or it is specified without a folder path, then AzCopy creates the journal file in the default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="c728b-380">AzCopy için bir komut sorun her zaman varsayılan klasöründe bir günlük dosyası var olup var veya bu seçeneği belirtilen bir klasörde varolup denetler.</span><span class="sxs-lookup"><span data-stu-id="c728b-380">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="c728b-381">Günlük dosyası her iki yerde mevcut değilse, AzCopy işlemi yeni olarak değerlendirir ve yeni bir günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c728b-381">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="c728b-382">Günlük dosyası mevcut değilse, AzCopy girdiğiniz komut satırı günlük dosyası komut satırında eşleşip eşleşmediğini denetler.</span><span class="sxs-lookup"><span data-stu-id="c728b-382">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="c728b-383">İki komut satırları eşleşirse, AzCopy tamamlanmamış işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="c728b-383">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="c728b-384">Bunlar eşleşmiyorsa ya da yeni bir işlemi başlatmak için ya da geçerli işlemi iptal etmek için günlük dosyasının üzerine istenir.</span><span class="sxs-lookup"><span data-stu-id="c728b-384">If they do not match, you are prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="c728b-385">Günlük dosyası işlemi başarıyla tamamlandıktan sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="c728b-385">The journal file is deleted upon successful completion of the operation.</span></span>

<span data-ttu-id="c728b-386">AzCopy önceki bir sürümü tarafından oluşturulmuş bir günlük dosyasından bir işlemi sürdürme desteklenmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="c728b-387">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="c728b-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="c728b-388">/@:"Parameter-File"</span><span class="sxs-lookup"><span data-stu-id="c728b-388">/@:"parameter-file"</span></span>
<span data-ttu-id="c728b-389">Parametreleri içeren dosyayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="c728b-390">Komut satırında bunlar yalnızca belirtilmiş gibi AzCopy dosyasındaki parametreleri işler.</span><span class="sxs-lookup"><span data-stu-id="c728b-390">AzCopy processes the parameters in the file just as if they had been specified on the command line.</span></span>

<span data-ttu-id="c728b-391">Bir yanıt dosyası, tek bir satıra birden çok parametreleri belirtin veya kendi satırında her parametre belirtin.</span><span class="sxs-lookup"><span data-stu-id="c728b-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="c728b-392">Tek bir parametre birden çok satıra yayılamaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="c728b-393">Yanıt dosyaları # sembolü ile başlayan açıklamaları satırları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="c728b-393">Response files can include comments lines that begin with the # symbol.</span></span>

<span data-ttu-id="c728b-394">Birden çok yanıt dosyaları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c728b-394">You can specify multiple response files.</span></span> <span data-ttu-id="c728b-395">Ancak, AzCopy iç içe yanıt dosyaları desteklemiyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="c728b-396">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="c728b-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="c728b-397">/Y</span><span class="sxs-lookup"><span data-stu-id="c728b-397">/Y</span></span>
<span data-ttu-id="c728b-398">Tüm AzCopy onay komut istemlerini bastırır.</span><span class="sxs-lookup"><span data-stu-id="c728b-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="c728b-399">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="c728b-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="c728b-400">/L</span><span class="sxs-lookup"><span data-stu-id="c728b-400">/L</span></span>
<span data-ttu-id="c728b-401">Yalnızca bir listeleme işlemi belirtir; hiçbir veri kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="c728b-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="c728b-402">AzCopy yorumlar birini kullanarak bu seçeneği olarak çalıştırmak için bir benzetimi bu olmadan komut satırı seçeneği /L ve kaç tane nesneleri kopyalanır sayılar, hangi nesnelerin denetlemek için aynı anda /V Ayrıntılı günlüğe kopyalanır seçeneği belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c728b-402">AzCopy interprets the using of this option as a simulation for running the command line without this option /L and counts how many objects are copied, you can specify option /V at the same time to check which objects are copied in the verbose log.</span></span>

<span data-ttu-id="c728b-403">Bu seçenek davranışını Ayrıca kaynak verilerin konumu ve yinelemeli modu seçeneği/s ve dosya düzeni seçeneği /Pattern varlığını tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="c728b-403">The behavior of this option is also determined by the location of the source data and the presence of the recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="c728b-404">AzCopy, bu seçenek kullanıldığında bu kaynak konumunun listesi ve okuma izni gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c728b-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="c728b-405">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="c728b-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="c728b-406">/ MT</span><span class="sxs-lookup"><span data-stu-id="c728b-406">/MT</span></span>
<span data-ttu-id="c728b-407">Aynı kaynak blob veya dosya indirilen dosyanın son değişiklik süreyi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c728b-407">Sets the downloaded file's last-modified time to be the same as the source blob or file's.</span></span>

<span data-ttu-id="c728b-408">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="c728b-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="c728b-409">/XN</span><span class="sxs-lookup"><span data-stu-id="c728b-409">/XN</span></span>
<span data-ttu-id="c728b-410">Daha yeni bir kaynak kaynak dışlar.</span><span class="sxs-lookup"><span data-stu-id="c728b-410">Excludes a newer source resource.</span></span> <span data-ttu-id="c728b-411">Son değişiklik zamanını kaynağının aynı ise kaynak kopyalanmaz veya hedef daha yeni.</span><span class="sxs-lookup"><span data-stu-id="c728b-411">The resource is not copied if the last modified time of the source is the same or newer than destination.</span></span>

<span data-ttu-id="c728b-412">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="c728b-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="c728b-413">/XO</span><span class="sxs-lookup"><span data-stu-id="c728b-413">/XO</span></span>
<span data-ttu-id="c728b-414">Eski bir kaynak kaynak dışlar.</span><span class="sxs-lookup"><span data-stu-id="c728b-414">Excludes an older source resource.</span></span> <span data-ttu-id="c728b-415">Son değişiklik zamanını kaynağının aynı ise kaynak kopyalanmaz veya hedef daha eski.</span><span class="sxs-lookup"><span data-stu-id="c728b-415">The resource is not copied if the last modified time of the source is the same or older than destination.</span></span>

<span data-ttu-id="c728b-416">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="c728b-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="c728b-417">/A</span><span class="sxs-lookup"><span data-stu-id="c728b-417">/A</span></span>
<span data-ttu-id="c728b-418">Yalnızca arşiv özniteliği kümesine sahip dosyaları karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="c728b-418">Uploads only files that have the Archive attribute set.</span></span>

<span data-ttu-id="c728b-419">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="c728b-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="c728b-420">/ IA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="c728b-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="c728b-421">Belirtilen öznitelikler kümesi olan dosyaları karşıya yükler.</span><span class="sxs-lookup"><span data-stu-id="c728b-421">Uploads only files that have any of the specified attributes set.</span></span>

<span data-ttu-id="c728b-422">Mevcut öznitelikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c728b-422">Available attributes include:</span></span>

* <span data-ttu-id="c728b-423">R Salt okunur dosyalar =</span><span class="sxs-lookup"><span data-stu-id="c728b-423">R = Read-only files</span></span>
* <span data-ttu-id="c728b-424">Arşivlenmeye hazır dosyalar bir =</span><span class="sxs-lookup"><span data-stu-id="c728b-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="c728b-425">S sistem dosyaları =</span><span class="sxs-lookup"><span data-stu-id="c728b-425">S = System files</span></span>
* <span data-ttu-id="c728b-426">H Gizli dosyalar =</span><span class="sxs-lookup"><span data-stu-id="c728b-426">H = Hidden files</span></span>
* <span data-ttu-id="c728b-427">C Sıkıştırılmış dosyaları =</span><span class="sxs-lookup"><span data-stu-id="c728b-427">C = Compressed files</span></span>
* <span data-ttu-id="c728b-428">N Normal dosyalar =</span><span class="sxs-lookup"><span data-stu-id="c728b-428">N = Normal files</span></span>
* <span data-ttu-id="c728b-429">E Şifrelenmiş dosyaları =</span><span class="sxs-lookup"><span data-stu-id="c728b-429">E = Encrypted files</span></span>
* <span data-ttu-id="c728b-430">T = geçici dosyalar</span><span class="sxs-lookup"><span data-stu-id="c728b-430">T = Temporary files</span></span>
* <span data-ttu-id="c728b-431">O çevrimdışı dosyalar =</span><span class="sxs-lookup"><span data-stu-id="c728b-431">O = Offline files</span></span>
* <span data-ttu-id="c728b-432">I dosyaları olmayan dizini =</span><span class="sxs-lookup"><span data-stu-id="c728b-432">I = Non-indexed files</span></span>

<span data-ttu-id="c728b-433">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="c728b-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="c728b-434">/ XA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="c728b-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="c728b-435">Belirtilen öznitelikler kümesi olan dosyaları dışlar.</span><span class="sxs-lookup"><span data-stu-id="c728b-435">Excludes files that have any of the specified attributes set.</span></span>

<span data-ttu-id="c728b-436">Mevcut öznitelikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c728b-436">Available attributes include:</span></span>

* <span data-ttu-id="c728b-437">R Salt okunur dosyalar =</span><span class="sxs-lookup"><span data-stu-id="c728b-437">R = Read-only files</span></span>
* <span data-ttu-id="c728b-438">Arşivlenmeye hazır dosyalar bir =</span><span class="sxs-lookup"><span data-stu-id="c728b-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="c728b-439">S sistem dosyaları =</span><span class="sxs-lookup"><span data-stu-id="c728b-439">S = System files</span></span>
* <span data-ttu-id="c728b-440">H Gizli dosyalar =</span><span class="sxs-lookup"><span data-stu-id="c728b-440">H = Hidden files</span></span>
* <span data-ttu-id="c728b-441">C Sıkıştırılmış dosyaları =</span><span class="sxs-lookup"><span data-stu-id="c728b-441">C = Compressed files</span></span>
* <span data-ttu-id="c728b-442">N Normal dosyalar =</span><span class="sxs-lookup"><span data-stu-id="c728b-442">N = Normal files</span></span>
* <span data-ttu-id="c728b-443">E Şifrelenmiş dosyaları =</span><span class="sxs-lookup"><span data-stu-id="c728b-443">E = Encrypted files</span></span>
* <span data-ttu-id="c728b-444">T = geçici dosyalar</span><span class="sxs-lookup"><span data-stu-id="c728b-444">T = Temporary files</span></span>
* <span data-ttu-id="c728b-445">O çevrimdışı dosyalar =</span><span class="sxs-lookup"><span data-stu-id="c728b-445">O = Offline files</span></span>
* <span data-ttu-id="c728b-446">I dosyaları olmayan dizini =</span><span class="sxs-lookup"><span data-stu-id="c728b-446">I = Non-indexed files</span></span>

<span data-ttu-id="c728b-447">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="c728b-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="c728b-448">/ Sınırlayıcı: "sınırlayıcı"</span><span class="sxs-lookup"><span data-stu-id="c728b-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="c728b-449">Bir blob adındaki sanal dizinleri sınırlandırmak için kullanılan sınırlayıcı karakter gösterir.</span><span class="sxs-lookup"><span data-stu-id="c728b-449">Indicates the delimiter character used to delimit virtual directories in a blob name.</span></span>

<span data-ttu-id="c728b-450">Varsayılan olarak, AzCopy kullanır / sınırlayıcı karakter olarak.</span><span class="sxs-lookup"><span data-stu-id="c728b-450">By default, AzCopy uses / as the delimiter character.</span></span> <span data-ttu-id="c728b-451">Ancak, ortak bir karakterle kullanarak AzCopy destekler (gibi @, # ya da %) ayırıcı olarak.</span><span class="sxs-lookup"><span data-stu-id="c728b-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="c728b-452">Komut satırında şu özel karakterleri birini içeren ihtiyacınız varsa, bir dosya adı ile çift tırnak içine alın.</span><span class="sxs-lookup"><span data-stu-id="c728b-452">If you need to include one of these special characters on the command line, enclose the file name with double quotes.</span></span>

<span data-ttu-id="c728b-453">Bu seçenek, yalnızca BLOB indirmek için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c728b-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="c728b-454">**Uygulanabilir:** BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="c728b-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="c728b-455">/ NC: "numarası-in-eşzamanlı-işlemler"</span><span class="sxs-lookup"><span data-stu-id="c728b-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="c728b-456">Eşzamanlı işlem sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-456">Specifies the number of concurrent operations.</span></span>

<span data-ttu-id="c728b-457">AzCopy varsayılan olarak, belirli bir sayıda veri aktarımı verimliliğini artırmak için eşzamanlı işlem başlatır.</span><span class="sxs-lookup"><span data-stu-id="c728b-457">AzCopy by default starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="c728b-458">Çok sayıda eş zamanlı görevleri bir düşük bant genişlikli ortamında ve ağ bağlantısını doldurmaya tam olarak tamamlanmasını işlemlerini önlemek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm the network connection and prevent the operations from fully completing.</span></span> <span data-ttu-id="c728b-459">Eşzamanlı operasyonlar gerçek kullanılabilir ağ bant genişliğine bağlı kısıtlama.</span><span class="sxs-lookup"><span data-stu-id="c728b-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="c728b-460">Eşzamanlı operasyonlar için üst sınırı 512'dir.</span><span class="sxs-lookup"><span data-stu-id="c728b-460">The upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="c728b-461">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="c728b-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="c728b-462">/ Kaynak türü: "Blob" | "Tablo"</span><span class="sxs-lookup"><span data-stu-id="c728b-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="c728b-463">Belirleyen `source` kaynaktır bir blob depolama öykünücüsünde çalıştıran yerel geliştirme ortamında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c728b-463">Specifies that the `source` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="c728b-464">**Uygulanabilir:** BLOB'ların, tabloları</span><span class="sxs-lookup"><span data-stu-id="c728b-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="c728b-465">/ DestType: "Blob" | "Tablo"</span><span class="sxs-lookup"><span data-stu-id="c728b-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="c728b-466">Belirleyen `destination` kaynaktır bir blob depolama öykünücüsünde çalıştıran yerel geliştirme ortamında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c728b-466">Specifies that the `destination` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="c728b-467">**Uygulanabilir:** BLOB'ların, tabloları</span><span class="sxs-lookup"><span data-stu-id="c728b-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="c728b-468">/ PKRS: "anahtar&#1;key2 anahtar&#3;..."</span><span class="sxs-lookup"><span data-stu-id="c728b-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="c728b-469">Tablo verileri dışarı aktarma işlemi hızını artırır paralel dışarı aktarma etkinleştirmek için bölüm anahtarı aralığının böler.</span><span class="sxs-lookup"><span data-stu-id="c728b-469">Splits the partition key range to enable exporting table data in parallel, which increases the speed of the export operation.</span></span>

<span data-ttu-id="c728b-470">Bu seçenek belirtilmezse, AzCopy tablo varlıkları vermek için tek bir iş parçacığı kullanır.</span><span class="sxs-lookup"><span data-stu-id="c728b-470">If this option is not specified, then AzCopy uses a single thread to export table entities.</span></span> <span data-ttu-id="c728b-471">Örneğin, kullanıcı /PKRS belirtir: "aa #bb" sonra AzCopy üç eşzamanlı işlem başlatır.</span><span class="sxs-lookup"><span data-stu-id="c728b-471">For example, if the user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="c728b-472">Her işlem, aşağıda gösterildiği gibi üç bölüm anahtarı aralıkları, birini verir:</span><span class="sxs-lookup"><span data-stu-id="c728b-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="c728b-473">[ilk bölüm anahtarı, aa)</span><span class="sxs-lookup"><span data-stu-id="c728b-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="c728b-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="c728b-474">[aa, bb)</span></span>

  <span data-ttu-id="c728b-475">[bb, son bölüm anahtarı]</span><span class="sxs-lookup"><span data-stu-id="c728b-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="c728b-476">**Uygulanabilir:** tabloları</span><span class="sxs-lookup"><span data-stu-id="c728b-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="c728b-477">/ SplitSize: "dosya boyutu"</span><span class="sxs-lookup"><span data-stu-id="c728b-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="c728b-478">32 MB, izin verilen minimum değer boyutu bölme dışarı aktarılan dosyayı olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-478">Specifies the exported file split size in MB, the minimal value allowed is 32.</span></span>

<span data-ttu-id="c728b-479">Bu seçenek belirtilmezse, AzCopy tablo verileri tek bir dosyaya dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="c728b-479">If this option is not specified, AzCopy exports table data to a single file.</span></span>

<span data-ttu-id="c728b-480">Bu seçenek belirtilmezse bile tablo verileri için blob aktarılır ve blob boyutu 200 GB sınırını dışarı aktarılan dosya boyutu, AzCopy dışarı aktarılan dosyayı ayırır.</span><span class="sxs-lookup"><span data-stu-id="c728b-480">If the table data is exported to a blob, and the exported file size reaches the 200 GB limit for blob size, then AzCopy splits the exported file, even if this option is not specified.</span></span>

<span data-ttu-id="c728b-481">**Uygulanabilir:** tabloları</span><span class="sxs-lookup"><span data-stu-id="c728b-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="c728b-482">/ EntityOperation: "InsertOrSkip" | "InsertOrMerge" | "Yerleştir veya Değiştir"</span><span class="sxs-lookup"><span data-stu-id="c728b-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="c728b-483">Tablo verileri alma davranışını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-483">Specifies the table data import behavior.</span></span>

* <span data-ttu-id="c728b-484">InsertOrSkip - var olan bir varlığı atlar veya tabloda mevcut değilse yeni bir varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="c728b-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="c728b-485">InsertOrMerge - var olan bir varlığı birleştirir veya tabloda mevcut değilse yeni bir varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="c728b-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="c728b-486">Yerleştir veya Değiştir - var olan bir varlığı değiştirir veya tabloda mevcut değilse yeni bir varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="c728b-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="c728b-487">**Uygulanabilir:** tabloları</span><span class="sxs-lookup"><span data-stu-id="c728b-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="c728b-488">/ MANIFEST: "bildirim dosyası"</span><span class="sxs-lookup"><span data-stu-id="c728b-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="c728b-489">Tabloyu dışarı ve içeri aktarma işlemi için bildirim dosyasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-489">Specifies the manifest file for the table export and import operation.</span></span>

<span data-ttu-id="c728b-490">Dışa aktarma işlemi sırasında bu seçenek isteğe bağlıdır, bu seçenek belirtilmezse, AzCopy önceden tanımlanmış ada sahip bir bildirim dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c728b-490">This option is optional during the export operation, AzCopy generates a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="c728b-491">Bu seçenek, veri dosyalarını bulmak için içeri aktarma işlemi sırasında gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c728b-491">This option is required during the import operation for locating the data files.</span></span>

<span data-ttu-id="c728b-492">**Uygulanabilir:** tabloları</span><span class="sxs-lookup"><span data-stu-id="c728b-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="c728b-493">/ SyncCopy</span><span class="sxs-lookup"><span data-stu-id="c728b-493">/SyncCopy</span></span>
<span data-ttu-id="c728b-494">BLOB veya iki Azure Storage uç noktalar arasında dosyaları zaman uyumlu olarak kopyalamak gösterir.</span><span class="sxs-lookup"><span data-stu-id="c728b-494">Indicates whether to synchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="c728b-495">AzCopy varsayılan olarak, sunucu tarafı zaman uyumsuz kopyayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="c728b-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="c728b-496">BLOB veya dosyaları için yerel bellek indirir ve bunları Azure depolama alanına yükler bir zaman uyumlu bir kopyasını gerçekleştirmek için bu seçeneği belirtin.</span><span class="sxs-lookup"><span data-stu-id="c728b-496">Specify this option to perform a synchronous copy, which downloads blobs or files to local memory and then uploads them to Azure Storage.</span></span>

<span data-ttu-id="c728b-497">Blob storage, dosya depolama içinde veya Blob depolamadan dosya depolama (veya tersi) içinde dosya kopyalarken, bu seçeneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c728b-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage to File storage or vice versa.</span></span>

<span data-ttu-id="c728b-498">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="c728b-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="c728b-499">/ SetContentType: "content-type"</span><span class="sxs-lookup"><span data-stu-id="c728b-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="c728b-500">Hedef BLOB'ları veya dosyaları için MIME içerik türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-500">Specifies the MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="c728b-501">AzCopy içerik türü bir blob veya dosya için varsayılan olarak application/octet-stream, için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c728b-501">AzCopy sets the content type for a blob or file to application/octet-stream by default.</span></span> <span data-ttu-id="c728b-502">Bu seçenek için bir değer açıkça belirterek tüm BLOB'ları veya dosyaları için içerik türü ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c728b-502">You can set the content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="c728b-503">Bu seçenek olmadan bir değer belirtirseniz, AzCopy her bir blob veya dosyanın içerik türü dosya uzantısını göre ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c728b-503">If you specify this option without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

<span data-ttu-id="c728b-504">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="c728b-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="c728b-505">/ PayloadFormat: "JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="c728b-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="c728b-506">Tablo dışarı aktarılan veri dosyasının biçimi belirtir.</span><span class="sxs-lookup"><span data-stu-id="c728b-506">Specifies the format of the table exported data file.</span></span>

<span data-ttu-id="c728b-507">Bu seçenek belirtilmezse, varsayılan olarak AzCopy tablo veri dosyası JSON biçiminde dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="c728b-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="c728b-508">**Uygulanabilir:** tabloları</span><span class="sxs-lookup"><span data-stu-id="c728b-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="c728b-509">Bilinen sorunlar ve en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="c728b-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="c728b-510">Veri kopyalama sırasında sınırı eşzamanlı yazma</span><span class="sxs-lookup"><span data-stu-id="c728b-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="c728b-511">BLOB veya AzCopy dosyalarıyla kopyaladığınızda, bunu kopyalamaya çalışırken, başka bir uygulama verileri değiştirme göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="c728b-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="c728b-512">Mümkünse, Kopyalamakta olduğunuz veri kopyalama işlemi sırasında değiştirilmeyen emin olun.</span><span class="sxs-lookup"><span data-stu-id="c728b-512">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="c728b-513">Örneğin, bir Azure sanal makine ile ilişkili bir VHD'nin kopyalarken, başka bir uygulama şu anda VHD'ye yazıyorsanız emin olun.</span><span class="sxs-lookup"><span data-stu-id="c728b-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="c728b-514">Bunu yapmak için iyi bir Kopyalanacak kaynak kiralama tarafından yoldur.</span><span class="sxs-lookup"><span data-stu-id="c728b-514">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="c728b-515">Alternatif olarak, bir anlık görüntü VHD'yi ilk oluşturun ve sonra anlık görüntü kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c728b-515">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="c728b-516">Bunlar kopyalanan sırada BLOB veya dosyalar için yazma diğer uygulamaların önleyemez, ardından işi tamamlanana zamanına göre kopyalanan kaynakların artık kaynak kaynaklarla tam eşlik gerekebileceğini aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="c728b-516">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="c728b-517">Bir Azcopy'i örnek bir makinede çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c728b-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="c728b-518">AzCopy veri aktarımını hızlandırmak için makine kaynak kullanımını en üst düzeye çıkarmak için tasarlanmış, yalnızca bir Azcopy'i örnek bir makinede çalıştırın ve seçeneğini belirtin öneririz `/NC` fazla eşzamanlı işlem gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="c728b-518">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="c728b-519">Daha fazla ayrıntı için yazın `AzCopy /?:NC` komut satırında.</span><span class="sxs-lookup"><span data-stu-id="c728b-519">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="c728b-520">FIPS uyumlu MD5 algoritmaları etkinleştirmek için AzCopy olduğunda, "kullanım FIPS uyumlu algoritmaları şifreleme, karma ve imzalama için".</span><span class="sxs-lookup"><span data-stu-id="c728b-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="c728b-521">AzCopy varsayılan olarak, MD5 nesneleri kopyalarken hesaplamak için .NET MD5 uygulama kullanır ancak AzCopy FIPS uyumlu MD5 ayarı etkinleştirmek için gereken bazı güvenlik gereksinimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="c728b-521">AzCopy by default uses .NET MD5 implementation to calculate the MD5 when copying objects, but there are some security requirements that need AzCopy to enable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="c728b-522">Bir app.config dosyası oluşturabilirsiniz `AzCopy.exe.config` özelliğiyle `AzureStorageUseV1MD5` ve AzCopy.exe ile kenara yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="c728b-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="c728b-523">Özellik "AzureStorageUseV1MD5" • True - varsayılan değer, AzCopy .NET MD5 uygulama kullanır.</span><span class="sxs-lookup"><span data-stu-id="c728b-523">For property "AzureStorageUseV1MD5" • True - The default value, AzCopy uses .NET MD5 implementation.</span></span>
<span data-ttu-id="c728b-524">• Yanlış – AzCopy FIPS uyumlu MD5 algoritması kullanır.</span><span class="sxs-lookup"><span data-stu-id="c728b-524">• False – AzCopy uses FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="c728b-525">Not FIPS uyumlu algoritmaları Windows makinenizde varsayılan olarak devre dışıdır, secpol.msc, Çalıştır penceresine yazın ve denetleme bu güvenlik ayarı anahtara -> yerel ilke güvenlik -> Seçenekler -> Sistem şifrelemesi: şifreleme, karma ve imzalama için kullan FIPS uyumlu algoritmaları.</span><span class="sxs-lookup"><span data-stu-id="c728b-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c728b-526">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c728b-526">Next steps</span></span>
<span data-ttu-id="c728b-527">Azure Storage ve AzCopy hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="c728b-527">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="c728b-528">Azure Storage belgeleri:</span><span class="sxs-lookup"><span data-stu-id="c728b-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="c728b-529">Azure Storage'a giriş</span><span class="sxs-lookup"><span data-stu-id="c728b-529">Introduction to Azure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="c728b-530">BLOB depolama alanından .NET kullanma</span><span class="sxs-lookup"><span data-stu-id="c728b-530">How to use Blob storage from .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="c728b-531">.NET dan File storage kullanma</span><span class="sxs-lookup"><span data-stu-id="c728b-531">How to use File storage from .NET</span></span>](../storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="c728b-532">Table storage .NET'kullanma</span><span class="sxs-lookup"><span data-stu-id="c728b-532">How to use Table storage from .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="c728b-533">Oluşturma, yönetme veya bir depolama hesabını silme</span><span class="sxs-lookup"><span data-stu-id="c728b-533">How to create, manage, or delete a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="c728b-534">Linux'ta AzCopy ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="c728b-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="c728b-535">Azure depolama blog gönderileri:</span><span class="sxs-lookup"><span data-stu-id="c728b-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="c728b-536">Azure Storage veri hareketi kitaplığı Önizleme Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="c728b-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="c728b-537">AzCopy: zaman uyumlu kopyası ve özelleştirilmiş içerik türü tanışın</span><span class="sxs-lookup"><span data-stu-id="c728b-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="c728b-538">AzCopy: Genel kullanılabilirlik, AzCopy 3.0 artı AzCopy 4.0 Önizleme sürümü tablo ve dosya desteği ile tanışın</span><span class="sxs-lookup"><span data-stu-id="c728b-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="c728b-539">AzCopy: Büyük ölçekli kopyalama senaryoları için en iyi duruma getirilmiş</span><span class="sxs-lookup"><span data-stu-id="c728b-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="c728b-540">AzCopy: Coğrafi olarak yedekli depolamaya okuma erişimi desteği</span><span class="sxs-lookup"><span data-stu-id="c728b-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="c728b-541">AzCopy: yeniden başlatılabilir modu ve SAS belirteci ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="c728b-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="c728b-542">AzCopy: arası hesap kopyalama Blob kullanma</span><span class="sxs-lookup"><span data-stu-id="c728b-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="c728b-543">AzCopy: Azure BLOB'ları karşıya yükleme ve indirme dosyaları</span><span class="sxs-lookup"><span data-stu-id="c728b-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

