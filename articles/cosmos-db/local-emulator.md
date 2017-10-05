---
title: "Yerel olarak Azure Cosmos DB öykünücü ile geliştirme | Microsoft Docs"
description: "Azure Cosmos DB öykünücüsü kullanarak, geliştirmek ve uygulamanızı yerel olarak ücretsiz, Azure aboneliği oluşturmadan test edin."
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
ms.openlocfilehash: a0f6a845a345ebd4ef0a58abf4934ce400103109
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="9aba9-104">Yerel geliştirme ve sınama için Azure Cosmos DB öykünücüsünü kullanma</span><span class="sxs-lookup"><span data-stu-id="9aba9-104">Use the Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="9aba9-105"><strong>İkili dosyalar</strong></span><span class="sxs-lookup"><span data-stu-id="9aba9-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="9aba9-106">MSI indirin</span><span class="sxs-lookup"><span data-stu-id="9aba9-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="9aba9-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="9aba9-108">Docker hub'a</span><span class="sxs-lookup"><span data-stu-id="9aba9-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-109"><strong>Docker kaynak</strong></span><span class="sxs-lookup"><span data-stu-id="9aba9-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="9aba9-110">Github</span><span class="sxs-lookup"><span data-stu-id="9aba9-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="9aba9-111">Azure Cosmos DB öykünücüsü geliştirme amacıyla Azure Cosmos DB hizmet öykünen yerel bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="9aba9-111">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="9aba9-112">Azure Cosmos DB öykünücüsü kullanarak, geliştirmek ve bir Azure aboneliği oluşturmak veya herhangi bir maliyet olmadan uygulamanızı yerel olarak test etmek.</span><span class="sxs-lookup"><span data-stu-id="9aba9-112">Using the Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="9aba9-113">Uygulamanızı Azure Cosmos DB öykünücüsünde nasıl çalıştığını ile memnun kaldığınızda, bulutta bir Azure Cosmos DB hesabı kullanmaya geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9aba9-113">When you're satisfied with how your application is working in the Azure Cosmos DB Emulator, you can switch to using an Azure Cosmos DB account in the cloud.</span></span>

<span data-ttu-id="9aba9-114">Bu makalede aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="9aba9-114">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="9aba9-115">Öykünücü yükleme</span><span class="sxs-lookup"><span data-stu-id="9aba9-115">Installing the Emulator</span></span>
> * <span data-ttu-id="9aba9-116">Windows için Docker öykünücü çalışan</span><span class="sxs-lookup"><span data-stu-id="9aba9-116">Running the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="9aba9-117">Kimlik doğrulama istekleri</span><span class="sxs-lookup"><span data-stu-id="9aba9-117">Authenticating requests</span></span>
> * <span data-ttu-id="9aba9-118">Öykünücüde Veri Gezgini'ni kullanma</span><span class="sxs-lookup"><span data-stu-id="9aba9-118">Using the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="9aba9-119">SSL sertifikaları verme</span><span class="sxs-lookup"><span data-stu-id="9aba9-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="9aba9-120">Öykünücü komut satırından çağırma</span><span class="sxs-lookup"><span data-stu-id="9aba9-120">Calling the Emulator from the command line</span></span>
> * <span data-ttu-id="9aba9-121">İzleme dosyaları toplama</span><span class="sxs-lookup"><span data-stu-id="9aba9-121">Collecting trace files</span></span>

<span data-ttu-id="9aba9-122">Burada Kirill Gavrylyuk Azure Cosmos DB öykünücü ile çalışmaya başlama gösterilmektedir aşağıdaki videoyu izleyerek çalışmaya başlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="9aba9-122">We recommend getting started by watching the following video, where Kirill Gavrylyuk shows how to get started with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="9aba9-123">Video öykünücüsü DocumentDB öykünücüsü olarak başvuruyor ancak aracı yüklendi unutmayın video basmaya itibaren Azure Cosmos DB öykünücüsü yeniden adlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="9aba9-123">Note that the video refers to the emulator as the DocumentDB Emulator, but the tool itself has been renamed the Azure Cosmos DB Emulator since taping the video.</span></span> <span data-ttu-id="9aba9-124">Video içindeki tüm bilgileri için Azure Cosmos DB öykünücüsü hala doğru olur.</span><span class="sxs-lookup"><span data-stu-id="9aba9-124">All information in the video is still accurate for the Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-the-emulator-works"></a><span data-ttu-id="9aba9-125">Öykünücü nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="9aba9-125">How the Emulator works</span></span>
<span data-ttu-id="9aba9-126">Azure Cosmos DB öykünücüsü yüksek doğruluk öykünmesi Azure Cosmos DB hizmet sağlar.</span><span class="sxs-lookup"><span data-stu-id="9aba9-126">The Azure Cosmos DB Emulator provides a high-fidelity emulation of the Azure Cosmos DB service.</span></span> <span data-ttu-id="9aba9-127">Azure Cosmos JSON belgelerini sorgulamak için destek dahil olmak üzere sağlama DB olarak aynı işlevselliği destekler ve koleksiyonları ölçekleme ve yürütme yordamları ve Tetikleyicileri depolanır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="9aba9-128">Geliştirmek ve Azure Cosmos DB öykünücüsü kullanarak uygulamaları test ve bunları Azure'a yalnızca tek bir yapılandırma için Azure Cosmos DB bağlantı uç noktasına değişikliği yaparak genel ölçekte dağıtma.</span><span class="sxs-lookup"><span data-stu-id="9aba9-128">You can develop and test applications using the Azure Cosmos DB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="9aba9-129">Yüksek kaliteli yerel öykünme gerçek Azure Cosmos DB hizmetinin oluşturduğumuz olsa da, Azure Cosmos DB öykünücüsü hizmet farklı uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-129">While we created a high-fidelity local emulation of the actual Azure Cosmos DB service, the implementation of the Azure Cosmos DB Emulator is different than that of the service.</span></span> <span data-ttu-id="9aba9-130">Örneğin, Azure Cosmos DB öykünücüsü Kalıcılık ve HTTPS protokol yığını bağlantısı için yerel dosya sistemi gibi standart işletim sistemi bileşenlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-130">For example, the Azure Cosmos DB Emulator uses standard OS components such as the local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="9aba9-131">Bu genel çoğaltma, okuma/yazma ve ince ayarlanabilir tutarlılık düzeyleri için tek basamaklı milisaniyelik gecikme süresi yok gibi Azure Cosmos DB öykünücüsü kullanılabilir Azure altyapı dayanan bazı işlevler anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via the Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="9aba9-132">Şu anda öykünücü veri Explorer'da yalnızca DocumentDB API koleksiyonları ve MongoDB koleksiyonları oluşturmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9aba9-132">At this time the Data Explorer in the emulator only supports the creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="9aba9-133">Öykünücü veri Explorer'da oluşturulmasını tablolar ve grafikler şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="9aba9-133">The Data Explorer in the emulator does not currently support the creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="9aba9-134">Sistem gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="9aba9-134">System requirements</span></span>
<span data-ttu-id="9aba9-135">Azure Cosmos DB öykünücüsü donanım ve yazılım gereksinimleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9aba9-135">The Azure Cosmos DB Emulator has the following hardware and software requirements:</span></span>

* <span data-ttu-id="9aba9-136">Yazılım gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="9aba9-136">Software requirements</span></span>
  * <span data-ttu-id="9aba9-137">Windows Server 2012 R2, Windows Server 2016 veya Windows 10</span><span class="sxs-lookup"><span data-stu-id="9aba9-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="9aba9-138">En düşük donanım gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="9aba9-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="9aba9-139">2 GB RAM</span><span class="sxs-lookup"><span data-stu-id="9aba9-139">2 GB RAM</span></span>
  * <span data-ttu-id="9aba9-140">10 GB kullanılabilir sabit disk alanı</span><span class="sxs-lookup"><span data-stu-id="9aba9-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="9aba9-141">Yükleme</span><span class="sxs-lookup"><span data-stu-id="9aba9-141">Installation</span></span>
<span data-ttu-id="9aba9-142">Azure Cosmos DB Öykünücüsünden yükleyip [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="9aba9-142">You can download and install the Azure Cosmos DB Emulator from the [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="9aba9-143">Yüklemek, yapılandırmak ve Azure Cosmos DB öykünücüsü çalıştırmak için bilgisayarda yönetici ayrıcalıkları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-143">To install, configure, and run the Azure Cosmos DB Emulator, you must have administrative privileges on the computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="9aba9-144">Windows için Docker çalışan</span><span class="sxs-lookup"><span data-stu-id="9aba9-144">Running on Docker for Windows</span></span>

<span data-ttu-id="9aba9-145">Azure Cosmos DB öykünücüsü Windows için Docker çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9aba9-145">The Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="9aba9-146">Öykünücü, Oracle Linux için Docker üzerinde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="9aba9-146">The Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="9aba9-147">Bulduktan sonra [Windows için Docker](https://www.docker.com/docker-windows) yüklü, öykünücü görüntünüzün Docker hub'dan sık kullanılan kabuğundan aşağıdaki komutu çalıştırarak çekebilir (cmd.exe, PowerShell, vs.).</span><span class="sxs-lookup"><span data-stu-id="9aba9-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull the Emulator image from Docker Hub by running the following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="9aba9-148">Görüntü başlatmak için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9aba9-148">To start the image, run the following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="9aba9-149">Yanıt aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="9aba9-149">The response looks similar to the following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import the SSL certificate from an administrator command prompt on the host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="9aba9-150">Öykünücü silindikten sonra etkileşimli Kabuk kapatma öykünücüsü'nın kapsayıcı kapatma işlemi başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="9aba9-150">Closing the interactive shell once the Emulator has been started will shutdown the Emulator’s container.</span></span>

<span data-ttu-id="9aba9-151">Uç noktası ve ana anahtarından içinde yanıt, istemci kullanın ve ana bilgisayara SSL sertifikasını içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="9aba9-151">Use the endpoint and master key in from the response in your client and import the SSL certificate into your host.</span></span> <span data-ttu-id="9aba9-152">SSL sertifikasını içeri aktarmak için bir yönetici komut isteminde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="9aba9-152">To import the SSL certificate, do the following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-the-emulator"></a><span data-ttu-id="9aba9-153">Öykünücü başlatma</span><span class="sxs-lookup"><span data-stu-id="9aba9-153">Start the Emulator</span></span>

<span data-ttu-id="9aba9-154">Azure Cosmos DB öykünücüsü başlatmak için Başlat düğmesine basın veya Windows tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="9aba9-154">To start the Azure Cosmos DB Emulator, select the Start button or press the Windows key.</span></span> <span data-ttu-id="9aba9-155">Yazmaya başlayın **Azure Cosmos DB öykünücüsü**ve uygulamaları listesinden öykünücü seçin.</span><span class="sxs-lookup"><span data-stu-id="9aba9-155">Begin typing **Azure Cosmos DB Emulator**, and select the emulator from the list of applications.</span></span> 

![Başlat düğmesine basın veya Windows tuşuna basın, yazmaya başlayın ** Azure Cosmos DB öykünücüsü ** ve uygulamalar listesinden öykünücü seçin](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="9aba9-157">Öykünücü çalıştırırken, Windows görev çubuğundaki bildirim alanında bir simge görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9aba9-157">When the emulator is running, you'll see an icon in the Windows taskbar notification area.</span></span> ![Azure Cosmos DB yerel öykünücüsü görev çubuğu bildirim](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="9aba9-159">Varsayılan olarak Azure Cosmos DB öykünücüsü 8081 numaralı bağlantı noktasını dinlemeye yerel makine ("localhost") çalışır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-159">The Azure Cosmos DB Emulator by default runs on the local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="9aba9-160">Varsayılan olarak Azure Cosmos DB öykünücü yüklendikten `C:\Program Files\Azure Cosmos DB Emulator` dizin.</span><span class="sxs-lookup"><span data-stu-id="9aba9-160">The Azure Cosmos DB Emulator is installed by default to the `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="9aba9-161">Ayrıca, başlatma ve komut satırından öykünücüsü durdurma.</span><span class="sxs-lookup"><span data-stu-id="9aba9-161">You can also start and stop the emulator from the command-line.</span></span> <span data-ttu-id="9aba9-162">Bkz: [komut satırı aracını referans](#command-line) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="9aba9-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="9aba9-163">Veri Gezgini'ni başlatın</span><span class="sxs-lookup"><span data-stu-id="9aba9-163">Start Data Explorer</span></span>

<span data-ttu-id="9aba9-164">Azure Cosmos DB öykünücüsü başlattığında, Azure Cosmos DB Data Explorer tarayıcınızda otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-164">When the Azure Cosmos DB emulator launches it will automatically open the Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="9aba9-165">Adresi olarak görünür [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="9aba9-165">The address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="9aba9-166">Explorer'ı kapatın ve daha sonra yeniden açmak istiyor musunuz URL'nin tarayıcınızda açın veya aşağıda gösterildiği gibi Azure Cosmos DB öykücüsünden Windows Tepsi simgesi başlatın.</span><span class="sxs-lookup"><span data-stu-id="9aba9-166">If you close the explorer and would like to re-open it later, you can either open the URL in your browser or launch it from the Azure Cosmos DB Emulator in the Windows Tray Icon as shown below.</span></span>

![Azure Cosmos DB yerel öykünücüsü Veri Gezgini Başlatıcısı](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="9aba9-168">Güncelleştirmeleri denetleme</span><span class="sxs-lookup"><span data-stu-id="9aba9-168">Checking for updates</span></span>
<span data-ttu-id="9aba9-169">Veri Gezgini indirme için kullanılabilir yeni bir güncelleştirme olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="9aba9-170">Azure Cosmos DB öykünücüsü bir sürümünde oluşturulan veri farklı bir sürümünü kullanırken erişilebilir olması garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="9aba9-170">Data created in one version of the Azure Cosmos DB Emulator is not guaranteed to be accessible when using a different version.</span></span> <span data-ttu-id="9aba9-171">Verileriniz için uzun vadeli kalıcı olması gerekiyorsa, bu verileri Azure Cosmos DB hesabı yerine Azure Cosmos DB öykünücüsü depolamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-171">If you need to persist your data for the long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in the Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="9aba9-172">Kimlik doğrulama istekleri</span><span class="sxs-lookup"><span data-stu-id="9aba9-172">Authenticating requests</span></span>
<span data-ttu-id="9aba9-173">Gibi bulutta Azure Cosmos DB ile Azure Cosmos DB öykünücüsüne karşı yaptığınız her isteğin kimliğinin doğrulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-173">Just as with Azure Cosmos DB in the cloud, every request that you make against the Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="9aba9-174">Azure Cosmos DB öykünücüsü ana anahtar kimlik doğrulaması için tek bir sabit hesap ve bilinen bir kimlik doğrulama anahtarı destekler.</span><span class="sxs-lookup"><span data-stu-id="9aba9-174">The Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="9aba9-175">Bu hesabı ve anahtarı Azure Cosmos DB öykünücü ile kullanmak için izin verilen tek kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-175">This account and key are the only credentials permitted for use with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="9aba9-176">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="9aba9-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="9aba9-177">Azure Cosmos DB öykünücüsü tarafından desteklenen ana anahtar yalnızca öykünücü ile kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-177">The master key supported by the Azure Cosmos DB Emulator is intended for use only with the emulator.</span></span> <span data-ttu-id="9aba9-178">Üretim Azure Cosmos DB hesabı ve anahtarı Azure Cosmos DB öykünücü ile kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="9aba9-178">You cannot use your production Azure Cosmos DB account and key with the Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="9aba9-179">Öykünücü /Key seçeneğiyle başlattıysanız yerine oluşturulan anahtarı kullanın "C2y6yDjf5/R, ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="</span><span class="sxs-lookup"><span data-stu-id="9aba9-179">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="9aba9-180">Ayrıca, yalnızca Azure Cosmos DB hizmet olarak Azure Cosmos DB öykünücüsü yalnızca SSL aracılığıyla güvenli iletişimi destekler.</span><span class="sxs-lookup"><span data-stu-id="9aba9-180">Additionally, just as the Azure Cosmos DB service, the Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-the-emulator-on-a-local-network"></a><span data-ttu-id="9aba9-181">Öykünücü bir yerel ağ üzerinde çalışıyor</span><span class="sxs-lookup"><span data-stu-id="9aba9-181">Running the emulator on a local network</span></span>

<span data-ttu-id="9aba9-182">Yerel bir ağda öykünücü çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9aba9-182">You can run the emulator on a local network.</span></span> <span data-ttu-id="9aba9-183">Ağ erişimini etkinleştirmek için /AllowNetworkAccess tasarrufunda belirtin [komut satırı](#command-line-syntax), gerektiren /Key belirttiğiniz = key_string veya/keyfile dosya_adı =.</span><span class="sxs-lookup"><span data-stu-id="9aba9-183">To enable network access, specify the /AllowNetworkAccess option at the [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="9aba9-184">/GenKeyFile kullanabileceğiniz önceden rastgele bir anahtar ile bir dosya oluşturmak için dosya_adı =.</span><span class="sxs-lookup"><span data-stu-id="9aba9-184">You can use /GenKeyFile=file_name to generate a file with a random key upfront.</span></span>  <span data-ttu-id="9aba9-185">Geçirebilirsiniz sonra için/keyfile dosya_adı veya /Key = contents_of_file =.</span><span class="sxs-lookup"><span data-stu-id="9aba9-185">Then you can pass that to /KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="9aba9-186">İlk kez ağ erişimini etkinleştirmek için kullanıcı kapatma öykünücü gerekir ve öykünücüsü'nın veri dizini (C:\Users\user_name\AppData\Local\CosmosDBEmulator) silin.</span><span class="sxs-lookup"><span data-stu-id="9aba9-186">To enable network access for the first time the user should shutdown the emulator and delete the emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-the-emulator"></a><span data-ttu-id="9aba9-187">Öykünücü ile geliştirme</span><span class="sxs-lookup"><span data-stu-id="9aba9-187">Developing with the Emulator</span></span>
<span data-ttu-id="9aba9-188">Masaüstünde çalışan Azure Cosmos DB öykünücüsü olduktan sonra desteklenen herhangi biri kullanabilirsiniz [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) veya [Azure Cosmos DB REST API](/rest/api/documentdb/) öykünücü ile etkileşim kurmak için.</span><span class="sxs-lookup"><span data-stu-id="9aba9-188">Once you have the Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or the [Azure Cosmos DB REST API](/rest/api/documentdb/) to interact with the Emulator.</span></span> <span data-ttu-id="9aba9-189">Azure Cosmos DB öykünücüsü de DocumentDB ve MongoDB API'ları ve görünüm için koleksiyonları oluşturun ve hiçbir kod yazmadan belgeleri düzenlemesine olanak tanır yerleşik bir Veri Gezgini içerir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-189">The Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for the DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect to the Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="9aba9-190">Kullanıyorsanız, [MongoDB için protokol desteği Azure Cosmos DB](mongodb-introduction.md), Lütfen bağlantı dizesi olarak şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="9aba9-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use the following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="9aba9-191">Var olan araçlarla kullanabilirsiniz [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) Azure Cosmos DB öykünücüsü bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="9aba9-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="9aba9-192">Ayrıca Azure Cosmos DB öykünücüsü ve Azure Cosmos DB hizmetini kullanarak arasında verileri geçirebilirsiniz [Azure Cosmos DB veri geçiş aracı](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="9aba9-192">You can also migrate data between the Azure Cosmos DB Emulator and the Azure Cosmos DB service using the [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="9aba9-193">Öykünücü /Key seçeneğiyle başlattıysanız yerine oluşturulan anahtarı kullanın "C2y6yDjf5/R, ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="</span><span class="sxs-lookup"><span data-stu-id="9aba9-193">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="9aba9-194">Varsayılan olarak Azure Cosmos DB öykünücüsü kullanarak 25 tek bölüm koleksiyonları veya 1 bölümlenmiş koleksiyonu kadar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9aba9-194">Using the Azure Cosmos DB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="9aba9-195">Bu değer değiştirme hakkında daha fazla bilgi için bkz: [PartitionCount değeri ayarı](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="9aba9-195">For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-the-ssl-certificate"></a><span data-ttu-id="9aba9-196">SSL sertifikasını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="9aba9-196">Export the SSL certificate</span></span>

<span data-ttu-id="9aba9-197">.NET dilleri ve çalışma zamanı Azure Cosmos DB yerel öykünücüsü güvenli bir şekilde bağlanmak için Windows sertifika deposunu kullan.</span><span class="sxs-lookup"><span data-stu-id="9aba9-197">.NET languages and runtime use the Windows Certificate Store to securely connect to the Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="9aba9-198">Diğer diller yönetme ve sertifikaları kullanarak kendi yöntemi vardır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="9aba9-199">Java kullanan kendi [sertifika deposu](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) Python kullanırken [yuva sarmalayıcıları](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="9aba9-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="9aba9-200">Diller ve Windows sertifika deposu ile tümleştirmek değil çalışma zamanları ile kullanmak üzere bir sertifika almak için Windows Sertifika Yöneticisi'ni kullanarak vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-200">In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store you will need to export it using the Windows Certificate Manager.</span></span> <span data-ttu-id="9aba9-201">Başlatılsın certlm.msc çalıştırarak ya da adım adım yönergeleri izleyin [Azure Cosmos DB öykünücüsü sertifikaları verme](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="9aba9-201">You can start it by running certlm.msc or follow the step by step instructions in [Export the Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="9aba9-202">Sertifika Yöneticisi'ni çalışmaya başladıktan sonra aşağıda gösterildiği gibi kişisel Sertifikalar'ı açmak ve bir BASE-64 kodlanmış X.509 (.cer) dosyası olarak kolay adı "DocumentDBEmulatorCertificate" Sertifika verme.</span><span class="sxs-lookup"><span data-stu-id="9aba9-202">Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Azure Cosmos DB yerel öykünücüsü SSL sertifikası](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="9aba9-204">X.509 Sertifikası'ndaki yönergeleri izleyerek Java sertifika deposuna alınabilir [Java CA sertifikalarını depolamak için bir sertifika ekleme](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="9aba9-204">The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="9aba9-205">Sertifikayı sertifika deposuna içeri aktarıldığında, Java ve MongoDB uygulamalar Azure Cosmos DB öykünücüsü bağlanabiliyor olur.</span><span class="sxs-lookup"><span data-stu-id="9aba9-205">Once the certificate is imported into the certificate store, Java and MongoDB applications will be able to connect to the Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="9aba9-206">Öykünücü Python ve Node.js SDK'ları bağlanırken SSL doğrulama devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-206">When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="9aba9-207"><a id="command-line"></a>Komut satırı aracı başvurusu</span><span class="sxs-lookup"><span data-stu-id="9aba9-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="9aba9-208">Yükleme konumundan, komut satırında başlatmak ve öykünücü durdurmak, seçenekleri yapılandırın ve diğer işlemleri gerçekleştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9aba9-208">From the installation location, you can use the command-line to start and stop the emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="9aba9-209">Komut satırı sözdizimi</span><span class="sxs-lookup"><span data-stu-id="9aba9-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="9aba9-210">Seçeneklerinin listesini görüntülemek için şunu yazın `CosmosDB.Emulator.exe /?` komut isteminde.</span><span class="sxs-lookup"><span data-stu-id="9aba9-210">To view the list of options, type `CosmosDB.Emulator.exe /?` at the command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="9aba9-211"><strong>Seçeneği</strong></span><span class="sxs-lookup"><span data-stu-id="9aba9-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="9aba9-212"><strong>Açıklama</strong></span><span class="sxs-lookup"><span data-stu-id="9aba9-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="9aba9-213"><strong>Komutu</strong></span><span class="sxs-lookup"><span data-stu-id="9aba9-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="9aba9-214"><strong>Bağımsız değişkenler</strong></span><span class="sxs-lookup"><span data-stu-id="9aba9-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-215">[Bağımsız değişkenler]</span><span class="sxs-lookup"><span data-stu-id="9aba9-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="9aba9-216">Varsayılan ayarlarla Azure Cosmos DB öykünücüsü başlatır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-216">Starts up the Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="9aba9-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="9aba9-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-218">[Help]</span><span class="sxs-lookup"><span data-stu-id="9aba9-218">[Help]</span></span></td>
  <td><span data-ttu-id="9aba9-219">Desteklenen komut satırı bağımsız değişkenleri listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9aba9-219">Displays the list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="9aba9-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="9aba9-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-221">kapatma</span><span class="sxs-lookup"><span data-stu-id="9aba9-221">Shutdown</span></span></td>
  <td><span data-ttu-id="9aba9-222">Azure Cosmos DB öykünücüsü kapatır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-222">Shuts down the Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="9aba9-223">CosmosDB.Emulator.exe Shutdown</span><span class="sxs-lookup"><span data-stu-id="9aba9-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-224">DataPath</span><span class="sxs-lookup"><span data-stu-id="9aba9-224">DataPath</span></span></td>
  <td><span data-ttu-id="9aba9-225">Veri dosyalarını depolamak yolu belirtir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-225">Specifies the path in which to store data files.</span></span> <span data-ttu-id="9aba9-226">% LocalAppdata%\CosmosDBEmulator varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="9aba9-227">CosmosDB.Emulator.exe /DataPath =&lt;datapath&gt;</span><span class="sxs-lookup"><span data-stu-id="9aba9-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="9aba9-228">&lt;DataPath&gt;: erişilebilir yolu</span><span class="sxs-lookup"><span data-stu-id="9aba9-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-229">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="9aba9-229">Port</span></span></td>
  <td><span data-ttu-id="9aba9-230">Öykünücü için kullanılacak bağlantı noktası numarasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-230">Specifies the port number to use for the emulator.</span></span>  <span data-ttu-id="9aba9-231">8081 varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="9aba9-232">CosmosDB.Emulator.exe Port =&lt;bağlantı noktası&gt;</span><span class="sxs-lookup"><span data-stu-id="9aba9-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="9aba9-233">&lt;bağlantı noktası&gt;: tek bir bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="9aba9-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="9aba9-234">MongoPort</span></span></td>
  <td><span data-ttu-id="9aba9-235">API MongoDB uyumluluk için kullanılacak bağlantı noktası numarasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-235">Specifies the port number to use for MongoDB compatibility API.</span></span> <span data-ttu-id="9aba9-236">Varsayılandır 10255 değerini bulur.</span><span class="sxs-lookup"><span data-stu-id="9aba9-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="9aba9-237">CosmosDB.Emulator.exe /MongoPort =&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="9aba9-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="9aba9-238">&lt;mongoport&gt;: tek bir bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="9aba9-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="9aba9-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="9aba9-240">Doğrudan bağlantı için kullanılacak bağlantı noktalarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-240">Specifies the ports to use for direct connectivity.</span></span> <span data-ttu-id="9aba9-241">Varsayılan 10251,10252,10253,10254 olur.</span><span class="sxs-lookup"><span data-stu-id="9aba9-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="9aba9-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="9aba9-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="9aba9-243">&lt;directports&gt;: 4 bağlantı noktalarının virgülle ayrılmış listesi</span><span class="sxs-lookup"><span data-stu-id="9aba9-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-244">Anahtar</span><span class="sxs-lookup"><span data-stu-id="9aba9-244">Key</span></span></td>
  <td><span data-ttu-id="9aba9-245">Öykünücü için yetkilendirme anahtar.</span><span class="sxs-lookup"><span data-stu-id="9aba9-245">Authorization key for the emulator.</span></span> <span data-ttu-id="9aba9-246">Anahtarı bir 64 baytlık vektör 64 tabanlı kodlama olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-246">Key must be the base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="9aba9-247">CosmosDB.Emulator.exe /Key:&lt;anahtarı&gt;</span><span class="sxs-lookup"><span data-stu-id="9aba9-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="9aba9-248">&lt;anahtar&gt;: anahtarı bir 64 baytlık vektör 64 tabanlı kodlama olması gerekir</span><span class="sxs-lookup"><span data-stu-id="9aba9-248">&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="9aba9-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="9aba9-250">Davranış sınırlama istek hızı etkinleştirilip etkinleştirilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="9aba9-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="9aba9-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="9aba9-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="9aba9-253">Davranış sınırlama istek hızı devre dışı belirtir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="9aba9-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="9aba9-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-255">Nouı</span><span class="sxs-lookup"><span data-stu-id="9aba9-255">NoUI</span></span></td>
  <td><span data-ttu-id="9aba9-256">Öykünücü kullanıcı arabirimi gösterme.</span><span class="sxs-lookup"><span data-stu-id="9aba9-256">Do not show the emulator user interface.</span></span></td>
  <td><span data-ttu-id="9aba9-257">CosmosDB.Emulator.exe/nouı</span><span class="sxs-lookup"><span data-stu-id="9aba9-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="9aba9-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="9aba9-259">Belge Gezgini başlatma sırasında gösterme.</span><span class="sxs-lookup"><span data-stu-id="9aba9-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="9aba9-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="9aba9-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-261">bölüm sayısı</span><span class="sxs-lookup"><span data-stu-id="9aba9-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="9aba9-262">Bölümlenmiş koleksiyonlar en fazla sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-262">Specifies the maximum number of partitioned collections.</span></span> <span data-ttu-id="9aba9-263">Bkz: [koleksiyonları sayısını değiştirme](#set-partitioncount) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="9aba9-263">See [Change the number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="9aba9-264">CosmosDB.Emulator.exe /PartitionCount =&lt;bölüm sayısı&gt;</span><span class="sxs-lookup"><span data-stu-id="9aba9-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="9aba9-265">&lt;bölüm sayısı&gt;: maksimum sayısı, izin verilen tek bölüm koleksiyonları.</span><span class="sxs-lookup"><span data-stu-id="9aba9-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="9aba9-266">Varsayılan 25'tir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-266">Default is 25.</span></span> <span data-ttu-id="9aba9-267">İzin verilen en fazla 250'dir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="9aba9-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="9aba9-269">Bölümler bölümlendirilmiş bir koleksiyon için varsayılan sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-269">Specifies the default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="9aba9-270">CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="9aba9-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="9aba9-271">&lt;defaultpartitioncount&gt; 25 varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="9aba9-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="9aba9-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="9aba9-273">Bir ağ üzerinden öykünücüsü erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="9aba9-273">Enables access to the emulator over a network.</span></span> <span data-ttu-id="9aba9-274">/Key geçmesi gereken =&lt;key_string&gt; veya/keyfile =&lt;dosya_adı&gt; ağ erişimini etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9aba9-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; to enable network access.</span></span></td>
  <td><span data-ttu-id="9aba9-275">CosmosDB.Emulator.exe AllowNetworkAccess /Key =&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="9aba9-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="9aba9-276">or</span><span class="sxs-lookup"><span data-stu-id="9aba9-276">or</span></span><br><br><span data-ttu-id="9aba9-277">CosmosDB.Emulator.exe /AllowNetworkAccess/keyfile =&lt;dosya_adı&gt;</span><span class="sxs-lookup"><span data-stu-id="9aba9-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="9aba9-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="9aba9-279">/AllowNetworkAccess kullanıldığında, güvenlik duvarı kurallarını ayarlama.</span><span class="sxs-lookup"><span data-stu-id="9aba9-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="9aba9-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="9aba9-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="9aba9-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="9aba9-282">Yeni bir yetkilendirme anahtar oluşturmak ve belirtilen dosyaya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9aba9-282">Generate a new authorization key and save to the specified file.</span></span> <span data-ttu-id="9aba9-283">Oluşturulan anahtarı /Key veya/keyfile seçenekleriyle kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-283">The generated key can be used with the /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="9aba9-284">CosmosDB.Emulator.exe /GenKeyFile =&lt;anahtar dosyasının yolu&gt;</span><span class="sxs-lookup"><span data-stu-id="9aba9-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path to key file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-285">Tutarlılık</span><span class="sxs-lookup"><span data-stu-id="9aba9-285">Consistency</span></span></td>
  <td><span data-ttu-id="9aba9-286">Hesap için varsayılan tutarlılık düzeyini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9aba9-286">Set the default consistency level for the account.</span></span></td>
  <td><span data-ttu-id="9aba9-287">CosmosDB.Emulator.exe /Consistency =&lt;tutarlılık&gt;</span><span class="sxs-lookup"><span data-stu-id="9aba9-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="9aba9-288">&lt;Tutarlılık&gt;: değeri şunlardan biri olmalıdır [tutarlılık düzeylerini](consistency-levels.md): oturum, güçlü, Eventual veya BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="9aba9-288">&lt;consistency&gt;: Value must be one of the following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="9aba9-289">Varsayılan değer oturumdur.</span><span class="sxs-lookup"><span data-stu-id="9aba9-289">The default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9aba9-290">?</span><span class="sxs-lookup"><span data-stu-id="9aba9-290">?</span></span></td>
  <td><span data-ttu-id="9aba9-291">Yardım iletisi göster.</span><span class="sxs-lookup"><span data-stu-id="9aba9-291">Show the help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-the-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="9aba9-292">Azure Cosmos DB öykünücüsü Azure Cosmos DB arasındaki farklar</span><span class="sxs-lookup"><span data-stu-id="9aba9-292">Differences between the Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="9aba9-293">Azure Cosmos DB öykünücüsü yerel geliştirici istasyonunda çalıştıran benzetilmiş bir ortam sağladığından, bazı arasındaki işlevsel farklılıklar öykünücüsü ve bir Azure Cosmos DB hesap bulutta vardır:</span><span class="sxs-lookup"><span data-stu-id="9aba9-293">Because the Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure Cosmos DB account in the cloud:</span></span>

* <span data-ttu-id="9aba9-294">Azure Cosmos DB öykünücüsü yalnızca tek bir sabit hesap ve bilinen bir ana anahtar destekler.</span><span class="sxs-lookup"><span data-stu-id="9aba9-294">The Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="9aba9-295">Anahtarını yeniden üretme Azure Cosmos DB öykünücüsünde mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-295">Key regeneration is not possible in the Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="9aba9-296">Azure Cosmos DB öykünücüsü ölçeklenebilir hizmet değil ve çok sayıda koleksiyonları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="9aba9-296">The Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="9aba9-297">Azure Cosmos DB öykünücüsü farklı benzetimini değil [Azure Cosmos DB tutarlılık düzeylerini](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="9aba9-297">The Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="9aba9-298">Azure Cosmos DB öykünücüsü benzetimi yapılamadı [bölgeli çoğaltma](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="9aba9-298">The Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="9aba9-299">Azure Cosmos DB öykünücüsü Azure Cosmos DB hizmetinde (örneğin belge boyutu sınırları, artan bölümlenmiş koleksiyonu depolama alanı) bulunan hizmet kota geçersiz kılmaları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="9aba9-299">The Azure Cosmos DB Emulator does not support the service quota overrides that are available in the Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="9aba9-300">Azure Cosmos DB öykünücüsü kopyanızı Azure Cosmos DB hizmetiyle en son değişikliklerle güncel olmayabilir gibi lütfen [Azure Cosmos DB kapasite Planlayıcısı](https://www.documentdb.com/capacityplanner) doğru şekilde üretim verimlilik (RUs) gereksinimlerini tahmin etmek için uygulama.</span><span class="sxs-lookup"><span data-stu-id="9aba9-300">As your copy of the Azure Cosmos DB Emulator might not be up to date with the most recent changes with the Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="9aba9-301"><a id="set-partitioncount"></a>Koleksiyonları sayısını değiştirme</span><span class="sxs-lookup"><span data-stu-id="9aba9-301"><a id="set-partitioncount"></a>Change the number of collections</span></span>

<span data-ttu-id="9aba9-302">Varsayılan olarak, en fazla 25 tek bölüm koleksiyonları veya Azure Cosmos DB öykünücüsü kullanarak 1 bölümlenmiş koleksiyon oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9aba9-302">By default, you can create up to 25 single partition collections, or 1 partitioned collection using the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="9aba9-303">Değiştirerek **PartitionCount** değer 250 tek bölüm koleksiyonları veya 10 bölümlenmiş koleksiyonlar veya herhangi bir bileşimini 250 tek bölüm aşmayan iki kadar oluşturabilirsiniz (burada 1 bölümlenmiş koleksiyonu 25 = tek bölümlü bir koleksiyon).</span><span class="sxs-lookup"><span data-stu-id="9aba9-303">By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="9aba9-304">Geçerli bölüm sayısı aşıldı sonra bir koleksiyon oluşturmayı denerseniz, öykünücü aşağıdaki iletiyle ServiceUnavailable bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9aba9-304">If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="9aba9-305">Azure Cosmos DB öykünücüsü koleksiyonları kullanılabilir sayısını değiştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="9aba9-305">To change the number of collections available to the Azure Cosmos DB Emulator, do the following:</span></span>

1. <span data-ttu-id="9aba9-306">Sağ tıklayarak tüm yerel Azure Cosmos DB öykünücüsü verileri Sil **Azure Cosmos DB öykünücüsü** sistem tepsisi tıklatıp, ardından simgesine **veri Sıfırla...** .</span><span class="sxs-lookup"><span data-stu-id="9aba9-306">Delete all local Azure Cosmos DB Emulator data by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="9aba9-307">Bu klasörde C:\Users\user_name\AppData\Local\CosmosDBEmulator tüm öykünücüsü verileri silin.</span><span class="sxs-lookup"><span data-stu-id="9aba9-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="9aba9-308">Tüm açık örnekleri sağ tıklayarak çıkmak **Azure Cosmos DB öykünücüsü** sistem tepsisi tıklatıp, ardından simgesine **çıkış**.</span><span class="sxs-lookup"><span data-stu-id="9aba9-308">Exit all open instances by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="9aba9-309">Çıkmak tüm örnekleri için bir dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-309">It may take a minute for all instances to exit.</span></span>
4. <span data-ttu-id="9aba9-310">En son sürümünü yüklemek [Azure Cosmos DB öykünücüsü](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="9aba9-310">Install the latest version of the [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="9aba9-311">Bir değer ayarlanarak PartitionCount bayrağı öykünücü başlatma < 250 =.</span><span class="sxs-lookup"><span data-stu-id="9aba9-311">Launch the emulator with the PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="9aba9-312">Örneğin: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="9aba9-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9aba9-313">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="9aba9-313">Troubleshooting</span></span>

<span data-ttu-id="9aba9-314">Azure Cosmos DB öykünücü ile karşılaştığınız sorunları gidermeye yardımcı olması için aşağıdaki ipuçlarını kullanın:</span><span class="sxs-lookup"><span data-stu-id="9aba9-314">Use the following tips to help troubleshoot issues you encounter with the Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="9aba9-315">Öykünücü yeni bir sürümünü yüklediyseniz ve hataları yaşıyor verilerinizi sıfırlama emin olun.</span><span class="sxs-lookup"><span data-stu-id="9aba9-315">If you installed a new version of the Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="9aba9-316">Sistem tepsisindeki Azure Cosmos DB öykünücü simgesine sağ tıklayıp sıfırlama verileri tıklatarak verilerinizi sıfırlayabilirsiniz...</span><span class="sxs-lookup"><span data-stu-id="9aba9-316">You can reset your data by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="9aba9-317">Hataları çözmezse kaldırın ve uygulamayı yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9aba9-317">If that does not fix the errors, you can uninstall and reinstall the app.</span></span> <span data-ttu-id="9aba9-318">Bkz: [yerel öykünücüsü kaldırma](#uninstall) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="9aba9-318">See [Uninstall the local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="9aba9-319">Azure Cosmos DB öykünücüsü çökerse c:\Users\user_name\AppData\Local\CrashDumps klasöründen döküm dosyaları toplamak, sıkıştırmak ve e-posta ekleme [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="9aba9-319">If the Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="9aba9-320">Kilitlenme karşılaşırsanız CosmosDB.StartupEntryPoint.exe içinde bir yönetici komut isteminden aşağıdaki komutu çalıştırın:`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="9aba9-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="9aba9-321">Bir bağlantı sorunu yaşarsanız [toplamak izleme dosyaları](#trace-files)sıkıştırmak ve e-posta ekleme [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="9aba9-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="9aba9-322">Alırsanız, bir **Hizmet kullanılamıyor** ileti öykünücü başarısız ağ yığınını başlatılamadı.</span><span class="sxs-lookup"><span data-stu-id="9aba9-322">If you receive a **Service Unavailable** message, the emulator might be failing to initialize the network stack.</span></span> <span data-ttu-id="9aba9-323">Ağ filtre sürücülerini sorunu neden olabileceğinden Pulse güvenli istemci veya Juniper ağları istemcisi yüklü olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="9aba9-323">Check to see if you have the Pulse secure client or Juniper networks client installed, as their network filter drivers may cause the problem.</span></span> <span data-ttu-id="9aba9-324">Kaldırma işlemi üçüncü taraf ağ filtre sürücüleri genellikle sorunu giderir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-324">Uninstalling third party network filter drivers typically fixes the issue.</span></span>

### <span data-ttu-id="9aba9-325"><a id="trace-files"></a>İzleme dosyaları Topla</span><span class="sxs-lookup"><span data-stu-id="9aba9-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="9aba9-326">Hata ayıklama izlemeleri toplamak için bir yönetici komut isteminden aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9aba9-326">To collect debugging traces, run the following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="9aba9-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="9aba9-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="9aba9-328">Gözcü program emin olmak için sistem tepsisi kapatıldı, bir dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-328">Watch the system tray to make sure the program has shut down, it may take a minute.</span></span> <span data-ttu-id="9aba9-329">Aynı zamanda yalnızca tıklatabilirsiniz **çıkış** Azure Cosmos DB öykünücüsü kullanıcı arabiriminde.</span><span class="sxs-lookup"><span data-stu-id="9aba9-329">You can also just click **Exit** in the Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="9aba9-330">Sorunu yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9aba9-330">Reproduce the problem.</span></span> <span data-ttu-id="9aba9-331">Veri Gezgini çalışmıyorsa, yalnızca birkaç saniye hata catch açmak için tarayıcı beklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-331">If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="9aba9-332">Gidin `%ProgramFiles%\Azure Cosmos DB Emulator` ve docdbemulator_000001.etl dosyasını bulun.</span><span class="sxs-lookup"><span data-stu-id="9aba9-332">Navigate to `%ProgramFiles%\Azure Cosmos DB Emulator` and find the docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="9aba9-333">.Etl dosyası ile birlikte yeniden oluşturma adımları için gönderme [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) hata ayıklama için.</span><span class="sxs-lookup"><span data-stu-id="9aba9-333">Send the .etl file along with repro steps to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="9aba9-334"><a id="uninstall"></a>Yerel öykünücüsü kaldırma</span><span class="sxs-lookup"><span data-stu-id="9aba9-334"><a id="uninstall"></a>Uninstall the local Emulator</span></span>

1. <span data-ttu-id="9aba9-335">Tüm açık örnekleri yerel öykünücüsü sistem tepsisindeki Azure Cosmos DB öykünücü simgesine sağ tıklayıp sonra Çıkış'ı tıklatarak çıkın.</span><span class="sxs-lookup"><span data-stu-id="9aba9-335">Exit all open instances of the local Emulator by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Exit.</span></span> <span data-ttu-id="9aba9-336">Çıkmak tüm örnekleri için bir dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9aba9-336">It may take a minute for all instances to exit.</span></span>
2. <span data-ttu-id="9aba9-337">Windows Arama kutusuna yazın **uygulamalar ve Özellikler** ve tıklayın **uygulamalar ve Özellikler (sistem ayarlarını)** sonucu.</span><span class="sxs-lookup"><span data-stu-id="9aba9-337">In the Windows search box, type **Apps & features** and click on the **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="9aba9-338">Uygulamalar listesinde kaydırın **Azure Cosmos DB öykünücüsü**, onu seçin, **kaldırma**, ardından onaylayın ve tıklatın **kaldırma** yeniden.</span><span class="sxs-lookup"><span data-stu-id="9aba9-338">In the list of apps, scroll to **Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="9aba9-339">Uygulama kaldırıldığında C:\Users gidin\<kullanıcı > \AppData\Local\CosmosDBEmulator ve klasörü silin.</span><span class="sxs-lookup"><span data-stu-id="9aba9-339">When the app is uninstalled, navigate to C:\Users\<user>\AppData\Local\CosmosDBEmulator and delete the folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9aba9-340">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9aba9-340">Next steps</span></span>

<span data-ttu-id="9aba9-341">Bu öğreticide, aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="9aba9-341">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9aba9-342">Yerel öykünücüsü yüklü</span><span class="sxs-lookup"><span data-stu-id="9aba9-342">Installed the local Emulator</span></span>
> * <span data-ttu-id="9aba9-343">Rand Docker Windows öykünücüsünde</span><span class="sxs-lookup"><span data-stu-id="9aba9-343">Rand the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="9aba9-344">Kimliği doğrulanmış istekler</span><span class="sxs-lookup"><span data-stu-id="9aba9-344">Authenticated requests</span></span>
> * <span data-ttu-id="9aba9-345">Veri Gezgini öykünücüsünde kullanılır</span><span class="sxs-lookup"><span data-stu-id="9aba9-345">Used the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="9aba9-346">Dışarı aktarılan SSL sertifikaları</span><span class="sxs-lookup"><span data-stu-id="9aba9-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="9aba9-347">Komut satırından öykünücü çağrılır</span><span class="sxs-lookup"><span data-stu-id="9aba9-347">Called the Emulator from the command line</span></span>
> * <span data-ttu-id="9aba9-348">Toplanan izleme dosyaları</span><span class="sxs-lookup"><span data-stu-id="9aba9-348">Collected trace files</span></span>

<span data-ttu-id="9aba9-349">Bu öğreticide, ücretsiz yerel geliştirme için yerel öykünücüsü kullanmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="9aba9-349">In this tutorial, you've learned how to use the local Emulator for free local development.</span></span> <span data-ttu-id="9aba9-350">Şimdi, sonraki öğretici devam ve öykünücüsü SSL sertifikaları vermek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9aba9-350">You can now proceed to the next tutorial and learn how to export Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="9aba9-351">Azure Cosmos DB öykünücüsü sertifikaları verme</span><span class="sxs-lookup"><span data-stu-id="9aba9-351">Export the Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
