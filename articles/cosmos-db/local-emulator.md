---
title: "hello Azure Cosmos DB öykünücü ile yerel olarak aaaDevelop | Microsoft Docs"
description: "Hello Azure Cosmos DB öykünücüsü kullanarak, geliştirmek ve uygulamanızı yerel olarak ücretsiz, Azure aboneliği oluşturmadan test edin."
services: cosmos-db
documentationcenter: 
keywords: "Azure Cosmos DB öykünücüsü"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="b0e6b-104">Hello Azure Cosmos DB öykünücüsü yerel geliştirme ve test amacıyla kullanın</span><span class="sxs-lookup"><span data-stu-id="b0e6b-104">Use hello Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="b0e6b-105"><strong>İkili dosyalar</strong></span><span class="sxs-lookup"><span data-stu-id="b0e6b-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="b0e6b-106">MSI indirin</span><span class="sxs-lookup"><span data-stu-id="b0e6b-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="b0e6b-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="b0e6b-108">Docker hub'a</span><span class="sxs-lookup"><span data-stu-id="b0e6b-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-109"><strong>Docker kaynak</strong></span><span class="sxs-lookup"><span data-stu-id="b0e6b-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="b0e6b-110">Github</span><span class="sxs-lookup"><span data-stu-id="b0e6b-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="b0e6b-111">Hello Azure Cosmos DB öykünücüsü hello Azure Cosmos DB hizmeti Geliştirme amaçlı öykünen yerel bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-111">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="b0e6b-112">Hello Azure Cosmos DB öykünücüsü kullanarak, geliştirmek ve bir Azure aboneliği oluşturmak veya herhangi bir maliyet olmadan uygulamanızı yerel olarak test etmek.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-112">Using hello Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="b0e6b-113">Uygulamanızı hello Azure Cosmos DB öykünücüsü nasıl çalıştığını ile memnun kaldığınızda, toousing hello buluttaki bir Azure Cosmos DB hesabını geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-113">When you're satisfied with how your application is working in hello Azure Cosmos DB Emulator, you can switch toousing an Azure Cosmos DB account in hello cloud.</span></span>

<span data-ttu-id="b0e6b-114">Bu makalede görevleri aşağıdaki hello yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="b0e6b-114">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="b0e6b-115">Merhaba öykünücüsü yükleme</span><span class="sxs-lookup"><span data-stu-id="b0e6b-115">Installing hello Emulator</span></span>
> * <span data-ttu-id="b0e6b-116">Merhaba öykünücüsü için Docker Windows üzerinde çalışan</span><span class="sxs-lookup"><span data-stu-id="b0e6b-116">Running hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="b0e6b-117">Kimlik doğrulama istekleri</span><span class="sxs-lookup"><span data-stu-id="b0e6b-117">Authenticating requests</span></span>
> * <span data-ttu-id="b0e6b-118">Merhaba öykünücüsü Hello Veri Gezgini kullanma</span><span class="sxs-lookup"><span data-stu-id="b0e6b-118">Using hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="b0e6b-119">SSL sertifikaları verme</span><span class="sxs-lookup"><span data-stu-id="b0e6b-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="b0e6b-120">Merhaba öykünücüsü hello komut satırından çağırma</span><span class="sxs-lookup"><span data-stu-id="b0e6b-120">Calling hello Emulator from hello command line</span></span>
> * <span data-ttu-id="b0e6b-121">İzleme dosyaları toplama</span><span class="sxs-lookup"><span data-stu-id="b0e6b-121">Collecting trace files</span></span>

<span data-ttu-id="b0e6b-122">Burada tooget hello Azure Cosmos DB öykünücü ile çalışmaya nasıl Kirill Gavrylyuk gösterir video, aşağıdaki hello izleyerek çalışmaya başlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-122">We recommend getting started by watching hello following video, where Kirill Gavrylyuk shows how tooget started with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="b0e6b-123">Merhaba video toohello öykünücüsü DocumentDB öykünücüsü hello başvuruyor, ancak hello aracı kendisini yeniden adlandırıldı Not hello Azure Cosmos DB öykünücüsü hello video basmaya itibaren.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-123">Note that hello video refers toohello emulator as hello DocumentDB Emulator, but hello tool itself has been renamed hello Azure Cosmos DB Emulator since taping hello video.</span></span> <span data-ttu-id="b0e6b-124">Merhaba video tüm bilgileri hello Azure Cosmos DB öykünücüsü hala doğru olur.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-124">All information in hello video is still accurate for hello Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a><span data-ttu-id="b0e6b-125">Merhaba öykünücüsü nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="b0e6b-125">How hello Emulator works</span></span>
<span data-ttu-id="b0e6b-126">Hello Azure Cosmos DB öykünücüsü hello Azure Cosmos DB hizmeti, yüksek doğruluk öykünme sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-126">hello Azure Cosmos DB Emulator provides a high-fidelity emulation of hello Azure Cosmos DB service.</span></span> <span data-ttu-id="b0e6b-127">Azure Cosmos JSON belgelerini sorgulamak için destek dahil olmak üzere sağlama DB olarak aynı işlevselliği destekler ve koleksiyonları ölçekleme ve yürütme yordamları ve Tetikleyicileri depolanır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="b0e6b-128">Geliştirme ve hello Azure Cosmos DB öykünücüsü kullanarak uygulamaları test etme ve bunları yalnızca tek bir yapılandırma için Azure Cosmos DB toohello bağlantı uç noktasının değişikliği yaparak küresel ölçekli tooAzure dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-128">You can develop and test applications using hello Azure Cosmos DB Emulator, and deploy them tooAzure at global scale by just making a single configuration change toohello connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="b0e6b-129">Yüksek kaliteli yerel öykünme hello gerçek Azure Cosmos DB hizmetinin oluşturduğumuz olsa da, hello hello Azure Cosmos DB öykünücüsü hello hizmeti farklı uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-129">While we created a high-fidelity local emulation of hello actual Azure Cosmos DB service, hello implementation of hello Azure Cosmos DB Emulator is different than that of hello service.</span></span> <span data-ttu-id="b0e6b-130">Örneğin, hello Azure Cosmos DB öykünücüsü hello yerel dosya sistemi gibi standart işletim sistemi bileşenlerini kalıcılığını ve HTTPS protokol yığını bağlantısı için kullanır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-130">For example, hello Azure Cosmos DB Emulator uses standard OS components such as hello local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="b0e6b-131">Bu genel çoğaltma, okuma/yazma ve ince ayarlanabilir tutarlılık düzeyleri için tek basamaklı milisaniyelik gecikme süresi yok gibi hello Azure Cosmos DB öykünücüsü kullanılabilir Azure altyapı dayanan bazı işlevler anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via hello Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="b0e6b-132">Merhaba bu zaman hello Veri Gezgini adresindeki öykünücüsü yalnızca DocumentDB API koleksiyonları ve MongoDB koleksiyonları hello oluşturmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-132">At this time hello Data Explorer in hello emulator only supports hello creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="b0e6b-133">Merhaba öykünücüsü Hello Veri Gezgini hello oluşturulmasını tablolar ve grafikler şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-133">hello Data Explorer in hello emulator does not currently support hello creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="b0e6b-134">Sistem gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="b0e6b-134">System requirements</span></span>
<span data-ttu-id="b0e6b-135">Hello Azure Cosmos DB öykünücüsü hello donanım ve yazılım gereksinimlerine sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b0e6b-135">hello Azure Cosmos DB Emulator has hello following hardware and software requirements:</span></span>

* <span data-ttu-id="b0e6b-136">Yazılım gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="b0e6b-136">Software requirements</span></span>
  * <span data-ttu-id="b0e6b-137">Windows Server 2012 R2, Windows Server 2016 veya Windows 10</span><span class="sxs-lookup"><span data-stu-id="b0e6b-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="b0e6b-138">En düşük donanım gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="b0e6b-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="b0e6b-139">2 GB RAM</span><span class="sxs-lookup"><span data-stu-id="b0e6b-139">2 GB RAM</span></span>
  * <span data-ttu-id="b0e6b-140">10 GB kullanılabilir sabit disk alanı</span><span class="sxs-lookup"><span data-stu-id="b0e6b-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="b0e6b-141">Yükleme</span><span class="sxs-lookup"><span data-stu-id="b0e6b-141">Installation</span></span>
<span data-ttu-id="b0e6b-142">İndirip hello Azure Cosmos DB öykünücüsü hello yükleyin [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-142">You can download and install hello Azure Cosmos DB Emulator from hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="b0e6b-143">tooinstall, yapılandırma ve hello Azure Cosmos DB öykünücüsü çalıştırma, hello bilgisayar üzerinde yönetici ayrıcalıklarına sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-143">tooinstall, configure, and run hello Azure Cosmos DB Emulator, you must have administrative privileges on hello computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="b0e6b-144">Windows için Docker çalışan</span><span class="sxs-lookup"><span data-stu-id="b0e6b-144">Running on Docker for Windows</span></span>

<span data-ttu-id="b0e6b-145">Windows için Docker Hello Azure Cosmos DB öykünücüsü çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-145">hello Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="b0e6b-146">Merhaba öykünücüsü, Oracle Linux için Docker üzerinde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-146">hello Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="b0e6b-147">Bulduktan sonra [Windows için Docker](https://www.docker.com/docker-windows) yüklü, hello öykünücü görüntünüzün Docker hub'dan sık kullanılan kabuğundan komutu aşağıdaki hello çalıştırarak çekebilir (cmd.exe, PowerShell, vs.).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull hello Emulator image from Docker Hub by running hello following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="b0e6b-148">toostart hello resim, hello aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-148">toostart hello image, run hello following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="b0e6b-149">Merhaba yanıt benzer toohello aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="b0e6b-149">hello response looks similar toohello following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="b0e6b-150">Öykünücü başlatıldı hello sonra kapatma hello öykünücüsü'nın kapsayıcı hello etkileşimli Kabuk kapatılıyor.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-150">Closing hello interactive shell once hello Emulator has been started will shutdown hello Emulator’s container.</span></span>

<span data-ttu-id="b0e6b-151">Hello uç noktası ve ana anahtarından içinde hello yanıt, istemci kullanın ve ana bilgisayara hello SSL sertifikasını içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-151">Use hello endpoint and master key in from hello response in your client and import hello SSL certificate into your host.</span></span> <span data-ttu-id="b0e6b-152">tooimport hello SSL sertifikası hello bir yönetici komut isteminden aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="b0e6b-152">tooimport hello SSL certificate, do hello following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a><span data-ttu-id="b0e6b-153">Başlangıç hello öykünücüsü</span><span class="sxs-lookup"><span data-stu-id="b0e6b-153">Start hello Emulator</span></span>

<span data-ttu-id="b0e6b-154">toostart hello Azure Cosmos DB öykünücüsü hello Başlat düğmesine basın veya hello Windows tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-154">toostart hello Azure Cosmos DB Emulator, select hello Start button or press hello Windows key.</span></span> <span data-ttu-id="b0e6b-155">Yazmaya başlayın **Azure Cosmos DB öykünücüsü**ve uygulamaları hello listesinden seçim hello öykünücüsü.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-155">Begin typing **Azure Cosmos DB Emulator**, and select hello emulator from hello list of applications.</span></span> 

![Hello Başlat düğmesine veya tuşuna hello Windows anahtarını seçin, yazmaya başlayın ** Azure Cosmos DB öykünücüsü ** ve uygulamaları hello listesinden seçim hello öykünücüsü](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="b0e6b-157">Merhaba öykünücüsü çalıştırırken hello Windows görev çubuğundaki bildirim alanında bir simge görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-157">When hello emulator is running, you'll see an icon in hello Windows taskbar notification area.</span></span> ![Azure Cosmos DB yerel öykünücüsü görev çubuğu bildirim](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="b0e6b-159">Varsayılan olarak Azure Cosmos DB öykünücüsü Hello 8081 numaralı bağlantı noktasını dinlemeye hello yerel makine ("localhost") çalışır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-159">hello Azure Cosmos DB Emulator by default runs on hello local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="b0e6b-160">Hello Azure Cosmos DB öykünücüsü tarafından varsayılan toohello yüklü `C:\Program Files\Azure Cosmos DB Emulator` dizin.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-160">hello Azure Cosmos DB Emulator is installed by default toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="b0e6b-161">Ayrıca, başlatma ve durdurma hello komut satırı hello öykünücüsünden.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-161">You can also start and stop hello emulator from hello command-line.</span></span> <span data-ttu-id="b0e6b-162">Bkz: [komut satırı aracını referans](#command-line) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="b0e6b-163">Veri Gezgini'ni başlatın</span><span class="sxs-lookup"><span data-stu-id="b0e6b-163">Start Data Explorer</span></span>

<span data-ttu-id="b0e6b-164">Hello Azure Cosmos DB öykünücüsü başlattığında, hello Azure Cosmos DB Data Explorer tarayıcınızda otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-164">When hello Azure Cosmos DB emulator launches it will automatically open hello Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="b0e6b-165">Başlangıç adresi olarak görünür [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-165">hello address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="b0e6b-166">Hello explorer kapatıp toore açık ister misiniz varsa, daha sonra hello URL tarayıcınızda açın ya da aşağıda gösterildiği gibi hello Windows Tepsi simgesi hello Azure Cosmos DB öykünücüsü'nden başlatın.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-166">If you close hello explorer and would like toore-open it later, you can either open hello URL in your browser or launch it from hello Azure Cosmos DB Emulator in hello Windows Tray Icon as shown below.</span></span>

![Azure Cosmos DB yerel öykünücüsü Veri Gezgini Başlatıcısı](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="b0e6b-168">Güncelleştirmeleri denetleme</span><span class="sxs-lookup"><span data-stu-id="b0e6b-168">Checking for updates</span></span>
<span data-ttu-id="b0e6b-169">Veri Gezgini indirme için kullanılabilir yeni bir güncelleştirme olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="b0e6b-170">Hello Azure Cosmos DB öykünücüsü bir sürümünde oluşturulan veri toobe erişilebilir farklı bir sürümünü kullanırken garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-170">Data created in one version of hello Azure Cosmos DB Emulator is not guaranteed toobe accessible when using a different version.</span></span> <span data-ttu-id="b0e6b-171">Hello uzun süreli verilerinizi toopersist gerekiyorsa, bu verileri Azure Cosmos DB hesabı yerine hello Azure Cosmos DB öykünücüsü depolamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-171">If you need toopersist your data for hello long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in hello Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="b0e6b-172">Kimlik doğrulama istekleri</span><span class="sxs-lookup"><span data-stu-id="b0e6b-172">Authenticating requests</span></span>
<span data-ttu-id="b0e6b-173">Gibi hello bulutta Azure Cosmos DB ile Azure Cosmos DB öykünücüsü hello karşı yaptığınız her isteğin kimliğinin doğrulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-173">Just as with Azure Cosmos DB in hello cloud, every request that you make against hello Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="b0e6b-174">Hello Azure Cosmos DB öykünücüsü ana anahtar kimlik doğrulaması için tek bir sabit hesap ve bilinen bir kimlik doğrulama anahtarı destekler.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-174">hello Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="b0e6b-175">Bu hesabı ve anahtarı hello Azure Cosmos DB öykünücü ile kullanmak için izin verilen hello yalnızca kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-175">This account and key are hello only credentials permitted for use with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="b0e6b-176">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="b0e6b-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="b0e6b-177">Merhaba ana hello Azure Cosmos DB öykünücüsü tarafından desteklenen anahtar yalnızca hello öykünücü ile kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-177">hello master key supported by hello Azure Cosmos DB Emulator is intended for use only with hello emulator.</span></span> <span data-ttu-id="b0e6b-178">Üretim Azure Cosmos DB hesabı ve anahtarı hello Azure Cosmos DB öykünücü ile kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-178">You cannot use your production Azure Cosmos DB account and key with hello Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="b0e6b-179">Merhaba /Key seçeneği ile Merhaba öykünücüsü başlattıysanız yerine hello oluşturulan anahtarı kullanın "C2y6yDjf5/R, ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="</span><span class="sxs-lookup"><span data-stu-id="b0e6b-179">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="b0e6b-180">Ayrıca, yalnızca hello Azure Cosmos DB hizmeti, hello Azure Cosmos DB öykünücüsü yalnızca desteklediği SSL üzerinden iletişimi güvenli hale getirin.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-180">Additionally, just as hello Azure Cosmos DB service, hello Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-hello-emulator-on-a-local-network"></a><span data-ttu-id="b0e6b-181">Yerel bir ağda Hello öykünücüsünün çalışır</span><span class="sxs-lookup"><span data-stu-id="b0e6b-181">Running hello emulator on a local network</span></span>

<span data-ttu-id="b0e6b-182">Yerel bir ağda hello öykünücüsü çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-182">You can run hello emulator on a local network.</span></span> <span data-ttu-id="b0e6b-183">tooenable ağ erişimi, hello /AllowNetworkAccess hello tasarrufunda belirtin [komut satırı](#command-line-syntax), gerektiren /Key belirttiğiniz = key_string veya/keyfile dosya_adı =.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-183">tooenable network access, specify hello /AllowNetworkAccess option at hello [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="b0e6b-184">/GenKeyFile kullanabileceğiniz dosya_adı toogenerate bir dosya önceden rastgele bir anahtar ile =.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-184">You can use /GenKeyFile=file_name toogenerate a file with a random key upfront.</span></span>  <span data-ttu-id="b0e6b-185">Bu çok/KeyFile geçirebilirsiniz sonra dosya_adı veya /Key = contents_of_file =.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-185">Then you can pass that too/KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="b0e6b-186">tooenable ağ erişimi hello ilk hello kullanıcı için kapatma hello öykünücüsü gerekir ve hello öykünücüsü'nın veri dizini (C:\Users\user_name\AppData\Local\CosmosDBEmulator) silin.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-186">tooenable network access for hello first time hello user should shutdown hello emulator and delete hello emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-hello-emulator"></a><span data-ttu-id="b0e6b-187">Merhaba öykünücü ile geliştirme</span><span class="sxs-lookup"><span data-stu-id="b0e6b-187">Developing with hello Emulator</span></span>
<span data-ttu-id="b0e6b-188">Masaüstünde çalışan Azure Cosmos DB öykünücüsü sahip hello sonra herhangi bir desteklenen kullanabilirsiniz [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) veya hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract hello öykünücü ile.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-188">Once you have hello Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract with hello Emulator.</span></span> <span data-ttu-id="b0e6b-189">Hello Azure Cosmos DB öykünücüsü de hello DocumentDB ve MongoDB API'ları ve görünüm için koleksiyonları oluşturun ve herhangi bir kod yazmak zorunda kalmadan belgeleri düzenlemesine olanak sağlayan yerleşik bir Veri Gezgini içerir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-189">hello Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for hello DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="b0e6b-190">Kullanıyorsanız, [MongoDB için protokol desteği Azure Cosmos DB](mongodb-introduction.md), Lütfen bağlantı dizesini izleyen hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="b0e6b-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use hello following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="b0e6b-191">Var olan araçlarla kullanabilirsiniz [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB öykünücüsü.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="b0e6b-192">Ayrıca hello Azure Cosmos DB öykünücüsü ve hello kullanarak hello Azure Cosmos DB hizmeti arasında verileri geçirebilirsiniz [Azure Cosmos DB veri geçiş aracı](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-192">You can also migrate data between hello Azure Cosmos DB Emulator and hello Azure Cosmos DB service using hello [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="b0e6b-193">Merhaba /Key seçeneği ile Merhaba öykünücüsü başlattıysanız yerine hello oluşturulan anahtarı kullanın "C2y6yDjf5/R, ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="</span><span class="sxs-lookup"><span data-stu-id="b0e6b-193">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="b0e6b-194">Hello Azure Cosmos DB öykünücüsü, varsayılan olarak kullanarak, too25 tek bölüm koleksiyonları veya 1 bölümlenmiş koleksiyon oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-194">Using hello Azure Cosmos DB emulator, by default, you can create up too25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="b0e6b-195">Bu değer değiştirme hakkında daha fazla bilgi için bkz: [ayar hello PartitionCount değeri](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-195">For more information about changing this value, see [Setting hello PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-hello-ssl-certificate"></a><span data-ttu-id="b0e6b-196">Merhaba SSL sertifikasını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="b0e6b-196">Export hello SSL certificate</span></span>

<span data-ttu-id="b0e6b-197">.NET dilleri ile çalışma zamanı kullanmak hello Windows sertifika deposunda toosecurely toohello Azure Cosmos DB yerel öykünücüsü bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-197">.NET languages and runtime use hello Windows Certificate Store toosecurely connect toohello Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="b0e6b-198">Diğer diller yönetme ve sertifikaları kullanarak kendi yöntemi vardır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="b0e6b-199">Java kullanan kendi [sertifika deposu](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) Python kullanırken [yuva sarmalayıcıları](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="b0e6b-200">Sipariş tooobtain sertifika toouse diller ve Windows sertifika deposunda hello ile entegre değil çalışma zamanları ile Merhaba Windows Sertifika Yöneticisi'ni kullanarak tooexport gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-200">In order tooobtain a certificate toouse with languages and runtimes that do not integrate with hello Windows Certificate Store you will need tooexport it using hello Windows Certificate Manager.</span></span> <span data-ttu-id="b0e6b-201">Başlatılsın certlm.msc çalıştırarak ya da hello adım adım yönergeleri izleyin [hello Azure Cosmos DB öykünücüsü sertifikaları verin](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-201">You can start it by running certlm.msc or follow hello step by step instructions in [Export hello Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="b0e6b-202">Merhaba Sertifika Yöneticisi'ni çalışır duruma geldiğinde BASE-64 kodlanmış X.509 (.cer) dosyası olarak açık hello kişisel aşağıda gösterildiği gibi sertifikaları ve dışarı aktarma hello kolay adı "DocumentDBEmulatorCertificate" sertifikasıyla hello.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-202">Once hello certificate manager is running, open hello Personal Certificates as shown below and export hello certificate with hello friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Azure Cosmos DB yerel öykünücüsü SSL sertifikası](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="b0e6b-204">Merhaba X.509 sertifikası alınabilir hello Java sertifika deposuna hello yönergeleri takip ederek [sertifika toohello Java CA deposuna sertifika ekleme](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-204">hello X.509 certificate can be imported into hello Java certificate store by following hello instructions in [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="b0e6b-205">Merhaba sertifika hello sertifika deposuna içeri aktarıldığında, Java ve MongoDB uygulamalar mümkün tooconnect toohello Azure Cosmos DB öykünücüsü olur.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-205">Once hello certificate is imported into hello certificate store, Java and MongoDB applications will be able tooconnect toohello Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="b0e6b-206">Toohello öykünücüsü Python ve Node.js SDK'ları bağlanırken SSL doğrulama devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-206">When connecting toohello emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="b0e6b-207"><a id="command-line"></a>Komut satırı aracı başvurusu</span><span class="sxs-lookup"><span data-stu-id="b0e6b-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="b0e6b-208">Hello yükleme konumundan hello komut satırı toostart kullanın ve hello öykünücüsü durdurmak, seçeneklerini yapılandırmak ve diğer işlemleri gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-208">From hello installation location, you can use hello command-line toostart and stop hello emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="b0e6b-209">Komut satırı sözdizimi</span><span class="sxs-lookup"><span data-stu-id="b0e6b-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="b0e6b-210">Seçenekler, türü tooview hello listesinde `CosmosDB.Emulator.exe /?` hello komut isteminde.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-210">tooview hello list of options, type `CosmosDB.Emulator.exe /?` at hello command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="b0e6b-211"><strong>Seçeneği</strong></span><span class="sxs-lookup"><span data-stu-id="b0e6b-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="b0e6b-212"><strong>Açıklama</strong></span><span class="sxs-lookup"><span data-stu-id="b0e6b-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="b0e6b-213"><strong>Komutu</strong></span><span class="sxs-lookup"><span data-stu-id="b0e6b-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="b0e6b-214"><strong>Bağımsız değişkenler</strong></span><span class="sxs-lookup"><span data-stu-id="b0e6b-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-215">[Bağımsız değişkenler]</span><span class="sxs-lookup"><span data-stu-id="b0e6b-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="b0e6b-216">Hello Azure Cosmos DB öykünücüsü varsayılan ayarlarla başlatır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-216">Starts up hello Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="b0e6b-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="b0e6b-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-218">[Help]</span><span class="sxs-lookup"><span data-stu-id="b0e6b-218">[Help]</span></span></td>
  <td><span data-ttu-id="b0e6b-219">Merhaba listesini görüntüler komut satırı bağımsız değişkenleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-219">Displays hello list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="b0e6b-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="b0e6b-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-221">kapatma</span><span class="sxs-lookup"><span data-stu-id="b0e6b-221">Shutdown</span></span></td>
  <td><span data-ttu-id="b0e6b-222">Hello Azure Cosmos DB öykünücüsü kapatır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-222">Shuts down hello Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="b0e6b-223">CosmosDB.Emulator.exe Shutdown</span><span class="sxs-lookup"><span data-stu-id="b0e6b-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-224">DataPath</span><span class="sxs-lookup"><span data-stu-id="b0e6b-224">DataPath</span></span></td>
  <td><span data-ttu-id="b0e6b-225">Hangi toostore veri dosyalarında Hello yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-225">Specifies hello path in which toostore data files.</span></span> <span data-ttu-id="b0e6b-226">% LocalAppdata%\CosmosDBEmulator varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="b0e6b-227">CosmosDB.Emulator.exe /DataPath =&lt;datapath&gt;</span><span class="sxs-lookup"><span data-stu-id="b0e6b-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="b0e6b-228">&lt;DataPath&gt;: erişilebilir yolu</span><span class="sxs-lookup"><span data-stu-id="b0e6b-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-229">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="b0e6b-229">Port</span></span></td>
  <td><span data-ttu-id="b0e6b-230">Başlangıç bağlantı noktası numarası toouse hello öykünücüsü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-230">Specifies hello port number toouse for hello emulator.</span></span>  <span data-ttu-id="b0e6b-231">8081 varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="b0e6b-232">CosmosDB.Emulator.exe Port =&lt;bağlantı noktası&gt;</span><span class="sxs-lookup"><span data-stu-id="b0e6b-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="b0e6b-233">&lt;bağlantı noktası&gt;: tek bir bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="b0e6b-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="b0e6b-234">MongoPort</span></span></td>
  <td><span data-ttu-id="b0e6b-235">API MongoDB uyumluluk için başlangıç bağlantı noktası numarası toouse belirtir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-235">Specifies hello port number toouse for MongoDB compatibility API.</span></span> <span data-ttu-id="b0e6b-236">Varsayılandır 10255 değerini bulur.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="b0e6b-237">CosmosDB.Emulator.exe /MongoPort =&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="b0e6b-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="b0e6b-238">&lt;mongoport&gt;: tek bir bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="b0e6b-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="b0e6b-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="b0e6b-240">Doğrudan bağlantı için bağlantı noktalarını toouse Hello belirtir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-240">Specifies hello ports toouse for direct connectivity.</span></span> <span data-ttu-id="b0e6b-241">Varsayılan 10251,10252,10253,10254 olur.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="b0e6b-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="b0e6b-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="b0e6b-243">&lt;directports&gt;: 4 bağlantı noktalarının virgülle ayrılmış listesi</span><span class="sxs-lookup"><span data-stu-id="b0e6b-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-244">Anahtar</span><span class="sxs-lookup"><span data-stu-id="b0e6b-244">Key</span></span></td>
  <td><span data-ttu-id="b0e6b-245">Merhaba öykünücüsü için yetkilendirme anahtar.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-245">Authorization key for hello emulator.</span></span> <span data-ttu-id="b0e6b-246">Anahtar hello bir 64 baytlık vektör 64 tabanlı kodlama olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-246">Key must be hello base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="b0e6b-247">CosmosDB.Emulator.exe /Key:&lt;anahtarı&gt;</span><span class="sxs-lookup"><span data-stu-id="b0e6b-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="b0e6b-248">&lt;anahtar&gt;: anahtarı bir 64 baytlık vektör base-64 hello kodlaması olması gerekir</span><span class="sxs-lookup"><span data-stu-id="b0e6b-248">&lt;key&gt;: Key must be hello base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="b0e6b-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="b0e6b-250">Davranış sınırlama istek hızı etkinleştirilip etkinleştirilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="b0e6b-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="b0e6b-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="b0e6b-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="b0e6b-253">Davranış sınırlama istek hızı devre dışı belirtir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="b0e6b-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="b0e6b-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-255">Nouı</span><span class="sxs-lookup"><span data-stu-id="b0e6b-255">NoUI</span></span></td>
  <td><span data-ttu-id="b0e6b-256">Merhaba öykünücüsü kullanıcı arabirimi gösterme.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-256">Do not show hello emulator user interface.</span></span></td>
  <td><span data-ttu-id="b0e6b-257">CosmosDB.Emulator.exe/nouı</span><span class="sxs-lookup"><span data-stu-id="b0e6b-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="b0e6b-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="b0e6b-259">Belge Gezgini başlatma sırasında gösterme.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="b0e6b-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="b0e6b-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-261">bölüm sayısı</span><span class="sxs-lookup"><span data-stu-id="b0e6b-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="b0e6b-262">Bölümlenmiş koleksiyonlar Hello sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-262">Specifies hello maximum number of partitioned collections.</span></span> <span data-ttu-id="b0e6b-263">Bkz: [değiştirme koleksiyonları hello sayısı](#set-partitioncount) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-263">See [Change hello number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="b0e6b-264">CosmosDB.Emulator.exe /PartitionCount =&lt;bölüm sayısı&gt;</span><span class="sxs-lookup"><span data-stu-id="b0e6b-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="b0e6b-265">&lt;bölüm sayısı&gt;: maksimum sayısı, izin verilen tek bölüm koleksiyonları.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="b0e6b-266">Varsayılan 25'tir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-266">Default is 25.</span></span> <span data-ttu-id="b0e6b-267">İzin verilen en fazla 250'dir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="b0e6b-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="b0e6b-269">Merhaba varsayılan bölümlendirilmiş bir koleksiyon için bölüm sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-269">Specifies hello default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="b0e6b-270">CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="b0e6b-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="b0e6b-271">&lt;defaultpartitioncount&gt; 25 varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="b0e6b-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="b0e6b-273">Etkinleştirir toohello öykünücüsü bir ağ üzerinden erişir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-273">Enables access toohello emulator over a network.</span></span> <span data-ttu-id="b0e6b-274">/Key geçmesi gereken =&lt;key_string&gt; veya/keyfile =&lt;dosya_adı&gt; tooenable ağ erişimi.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; tooenable network access.</span></span></td>
  <td><span data-ttu-id="b0e6b-275">CosmosDB.Emulator.exe AllowNetworkAccess /Key =&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="b0e6b-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="b0e6b-276">or</span><span class="sxs-lookup"><span data-stu-id="b0e6b-276">or</span></span><br><br><span data-ttu-id="b0e6b-277">CosmosDB.Emulator.exe /AllowNetworkAccess/keyfile =&lt;dosya_adı&gt;</span><span class="sxs-lookup"><span data-stu-id="b0e6b-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="b0e6b-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="b0e6b-279">/AllowNetworkAccess kullanıldığında, güvenlik duvarı kurallarını ayarlama.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="b0e6b-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="b0e6b-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="b0e6b-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="b0e6b-282">Yeni bir yetkilendirme anahtar oluşturmak ve toohello belirtilen dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-282">Generate a new authorization key and save toohello specified file.</span></span> <span data-ttu-id="b0e6b-283">oluşturulan başlangıç anahtarı hello /Key veya/keyfile seçenekleriyle kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-283">hello generated key can be used with hello /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="b0e6b-284">CosmosDB.Emulator.exe /GenKeyFile =&lt;yol tookey dosyası&gt;</span><span class="sxs-lookup"><span data-stu-id="b0e6b-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path tookey file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-285">Tutarlılık</span><span class="sxs-lookup"><span data-stu-id="b0e6b-285">Consistency</span></span></td>
  <td><span data-ttu-id="b0e6b-286">Merhaba varsayılan tutarlılık düzeyi hello hesabı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-286">Set hello default consistency level for hello account.</span></span></td>
  <td><span data-ttu-id="b0e6b-287">CosmosDB.Emulator.exe /Consistency =&lt;tutarlılık&gt;</span><span class="sxs-lookup"><span data-stu-id="b0e6b-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="b0e6b-288">&lt;Tutarlılık&gt;: değer hello aşağıdakilerden biri olması gerekir [tutarlılık düzeylerini](consistency-levels.md): oturum, güçlü, Eventual veya BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-288">&lt;consistency&gt;: Value must be one of hello following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="b0e6b-289">Oturum Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-289">hello default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b0e6b-290">?</span><span class="sxs-lookup"><span data-stu-id="b0e6b-290">?</span></span></td>
  <td><span data-ttu-id="b0e6b-291">Merhaba Yardım iletisi göster.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-291">Show hello help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="b0e6b-292">Hello Azure Cosmos DB öykünücüsü ve Azure Cosmos DB arasındaki farklar</span><span class="sxs-lookup"><span data-stu-id="b0e6b-292">Differences between hello Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="b0e6b-293">Hello Azure Cosmos DB öykünücüsü yerel geliştirici istasyonunda çalıştıran benzetilmiş bir ortam sağladığından, bazı arasındaki işlevsel farklılıklar hello öykünücüsü ve bir Azure Cosmos DB hesap hello bulutta vardır:</span><span class="sxs-lookup"><span data-stu-id="b0e6b-293">Because hello Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between hello emulator and an Azure Cosmos DB account in hello cloud:</span></span>

* <span data-ttu-id="b0e6b-294">yalnızca tek bir sabit hesap ve bilinen bir ana anahtar Hello Azure Cosmos DB öykünücüsü destekler.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-294">hello Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="b0e6b-295">Anahtarını yeniden üretme hello Azure Cosmos DB öykünücüsü mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-295">Key regeneration is not possible in hello Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="b0e6b-296">Hello Azure Cosmos DB öykünücüsü ölçeklenebilir hizmet değil ve çok sayıda koleksiyonları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-296">hello Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="b0e6b-297">Hello Azure Cosmos DB öykünücüsü farklı benzetimini değil [Azure Cosmos DB tutarlılık düzeylerini](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-297">hello Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="b0e6b-298">Hello Azure Cosmos DB öykünücüsü benzetimi yapılamadı [bölgeli çoğaltma](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-298">hello Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="b0e6b-299">Hello Azure Cosmos DB öykünücüsü hello Azure Cosmos DB hizmetinde (örneğin belge boyutu sınırları, artan bölümlenmiş koleksiyonu depolama alanı) bulunan hello hizmeti kota geçersiz kılmaları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-299">hello Azure Cosmos DB Emulator does not support hello service quota overrides that are available in hello Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="b0e6b-300">Hello Azure Cosmos DB öykünücüsü kopyanızı hello Azure Cosmos DB hizmeti ile Merhaba en son değişikliklerle toodate yukarı olmayabilir gibi lütfen [Azure Cosmos DB kapasite Planlayıcısı](https://www.documentdb.com/capacityplanner) tooaccurately tahmin üretim verimlilik (RUs) uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-300">As your copy of hello Azure Cosmos DB Emulator might not be up toodate with hello most recent changes with hello Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) tooaccurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="b0e6b-301"><a id="set-partitioncount"></a>Koleksiyonları Hello sayısını değiştirme</span><span class="sxs-lookup"><span data-stu-id="b0e6b-301"><a id="set-partitioncount"></a>Change hello number of collections</span></span>

<span data-ttu-id="b0e6b-302">Varsayılan olarak, too25 tek bölüm koleksiyonları veya hello Azure Cosmos DB öykünücüsü kullanarak 1 bölümlenmiş koleksiyonunu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-302">By default, you can create up too25 single partition collections, or 1 partitioned collection using hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="b0e6b-303">Merhaba değiştirerek **PartitionCount** değeri too250 tek bölüm koleksiyonları veya 10 bölümlenmiş koleksiyonlar oluşturabilir ya da herhangi bir bileşimini hello 250 tek aşmayan iki bölümleri (burada 1 bölümlenmiş Koleksiyon 25 tek bölümlü bir koleksiyon =).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-303">By modifying hello **PartitionCount** value, you can create up too250 single partition collections or 10 partitioned collections, or any combination of hello two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="b0e6b-304">Merhaba geçerli bölüm sayısı aşıldı sonra toocreate koleksiyonu çalışırsanız hello öykünücüsü iletiden hello ile bir ServiceUnavailable özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-304">If you attempt toocreate a collection after hello current partition count has been exceeded, hello emulator throws a ServiceUnavailable exception, with hello following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="b0e6b-305">koleksiyonları kullanılabilir toohello Azure Cosmos DB öykünücüsü toochange hello sayısı hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="b0e6b-305">toochange hello number of collections available toohello Azure Cosmos DB Emulator, do hello following:</span></span>

1. <span data-ttu-id="b0e6b-306">Merhaba sağ tıklayarak tüm yerel Azure Cosmos DB öykünücüsü verilerini silmek **Azure Cosmos DB öykünücüsü** hello sistem tepsisi ve ardından simgesine **veri Sıfırla...** .</span><span class="sxs-lookup"><span data-stu-id="b0e6b-306">Delete all local Azure Cosmos DB Emulator data by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="b0e6b-307">Bu klasörde C:\Users\user_name\AppData\Local\CosmosDBEmulator tüm öykünücüsü verileri silin.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="b0e6b-308">Tüm açık örnekleri hello sağ tıklayarak çıkmak **Azure Cosmos DB öykünücüsü** hello sistem tepsisi ve ardından simgesine **çıkış**.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-308">Exit all open instances by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="b0e6b-309">Tüm örnekleri tooexit bir dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-309">It may take a minute for all instances tooexit.</span></span>
4. <span data-ttu-id="b0e6b-310">Merhaba Hello en son sürümünü yüklemek [Azure Cosmos DB öykünücüsü](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-310">Install hello latest version of hello [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="b0e6b-311">Bir değer ayarlanarak Hello öykünücü hello PartitionCount bayrağı ile başlatın < 250 =.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-311">Launch hello emulator with hello PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="b0e6b-312">Örneğin: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b0e6b-313">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b0e6b-313">Troubleshooting</span></span>

<span data-ttu-id="b0e6b-314">Toohelp hello Azure Cosmos DB öykünücü ile karşılaştığınız sorunları sorun giderme ipuçları aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b0e6b-314">Use hello following tips toohelp troubleshoot issues you encounter with hello Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="b0e6b-315">Merhaba öykünücüsü yeni bir sürümünü yüklediyseniz ve hataları yaşıyor verilerinizi sıfırlama emin olun.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-315">If you installed a new version of hello Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="b0e6b-316">Verilerinizi hello sistem tepsisi hello Azure Cosmos DB öykünücü simgesine sağ tıklayıp sıfırlama verileri tıklatarak sıfırlayabilirsiniz...</span><span class="sxs-lookup"><span data-stu-id="b0e6b-316">You can reset your data by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="b0e6b-317">Merhaba hataları çözmezse kaldırın ve hello uygulamayı yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-317">If that does not fix hello errors, you can uninstall and reinstall hello app.</span></span> <span data-ttu-id="b0e6b-318">Bkz: [hello yerel öykünücüsü kaldırma](#uninstall) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-318">See [Uninstall hello local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="b0e6b-319">Hello Azure Cosmos DB öykünücüsü çökerse c:\Users\user_name\AppData\Local\CrashDumps klasöründen döküm dosyaları toplamak, sıkıştırmak ve bunları tooan e-postaya çok eklemek[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-319">If hello Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="b0e6b-320">Kilitlenme karşılaşırsanız, komutu bir yönetici komut isteminden aşağıdaki hello CosmosDB.StartupEntryPoint.exe içinde çalıştırın:`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="b0e6b-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run hello following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="b0e6b-321">Bir bağlantı sorunu yaşarsanız [toplamak izleme dosyaları](#trace-files)sıkıştırmak ve bunları tooan e-postaya çok eklemek[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b0e6b-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="b0e6b-322">Alırsanız, bir **Hizmet kullanılamıyor** iletisi, hello öykünücüsü tooinitialize hello ağ yığınını başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-322">If you receive a **Service Unavailable** message, hello emulator might be failing tooinitialize hello network stack.</span></span> <span data-ttu-id="b0e6b-323">Ağ filtre sürücülerini hello sorunu neden olabileceğinden hello Pulse güvenli istemci veya Juniper ağları istemcisi yüklü varsa toosee denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-323">Check toosee if you have hello Pulse secure client or Juniper networks client installed, as their network filter drivers may cause hello problem.</span></span> <span data-ttu-id="b0e6b-324">Kaldırma işlemi üçüncü taraf ağ filtre sürücüleri genellikle hello sorunu giderir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-324">Uninstalling third party network filter drivers typically fixes hello issue.</span></span>

### <span data-ttu-id="b0e6b-325"><a id="trace-files"></a>İzleme dosyaları Topla</span><span class="sxs-lookup"><span data-stu-id="b0e6b-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="b0e6b-326">toocollect hata ayıklama izlemeleri, komutları bir yönetici komut isteminden aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b0e6b-326">toocollect debugging traces, run hello following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="b0e6b-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="b0e6b-328">Gözcü hello sistem tepsisi toomake emin hello program kapatıldı, bir dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-328">Watch hello system tray toomake sure hello program has shut down, it may take a minute.</span></span> <span data-ttu-id="b0e6b-329">Aynı zamanda yalnızca tıklatabilirsiniz **çıkış** hello Azure Cosmos DB öykünücüsü kullanıcı arabiriminde.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-329">You can also just click **Exit** in hello Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="b0e6b-330">Merhaba sorunu yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-330">Reproduce hello problem.</span></span> <span data-ttu-id="b0e6b-331">Veri Gezgini çalışmıyorsa, yalnızca toowait hello tarayıcı tooopen birkaç saniye toocatch hello hata için gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-331">If Data Explorer is not working, you only need toowait for hello browser tooopen for a few seconds toocatch hello error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="b0e6b-332">Çok gidin`%ProgramFiles%\Azure Cosmos DB Emulator` ve hello docdbemulator_000001.etl dosyasını bulun.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-332">Navigate too`%ProgramFiles%\Azure Cosmos DB Emulator` and find hello docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="b0e6b-333">Merhaba .etl dosyası yeniden oluşturma adımları birlikte çok gönderme[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) hata ayıklama için.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-333">Send hello .etl file along with repro steps too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="b0e6b-334"><a id="uninstall"></a>Kaldırma yerel öykünücüsü hello</span><span class="sxs-lookup"><span data-stu-id="b0e6b-334"><a id="uninstall"></a>Uninstall hello local Emulator</span></span>

1. <span data-ttu-id="b0e6b-335">Tüm açık örnekleri hello çıkmak hello sistem tepsisi hello Azure Cosmos DB öykünücü simgesine sağ tıklayarak ve sonra da çıkış'ı tıklatarak yerel öykünücüsü.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-335">Exit all open instances of hello local Emulator by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Exit.</span></span> <span data-ttu-id="b0e6b-336">Tüm örnekleri tooexit bir dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-336">It may take a minute for all instances tooexit.</span></span>
2. <span data-ttu-id="b0e6b-337">Merhaba Windows Arama kutusuna yazın **uygulamalar ve Özellikler** üzerinde hello tıklatıp **uygulamalar ve Özellikler (sistem ayarlarını)** sonucu.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-337">In hello Windows search box, type **Apps & features** and click on hello **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="b0e6b-338">Uygulamaları Hello listesinde çok kaydırma**Azure Cosmos DB öykünücüsü**, onu seçin, **kaldırma**, ardından onaylayın ve tıklatın **kaldırma** yeniden.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-338">In hello list of apps, scroll too**Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="b0e6b-339">Merhaba uygulama kaldırıldığında tooC:\Users gidin\<kullanıcı > \AppData\Local\CosmosDBEmulator ve delete hello klasör.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-339">When hello app is uninstalled, navigate tooC:\Users\<user>\AppData\Local\CosmosDBEmulator and delete hello folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b0e6b-340">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b0e6b-340">Next steps</span></span>

<span data-ttu-id="b0e6b-341">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="b0e6b-341">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b0e6b-342">Yüklü yerel öykünücüsü hello</span><span class="sxs-lookup"><span data-stu-id="b0e6b-342">Installed hello local Emulator</span></span>
> * <span data-ttu-id="b0e6b-343">Rand öykünücüsü Docker için Windows hello</span><span class="sxs-lookup"><span data-stu-id="b0e6b-343">Rand hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="b0e6b-344">Kimliği doğrulanmış istekler</span><span class="sxs-lookup"><span data-stu-id="b0e6b-344">Authenticated requests</span></span>
> * <span data-ttu-id="b0e6b-345">Merhaba öykünücüsü Hello Veri Gezgini kullanılan</span><span class="sxs-lookup"><span data-stu-id="b0e6b-345">Used hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="b0e6b-346">Dışarı aktarılan SSL sertifikaları</span><span class="sxs-lookup"><span data-stu-id="b0e6b-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="b0e6b-347">Merhaba öykünücüsü hello komut satırından çağrılan</span><span class="sxs-lookup"><span data-stu-id="b0e6b-347">Called hello Emulator from hello command line</span></span>
> * <span data-ttu-id="b0e6b-348">Toplanan izleme dosyaları</span><span class="sxs-lookup"><span data-stu-id="b0e6b-348">Collected trace files</span></span>

<span data-ttu-id="b0e6b-349">Bu öğreticide, nasıl toouse hello boş yerel geliştirme için yerel öykünücüsü öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-349">In this tutorial, you've learned how toouse hello local Emulator for free local development.</span></span> <span data-ttu-id="b0e6b-350">Şimdi toohello sonraki öğretici devam ve öğrenin nasıl tooexport öykünücüsü SSL sertifikaları.</span><span class="sxs-lookup"><span data-stu-id="b0e6b-350">You can now proceed toohello next tutorial and learn how tooexport Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b0e6b-351">Hello Azure Cosmos DB öykünücüsü sertifikaları verme</span><span class="sxs-lookup"><span data-stu-id="b0e6b-351">Export hello Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
