---
title: "aaaHow tooData profil veri kaynakları"
description: "Azure veri Kataloğu'nda veri kaynaklarını kaydederek zaman tooinclude tablo ve sütun düzeyi verileri nasıl profilleri ve toouse veri toounderstand veri kaynaklarını nasıl profilleri vurgulama nasıl-tooarticle."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="44ae9-103">Veri profili veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="44ae9-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="44ae9-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="44ae9-104">Introduction</span></span>
<span data-ttu-id="44ae9-105">**Microsoft Azure veri Kataloğu** bir kayıt ve sistemi kurumsal veri kaynakları için bulma görevi gören bir tam olarak yönetilen bir bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="44ae9-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="44ae9-106">Diğer bir deyişle, **Azure veri Kataloğu** tüm yardımcı kişilerle ilgili bulmak, anlamak ve veri kaynaklarını kullanmak ve kuruluşların tooget yardımcı olacak daha fazla kendi varolan veriler değeri.</span><span class="sxs-lookup"><span data-stu-id="44ae9-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data.</span></span> <span data-ttu-id="44ae9-107">Ne zaman bir veri kaynağı kayıtlı ile **Azure veri Kataloğu**, meta verilerini kopyalanır ve hello hizmeti tarafından dizine ancak hello Öykü yok uç.</span><span class="sxs-lookup"><span data-stu-id="44ae9-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span>

<span data-ttu-id="44ae9-108">Merhaba **profil oluşturma verilerini** özelliği **Azure veri Kataloğu** hello veri kataloğunuzu desteklenen veri kaynaklarından inceler ve istatistikleri ve bu verileri hakkında bilgiler toplar.</span><span class="sxs-lookup"><span data-stu-id="44ae9-108">hello **Data Profiling** feature of **Azure Data Catalog** examines hello data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="44ae9-109">Kolay tooinclude veri varlıklarınız profilini olur.</span><span class="sxs-lookup"><span data-stu-id="44ae9-109">It's easy tooinclude a profile of your data assets.</span></span> <span data-ttu-id="44ae9-110">Bir veri varlığına kaydederken seçin **dahil veri profili** hello veri kaynağı kayıt aracında.</span><span class="sxs-lookup"><span data-stu-id="44ae9-110">When you register a data asset, choose **Include Data Profile** in hello data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="44ae9-111">Profil oluşturma verilerini nedir</span><span class="sxs-lookup"><span data-stu-id="44ae9-111">What is Data Profiling</span></span>
<span data-ttu-id="44ae9-112">Profil oluşturma verilerini hello veri Kaydedilmekte hello veri kaynağındaki inceler ve istatistikleri ve bu verileri hakkında bilgiler toplar.</span><span class="sxs-lookup"><span data-stu-id="44ae9-112">Data profiling examines hello data in hello data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="44ae9-113">Veri kaynağı bulma sırasında bu İstatistikler hello veri toosolve hello uygunluğunu iş sorunlarını belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="44ae9-113">During data source discovery, these statistics can help you determine hello suitability of hello data toosolve their business problem.</span></span>

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

<span data-ttu-id="44ae9-114">Merhaba aşağıdaki veri kaynakları profil oluşturma verilerini destekler:</span><span class="sxs-lookup"><span data-stu-id="44ae9-114">hello following data sources support data profiling:</span></span>

* <span data-ttu-id="44ae9-115">SQL Server'ın (Azure SQL DB ve Azure SQL Data Warehouse dahil) tabloları ve görünümleri</span><span class="sxs-lookup"><span data-stu-id="44ae9-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="44ae9-116">Oracle tabloları ve görünümleri</span><span class="sxs-lookup"><span data-stu-id="44ae9-116">Oracle tables and views</span></span>
* <span data-ttu-id="44ae9-117">Teradata tabloları ve görünümleri</span><span class="sxs-lookup"><span data-stu-id="44ae9-117">Teradata tables and views</span></span>
* <span data-ttu-id="44ae9-118">Hive tabloları</span><span class="sxs-lookup"><span data-stu-id="44ae9-118">Hive tables</span></span>

<span data-ttu-id="44ae9-119">Veri varlıklarını kaydetme kullanıcılar yardımcı olduğunda dahil olmak üzere veri profilleri de dahil olmak üzere, veri kaynakları ile ilgili soruları yanıtlayın:</span><span class="sxs-lookup"><span data-stu-id="44ae9-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="44ae9-120">Bunu iş sorunumu kullanılan toosolve olabilir?</span><span class="sxs-lookup"><span data-stu-id="44ae9-120">Can it be used toosolve my business problem?</span></span>
* <span data-ttu-id="44ae9-121">Merhaba verileri tooparticular standartları veya kalıp uygun mu?</span><span class="sxs-lookup"><span data-stu-id="44ae9-121">Does hello data conform tooparticular standards or patterns?</span></span>
* <span data-ttu-id="44ae9-122">Bazı hello anormallikleri hello veri kaynağının nelerdir?</span><span class="sxs-lookup"><span data-stu-id="44ae9-122">What are some of hello anomalies of hello data source?</span></span>
* <span data-ttu-id="44ae9-123">Bu veriler my uygulamasına tümleştirme olası zorluklar nelerdir?</span><span class="sxs-lookup"><span data-stu-id="44ae9-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="44ae9-124">Verileri bir uygulamaya nasıl tümleşik belgelerine tooan varlık toodescribe de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44ae9-124">You can also add documentation tooan asset toodescribe how data could be integrated into an application.</span></span> <span data-ttu-id="44ae9-125">Bkz: [nasıl toodocument veri kaynakları](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="44ae9-125">See [How toodocument data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="44ae9-126">Tooinclude veri nasıl profil data source kaydedilirken</span><span class="sxs-lookup"><span data-stu-id="44ae9-126">How tooinclude a data profile when registering a data source</span></span>
<span data-ttu-id="44ae9-127">Kolay tooinclude veri kaynağınızın bir profil var.</span><span class="sxs-lookup"><span data-stu-id="44ae9-127">It's easy tooinclude a profile of your data source.</span></span> <span data-ttu-id="44ae9-128">Hello bir veri kaynağını kaydettiğinizde **kayıtlı nesneler toobe** hello veri kaynağı kaydı panelinde aracı, seçin **dahil veri profili**.</span><span class="sxs-lookup"><span data-stu-id="44ae9-128">When you register a data source, in hello **Objects toobe registered** panel of hello data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="44ae9-129">toolearn tooregister veri kaynaklarını nasıl görürüm hakkında daha fazla bilgi [nasıl tooregister veri kaynakları](data-catalog-how-to-register.md) ve [Azure veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="44ae9-129">toolearn more about how tooregister data sources, see [How tooregister data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="44ae9-130">Veri profillerini içeren veri varlıklarını üzerinde filtreleme</span><span class="sxs-lookup"><span data-stu-id="44ae9-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="44ae9-131">Veri profili içeren toodiscover veri varlıklarını içerebilir `has:tableDataProfiles` veya `has:columnsDataProfiles` arama terimleri biri olarak.</span><span class="sxs-lookup"><span data-stu-id="44ae9-131">toodiscover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="44ae9-132">Seçme **dahil veri profili** hello veri kaynağı kayıt aracını tablo ve sütun düzeyi profil bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="44ae9-132">Selecting **Include Data Profile** in hello data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="44ae9-133">Ancak, hello veri Kataloğu API'si veri varlıklarını toobe eklenen profili bilgileri yalnızca bir kümesi kayıtlı sağlar.</span><span class="sxs-lookup"><span data-stu-id="44ae9-133">However, hello Data Catalog API allows data assets toobe registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="44ae9-134">Veri profili bilgilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="44ae9-134">Viewing data profile information</span></span>
<span data-ttu-id="44ae9-135">Bir profili uygun veri kaynağıyla bulduktan sonra hello veri profili ayrıntıları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44ae9-135">Once you find a suitable data source with a profile, you can view hello data profile details.</span></span> <span data-ttu-id="44ae9-136">tooview hello veri profili, bir veri varlığına seçip **veri profili** hello veri Kataloğu portalı penceresinde.</span><span class="sxs-lookup"><span data-stu-id="44ae9-136">tooview hello data profile, select a data asset and choose **Data Profile** in hello Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="44ae9-137">Bir veri profilinde **Azure veri Kataloğu** tablo ve sütun profil bilgileri de dahil olmak üzere gösterir:</span><span class="sxs-lookup"><span data-stu-id="44ae9-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="44ae9-138">Nesne veri profili</span><span class="sxs-lookup"><span data-stu-id="44ae9-138">Object data profile</span></span>
* <span data-ttu-id="44ae9-139">Satır sayısı</span><span class="sxs-lookup"><span data-stu-id="44ae9-139">Number of rows</span></span>
* <span data-ttu-id="44ae9-140">Tablo boyutu</span><span class="sxs-lookup"><span data-stu-id="44ae9-140">Table size</span></span>
* <span data-ttu-id="44ae9-141">Merhaba nesne en son güncelleştirildiği</span><span class="sxs-lookup"><span data-stu-id="44ae9-141">When hello object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="44ae9-142">Sütun veri profili</span><span class="sxs-lookup"><span data-stu-id="44ae9-142">Column data profile</span></span>
* <span data-ttu-id="44ae9-143">Sütun veri türü</span><span class="sxs-lookup"><span data-stu-id="44ae9-143">Column data type</span></span>
* <span data-ttu-id="44ae9-144">Farklı değerleri sayısı</span><span class="sxs-lookup"><span data-stu-id="44ae9-144">Number of distinct values</span></span>
* <span data-ttu-id="44ae9-145">NULL değerlere sahip satır sayısı</span><span class="sxs-lookup"><span data-stu-id="44ae9-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="44ae9-146">Minimum, maksimum, ortalama ve sütun değerleri için standart sapma</span><span class="sxs-lookup"><span data-stu-id="44ae9-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="44ae9-147">Özet</span><span class="sxs-lookup"><span data-stu-id="44ae9-147">Summary</span></span>
<span data-ttu-id="44ae9-148">Hakkında bilgi kayıtlı veri varlıklarını toohelp hello uygunluğunu hello veri toosolve iş sorunlarını belirlemek ve profil oluşturma verilerini istatistikler sağlar.</span><span class="sxs-lookup"><span data-stu-id="44ae9-148">Data profiling provides statistics and information about registered data assets toohelp you determine hello suitability of hello data toosolve business problems.</span></span> <span data-ttu-id="44ae9-149">Açıklama ve veri kaynaklarını belgeleme yanı sıra veri profilleri, verilerinizin daha derin bir anlayış kullanıcılara verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44ae9-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="44ae9-150">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="44ae9-150">See Also</span></span>
* [<span data-ttu-id="44ae9-151">Nasıl tooregister veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="44ae9-151">How tooregister data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="44ae9-152">Azure Veri Kataloğu ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="44ae9-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
