---
title: "aaaCopy veya taşıma veri tooAzure Storage ile AzCopy Linux'ta | Microsoft Docs"
description: "Merhaba AzCopy blob ve dosya içerikten Linux yardımcı programı toomove veya kopya veri tooor kullanın. Yerel dosyalarından veri tooAzure depolama kopyalayın veya içinde veya depolama hesapları arasında veri kopyalayın. Kolayca, veri tooAzure depolama geçirin."
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
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: ee39c311d996a046999b7fd4a4eb873f25b4eb86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="3784b-105">Linux'ta AzCopy ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="3784b-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="3784b-106">Linux üzerinde AzCopy en uygun performans ile basit komutları kullanarak Microsoft Azure Blob ve dosya depolama biriminden veri tooand kopyalanması için tasarlanmış bir komut satırı yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="3784b-106">AzCopy on Linux is a command-line utility designed for copying data tooand from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="3784b-107">Bir nesne tooanother veri depolama hesabınızda veya depolama hesapları arasında kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3784b-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="3784b-108">İndirebilirsiniz AzCopy iki sürümü vardır.</span><span class="sxs-lookup"><span data-stu-id="3784b-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="3784b-109">Linux üzerinde AzCopy .NET Core POSIX stili komut satırı seçenekleri sunan Linux platformlar hedefler Framework ile yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="3784b-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="3784b-110">[AzCopy Windows](../storage-use-azcopy.md) .NET Framework ile oluşturulan ve Windows stili komut satırı seçenekleri sunar.</span><span class="sxs-lookup"><span data-stu-id="3784b-110">[AzCopy on Windows](../storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="3784b-111">Bu makalede, AzCopy Linux üzerinde yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="3784b-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="3784b-112">AzCopy yükleyip</span><span class="sxs-lookup"><span data-stu-id="3784b-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="3784b-113">Linux üzerinde yükleme</span><span class="sxs-lookup"><span data-stu-id="3784b-113">Installation on Linux</span></span>

<span data-ttu-id="3784b-114">AzCopy Linux'ta hello platformunda .NET Core framework gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3784b-114">AzCopy on Linux requires .NET Core framework on hello platform.</span></span> <span data-ttu-id="3784b-115">Merhaba üzerinde Hello yükleme yönergelerine bakın [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) sayfası.</span><span class="sxs-lookup"><span data-stu-id="3784b-115">See hello installation instructions on hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="3784b-116">Örnek olarak, .NET Core üzerinde Ubuntu 16.10 şimdi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3784b-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="3784b-117">Merhaba son yükleme kılavuzu için ziyaret [.NET Core Linux'ta](https://www.microsoft.com/net/core#linuxubuntu) yükleme sayfası.</span><span class="sxs-lookup"><span data-stu-id="3784b-117">For hello latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="3784b-118">.NET Core yüklendiğinde, indirin ve AzCopy yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3784b-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="3784b-119">AzCopy Linux'ta yüklendikten sonra ayıklanan hello dosyalarını kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3784b-119">You can remove hello extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="3784b-120">Süper kullanıcı ayrıcalıkları yoksa, alternatif olarak, aynı zamanda hello Kabuk komut dosyasını kullanarak AzCopy 'azcopy' hello ayıklanan klasöründe çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3784b-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using hello shell script 'azcopy' in hello extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="3784b-121">Ubuntu alternatif yükleme</span><span class="sxs-lookup"><span data-stu-id="3784b-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="3784b-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="3784b-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="3784b-123">.Net için apt kaynağı Ekle Çekirdek:</span><span class="sxs-lookup"><span data-stu-id="3784b-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="3784b-124">Microsoft Linux ürün depo apt kaynağı ekleyin ve AzCopy yükleyin:</span><span class="sxs-lookup"><span data-stu-id="3784b-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

<span data-ttu-id="3784b-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="3784b-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="3784b-126">.Net için apt kaynağı Ekle Çekirdek:</span><span class="sxs-lookup"><span data-stu-id="3784b-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="3784b-127">Microsoft Linux ürün depo apt kaynağı ekleyin ve AzCopy yükleyin:</span><span class="sxs-lookup"><span data-stu-id="3784b-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

<span data-ttu-id="3784b-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="3784b-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="3784b-129">.Net için apt kaynağı Ekle Çekirdek:</span><span class="sxs-lookup"><span data-stu-id="3784b-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="3784b-130">Microsoft Linux ürün depo apt kaynağı ekleyin ve AzCopy yükleyin:</span><span class="sxs-lookup"><span data-stu-id="3784b-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="3784b-131">İlk AzCopy komut yazma</span><span class="sxs-lookup"><span data-stu-id="3784b-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="3784b-132">AzCopy komutları Hello temel sözdizimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="3784b-132">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="3784b-133">Örnek hello veri tooand Microsoft Azure BLOB'ları ve dosyalarından kopyalamak için çeşitli senaryolar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3784b-133">hello following examples demonstrate various scenarios for copying data tooand from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="3784b-134">Toohello başvuran `azcopy --help` her örnekte kullanılan hello parametrelerinin ayrıntılı bir açıklama için menüsü.</span><span class="sxs-lookup"><span data-stu-id="3784b-134">Refer toohello `azcopy --help` menu for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="3784b-135">BLOB: karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="3784b-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="3784b-136">Tek blob indirin</span><span class="sxs-lookup"><span data-stu-id="3784b-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3784b-137">Varsa hello klasörü `/mnt/myfiles` yok, AzCopy oluşturur ve indirir `abc.txt ` hello yeni klasöre.</span><span class="sxs-lookup"><span data-stu-id="3784b-137">If hello folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="3784b-138">Tek blob ikincil bölge ' indirin</span><span class="sxs-lookup"><span data-stu-id="3784b-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3784b-139">Okuma erişimli coğrafi olarak yedekli depolama etkin olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3784b-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="3784b-140">Tüm BLOB'ları indirme</span><span class="sxs-lookup"><span data-stu-id="3784b-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="3784b-141">Merhaba aşağıdaki varsayın BLOB'lar hello belirtilen kapsayıcısında bulunur:</span><span class="sxs-lookup"><span data-stu-id="3784b-141">Assume hello following blobs reside in hello specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="3784b-142">Merhaba yükleme işleminden sonra dizin hello `/mnt/myfiles` hello aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="3784b-142">After hello download operation, hello directory `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="3784b-143">Seçeneği belirtmezseniz, `--recursive`, hiçbir blob indirilir.</span><span class="sxs-lookup"><span data-stu-id="3784b-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="3784b-144">BLOB'lar ile belirtilen bir önek indirin</span><span class="sxs-lookup"><span data-stu-id="3784b-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="3784b-145">Merhaba aşağıdaki varsayın BLOB'lar hello belirtilen kapsayıcısında bulunur.</span><span class="sxs-lookup"><span data-stu-id="3784b-145">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="3784b-146">Merhaba önek ile başlayan tüm BLOB'lar `a` indirilir.</span><span class="sxs-lookup"><span data-stu-id="3784b-146">All blobs beginning with hello prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="3784b-147">Merhaba yükleme işleminden sonra klasörü hello `/mnt/myfiles` hello aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="3784b-147">After hello download operation, hello folder `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="3784b-148">Merhaba önek hello blob adı ilk kısmı hello forms toohello sanal dizini uygular.</span><span class="sxs-lookup"><span data-stu-id="3784b-148">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="3784b-149">Yukarıda gösterilen hello örnekte hiçbir blob indirilen şekilde hello sanal dizin hello Belirtilen önek, eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="3784b-149">In hello example shown above, hello virtual directory does not match hello specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="3784b-150">Merhaba, ayrıca, seçenek `--recursive` belirtilmezse, AzCopy BLOB indirmek değil.</span><span class="sxs-lookup"><span data-stu-id="3784b-150">In addition, if hello option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="3784b-151">Dışa aktarılan dosyaları toobe hello son değişiklik saatini ayarlayın kaynak BLOB'ları hello aynı</span><span class="sxs-lookup"><span data-stu-id="3784b-151">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="3784b-152">Son değiştiren bunların zamana dayalı hello indirme işlemi de BLOB'lar hariç tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3784b-152">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="3784b-153">Tooexclude BLOB'lar, son değişiklik zamanını hello aynı ya da hello hedef dosya daha yeni olan isterseniz, örneğin, hello ekleyin `--exclude-newer` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="3784b-153">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="3784b-154">Veya, son değişiklik zamanını hello aynı ya da hello hedef dosyanın daha eski olan tooexclude BLOB'ları istiyorsanız hello ekleyin `--exclude-older` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="3784b-154">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="3784b-155">BLOB: karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="3784b-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="3784b-156">Tek dosya karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="3784b-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3784b-157">Merhaba belirtilen hedef kapsayıcı mevcut değilse, AzCopy oluşturur ve karşıya dosya içine hello.</span><span class="sxs-lookup"><span data-stu-id="3784b-157">If hello specified destination container does not exist, AzCopy creates it and uploads hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="3784b-158">Tek dosya toovirtual dizin karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="3784b-158">Upload single file toovirtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3784b-159">Merhaba belirtilen sanal dizin yok, AzCopy hello dosya tooinclude hello sanal dizinde hello blob adı yükler (*örneğin*, `vd/abc.txt` yukarıdaki hello örnekteki).</span><span class="sxs-lookup"><span data-stu-id="3784b-159">If hello specified virtual directory does not exist, AzCopy uploads hello file tooinclude hello virtual directory in hello blob name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="3784b-160">Tüm dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="3784b-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="3784b-161">Seçeneğini belirterek `--recursive` hello yüklemeleri Merhaba içeriğine belirtilen dizin tooBlob depolama yinelemeli olarak tüm alt klasörleri ve bunların dosyaları da karşıya anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3784b-161">Specifying option `--recursive` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="3784b-162">Örneği için hello aşağıdaki varsayın dosyaları klasöründe bulunan `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="3784b-162">For instance, assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="3784b-163">Merhaba karşıya yükleme işleminden sonra aşağıdaki dosyaları hello hello kapsayıcı içerir:</span><span class="sxs-lookup"><span data-stu-id="3784b-163">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="3784b-164">Seçenek'ne zaman hello `--recursive` hello aşağıdaki üç dosyayı karşıya yalnızca, belirtilmedi:</span><span class="sxs-lookup"><span data-stu-id="3784b-164">When hello option `--recursive` is not specified, only hello following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="3784b-165">Belirtilen desenle eşleşen dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="3784b-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="3784b-166">Merhaba aşağıdaki varsayın dosyaları klasöründe bulunan `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="3784b-166">Assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="3784b-167">Merhaba karşıya yükleme işleminden sonra aşağıdaki dosyaları hello hello kapsayıcı içerir:</span><span class="sxs-lookup"><span data-stu-id="3784b-167">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="3784b-168">Seçenek'ne zaman hello `--recursive` belirtilmezse, AzCopy atlar alt dizinlerde olan dosyaları:</span><span class="sxs-lookup"><span data-stu-id="3784b-168">When hello option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="3784b-169">Hedef BLOB Hello MIME içerik türünü belirtin</span><span class="sxs-lookup"><span data-stu-id="3784b-169">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="3784b-170">Çok hedef blob hello içerik türü varsayılan olarak, AzCopy ayarlar`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="3784b-170">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="3784b-171">Ancak, açıkça hello seçeneği aracılığıyla hello içerik türünü belirtebilirsiniz `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="3784b-171">However, you can explicitly specify hello content type via hello option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="3784b-172">Bu sözdiziminin hello içerik türü için tüm BLOB'ları bir karşıya yükleme işleminde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3784b-172">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="3784b-173">Merhaba, seçenek `--set-content-type` AzCopy her bir dosya veya blob ayarlar sonra bir değer belirtilirse kullanıcının içerik türünü according tooits dosya uzantısı.</span><span class="sxs-lookup"><span data-stu-id="3784b-173">If hello option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according tooits file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="3784b-174">BLOB: kopyalama</span><span class="sxs-lookup"><span data-stu-id="3784b-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="3784b-175">Depolama hesabı içinde tek blob kopyalama</span><span class="sxs-lookup"><span data-stu-id="3784b-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3784b-176">Bir blob--eşitleme kopyalama seçeneği olmadan kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3784b-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="3784b-177">Tek blob depolama hesapları arasında kopyalama</span><span class="sxs-lookup"><span data-stu-id="3784b-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="3784b-178">Bir blob--eşitleme kopyalama seçeneği olmadan kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3784b-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="3784b-179">İkincil bölge tooprimary bölgesinden tek blob kopyalama</span><span class="sxs-lookup"><span data-stu-id="3784b-179">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="3784b-180">Okuma erişimli coğrafi olarak yedekli depolama etkin olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3784b-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="3784b-181">Depolama hesapları arasında tek blob ve onun anlık görüntüleri kopyalama</span><span class="sxs-lookup"><span data-stu-id="3784b-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="3784b-182">Hello kopyalama işleminden sonra hello hedef kapsayıcı hello blob ve onun anlık görüntülerini içerir.</span><span class="sxs-lookup"><span data-stu-id="3784b-182">After hello copy operation, hello target container includes hello blob and its snapshots.</span></span> <span data-ttu-id="3784b-183">Merhaba kapsayıcı hello aşağıdakileri içeren blob ve onun anlık görüntüler:</span><span class="sxs-lookup"><span data-stu-id="3784b-183">hello container includes hello following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="3784b-184">Zaman uyumlu olarak depolama hesapları arasında BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="3784b-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="3784b-185">AzCopy varsayılan olarak, iki depolama uç noktaları arasında verileri zaman uyumsuz olarak kopyalar.</span><span class="sxs-lookup"><span data-stu-id="3784b-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="3784b-186">Bu nedenle, hiçbir SLA ne kadar hızlı blob bakımından sahip yedek bant genişliğini kapasite kullanarak hello arka planda hello kopyalama işlemi çalıştırır kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="3784b-186">Therefore, hello copy operation runs in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="3784b-187">Merhaba `--sync-copy` seçeneği sağlar hello kopyalama işlemi tutarlı hızı alır.</span><span class="sxs-lookup"><span data-stu-id="3784b-187">hello `--sync-copy` option ensures that hello copy operation gets consistent speed.</span></span> <span data-ttu-id="3784b-188">AzCopy hello BLOB'lar yükleyerek hello zaman uyumlu kopyası gerçekleştirir toocopy hello öğesinden belirtilen kaynak toolocal bellek ve ardından toohello Blob Depolama Hedef karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="3784b-188">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="3784b-189">`--sync-copy`Ek çıkış karşılaştırıldığında maliyet tooasynchronous kopya oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="3784b-189">`--sync-copy` might generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="3784b-190">Önerilen yaklaşımı hello toouse hello olan Azure VM'deki, bu seçenek olan aynı bölgede kaynak depolama hesabı tooavoid çıkışı maliyeti.</span><span class="sxs-lookup"><span data-stu-id="3784b-190">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="3784b-191">Dosya: karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="3784b-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="3784b-192">Tek dosya indirme</span><span class="sxs-lookup"><span data-stu-id="3784b-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3784b-193">Merhaba kaynağıdır Azure dosya paylaşımının, sonra da hello tam dosya adı belirtmelisiniz belirtilmişse (*örneğin* `abc.txt`) toodownload tek bir dosya veya seçeneğini belirtin `--recursive` toodownload tüm dosyaları hello paylaşımı yinelemeli olarak.</span><span class="sxs-lookup"><span data-stu-id="3784b-193">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `--recursive` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="3784b-194">Bir dosya düzeni ve seçenek toospecify çalışırken `--recursive` birlikte hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="3784b-194">Attempting toospecify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="3784b-195">Tüm dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="3784b-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="3784b-196">Boş klasörleri indirilmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3784b-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="3784b-197">Dosya: karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="3784b-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="3784b-198">Tek dosya karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="3784b-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="3784b-199">Tüm dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="3784b-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="3784b-200">Boş klasörleri değil karşıya unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3784b-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="3784b-201">Belirtilen desenle eşleşen dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="3784b-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="3784b-202">Dosya: kopyalama</span><span class="sxs-lookup"><span data-stu-id="3784b-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="3784b-203">Dosya paylaşımlarında kopyalayın</span><span class="sxs-lookup"><span data-stu-id="3784b-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="3784b-204">Dosya paylaşımlarında bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3784b-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="3784b-205">Dosya Paylaşımı tooblob kopyalayın</span><span class="sxs-lookup"><span data-stu-id="3784b-205">Copy from file share tooblob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="3784b-206">Dosya Paylaşımı tooblob bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3784b-206">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="3784b-207">BLOB toofile paylaşımından kopyalayın</span><span class="sxs-lookup"><span data-stu-id="3784b-207">Copy from blob toofile share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="3784b-208">Blob toofile paylaşımından bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3784b-208">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="3784b-209">Zaman uyumlu olarak dosyaları kopyalayın</span><span class="sxs-lookup"><span data-stu-id="3784b-209">Synchronously copy files</span></span>
<span data-ttu-id="3784b-210">Merhaba belirtebilirsiniz `--sync-copy` toocopy veri dosya depolama tooFile depolama, File Storage tooBlob depolama ve Blob Depolama tooFile depolama zaman uyumlu olarak seçeneği.</span><span class="sxs-lookup"><span data-stu-id="3784b-210">You can specify hello `--sync-copy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously.</span></span> <span data-ttu-id="3784b-211">AzCopy bu işlemi hello kaynak veri toolocal bellek indiriliyor ve toodestination karşıya yükleme çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="3784b-211">AzCopy runs this operation by downloading hello source data toolocal memory, and then uploading it toodestination.</span></span> <span data-ttu-id="3784b-212">Bu durumda, standart çıkış maliyet geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="3784b-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="3784b-213">Dosya depolama tooBlob depolama kopyalarken hello varsayılan blob türü blok blobu, kullanıcı seçeneği belirtebilirsiniz `/BlobType:page` toochange hello hedef blob türü.</span><span class="sxs-lookup"><span data-stu-id="3784b-213">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="3784b-214">Unutmayın `--sync-copy` karşılaştırma tooasynchronous kopyalama maliyet ek çıkış oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="3784b-214">Note that `--sync-copy` might generate additional egress cost comparing tooasynchronous copy.</span></span> <span data-ttu-id="3784b-215">Önerilen yaklaşımı hello toouse hello olan Azure VM'deki, bu seçenek olan aynı bölgede kaynak depolama hesabı tooavoid çıkışı maliyeti.</span><span class="sxs-lookup"><span data-stu-id="3784b-215">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="3784b-216">Diğer AzCopy özellikleri</span><span class="sxs-lookup"><span data-stu-id="3784b-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="3784b-217">Merhaba hedefte mevcut olmayan veri Kopyala</span><span class="sxs-lookup"><span data-stu-id="3784b-217">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="3784b-218">Merhaba `--exclude-older` ve `--exclude-newer` parametreler, sırasıyla kopyalanmasını tooexclude daha eski veya yeni kaynak kaynakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="3784b-218">hello `--exclude-older` and `--exclude-newer` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="3784b-219">Merhaba hedef yoksa toocopy kaynak kaynakları yalnızca istiyorsanız, her iki parametre hello AzCopy komut belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3784b-219">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a><span data-ttu-id="3784b-220">Bir yapılandırma dosyası toospecify komut satırı parametreleri kullanma</span><span class="sxs-lookup"><span data-stu-id="3784b-220">Use a configuration file toospecify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="3784b-221">AzCopy komut satırı parametreleri herhangi bir yapılandırma dosyası içerebilir.</span><span class="sxs-lookup"><span data-stu-id="3784b-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="3784b-222">Merhaba komut satırında bir hello içeriğiyle doğrudan değiştirme hello dosyasının gerçekleştirme belirtilmiş sanki AzCopy işlemleri hello dosyasındaki parametreleri hello.</span><span class="sxs-lookup"><span data-stu-id="3784b-222">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="3784b-223">Adlı bir yapılandırma dosyası varsayın `copyoperation`, satırlardan hello içerir.</span><span class="sxs-lookup"><span data-stu-id="3784b-223">Assume a configuration file named `copyoperation`, that contains hello following lines.</span></span> <span data-ttu-id="3784b-224">Tek bir satıra her AzCopy parametresi belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="3784b-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="3784b-225">veya satırları ayrı:</span><span class="sxs-lookup"><span data-stu-id="3784b-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="3784b-226">AzCopy, iki hattında hello parametre bölerseniz hello için aşağıda gösterildiği gibi başarısız `--source-key` parametre:</span><span class="sxs-lookup"><span data-stu-id="3784b-226">AzCopy fails if you split hello parameter across two lines, as shown here for hello `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="3784b-227">Paylaşılan erişim imzası (SAS) belirtin</span><span class="sxs-lookup"><span data-stu-id="3784b-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="3784b-228">Ayrıca, bir SAS hello kapsayıcı URI belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3784b-228">You can also specify a SAS on hello container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="3784b-229">AzCopy şu anda yalnızca hello desteklediğini unutmayın [hesap SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="3784b-229">Note that AzCopy currently only supports hello [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="3784b-230">Günlük dosyası klasörü</span><span class="sxs-lookup"><span data-stu-id="3784b-230">Journal file folder</span></span>
<span data-ttu-id="3784b-231">Bir komut tooAzCopy sorun her zaman hello varsayılan klasöründe bir günlük dosyası var olup var veya bu seçeneği belirtilen bir klasörde varolup denetler.</span><span class="sxs-lookup"><span data-stu-id="3784b-231">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="3784b-232">Her iki yerde Hello günlük dosyası mevcut değilse, AzCopy hello işlemi yeni olarak değerlendirir ve yeni bir günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3784b-232">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="3784b-233">Merhaba günlük dosyası mevcut değilse, AzCopy girdiğiniz hello komut satırı hello komut satırı hello günlük dosyasında eşleşip eşleşmediğini denetler.</span><span class="sxs-lookup"><span data-stu-id="3784b-233">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="3784b-234">Merhaba iki komut satırları eşleşirse, AzCopy hello tamamlanmamış işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="3784b-234">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="3784b-235">Bunlar eşleşmiyorsa AzCopy kullanıcı tooeither üzerine yaz hello günlük dosyası toostart yeni işlem ya da toocancel hello geçerli işlem ister.</span><span class="sxs-lookup"><span data-stu-id="3784b-235">If they do not match, AzCopy prompts user tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="3784b-236">Merhaba günlük dosyası için toouse hello varsayılan konum istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="3784b-236">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="3784b-237">Seçeneği unutursanız `--resume`, veya seçeneğini belirtin `--resume` hello klasör yolu, yukarıda gösterildiği gibi AzCopy hello günlük dosyası olan hello varsayılan konumda, oluşturur `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="3784b-237">If you omit option `--resume`, or specify option `--resume` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="3784b-238">Merhaba günlük dosyası zaten varsa, AzCopy hello günlük dosyasına dayalı hello işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="3784b-238">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="3784b-239">Toospecify hello günlük dosyası için özel bir konum istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="3784b-239">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="3784b-240">Bu örnek, zaten yoksa, hello günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3784b-240">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="3784b-241">Mevcut değilse, AzCopy hello günlük dosyasına dayalı hello işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="3784b-241">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="3784b-242">Tooresume AzCopy işlemi istiyorsanız yineleyin hello aynı komutu.</span><span class="sxs-lookup"><span data-stu-id="3784b-242">If you want tooresume an AzCopy operation, repeat hello same command.</span></span> <span data-ttu-id="3784b-243">AzCopy sonra Linux'ta onay ister:</span><span class="sxs-lookup"><span data-stu-id="3784b-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="3784b-244">Çıktı ayrıntılı günlükleri</span><span class="sxs-lookup"><span data-stu-id="3784b-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="3784b-245">Eşzamanlı operasyonlar toostart Hello sayısını belirtin</span><span class="sxs-lookup"><span data-stu-id="3784b-245">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="3784b-246">Seçenek `--parallel-level` eşzamanlı kopyalama işlemleri hello sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3784b-246">Option `--parallel-level` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="3784b-247">Varsayılan olarak, belirli bir sayıda eşzamanlı işlem tooincrease hello veri aktarımı işleme AzCopy başlatır.</span><span class="sxs-lookup"><span data-stu-id="3784b-247">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="3784b-248">eşzamanlı operasyonlar Hello sayısı eşittir sekiz katı hello elinizde işlemci sayısı.</span><span class="sxs-lookup"><span data-stu-id="3784b-248">hello number of concurrent operations is equal eight times hello number of processors you have.</span></span> <span data-ttu-id="3784b-249">Düşük bant genişlikli ağ üzerinden AzCopy çalıştırıyorsanız, daha düşük bir sayı için--kaynak rekabet tarafından nedeniyle paralel düzeyi tooavoid hatası belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3784b-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level tooavoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="3784b-250">tooview hello tam listesi 'azcopy--Yardım' AzCopy parametrelerinin denetleyin menüsü.</span><span class="sxs-lookup"><span data-stu-id="3784b-250">tooview hello complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="3784b-251">Bilinen sorunlar ve en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="3784b-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-hello-system"></a><span data-ttu-id="3784b-252">Hata: .NET Core hello sistemde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="3784b-252">Error: .NET Core is not found in hello system.</span></span>
<span data-ttu-id="3784b-253">.NET Core hello sistemde yüklü olmadığını belirten bir hatayla karşılaşırsanız, yol toohello .NET Core ikili hello `dotnet` eksik olabilir.</span><span class="sxs-lookup"><span data-stu-id="3784b-253">If you encounter an error stating that .NET Core is not installed in hello system, hello PATH toohello .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="3784b-254">İçinde bu sorunu tooaddress sipariş, hello .NET Core ikili hello sistemde bulunamadı:</span><span class="sxs-lookup"><span data-stu-id="3784b-254">In order tooaddress this issue, find hello .NET Core binary in hello system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="3784b-255">Bu, hello yolu toohello dotnet ikili döndürür.</span><span class="sxs-lookup"><span data-stu-id="3784b-255">This returns hello path toohello dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="3784b-256">Şimdi bu yolu toohello PATH değişkeni ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3784b-256">Now add this path toohello PATH variable.</span></span> <span data-ttu-id="3784b-257">Sudo için secure_path toocontain hello yolu toohello dotnet ikili düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="3784b-257">For sudo, edit secure_path toocontain hello path toohello dotnet binary:</span></span>
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

<span data-ttu-id="3784b-258">Bu örnekte, secure_path değişken olarak okur:</span><span class="sxs-lookup"><span data-stu-id="3784b-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="3784b-259">Merhaba geçerli kullanıcı için.bash_profile/.profile tooinclude hello yolu toohello dotnet PATH değişkeni ikili düzenleme</span><span class="sxs-lookup"><span data-stu-id="3784b-259">For hello current user, edit .bash_profile/.profile tooinclude hello path toohello dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

<span data-ttu-id="3784b-260">.NET Core şimdi yolunda olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="3784b-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="3784b-261">AzCopy yükleme hatası</span><span class="sxs-lookup"><span data-stu-id="3784b-261">Error Installing AzCopy</span></span>
<span data-ttu-id="3784b-262">AzCopy yükleme ile ilgili sorunlarla karşılaşırsanız, AzCopy hello hello bash betik kullanarak ayıklanan toorun deneyebilirsiniz `azcopy` klasör.</span><span class="sxs-lookup"><span data-stu-id="3784b-262">If you encounter issues with AzCopy installation, you may try toorun AzCopy using hello bash script in hello extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="3784b-263">Veri kopyalama sırasında sınırı eşzamanlı yazma</span><span class="sxs-lookup"><span data-stu-id="3784b-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="3784b-264">BLOB veya AzCopy dosyalarıyla kopyaladığınızda, bunu kopyalamaya çalışırken, başka bir uygulama hello veri değiştirme göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="3784b-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="3784b-265">Mümkünse, Kopyalamakta olduğunuz hello veri hello kopyalama işlemi sırasında değiştirilmeyen emin olun.</span><span class="sxs-lookup"><span data-stu-id="3784b-265">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="3784b-266">Örneğin, bir Azure sanal makine ile ilişkili bir VHD'nin kopyalarken, başka bir uygulama şu anda toohello VHD yazıyorsanız emin olun.</span><span class="sxs-lookup"><span data-stu-id="3784b-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="3784b-267">Bir en iyi yolu toodo bu hello kaynak toobe kiralama tarafından kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="3784b-267">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="3784b-268">Alternatif olarak, bir anlık görüntüsünü hello VHD ilk oluşturun ve sonra hello anlık görüntüsü kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="3784b-268">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="3784b-269">Kopyalanan sonra hello süresi hello işi tarafından bittikten unutmayın ancak diğer uygulamaların tooblobs veya dosyaları yazma önleyemez, hello kopyalanan artık hello kaynak kaynaklarla tam eşlik kaynaklarınız olabilir.</span><span class="sxs-lookup"><span data-stu-id="3784b-269">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="3784b-270">Bir Azcopy'i örnek bir makinede çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3784b-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="3784b-271">AzCopy, makine kaynak tooaccelerate hello veri aktarımı tasarlanmış toomaximize hello kullanımı, bir makinede yalnızca bir AzCopy çalıştırır ve hello seçeneğini belirtin öneririz `--parallel-level` fazla eşzamanlı işlem gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="3784b-271">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="3784b-272">Daha fazla ayrıntı için yazın `AzCopy --help parallel-level` hello komut satırında.</span><span class="sxs-lookup"><span data-stu-id="3784b-272">For more details, type `AzCopy --help parallel-level` at hello command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3784b-273">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3784b-273">Next steps</span></span>
<span data-ttu-id="3784b-274">Azure Storage ve AzCopy hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="3784b-274">For more information about Azure Storage and AzCopy, see hello following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="3784b-275">Azure Storage belgeleri:</span><span class="sxs-lookup"><span data-stu-id="3784b-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="3784b-276">Giriş tooAzure depolama</span><span class="sxs-lookup"><span data-stu-id="3784b-276">Introduction tooAzure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="3784b-277">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3784b-277">Create a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="3784b-278">BLOB Depolama Gezgini ile yönetme</span><span class="sxs-lookup"><span data-stu-id="3784b-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="3784b-279">Hello Azure CLI 2.0 Azure Storage ile kullanma</span><span class="sxs-lookup"><span data-stu-id="3784b-279">Using hello Azure CLI 2.0 with Azure Storage</span></span>](../storage-azure-cli.md)
* [<span data-ttu-id="3784b-280">Nasıl toouse Blob depolama alanından C++</span><span class="sxs-lookup"><span data-stu-id="3784b-280">How toouse Blob storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="3784b-281">Nasıl toouse Java'dan Blob storage</span><span class="sxs-lookup"><span data-stu-id="3784b-281">How toouse Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="3784b-282">Nasıl toouse node.js'den Blob storage</span><span class="sxs-lookup"><span data-stu-id="3784b-282">How toouse Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="3784b-283">Nasıl toouse python'dan Blob storage</span><span class="sxs-lookup"><span data-stu-id="3784b-283">How toouse Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="3784b-284">Azure depolama blog gönderileri:</span><span class="sxs-lookup"><span data-stu-id="3784b-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="3784b-285">AzCopy Linux preview'daki tanışın</span><span class="sxs-lookup"><span data-stu-id="3784b-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="3784b-286">Azure Storage veri hareketi kitaplığı Önizleme Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="3784b-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="3784b-287">AzCopy: zaman uyumlu kopyası ve özelleştirilmiş içerik türü tanışın</span><span class="sxs-lookup"><span data-stu-id="3784b-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="3784b-288">AzCopy: Genel kullanılabilirlik, AzCopy 3.0 artı AzCopy 4.0 Önizleme sürümü tablo ve dosya desteği ile tanışın</span><span class="sxs-lookup"><span data-stu-id="3784b-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="3784b-289">AzCopy: Büyük ölçekli kopyalama senaryoları için en iyi duruma getirilmiş</span><span class="sxs-lookup"><span data-stu-id="3784b-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="3784b-290">AzCopy: Coğrafi olarak yedekli depolamaya okuma erişimi desteği</span><span class="sxs-lookup"><span data-stu-id="3784b-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="3784b-291">AzCopy: yeniden başlatılabilir modu ve SAS belirteci ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="3784b-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="3784b-292">AzCopy: arası hesap kopyalama Blob kullanma</span><span class="sxs-lookup"><span data-stu-id="3784b-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="3784b-293">AzCopy: Azure BLOB'ları karşıya yükleme ve indirme dosyaları</span><span class="sxs-lookup"><span data-stu-id="3784b-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

