---
title: "Oyun uygulaması için Azure Mobile Engagement uygulaması"
description: "Azure Mobile Engagement uygulamak için oyun uygulaması senaryosu"
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
ms.openlocfilehash: 0ca35a3d634db8eb5c63afacba046a35b8a3e7ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="fc2d8-103">Oyun uygulaması ile Mobile Engagement uygulama</span><span class="sxs-lookup"><span data-stu-id="fc2d8-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="fc2d8-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="fc2d8-104">Overview</span></span>
<span data-ttu-id="fc2d8-105">Oyun başlatma yeni bir temel Balıkçılık role play/stratejisi oyun uygulaması sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="fc2d8-106">Oyun 6 ay için hazır ve çalışır olmuştur.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-106">The game has been up and running for 6 months.</span></span> <span data-ttu-id="fc2d8-107">Bu oyun büyük bir başarı ve yüklemeleri milyonlarca sahiptir ve bekletme diğer başlatma oyun uygulamalara kıyasla çok yüksek.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-107">This game is a huge success, and it has millions of downloads and the retention is very high compared to other start-up game apps.</span></span> <span data-ttu-id="fc2d8-108">Üç aylık gözden geçirme toplantı adresindeki Paydaşlar (ARPU) kullanıcı başına ortalama gelir artırmak ihtiyaç duydukları kabul etmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-108">At the quarterly review meeting, stakeholders agree they need to increase average revenue per user (ARPU).</span></span> <span data-ttu-id="fc2d8-109">Premium oyun paketlerin özel teklifler kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="fc2d8-110">Oyun bu paketleri, kullanıcıların kendi Balıkçılık satırları ve lures veya tackles oyundaki performansını ve görünümünü yükseltme izin verin.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-110">These game packs allow users to upgrade the appearance and performance of their fishing lines and lures or tackles in the game.</span></span> <span data-ttu-id="fc2d8-111">Bununla birlikte, paket satış çok düşük.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-111">However, package sales are very low.</span></span> <span data-ttu-id="fc2d8-112">Bu nedenle bunlar ilk olarak Müşteri Deneyimi analiz aracı ile analiz etmek karar verin ve ardından bir katılım geliştirmek için kesimleme satış kullanarak artırmak için program Gelişmiş.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-112">So they decide first to analyze the customer experience with an analytics tool, and then to develop an engagement program to increase sales using advanced segmentation.</span></span>

<span data-ttu-id="fc2d8-113">Temel [Azure Mobile Engagement - en iyi yöntemlerle Başlangıç Kılavuzu](mobile-engagement-getting-started-best-practices.md) bir katılım stratejisi oluşturmaya.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-113">Based on the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="fc2d8-114">Hedefleri ve KPI'leri</span><span class="sxs-lookup"><span data-stu-id="fc2d8-114">Objectives and KPIs</span></span>
<span data-ttu-id="fc2d8-115">Önemli katılımcılara oyun karşılamak için.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-115">Key stakeholders for the game meet.</span></span> <span data-ttu-id="fc2d8-116">Tüm % 15 premium paket satışları artırmak için bir ana hedef üzerinde-kabul ediyorum.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-116">All agree on one main objective - to increase premium package sales by 15%.</span></span> <span data-ttu-id="fc2d8-117">Bunlar iş anahtar performans göstergelerini (KPI'lar) ölçü ve sürücü bu amaç oluşturun</span><span class="sxs-lookup"><span data-stu-id="fc2d8-117">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span></span>

* <span data-ttu-id="fc2d8-118">Oyun hangi düzeyde, bu paketleri satın alınan?</span><span class="sxs-lookup"><span data-stu-id="fc2d8-118">On which level of the game are these packages purchased?</span></span>
* <span data-ttu-id="fc2d8-119">Kullanıcı başına, oturumu başına, haftalık ve aylık gelir nedir?</span><span class="sxs-lookup"><span data-stu-id="fc2d8-119">What is the revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="fc2d8-120">Sık kullanılan satın alma türleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="fc2d8-120">What are the favorite purchase types?</span></span>

<span data-ttu-id="fc2d8-121">Bölüm 1 / [Başlarken Kılavuzu](mobile-engagement-getting-started-best-practices.md) hedefleri ve KPI'leri nasıl tanımlanacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-121">Part 1 of the [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how to define the objectives and KPIs.</span></span> 

<span data-ttu-id="fc2d8-122">Şimdi tanımlanan iş KPI'leri ile yeni kullanıcı eğilimlerini ve saklama belirlemek için katılım KPI'leri mobil ürün Yöneticisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-122">With the Business KPIs now defined, the Mobile Product Manager creates Engagement KPIs to determine new user trends and retention.</span></span>

* <span data-ttu-id="fc2d8-123">İzleme bekletme ve şu aralıklar kullanın: her gün, 2 günde, haftalık, aylık ve 3 ayda</span><span class="sxs-lookup"><span data-stu-id="fc2d8-123">Monitor retention and use across the following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="fc2d8-124">Etkin kullanıcı sayısı</span><span class="sxs-lookup"><span data-stu-id="fc2d8-124">Active user counts</span></span>
* <span data-ttu-id="fc2d8-125">Uygulama derecelendirme deposundaki</span><span class="sxs-lookup"><span data-stu-id="fc2d8-125">The app rating in the store</span></span>

<span data-ttu-id="fc2d8-126">BT Ekibi önerilerine dayalı olarak, aşağıdaki teknik KPI'ları, aşağıdaki soruları yanıtlamak için eklendi:</span><span class="sxs-lookup"><span data-stu-id="fc2d8-126">Based on recommendations from the IT team, the following technical KPIs were added to answer the following questions:</span></span>

* <span data-ttu-id="fc2d8-127">My kullanıcı yolu nedir (hangi sayfasını ziyaret, ne kadar zaman kullanıcılar harcamanız üzerinde)</span><span class="sxs-lookup"><span data-stu-id="fc2d8-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="fc2d8-128">Kilitlenme veya oturum başına karşılaşılan hataların sayısı</span><span class="sxs-lookup"><span data-stu-id="fc2d8-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="fc2d8-129">İşletim sistemi sürümleri çalıştıran Kullanıcılarım nelerdir?</span><span class="sxs-lookup"><span data-stu-id="fc2d8-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="fc2d8-130">Kullanıcılarım için ekran ortalama boyutu nedir?</span><span class="sxs-lookup"><span data-stu-id="fc2d8-130">What is the average size of screen for my users?</span></span>
* <span data-ttu-id="fc2d8-131">Ne tür bir internet bağlantısı Kullanıcılarım var mı?</span><span class="sxs-lookup"><span data-stu-id="fc2d8-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="fc2d8-132">Her KPI için ihtiyaç duyacağı ve kendi playbook nerede veri mobil ürün Yöneticisi belirtir.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-132">For each KPI the Mobile Product Manager specifies the data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="fc2d8-133">Katılım programı ve tümleştirme</span><span class="sxs-lookup"><span data-stu-id="fc2d8-133">Engagement program and integration</span></span>
<span data-ttu-id="fc2d8-134">Gelişmiş katılım programı oluşturulmadan önce mobil proje Director projeden derin bir anlayış nasıl ve ürünleri kullanıcılar tarafından tüketilen olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-134">Before building an advanced engagement program, the Mobile Project Director in charge of the project should have a deep understanding of how and when products are consumed by the users.</span></span>

<span data-ttu-id="fc2d8-135">3 ay sonra kendi uygulama anında iletme bildirimi satış artırmak için yeterli veri mobil proje Director topladı.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-135">After 3 months, the Mobile Project Director has collected enough data to enhance his in-app push notification sales.</span></span> <span data-ttu-id="fc2d8-136">Hüseyin, öğrenir:</span><span class="sxs-lookup"><span data-stu-id="fc2d8-136">He learns that:</span></span>

* <span data-ttu-id="fc2d8-137">İlk satın alma genellikle 14 düzeyinde gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-137">The first purchase generally happens at the level 14.</span></span> <span data-ttu-id="fc2d8-138">Bu gibi durumlarda için % 90'ını, satın alma yeni efsanevi Silahlar için 3 ' dir.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-138">For 90% of those cases, the purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="fc2d8-139">Bu gibi durumlarda % 80'i, ürünle birlikte devam etmek ve daha fazla olun bir satın alma, yaptığınız kullanıcılar satın alır.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-139">In 80 % of those cases, users who have made a purchase, continue with the product and make more purchases.</span></span>
* <span data-ttu-id="fc2d8-140">20 düzeyi geçtiğinde kullanıcılar birden fazla 10/hafta harcamanız başlatın.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-140">Users who have passed the level 20, start to spend more than $10/week.</span></span>
* <span data-ttu-id="fc2d8-141">Kullanıcılar, 16, 24 ve 32 düzeyinde premium paketleri satın eğilimindedir.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-141">Users tend to buy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="fc2d8-142">Bu çözümleme sayesinde mobil proje Director belirli itme uygulama satış artırmak için bildirim dizileri oluşturmaya karar verir.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-142">Thanks to this analysis the Mobile Project Director decides to create specific push notification sequences to increase in app sales.</span></span> <span data-ttu-id="fc2d8-143">Halil, kendisine çağıran üç anında iletme sıralarını oluşturur: program, satış programı ve etkin olmayan programı'na Hoş Geldiniz.</span><span class="sxs-lookup"><span data-stu-id="fc2d8-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="fc2d8-144">Daha fazla bilgi için bkz [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="fc2d8-144">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
