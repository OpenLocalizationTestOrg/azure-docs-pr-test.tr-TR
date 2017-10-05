---
title: "Veri kaynaklarını belgeleme | Microsoft Docs"
description: "Nasıl yapılır makalesi Azure veri Kataloğu veri varlıklarını belgeleme vurgulama."
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
ms.openlocfilehash: ffe951f60afb57524568fe1ed3b3668d0088e124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="9ff41-103">Veri kaynaklarını belgelendirme</span><span class="sxs-lookup"><span data-stu-id="9ff41-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="9ff41-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="9ff41-104">Introduction</span></span>
<span data-ttu-id="9ff41-105">**Microsoft Azure veri Kataloğu** bir kayıt ve sistemi kurumsal veri kaynakları için bulma görevi gören bir tam olarak yönetilen bir bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="9ff41-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="9ff41-106">Diğer bir deyişle, **Azure veri Kataloğu** tüm bulmak, kişilerin yardımcı olma hakkında olan *anlamak*, veri kaynaklarını kullanmak ve kuruluşların kendi var olan verilerden daha fazla değer almak için.</span><span class="sxs-lookup"><span data-stu-id="9ff41-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations to get more value from their existing data.</span></span>

<span data-ttu-id="9ff41-107">Ne zaman bir veri kaynağı kayıtlı ile **Azure veri Kataloğu**, meta verilerini kopyalanır ve hizmet tarafından dizine ancak Öykü yok sonlanmıyor.</span><span class="sxs-lookup"><span data-stu-id="9ff41-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span> <span data-ttu-id="9ff41-108">**Azure veri Kataloğu** kullanıcılara ayrıca kullanım ve veri kaynağı için genel senaryolar açıklayabilirsiniz kendi kapsamlı belgeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ff41-108">**Azure Data Catalog** also allows users to provide their own complete documentation that can describe the usage and common scenarios for the data source.</span></span>

<span data-ttu-id="9ff41-109">İçinde [veri kaynaklarına açıklama ekleme](data-catalog-how-to-annotate.md), veri kaynağı bilen uzmanlar, etiketler ve bir açıklama açıklayabilirsiniz olduğunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9ff41-109">In [How to annotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know the data source can annotate it with tags and a description.</span></span> <span data-ttu-id="9ff41-110">**Azure veri Kataloğu** portal, böylece kullanıcılar tam veri varlıklarını ve kapsayıcıları belge bir zengin metin düzenleyicisi içerir.</span><span class="sxs-lookup"><span data-stu-id="9ff41-110">The **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="9ff41-111">Düzenleyici, paragraf biçimlendirmesini başlıkları gibi metin biçimlendirmesini, madde işaretli listeler, numaralandırılmış listeler ve tabloları içerir.</span><span class="sxs-lookup"><span data-stu-id="9ff41-111">The editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="9ff41-112">Etiketleri ve açıklamaları basit ek açıklamalar için mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="9ff41-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="9ff41-113">Ancak, veri tüketicileri daha iyi bir veri kaynağı için bir veri kaynağı ve iş senaryolarını kullanımını anlamanıza yardımcı olmak için uzman tam, ayrıntılı belgelere sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="9ff41-113">However, to help data consumers better understand the use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="9ff41-114">Bir veri kaynağı belge kolaydır.</span><span class="sxs-lookup"><span data-stu-id="9ff41-114">It's easy to document a data source.</span></span> <span data-ttu-id="9ff41-115">Bir veri varlığına veya kapsayıcı seçin ve **belgelerine**.</span><span class="sxs-lookup"><span data-stu-id="9ff41-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="9ff41-116">Veri varlıklarını belgeleme</span><span class="sxs-lookup"><span data-stu-id="9ff41-116">Documenting data assets</span></span>
<span data-ttu-id="9ff41-117">Avantajı **Azure veri Kataloğu** belgelerine veri varlıklarınız varlıklarınızın tam bir açıklamasını oluşturmak için veri kataloğunuzu bir içerik deposu olarak kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ff41-117">The benefit of **Azure Data Catalog** documentation allows you to use your Data Catalog as a content repository to create a complete narrative of your data assets.</span></span> <span data-ttu-id="9ff41-118">Kapsayıcılar ve tabloları açıklar ayrıntılı içerik keşfedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ff41-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="9ff41-119">SharePoint veya bir dosya paylaşımı gibi başka bir content deposundaki içerik zaten varsa bu var olan içerik başvurmak için varlık belgelere bağlantılar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ff41-119">If you already have content in another content repository, such as SharePoint or a file share, you can add to the asset documentation links to reference this existing content.</span></span> <span data-ttu-id="9ff41-120">Bu özellik, varolan belgelerinizi daha bulunabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="9ff41-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="9ff41-121">Belge arama dizinine dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="9ff41-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="9ff41-122">Belge düzeyi değeri bir kapsayıcıdaki tablo şemasını ayrıntılı bir açıklaması için veri varlık kapsayıcısının ve özelliklerini açıklayan aralığında değişebilir.</span><span class="sxs-lookup"><span data-stu-id="9ff41-122">The level of documentation can range from describing the characteristics and value of a data asset container to a detailed description of table schema within a container.</span></span> <span data-ttu-id="9ff41-123">Sağlanan belge düzeyi, iş gereksinimlerinize göre güdümlü.</span><span class="sxs-lookup"><span data-stu-id="9ff41-123">The level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="9ff41-124">Ancak genel olarak, işte birkaç Artıları ve eksileri veri varlıklarını belgeleme biri:</span><span class="sxs-lookup"><span data-stu-id="9ff41-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="9ff41-125">Yalnızca bir kapsayıcı belge: tüm içeriği tek bir yerde olsa da, kullanıcıların bilinçli bir karar gerekli bilgileri eksik.</span><span class="sxs-lookup"><span data-stu-id="9ff41-125">Document just a container: All the content is in one place, but might lack necessary details for users to make an informed decision.</span></span>
* <span data-ttu-id="9ff41-126">Yalnızca tablolar belge: içeriği o nesneye özgü, ancak kullanıcılarınızın belgeler için birden fazla yerde sahip.</span><span class="sxs-lookup"><span data-stu-id="9ff41-126">Document just the tables: Content is specific to that object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="9ff41-127">Belge kapsayıcıları ve tablolar: en kapsamlı bir yaklaşım, ancak daha fazla bakım belgelerin getirebilir.</span><span class="sxs-lookup"><span data-stu-id="9ff41-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of the documents.</span></span>

## <a name="summary"></a><span data-ttu-id="9ff41-128">Özet</span><span class="sxs-lookup"><span data-stu-id="9ff41-128">Summary</span></span>
<span data-ttu-id="9ff41-129">Veri kaynakları ile belgeleme **Azure veri Kataloğu** biçiminde anlatı veri varlıklarınız hakkında gerektiği kadar ayrıntılı olarak oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ff41-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="9ff41-130">Bağlantıları kullanarak, varolan belgeleri ve veri varlıkları bir araya getirir bir var olan içerik deposu depolanan içerik bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ff41-130">By using links, you can link to content stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="9ff41-131">Kullanıcılarınıza uygun veri varlıklarını bulma sonra belgeleri eksiksiz bir kümesini sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="9ff41-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>
