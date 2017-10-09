---
title: Power BI ile SQL Data Warehouse aaaUse | Microsoft Docs
description: "Power BI çözümleri geliştirmek için Azure SQL Data Warehouse ile kullanma ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="e9bcd-103">Power BI ile SQL veri ambarı kullanın</span><span class="sxs-lookup"><span data-stu-id="e9bcd-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="e9bcd-104">Azure SQL Database'de olduğu gibi kullanıcı tooleverage güçlü mantıksal aşağı itme hello analitik Power BI özelliklerini yanında SQL veri ambarı doğrudan bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user tooleverage powerful logical pushdown alongside hello analytical capabilities of Power BI.</span></span>  <span data-ttu-id="e9bcd-105">Merhaba veri keşfetmenizde doğrudan bağlantı ile sorgular geri tooyour Azure SQL Data Warehouse gerçek zamanlı olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-105">With Direct Connect, queries are sent back tooyour Azure SQL Data Warehouse in real time as you explore hello data.</span></span>  <span data-ttu-id="e9bcd-106">Bu, birleştirilmiş SQL Data Warehouse, kullanıcıların sağlar hello ölçeğini ile toocreate dinamik raporlar terabayt veri göre dakika cinsinden.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-106">This, combined with hello scale of SQL Data Warehouse, enables users toocreate dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="e9bcd-107">Ayrıca, Power BI düğmesi açık hello hello giriş kullanıcılara toodirectly Azure diğer bölümlerden bilgilerini toplamadan Power BI tootheir SQL Data Warehouse bağlanın.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-107">In addition, hello introduction of hello Open in Power BI button allows users toodirectly connect Power BI tootheir SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="e9bcd-108">Doğrudan bağlantı Lütfen Not kullanırken:</span><span class="sxs-lookup"><span data-stu-id="e9bcd-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="e9bcd-109">(Daha fazla Ayrıntılar için aşağıya bakın) bağlanırken Hello tam sunucu adını belirtin</span><span class="sxs-lookup"><span data-stu-id="e9bcd-109">Specify hello fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="e9bcd-110">Merhaba veritabanı yapılandırılması için güvenlik duvarı kuralları çok "erişim tooAzure Hizmetleri izin ver" emin olun.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-110">Ensure firewall rules for hello database are configured too"Allow access tooAzure services".</span></span>
* <span data-ttu-id="e9bcd-111">Bir sütunun seçilmesi veya bir filtre eklemeden gibi her eylem hello veri ambarı doğrudan sorgu</span><span class="sxs-lookup"><span data-stu-id="e9bcd-111">Every action such as selecting a column or adding a filter will  directly query hello data warehouse</span></span>
* <span data-ttu-id="e9bcd-112">Döşeme yaklaşık 15 (yenileme zamanlanan toobe gerekmez) dakikada bir yenilenir.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-112">Tiles are refreshed approximately every 15 minutes (refresh does not need toobe scheduled)</span></span>
* <span data-ttu-id="e9bcd-113">Soru- cevap veri kümeleri doğrudan bağlanmak için kullanılabilir değil</span><span class="sxs-lookup"><span data-stu-id="e9bcd-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="e9bcd-114">Şema değişiklikleri otomatik olarak toplanmaz</span><span class="sxs-lookup"><span data-stu-id="e9bcd-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="e9bcd-115">Tüm doğrudan bağlanmak sorguları 2 dakika sonra zaman aşımına uğrar</span><span class="sxs-lookup"><span data-stu-id="e9bcd-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="e9bcd-116">Biz tooimprove hello deneyimleri devam ederken bu kısıtlamaları ve notlar değişebilir.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-116">These restrictions and notes may change as we continue tooimprove hello experiences.</span></span> <span data-ttu-id="e9bcd-117">Merhaba adımları tooconnect ayrıntılı aşağıda.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-117">hello steps tooconnect are detailed below.</span></span>  

## <a name="using-hello-open-in-power-bi-button"></a><span data-ttu-id="e9bcd-118">Merhaba 'Power bı'da Aç' düğmesini kullanarak</span><span class="sxs-lookup"><span data-stu-id="e9bcd-118">Using hello ‘Open in Power BI’ button</span></span>
<span data-ttu-id="e9bcd-119">Power BI düğmesi açık hello ile Merhaba en kolay yolu toomove SQL veri ambarı ve Power BI arasında olur.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-119">hello easiest way toomove between your SQL Data Warehouse and Power BI is with hello Open in Power BI button.</span></span> <span data-ttu-id="e9bcd-120">Bu düğme sağlar tooseamlessly başlamak Power BI'da yeni panolar oluşturma.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-120">This button allows you tooseamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="e9bcd-121">başlatılan tooget hello Klasik Azure Portalı'nda tooyour SQL Data Warehouse örneğine gidin.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-121">tooget started navigate tooyour SQL Data Warehouse instance in hello Azure Classic Portal.</span></span>
2. <span data-ttu-id="e9bcd-122">Merhaba 'Power bı'da Aç' düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-122">Click hello 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="e9bcd-123">Biz mümkün toosign değilseniz, size, doğrudan veya Power BI hesabınız yoksa, toosign bileşenini gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-123">If we are not able toosign you in directly, or if you do not have a Power BI account, you will need toosign-in.</span></span>  
4. <span data-ttu-id="e9bcd-124">SQL veri ambarı hello bilgileriyle SQL Data Warehouse bağlantı sayfası toohello önceden doldurulmuş yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-124">You will be directed toohello SQL Data Warehouse connection page, with hello information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="e9bcd-125">Kimlik bilgilerinizi girdikten sonra tam olarak bağlı tooyour SQL Data Warehouse olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-125">After entering your credentials you will be fully connected tooyour SQL Data Warehouse.</span></span>

## <a name="connecting-through-hello-power-bi-portal"></a><span data-ttu-id="e9bcd-126">Merhaba Power BI Portalı aracılığıyla bağlanma</span><span class="sxs-lookup"><span data-stu-id="e9bcd-126">Connecting through hello Power BI portal</span></span>
<span data-ttu-id="e9bcd-127">Toplama toousing hello içinde Aç Power BI düğmesi, kullanıcıların hello Power BI Portal tootheir SQL Data Warehouse da bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-127">In addition toousing hello Open in Power BI button, users can also connect tootheir SQL Data Warehouse through hello Power BI Portal.</span></span>

1. <span data-ttu-id="e9bcd-128">Merhaba Gezinti bölmesinin hello altındaki ' Veri Al' tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-128">Click 'Get Data' at hello bottom of hello navigation pane.</span></span>
2. <span data-ttu-id="e9bcd-129">'Veritabanlarını' seçin.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="e9bcd-130">Bir kez 'Azure SQL Data Warehouse' hello veritabanlarını sayfasında, seçin ve 'Bağlan' ı.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-130">Once on hello Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="e9bcd-131">Merhaba gerekli bağlantı bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-131">Enter hello necessary connection information.</span></span>  <span data-ttu-id="e9bcd-132">Sunucu adını ve veritabanı adını hello Azure portalında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-132">Your server name and database name can be found in hello Azure Portal.</span></span>
5. <span data-ttu-id="e9bcd-133">Size, toohello ana sayfa bağlantınızı 'Veri kümeleri' altında yeni bir giriş yapıldıktan sonra ve Power BI örneğinizi hello adıyla görünür yeniden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-133">You will be directed back toohello main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with hello name of your instance.</span></span>  
6. <span data-ttu-id="e9bcd-134">Merhaba yeni veri kümesi tooexplore tıklayabilirsiniz tüm hello tabloların ve görünümlerin veritabanınızdaki.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-134">You can click on hello new dataset tooexplore all of hello tables and views in your database.</span></span> <span data-ttu-id="e9bcd-135">Bir sütunun seçilmesi, visual dinamik olarak oluşturma bir sorgu geri toohello kaynağı gönderir.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-135">Selecting a column will send a query back toohello source, dynamically creating your visual.</span></span> <span data-ttu-id="e9bcd-136">Bu görsel yeni bir raporda kaydedilebilir ve geri tooyour Pano sabitlenir.</span><span class="sxs-lookup"><span data-stu-id="e9bcd-136">These visuals can be saved in a new report and pinned back tooyour dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
