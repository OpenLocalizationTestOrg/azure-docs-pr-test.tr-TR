---
title: "Oyun uygulaması için aaaAzure Mobile Engagement uygulaması"
description: "Oyun uygulaması senaryosu tooimplement Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="77c67-103">Oyun uygulaması ile Mobile Engagement uygulama</span><span class="sxs-lookup"><span data-stu-id="77c67-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="77c67-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="77c67-104">Overview</span></span>
<span data-ttu-id="77c67-105">Oyun başlatma yeni bir temel Balıkçılık role play/stratejisi oyun uygulaması sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="77c67-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="77c67-106">Merhaba oyun 6 ay için hazır ve çalışır olmuştur.</span><span class="sxs-lookup"><span data-stu-id="77c67-106">hello game has been up and running for 6 months.</span></span> <span data-ttu-id="77c67-107">Bu oyun büyük bir başarı ve yüklemeleri milyonlarca sahiptir ve hello bekletme çok yüksek karşılaştırılan tooother başlatma oyun uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="77c67-107">This game is a huge success, and it has millions of downloads and hello retention is very high compared tooother start-up game apps.</span></span> <span data-ttu-id="77c67-108">Merhaba üç aylık gözden geçirme toplantı adresindeki Paydaşlar (ARPU) kullanıcı başına ortalama gelir tooincrease ihtiyaç duydukları kabul etmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="77c67-108">At hello quarterly review meeting, stakeholders agree they need tooincrease average revenue per user (ARPU).</span></span> <span data-ttu-id="77c67-109">Premium oyun paketlerin özel teklifler kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="77c67-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="77c67-110">Bu oyun paketleri hello oyunda kullanıcılar tooupgrade hello görünümünü ve bunların Balıkçılık satırları ve lures veya tackles performansını izin verir.</span><span class="sxs-lookup"><span data-stu-id="77c67-110">These game packs allow users tooupgrade hello appearance and performance of their fishing lines and lures or tackles in hello game.</span></span> <span data-ttu-id="77c67-111">Bununla birlikte, paket satış çok düşük.</span><span class="sxs-lookup"><span data-stu-id="77c67-111">However, package sales are very low.</span></span> <span data-ttu-id="77c67-112">Bunlar karar vermek için ilk tooanalyze hello Müşteri Deneyimi analiz aracı ile ve ardından bir katılım programı tooincrease satış kullanarak toodevelop kesimleme Gelişmiş.</span><span class="sxs-lookup"><span data-stu-id="77c67-112">So they decide first tooanalyze hello customer experience with an analytics tool, and then toodevelop an engagement program tooincrease sales using advanced segmentation.</span></span>

<span data-ttu-id="77c67-113">Merhaba üzerinde temel [Azure Mobile Engagement - en iyi yöntemlerle Başlangıç Kılavuzu](mobile-engagement-getting-started-best-practices.md) bir katılım stratejisi oluşturmaya.</span><span class="sxs-lookup"><span data-stu-id="77c67-113">Based on hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="77c67-114">Hedefleri ve KPI'leri</span><span class="sxs-lookup"><span data-stu-id="77c67-114">Objectives and KPIs</span></span>
<span data-ttu-id="77c67-115">Önemli katılımcılara hello oyun karşılamak için.</span><span class="sxs-lookup"><span data-stu-id="77c67-115">Key stakeholders for hello game meet.</span></span> <span data-ttu-id="77c67-116">Tüm bir ana hedef - % 15 göre tooincrease premium paket satış üzerinde kabul ediyorum.</span><span class="sxs-lookup"><span data-stu-id="77c67-116">All agree on one main objective - tooincrease premium package sales by 15%.</span></span> <span data-ttu-id="77c67-117">Bu amaç iş anahtar performans göstergelerini (KPI'lar) toomeasure ve sürücü oluşturun</span><span class="sxs-lookup"><span data-stu-id="77c67-117">They create Business Key Performance Indicators (KPIs) toomeasure and drive this objective</span></span>

* <span data-ttu-id="77c67-118">Merhaba oyun hangi düzeyde, bu paketleri satın alınan?</span><span class="sxs-lookup"><span data-stu-id="77c67-118">On which level of hello game are these packages purchased?</span></span>
* <span data-ttu-id="77c67-119">Kullanıcı başına, oturumu başına, haftalık ve aylık hello gelir nedir?</span><span class="sxs-lookup"><span data-stu-id="77c67-119">What is hello revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="77c67-120">Merhaba sık kullanılan satın alma türleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="77c67-120">What are hello favorite purchase types?</span></span>

<span data-ttu-id="77c67-121">Merhaba 1 parçası [Başlarken Kılavuzu](mobile-engagement-getting-started-best-practices.md) toodefine nasıl hello hedefler ve KPI'ler açıklar.</span><span class="sxs-lookup"><span data-stu-id="77c67-121">Part 1 of hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how toodefine hello objectives and KPIs.</span></span> 

<span data-ttu-id="77c67-122">İş KPI'leri şimdi tanımlanan hello ile katılım KPI'leri toodetermine yeni kullanıcı eğilimlerini ve saklama başlangıç mobil ürün Yöneticisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="77c67-122">With hello Business KPIs now defined, hello Mobile Product Manager creates Engagement KPIs toodetermine new user trends and retention.</span></span>

* <span data-ttu-id="77c67-123">İzleme bekletme ve aralıklarını aşağıdaki hello arasında kullanın: her gün, 2 günde, haftalık, aylık ve 3 ayda</span><span class="sxs-lookup"><span data-stu-id="77c67-123">Monitor retention and use across hello following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="77c67-124">Etkin kullanıcı sayısı</span><span class="sxs-lookup"><span data-stu-id="77c67-124">Active user counts</span></span>
* <span data-ttu-id="77c67-125">Merhaba Hello uygulama derecesi depolama</span><span class="sxs-lookup"><span data-stu-id="77c67-125">hello app rating in hello store</span></span>

<span data-ttu-id="77c67-126">Merhaba BT Ekibi önerilerine dayalı olarak, hello teknik KPI'ları aşağıdaki soruları aşağıdaki tooanswer hello eklendi:</span><span class="sxs-lookup"><span data-stu-id="77c67-126">Based on recommendations from hello IT team, hello following technical KPIs were added tooanswer hello following questions:</span></span>

* <span data-ttu-id="77c67-127">My kullanıcı yolu nedir (hangi sayfasını ziyaret, ne kadar zaman kullanıcılar harcamanız üzerinde)</span><span class="sxs-lookup"><span data-stu-id="77c67-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="77c67-128">Kilitlenme veya oturum başına karşılaşılan hataların sayısı</span><span class="sxs-lookup"><span data-stu-id="77c67-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="77c67-129">İşletim sistemi sürümleri çalıştıran Kullanıcılarım nelerdir?</span><span class="sxs-lookup"><span data-stu-id="77c67-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="77c67-130">Kullanıcılarım için ekranın hello ortalama boyutu nedir?</span><span class="sxs-lookup"><span data-stu-id="77c67-130">What is hello average size of screen for my users?</span></span>
* <span data-ttu-id="77c67-131">Ne tür bir internet bağlantısı Kullanıcılarım var mı?</span><span class="sxs-lookup"><span data-stu-id="77c67-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="77c67-132">Her KPI için ihtiyaç duyacağı ve kendi playbook nerede hello veri hello mobil ürün Yöneticisi belirtir.</span><span class="sxs-lookup"><span data-stu-id="77c67-132">For each KPI hello Mobile Product Manager specifies hello data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="77c67-133">Katılım programı ve tümleştirme</span><span class="sxs-lookup"><span data-stu-id="77c67-133">Engagement program and integration</span></span>
<span data-ttu-id="77c67-134">Gelişmiş katılım programı oluşturulmadan önce hello mobil proje Director hello proje sorumlu nasıl ve ne zaman ürünleri hello kullanıcılar tarafından tüketilen'ın derin bir anlayış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="77c67-134">Before building an advanced engagement program, hello Mobile Project Director in charge of hello project should have a deep understanding of how and when products are consumed by hello users.</span></span>

<span data-ttu-id="77c67-135">3 ay sonra kendi uygulama anında iletme bildirimi satış yeterli veri tooenhance hello mobil proje Director topladı.</span><span class="sxs-lookup"><span data-stu-id="77c67-135">After 3 months, hello Mobile Project Director has collected enough data tooenhance his in-app push notification sales.</span></span> <span data-ttu-id="77c67-136">Hüseyin, öğrenir:</span><span class="sxs-lookup"><span data-stu-id="77c67-136">He learns that:</span></span>

* <span data-ttu-id="77c67-137">Merhaba ilk satın alma genellikle 14 hello düzeyinde gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="77c67-137">hello first purchase generally happens at hello level 14.</span></span> <span data-ttu-id="77c67-138">Bu gibi durumlarda için % 90'ını, hello satınalma yeni efsanevi Silahlar için 3'dır.</span><span class="sxs-lookup"><span data-stu-id="77c67-138">For 90% of those cases, hello purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="77c67-139">% 80 bu örneklerinin hello ürünle devam etmek ve daha fazla olun bir satın alma, yaptığınız kullanıcılar satın alır.</span><span class="sxs-lookup"><span data-stu-id="77c67-139">In 80 % of those cases, users who have made a purchase, continue with hello product and make more purchases.</span></span>
* <span data-ttu-id="77c67-140">Merhaba düzeyi 20 geçtiğinde, 10/hafta birden çok toospend Başlat kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="77c67-140">Users who have passed hello level 20, start toospend more than $10/week.</span></span>
* <span data-ttu-id="77c67-141">Kullanıcılar, 16, 24 ve 32 düzeyinde toobuy premium paketleri eğilimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="77c67-141">Users tend toobuy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="77c67-142">Merhaba mobil proje Director toocreate belirli anında iletme bildirimi dizileri tooincrease uygulama satış karar toothis analiz teşekkür eder.</span><span class="sxs-lookup"><span data-stu-id="77c67-142">Thanks toothis analysis hello Mobile Project Director decides toocreate specific push notification sequences tooincrease in app sales.</span></span> <span data-ttu-id="77c67-143">Halil, kendisine çağıran üç anında iletme sıralarını oluşturur: program, satış programı ve etkin olmayan programı'na Hoş Geldiniz.</span><span class="sxs-lookup"><span data-stu-id="77c67-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="77c67-144">Daha fazla bilgi için toohello başvurun [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="77c67-144">For more information refer toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
