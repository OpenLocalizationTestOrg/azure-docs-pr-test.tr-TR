---
title: "'büyük veri' veri kaynaklarıyla aaaHow toowork | Microsoft Docs"
description: "Azure Blob Storage, Azure Data Lake ve Hadoop HDFS dahil 'büyük veri' veri kaynaklarıyla Azure veri Kataloğu'nu kullanarak için vurgulama desenleri nasıl tooarticle."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="d600c-103">Azure veri Kataloğu'nda toowork büyük veri ile nasıl kaynakları</span><span class="sxs-lookup"><span data-stu-id="d600c-103">How toowork with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="d600c-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="d600c-104">Introduction</span></span>
<span data-ttu-id="d600c-105">**Microsoft Azure veri Kataloğu** bir kayıt ve sistemi kurumsal veri kaynakları için bulma görevi gören bir tam olarak yönetilen bir bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="d600c-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="d600c-106">Bu, Bul, anlamak ve veri kaynaklarını kullanan kişilerin ve kuruluşların tooget daha fazla değer büyük veri dahil olmak üzere kendi mevcut veri kaynaklarından veri hakkında olur.</span><span class="sxs-lookup"><span data-stu-id="d600c-106">It is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="d600c-107">**Azure veri Kataloğu** hello Azure blogu depolama BLOB'ları ve dizinleri yanı sıra Hadoop HDFS dosyaları ve dizinleri kaydını destekler.</span><span class="sxs-lookup"><span data-stu-id="d600c-107">**Azure Data Catalog** supports hello registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="d600c-108">Bu veri kaynaklarının yarı yapılandırılmış yapısını Hello büyük esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="d600c-108">hello semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="d600c-109">Bununla birlikte, çoğu değerden bunlarla kaydetme hello tooget **Azure veri Kataloğu**, kullanıcıların hello veri kaynaklarını nasıl düzenlendiği düşünmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d600c-109">However, tooget hello most value from registering them with **Azure Data Catalog**, users must consider how hello data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="d600c-110">Mantıksal veri kümeleri olarak dizinler</span><span class="sxs-lookup"><span data-stu-id="d600c-110">Directories as logical data sets</span></span>
<span data-ttu-id="d600c-111">Büyük veri kaynakları düzenlemek için genel bir desen tootreat dizinleri olarak mantıksal veri kümeleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="d600c-111">A common pattern for organizing big data sources is tootreat directories as logical data sets.</span></span> <span data-ttu-id="d600c-112">Üst düzey dizinleri kullanılan toodefine bir veri kümesinin alt bölüm tanımlayın ve içerdikleri hello hello verilerin kendisini depolamak var.</span><span class="sxs-lookup"><span data-stu-id="d600c-112">Top-level directories are used toodefine a data set, while subfolders define partitions, and hello files they contain store hello data itself.</span></span>

<span data-ttu-id="d600c-113">Bu desen örneği olabilir:</span><span class="sxs-lookup"><span data-stu-id="d600c-113">An example of this pattern might be:</span></span>

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

<span data-ttu-id="d600c-114">Bu örnekte, mantıksal veri kümeleri vehicle_maintenance_events ve location_tracking_events temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d600c-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="d600c-115">Bu klasörlerinin her biri, ay ve yıl alt klasörler halinde düzenlenmiştir veri dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="d600c-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="d600c-116">Bu klasörlerinin her biri, yüzlerce veya binlerce dosya büyük olasılıkla içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d600c-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="d600c-117">Bu modelinde tek tek dosyalarıyla kaydetme **Azure veri Kataloğu** büyük olasılıkla mantıklı değildir.</span><span class="sxs-lookup"><span data-stu-id="d600c-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="d600c-118">Bunun yerine, hello verilerle çalışma anlamlı toohello kullanıcılar hello veri kümelerini temsil hello dizinleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d600c-118">Instead, register hello directories that represent hello data sets that be meaningful toohello users working with hello data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="d600c-119">Başvuru veri dosyaları</span><span class="sxs-lookup"><span data-stu-id="d600c-119">Reference data files</span></span>
<span data-ttu-id="d600c-120">Tamamlayıcı düzeni toostore başvuru veri kümelerini tek tek dosyalar olarak ' dir.</span><span class="sxs-lookup"><span data-stu-id="d600c-120">A complementary pattern is toostore reference data sets as individual files.</span></span> <span data-ttu-id="d600c-121">Bu veri kümeleri hello 'küçük' tarafı büyük veri olarak düşünülen ve genellikle bir analitik veri modelindeki benzer toodimensions bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d600c-121">These data sets may be thought of as hello 'small' side of big data, and are often similar toodimensions in an analytical data model.</span></span> <span data-ttu-id="d600c-122">Başvuru veri dosyaları başka bir yerde hello büyük veri deposunda depolanan hello veri dosyalarının hello toplu kullanılan tooprovide bağlamının kayıtları içerir.</span><span class="sxs-lookup"><span data-stu-id="d600c-122">Reference data files contain records that are used tooprovide context for hello bulk of hello data files stored elsewhere in hello big data store.</span></span>

<span data-ttu-id="d600c-123">Bu desen örneği olabilir:</span><span class="sxs-lookup"><span data-stu-id="d600c-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="d600c-124">Bir analist veya veri Bilimcisi hello büyük dizin yapıları içinde yer alan hello verilerle çalışırken, bu başvuru dosyalardaki hello veriler kullanılan tooprovide olan varlıkları hello büyük veri tooonly adı veya kimliği tarafından başvurulan için daha ayrıntılı bilgi olabilir ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d600c-124">When an analyst or data scientist is working with hello data contained in hello larger directory structures, hello data in these reference files can be used tooprovide more detailed information for entities that are referred tooonly by name or ID in hello larger data set.</span></span>

<span data-ttu-id="d600c-125">Bu modelinde tooregister hello tek referans veri dosyalarıyla mantıklıdır **Azure veri Kataloğu**.</span><span class="sxs-lookup"><span data-stu-id="d600c-125">In this pattern, it makes sense tooregister hello individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="d600c-126">Her dosyanın bir veri kümesini temsil eder ve her bir açıklama ve tek tek bulunan.</span><span class="sxs-lookup"><span data-stu-id="d600c-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="d600c-127">Alternatif desenleri</span><span class="sxs-lookup"><span data-stu-id="d600c-127">Alternate patterns</span></span>
<span data-ttu-id="d600c-128">Hello hello önceki bölümde açıklanan desenleri büyük veri deposu düzenlenebilir yalnızca iki olası yolları vardır, ancak her farklı bir uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="d600c-128">hello patterns described in hello preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="d600c-129">Nasıl veri kaynaklarınızı, büyük veri kaynaklarıyla kaydedilirken yapılandırılmıştır bağımsız olarak **Azure veri Kataloğu**, odak, değer tooothers içinde çeken hello veri kümelerini temsil hello dosyaları ve dizinleri kaydetmede, Kuruluş.</span><span class="sxs-lookup"><span data-stu-id="d600c-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering hello files and directories that represent hello data sets that are of value tooothers within your organization.</span></span> <span data-ttu-id="d600c-130">Tüm dosyaları ve dizinleri kaydetme hello Kataloğu, kullanıcıların toofind için daha zor ne ihtiyaç duydukları kolaylaştırarak daraltabilir.</span><span class="sxs-lookup"><span data-stu-id="d600c-130">Registering all files and directories can clutter hello catalog, making it harder for users toofind what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="d600c-131">Özet</span><span class="sxs-lookup"><span data-stu-id="d600c-131">Summary</span></span>
<span data-ttu-id="d600c-132">Veri kaynakları ile kaydetme **Azure veri Kataloğu** daha kolay toodiscover yapar ve anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d600c-132">Registering data sources with **Azure Data Catalog** makes them easier toodiscover and understand.</span></span> <span data-ttu-id="d600c-133">Kaydetme ve, mantıksal veri kümelerini temsil hello büyük veri dosyaları ve dizinleri yorumlama ihtiyaç duydukları hello büyük veri kaynaklarını bulabilir ve kullanıcıların yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d600c-133">By registering and annotating hello big data files and directories that represent logical data sets, you can help users find and use hello big data sources they need.</span></span>
