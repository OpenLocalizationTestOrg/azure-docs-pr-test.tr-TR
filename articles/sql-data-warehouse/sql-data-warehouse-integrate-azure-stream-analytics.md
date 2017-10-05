---
title: "SQL Data Warehouse ile Azure akış analizi kullanın | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse ile Azure akış analizi kullanımı hakkında ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 14783f0464764a11d7f03a5db1c2d63728a4cb50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="02fa1-103">SQL Data Warehouse ile Azure akış analizi kullanın</span><span class="sxs-lookup"><span data-stu-id="02fa1-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="02fa1-104">Azure Stream Analytics akış verileri bulutta üzerinden düşük gecikmeli, yüksek oranda kullanılabilir, ölçeklenebilir karmaşık olay işlemesi sağlayan tam olarak yönetilen bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="02fa1-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="02fa1-105">Okuyarak temel kavramları öğrenebilirsiniz [Azure Stream Analytics'e giriş][Introduction to Azure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="02fa1-105">You can learn the basics by reading [Introduction to Azure Stream Analytics][Introduction to Azure Stream Analytics].</span></span> <span data-ttu-id="02fa1-106">Ardından izleyerek akış Analizi ile bir uçtan uca çözüm oluşturmak nasıl öğrenebilirsiniz [Azure Stream Analytics ile çalışmaya başlamak] [ Get started using Azure Stream Analytics] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="02fa1-106">You can then learn how to create an end-to-end solution with Stream Analytics by following the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="02fa1-107">Bu makalede, Azure SQL Data Warehouse veritabanınızı, akış analizi işleri için çıkış havuzu olarak kullanmak üzere öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="02fa1-107">In this article, you will learn how to use your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02fa1-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="02fa1-108">Prerequisites</span></span>
<span data-ttu-id="02fa1-109">İlk olarak, aşağıdaki adımları çalıştırın [Azure Stream Analytics ile çalışmaya başlamak] [ Get started using Azure Stream Analytics] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="02fa1-109">First, run through the following steps in the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="02fa1-110">Olay hub'ı giriş oluştur</span><span class="sxs-lookup"><span data-stu-id="02fa1-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="02fa1-111">Yapılandırma ve olay Oluşturucu uygulamasını başlatın</span><span class="sxs-lookup"><span data-stu-id="02fa1-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="02fa1-112">Akış analizi işi sağlama</span><span class="sxs-lookup"><span data-stu-id="02fa1-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="02fa1-113">İş Girişi ve sorgu belirtin</span><span class="sxs-lookup"><span data-stu-id="02fa1-113">Specify job input and query</span></span>

<span data-ttu-id="02fa1-114">Ardından, bir Azure SQL Data Warehouse veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="02fa1-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="02fa1-115">İş çıktısı belirtin: Azure SQL veri ambarı veritabanı</span><span class="sxs-lookup"><span data-stu-id="02fa1-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="02fa1-116">1. Adım</span><span class="sxs-lookup"><span data-stu-id="02fa1-116">Step 1</span></span>
<span data-ttu-id="02fa1-117">Stream Analytics işinde tıklatın **çıkış** sayfa ve ardından üstünden **Çıktı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="02fa1-117">In your Stream Analytics job click **OUTPUT** from the top of the page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="02fa1-118">2. Adım</span><span class="sxs-lookup"><span data-stu-id="02fa1-118">Step 2</span></span>
<span data-ttu-id="02fa1-119">SQL veritabanı'nı seçin ve İleri'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="02fa1-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="02fa1-120">3. Adım</span><span class="sxs-lookup"><span data-stu-id="02fa1-120">Step 3</span></span>
<span data-ttu-id="02fa1-121">Sonraki sayfada aşağıdaki değerleri girin:</span><span class="sxs-lookup"><span data-stu-id="02fa1-121">Enter the following values on the next page:</span></span>

* <span data-ttu-id="02fa1-122">*Diğer ad çıktı*: Bu iş çıktısı için bir kolay ad girin.</span><span class="sxs-lookup"><span data-stu-id="02fa1-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="02fa1-123">*Abonelik*:</span><span class="sxs-lookup"><span data-stu-id="02fa1-123">*Subscription*:</span></span>
  * <span data-ttu-id="02fa1-124">SQL Data Warehouse veritabanınıza Stream Analytics işi ile aynı abonelikte ise, SQL veritabanını kullan geçerli abonelikten seçin.</span><span class="sxs-lookup"><span data-stu-id="02fa1-124">If your SQL Data Warehouse database is in the same subscription as the Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="02fa1-125">Veritabanınız farklı bir abonelikte ise, SQL veritabanını kullan başka bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="02fa1-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="02fa1-126">*Veritabanı*: hedef veritabanının adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="02fa1-126">*Database*: Specify the name of a destination database.</span></span>
* <span data-ttu-id="02fa1-127">*Sunucu adı*: yalnızca belirtilen veritabanı sunucusu adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="02fa1-127">*Server Name*: Specify the server name for the database you just specified.</span></span> <span data-ttu-id="02fa1-128">Bunu bulmak için Azure Klasik Portalı'nı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02fa1-128">You can use the Azure Classic Portal to find this.</span></span>

![][server-name]

* <span data-ttu-id="02fa1-129">*Kullanıcı adı*: veritabanı için yazma izinlerine sahip bir hesabın kullanıcı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="02fa1-129">*User Name*: Specify the user name of an account that has write permissions for the database.</span></span>
* <span data-ttu-id="02fa1-130">*Parola*: Belirtilen kullanıcı hesabı için parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="02fa1-130">*Password*: Provide the password for the specified user account.</span></span>
* <span data-ttu-id="02fa1-131">*Tablo*: veritabanında hedef tablo adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="02fa1-131">*Table*: Specify the name of the target table in the database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="02fa1-132">4. Adım</span><span class="sxs-lookup"><span data-stu-id="02fa1-132">Step 4</span></span>
<span data-ttu-id="02fa1-133">Bu iş çıktısı eklemek ve akış analizi veritabanına başarıyla bağlanabildiğini doğrulamak için onay düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02fa1-133">Click the check button to add this job output and to verify that Stream Analytics can successfully connect to the database.</span></span>

![][test-connection]

<span data-ttu-id="02fa1-134">Veritabanı bağlantısı başarılı olduğunda, portalın altındaki bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="02fa1-134">When the connection to the database succeeds, you will see a notification at the bottom of the portal.</span></span> <span data-ttu-id="02fa1-135">Veritabanı bağlantısı test etmek için alttaki Bağlantıyı Sına tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02fa1-135">You can click Test Connection at the bottom to test the connection to the database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02fa1-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="02fa1-136">Next steps</span></span>
<span data-ttu-id="02fa1-137">Tümleştirme genel bakış için bkz: [SQL Data Warehouse tümleştirme genel bakış][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="02fa1-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="02fa1-138">Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="02fa1-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction to Azure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
