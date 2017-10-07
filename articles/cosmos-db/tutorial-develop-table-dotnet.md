---
title: "Azure Cosmos DB: Merhaba tablo API .NET geliştirme | Microsoft Docs"
description: "Bilgi nasıl toodevelop .NET kullanarak Azure Cosmos veritabanı tablo API ile"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a><span data-ttu-id="a8818-103">Azure Cosmos DB: hello .NET tablo API ile geliştirme</span><span class="sxs-lookup"><span data-stu-id="a8818-103">Azure Cosmos DB: Develop with hello Table API in .NET</span></span>

<span data-ttu-id="a8818-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="a8818-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="a8818-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8818-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="a8818-106">Bu öğretici hello aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="a8818-106">This tutorial covers hello following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="a8818-107">Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8818-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="a8818-108">Merhaba app.config dosyasında işlevselliğini etkinleştirmek</span><span class="sxs-lookup"><span data-stu-id="a8818-108">Enable functionality in hello app.config file</span></span> 
> * <span data-ttu-id="a8818-109">Hello kullanarak bir tablo oluşturma [tablo API](table-introduction.md) (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="a8818-109">Create a table using hello [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="a8818-110">Bir varlık tooa tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="a8818-110">Add an entity tooa table</span></span> 
> * <span data-ttu-id="a8818-111">Toplu işlem varlık yerleştirme</span><span class="sxs-lookup"><span data-stu-id="a8818-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="a8818-112">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="a8818-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="a8818-113">Otomatik ikincil dizinler kullanarak sorgu varlıklar</span><span class="sxs-lookup"><span data-stu-id="a8818-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="a8818-114">Bir varlığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="a8818-114">Replace an entity</span></span> 
> * <span data-ttu-id="a8818-115">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="a8818-115">Delete an entity</span></span> 
> * <span data-ttu-id="a8818-116">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="a8818-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="a8818-117">Azure Cosmos DB tablolarında</span><span class="sxs-lookup"><span data-stu-id="a8818-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="a8818-118">Azure Cosmos DB sağlar hello [tablo API](table-introduction.md) (Önizleme) bir anahtar-değer deposu Şeması daha az bir tasarım gereken uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="a8818-118">Azure Cosmos DB provides hello [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="a8818-119">[Azure Table storage](../storage/common/storage-introduction.md) SDK'lar ve REST API'leri Azure Cosmos DB ile kullanılan toowork olabilir.</span><span class="sxs-lookup"><span data-stu-id="a8818-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used toowork with Azure Cosmos DB.</span></span> <span data-ttu-id="a8818-120">Yüksek verimlilik gereksinimleriyle Azure Cosmos DB toocreate tabloları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="a8818-120">You can use Azure Cosmos DB toocreate tables with high throughput requirements.</span></span> <span data-ttu-id="a8818-121">Azure Cosmos DB, şu anda genel önizlemede olan, aktarım hızı açısından iyileştirilmiş tabloları (resmi olmayan adı "premium tablolar"dır) destekler.</span><span class="sxs-lookup"><span data-stu-id="a8818-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="a8818-122">Toouse Azure Table storage yüksek depolama ve daha düşük işleme gereksinimlerine sahip tablolar için devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8818-122">You can continue toouse Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="a8818-123">Azure Cosmos DB gelecekteki bir güncelleştirme depolama için iyileştirilmiş tablolar için destek getirir ve var olan ve yeni Azure depolama hesapları sorunsuz olacaktır tablo tooAzure Cosmos DB yükseltilecektir.</span><span class="sxs-lookup"><span data-stu-id="a8818-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded tooAzure Cosmos DB.</span></span>

<span data-ttu-id="a8818-124">Şu anda Azure Table storage kullanıyorsanız, aşağıdaki yararları hello "premium tablo" preview ile Merhaba elde:</span><span class="sxs-lookup"><span data-stu-id="a8818-124">If you currently use Azure Table storage, you gain hello following benefits with hello "premium table" preview:</span></span>

- <span data-ttu-id="a8818-125">Anahtar teslim [genel dağıtım](distribute-data-globally.md) birden çok giriş ile ve [otomatik ve el ile yük devretme](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="a8818-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="a8818-126">Otomatik şema tüm özelliklerini ("ikincil dizinler") ve hızlı sorguları karşı dizin belirsiz desteği</span><span class="sxs-lookup"><span data-stu-id="a8818-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="a8818-127">Desteği [depolama ve işleme bağımsız ölçeklendirme](partition-data.md), herhangi bir sayıda bölgeler arasında</span><span class="sxs-lookup"><span data-stu-id="a8818-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="a8818-128">Desteği [tablo başına ayrılmış işleme](request-units.md) , ölçeklendirilmiş yüzlerce toomillions saniyedeki istek</span><span class="sxs-lookup"><span data-stu-id="a8818-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds toomillions of requests per second</span></span>
- <span data-ttu-id="a8818-129">Desteği [beş ince ayarlanabilir tutarlılık düzeyleri](consistency-levels.md) tootrade kapatma kullanılabilirlik, gecikme ve tutarlılık tabanlı uygulama gereksinimlerinize göre</span><span class="sxs-lookup"><span data-stu-id="a8818-129">Support for [five tunable consistency levels](consistency-levels.md) tootrade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="a8818-130">tek bir bölge ve yeteneği tooadd daha fazla içinde % 99,99 kullanılabilirlik yüksek kullanılabilirlik için bölgeler ve [endüstri lideri kapsamlı SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/) genel kullanılabilirliğine</span><span class="sxs-lookup"><span data-stu-id="a8818-130">99.99% availability within a single region, and ability tooadd more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="a8818-131">Merhaba mevcut Azure depolama .NET SDK'sı ile çalışma ve kod değişiklikleri tooyour uygulama</span><span class="sxs-lookup"><span data-stu-id="a8818-131">Work with hello existing Azure storage .NET SDK, and no code changes tooyour application</span></span>

<span data-ttu-id="a8818-132">Merhaba Önizleme sırasında Azure Cosmos DB destekler tablo hello .NET SDK kullanarak API hello.</span><span class="sxs-lookup"><span data-stu-id="a8818-132">During hello preview, Azure Cosmos DB supports hello Table API using hello .NET SDK.</span></span> <span data-ttu-id="a8818-133">Merhaba indirebilirsiniz [Azure depolama Preview SDK](https://aka.ms/premiumtablenuget) hello olan Nuget'ten, aynı sınıfları ve yöntem imzaları hello olarak [Azure depolama SDK'sı](https://www.nuget.org/packages/WindowsAzure.Storage), ancak hello kullanarak tooAzure Cosmos DB hesaplarına da bağlanabilirsiniz Tablo API.</span><span class="sxs-lookup"><span data-stu-id="a8818-133">You can download hello [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has hello same classes and method signatures as hello [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect tooAzure Cosmos DB accounts using hello Table API.</span></span>

<span data-ttu-id="a8818-134">karmaşık Azure Table depolama görevleri hakkında daha fazla toolearn bakın:</span><span class="sxs-lookup"><span data-stu-id="a8818-134">toolearn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="a8818-135">Giriş tooAzure Cosmos DB: Tablo API</span><span class="sxs-lookup"><span data-stu-id="a8818-135">Introduction tooAzure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="a8818-136">Tablo hizmeti başvuru belgelerini kullanılabilir API'ler ile ilgili tam Ayrıntılar için hello [.NET başvurusu için depolama istemci kitaplığı](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="a8818-136">hello Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="a8818-137">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="a8818-137">About this tutorial</span></span>
<span data-ttu-id="a8818-138">Bu öğretici, Azure Cosmos DB hello Azure Table depolama SDK'sı ile bilgi sahibiyseniz ve toouse hello premium özellikleri kullanılabilir istediğiniz geliştiriciler için kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="a8818-138">This tutorial is for developers who are familiar with hello Azure Table storage SDK, and would like toouse hello premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="a8818-139">Bağlı olduğu [.NET kullanarak Azure Table storage ile çalışmaya başlama](table-storage-how-to-use-dotnet.md) ve nasıl ek yeteneklerinden tootake ikincil dizinler, sağlanan işleme ve gibi birden çok giriş gösterir.</span><span class="sxs-lookup"><span data-stu-id="a8818-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how tootake advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="a8818-140">Biz nasıl toouse Azure portal toocreate bir Azure Cosmos DB hesap hello oluşturmak ve bir tablo uygulamasını dağıtmak kapsar.</span><span class="sxs-lookup"><span data-stu-id="a8818-140">We cover how toouse hello Azure portal toocreate an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="a8818-141">Biz de .NET örnekleri oluşturma ve tablo, silme ve ekleme, güncelleştirme, silme ve tablo verileri Sorgulama yol.</span><span class="sxs-lookup"><span data-stu-id="a8818-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="a8818-142">Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve hello kullan **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a8818-142">If you don't already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="a8818-143">Etkinleştirdiğinizden emin olun **Azure geliştirme** hello Visual Studio Kurulumu sırasında.</span><span class="sxs-lookup"><span data-stu-id="a8818-143">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="a8818-144">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8818-144">Create a database account</span></span>

<span data-ttu-id="a8818-145">Hello Azure portalında bir Azure Cosmos DB hesabı oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="a8818-145">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="a8818-146">Zaten Azure Cosmos DB hesabınız var mı?</span><span class="sxs-lookup"><span data-stu-id="a8818-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="a8818-147">Bu durumda, İleri çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="a8818-147">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="a8818-148">Bir Azure DocumentDB hesabına sahip miydiniz?</span><span class="sxs-lookup"><span data-stu-id="a8818-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="a8818-149">Bu nedenle, hesabınızı şimdi bir Azure Cosmos DB hesabı ise ve şimdi çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="a8818-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="a8818-150">Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) toosetup öykünücüsü hello ve İleri çok atlayabilirsiniz[, Visual Studio çözümünü kurmak](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="a8818-150">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a><span data-ttu-id="a8818-151">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="a8818-151">Clone hello sample application</span></span>

<span data-ttu-id="a8818-152">Şimdi şimdi kopyalama tablo uygulama github'dan hello bağlantı dizesini ayarlamak ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a8818-152">Now let's clone a Table app from github, set hello connection string, and run it.</span></span>

1. <span data-ttu-id="a8818-153">Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="a8818-153">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="a8818-154">Çalışma hello aşağıdaki tooclone hello örnek depo komutu.</span><span class="sxs-lookup"><span data-stu-id="a8818-154">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="a8818-155">Ardından Visual Studio'da hello çözüm dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="a8818-155">Then open hello solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="a8818-156">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="a8818-156">Update your connection string</span></span>

<span data-ttu-id="a8818-157">Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="a8818-157">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="a8818-158">Merhaba, [Azure portal](http://portal.azure.com/), Azure Cosmos DB hesap, sol gezinti hello tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="a8818-158">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="a8818-159">Merhaba sonraki adımda hello app.config dosyasına hello sağ tarafında Merhaba ekranında toocopy hello bağlantı dizesi hello Kopyala düğmesi kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a8818-159">You'll use hello copy buttons on hello right side of hello screen toocopy hello connection string into hello app.config file in hello next step.</span></span>

2. <span data-ttu-id="a8818-160">Visual Studio'da hello app.config dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="a8818-160">In Visual Studio, open hello app.config file.</span></span> 

3. <span data-ttu-id="a8818-161">URI değeri (Merhaba Kopyala düğmesini kullanarak) hello Portal'dan kopyalayın ve hale hello app.config hello hesabı-anahtar değeri. App.config hesap adı için daha önce oluşturduğunuz hello hesap adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a8818-161">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello account-key in app.config. Use hello account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="a8818-162">toouse bu uygulama standart Azure tablo depolaması ile toochange hello bağlantı dizesinde gereken `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="a8818-162">toouse this app with standard Azure Table Storage, you need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="a8818-163">Merhaba hesap adı, Azure depolama birincil anahtarı olarak tablo hesap adı ve anahtar kullanın.</span><span class="sxs-lookup"><span data-stu-id="a8818-163">Use hello account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a><span data-ttu-id="a8818-164">Derleme ve hello uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="a8818-164">Build and deploy hello app</span></span>
1. <span data-ttu-id="a8818-165">Visual Studio'da hello projeye sağ tıklayın **Çözüm Gezgini** ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="a8818-165">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="a8818-166">Merhaba NuGet içinde **Gözat** kutusuna ***WindowsAzure.Storage PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="a8818-166">In hello NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="a8818-167">Denetleme **yayın öncesi sürümler dahil**.</span><span class="sxs-lookup"><span data-stu-id="a8818-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="a8818-168">Merhaba sonuçlarından hello yüklemek **WindowsAzure.Storage PremiumTable** ve hello Önizleme derlemesinin seçin `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="a8818-168">From hello results, install hello **WindowsAzure.Storage-PremiumTable** and choose hello preview build `0.0.1-preview`.</span></span> <span data-ttu-id="a8818-169">Bu eylemin hello Azure Table depolama paketi ve tüm bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="a8818-169">This action installs hello Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="a8818-170">CTRL + F5'e tıklayın toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a8818-170">Click CTRL + F5 toorun hello application.</span></span> 

<span data-ttu-id="a8818-171">Şimdi tooData Explorer geri dönün ve sorgu görmek değiştirmek ve bu tablo verilerle çalışmak.</span><span class="sxs-lookup"><span data-stu-id="a8818-171">You can now go back tooData Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="a8818-172">toouse bu uygulama ile bir Azure Cosmos DB öykünücü, yalnızca size gereken toochange hello bağlantı dizesinde `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="a8818-172">toouse this app with an Azure Cosmos DB Emulator, you just need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="a8818-173">Değerin altında Hello öykünücüsü kullanın.</span><span class="sxs-lookup"><span data-stu-id="a8818-173">Use hello below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="a8818-174">Azure Cosmos DB özellikleri</span><span class="sxs-lookup"><span data-stu-id="a8818-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="a8818-175">Azure Cosmos DB hello Azure Table storage API'si kullanılamaz özelliklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="a8818-175">Azure Cosmos DB supports a number of capabilities that are not available in hello Azure Table storage API.</span></span> <span data-ttu-id="a8818-176">Merhaba yeni işlevsellik hello aşağıdaki aracılığıyla etkinleştirilebilir `appSettings` yapılandırma değerlerini.</span><span class="sxs-lookup"><span data-stu-id="a8818-176">hello new functionality can be enabled via hello following `appSettings` configuration values.</span></span> <span data-ttu-id="a8818-177">Biz herhangi yeni imzalar veya aşırı toohello Önizleme Azure depolama SDK'sını tanıtmak değil.</span><span class="sxs-lookup"><span data-stu-id="a8818-177">We did not introduce any new signatures or overloads toohello preview Azure Storage SDK.</span></span> <span data-ttu-id="a8818-178">Bu, tooconnect tooboth standart ve premium tablolar ve Bloblar ve kuyruklarda olduğu gibi diğer Azure Storage Hizmetleri ile iş sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8818-178">This allows you tooconnect tooboth standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="a8818-179">Anahtar</span><span class="sxs-lookup"><span data-stu-id="a8818-179">Key</span></span> | <span data-ttu-id="a8818-180">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a8818-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a8818-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="a8818-181">TableConnectionMode</span></span>  | <span data-ttu-id="a8818-182">Azure Cosmos DB iki bağlantı modunu destekler.</span><span class="sxs-lookup"><span data-stu-id="a8818-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="a8818-183">İçinde `Gateway` modu, istekleri her zaman yapılan toohello karşılık gelen veri bölümlerini iletir toohello Azure Cosmos DB gateway.</span><span class="sxs-lookup"><span data-stu-id="a8818-183">In `Gateway` mode, requests are always made toohello Azure Cosmos DB gateway, which forwards it toohello corresponding data partitions.</span></span> <span data-ttu-id="a8818-184">İçinde `Direct` bağlantı modunu hello istemci tabloları toopartitions hello eşlenmesini getirir ve istekleri doğrudan veri bölümlerini karşı yapılır.</span><span class="sxs-lookup"><span data-stu-id="a8818-184">In `Direct` connectivity mode, hello client fetches hello mapping of tables toopartitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="a8818-185">Öneririz `Direct`, hello varsayılan.</span><span class="sxs-lookup"><span data-stu-id="a8818-185">We recommend `Direct`, hello default.</span></span>  |
| <span data-ttu-id="a8818-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="a8818-186">TableConnectionProtocol</span></span> | <span data-ttu-id="a8818-187">Azure Cosmos DB destekleyen iki bağlantı protokol - `Https` ve `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="a8818-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="a8818-188">`Tcp`Merhaba varsayılandır ve daha basit olduğu için önerilir.</span><span class="sxs-lookup"><span data-stu-id="a8818-188">`Tcp` is hello default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="a8818-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="a8818-189">TablePreferredLocations</span></span> | <span data-ttu-id="a8818-190">Tercih edilen (çok girişli) konumları okuma için virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="a8818-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="a8818-191">Her Azure Cosmos DB hesabı 1 ile ilişkili olabilir-30 + bölgeleri.</span><span class="sxs-lookup"><span data-stu-id="a8818-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="a8818-192">Her istemci örneği, düşük gecikme süresi okumalar için tercih edilen hello sırayla Bu bölgeler kümesini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8818-192">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="a8818-193">Merhaba bölgeler gerekir adlı kullanarak kendi [görünen adları](https://msdn.microsoft.com/library/azure/gg441293.aspx), örneğin, `West US`.</span><span class="sxs-lookup"><span data-stu-id="a8818-193">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="a8818-194">Ayrıca bkz. [birden çok giriş API'leri](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="a8818-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="a8818-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="a8818-195">TableConsistencyLevel</span></span> | <span data-ttu-id="a8818-196">Devre dışı gecikme, tutarlılık ve kullanılabilirlik arasında beş iyi tanımlanmış tutarlılık düzeyleri arasında seçerek ticari: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, ve `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="a8818-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="a8818-197">Varsayılan değer `Session`.</span><span class="sxs-lookup"><span data-stu-id="a8818-197">Default is `Session`.</span></span> <span data-ttu-id="a8818-198">Tutarlılık düzeyi Hello seçimine önemli performans farkı bölgeli kurulumlarında yapar.</span><span class="sxs-lookup"><span data-stu-id="a8818-198">hello choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="a8818-199">Bkz: [tutarlılık düzeylerini](consistency-levels.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="a8818-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="a8818-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="a8818-200">TableThroughput</span></span> | <span data-ttu-id="a8818-201">Saniye başına istek birimleri (RU) cinsinden hello tablo için ayrılmış işleme.</span><span class="sxs-lookup"><span data-stu-id="a8818-201">Reserved throughput for hello table expressed in request units (RU) per second.</span></span> <span data-ttu-id="a8818-202">Tek tablolar 100s-RU/s milyonlarca destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="a8818-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="a8818-203">Bkz: [istek birimleri](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="a8818-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="a8818-204">Varsayılan değer`400`</span><span class="sxs-lookup"><span data-stu-id="a8818-204">Default is `400`</span></span> |
| <span data-ttu-id="a8818-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="a8818-205">TableIndexingPolicy</span></span> | <span data-ttu-id="a8818-206">Tutarlı ve otomatik ikincil tablo içindeki tüm sütunların dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8818-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="a8818-207">JSON İlkesi belirtimi dizin uyumlu toohello dize.</span><span class="sxs-lookup"><span data-stu-id="a8818-207">JSON string conforming toohello indexing policy specification.</span></span> <span data-ttu-id="a8818-208">Bkz: [dizin oluşturma ilkesi](indexing-policies.md) toosee dizin oluşturma ilkesi tooinclude/çıkarma belirli sütunlardaki nasıl değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8818-208">See [Indexing Policy](indexing-policies.md) toosee how you can change indexing policy tooinclude/exclude specific columns.</span></span> | <span data-ttu-id="a8818-209">Tüm özellikleri (dizeler için karma) ve numaraları aralığını otomatik dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8818-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="a8818-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="a8818-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="a8818-211">Merhaba maksimum tek gidiş dönüş tablosu sorgu başına döndürülen öğe sayısını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a8818-211">Configure hello maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="a8818-212">Varsayılan değer `-1`, Azure Cosmos hello değer çalışma zamanında dinamik olarak belirleyen DB olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8818-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |
| <span data-ttu-id="a8818-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="a8818-213">TableQueryEnableScan</span></span> | <span data-ttu-id="a8818-214">Merhaba sorgu hello dizin için herhangi bir filtre kullanamıyorsanız, ardından çalıştırın yine de bir tarama.</span><span class="sxs-lookup"><span data-stu-id="a8818-214">If hello query cannot use hello index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="a8818-215">Varsayılan değer `false`.</span><span class="sxs-lookup"><span data-stu-id="a8818-215">Default is `false`.</span></span>|
| <span data-ttu-id="a8818-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="a8818-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="a8818-217">Çapraz bölüm sorgusu yürütme için paralellik derecesi Hello.</span><span class="sxs-lookup"><span data-stu-id="a8818-217">hello degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="a8818-218">`0`hiçbir önceden getirme ile seri olduğu `1` önceden getirme ile seri ve daha yüksek değerlerini tutan paralellik artış hello oranı.</span><span class="sxs-lookup"><span data-stu-id="a8818-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase hello rate of parallelism.</span></span> <span data-ttu-id="a8818-219">Varsayılan değer `-1`, Azure Cosmos hello değer çalışma zamanında dinamik olarak belirleyen DB olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8818-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |

<span data-ttu-id="a8818-220">toochange hello varsayılan değer, açık hello `app.config` Visual Studio'daki Çözüm Gezgini'nden dosya.</span><span class="sxs-lookup"><span data-stu-id="a8818-220">toochange hello default value, open hello `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="a8818-221">Merhaba Merhaba içeriğine Ekle `<appSettings>` aşağıda gösterilen öğesi.</span><span class="sxs-lookup"><span data-stu-id="a8818-221">Add hello contents of hello `<appSettings>` element shown below.</span></span> <span data-ttu-id="a8818-222">Değiştir `account-name` depolama hesabınızın hello adla ve `account-key` hesap erişim anahtarı ile.</span><span class="sxs-lookup"><span data-stu-id="a8818-222">Replace `account-name` with hello name of your storage account, and `account-key` with your account access key.</span></span> 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

<span data-ttu-id="a8818-223">Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım.</span><span class="sxs-lookup"><span data-stu-id="a8818-223">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="a8818-224">Açık hello `Program.cs` dosyanız varsa ve bulma Bu kod satırları hello tablo kaynakları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8818-224">Open hello `Program.cs` file and you find that these lines of code create hello Table resources.</span></span> 

## <a name="create-hello-table-client"></a><span data-ttu-id="a8818-225">Merhaba tablo istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8818-225">Create hello table client</span></span>
<span data-ttu-id="a8818-226">Başlatır bir `CloudTableClient` tooconnect toohello tablo hesabı.</span><span class="sxs-lookup"><span data-stu-id="a8818-226">You initialize a `CloudTableClient` tooconnect toohello table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="a8818-227">Bu istemci hello kullanarak başlatılır `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, ve `TablePreferredLocations` hello uygulama ayarlarında belirtilen yapılandırma değerleri.</span><span class="sxs-lookup"><span data-stu-id="a8818-227">This client is initialized using hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in hello app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="a8818-228">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8818-228">Create a table</span></span>
<span data-ttu-id="a8818-229">Ardından, kullanarak bir tablo oluşturun `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="a8818-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="a8818-230">Azure Cosmos DB tablolarında depolama ve işleme açısından bağımsız olarak ölçeklendirebilirsiniz ve bölümleme hello hizmeti tarafından otomatik olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a8818-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by hello service.</span></span> <span data-ttu-id="a8818-231">Azure Cosmos DB sabit boyutlu ve sınırsız tabloları destekler.</span><span class="sxs-lookup"><span data-stu-id="a8818-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="a8818-232">Bkz: [Azure Cosmos DB'de bölümleme](partition-data.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="a8818-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="a8818-233">Tabloları nasıl oluşturulduğunu, önemli bir fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="a8818-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="a8818-234">Azure Cosmos DB işlemleri için Azure storage'nın tüketim tabanlı modeli farklı verimlilik ayırır.</span><span class="sxs-lookup"><span data-stu-id="a8818-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="a8818-235">Merhaba ayırma modeli iki önemli faydası vardır:</span><span class="sxs-lookup"><span data-stu-id="a8818-235">hello reservation model has two key benefits:</span></span>

* <span data-ttu-id="a8818-236">Üretilen iş ayrılmış /, istek hızı düzeyinde veya altında sağlanan işleme ise, hiçbir zaman kısıtlanan için ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="a8818-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="a8818-237">Merhaba ayırma modeli daha fazla [verimlilik yoğun iş yükleri için düşük maliyetli](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="a8818-237">hello reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="a8818-238">Merhaba ayarını yapılandırarak hello varsayılan işleme yapılandırabilirsiniz `TableThroughput` RU (istek birimleri) / saniye cinsinden.</span><span class="sxs-lookup"><span data-stu-id="a8818-238">You can configure hello default throughput by configuring hello setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="a8818-239">Bir 1 KB varlığı okuma 1 olarak normalleştirilmiş RU ve diğer işlemlerin, CPU, bellek ve IOPS tüketime dayanarak RU değeri sabit normalleştirilmiş tooa olan.</span><span class="sxs-lookup"><span data-stu-id="a8818-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized tooa fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="a8818-240">Daha fazla bilgi edinmek [istek birimleri Azure Cosmos veritabanı](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="a8818-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a8818-241">Tablo depolama SDK'sı şu anda değiştirme verimlilik desteklemez, ancak hello verimlilik eşzamanlı olarak hello Azure portalında veya Azure CLI kullanarak dilediğiniz zaman değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8818-241">While Table storage SDK does not currently support modifying throughput, you can change hello throughput instantaneously at any time using hello Azure portal or Azure CLI.</span></span>

<span data-ttu-id="a8818-242">Ardından, biz hello basit okuyun, yol ve hello Azure Table depolama SDK'sını kullanarak (CRUD) işlemleridir yazma.</span><span class="sxs-lookup"><span data-stu-id="a8818-242">Next, we walk through hello simple read and write (CRUD) operations using hello Azure Table storage SDK.</span></span> <span data-ttu-id="a8818-243">Bu öğretici, tahmin edilebilir düşük tek basamaklı milisaniyelik gecikme ve Azure Cosmos DB tarafından sağlanan hızlı sorguları gösterir.</span><span class="sxs-lookup"><span data-stu-id="a8818-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="a8818-244">Bir varlık tooa tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="a8818-244">Add an entity tooa table</span></span>
<span data-ttu-id="a8818-245">Azure Table depolama varlıklarda genişletmek hello `TableEntity` sınıfı ve olmalıdır `PartitionKey` ve `RowKey` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="a8818-245">Entities in Azure Table storage extend from hello `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="a8818-246">Bir müşteri varlığı için örnek tanımı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a8818-246">Here's a sample definition for a customer entity.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="a8818-247">Aşağıdaki kod parçacığında hello nasıl tooinsert varlıkla bir hello Azure depolama SDK'sı gösterir.</span><span class="sxs-lookup"><span data-stu-id="a8818-247">hello following snippet shows how tooinsert an entity with hello Azure storage SDK.</span></span> <span data-ttu-id="a8818-248">Azure Cosmos DB herhangi ölçekli, düşük gecikme süresi Merhaba dünya genelindeki garanti için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a8818-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across hello world.</span></span>

<span data-ttu-id="a8818-249">Yazma tamamlamak < 15 ms p99 ve çalışan uygulamalar için p50 adresindeki ~ 6 ms hello hello Azure Cosmos DB hesabı ile aynı bölgeye.</span><span class="sxs-lookup"><span data-stu-id="a8818-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in hello same region as hello Azure Cosmos DB account.</span></span> <span data-ttu-id="a8818-250">Ve bu süre Yazar hello bulgusunun hesapları geri toohello istemci yalnızca bunlar zaman uyumlu olarak, bir işlemi tamamlandıktan sonra çoğaltılır ve tüm içeriğini dizine sonra onaylanan.</span><span class="sxs-lookup"><span data-stu-id="a8818-250">And this duration accounts for hello fact that writes are acknowledged back toohello client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="a8818-251">Hello Azure Cosmos DB için tablo API önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="a8818-251">hello Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="a8818-252">Genel kullanılabilirliğine hello p99 gecikme garanti SLA'lar gibi diğer Azure Cosmos DB API'leri tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a8818-252">At general availability, hello p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="a8818-253">Toplu işlem varlık yerleştirme</span><span class="sxs-lookup"><span data-stu-id="a8818-253">Insert a batch of entities</span></span>
<span data-ttu-id="a8818-254">Azure tablo depolama destekler olanak sağlayan bir toplu işlem API güncelleştirmeleri, siler, birleştirme ve ekleme aynı tek toplu işlem hello.</span><span class="sxs-lookup"><span data-stu-id="a8818-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in hello same single batch operation.</span></span> <span data-ttu-id="a8818-255">Azure Cosmos DB hello sınırlamaları bazıları hello toplu işlem API Azure Table storage yok.</span><span class="sxs-lookup"><span data-stu-id="a8818-255">Azure Cosmos DB does not have some of hello limitations on hello batch API as Azure Table storage.</span></span> <span data-ttu-id="a8818-256">Örneğin, bir toplu iş içinde birden çok okuma yapabilirsiniz, birden çok yazma toohello gerçekleştirebileceğiniz bir yığın içindeki aynı varlık ve toplu iş başına 100 işlemlerini sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="a8818-256">For example, you can perform multiple reads within a batch, you can perform multiple writes toohello same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="a8818-257">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="a8818-257">Retrieve a single entity</span></span>
<span data-ttu-id="a8818-258">Tam Azure Cosmos DB'de (alır) alır < 10 ms p99 ve ~ 1 ms içinde p50 adresindeki hello aynı Azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="a8818-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in hello same Azure region.</span></span> <span data-ttu-id="a8818-259">Düşük gecikme süresi okumalar sayıda bölgeleri tooyour hesabını ekleyin ve kendi yerel bölgesinden ("çok konaklı") uygulamaları tooread ayarlayarak dağıtmak `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="a8818-259">You can add as many regions tooyour account for low latency reads, and deploy applications tooread from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="a8818-260">Aşağıdaki kod parçacığında hello kullanarak tek bir varlık alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a8818-260">You can retrieve a single entity using hello following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="a8818-261">Çok girişli API'leri hakkında bilgi edinin [birden çok bölgeye ile geliştirme](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="a8818-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="a8818-262">Otomatik ikincil dizinler kullanarak sorgu varlıklar</span><span class="sxs-lookup"><span data-stu-id="a8818-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="a8818-263">Tablolar sorgulanan hello kullanarak `TableQuery` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="a8818-263">Tables can be queried using hello `TableQuery` class.</span></span> <span data-ttu-id="a8818-264">Azure Cosmos DB tablonuz içindeki tüm sütunlar otomatik olarak dizinler bir yazma iyileştirilmiş veritabanı altyapısı vardır.</span><span class="sxs-lookup"><span data-stu-id="a8818-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="a8818-265">Azure Cosmos DB'de dizin belirsiz tooschema olur.</span><span class="sxs-lookup"><span data-stu-id="a8818-265">Indexing in Azure Cosmos DB is agnostic tooschema.</span></span> <span data-ttu-id="a8818-266">Bu nedenle, şemanızı satırlar arasında farklı olsa bile veya hello şema zamanla dönüşmesi varsa, otomatik olarak dizine alınır.</span><span class="sxs-lookup"><span data-stu-id="a8818-266">Therefore, even if your schema is different between rows, or if hello schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="a8818-267">Azure Cosmos DB otomatik ikincil dizinler desteklediğinden, herhangi bir özellik sorguları hello dizini kullanabilir ve verimli bir şekilde sunulması.</span><span class="sxs-lookup"><span data-stu-id="a8818-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use hello index and be served efficiently.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

<span data-ttu-id="a8818-268">Önizleme'de, Azure Cosmos DB hello destekler aynı sorgu Azure Table storage'hello tablo API için işlevselliği.</span><span class="sxs-lookup"><span data-stu-id="a8818-268">In preview, Azure Cosmos DB supports hello same query functionality as Azure Table storage for hello Table API.</span></span> <span data-ttu-id="a8818-269">Azure Cosmos DB, sıralama, toplamalar, Jeo-uzamsal sorgu, hiyerarşi ve çok çeşitli yerleşik işlevler de destekler.</span><span class="sxs-lookup"><span data-stu-id="a8818-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="a8818-270">Merhaba ek işlevsellik gelecekteki hizmet güncelleştirmesi hello tablo API sağlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8818-270">hello additional functionality will be provided in hello Table API in a future service update.</span></span> <span data-ttu-id="a8818-271">Bkz: [Azure Cosmos DB sorgusu](documentdb-sql-query.md) bu özelliklere genel bakış.</span><span class="sxs-lookup"><span data-stu-id="a8818-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="a8818-272">Bir varlığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="a8818-272">Replace an entity</span></span>
<span data-ttu-id="a8818-273">bir varlık tooupdate hello tablo hizmetinden alın, hello varlık nesnesini değiştirin ve ardından hello Değişiklikleri Kaydet toohello tablo hizmeti yeniden.</span><span class="sxs-lookup"><span data-stu-id="a8818-273">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="a8818-274">Merhaba aşağıdaki kod mevcut bir müşterinin telefon numarasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="a8818-274">hello following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="a8818-275">Benzer şekilde, gerçekleştirebileceğiniz `InsertOrMerge` veya `Merge` işlemleri.</span><span class="sxs-lookup"><span data-stu-id="a8818-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="a8818-276">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="a8818-276">Delete an entity</span></span>
<span data-ttu-id="a8818-277">Hello kullanarak aldıktan sonra bir varlık kolayca silebilirsiniz bir varlığı güncelleştirmek için gösterilen aynı düzeni.</span><span class="sxs-lookup"><span data-stu-id="a8818-277">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="a8818-278">koddan hello alır ve bir müşteri varlığı siler.</span><span class="sxs-lookup"><span data-stu-id="a8818-278">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="a8818-279">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="a8818-279">Delete a table</span></span>
<span data-ttu-id="a8818-280">Son olarak, aşağıdaki kod örneğine hello bir depolama hesabından bir tablo siler.</span><span class="sxs-lookup"><span data-stu-id="a8818-280">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="a8818-281">Silin ve hemen Azure Cosmos DB içeren bir tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8818-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="a8818-282">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="a8818-282">Clean up resources</span></span> 

<span data-ttu-id="a8818-283">Bu uygulama toocontinue toouse denetlemeyecekseniz tüm kaynaklar Bu öğreticide hello Azure portal tarafından oluşturulan adımları toodelete aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="a8818-283">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>   

1. <span data-ttu-id="a8818-284">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a8818-284">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span>  
2. <span data-ttu-id="a8818-285">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="a8818-285">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a8818-286">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a8818-286">Next steps</span></span>

<span data-ttu-id="a8818-287">Bu öğreticide tooget hello tablo API ile Azure Cosmos DB kullanarak çalışmaya nasıl ele ve hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="a8818-287">In this tutorial, we covered how tooget started using Azure Cosmos DB with hello Table API, and you've done hello following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="a8818-288">Bir Azure Cosmos DB hesabı oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="a8818-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="a8818-289">Merhaba app.config dosyasında etkin işlevi</span><span class="sxs-lookup"><span data-stu-id="a8818-289">Enabled functionality in hello app.config file</span></span> 
> * <span data-ttu-id="a8818-290">Bir tablo oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="a8818-290">Created a table</span></span> 
> * <span data-ttu-id="a8818-291">Bir varlık tooa tablo eklendi</span><span class="sxs-lookup"><span data-stu-id="a8818-291">Added an entity tooa table</span></span> 
> * <span data-ttu-id="a8818-292">Toplu işlem varlık eklenen</span><span class="sxs-lookup"><span data-stu-id="a8818-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="a8818-293">Tek bir varlık alınan</span><span class="sxs-lookup"><span data-stu-id="a8818-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="a8818-294">Otomatik ikincil dizinler kullanılarak sorgulanan varlıklar</span><span class="sxs-lookup"><span data-stu-id="a8818-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="a8818-295">Bir varlık değiştirildi</span><span class="sxs-lookup"><span data-stu-id="a8818-295">Replaced an entity</span></span> 
> * <span data-ttu-id="a8818-296">Bir varlık silindi</span><span class="sxs-lookup"><span data-stu-id="a8818-296">Deleted an entity</span></span> 
> * <span data-ttu-id="a8818-297">Bir tablo silindi</span><span class="sxs-lookup"><span data-stu-id="a8818-297">Deleted a table</span></span>  

<span data-ttu-id="a8818-298">Şimdi toohello sonraki öğretici devam ve tablo verileri sorgulama hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="a8818-298">You can now proceed toohello next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="a8818-299">Tablo API Hello ile sorgulama</span><span class="sxs-lookup"><span data-stu-id="a8818-299">Query with hello Table API</span></span>](tutorial-query-table.md)
