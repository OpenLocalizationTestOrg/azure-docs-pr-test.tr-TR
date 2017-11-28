---
title: "aaaCreate hello Azure Analysis Services Web Tasarımcısı kullanarak tablolu model | Microsoft Docs"
description: "Nasıl toocreate kullanarak bir Azure Analysis Services tablolu model hello Azure portalında Web Tasarımcısı hakkında bilgi edinin."
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
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="bf83f-103">Azure portalında bir model oluşturma</span><span class="sxs-lookup"><span data-stu-id="bf83f-103">Create a model in Azure portal</span></span>

<span data-ttu-id="bf83f-104">Hello Azure Analysis Services web Tasarımcısı (Önizleme) Özelliği Azure portalında hızlı ve kolay bir şekilde toocreate sağlar ve tablolu modeller ve sorgu modelini veri sağ tarayıcınızda düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="bf83f-104">hello Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way toocreate and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="bf83f-105">Unutmayın, hello web Designer **Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="bf83f-105">Keep in mind, hello web designer is **preview**.</span></span> <span data-ttu-id="bf83f-106">Yeni işlevselliği Önizleme, tüm başlangıç saatinin eklenen sırada işlevselliği sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="bf83f-106">While new functionality is being added all hello time, in preview, functionality is limited.</span></span> <span data-ttu-id="bf83f-107">Daha gelişmiş modeli geliştirme ve test amacıyla, bu en iyi toouse Visual Studio (SSDT) ve SQL Server Management Studio (SSMS) olur.</span><span class="sxs-lookup"><span data-stu-id="bf83f-107">For more advanced model development and testing, it's best toouse Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf83f-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bf83f-108">Prerequisites</span></span>

- <span data-ttu-id="bf83f-109">Bir hello standart veya Geliştirici katmanı Azure Analysis Services sunucusunda.</span><span class="sxs-lookup"><span data-stu-id="bf83f-109">An Azure Analysis Services server at hello Standard or Developer tier.</span></span> <span data-ttu-id="bf83f-110">Merhaba Web Tasarımcısı kullanılarak oluşturulan yeni modelleri DirectQuery, bu Katmanlar tarafından desteklenen ' dir.</span><span class="sxs-lookup"><span data-stu-id="bf83f-110">New models created by using hello Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="bf83f-111">Bir Azure SQL Database, Azure SQL Data Warehouse veya Power BI Desktop (.pbix) dosyası olarak bir veri kaynağı.</span><span class="sxs-lookup"><span data-stu-id="bf83f-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="bf83f-112">Yeni modelleri veri kaynaklarını Power BI Desktop dosyaları destek Azure SQL Database, Azure SQL Data Warehouse, Oracle ve Teradata oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bf83f-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="bf83f-113">Bir SQL Server hesabı ve tooAzure SQL veritabanına veya Azure SQL veri ambarı veri kaynaklarına bağlanmak için parola.</span><span class="sxs-lookup"><span data-stu-id="bf83f-113">A SQL Server account and password for connecting tooAzure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="toocreate-a-new-tabular-model"></a><span data-ttu-id="bf83f-114">Yeni bir tablolu model toocreate</span><span class="sxs-lookup"><span data-stu-id="bf83f-114">toocreate a new tabular model</span></span>

1. <span data-ttu-id="bf83f-115">Sunucunuzun içinde **genel bakış** dikey > **Web Tasarımcısı**, tıklatın **açık**.</span><span class="sxs-lookup"><span data-stu-id="bf83f-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![Azure portalında bir model oluşturma](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="bf83f-117">İçinde **Web Tasarımcısı** > **modelleri**, tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="bf83f-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Azure portalında bir model oluşturma](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="bf83f-119">İçinde **yeni model**, model adını yazın ve ardından bir veri kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="bf83f-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![Azure portalında yeni model iletişim kutusu](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="bf83f-121">İçinde **Bağlan**, hello bağlantı özelliklerini girin.</span><span class="sxs-lookup"><span data-stu-id="bf83f-121">In **Connect**, enter hello connection properties.</span></span> <span data-ttu-id="bf83f-122">Kullanıcı adı ve parola bir SQL Server hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf83f-122">Username and password must be a SQL Server account.</span></span>

     ![Azure portalında iletişim Bağlan](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="bf83f-124">İçinde **tabloları ve görünümleri**modelinizde hello tabloları tooinclude seçin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="bf83f-124">In **Tables and views**, select hello tables tooinclude in your model, and then click **Create**.</span></span> <span data-ttu-id="bf83f-125">Bir anahtar çifti ile tablolar arasında ilişkiler otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bf83f-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![Tabloları ve görünümleri seçin](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="bf83f-127">Yeni modelinizi tarayıcınızda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bf83f-127">Your new model appears in your browser.</span></span> <span data-ttu-id="bf83f-128">Buradan, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bf83f-128">From here, you can:</span></span>   

- <span data-ttu-id="bf83f-129">Model veri alanları toohello Sorgu Tasarımcısı sürükleme ve filtreler ekleyerek sorgu.</span><span class="sxs-lookup"><span data-stu-id="bf83f-129">Query model data by dragging fields toohello query designer and adding filters.</span></span>
- <span data-ttu-id="bf83f-130">Yeni ölçüleri tablolarda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bf83f-130">Create new measures in tables.</span></span>
- <span data-ttu-id="bf83f-131">Merhaba json Düzenleyicisi'ni kullanarak model meta verilerini düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="bf83f-131">Edit model metadata by using hello json editor.</span></span>
- <span data-ttu-id="bf83f-132">Merhaba modeli, Visual Studio (SSDT), Power BI Desktop veya Excel'de açın.</span><span class="sxs-lookup"><span data-stu-id="bf83f-132">Open hello model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![Tabloları ve görünümleri seçin](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="bf83f-134">Model meta verilerini düzenleyin veya yeni ölçüleri tarayıcınızda oluşturduğunuzda, bu değişiklikleri tooyour modeli Azure'da kaydediyorsanız.</span><span class="sxs-lookup"><span data-stu-id="bf83f-134">When you edit model metadata or create new measures in your browser, you're saving those changes tooyour model in Azure.</span></span> <span data-ttu-id="bf83f-135">Ayrıca SSDT, Power BI Desktop veya Excel modelinizde üzerinde çalışıyorsanız, modelinizi eşitlenmemiş elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf83f-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bf83f-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bf83f-136">Next steps</span></span> 
[<span data-ttu-id="bf83f-137">Veritabanı rolleri ve kullanıcıları yönetme</span><span class="sxs-lookup"><span data-stu-id="bf83f-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="bf83f-138">Excel ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="bf83f-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


