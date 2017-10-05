---
title: "'Büyük veri' veri kaynağı ile çalışma | Microsoft Docs"
description: "Nasıl yapılır makalesi Azure Blob Storage, Azure Data Lake ve Hadoop HDFS dahil 'büyük veri' veri kaynaklarıyla Azure veri Kataloğu'nu kullanarak desenleri vurgulama."
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
ms.openlocfilehash: 001d80ce42f0e87276e59d70dffb75eb561d96cd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-work-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="d5f63-103">Büyük veri kaynaklarında Azure veri Kataloğu ile çalışmaya nasıl</span><span class="sxs-lookup"><span data-stu-id="d5f63-103">How to work with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="d5f63-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="d5f63-104">Introduction</span></span>
<span data-ttu-id="d5f63-105">**Microsoft Azure veri Kataloğu** bir kayıt ve sistemi kurumsal veri kaynakları için bulma görevi gören bir tam olarak yönetilen bir bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="d5f63-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="d5f63-106">Tüm yardımcı kişilerle ilgili bulmak, anlamak ve daha fazla değer büyük veri dahil olmak üzere kendi mevcut veri kaynaklarından veri almak için veri kaynakları ve yardımcı kuruluşlar kullanın içindir.</span><span class="sxs-lookup"><span data-stu-id="d5f63-106">It is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="d5f63-107">**Azure veri Kataloğu** Azure blogu depolama BLOB'ları ve dizinleri yanı sıra Hadoop HDFS dosyaları ve dizinleri kaydını destekler.</span><span class="sxs-lookup"><span data-stu-id="d5f63-107">**Azure Data Catalog** supports the registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="d5f63-108">Bu veri kaynaklarının yarı yapılandırılmış yapısını büyük esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5f63-108">The semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="d5f63-109">Ancak, bunları kaydetme en çok değer almak için **Azure veri Kataloğu**, kullanıcıların veri kaynaklarını nasıl düzenlendiği düşünmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5f63-109">However, to get the most value from registering them with **Azure Data Catalog**, users must consider how the data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="d5f63-110">Mantıksal veri kümeleri olarak dizinler</span><span class="sxs-lookup"><span data-stu-id="d5f63-110">Directories as logical data sets</span></span>
<span data-ttu-id="d5f63-111">Büyük veri kaynakları düzenlemek için genel bir desen dizinleri mantıksal veri kümeleri davran sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="d5f63-111">A common pattern for organizing big data sources is to treat directories as logical data sets.</span></span> <span data-ttu-id="d5f63-112">Üst düzey dizinleri, bir veri kümesinin alt bölüm tanımlayın ve içerdikleri dosyalar verileri depolamak tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d5f63-112">Top-level directories are used to define a data set, while subfolders define partitions, and the files they contain store the data itself.</span></span>

<span data-ttu-id="d5f63-113">Bu desen örneği olabilir:</span><span class="sxs-lookup"><span data-stu-id="d5f63-113">An example of this pattern might be:</span></span>

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

<span data-ttu-id="d5f63-114">Bu örnekte, mantıksal veri kümeleri vehicle_maintenance_events ve location_tracking_events temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d5f63-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="d5f63-115">Bu klasörlerinin her biri, ay ve yıl alt klasörler halinde düzenlenmiştir veri dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="d5f63-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="d5f63-116">Bu klasörlerinin her biri, yüzlerce veya binlerce dosya büyük olasılıkla içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d5f63-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="d5f63-117">Bu modelinde tek tek dosyalarıyla kaydetme **Azure veri Kataloğu** büyük olasılıkla mantıklı değildir.</span><span class="sxs-lookup"><span data-stu-id="d5f63-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="d5f63-118">Bunun yerine, verileri ile çalışma kullanıcılara anlamlı veri kümeleri temsil dizinleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d5f63-118">Instead, register the directories that represent the data sets that be meaningful to the users working with the data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="d5f63-119">Başvuru veri dosyaları</span><span class="sxs-lookup"><span data-stu-id="d5f63-119">Reference data files</span></span>
<span data-ttu-id="d5f63-120">Tek tek dosyalar olarak başvuru veri kümelerini depolamak için tamamlayıcı bir düzen yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="d5f63-120">A complementary pattern is to store reference data sets as individual files.</span></span> <span data-ttu-id="d5f63-121">Bu veri kümeleri, büyük veri 'küçük' yan düşünülen ve genellikle bir analitik veri modelindeki boyutlara benzer olarak.</span><span class="sxs-lookup"><span data-stu-id="d5f63-121">These data sets may be thought of as the 'small' side of big data, and are often similar to dimensions in an analytical data model.</span></span> <span data-ttu-id="d5f63-122">Başvuru veri dosyaları için başka bir yerde büyük veri deposunda depolanan veri dosyaları toplu bağlamı sağlamak için kullanılan kayıtları içerir.</span><span class="sxs-lookup"><span data-stu-id="d5f63-122">Reference data files contain records that are used to provide context for the bulk of the data files stored elsewhere in the big data store.</span></span>

<span data-ttu-id="d5f63-123">Bu desen örneği olabilir:</span><span class="sxs-lookup"><span data-stu-id="d5f63-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="d5f63-124">Bir analisti ya da veri Bilimcisi büyük dizin yapıları içinde yer alan verilerle çalışırken, bu başvuru dosyalardaki veriler yalnızca ada veya Kimliğe göre daha büyük veri kümesinde başvurulan varlıklar için daha ayrıntılı bilgi sağlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d5f63-124">When an analyst or data scientist is working with the data contained in the larger directory structures, the data in these reference files can be used to provide more detailed information for entities that are referred to only by name or ID in the larger data set.</span></span>

<span data-ttu-id="d5f63-125">Bu modelinde tek referans veri dosyalarıyla kaydetmek için mantıklıdır **Azure veri Kataloğu**.</span><span class="sxs-lookup"><span data-stu-id="d5f63-125">In this pattern, it makes sense to register the individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="d5f63-126">Her dosyanın bir veri kümesini temsil eder ve her bir açıklama ve tek tek bulunan.</span><span class="sxs-lookup"><span data-stu-id="d5f63-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="d5f63-127">Alternatif desenleri</span><span class="sxs-lookup"><span data-stu-id="d5f63-127">Alternate patterns</span></span>
<span data-ttu-id="d5f63-128">Büyük veri deposu düzenlenebilir yalnızca iki olası yolları önceki bölümde açıklanan desenleri alır, ancak her farklı bir uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="d5f63-128">The patterns described in the preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="d5f63-129">Nasıl veri kaynaklarınızı, büyük veri kaynaklarıyla kaydedilirken yapılandırılmıştır bağımsız olarak **Azure veri Kataloğu**, odak dosyaları ve diğerlerinin içinde değerinin olan veri kümeleri temsil dizinleri kaydetmede, Kuruluş.</span><span class="sxs-lookup"><span data-stu-id="d5f63-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering the files and directories that represent the data sets that are of value to others within your organization.</span></span> <span data-ttu-id="d5f63-130">Tüm dosyaları ve dizinleri kaydetme ne ihtiyaç duydukları bulmak kullanıcılar için daha zor hale getirme katalog daraltabilir.</span><span class="sxs-lookup"><span data-stu-id="d5f63-130">Registering all files and directories can clutter the catalog, making it harder for users to find what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="d5f63-131">Özet</span><span class="sxs-lookup"><span data-stu-id="d5f63-131">Summary</span></span>
<span data-ttu-id="d5f63-132">Veri kaynakları ile kaydetme **Azure veri Kataloğu** bulunmasını ve anlaşılmasını daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="d5f63-132">Registering data sources with **Azure Data Catalog** makes them easier to discover and understand.</span></span> <span data-ttu-id="d5f63-133">Kaydetme ve büyük veri dosyaları ve mantıksal veri kümelerini temsil dizinleri yorumlama ihtiyaç duydukları büyük veri kaynaklarını bulabilir ve kullanıcıların yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d5f63-133">By registering and annotating the big data files and directories that represent logical data sets, you can help users find and use the big data sources they need.</span></span>
