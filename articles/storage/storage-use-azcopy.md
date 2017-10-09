---
title: "aaaCopy veya taşıma veri tooAzure Storage ile AzCopy Windows | Microsoft Docs"
description: "Blob, tablo ve dosya içeriği Windows yardımcı programı toomove veya kopya veri tooor Hello AzCopy kullanın. Yerel dosyalarından veri tooAzure depolama kopyalayın veya içinde veya depolama hesapları arasında veri kopyalayın. Kolayca, veri tooAzure depolama geçirin."
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
ms.openlocfilehash: a77db84c3a3e06f0ad4e87d02b14a5c62ed8d9ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a><span data-ttu-id="d91ab-105">Windows hello AzCopy ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="d91ab-105">Transfer data with hello AzCopy on Windows</span></span>
<span data-ttu-id="d91ab-106">AzCopy en uygun performans ile basit komutları kullanarak Microsoft Azure Blob, dosya ve tablo depolama biriminden veri tooand kopyalanması için tasarlanmış bir komut satırı yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-106">AzCopy is a command-line utility designed for copying data tooand from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="d91ab-107">Bir nesne tooanother veri depolama hesabınızda veya depolama hesapları arasında kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91ab-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="d91ab-108">İndirebilirsiniz AzCopy iki sürümü vardır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="d91ab-109">AzCopy Windows .NET Framework ile oluşturulur ve Windows stili komut satırı seçenekleri sunar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="d91ab-110">[Linux üzerinde AzCopy](storage-use-azcopy-linux.md) çekirdek, POSIX stili komut satırı seçenekleri sunan Linux platformlar hedefler ile .NET Framework yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="d91ab-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="d91ab-111">Bu makalede Windows AzCopy kapsar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="d91ab-112">AzCopy yükleyip</span><span class="sxs-lookup"><span data-stu-id="d91ab-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="d91ab-113">Windows üzerinde AzCopy</span><span class="sxs-lookup"><span data-stu-id="d91ab-113">AzCopy on Windows</span></span>
<span data-ttu-id="d91ab-114">Merhaba karşıdan [AzCopy Windows en son sürümünü](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="d91ab-114">Download hello [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="d91ab-115">Windows yükleme</span><span class="sxs-lookup"><span data-stu-id="d91ab-115">Installation on Windows</span></span>
<span data-ttu-id="d91ab-116">AzCopy hello Yükleyicisi'ni kullanarak Windows yükledikten sonra bir komut penceresi açın ve toohello AzCopy yükleme dizini, bilgisayarınızdaki - hello burada gidin `AzCopy.exe` yürütülebilir bulunur.</span><span class="sxs-lookup"><span data-stu-id="d91ab-116">After installing AzCopy on Windows using hello installer, open a command window and navigate toohello AzCopy installation directory on your computer - where hello `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="d91ab-117">İsterseniz, hello AzCopy yükleme konumu tooyour sistem yolu ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91ab-117">If desired, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="d91ab-118">Varsayılan olarak, AzCopy da yüklü olduğundan`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` veya `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="d91ab-118">By default, AzCopy is installed too`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="d91ab-119">İlk AzCopy komut yazma</span><span class="sxs-lookup"><span data-stu-id="d91ab-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="d91ab-120">AzCopy komutları Hello temel sözdizimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d91ab-120">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="d91ab-121">Örnek hello çeşitli Microsoft Azure BLOB'ları, dosyaları ve tablolardan veri tooand kopyalama senaryoları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-121">hello following examples demonstrate a variety of scenarios for copying data tooand from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="d91ab-122">Toohello başvuran [AzCopy parametreleri](#azcopy-parameters) her örnekte kullanılan hello parametreler ayrıntılı bir açıklaması için bölüm.</span><span class="sxs-lookup"><span data-stu-id="d91ab-122">Refer toohello [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="d91ab-123">BLOB: karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="d91ab-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="d91ab-124">Tek blob indirin</span><span class="sxs-lookup"><span data-stu-id="d91ab-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="d91ab-125">Unutmayın hello klasörü `C:\myfolder` yok, AzCopy oluşturmak ve indirme `abc.txt ` hello yeni klasöre.</span><span class="sxs-lookup"><span data-stu-id="d91ab-125">Note that if hello folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="d91ab-126">Tek blob ikincil bölge ' indirin</span><span class="sxs-lookup"><span data-stu-id="d91ab-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="d91ab-127">Okuma erişimli coğrafi olarak yedekli depolama etkin olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="d91ab-128">Tüm BLOB'ları indirme</span><span class="sxs-lookup"><span data-stu-id="d91ab-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="d91ab-129">Merhaba aşağıdaki varsayın BLOB'lar hello belirtilen kapsayıcısında bulunur:</span><span class="sxs-lookup"><span data-stu-id="d91ab-129">Assume hello following blobs reside in hello specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="d91ab-130">Merhaba yükleme işleminden sonra dizin hello `C:\myfolder` hello aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="d91ab-130">After hello download operation, hello directory `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="d91ab-131">Seçeneği belirtmezseniz, `/S`, blob yok indirilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-131">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="d91ab-132">BLOB'lar ile belirtilen bir önek indirin</span><span class="sxs-lookup"><span data-stu-id="d91ab-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="d91ab-133">Merhaba aşağıdaki varsayın BLOB'lar hello belirtilen kapsayıcısında bulunur.</span><span class="sxs-lookup"><span data-stu-id="d91ab-133">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="d91ab-134">Merhaba önek ile başlayan tüm BLOB'lar `a` yüklenir:</span><span class="sxs-lookup"><span data-stu-id="d91ab-134">All blobs beginning with hello prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="d91ab-135">Merhaba yükleme işleminden sonra klasörü hello `C:\myfolder` hello aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="d91ab-135">After hello download operation, hello folder `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="d91ab-136">Merhaba önek hello blob adı ilk kısmı hello forms toohello sanal dizini uygular.</span><span class="sxs-lookup"><span data-stu-id="d91ab-136">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="d91ab-137">Yukarıda gösterilen hello örnekte yüklenmez şekilde hello sanal dizin hello Belirtilen önek, eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="d91ab-137">In hello example shown above, hello virtual directory does not match hello specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="d91ab-138">Merhaba, ayrıca, seçenek `\S` belirtilmezse, AzCopy değil BLOB indirin.</span><span class="sxs-lookup"><span data-stu-id="d91ab-138">In addition, if hello option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="d91ab-139">Dışa aktarılan dosyaları toobe hello son değişiklik saatini ayarlayın kaynak BLOB'ları hello aynı</span><span class="sxs-lookup"><span data-stu-id="d91ab-139">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="d91ab-140">Son değiştiren bunların zamana dayalı hello indirme işlemi de BLOB'lar hariç tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91ab-140">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="d91ab-141">Tooexclude BLOB'lar, son değişiklik zamanını hello aynı ya da hello hedef dosya daha yeni olan isterseniz, örneğin, hello ekleyin `/XN` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="d91ab-141">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="d91ab-142">Veya, son değişiklik zamanını hello aynı ya da hello hedef dosyanın daha eski olan tooexclude BLOB'ları istiyorsanız hello ekleyin `/XO` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="d91ab-142">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="d91ab-143">BLOB: karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="d91ab-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="d91ab-144">Tek dosya karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d91ab-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="d91ab-145">Hello belirtilen hedef kapsayıcı mevcut değilse, AzCopy oluşturun ve hello dosyası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d91ab-145">If hello specified destination container does not exist, AzCopy will create it and upload hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="d91ab-146">Tek dosya toovirtual dizin karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="d91ab-146">Upload single file toovirtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="d91ab-147">Merhaba belirtilen sanal dizin yok, AzCopy hello dosya tooinclude hello sanal dizin adının içinde karşıya yükler (*örneğin*, `vd/abc.txt` yukarıdaki hello örnekteki).</span><span class="sxs-lookup"><span data-stu-id="d91ab-147">If hello specified virtual directory does not exist, AzCopy will upload hello file tooinclude hello virtual directory in its name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="d91ab-148">Tüm dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d91ab-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="d91ab-149">Seçeneğini belirterek `/S` hello yüklemeleri Merhaba içeriğine belirtilen dizin tooBlob depolama yinelemeli olarak tüm alt klasörleri ve bunların dosyaları da karşıya yüklenecek olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-149">Specifying option `/S` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="d91ab-150">Örneği için hello aşağıdaki varsayın dosyaları klasöründe bulunan `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="d91ab-150">For instance, assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="d91ab-151">Merhaba karşıya yükleme işleminden sonra aşağıdaki dosyaları hello hello kapsayıcı içerir:</span><span class="sxs-lookup"><span data-stu-id="d91ab-151">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="d91ab-152">Seçeneği belirtmezseniz, `/S`, AzCopy değil yinelemeli olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d91ab-152">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="d91ab-153">Merhaba karşıya yükleme işleminden sonra aşağıdaki dosyaları hello hello kapsayıcı içerir:</span><span class="sxs-lookup"><span data-stu-id="d91ab-153">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="d91ab-154">Belirtilen desenle eşleşen dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d91ab-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="d91ab-155">Merhaba aşağıdaki varsayın dosyaları klasöründe bulunan `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="d91ab-155">Assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="d91ab-156">Merhaba karşıya yükleme işleminden sonra aşağıdaki dosyaları hello hello kapsayıcı içerir:</span><span class="sxs-lookup"><span data-stu-id="d91ab-156">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="d91ab-157">Seçeneği belirtmezseniz, `/S`, AzCopy yalnızca sanal bir dizinde bulunan değilsiniz BLOB'ları karşıya:</span><span class="sxs-lookup"><span data-stu-id="d91ab-157">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="d91ab-158">Hedef BLOB Hello MIME içerik türünü belirtin</span><span class="sxs-lookup"><span data-stu-id="d91ab-158">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="d91ab-159">Çok hedef blob hello içerik türü varsayılan olarak, AzCopy ayarlar`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="d91ab-159">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="d91ab-160">3.1.0 sürümünden başlayarak, hello içerik türü hello seçeneği aracılığıyla açıkça belirtebilirsiniz `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="d91ab-160">Beginning with version 3.1.0, you can explicitly specify hello content type via hello option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="d91ab-161">Bu sözdiziminin hello içerik türü için tüm BLOB'ları bir karşıya yükleme işleminde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-161">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="d91ab-162">Belirtirseniz `/SetContentType` olmayan bir değer, ardından AzCopy her blob veya dosyanın içerik türü dosya uzantısı tooits göre ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-162">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="d91ab-163">BLOB: kopyalama</span><span class="sxs-lookup"><span data-stu-id="d91ab-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="d91ab-164">Depolama hesabı içinde tek blob kopyalama</span><span class="sxs-lookup"><span data-stu-id="d91ab-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="d91ab-165">Bir depolama hesabındaki blob kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="d91ab-166">Tek blob depolama hesapları arasında kopyalama</span><span class="sxs-lookup"><span data-stu-id="d91ab-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="d91ab-167">Bir blob depolama hesapları arasında kopyaladığınızda, bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="d91ab-168">İkincil bölge tooprimary bölgesinden tek blob kopyalama</span><span class="sxs-lookup"><span data-stu-id="d91ab-168">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="d91ab-169">Okuma erişimli coğrafi olarak yedekli depolama etkin olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="d91ab-170">Depolama hesapları arasında tek blob ve onun anlık görüntüleri kopyalama</span><span class="sxs-lookup"><span data-stu-id="d91ab-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="d91ab-171">Merhaba kopyalama işleminden sonra hello hedef kapsayıcı hello blob ve kendi anlık görüntülerini içerir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-171">After hello copy operation, hello target container will include hello blob and its snapshots.</span></span> <span data-ttu-id="d91ab-172">Merhaba blob yukarıdaki hello örnekte iki anlık görüntüsü sahip olduğunu varsayarak, hello kapsayıcı hello aşağıdaki içerecektir blob ve anlık görüntüler:</span><span class="sxs-lookup"><span data-stu-id="d91ab-172">Assuming hello blob in hello example above has two snapshots, hello container will include hello following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="d91ab-173">Zaman uyumlu olarak depolama hesapları arasında BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="d91ab-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="d91ab-174">AzCopy varsayılan olarak, iki depolama uç noktaları arasında verileri zaman uyumsuz olarak kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="d91ab-175">Bu nedenle, başlangıç kopyalama işlemi hiçbir SLA sahip yedek bant genişliğini kapasite kullanarak hello arka planda çalışır açısından ne kadar hızlı bir blob kopyalanır ve hello kopyalama tamamlandı başarısız oldu veya kadar AzCopy hello kopyalama durumu düzenli olarak denetler.</span><span class="sxs-lookup"><span data-stu-id="d91ab-175">Therefore, hello copy operation will run in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check hello copy status until hello copying is completed or failed.</span></span>

<span data-ttu-id="d91ab-176">Merhaba `/SyncCopy` seçeneği, hello kopyalama işlemi tutarlı hızı elde etmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-176">hello `/SyncCopy` option ensures that hello copy operation will get consistent speed.</span></span> <span data-ttu-id="d91ab-177">AzCopy hello BLOB'lar yükleyerek hello zaman uyumlu kopyası gerçekleştirir toocopy hello öğesinden belirtilen kaynak toolocal bellek ve ardından toohello Blob Depolama Hedef karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="d91ab-177">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="d91ab-178">`/SyncCopy`Karşılaştırılan tooasynchronous kopyalama hello maliyet ek çıkış önerilen yaklaşımı oluşturabilir toouse bu hello olan bir Azure VM seçenektir aynı bölgede kaynak depolama hesabı tooavoid çıkışı maliyeti.</span><span class="sxs-lookup"><span data-stu-id="d91ab-178">`/SyncCopy` might generate additional egress cost compared tooasynchronous copy, hello recommended approach is toouse this option in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="d91ab-179">Dosya: karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="d91ab-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="d91ab-180">Tek dosya indirme</span><span class="sxs-lookup"><span data-stu-id="d91ab-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="d91ab-181">Merhaba kaynağıdır Azure dosya paylaşımının, sonra da hello tam dosya adı belirtmelisiniz belirtilmişse (*örneğin* `abc.txt`) toodownload tek bir dosya veya seçeneğini belirtin `/S` toodownload tüm dosyaları hello paylaşımı yinelemeli olarak.</span><span class="sxs-lookup"><span data-stu-id="d91ab-181">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `/S` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="d91ab-182">Bir dosya düzeni ve seçenek toospecify çalışırken `/S` birlikte bir hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-182">Attempting toospecify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="d91ab-183">Tüm dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="d91ab-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="d91ab-184">Boş klasörleri indirilmeyecek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-184">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="d91ab-185">Dosya: karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="d91ab-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="d91ab-186">Tek dosya karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d91ab-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="d91ab-187">Tüm dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d91ab-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="d91ab-188">Boş klasörleri karşıya unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-188">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="d91ab-189">Belirtilen desenle eşleşen dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d91ab-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="d91ab-190">Dosya: kopyalama</span><span class="sxs-lookup"><span data-stu-id="d91ab-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="d91ab-191">Dosya paylaşımlarında kopyalayın</span><span class="sxs-lookup"><span data-stu-id="d91ab-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="d91ab-192">Dosya paylaşımlarında bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="d91ab-193">Dosya Paylaşımı tooblob kopyalayın</span><span class="sxs-lookup"><span data-stu-id="d91ab-193">Copy from file share tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="d91ab-194">Dosya Paylaşımı tooblob bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-194">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="d91ab-195">BLOB toofile paylaşımından kopyalayın</span><span class="sxs-lookup"><span data-stu-id="d91ab-195">Copy from blob toofile share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="d91ab-196">Blob toofile paylaşımından bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-196">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="d91ab-197">Zaman uyumlu olarak dosyaları kopyalayın</span><span class="sxs-lookup"><span data-stu-id="d91ab-197">Synchronously copy files</span></span>
<span data-ttu-id="d91ab-198">Merhaba belirtebilirsiniz `/SyncCopy` seçeneğini dosya depolama tooBlob depolama alanından, depolama, File Storage tooFile toocopy verileri ve Blob Depolama tooFile depolama alanından eşzamanlı olarak, AzCopy hello kaynak veri toolocal bellek yükleyerek bunu yapar ve yükleyin yeniden toodestination.</span><span class="sxs-lookup"><span data-stu-id="d91ab-198">You can specify hello `/SyncCopy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously, AzCopy does this by downloading hello source data toolocal memory and upload it again toodestination.</span></span> <span data-ttu-id="d91ab-199">Standart çıkış maliyet uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-199">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="d91ab-200">Dosya depolama tooBlob depolama kopyalarken hello varsayılan blob türü blok blobu, kullanıcı seçeneği belirtebilirsiniz `/BlobType:page` toochange hello hedef blob türü.</span><span class="sxs-lookup"><span data-stu-id="d91ab-200">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="d91ab-201">Unutmayın `/SyncCopy` karşılaştırma tooasynchronous kopyalama maliyet ek çıkış oluşturabilir, hello önerilen yaklaşım ise bu seçeneği hello hello olan Azure VM toouse aynı bölgede kaynak depolama hesabı tooavoid çıkışı maliyeti.</span><span class="sxs-lookup"><span data-stu-id="d91ab-201">Note that `/SyncCopy` might generate additional egress cost comparing tooasynchronous copy, hello recommended approach is toouse this option in hello Azure VM which is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="d91ab-202">Tablo: dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="d91ab-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="d91ab-203">Dışarı aktarma tablosu</span><span class="sxs-lookup"><span data-stu-id="d91ab-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="d91ab-204">AzCopy bir bildirim dosyası toohello belirtilen hedef klasör yazar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-204">AzCopy writes a manifest file toohello specified destination folder.</span></span> <span data-ttu-id="d91ab-205">Merhaba bildirim dosyası hello alma işlemi toolocate hello gerekli verileri dosyalarında kullanılır ve veri doğrulama gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d91ab-205">hello manifest file is used in hello import process toolocate hello necessary data files and perform data validation.</span></span> <span data-ttu-id="d91ab-206">Merhaba bildirim dosyası adlandırma kuralı varsayılan olarak aşağıdaki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="d91ab-206">hello manifest file uses hello following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="d91ab-207">Kullanıcı ayrıca hello seçeneği belirtin `/Manifest:<manifest file name>` tooset hello yayılma dosyası adı.</span><span class="sxs-lookup"><span data-stu-id="d91ab-207">User can also specify hello option `/Manifest:<manifest file name>` tooset hello manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="d91ab-208">Birden çok dosyalarına bölünmüş dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="d91ab-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="d91ab-209">AzCopy kullanan bir *birim dizin* veri bölme hello dosya toodistinguish birden çok dosya adları.</span><span class="sxs-lookup"><span data-stu-id="d91ab-209">AzCopy uses a *volume index* in hello split data file names toodistinguish multiple files.</span></span> <span data-ttu-id="d91ab-210">Merhaba birim dizini iki bölümden oluşur bir *bölüm anahtarı aralığının dizin* ve *bölünmüş dosya dizini*.</span><span class="sxs-lookup"><span data-stu-id="d91ab-210">hello volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="d91ab-211">Her iki dizinleri sıfır tabanlı.</span><span class="sxs-lookup"><span data-stu-id="d91ab-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="d91ab-212">Merhaba bölüm anahtarı aralığının dizin 0 olacaktır, kullanıcı seçeneği belirlemezse `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="d91ab-212">hello partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="d91ab-213">Örneğin, AzCopy seçeneği hello kullanıcının belirttiği sonra iki veri dosyalarını oluşturur düşünelim `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="d91ab-213">For instance, suppose AzCopy generates two data files after hello user specifies option `/SplitSize`.</span></span> <span data-ttu-id="d91ab-214">veri dosyası adları kaynaklanan hello olabilir:</span><span class="sxs-lookup"><span data-stu-id="d91ab-214">hello resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="d91ab-215">Bu hello olası en küçük değerin seçenek için Not `/SplitSize` 32 MB'dir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-215">Note that hello minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="d91ab-216">Merhaba hedef Blob Depolama belirtilirse, AzCopy hello veri dosyası bir kez kendi boyutları ulaştığında hello blob boyutu sınırlaması (200 GB) bölme, bakılmaksızın olup seçeneği `/SplitSize` hello kullanıcı tarafından belirtilen.</span><span class="sxs-lookup"><span data-stu-id="d91ab-216">If hello specified destination is Blob storage, AzCopy will split hello data file once its sizes reaches hello blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by hello user.</span></span>

### <a name="export-table-toojson-or-csv-data-file-format"></a><span data-ttu-id="d91ab-217">Dışarı aktarma tablosu tooJSON veya CSV veri dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="d91ab-217">Export table tooJSON or CSV data file format</span></span>
<span data-ttu-id="d91ab-218">Varsayılan olarak AzCopy tabloları tooJSON veri dosyalarını dışarı aktarır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-218">AzCopy by default exports tables tooJSON data files.</span></span> <span data-ttu-id="d91ab-219">Merhaba seçeneği belirtebilirsiniz `/PayloadFormat:JSON|CSV` tooexport hello tablolar JSON veya CSV olarak.</span><span class="sxs-lookup"><span data-stu-id="d91ab-219">You can specify hello option `/PayloadFormat:JSON|CSV` tooexport hello tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="d91ab-220">Merhaba CSV yük biçimi belirtirken, AzCopy ayrıca dosya uzantısına sahip bir şema dosyası oluştur `.schema.csv` her veri dosyası için.</span><span class="sxs-lookup"><span data-stu-id="d91ab-220">When specifying hello CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="d91ab-221">Tablo varlıkları eşzamanlı olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="d91ab-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="d91ab-222">AzCopy, eşzamanlı işlem tooexport varlıklar başlayacak, hello kullanıcı seçeneği belirttiğinde `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="d91ab-222">AzCopy will start concurrent operations tooexport entities when hello user specifies option `/PKRS`.</span></span> <span data-ttu-id="d91ab-223">Her bir işlemin bir bölüm anahtarı aralığının dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="d91ab-224">Merhaba eşzamanlı işlem sayısını da seçeneği tarafından denetlendiğini unutmayın `/NC`.</span><span class="sxs-lookup"><span data-stu-id="d91ab-224">Note that hello number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="d91ab-225">AzCopy kullanan çekirdekli işlemciler hello sayısı hello varsayılan değeri olarak `/NC` tablo varlıkları kopyalarken olsa bile `/NC` belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="d91ab-225">AzCopy uses hello number of core processors as hello default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="d91ab-226">Merhaba kullanıcı seçeneği belirttiğinde `/PKRS`, AzCopy hello hello iki değerleri - bölüm anahtar aralıklarına karşılık örtük veya açık olarak belirtilen eşzamanlı işlemleri - toodetermine hello eşzamanlı işlem toostart sayıda küçük kullanır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-226">When hello user specifies option `/PKRS`, AzCopy uses hello smaller of hello two values - partition key ranges versus implicitly or explicitly specified concurrent operations - toodetermine hello number of concurrent operations toostart.</span></span> <span data-ttu-id="d91ab-227">Daha fazla ayrıntı için yazın `AzCopy /?:NC` hello komut satırında.</span><span class="sxs-lookup"><span data-stu-id="d91ab-227">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="export-table-tooblob"></a><span data-ttu-id="d91ab-228">Tablo tooblob dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="d91ab-228">Export table tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="d91ab-229">AzCopy adlandırma kuralı aşağıdaki ile Merhaba blob kapsayıcısı içinde bir JSON veri dosyası oluşturur:</span><span class="sxs-lookup"><span data-stu-id="d91ab-229">AzCopy will generate a JSON data file into hello blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="d91ab-230">oluşturulan hello JSON veri dosyası en küçük meta verileri için hello yük biçimi izler.</span><span class="sxs-lookup"><span data-stu-id="d91ab-230">hello generated JSON data file follows hello payload format for minimal metadata.</span></span> <span data-ttu-id="d91ab-231">Bu yük biçimi hakkında daha fazla bilgi için bkz: [tablo hizmeti işlemleri için yük biçimi](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="d91ab-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="d91ab-232">Tablolar tooblobs dışarı aktarılırken AzCopy hello tablo varlıkları toolocal geçici veri dosyalarını indirir ve bu varlıkları toohello blob karşıya yükleme olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-232">Note that when exporting tables tooblobs, AzCopy will download hello Table entities toolocal temporary data files and then upload those entities toohello blob.</span></span> <span data-ttu-id="d91ab-233">Bu geçici veri dosyalarını hello varsayılan yolu ile hello günlük dosyası klasörü içine konur "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>" olarak seçeneği belirtebilirsiniz/Z: [günlük dosyası klasörü] toochange hello günlük dosyası klasörü konumu ve bu nedenle hello geçici veri dosyaları konumunu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d91ab-233">These temporary data files are put into hello journal file folder with hello default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] toochange hello journal file folder location and thus change hello temporary data files location.</span></span> <span data-ttu-id="d91ab-234">Merhaba, silindikten sonra hello geçici veri dosyasında yerel disk hemen silinecek rağmen dosyalarının boyutu, tablo varlıklarınızı boyutu ve hello seçeneği /SplitSize ile belirtilen hello boyutu tarafından belirlenir geçici verileri karşıya toohello blob, lütfen emin olun silinmeden önce yeterli yerel disk alanı toostore bu geçici veri dosyalarını sahip.</span><span class="sxs-lookup"><span data-stu-id="d91ab-234">hello temporary data files' size is decided by your table entities' size and hello size you specified with hello option /SplitSize, although hello temporary data file in local disk will be deleted instantly once it has been uploaded toohello blob, please make sure you have enough local disk space toostore these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="d91ab-235">Tablo: alma</span><span class="sxs-lookup"><span data-stu-id="d91ab-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="d91ab-236">Alma tablosu</span><span class="sxs-lookup"><span data-stu-id="d91ab-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="d91ab-237">Merhaba seçeneği `/EntityOperation` nasıl tooinsert varlıklarının içinde tablo hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-237">hello option `/EntityOperation` indicates how tooinsert entities into hello table.</span></span> <span data-ttu-id="d91ab-238">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d91ab-238">Possible values are:</span></span>

* <span data-ttu-id="d91ab-239">`InsertOrSkip`: Var olan bir varlığı atlar veya hello tabloda mevcut değilse yeni bir varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="d91ab-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="d91ab-240">`InsertOrMerge`: Birleştirir var olan bir varlığı veya hello tabloda mevcut değilse yeni bir varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="d91ab-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="d91ab-241">`InsertOrReplace`: Var olan bir varlığı değiştirir veya hello tabloda mevcut değilse yeni bir varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="d91ab-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="d91ab-242">Seçeneği belirtemezsiniz Not `/PKRS` hello alma senaryoda.</span><span class="sxs-lookup"><span data-stu-id="d91ab-242">Note that you cannot specify option `/PKRS` in hello import scenario.</span></span> <span data-ttu-id="d91ab-243">Merhaba verme senaryosu, hangi belirtmelisiniz seçeneği aksine `/PKRS` toostart eşzamanlı işlem, AzCopy varsayılan olarak başlayacak eş zamanlı görevleri bir tablo içeri aktardığınızda.</span><span class="sxs-lookup"><span data-stu-id="d91ab-243">Unlike hello export scenario, in which you must specify option `/PKRS` toostart concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="d91ab-244">Merhaba varsayılan başlatılan eşzamanlı işlem sayısını eşit toohello çekirdekli işlemciler sayısıdır; Bununla birlikte, eşzamanlı seçeneğiyle farklı sayıda belirtebilirsiniz `/NC`.</span><span class="sxs-lookup"><span data-stu-id="d91ab-244">hello default number of concurrent operations started is equal toohello number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="d91ab-245">Daha fazla ayrıntı için yazın `AzCopy /?:NC` hello komut satırında.</span><span class="sxs-lookup"><span data-stu-id="d91ab-245">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

<span data-ttu-id="d91ab-246">AzCopy yalnızca JSON değil CSV içe aktarma desteklediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="d91ab-247">AzCopy değil kullanıcı tarafından oluşturulan JSON öğesinden tablo içeri aktarmalar destekler ve dosyaları bildirimi.</span><span class="sxs-lookup"><span data-stu-id="d91ab-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="d91ab-248">Bu dosyaların her ikisinin bir AzCopy tablo verme etki alanından gelmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="d91ab-249">tooavoid hataları, lütfen değiştirmeyin hello dışarı JSON ya da bildirim dosyası.</span><span class="sxs-lookup"><span data-stu-id="d91ab-249">tooavoid errors, please do not modify hello exported JSON or manifest file.</span></span>

### <a name="import-entities-tootable-using-blobs"></a><span data-ttu-id="d91ab-250">BLOB alma varlıklar tootable kullanma</span><span class="sxs-lookup"><span data-stu-id="d91ab-250">Import entities tootable using blobs</span></span>
<span data-ttu-id="d91ab-251">Bir Blob kapsayıcısını hello aşağıdakileri içeren varsayalım: Azure tablo ve eşlik eden bildirim dosyasını temsil eden bir JSON dosyası.</span><span class="sxs-lookup"><span data-stu-id="d91ab-251">Assume a Blob container contains hello following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="d91ab-252">Bu blob kapsayıcısında hello bildirim dosyası kullanarak bir tabloya komutu tooimport varlıklar aşağıdaki hello çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d91ab-252">You can run hello following command tooimport entities into a table using hello manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="d91ab-253">Diğer AzCopy özellikleri</span><span class="sxs-lookup"><span data-stu-id="d91ab-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="d91ab-254">Merhaba hedefte mevcut olmayan veri Kopyala</span><span class="sxs-lookup"><span data-stu-id="d91ab-254">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="d91ab-255">Merhaba `/XO` ve `/XN` parametreler, sırasıyla kopyalanmasını tooexclude daha eski veya yeni kaynak kaynakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-255">hello `/XO` and `/XN` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="d91ab-256">Merhaba hedef yoksa toocopy kaynak kaynakları yalnızca istiyorsanız, her iki parametre hello AzCopy komut belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d91ab-256">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="d91ab-257">Merhaba kaynak veya hedef tablo olduğunda bu desteklenmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-257">Note that this is not supported when either hello source or destination is a table.</span></span>

### <a name="use-a-response-file-toospecify-command-line-parameters"></a><span data-ttu-id="d91ab-258">Bir yanıt dosyası toospecify komut satırı parametreleri kullanma</span><span class="sxs-lookup"><span data-stu-id="d91ab-258">Use a response file toospecify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="d91ab-259">AzCopy komut satırı parametreleri bir yanıt dosyası içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="d91ab-260">Merhaba komut satırında bir hello içeriğiyle doğrudan değiştirme hello dosyasının gerçekleştirme belirtilmiş sanki AzCopy işlemleri hello dosyasındaki parametreleri hello.</span><span class="sxs-lookup"><span data-stu-id="d91ab-260">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="d91ab-261">Adlı bir yanıt dosyası varsayın `copyoperation.txt`, satırlardan hello içerir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-261">Assume a response file named `copyoperation.txt`, that contains hello following lines.</span></span> <span data-ttu-id="d91ab-262">Tek bir satıra her AzCopy parametresi belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="d91ab-263">veya satırları ayrı:</span><span class="sxs-lookup"><span data-stu-id="d91ab-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="d91ab-264">AzCopy başarısız olacak iki hattında hello parametre bölerseniz hello için aşağıda gösterildiği gibi `/sourcekey` parametre:</span><span class="sxs-lookup"><span data-stu-id="d91ab-264">AzCopy will fail if you split hello parameter across two lines, as shown here for hello `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a><span data-ttu-id="d91ab-265">Birden çok yanıt dosyaları toospecify komut satırı parametreleri kullanma</span><span class="sxs-lookup"><span data-stu-id="d91ab-265">Use multiple response files toospecify command-line parameters</span></span>
<span data-ttu-id="d91ab-266">Adlı bir yanıt dosyası varsayın `source.txt` kaynak kapsayıcı belirtir:</span><span class="sxs-lookup"><span data-stu-id="d91ab-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="d91ab-267">Ve adlı bir yanıt dosyası `dest.txt` hello dosya sisteminde bir hedef klasör belirtir:</span><span class="sxs-lookup"><span data-stu-id="d91ab-267">And a response file named `dest.txt` that specifies a destination folder in hello file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="d91ab-268">Ve adlı bir yanıt dosyası `options.txt` AzCopy seçeneklerini belirtir:</span><span class="sxs-lookup"><span data-stu-id="d91ab-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="d91ab-269">AzCopy toocall bu yanıt dosyaları ile her biri bulunan bir dizinde `C:\responsefiles`, bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="d91ab-269">toocall AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="d91ab-270">Tüm hello tek tek parametreleri hello komut satırında eklenirse gibi AzCopy bu komut işler:</span><span class="sxs-lookup"><span data-stu-id="d91ab-270">AzCopy processes this command just as it would if you included all of hello individual parameters on hello command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="d91ab-271">Paylaşılan erişim imzası (SAS) belirtin</span><span class="sxs-lookup"><span data-stu-id="d91ab-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="d91ab-272">Ayrıca, bir SAS hello kapsayıcı URI belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d91ab-272">You can also specify a SAS on hello container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="d91ab-273">Günlük dosyası klasörü</span><span class="sxs-lookup"><span data-stu-id="d91ab-273">Journal file folder</span></span>
<span data-ttu-id="d91ab-274">Bir komut tooAzCopy sorun her zaman hello varsayılan klasöründe bir günlük dosyası var olup var veya bu seçeneği belirtilen bir klasörde varolup denetler.</span><span class="sxs-lookup"><span data-stu-id="d91ab-274">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="d91ab-275">Her iki yerde Hello günlük dosyası mevcut değilse, AzCopy hello işlemi yeni olarak değerlendirir ve yeni bir günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d91ab-275">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="d91ab-276">Merhaba günlük dosyası mevcut değilse, AzCopy girdiğiniz hello komut satırı hello komut satırı hello günlük dosyasında eşleşip eşleşmediğini kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="d91ab-276">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="d91ab-277">Merhaba iki komut satırları eşleşirse, AzCopy hello tamamlanmamış işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="d91ab-277">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="d91ab-278">Bunlar eşleşmiyorsa istendiğinde tooeither üzerine yaz hello günlük dosyası toostart yeni işlem ya da toocancel hello geçerli işlem olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-278">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="d91ab-279">Merhaba günlük dosyası için toouse hello varsayılan konum istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="d91ab-279">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="d91ab-280">Seçeneği unutursanız `/Z`, veya seçeneğini belirtin `/Z` hello klasör yolu, yukarıda gösterildiği gibi AzCopy hello günlük dosyası olan hello varsayılan konumda, oluşturur `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="d91ab-280">If you omit option `/Z`, or specify option `/Z` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="d91ab-281">Merhaba günlük dosyası zaten varsa, AzCopy hello günlük dosyasına dayalı hello işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="d91ab-281">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="d91ab-282">Toospecify hello günlük dosyası için özel bir konum istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="d91ab-282">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="d91ab-283">Bu örnek, zaten yoksa, hello günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d91ab-283">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="d91ab-284">Mevcut değilse, AzCopy hello günlük dosyasına dayalı hello işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="d91ab-284">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="d91ab-285">Tooresume AzCopy işlemi istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="d91ab-285">If you want tooresume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="d91ab-286">Bu örnek toocomplete başarısız olmuş hello son işlem sürdürür.</span><span class="sxs-lookup"><span data-stu-id="d91ab-286">This example resumes hello last operation, which may have failed toocomplete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="d91ab-287">Bir günlük dosyası oluşturur</span><span class="sxs-lookup"><span data-stu-id="d91ab-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="d91ab-288">Seçeneğini belirtirseniz `/V` bir dosya yolu toohello ayrıntılı günlüğü sağlamadan sonra AzCopy hello günlük dosyası olan hello varsayılan konumda oluşturur `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="d91ab-288">If you specify option `/V` without providing a file path toohello verbose log, then AzCopy creates hello log file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="d91ab-289">Aksi takdirde, özel bir konumda bir günlük dosyası oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d91ab-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="d91ab-290">Seçenek aşağıdaki göreli bir yol belirtirseniz, unutmayın `/V`, gibi `/V:test/azcopy1.log`, hello ayrıntılı günlük hello geçerli çalışma dizini adlı bir alt klasör içinde oluşturulan sonra `test`.</span><span class="sxs-lookup"><span data-stu-id="d91ab-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then hello verbose log is created in hello current working directory within a subfolder named `test`.</span></span>

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="d91ab-291">Eşzamanlı operasyonlar toostart Hello sayısını belirtin</span><span class="sxs-lookup"><span data-stu-id="d91ab-291">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="d91ab-292">Seçenek `/NC` eşzamanlı kopyalama işlemleri hello sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-292">Option `/NC` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="d91ab-293">Varsayılan olarak, belirli bir sayıda eşzamanlı işlem tooincrease hello veri aktarımı işleme AzCopy başlatır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-293">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="d91ab-294">Tablo işlemleri için hello eşzamanlı işlem elinizde işlemci sayısına eşit toohello sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-294">For Table operations, hello number of concurrent operations is equal toohello number of processors you have.</span></span> <span data-ttu-id="d91ab-295">BLOB ve dosya işlemleri, eşzamanlı işlem sayısını hello için 8 kat hello elinizde işlemci sayısına eşittir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-295">For Blob and File operations, hello number of concurrent operations is equal 8 times hello number of processors you have.</span></span> <span data-ttu-id="d91ab-296">Düşük bant genişlikli ağ üzerinden AzCopy çalıştırıyorsanız, kaynak rekabet tarafından nedeniyle /NC tooavoid hatası için daha düşük bir sayı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91ab-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC tooavoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="d91ab-297">AzCopy Azure Storage öykünücüsüne karşı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d91ab-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="d91ab-298">AzCopy hello karşı çalıştırabilirsiniz [Azure Storage öykünücüsü](storage-use-emulator.md) BLOB'lar için:</span><span class="sxs-lookup"><span data-stu-id="d91ab-298">You can run AzCopy against hello [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="d91ab-299">ve tabloları:</span><span class="sxs-lookup"><span data-stu-id="d91ab-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="d91ab-300">AzCopy parametreleri</span><span class="sxs-lookup"><span data-stu-id="d91ab-300">AzCopy Parameters</span></span>
<span data-ttu-id="d91ab-301">AzCopy için Parametreler aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="d91ab-302">AzCopy kullanma hakkında Yardım için hello komut satırından komutları aşağıdaki hello birini yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d91ab-302">You can also type one of hello following commands from hello command line for help in using AzCopy:</span></span>

* <span data-ttu-id="d91ab-303">AzCopy için ayrıntılı komut satırı Yardım için:`AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="d91ab-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="d91ab-304">Herhangi bir AzCopy parametre ile ilgili ayrıntılı yardım için:`AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="d91ab-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="d91ab-305">Komut satırı örnekleri için:`AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="d91ab-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="d91ab-306">/ Kaynak: "kaynak"</span><span class="sxs-lookup"><span data-stu-id="d91ab-306">/Source:"source"</span></span>
<span data-ttu-id="d91ab-307">Merhaba veri kaynağından hangi toocopy belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-307">Specifies hello source data from which toocopy.</span></span> <span data-ttu-id="d91ab-308">Merhaba kaynak dosya sistemi dizini, bir blob kapsayıcı, blob sanal dizin, bir depolama dosya paylaşımı, bir depolama dosyası dizini veya bir Azure tablosu olabilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-308">hello source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="d91ab-309">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="d91ab-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="d91ab-310">/ Taşınmaya: "hedef"</span><span class="sxs-lookup"><span data-stu-id="d91ab-310">/Dest:"destination"</span></span>
<span data-ttu-id="d91ab-311">Merhaba hedef toocopy belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-311">Specifies hello destination toocopy to.</span></span> <span data-ttu-id="d91ab-312">Merhaba hedef dosya sistemi dizini, bir blob kapsayıcı, blob sanal dizin, bir depolama dosya paylaşımı, bir depolama dosyası dizini veya bir Azure tablosu olabilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-312">hello destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="d91ab-313">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="d91ab-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="d91ab-314">/ Desen: "dosya deseni"</span><span class="sxs-lookup"><span data-stu-id="d91ab-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="d91ab-315">Hangi dosyaların toocopy belirten bir dosya düzeni belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-315">Specifies a file pattern that indicates which files toocopy.</span></span> <span data-ttu-id="d91ab-316">Merhaba /Pattern parametresi Hello davranışını hello kaynak verilerin hello konumunu ve hello Özyinelemeli modu seçeneği hello varlığını tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-316">hello behavior of hello /Pattern parameter is determined by hello location of hello source data, and hello presence of hello recursive mode option.</span></span> <span data-ttu-id="d91ab-317">/S. seçeneği belirtilen Özyinelemeli modu</span><span class="sxs-lookup"><span data-stu-id="d91ab-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="d91ab-318">Merhaba belirtilen kaynak bir dizin hello dosya sisteminde standart joker karakterler etkindir ve hello dizini içindeki dosyaların eşleştirme hello dosya deseni sağlanan ise.</span><span class="sxs-lookup"><span data-stu-id="d91ab-318">If hello specified source is a directory in hello file system, then standard wildcards are in effect, and hello file pattern provided is matched against files within hello directory.</span></span> <span data-ttu-id="d91ab-319">/S Belirtilen seçeneği sonra AzCopy de hello dizini altındaki tüm alt klasörlerdeki tüm dosyaları karşı hello belirtilen desenle eşleşiyorsa.</span><span class="sxs-lookup"><span data-stu-id="d91ab-319">If option /S is specified, then AzCopy also matches hello specified pattern against all files in any subfolders beneath hello directory.</span></span>

<span data-ttu-id="d91ab-320">Merhaba belirtilen kaynak blob kapsayıcısı veya sanal dizin ise, joker karakter uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="d91ab-320">If hello specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="d91ab-321">/S Belirtilen seçeneği sonra AzCopy hello belirtilen dosya düzeni blob önek olarak yorumlar varsa.</span><span class="sxs-lookup"><span data-stu-id="d91ab-321">If option /S is specified, then AzCopy interprets hello specified file pattern as a blob prefix.</span></span> <span data-ttu-id="d91ab-322">/S belirtilmezse, seçeneği sonra AzCopy tam blob adlarıyla hello dosya desen eşleşirse.</span><span class="sxs-lookup"><span data-stu-id="d91ab-322">If option /S is not specified, then AzCopy matches hello file pattern against exact blob names.</span></span>

<span data-ttu-id="d91ab-323">Merhaba kaynağıdır Azure dosya paylaşımının sonra hello tam dosya adı (örneğin abc.txt) ya da belirtmelisiniz belirtilmişse toocopy tek bir dosya veya seçeneği /S toocopy tüm dosyaları hello paylaşımı yinelemeli olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="d91ab-323">If hello specified source is an Azure file share, then you must either specify hello exact file name, (e.g. abc.txt) toocopy a single file, or specify option /S toocopy all files in hello share recursively.</span></span> <span data-ttu-id="d91ab-324">Bir dosya düzeni ve seçenek toospecify çalışırken /S birlikte bir hataya neden olur.</span><span class="sxs-lookup"><span data-stu-id="d91ab-324">Attempting toospecify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="d91ab-325">AzCopy büyük küçük harfe duyarlı bir blob kapsayıcı veya blob sanal dizin hello/Source olduğunda ve diğer durumlarda kullanan tüm eşleştirme büyük küçük harf duyarsız hello eşleşen kullanır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-325">AzCopy uses case-sensitive matching when hello /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all hello other cases.</span></span>

<span data-ttu-id="d91ab-326">Merhaba hiçbir dosya deseni belirtildiğinde kullanılan varsayılan dosya düzeni olan *.*</span><span class="sxs-lookup"><span data-stu-id="d91ab-326">hello default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="d91ab-327">bir dosya sistemi konumu veya bir Azure depolama konumu için boş bir önek.</span><span class="sxs-lookup"><span data-stu-id="d91ab-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="d91ab-328">Birden çok dosya desenlerinin belirtilmesi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="d91ab-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="d91ab-329">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="d91ab-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="d91ab-330">/ DestKey: "depolama anahtar"</span><span class="sxs-lookup"><span data-stu-id="d91ab-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="d91ab-331">Merhaba depolama hesabı anahtarı hello hedef kaynak için belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-331">Specifies hello storage account key for hello destination resource.</span></span>

<span data-ttu-id="d91ab-332">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="d91ab-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="d91ab-333">/ DestSAS: "sas belirteci"</span><span class="sxs-lookup"><span data-stu-id="d91ab-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="d91ab-334">(Eğer varsa) hello hedef için okuma ve yazma izinlerine sahip paylaşılan erişim imzası (SAS) belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for hello destination (if applicable).</span></span> <span data-ttu-id="d91ab-335">Surround hello SAS şekliyle çift tırnak işareti ile komut satırı özel karakterler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="d91ab-335">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="d91ab-336">Merhaba hedef kaynak, bir blob kapsayıcısını, dosya paylaşımı veya tablo ise, bu seçenek hello SAS belirteci tarafından izlenen ya da belirtebilirsiniz veya hello hedef blob kapsayıcısını, dosya paylaşımı veya tablonun URI, bu seçeneği olmadan bir parçası olarak hello SAS belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91ab-336">If hello destination resource is a blob container, file share or table, you can either specify this option followed by hello SAS token, or you can specify hello SAS as part of hello destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="d91ab-337">Merhaba kaynak ve hedef olan hem BLOB'ları sonra hello hedef blob hello içinde aynı bulunmalıdır hello kaynak blob depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="d91ab-337">If hello source and destination are both blobs, then hello destination blob must reside within hello same storage account as hello source blob.</span></span>

<span data-ttu-id="d91ab-338">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="d91ab-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="d91ab-339">/ SourceKey: "depolama anahtar"</span><span class="sxs-lookup"><span data-stu-id="d91ab-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="d91ab-340">Merhaba depolama hesabı anahtarı hello kaynak kaynağın belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-340">Specifies hello storage account key for hello source resource.</span></span>

<span data-ttu-id="d91ab-341">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="d91ab-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="d91ab-342">/ SourceSAS: "sas belirteci"</span><span class="sxs-lookup"><span data-stu-id="d91ab-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="d91ab-343">Merhaba kaynak için okuma ve liste izinlerine sahip paylaşılan erişim imzası (varsa) belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-343">Specifies a Shared Access Signature with READ and LIST permissions for hello source (if applicable).</span></span> <span data-ttu-id="d91ab-344">Surround hello SAS şekliyle çift tırnak işareti ile komut satırı özel karakterler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="d91ab-344">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="d91ab-345">Bir blob kapsayıcısını Hello kaynak kaynak ise ve bir anahtar ya da SAS sağlanan hello blob kapsayıcısı anonim erişim okunacak.</span><span class="sxs-lookup"><span data-stu-id="d91ab-345">If hello source resource is a blob container, and neither a key nor a SAS is provided, then hello blob container will be read via anonymous access.</span></span>

<span data-ttu-id="d91ab-346">Merhaba kaynağı bir dosya paylaşımı veya tablo ise, bir anahtar veya bir SAS sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-346">If hello source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="d91ab-347">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="d91ab-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="d91ab-348">/ S</span><span class="sxs-lookup"><span data-stu-id="d91ab-348">/S</span></span>
<span data-ttu-id="d91ab-349">Kopyalama işlemleri için özyinelemeli modunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="d91ab-350">Özyinelemeli modunda AzCopy tüm BLOB veya alt klasörler de dahil hello belirtilen dosya deseni ile eşleşen dosyaları kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-350">In recursive mode, AzCopy will copy all blobs or files that match hello specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="d91ab-351">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="d91ab-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="d91ab-352">/ BlobType: "blok" | "Sayfa" | "Ekle"</span><span class="sxs-lookup"><span data-stu-id="d91ab-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="d91ab-353">Merhaba hedef blob blok blobu, bir sayfa blob'u ya da bir ek blobu olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-353">Specifies whether hello destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="d91ab-354">Bu seçenek yalnızca bir blob karşıya yüklenirken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="d91ab-355">Aksi takdirde bir hata oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d91ab-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="d91ab-356">Merhaba hedef blob ise ve bu seçenek, varsayılan olarak, belirtilmemiş bir blok blobu AzCopy oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d91ab-356">If hello destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="d91ab-357">**Uygulanabilir:** BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="d91ab-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="d91ab-358">/ CheckMD5</span><span class="sxs-lookup"><span data-stu-id="d91ab-358">/CheckMD5</span></span>
<span data-ttu-id="d91ab-359">Karşıdan yüklenen veriler için MD5 karma değeri hesaplar ve hello blob depolanmış hello MD5 karma veya dosyanın içeriği MD5 özelliğini hesaplanan hello karmayla eşleşen doğrular.</span><span class="sxs-lookup"><span data-stu-id="d91ab-359">Calculates an MD5 hash for downloaded data and verifies that hello MD5 hash stored in hello blob or file's Content-MD5 property matches hello calculated hash.</span></span> <span data-ttu-id="d91ab-360">Bu seçenek tooperform hello MD5 denetimi verilerini yüklerken belirtmeniz gerekir böylece hello MD5 onay varsayılan olarak kapalıdır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-360">hello MD5 check is turned off by default, so you must specify this option tooperform hello MD5 check when downloading data.</span></span>

<span data-ttu-id="d91ab-361">Azure Storage için hello blob depolanan MD5 karma değeri bu hello garanti etmez Not veya dosya güncel olduğundan.</span><span class="sxs-lookup"><span data-stu-id="d91ab-361">Note that Azure Storage doesn't guarantee that hello MD5 hash stored for hello blob or file is up-to-date.</span></span> <span data-ttu-id="d91ab-362">Merhaba blob veya dosya değiştirildiğinde istemcinin sorumluluk tooupdate hello MD5 var.</span><span class="sxs-lookup"><span data-stu-id="d91ab-362">It is client's responsibility tooupdate hello MD5 whenever hello blob or file is modified.</span></span>

<span data-ttu-id="d91ab-363">AzCopy her zaman bir Azure blob veya dosya için hello Content-MD5 özelliği dosyalarını karşıya yükledikten sonra toohello hizmet ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-363">AzCopy always sets hello Content-MD5 property for an Azure blob or file after uploading it toohello service.</span></span>  

<span data-ttu-id="d91ab-364">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="d91ab-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="d91ab-365">/ Anlık görüntü</span><span class="sxs-lookup"><span data-stu-id="d91ab-365">/Snapshot</span></span>
<span data-ttu-id="d91ab-366">Gösterir olup olmadığını tootransfer anlık görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d91ab-366">Indicates whether tootransfer snapshots.</span></span> <span data-ttu-id="d91ab-367">Bu seçenek, yalnızca Hello kaynak blob olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-367">This option is only valid when hello source is a blob.</span></span>

<span data-ttu-id="d91ab-368">Merhaba aktarılan blob anlık görüntüler şu biçimde adlandırılır: blob adı (anlık görüntü-time) .extension</span><span class="sxs-lookup"><span data-stu-id="d91ab-368">hello transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="d91ab-369">Varsayılan olarak, anlık görüntüleri kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="d91ab-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="d91ab-370">**Uygulanabilir:** BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="d91ab-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="d91ab-371">/ V: [verbose-günlük dosyası]</span><span class="sxs-lookup"><span data-stu-id="d91ab-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="d91ab-372">Bir günlük dosyasına çıkarır ayrıntılı durum iletileri.</span><span class="sxs-lookup"><span data-stu-id="d91ab-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="d91ab-373">Varsayılan olarak, hello ayrıntılı günlük dosyası içinde AzCopyVerbose.log adlı `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="d91ab-373">By default, hello verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="d91ab-374">Varolan bir dosya konumu için bu seçeneği belirtirseniz, hello ayrıntılı günlük eklenmiş toothat dosyası olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-374">If you specify an existing file location for this option, hello verbose log will be appended toothat file.</span></span>  

<span data-ttu-id="d91ab-375">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="d91ab-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="d91ab-376">/ Z: [günlük dosyası klasörü]</span><span class="sxs-lookup"><span data-stu-id="d91ab-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="d91ab-377">Bir işlemi sürdürme bir günlük dosyası klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="d91ab-378">AzCopy her zaman bir işlem yarıda kesildi durumunda sürdürme destekler.</span><span class="sxs-lookup"><span data-stu-id="d91ab-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="d91ab-379">Bu seçenek belirtilmezse ya da bir klasör yolu belirtilen, AzCopy % LocalAppData%\Microsoft\Azure\AzCopy olan hello varsayılan konumda, hello günlük dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d91ab-379">If this option is not specified, or it is specified without a folder path, then AzCopy will create hello journal file in hello default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="d91ab-380">Bir komut tooAzCopy sorun her zaman hello varsayılan klasöründe bir günlük dosyası var olup var veya bu seçeneği belirtilen bir klasörde varolup denetler.</span><span class="sxs-lookup"><span data-stu-id="d91ab-380">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="d91ab-381">Her iki yerde Hello günlük dosyası mevcut değilse, AzCopy hello işlemi yeni olarak değerlendirir ve yeni bir günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d91ab-381">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="d91ab-382">Merhaba günlük dosyası mevcut değilse, AzCopy girdiğiniz hello komut satırı hello komut satırı hello günlük dosyasında eşleşip eşleşmediğini kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="d91ab-382">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="d91ab-383">Merhaba iki komut satırları eşleşirse, AzCopy hello tamamlanmamış işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="d91ab-383">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="d91ab-384">Bunlar eşleşmiyorsa istendiğinde tooeither üzerine yaz hello günlük dosyası toostart yeni işlem ya da toocancel hello geçerli işlem olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-384">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="d91ab-385">Merhaba günlük dosyası hello işlemi başarıyla tamamlandıktan sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-385">hello journal file is deleted upon successful completion of hello operation.</span></span>

<span data-ttu-id="d91ab-386">AzCopy önceki bir sürümü tarafından oluşturulmuş bir günlük dosyasından bir işlemi sürdürme desteklenmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="d91ab-387">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="d91ab-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="d91ab-388">/@:"Parameter-File"</span><span class="sxs-lookup"><span data-stu-id="d91ab-388">/@:"parameter-file"</span></span>
<span data-ttu-id="d91ab-389">Parametreleri içeren dosyayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="d91ab-390">Merhaba komut satırında bunlar yalnızca belirtilmiş sanki AzCopy işlemleri hello dosyasındaki parametreleri hello.</span><span class="sxs-lookup"><span data-stu-id="d91ab-390">AzCopy processes hello parameters in hello file just as if they had been specified on hello command line.</span></span>

<span data-ttu-id="d91ab-391">Bir yanıt dosyası, tek bir satıra birden çok parametreleri belirtin veya kendi satırında her parametre belirtin.</span><span class="sxs-lookup"><span data-stu-id="d91ab-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="d91ab-392">Tek bir parametre birden çok satıra yayılamaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="d91ab-393">Yanıt dosyaları hello # sembolü ile başlayan açıklamaları çizgiler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-393">Response files can include comments lines that begin with hello # symbol.</span></span>

<span data-ttu-id="d91ab-394">Birden çok yanıt dosyaları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91ab-394">You can specify multiple response files.</span></span> <span data-ttu-id="d91ab-395">Ancak, AzCopy iç içe yanıt dosyaları desteklemiyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="d91ab-396">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="d91ab-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="d91ab-397">/Y</span><span class="sxs-lookup"><span data-stu-id="d91ab-397">/Y</span></span>
<span data-ttu-id="d91ab-398">Tüm AzCopy onay komut istemlerini bastırır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="d91ab-399">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="d91ab-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="d91ab-400">/L</span><span class="sxs-lookup"><span data-stu-id="d91ab-400">/L</span></span>
<span data-ttu-id="d91ab-401">Yalnızca bir listeleme işlemi belirtir; hiçbir veri kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="d91ab-402">AzCopy yorumlama hello kullanarak bu olmadan çalışan hello komut satırı için bir benzetimi olarak bu seçeneğin /L seçeneği ve kaç tane nesneleri kopyalanacak sayısı, seçeneği belirtebilirsiniz /V hello adresindeki aynı zaman toocheck hangi nesnelerin hello ayrıntılı günlüğüne kopyalanacak.</span><span class="sxs-lookup"><span data-stu-id="d91ab-402">AzCopy will interpret hello using of this option as a simulation for running hello command line without this option /L and count how many objects will be copied, you can specify option /V at hello same time toocheck which objects will be copied in hello verbose log.</span></span>

<span data-ttu-id="d91ab-403">Bu seçenek Hello davranışını da hello kaynak verilerin hello konumunu ve hello Özyinelemeli modu seçeneği/s ve dosya düzeni seçeneği /Pattern hello varlığını tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-403">hello behavior of this option is also determined by hello location of hello source data and hello presence of hello recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="d91ab-404">AzCopy, bu seçenek kullanıldığında bu kaynak konumunun listesi ve okuma izni gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="d91ab-405">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="d91ab-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="d91ab-406">/ MT</span><span class="sxs-lookup"><span data-stu-id="d91ab-406">/MT</span></span>
<span data-ttu-id="d91ab-407">Merhaba indirilen dosyanın son değiştirilme zamanı toobe Merhaba, aynı, hello kaynak blob veya dosya ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-407">Sets hello downloaded file's last-modified time toobe hello same as hello source blob or file's.</span></span>

<span data-ttu-id="d91ab-408">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="d91ab-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="d91ab-409">/XN</span><span class="sxs-lookup"><span data-stu-id="d91ab-409">/XN</span></span>
<span data-ttu-id="d91ab-410">Daha yeni bir kaynak kaynak dışlar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-410">Excludes a newer source resource.</span></span> <span data-ttu-id="d91ab-411">Merhaba hello kaynağının son değişiklik zamanını hello aynı veya daha yeni hedef ise hello kaynak kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="d91ab-411">hello resource will not be copied if hello last modified time of hello source is hello same or newer than destination.</span></span>

<span data-ttu-id="d91ab-412">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="d91ab-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="d91ab-413">/XO</span><span class="sxs-lookup"><span data-stu-id="d91ab-413">/XO</span></span>
<span data-ttu-id="d91ab-414">Eski bir kaynak kaynak dışlar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-414">Excludes an older source resource.</span></span> <span data-ttu-id="d91ab-415">Merhaba hello kaynağının son değişiklik zamanını hello aynı ya da hedef daha eski ise hello kaynak kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="d91ab-415">hello resource will not be copied if hello last modified time of hello source is hello same or older than destination.</span></span>

<span data-ttu-id="d91ab-416">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="d91ab-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="d91ab-417">/A</span><span class="sxs-lookup"><span data-stu-id="d91ab-417">/A</span></span>
<span data-ttu-id="d91ab-418">Yalnızca hello arşiv özniteliği kümesine sahip dosyaları karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="d91ab-418">Uploads only files that have hello Archive attribute set.</span></span>

<span data-ttu-id="d91ab-419">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="d91ab-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="d91ab-420">/ IA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="d91ab-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="d91ab-421">Belirtilen öznitelikler kümesi hello olan yüklemeler yalnızca dosyaları.</span><span class="sxs-lookup"><span data-stu-id="d91ab-421">Uploads only files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="d91ab-422">Mevcut öznitelikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d91ab-422">Available attributes include:</span></span>

* <span data-ttu-id="d91ab-423">R Salt okunur dosyalar =</span><span class="sxs-lookup"><span data-stu-id="d91ab-423">R = Read-only files</span></span>
* <span data-ttu-id="d91ab-424">Arşivlenmeye hazır dosyalar bir =</span><span class="sxs-lookup"><span data-stu-id="d91ab-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="d91ab-425">S sistem dosyaları =</span><span class="sxs-lookup"><span data-stu-id="d91ab-425">S = System files</span></span>
* <span data-ttu-id="d91ab-426">H Gizli dosyalar =</span><span class="sxs-lookup"><span data-stu-id="d91ab-426">H = Hidden files</span></span>
* <span data-ttu-id="d91ab-427">C Sıkıştırılmış dosyaları =</span><span class="sxs-lookup"><span data-stu-id="d91ab-427">C = Compressed files</span></span>
* <span data-ttu-id="d91ab-428">N Normal dosyalar =</span><span class="sxs-lookup"><span data-stu-id="d91ab-428">N = Normal files</span></span>
* <span data-ttu-id="d91ab-429">E Şifrelenmiş dosyaları =</span><span class="sxs-lookup"><span data-stu-id="d91ab-429">E = Encrypted files</span></span>
* <span data-ttu-id="d91ab-430">T = geçici dosyalar</span><span class="sxs-lookup"><span data-stu-id="d91ab-430">T = Temporary files</span></span>
* <span data-ttu-id="d91ab-431">O çevrimdışı dosyalar =</span><span class="sxs-lookup"><span data-stu-id="d91ab-431">O = Offline files</span></span>
* <span data-ttu-id="d91ab-432">I dosyaları olmayan dizini =</span><span class="sxs-lookup"><span data-stu-id="d91ab-432">I = Non-indexed files</span></span>

<span data-ttu-id="d91ab-433">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="d91ab-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="d91ab-434">/ XA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="d91ab-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="d91ab-435">Belirtilen hello olan dosyaları dışlar öznitelikleri kümesi.</span><span class="sxs-lookup"><span data-stu-id="d91ab-435">Excludes files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="d91ab-436">Mevcut öznitelikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d91ab-436">Available attributes include:</span></span>

* <span data-ttu-id="d91ab-437">R Salt okunur dosyalar =</span><span class="sxs-lookup"><span data-stu-id="d91ab-437">R = Read-only files</span></span>
* <span data-ttu-id="d91ab-438">Arşivlenmeye hazır dosyalar bir =</span><span class="sxs-lookup"><span data-stu-id="d91ab-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="d91ab-439">S sistem dosyaları =</span><span class="sxs-lookup"><span data-stu-id="d91ab-439">S = System files</span></span>
* <span data-ttu-id="d91ab-440">H Gizli dosyalar =</span><span class="sxs-lookup"><span data-stu-id="d91ab-440">H = Hidden files</span></span>
* <span data-ttu-id="d91ab-441">C Sıkıştırılmış dosyaları =</span><span class="sxs-lookup"><span data-stu-id="d91ab-441">C = Compressed files</span></span>
* <span data-ttu-id="d91ab-442">N Normal dosyalar =</span><span class="sxs-lookup"><span data-stu-id="d91ab-442">N = Normal files</span></span>
* <span data-ttu-id="d91ab-443">E Şifrelenmiş dosyaları =</span><span class="sxs-lookup"><span data-stu-id="d91ab-443">E = Encrypted files</span></span>
* <span data-ttu-id="d91ab-444">T = geçici dosyalar</span><span class="sxs-lookup"><span data-stu-id="d91ab-444">T = Temporary files</span></span>
* <span data-ttu-id="d91ab-445">O çevrimdışı dosyalar =</span><span class="sxs-lookup"><span data-stu-id="d91ab-445">O = Offline files</span></span>
* <span data-ttu-id="d91ab-446">I dosyaları olmayan dizini =</span><span class="sxs-lookup"><span data-stu-id="d91ab-446">I = Non-indexed files</span></span>

<span data-ttu-id="d91ab-447">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="d91ab-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="d91ab-448">/ Sınırlayıcı: "sınırlayıcı"</span><span class="sxs-lookup"><span data-stu-id="d91ab-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="d91ab-449">Bir blob adı toodelimit sanal dizinleri Hello sınırlayıcı karakter kullanılan gösterir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-449">Indicates hello delimiter character used toodelimit virtual directories in a blob name.</span></span>

<span data-ttu-id="d91ab-450">Varsayılan olarak, AzCopy kullanır / hello sınırlayıcı karakter olarak.</span><span class="sxs-lookup"><span data-stu-id="d91ab-450">By default, AzCopy uses / as hello delimiter character.</span></span> <span data-ttu-id="d91ab-451">Ancak, ortak bir karakterle kullanarak AzCopy destekler (gibi @, # ya da %) ayırıcı olarak.</span><span class="sxs-lookup"><span data-stu-id="d91ab-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="d91ab-452">Tooinclude hello komut satırında şu özel karakterleri birini gerekiyorsa, hello dosya adıyla çift tırnak içine alın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-452">If you need tooinclude one of these special characters on hello command line, enclose hello file name with double quotes.</span></span>

<span data-ttu-id="d91ab-453">Bu seçenek, yalnızca BLOB indirmek için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="d91ab-454">**Uygulanabilir:** BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="d91ab-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="d91ab-455">/ NC: "numarası-in-eşzamanlı-işlemler"</span><span class="sxs-lookup"><span data-stu-id="d91ab-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="d91ab-456">Merhaba eşzamanlı işlem sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-456">Specifies hello number of concurrent operations.</span></span>

<span data-ttu-id="d91ab-457">AzCopy varsayılan olarak, belirli bir sayıda eşzamanlı işlem tooincrease hello veri aktarımı işleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-457">AzCopy by default starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="d91ab-458">Çok sayıda eş zamanlı görevleri bir düşük bant genişlikli ortamında hello ağ bağlantısı doldurmaya ve tam olarak tamamlanmasını hello işlemlerini önlemek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm hello network connection and prevent hello operations from fully completing.</span></span> <span data-ttu-id="d91ab-459">Eşzamanlı operasyonlar gerçek kullanılabilir ağ bant genişliğine bağlı kısıtlama.</span><span class="sxs-lookup"><span data-stu-id="d91ab-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="d91ab-460">eşzamanlı operasyonlar için üst sınır Hello 512'dir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-460">hello upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="d91ab-461">**Uygulanabilir:** BLOB'lar, dosyalar, tablolar</span><span class="sxs-lookup"><span data-stu-id="d91ab-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="d91ab-462">/ Kaynak türü: "Blob" | "Tablo"</span><span class="sxs-lookup"><span data-stu-id="d91ab-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="d91ab-463">Bu hello belirtir `source` kaynaktır blob hello depolama öykünücüsünde çalıştıran hello yerel geliştirme ortamında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-463">Specifies that hello `source` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="d91ab-464">**Uygulanabilir:** BLOB'ların, tabloları</span><span class="sxs-lookup"><span data-stu-id="d91ab-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="d91ab-465">/ DestType: "Blob" | "Tablo"</span><span class="sxs-lookup"><span data-stu-id="d91ab-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="d91ab-466">Bu hello belirtir `destination` kaynaktır blob hello depolama öykünücüsünde çalıştıran hello yerel geliştirme ortamında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-466">Specifies that hello `destination` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="d91ab-467">**Uygulanabilir:** BLOB'ların, tabloları</span><span class="sxs-lookup"><span data-stu-id="d91ab-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="d91ab-468">/ PKRS: "anahtar&#1;key2 anahtar&#3;..."</span><span class="sxs-lookup"><span data-stu-id="d91ab-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="d91ab-469">Bölmelerini hello dışa aktarma işlemi hello hızını artırır paralel tablo verileri dışarı aktarma bölüm anahtarı aralığının tooenable hello.</span><span class="sxs-lookup"><span data-stu-id="d91ab-469">Splits hello partition key range tooenable exporting table data in parallel, which increases hello speed of hello export operation.</span></span>

<span data-ttu-id="d91ab-470">Bu seçenek belirtilmezse, AzCopy tek iş parçacığı tooexport tablo varlıkları kullanır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-470">If this option is not specified, then AzCopy uses a single thread tooexport table entities.</span></span> <span data-ttu-id="d91ab-471">Örneğin, hello kullanıcı /PKRS belirtir: "aa #bb" sonra AzCopy üç eşzamanlı işlem başlatır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-471">For example, if hello user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="d91ab-472">Her işlem, aşağıda gösterildiği gibi üç bölüm anahtarı aralıkları, birini verir:</span><span class="sxs-lookup"><span data-stu-id="d91ab-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="d91ab-473">[ilk bölüm anahtarı, aa)</span><span class="sxs-lookup"><span data-stu-id="d91ab-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="d91ab-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="d91ab-474">[aa, bb)</span></span>

  <span data-ttu-id="d91ab-475">[bb, son bölüm anahtarı]</span><span class="sxs-lookup"><span data-stu-id="d91ab-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="d91ab-476">**Uygulanabilir:** tabloları</span><span class="sxs-lookup"><span data-stu-id="d91ab-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="d91ab-477">/ SplitSize: "dosya boyutu"</span><span class="sxs-lookup"><span data-stu-id="d91ab-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="d91ab-478">Dışarı aktarılan dosya boyutu (MB) bölme Merhaba, izin verilen minimum değer hello 32'dir belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-478">Specifies hello exported file split size in MB, hello minimal value allowed is 32.</span></span>

<span data-ttu-id="d91ab-479">Bu seçenek belirtilmezse, AzCopy tablo veri toosingle dosyayı dışarı aktarır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-479">If this option is not specified, AzCopy will export table data toosingle file.</span></span>

<span data-ttu-id="d91ab-480">Ardından bu seçenek belirtilmezse bile hello tablo verileri dışarı aktarılan tooa blob ise ve hello dışarı aktarılan dosyayı blob boyutu hello 200 GB sınırını boyutu, AzCopy hello dışarı aktarılan dosyayı, bölecek.</span><span class="sxs-lookup"><span data-stu-id="d91ab-480">If hello table data is exported tooa blob, and hello exported file size reaches hello 200 GB limit for blob size, then AzCopy will split hello exported file, even if this option is not specified.</span></span>

<span data-ttu-id="d91ab-481">**Uygulanabilir:** tabloları</span><span class="sxs-lookup"><span data-stu-id="d91ab-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="d91ab-482">/ EntityOperation: "InsertOrSkip" | "InsertOrMerge" | "Yerleştir veya Değiştir"</span><span class="sxs-lookup"><span data-stu-id="d91ab-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="d91ab-483">Merhaba tablo veri alma davranışını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-483">Specifies hello table data import behavior.</span></span>

* <span data-ttu-id="d91ab-484">InsertOrSkip - var olan bir varlığı atlar veya hello tabloda mevcut değilse yeni bir varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="d91ab-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="d91ab-485">InsertOrMerge - var olan bir varlığı birleştirir veya hello tabloda mevcut değilse yeni bir varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="d91ab-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="d91ab-486">Yerleştir veya Değiştir - var olan bir varlığı değiştirir veya hello tabloda mevcut değilse yeni bir varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="d91ab-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="d91ab-487">**Uygulanabilir:** tabloları</span><span class="sxs-lookup"><span data-stu-id="d91ab-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="d91ab-488">/ MANIFEST: "bildirim dosyası"</span><span class="sxs-lookup"><span data-stu-id="d91ab-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="d91ab-489">Merhaba tablo dışarı ve içeri aktarma işlemi için hello bildirim dosyası belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-489">Specifies hello manifest file for hello table export and import operation.</span></span>

<span data-ttu-id="d91ab-490">Bu seçenek hello dışa aktarma işlemi sırasında isteğe bağlı olduğundan, bu seçenek belirtilmezse, AzCopy önceden tanımlanmış ada sahip bir bildirim dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d91ab-490">This option is optional during hello export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="d91ab-491">Bu seçenek, hello veri dosyalarını bulmak için hello içeri aktarma işlemi sırasında gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-491">This option is required during hello import operation for locating hello data files.</span></span>

<span data-ttu-id="d91ab-492">**Uygulanabilir:** tabloları</span><span class="sxs-lookup"><span data-stu-id="d91ab-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="d91ab-493">/ SyncCopy</span><span class="sxs-lookup"><span data-stu-id="d91ab-493">/SyncCopy</span></span>
<span data-ttu-id="d91ab-494">Gösterir toosynchronously BLOB veya iki Azure Storage uç noktalar arasında dosyaları kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-494">Indicates whether toosynchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="d91ab-495">AzCopy varsayılan olarak, sunucu tarafı zaman uyumsuz kopyayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="d91ab-496">Bu seçenek tooperform eş zamanlı belirtin, BLOB'ları yükler veya toolocal bellek dosyaları ve bunları tooAzure depolama yükler kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-496">Specify this option tooperform a synchronous copy, which downloads blobs or files toolocal memory and then uploads them tooAzure Storage.</span></span>

<span data-ttu-id="d91ab-497">Blob storage, dosya depolama içinde veya Blob, depolama tooFile depolama veya bunun tersini de içinde dosya kopyalarken, bu seçeneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91ab-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage tooFile storage or vice versa.</span></span>

<span data-ttu-id="d91ab-498">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="d91ab-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="d91ab-499">/ SetContentType: "content-type"</span><span class="sxs-lookup"><span data-stu-id="d91ab-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="d91ab-500">Hedef BLOB'ları veya dosyaları için içerik Hello MIME türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-500">Specifies hello MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="d91ab-501">İçerik türü için bir blob hello veya tooapplication/octet-stream, varsayılan olarak dosya AzCopy kümeleri.</span><span class="sxs-lookup"><span data-stu-id="d91ab-501">AzCopy sets hello content type for a blob or file tooapplication/octet-stream by default.</span></span> <span data-ttu-id="d91ab-502">Bu seçenek için bir değer açıkça belirterek hello içerik türü için tüm BLOB'ları veya dosyaları ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91ab-502">You can set hello content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="d91ab-503">Ardından, bu seçenek olmadan bir değer belirtirseniz, AzCopy her blob veya dosyanın içerik türü dosya uzantısı tooits göre ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d91ab-503">If you specify this option without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

<span data-ttu-id="d91ab-504">**Uygulanabilir:** BLOB'ların, dosyaları</span><span class="sxs-lookup"><span data-stu-id="d91ab-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="d91ab-505">/ PayloadFormat: "JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="d91ab-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="d91ab-506">Merhaba tablo dışarı aktarılan verileri dosyası Hello biçimini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-506">Specifies hello format of hello table exported data file.</span></span>

<span data-ttu-id="d91ab-507">Bu seçenek belirtilmezse, varsayılan olarak AzCopy tablo veri dosyası JSON biçiminde dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="d91ab-508">**Uygulanabilir:** tabloları</span><span class="sxs-lookup"><span data-stu-id="d91ab-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="d91ab-509">Bilinen sorunlar ve en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="d91ab-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="d91ab-510">Veri kopyalama sırasında sınırı eşzamanlı yazma</span><span class="sxs-lookup"><span data-stu-id="d91ab-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="d91ab-511">BLOB veya AzCopy dosyalarıyla kopyaladığınızda, bunu kopyalamaya çalışırken, başka bir uygulama hello veri değiştirme göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="d91ab-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="d91ab-512">Mümkünse, Kopyalamakta olduğunuz hello veri hello kopyalama işlemi sırasında değiştirilmeyen emin olun.</span><span class="sxs-lookup"><span data-stu-id="d91ab-512">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="d91ab-513">Örneğin, bir Azure sanal makine ile ilişkili bir VHD'nin kopyalarken, başka bir uygulama şu anda toohello VHD yazıyorsanız emin olun.</span><span class="sxs-lookup"><span data-stu-id="d91ab-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="d91ab-514">Bir en iyi yolu toodo bu hello kaynak toobe kiralama tarafından kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-514">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="d91ab-515">Alternatif olarak, bir anlık görüntüsünü hello VHD ilk oluşturun ve sonra hello anlık görüntüsü kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-515">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="d91ab-516">Kopyalanan sonra hello süresi hello işi tarafından bittikten unutmayın ancak diğer uygulamaların tooblobs veya dosyaları yazma önleyemez, hello kopyalanan artık hello kaynak kaynaklarla tam eşlik kaynaklarınız olabilir.</span><span class="sxs-lookup"><span data-stu-id="d91ab-516">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="d91ab-517">Bir Azcopy'i örnek bir makinede çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="d91ab-518">AzCopy, makine kaynak tooaccelerate hello veri aktarımı tasarlanmış toomaximize hello kullanımı, bir makinede yalnızca bir AzCopy çalıştırır ve hello seçeneğini belirtin öneririz `/NC` fazla eşzamanlı işlem gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="d91ab-518">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="d91ab-519">Daha fazla ayrıntı için yazın `AzCopy /?:NC` hello komut satırında.</span><span class="sxs-lookup"><span data-stu-id="d91ab-519">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="d91ab-520">FIPS uyumlu MD5 algoritmaları etkinleştirmek için AzCopy olduğunda, "kullanım FIPS uyumlu algoritmaları şifreleme, karma ve imzalama için".</span><span class="sxs-lookup"><span data-stu-id="d91ab-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="d91ab-521">AzCopy varsayılan .NET MD5 uygulama toocalculate hello MD5 nesneleri kopyalarken kullanır, ancak AzCopy tooenable FIPS uyumlu MD5 ayarı gereken bazı güvenlik gereksinimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-521">AzCopy by default uses .NET MD5 implementation toocalculate hello MD5 when copying objects, but there are some security requirements that need AzCopy tooenable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="d91ab-522">Bir app.config dosyası oluşturabilirsiniz `AzCopy.exe.config` özelliğiyle `AzureStorageUseV1MD5` ve AzCopy.exe ile kenara yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="d91ab-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="d91ab-523">"AzureStorageUseV1MD5" • özelliği için True - hello varsayılan değeri, AzCopy .NET MD5 uygulama kullanır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-523">For property "AzureStorageUseV1MD5" • True - hello default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="d91ab-524">• Yanlış – AzCopy FIPS uyumlu MD5 algoritması kullanır.</span><span class="sxs-lookup"><span data-stu-id="d91ab-524">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="d91ab-525">Not FIPS uyumlu algoritmaları Windows makinenizde varsayılan olarak devre dışıdır, secpol.msc, Çalıştır penceresine yazın ve denetleme bu güvenlik ayarı anahtara -> yerel ilke güvenlik -> Seçenekler -> Sistem şifrelemesi: şifreleme, karma ve imzalama için kullan FIPS uyumlu algoritmaları.</span><span class="sxs-lookup"><span data-stu-id="d91ab-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d91ab-526">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d91ab-526">Next steps</span></span>
<span data-ttu-id="d91ab-527">Azure Storage ve AzCopy hakkında daha fazla bilgi için aşağıdaki kaynakları toohello bakın.</span><span class="sxs-lookup"><span data-stu-id="d91ab-527">For more information about Azure Storage and AzCopy, refer toohello following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="d91ab-528">Azure Storage belgeleri:</span><span class="sxs-lookup"><span data-stu-id="d91ab-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="d91ab-529">Giriş tooAzure depolama</span><span class="sxs-lookup"><span data-stu-id="d91ab-529">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="d91ab-530">Nasıl toouse Blob depolama alanından .NET</span><span class="sxs-lookup"><span data-stu-id="d91ab-530">How toouse Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="d91ab-531">Nasıl toouse dosya depolama biriminden .NET</span><span class="sxs-lookup"><span data-stu-id="d91ab-531">How toouse File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="d91ab-532">Nasıl toouse .NET tablo depolamasından</span><span class="sxs-lookup"><span data-stu-id="d91ab-532">How toouse Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="d91ab-533">Nasıl toocreate, yönetme veya bir depolama hesabı silme</span><span class="sxs-lookup"><span data-stu-id="d91ab-533">How toocreate, manage, or delete a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="d91ab-534">Linux'ta AzCopy ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="d91ab-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="d91ab-535">Azure depolama blog gönderileri:</span><span class="sxs-lookup"><span data-stu-id="d91ab-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="d91ab-536">Azure Storage veri hareketi kitaplığı Önizleme Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="d91ab-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="d91ab-537">AzCopy: zaman uyumlu kopyası ve özelleştirilmiş içerik türü tanışın</span><span class="sxs-lookup"><span data-stu-id="d91ab-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="d91ab-538">AzCopy: Genel kullanılabilirlik, AzCopy 3.0 artı AzCopy 4.0 Önizleme sürümü tablo ve dosya desteği ile tanışın</span><span class="sxs-lookup"><span data-stu-id="d91ab-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="d91ab-539">AzCopy: Büyük ölçekli kopyalama senaryoları için en iyi duruma getirilmiş</span><span class="sxs-lookup"><span data-stu-id="d91ab-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="d91ab-540">AzCopy: Coğrafi olarak yedekli depolamaya okuma erişimi desteği</span><span class="sxs-lookup"><span data-stu-id="d91ab-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="d91ab-541">AzCopy: yeniden başlatılabilir modu ve SAS belirteci ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="d91ab-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="d91ab-542">AzCopy: arası hesap kopyalama Blob kullanma</span><span class="sxs-lookup"><span data-stu-id="d91ab-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="d91ab-543">AzCopy: Azure BLOB'ları karşıya yükleme ve indirme dosyaları</span><span class="sxs-lookup"><span data-stu-id="d91ab-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

