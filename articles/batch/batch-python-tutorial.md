---
title: "aaaTutorial - kullanım hello Python için Azure Batch SDK'sı | Microsoft Docs"
description: "Azure Batch temel kavramlarını Hello öğrenin ve Python kullanarak basit bir çözüm oluşturun."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a><span data-ttu-id="a52f5-103">Python için Hello Batch SDK'sı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a52f5-103">Get started with hello Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a52f5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a52f5-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="a52f5-105">Python</span><span class="sxs-lookup"><span data-stu-id="a52f5-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="a52f5-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="a52f5-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="a52f5-107">Merhaba temel bilgileri öğrenmek [Azure Batch] [ azure_batch] ve hello [Batch Python] [ py_azure_sdk] istemci Python'da yazılmış küçük bir Batch uygulamasından aşağıdakiler ele gibi.</span><span class="sxs-lookup"><span data-stu-id="a52f5-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="a52f5-108">İki hello buluttaki Linux sanal makinelerde paralel iş yükünü betikleri kullanım hello Batch hizmeti tooprocess nasıl örnek ve ile nasıl etkileşim kurduklarını ele [Azure Storage](../storage/common/storage-introduction.md) dosya hazırlığı ve alımı için.</span><span class="sxs-lookup"><span data-stu-id="a52f5-108">We look at how two sample scripts use hello Batch service tooprocess a parallel workload on Linux virtual machines in hello cloud, and how they interact with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="a52f5-109">Ortak Batch uygulama iş akışı öğrenin ve hello başlıca Batch bileşenleri işler, görevler, havuzlar gibi temel bir anlayış edinmek ve işlem düğümleri.</span><span class="sxs-lookup"><span data-stu-id="a52f5-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="a52f5-110">![Batch çözümü iş akışı (temel)][11]</span><span class="sxs-lookup"><span data-stu-id="a52f5-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="a52f5-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a52f5-111">Prerequisites</span></span>
<span data-ttu-id="a52f5-112">Bu makalede, Python ve Linux alışkanlığına sahip olduğunuz varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-112">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="a52f5-113">Aşağıda Azure ve hello toplu işlem ve depolama hizmetleri için belirtilen mümkün toosatisfy hello hesap oluşturma gerekliliklerini olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="a52f5-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="a52f5-114">Hesaplar</span><span class="sxs-lookup"><span data-stu-id="a52f5-114">Accounts</span></span>
* <span data-ttu-id="a52f5-115">**Azure hesabı**: Henüz bir Azure aboneliğiniz yoksa, [ücretsiz Azure hesabı oluşturun][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="a52f5-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="a52f5-116">**Batch hesabı**: Azure aboneliğiniz olduktan sonra, [Azure Batch hesabı oluşturun](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a52f5-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="a52f5-117">**Storage hesabı**: Bkz. [Azure Storage hesapları hakkında](../storage/common/storage-create-storage-account.md) sayfası, [Storage hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) bölümü.</span><span class="sxs-lookup"><span data-stu-id="a52f5-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="a52f5-118">Kod örneği</span><span class="sxs-lookup"><span data-stu-id="a52f5-118">Code sample</span></span>
<span data-ttu-id="a52f5-119">Merhaba Python Eğitmen [kod örneği] [ github_article_samples] birçok Batch kod örnekleri bulunan hello hello biri [azure-batch-samples] [ github_samples] havuzda GitHub.</span><span class="sxs-lookup"><span data-stu-id="a52f5-119">hello Python tutorial [code sample][github_article_samples] is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="a52f5-120">Tüm hello örnekleri tıklayarak indirebileceğiniz **Kopyala veya indir > ZIP'i indir** hello depo giriş sayfasındaki veya hello tıklatarak [azure-batch-samples-master.zip] [ github_samples_zip]doğrudan indirme bağlantısına.</span><span class="sxs-lookup"><span data-stu-id="a52f5-120">You can download all hello samples by clicking **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="a52f5-121">Merhaba hello ZIP dosyasının içeriğini ayıkladıktan sonra Bu öğretici için hello iki betikleri hello bulunan `article_samples` dizini:</span><span class="sxs-lookup"><span data-stu-id="a52f5-121">Once you've extracted hello contents of hello ZIP file, hello two scripts for this tutorial are found in hello `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="a52f5-122">Python ortamı</span><span class="sxs-lookup"><span data-stu-id="a52f5-122">Python environment</span></span>
<span data-ttu-id="a52f5-123">toorun hello *python_tutorial_client.py* örnek betik, yerel iş istasyonunda ihtiyacınız bir **Python yorumlayıcı** sürümüyle uyumlu **2.7** veya **3.3 +**.</span><span class="sxs-lookup"><span data-stu-id="a52f5-123">toorun hello *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="a52f5-124">Merhaba betik Linux ve Windows'da test edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-124">hello script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="a52f5-125">şifreleme bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="a52f5-125">cryptography dependencies</span></span>
<span data-ttu-id="a52f5-126">Merhaba hello bağımlılıkları yüklemelisiniz [şifreleme] [ crypto] hello tarafından gerekli Kitaplığı `azure-batch` ve `azure-storage` Python paketlerini.</span><span class="sxs-lookup"><span data-stu-id="a52f5-126">You must install hello dependencies for hello [cryptography][crypto] library, required by hello `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="a52f5-127">Platformunuz için uygun işlemleri aşağıdaki hello birini gerçekleştirin veya toohello başvurun [şifreleme yükleme] [ crypto_install] daha fazla bilgi için ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="a52f5-127">Perform one of hello following operations appropriate for your platform, or refer toohello [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="a52f5-128">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a52f5-128">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="a52f5-129">CentOS</span><span class="sxs-lookup"><span data-stu-id="a52f5-129">CentOS</span></span>

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* <span data-ttu-id="a52f5-130">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="a52f5-130">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="a52f5-131">Windows</span><span class="sxs-lookup"><span data-stu-id="a52f5-131">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> <span data-ttu-id="a52f5-132">Python 3.3 + Linux'ta için yüklüyorsanız, hello python3 eşdeğerleri hello Python bağımlılıkları için kullanın.</span><span class="sxs-lookup"><span data-stu-id="a52f5-132">If installing for Python 3.3+ on Linux, use hello python3 equivalents for hello Python dependencies.</span></span> <span data-ttu-id="a52f5-133">Örneğin, Ubuntu üzerinde: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span><span class="sxs-lookup"><span data-stu-id="a52f5-133">For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span></span>
>
>

### <a name="azure-packages"></a><span data-ttu-id="a52f5-134">Azure paketleri</span><span class="sxs-lookup"><span data-stu-id="a52f5-134">Azure packages</span></span>
<span data-ttu-id="a52f5-135">Ardından, hello yüklemek **Azure Batch** ve **Azure Storage** Python paketlerini.</span><span class="sxs-lookup"><span data-stu-id="a52f5-135">Next, install hello **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="a52f5-136">Kullanarak her iki paketi yükleyebilirsiniz **PIP** ve hello *requirements.txt* burada bulundu:</span><span class="sxs-lookup"><span data-stu-id="a52f5-136">You can install both packages by using **pip** and hello *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="a52f5-137">Sorunu aşağıdaki **PIP** komut tooinstall hello Batch ve Storage paketlerini:</span><span class="sxs-lookup"><span data-stu-id="a52f5-137">Issue following **pip** command tooinstall hello Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="a52f5-138">Veya hello yükleyebilirsiniz [azure-batch] [ pypi_batch] ve [azure depolama] [ pypi_storage] Python paketlerini el ile:</span><span class="sxs-lookup"><span data-stu-id="a52f5-138">Or, you can install hello [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> <span data-ttu-id="a52f5-139">Ayrıcalıksız bir hesap kullanıyorsanız, komutlarınıza tooprefix gerekebilir `sudo`.</span><span class="sxs-lookup"><span data-stu-id="a52f5-139">If you are using an unprivileged account, you may need tooprefix your commands with `sudo`.</span></span> <span data-ttu-id="a52f5-140">Örneğin, `sudo pip install -r requirements.txt`.</span><span class="sxs-lookup"><span data-stu-id="a52f5-140">For example, `sudo pip install -r requirements.txt`.</span></span> <span data-ttu-id="a52f5-141">Python paketlerini yükleme hakkında daha fazla bilgi için python.org sayfasındaki [Paketleri Yükleme][pypi_install] bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="a52f5-141">For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.</span></span>
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="a52f5-142">Batch Python eğitmen kodu örneği</span><span class="sxs-lookup"><span data-stu-id="a52f5-142">Batch Python tutorial code sample</span></span>
<span data-ttu-id="a52f5-143">Merhaba Batch Python Eğitmen kodu örneği, iki Python betiği ve birkaç veri dosyasından oluşur.</span><span class="sxs-lookup"><span data-stu-id="a52f5-143">hello Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="a52f5-144">**python_tutorial_client.PY**: (sanal makineler) işlem düğümlerinde paralel iş yükünü hello toplu işlem ve depolama hizmetleri tooexecute ile etkileşim kurar.</span><span class="sxs-lookup"><span data-stu-id="a52f5-144">**python_tutorial_client.py**: Interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="a52f5-145">Merhaba *python_tutorial_client.py* komut dosyası yerel iş istasyonunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-145">hello *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="a52f5-146">**python_tutorial_task.PY**: çalıştığı hello betik işlem düğümlerini Azure tooperform hello gerçek çalışma.</span><span class="sxs-lookup"><span data-stu-id="a52f5-146">**python_tutorial_task.py**: hello script that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="a52f5-147">Merhaba örneğinde, *python_tutorial_task.py* hello metni (girdi dosyası hello) Azure Storage'dan indirilen dosyada ayrıştırıyor.</span><span class="sxs-lookup"><span data-stu-id="a52f5-147">In hello sample, *python_tutorial_task.py* parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="a52f5-148">Bir metin dosyası oluşturur sonra (Merhaba çıktı dosyası) hello giriş dosyasında görünen hello ilk üç sözcük listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-148">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="a52f5-149">Merhaba çıktı dosyasını oluşturduktan sonra *python_tutorial_task.py* karşıya dosya tooAzure depolama hello.</span><span class="sxs-lookup"><span data-stu-id="a52f5-149">After it creates hello output file, *python_tutorial_task.py* uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="a52f5-150">İndirme toohello istemci komut dosyası iş istasyonunuza çalıştıran için kullanılabilir yapar.</span><span class="sxs-lookup"><span data-stu-id="a52f5-150">This makes it available for download toohello client script running on your workstation.</span></span> <span data-ttu-id="a52f5-151">Merhaba *python_tutorial_task.py* işlem hello Batch hizmeti düğümünde birden fazla paralel betik çalışır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-151">hello *python_tutorial_task.py* script runs in parallel on multiple compute nodes in hello Batch service.</span></span>
* <span data-ttu-id="a52f5-152">**./Data/taskdata\*.txt**: hello üzerinde çalıştırmak hello görevleri işlem düğümleri için bu üç metin dosyaları hello girin.</span><span class="sxs-lookup"><span data-stu-id="a52f5-152">**./data/taskdata\*.txt**: These three text files provide hello input for hello tasks that run on hello compute nodes.</span></span>

<span data-ttu-id="a52f5-153">Aşağıdaki diyagramda hello hello istemci ve görev betikleri tarafından gerçekleştirilen birincil işlemleri hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-153">hello following diagram illustrates hello primary operations that are performed by hello client and task scripts.</span></span> <span data-ttu-id="a52f5-154">Bu temel iş akışı, Batch’le oluşturulan çok sayıda işlem çözümünün tipik halidir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-154">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="a52f5-155">Bu her özelliğe hello Batch hizmeti uygun olmadığı belirtilirken, neredeyse her Batch senaryosu iş akışının bölümlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-155">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="a52f5-156">![Batch örnek iş akışı][8]</span><span class="sxs-lookup"><span data-stu-id="a52f5-156">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="a52f5-157">**1. Adım.**</span><span class="sxs-lookup"><span data-stu-id="a52f5-157">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="a52f5-158">Azure Blob Storage’da **kapsayıcılar** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a52f5-158">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="a52f5-159">
[**2. Adım.**](#step-2-upload-task-script-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="a52f5-159">
[**Step 2.**](#step-2-upload-task-script-and-data-files)</span></span> <span data-ttu-id="a52f5-160">Görev betiğini ve girdi dosyalarını toocontainers karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a52f5-160">Upload task script and input files toocontainers.</span></span><br/><span data-ttu-id="a52f5-161">
[**3. Adım.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="a52f5-161">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="a52f5-162">Batch **havuzu** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a52f5-162">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="a52f5-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="a52f5-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="a52f5-164">Merhaba havuzu **StartTask** yüklemeleri hello görev betiğini (python_tutorial_task.py) toonodes hello havuzuna Katıl gibi.</span><span class="sxs-lookup"><span data-stu-id="a52f5-164">hello pool **StartTask** downloads hello task script (python_tutorial_task.py) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="a52f5-165">
[**4. Adım.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="a52f5-165">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="a52f5-166">Batch **işi** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a52f5-166">Create a Batch **job**.</span></span><br/><span data-ttu-id="a52f5-167">
[**5. Adım**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="a52f5-167">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="a52f5-168">Ekleme **görevleri** toohello işi.</span><span class="sxs-lookup"><span data-stu-id="a52f5-168">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="a52f5-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="a52f5-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="a52f5-170">Merhaba, düğümlerde zamanlanmış tooexecute görevlerdir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-170">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="a52f5-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="a52f5-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="a52f5-172">Her görev kendi girdi verilerini Azure Storage’dan indirip yürütmeye başlar.</span><span class="sxs-lookup"><span data-stu-id="a52f5-172">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="a52f5-173">
[**6. Adım**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="a52f5-173">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="a52f5-174">Görevleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="a52f5-174">Monitor tasks.</span></span><br/>
  <span data-ttu-id="a52f5-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="a52f5-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="a52f5-176">Görevlerin tamamlanmasıyla, kendi çıktı veri tooAzure depolama karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a52f5-176">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="a52f5-177">
[**7. Adım**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="a52f5-177">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="a52f5-178">Storage’dan görev çıktısını indirin.</span><span class="sxs-lookup"><span data-stu-id="a52f5-178">Download task output from Storage.</span></span>

<span data-ttu-id="a52f5-179">Yukarıda belirtildiği gibi, her Batch çözümü tam olarak bu adımları gerçekleştirmese ve çok daha fazlasını içerebilse de; bu örnek, Batch çözümünde bulunan ortak işlemleri göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-179">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="a52f5-180">İstemci komut dosyasını hazırlama</span><span class="sxs-lookup"><span data-stu-id="a52f5-180">Prepare client script</span></span>
<span data-ttu-id="a52f5-181">Merhaba örneği çalıştırmadan önce Batch ve Storage hesabı kimlik bilgilerinizi çok eklemek*python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="a52f5-181">Before you run hello sample, add your Batch and Storage account credentials too*python_tutorial_client.py*.</span></span> <span data-ttu-id="a52f5-182">Henüz yapmadıysanız, kimlik bilgilerinizle izleyerek, sık kullanılan Düzenleyicisi ve güncelleştirme hello hello dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="a52f5-182">If you have not done so already, open hello file in your favorite editor and update hello following lines with your credentials.</span></span>

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

<span data-ttu-id="a52f5-183">Batch ve Storage hesabı kimlik bilgilerinizi her hizmetin hesap dikey hello hello bulabilirsiniz [Azure portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="a52f5-183">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="a52f5-184">![Merhaba portalda batch kimlik bilgileri][9]
![hello portalda Storage kimlik bilgileri][10]</span><span class="sxs-lookup"><span data-stu-id="a52f5-184">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="a52f5-185">Aşağıdaki bölümlerde hello biz tarafından kullanılan hello adımları analiz hello tooprocess hello Batch hizmeti iş yükünü komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="a52f5-185">In hello following sections, we analyze hello steps used by hello scripts tooprocess a workload in hello Batch service.</span></span> <span data-ttu-id="a52f5-186">Düzenli olarak çalışırken toohello betiklere yolunuzu hello makalenin hello rest aracılığıyla iş toorefer öneririz.</span><span class="sxs-lookup"><span data-stu-id="a52f5-186">We encourage you toorefer regularly toohello scripts in your editor while you work your way through hello rest of hello article.</span></span>

<span data-ttu-id="a52f5-187">Aşağıdaki satırda toohello gidin **python_tutorial_client.py** toostart adım 1:</span><span class="sxs-lookup"><span data-stu-id="a52f5-187">Navigate toohello following line in **python_tutorial_client.py** toostart with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="a52f5-188">1. Adım: Storage kapsayıcıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="a52f5-188">Step 1: Create Storage containers</span></span>
<span data-ttu-id="a52f5-189">![Azure Depolama'da kapsayıcı oluşturma][1]
</span><span class="sxs-lookup"><span data-stu-id="a52f5-189">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="a52f5-190">Azure Storage ilet etkileşimde bulunmak için Batch’te yerleşik destek bulunur.</span><span class="sxs-lookup"><span data-stu-id="a52f5-190">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="a52f5-191">Storage hesabınızdaki kapsayıcılar, Batch hesabınızda çalışan hello görevler için gerekli hello dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a52f5-191">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="a52f5-192">Merhaba kapsayıcılara hello görevlerin oluşturduğu bir yerde toostore hello çıktı verilerini de sağlar.</span><span class="sxs-lookup"><span data-stu-id="a52f5-192">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="a52f5-193">ilk şey hello hello *python_tutorial_client.py* komut dosyasının yaptığını üç kapsayıcı oluşturmaktır [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span><span class="sxs-lookup"><span data-stu-id="a52f5-193">hello first thing hello *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="a52f5-194">**Uygulama**: Bu kapsayıcı hello görevleriniz tarafından çalıştırılan hello Python betiğini depolayacaktır *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="a52f5-194">**application**: This container will store hello Python script run by hello tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="a52f5-195">**Giriş**: görevler hello hello veri dosyaları tooprocess yükleyecek *giriş* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="a52f5-195">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="a52f5-196">**Çıktı**: görevler girdi dosyası işlemeyi tamamladıklarında hello sonuçları toohello karşıya yükleyecek *çıkış* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="a52f5-196">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="a52f5-197">Sipariş toointeract bir depolama hesabı ve kapsayıcı, oluşturma hello kullanırız [azure depolama] [ pypi_storage] toocreate paketini bir [BlockBlobService] [ py_blockblobservice] nesne--hello "blob istemcisi"</span><span class="sxs-lookup"><span data-stu-id="a52f5-197">In order toointeract with a Storage account and create containers, we use hello [azure-storage][pypi_storage] package toocreate a [BlockBlobService][py_blockblobservice] object--hello "blob client."</span></span> <span data-ttu-id="a52f5-198">Ardından üç kapsayıcı hello blob istemcisini kullanarak hello depolama hesabında oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="a52f5-198">We then create three containers in hello Storage account using hello blob client.</span></span>

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

<span data-ttu-id="a52f5-199">Merhaba kapsayıcılara oluşturduktan sonra Merhaba uygulaması artık hello görevler tarafından kullanılacak hello dosyaları karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="a52f5-200">[Nasıl toouse python'dan Azure Blob storage](../storage/blobs/storage-python-how-to-use-blob-storage.md) Azure Storage kapsayıcıları ve blob'larla çalışma hakkında kapsamlı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a52f5-200">[How toouse Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="a52f5-201">Batch ile çalışmaya başladığınızda okuma listenizin hello yukarıya yakın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="a52f5-202">2. Adım: Görev betiğini ve veri dosyalarını karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="a52f5-202">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="a52f5-203">![Karşıya yükleme görev uygulamasını ve girdi (veri) toocontainers dosyaları][2]
</span><span class="sxs-lookup"><span data-stu-id="a52f5-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="a52f5-204">Merhaba dosyayı karşıya yükleme işlemi, *python_tutorial_client.py* ilk tanımlar **uygulama** ve **giriş** hello yerel makinede oldukları gibi dosya yolları.</span><span class="sxs-lookup"><span data-stu-id="a52f5-204">In hello file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="a52f5-205">Sonra hello önceki adımda oluşturduğunuz bu dosyaları toohello kapsayıcıları yükler.</span><span class="sxs-lookup"><span data-stu-id="a52f5-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

<span data-ttu-id="a52f5-206">Liste anlamayı kullanarak, hello `upload_file_to_container` çağrıldığında her dosya hello koleksiyonlarda ve iki [ResourceFile] [ py_resource_file] koleksiyonu doldurulur.</span><span class="sxs-lookup"><span data-stu-id="a52f5-206">Using list comprehension, hello `upload_file_to_container` function is called for each file in hello collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="a52f5-207">Merhaba `upload_file_to_container` işlevi aşağıda görünür:</span><span class="sxs-lookup"><span data-stu-id="a52f5-207">hello `upload_file_to_container` function appears below:</span></span>

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a><span data-ttu-id="a52f5-208">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="a52f5-208">ResourceFiles</span></span>
<span data-ttu-id="a52f5-209">A [ResourceFile] [ py_resource_file] hello URL tooa indirilen tooa Azure depolama alanı dosyasında toplu görevlerle işlem düğümü, görev çalıştırılmadan önce sağlar.</span><span class="sxs-lookup"><span data-stu-id="a52f5-209">A [ResourceFile][py_resource_file] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="a52f5-210">Merhaba [ResourceFile][py_resource_file].** blob_source** özelliği, Azure Storage'da yer aldığından hello hello dosyanın tam URL'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-210">hello [ResourceFile][py_resource_file].**blob_source** property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="a52f5-211">Merhaba URL ayrıca güvenli erişim toohello dosya sağlayan bir paylaşılan erişim imzası (SAS) içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-211">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="a52f5-212">Batch’teki çoğu görev türünde *ResourceFiles* özelliği vardır; bu özellikte şunlar bulunur:</span><span class="sxs-lookup"><span data-stu-id="a52f5-212">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="a52f5-213">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="a52f5-213">[CloudTask][py_task]</span></span>
* <span data-ttu-id="a52f5-214">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="a52f5-214">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="a52f5-215">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="a52f5-215">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="a52f5-216">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="a52f5-216">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="a52f5-217">Bu örnek hello JobPreparationTask veya JobReleaseTask görev türlerini kullanmaz, ancak daha fazla bilgiyi ilgili [iş hazırlama ve tamamlama görevlerini çalıştırma Azure Batch işlem düğümlerinde](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="a52f5-217">This sample does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="a52f5-218">Paylaşılan erişim imzası (SAS)</span><span class="sxs-lookup"><span data-stu-id="a52f5-218">Shared access signature (SAS)</span></span>
<span data-ttu-id="a52f5-219">Paylaşılan erişim imzaları güvenli erişim toocontainers ve Azure Storage blobları sağlayan dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-219">Shared access signatures are strings that provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="a52f5-220">Merhaba *python_tutorial_client.py* betiği hem blob kullanır ve kapsayıcı paylaşılan erişim imzası ve nasıl tooobtain bu paylaşılan erişim imzası dizeleri depolama hizmeti hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-220">hello *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="a52f5-221">**Blob paylaşılan erişim imzaları**: depolama biriminden hello görev betiğini ve girdi veri dosyalarını indirdiğinde blob paylaşılan erişim imzaları hello havuza ait StartTask kullanır (bkz [3. adım](#step-3-create-batch-pool) aşağıda).</span><span class="sxs-lookup"><span data-stu-id="a52f5-221">**Blob shared access signatures**: hello pool's StartTask uses blob shared access signatures when it downloads hello task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="a52f5-222">Merhaba `upload_file_to_container` işlevi *python_tutorial_client.py* her blob'un paylaşılan erişim imzasını alan hello kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-222">hello `upload_file_to_container` function in *python_tutorial_client.py* contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="a52f5-223">Bunu çağırarak yapar [BlockBlobService.make_blob_url] [ py_make_blob_url] hello depolama modülü.</span><span class="sxs-lookup"><span data-stu-id="a52f5-223">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in hello Storage module.</span></span>
* <span data-ttu-id="a52f5-224">**Kapsayıcı paylaşılan erişim imzası**: her görev hello işlem düğümü işini bitirdiğinde, kendi çıktı dosyasını toohello yükler *çıkış* Azure storage'da kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="a52f5-224">**Container shared access signature**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="a52f5-225">toodo bunu *python_tutorial_task.py* toohello kapsayıcısına yazma erişimi sağlayan kapsayıcı paylaşılan erişim imzasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-225">toodo so, *python_tutorial_task.py* uses a container shared access signature that provides write access toohello container.</span></span> <span data-ttu-id="a52f5-226">Merhaba `get_container_sas_token` işlevi *python_tutorial_client.py* daha sonra bir komut satırı bağımsız değişkeni toohello görevleri olarak geçirilir hello kapsayıcının paylaşılan erişim imzasını alır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-226">hello `get_container_sas_token` function in *python_tutorial_client.py* obtains hello container's shared access signature, which is then passed as a command-line argument toohello tasks.</span></span> <span data-ttu-id="a52f5-227">#5. adım [Ekle görevleri tooa iş](#step-5-add-tasks-to-job), hello hello kapsayıcı SAS kullanımını açıklar.</span><span class="sxs-lookup"><span data-stu-id="a52f5-227">Step #5, [Add tasks tooa job](#step-5-add-tasks-to-job), discusses hello usage of hello container SAS.</span></span>

> [!TIP]
> <span data-ttu-id="a52f5-228">Hello iki parçalı seriyi kullanıma paylaşılan erişim imzalarındaki [1. Bölüm: Merhaba SAS modelini anlama](../storage/common/storage-dotnet-shared-access-signature-part-1.md) ve [Kısım 2: oluşturma ve bir SAS hello Blob hizmeti ile kullanma](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn güvenli erişim sağlama hakkında daha fazla bilgi Depolama hesabınızdaki toodata.</span><span class="sxs-lookup"><span data-stu-id="a52f5-228">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with hello Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="a52f5-229">3. Adım: Batch havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a52f5-229">Step 3: Create Batch pool</span></span>
<span data-ttu-id="a52f5-230">![Batch havuzu oluşturma][3]
</span><span class="sxs-lookup"><span data-stu-id="a52f5-230">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="a52f5-231">Batch **havuzu**, Batch’in işe ait görevleri yürüttüğü işlem düğümlerinin (sanal makineler) koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="a52f5-231">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="a52f5-232">Merhaba görev betiğini ve veri dosyalarını toohello depolama hesabı, gönderildikten sonra *python_tutorial_client.py* hello Batch Python modülünü kullanarak hello Batch hizmetiyle etkileşimi başlatır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-232">After it uploads hello task script and data files toohello Storage account, *python_tutorial_client.py* starts its interaction with hello Batch service by using hello Batch Python module.</span></span> <span data-ttu-id="a52f5-233">toodo bunu bir [BatchServiceClient] [ py_batchserviceclient] oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="a52f5-233">toodo so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

<span data-ttu-id="a52f5-234">Ardından, işlem düğümleri havuzu hello çağrısıyla Batch hesabında çok oluşturulan`create_pool`.</span><span class="sxs-lookup"><span data-stu-id="a52f5-234">Next, a pool of compute nodes is created in hello Batch account with a call too`create_pool`.</span></span>

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="a52f5-235">Bir havuz oluşturduğunuzda, tanımladığınız bir [PoolAddParameter] [ py_pooladdparam] hello havuz için bazı özellikler belirtir:</span><span class="sxs-lookup"><span data-stu-id="a52f5-235">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for hello pool:</span></span>

* <span data-ttu-id="a52f5-236">**Kimliği** hello havuzunun (*kimliği* - gerekli)</span><span class="sxs-lookup"><span data-stu-id="a52f5-236">**ID** of hello pool (*id* - required)</span></span><p/><span data-ttu-id="a52f5-237">Batch’deki çoğu varlık gibi, yeni havuzunuzda da, Batch hesabınızın içinde benzersiz bir kimlik olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-237">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="a52f5-238">Kodunuzu toothis havuz Kimliğini kullanarak ifade eder ve hello Azure hello havuzunda şekilde tanımlarsınız [portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="a52f5-238">Your code refers toothis pool using its ID, and it's how you identify hello pool in hello Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="a52f5-239">**İşlem düğümleri sayısı** (*target_dedicated* - gerekli)</span><span class="sxs-lookup"><span data-stu-id="a52f5-239">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="a52f5-240">Bu özellik hello havuzda kaç VM dağıtılması gerekir belirtir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-240">This property specifies how many VMs should be deployed in hello pool.</span></span> <span data-ttu-id="a52f5-241">Tüm Batch hesaplarının bir varsayılan olması önemli toonote olan **kota** sınırları sayısı hello **çekirdek** (ve dolayısıyla işlem düğümleriyle) bir Batch hesabında.</span><span class="sxs-lookup"><span data-stu-id="a52f5-241">It is important toonote that all Batch accounts have a default **quota** that limits hello number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="a52f5-242">Merhaba varsayılan kotalar ve yönergeleri hakkında çok bulabileceğiniz[kota artırma](batch-quota-limit.md#increase-a-quota) (örneğin, çekirdek Batch hesabınızdaki en yüksek sayısı hello) içinde [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="a52f5-242">You can find hello default quotas and instructions on how too[increase a quota](batch-quota-limit.md#increase-a-quota) (such as hello maximum number of cores in your Batch account) in [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="a52f5-243">Kendinizi "Neden havuzum X düğümden fazlasına ulaşamıyor?" sorusunu sorarken bulursanız</span><span class="sxs-lookup"><span data-stu-id="a52f5-243">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="a52f5-244">Bu çekirdek kotası hello neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-244">this core quota may be hello cause.</span></span>
* <span data-ttu-id="a52f5-245">Düğümler için **işletim sistemi** (*virtual_machine_configuration***veya***cloud_service_configuration* - gerekli)</span><span class="sxs-lookup"><span data-stu-id="a52f5-245">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="a52f5-246">*python_tutorial_client.py* öğesinde [VirtualMachineConfiguration][py_vm_config] kullanarak Linux için havuz oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="a52f5-246">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="a52f5-247">Merhaba `select_latest_verified_vm_image_with_node_agent_sku` işlevi `common.helpers` çalışmak basitleştirir [Azure Virtual Machines Marketi] [ vm_marketplace] görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a52f5-247">hello `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="a52f5-248">Market görüntülerini kullanma hakkında daha fazla bilgi için bkz. [Azure Batch havuzlarında Linux işlem düğümlerini hazırlama](batch-linux-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="a52f5-248">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="a52f5-249">**İşlem düğümlerinin boyutu** (*vm_size* - gerekli)</span><span class="sxs-lookup"><span data-stu-id="a52f5-249">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="a52f5-250">[VirtualMachineConfiguration][py_vm_config] için Linux düğümleri belirlediğimizden, bir VM boyutunu (bu örnekte `STANDARD_A1`) [Azure’de sanal makine boyutları](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)’nda belirttik.</span><span class="sxs-lookup"><span data-stu-id="a52f5-250">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a52f5-251">Bir kez daha, daha fazla bilgi için bkz. [Azure Batch havuzlarında Linux işlem düğümlerini hazırlama](batch-linux-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="a52f5-251">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="a52f5-252">**Görev Başlat** (*start_task* - gerekli değil)</span><span class="sxs-lookup"><span data-stu-id="a52f5-252">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="a52f5-253">Yukarıdaki fiziksel düğüm özellikleri Hello yanı sıra siz de belirtebilir bir [StartTask] [ py_starttask] hello havuzu (gerekli değildir).</span><span class="sxs-lookup"><span data-stu-id="a52f5-253">Along with hello above physical node properties, you may also specify a [StartTask][py_starttask] for hello pool (it is not required).</span></span> <span data-ttu-id="a52f5-254">Bu düğüme hello havuzuna katılır ve her bir düğümü yeniden Hello StartTask her düğümde yürütür.</span><span class="sxs-lookup"><span data-stu-id="a52f5-254">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="a52f5-255">Merhaba StartTask özellikle Merhaba, görevlerinizin çalıştığı hello uygulamaları yükleme gibi görevlerini yürütülmesi için işlem düğümlerinin hazırlanmasında yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-255">hello StartTask is especially useful for preparing compute nodes for hello execution of tasks, such as installing hello applications that your tasks run.</span></span><p/><span data-ttu-id="a52f5-256">Bu örnek uygulamasında hello StartTask, Storage'dan indirilen hello dosyaları kopyalar (hangi belirtilen hello StartTask'ın kullanarak **resource_files** özelliği) hello StartTask gelen *çalışma dizini* toohello *paylaşılan* hello düğüm üzerinde çalışan tüm görevlerin dizin.</span><span class="sxs-lookup"><span data-stu-id="a52f5-256">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello StartTask's **resource_files** property) from hello StartTask *working directory* toohello *shared* directory that all tasks running on hello node can access.</span></span> <span data-ttu-id="a52f5-257">Esas olarak, bu kopyalar `python_tutorial_task.py` toohello paylaşılan her düğüme hello düğümü hello havuza katılmış olduğundan hello düğümü üzerinde çalışacak herhangi bir görevi erişebilmesi.</span><span class="sxs-lookup"><span data-stu-id="a52f5-257">Essentially, this copies `python_tutorial_task.py` toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

<span data-ttu-id="a52f5-258">Merhaba çağrısı toohello karşılaşabilirsiniz `wrap_commands_in_shell` yardımcı işlevi.</span><span class="sxs-lookup"><span data-stu-id="a52f5-258">You may notice hello call toohello `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="a52f5-259">Bu işlev ayrı komutların koleksiyonunu alır ve görevin komut satırı özelliğine uygun tek bir komut satırı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a52f5-259">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="a52f5-260">Ayrıca içinde yukarıdaki hello kod parçacığında dikkat çeken bir şey hello hello iki ortam değişkenleri kullanımıdır **command_line** hello StartTask özelliğinin: `AZ_BATCH_TASK_WORKING_DIR` ve `AZ_BATCH_NODE_SHARED_DIR`.</span><span class="sxs-lookup"><span data-stu-id="a52f5-260">Also notable in hello code snippet above is hello use of two environment variables in hello **command_line** property of hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="a52f5-261">Batch havuzundaki her işlem düğümü belirli tooBatch olan birkaç ortam değişkenlerini otomatik olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-261">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="a52f5-262">Bir görev tarafından yürütülen herhangi bir işlem toothese ortam değişkenlerine erişim vardır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-262">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="a52f5-263">bir Batch havuzu yanı sıra görev çalışma dizinleri hakkında bilgilerin işlem düğümlerinde kullanılabilir hello ortam değişkenleri hakkında daha fazla toofind bkz **görevler için ortam ayarları** ve **dosyalar ve dizinler ** hello içinde [Azure Batch özelliklerine genel bakış](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="a52f5-263">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in hello [overview of Azure Batch features](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="a52f5-264">4. Adım: Batch işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a52f5-264">Step 4: Create Batch job</span></span>
<span data-ttu-id="a52f5-265">![Batch işi oluşturma][4]</span><span class="sxs-lookup"><span data-stu-id="a52f5-265">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="a52f5-266">Batch **işi**, görevler koleksiyonudur ve işlem düğümlerinin bir havuzuyla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-266">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="a52f5-267">Merhaba görevleri bir işlemle ilişkili hello havuzun işlem düğümleri üzerinde yürütün.</span><span class="sxs-lookup"><span data-stu-id="a52f5-267">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="a52f5-268">İş önceliği, ilişkisi tooother işlerini hello toplu işlem hesabı ve bir işi yalnızca ilgili iş yüklerinde görevlerin düzenlenmesi ve için aynı zamanda hello en fazla çalışma hello işin (ve uzantılarının, görevleri) gibi bazı kısıtlamalar izlenmesi için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a52f5-268">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) and job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="a52f5-269">Bu örnekte, ancak hello iş #3. adımda oluşturulan hello havuzu ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-269">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="a52f5-270">Yapılandırılmış başka ek özellik yoktur.</span><span class="sxs-lookup"><span data-stu-id="a52f5-270">No additional properties are configured.</span></span>

<span data-ttu-id="a52f5-271">Tüm Batch işleri belirli bir havuzla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-271">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="a52f5-272">Bu ilişkilendirme hello işin görevlerinin hangi düğümleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-272">This association indicates which nodes hello job's tasks execute on.</span></span> <span data-ttu-id="a52f5-273">Hello kullanarak hello havuzu belirtin [Poolınformation] [ py_poolinfo] hello aşağıdaki kod parçacığında gösterildiği gibi özelliği.</span><span class="sxs-lookup"><span data-stu-id="a52f5-273">You specify hello pool by using hello [PoolInformation][py_poolinfo] property, as shown in hello code snippet below.</span></span>

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="a52f5-274">Bir işi oluşturuldu, görevler tooperform hello iş eklenir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-274">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="a52f5-275">5. adım: görevleri toojob ekleme</span><span class="sxs-lookup"><span data-stu-id="a52f5-275">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="a52f5-276">![Görevleri toojob Ekle][5]</span><span class="sxs-lookup"><span data-stu-id="a52f5-276">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="a52f5-277">
*(1) görevler toohello iş eklenir, düğümlerde zamanlanmış toorun (2) hello görevlerdir ve (3) hello görevleri hello veri dosyaları tooprocess indirme*</span><span class="sxs-lookup"><span data-stu-id="a52f5-277">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="a52f5-278">Toplu **görevleri** hello üzerinde yürütülen hello tek tek iş birimleri işlem düğümlerini şunlardır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-278">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="a52f5-279">Bir görev, bir komut satırı ve hello komut dosyaları veya bu komut satırında belirttiğiniz yürütülebilir dosyaları çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-279">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="a52f5-280">tooactually gerçekleştirmek iş, görevleri tooa iş eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-280">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="a52f5-281">Her [CloudTask] [ py_task] komut satırı özelliğiyle birlikte yapılandırılan ve [ResourceFiles] [ py_resource_file] (Merhaba havuza ait startTask gibi) bu hello komut satırı otomatik olarak yürütülmeden önce görevin toohello düğümü indirir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-281">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="a52f5-282">Merhaba örnekte, her görev yalnızca bir dosya işler.</span><span class="sxs-lookup"><span data-stu-id="a52f5-282">In hello sample, each task processes only one file.</span></span> <span data-ttu-id="a52f5-283">Bu nedenle, kendi ResourceFiles koleksiyonunda tek bir öğe bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-283">Thus, its ResourceFiles collection contains a single element.</span></span>

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> <span data-ttu-id="a52f5-284">Ortam değişkenlerine eriştiklerinde gibi `$AZ_BATCH_NODE_SHARED_DIR` veya hello düğümün bulunmayan bir uygulama yürüttüklerinde `PATH`, görev komut satırları hello çağırma gerekir açıkça gibi kabuğunda `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span><span class="sxs-lookup"><span data-stu-id="a52f5-284">When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in hello node's `PATH`, task command lines must invoke hello shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span></span> <span data-ttu-id="a52f5-285">Bu gereksinim, görevlerinizin hello düğümün bir uygulama yürütüyorsa gereksizdir `PATH` ve herhangi bir ortam değişkeni başvurusu değil.</span><span class="sxs-lookup"><span data-stu-id="a52f5-285">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` and do not reference any environment variables.</span></span>
>
>

<span data-ttu-id="a52f5-286">Merhaba içinde `for` Yukarıdaki kod parçacığında hello döngüde hello komut satırı hello görev için çok geçirilen beş komut satırı bağımsız değişkenlerini ile oluşturulur görebilirsiniz*python_tutorial_task.py*:</span><span class="sxs-lookup"><span data-stu-id="a52f5-286">Within hello `for` loop in hello code snippet above, you can see that hello command line for hello task is constructed with five command-line arguments that are passed too*python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="a52f5-287">**FilePath**: hello düğümde yer aldığından bu hello yerel yol toohello dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-287">**filepath**: This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="a52f5-288">ResourceFile nesnesi'ne zaman hello `upload_file_to_container` oluşturulduğu yukarıdaki adım 2'de hello dosya adı bu özellik için kullanılır (Merhaba `file_path` hello ResourceFile oluşturucuda parametresinde).</span><span class="sxs-lookup"><span data-stu-id="a52f5-288">When hello ResourceFile object in `upload_file_to_container` was created in Step 2 above, hello file name was used for this property (hello `file_path` parameter in hello ResourceFile constructor).</span></span> <span data-ttu-id="a52f5-289">Bu, hello dosya bulunabilir hello aynı gösterir hello düğümü olarak dizininde *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="a52f5-289">This indicates that hello file can be found in hello same directory on hello node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="a52f5-290">**NumWords**: hello üst *N* sözcükler toohello çıktı dosyasına yazılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-290">**numwords**: hello top *N* words should be written toohello output file.</span></span>
3. <span data-ttu-id="a52f5-291">**storageaccount**: hello hello hello kapsayıcı toowhich hello görev çıktısını sahibi depolama hesabı adını karşıya yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-291">**storageaccount**: hello name of hello Storage account that owns hello container toowhich hello task output should be uploaded.</span></span>
4. <span data-ttu-id="a52f5-292">**storagecontainer**: hello depolama kapsayıcısı toowhich hello hello adını çıktı dosyaları karşıya yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-292">**storagecontainer**: hello name of hello Storage container toowhich hello output files should be uploaded.</span></span>
5. <span data-ttu-id="a52f5-293">**sastoken**: yazma erişimi toohello sağlayan hello paylaşılan erişim imzası (SAS) **çıkış** Azure storage'da kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="a52f5-293">**sastoken**: hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="a52f5-294">Merhaba *python_tutorial_task.py* komut dosyası bu paylaşılan erişim imzasını kullanır, kendi BlockBlobService başvurusunu oluşturduğunda.</span><span class="sxs-lookup"><span data-stu-id="a52f5-294">hello *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="a52f5-295">Bu, yazma erişimi toohello kapsayıcı hello depolama hesabı için erişim anahtarı gerekmeden sağlar.</span><span class="sxs-lookup"><span data-stu-id="a52f5-295">This provides write access toohello container without requiring an access key for hello storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="a52f5-296">6. Adım: Görevleri izleme</span><span class="sxs-lookup"><span data-stu-id="a52f5-296">Step 6: Monitor tasks</span></span>
<span data-ttu-id="a52f5-297">![Görevleri izleme][6]</span><span class="sxs-lookup"><span data-stu-id="a52f5-297">![Monitor tasks][6]</span></span><br/><span data-ttu-id="a52f5-298">
*komut dosyası (1) izleyiciler hello görevleri tamamlama durumu için hello ve (2) hello görevler de sonuç verilerini tooAzure depolama yükler*</span><span class="sxs-lookup"><span data-stu-id="a52f5-298">
*hello script (1) monitors hello tasks for completion status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="a52f5-299">Görevleri tooa iş eklendiğinde bunlar otomatik olarak kuyruğa ve hello işle ilişkili hello havuzundaki işlem düğümlerinde yürütülmesi için zamanlanan.</span><span class="sxs-lookup"><span data-stu-id="a52f5-299">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="a52f5-300">Belirttiğiniz hello ayarlarına bağlı olarak, Batch tüm kuyruğa alınan, zamanlama, yeniden deneniyor ve diğer görev yönetimi görevlerini işler.</span><span class="sxs-lookup"><span data-stu-id="a52f5-300">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="a52f5-301">Toomonitoring görev yürütme birçok yaklaşım vardır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-301">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="a52f5-302">Merhaba `wait_for_tasks_to_complete` işlevi *python_tutorial_client.py* hello bu durumda, belirli bir durumu için görevleri izlemenin basit bir örnek sağlar [tamamlandı] [ py_taskstate] durumu.</span><span class="sxs-lookup"><span data-stu-id="a52f5-302">hello `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, hello [completed][py_taskstate] state.</span></span>

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="a52f5-303">7. Adım: Görev çıktısı indirme</span><span class="sxs-lookup"><span data-stu-id="a52f5-303">Step 7: Download task output</span></span>
<span data-ttu-id="a52f5-304">![Storage'dan görev çıktısını indirme][7]</span><span class="sxs-lookup"><span data-stu-id="a52f5-304">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="a52f5-305">Merhaba iş tamamlandığında, hello görevleri hello çıktısını Azure Storage'dan indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-305">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="a52f5-306">Bu çağrı çok yapılır`download_blobs_from_container` içinde *python_tutorial_client.py*:</span><span class="sxs-lookup"><span data-stu-id="a52f5-306">This is done with a call too`download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> <span data-ttu-id="a52f5-307">Çağrı çok hello`download_blobs_from_container` içinde *python_tutorial_client.py* hello dosyaları indirilen tooyour giriş dizini olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-307">hello call too`download_blobs_from_container` in *python_tutorial_client.py* specifies that hello files should be downloaded tooyour home directory.</span></span> <span data-ttu-id="a52f5-308">Ücretsiz toomodify düşünüyorsanız bu konumu çıktı.</span><span class="sxs-lookup"><span data-stu-id="a52f5-308">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="a52f5-309">8. Adım: Sil kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="a52f5-309">Step 8: Delete containers</span></span>
<span data-ttu-id="a52f5-310">Azure Storage'da yer alan veriler için ücretlendirildiğinizden, Batch işleriniz için artık BLOB'lar gerekli bir fikir tooremove her zaman olduğu.</span><span class="sxs-lookup"><span data-stu-id="a52f5-310">Because you are charged for data that resides in Azure Storage, it is always a good idea tooremove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="a52f5-311">İçinde *python_tutorial_client.py*, bu çok sahip üç çağrı yapılır[BlockBlobService.delete_container][py_delete_container]:</span><span class="sxs-lookup"><span data-stu-id="a52f5-311">In *python_tutorial_client.py*, this is done with three calls too[BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="a52f5-312">9. adım: hello işi ve hello havuzu silme</span><span class="sxs-lookup"><span data-stu-id="a52f5-312">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="a52f5-313">Merhaba tarafından oluşturulan istendiğinde toodelete hello iş ve hello havuzu olduğunuz Hello son adımda *python_tutorial_client.py* komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="a52f5-313">In hello final step, you are prompted toodelete hello job and hello pool that were created by hello *python_tutorial_client.py* script.</span></span> <span data-ttu-id="a52f5-314">İşlerin ve görevlerin kendileri için sizden ücret istenmese de, işlem düğümleri için *ücret* istenecektir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-314">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="a52f5-315">Bu nedenle, düğümleri yalnızca gerektiğinde ayırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-315">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="a52f5-316">Kullanılmayan havuzların silinmesi bakım işleminizin bir parçası olabilir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-316">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="a52f5-317">Merhaba BatchServiceClient's [JobOperations] [ py_job] ve [PoolOperations] [ py_pool] her ikisi de olan ilgili silme yöntemleri vardır silme işlemini onaylamak olursa çağrılır:</span><span class="sxs-lookup"><span data-stu-id="a52f5-317">hello BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> <span data-ttu-id="a52f5-318">İşlem kaynaklarının ücretli olduğunu unutmayın; kullanılmayan havuzların silinmesi masrafları azaltacaktır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-318">Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost.</span></span> <span data-ttu-id="a52f5-319">Ayrıca, bir havuzun silinmesinin Bu havuz içindeki tüm işlem düğümlerini siler ve hello havuz silindikten sonra hello düğümlerinde tüm veriler kurtarılamaz olacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a52f5-319">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-sample-script"></a><span data-ttu-id="a52f5-320">Merhaba örnek betiği çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a52f5-320">Run hello sample script</span></span>
<span data-ttu-id="a52f5-321">Merhaba çalıştırdığınızda *python_tutorial_client.py* hello öğretici betikten [kod örneği][github_article_samples], hello konsol çıktısı benzer toohello aşağıdaki verilir.</span><span class="sxs-lookup"><span data-stu-id="a52f5-321">When you run hello *python_tutorial_client.py* script from hello tutorial [code sample][github_article_samples], hello console output is similar toohello following.</span></span> <span data-ttu-id="a52f5-322">Konumunda bir duraklama yoktur `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` hello havuzun işlem düğümleri oluşturulur, başlatıldığından ve hello havuzun görev başlatma hello komutlarda çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="a52f5-322">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while hello pool's compute nodes are created, started, and hello commands in hello pool's start task are executed.</span></span> <span data-ttu-id="a52f5-323">Kullanım hello [Azure portal] [ azure_portal] toomonitor havuzu, işlem düğümleri, işi ve görevleri yürütme sırasında ve sonrasında.</span><span class="sxs-lookup"><span data-stu-id="a52f5-323">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="a52f5-324">Kullanım hello [Azure portal] [ azure_portal] veya hello [Microsoft Azure Storage Gezgini] [ storage_explorer] tooview hello depolama kaynaklarını (kapsayıcılar ve bloblar) Merhaba uygulama tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a52f5-324">Use hello [Azure portal][azure_portal] or hello [Microsoft Azure Storage Explorer][storage_explorer] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

> [!TIP]
> <span data-ttu-id="a52f5-325">Merhaba çalıştırmak *python_tutorial_client.py* hello içinde komut gelen `azure-batch-samples/Python/Batch/article_samples` dizin.</span><span class="sxs-lookup"><span data-stu-id="a52f5-325">Run hello *python_tutorial_client.py* script from within hello `azure-batch-samples/Python/Batch/article_samples` directory.</span></span> <span data-ttu-id="a52f5-326">Merhaba göreli bir yol kullanır `common.helpers` görebilirsiniz için modülü içe aktarma `ImportError: No module named 'common'` bu dizin içinde hello betikten çalıştırmazsanız.</span><span class="sxs-lookup"><span data-stu-id="a52f5-326">It uses a relative path for hello `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run hello script from within this directory.</span></span>
>
>

<span data-ttu-id="a52f5-327">Tipik yürütme süresi **yaklaşık 5-7 dakika** çalıştırdığınızda hello örnek varsayılan yapılandırmasında.</span><span class="sxs-lookup"><span data-stu-id="a52f5-327">Typical execution time is **approximately 5-7 minutes** when you run hello sample in its default configuration.</span></span>

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="a52f5-328">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a52f5-328">Next steps</span></span>
<span data-ttu-id="a52f5-329">Ücretsiz toomake değişiklikleri çok eşitleyerek*python_tutorial_client.py* ve *python_tutorial_task.py* tooexperiment farklı olan işlem senaryoları.</span><span class="sxs-lookup"><span data-stu-id="a52f5-329">Feel free toomake changes too*python_tutorial_client.py* and *python_tutorial_task.py* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="a52f5-330">Örneğin, bir yürütme gecikmesi çok eklemeyi deneyin*python_tutorial_task.py* uzun süre çalışan toosimulate görevler ve bunları hello Portalı'nda izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a52f5-330">For example, try adding an execution delay too*python_tutorial_task.py* toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="a52f5-331">Deneyin daha fazla görev eklemeye veya işlem düğümleri hello sayısını ayarlama.</span><span class="sxs-lookup"><span data-stu-id="a52f5-331">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="a52f5-332">İçin mantığı toocheck eklemek ve varolan bir havuzu toospeed yürütme saati hello kullanılmasına izin verin.</span><span class="sxs-lookup"><span data-stu-id="a52f5-332">Add logic toocheck for and allow hello use of an existing pool toospeed execution time.</span></span>

<span data-ttu-id="a52f5-333">Merhaba temel iş akışı Batch çözümünün ile tanıdık, zaman toodig hello Batch hizmetinin ek özelliklerinin toohello içinde olduğu.</span><span class="sxs-lookup"><span data-stu-id="a52f5-333">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="a52f5-334">Gözden geçirme hello [genel bakış Azure Batch özelliklerine](batch-api-basics.md) yeni toohello hizmeti olup olmadığınızı öneririz makalesi.</span><span class="sxs-lookup"><span data-stu-id="a52f5-334">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="a52f5-335">Başlat'hello altında diğer Batch geliştirmesi makalelerine **geliştirme ayrıntılı** hello içinde [Batch öğrenme yolu][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="a52f5-335">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="a52f5-336">Merhaba toplu ile Merhaba "ilk N sözcük" iş yükünü işlemenin farklı bir uygulama kullanıma [TopNWords] [ github_topnwords] örnek.</span><span class="sxs-lookup"><span data-stu-id="a52f5-336">Check out a different implementation of processing hello "top N words" workload with Batch in hello [TopNWords][github_topnwords] sample.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Azure Depolama’da kapsayıcı oluşturma"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Karşıya yükleme görev uygulamasını ve girdi (veri) toocontainers dosyaları"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Batch havuzu oluşturma"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Batch işi oluşturma"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Görevleri toojob Ekle"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Görevleri izleme"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Depolama’dan görev çıkışını indirme"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Batch çözümü iş akışı (tam diyagram)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Portalda Batch kimlik bilgileri"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Portalda Depolama kimlik bilgileri"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Batch çözümü iş akışı (minimal diyagram)"
