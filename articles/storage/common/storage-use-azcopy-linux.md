---
title: "Kopyalama veya Linux'ta Azure Storage ile AzCopy için veri taşıma | Microsoft Docs"
description: "AzCopy Linux yardımcı taşımak veya için veya blob ve dosya içeriği veri kopyalamak için kullanın. Verileri Azure depolama birimine yerel dosyalarından kopyalamak veya içinde veya depolama hesapları arasında veri kopyalama. Kolayca verilerinizi Azure depolama alanına geçiş."
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
ms.openlocfilehash: 441227d84b9c1ec721ae36fdc423ba797654f128
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="32b20-105">Linux'ta AzCopy ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="32b20-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="32b20-106">Linux üzerinde AzCopy en uygun performans ile basit komutları kullanarak Microsoft Azure Blob ve dosya depolama gelen ve giden veri kopyalamak için tasarlanmış bir komut satırı yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="32b20-106">AzCopy on Linux is a command-line utility designed for copying data to and from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="32b20-107">Verileri bir nesneden diğerine depolama hesabınızda veya depolama hesapları arasında kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32b20-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="32b20-108">İndirebilirsiniz AzCopy iki sürümü vardır.</span><span class="sxs-lookup"><span data-stu-id="32b20-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="32b20-109">Linux üzerinde AzCopy .NET Core POSIX stili komut satırı seçenekleri sunan Linux platformlar hedefler Framework ile yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="32b20-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="32b20-110">[AzCopy Windows](../storage-use-azcopy.md) .NET Framework ile oluşturulan ve Windows stili komut satırı seçenekleri sunar.</span><span class="sxs-lookup"><span data-stu-id="32b20-110">[AzCopy on Windows](../storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="32b20-111">Bu makalede, AzCopy Linux üzerinde yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="32b20-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="32b20-112">AzCopy yükleyip</span><span class="sxs-lookup"><span data-stu-id="32b20-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="32b20-113">Linux üzerinde yükleme</span><span class="sxs-lookup"><span data-stu-id="32b20-113">Installation on Linux</span></span>

<span data-ttu-id="32b20-114">AzCopy Linux'ta platformunda .NET Core framework gerektirir.</span><span class="sxs-lookup"><span data-stu-id="32b20-114">AzCopy on Linux requires .NET Core framework on the platform.</span></span> <span data-ttu-id="32b20-115">Yükleme yönergelerine bakın [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) sayfası.</span><span class="sxs-lookup"><span data-stu-id="32b20-115">See the installation instructions on the [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="32b20-116">Örnek olarak, .NET Core üzerinde Ubuntu 16.10 şimdi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="32b20-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="32b20-117">En son kurulum kılavuzunu için ziyaret [.NET Core Linux'ta](https://www.microsoft.com/net/core#linuxubuntu) yükleme sayfası.</span><span class="sxs-lookup"><span data-stu-id="32b20-117">For the latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="32b20-118">.NET Core yüklendiğinde, indirin ve AzCopy yükleyin.</span><span class="sxs-lookup"><span data-stu-id="32b20-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="32b20-119">AzCopy Linux'ta yüklendikten sonra ayıklanan dosyaları kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32b20-119">You can remove the extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="32b20-120">Alternatif olarak süper kullanıcı ayrıcalıkları yoksa Kabuk betiği 'azcopy' ayıklanan klasöründe kullanarak AzCopy de çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32b20-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using the shell script 'azcopy' in the extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="32b20-121">Ubuntu alternatif yükleme</span><span class="sxs-lookup"><span data-stu-id="32b20-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="32b20-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="32b20-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="32b20-123">.Net için apt kaynağı Ekle Çekirdek:</span><span class="sxs-lookup"><span data-stu-id="32b20-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="32b20-124">Microsoft Linux ürün depo apt kaynağı ekleyin ve AzCopy yükleyin:</span><span class="sxs-lookup"><span data-stu-id="32b20-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="32b20-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="32b20-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="32b20-126">.Net için apt kaynağı Ekle Çekirdek:</span><span class="sxs-lookup"><span data-stu-id="32b20-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="32b20-127">Microsoft Linux ürün depo apt kaynağı ekleyin ve AzCopy yükleyin:</span><span class="sxs-lookup"><span data-stu-id="32b20-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="32b20-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="32b20-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="32b20-129">.Net için apt kaynağı Ekle Çekirdek:</span><span class="sxs-lookup"><span data-stu-id="32b20-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="32b20-130">Microsoft Linux ürün depo apt kaynağı ekleyin ve AzCopy yükleyin:</span><span class="sxs-lookup"><span data-stu-id="32b20-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="32b20-131">İlk AzCopy komut yazma</span><span class="sxs-lookup"><span data-stu-id="32b20-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="32b20-132">AzCopy komutları temel sözdizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="32b20-132">The basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="32b20-133">Aşağıdaki örnekler verileri için ve Microsoft Azure BLOB'ları ve dosyalarından kopyalamak için çeşitli senaryolar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="32b20-133">The following examples demonstrate various scenarios for copying data to and from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="32b20-134">Başvurmak `azcopy --help` her örnekte kullanılan parametreleri ayrıntılı bir açıklaması için menüsü.</span><span class="sxs-lookup"><span data-stu-id="32b20-134">Refer to the `azcopy --help` menu for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="32b20-135">BLOB: karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="32b20-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="32b20-136">Tek blob indirin</span><span class="sxs-lookup"><span data-stu-id="32b20-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="32b20-137">Varsa klasörü `/mnt/myfiles` yok, AzCopy oluşturur ve indirir `abc.txt ` yeni klasöre.</span><span class="sxs-lookup"><span data-stu-id="32b20-137">If the folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="32b20-138">Tek blob ikincil bölge ' indirin</span><span class="sxs-lookup"><span data-stu-id="32b20-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="32b20-139">Okuma erişimli coğrafi olarak yedekli depolama etkin olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="32b20-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="32b20-140">Tüm BLOB'ları indirme</span><span class="sxs-lookup"><span data-stu-id="32b20-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="32b20-141">Aşağıdaki BLOB'ları belirtilen kapsayıcıda bulunan varsayın:</span><span class="sxs-lookup"><span data-stu-id="32b20-141">Assume the following blobs reside in the specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="32b20-142">Dizin yükleme işleminden sonra `/mnt/myfiles` aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="32b20-142">After the download operation, the directory `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="32b20-143">Seçeneği belirtmezseniz, `--recursive`, hiçbir blob indirilir.</span><span class="sxs-lookup"><span data-stu-id="32b20-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="32b20-144">BLOB'lar ile belirtilen bir önek indirin</span><span class="sxs-lookup"><span data-stu-id="32b20-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="32b20-145">Aşağıdaki BLOB'ları belirtilen kapsayıcıda bulunan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="32b20-145">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="32b20-146">Önek ile başlayan tüm BLOB'lar `a` indirilir.</span><span class="sxs-lookup"><span data-stu-id="32b20-146">All blobs beginning with the prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="32b20-147">Klasör yükleme işleminden sonra `/mnt/myfiles` aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="32b20-147">After the download operation, the folder `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="32b20-148">Önek blob adı ilk bölümü forms bir sanal dizin geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="32b20-148">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="32b20-149">Hiçbir blob indirilen şekilde yukarıda gösterilen örnekte, sanal dizin belirtilen bir önek eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="32b20-149">In the example shown above, the virtual directory does not match the specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="32b20-150">Ayrıca, varsa seçeneği `--recursive` belirtilmezse, AzCopy BLOB indirmek değil.</span><span class="sxs-lookup"><span data-stu-id="32b20-150">In addition, if the option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="32b20-151">Kaynak BLOB olarak aynı olmalıdır dışarı aktarılan dosyaların son değiştirme zamanı ayarlama</span><span class="sxs-lookup"><span data-stu-id="32b20-151">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="32b20-152">Son değiştiren bunların zamana dayalı indirme işlemi de BLOB'lar hariç tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32b20-152">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="32b20-153">Son değişiklik zamanı BLOB'lar dışlamak istiyorsanız, örneğin, aynı veya daha yeni hedef dosya eklemektir `--exclude-newer` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="32b20-153">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="32b20-154">Ya da son değişiklik zamanı BLOB'lar hariç tutmak istediğiniz ise, aynı veya daha eski hedef dosya ekleme `--exclude-older` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="32b20-154">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="32b20-155">BLOB: karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="32b20-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="32b20-156">Tek dosya karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="32b20-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="32b20-157">Belirtilen hedef kapsayıcı mevcut değilse, AzCopy oluşturur ve dosyayı içine yükler.</span><span class="sxs-lookup"><span data-stu-id="32b20-157">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="32b20-158">Sanal dizin için tek dosya karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="32b20-158">Upload single file to virtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="32b20-159">Belirtilen sanal dizin yoksa, AzCopy sanal dizin içinde blob adını içerecek şekilde dosyayı yükler (*örneğin*, `vd/abc.txt` Yukarıdaki örnekteki).</span><span class="sxs-lookup"><span data-stu-id="32b20-159">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in the blob name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="32b20-160">Tüm dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="32b20-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="32b20-161">Seçeneğini belirterek `--recursive` belirtilen dizin içeriğini tüm alt klasörleri ve bunların dosyaları da karşıya anlamı Blob Depolama yinelemeli olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="32b20-161">Specifying option `--recursive` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="32b20-162">Örneğin, aşağıdaki dosyaları klasöründe bulunan varsayın `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="32b20-162">For instance, assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="32b20-163">Karşıya yükleme işleminden sonra kapsayıcı aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="32b20-163">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="32b20-164">Zaman seçeneği `--recursive` belirtilmezse, yalnızca aşağıdaki üç dosyalar yüklenir:</span><span class="sxs-lookup"><span data-stu-id="32b20-164">When the option `--recursive` is not specified, only the following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="32b20-165">Belirtilen desenle eşleşen dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="32b20-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="32b20-166">Aşağıdaki dosyaları klasöründe bulunan varsayın `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="32b20-166">Assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="32b20-167">Karşıya yükleme işleminden sonra kapsayıcı aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="32b20-167">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="32b20-168">Zaman seçeneği `--recursive` belirtilmezse, AzCopy atlar alt dizinlerde olan dosyaları:</span><span class="sxs-lookup"><span data-stu-id="32b20-168">When the option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="32b20-169">Hedef blob MIME içerik türünü belirtin</span><span class="sxs-lookup"><span data-stu-id="32b20-169">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="32b20-170">Varsayılan olarak, içerik türü için bir hedef blob AzCopy ayarlar `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="32b20-170">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="32b20-171">Ancak, açıkça seçeneği aracılığıyla içerik türünü belirtebilirsiniz `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="32b20-171">However, you can explicitly specify the content type via the option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="32b20-172">Bu sözdiziminin bir karşıya yükleme işleminde tüm BLOB'lar için içerik türünü ayarlar.</span><span class="sxs-lookup"><span data-stu-id="32b20-172">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="32b20-173">Varsa seçeneği `--set-content-type` AzCopy her bir blob veya dosyanın içerik türü dosya uzantısını göre ayarlar daha sonra bir değer belirtilirse.</span><span class="sxs-lookup"><span data-stu-id="32b20-173">If the option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="32b20-174">BLOB: kopyalama</span><span class="sxs-lookup"><span data-stu-id="32b20-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="32b20-175">Depolama hesabı içinde tek blob kopyalama</span><span class="sxs-lookup"><span data-stu-id="32b20-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="32b20-176">Bir blob--eşitleme kopyalama seçeneği olmadan kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="32b20-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="32b20-177">Tek blob depolama hesapları arasında kopyalama</span><span class="sxs-lookup"><span data-stu-id="32b20-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="32b20-178">Bir blob--eşitleme kopyalama seçeneği olmadan kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="32b20-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="32b20-179">Birincil bölge ikincil bölge'den blob'a tek kopyalama</span><span class="sxs-lookup"><span data-stu-id="32b20-179">Copy single blob from secondary region to primary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="32b20-180">Okuma erişimli coğrafi olarak yedekli depolama etkin olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="32b20-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="32b20-181">Depolama hesapları arasında tek blob ve onun anlık görüntüleri kopyalama</span><span class="sxs-lookup"><span data-stu-id="32b20-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="32b20-182">Kopyalama işleminden sonra hedef kapsayıcı blob ve onun anlık görüntülerini içerir.</span><span class="sxs-lookup"><span data-stu-id="32b20-182">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="32b20-183">Kapsayıcı aşağıdaki blob ve onun anlık görüntülerini içerir:</span><span class="sxs-lookup"><span data-stu-id="32b20-183">The container includes the following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="32b20-184">Zaman uyumlu olarak depolama hesapları arasında BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="32b20-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="32b20-185">AzCopy varsayılan olarak, iki depolama uç noktaları arasında verileri zaman uyumsuz olarak kopyalar.</span><span class="sxs-lookup"><span data-stu-id="32b20-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="32b20-186">Bu nedenle, hiçbir SLA ne kadar hızlı blob bakımından sahip yedek bant genişliğini kapasite kullanarak arka plan kopyalama işlemi çalıştırmalarında kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="32b20-186">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="32b20-187">`--sync-copy` Seçeneği sağlar kopyalama işlemi tutarlı hızı alır.</span><span class="sxs-lookup"><span data-stu-id="32b20-187">The `--sync-copy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="32b20-188">AzCopy zaman uyumlu kopyası yerel bellek için belirtilen kaynak kopyalamak için BLOB'ları karşıdan yükleyip ardından Blob Depolama hedefe karşıya yükleme gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="32b20-188">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="32b20-189">`--sync-copy`zaman uyumsuz kopyaya karşılaştırıldığında ek çıkışı maliyeti oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="32b20-189">`--sync-copy` might generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="32b20-190">Çıkış maliyet önlemek için kaynak depolama hesabınız ile aynı bölgede olan Azure VM'deki, bu seçeneği kullanmak için önerilen yaklaşımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="32b20-190">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="32b20-191">Dosya: karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="32b20-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="32b20-192">Tek dosya indirme</span><span class="sxs-lookup"><span data-stu-id="32b20-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="32b20-193">Belirtilen kaynak bir Azure dosya paylaşımıdır sonra ya da tam dosya adını belirtmeniz gerekir (*örneğin* `abc.txt`) tek bir dosya indirme veya seçenek belirtmek için `--recursive` paylaşımı yinelemeli olarak tüm dosyaları indirmek için.</span><span class="sxs-lookup"><span data-stu-id="32b20-193">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `--recursive` to download all files in the share recursively.</span></span> <span data-ttu-id="32b20-194">Bir dosya düzeni ve seçenek belirtmek çalışırken `--recursive` birlikte hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="32b20-194">Attempting to specify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="32b20-195">Tüm dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="32b20-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="32b20-196">Boş klasörleri indirilmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="32b20-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="32b20-197">Dosya: karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="32b20-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="32b20-198">Tek dosya karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="32b20-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="32b20-199">Tüm dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="32b20-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="32b20-200">Boş klasörleri değil karşıya unutmayın.</span><span class="sxs-lookup"><span data-stu-id="32b20-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="32b20-201">Belirtilen desenle eşleşen dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="32b20-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="32b20-202">Dosya: kopyalama</span><span class="sxs-lookup"><span data-stu-id="32b20-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="32b20-203">Dosya paylaşımlarında kopyalayın</span><span class="sxs-lookup"><span data-stu-id="32b20-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="32b20-204">Dosya paylaşımlarında bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="32b20-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="32b20-205">BLOB dosya paylaşımından kopyalayın</span><span class="sxs-lookup"><span data-stu-id="32b20-205">Copy from file share to blob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="32b20-206">Dosya blob öğesine dosya paylaşımından kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="32b20-206">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="32b20-207">BLOB üzerinden dosya paylaşımına kopyalayın</span><span class="sxs-lookup"><span data-stu-id="32b20-207">Copy from blob to file share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="32b20-208">Dosya Paylaşımı için blobundan bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="32b20-208">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="32b20-209">Zaman uyumlu olarak dosyaları kopyalayın</span><span class="sxs-lookup"><span data-stu-id="32b20-209">Synchronously copy files</span></span>
<span data-ttu-id="32b20-210">Belirleyebileceğiniz `--sync-copy` veri dosya depolama biriminden dosya depolama için dosya depolama Blob depolama alanına ve Blob depolama biriminden dosya depolama alanına eşzamanlı olarak kopyalamak için seçeneği.</span><span class="sxs-lookup"><span data-stu-id="32b20-210">You can specify the `--sync-copy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously.</span></span> <span data-ttu-id="32b20-211">AzCopy bu işlem için yerel bellek veri kaynağını indirme ve hedef için karşıya yükleme olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="32b20-211">AzCopy runs this operation by downloading the source data to local memory, and then uploading it to destination.</span></span> <span data-ttu-id="32b20-212">Bu durumda, standart çıkış maliyet geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="32b20-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="32b20-213">Dosya depolama biriminden Blob depolama alanına kopyalama işlemi sırasında varsayılan blob türü blok blobu, kullanıcı seçeneği belirtebilirsiniz `/BlobType:page` hedef blob türünü değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="32b20-213">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="32b20-214">Unutmayın `--sync-copy` zaman uyumsuz kopyaya karşılaştırma maliyet ek çıkış oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="32b20-214">Note that `--sync-copy` might generate additional egress cost comparing to asynchronous copy.</span></span> <span data-ttu-id="32b20-215">Çıkış maliyet önlemek için kaynak depolama hesabınız ile aynı bölgede olan Azure VM'deki, bu seçeneği kullanmak için önerilen yaklaşımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="32b20-215">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="32b20-216">Diğer AzCopy özellikleri</span><span class="sxs-lookup"><span data-stu-id="32b20-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="32b20-217">Hedefte mevcut olmayan veri Kopyala</span><span class="sxs-lookup"><span data-stu-id="32b20-217">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="32b20-218">`--exclude-older` Ve `--exclude-newer` parametreleri, sırasıyla kopyalanmasını daha eski veya yeni kaynak kaynakları hariç tut izin verir.</span><span class="sxs-lookup"><span data-stu-id="32b20-218">The `--exclude-older` and `--exclude-newer` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="32b20-219">Yalnızca hedef yoksa kaynak kaynakları kopyalamak isterseniz, AzCopy komut parametrelerinin her ikisini de belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="32b20-219">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-to-specify-command-line-parameters"></a><span data-ttu-id="32b20-220">Komut satırı parametrelerini belirtmek için bir yapılandırma dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="32b20-220">Use a configuration file to specify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="32b20-221">AzCopy komut satırı parametreleri herhangi bir yapılandırma dosyası içerebilir.</span><span class="sxs-lookup"><span data-stu-id="32b20-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="32b20-222">Komut satırında belirtilmiş gibi AzCopy dosyasının içeriğiyle doğrudan bir değiştirme gerçekleştirme dosyasındaki parametreleri işler.</span><span class="sxs-lookup"><span data-stu-id="32b20-222">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="32b20-223">Adlı bir yapılandırma dosyası varsayın `copyoperation`, aşağıdaki satırları içeren.</span><span class="sxs-lookup"><span data-stu-id="32b20-223">Assume a configuration file named `copyoperation`, that contains the following lines.</span></span> <span data-ttu-id="32b20-224">Tek bir satıra her AzCopy parametresi belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="32b20-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="32b20-225">veya satırları ayrı:</span><span class="sxs-lookup"><span data-stu-id="32b20-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="32b20-226">AzCopy bozulursa parametresi iki satır arasında bölmek için aşağıda gösterildiği gibi `--source-key` parametre:</span><span class="sxs-lookup"><span data-stu-id="32b20-226">AzCopy fails if you split the parameter across two lines, as shown here for the `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="32b20-227">Paylaşılan erişim imzası (SAS) belirtin</span><span class="sxs-lookup"><span data-stu-id="32b20-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="32b20-228">Ayrıca, bir SAS kapsayıcısında URI belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="32b20-228">You can also specify a SAS on the container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="32b20-229">AzCopy şu anda yalnızca destekler Not [hesap SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="32b20-229">Note that AzCopy currently only supports the [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="32b20-230">Günlük dosyası klasörü</span><span class="sxs-lookup"><span data-stu-id="32b20-230">Journal file folder</span></span>
<span data-ttu-id="32b20-231">AzCopy için bir komut sorun her zaman varsayılan klasöründe bir günlük dosyası var olup var veya bu seçeneği belirtilen bir klasörde varolup denetler.</span><span class="sxs-lookup"><span data-stu-id="32b20-231">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="32b20-232">Günlük dosyası her iki yerde mevcut değilse, AzCopy işlemi yeni olarak değerlendirir ve yeni bir günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="32b20-232">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="32b20-233">Günlük dosyası mevcut değilse, AzCopy girdiğiniz komut satırı günlük dosyası komut satırında eşleşip eşleşmediğini denetler.</span><span class="sxs-lookup"><span data-stu-id="32b20-233">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="32b20-234">İki komut satırları eşleşirse, AzCopy tamamlanmamış işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="32b20-234">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="32b20-235">Bunlar eşleşmiyorsa AzCopy kullanıcı ya da yeni bir işlemi başlatmak için ya da geçerli işlemi iptal etmek için günlük dosyasının üzerine yazmak ister.</span><span class="sxs-lookup"><span data-stu-id="32b20-235">If they do not match, AzCopy prompts user to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="32b20-236">Varsayılan konumu için günlük dosyası kullanmak istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="32b20-236">If you want to use the default location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="32b20-237">Seçeneği unutursanız `--resume`, veya seçeneğini belirtin `--resume` klasör yolu, yukarıda gösterildiği gibi AzCopy günlük dosyası olan varsayılan konumda oluşturur `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="32b20-237">If you omit option `--resume`, or specify option `--resume` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="32b20-238">Günlük dosyası zaten varsa, AzCopy günlük dosyasına dayalı işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="32b20-238">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="32b20-239">Günlük dosyası için özel bir konum belirtmek istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="32b20-239">If you want to specify a custom location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="32b20-240">Zaten yoksa, bu örnek günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="32b20-240">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="32b20-241">Mevcut değilse, AzCopy günlük dosyasına dayalı işlemi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="32b20-241">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="32b20-242">AzCopy çalışmaya devam etmesini istiyorsanız, aynı komutu yineleyin.</span><span class="sxs-lookup"><span data-stu-id="32b20-242">If you want to resume an AzCopy operation, repeat the same command.</span></span> <span data-ttu-id="32b20-243">AzCopy sonra Linux'ta onay ister:</span><span class="sxs-lookup"><span data-stu-id="32b20-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at the journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want to resume the operation? Choose Yes to resume, choose No to overwrite the journal to start a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="32b20-244">Çıktı ayrıntılı günlükleri</span><span class="sxs-lookup"><span data-stu-id="32b20-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="32b20-245">Başlatmak için eşzamanlı işlem sayısını belirtin</span><span class="sxs-lookup"><span data-stu-id="32b20-245">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="32b20-246">Seçenek `--parallel-level` eşzamanlı kopyalama işlemlerinin sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="32b20-246">Option `--parallel-level` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="32b20-247">Varsayılan olarak, belirli bir sayıda veri aktarımı verimliliğini artırmak için eşzamanlı işlem AzCopy başlatır.</span><span class="sxs-lookup"><span data-stu-id="32b20-247">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="32b20-248">Eşzamanlı işlem sayısını eşittir sekiz katı elinizde işlemci sayısı.</span><span class="sxs-lookup"><span data-stu-id="32b20-248">The number of concurrent operations is equal eight times the number of processors you have.</span></span> <span data-ttu-id="32b20-249">Düşük bant genişlikli ağ üzerinden AzCopy çalıştırıyorsanız, kaynak rekabet tarafından nedeniyle başarısız oldu önlemek için daha düşük bir sayı--paralel düzeyi için belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32b20-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level to avoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="32b20-250">AzCopy parametreler tam listesini görüntülemek için 'azcopy--Yardım' denetleyin menüsü.</span><span class="sxs-lookup"><span data-stu-id="32b20-250">To view the complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="32b20-251">Bilinen sorunlar ve en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="32b20-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-the-system"></a><span data-ttu-id="32b20-252">Hata: .NET Core sistemde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="32b20-252">Error: .NET Core is not found in the system.</span></span>
<span data-ttu-id="32b20-253">.NET Core .NET Core ikili yolu sisteminde yüklü olmadığını belirten bir hatayla karşılaşırsanız `dotnet` eksik olabilir.</span><span class="sxs-lookup"><span data-stu-id="32b20-253">If you encounter an error stating that .NET Core is not installed in the system, the PATH to the .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="32b20-254">Bu sorunu gidermek için .NET Core sisteminde ikili bulun:</span><span class="sxs-lookup"><span data-stu-id="32b20-254">In order to address this issue, find the .NET Core binary in the system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="32b20-255">Bu yol için dotnet ikili döndürür.</span><span class="sxs-lookup"><span data-stu-id="32b20-255">This returns the path to the dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="32b20-256">Şimdi bu yolu PATH değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="32b20-256">Now add this path to the PATH variable.</span></span> <span data-ttu-id="32b20-257">Sudo için secure_path ikili dotnet yolunu içerecek şekilde düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="32b20-257">For sudo, edit secure_path to contain the path to the dotnet binary:</span></span>
```bash 
sudo visudo
### Append the path found in the preceding example to 'secure_path' variable
```

<span data-ttu-id="32b20-258">Bu örnekte, secure_path değişken olarak okur:</span><span class="sxs-lookup"><span data-stu-id="32b20-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="32b20-259">Geçerli kullanıcı için PATH değişkeni ikili dotnet yolunu içerecek şekilde.bash_profile/.profile Düzenle</span><span class="sxs-lookup"><span data-stu-id="32b20-259">For the current user, edit .bash_profile/.profile to include the path to the dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append the path found in the preceding example to 'PATH' variable
```

<span data-ttu-id="32b20-260">.NET Core şimdi yolunda olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="32b20-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="32b20-261">AzCopy yükleme hatası</span><span class="sxs-lookup"><span data-stu-id="32b20-261">Error Installing AzCopy</span></span>
<span data-ttu-id="32b20-262">AzCopy yükleme ile ilgili sorunlarla karşılaşırsanız, AzCopy bash betik ayıklanan kullanarak çalıştırmak çalışabilir `azcopy` klasör.</span><span class="sxs-lookup"><span data-stu-id="32b20-262">If you encounter issues with AzCopy installation, you may try to run AzCopy using the bash script in the extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="32b20-263">Veri kopyalama sırasında sınırı eşzamanlı yazma</span><span class="sxs-lookup"><span data-stu-id="32b20-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="32b20-264">BLOB veya AzCopy dosyalarıyla kopyaladığınızda, bunu kopyalamaya çalışırken, başka bir uygulama verileri değiştirme göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="32b20-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="32b20-265">Mümkünse, Kopyalamakta olduğunuz veri kopyalama işlemi sırasında değiştirilmeyen emin olun.</span><span class="sxs-lookup"><span data-stu-id="32b20-265">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="32b20-266">Örneğin, bir Azure sanal makine ile ilişkili bir VHD'nin kopyalarken, başka bir uygulama şu anda VHD'ye yazıyorsanız emin olun.</span><span class="sxs-lookup"><span data-stu-id="32b20-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="32b20-267">Bunu yapmak için iyi bir Kopyalanacak kaynak kiralama tarafından yoldur.</span><span class="sxs-lookup"><span data-stu-id="32b20-267">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="32b20-268">Alternatif olarak, bir anlık görüntü VHD'yi ilk oluşturun ve sonra anlık görüntü kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="32b20-268">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="32b20-269">Bunlar kopyalanan sırada BLOB veya dosyalar için yazma diğer uygulamaların önleyemez, ardından işi tamamlanana zamanına göre kopyalanan kaynakların artık kaynak kaynaklarla tam eşlik gerekebileceğini aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="32b20-269">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="32b20-270">Bir Azcopy'i örnek bir makinede çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="32b20-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="32b20-271">AzCopy veri aktarımını hızlandırmak için makine kaynak kullanımını en üst düzeye çıkarmak için tasarlanmış, yalnızca bir Azcopy'i örnek bir makinede çalıştırın ve seçeneğini belirtin öneririz `--parallel-level` fazla eşzamanlı işlem gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="32b20-271">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="32b20-272">Daha fazla ayrıntı için yazın `AzCopy --help parallel-level` komut satırında.</span><span class="sxs-lookup"><span data-stu-id="32b20-272">For more details, type `AzCopy --help parallel-level` at the command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32b20-273">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="32b20-273">Next steps</span></span>
<span data-ttu-id="32b20-274">Azure Storage ve AzCopy hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="32b20-274">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="32b20-275">Azure Storage belgeleri:</span><span class="sxs-lookup"><span data-stu-id="32b20-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="32b20-276">Azure Storage'a giriş</span><span class="sxs-lookup"><span data-stu-id="32b20-276">Introduction to Azure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="32b20-277">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="32b20-277">Create a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="32b20-278">BLOB Depolama Gezgini ile yönetme</span><span class="sxs-lookup"><span data-stu-id="32b20-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="32b20-279">Azure Storage ile Azure CLI 2.0 kullanma</span><span class="sxs-lookup"><span data-stu-id="32b20-279">Using the Azure CLI 2.0 with Azure Storage</span></span>](../storage-azure-cli.md)
* [<span data-ttu-id="32b20-280">C++ içinden BLOB storage kullanma</span><span class="sxs-lookup"><span data-stu-id="32b20-280">How to use Blob storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="32b20-281">Java'da Blob Depolama'yı kullanma</span><span class="sxs-lookup"><span data-stu-id="32b20-281">How to use Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="32b20-282">Node.js'de Blob Depolama'yı kullanma</span><span class="sxs-lookup"><span data-stu-id="32b20-282">How to use Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="32b20-283">Python'da Blob Depolama'yı kullanma</span><span class="sxs-lookup"><span data-stu-id="32b20-283">How to use Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="32b20-284">Azure depolama blog gönderileri:</span><span class="sxs-lookup"><span data-stu-id="32b20-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="32b20-285">AzCopy Linux preview'daki tanışın</span><span class="sxs-lookup"><span data-stu-id="32b20-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="32b20-286">Azure Storage veri hareketi kitaplığı Önizleme Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="32b20-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="32b20-287">AzCopy: zaman uyumlu kopyası ve özelleştirilmiş içerik türü tanışın</span><span class="sxs-lookup"><span data-stu-id="32b20-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="32b20-288">AzCopy: Genel kullanılabilirlik, AzCopy 3.0 artı AzCopy 4.0 Önizleme sürümü tablo ve dosya desteği ile tanışın</span><span class="sxs-lookup"><span data-stu-id="32b20-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="32b20-289">AzCopy: Büyük ölçekli kopyalama senaryoları için en iyi duruma getirilmiş</span><span class="sxs-lookup"><span data-stu-id="32b20-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="32b20-290">AzCopy: Coğrafi olarak yedekli depolamaya okuma erişimi desteği</span><span class="sxs-lookup"><span data-stu-id="32b20-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="32b20-291">AzCopy: yeniden başlatılabilir modu ve SAS belirteci ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="32b20-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="32b20-292">AzCopy: arası hesap kopyalama Blob kullanma</span><span class="sxs-lookup"><span data-stu-id="32b20-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="32b20-293">AzCopy: Azure BLOB'ları karşıya yükleme ve indirme dosyaları</span><span class="sxs-lookup"><span data-stu-id="32b20-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

