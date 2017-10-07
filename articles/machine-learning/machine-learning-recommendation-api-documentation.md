---
title: "aaaMachine öğrenme önerileri API belgeleri | Microsoft Docs"
description: "Azure Machine Learning önerileri API'si belgeleri önerileri altyapısının hello Microsoft Azure Market kullanılabilir."
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="b70a4-103">Azure Machine Learning Öneri API’si Belgeleri</span><span class="sxs-lookup"><span data-stu-id="b70a4-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="b70a4-104">Merhaba önerileri API Bilişsel hizmeti yerine bu sürümünü kullanarak başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="b70a4-105">Merhaba önerileri Bilişsel hizmet bu hizmeti koyacağınız ve tüm hello yeni özellikler vardır geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="b70a4-106">Toplu işlem desteği, daha iyi API'si Gezgini, bir temizleyici API yüzeyi, daha tutarlı kaydolma/faturalandırma deneyimi, vb. gibi yeni özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="b70a4-107">Daha fazla bilgi edinmek [geçiş toohello yeni Bilişsel hizmeti](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="b70a4-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="b70a4-108">Bu belgede, Microsoft Azure Machine Learning önerileri API'leri gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="b70a4-109">1. Genel bir bakış</span><span class="sxs-lookup"><span data-stu-id="b70a4-109">1. General overview</span></span>
<span data-ttu-id="b70a4-110">Bu belge, bir API Başvurusu değil.</span><span class="sxs-lookup"><span data-stu-id="b70a4-110">This document is an API reference.</span></span> <span data-ttu-id="b70a4-111">"Azure Machine Learning öneri – Hızlı Başlat" Merhaba belgeyle başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-111">You should start with hello “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="b70a4-112">Hello Azure Machine Learning önerileri API'si mantıksal gruplar aşağıdaki hello ayrılabilir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-112">hello Azure Machine Learning Recommendations API can be divided into hello following logical groups:</span></span>

* <span data-ttu-id="b70a4-113"><ins>Sınırlamalar</ins> -önerileri API sınırlamaları.</span><span class="sxs-lookup"><span data-stu-id="b70a4-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="b70a4-114"><ins>Genel bilgiler</ins> -kimlik doğrulaması hakkında bilgi hizmet URI'si ve sürüm oluşturma.</span><span class="sxs-lookup"><span data-stu-id="b70a4-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="b70a4-115"><ins>Model Basic</ins> -toodo hello temel işlemleri modeli sağlayan API (örneğin oluşturma, güncelleştirme ve bir modeli silme).</span><span class="sxs-lookup"><span data-stu-id="b70a4-115"><ins>Model Basic</ins> - APIs that enable you toodo hello basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="b70a4-116"><ins>Model Gelişmiş</ins> -hello model üzerinde Gelişmiş tooget veri ınsights'ı etkinleştir API'leri.</span><span class="sxs-lookup"><span data-stu-id="b70a4-116"><ins>Model Advanced</ins> - APIs that enable you tooget advanced data insights on hello model.</span></span>
* <span data-ttu-id="b70a4-117"><ins>Model iş kuralları</ins> -toomanage iş kuralları hello modeli öneri sonuçlarını sağlayan API.</span><span class="sxs-lookup"><span data-stu-id="b70a4-117"><ins>Model Business Rules</ins> - APIs that enable you toomanage business rules on hello model recommendation results.</span></span>
* <span data-ttu-id="b70a4-118"><ins>Katalog</ins> -toodo temel işlemleri modeli katalogunda sağlayan API.</span><span class="sxs-lookup"><span data-stu-id="b70a4-118"><ins>Catalog</ins> - APIs that enable you toodo basic operations on a model catalog.</span></span> <span data-ttu-id="b70a4-119">Bir katalog hello Kullanım verilerinin hello öğelerde meta veri bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-119">A catalog contains metadata information on hello items of hello usage data.</span></span>
* <span data-ttu-id="b70a4-120"><ins>Özellik</ins> -tooget Öngörüler öğede hello kataloğuna sağlayan API ve nasıl toouse bu bilgileri toobuild daha iyi öneriler.</span><span class="sxs-lookup"><span data-stu-id="b70a4-120"><ins>Feature</ins> - APIs that enable tooget insights on item into hello catalog and how toouse this information toobuild better recommendations.</span></span>
* <span data-ttu-id="b70a4-121"><ins>Kullanım verileri</ins> -toodo temel işlemleri hello modeli kullanım verilerini sağlayan API.</span><span class="sxs-lookup"><span data-stu-id="b70a4-121"><ins>Usage Data</ins> - APIs that enable you toodo basic operations on hello model usage data.</span></span> <span data-ttu-id="b70a4-122">Kullanım verileri hello temel formda çiftlerini &#60; UserID &#62; içeren satırları oluşur, &#60; ItemId &#62;.</span><span class="sxs-lookup"><span data-stu-id="b70a4-122">Usage data in hello basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="b70a4-123"><ins>Yapı</ins> - bir model tootrigger sağlayan API yapı ve ilgili toothis temel işlemleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-123"><ins>Build</ins> - APIs that enable you tootrigger a model build and do basic operations that are related toothis build.</span></span> <span data-ttu-id="b70a4-124">Değerli kullanım verileri bulduktan sonra model yapı tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="b70a4-125"><ins>Öneri</ins> -hello derleme bir modelin sona erince tooconsume öneriler sağlayan API.</span><span class="sxs-lookup"><span data-stu-id="b70a4-125"><ins>Recommendation</ins> - APIs that enable you tooconsume recommendations once hello build of a model ends.</span></span>
* <span data-ttu-id="b70a4-126"><ins>Kullanıcı verilerini</ins> -hello kullanıcı kullanım verilerini toofetch bilgi sağlayan API.</span><span class="sxs-lookup"><span data-stu-id="b70a4-126"><ins>User Data</ins> - APIs that enable you toofetch information on hello user usage data.</span></span>
* <span data-ttu-id="b70a4-127"><ins>Bildirimleri</ins> -tooyour API işlemleri ilgili sorunları tooreceive bildirimlerini sağlayan API'ler.</span><span class="sxs-lookup"><span data-stu-id="b70a4-127"><ins>Notifications</ins> - APIs that enable you tooreceive notifications on problems related tooyour API operations.</span></span> <span data-ttu-id="b70a4-128">(Örneğin, kullanım verilerini veri alımı ve hello olayları işleme testlerden çoğunu aracılığıyla bildirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="b70a4-128">(For example, you are reporting usage data via Data Acquisition and most of hello events processing are failing.</span></span> <span data-ttu-id="b70a4-129">Bir hata bildirimi gerçekleştirilecektir.)</span><span class="sxs-lookup"><span data-stu-id="b70a4-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="b70a4-130">2. Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="b70a4-130">2. Limitations</span></span>
* <span data-ttu-id="b70a4-131">Merhaba en büyük abonelik başına model sayısı 10'dur.</span><span class="sxs-lookup"><span data-stu-id="b70a4-131">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="b70a4-132">Merhaba derlemeleri modeli başına en fazla 20'dir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-132">hello maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="b70a4-133">Merhaba en fazla bir katalog tutabilir öğe sayısı 100. 000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-133">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="b70a4-134">Merhaba maksimum tutulur kullanım noktaları ~ 5,000,000 sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-134">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="b70a4-135">Yeni bir tane karşıya bildirilen veya gereken hello eski silinir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-135">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="b70a4-136">Merhaba en büyük boyutu (örn. içeri aktarma katalog verilerini, kullanım verileri İçeri Aktar) POSTASINA gönderilen veri 200 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-136">hello maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="b70a4-137">Merhaba maksimum öneriler alınırken 150 olduğunda için sorulan öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-137">hello maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="b70a4-138">3. API - genel bilgiler</span><span class="sxs-lookup"><span data-stu-id="b70a4-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="b70a4-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="b70a4-139">3.1.</span></span> <span data-ttu-id="b70a4-140">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="b70a4-140">Authentication</span></span>
<span data-ttu-id="b70a4-141">Lütfen kimlik doğrulaması ile ilgili hello Microsoft Azure Market yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="b70a4-141">Please follow hello Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="b70a4-142">Merhaba Market ya da hello temel veya OAuth kimlik doğrulama yöntemini destekler.</span><span class="sxs-lookup"><span data-stu-id="b70a4-142">hello marketplace supports either hello Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="b70a4-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="b70a4-143">3.2.</span></span> <span data-ttu-id="b70a4-144">Hizmet URI'si</span><span class="sxs-lookup"><span data-stu-id="b70a4-144">Service URI</span></span>
<span data-ttu-id="b70a4-145">hello Azure Machine Learning önerileri API'leri için Hello hizmet kök URI [burada.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="b70a4-145">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="b70a4-146">Merhaba tam hizmet URI'si hello OData belirtimi öğeleri kullanılarak ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-146">hello full service URI is expressed using elements of hello OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="b70a4-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="b70a4-147">3.3.</span></span> <span data-ttu-id="b70a4-148">API sürümü</span><span class="sxs-lookup"><span data-stu-id="b70a4-148">API version</span></span>
<span data-ttu-id="b70a4-149">Her API çağrısı, hello sonunda too1.0 ayarlanmalıdır apiVersion adlı bir sorgu parametresi sahip olur.</span><span class="sxs-lookup"><span data-stu-id="b70a4-149">Each API call will have, at hello end, a query parameter called apiVersion that should be set too1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="b70a4-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="b70a4-150">3.4.</span></span> <span data-ttu-id="b70a4-151">Kimlikleri büyük küçük harf duyarlıdır</span><span class="sxs-lookup"><span data-stu-id="b70a4-151">IDs are case sensitive</span></span>
<span data-ttu-id="b70a4-152">Herhangi bir hello API ' ları tarafından döndürülen kimlikleri, büyük/küçük harfe duyarlıdır ve bu nedenle sonraki API çağrıları parametre olarak geçirilen kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-152">IDs, returned by any of hello APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="b70a4-153">Örneğin, model kimlikleri ve Katalog büyük küçük harfe duyarlı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="b70a4-154">4. Öneriler kalite ve soğuk öğeleri</span><span class="sxs-lookup"><span data-stu-id="b70a4-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="b70a4-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="b70a4-155">4.1.</span></span> <span data-ttu-id="b70a4-156">Öneri kalitesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-156">Recommendation quality</span></span>
<span data-ttu-id="b70a4-157">Öneri model oluşturma genellikle yeterli tooallow hello sistem tooprovide önerileri olur.</span><span class="sxs-lookup"><span data-stu-id="b70a4-157">Creating a recommendation model is usually enough tooallow hello system tooprovide recommendations.</span></span> <span data-ttu-id="b70a4-158">Bununla birlikte, öneri kalitesini işlenen hello kullanıma göre değişir ve hello katalog kapsamını hello.</span><span class="sxs-lookup"><span data-stu-id="b70a4-158">Nevertheless, recommendation quality varies based on hello usage processed and hello coverage of hello catalog.</span></span> <span data-ttu-id="b70a4-159">Örneğin çok soğuk öğelerinin (öğeleri önemli kullanım olmadan) varsa, bu tür bir öğe için bir öneri sağlama veya böyle bir öğe önerilen bir kullanarak sorunlar hello sistem olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-159">For example if you have a lot of cold items (items without significant usage), hello system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="b70a4-160">Sipariş tooovercome hello soğuk öğesi sorunda hello sistem hello öğeleri tooenhance hello önerileri meta verileri hello kullanılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-160">In order tooovercome hello cold item problem, hello system allows hello use of metadata of hello items tooenhance hello recommendations.</span></span> <span data-ttu-id="b70a4-161">Bu meta veriler başvurulan tooas özellik gibidir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-161">This metadata is referred tooas features.</span></span> <span data-ttu-id="b70a4-162">Bir kitaptaki yazar veya bir film aktör Bunun tipik özellikleridir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="b70a4-163">Özellikler anahtar/değer dizeleri hello biçiminde hello katalog aracılığıyla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-163">Features are provided via hello catalog in hello form of key/value strings.</span></span> <span data-ttu-id="b70a4-164">Merhaba tam biçim hello katalog dosyası için lütfen toohello bakın [alma katalog bölümü](#81-import-catalog-data).</span><span class="sxs-lookup"><span data-stu-id="b70a4-164">For hello full format of hello catalog file, please refer toohello [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="b70a4-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="b70a4-165">4.2.</span></span> <span data-ttu-id="b70a4-166">RANK derleme</span><span class="sxs-lookup"><span data-stu-id="b70a4-166">Rank build</span></span>
<span data-ttu-id="b70a4-167">Özellikleri hello öneri modeli artırabilir, ancak toodo şekilde anlamlı özellikleri hello kullanımını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-167">Features can enhance hello recommendation model, but toodo so requires hello use of meaningful features.</span></span> <span data-ttu-id="b70a4-168">Yeni bir yapı tanıtılan - bu amaç için bir sıra oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="b70a4-169">Bu yapı özellikleri hello yararlılığı rank.</span><span class="sxs-lookup"><span data-stu-id="b70a4-169">This build will rank hello usefulness of features.</span></span> <span data-ttu-id="b70a4-170">Anlamlı bir özellik, bir sıra puan 2 ve yedekleme ile bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="b70a4-171">Merhaba özelliklerinin anlamlı olan anlama sonra anlamlı özelliklerinin hello listesi (veya alt liste) içeren bir öneri yapı tetikler.</span><span class="sxs-lookup"><span data-stu-id="b70a4-171">After understanding which of hello features are meaningful, trigger a recommendation build with hello list (or sublist) of meaningful features.</span></span> <span data-ttu-id="b70a4-172">Bunlar için hello geliştirme soğuk öğeleri ve yarı öğelerinin özellik olası toouse olur.</span><span class="sxs-lookup"><span data-stu-id="b70a4-172">It is possible toouse these feature for hello enhancement of both warm items and cold items.</span></span> <span data-ttu-id="b70a4-173">Bunları sıcak öğeleri için sipariş toouse hello `UseFeatureInModel` yapı parametresi ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-173">In order toouse them for warm items, hello `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="b70a4-174">Soğuk öğeleri için sipariş toouse özellikleri hello `AllowColdItemPlacement` yapı parametresi etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-174">In order toouse features for cold items, hello `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="b70a4-175">Not: Bu olası tooenable değil `AllowColdItemPlacement` etkinleştirmeden `UseFeatureInModel`.</span><span class="sxs-lookup"><span data-stu-id="b70a4-175">Note: It is not possible tooenable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="b70a4-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="b70a4-176">4.3.</span></span> <span data-ttu-id="b70a4-177">Öneri mantığı</span><span class="sxs-lookup"><span data-stu-id="b70a4-177">Recommendation reasoning</span></span>
<span data-ttu-id="b70a4-178">Öneri mantığı özellik kullanımı başka bir yönüdür.</span><span class="sxs-lookup"><span data-stu-id="b70a4-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="b70a4-179">Aslında, hello Azure Machine Learning önerileri altyapısı özellikleri tooprovide öneri açıklamaları (paketini kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b70a4-179">Indeed, hello Azure Machine Learning Recommendations engine can use features tooprovide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="b70a4-180">akıl), toomore güvenirlik hello öndeki öğe hello öneri tüketiciden önerilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-180">reasoning), leading toomore confidence in hello recommended item from hello recommendation consumer.</span></span>
<span data-ttu-id="b70a4-181">tooenable, hello akıl `AllowFeatureCorrelation` ve `ReasoningFeatureList` parametreleri Kurulum önceki toorequesting bir öneri yapı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-181">tooenable reasoning, hello `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior toorequesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="b70a4-182">5. Temel modeli</span><span class="sxs-lookup"><span data-stu-id="b70a4-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="b70a4-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="b70a4-183">5.1.</span></span> <span data-ttu-id="b70a4-184">Model oluşturma</span><span class="sxs-lookup"><span data-stu-id="b70a4-184">Create Model</span></span>
<span data-ttu-id="b70a4-185">"Model oluşturma" isteği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b70a4-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="b70a4-186">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-186">HTTP Method</span></span> | <span data-ttu-id="b70a4-187">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-188">YAYINLA</span><span class="sxs-lookup"><span data-stu-id="b70a4-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-189">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-190">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-190">Parameter Name</span></span> | <span data-ttu-id="b70a4-191">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-192">modelName</span><span class="sxs-lookup"><span data-stu-id="b70a4-192">modelName</span></span> |<span data-ttu-id="b70a4-193">Yalnızca harf (A-Z, a-z), sayılar (0-9), tireler (-) ve alt çizgi (_).</span><span class="sxs-lookup"><span data-stu-id="b70a4-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="b70a4-194">En fazla uzunluk: 20</span><span class="sxs-lookup"><span data-stu-id="b70a4-194">Max length: 20</span></span> |
| <span data-ttu-id="b70a4-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-195">apiVersion</span></span> |<span data-ttu-id="b70a4-196">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-196">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-197">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-197">Request Body</span></span> |<span data-ttu-id="b70a4-198">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-198">NONE</span></span> |

<span data-ttu-id="b70a4-199">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-199">**Response**:</span></span>

<span data-ttu-id="b70a4-200">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="b70a4-201">`feed/entry/content/properties/id`-Hello model kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-201">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="b70a4-202">**Not**: model kimliği büyük küçük harfe duyarlı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="b70a4-203">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-203">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="52-get-model"></a><span data-ttu-id="b70a4-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="b70a4-204">5.2.</span></span> <span data-ttu-id="b70a4-205">Model alma</span><span class="sxs-lookup"><span data-stu-id="b70a4-205">Get Model</span></span>
<span data-ttu-id="b70a4-206">"Get modeli" isteği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b70a4-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="b70a4-207">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-207">HTTP Method</span></span> | <span data-ttu-id="b70a4-208">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-209">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="b70a4-210">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-211">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-211">Parameter Name</span></span> | <span data-ttu-id="b70a4-212">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-213">id</span><span class="sxs-lookup"><span data-stu-id="b70a4-213">id</span></span> |<span data-ttu-id="b70a4-214">Benzersiz tanımlayıcı hello modelinin (büyük küçük harf duyarlı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-214">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="b70a4-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-215">apiVersion</span></span> |<span data-ttu-id="b70a4-216">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-216">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-217">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-217">Request Body</span></span> |<span data-ttu-id="b70a4-218">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-218">NONE</span></span> |

<span data-ttu-id="b70a4-219">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-219">**Response**:</span></span>

<span data-ttu-id="b70a4-220">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-220">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-221">Merhaba model veri öğeleri aşağıdaki hello altında bulunabilir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-221">hello model data can be found under hello following elements:</span></span>

* <span data-ttu-id="b70a4-222">`feed/entry/content/properties/Id`-Model benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="b70a4-223">`feed/entry/content/properties/Name`-Model adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="b70a4-224">`feed/entry/content/properties/Date`-Model oluşturulma tarihi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="b70a4-225">`feed/entry/content/properties/Status`-Model durumu.</span><span class="sxs-lookup"><span data-stu-id="b70a4-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="b70a4-226">Merhaba aşağıdakilerden biri:</span><span class="sxs-lookup"><span data-stu-id="b70a4-226">One of hello following:</span></span>
  * <span data-ttu-id="b70a4-227">Oluşturulan - modeli oluşturulur ve Katalog ve kullanım içermiyor.</span><span class="sxs-lookup"><span data-stu-id="b70a4-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="b70a4-228">ReadyForBuild - Model oluşturulur ve Katalog ve kullanım içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="b70a4-229">`feed/entry/content/properties/HasActiveBuild`-Hello model başarıyla yerleşik gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="b70a4-230">`feed/entry/content/properties/BuildId`-Model etkin yapı kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="b70a4-231">`feed/entry/content/properties/Mpr`-Model ortalama yüzdebirlik Derecelendirme (MPR - ModelInsight daha fazla bilgi için bkz.).</span><span class="sxs-lookup"><span data-stu-id="b70a4-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="b70a4-232">`feed/entry/content/properties/UserName`-Model iç kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="b70a4-233">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-233">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a><span data-ttu-id="b70a4-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="b70a4-234">5.3.</span></span>    <span data-ttu-id="b70a4-235">Tüm modelleri Al</span><span class="sxs-lookup"><span data-stu-id="b70a4-235">Get All Models</span></span>
<span data-ttu-id="b70a4-236">Merhaba geçerli kullanıcının tüm modelleri alır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-236">Retrieves all models of hello current user.</span></span>

| <span data-ttu-id="b70a4-237">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-237">HTTP Method</span></span> | <span data-ttu-id="b70a4-238">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-239">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="b70a4-240">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-241">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-241">Parameter Name</span></span> | <span data-ttu-id="b70a4-242">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-243">apiVersion</span></span> |<span data-ttu-id="b70a4-244">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-244">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-245">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-245">Request Body</span></span> |<span data-ttu-id="b70a4-246">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-246">NONE</span></span> |

<span data-ttu-id="b70a4-247">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-247">**Response**:</span></span>

<span data-ttu-id="b70a4-248">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="b70a4-249">`feed/entry/content/properties/Id`-Model benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="b70a4-250">`feed/entry/content/properties/Name`-Model adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="b70a4-251">`feed/entry/content/properties/Date`-Model oluşturulma tarihi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="b70a4-252">`feed/entry/content/properties/Status`-Model durumu.</span><span class="sxs-lookup"><span data-stu-id="b70a4-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="b70a4-253">Merhaba aşağıdakilerden biri:</span><span class="sxs-lookup"><span data-stu-id="b70a4-253">One of hello following:</span></span>
  * <span data-ttu-id="b70a4-254">Oluşturulan - modeli oluşturulur ve Katalog ve kullanım içermiyor.</span><span class="sxs-lookup"><span data-stu-id="b70a4-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="b70a4-255">ReadyForBuild - Model oluşturulur ve Katalog ve kullanım içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="b70a4-256">`feed/entry/content/properties/HasActiveBuild`-Hello model başarıyla yerleşik gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="b70a4-257">`feed/entry/content/properties/BuildId`-Model etkin yapı kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="b70a4-258">`feed/entry/content/properties/Mpr`-Model MPR (daha fazla bilgi için bkz: ModelInsight).</span><span class="sxs-lookup"><span data-stu-id="b70a4-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="b70a4-259">`feed/entry/content/properties/UserName`-Model iç kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="b70a4-260">`feed/entry/content/properties/UsageFileNames`-Model kullanım dosyalar virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="b70a4-261">`feed/entry/content/properties/CatalogId`-Model katalog kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="b70a4-262">`feed/entry/content/properties/Description`-Model açıklaması.</span><span class="sxs-lookup"><span data-stu-id="b70a4-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="b70a4-263">`feed/entry/content/properties/CatalogFileName`-Model katalog dosyası adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="b70a4-264">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-264">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a><span data-ttu-id="b70a4-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="b70a4-265">5.4.</span></span>    <span data-ttu-id="b70a4-266">Bir güncelleştirme modeli</span><span class="sxs-lookup"><span data-stu-id="b70a4-266">Update Model</span></span>
<span data-ttu-id="b70a4-267">Merhaba modeli güncelleştirmesi ya da etkin yapı kimliği hello</span><span class="sxs-lookup"><span data-stu-id="b70a4-267">You can update hello model description or hello active build ID.</span></span><br><span data-ttu-id="b70a4-268">
<ins>Etkin yapı kimliği</ins> -her derleme her model için bir yapı kimliği vardır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="b70a4-269">Merhaba etkin yapı kimliği hello ilk başarılı her yeni modelinin yapıdır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-269">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="b70a4-270">Bir etkin yapı Kimliğine sahip ve ek derlemeler hello için bunu bir kez aynı modelin ihtiyacınız tooexplicitly ayarlayın, bu, hello varsayılan derleme gibi kimliği istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="b70a4-270">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="b70a4-271">Ne zaman toouse, bir otomatik olarak kullanılacak hello varsayılan istediğiniz hello derleme kimliği belirtmezseniz, öneriler, tüketir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-271">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span><br>
<span data-ttu-id="b70a4-272">Üretim - toobuild yeni modelleri öneri modeline sahiptir ve bunları yükseltmeden önce bunları tooproduction test sonra bu düzenek - sağlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-272">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="b70a4-273">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-273">HTTP Method</span></span> | <span data-ttu-id="b70a4-274">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-275">PUT</span><span class="sxs-lookup"><span data-stu-id="b70a4-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="b70a4-276">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-277">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-277">Parameter Name</span></span> | <span data-ttu-id="b70a4-278">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-279">id</span><span class="sxs-lookup"><span data-stu-id="b70a4-279">id</span></span> |<span data-ttu-id="b70a4-280">Benzersiz tanımlayıcı hello modelinin (büyük küçük harf duyarlı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-280">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="b70a4-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-281">apiVersion</span></span> |<span data-ttu-id="b70a4-282">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-282">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-283">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="b70a4-284">Merhaba XML açıklama etiketleri ve ActiveBuildId isteğe bağlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-284">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="b70a4-285">Açıklama veya ActiveBuildId tooset istemiyorsanız hello tüm etiket kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-285">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="b70a4-286">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-286">**Response**:</span></span>

<span data-ttu-id="b70a4-287">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="b70a4-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="b70a4-288">5.5.</span></span>    <span data-ttu-id="b70a4-289">Model Sil</span><span class="sxs-lookup"><span data-stu-id="b70a4-289">Delete Model</span></span>
<span data-ttu-id="b70a4-290">Kimliğe göre var olan bir model siler</span><span class="sxs-lookup"><span data-stu-id="b70a4-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="b70a4-291">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-291">HTTP Method</span></span> | <span data-ttu-id="b70a4-292">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-293">SİL</span><span class="sxs-lookup"><span data-stu-id="b70a4-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="b70a4-294">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-295">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-295">Parameter Name</span></span> | <span data-ttu-id="b70a4-296">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-297">id</span><span class="sxs-lookup"><span data-stu-id="b70a4-297">id</span></span> |<span data-ttu-id="b70a4-298">Benzersiz tanımlayıcı hello modelinin (büyük küçük harf duyarlı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-298">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="b70a4-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-299">apiVersion</span></span> |<span data-ttu-id="b70a4-300">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-300">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-301">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-301">Request Body</span></span> |<span data-ttu-id="b70a4-302">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-302">NONE</span></span> |

<span data-ttu-id="b70a4-303">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-303">**Response**:</span></span>

<span data-ttu-id="b70a4-304">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-304">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-305">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-305">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a><span data-ttu-id="b70a4-306">6. Gelişmiş modeli</span><span class="sxs-lookup"><span data-stu-id="b70a4-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="b70a4-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="b70a4-307">6.1.</span></span>    <span data-ttu-id="b70a4-308">Model veri öngörüleri</span><span class="sxs-lookup"><span data-stu-id="b70a4-308">Model Data Insight</span></span>
<span data-ttu-id="b70a4-309">İstatistik bilgileri, bu model ile oluşturulmuş hello kullanım verilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="b70a4-309">Returns statistical data on hello usage data that this model was built with.</span></span>

<span data-ttu-id="b70a4-310">Yalnızca öneri derleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="b70a4-311">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-311">HTTP Method</span></span> | <span data-ttu-id="b70a4-312">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-313">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="b70a4-314">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-315">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-315">Parameter Name</span></span> | <span data-ttu-id="b70a4-316">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-317">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-317">modelId</span></span> |<span data-ttu-id="b70a4-318">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-318">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-319">apiVersion</span></span> |<span data-ttu-id="b70a4-320">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-320">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-321">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-321">Request Body</span></span> |<span data-ttu-id="b70a4-322">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-322">NONE</span></span> |

<span data-ttu-id="b70a4-323">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-323">**Response**:</span></span>

<span data-ttu-id="b70a4-324">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-324">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-325">Merhaba veri özellikleri koleksiyonu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b70a4-325">hello data is returned as a collection of properties.</span></span>

* <span data-ttu-id="b70a4-326">`feed/entry/id/content/properties/key`-Hello özellik adı tutar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-326">`feed/entry/id/content/properties/key` - Holds hello property name.</span></span>
* <span data-ttu-id="b70a4-327">`feed/entry/id/content/properties/value`-Başlangıç özellik değeri tutar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-327">`feed/entry/id/content/properties/value` - Holds hello property value.</span></span>

<span data-ttu-id="b70a4-328">Merhaba tabloda her anahtar temsil eden hello değeri gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-328">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="b70a4-329">Anahtar</span><span class="sxs-lookup"><span data-stu-id="b70a4-329">Key</span></span> | <span data-ttu-id="b70a4-330">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b70a4-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="b70a4-331">AvgItemLength</span></span> |<span data-ttu-id="b70a4-332">Her öğe ayrı kullanıcıların ortalama sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="b70a4-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="b70a4-333">AvgUserLength</span></span> |<span data-ttu-id="b70a4-334">Kullanıcı başına farklı öğelerin ortalama sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="b70a4-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="b70a4-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="b70a4-336">Modelled olamaz ayıklama öğeleri sonra öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="b70a4-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="b70a4-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="b70a4-338">Ayıklama kullanıcılar ve modelled olamaz öğeler sonra kullanım sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="b70a4-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="b70a4-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="b70a4-340">Ayıklama kullanıcılar ve modelled olamaz öğeler sonra kullanım sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="b70a4-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="b70a4-341">MaxItemLength</span></span> |<span data-ttu-id="b70a4-342">Merhaba en popüler öğesi için benzersiz kullanıcı sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-342">Number of distinct users for hello most popular item.</span></span> |
| <span data-ttu-id="b70a4-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="b70a4-343">MaxUserLength</span></span> |<span data-ttu-id="b70a4-344">Bir kullanıcı için farklı öğe sayısı üst sınırından.</span><span class="sxs-lookup"><span data-stu-id="b70a4-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="b70a4-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="b70a4-345">MinItemLength</span></span> |<span data-ttu-id="b70a4-346">Bir öğe için benzersiz kullanıcı sayısı üst sınırından.</span><span class="sxs-lookup"><span data-stu-id="b70a4-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="b70a4-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="b70a4-347">MinUserLength</span></span> |<span data-ttu-id="b70a4-348">En az bir kullanıcı için farklı öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="b70a4-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="b70a4-349">RawNumberOfItems</span></span> |<span data-ttu-id="b70a4-350">Merhaba kullanım dosyalar öğelerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-350">Number of items in hello usage files.</span></span> |
| <span data-ttu-id="b70a4-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="b70a4-351">RawNumberOfUsers</span></span> |<span data-ttu-id="b70a4-352">Tüm ayıklama önce kullanım noktalarını sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="b70a4-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="b70a4-353">RawNumberOfRecords</span></span> |<span data-ttu-id="b70a4-354">Tüm ayıklama önce kullanım noktalarını sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="b70a4-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="b70a4-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="b70a4-356">Yok</span><span class="sxs-lookup"><span data-stu-id="b70a4-356">N/A</span></span> |
| <span data-ttu-id="b70a4-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="b70a4-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="b70a4-358">Yok</span><span class="sxs-lookup"><span data-stu-id="b70a4-358">N/A</span></span> |
| <span data-ttu-id="b70a4-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="b70a4-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="b70a4-360">Yok</span><span class="sxs-lookup"><span data-stu-id="b70a4-360">N/A</span></span> |

<span data-ttu-id="b70a4-361">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-361">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a><span data-ttu-id="b70a4-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="b70a4-362">6.2.</span></span>    <span data-ttu-id="b70a4-363">Model Insight</span><span class="sxs-lookup"><span data-stu-id="b70a4-363">Model Insight</span></span>
<span data-ttu-id="b70a4-364">Döndürür model Insight hello etkin yapı üzerinde veya (belirtilmişse) belirli bir yapı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="b70a4-364">Returns model insight on hello active build or (if given) on a specific build.</span></span>

<span data-ttu-id="b70a4-365">Yalnızca öneri derleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="b70a4-366">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-366">HTTP Method</span></span> | <span data-ttu-id="b70a4-367">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-368">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-368">GET</span></span> |<span data-ttu-id="b70a4-369">Etkin yapı Kimliğine sahip:</span><span class="sxs-lookup"><span data-stu-id="b70a4-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-370">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-371">Özel derleme Kimliğine sahip:</span><span class="sxs-lookup"><span data-stu-id="b70a4-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-372">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-372">Parameter Name</span></span> | <span data-ttu-id="b70a4-373">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-374">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-374">modelId</span></span> |<span data-ttu-id="b70a4-375">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-375">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-376">Buildıd</span><span class="sxs-lookup"><span data-stu-id="b70a4-376">buildId</span></span> |<span data-ttu-id="b70a4-377">İsteğe bağlı - başarılı bir yapı tanımlayan bir numara.</span><span class="sxs-lookup"><span data-stu-id="b70a4-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="b70a4-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-378">apiVersion</span></span> |<span data-ttu-id="b70a4-379">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-379">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-380">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-380">Request Body</span></span> |<span data-ttu-id="b70a4-381">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-381">NONE</span></span> |

<span data-ttu-id="b70a4-382">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-382">**Response**:</span></span>

<span data-ttu-id="b70a4-383">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-383">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-384">Merhaba veri özellikleri koleksiyonu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b70a4-384">hello data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="b70a4-385">Merhaba tabloda her anahtar temsil eden hello değeri gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-385">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="b70a4-386">Anahtar</span><span class="sxs-lookup"><span data-stu-id="b70a4-386">Key</span></span> | <span data-ttu-id="b70a4-387">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b70a4-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="b70a4-388">CatalogCoverage</span></span> |<span data-ttu-id="b70a4-389">Başlangıç kataloğu hangi kısmının ile kullanım desenlerini modelled.</span><span class="sxs-lookup"><span data-stu-id="b70a4-389">What part of hello catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="b70a4-390">Merhaba rest hello öğelerinin içerik tabanlı özellikleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-390">hello rest of hello items will need content-based features.</span></span> |
| <span data-ttu-id="b70a4-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="b70a4-391">Mpr</span></span> |<span data-ttu-id="b70a4-392">Merhaba modeli yüzdebirlik sıralamasını anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-392">Mean percentile ranking of hello model.</span></span> <span data-ttu-id="b70a4-393">Daha düşük daha iyidir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-393">Lower is better.</span></span> |
| <span data-ttu-id="b70a4-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="b70a4-394">NumberOfDimensions</span></span> |<span data-ttu-id="b70a4-395">Merhaba matris factorization algoritması tarafından kullanılan dimensions sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-395">Number of dimensions used by hello matrix factorization algorithm.</span></span> |

<span data-ttu-id="b70a4-396">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-396">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a><span data-ttu-id="b70a4-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="b70a4-397">6.3.</span></span>    <span data-ttu-id="b70a4-398">Model örnek alma</span><span class="sxs-lookup"><span data-stu-id="b70a4-398">Get Model Sample</span></span>
<span data-ttu-id="b70a4-399">Merhaba öneri model örneği alır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-399">Gets a sample of hello recommendation model.</span></span>

| <span data-ttu-id="b70a4-400">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-400">HTTP Method</span></span> | <span data-ttu-id="b70a4-401">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-402">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="b70a4-403">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-404">Özel derleme Kimliğine sahip:</span><span class="sxs-lookup"><span data-stu-id="b70a4-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="b70a4-405">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-406">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-406">Parameter Name</span></span> | <span data-ttu-id="b70a4-407">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-408">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-408">modelId</span></span> |<span data-ttu-id="b70a4-409">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-409">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-410">apiVersion</span></span> |<span data-ttu-id="b70a4-411">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-411">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-412">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-412">Request Body</span></span> |<span data-ttu-id="b70a4-413">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-413">NONE</span></span> |

<span data-ttu-id="b70a4-414">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-414">**Response**:</span></span>

<span data-ttu-id="b70a4-415">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-415">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-416">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-416">OData XML</span></span>

<span data-ttu-id="b70a4-417">Yanıt ham metin biçiminde verilir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-417">Response is returned in raw text format:</span></span>

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="b70a4-418">7. Model iş kuralları</span><span class="sxs-lookup"><span data-stu-id="b70a4-418">7. Model Business Rules</span></span>
<span data-ttu-id="b70a4-419">Bu, desteklenen kuralları hello türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b70a4-419">These are hello types of rules supported:</span></span>

* <span data-ttu-id="b70a4-420"><strong>Engelleme</strong> -engelleme tooprovide hello öneri sonuçlarında tooreturn istiyor musunuz öğelerinin bir listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-420"><strong>BlockList</strong> - BlockList enables you tooprovide a list of items that you do not want tooreturn in hello recommendation results.</span></span> 
* <span data-ttu-id="b70a4-421"><strong>FeatureBlockList</strong> -özelliğini engelleme özelliklerinin hello değerlerine göre tooblock öğeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you tooblock items based on hello values of its features.</span></span>

<span data-ttu-id="b70a4-422">*1000'den fazla öğe tek engelleme kuralında gönderme veya aramanız zaman aşımı olabilir. 1000'den fazla öğe tooblock gerekiyorsa, birkaç engelleme çağrıları yapabilirsiniz.*</span><span class="sxs-lookup"><span data-stu-id="b70a4-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need tooblock more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="b70a4-423"><strong>Upsale</strong> -Upsale tooenforce öğeleri tooreturn hello öneri sonuçlarında sağlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-423"><strong>Upsale</strong> - Upsale enables you tooenforce items tooreturn in hello recommendation results.</span></span>
* <span data-ttu-id="b70a4-424"><strong>Beyaz liste</strong> -beyaz liste etkinleştirir, tooonly öğelerin listesini önerileri öneririz.</span><span class="sxs-lookup"><span data-stu-id="b70a4-424"><strong>WhiteList</strong> - White List enables you tooonly suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="b70a4-425"><strong>FeatureWhiteList</strong> -özellik beyaz listesi belirli özellik değerlerine sahip tooonly öneri öğeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-425"><strong>FeatureWhiteList</strong> - Feature White List enables you tooonly recommend items that have specific feature values.</span></span>
* <span data-ttu-id="b70a4-426"><strong>PerSeedBlockList</strong> - çekirdek engelleme listesi etkinleştirir, tooprovide her bir öneri sonuçları olarak döndürülen öğe listesi öğesi başına.</span><span class="sxs-lookup"><span data-stu-id="b70a4-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you tooprovide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="b70a4-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="b70a4-427">7.1.</span></span>    <span data-ttu-id="b70a4-428">Modeli kuralları Al</span><span class="sxs-lookup"><span data-stu-id="b70a4-428">Get Model Rules</span></span>
| <span data-ttu-id="b70a4-429">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-429">HTTP Method</span></span> | <span data-ttu-id="b70a4-430">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-431">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="b70a4-432">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-433">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-433">Parameter Name</span></span> | <span data-ttu-id="b70a4-434">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-435">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-435">modelId</span></span> |<span data-ttu-id="b70a4-436">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-436">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-437">apiVersion</span></span> |<span data-ttu-id="b70a4-438">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-438">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-439">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-439">Request Body</span></span> |<span data-ttu-id="b70a4-440">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-440">NONE</span></span> |

<span data-ttu-id="b70a4-441">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-441">**Response**:</span></span>

<span data-ttu-id="b70a4-442">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="b70a4-443">`feed/entry/content/properties/Id`-Bu kural benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="b70a4-444">`feed/entry/content/properties/Type`-Hello kural türü.</span><span class="sxs-lookup"><span data-stu-id="b70a4-444">`feed/entry/content/properties/Type` - Type of hello rule.</span></span>
* <span data-ttu-id="b70a4-445">`feed/entry/content/properties/Parameter`-Kural parametresi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="b70a4-446">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-446">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a><span data-ttu-id="b70a4-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="b70a4-447">7.2.</span></span>    <span data-ttu-id="b70a4-448">Kural Ekle</span><span class="sxs-lookup"><span data-stu-id="b70a4-448">Add Rule</span></span>
| <span data-ttu-id="b70a4-449">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-449">HTTP Method</span></span> | <span data-ttu-id="b70a4-450">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-451">YAYINLA</span><span class="sxs-lookup"><span data-stu-id="b70a4-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="b70a4-452">ÜSTBİLGİ</span><span class="sxs-lookup"><span data-stu-id="b70a4-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="b70a4-453">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-453">Parameter Name</span></span> | <span data-ttu-id="b70a4-454">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-455">apiVersion</span></span> |<span data-ttu-id="b70a4-456">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-456">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-457">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-457">Request Body</span></span> | |

<span data-ttu-id="b70a4-458"><ins>Öğesi kimlikleri için iş kuralları sağlayan her emin toouse hello hello öğesinin dış kimliği yapın (Merhaba katalog dosyasında kullanılan aynı kimliği hello)</ins></span><span class="sxs-lookup"><span data-stu-id="b70a4-458"><ins>Whenever providing Item Ids for business rules, make sure toouse hello External Id of hello item (hello same Id that you used in hello catalog file)</ins></span></span><br><span data-ttu-id="b70a4-459">
<ins>tooadd engelleme kuralı:</ins></span><span class="sxs-lookup"><span data-stu-id="b70a4-459">
<ins>tooadd a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="b70a4-460"><ins>
<ins>tooadd FeatureBlockList kural:</ins></span><span class="sxs-lookup"><span data-stu-id="b70a4-460"><ins>
<ins>tooadd a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="b70a4-461"><ins>tooadd bir Upsale kuralı:</ins></span><span class="sxs-lookup"><span data-stu-id="b70a4-461"><ins> tooadd an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="b70a4-462">
<ins>tooadd bir beyaz liste kural:</ins></span><span class="sxs-lookup"><span data-stu-id="b70a4-462">
<ins>tooadd a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="b70a4-463"><ins>
<ins>tooadd FeatureWhiteList kural:</ins></span><span class="sxs-lookup"><span data-stu-id="b70a4-463"><ins>
<ins>tooadd a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="b70a4-464"><ins>tooadd PerSeedBlockList kural:</ins></span><span class="sxs-lookup"><span data-stu-id="b70a4-464"><ins> tooadd a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="b70a4-465">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-465">**Response**:</span></span>

<span data-ttu-id="b70a4-466">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-466">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-467">Merhaba API Yeni kuralın ayrıntılarını ile oluşturulan hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="b70a4-467">hello API returns hello newly created rule with its details.</span></span> <span data-ttu-id="b70a4-468">Merhaba kuralları özellik yolları aşağıdaki hello alınabilir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-468">hello rules property can be retrieved from hello following paths:</span></span>

* <span data-ttu-id="b70a4-469">`feed/entry/content/properties/Id`-Bu kural benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="b70a4-470">`feed/entry/content/properties/Type`-Hello kural türü: engelleme veya Upsale.</span><span class="sxs-lookup"><span data-stu-id="b70a4-470">`feed/entry/content/properties/Type` - Type of hello rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="b70a4-471">`feed/entry/content/properties/Parameter`-Kural parametresi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="b70a4-472">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-472">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a><span data-ttu-id="b70a4-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="b70a4-473">7.3.</span></span>    <span data-ttu-id="b70a4-474">Kural silme</span><span class="sxs-lookup"><span data-stu-id="b70a4-474">Delete Rule</span></span>
| <span data-ttu-id="b70a4-475">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-475">HTTP Method</span></span> | <span data-ttu-id="b70a4-476">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-477">SİL</span><span class="sxs-lookup"><span data-stu-id="b70a4-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-478">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-479">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-479">Parameter Name</span></span> | <span data-ttu-id="b70a4-480">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-481">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-481">modelId</span></span> |<span data-ttu-id="b70a4-482">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-482">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-483">filterId</span><span class="sxs-lookup"><span data-stu-id="b70a4-483">filterId</span></span> |<span data-ttu-id="b70a4-484">Merhaba filtre benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-484">Unique identifier of hello filter</span></span> |
| <span data-ttu-id="b70a4-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-485">apiVersion</span></span> |<span data-ttu-id="b70a4-486">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-486">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-487">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-487">Request Body</span></span> |<span data-ttu-id="b70a4-488">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-488">NONE</span></span> |

<span data-ttu-id="b70a4-489">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-489">**Response**:</span></span>

<span data-ttu-id="b70a4-490">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="b70a4-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="b70a4-491">7.4.</span></span>    <span data-ttu-id="b70a4-492">Tüm kuralları Sil</span><span class="sxs-lookup"><span data-stu-id="b70a4-492">Delete All Rules</span></span>
| <span data-ttu-id="b70a4-493">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-493">HTTP Method</span></span> | <span data-ttu-id="b70a4-494">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-495">SİL</span><span class="sxs-lookup"><span data-stu-id="b70a4-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-496">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-497">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-497">Parameter Name</span></span> | <span data-ttu-id="b70a4-498">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-499">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-499">modelId</span></span> |<span data-ttu-id="b70a4-500">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-501">apiVersion</span></span> |<span data-ttu-id="b70a4-502">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-502">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-503">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-503">Request Body</span></span> |<span data-ttu-id="b70a4-504">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-504">NONE</span></span> |

<span data-ttu-id="b70a4-505">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-505">**Response**:</span></span>

<span data-ttu-id="b70a4-506">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="b70a4-507">8. Katalog</span><span class="sxs-lookup"><span data-stu-id="b70a4-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="b70a4-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="b70a4-508">8.1.</span></span>    <span data-ttu-id="b70a4-509">Katalog verileri içeri aktar</span><span class="sxs-lookup"><span data-stu-id="b70a4-509">Import Catalog Data</span></span>
<span data-ttu-id="b70a4-510">Aynı model birkaç katalog dosyaları toohello birkaç çağrılarla yüklerseniz, biz yalnızca hello yeni katalog öğeleri ekler.</span><span class="sxs-lookup"><span data-stu-id="b70a4-510">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="b70a4-511">Varolan öğeleri hello özgün değerleriyle kalır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-511">Existing items will remain with hello original values.</span></span> <span data-ttu-id="b70a4-512">Bu yöntemi kullanarak katalog verilerini güncelleştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="b70a4-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="b70a4-513">başlangıç kataloğu veri biçimini izleyen hello izlemelidir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-513">hello catalog data should follow hello following format:</span></span>

* <span data-ttu-id="b70a4-514">Özellikleri-`<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="b70a4-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="b70a4-515">İle özellikleri-`<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="b70a4-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="b70a4-516">Not: hello en büyük dosya boyutu 200 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-516">Note: hello maximum file size is 200MB.</span></span>

<span data-ttu-id="b70a4-517">** Ayrıntıları Biçimlendir **</span><span class="sxs-lookup"><span data-stu-id="b70a4-517">** Format details **</span></span>

| <span data-ttu-id="b70a4-518">Ad</span><span class="sxs-lookup"><span data-stu-id="b70a4-518">Name</span></span> | <span data-ttu-id="b70a4-519">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="b70a4-519">Mandatory</span></span> | <span data-ttu-id="b70a4-520">Tür</span><span class="sxs-lookup"><span data-stu-id="b70a4-520">Type</span></span> | <span data-ttu-id="b70a4-521">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b70a4-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b70a4-522">Öğe kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-522">Item Id</span></span> |<span data-ttu-id="b70a4-523">Evet</span><span class="sxs-lookup"><span data-stu-id="b70a4-523">Yes</span></span> |<span data-ttu-id="b70a4-524">[A-z], [a-z], [0-9], [_] &#40; Alt çizgi &#41; [-] &#40; çizgi &#41;</span><span class="sxs-lookup"><span data-stu-id="b70a4-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="b70a4-525">En fazla uzunluk: 50</span><span class="sxs-lookup"><span data-stu-id="b70a4-525">Max length: 50</span></span> |<span data-ttu-id="b70a4-526">Bir öğeyi benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="b70a4-527">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-527">Item Name</span></span> |<span data-ttu-id="b70a4-528">Evet</span><span class="sxs-lookup"><span data-stu-id="b70a4-528">Yes</span></span> |<span data-ttu-id="b70a4-529">Herhangi bir alfasayısal karakter</span><span class="sxs-lookup"><span data-stu-id="b70a4-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="b70a4-530">En fazla uzunluk: 255</span><span class="sxs-lookup"><span data-stu-id="b70a4-530">Max length: 255</span></span> |<span data-ttu-id="b70a4-531">Öğe adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-531">Item name.</span></span> |
| <span data-ttu-id="b70a4-532">Öğesi kategorisi</span><span class="sxs-lookup"><span data-stu-id="b70a4-532">Item Category</span></span> |<span data-ttu-id="b70a4-533">Evet</span><span class="sxs-lookup"><span data-stu-id="b70a4-533">Yes</span></span> |<span data-ttu-id="b70a4-534">Herhangi bir alfasayısal karakter</span><span class="sxs-lookup"><span data-stu-id="b70a4-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="b70a4-535">En fazla uzunluk: 255</span><span class="sxs-lookup"><span data-stu-id="b70a4-535">Max length: 255</span></span> |<span data-ttu-id="b70a4-536">Kategori toowhich bu öğenin ait olduğu (örneğin pişirme kitapları, ekranda...); boş olabilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-536">Category toowhich this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="b70a4-537">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b70a4-537">Description</span></span> |<span data-ttu-id="b70a4-538">Hayır, özellikleri olmadıkça var (ancak boş olabilir)</span><span class="sxs-lookup"><span data-stu-id="b70a4-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="b70a4-539">Herhangi bir alfasayısal karakter</span><span class="sxs-lookup"><span data-stu-id="b70a4-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="b70a4-540">En fazla uzunluk: 4000</span><span class="sxs-lookup"><span data-stu-id="b70a4-540">Max length: 4000</span></span> |<span data-ttu-id="b70a4-541">Bu öğenin açıklaması.</span><span class="sxs-lookup"><span data-stu-id="b70a4-541">Description of this item.</span></span> |
| <span data-ttu-id="b70a4-542">Özellikler listesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-542">Features list</span></span> |<span data-ttu-id="b70a4-543">Hayır</span><span class="sxs-lookup"><span data-stu-id="b70a4-543">No</span></span> |<span data-ttu-id="b70a4-544">Herhangi bir alfasayısal karakter</span><span class="sxs-lookup"><span data-stu-id="b70a4-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="b70a4-545">En fazla uzunluk: 4000; Özellikler: 20 sayısı üst sınırı</span><span class="sxs-lookup"><span data-stu-id="b70a4-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="b70a4-546">Özellik adı virgülle ayrılmış listesini = kullanılan tooenhance modeli öneri; olabilir özellik değeri bkz: [konuları Gelişmiş](#2-advanced-topics) bölümü.</span><span class="sxs-lookup"><span data-stu-id="b70a4-546">Comma-separated list of feature name=feature value that can be used tooenhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="b70a4-547">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-547">HTTP Method</span></span> | <span data-ttu-id="b70a4-548">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-549">YAYINLA</span><span class="sxs-lookup"><span data-stu-id="b70a4-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-550">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="b70a4-551">ÜSTBİLGİ</span><span class="sxs-lookup"><span data-stu-id="b70a4-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="b70a4-552">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-552">Parameter Name</span></span> | <span data-ttu-id="b70a4-553">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-554">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-554">modelId</span></span> |<span data-ttu-id="b70a4-555">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-555">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-556">Dosya adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-556">filename</span></span> |<span data-ttu-id="b70a4-557">Başlangıç kataloğu metinsel tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-557">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="b70a4-558">Yalnızca harf (A-Z, a-z), sayılar (0-9), tireler (-) ve alt çizgi (_).</span><span class="sxs-lookup"><span data-stu-id="b70a4-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="b70a4-559">En fazla uzunluk: 50</span><span class="sxs-lookup"><span data-stu-id="b70a4-559">Max length: 50</span></span> |
| <span data-ttu-id="b70a4-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-560">apiVersion</span></span> |<span data-ttu-id="b70a4-561">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-561">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-562">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-562">Request Body</span></span> |<span data-ttu-id="b70a4-563">Örnek (özelliklerle ile):</span><span class="sxs-lookup"><span data-stu-id="b70a4-563">Example (with features):</span></span><br/><span data-ttu-id="b70a4-564">Clara Callan, kitap hello kitap açıklama 2406e770-769c-4189-89de-1c9283f93a96, yazar Richard Erikli = yayımcı Harper Flamingo Kanada = yıl 2001 =</span><span class="sxs-lookup"><span data-stu-id="b70a4-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,hello book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="b70a4-565">21bf8088-b6c0-4509-870c-e1c7ac78304a, hello Forgetting yer: A kurgu (Byzantium defteri), kitap,, yazar Nick Bantock = yayımcı Harpercollins, = yıl 1997 =</span><span class="sxs-lookup"><span data-stu-id="b70a4-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="b70a4-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23, Spadework, kitap,, yazar Attila Findley = yayımcı HarperFlamingo Kanada = yıl 2001 =</span><span class="sxs-lookup"><span data-stu-id="b70a4-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="b70a4-567">552a1940-21e4-4399-82bb-594b46d7ed54, Restraint, hayvanlar, kitap, hello kitap açıklama Yazar Magnus değirmenler = yayımcı Arcade yayımlama = yıl 1998 =</span><span class="sxs-lookup"><span data-stu-id="b70a4-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,hello book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="b70a4-568">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-568">**Response**:</span></span>

<span data-ttu-id="b70a4-569">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-569">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-570">Merhaba API hello alma raporunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="b70a4-570">hello API returns a report of hello import.</span></span>

* <span data-ttu-id="b70a4-571">`feed\entry\content\properties\LineCount`-Kabul satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="b70a4-572">`feed\entry\content\properties\ErrorCount`-Tooan hata eklenmemiş satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="b70a4-573">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-573">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a><span data-ttu-id="b70a4-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="b70a4-574">8.2.</span></span>    <span data-ttu-id="b70a4-575">Katalog alma</span><span class="sxs-lookup"><span data-stu-id="b70a4-575">Get Catalog</span></span>
<span data-ttu-id="b70a4-576">Tüm katalog öğelerini alır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="b70a4-577">başlangıç kataloğu olacaktır aynı anda bir sayfa alınır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-577">hello catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="b70a4-578">Belirli dizinindeki tooget öğe istiyorsanız hello $skip odata parametresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b70a4-578">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="b70a4-579">Örneğin, 100 konumdan başlayarak tooget öğe istiyorsanız, hello parametre $skip ekleme = 100 toohello istek.</span><span class="sxs-lookup"><span data-stu-id="b70a4-579">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="b70a4-580">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-580">HTTP Method</span></span> | <span data-ttu-id="b70a4-581">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-582">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-583">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-584">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-584">Parameter Name</span></span> | <span data-ttu-id="b70a4-585">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-586">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-586">modelId</span></span> |<span data-ttu-id="b70a4-587">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-587">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-588">apiVersion</span></span> |<span data-ttu-id="b70a4-589">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-589">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-590">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-590">Request Body</span></span> |<span data-ttu-id="b70a4-591">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-591">NONE</span></span> |

<span data-ttu-id="b70a4-592">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-592">**Response**:</span></span>

<span data-ttu-id="b70a4-593">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-593">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-594">Merhaba yanıt katalog öğesi her bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-594">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="b70a4-595">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-595">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-596">`feed/entry/content/properties/ExternalId`-Katalog öğesi dış kimliği, bir hello müşteri tarafından sağlanan hello.</span><span class="sxs-lookup"><span data-stu-id="b70a4-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, hello one provided by hello customer.</span></span>
* <span data-ttu-id="b70a4-597">`feed/entry/content/properties/InternalId`-Katalog öğesi iç kimliği, Azure Machine Learning önerileri oluşturan bir hello.</span><span class="sxs-lookup"><span data-stu-id="b70a4-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="b70a4-598">`feed/entry/content/properties/Name`-Katalog öğesi adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="b70a4-599">`feed/entry/content/properties/Category`-Katalog öğesi kategorisi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="b70a4-600">`feed/entry/content/properties/Description`-Katalog öğesi açıklaması.</span><span class="sxs-lookup"><span data-stu-id="b70a4-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="b70a4-601">`feed/entry/content/properties/Metadata`-Öğe meta verisi katalog.</span><span class="sxs-lookup"><span data-stu-id="b70a4-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="b70a4-602">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-602">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="b70a4-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="b70a4-603">8.3.</span></span>    <span data-ttu-id="b70a4-604">Katalog öğeleri belirteci göre alma</span><span class="sxs-lookup"><span data-stu-id="b70a4-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="b70a4-605">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-605">HTTP Method</span></span> | <span data-ttu-id="b70a4-606">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-607">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-608">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-609">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-609">Parameter Name</span></span> | <span data-ttu-id="b70a4-610">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-611">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-611">modelId</span></span> |<span data-ttu-id="b70a4-612">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-612">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-613">Belirteç</span><span class="sxs-lookup"><span data-stu-id="b70a4-613">token</span></span> |<span data-ttu-id="b70a4-614">Belirteç hello katalog öğesi'nin adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-614">Token of hello catalog item’s name.</span></span> <span data-ttu-id="b70a4-615">En az 3 karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="b70a4-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-616">apiVersion</span></span> |<span data-ttu-id="b70a4-617">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-617">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-618">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-618">Request Body</span></span> |<span data-ttu-id="b70a4-619">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-619">NONE</span></span> |

<span data-ttu-id="b70a4-620">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-620">**Response**:</span></span>

<span data-ttu-id="b70a4-621">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-621">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-622">Merhaba yanıt katalog öğesi her bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-622">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="b70a4-623">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-623">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-624">`feed/entry/content/properties/InternalId`-Katalog öğesi iç kimliği, Azure Machine Learning önerileri oluşturan bir hello.</span><span class="sxs-lookup"><span data-stu-id="b70a4-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="b70a4-625">`feed/entry/content/properties/Name`-Katalog öğesi adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="b70a4-626">`feed/entry/content/properties/Rating`-(gelecekte kullanmak için)</span><span class="sxs-lookup"><span data-stu-id="b70a4-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="b70a4-627">`feed/entry/content/properties/Reasoning`-(gelecekte kullanmak için)</span><span class="sxs-lookup"><span data-stu-id="b70a4-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="b70a4-628">`feed/entry/content/properties/Metadata`-(gelecekte kullanmak için)</span><span class="sxs-lookup"><span data-stu-id="b70a4-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="b70a4-629">`feed/entry/content/properties/FormattedRating`-(gelecekte kullanmak için)</span><span class="sxs-lookup"><span data-stu-id="b70a4-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="b70a4-630">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-630">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a><span data-ttu-id="b70a4-631">9. Kullanım verileri</span><span class="sxs-lookup"><span data-stu-id="b70a4-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="b70a4-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="b70a4-632">9.1.</span></span>    <span data-ttu-id="b70a4-633">Kullanım verilerini alma</span><span class="sxs-lookup"><span data-stu-id="b70a4-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="b70a4-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="b70a4-634">9.1.1.</span></span> <span data-ttu-id="b70a4-635">Dosya karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="b70a4-635">Uploading File</span></span>
<span data-ttu-id="b70a4-636">Bu bölümde gösterilmiştir nasıl dosyası kullanarak tooupload kullanım verileri.</span><span class="sxs-lookup"><span data-stu-id="b70a4-636">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="b70a4-637">Bu API birkaç kez ile kullanım verilerini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b70a4-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="b70a4-638">Tüm kullanım verileri tüm çağrıları için kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="b70a4-639">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-639">HTTP Method</span></span> | <span data-ttu-id="b70a4-640">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-641">YAYINLA</span><span class="sxs-lookup"><span data-stu-id="b70a4-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-642">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-643">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-643">Parameter Name</span></span> | <span data-ttu-id="b70a4-644">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-645">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-645">modelId</span></span> |<span data-ttu-id="b70a4-646">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-646">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-647">Dosya adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-647">filename</span></span> |<span data-ttu-id="b70a4-648">Başlangıç kataloğu metinsel tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-648">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="b70a4-649">Yalnızca harf (A-Z, a-z), sayılar (0-9), tireler (-) ve alt çizgi (_).</span><span class="sxs-lookup"><span data-stu-id="b70a4-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="b70a4-650">En fazla uzunluk: 50</span><span class="sxs-lookup"><span data-stu-id="b70a4-650">Max length: 50</span></span> |
| <span data-ttu-id="b70a4-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-651">apiVersion</span></span> |<span data-ttu-id="b70a4-652">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-652">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-653">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-653">Request Body</span></span> |<span data-ttu-id="b70a4-654">Kullanım verileri.</span><span class="sxs-lookup"><span data-stu-id="b70a4-654">Usage data.</span></span> <span data-ttu-id="b70a4-655">Biçimi:</span><span class="sxs-lookup"><span data-stu-id="b70a4-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="b70a4-656">Ad</span><span class="sxs-lookup"><span data-stu-id="b70a4-656">Name</span></span></th><th><span data-ttu-id="b70a4-657">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="b70a4-657">Mandatory</span></span></th><th><span data-ttu-id="b70a4-658">Tür</span><span class="sxs-lookup"><span data-stu-id="b70a4-658">Type</span></span></th><th><span data-ttu-id="b70a4-659">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b70a4-659">Description</span></span></th></tr><tr><td><span data-ttu-id="b70a4-660">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-660">User Id</span></span></td><td><span data-ttu-id="b70a4-661">Evet</span><span class="sxs-lookup"><span data-stu-id="b70a4-661">Yes</span></span></td><td><span data-ttu-id="b70a4-662">[A-z], [a-z], [0-9], [_] &#40; Alt çizgi &#41; [-] &#40; çizgi &#41;</span><span class="sxs-lookup"><span data-stu-id="b70a4-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="b70a4-663">En fazla uzunluk: 255</span><span class="sxs-lookup"><span data-stu-id="b70a4-663">Max length: 255</span></span> </td><td><span data-ttu-id="b70a4-664">Bir kullanıcının benzersiz tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="b70a4-665">Öğe kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-665">Item Id</span></span></td><td><span data-ttu-id="b70a4-666">Evet</span><span class="sxs-lookup"><span data-stu-id="b70a4-666">Yes</span></span></td><td><span data-ttu-id="b70a4-667">[A-z], [a-z], [0-9], [&#95;] &#40; Alt çizgi &#41; [-] &#40; çizgi &#41;</span><span class="sxs-lookup"><span data-stu-id="b70a4-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="b70a4-668">En fazla uzunluk: 50</span><span class="sxs-lookup"><span data-stu-id="b70a4-668">Max length: 50</span></span></td><td><span data-ttu-id="b70a4-669">Bir öğeyi benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="b70a4-670">Zaman</span><span class="sxs-lookup"><span data-stu-id="b70a4-670">Time</span></span></td><td><span data-ttu-id="b70a4-671">Hayır</span><span class="sxs-lookup"><span data-stu-id="b70a4-671">No</span></span></td><td><span data-ttu-id="b70a4-672">Tarih biçiminde: YYYY/AA/ddTHH (örneğin 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="b70a4-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="b70a4-673">Veri zamanı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="b70a4-674">Olay</span><span class="sxs-lookup"><span data-stu-id="b70a4-674">Event</span></span></td><td><span data-ttu-id="b70a4-675">Yok; sağlanan daha sonra tarih de konulmalıdır</span><span class="sxs-lookup"><span data-stu-id="b70a4-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="b70a4-676">Merhaba aşağıdakilerden biri:</span><span class="sxs-lookup"><span data-stu-id="b70a4-676">One of hello following:</span></span><br><span data-ttu-id="b70a4-677">• Tıklatın</span><span class="sxs-lookup"><span data-stu-id="b70a4-677">• Click</span></span><br><span data-ttu-id="b70a4-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="b70a4-678">• RecommendationClick</span></span><br><span data-ttu-id="b70a4-679">• AddShopCart</span><span class="sxs-lookup"><span data-stu-id="b70a4-679">•    AddShopCart</span></span><br><span data-ttu-id="b70a4-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="b70a4-680">• RemoveShopCart</span></span><br><span data-ttu-id="b70a4-681">• Satın alma</span><span class="sxs-lookup"><span data-stu-id="b70a4-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="b70a4-682">En büyük dosya boyutu: 200MB</span><span class="sxs-lookup"><span data-stu-id="b70a4-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="b70a4-683">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="b70a4-684">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-684">**Response**:</span></span>

<span data-ttu-id="b70a4-685">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="b70a4-686">`Feed\entry\content\properties\LineCount`-Kabul satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="b70a4-687">`Feed\entry\content\properties\ErrorCount`-Tooan hata eklenmemiş satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="b70a4-688">`Feed\entry\content\properties\FileId`-Dosya tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="b70a4-689">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-689">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="b70a4-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="b70a4-690">9.1.2.</span></span> <span data-ttu-id="b70a4-691">Veri alma kullanma</span><span class="sxs-lookup"><span data-stu-id="b70a4-691">Using Data Acquisition</span></span>
<span data-ttu-id="b70a4-692">Bu bölüm, gerçek toosend olayları tooAzure Machine Learning önerileri, genellikle Web sitenizi nasıl zaman gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-692">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="b70a4-693">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-693">HTTP Method</span></span> | <span data-ttu-id="b70a4-694">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-695">YAYINLA</span><span class="sxs-lookup"><span data-stu-id="b70a4-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="b70a4-696">ÜSTBİLGİ</span><span class="sxs-lookup"><span data-stu-id="b70a4-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="b70a4-697">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-697">Parameter Name</span></span> | <span data-ttu-id="b70a4-698">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-699">apiVersion</span></span> |<span data-ttu-id="b70a4-700">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-700">1.0</span></span> |
| <span data-ttu-id="b70a4-701">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-701">Request body</span></span> |<span data-ttu-id="b70a4-702">Olay veri girişi toosend istediğiniz her olay için.</span><span class="sxs-lookup"><span data-stu-id="b70a4-702">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="b70a4-703">Merhaba aynı kullanıcı veya tarayıcı oturumunu hello için aynı kimliği hello SessionID alanında göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-703">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="b70a4-704">(Olay gövdesi aşağıdaki örneği bakın.)</span><span class="sxs-lookup"><span data-stu-id="b70a4-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="b70a4-705">Olay 'Tıklatın' Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b70a4-705">Example for event 'Click':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="b70a4-706">Olay 'RecommendationClick' Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b70a4-706">Example for event 'RecommendationClick':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="b70a4-707">Olay 'AddShopCart' Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b70a4-707">Example for event 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="b70a4-708">Olay 'RemoveShopCart' Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b70a4-708">Example for event 'RemoveShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
              <EventData>
                      <Name>RemoveShopCart</Name>
                      <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="b70a4-709">Olay 'Satınalma' Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b70a4-709">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="b70a4-710">Örnek 2 olayları, 'Düğmesini tıklatarak' ve 'AddShopCart' gönderme:</span><span class="sxs-lookup"><span data-stu-id="b70a4-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

<span data-ttu-id="b70a4-711">**Yanıt**: HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="b70a4-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="b70a4-712">9.2.</span></span>    <span data-ttu-id="b70a4-713">Liste modeli kullanım dosyalar</span><span class="sxs-lookup"><span data-stu-id="b70a4-713">List Model Usage Files</span></span>
<span data-ttu-id="b70a4-714">Tüm model kullanım dosyalar meta verilerini alır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="b70a4-715">Merhaba kullanım dosyalar olacak bir sayfa aynı anda aldı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-715">hello usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="b70a4-716">Her sayfa içerir 100 öğeleri.</span><span class="sxs-lookup"><span data-stu-id="b70a4-716">Each page containes 100 items.</span></span> <span data-ttu-id="b70a4-717">Belirli dizinindeki tooget öğe istiyorsanız hello $skip odata parametresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b70a4-717">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="b70a4-718">Örneğin, 100 konumdan başlayarak tooget öğe istiyorsanız, hello parametre $skip ekleme = 100 toohello istek.</span><span class="sxs-lookup"><span data-stu-id="b70a4-718">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="b70a4-719">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-719">HTTP Method</span></span> | <span data-ttu-id="b70a4-720">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-721">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-722">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-723">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-723">Parameter Name</span></span> | <span data-ttu-id="b70a4-724">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-725">forModelId</span></span> |<span data-ttu-id="b70a4-726">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-726">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-727">apiVersion</span></span> |<span data-ttu-id="b70a4-728">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-728">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-729">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-729">Request Body</span></span> |<span data-ttu-id="b70a4-730">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-730">NONE</span></span> |

<span data-ttu-id="b70a4-731">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-731">**Response**:</span></span>

<span data-ttu-id="b70a4-732">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-732">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-733">Merhaba yanıt kullanım dosyasını her bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-733">hello response includes one entry per usage file.</span></span> <span data-ttu-id="b70a4-734">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-734">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-735">`feed\entry\content\properties\Id`-Kullanım dosya kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="b70a4-736">`feed\entry\content\properties\Length`-MB cinsinden kullanım dosya uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="b70a4-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="b70a4-737">`feed\entry\content\properties\DateModified`-Hello kullanım dosyasını oluşturulduğu tarih.</span><span class="sxs-lookup"><span data-stu-id="b70a4-737">`feed\entry\content\properties\DateModified` - Date when hello usage file was created.</span></span>
* <span data-ttu-id="b70a4-738">`feed\entry\content\properties\UseInModel`-Olup hello kullanım dosyasını hello modelinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-738">`feed\entry\content\properties\UseInModel` - Whether hello usage file is used in hello model.</span></span>

<span data-ttu-id="b70a4-739">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-739">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a><span data-ttu-id="b70a4-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="b70a4-740">9.3.</span></span>    <span data-ttu-id="b70a4-741">Kullanım istatistiklerini alın</span><span class="sxs-lookup"><span data-stu-id="b70a4-741">Get Usage Statistics</span></span>
<span data-ttu-id="b70a4-742">Kullanım istatistiklerini alır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-742">Gets usage statistics.</span></span>

| <span data-ttu-id="b70a4-743">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-743">HTTP Method</span></span> | <span data-ttu-id="b70a4-744">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-745">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-746">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-747">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-747">Parameter Name</span></span> | <span data-ttu-id="b70a4-748">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-749">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-749">modelId</span></span> |<span data-ttu-id="b70a4-750">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-750">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-751">StartDate</span><span class="sxs-lookup"><span data-stu-id="b70a4-751">startDate</span></span> |<span data-ttu-id="b70a4-752">Başlangıç tarihi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-752">Start date.</span></span> <span data-ttu-id="b70a4-753">Biçimi: yyyy/aa/ddTHH</span><span class="sxs-lookup"><span data-stu-id="b70a4-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="b70a4-754">endDate</span><span class="sxs-lookup"><span data-stu-id="b70a4-754">endDate</span></span> |<span data-ttu-id="b70a4-755">Bitiş tarihi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-755">End date.</span></span> <span data-ttu-id="b70a4-756">Biçimi: yyyy/aa/ddTHH</span><span class="sxs-lookup"><span data-stu-id="b70a4-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="b70a4-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="b70a4-757">eventTypes</span></span> |<span data-ttu-id="b70a4-758">Virgülle ayrılmış dize olay türleri veya tüm olayları tooget null</span><span class="sxs-lookup"><span data-stu-id="b70a4-758">Comma-separated string of event types or null tooget all events</span></span> |
| <span data-ttu-id="b70a4-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-759">apiVersion</span></span> |<span data-ttu-id="b70a4-760">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-760">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-761">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-761">Request Body</span></span> |<span data-ttu-id="b70a4-762">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-762">NONE</span></span> |

<span data-ttu-id="b70a4-763">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-763">**Response**:</span></span>

<span data-ttu-id="b70a4-764">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-764">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-765">Anahtar/değer öğeleri koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="b70a4-765">A collection of key/value elements.</span></span> <span data-ttu-id="b70a4-766">Her bir saate göre gruplandırılmış belirli bir olay türü için olayları hello toplamını içeriyor.</span><span class="sxs-lookup"><span data-stu-id="b70a4-766">Each one contains hello sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="b70a4-767">`feed\entry[i]\content\properties\Key`-Başlangıç saati (saate göre gruplandırılmış) içerir ve hello olay türü.</span><span class="sxs-lookup"><span data-stu-id="b70a4-767">`feed\entry[i]\content\properties\Key` - Contains hello time (grouped by hour) and hello event type.</span></span>
* <span data-ttu-id="b70a4-768">`feed\entry[i]\content\properties\Value`-Toplam olay sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="b70a4-769">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-769">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="b70a4-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="b70a4-770">9.4.</span></span>    <span data-ttu-id="b70a4-771">Kullanım örneği Al</span><span class="sxs-lookup"><span data-stu-id="b70a4-771">Get Usage File Sample</span></span>
<span data-ttu-id="b70a4-772">Alır kullanım dosya içeriğinin ilk 2 KB hello.</span><span class="sxs-lookup"><span data-stu-id="b70a4-772">Retrieves hello first 2KB of usage file content.</span></span>

| <span data-ttu-id="b70a4-773">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-773">HTTP Method</span></span> | <span data-ttu-id="b70a4-774">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-775">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-776">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-777">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-777">Parameter Name</span></span> | <span data-ttu-id="b70a4-778">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-779">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-779">modelId</span></span> |<span data-ttu-id="b70a4-780">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-780">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-781">Fileıd</span><span class="sxs-lookup"><span data-stu-id="b70a4-781">fileId</span></span> |<span data-ttu-id="b70a4-782">Merhaba modeli kullanım dosyanın benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-782">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="b70a4-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-783">apiVersion</span></span> |<span data-ttu-id="b70a4-784">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-784">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-785">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-785">Request Body</span></span> |<span data-ttu-id="b70a4-786">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-786">NONE</span></span> |

<span data-ttu-id="b70a4-787">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-787">**Response**:</span></span>

<span data-ttu-id="b70a4-788">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-788">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-789">Yanıt ham metin biçiminde verilir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-789">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a><span data-ttu-id="b70a4-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="b70a4-790">9.5.</span></span>    <span data-ttu-id="b70a4-791">Model kullanım dosyasını Al</span><span class="sxs-lookup"><span data-stu-id="b70a4-791">Get Model Usage File</span></span>
<span data-ttu-id="b70a4-792">Merhaba tam hello kullanım dosyasının içeriğini alır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-792">Retrieves hello full content of hello usage file.</span></span>

| <span data-ttu-id="b70a4-793">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-793">HTTP Method</span></span> | <span data-ttu-id="b70a4-794">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-795">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-796">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-797">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-797">Parameter Name</span></span> | <span data-ttu-id="b70a4-798">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-799">Orta</span><span class="sxs-lookup"><span data-stu-id="b70a4-799">mid</span></span> |<span data-ttu-id="b70a4-800">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-800">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-801">FID</span><span class="sxs-lookup"><span data-stu-id="b70a4-801">fid</span></span> |<span data-ttu-id="b70a4-802">Merhaba modeli kullanım dosyanın benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-802">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="b70a4-803">İndirme</span><span class="sxs-lookup"><span data-stu-id="b70a4-803">download</span></span> |<span data-ttu-id="b70a4-804">1</span><span class="sxs-lookup"><span data-stu-id="b70a4-804">1</span></span> |
| <span data-ttu-id="b70a4-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-805">apiVersion</span></span> |<span data-ttu-id="b70a4-806">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-806">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-807">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-807">Request Body</span></span> |<span data-ttu-id="b70a4-808">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-808">NONE</span></span> |

<span data-ttu-id="b70a4-809">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-809">**Response**:</span></span>

<span data-ttu-id="b70a4-810">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-810">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-811">Yanıt ham metin biçiminde verilir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-811">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a><span data-ttu-id="b70a4-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="b70a4-812">9.6.</span></span>    <span data-ttu-id="b70a4-813">Kullanım dosyasını silin</span><span class="sxs-lookup"><span data-stu-id="b70a4-813">Delete Usage File</span></span>
<span data-ttu-id="b70a4-814">Merhaba belirtilen model kullanım dosyasını siler.</span><span class="sxs-lookup"><span data-stu-id="b70a4-814">Deletes hello specified model usage file.</span></span>

| <span data-ttu-id="b70a4-815">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-815">HTTP Method</span></span> | <span data-ttu-id="b70a4-816">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-817">SİL</span><span class="sxs-lookup"><span data-stu-id="b70a4-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-818">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-819">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-819">Parameter Name</span></span> | <span data-ttu-id="b70a4-820">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-821">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-821">modelId</span></span> |<span data-ttu-id="b70a4-822">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-822">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-823">Fileıd</span><span class="sxs-lookup"><span data-stu-id="b70a4-823">fileId</span></span> |<span data-ttu-id="b70a4-824">Silinen hello dosya toobe benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-824">Unique identifier of hello file toobe deleted</span></span> |
| <span data-ttu-id="b70a4-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-825">apiVersion</span></span> |<span data-ttu-id="b70a4-826">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-826">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-827">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-827">Request Body</span></span> |<span data-ttu-id="b70a4-828">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-828">NONE</span></span> |

<span data-ttu-id="b70a4-829">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-829">**Response**:</span></span>

<span data-ttu-id="b70a4-830">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="b70a4-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="b70a4-831">9.7.</span></span>    <span data-ttu-id="b70a4-832">Tüm kullanım dosyalarını silin</span><span class="sxs-lookup"><span data-stu-id="b70a4-832">Delete All Usage Files</span></span>
<span data-ttu-id="b70a4-833">Tüm model kullanım dosyalarını siler.</span><span class="sxs-lookup"><span data-stu-id="b70a4-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="b70a4-834">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-834">HTTP Method</span></span> | <span data-ttu-id="b70a4-835">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-836">SİL</span><span class="sxs-lookup"><span data-stu-id="b70a4-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-837">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-838">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-838">Parameter Name</span></span> | <span data-ttu-id="b70a4-839">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-840">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-840">modelId</span></span> |<span data-ttu-id="b70a4-841">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-841">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-842">apiVersion</span></span> |<span data-ttu-id="b70a4-843">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-843">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-844">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-844">Request Body</span></span> |<span data-ttu-id="b70a4-845">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-845">NONE</span></span> |

<span data-ttu-id="b70a4-846">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-846">**Response**:</span></span>

<span data-ttu-id="b70a4-847">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="b70a4-848">10. Özellikler</span><span class="sxs-lookup"><span data-stu-id="b70a4-848">10. Features</span></span>
<span data-ttu-id="b70a4-849">Bu bölümde tooretrieve özellik içeri hello özellikleri ve bunların değerleri, kendi derece gibi bilgileri nasıl ve ne zaman bu derece ayrıldı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-849">This section shows how tooretrieve feature information, such as hello imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="b70a4-850">Özellikler hello katalog verilerini bir parçası olarak içe aktarılır ve bunların derece derece yapı yapıldığında sonra ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-850">Features are imported as part of hello catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="b70a4-851">Özellik derece kullanım verilerini ve tür öğelerinin according toohello düzenini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b70a4-851">Feature rank can change according toohello pattern of usage data and type of items.</span></span> <span data-ttu-id="b70a4-852">Ancak tutarlı kullanım/öğeler için yalnızca küçük dalgalanmaları hello derece olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-852">But for consistent usage/items, hello rank should have only small fluctuations.</span></span>
<span data-ttu-id="b70a4-853">Özellikler Hello derecesini negatif olmayan bir sayıdır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-853">hello rank of features is a non-negative number.</span></span> <span data-ttu-id="b70a4-854">Merhaba numarası 0 bu hello özelliği olmayan derece anlamına gelir (Bu hello ilk derece yapı API önceki toohello tamamlanmasından çağırma olur).</span><span class="sxs-lookup"><span data-stu-id="b70a4-854">hello  number 0 means that hello feature was not ranked (happens if you invoke this API prior toohello completion of hello first rank build).</span></span> <span data-ttu-id="b70a4-855">hangi hello derece öznitelikli hello tarih hello puan yenilik adı verilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-855">hello date at which hello rank was attributed is called hello score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="b70a4-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="b70a4-856">10.1.</span></span> <span data-ttu-id="b70a4-857">(İçin son derece derleme) özellikleri bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="b70a4-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="b70a4-858">Merhaba son başarılı derece yapı için bir derecelendirme hello özellik bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-858">Retrieves hello feature information, including ranking, for hello last successful rank build.</span></span>

| <span data-ttu-id="b70a4-859">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-859">HTTP Method</span></span> | <span data-ttu-id="b70a4-860">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-861">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-862">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-863">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-863">Parameter Name</span></span> | <span data-ttu-id="b70a4-864">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-865">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-865">modelId</span></span> |<span data-ttu-id="b70a4-866">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-866">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="b70a4-867">samplingSize</span></span> |<span data-ttu-id="b70a4-868">Başlangıç Kataloğu'nda mevcut toohello verileri göre her bir özellik için değerleri tooinclude sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-868">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span> <br/><span data-ttu-id="b70a4-869">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b70a4-869">Possible values are:</span></span><br> <span data-ttu-id="b70a4-870">-1 - tüm örnekleri.</span><span class="sxs-lookup"><span data-stu-id="b70a4-870">-1 - All samples.</span></span> <br><span data-ttu-id="b70a4-871">0 - hiçbir örnekleme.</span><span class="sxs-lookup"><span data-stu-id="b70a4-871">0 - No sampling.</span></span> <br><span data-ttu-id="b70a4-872">N - her bir özellik adı için dönüş N örneklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="b70a4-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-873">apiVersion</span></span> |<span data-ttu-id="b70a4-874">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-874">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-875">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-875">Request Body</span></span> |<span data-ttu-id="b70a4-876">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-876">NONE</span></span> |

<span data-ttu-id="b70a4-877">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-877">**Response**:</span></span>

<span data-ttu-id="b70a4-878">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-878">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-879">Merhaba yanıt özellik bilgileri girişlerinin listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-879">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="b70a4-880">Her giriş içerir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-880">Each entry contains:</span></span>

* <span data-ttu-id="b70a4-881">`feed/entry/content/m:properties/d:Name`-Özellik adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="b70a4-882">`feed/entry/content/m:properties/d:RankUpdateDate`-Date ayrılmış toothis özellik, sıralama sırasında hangi hello paketini:</span><span class="sxs-lookup"><span data-stu-id="b70a4-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="b70a4-883">puan yenilik özelliği.</span><span class="sxs-lookup"><span data-stu-id="b70a4-883">score freshness feature.</span></span> <span data-ttu-id="b70a4-884">Geçmiş bir tarih ('0001-01-01T00:00:00') hiçbir derece yapı gerçekleştirildiğini anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="b70a4-885">`feed/entry/content/m:properties/d:Rank`-Özellik derece (kayan nokta).</span><span class="sxs-lookup"><span data-stu-id="b70a4-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="b70a4-886">2.0 ve yedekleme bir derece iyi bir özellik olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="b70a4-887">`feed/entry/content/m:properties/d:SampleValues`-İstenen toohello örnekleme boyut değerleri virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="b70a4-888">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="b70a4-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="b70a4-889">10.2.</span></span> <span data-ttu-id="b70a4-890">(Belirli derece derleme için) özellikleri bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="b70a4-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="b70a4-891">Belirli bir derece yapı sıralaması hello hello özellik bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-891">Retrieves hello feature information, including hello ranking for a specific rank build.</span></span>

| <span data-ttu-id="b70a4-892">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-892">HTTP Method</span></span> | <span data-ttu-id="b70a4-893">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-894">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-895">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-896">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-896">Parameter Name</span></span> | <span data-ttu-id="b70a4-897">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-898">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-898">modelId</span></span> |<span data-ttu-id="b70a4-899">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-899">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="b70a4-900">samplingSize</span></span> |<span data-ttu-id="b70a4-901">Başlangıç Kataloğu'nda mevcut toohello verileri göre her bir özellik için değerleri tooinclude sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-901">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span><br/> <span data-ttu-id="b70a4-902">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b70a4-902">Possible values are:</span></span><br> <span data-ttu-id="b70a4-903">-1 - tüm örnekleri.</span><span class="sxs-lookup"><span data-stu-id="b70a4-903">-1 - All samples.</span></span> <br><span data-ttu-id="b70a4-904">0 - hiçbir örnekleme.</span><span class="sxs-lookup"><span data-stu-id="b70a4-904">0 - No sampling.</span></span> <br><span data-ttu-id="b70a4-905">N - her bir özellik adı için dönüş N örneklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="b70a4-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="b70a4-906">rankBuildId</span></span> |<span data-ttu-id="b70a4-907">Merhaba derece yapı veya -1 hello son derece yapı için benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-907">Unique identifier of hello rank build or -1 for hello last rank build</span></span> |
| <span data-ttu-id="b70a4-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-908">apiVersion</span></span> |<span data-ttu-id="b70a4-909">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-909">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-910">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-910">Request Body</span></span> |<span data-ttu-id="b70a4-911">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-911">NONE</span></span> |

<span data-ttu-id="b70a4-912">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-912">**Response**:</span></span>

<span data-ttu-id="b70a4-913">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-913">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-914">Merhaba yanıt özellik bilgileri girişlerinin listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-914">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="b70a4-915">Her giriş içerir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-915">Each entry contains:</span></span>

* <span data-ttu-id="b70a4-916">`feed/entry/content/m:properties/d:Name`-Özellik adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="b70a4-917">`feed/entry/content/m:properties/d:RankUpdateDate`-Date ayrılmış toothis özellik, sıralama sırasında hangi hello paketini:</span><span class="sxs-lookup"><span data-stu-id="b70a4-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="b70a4-918">puan yenilik özelliği.</span><span class="sxs-lookup"><span data-stu-id="b70a4-918">score freshness feature.</span></span> <span data-ttu-id="b70a4-919">Geçmiş bir tarih ('0001-01-01T00:00:00') hiçbir derece yapı gerçekleştirildiğini anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="b70a4-920">`feed/entry/content/m:properties/d:Rank`-Özellik derece (kayan nokta).</span><span class="sxs-lookup"><span data-stu-id="b70a4-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="b70a4-921">2.0 ve yedekleme bir derece iyi bir özellik olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="b70a4-922">`feed/entry/content/m:properties/d:SampleValues`-İstenen toohello örnekleme boyut değerleri virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="b70a4-923">OData</span><span class="sxs-lookup"><span data-stu-id="b70a4-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a><span data-ttu-id="b70a4-924">11. Oluşturma</span><span class="sxs-lookup"><span data-stu-id="b70a4-924">11. Build</span></span>
  <span data-ttu-id="b70a4-925">Bu bölümde hello açıklanmaktadır toobuilds ilgili farklı API'ler.</span><span class="sxs-lookup"><span data-stu-id="b70a4-925">This section explains hello different APIs related toobuilds.</span></span> <span data-ttu-id="b70a4-926">Derleme 3 türleri vardır: bir öneri yapı, derece yapı ve (sık birlikte satın) FBT derleme.</span><span class="sxs-lookup"><span data-stu-id="b70a4-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="b70a4-927">Merhaba öneri yapı, bir öneri modeli tahminleri için kullanılan toogenerate amaçtır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-927">hello recommendation build's purpose is toogenerate a recommendation model used for predictions.</span></span> <span data-ttu-id="b70a4-928">Öngörüler (için yapı bu tür) içinde iki özellikleri getirir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="b70a4-929">I2I - paketini</span><span class="sxs-lookup"><span data-stu-id="b70a4-929">I2I - a.k.a.</span></span> <span data-ttu-id="b70a4-930">Madde tooItem önerileri - verilen öğeyi veya liste öğelerinin bu seçenek, büyük olasılıkla toobe çok ilgisini çeken öğeleri listesini tahmin.</span><span class="sxs-lookup"><span data-stu-id="b70a4-930">Item tooItem recommendations - given an item or a list of items this option will predict a list of items that are likely toobe of high interest.</span></span>
* <span data-ttu-id="b70a4-931">U2I - paketini</span><span class="sxs-lookup"><span data-stu-id="b70a4-931">U2I - a.k.a.</span></span> <span data-ttu-id="b70a4-932">Kullanıcı tooItem önerileri verilen bir kullanıcı kimliği (ve isteğe bağlı olarak bir öğe listesi) - Bu seçenek, büyük olasılıkla toobe verilen kullanıcı (ve ek dilediği öğelerinin) hello çok ilgisini öğeleri listesini tahmin etmek.</span><span class="sxs-lookup"><span data-stu-id="b70a4-932">User tooItem recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely toobe of high interest for hello given user (and its additional choice of items).</span></span> <span data-ttu-id="b70a4-933">Merhaba U2I önerileri hello model oluşturulmuş toohello süresini hello kullanıcının ilgi olan öğelerin hello geçmişini dayanır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-933">hello U2I recommendations are based on hello history of items that were of interest for hello user up toohello time hello model was built.</span></span>

<span data-ttu-id="b70a4-934">Bir derece yapı özelliklerinizi hello yararlılığı hakkında toolearn sağlayan teknik bir yapıdır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-934">A rank build is a technical build that allows you toolearn about hello usefulness of your features.</span></span> <span data-ttu-id="b70a4-935">Genellikle, sipariş tooget hello en iyi sonucu özellikleri içeren bir öneri model için aşağıdaki adımları hello izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-935">Usually, in order tooget hello best result for a recommendation model involving features, you should take hello following steps:</span></span>

* <span data-ttu-id="b70a4-936">(Özelliklerinizi hello puanı kararlı değilse) derece bir derlemeyi tetiklemeyi ve hello özelliği puanı almak kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="b70a4-936">Trigger a rank build (unless hello score of your features is stable) and wait till you get hello feature score.</span></span>
* <span data-ttu-id="b70a4-937">Arama hello tarafından özelliklerinizi Hello derecesini almak [özellikleri bilgi al](#101-get-features-info-for-last-rank-build) API.</span><span class="sxs-lookup"><span data-stu-id="b70a4-937">Retrieve hello rank of your features by calling hello [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="b70a4-938">Bir öneri yapı şu parametreler hello ile yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="b70a4-938">Configure a recommendation build with hello following parameters:</span></span>
  * <span data-ttu-id="b70a4-939">`useFeatureInModel`-TooTrue ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-939">`useFeatureInModel` - Set tooTrue.</span></span>
  * <span data-ttu-id="b70a4-940">`ModelingFeatureList`-2.0 veya daha fazla puanı özelliklerinin set tooa virgülle ayrılmış listesi (Merhaba önceki adımda alınan toohello sıralar according).</span><span class="sxs-lookup"><span data-stu-id="b70a4-940">`ModelingFeatureList` - Set tooa comma-separated list of features with a score of 2.0 or more (according toohello ranks you retrieved in hello previous step).</span></span>
  * <span data-ttu-id="b70a4-941">`AllowColdItemPlacement`-TooTrue ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-941">`AllowColdItemPlacement` - Set tooTrue.</span></span>
  * <span data-ttu-id="b70a4-942">İsteğe bağlı olarak ayarlayabilirsiniz `EnableFeatureCorrelation` tooTrue ve `ReasoningFeatureList` toohello açıklamalarını (genellikle aynı özelliklerin listesi kullanılan Model oluşturma veya bir alt liste hello) toouse istediğiniz özelliklerin listesi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-942">Optionally you can set `EnableFeatureCorrelation` tooTrue and `ReasoningFeatureList` toohello list of features you want toouse for explanations (usually hello same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="b70a4-943">Merhaba öneri yapı yapılandırılmış hello parametrelerle tetikler.</span><span class="sxs-lookup"><span data-stu-id="b70a4-943">Trigger hello recommendation build with hello configured parameters.</span></span>

<span data-ttu-id="b70a4-944">Not: herhangi bir parametre yapılandırmazsanız (örneğin hello öneri yapı parametresiz çağırma) veya açıkça özellikleri hello kullanımını devre dışı değil (örneğin `UseFeatureInModel` ayarlamak tooFalse), hello sistem hello özelliği ile ilgili parametreleri ayarlayacak derece yapı mevcut durumda toohello değerleri yukarıdaki açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-944">Note: If you do not configure any parameters (e.g. invoke hello recommendation build without parameters) or you do not explicitly disable hello usage of features (e.g. `UseFeatureInModel` set tooFalse), hello system will set up hello feature-related parameters toohello explained values above in case a rank build exists.</span></span>

<span data-ttu-id="b70a4-945">Bir derece yapı çalıştırma sınırlaması yoktur ve bir öneri yapı eşzamanlı olarak Merhaba aynı modeli.</span><span class="sxs-lookup"><span data-stu-id="b70a4-945">There is no restriction on running a rank build and a recommendation build concurrently for hello same model.</span></span> <span data-ttu-id="b70a4-946">Bununla birlikte, aynı aynı paralel olarak model hello yazın hello iki derlemelerini çalıştırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="b70a4-946">Nevertheless, you cannot run two builds of hello same type on hello same model in parallel.</span></span>

<span data-ttu-id="b70a4-947">(Sık birlikte satın) FBT yapı henüz doğası gereği homojen olmayan katalogları için yararlı olan "Klasik" bazen öneren adlı başka bir önerileri algoritmasıdır (homojen: defterleri, filmler, bazı yemek deneyerek; homojen olmayan: bilgisayar ve cihazlar, etki alanları arası, oldukça farklı).</span><span class="sxs-lookup"><span data-stu-id="b70a4-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="b70a4-948">Not: hello karşıya yüklediğiniz kullanım dosyalar içeriyorsa hello isteğe bağlı alan "olay türü", daha sonra FBT için yalnızca "Satın Al" olayları modelleme kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-948">Note: if hello usage files that you uploaded contain hello optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="b70a4-949">Olay türü sağlanırsa tüm olayları satın alma olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="b70a4-950">11.1 parametreleri derleme</span><span class="sxs-lookup"><span data-stu-id="b70a4-950">11.1 Build parameters</span></span>
<span data-ttu-id="b70a4-951">Her bir yapı türü (aşağıda gösterilen) parametreleri kümesini aracılığıyla yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="b70a4-952">Merhaba parametreleri yapılandırmazsanız, hello sistem otomatik olarak toohello bilgi hello zaman mevcut bir derlemeyi tetiklemeyi göre değerleri toohello parametreleri öznitelik.</span><span class="sxs-lookup"><span data-stu-id="b70a4-952">If you don't configure hello parameters, hello system will automatically attribute values toohello parameters according toohello information present at hello time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="b70a4-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="b70a4-953">11.1.1.</span></span> <span data-ttu-id="b70a4-954">Kullanım Kondansatör</span><span class="sxs-lookup"><span data-stu-id="b70a4-954">Usage condenser</span></span>
<span data-ttu-id="b70a4-955">Kullanıcılar veya birkaç kullanım noktalarıyla öğeleri bilgileri'den daha fazla gürültü içerebilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="b70a4-956">Merhaba sistem toopredict hello en az bir model kullanılan kullanıcı/öğe toobe başına kullanım noktası denemesi sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-956">hello system attempts toopredict hello minimal number of usage points per user/item toobe used in a model.</span></span> <span data-ttu-id="b70a4-957">Bu numara, hello ItemCutoffLowerBound ve öğeleri ve hello UserCutOffLowerBound ve kullanıcılar için UserCutoffUpperBound parametreleri tarafından tanımlanan hello aralık ItemCutoffUpperBound parametreleri tarafından tanımlanan hello aralıkta olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-957">This number will be within hello range defined by hello ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and hello range defined by hello UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="b70a4-958">Merhaba Kondansatör etkisi öğeler veya kullanıcıların ayarıyla hello karşılık gelen sınırları toozero en az biri en aza indirgenebilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-958">hello condenser effect on items or users can be minimized by setting at least one of hello corresponding bounds toozero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="b70a4-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="b70a4-959">11.1.2.</span></span> <span data-ttu-id="b70a4-960">RANK yapı parametreleri</span><span class="sxs-lookup"><span data-stu-id="b70a4-960">Rank build parameters</span></span>
<span data-ttu-id="b70a4-961">Merhaba tabloda derece bir yapı için hello yapı parametreleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-961">hello table below depicts hello build parameters for a rank build.</span></span>

| <span data-ttu-id="b70a4-962">Anahtar</span><span class="sxs-lookup"><span data-stu-id="b70a4-962">Key</span></span> | <span data-ttu-id="b70a4-963">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b70a4-963">Description</span></span> | <span data-ttu-id="b70a4-964">Tür</span><span class="sxs-lookup"><span data-stu-id="b70a4-964">Type</span></span> | <span data-ttu-id="b70a4-965">Geçerli bir değer</span><span class="sxs-lookup"><span data-stu-id="b70a4-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b70a4-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="b70a4-966">NumberOfModelIterations</span></span> |<span data-ttu-id="b70a4-967">Merhaba hello modeli gerçekleştirir yineleme sayısını hello tarafından yansıtılan zaman ve hello model doğruluğundan genel işlem.</span><span class="sxs-lookup"><span data-stu-id="b70a4-967">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="b70a4-968">Merhaba daha yüksek hello sayı, hello daha iyi doğruluk alırsınız, ancak hello hesaplamak için daha uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="b70a4-968">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="b70a4-969">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-969">Integer</span></span> |<span data-ttu-id="b70a4-970">10-50</span><span class="sxs-lookup"><span data-stu-id="b70a4-970">10-50</span></span> |
| <span data-ttu-id="b70a4-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="b70a4-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="b70a4-972">Merhaba dimensions sayısı 'Özellikler' hello modeli toohello sayısı toofind verilerinizi içinde deneyecek ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-972">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="b70a4-973">Boyutlar Hello sayısını artırmayı daha iyi hello sonuçlarını daha küçük kümeler halinde hassas ayar yapma izin verir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-973">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="b70a4-974">Ancak, çok fazla boyutları bulmalarını bağıntıları öğeleri arasında hello modeli engeller.</span><span class="sxs-lookup"><span data-stu-id="b70a4-974">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="b70a4-975">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-975">Integer</span></span> |<span data-ttu-id="b70a4-976">10-40</span><span class="sxs-lookup"><span data-stu-id="b70a4-976">10-40</span></span> |
| <span data-ttu-id="b70a4-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="b70a4-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="b70a4-978">Merhaba öğesi alt sınır hello Kondansatör için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-978">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="b70a4-979">Yukarıdaki kullanım Kondansatör bakın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-979">See usage condenser above.</span></span> |<span data-ttu-id="b70a4-980">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-980">Integer</span></span> |<span data-ttu-id="b70a4-981">2 veya daha fazla (0 Kondansatör devre dışı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="b70a4-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="b70a4-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="b70a4-983">Merhaba öğesi üst sınır hello Kondansatör için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-983">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="b70a4-984">Yukarıdaki kullanım Kondansatör bakın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-984">See usage condenser above.</span></span> |<span data-ttu-id="b70a4-985">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-985">Integer</span></span> |<span data-ttu-id="b70a4-986">2 veya daha fazla (0 Kondansatör devre dışı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="b70a4-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="b70a4-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="b70a4-988">Merhaba kullanıcı alt sınır hello Kondansatör için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-988">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="b70a4-989">Yukarıdaki kullanım Kondansatör bakın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-989">See usage condenser above.</span></span> |<span data-ttu-id="b70a4-990">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-990">Integer</span></span> |<span data-ttu-id="b70a4-991">2 veya daha fazla (0 Kondansatör devre dışı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="b70a4-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="b70a4-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="b70a4-993">Merhaba kullanıcı üst sınır hello Kondansatör için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-993">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="b70a4-994">Yukarıdaki kullanım Kondansatör bakın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-994">See usage condenser above.</span></span> |<span data-ttu-id="b70a4-995">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-995">Integer</span></span> |<span data-ttu-id="b70a4-996">2 veya daha fazla (0 Kondansatör devre dışı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="b70a4-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="b70a4-997">11.1.3.</span></span> <span data-ttu-id="b70a4-998">Öneri yapı parametreleri</span><span class="sxs-lookup"><span data-stu-id="b70a4-998">Recommendation build parameters</span></span>
<span data-ttu-id="b70a4-999">Merhaba tabloda öneri yapı için hello yapı parametreleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-999">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="b70a4-1000">Anahtar</span><span class="sxs-lookup"><span data-stu-id="b70a4-1000">Key</span></span> | <span data-ttu-id="b70a4-1001">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b70a4-1001">Description</span></span> | <span data-ttu-id="b70a4-1002">Tür</span><span class="sxs-lookup"><span data-stu-id="b70a4-1002">Type</span></span> | <span data-ttu-id="b70a4-1003">Geçerli bir değer</span><span class="sxs-lookup"><span data-stu-id="b70a4-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b70a4-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="b70a4-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="b70a4-1005">Merhaba hello modeli gerçekleştirir yineleme sayısını hello tarafından yansıtılan zaman ve hello model doğruluğundan genel işlem.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1005">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="b70a4-1006">Merhaba daha yüksek hello sayı, hello daha iyi doğruluk alırsınız, ancak hello hesaplamak için daha uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1006">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="b70a4-1007">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1007">Integer</span></span> |<span data-ttu-id="b70a4-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="b70a4-1008">10-50</span></span> |
| <span data-ttu-id="b70a4-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="b70a4-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="b70a4-1010">Merhaba dimensions sayısı 'Özellikler' hello modeli toohello sayısı toofind verilerinizi içinde deneyecek ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1010">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="b70a4-1011">Boyutlar Hello sayısını artırmayı daha iyi hello sonuçlarını daha küçük kümeler halinde hassas ayar yapma izin verir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1011">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="b70a4-1012">Ancak, çok fazla boyutları bulmalarını bağıntıları öğeleri arasında hello modeli engeller.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1012">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="b70a4-1013">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1013">Integer</span></span> |<span data-ttu-id="b70a4-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="b70a4-1014">10-40</span></span> |
| <span data-ttu-id="b70a4-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="b70a4-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="b70a4-1016">Merhaba öğesi alt sınır hello Kondansatör için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1016">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="b70a4-1017">Yukarıdaki kullanım Kondansatör bakın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1017">See usage condenser above.</span></span> |<span data-ttu-id="b70a4-1018">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1018">Integer</span></span> |<span data-ttu-id="b70a4-1019">2 veya daha fazla (0 Kondansatör devre dışı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="b70a4-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="b70a4-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="b70a4-1021">Merhaba öğesi üst sınır hello Kondansatör için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1021">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="b70a4-1022">Yukarıdaki kullanım Kondansatör bakın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1022">See usage condenser above.</span></span> |<span data-ttu-id="b70a4-1023">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1023">Integer</span></span> |<span data-ttu-id="b70a4-1024">2 veya daha fazla (0 Kondansatör devre dışı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="b70a4-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="b70a4-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="b70a4-1026">Merhaba kullanıcı alt sınır hello Kondansatör için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1026">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="b70a4-1027">Yukarıdaki kullanım Kondansatör bakın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1027">See usage condenser above.</span></span> |<span data-ttu-id="b70a4-1028">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1028">Integer</span></span> |<span data-ttu-id="b70a4-1029">2 veya daha fazla (0 Kondansatör devre dışı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="b70a4-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="b70a4-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="b70a4-1031">Merhaba kullanıcı üst sınır hello Kondansatör için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1031">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="b70a4-1032">Yukarıdaki kullanım Kondansatör bakın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1032">See usage condenser above.</span></span> |<span data-ttu-id="b70a4-1033">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1033">Integer</span></span> |<span data-ttu-id="b70a4-1034">2 veya daha fazla (0 Kondansatör devre dışı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="b70a4-1035">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b70a4-1035">Description</span></span> |<span data-ttu-id="b70a4-1036">Açıklama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1036">Build description.</span></span> |<span data-ttu-id="b70a4-1037">Dize</span><span class="sxs-lookup"><span data-stu-id="b70a4-1037">String</span></span> |<span data-ttu-id="b70a4-1038">Herhangi bir metin en çok 512 karakter</span><span class="sxs-lookup"><span data-stu-id="b70a4-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="b70a4-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="b70a4-1039">EnableModelingInsights</span></span> |<span data-ttu-id="b70a4-1040">Merhaba öneri model üzerinde toocompute ölçümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1040">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="b70a4-1041">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b70a4-1041">Boolean</span></span> |<span data-ttu-id="b70a4-1042">True/False</span><span class="sxs-lookup"><span data-stu-id="b70a4-1042">True/False</span></span> |
| <span data-ttu-id="b70a4-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="b70a4-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="b70a4-1044">Özellikler sipariş tooenhance hello öneri modelinde kullandıysanız gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1044">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="b70a4-1045">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b70a4-1045">Boolean</span></span> |<span data-ttu-id="b70a4-1046">True/False</span><span class="sxs-lookup"><span data-stu-id="b70a4-1046">True/False</span></span> |
| <span data-ttu-id="b70a4-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="b70a4-1047">ModelingFeatureList</span></span> |<span data-ttu-id="b70a4-1048">Sipariş tooenhance hello öneri de hello öneri derlemede kullanılan özellik adları toobe virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1048">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="b70a4-1049">Dize</span><span class="sxs-lookup"><span data-stu-id="b70a4-1049">String</span></span> |<span data-ttu-id="b70a4-1050">Özellik adlarını, too512 karakter</span><span class="sxs-lookup"><span data-stu-id="b70a4-1050">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="b70a4-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="b70a4-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="b70a4-1052">Hello öneri de soğuk öğeleri özelliği benzerlik anında olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1052">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="b70a4-1053">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b70a4-1053">Boolean</span></span> |<span data-ttu-id="b70a4-1054">True/False</span><span class="sxs-lookup"><span data-stu-id="b70a4-1054">True/False</span></span> |
| <span data-ttu-id="b70a4-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="b70a4-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="b70a4-1056">Mantığı içinde kullanılabilir özellikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="b70a4-1057">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b70a4-1057">Boolean</span></span> |<span data-ttu-id="b70a4-1058">True/False</span><span class="sxs-lookup"><span data-stu-id="b70a4-1058">True/False</span></span> |
| <span data-ttu-id="b70a4-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="b70a4-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="b70a4-1060">Tümceler (örn. öneri açıklamaları) akıl için kullanılan özellik adları toobe virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1060">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="b70a4-1061">Dize</span><span class="sxs-lookup"><span data-stu-id="b70a4-1061">String</span></span> |<span data-ttu-id="b70a4-1062">Özellik adlarını, too512 karakter</span><span class="sxs-lookup"><span data-stu-id="b70a4-1062">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="b70a4-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="b70a4-1063">EnableU2I</span></span> |<span data-ttu-id="b70a4-1064">Kişiselleştirilmiş hello öneri paketini izin ver</span><span class="sxs-lookup"><span data-stu-id="b70a4-1064">Allow hello personalized recommendation a.k.a.</span></span> <span data-ttu-id="b70a4-1065">U2I (kullanıcı tooitem öneriler).</span><span class="sxs-lookup"><span data-stu-id="b70a4-1065">U2I (user tooitem recommendations).</span></span> |<span data-ttu-id="b70a4-1066">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b70a4-1066">Boolean</span></span> |<span data-ttu-id="b70a4-1067">True/False (varsayılan true)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="b70a4-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1068">11.1.4.</span></span> <span data-ttu-id="b70a4-1069">FBT yapı parametreleri</span><span class="sxs-lookup"><span data-stu-id="b70a4-1069">FBT build parameters</span></span>
<span data-ttu-id="b70a4-1070">Merhaba tabloda öneri yapı için hello yapı parametreleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1070">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="b70a4-1071">Anahtar</span><span class="sxs-lookup"><span data-stu-id="b70a4-1071">Key</span></span> | <span data-ttu-id="b70a4-1072">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b70a4-1072">Description</span></span> | <span data-ttu-id="b70a4-1073">Tür</span><span class="sxs-lookup"><span data-stu-id="b70a4-1073">Type</span></span> | <span data-ttu-id="b70a4-1074">Geçerli değer (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b70a4-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="b70a4-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="b70a4-1076">Koruyucu hello modeli nasıl.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1076">How conservative hello model is.</span></span> <span data-ttu-id="b70a4-1077">Modelleme için kabul öğeleri toobe ortak oluşumları sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1077">Number of co-occurrences of items toobe considered for modeling.</span></span> |<span data-ttu-id="b70a4-1078">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1078">Integer</span></span> |<span data-ttu-id="b70a4-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1079">3-50 (6)</span></span> |
| <span data-ttu-id="b70a4-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="b70a4-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="b70a4-1081">Öğe sık kümesinde sınırları hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1081">Bounds hello number of items in a frequent set.</span></span> |<span data-ttu-id="b70a4-1082">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1082">Integer</span></span> |<span data-ttu-id="b70a4-1083">2-3 (2)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1083">2-3 (2)</span></span> |
| <span data-ttu-id="b70a4-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="b70a4-1084">FbtMinimalScore</span></span> |<span data-ttu-id="b70a4-1085">Sık kümesi hello dahil sipariş toobe içinde döndürülen en az puan sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1085">Minimal score that a frequent set should have in order toobe included in hello returned results.</span></span> <span data-ttu-id="b70a4-1086">Merhaba yüksek hello daha iyi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1086">hello higher hello better.</span></span> |<span data-ttu-id="b70a4-1087">Çift</span><span class="sxs-lookup"><span data-stu-id="b70a4-1087">Double</span></span> |<span data-ttu-id="b70a4-1088">0 ve üstünde (0)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1088">0 and above (0)</span></span> |
| <span data-ttu-id="b70a4-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="b70a4-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="b70a4-1090">Merhaba yapı tarafından kullanılan hello benzerlik işlevi toobe tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1090">Defines hello similarity function toobe used by hello build.</span></span> <span data-ttu-id="b70a4-1091">Yükseltme serendipity korur, ortak oluşumu öngörülebilirlik ayrıcalıklı kılar ve Jaccard hello iki arasında iyi bir seçim değil.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between hello two.</span></span> |<span data-ttu-id="b70a4-1092">Dize</span><span class="sxs-lookup"><span data-stu-id="b70a4-1092">String</span></span> |<span data-ttu-id="b70a4-1093">cooccurrence, yükseltme, jaccard (yükseltme)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="b70a4-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1094">11.2.</span></span> <span data-ttu-id="b70a4-1095">Tetikleyici bir öneri derleme</span><span class="sxs-lookup"><span data-stu-id="b70a4-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="b70a4-1096">Varsayılan olarak bu API öneri modeli yapı tetikler.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="b70a4-1097">tootrigger bir derece derleme (sipariş tooscore özelliklerinde), hello yapı API değişken yapı tür parametresi birlikte kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1097">tootrigger a rank build (in order tooscore  features), hello build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="b70a4-1098">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1098">HTTP Method</span></span> | <span data-ttu-id="b70a4-1099">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1100">YAYINLA</span><span class="sxs-lookup"><span data-stu-id="b70a4-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1101">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="b70a4-1102">ÜSTBİLGİ</span><span class="sxs-lookup"><span data-stu-id="b70a4-1102">HEADER</span></span> |<span data-ttu-id="b70a4-1103">`"Content-Type", "text/xml"`(İstek gövdesi gönderiliyorsa)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="b70a4-1104">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1104">Parameter Name</span></span> | <span data-ttu-id="b70a4-1105">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1106">modelId</span></span> |<span data-ttu-id="b70a4-1107">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1107">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="b70a4-1108">userDescription</span></span> |<span data-ttu-id="b70a4-1109">Başlangıç kataloğu metinsel tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1109">Textual identifier of hello catalog.</span></span> <span data-ttu-id="b70a4-1110">Boşluklar kullanırsanız, % 20 yerine kodlamak gerekir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="b70a4-1111">Yukarıdaki örnekte bkz.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1111">See example above.</span></span><br><span data-ttu-id="b70a4-1112">En fazla uzunluk: 50</span><span class="sxs-lookup"><span data-stu-id="b70a4-1112">Max length: 50</span></span> |
| <span data-ttu-id="b70a4-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1113">apiVersion</span></span> |<span data-ttu-id="b70a4-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-1115">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1115">Request Body</span></span> |<span data-ttu-id="b70a4-1116">Boş bırakılırsa hello yapı hello varsayılan derleme parametrelerle yürütülür.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1116">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="b70a4-1117">Hello parametreleri XML olarak tooset hello yapı parametreleri isterseniz, örnek aşağıdaki hello olduğu gibi hello gövdesine gönderin.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1117">If you want tooset hello build parameters, send hello parameters as XML into hello body as in hello following sample.</span></span> <span data-ttu-id="b70a4-1118">(Merhaba parametreleri bir açıklaması için hello "yapı parametreleri" bölümüne bakın.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="b70a4-1118">(See hello "Build parameters" section for an explanation of hello parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="b70a4-1119">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1119">**Response**:</span></span>

<span data-ttu-id="b70a4-1120">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1121">Bu zaman uyumsuz bir API'dir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1121">This is an asynchronous API.</span></span> <span data-ttu-id="b70a4-1122">Yanıt olarak bir yapı kimliği alırsınız.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="b70a4-1123">Merhaba derleme sona erdiğinde tooknow hello "Get derlemeler durumu bir modelin" API çağrısı ve gerekir bulun hello yanıtta bu derleme kimliği.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1123">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="b70a4-1124">Bir yapı dakika toohours hello hello verilerin boyutuna bağlı olarak gelen alabileceğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1124">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="b70a4-1125">Merhaba yapı kadar sona erer önerileri kullanamayacaklarını.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1125">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="b70a4-1126">Geçerli yapı durumu:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1126">Valid build status:</span></span>

* <span data-ttu-id="b70a4-1127">Oluşturma - yapı isteği oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="b70a4-1128">Sıraya alınmış - yapı isteği gönderildi ve kuyruğa alınır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="b70a4-1129">Yapı - Yapı devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="b70a4-1130">Başarılı - yapı başarılı bir şekilde sona erdi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="b70a4-1131">Hata - derleme bir hata ile sona erdi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="b70a4-1132">İptal - derleme iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="b70a4-1133">İptal etme - hello yapı için bir iptal etme isteği gönderildi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1133">Cancelling - A cancel request for hello build was sent.</span></span>

<span data-ttu-id="b70a4-1134">Kimliği yolu izleyerek hello altında bulunabilir bu hello yapı dikkat edin:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="b70a4-1134">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="b70a4-1135">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-1135">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="b70a4-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1136">11.3.</span></span> <span data-ttu-id="b70a4-1137">Tetikleyici yapı (öneri, derece veya FBT)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="b70a4-1138">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1138">HTTP Method</span></span> | <span data-ttu-id="b70a4-1139">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1140">YAYINLA</span><span class="sxs-lookup"><span data-stu-id="b70a4-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1141">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="b70a4-1142">ÜSTBİLGİ</span><span class="sxs-lookup"><span data-stu-id="b70a4-1142">HEADER</span></span> |<span data-ttu-id="b70a4-1143">`"Content-Type", "text/xml"`(İstek gövdesi gönderiliyorsa)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="b70a4-1144">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1144">Parameter Name</span></span> | <span data-ttu-id="b70a4-1145">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1146">modelId</span></span> |<span data-ttu-id="b70a4-1147">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1147">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="b70a4-1148">userDescription</span></span> |<span data-ttu-id="b70a4-1149">Başlangıç kataloğu metinsel tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1149">Textual identifier of hello catalog.</span></span> <span data-ttu-id="b70a4-1150">Boşluklar kullanırsanız, % 20 yerine kodlamak gerekir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="b70a4-1151">Yukarıdaki örnekte bkz.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1151">See example above.</span></span><br><span data-ttu-id="b70a4-1152">En fazla uzunluk: 50</span><span class="sxs-lookup"><span data-stu-id="b70a4-1152">Max length: 50</span></span> |
| <span data-ttu-id="b70a4-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="b70a4-1153">buildType</span></span> |<span data-ttu-id="b70a4-1154">Merhaba yapı tooinvoke türü:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1154">Type of hello build tooinvoke:</span></span> <br/> <span data-ttu-id="b70a4-1155">-Öneri yapı ' Önerisi'</span><span class="sxs-lookup"><span data-stu-id="b70a4-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="b70a4-1156">-'Rank derleme için sıralaması'</span><span class="sxs-lookup"><span data-stu-id="b70a4-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="b70a4-1157">-FBT yapı için ' Fbt'</span><span class="sxs-lookup"><span data-stu-id="b70a4-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="b70a4-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1158">apiVersion</span></span> |<span data-ttu-id="b70a4-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-1160">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1160">Request Body</span></span> |<span data-ttu-id="b70a4-1161">Boş bırakılırsa hello yapı hello varsayılan derleme parametrelerle yürütülür.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1161">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="b70a4-1162">Merhaba gövdesinde gibi örnek aşağıdaki hello içine tooset yapı parametreleri istiyorsanız, bunları XML olarak gönderin.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1162">If you want tooset build parameters, send them as XML into hello body like in hello following sample.</span></span> <span data-ttu-id="b70a4-1163">(Bir açıklama ve hello parametrelerin tam listesi için hello "yapı parametreleri" bölümüne bakın.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="b70a4-1163">(See hello "Build parameters" section for an explanation and full list of hello parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="b70a4-1164">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1164">**Response**:</span></span>

<span data-ttu-id="b70a4-1165">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1166">Bu zaman uyumsuz bir API'dir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1166">This is an asynchronous API.</span></span> <span data-ttu-id="b70a4-1167">Yanıt olarak bir yapı kimliği alırsınız.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="b70a4-1168">Merhaba derleme sona erdiğinde tooknow hello "Get derlemeler durumu bir modelin" API çağrısı ve gerekir bulun hello yanıtta bu derleme kimliği.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1168">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="b70a4-1169">Bir yapı dakika toohours hello hello verilerin boyutuna bağlı olarak gelen alabileceğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1169">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="b70a4-1170">Merhaba yapı kadar sona erer önerileri kullanamayacaklarını.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1170">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="b70a4-1171">Geçerli yapı durumu:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1171">Valid build status:</span></span>

* <span data-ttu-id="b70a4-1172">Oluşturma - Model oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1172">Create - Model was created.</span></span>
* <span data-ttu-id="b70a4-1173">Sıraya alınmış - Model yapı tetiklendi ve kuyruğa alınır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="b70a4-1174">Yapı - modeli oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="b70a4-1175">Başarılı - yapı başarılı bir şekilde sona erdi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="b70a4-1176">Hata - derleme bir hata ile sona erdi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="b70a4-1177">İptal - derleme iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="b70a4-1178">İptal etme - derleme iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="b70a4-1179">Kimliği yolu izleyerek hello altında bulunabilir bu hello yapı dikkat edin:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="b70a4-1179">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="b70a4-1180">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-1180">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="b70a4-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1181">11.4.</span></span> <span data-ttu-id="b70a4-1182">Bir modelin derlemeleri durumunu Al</span><span class="sxs-lookup"><span data-stu-id="b70a4-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="b70a4-1183">Yapılar ve belirtilen bir model için durumlarını alır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="b70a4-1184">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1184">HTTP Method</span></span> | <span data-ttu-id="b70a4-1185">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1186">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1187">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1188">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1188">Parameter Name</span></span> | <span data-ttu-id="b70a4-1189">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1190">modelId</span></span> |<span data-ttu-id="b70a4-1191">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1191">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="b70a4-1192">onlyLastBuild</span></span> |<span data-ttu-id="b70a4-1193">Gösteren tüm hello tooreturn hello modeli geçmişini ya da hello en son yapı yalnızca hello durumunu derleme</span><span class="sxs-lookup"><span data-stu-id="b70a4-1193">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build</span></span> |
| <span data-ttu-id="b70a4-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1194">apiVersion</span></span> |<span data-ttu-id="b70a4-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1195">1.0</span></span> |

<span data-ttu-id="b70a4-1196">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1196">**Response**:</span></span>

<span data-ttu-id="b70a4-1197">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1198">Merhaba yanıt yapı her bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1198">hello response includes one entry per build.</span></span> <span data-ttu-id="b70a4-1199">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1199">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-1200">`feed/entry/content/properties/UserName`-Hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1200">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="b70a4-1201">`feed/entry/content/properties/ModelName`-Hello model adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1201">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="b70a4-1202">`feed/entry/content/properties/ModelId`-Model benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="b70a4-1203">`feed/entry/content/properties/IsDeployed`-Olup hello yapı (paketini dağıtılır</span><span class="sxs-lookup"><span data-stu-id="b70a4-1203">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="b70a4-1204">Etkin yapı).</span><span class="sxs-lookup"><span data-stu-id="b70a4-1204">active build).</span></span>
* <span data-ttu-id="b70a4-1205">`feed/entry/content/properties/BuildId`-Benzersiz tanımlayıcısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="b70a4-1206">`feed/entry/content/properties/BuildType`-Hello yapı türü.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1206">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="b70a4-1207">`feed/entry/content/properties/Status`-Durum oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="b70a4-1208">Merhaba aşağıdakilerden biri olabilir: hata, yapı, sıraya alınan, Cancelling, iptal edildi, başarılı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1208">Can be one of hello following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="b70a4-1209">`feed/entry/content/properties/StatusMessage`-Ayrıntılı durum iletisi (yalnızca toospecific durumlar geçerlidir).</span><span class="sxs-lookup"><span data-stu-id="b70a4-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="b70a4-1210">`feed/entry/content/properties/Progress`-İlerleme durumu (%) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="b70a4-1211">`feed/entry/content/properties/StartTime`-Başlangıç saati oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="b70a4-1212">`feed/entry/content/properties/EndTime`-Bitiş saati oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="b70a4-1213">`feed/entry/content/properties/ExecutionTime`-Yapı süresi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="b70a4-1214">`feed/entry/content/properties/ProgressStep`-Devam eden bir derleme geçerli aşamasını hello hakkında ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1214">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="b70a4-1215">Geçerli yapı durumu:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1215">Valid build status:</span></span>

* <span data-ttu-id="b70a4-1216">Oluşturulan - yapı isteği girdisi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="b70a4-1217">Sıraya alınmış - oluşturma isteği tetiklendi ve kuyruğa alınır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="b70a4-1218">Yapı - Yapı işlemi devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="b70a4-1219">Başarılı - yapı başarılı bir şekilde sona erdi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="b70a4-1220">Hata - derleme bir hata ile sona erdi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="b70a4-1221">İptal - derleme iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="b70a4-1222">İptal etme - derleme iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="b70a4-1223">Derleme türü için geçerli değerler:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1223">Valid values for build type:</span></span>

* <span data-ttu-id="b70a4-1224">RANK - derece oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="b70a4-1225">Öneri - öneri derleme.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="b70a4-1226">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-1226">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
                    <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
                    <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
                    <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
                    <d:BuildId m:type="Edm.String">1000272</d:BuildId>
                    <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
                    <d:Status m:type="Edm.String">Success</d:Status>
                    <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
                    <d:Progress m:type="Edm.String">0</d:Progress>
                    <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
                    <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
                    <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
                    <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
                    <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
                </m:properties>
            </content>
        </entry>
    </feed>


### <a name="115-get-builds-status"></a><span data-ttu-id="b70a4-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1227">11.5.</span></span> <span data-ttu-id="b70a4-1228">Derlemeleri durumunu Al</span><span class="sxs-lookup"><span data-stu-id="b70a4-1228">Get Builds Status</span></span>
<span data-ttu-id="b70a4-1229">Alır, bir kullanıcının tüm modellerin durumlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="b70a4-1230">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1230">HTTP Method</span></span> | <span data-ttu-id="b70a4-1231">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1232">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1233">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1234">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1234">Parameter Name</span></span> | <span data-ttu-id="b70a4-1235">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="b70a4-1236">onlyLastBuild</span></span> |<span data-ttu-id="b70a4-1237">Gösteren tüm hello tooreturn hello modeli geçmişini ya da hello en son yapı yalnızca hello durumunu derleme.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1237">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="b70a4-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1238">apiVersion</span></span> |<span data-ttu-id="b70a4-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1239">1.0</span></span> |

<span data-ttu-id="b70a4-1240">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1240">**Response**:</span></span>

<span data-ttu-id="b70a4-1241">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1242">Merhaba yanıt yapı her bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1242">hello response includes one entry per build.</span></span> <span data-ttu-id="b70a4-1243">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1243">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-1244">`feed/entry/content/properties/UserName`-Hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1244">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="b70a4-1245">`feed/entry/content/properties/ModelName`-Hello model adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1245">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="b70a4-1246">`feed/entry/content/properties/ModelId`-Model benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="b70a4-1247">`feed/entry/content/properties/IsDeployed`-Olup hello yapı dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1247">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed.</span></span>
* <span data-ttu-id="b70a4-1248">`feed/entry/content/properties/BuildId`-Benzersiz tanımlayıcısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="b70a4-1249">`feed/entry/content/properties/BuildType`-Hello yapı türü.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1249">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="b70a4-1250">`feed/entry/content/properties/Status`-Durum oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="b70a4-1251">Merhaba aşağıdakilerden biri olabilir: hata, yapı, sıraya alınan, iptal edildi, Cancelling, başarılı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1251">Can be one of hello following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="b70a4-1252">`feed/entry/content/properties/StatusMessage`-Ayrıntılı durum iletisi (yalnızca toospecific durumlar geçerlidir).</span><span class="sxs-lookup"><span data-stu-id="b70a4-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="b70a4-1253">`feed/entry/content/properties/Progress`-İlerleme durumu (%) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="b70a4-1254">`feed/entry/content/properties/StartTime`-Başlangıç saati oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="b70a4-1255">`feed/entry/content/properties/EndTime`-Bitiş saati oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="b70a4-1256">`feed/entry/content/properties/ExecutionTime`-Yapı süresi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="b70a4-1257">`feed/entry/content/properties/ProgressStep`-Devam eden bir derleme geçerli aşamasını hello hakkında ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1257">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="b70a4-1258">Geçerli yapı durumu:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1258">Valid build status:</span></span>

* <span data-ttu-id="b70a4-1259">Oluşturulan - yapı isteği girdisi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="b70a4-1260">Sıraya alınmış - oluşturma isteği tetiklendi ve kuyruğa alınır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="b70a4-1261">Yapı - Yapı işlemi devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="b70a4-1262">Başarılı - yapı başarılı bir şekilde sona erdi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="b70a4-1263">Hata - derleme bir hata ile sona erdi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="b70a4-1264">İptal - derleme iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="b70a4-1265">İptal etme - derleme iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="b70a4-1266">Derleme türü için geçerli değerler:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1266">Valid values for build type:</span></span>

* <span data-ttu-id="b70a4-1267">RANK - derece oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="b70a4-1268">Öneri - öneri derleme.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="b70a4-1269">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-1269">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
                    <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
                    <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
                    <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
                    <d:BuildId m:type="Edm.String">1000272</d:BuildId>
                    <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
                    <d:Status m:type="Edm.String">Success</d:Status>
                    <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
                    <d:Progress m:type="Edm.String">0</d:Progress>
                    <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
                    <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
                    <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
                    <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
                    <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
                </m:properties>
            </content>
        </entry>
    </feed>


### <a name="116-delete-build"></a><span data-ttu-id="b70a4-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1270">11.6.</span></span> <span data-ttu-id="b70a4-1271">Yapı Sil</span><span class="sxs-lookup"><span data-stu-id="b70a4-1271">Delete Build</span></span>
<span data-ttu-id="b70a4-1272">Bir yapı siler.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1272">Deletes a build.</span></span>

<span data-ttu-id="b70a4-1273">NOT:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1273">NOTE:</span></span> <br><span data-ttu-id="b70a4-1274">Etkin bir yapı silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1274">You cannot delete an active build.</span></span> <span data-ttu-id="b70a4-1275">Merhaba modeli olmalıdır tooa farklı etkin yapı silmeden önce güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1275">hello model should be updated tooa different active build before you delete it.</span></span><br><span data-ttu-id="b70a4-1276">Devam eden yapı silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="b70a4-1277">Merhaba yapı ilk çağırarak iptal <strong>iptal yapı</strong>.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1277">You should cancel hello build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="b70a4-1278">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1278">HTTP Method</span></span> | <span data-ttu-id="b70a4-1279">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1280">SİL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1281">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1282">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1282">Parameter Name</span></span> | <span data-ttu-id="b70a4-1283">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1284">Buildıd</span><span class="sxs-lookup"><span data-stu-id="b70a4-1284">buildId</span></span> |<span data-ttu-id="b70a4-1285">Merhaba yapı benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1285">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="b70a4-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1286">apiVersion</span></span> |<span data-ttu-id="b70a4-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1287">1.0</span></span> |

<span data-ttu-id="b70a4-1288">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="b70a4-1288">**Response:**</span></span>

<span data-ttu-id="b70a4-1289">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="b70a4-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1290">11.7.</span></span> <span data-ttu-id="b70a4-1291">Derleme iptal et</span><span class="sxs-lookup"><span data-stu-id="b70a4-1291">Cancel Build</span></span>
<span data-ttu-id="b70a4-1292">Durum oluşturulmasında, bir derlemede iptal eder.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="b70a4-1293">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1293">HTTP Method</span></span> | <span data-ttu-id="b70a4-1294">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1295">PUT</span><span class="sxs-lookup"><span data-stu-id="b70a4-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1296">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1297">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1297">Parameter Name</span></span> | <span data-ttu-id="b70a4-1298">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1299">Buildıd</span><span class="sxs-lookup"><span data-stu-id="b70a4-1299">buildId</span></span> |<span data-ttu-id="b70a4-1300">Merhaba yapı benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1300">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="b70a4-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1301">apiVersion</span></span> |<span data-ttu-id="b70a4-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1302">1.0</span></span> |

<span data-ttu-id="b70a4-1303">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="b70a4-1303">**Response:**</span></span>

<span data-ttu-id="b70a4-1304">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="b70a4-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1305">11.8.</span></span> <span data-ttu-id="b70a4-1306">Yapı parametreleri Al</span><span class="sxs-lookup"><span data-stu-id="b70a4-1306">Get Build Parameters</span></span>
<span data-ttu-id="b70a4-1307">Alır parametreleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="b70a4-1308">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1308">HTTP Method</span></span> | <span data-ttu-id="b70a4-1309">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1310">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1311">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1312">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1312">Parameter Name</span></span> | <span data-ttu-id="b70a4-1313">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1314">Buildıd</span><span class="sxs-lookup"><span data-stu-id="b70a4-1314">buildId</span></span> |<span data-ttu-id="b70a4-1315">Merhaba yapı benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1315">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="b70a4-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1316">apiVersion</span></span> |<span data-ttu-id="b70a4-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1317">1.0</span></span> |

<span data-ttu-id="b70a4-1318">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="b70a4-1318">**Response:**</span></span>

<span data-ttu-id="b70a4-1319">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1320">Bu API anahtar/değer öğe koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="b70a4-1321">Her öğe bir parametre ve değerini temsil eder:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="b70a4-1322">`feed/entry/content/properties/Key`-Parametre adı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="b70a4-1323">`feed/entry/content/properties/Value`-Parametre değeri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="b70a4-1324">Merhaba tabloda her anahtar temsil eden hello değeri gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1324">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="b70a4-1325">Anahtar</span><span class="sxs-lookup"><span data-stu-id="b70a4-1325">Key</span></span> | <span data-ttu-id="b70a4-1326">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b70a4-1326">Description</span></span> | <span data-ttu-id="b70a4-1327">Tür</span><span class="sxs-lookup"><span data-stu-id="b70a4-1327">Type</span></span> | <span data-ttu-id="b70a4-1328">Geçerli bir değer</span><span class="sxs-lookup"><span data-stu-id="b70a4-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b70a4-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="b70a4-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="b70a4-1330">Merhaba hello modeli gerçekleştirir yineleme sayısını hello tarafından yansıtılan zaman ve hello model doğruluğundan genel işlem.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1330">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="b70a4-1331">Merhaba daha yüksek hello sayı, hello daha iyi doğruluk alırsınız, ancak hello hesaplamak için daha uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1331">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="b70a4-1332">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1332">Integer</span></span> |<span data-ttu-id="b70a4-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="b70a4-1333">10-50</span></span> |
| <span data-ttu-id="b70a4-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="b70a4-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="b70a4-1335">Merhaba dimensions sayısı 'Özellikler' hello modeli toohello sayısı toofind verilerinizi içinde deneyecek ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1335">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="b70a4-1336">Boyutlar Hello sayısını artırmayı daha iyi hello sonuçlarını daha küçük kümeler halinde hassas ayar yapma izin verir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1336">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="b70a4-1337">Ancak, çok fazla boyutları bulmalarını bağıntıları öğeleri arasında hello modeli engeller.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1337">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="b70a4-1338">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1338">Integer</span></span> |<span data-ttu-id="b70a4-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="b70a4-1339">10-40</span></span> |
| <span data-ttu-id="b70a4-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="b70a4-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="b70a4-1341">Merhaba öğesi alt sınır hello Kondansatör için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1341">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="b70a4-1342">Yukarıdaki kullanım Kondansatör bakın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1342">See usage condenser above.</span></span> |<span data-ttu-id="b70a4-1343">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1343">Integer</span></span> |<span data-ttu-id="b70a4-1344">2 veya daha fazla (0 Kondansatör devre dışı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="b70a4-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="b70a4-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="b70a4-1346">Merhaba öğesi üst sınır hello Kondansatör için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1346">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="b70a4-1347">Yukarıdaki kullanım Kondansatör bakın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1347">See usage condenser above.</span></span> |<span data-ttu-id="b70a4-1348">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1348">Integer</span></span> |<span data-ttu-id="b70a4-1349">2 veya daha fazla (0 Kondansatör devre dışı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="b70a4-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="b70a4-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="b70a4-1351">Merhaba kullanıcı alt sınır hello Kondansatör için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1351">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="b70a4-1352">Yukarıdaki kullanım Kondansatör bakın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1352">See usage condenser above.</span></span> |<span data-ttu-id="b70a4-1353">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1353">Integer</span></span> |<span data-ttu-id="b70a4-1354">2 veya daha fazla (0 Kondansatör devre dışı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="b70a4-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="b70a4-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="b70a4-1356">Merhaba kullanıcı üst sınır hello Kondansatör için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1356">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="b70a4-1357">Yukarıdaki kullanım Kondansatör bakın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1357">See usage condenser above.</span></span> |<span data-ttu-id="b70a4-1358">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1358">Integer</span></span> |<span data-ttu-id="b70a4-1359">2 veya daha fazla (0 Kondansatör devre dışı)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="b70a4-1360">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b70a4-1360">Description</span></span> |<span data-ttu-id="b70a4-1361">Açıklama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1361">Build description.</span></span> |<span data-ttu-id="b70a4-1362">Dize</span><span class="sxs-lookup"><span data-stu-id="b70a4-1362">String</span></span> |<span data-ttu-id="b70a4-1363">Herhangi bir metin en çok 512 karakter</span><span class="sxs-lookup"><span data-stu-id="b70a4-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="b70a4-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="b70a4-1364">EnableModelingInsights</span></span> |<span data-ttu-id="b70a4-1365">Merhaba öneri model üzerinde toocompute ölçümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1365">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="b70a4-1366">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b70a4-1366">Boolean</span></span> |<span data-ttu-id="b70a4-1367">True/False</span><span class="sxs-lookup"><span data-stu-id="b70a4-1367">True/False</span></span> |
| <span data-ttu-id="b70a4-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="b70a4-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="b70a4-1369">Özellikler sipariş tooenhance hello öneri modelinde kullandıysanız gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1369">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="b70a4-1370">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b70a4-1370">Boolean</span></span> |<span data-ttu-id="b70a4-1371">True/False</span><span class="sxs-lookup"><span data-stu-id="b70a4-1371">True/False</span></span> |
| <span data-ttu-id="b70a4-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="b70a4-1372">ModelingFeatureList</span></span> |<span data-ttu-id="b70a4-1373">Sipariş tooenhance hello öneri de hello öneri derlemede kullanılan özellik adları toobe virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1373">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="b70a4-1374">Dize</span><span class="sxs-lookup"><span data-stu-id="b70a4-1374">String</span></span> |<span data-ttu-id="b70a4-1375">Özellik adlarını, too512 karakter</span><span class="sxs-lookup"><span data-stu-id="b70a4-1375">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="b70a4-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="b70a4-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="b70a4-1377">Hello öneri de soğuk öğeleri özelliği benzerlik anında olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1377">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="b70a4-1378">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b70a4-1378">Boolean</span></span> |<span data-ttu-id="b70a4-1379">True/False</span><span class="sxs-lookup"><span data-stu-id="b70a4-1379">True/False</span></span> |
| <span data-ttu-id="b70a4-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="b70a4-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="b70a4-1381">Mantığı içinde kullanılabilir özellikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="b70a4-1382">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b70a4-1382">Boolean</span></span> |<span data-ttu-id="b70a4-1383">True/False</span><span class="sxs-lookup"><span data-stu-id="b70a4-1383">True/False</span></span> |
| <span data-ttu-id="b70a4-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="b70a4-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="b70a4-1385">Tümceler (örn. öneri açıklamaları) akıl için kullanılan özellik adları toobe virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1385">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="b70a4-1386">Dize</span><span class="sxs-lookup"><span data-stu-id="b70a4-1386">String</span></span> |<span data-ttu-id="b70a4-1387">Özellik adlarını, too512 karakter</span><span class="sxs-lookup"><span data-stu-id="b70a4-1387">Feature names, up too512 chars</span></span> |

<span data-ttu-id="b70a4-1388">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-1388">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a><span data-ttu-id="b70a4-1389">12. Öneri</span><span class="sxs-lookup"><span data-stu-id="b70a4-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="b70a4-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1390">12.1.</span></span> <span data-ttu-id="b70a4-1391">(İçin etkin yapı) öğesi öneriler alın</span><span class="sxs-lookup"><span data-stu-id="b70a4-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="b70a4-1392">"Öneri" Merhaba etkin yapı türü önerileri alın veya "Fbt" oluştururken Çekirdeği (giriş) öğelerinin bir listesini esas.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1392">Get recommendations of hello active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="b70a4-1393">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1393">HTTP Method</span></span> | <span data-ttu-id="b70a4-1394">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1395">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1396">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1397">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1397">Parameter Name</span></span> | <span data-ttu-id="b70a4-1398">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1399">modelId</span></span> |<span data-ttu-id="b70a4-1400">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1400">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-1401">öğe kimliklerinin</span><span class="sxs-lookup"><span data-stu-id="b70a4-1401">itemIds</span></span> |<span data-ttu-id="b70a4-1402">Merhaba öğeleri toorecommend için virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1402">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="b70a4-1403">Merhaba etkin yapı ise yalnızca bir öğe gönderebilirsiniz sonra FBT yazın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1403">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="b70a4-1404">En fazla uzunluk: 1024</span><span class="sxs-lookup"><span data-stu-id="b70a4-1404">Max length: 1024</span></span> |
| <span data-ttu-id="b70a4-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="b70a4-1405">numberOfResults</span></span> |<span data-ttu-id="b70a4-1406">Gerekli sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1406">Number of required results</span></span> <br> <span data-ttu-id="b70a4-1407">En fazla: 150</span><span class="sxs-lookup"><span data-stu-id="b70a4-1407">Max: 150</span></span> |
| <span data-ttu-id="b70a4-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="b70a4-1408">includeMetatadata</span></span> |<span data-ttu-id="b70a4-1409">Gelecekte kullanmak, her zaman yanlış</span><span class="sxs-lookup"><span data-stu-id="b70a4-1409">Future use, always false</span></span> |
| <span data-ttu-id="b70a4-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1410">apiVersion</span></span> |<span data-ttu-id="b70a4-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1411">1.0</span></span> |

<span data-ttu-id="b70a4-1412">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="b70a4-1412">**Response:**</span></span>

<span data-ttu-id="b70a4-1413">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1414">Merhaba yanıt önerilen öğe başına bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1414">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="b70a4-1415">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1415">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-1416">`Feed\entry\content\properties\Id`-Önerilen öğesi kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="b70a4-1417">`Feed\entry\content\properties\Name`-Hello öğesinin adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1417">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="b70a4-1418">`Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1418">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="b70a4-1419">`Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="b70a4-1420">Aşağıdaki örnek yanıt Hello 10 önerilen öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1420">hello example response below includes 10 recommended items.</span></span>

<span data-ttu-id="b70a4-1421">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-1421">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="b70a4-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1422">12.2.</span></span> <span data-ttu-id="b70a4-1423">(Biri, belirli bir yapı) öğesi öneriler alın</span><span class="sxs-lookup"><span data-stu-id="b70a4-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="b70a4-1424">Belli bir yapı türü "Öneri" veya "Fbt" öneriler alın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="b70a4-1425">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1425">HTTP Method</span></span> | <span data-ttu-id="b70a4-1426">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1427">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1428">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1429">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1429">Parameter Name</span></span> | <span data-ttu-id="b70a4-1430">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1431">modelId</span></span> |<span data-ttu-id="b70a4-1432">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1432">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-1433">öğe kimliklerinin</span><span class="sxs-lookup"><span data-stu-id="b70a4-1433">itemIds</span></span> |<span data-ttu-id="b70a4-1434">Merhaba öğeleri toorecommend için virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1434">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="b70a4-1435">Merhaba etkin yapı ise yalnızca bir öğe gönderebilirsiniz sonra FBT yazın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1435">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="b70a4-1436">En fazla uzunluk: 1024</span><span class="sxs-lookup"><span data-stu-id="b70a4-1436">Max length: 1024</span></span> |
| <span data-ttu-id="b70a4-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="b70a4-1437">numberOfResults</span></span> |<span data-ttu-id="b70a4-1438">Gerekli sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1438">Number of required results</span></span> <br> <span data-ttu-id="b70a4-1439">En fazla: 150</span><span class="sxs-lookup"><span data-stu-id="b70a4-1439">Max: 150</span></span> |
| <span data-ttu-id="b70a4-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="b70a4-1440">includeMetatadata</span></span> |<span data-ttu-id="b70a4-1441">Gelecekte kullanmak, her zaman yanlış</span><span class="sxs-lookup"><span data-stu-id="b70a4-1441">Future use, always false</span></span> |
| <span data-ttu-id="b70a4-1442">Buildıd</span><span class="sxs-lookup"><span data-stu-id="b70a4-1442">buildId</span></span> |<span data-ttu-id="b70a4-1443">Bu öneri istek kimliği toouse Hello derleme</span><span class="sxs-lookup"><span data-stu-id="b70a4-1443">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="b70a4-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1444">apiVersion</span></span> |<span data-ttu-id="b70a4-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1445">1.0</span></span> |

<span data-ttu-id="b70a4-1446">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="b70a4-1446">**Response:**</span></span>

<span data-ttu-id="b70a4-1447">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1448">Merhaba yanıt önerilen öğe başına bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1448">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="b70a4-1449">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1449">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-1450">`Feed\entry\content\properties\Id`-Önerilen öğesi kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="b70a4-1451">`Feed\entry\content\properties\Name`-Hello öğesinin adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1451">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="b70a4-1452">`Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1452">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="b70a4-1453">`Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="b70a4-1454">12,1 yanıt örnekte bkz:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="b70a4-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1455">12.3.</span></span> <span data-ttu-id="b70a4-1456">(İçin etkin yapı) FBT öneriler alın</span><span class="sxs-lookup"><span data-stu-id="b70a4-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="b70a4-1457">Bir çekirdek (giriş) öğesi "Fbt" temel türü hello etkin yapı öneriler alın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1457">Get recommendations of hello active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="b70a4-1458">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1458">HTTP Method</span></span> | <span data-ttu-id="b70a4-1459">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1460">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1461">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1462">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1462">Parameter Name</span></span> | <span data-ttu-id="b70a4-1463">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1464">modelId</span></span> |<span data-ttu-id="b70a4-1465">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1465">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-1466">öğe kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1466">itemId</span></span> |<span data-ttu-id="b70a4-1467">Öğe toorecommend için.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1467">Item toorecommend for.</span></span> <br><span data-ttu-id="b70a4-1468">En fazla uzunluk: 1024</span><span class="sxs-lookup"><span data-stu-id="b70a4-1468">Max length: 1024</span></span> |
| <span data-ttu-id="b70a4-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="b70a4-1469">numberOfResults</span></span> |<span data-ttu-id="b70a4-1470">Gerekli sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1470">Number of required results</span></span> <br><span data-ttu-id="b70a4-1471">En fazla: 150</span><span class="sxs-lookup"><span data-stu-id="b70a4-1471">Max: 150</span></span> |
| <span data-ttu-id="b70a4-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="b70a4-1472">minimalScore</span></span> |<span data-ttu-id="b70a4-1473">Sık kümesi hello dahil sipariş toobe içinde döndürülen en az puan sonuçları</span><span class="sxs-lookup"><span data-stu-id="b70a4-1473">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="b70a4-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="b70a4-1474">includeMetatadata</span></span> |<span data-ttu-id="b70a4-1475">Gelecekte kullanmak, her zaman yanlış</span><span class="sxs-lookup"><span data-stu-id="b70a4-1475">Future use, always false</span></span> |
| <span data-ttu-id="b70a4-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1476">apiVersion</span></span> |<span data-ttu-id="b70a4-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1477">1.0</span></span> |

<span data-ttu-id="b70a4-1478">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="b70a4-1478">**Response:**</span></span>

<span data-ttu-id="b70a4-1479">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1480">Merhaba yanıt önerilen öğesi kümesi (genellikle hello çekirdek/giriş öğesi ile birlikte satın öğeleri kümesi) her bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1480">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="b70a4-1481">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1481">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-1482">`Feed\entry\content\properties\Id1`-Önerilen öğesi kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="b70a4-1483">`Feed\entry\content\properties\Name1`-Hello öğesinin adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1483">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="b70a4-1484">`Feed\entry\content\properties\Id2`-2 önerilen öğesi kimliği (isteğe bağlı).</span><span class="sxs-lookup"><span data-stu-id="b70a4-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="b70a4-1485">`Feed\entry\content\properties\Name2`-Öğesinin adı hello 2 (isteğe bağlı).</span><span class="sxs-lookup"><span data-stu-id="b70a4-1485">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="b70a4-1486">`Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1486">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="b70a4-1487">`Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="b70a4-1488">Merhaba örnek yanıt aşağıdaki 3 önerilen öğesi ayarlar içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1488">hello example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="b70a4-1489">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-1489">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="b70a4-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1490">12.4.</span></span> <span data-ttu-id="b70a4-1491">(Biri, belirli bir yapı) FBT öneriler alın</span><span class="sxs-lookup"><span data-stu-id="b70a4-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="b70a4-1492">Belli bir yapı türü "Fbt" öneriler alın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="b70a4-1493">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1493">HTTP Method</span></span> | <span data-ttu-id="b70a4-1494">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1495">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1496">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1497">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1497">Parameter Name</span></span> | <span data-ttu-id="b70a4-1498">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1499">modelId</span></span> |<span data-ttu-id="b70a4-1500">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-1501">öğe kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1501">itemId</span></span> |<span data-ttu-id="b70a4-1502">Öğe toorecommend için.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1502">Item toorecommend for.</span></span> <br><span data-ttu-id="b70a4-1503">En fazla uzunluk: 1024</span><span class="sxs-lookup"><span data-stu-id="b70a4-1503">Max length: 1024</span></span> |
| <span data-ttu-id="b70a4-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="b70a4-1504">numberOfResults</span></span> |<span data-ttu-id="b70a4-1505">Gerekli sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1505">Number of required results</span></span> <br><span data-ttu-id="b70a4-1506">En fazla: 150</span><span class="sxs-lookup"><span data-stu-id="b70a4-1506">Max: 150</span></span> |
| <span data-ttu-id="b70a4-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="b70a4-1507">minimalScore</span></span> |<span data-ttu-id="b70a4-1508">Sık kümesi hello dahil sipariş toobe içinde döndürülen en az puan sonuçları</span><span class="sxs-lookup"><span data-stu-id="b70a4-1508">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="b70a4-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="b70a4-1509">includeMetatadata</span></span> |<span data-ttu-id="b70a4-1510">Gelecekte kullanmak, her zaman yanlış</span><span class="sxs-lookup"><span data-stu-id="b70a4-1510">Future use, always false</span></span> |
| <span data-ttu-id="b70a4-1511">Buildıd</span><span class="sxs-lookup"><span data-stu-id="b70a4-1511">buildId</span></span> |<span data-ttu-id="b70a4-1512">Bu öneri istek kimliği toouse Hello derleme</span><span class="sxs-lookup"><span data-stu-id="b70a4-1512">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="b70a4-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1513">apiVersion</span></span> |<span data-ttu-id="b70a4-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1514">1.0</span></span> |

<span data-ttu-id="b70a4-1515">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="b70a4-1515">**Response:**</span></span>

<span data-ttu-id="b70a4-1516">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1517">Merhaba yanıt önerilen öğesi kümesi (genellikle hello çekirdek/giriş öğesi ile birlikte satın öğeleri kümesi) her bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1517">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="b70a4-1518">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1518">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-1519">`Feed\entry\content\properties\Id1`-Önerilen öğesi kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="b70a4-1520">`Feed\entry\content\properties\Name1`-Hello öğesinin adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1520">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="b70a4-1521">`Feed\entry\content\properties\Id2`-2 önerilen öğesi kimliği (isteğe bağlı).</span><span class="sxs-lookup"><span data-stu-id="b70a4-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="b70a4-1522">`Feed\entry\content\properties\Name2`-Öğesinin adı hello 2 (isteğe bağlı).</span><span class="sxs-lookup"><span data-stu-id="b70a4-1522">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="b70a4-1523">`Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1523">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="b70a4-1524">`Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="b70a4-1525">12.3 yanıt örnekte bkz:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="b70a4-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1526">12.5.</span></span> <span data-ttu-id="b70a4-1527">Kullanıcı öneriler alın (etkin derleme için)</span><span class="sxs-lookup"><span data-stu-id="b70a4-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="b70a4-1528">Tür "Öneri" etkin yapı işaretlenmiş bir yapı kullanıcı öneriler alın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="b70a4-1529">Merhaba API hello kullanıcı toohello kullanım geçmişine göre tahmin edilen madde listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1529">hello API will return a list of predicted item according toohello usage history of hello user.</span></span>

<span data-ttu-id="b70a4-1530">Notlar:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1530">Notes:</span></span> 

1. <span data-ttu-id="b70a4-1531">FBT derleme için hiçbir kullanıcı öneri yok.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="b70a4-1532">Bu yöntem bir hata döndürür olacak FBT Hello etkin yapı ise.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1532">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="b70a4-1533">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1533">HTTP Method</span></span> | <span data-ttu-id="b70a4-1534">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1535">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1536">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1537">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1537">Parameter Name</span></span> | <span data-ttu-id="b70a4-1538">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1539">modelId</span></span> |<span data-ttu-id="b70a4-1540">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1540">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-1541">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1541">userId</span></span> |<span data-ttu-id="b70a4-1542">Merhaba kullanıcının benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1542">Unique identifier of hello user</span></span> |
| <span data-ttu-id="b70a4-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="b70a4-1543">numberOfResults</span></span> |<span data-ttu-id="b70a4-1544">Gerekli sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1544">Number of required results</span></span> |
| <span data-ttu-id="b70a4-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="b70a4-1545">includeMetatadata</span></span> |<span data-ttu-id="b70a4-1546">Gelecekte kullanmak, her zaman yanlış</span><span class="sxs-lookup"><span data-stu-id="b70a4-1546">Future use, always false</span></span> |
| <span data-ttu-id="b70a4-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1547">apiVersion</span></span> |<span data-ttu-id="b70a4-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1548">1.0</span></span> |

<span data-ttu-id="b70a4-1549">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="b70a4-1549">**Response:**</span></span>

<span data-ttu-id="b70a4-1550">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1551">Merhaba yanıt önerilen öğe başına bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1551">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="b70a4-1552">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1552">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-1553">`Feed\entry\content\properties\Id`-Önerilen öğesi kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="b70a4-1554">`Feed\entry\content\properties\Name`-Hello öğesinin adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1554">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="b70a4-1555">`Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1555">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="b70a4-1556">`Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="b70a4-1557">12,1 yanıt örnekte bkz:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="b70a4-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1558">12.6.</span></span> <span data-ttu-id="b70a4-1559">Kullanıcı öneriler öğesi listesiyle (için etkin yapı) alın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="b70a4-1560">Tür "Öneri" ek öğeler listesi ile etkin yapı olarak işaretlenmiş bir yapı kullanıcı öneriler alın</span><span class="sxs-lookup"><span data-stu-id="b70a4-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="b70a4-1561">Merhaba API hello kullanıcı ve hello ek sağlanan öğeleri toohello kullanım geçmişine göre tahmin edilen madde listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1561">hello API will return a list of predicted item according toohello usage history of hello user and hello additional provided items.</span></span>

<span data-ttu-id="b70a4-1562">Notlar:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1562">Notes:</span></span> 

1. <span data-ttu-id="b70a4-1563">FBT derleme için hiçbir kullanıcı öneri yok.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="b70a4-1564">Bu yöntem bir hata döndürür olacak FBT Hello etkin yapı ise.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1564">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="b70a4-1565">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1565">HTTP Method</span></span> | <span data-ttu-id="b70a4-1566">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1567">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1568">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1569">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1569">Parameter Name</span></span> | <span data-ttu-id="b70a4-1570">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1571">modelId</span></span> |<span data-ttu-id="b70a4-1572">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1572">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-1573">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1573">userId</span></span> |<span data-ttu-id="b70a4-1574">Merhaba kullanıcının benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1574">Unique identifier of hello user</span></span> |
| <span data-ttu-id="b70a4-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="b70a4-1575">itemsIds</span></span> |<span data-ttu-id="b70a4-1576">Merhaba öğeleri toorecommend için virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1576">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="b70a4-1577">En fazla uzunluk: 1024</span><span class="sxs-lookup"><span data-stu-id="b70a4-1577">Max length: 1024</span></span> |
| <span data-ttu-id="b70a4-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="b70a4-1578">numberOfResults</span></span> |<span data-ttu-id="b70a4-1579">Gerekli sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1579">Number of required results</span></span> |
| <span data-ttu-id="b70a4-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="b70a4-1580">includeMetatadata</span></span> |<span data-ttu-id="b70a4-1581">Gelecekte kullanmak, her zaman yanlış</span><span class="sxs-lookup"><span data-stu-id="b70a4-1581">Future use, always false</span></span> |
| <span data-ttu-id="b70a4-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1582">apiVersion</span></span> |<span data-ttu-id="b70a4-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1583">1.0</span></span> |

<span data-ttu-id="b70a4-1584">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="b70a4-1584">**Response:**</span></span>

<span data-ttu-id="b70a4-1585">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1586">Merhaba yanıt önerilen öğe başına bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1586">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="b70a4-1587">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1587">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-1588">`Feed\entry\content\properties\Id`-Önerilen öğesi kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="b70a4-1589">`Feed\entry\content\properties\Name`-Hello öğesinin adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1589">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="b70a4-1590">`Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1590">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="b70a4-1591">`Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="b70a4-1592">12,1 yanıt örnekte bkz:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="b70a4-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1593">12.7.</span></span> <span data-ttu-id="b70a4-1594">(Biri, belirli bir yapı) kullanıcı öneriler alın</span><span class="sxs-lookup"><span data-stu-id="b70a4-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="b70a4-1595">Belli bir yapı türü "Öneri" kullanıcı öneriler alın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="b70a4-1596">Merhaba API (Merhaba belirli derlemede kullanılan) hello kullanıcı toohello kullanım geçmişine göre tahmin edilen madde listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1596">hello API will return a list of predicted item according toohello usage history of hello user (used in hello specific build).</span></span>

<span data-ttu-id="b70a4-1597">Not: FBT derleme için hiçbir kullanıcı öneri yok.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="b70a4-1598">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1598">HTTP Method</span></span> | <span data-ttu-id="b70a4-1599">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1600">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1601">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1602">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1602">Parameter Name</span></span> | <span data-ttu-id="b70a4-1603">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1604">modelId</span></span> |<span data-ttu-id="b70a4-1605">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1605">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-1606">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1606">userId</span></span> |<span data-ttu-id="b70a4-1607">Merhaba kullanıcının benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1607">Unique identifier of hello user</span></span> |
| <span data-ttu-id="b70a4-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="b70a4-1608">numberOfResults</span></span> |<span data-ttu-id="b70a4-1609">Gerekli sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1609">Number of required results</span></span> |
| <span data-ttu-id="b70a4-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="b70a4-1610">includeMetatadata</span></span> |<span data-ttu-id="b70a4-1611">Gelecekte kullanmak, her zaman yanlış</span><span class="sxs-lookup"><span data-stu-id="b70a4-1611">Future use, always false</span></span> |
| <span data-ttu-id="b70a4-1612">Buildıd</span><span class="sxs-lookup"><span data-stu-id="b70a4-1612">buildId</span></span> |<span data-ttu-id="b70a4-1613">Bu öneri istek kimliği toouse Hello derleme</span><span class="sxs-lookup"><span data-stu-id="b70a4-1613">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="b70a4-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1614">apiVersion</span></span> |<span data-ttu-id="b70a4-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1615">1.0</span></span> |

<span data-ttu-id="b70a4-1616">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="b70a4-1616">**Response:**</span></span>

<span data-ttu-id="b70a4-1617">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1618">Merhaba yanıt önerilen öğe başına bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1618">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="b70a4-1619">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1619">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-1620">`Feed\entry\content\properties\Id`-Önerilen öğesi kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="b70a4-1621">`Feed\entry\content\properties\Name`-Hello öğesinin adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1621">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="b70a4-1622">`Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1622">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="b70a4-1623">`Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="b70a4-1624">12,1 yanıt örnekte bkz:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="b70a4-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1625">12.8.</span></span> <span data-ttu-id="b70a4-1626">Öğe listesi (belirli bir yapı) ile kullanıcı öneriler alın</span><span class="sxs-lookup"><span data-stu-id="b70a4-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="b70a4-1627">Belirli bir yapı türü "Öneri" kullanıcı öneriler ve ek öğeler hello listesini alın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1627">Get user recommendations of a specific build of type "Recommendation" and hello list of additional items.</span></span>

<span data-ttu-id="b70a4-1628">Merhaba API hello kullanıcı toohello kullanım geçmişini ve hello ek öğeler listesi göre tahmin edilen madde listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1628">hello API will return a list of predicted item according toohello usage history of hello user and hello additional list of items.</span></span>

<span data-ttu-id="b70a4-1629">Not: Työnetici, FBT yapı için hiçbir kullanıcı önerilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="b70a4-1630">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1630">HTTP Method</span></span> | <span data-ttu-id="b70a4-1631">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1632">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1633">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1634">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1634">Parameter Name</span></span> | <span data-ttu-id="b70a4-1635">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1636">modelId</span></span> |<span data-ttu-id="b70a4-1637">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1637">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-1638">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1638">userId</span></span> |<span data-ttu-id="b70a4-1639">Merhaba kullanıcının benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1639">Unique identifier of hello user</span></span> |
| <span data-ttu-id="b70a4-1640">öğe kimliklerinin</span><span class="sxs-lookup"><span data-stu-id="b70a4-1640">itemIds</span></span> |<span data-ttu-id="b70a4-1641">Merhaba öğeleri toorecommend için virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1641">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="b70a4-1642">En fazla uzunluk: 1024</span><span class="sxs-lookup"><span data-stu-id="b70a4-1642">Max length: 1024</span></span> |
| <span data-ttu-id="b70a4-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="b70a4-1643">numberOfResults</span></span> |<span data-ttu-id="b70a4-1644">Gerekli sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1644">Number of required results</span></span> |
| <span data-ttu-id="b70a4-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="b70a4-1645">includeMetatadata</span></span> |<span data-ttu-id="b70a4-1646">Gelecekte kullanmak, her zaman yanlış</span><span class="sxs-lookup"><span data-stu-id="b70a4-1646">Future use, always false</span></span> |
| <span data-ttu-id="b70a4-1647">Buildıd</span><span class="sxs-lookup"><span data-stu-id="b70a4-1647">buildId</span></span> |<span data-ttu-id="b70a4-1648">Bu öneri istek kimliği toouse Hello derleme</span><span class="sxs-lookup"><span data-stu-id="b70a4-1648">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="b70a4-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1649">apiVersion</span></span> |<span data-ttu-id="b70a4-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1650">1.0</span></span> |

<span data-ttu-id="b70a4-1651">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="b70a4-1651">**Response:**</span></span>

<span data-ttu-id="b70a4-1652">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1653">Merhaba yanıt önerilen öğe başına bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1653">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="b70a4-1654">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1654">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-1655">`Feed\entry\content\properties\Id`-Önerilen öğesi kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="b70a4-1656">`Feed\entry\content\properties\Name`-Hello öğesinin adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1656">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="b70a4-1657">`Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1657">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="b70a4-1658">`Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="b70a4-1659">12,1 yanıt örnekte bkz:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="b70a4-1660">13. Kullanıcı Kullanım Geçmişi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1660">13. User Usage History</span></span>
<span data-ttu-id="b70a4-1661">Bir öneri model oluşturulmuş bir kez hello sistem hello derleme için kullanılan tooretrieve hello kullanıcı geçmişi (öğeleri ilişkili tooa belirli kullanıcı) izin verir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1661">Once a recommendation model was built hello system will allow tooretrieve hello user history (items associated tooa specific user) used for hello build.</span></span>
<span data-ttu-id="b70a4-1662">Bu API izin tooretrieve hello kullanıcı geçmişi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1662">This API allow tooretrieve hello user history</span></span>

<span data-ttu-id="b70a4-1663">Not: hello kullanıcı geçmişi yalnızca öneri derlemeler için şu anda büyük/küçük harf yok.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1663">Note: hello user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="b70a4-1664">13,1 kullanıcı geçmişi alma</span><span class="sxs-lookup"><span data-stu-id="b70a4-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="b70a4-1665">Alma hello hello etkin kullanılan öğe listesi oluşturmak veya kullanıcı kimliği verilen hello için belirtilen hello oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1665">Retrieve hello list of item used in hello active build or in hello specified build for hello given user id.</span></span>

| <span data-ttu-id="b70a4-1666">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1666">HTTP Method</span></span> | <span data-ttu-id="b70a4-1667">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1668">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1668">GET</span></span> |<span data-ttu-id="b70a4-1669">Merhaba kullanıcı geçmişi hello etkin yapı için alın.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1669">Get hello user history for hello active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="b70a4-1670">Yapı verilen Merhaba Hello kullanıcı geçmişini alma`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="b70a4-1670">Get hello user history for hello given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="b70a4-1671">Örnek:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="b70a4-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="b70a4-1672">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1672">Parameter Name</span></span> | <span data-ttu-id="b70a4-1673">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1674">modelId</span></span> |<span data-ttu-id="b70a4-1675">Merhaba hello modelinin benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1675">hello unique identifier of hello model.</span></span> |
| <span data-ttu-id="b70a4-1676">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1676">userId</span></span> |<span data-ttu-id="b70a4-1677">Merhaba hello kullanıcının benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1677">hello unique identifier of hello user.</span></span> |
| <span data-ttu-id="b70a4-1678">Buildıd</span><span class="sxs-lookup"><span data-stu-id="b70a4-1678">buildId</span></span> |<span data-ttu-id="b70a4-1679">İsteğe bağlı bir parametre hangi yapıdan hello kullanıcı geçmişi fetch olmalıdır tooindicate izin ver</span><span class="sxs-lookup"><span data-stu-id="b70a4-1679">optional parameter, allow tooindicate from which build hello user history should be fetch</span></span> |
| <span data-ttu-id="b70a4-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1680">apiVersion</span></span> |<span data-ttu-id="b70a4-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1681">1.0</span></span> |

<span data-ttu-id="b70a4-1682">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="b70a4-1682">**Response:**</span></span>

<span data-ttu-id="b70a4-1683">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1684">Merhaba yanıt önerilen öğe başına bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1684">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="b70a4-1685">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1685">Each entry has hello following data:</span></span>

* <span data-ttu-id="b70a4-1686">`Feed\entry\content\properties\Id`-Önerilen öğesi kimliği</span><span class="sxs-lookup"><span data-stu-id="b70a4-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="b70a4-1687">`Feed\entry\content\properties\Name`-Hello öğesinin adı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1687">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="b70a4-1688">`Feed\entry\content\properties\Rating`-YOK.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="b70a4-1689">`Feed\entry\content\properties\Reasoning`-YOK.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="b70a4-1690">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-1690">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a><span data-ttu-id="b70a4-1691">14. Bildirimler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1691">14. Notifications</span></span>
<span data-ttu-id="b70a4-1692">Hello sistemde kalıcı hata oluştuğunda azure Machine Learning önerileri bildirimleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in hello system.</span></span> <span data-ttu-id="b70a4-1693">3 bildirim türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="b70a4-1694">Derleme hatası: Bu bildirim için her derleme hatası tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="b70a4-1695">Veri alma hatası: Bu bildirim işleme 100'den fazla hataları hello son 5 dakika içinde kullanım olaylarının modeli başına hello işleme sahip olduğumuz geldiğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of usage events per model.</span></span>
3. <span data-ttu-id="b70a4-1696">Biz 100'den fazla hataları hello son 5 dakika içinde bir öneri istekleri modeli başına hello işlenmesini varsa öneri tüketim hatası - Bu bildirim tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="b70a4-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1697">14.1.</span></span> <span data-ttu-id="b70a4-1698">Bildirimleri alma</span><span class="sxs-lookup"><span data-stu-id="b70a4-1698">Get Notifications</span></span>
<span data-ttu-id="b70a4-1699">Tek bir model veya tüm modelleri için tüm hello bildirimleri alır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1699">Retrieves all hello notifications for all models or for a single model.</span></span>

| <span data-ttu-id="b70a4-1700">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1700">HTTP Method</span></span> | <span data-ttu-id="b70a4-1701">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1702">AL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1703">Tüm modelleri için tüm bildirimleri alma:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1704">Örneğin, belirli bir model için bildirimleri almak için:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="b70a4-1705">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1705">Parameter Name</span></span> | <span data-ttu-id="b70a4-1706">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1707">modelId</span></span> |<span data-ttu-id="b70a4-1708">İsteğe bağlı parametre.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1708">Optional parameter.</span></span> <span data-ttu-id="b70a4-1709">Atlanırsa, tüm modelleri için tüm bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="b70a4-1710">Geçerli değer: hello modelinin benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1710">Valid value: unique identifier of hello model.</span></span> |
| <span data-ttu-id="b70a4-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1711">apiVersion</span></span> |<span data-ttu-id="b70a4-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-1713">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1713">Request Body</span></span> |<span data-ttu-id="b70a4-1714">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-1714">NONE</span></span> |

<span data-ttu-id="b70a4-1715">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="b70a4-1715">**Response:**</span></span>

<span data-ttu-id="b70a4-1716">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="b70a4-1717">OData XML</span><span class="sxs-lookup"><span data-stu-id="b70a4-1717">OData XML</span></span>

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a><span data-ttu-id="b70a4-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1718">14.2.</span></span> <span data-ttu-id="b70a4-1719">Model uyarılarını silme</span><span class="sxs-lookup"><span data-stu-id="b70a4-1719">Delete Model Notifications</span></span>
<span data-ttu-id="b70a4-1720">Bir model için tüm okuma bildirimleri siler.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="b70a4-1721">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1721">HTTP Method</span></span> | <span data-ttu-id="b70a4-1722">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1723">SİL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="b70a4-1724">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1725">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1725">Parameter Name</span></span> | <span data-ttu-id="b70a4-1726">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="b70a4-1727">modelId</span></span> |<span data-ttu-id="b70a4-1728">Merhaba modeli benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1728">Unique identifier of hello model</span></span> |
| <span data-ttu-id="b70a4-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1729">apiVersion</span></span> |<span data-ttu-id="b70a4-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-1731">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1731">Request Body</span></span> |<span data-ttu-id="b70a4-1732">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-1732">NONE</span></span> |

<span data-ttu-id="b70a4-1733">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1733">**Response**:</span></span>

<span data-ttu-id="b70a4-1734">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="b70a4-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1735">14.3.</span></span> <span data-ttu-id="b70a4-1736">Kullanıcı bildirimleri Sil</span><span class="sxs-lookup"><span data-stu-id="b70a4-1736">Delete User Notifications</span></span>
<span data-ttu-id="b70a4-1737">Tüm modelleri ilişkin tüm bildirimler siler.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="b70a4-1738">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1738">HTTP Method</span></span> | <span data-ttu-id="b70a4-1739">URI</span><span class="sxs-lookup"><span data-stu-id="b70a4-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1740">SİL</span><span class="sxs-lookup"><span data-stu-id="b70a4-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="b70a4-1741">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="b70a4-1741">Parameter Name</span></span> | <span data-ttu-id="b70a4-1742">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="b70a4-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b70a4-1743">apiVersion</span></span> |<span data-ttu-id="b70a4-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="b70a4-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="b70a4-1745">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="b70a4-1745">Request Body</span></span> |<span data-ttu-id="b70a4-1746">YOK</span><span class="sxs-lookup"><span data-stu-id="b70a4-1746">NONE</span></span> |

<span data-ttu-id="b70a4-1747">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="b70a4-1747">**Response**:</span></span>

<span data-ttu-id="b70a4-1748">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="b70a4-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="b70a4-1749">15. Yasal Bilgiler</span><span class="sxs-lookup"><span data-stu-id="b70a4-1749">15. Legal</span></span>
<span data-ttu-id="b70a4-1750">Bu belgede sağlanan "olarak-olan".</span><span class="sxs-lookup"><span data-stu-id="b70a4-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="b70a4-1751">URL ve diğer Internet Web sitesi başvuruları dahil olmak üzere bu belgede belirtilen bilgiler ve görüntüler bildirim yapılmadan değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="b70a4-1752">Burada açıklanan bazı örnekler yalnızca çizim için sağlanmıştır ve kurgusaldır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="b70a4-1753">Gerçek bir ilişki veya bağlantı amaçlanmamıştır veya çıkarılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="b70a4-1754">Bu belge, herhangi bir yasal hak ile herhangi bir Microsoft ürünü üzerinde tooany fikri mülkiyet sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1754">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="b70a4-1755">Kopyalayabilir ve bu belgeyi şirket içinde kullanmak başvuru amaçlıdır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="b70a4-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="b70a4-1757">Tüm hakları saklıdır.</span><span class="sxs-lookup"><span data-stu-id="b70a4-1757">All rights reserved.</span></span>

