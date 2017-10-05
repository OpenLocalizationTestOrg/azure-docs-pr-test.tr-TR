---
title: "Power BI ile SQL veri ambarı kullanın | Microsoft Docs"
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
ms.openlocfilehash: 4b7609fc5d6ce7bf0e3bd3ebf6d8f52e93a40a75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="cee59-103">Power BI ile SQL veri ambarı kullanın</span><span class="sxs-lookup"><span data-stu-id="cee59-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="cee59-104">Olarak Azure SQL veritabanı ile SQL veri ambarı doğrudan bağlantı Power BI analitik yeteneklerini yanında aşağı güçlü mantıksal itme yararlanan olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="cee59-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user to leverage powerful logical pushdown alongside the analytical capabilities of Power BI.</span></span>  <span data-ttu-id="cee59-105">Veri keşfetmenizde doğrudan bağlantı ile sorgular gerçek zamanlı Azure SQL veri ambarı için geri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="cee59-105">With Direct Connect, queries are sent back to your Azure SQL Data Warehouse in real time as you explore the data.</span></span>  <span data-ttu-id="cee59-106">Bu, birleştirilmiş ölçekli SQL Data Warehouse, terabayt veri göre dakika cinsinden dinamik raporlar oluşturmak için kullanıcıların sağlar.</span><span class="sxs-lookup"><span data-stu-id="cee59-106">This, combined with the scale of SQL Data Warehouse, enables users to create dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="cee59-107">Ayrıca, Power BI düğmesi Aç giriş doğrudan Power BI kendi SQL veri ambarı'na Azure diğer bölümlerden bilgilerini toplamadan bağlanmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="cee59-107">In addition, the introduction of the Open in Power BI button allows users to directly connect Power BI to their SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="cee59-108">Doğrudan bağlantı Lütfen Not kullanırken:</span><span class="sxs-lookup"><span data-stu-id="cee59-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="cee59-109">(Daha fazla Ayrıntılar için aşağıya bakın) bağlanırken tam sunucu adını belirtin</span><span class="sxs-lookup"><span data-stu-id="cee59-109">Specify the fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="cee59-110">Veritabanı için güvenlik duvarı kurallarının "Azure hizmetlerine erişime izin ver" için yapılandırılmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="cee59-110">Ensure firewall rules for the database are configured to "Allow access to Azure services".</span></span>
* <span data-ttu-id="cee59-111">Bir sütunun seçilmesi veya bir filtre eklemeden gibi her eylem veri ambarı doğrudan sorgu</span><span class="sxs-lookup"><span data-stu-id="cee59-111">Every action such as selecting a column or adding a filter will  directly query the data warehouse</span></span>
* <span data-ttu-id="cee59-112">Döşeme yaklaşık 15 (yenileme zamanlanacak gerekmez) dakikada bir yenilenir.</span><span class="sxs-lookup"><span data-stu-id="cee59-112">Tiles are refreshed approximately every 15 minutes (refresh does not need to be scheduled)</span></span>
* <span data-ttu-id="cee59-113">Soru- cevap veri kümeleri doğrudan bağlanmak için kullanılabilir değil</span><span class="sxs-lookup"><span data-stu-id="cee59-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="cee59-114">Şema değişiklikleri otomatik olarak toplanmaz</span><span class="sxs-lookup"><span data-stu-id="cee59-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="cee59-115">Tüm doğrudan bağlanmak sorguları 2 dakika sonra zaman aşımına uğrar</span><span class="sxs-lookup"><span data-stu-id="cee59-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="cee59-116">Deneyimleri geliştirmeye devam ederken bu kısıtlamaları ve notlar değişebilir.</span><span class="sxs-lookup"><span data-stu-id="cee59-116">These restrictions and notes may change as we continue to improve the experiences.</span></span> <span data-ttu-id="cee59-117">Bağlanmak için adımlar aşağıda ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cee59-117">The steps to connect are detailed below.</span></span>  

## <a name="using-the-open-in-power-bi-button"></a><span data-ttu-id="cee59-118">'Power bı'da Aç' düğmesini kullanarak</span><span class="sxs-lookup"><span data-stu-id="cee59-118">Using the ‘Open in Power BI’ button</span></span>
<span data-ttu-id="cee59-119">SQL veri ambarı ve Power BI arasında taşımak için kolay Power BI düğmesi açıkken yoludur.</span><span class="sxs-lookup"><span data-stu-id="cee59-119">The easiest way to move between your SQL Data Warehouse and Power BI is with the Open in Power BI button.</span></span> <span data-ttu-id="cee59-120">Bu düğme, sorunsuz bir şekilde yeni pano Power BI'da oluşturmaya başlamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="cee59-120">This button allows you to seamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="cee59-121">Başlamak için Azure Klasik Portalı'nda SQL Data Warehouse örneğiniz gidin.</span><span class="sxs-lookup"><span data-stu-id="cee59-121">To get started navigate to your SQL Data Warehouse instance in the Azure Classic Portal.</span></span>
2. <span data-ttu-id="cee59-122">"Power BI'da aç" düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cee59-122">Click the 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="cee59-123">Doğrudan oturum açmak yapamıyoruz ya da Power BI hesabınız yoksa, oturum açması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cee59-123">If we are not able to sign you in directly, or if you do not have a Power BI account, you will need to sign-in.</span></span>  
4. <span data-ttu-id="cee59-124">SQL Data Warehouse bağlantı sayfası, önceden doldurulmuş SQL veri ambarı bilgileriyle yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cee59-124">You will be directed to the SQL Data Warehouse connection page, with the information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="cee59-125">Kimlik bilgilerinizi girdikten sonra tam olarak, SQL Data Warehouse bağlanır.</span><span class="sxs-lookup"><span data-stu-id="cee59-125">After entering your credentials you will be fully connected to your SQL Data Warehouse.</span></span>

## <a name="connecting-through-the-power-bi-portal"></a><span data-ttu-id="cee59-126">Power BI Portalı aracılığıyla bağlanma</span><span class="sxs-lookup"><span data-stu-id="cee59-126">Connecting through the Power BI portal</span></span>
<span data-ttu-id="cee59-127">Power BI düğmesi Aç kullanarak ek olarak, kullanıcılar ayrıca kendi SQL Data Warehouse Power BI Portalı aracılığıyla bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="cee59-127">In addition to using the Open in Power BI button, users can also connect to their SQL Data Warehouse through the Power BI Portal.</span></span>

1. <span data-ttu-id="cee59-128">Alt Gezinti Bölmesi ' Veri Al' tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cee59-128">Click 'Get Data' at the bottom of the navigation pane.</span></span>
2. <span data-ttu-id="cee59-129">'Veritabanlarını' seçin.</span><span class="sxs-lookup"><span data-stu-id="cee59-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="cee59-130">Bir kez 'Azure SQL Data Warehouse' veritabanlarını sayfasında, seçin ve 'Bağlan' ı.</span><span class="sxs-lookup"><span data-stu-id="cee59-130">Once on the Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="cee59-131">Gerekli bağlantı bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="cee59-131">Enter the necessary connection information.</span></span>  <span data-ttu-id="cee59-132">Sunucu adını ve veritabanı adını Azure Portalı'nda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="cee59-132">Your server name and database name can be found in the Azure Portal.</span></span>
5. <span data-ttu-id="cee59-133">Power BI, ana sayfasına yönlendirilir ve bağlantınızı 'Veri kümeleri' altında yeni bir giriş yapıldıktan sonra örneğinizi adıyla görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cee59-133">You will be directed back to the main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with the name of your instance.</span></span>  
6. <span data-ttu-id="cee59-134">Tüm tabloları ve görünümleri veritabanınızdaki keşfetmek için yeni veri kümesi üzerinde tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cee59-134">You can click on the new dataset to explore all of the tables and views in your database.</span></span> <span data-ttu-id="cee59-135">Bir sütunun seçilmesi bir sorgu, visual dinamik olarak oluşturma geri kaynağına gönderir.</span><span class="sxs-lookup"><span data-stu-id="cee59-135">Selecting a column will send a query back to the source, dynamically creating your visual.</span></span> <span data-ttu-id="cee59-136">Bu görsel, yeni bir raporda kaydedilir ve geri panonuza sabitlenir.</span><span class="sxs-lookup"><span data-stu-id="cee59-136">These visuals can be saved in a new report and pinned back to your dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
