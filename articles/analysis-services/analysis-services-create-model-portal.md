---
title: "Azure Analysis Services Web Tasarımcısı kullanarak tablolu model oluşturma | Microsoft Docs"
description: "Azure portalında Web Tasarımcısını kullanarak bir Azure Analysis Services tablolu model oluşturmayı öğrenin."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: bd58f1845dabf6afb47ce27236d14479677a8808
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="b07f4-103">Azure portalında bir model oluşturma</span><span class="sxs-lookup"><span data-stu-id="b07f4-103">Create a model in Azure portal</span></span>

<span data-ttu-id="b07f4-104">Azure portalında Azure Analysis Services web Tasarımcısı (Önizleme) özelliği oluşturmak ve tablolu modeller düzenleyin ve model veri sağ tarayıcınızda sorgulamak için hızlı ve kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="b07f4-104">The Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way to create and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="b07f4-105">Unutmayın, web Designer **Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="b07f4-105">Keep in mind, the web designer is **preview**.</span></span> <span data-ttu-id="b07f4-106">Her zaman Önizleme, eklenmiş yeni işlevi sırada işlevselliği sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b07f4-106">While new functionality is being added all the time, in preview, functionality is limited.</span></span> <span data-ttu-id="b07f4-107">Daha gelişmiş modeli geliştirme ve test için Visual Studio (SSDT) ve SQL Server Management Studio (SSMS) kullanmak en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="b07f4-107">For more advanced model development and testing, it's best to use Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b07f4-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b07f4-108">Prerequisites</span></span>

- <span data-ttu-id="b07f4-109">Bir standart veya Geliştirici katmanı Azure Analysis Services sunucusunda.</span><span class="sxs-lookup"><span data-stu-id="b07f4-109">An Azure Analysis Services server at the Standard or Developer tier.</span></span> <span data-ttu-id="b07f4-110">Web Tasarımcısı'nı kullanarak oluşturduğunuz yeni modelleri DirectQuery, bu Katmanlar tarafından desteklenen ' dir.</span><span class="sxs-lookup"><span data-stu-id="b07f4-110">New models created by using the Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="b07f4-111">Bir Azure SQL Database, Azure SQL Data Warehouse veya Power BI Desktop (.pbix) dosyası olarak bir veri kaynağı.</span><span class="sxs-lookup"><span data-stu-id="b07f4-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="b07f4-112">Yeni modelleri veri kaynaklarını Power BI Desktop dosyaları destek Azure SQL Database, Azure SQL Data Warehouse, Oracle ve Teradata oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b07f4-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="b07f4-113">Bir SQL Server hesabı ve Azure SQL Database veya Azure SQL veri ambarı veri kaynaklarına bağlanmak için parola.</span><span class="sxs-lookup"><span data-stu-id="b07f4-113">A SQL Server account and password for connecting to Azure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="to-create-a-new-tabular-model"></a><span data-ttu-id="b07f4-114">Yeni bir tablolu model oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="b07f4-114">To create a new tabular model</span></span>

1. <span data-ttu-id="b07f4-115">Sunucunuzun içinde **genel bakış** dikey > **Web Tasarımcısı**, tıklatın **açık**.</span><span class="sxs-lookup"><span data-stu-id="b07f4-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![Azure portalında bir model oluşturma](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="b07f4-117">İçinde **Web Tasarımcısı** > **modelleri**, tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="b07f4-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Azure portalında bir model oluşturma](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="b07f4-119">İçinde **yeni model**, model adını yazın ve ardından bir veri kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="b07f4-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![Azure portalında yeni model iletişim kutusu](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="b07f4-121">İçinde **Bağlan**, bağlantı özelliklerini girin.</span><span class="sxs-lookup"><span data-stu-id="b07f4-121">In **Connect**, enter the connection properties.</span></span> <span data-ttu-id="b07f4-122">Kullanıcı adı ve parola bir SQL Server hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b07f4-122">Username and password must be a SQL Server account.</span></span>

     ![Azure portalında iletişim Bağlan](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="b07f4-124">İçinde **tabloları ve görünümleri**, modelinize eklemek ve ardından istediğiniz tabloları seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="b07f4-124">In **Tables and views**, select the tables to include in your model, and then click **Create**.</span></span> <span data-ttu-id="b07f4-125">Bir anahtar çifti ile tablolar arasında ilişkiler otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b07f4-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![Tabloları ve görünümleri seçin](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="b07f4-127">Yeni modelinizi tarayıcınızda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b07f4-127">Your new model appears in your browser.</span></span> <span data-ttu-id="b07f4-128">Buradan, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b07f4-128">From here, you can:</span></span>   

- <span data-ttu-id="b07f4-129">Model verileri sorgu alanları Sorgu Tasarımcısı sürüklemek ve filtreleri ekleme.</span><span class="sxs-lookup"><span data-stu-id="b07f4-129">Query model data by dragging fields to the query designer and adding filters.</span></span>
- <span data-ttu-id="b07f4-130">Yeni ölçüleri tablolarda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b07f4-130">Create new measures in tables.</span></span>
- <span data-ttu-id="b07f4-131">Json Düzenleyicisi'ni kullanarak model meta verilerini düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="b07f4-131">Edit model metadata by using the json editor.</span></span>
- <span data-ttu-id="b07f4-132">Model, Visual Studio (SSDT), Power BI Desktop veya Excel'de açın.</span><span class="sxs-lookup"><span data-stu-id="b07f4-132">Open the model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![Tabloları ve görünümleri seçin](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="b07f4-134">Model meta verilerini düzenleyin veya yeni ölçüleri tarayıcınızda oluşturduğunuzda, bu değişiklikleri modelinizi Azure kaydetmeyi.</span><span class="sxs-lookup"><span data-stu-id="b07f4-134">When you edit model metadata or create new measures in your browser, you're saving those changes to your model in Azure.</span></span> <span data-ttu-id="b07f4-135">Ayrıca SSDT, Power BI Desktop veya Excel modelinizde üzerinde çalışıyorsanız, modelinizi eşitlenmemiş elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b07f4-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b07f4-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b07f4-136">Next steps</span></span> 
[<span data-ttu-id="b07f4-137">Veritabanı rolleri ve kullanıcıları yönetme</span><span class="sxs-lookup"><span data-stu-id="b07f4-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="b07f4-138">Excel ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="b07f4-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


