---
title: "aaaUse SQL Data Warehouse ile Azure akış analizi | Microsoft Docs"
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
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="c89df-103">SQL Data Warehouse ile Azure akış analizi kullanın</span><span class="sxs-lookup"><span data-stu-id="c89df-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="c89df-104">Azure Stream Analytics hello bulutta veri akış üzerinden düşük gecikmeli, yüksek oranda kullanılabilir, ölçeklenebilir karmaşık olay işlemesi sağlayan tam olarak yönetilen bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="c89df-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="c89df-105">Okuyarak hello temel kavramları öğrenebilirsiniz [giriş tooAzure Stream Analytics][Introduction tooAzure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="c89df-105">You can learn hello basics by reading [Introduction tooAzure Stream Analytics][Introduction tooAzure Stream Analytics].</span></span> <span data-ttu-id="c89df-106">Ardından nasıl toocreate izleyerek bir uçtan uca çözüm akış Analizi ile Merhaba öğrenebilirsiniz [Azure Stream Analytics ile çalışmaya başlamak] [ Get started using Azure Stream Analytics] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="c89df-106">You can then learn how toocreate an end-to-end solution with Stream Analytics by following hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="c89df-107">Bu makalede, Azure SQL veri ambarı nasıl toouse veritabanı akış analizi işleriniz için çıkış havuzu olarak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c89df-107">In this article, you will learn how toouse your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c89df-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c89df-108">Prerequisites</span></span>
<span data-ttu-id="c89df-109">Öncelikle hello adımlarını izleyerek hello aracılığıyla çalıştırın [Azure Stream Analytics ile çalışmaya başlamak] [ Get started using Azure Stream Analytics] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="c89df-109">First, run through hello following steps in hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="c89df-110">Olay hub'ı giriş oluştur</span><span class="sxs-lookup"><span data-stu-id="c89df-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="c89df-111">Yapılandırma ve olay Oluşturucu uygulamasını başlatın</span><span class="sxs-lookup"><span data-stu-id="c89df-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="c89df-112">Akış analizi işi sağlama</span><span class="sxs-lookup"><span data-stu-id="c89df-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="c89df-113">İş Girişi ve sorgu belirtin</span><span class="sxs-lookup"><span data-stu-id="c89df-113">Specify job input and query</span></span>

<span data-ttu-id="c89df-114">Ardından, bir Azure SQL Data Warehouse veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c89df-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="c89df-115">İş çıktısı belirtin: Azure SQL veri ambarı veritabanı</span><span class="sxs-lookup"><span data-stu-id="c89df-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="c89df-116">1. Adım</span><span class="sxs-lookup"><span data-stu-id="c89df-116">Step 1</span></span>
<span data-ttu-id="c89df-117">Stream Analytics işinde tıklatın **çıkış** hello sayfasının ve ardından hello üstten **Çıktı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c89df-117">In your Stream Analytics job click **OUTPUT** from hello top of hello page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="c89df-118">2. Adım</span><span class="sxs-lookup"><span data-stu-id="c89df-118">Step 2</span></span>
<span data-ttu-id="c89df-119">SQL veritabanı'nı seçin ve İleri'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c89df-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="c89df-120">3. Adım</span><span class="sxs-lookup"><span data-stu-id="c89df-120">Step 3</span></span>
<span data-ttu-id="c89df-121">Merhaba sonraki sayfada değerleri aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="c89df-121">Enter hello following values on hello next page:</span></span>

* <span data-ttu-id="c89df-122">*Diğer ad çıktı*: Bu iş çıktısı için bir kolay ad girin.</span><span class="sxs-lookup"><span data-stu-id="c89df-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="c89df-123">*Abonelik*:</span><span class="sxs-lookup"><span data-stu-id="c89df-123">*Subscription*:</span></span>
  * <span data-ttu-id="c89df-124">SQL Data Warehouse veritabanınıza hello ise hello Stream Analytics işi, aynı abonelik geçerli abonelikten kullanım SQL veritabanı seçin.</span><span class="sxs-lookup"><span data-stu-id="c89df-124">If your SQL Data Warehouse database is in hello same subscription as hello Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="c89df-125">Veritabanınız farklı bir abonelikte ise, SQL veritabanını kullan başka bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="c89df-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="c89df-126">*Veritabanı*: hello bir hedef veritabanı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="c89df-126">*Database*: Specify hello name of a destination database.</span></span>
* <span data-ttu-id="c89df-127">*Sunucu adı*: yalnızca belirtilen hello veritabanı için hello sunucu adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="c89df-127">*Server Name*: Specify hello server name for hello database you just specified.</span></span> <span data-ttu-id="c89df-128">Merhaba Klasik Azure portalı toofind bunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89df-128">You can use hello Azure Classic Portal toofind this.</span></span>

![][server-name]

* <span data-ttu-id="c89df-129">*Kullanıcı adı*: hello hello veritabanı için yazma izinlerine sahip bir hesabın kullanıcı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="c89df-129">*User Name*: Specify hello user name of an account that has write permissions for hello database.</span></span>
* <span data-ttu-id="c89df-130">*Parola*: sağlamak hello hello parolasını belirtilen kullanıcı hesabı.</span><span class="sxs-lookup"><span data-stu-id="c89df-130">*Password*: Provide hello password for hello specified user account.</span></span>
* <span data-ttu-id="c89df-131">*Tablo*: hello veritabanında hello hello hedef tablo adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="c89df-131">*Table*: Specify hello name of hello target table in hello database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="c89df-132">4. Adım</span><span class="sxs-lookup"><span data-stu-id="c89df-132">Step 4</span></span>
<span data-ttu-id="c89df-133">Merhaba onay düğmesine tooadd bu iş çıktısı ve akış analizi toohello veritabanı başarıyla bağlanabildiğinizi tooverify'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c89df-133">Click hello check button tooadd this job output and tooverify that Stream Analytics can successfully connect toohello database.</span></span>

![][test-connection]

<span data-ttu-id="c89df-134">Merhaba bağlantı toohello veritabanı başarılı olduğunda hello portal hello altındaki bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c89df-134">When hello connection toohello database succeeds, you will see a notification at hello bottom of hello portal.</span></span> <span data-ttu-id="c89df-135">Bağlantıyı Sına hello alt tootest hello bağlantı toohello veritabanını tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89df-135">You can click Test Connection at hello bottom tootest hello connection toohello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c89df-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c89df-136">Next steps</span></span>
<span data-ttu-id="c89df-137">Tümleştirme genel bakış için bkz: [SQL Data Warehouse tümleştirme genel bakış][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="c89df-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="c89df-138">Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="c89df-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
