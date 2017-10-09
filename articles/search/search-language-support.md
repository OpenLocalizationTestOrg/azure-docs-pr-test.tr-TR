---
title: "aaaAzure arama çoklu dil | Microsoft Docs"
description: "Azure arama, dil Çözümleyicileri Lucene ve doğal dil işleme teknolojisi Microsoft'tan gelen yararlanarak 56 dilleri destekler."
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="70cf7-103">Azure Search'te birden çok dilde belgeler için dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="70cf7-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="70cf7-104">Portal</span><span class="sxs-lookup"><span data-stu-id="70cf7-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="70cf7-105">REST</span><span class="sxs-lookup"><span data-stu-id="70cf7-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="70cf7-106">.NET</span><span class="sxs-lookup"><span data-stu-id="70cf7-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="70cf7-107">Dil Çözümleyicileri unleashing hello gücünü hello dizin tanımı aranabilir alanında bulunan bir özellik ayarı olarak kadar kolaydır.</span><span class="sxs-lookup"><span data-stu-id="70cf7-107">Unleashing hello power of language analyzers is as easy as setting one property on a searchable field in hello index definition.</span></span> <span data-ttu-id="70cf7-108">Şimdi bu adımı hello portalında yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70cf7-108">Now you can do this step in hello portal.</span></span>

<span data-ttu-id="70cf7-109">Azure Portal dikey penceresi ekran görüntüleri hello Azure arama için bir dizin şemasını kullanıcılar toodefine izin aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="70cf7-109">Below are screenshots of hello Azure Portal blades for Azure Search that allow users toodefine an index schema.</span></span> <span data-ttu-id="70cf7-110">Bu dikey pencereden kullanıcılar hello alanların tümünü oluşturabilir ve bunların her biri için hello Çözümleyicisi özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="70cf7-110">From this blade, users can create all of hello fields and set hello analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70cf7-111">Yalnızca bir dil Çözümleyicisi alan tanımı sırasında gibi hello yeni bir dizin oluşturma plan veya yeni bir alan tooan var olan dizini eklerken ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70cf7-111">You can only set a language analyzer during field definition, as in when creating a new index from hello ground up, or when adding a new field tooan existing index.</span></span> <span data-ttu-id="70cf7-112">Hello alan oluşturulurken hello Çözümleyicisi de dahil olmak üzere tüm özniteliklerin tam olarak belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="70cf7-112">Make sure you fully specify all attributes, including hello analyzer, while creating hello field.</span></span> <span data-ttu-id="70cf7-113">Merhaba özniteliklerin mümkün tooedit olması veya değişiklikleri kaydettikten sonra hello Çözümleyicisi türünü değiştirin olmaz.</span><span class="sxs-lookup"><span data-stu-id="70cf7-113">You won't be able tooedit hello attributes or change hello analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="70cf7-114">Yeni bir alan tanımı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="70cf7-114">Define a new field definition</span></span>
1. <span data-ttu-id="70cf7-115">İçinde toohello oturum [Azure portal](https://portal.azure.com) ve açık hello hizmeti dikey search hizmetinizin.</span><span class="sxs-lookup"><span data-stu-id="70cf7-115">Sign in toohello [Azure portal](https://portal.azure.com) and open hello service blade of your search service.</span></span>
2. <span data-ttu-id="70cf7-116">' I tıklatın **Ekle dizin** hello komut yeni bir dizin hello hizmet Pano toostart hello üstünde çubuk veya varolan bir dizin tooset bir Çözümleyicisi ekleyeceğiniz yeni alanlar açın tooan varolan bir dizini.</span><span class="sxs-lookup"><span data-stu-id="70cf7-116">Click **Add index** in hello command bar at hello top of hello service dashboard toostart a new index, or open an existing index tooset an analyzer on new fields you're adding tooan existing index.</span></span>
3. <span data-ttu-id="70cf7-117">Merhaba alanları dikey penceresi görünür hello dizin hello şemasını tanımlamak için seçenekler sunan hello Çözümleyicisi sekmesinde de dahil olmak üzere bir dil Çözümleyicisi seçmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="70cf7-117">hello Fields blade appears, giving you options for defining hello schema of hello index, including hello Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="70cf7-118">Alanlarda alan tanımı sağlayan bir adı hello veri türü seçme ve öznitelikleri toomark hello alan tam metin aranabilir, arama sonuçlarında, model Gezinti yapılarda kullanılabilir alınabilir sıralanabilir vb. ayarı başlatın.</span><span class="sxs-lookup"><span data-stu-id="70cf7-118">In Fields, start a field definition by providing a name, choosing hello data type, and setting attributes toomark hello field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="70cf7-119">Toohello sonraki alan taşımadan önce hello açmak **Çözümleyicisi** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="70cf7-119">Before moving on toohello next field, open hello **Analyzer** tab.</span></span>

<span data-ttu-id="70cf7-120">![][1]
*tooselect bir Çözümleyicisi hello alanları dikey penceresinde hello Çözümleyicisi sekmesini tıklatın*</span><span class="sxs-lookup"><span data-stu-id="70cf7-120">![][1]
*tooselect an analyzer, click hello Analyzer tab on hello Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="70cf7-121">Bir analyzer'ı seçin</span><span class="sxs-lookup"><span data-stu-id="70cf7-121">Choose an analyzer</span></span>
1. <span data-ttu-id="70cf7-122">Tanımladığınız toofind hello alan kaydırın.</span><span class="sxs-lookup"><span data-stu-id="70cf7-122">Scroll toofind hello field you are defining.</span></span>
2. <span data-ttu-id="70cf7-123">Merhaba alan aranabilir olarak işaretlenmiş henüz yoksa, hello onay kutusu şimdi toomark tıklatın olarak **aranabilir**.</span><span class="sxs-lookup"><span data-stu-id="70cf7-123">If you haven't marked hello field as searchable, click hello checkbox now toomark it as **Searchable**.</span></span>
3. <span data-ttu-id="70cf7-124">Merhaba Çözümleyicisi alanı toodisplay hello listesi kullanılabilir çözümleyiciler tıklatın.</span><span class="sxs-lookup"><span data-stu-id="70cf7-124">Click hello Analyzer area toodisplay hello list of available analyzers.</span></span>
4. <span data-ttu-id="70cf7-125">Merhaba Çözümleyicisi seçin toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="70cf7-125">Choose hello analyzer you want toouse.</span></span>

<span data-ttu-id="70cf7-126">![][2]
*Her bir alan için desteklenen hello çözümleyiciler birini seçin*</span><span class="sxs-lookup"><span data-stu-id="70cf7-126">![][2]
*Select one of hello supported analyzers for each field*</span></span>

<span data-ttu-id="70cf7-127">Varsayılan olarak, tüm aranabilir alanları hello kullan [standart Lucene Çözümleyicisi](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) dil belirsiz olduğu.</span><span class="sxs-lookup"><span data-stu-id="70cf7-127">By default, all searchable fields use hello [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="70cf7-128">tooview hello tam listesini desteklenen çözümleyiciler bkz [dil desteği Azure Search'te](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="70cf7-128">tooview hello full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="70cf7-129">Merhaba dil Çözümleyicisi için bir alan seçtikten sonra bu alan için dizin oluşturma ve arama her istek ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="70cf7-129">Once hello language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="70cf7-130">Bir sorgu farklı çözümleyicilerini kullanarak birden çok alan karşı verildiğinde hello sorgu bağımsız olarak her bir alan için doğru çözümleyiciler hello tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="70cf7-130">When a query is issued against multiple fields using different analyzers, hello query will be processed independently by hello right analyzers for each field.</span></span>

<span data-ttu-id="70cf7-131">Birçok web ve mobil uygulamalar kullanıcılar farklı diller kullanılarak Merhaba Dünya geçici hizmet.</span><span class="sxs-lookup"><span data-stu-id="70cf7-131">Many web and mobile applications serve users around hello globe using different languages.</span></span> <span data-ttu-id="70cf7-132">Bu senaryo için dizin gibi desteklenen her dil için bir alan oluşturarak olası toodefine olur.</span><span class="sxs-lookup"><span data-stu-id="70cf7-132">It’s possible toodefine an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="70cf7-133">![][3]
*Desteklenen her dil için bir açıklama alanı ile dizin tanımı*</span><span class="sxs-lookup"><span data-stu-id="70cf7-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="70cf7-134">Bir sorgu verme hello Aracısı Hello dilinin bilinen, arama isteği hello kullanarak kapsamlı tooa belirli alan olabilir **searchFields** sorgu parametresi.</span><span class="sxs-lookup"><span data-stu-id="70cf7-134">If hello language of hello agent issuing a query is known, a search request can be scoped tooa specific field using hello **searchFields** query parameter.</span></span> <span data-ttu-id="70cf7-135">Merhaba aşağıdaki sorguyu yalnızca Lehçe hello açıklamasında karşı verilir:</span><span class="sxs-lookup"><span data-stu-id="70cf7-135">hello following query will be issued only against hello description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="70cf7-136">Dizininizi hello portalından sorgulayabilirsiniz kullanarak **arama Gezgini** bir sorgu benzer toohello yukarıda gösterilenle toopaste.</span><span class="sxs-lookup"><span data-stu-id="70cf7-136">You can query your index from hello portal, using **Search explorer** toopaste in a query similar toohello one shown above.</span></span> <span data-ttu-id="70cf7-137">Arama Gezgini hello hizmeti dikey hello komut çubuğunda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="70cf7-137">Search explorer is available from hello command bar in hello service blade.</span></span> <span data-ttu-id="70cf7-138">Bkz: [hello portalındaki Azure Search dizininizi sorgulama](search-explorer.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="70cf7-138">See [Query your Azure Search index in hello portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="70cf7-139">Bazen hello bir sorgu verme hello Aracısı'nın dil bilinmiyor, hangi servis talebi hello sorgu karşı tüm alanlar aynı anda verilebilir.</span><span class="sxs-lookup"><span data-stu-id="70cf7-139">Sometimes hello language of hello agent issuing a query is not known, in which case hello query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="70cf7-140">Gerekirse, belirli bir dilde sonuçları için tercih kullanılarak tanımlanabilir [profilleri Puanlama](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="70cf7-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="70cf7-141">Merhaba aşağıdaki örnekte, Lehçe ve Fransızca yüksek göreli toomatches İngilizce hello açıklamasında bulunan eşleşmeler skoru:</span><span class="sxs-lookup"><span data-stu-id="70cf7-141">In hello example below, matches found in hello description in English will be scored higher relative toomatches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="70cf7-142">.NET Geliştirici değilseniz, dil Çözümleyicileri hello kullanarak yapılandırabileceğinize dikkat edin [Azure Search .NET SDK'sı](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="70cf7-142">If you're a .NET developer, note that you can configure language analyzers using hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="70cf7-143">Merhaba en son sürüm hello Microsoft dil Çözümleyicileri de destekler.</span><span class="sxs-lookup"><span data-stu-id="70cf7-143">hello latest release includes support for hello Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
