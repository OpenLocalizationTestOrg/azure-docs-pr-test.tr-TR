---
title: "Azure Cosmos DB: .NET API tabloda geliştirme | Microsoft Docs"
description: ".NET kullanarak Azure Cosmos veritabanı tablosu API'si ile geliştirmeyi öğrenin"
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
ms.openlocfilehash: 52cb5f2569b6c3a5301752b1e8bfb6cea13ff7f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-develop-with-the-table-api-in-net"></a><span data-ttu-id="6a026-103">Azure Cosmos DB: .NET API tabloda geliştirin</span><span class="sxs-lookup"><span data-stu-id="6a026-103">Azure Cosmos DB: Develop with the Table API in .NET</span></span>

<span data-ttu-id="6a026-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="6a026-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="6a026-105">Bu hizmetle belge, anahtar/değer ve grafik veritabanlarını kolayca oluşturup sorgulayabilir ve tüm bunları yaparken Azure Cosmos DB'nin genel dağıtım ve yatay ölçeklendirme özelliklerinden faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a026-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="6a026-106">Bu öğretici, aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="6a026-106">This tutorial covers the following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="6a026-107">Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a026-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="6a026-108">App.config dosyasında işlevselliğini etkinleştirmek</span><span class="sxs-lookup"><span data-stu-id="6a026-108">Enable functionality in the app.config file</span></span> 
> * <span data-ttu-id="6a026-109">Kullanarak bir tablo oluşturmak [tablo API](table-introduction.md) (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="6a026-109">Create a table using the [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="6a026-110">Tabloya bir varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="6a026-110">Add an entity to a table</span></span> 
> * <span data-ttu-id="6a026-111">Toplu işlem varlık yerleştirme</span><span class="sxs-lookup"><span data-stu-id="6a026-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="6a026-112">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="6a026-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="6a026-113">Otomatik ikincil dizinler kullanarak sorgu varlıklar</span><span class="sxs-lookup"><span data-stu-id="6a026-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="6a026-114">Bir varlığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="6a026-114">Replace an entity</span></span> 
> * <span data-ttu-id="6a026-115">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="6a026-115">Delete an entity</span></span> 
> * <span data-ttu-id="6a026-116">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="6a026-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="6a026-117">Azure Cosmos DB tablolarında</span><span class="sxs-lookup"><span data-stu-id="6a026-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="6a026-118">Azure Cosmos DB sağlar [tablo API](table-introduction.md) (Önizleme) bir anahtar-değer deposu Şeması daha az bir tasarım gereken uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="6a026-118">Azure Cosmos DB provides the [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="6a026-119">Azure Cosmos DB ile çalışmak için [Azure Tablo depolama](../storage/common/storage-introduction.md) SDK’ları ve REST API’ler kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6a026-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used to work with Azure Cosmos DB.</span></span> <span data-ttu-id="6a026-120">Azure Cosmos DB’yi kullanarak yüksek aktarım hızı gereksinimleri olan tablolar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a026-120">You can use Azure Cosmos DB to create tables with high throughput requirements.</span></span> <span data-ttu-id="6a026-121">Azure Cosmos DB, şu anda genel önizlemede olan, aktarım hızı açısından iyileştirilmiş tabloları (resmi olmayan adı "premium tablolar"dır) destekler.</span><span class="sxs-lookup"><span data-stu-id="6a026-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="6a026-122">Yüksek depolama, düşük aktarım hızı gereksinimleri olan tablolar için Azure Tablo depolamayı kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a026-122">You can continue to use Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="6a026-123">Azure Cosmos DB gelecekteki bir güncelleştirme depolama için iyileştirilmiş tablolar için destek getirir ve mevcut ve yeni Azure Table depolama hesaplarını Azure Cosmos DB sorunsuz bir şekilde yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="6a026-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded to Azure Cosmos DB.</span></span>

<span data-ttu-id="6a026-124">Şu anda Azure Table depolama kullanırsanız, "premium tablo" Önizleme ile aşağıdaki avantajlara sahip olursunuz:</span><span class="sxs-lookup"><span data-stu-id="6a026-124">If you currently use Azure Table storage, you gain the following benefits with the "premium table" preview:</span></span>

- <span data-ttu-id="6a026-125">Anahtar teslim [genel dağıtım](distribute-data-globally.md) birden çok giriş ile ve [otomatik ve el ile yük devretme](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="6a026-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="6a026-126">Otomatik şema tüm özelliklerini ("ikincil dizinler") ve hızlı sorguları karşı dizin belirsiz desteği</span><span class="sxs-lookup"><span data-stu-id="6a026-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="6a026-127">Desteği [depolama ve işleme bağımsız ölçeklendirme](partition-data.md), herhangi bir sayıda bölgeler arasında</span><span class="sxs-lookup"><span data-stu-id="6a026-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="6a026-128">Desteği [tablo başına ayrılmış işleme](request-units.md) , ölçeklendirilmiş istekleri saniye başına milyonlarca yüzlerce gelen</span><span class="sxs-lookup"><span data-stu-id="6a026-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds to millions of requests per second</span></span>
- <span data-ttu-id="6a026-129">Desteği [beş ince ayarlanabilir tutarlılık düzeyleri](consistency-levels.md) kullanılabilirlik, gecikme ve uygulamanıza dayalı tutarlılık kapalı ticari gerekiyor</span><span class="sxs-lookup"><span data-stu-id="6a026-129">Support for [five tunable consistency levels](consistency-levels.md) to trade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="6a026-130">tek bölge ve yüksek kullanılabilirlik için daha fazla bölgeler ekleme yeteneği içinde % 99,99 kullanılabilirlik ve [endüstri lideri kapsamlı SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/) genel kullanılabilirliğine</span><span class="sxs-lookup"><span data-stu-id="6a026-130">99.99% availability within a single region, and ability to add more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="6a026-131">Var olan Azure depolama .NET SDK'sı ile çalışma ve uygulamanız için hiçbir kod değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="6a026-131">Work with the existing Azure storage .NET SDK, and no code changes to your application</span></span>

<span data-ttu-id="6a026-132">Önizleme sırasında Azure Cosmos DB .NET SDK kullanarak tablo API destekler.</span><span class="sxs-lookup"><span data-stu-id="6a026-132">During the preview, Azure Cosmos DB supports the Table API using the .NET SDK.</span></span> <span data-ttu-id="6a026-133">İndirebilirsiniz [Azure depolama Preview SDK](https://aka.ms/premiumtablenuget) Nuget'ten, sahip aynı sınıfları ve yöntem imzaları olarak [Azure depolama SDK'sı](https://www.nuget.org/packages/WindowsAzure.Storage), ancak tablo API kullanarak Azure Cosmos DB hesaplarına da bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a026-133">You can download the [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has the same classes and method signatures as the [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect to Azure Cosmos DB accounts using the Table API.</span></span>

<span data-ttu-id="6a026-134">Karmaşık Azure Table depolama görevleri hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="6a026-134">To learn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="6a026-135">Azure Cosmos DB giriş: Tablo API</span><span class="sxs-lookup"><span data-stu-id="6a026-135">Introduction to Azure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="6a026-136">Kullanılabilir API'ler ile ilgili tam Ayrıntılar için tablo hizmeti başvuru belgelerini [.NET başvurusu için depolama istemci kitaplığı](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="6a026-136">The Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="6a026-137">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="6a026-137">About this tutorial</span></span>
<span data-ttu-id="6a026-138">Bu öğretici Azure Table storage'ı SDK bilgi sahibiyseniz ve kullanılabilir premium özellikleri kullanmak istediğiniz geliştiriciler için Azure Cosmos DB kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="6a026-138">This tutorial is for developers who are familiar with the Azure Table storage SDK, and would like to use the premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="6a026-139">Bağlı olduğu [.NET kullanarak Azure Table storage ile çalışmaya başlama](table-storage-how-to-use-dotnet.md) ve ikincil dizinler, sağlanan işleme ve birden çok giriş gibi ek özellikler yararlanmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="6a026-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how to take advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="6a026-140">Size bir Azure Cosmos DB hesabı oluşturun ve ardından derleme ve tablo uygulamayı dağıtmak için Azure portalını kullanmayı kapsar.</span><span class="sxs-lookup"><span data-stu-id="6a026-140">We cover how to use the Azure portal to create an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="6a026-141">Biz de .NET örnekleri oluşturma ve tablo, silme ve ekleme, güncelleştirme, silme ve tablo verileri Sorgulama yol.</span><span class="sxs-lookup"><span data-stu-id="6a026-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="6a026-142">Visual Studio yüklü 2017 yoksa kullanın karşıdan yükleyip **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6a026-142">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="6a026-143">Visual Studio kurulumu sırasında **Azure dağıtımını** etkinleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="6a026-143">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="6a026-144">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a026-144">Create a database account</span></span>

<span data-ttu-id="6a026-145">Azure portalında bir Azure Cosmos DB hesabı oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="6a026-145">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="6a026-146">Zaten Azure Cosmos DB hesabınız var mı?</span><span class="sxs-lookup"><span data-stu-id="6a026-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="6a026-147">Bu durumda, İleri için atlayabilirsiniz [, Visual Studio çözümü ayarlama](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="6a026-147">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="6a026-148">Bir Azure DocumentDB hesabına sahip miydiniz?</span><span class="sxs-lookup"><span data-stu-id="6a026-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="6a026-149">Bu nedenle, hesabınızı şimdi bir Azure Cosmos DB hesabı ise ve size atlayabilirsiniz [, Visual Studio çözümü ayarlama](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="6a026-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="6a026-150">Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen bölümündeki adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) öykünücü kurulması ve için İleri atlayabilirsiniz [, Visual Studio çözümünü kurmak](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="6a026-150">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting to any location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-the-sample-application"></a><span data-ttu-id="6a026-151">Örnek uygulamayı kopyalama</span><span class="sxs-lookup"><span data-stu-id="6a026-151">Clone the sample application</span></span>

<span data-ttu-id="6a026-152">Şimdi GitHub'dan bir Tablo uygulaması kopyalayalım, bağlantı dizesini ayarlayalım ve uygulamayı çalıştıralım.</span><span class="sxs-lookup"><span data-stu-id="6a026-152">Now let's clone a Table app from github, set the connection string, and run it.</span></span>

1. <span data-ttu-id="6a026-153">Git bash gibi bir git terminal penceresi açın ve `cd` ile çalışma dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="6a026-153">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="6a026-154">Örnek depoyu kopyalamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6a026-154">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="6a026-155">Ardından çözüm dosyasını Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="6a026-155">Then open the solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="6a026-156">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="6a026-156">Update your connection string</span></span>

<span data-ttu-id="6a026-157">Bu adımda Azure portalına dönerek bağlantı dizesi bilgilerinizi kopyalayıp uygulamaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6a026-157">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="6a026-158">[Azure portalında](http://portal.azure.com/), Azure Cosmos DB hesabınızın sol taraftaki gezinti menüsünden **Anahtarlar**'a ve ardından **Okuma/Yazma Anahtarları**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a026-158">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="6a026-159">Bağlantı dizesi app.config dosyasına bir sonraki adımda kopyalamak için kopya düğmeleri ekranın sağ tarafta kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="6a026-159">You'll use the copy buttons on the right side of the screen to copy the connection string into the app.config file in the next step.</span></span>

2. <span data-ttu-id="6a026-160">Visual Studio'da app.config dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="6a026-160">In Visual Studio, open the app.config file.</span></span> 

3. <span data-ttu-id="6a026-161">URI değeri (Kopyala düğmesini kullanarak) Portal'dan kopyalayın ve hesap anahtarı değerini app.config dosyasında yapın. App.config hesap adı için daha önce oluşturduğunuz hesap adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6a026-161">Copy your URI value from the portal (using the copy button) and make it the value of the account-key in app.config. Use the account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="6a026-162">Bu uygulamayı standart Azure Table Storage'ı kullanmak için bağlantı dizesinde değiştirmeniz gerekir `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="6a026-162">To use this app with standard Azure Table Storage, you need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="6a026-163">Hesap adı, Azure depolama birincil anahtarı olarak tablo hesap adı ve anahtar kullanın.</span><span class="sxs-lookup"><span data-stu-id="6a026-163">Use the account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-the-app"></a><span data-ttu-id="6a026-164">Derleme ve uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="6a026-164">Build and deploy the app</span></span>
1. <span data-ttu-id="6a026-165">Visual Studio'nun **Çözüm Gezgini** bölümünde projeye sağ tıklayın ve ardından **NuGet Paketlerini Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a026-165">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="6a026-166">NuGet'teki **Gözat** kutusuna ***WindowsAzure.Storage PremiumTable*** yazın.</span><span class="sxs-lookup"><span data-stu-id="6a026-166">In the NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="6a026-167">Denetleme **yayın öncesi sürümler dahil**.</span><span class="sxs-lookup"><span data-stu-id="6a026-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="6a026-168">Sonuçlardan yüklemek **WindowsAzure.Storage PremiumTable** ve önizleme derlemesinin seçin `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="6a026-168">From the results, install the **WindowsAzure.Storage-PremiumTable** and choose the preview build `0.0.1-preview`.</span></span> <span data-ttu-id="6a026-169">Bu eylem, Azure Table depolama paketi ve tüm bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="6a026-169">This action installs the Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="6a026-170">Uygulamayı çalıştırmak için CTRL+F5 tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="6a026-170">Click CTRL + F5 to run the application.</span></span> 

<span data-ttu-id="6a026-171">Şimdi Veri Gezgini için geri dönün ve sorgu görmek değiştirmek ve bu tablo verilerle çalışmak.</span><span class="sxs-lookup"><span data-stu-id="6a026-171">You can now go back to Data Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="6a026-172">Bu uygulamayı bir Azure Cosmos DB öykünücü ile kullanmak için bağlantı dizesini değiştirmek yeterlidir `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="6a026-172">To use this app with an Azure Cosmos DB Emulator, you just need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="6a026-173">Kullanım öykünücüsü değerin altında.</span><span class="sxs-lookup"><span data-stu-id="6a026-173">Use the below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="6a026-174">Azure Cosmos DB özellikleri</span><span class="sxs-lookup"><span data-stu-id="6a026-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="6a026-175">Azure Cosmos DB Azure Table storage ' API kullanılamaz özelliklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="6a026-175">Azure Cosmos DB supports a number of capabilities that are not available in the Azure Table storage API.</span></span> <span data-ttu-id="6a026-176">Yeni işlevselliği aşağıdaki aracılığıyla etkinleştirilebilir `appSettings` yapılandırma değerlerini.</span><span class="sxs-lookup"><span data-stu-id="6a026-176">The new functionality can be enabled via the following `appSettings` configuration values.</span></span> <span data-ttu-id="6a026-177">Biz herhangi bir yeni imzalar veya Azure depolama SDK'sını Önizleme için aşırı tanıtmak değil.</span><span class="sxs-lookup"><span data-stu-id="6a026-177">We did not introduce any new signatures or overloads to the preview Azure Storage SDK.</span></span> <span data-ttu-id="6a026-178">Bu, standart ve premium tablolara bağlanmak ve Bloblar ve kuyruklarda olduğu gibi diğer Azure Storage Hizmetleri ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6a026-178">This allows you to connect to both standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="6a026-179">Anahtar</span><span class="sxs-lookup"><span data-stu-id="6a026-179">Key</span></span> | <span data-ttu-id="6a026-180">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6a026-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6a026-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="6a026-181">TableConnectionMode</span></span>  | <span data-ttu-id="6a026-182">Azure Cosmos DB iki bağlantı modunu destekler.</span><span class="sxs-lookup"><span data-stu-id="6a026-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="6a026-183">İçinde `Gateway` modunda her zaman yapılan istekler Azure Cosmos DB ağ geçidi, karşılık gelen veri bölümleri iletir.</span><span class="sxs-lookup"><span data-stu-id="6a026-183">In `Gateway` mode, requests are always made to the Azure Cosmos DB gateway, which forwards it to the corresponding data partitions.</span></span> <span data-ttu-id="6a026-184">İçinde `Direct` bağlantı modunu istemci tabloları eşleme bölümlere getirir ve istekleri doğrudan veri bölümlerini karşı yapılır.</span><span class="sxs-lookup"><span data-stu-id="6a026-184">In `Direct` connectivity mode, the client fetches the mapping of tables to partitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="6a026-185">Öneririz `Direct`, varsayılan değer.</span><span class="sxs-lookup"><span data-stu-id="6a026-185">We recommend `Direct`, the default.</span></span>  |
| <span data-ttu-id="6a026-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="6a026-186">TableConnectionProtocol</span></span> | <span data-ttu-id="6a026-187">Azure Cosmos DB destekleyen iki bağlantı protokol - `Https` ve `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="6a026-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="6a026-188">`Tcp`varsayılan ayardır ve daha basit olduğu için önerilir.</span><span class="sxs-lookup"><span data-stu-id="6a026-188">`Tcp` is the default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="6a026-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="6a026-189">TablePreferredLocations</span></span> | <span data-ttu-id="6a026-190">Tercih edilen (çok girişli) konumları okuma için virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="6a026-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="6a026-191">Her Azure Cosmos DB hesabı 1 ile ilişkili olabilir-30 + bölgeleri.</span><span class="sxs-lookup"><span data-stu-id="6a026-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="6a026-192">Her bir istemci örnek bir alt kümesini Bu bölgeler düşük gecikme süresi okuma tercih edilen sırayı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a026-192">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="6a026-193">Bölgeleri kullanma şeklinde adlandırılmalıdır kendi [görünen adları](https://msdn.microsoft.com/library/azure/gg441293.aspx), örneğin, `West US`.</span><span class="sxs-lookup"><span data-stu-id="6a026-193">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="6a026-194">Ayrıca bkz. [birden çok giriş API'leri](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="6a026-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="6a026-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="6a026-195">TableConsistencyLevel</span></span> | <span data-ttu-id="6a026-196">Devre dışı gecikme, tutarlılık ve kullanılabilirlik arasında beş iyi tanımlanmış tutarlılık düzeyleri arasında seçerek ticari: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, ve `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="6a026-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="6a026-197">Varsayılan değer `Session`.</span><span class="sxs-lookup"><span data-stu-id="6a026-197">Default is `Session`.</span></span> <span data-ttu-id="6a026-198">Tutarlılık düzeyi seçimi önemli performans farkı bölgeli kurulumlarında yapar.</span><span class="sxs-lookup"><span data-stu-id="6a026-198">The choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="6a026-199">Bkz: [tutarlılık düzeylerini](consistency-levels.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="6a026-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="6a026-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="6a026-200">TableThroughput</span></span> | <span data-ttu-id="6a026-201">Saniye başına istek birimleri (RU) cinsinden tablo için ayrılmış işleme.</span><span class="sxs-lookup"><span data-stu-id="6a026-201">Reserved throughput for the table expressed in request units (RU) per second.</span></span> <span data-ttu-id="6a026-202">Tek tablolar 100s-RU/s milyonlarca destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="6a026-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="6a026-203">Bkz: [istek birimleri](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="6a026-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="6a026-204">Varsayılan değer`400`</span><span class="sxs-lookup"><span data-stu-id="6a026-204">Default is `400`</span></span> |
| <span data-ttu-id="6a026-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="6a026-205">TableIndexingPolicy</span></span> | <span data-ttu-id="6a026-206">Tutarlı ve otomatik ikincil tablo içindeki tüm sütunların dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a026-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="6a026-207">Dizin oluşturma ilkesi belirtimine uygun JSON dizesi.</span><span class="sxs-lookup"><span data-stu-id="6a026-207">JSON string conforming to the indexing policy specification.</span></span> <span data-ttu-id="6a026-208">Bkz: [dizin oluşturma ilkesi](indexing-policies.md) belirli sütunlardaki dahil etme/hariç tutma için dizin oluşturma ilkesi nasıl değiştiğini görmek için.</span><span class="sxs-lookup"><span data-stu-id="6a026-208">See [Indexing Policy](indexing-policies.md) to see how you can change indexing policy to include/exclude specific columns.</span></span> | <span data-ttu-id="6a026-209">Tüm özellikleri (dizeler için karma) ve numaraları aralığını otomatik dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a026-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="6a026-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="6a026-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="6a026-211">Tek gidiş dönüş tablosu sorgu başına döndürülen öğe sayısını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6a026-211">Configure the maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="6a026-212">Varsayılan değer `-1`, Azure Cosmos değer çalışma zamanında dinamik olarak belirleyen DB olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6a026-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |
| <span data-ttu-id="6a026-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="6a026-213">TableQueryEnableScan</span></span> | <span data-ttu-id="6a026-214">Sorgu için herhangi bir filtre dizini kullanamıyorsanız, ardından çalıştırın yine de bir tarama.</span><span class="sxs-lookup"><span data-stu-id="6a026-214">If the query cannot use the index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="6a026-215">Varsayılan değer `false`.</span><span class="sxs-lookup"><span data-stu-id="6a026-215">Default is `false`.</span></span>|
| <span data-ttu-id="6a026-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="6a026-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="6a026-217">Çapraz bölüm sorgusu yürütme için paralellik derecesi.</span><span class="sxs-lookup"><span data-stu-id="6a026-217">The degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="6a026-218">`0`hiçbir önceden getirme ile seri olduğu `1` olan seri önceden getirilirken ve daha yüksek değerlerle artırmak paralellik oranı.</span><span class="sxs-lookup"><span data-stu-id="6a026-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase the rate of parallelism.</span></span> <span data-ttu-id="6a026-219">Varsayılan değer `-1`, Azure Cosmos değer çalışma zamanında dinamik olarak belirleyen DB olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6a026-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |

<span data-ttu-id="6a026-220">Varsayılan değeri değiştirmek için açın `app.config` Visual Studio'daki Çözüm Gezgini'nden dosya.</span><span class="sxs-lookup"><span data-stu-id="6a026-220">To change the default value, open the `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="6a026-221">`<appSettings>` öğesinin içeriğini aşağıda gösterildiği gibi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6a026-221">Add the contents of the `<appSettings>` element shown below.</span></span> <span data-ttu-id="6a026-222">Değiştir `account-name` depolama hesabınızın adıyla ve `account-key` hesap erişim anahtarı ile.</span><span class="sxs-lookup"><span data-stu-id="6a026-222">Replace `account-name` with the name of your storage account, and `account-key` with your account access key.</span></span> 

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

<span data-ttu-id="6a026-223">Uygulamada gerçekleşen işlemleri hızlıca gözden geçirelim.</span><span class="sxs-lookup"><span data-stu-id="6a026-223">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="6a026-224">Açık `Program.cs` dosyanız varsa ve bulma Bu kod satırları tablo kaynakları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6a026-224">Open the `Program.cs` file and you find that these lines of code create the Table resources.</span></span> 

## <a name="create-the-table-client"></a><span data-ttu-id="6a026-225">Tablo istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a026-225">Create the table client</span></span>
<span data-ttu-id="6a026-226">Başlatır bir `CloudTableClient` tablo hesabınıza bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="6a026-226">You initialize a `CloudTableClient` to connect to the table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="6a026-227">Bu istemci kullanarak başlatılır `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, ve `TablePreferredLocations` uygulama ayarlarında belirtilen yapılandırma değerleri.</span><span class="sxs-lookup"><span data-stu-id="6a026-227">This client is initialized using the `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in the app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="6a026-228">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a026-228">Create a table</span></span>
<span data-ttu-id="6a026-229">Ardından, kullanarak bir tablo oluşturun `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="6a026-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="6a026-230">Azure Cosmos DB tablolarında depolama ve işleme açısından bağımsız olarak ölçeklendirebilirsiniz ve bölümlendirme hizmeti tarafından otomatik olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="6a026-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by the service.</span></span> <span data-ttu-id="6a026-231">Azure Cosmos DB sabit boyutlu ve sınırsız tabloları destekler.</span><span class="sxs-lookup"><span data-stu-id="6a026-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="6a026-232">Bkz: [Azure Cosmos DB'de bölümleme](partition-data.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="6a026-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="6a026-233">Tabloları nasıl oluşturulduğunu, önemli bir fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="6a026-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="6a026-234">Azure Cosmos DB işlemleri için Azure storage'nın tüketim tabanlı modeli farklı verimlilik ayırır.</span><span class="sxs-lookup"><span data-stu-id="6a026-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="6a026-235">Ayırma modeli iki önemli faydası vardır:</span><span class="sxs-lookup"><span data-stu-id="6a026-235">The reservation model has two key benefits:</span></span>

* <span data-ttu-id="6a026-236">Üretilen iş ayrılmış /, istek hızı düzeyinde veya altında sağlanan işleme ise, hiçbir zaman kısıtlanan için ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="6a026-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="6a026-237">Ayırma modeldir daha fazla [verimlilik yoğun iş yükleri için düşük maliyetli](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="6a026-237">The reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="6a026-238">Varsayılan işleme ayarını yapılandırarak yapılandırabileceğiniz `TableThroughput` RU (istek birimleri) / saniye cinsinden.</span><span class="sxs-lookup"><span data-stu-id="6a026-238">You can configure the default throughput by configuring the setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="6a026-239">Bir 1 KB varlığı okuma 1 olarak normalleştirilmiş RU ve diğer işlemlerin, CPU, bellek ve IOPS tüketime dayanarak sabit bir RU değere normalleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="6a026-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized to a fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="6a026-240">Daha fazla bilgi edinmek [istek birimleri Azure Cosmos veritabanı](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="6a026-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6a026-241">Tablo depolama SDK'sı şu anda değiştirme verimlilik desteklemez, ancak işleme eşzamanlı olarak Azure portalında veya Azure CLI kullanarak dilediğiniz zaman değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a026-241">While Table storage SDK does not currently support modifying throughput, you can change the throughput instantaneously at any time using the Azure portal or Azure CLI.</span></span>

<span data-ttu-id="6a026-242">Ardından, biz basit okuyun, yol ve Azure Table depolama SDK'sını kullanarak (CRUD) işlemleridir yazma.</span><span class="sxs-lookup"><span data-stu-id="6a026-242">Next, we walk through the simple read and write (CRUD) operations using the Azure Table storage SDK.</span></span> <span data-ttu-id="6a026-243">Bu öğretici, tahmin edilebilir düşük tek basamaklı milisaniyelik gecikme ve Azure Cosmos DB tarafından sağlanan hızlı sorguları gösterir.</span><span class="sxs-lookup"><span data-stu-id="6a026-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="6a026-244">Tabloya bir varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="6a026-244">Add an entity to a table</span></span>
<span data-ttu-id="6a026-245">Azure Table depolama varlıklarda genişletmek `TableEntity` sınıfı ve olmalıdır `PartitionKey` ve `RowKey` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="6a026-245">Entities in Azure Table storage extend from the `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="6a026-246">Bir müşteri varlığı için örnek tanımı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6a026-246">Here's a sample definition for a customer entity.</span></span>

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

<span data-ttu-id="6a026-247">Aşağıdaki kod parçacığında, Azure depolama SDK'sı sahip bir varlık eklemek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6a026-247">The following snippet shows how to insert an entity with the Azure storage SDK.</span></span> <span data-ttu-id="6a026-248">Azure Cosmos DB herhangi ölçekli, düşük gecikme dünya genelindeki garanti için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="6a026-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across the world.</span></span>

<span data-ttu-id="6a026-249">Yazma tamamlamak < 15 ms p99 ve Azure Cosmos DB hesabı ile aynı bölgede çalışan uygulamalar için p50 adresindeki ~ 6 ms.</span><span class="sxs-lookup"><span data-stu-id="6a026-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in the same region as the Azure Cosmos DB account.</span></span> <span data-ttu-id="6a026-250">Ve bu süre yalnızca bunlar zaman uyumlu olarak, bir işlemi tamamlandıktan sonra çoğaltılır ve tüm içeriğini dizine sonra yazma istemciye onaylanan, olgu için hesaplar.</span><span class="sxs-lookup"><span data-stu-id="6a026-250">And this duration accounts for the fact that writes are acknowledged back to the client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="6a026-251">Azure Cosmos DB tablo API önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="6a026-251">The Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="6a026-252">Genel kullanılabilirliğine p99 gecikme garanti SLA'lar gibi diğer Azure Cosmos DB API'leri tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="6a026-252">At general availability, the p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="6a026-253">Toplu işlem varlık yerleştirme</span><span class="sxs-lookup"><span data-stu-id="6a026-253">Insert a batch of entities</span></span>
<span data-ttu-id="6a026-254">Azure tablo depolama destekler, güncelleştirmelerinin birleştirmek olanak tanır, bir toplu işlem API, siler ve aynı tek toplu işlemde ekler.</span><span class="sxs-lookup"><span data-stu-id="6a026-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in the same single batch operation.</span></span> <span data-ttu-id="6a026-255">Azure Cosmos DB bazı sınırlamaları toplu işlem API Azure Table storage yok.</span><span class="sxs-lookup"><span data-stu-id="6a026-255">Azure Cosmos DB does not have some of the limitations on the batch API as Azure Table storage.</span></span> <span data-ttu-id="6a026-256">Örneğin, bir toplu iş içinde birden çok okuma yapabilirsiniz, bir toplu iş içinde aynı varlığa birden çok yazma gerçekleştirebilirsiniz ve toplu iş başına 100 işlemlerini sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="6a026-256">For example, you can perform multiple reads within a batch, you can perform multiple writes to the same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="6a026-257">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="6a026-257">Retrieve a single entity</span></span>
<span data-ttu-id="6a026-258">Tam Azure Cosmos DB'de (alır) alır < p99 ve ~ 1 10 ms p50 aynı Azure bölgesinde adresindeki ms.</span><span class="sxs-lookup"><span data-stu-id="6a026-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in the same Azure region.</span></span> <span data-ttu-id="6a026-259">Sayıda bölgeler için düşük gecikmeli okuma hesabınıza eklemek ve kendi yerel bölgesinden ("çok konaklı") ayarlayarak okumak için dağıtırken `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="6a026-259">You can add as many regions to your account for low latency reads, and deploy applications to read from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="6a026-260">Aşağıdaki kod parçacığını kullanarak tek bir varlık alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6a026-260">You can retrieve a single entity using the following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="6a026-261">Çok girişli API'leri hakkında bilgi edinin [birden çok bölgeye ile geliştirme](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="6a026-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="6a026-262">Otomatik ikincil dizinler kullanarak sorgu varlıklar</span><span class="sxs-lookup"><span data-stu-id="6a026-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="6a026-263">Tablolar sorgulanan kullanarak `TableQuery` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="6a026-263">Tables can be queried using the `TableQuery` class.</span></span> <span data-ttu-id="6a026-264">Azure Cosmos DB tablonuz içindeki tüm sütunlar otomatik olarak dizinler bir yazma iyileştirilmiş veritabanı altyapısı vardır.</span><span class="sxs-lookup"><span data-stu-id="6a026-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="6a026-265">Azure Cosmos DB'de dizin şemasına bağımsızdır.</span><span class="sxs-lookup"><span data-stu-id="6a026-265">Indexing in Azure Cosmos DB is agnostic to schema.</span></span> <span data-ttu-id="6a026-266">Bu nedenle, şemanızı satırlar arasında farklı olsa bile veya şema zamanla dönüşmesi varsa, otomatik olarak dizine alınır.</span><span class="sxs-lookup"><span data-stu-id="6a026-266">Therefore, even if your schema is different between rows, or if the schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="6a026-267">Azure Cosmos DB otomatik ikincil dizinler desteklediğinden, herhangi bir özellik sorguları dizini kullanabilir ve verimli bir şekilde sunulması.</span><span class="sxs-lookup"><span data-stu-id="6a026-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use the index and be served efficiently.</span></span>

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

<span data-ttu-id="6a026-268">Önizleme'de, Azure Cosmos DB tablo API için Azure Table storage aynı sorgu işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="6a026-268">In preview, Azure Cosmos DB supports the same query functionality as Azure Table storage for the Table API.</span></span> <span data-ttu-id="6a026-269">Azure Cosmos DB, sıralama, toplamalar, Jeo-uzamsal sorgu, hiyerarşi ve çok çeşitli yerleşik işlevler de destekler.</span><span class="sxs-lookup"><span data-stu-id="6a026-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="6a026-270">Ek işlevsellik gelecekteki hizmeti güncelleştirmesine tablo API'sindeki sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6a026-270">The additional functionality will be provided in the Table API in a future service update.</span></span> <span data-ttu-id="6a026-271">Bkz: [Azure Cosmos DB sorgusu](documentdb-sql-query.md) bu özelliklere genel bakış.</span><span class="sxs-lookup"><span data-stu-id="6a026-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="6a026-272">Bir varlığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="6a026-272">Replace an entity</span></span>
<span data-ttu-id="6a026-273">Bir varlığı güncelleştirmek için Tablo hizmetinden alın, varlık nesnesini değiştirin ve değişiklikleri Tablo hizmetine geri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6a026-273">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="6a026-274">Aşağıdaki kod mevcut bir müşterinin telefon numarasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="6a026-274">The following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="6a026-275">Benzer şekilde, gerçekleştirebileceğiniz `InsertOrMerge` veya `Merge` işlemleri.</span><span class="sxs-lookup"><span data-stu-id="6a026-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="6a026-276">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="6a026-276">Delete an entity</span></span>
<span data-ttu-id="6a026-277">Bir varlığı güncelleştirmek için gösterilen aynı yöntemi kullanarak, bir varlığı aldıktan sonra kolayca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a026-277">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="6a026-278">Aşağıdaki kod bir müşteri girişini alır ve siler.</span><span class="sxs-lookup"><span data-stu-id="6a026-278">The following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="6a026-279">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="6a026-279">Delete a table</span></span>
<span data-ttu-id="6a026-280">Son olarak aşağıdaki kod örneği bir depolama hesabından bir tablo siler.</span><span class="sxs-lookup"><span data-stu-id="6a026-280">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="6a026-281">Silin ve hemen Azure Cosmos DB içeren bir tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6a026-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="6a026-282">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="6a026-282">Clean up resources</span></span> 

<span data-ttu-id="6a026-283">Bu uygulamayı kullanmaya devam etmeyecekseniz aşağıdaki adımları kullanarak Azure portalında bu öğretici tarafından oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="6a026-283">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>   

1. <span data-ttu-id="6a026-284">Azure portalında sol taraftaki menüden, **Kaynak grupları**'na ve ardından oluşturduğunuz kaynağın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a026-284">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span>  
2. <span data-ttu-id="6a026-285">Kaynak grubu sayfanızda, **Sil**'e tıklayın, metin kutusuna silinecek kaynağın adını yazın ve ardından **Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a026-285">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6a026-286">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6a026-286">Next steps</span></span>

<span data-ttu-id="6a026-287">Bu öğretici, size Azure Cosmos DB tablo API ile kullanmaya başlamak nasıl ele ve aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="6a026-287">In this tutorial, we covered how to get started using Azure Cosmos DB with the Table API, and you've done the following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="6a026-288">Bir Azure Cosmos DB hesabı oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="6a026-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="6a026-289">App.config dosyasında etkin işlevi</span><span class="sxs-lookup"><span data-stu-id="6a026-289">Enabled functionality in the app.config file</span></span> 
> * <span data-ttu-id="6a026-290">Bir tablo oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="6a026-290">Created a table</span></span> 
> * <span data-ttu-id="6a026-291">Tabloya bir varlık eklenen</span><span class="sxs-lookup"><span data-stu-id="6a026-291">Added an entity to a table</span></span> 
> * <span data-ttu-id="6a026-292">Toplu işlem varlık eklenen</span><span class="sxs-lookup"><span data-stu-id="6a026-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="6a026-293">Tek bir varlık alınan</span><span class="sxs-lookup"><span data-stu-id="6a026-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="6a026-294">Otomatik ikincil dizinler kullanılarak sorgulanan varlıklar</span><span class="sxs-lookup"><span data-stu-id="6a026-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="6a026-295">Bir varlık değiştirildi</span><span class="sxs-lookup"><span data-stu-id="6a026-295">Replaced an entity</span></span> 
> * <span data-ttu-id="6a026-296">Bir varlık silindi</span><span class="sxs-lookup"><span data-stu-id="6a026-296">Deleted an entity</span></span> 
> * <span data-ttu-id="6a026-297">Bir tablo silindi</span><span class="sxs-lookup"><span data-stu-id="6a026-297">Deleted a table</span></span>  

<span data-ttu-id="6a026-298">Şimdi, sonraki öğretici devam etmek ve tablo verileri sorgulama hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6a026-298">You can now proceed to the next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a026-299">Tablo API sorgusu</span><span class="sxs-lookup"><span data-stu-id="6a026-299">Query with the Table API</span></span>](tutorial-query-table.md)
