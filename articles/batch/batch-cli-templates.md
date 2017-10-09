---
title: "Azure Batch aaaRun (Önizleme) kod yazmadan uçtan uca iş | Microsoft Docs"
description: "Şablon dosyalarını hello Azure CLI toocreate toplu havuzlar, işler ve görevler için oluşturun."
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="2a543-103">Azure Batch CLI Şablonlarını ve Dosya Aktarımı (Önizleme) özelliğini kullanma</span><span class="sxs-lookup"><span data-stu-id="2a543-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="2a543-104">Hello Azure CLI kullanarak kod yazma olmadan olası toorun toplu işleri değildir.</span><span class="sxs-lookup"><span data-stu-id="2a543-104">Using hello Azure CLI it is possible toorun Batch jobs without writing code.</span></span>

<span data-ttu-id="2a543-105">Şablon dosyaları oluşturulur ve hello Batch havuzları, işleri ve görevleri toobe oluşturulan izin Azure CLI ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a543-105">Template files can be created and used with hello Azure CLI that allow Batch pools, jobs, and tasks toobe created.</span></span> <span data-ttu-id="2a543-106">İş giriş dosyaları karşıdan hello toplu işlem hesabı ve iş çıktısı dosyalarıyla ilişkili hello depolama hesabı kolayca yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="2a543-106">Job input files can be easily uploaded to hello storage account associated with hello Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="2a543-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2a543-107">Overview</span></span>

<span data-ttu-id="2a543-108">Bir uzantı toohello Azure CLI toplu kullanılan toobe uçtan uca geliştiriciler olmayan kullanıcılar tarafından sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a543-108">An extension toohello Azure CLI enables Batch toobe used end-to-end by users who are not developers.</span></span> <span data-ttu-id="2a543-109">Bir havuz oluşturulabilir, işler ve oluşturulan, ilişkili görevler girdi verileri karşıya ve karşıdan – hello elde edilen çıktı verilerini kod gerekmez, CLI hello doğrudan kullanılan veya komut dosyalarına tümleştirilmekte.</span><span class="sxs-lookup"><span data-stu-id="2a543-109">A pool can be created, input data uploaded, jobs and associated tasks created, and hello resulting output data downloaded – no code required, hello CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="2a543-110">Toplu şablonları yapı hello üzerinde [hello Azure CLI mevcut toplu desteği](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) JSON dosyaları hello oluşturulmasını havuzlar, işler, görevler ve diğer öğeleri için toospecify özellik değerlerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="2a543-110">Batch templates build on hello [existing Batch support in hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files toospecify property values for hello creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="2a543-111">Toplu işlem şablonları ile Merhaba aşağıdaki özellikleri hello JSON dosyaları ile olası nedir üzerinden eklendi:</span><span class="sxs-lookup"><span data-stu-id="2a543-111">With Batch templates, hello following capabilities are added over what is possible with hello JSON files:</span></span>

-   <span data-ttu-id="2a543-112">Parametreleri tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2a543-112">Parameters can be defined.</span></span> <span data-ttu-id="2a543-113">Merhaba şablon kullanıldığında, yalnızca hello parametre hello şablon gövdesinde belirtilen diğer öğesi özellik değerleri ile belirtilen toocreate hello öğesi değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="2a543-113">When hello template is used, only hello parameter values are specified toocreate hello item, with other item property values being specified in hello template body.</span></span> <span data-ttu-id="2a543-114">Batch ve uygulamaları toobe Batch tarafından çalıştırma özelliğini algılayan bir kullanıcı, havuz, iş ve görev özellik değerlerini belirterek şablonları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a543-114">A user who understands Batch and the applications toobe run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="2a543-115">Toplu işlem ve/veya uygulamalar bilmiyorsanız daha az bir kullanıcı toospecify hello değerleri hello tanımlanan parametreler için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="2a543-115">A user less familiar with Batch and/or the applications only needs toospecify hello values for hello defined parameters.</span></span>

-   <span data-ttu-id="2a543-116">İş görevi oluşturucuları oluşturun veya pek çok görev tanımları toobe oluşturulan ve önemli ölçüde basitleştirme iş gönderme hello önleme bir iş ile ilgili daha fazla görev gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a543-116">Job task factories create one or more tasks associated with a job, avoiding hello need for many task definitions toobe created and significantly simplifying job submission.</span></span>


<span data-ttu-id="2a543-117">Çıktı veri dosyaları çoğunlukla üretilir ve girdi veri dosyalarını işleri sağlanan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a543-117">Input data files need toobe supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="2a543-118">Varsayılan olarak bir depolama hesabını ilişkili, her Batch ile kolayca aktarılan tooand hiçbir kodlama ile CLI kullanarak bu depolama hesabından hesabı ve dosyaları olabilir ve hiçbir depolama kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a543-118">A storage account is associated, by default, with each Batch account and files can be easily transferred tooand from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="2a543-119">Örneğin, [ffmpeg](http://ffmpeg.org/) , ses ve video dosyaları işler yaygın bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="2a543-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="2a543-120">Hello Azure Batch CLI kullanılan tooinvoke ffmpeg tootranscode kaynak video dosyaları toodifferent çözümleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a543-120">hello Azure Batch CLI can be used tooinvoke ffmpeg tootranscode source video files toodifferent resolutions.</span></span>

-   <span data-ttu-id="2a543-121">Bir havuzu şablonu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2a543-121">A pool template is created.</span></span> <span data-ttu-id="2a543-122">Hello şablon oluşturma hello kullanıcı toocall nasıl hello ffmpeg uygulama ve gereklilikleri bilir; Merhaba belirtin uygun işletim sistemi, VM boyutu nasıl ffmpeg yüklü (bir uygulama paketi veya örneğin bir paket Yöneticisi'ni kullanarak) ve diğer havuz özellik değerleri.</span><span class="sxs-lookup"><span data-stu-id="2a543-122">hello user creating hello template knows how toocall hello ffmpeg application and its requirements; they specify hello appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="2a543-123">Bu nedenle Hello şablon kullanıldığında, yalnızca hello havuzu kimliği ve VM'lerin sayısını belirtilen toobe gerekir parametreleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2a543-123">Parameters are created so when hello template is used, only hello pool id and number of VMs need toobe specified.</span></span>

-   <span data-ttu-id="2a543-124">Bir proje şablonu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2a543-124">A job template is created.</span></span> <span data-ttu-id="2a543-125">Merhaba kullanıcı oluşturma hello şablonu nasıl ffmpeg gereksinimlerini toobe tootranscode kaynak video tooa farklı çözümleme çağrılır ve hello görev komut satırını belirtir bilir; Bunlar, ayrıca her giriş dosyası için gerekli bir görev ile Merhaba kaynak video dosyaları içeren bir klasör olduğunu bilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a543-125">hello user creating hello template knows how ffmpeg needs toobe invoked tootranscode source video tooa different resolution and specifies hello task command line; they also know that there is a folder containing hello source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="2a543-126">Video dosyaları tootranscode kümesi son kullanıcı ilk hello havuzu şablonunu kullanarak, yalnızca hello havuzu kimliği ve gerekli VM'lerin sayısını belirten bir havuz oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2a543-126">An end user with a set of video files tootranscode first creates a pool using hello pool template, specifying only hello pool id and number of VMs required.</span></span> <span data-ttu-id="2a543-127">Ardından hello kaynak dosyaları tootranscode karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a543-127">They can then upload hello source files tootranscode.</span></span> <span data-ttu-id="2a543-128">Bir işi yalnızca hello Havuz kimliği ve karşıya hello kaynak dosyalarının konumunu belirtme hello proje şablonunu kullanarak ardından gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="2a543-128">A job can then be submitted using hello job template, specifying only hello pool id and location of hello source files uploaded.</span></span> <span data-ttu-id="2a543-129">oluşturulan giriş dosya başına tek bir görev Hello toplu iş oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2a543-129">hello Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="2a543-130">Son olarak, hello kod çevrimi çıktı dosyaları karşıdan yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="2a543-130">Finally, hello transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="2a543-131">Yükleme</span><span class="sxs-lookup"><span data-stu-id="2a543-131">Installation</span></span>

<span data-ttu-id="2a543-132">Merhaba şablon ve dosya aktarımı özellikleri yüklü bir uzantı toobe gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2a543-132">hello template and file transfer capabilities require an extension toobe installed.</span></span>

<span data-ttu-id="2a543-133">Yönergeler için nasıl tooinstall hello Azure CLI bkz [Azure CLI 2.0 yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2a543-133">For instructions on how tooinstall hello Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="2a543-134">Azure CLI yüklenmiş bir kez hello hello toplu uzantısı aşağıdaki CLI komutu kullanılarak yüklenebilir:</span><span class="sxs-lookup"><span data-stu-id="2a543-134">Once hello Azure CLI has been installed, hello Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="2a543-135">Merhaba toplu uzantısı hakkında daha fazla bilgi için bkz: [için Microsoft Azure toplu işlem CLI uzantıları Windows, Mac ve Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span><span class="sxs-lookup"><span data-stu-id="2a543-135">For more information about hello Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="2a543-136">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="2a543-136">Templates</span></span>

<span data-ttu-id="2a543-137">Hello Azure Batch CLI havuzlar, işler ve görevler toobe özellik adlarını ve değerlerini içeren bir JSON dosyası belirterek oluşturulan gibi öğeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a543-137">hello Azure Batch CLI allows items such as pools, jobs, and tasks toobe created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="2a543-138">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2a543-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="2a543-139">Azure Batch işlevsellik ve sözdizimi benzer tooAzure Resource Manager şablonları şablonlarıdır.</span><span class="sxs-lookup"><span data-stu-id="2a543-139">Azure Batch templates are similar tooAzure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="2a543-140">Öğe özellik adları ve değerleri içerir, ancak ana kavramlar aşağıdaki hello eklemek JSON dosyaları bunlar:</span><span class="sxs-lookup"><span data-stu-id="2a543-140">They are JSON files that contain item property names and values, but add hello following main concepts:</span></span>

-   <span data-ttu-id="2a543-141">**Parametreler**</span><span class="sxs-lookup"><span data-stu-id="2a543-141">**Parameters**</span></span>

    -   <span data-ttu-id="2a543-142">Yalnızca hello şablon kullanıldığında, sağlanan toobe gerek parametre değerleri ile bir gövde bölümünde belirtilen özellik değerleri toobe izin verir.</span><span class="sxs-lookup"><span data-stu-id="2a543-142">Allow property values toobe specified in a body section, with only parameter values needing toobe supplied when hello template is used.</span></span> <span data-ttu-id="2a543-143">Örneğin, bir havuz için tam tanımı hello hello gövde ve havuzu kimliği için tanımlanan yalnızca bir parametre yerleştirilemedi; yalnızca bir havuz kimliği dizesi, bu nedenle bir havuzu sağlanan toobe toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a543-143">For example, hello complete definition for a pool could be placed in hello body and only one parameter defined for pool id; only a pool id string therefore needs toobe supplied toocreate a pool.</span></span>
        
    -   <span data-ttu-id="2a543-144">Merhaba şablon gövde toplu bilgisine sahip biri tarafından yazılan ve hello uygulamaları toobe Batch tarafından çalıştırın; Merhaba şablon kullanıldığında, yalnızca hello yazar tarafından tanımlanan parametreler için değer sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a543-144">hello template body can be authored by someone with knowledge of Batch and hello applications toobe run by Batch; only values for hello author-defined parameters must be supplied when hello template is used.</span></span> <span data-ttu-id="2a543-145">Merhaba ayrıntılı toplu olmayan bir kullanıcı ve/veya uygulama bilgisi, bu nedenle şablonları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a543-145">A user without hello in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="2a543-146">**Değişkenler**</span><span class="sxs-lookup"><span data-stu-id="2a543-146">**Variables**</span></span>

    -   <span data-ttu-id="2a543-147">Tek bir yerde belirtilen ve hello şablon gövdesi bir veya daha fazla yerde kullanılan basit veya karmaşık parametre değerleri toobe izin verir.</span><span class="sxs-lookup"><span data-stu-id="2a543-147">Allow simple or complex parameter values toobe specified in one place and used in one or more places in hello template body.</span></span> <span data-ttu-id="2a543-148">Değişkenleri basitleştirmek ve hello şablon hello boyutunu yanı daha rahat bir değeri değişebilir konumu toochange özellikleri sağlayarak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="2a543-148">Variables can simplify and reduce hello size of hello template, as well as make it more maintainable by having one location toochange properties whose value may change.</span></span>

-   <span data-ttu-id="2a543-149">**Daha yüksek düzeyli yapıları**</span><span class="sxs-lookup"><span data-stu-id="2a543-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="2a543-150">Bazı daha yüksek düzeyli yapıları hello Batch API'lerini henüz kullanılamıyor hello şablon kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a543-150">Some higher-level constructs are available in hello template that are not yet available in hello Batch APIs.</span></span> <span data-ttu-id="2a543-151">Örneğin, bir görev fabrikası ortak görev tanımı kullanarak hello işi için birden çok görev oluşturur bir proje şablonu içinde tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2a543-151">For example, a task factory can be defined in a job template that creates multiple tasks for hello job using a common task definition.</span></span> <span data-ttu-id="2a543-152">Bu yapıları dinamik olarak görev başına bir dosyayı gibi birden çok JSON dosyası oluşturun yanı sıra betiği örneğin bir paket Yöneticisi üzerinden dosyaları tooinstall uygulamaları oluşturmak için hello gerek toocode kaçının.</span><span class="sxs-lookup"><span data-stu-id="2a543-152">These constructs avoid hello need toocode to dynamically create multiple JSON files, such as one file per task, as well as create script files tooinstall applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="2a543-153">Bazı noktası, geçerli, bu yapıları olabilir toothe Batch hizmetini ve kullanılabilir eklendiği hello Batch API'leri, Uı'lar vb..</span><span class="sxs-lookup"><span data-stu-id="2a543-153">At some point, where applicable, these constructs may be added toothe Batch service and available in hello Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="2a543-154">Havuzu şablonları</span><span class="sxs-lookup"><span data-stu-id="2a543-154">Pool templates</span></span>

<span data-ttu-id="2a543-155">Ayrıca toohello standart şablon özelliklerini parametreler ve değişkenler, daha yüksek düzeyli yapıları aşağıdaki hello hello havuzu şablonu tarafından desteklenir:</span><span class="sxs-lookup"><span data-stu-id="2a543-155">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello pool template:</span></span>

-   <span data-ttu-id="2a543-156">**Paket referanslarını**</span><span class="sxs-lookup"><span data-stu-id="2a543-156">**Package references**</span></span>

    -   <span data-ttu-id="2a543-157">İsteğe bağlı olarak yazılım kopyalanan toobe toopool düğümlere paketini kullanarak yöneticileri izin verir.</span><span class="sxs-lookup"><span data-stu-id="2a543-157">Optionally allows software toobe copied toopool nodes by using package managers.</span></span> <span data-ttu-id="2a543-158">Merhaba Paket Yöneticisi ve paket kimliği belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="2a543-158">hello package manager and package id are specified.</span></span> <span data-ttu-id="2a543-159">Mümkün toodeclare olan bir veya daha fazla paket önler hello gerek toocreate hello gerekli paketleri alır bir komut dosyası, hello komut dosyası yükleyin ve her bir havuz düğümde hello komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2a543-159">Being able toodeclare one or more packages avoids hello need toocreate a script that gets hello required packages, install hello script, and run hello script on each pool node.</span></span>

<span data-ttu-id="2a543-160">bir havuz kimliği dizesi ve hello sayısı VM'ler sağlanan toobe toouse yüklü ve yalnızca Linux VM'ler havuzu ile ffmpeg oluşturan bir şablon örneği gerektirir Hello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2a543-160">hello following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and hello number of VMs toobe supplied toouse:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

<span data-ttu-id="2a543-161">Merhaba şablon dosyası adlandırırsanız _havuzu ffmpeg.json_, hello şablon gibi çağrıldığı sonra:</span><span class="sxs-lookup"><span data-stu-id="2a543-161">If hello template file was named _pool-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="2a543-162">Proje şablonları</span><span class="sxs-lookup"><span data-stu-id="2a543-162">Job templates</span></span>

<span data-ttu-id="2a543-163">Ayrıca toohello standart şablon özelliklerini parametreler ve değişkenler, daha yüksek düzeyli yapıları aşağıdaki hello hello proje şablonu tarafından desteklenir:</span><span class="sxs-lookup"><span data-stu-id="2a543-163">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello job template:</span></span>

-   <span data-ttu-id="2a543-164">**Görev Fabrika**</span><span class="sxs-lookup"><span data-stu-id="2a543-164">**Task factory**</span></span>

    -   <span data-ttu-id="2a543-165">Bir iş için birden çok görevleri bir görev tanımından oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2a543-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="2a543-166">Üç tür görev Fabrika desteklenir – parametrik, dosya başına görev sweep ve görev koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="2a543-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="2a543-167">Merhaba, her kaynak video dosyası oluşturulan bir görev ile ffmpeg kodlamasını MP4 video dosyaları tooone iki alt çözünürlüğü için kullandığı bir işi oluşturan bir şablon örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="2a543-167">hello following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files tooone of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

<span data-ttu-id="2a543-168">Merhaba şablon dosyası adlandırırsanız _iş ffmpeg.json_, hello şablon gibi çağrıldığı sonra:</span><span class="sxs-lookup"><span data-stu-id="2a543-168">If hello template file was named _job-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="2a543-169">Dosya grupları ve dosya aktarımı</span><span class="sxs-lookup"><span data-stu-id="2a543-169">File groups and file transfer</span></span>

<span data-ttu-id="2a543-170">Çoğu işler ve görevler girdi dosyası gerektirir ve çıktı dosyaları üretir.</span><span class="sxs-lookup"><span data-stu-id="2a543-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="2a543-171">Her ikisi de girişi dosyaları ve çıktı dosyaları genellikle hello istemci toohello düğümünden veya hello düğüm toohello istemcisi aktarılan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a543-171">Both input files and output files typically need toobe transferred, either from hello client toohello node, or from hello node toohello client.</span></span> <span data-ttu-id="2a543-172">Hello Azure Batch CLI uzantısı koyma dosya aktarımı soyutlar ve her toplu işlem hesabı için varsayılan olarak oluşturulan hello depolama hesabı kullanır.</span><span class="sxs-lookup"><span data-stu-id="2a543-172">hello Azure Batch CLI extension abstracts away file transfer and utilizes hello storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="2a543-173">Bir dosya grubu hello Azure depolama hesabı oluşturulur tooa kapsayıcı karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="2a543-173">A file group equates tooa container that is created in hello Azure storage account.</span></span> <span data-ttu-id="2a543-174">Merhaba dosya grubu alt klasörleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a543-174">hello file group may have subfolders.</span></span>

<span data-ttu-id="2a543-175">Merhaba toplu CLI uzantısını komutları istemci tooa belirtilen dosya grubu karşıya yükleme dosyalarından ve hello belirtilen dosya grubu tooa istemci yükleme dosyalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a543-175">hello Batch CLI extension provides commands for uploading files from client tooa specified file group and downloading files from hello specified file group tooa client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="2a543-176">Havuz ve proje şablonları havuzu düğümleri üzerine kopyalama için belirtilen dosya grupları toobe depolanan dosyaları izin verin veya havuzu düğümleri tooa dosya grubu yedekleme.</span><span class="sxs-lookup"><span data-stu-id="2a543-176">Pool and job templates allow files stored in file groups toobe specified for copy onto pool nodes or off pool nodes back tooa file group.</span></span> <span data-ttu-id="2a543-177">Örneğin, hello kaynak video dosyalarının üzerine hello düğümü kodlama dönüştürme için aşağı kopyalanan hello konumu olarak daha önce belirtilen iş şablonunda hello dosya grubu "ffmpeg-Giriş" Merhaba görev Fabrika için belirtilir; Merhaba dosya grubu "ffmpeg-output" Hello hello kod çevrimi çıkış dosyalarının nerede konumu kopyalanan her görev çalıştıran toofrom hello düğüm olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a543-177">For example, in the job template specified previously, hello file group “ffmpeg-input” is specified for hello task factory as hello location of hello source video files copied down onto hello node for transcoding; hello file group “ffmpeg-output” is used as hello location where hello transcoded output files are copied toofrom hello node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="2a543-178">Özet</span><span class="sxs-lookup"><span data-stu-id="2a543-178">Summary</span></span>

<span data-ttu-id="2a543-179">Şablon ve dosya aktarımı desteği şu anda eklenmiş yalnızca Azure CLI toohello.</span><span class="sxs-lookup"><span data-stu-id="2a543-179">Template and file transfer support have currently been added only toohello Azure CLI.</span></span> <span data-ttu-id="2a543-180">Merhaba, Araştırmacıları, BT kullanıcıları vb. gibi hello Batch API'lerini kullanarak toodevelop kod gerekmez toplu toousers kullanabilirsiniz tooexpand hello İzleyici hedeftir.</span><span class="sxs-lookup"><span data-stu-id="2a543-180">hello goal is tooexpand hello audience that can use Batch toousers who do not need toodevelop code using hello Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="2a543-181">Kodlama olmadan Azure, toplu ve toplu iş çalıştırmak hello uygulamaları toobe bilgisine sahip kullanıcılar havuzu ve iş oluşturma için şablonlar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a543-181">Without coding, users with knowledge of Azure, Batch, and hello applications toobe run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="2a543-182">Şablon parametreleri ile kullanıcılar toplu işlem ve hello uygulamaların ayrıntılı bilgisi olmadan hello şablonları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a543-182">With template parameters, users without detailed knowledge of Batch and hello applications can use hello templates.</span></span>

<span data-ttu-id="2a543-183">Merhaba hello Azure CLI için toplu uzantısı denemek ve bu makalenin veya hello aracılığıyla ya da hello yorumlarını bize herhangi bir geri bildirim veya öneriler, sağlayın [Azure Batch forumunu](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span><span class="sxs-lookup"><span data-stu-id="2a543-183">Try out hello Batch extension for hello Azure CLI and provide us with any feedback or suggestions, either in hello comments for this article or via hello [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a543-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a543-184">Next steps</span></span>

- <span data-ttu-id="2a543-185">Merhaba toplu şablonları blog gönderisi bkz: [çalışan Azure Batch işleri kullanarak hello Azure CLI – gerekli kod](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span><span class="sxs-lookup"><span data-stu-id="2a543-185">See hello Batch templates blog post: [Running Azure Batch jobs using hello Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="2a543-186">Ayrıntılı Kurulum ve kullanım belgeler, örnekler ve kaynak kodu hello kullanılabilir [Azure GitHub deposunu](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="2a543-186">Detailed installation and usage documentation, samples, and source code are available in hello [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
