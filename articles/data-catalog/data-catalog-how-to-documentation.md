---
title: "aaaHow toodocument veri kaynakları | Microsoft Docs"
description: "Nasıl tooarticle vurgulama nasıl toodocument veri varlıklarını Azure veri Kataloğu."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 053b1701-b848-4ada-b726-6f485caa9961
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 4e46838d91ab4d0c0bc569ac526a0c729134bb10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="e47c1-103">Veri kaynaklarını belgelendirme</span><span class="sxs-lookup"><span data-stu-id="e47c1-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="e47c1-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="e47c1-104">Introduction</span></span>
<span data-ttu-id="e47c1-105">**Microsoft Azure veri Kataloğu** bir kayıt ve sistemi kurumsal veri kaynakları için bulma görevi gören bir tam olarak yönetilen bir bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="e47c1-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="e47c1-106">Diğer bir deyişle, **Azure veri Kataloğu** tüm bulmak, kişilerin yardımcı olma hakkında olan *anlamak*, veri kaynaklarını kullanmak ve daha fazla değer, var olan verilerden kuruluşlar tooget yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e47c1-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations tooget more value from their existing data.</span></span>

<span data-ttu-id="e47c1-107">Ne zaman bir veri kaynağı kayıtlı ile **Azure veri Kataloğu**, meta verilerini kopyalanır ve hello hizmeti tarafından dizine ancak hello Öykü yok uç.</span><span class="sxs-lookup"><span data-stu-id="e47c1-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span> <span data-ttu-id="e47c1-108">**Azure veri Kataloğu** de kullanıcıların tooprovide hello kullanım ve hello veri kaynağı için genel senaryolar açıklayabilirsiniz kendi kapsamlı belgeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e47c1-108">**Azure Data Catalog** also allows users tooprovide their own complete documentation that can describe hello usage and common scenarios for hello data source.</span></span>

<span data-ttu-id="e47c1-109">İçinde [nasıl tooannotate veri kaynaklarını](data-catalog-how-to-annotate.md), hello veri kaynağı bilen uzmanlar, etiketler ve bir açıklama açıklayabilirsiniz olduğunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e47c1-109">In [How tooannotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know hello data source can annotate it with tags and a description.</span></span> <span data-ttu-id="e47c1-110">Merhaba **Azure veri Kataloğu** portal, böylece kullanıcılar tam veri varlıklarını ve kapsayıcıları belge bir zengin metin düzenleyicisi içerir.</span><span class="sxs-lookup"><span data-stu-id="e47c1-110">hello **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="e47c1-111">Merhaba Düzenleyici paragraf biçimlendirme, başlıkları gibi metin biçimlendirmesini, madde işaretli listeler, numaralandırılmış listeler ve tabloları içerir.</span><span class="sxs-lookup"><span data-stu-id="e47c1-111">hello editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="e47c1-112">Etiketleri ve açıklamaları basit ek açıklamalar için mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="e47c1-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="e47c1-113">Ancak, toohelp veri tüketicileri bir veri kaynağı hello kullanımını daha iyi anlamak ve bir veri kaynağı uzmanı için iş senaryolarını tam, ayrıntılı belgelere sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="e47c1-113">However, toohelp data consumers better understand hello use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="e47c1-114">Kolay toodocument bir veri kaynağı değil.</span><span class="sxs-lookup"><span data-stu-id="e47c1-114">It's easy toodocument a data source.</span></span> <span data-ttu-id="e47c1-115">Bir veri varlığına veya kapsayıcı seçin ve **belgelerine**.</span><span class="sxs-lookup"><span data-stu-id="e47c1-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="e47c1-116">Veri varlıklarını belgeleme</span><span class="sxs-lookup"><span data-stu-id="e47c1-116">Documenting data assets</span></span>
<span data-ttu-id="e47c1-117">Merhaba yararı **Azure veri Kataloğu** belgelerine toouse sağlar, verilerinizi veri varlıklarınız varlıklarınızın tam bir açıklamasını içerik deposu toocreate katalog.</span><span class="sxs-lookup"><span data-stu-id="e47c1-117">hello benefit of **Azure Data Catalog** documentation allows you toouse your Data Catalog as a content repository toocreate a complete narrative of your data assets.</span></span> <span data-ttu-id="e47c1-118">Kapsayıcılar ve tabloları açıklar ayrıntılı içerik keşfedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e47c1-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="e47c1-119">SharePoint veya bir dosya paylaşımı gibi başka bir content deposundaki içerik zaten varsa bu var olan içerik toohello varlık belgelere bağlantılar tooreference ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e47c1-119">If you already have content in another content repository, such as SharePoint or a file share, you can add toohello asset documentation links tooreference this existing content.</span></span> <span data-ttu-id="e47c1-120">Bu özellik, varolan belgelerinizi daha bulunabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="e47c1-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="e47c1-121">Belge arama dizinine dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="e47c1-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="e47c1-122">Merhaba belge düzeyi hello özellikleri ve bir veri değeri açıklayan değişebilir varlık kapsayıcı tooa ayrıntılı bir kapsayıcıdaki tablo şemasını açıklaması.</span><span class="sxs-lookup"><span data-stu-id="e47c1-122">hello level of documentation can range from describing hello characteristics and value of a data asset container tooa detailed description of table schema within a container.</span></span> <span data-ttu-id="e47c1-123">sağlanan belgelerine Hello düzeyi, iş gereksinimlerinize göre güdümlü.</span><span class="sxs-lookup"><span data-stu-id="e47c1-123">hello level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="e47c1-124">Ancak genel olarak, işte birkaç Artıları ve eksileri veri varlıklarını belgeleme biri:</span><span class="sxs-lookup"><span data-stu-id="e47c1-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="e47c1-125">Yalnızca bir kapsayıcı belge: tüm Merhaba içeriğine tek bir yerde olmakla birlikte, olmaması gereken ayrıntıları için kullanıcıların toomake bilinçli bir karar.</span><span class="sxs-lookup"><span data-stu-id="e47c1-125">Document just a container: All hello content is in one place, but might lack necessary details for users toomake an informed decision.</span></span>
* <span data-ttu-id="e47c1-126">Yalnızca hello tabloları belge: içerik belirli toothat nesnesi, ancak kullanıcılarınızın belgeler için birden fazla yerde sahip.</span><span class="sxs-lookup"><span data-stu-id="e47c1-126">Document just hello tables: Content is specific toothat object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="e47c1-127">Belge kapsayıcıları ve tablolar: en kapsamlı bir yaklaşım, ancak daha fazla bakım hello belgelerin getirebilir.</span><span class="sxs-lookup"><span data-stu-id="e47c1-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of hello documents.</span></span>

## <a name="summary"></a><span data-ttu-id="e47c1-128">Özet</span><span class="sxs-lookup"><span data-stu-id="e47c1-128">Summary</span></span>
<span data-ttu-id="e47c1-129">Veri kaynakları ile belgeleme **Azure veri Kataloğu** biçiminde anlatı veri varlıklarınız hakkında gerektiği kadar ayrıntılı olarak oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e47c1-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="e47c1-130">Bağlantıları kullanarak, varolan belgeleri ve veri varlıkları bir araya getirir bir var olan içerik deposu depolanan toocontent bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e47c1-130">By using links, you can link toocontent stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="e47c1-131">Kullanıcılarınıza uygun veri varlıklarını bulma sonra belgeleri eksiksiz bir kümesini sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="e47c1-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>
