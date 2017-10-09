---
title: "Node.js içinde Azure Search ile çalışmaya aaaGet | Microsoft Docs"
description: "Programlama diliniz olarak Node.js kullanarak, Azure'da barındırılan bir bulut arama hizmeti üzerinde arama uygulaması derleme konusunu inceleyin."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="7f970-103">Node.js'de Azure Search kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7f970-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f970-104">Portal</span><span class="sxs-lookup"><span data-stu-id="7f970-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="7f970-105">.NET</span><span class="sxs-lookup"><span data-stu-id="7f970-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="7f970-106">Nasıl toobuild özel bir Node.js arama arama deneyimi için Azure Search kullanan uygulamayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7f970-106">Learn how toobuild a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="7f970-107">Bu öğretici hello kullanır [Azure Search Hizmeti REST API'si](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello nesneleri ve bu alıştırmada kullanılan işlemleri.</span><span class="sxs-lookup"><span data-stu-id="7f970-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="7f970-108">Kullandık [Node.js](https://Nodejs.org) ve NPM, [Sublime Text 3](http://www.sublimetext.com/3)ve Windows 8.1 toodevelop'de Windows PowerShell ve bu kodu sınayın.</span><span class="sxs-lookup"><span data-stu-id="7f970-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 toodevelop and test this code.</span></span>

<span data-ttu-id="7f970-109">toorun hello için kaydolabilirsiniz bir Azure Search hizmeti bu örnek olmalıdır [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f970-109">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7f970-110">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="7f970-110">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-hello-data"></a><span data-ttu-id="7f970-111">Merhaba veri hakkında</span><span class="sxs-lookup"><span data-stu-id="7f970-111">About hello data</span></span>
<span data-ttu-id="7f970-112">Bu örnek uygulama hello verileri kullanan [Birleşik Devletler Jeoloji Hizmetleri (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtrelenmiş hello Rhode Island eyaleti tooreduce hello veri kümesi boyutu.</span><span class="sxs-lookup"><span data-stu-id="7f970-112">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="7f970-113">Bu veri toobuild akışlar, Göller ve zirveler gibi jeolojik özelliklerin yanı sıra hastaneler ve okullar gibi önemli binaları döndüren bir arama uygulaması kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="7f970-113">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="7f970-114">Bu uygulamada hello **Dataındexer** programı oluşturup yükleri hello dizini kullanarak bir [dizin oluşturucu](https://msdn.microsoft.com/library/azure/dn798918.aspx) hello alma yapısı, filtrelenmiş USGS veri kümesini ortak bir Azure SQL veritabanından.</span><span class="sxs-lookup"><span data-stu-id="7f970-114">In this application, hello **DataIndexer** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="7f970-115">Kimlik bilgileri ve bağlantı bilgileri toohello çevrimiçi veri kaynağına hello program kodu içinde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7f970-115">Credentials and connection information toohello online data source is provided in hello program code.</span></span> <span data-ttu-id="7f970-116">Ek yapılandırma gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="7f970-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="7f970-117">Bu veri kümesi toostay hello 10.000 belge limiti hello ücretsiz fiyatlandırma katmanı altında üzerinde bir filtre uygulanmış.</span><span class="sxs-lookup"><span data-stu-id="7f970-117">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="7f970-118">Merhaba standart katmanı kullanırsanız bu limit uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="7f970-118">If you use hello standard tier, this limit does not apply.</span></span> <span data-ttu-id="7f970-119">Her fiyatlandırma katmanının kapasitesi hakkında ayrıntılı bilgi için bkz: [Search hizmet limitleri](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="7f970-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="7f970-120">Merhaba hizmet adı ve Azure Search hizmetinizin api anahtarını bulma</span><span class="sxs-lookup"><span data-stu-id="7f970-120">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="7f970-121">Merhaba hizmeti oluşturduktan sonra dönüş toohello portal tooget hello URL'si veya `api-key`.</span><span class="sxs-lookup"><span data-stu-id="7f970-121">After you create hello service, return toohello portal tooget hello URL or `api-key`.</span></span> <span data-ttu-id="7f970-122">Bağlantıları tooyour arama hizmeti gerektiren her iki hello URL'ye sahip ve bir `api-key` tooauthenticate hello çağrısı.</span><span class="sxs-lookup"><span data-stu-id="7f970-122">Connections tooyour Search service require that you have both hello URL and an `api-key` tooauthenticate hello call.</span></span>

1. <span data-ttu-id="7f970-123">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f970-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7f970-124">Merhaba atlama çubuğunda, **Search Hizmeti** tüm Azure arama hizmetleri aboneliğiniz için sağlanan toolist.</span><span class="sxs-lookup"><span data-stu-id="7f970-124">In hello jump bar, click **Search service** toolist all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="7f970-125">Toouse istediğiniz hello hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="7f970-125">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="7f970-126">Merhaba hizmet panosunda hello yönetici anahtarlarına erişim için anahtar simgesine hello gibi önemli bilgiler için kutucuklar görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7f970-126">On hello service dashboard, you should see tiles for essential information, such as hello key icon for accessing hello admin keys.</span></span>
5. <span data-ttu-id="7f970-127">Merhaba hizmet URL'si, bir yönetici anahtarını ve sorgu anahtarını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="7f970-127">Copy hello service URL, an admin key, and a query key.</span></span> <span data-ttu-id="7f970-128">Toohello config.js. dosyasına eklerken, tüm üç daha sonra gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f970-128">You need all three later when you add them toohello config.js file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="7f970-129">Merhaba örnek dosyalarını indirme</span><span class="sxs-lookup"><span data-stu-id="7f970-129">Download hello sample files</span></span>
<span data-ttu-id="7f970-130">Her iki yaklaşım toodownload hello örnek aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7f970-130">Use either one of hello following approaches toodownload hello sample.</span></span>

1. <span data-ttu-id="7f970-131">Çok Git[Azuresearchnodejsındexerdemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="7f970-131">Go too[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="7f970-132">Tıklatın **ZIP'i indir**hello .zip dosyasını kaydedin ve ardından içerdiği tüm hello dosyaları ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f970-132">Click **Download ZIP**, save hello .zip file, and then extract all hello files it contains.</span></span>

<span data-ttu-id="7f970-133">Sonraki tüm dosya değişiklikleri ve çalıştırma deyimleri bu klasördeki dosyalara uygulanır.</span><span class="sxs-lookup"><span data-stu-id="7f970-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="7f970-134">Merhaba config.js güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7f970-134">Update hello config.js.</span></span> <span data-ttu-id="7f970-135">Search hizmetinizin URL'si ve api anahtarı ile güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7f970-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="7f970-136">URL ve daha önce kopyaladığınız api anahtarını hello kullanarak yapılandırma dosyasında hello URL, yönetici anahtarını ve sorgu anahtarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="7f970-136">Using hello URL and api-key that you copied earlier, specify hello URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="7f970-137">Yönetici anahtarları, dizin oluşturma ve silme ile belge yükleme de dahil olmak üzere hizmet işlemleri üzerinde tam denetim hakkı verir.</span><span class="sxs-lookup"><span data-stu-id="7f970-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="7f970-138">Buna karşılık sorgu anahtarları tooAzure arama bağlanan istemci uygulamaları tarafından genellikle kullanılan salt okunur işlemler içindir.</span><span class="sxs-lookup"><span data-stu-id="7f970-138">In contrast, query keys are for read-only operations, typically used by client applications that connect tooAzure Search.</span></span>

<span data-ttu-id="7f970-139">Bu örnekte, anahtar toohelp pekiştirmek hello sorgu anahtarını istemci uygulamalarında kullanma hello en iyi uygulama olarak hello sorgu içerir.</span><span class="sxs-lookup"><span data-stu-id="7f970-139">In this sample, we include hello query key toohelp reinforce hello best practice of using hello query key in client applications.</span></span>

<span data-ttu-id="7f970-140">Aşağıdaki ekran görüntüsü gösterildiği hello **config.js** hello ile bir metin düzenleyicisinde açın nerede tooupdate hello hello dosyasıyla değerden görebilmeniz için güncelleştireceğinizi ilgili girişler arama hizmetiniz için geçerli.</span><span class="sxs-lookup"><span data-stu-id="7f970-140">hello following screenshot shows **config.js** open in a text editor, with hello relevant entries demarcated so that you can see where tooupdate hello file with hello values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a><span data-ttu-id="7f970-141">Ana bilgisayar hello örnek için çalışma zamanı ortamı</span><span class="sxs-lookup"><span data-stu-id="7f970-141">Host a runtime environment for hello sample</span></span>
<span data-ttu-id="7f970-142">Merhaba örnek genel olarak npm kullanarak yükleyebileceğiniz bir HTTP sunucusu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7f970-142">hello sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="7f970-143">Bir PowerShell penceresinde aşağıdaki komutları hello için kullanın.</span><span class="sxs-lookup"><span data-stu-id="7f970-143">Use a PowerShell window for hello following commands.</span></span>

1. <span data-ttu-id="7f970-144">Merhaba içeren toohello klasörüne gidin **package.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="7f970-144">Navigate toohello folder that contains hello **package.json** file.</span></span>
2. <span data-ttu-id="7f970-145">`npm install` yazın.</span><span class="sxs-lookup"><span data-stu-id="7f970-145">Type `npm install`.</span></span>
3. <span data-ttu-id="7f970-146">`npm install -g http-server` yazın.</span><span class="sxs-lookup"><span data-stu-id="7f970-146">Type `npm install -g http-server`.</span></span>

## <a name="build-hello-index-and-run-hello-application"></a><span data-ttu-id="7f970-147">Merhaba dizini oluşturun ve hello uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="7f970-147">Build hello index and run hello application</span></span>
1. <span data-ttu-id="7f970-148">`npm run indexDocuments` yazın.</span><span class="sxs-lookup"><span data-stu-id="7f970-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="7f970-149">`npm run build` yazın.</span><span class="sxs-lookup"><span data-stu-id="7f970-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="7f970-150">`npm run start_server` yazın.</span><span class="sxs-lookup"><span data-stu-id="7f970-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="7f970-151">Tarayıcınızı `http://localhost:8080/index.html` adresine yönlendirin</span><span class="sxs-lookup"><span data-stu-id="7f970-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="7f970-152">USGS verilerinde arama</span><span class="sxs-lookup"><span data-stu-id="7f970-152">Search on USGS data</span></span>
<span data-ttu-id="7f970-153">Merhaba USGS veri kümesini ilgili toohello Rhode Island eyaleti kayıtları içerir.</span><span class="sxs-lookup"><span data-stu-id="7f970-153">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="7f970-154">Tıklatırsanız **arama** bir boş arama kutusunda, hello ilk 50 girişi hello varsayılan olduğu alırsınız.</span><span class="sxs-lookup"><span data-stu-id="7f970-154">If you click **Search** on an empty search box, you get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="7f970-155">Bir arama terimi girerek hello arama motoru toogo üzerinde bir şey sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f970-155">Entering a search term gives hello search engine something toogo on.</span></span> <span data-ttu-id="7f970-156">Bölgesel bir ad girmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="7f970-156">Try entering a regional name.</span></span> <span data-ttu-id="7f970-157">"Roger Williams", Rhode Island hello ilk İdarecisi oluştu.</span><span class="sxs-lookup"><span data-stu-id="7f970-157">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="7f970-158">Çok sayıda parka, binaya ve okula onun adı verildi.</span><span class="sxs-lookup"><span data-stu-id="7f970-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="7f970-159">Ayrıca, bu terimlerden herhangi birini de deneyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7f970-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="7f970-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="7f970-160">Pawtucket</span></span>
* <span data-ttu-id="7f970-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="7f970-161">Pembroke</span></span>
* <span data-ttu-id="7f970-162">kaz + şapka</span><span class="sxs-lookup"><span data-stu-id="7f970-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f970-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7f970-163">Next steps</span></span>
<span data-ttu-id="7f970-164">Bu Node.js ve hello USGS veri kümesini temel alan hello ilk Azure Search öğreticisidir.</span><span class="sxs-lookup"><span data-stu-id="7f970-164">This is hello first Azure Search tutorial based on Node.js and hello USGS dataset.</span></span> <span data-ttu-id="7f970-165">Zaman içinde biz özel çözümlerinizde toouse isteyebilirsiniz ek arama özellikleri Bu öğretici toodemonstrate genişletmeniz.</span><span class="sxs-lookup"><span data-stu-id="7f970-165">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="7f970-166">Zaten Azure Search ile ilgili belirli bir altyapınız varsa öneri araçlarını (yazarken tamamlanan veya otomatik tamamlanan sorgular ), filtreleri ve çok yönlü gezinmeyi denemek için, bu örneği dayanak olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f970-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="7f970-167">Ayrıca, numaralar ekleyerek ve böylece kullanıcılar hello sonuçları belgeleri toplu işleme hello arama sonuçları sayfasını artırabilir.</span><span class="sxs-lookup"><span data-stu-id="7f970-167">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="7f970-168">Yeni tooAzure arama?</span><span class="sxs-lookup"><span data-stu-id="7f970-168">New tooAzure Search?</span></span> <span data-ttu-id="7f970-169">Diğer öğreticiler toodevelop bir neler yapabileceğinizi anlamak çalışırken öneririz.</span><span class="sxs-lookup"><span data-stu-id="7f970-169">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="7f970-170">Ziyaret bizim [belge sayfasının](https://azure.microsoft.com/documentation/services/search/) toofind daha fazla kaynak.</span><span class="sxs-lookup"><span data-stu-id="7f970-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="7f970-171">Merhaba bağlantılar da görüntüleyebilirsiniz bizim [Video ve öğretici listemiz](search-video-demo-tutorial-list.md) tooaccess daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="7f970-171">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
