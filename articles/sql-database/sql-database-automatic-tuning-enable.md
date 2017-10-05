---
title: "Azure SQL veritabanı için otomatik olarak ayarlamayı etkinleştirmek | Microsoft Docs"
description: "Otomatik Azure SQL veritabanınızda kolayca ayarlama etkinleştirebilirsiniz."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: b391b1f7aa37c5a06fc320ce892534187deb4959
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="edee3-103">Otomatik ayarlamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="edee3-103">Enable automatic tuning</span></span>

<span data-ttu-id="edee3-104">Azure SQL veritabanı sürekli sorgularınızı izler ve İş yükünüzün performansını iyileştirmek için yapabileceğiniz eylemi tanımlayan bir otomatik olarak yönetilen veri hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="edee3-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies the action that you can perform to improve performance of your workload.</span></span> <span data-ttu-id="edee3-105">Önerileri gözden geçirin ve el ile uygulamadan veya için otomatik olarak düzeltme eylemleri uygulamak Azure SQL veritabanı sağlar - bu olarak bilinir **otomatik ayarlama modu**.</span><span class="sxs-lookup"><span data-stu-id="edee3-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="edee3-106">Otomatik ayarlama sunucu veya veritabanı düzeyinde etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="edee3-106">Automatic tuning can be enabled at the server or the database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="edee3-107">Otomatik sunucu üzerinde ayarlama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="edee3-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="edee3-108">Azure SQL veritabanı sunucusuna otomatik olarak ayarlamayı etkinleştirmek için Azure portalında sunucusuna gidin ve ardından **otomatik ayarlama** menüde.</span><span class="sxs-lookup"><span data-stu-id="edee3-108">To enable automatic tuning on Azure SQL Database server, navigate to the server in Azure portal and then select **Automatic tuning** in the menu.</span></span> <span data-ttu-id="edee3-109">İstediğiniz etkinleştirmek ve seçmek için otomatik ayarlama seçenekleri seçin **Uygula**:</span><span class="sxs-lookup"><span data-stu-id="edee3-109">Select the automatic tuning options you want to enable and select **Apply**:</span></span>

![Sunucu](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="edee3-111">Sunucuda otomatik ayarlama seçenekleri, sunucudaki tüm veritabanları için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="edee3-111">Automatic tuning options on server are applied to all databases on the server.</span></span> <span data-ttu-id="edee3-112">Varsayılan olarak, tüm veritabanları, kendi üst sunucusundan yapılandırmasını devralmak, ancak bu kullanılabilir geçersiz kılındı ve tek tek her veritabanı için belirtilen.</span><span class="sxs-lookup"><span data-stu-id="edee3-112">By default, all databases inherit the configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="edee3-113">Otomatik veritabanı ayarlama yapılandırın</span><span class="sxs-lookup"><span data-stu-id="edee3-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="edee3-114">Azure portalı ayrı ayrı her veritabanını ayarlama yapılandırmasını otomatik belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="edee3-114">The Azure portal enables you to individually specify the automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="edee3-115">Aynı yapılandırma ayarları her veritabanı üzerinde otomatik olarak uygulanabilir şekilde otomatik ayarlama yapılandırma sunucusu düzeyinde yönetmek için genel yüklenmemesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="edee3-115">The general recommendation is to manage the automatic tuning configuration at server level so the same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="edee3-116">Veritabanı farklı ise tek bir veritabanının üzerine otomatik ayarlama başkalarının aynı sunucuda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="edee3-116">Configure automatic tuning on an individual database if the database is different that others on the same server.</span></span>
>

<span data-ttu-id="edee3-117">Otomatik üzerinde tek bir veritabanı ayarlamayı etkinleştirmek için Azure portalında veritabanına gidin ve sonra hem de seçin **otomatik ayarlama**.</span><span class="sxs-lookup"><span data-stu-id="edee3-117">To enable automatic tuning on a single database, navigate to the database in the Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="edee3-118">Onay kutusunu seçerek veritabanından ayarları devralmak için tek bir veritabanı yapılandırabilir veya yapılandırma veritabanı için ayrı ayrı belirtin.</span><span class="sxs-lookup"><span data-stu-id="edee3-118">You can configure a single database to inherit the settings from the database by selecting the checkbox or you can specify the configuration for a database individually.</span></span>

![Database](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="edee3-120">Uygun yapılandırma seçtikten sonra tıklatın **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="edee3-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edee3-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="edee3-121">Next steps</span></span>
* <span data-ttu-id="edee3-122">Okuma [otomatik ayarlama makale](sql-database-automatic-tuning.md) nasıl performansınızı geliştirmenize yardımcı olabilir ve otomatik ayarlama hakkında daha fazla bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="edee3-122">Read the [Automatic tuning article](sql-database-automatic-tuning.md) to learn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="edee3-123">Bkz: [performans önerileri](sql-database-advisor.md) Azure SQL veritabanı performans önerileri genel bakış.</span><span class="sxs-lookup"><span data-stu-id="edee3-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="edee3-124">Bkz: [sorgu performansı öngörüleri](sql-database-query-performance.md) üst sorgularınızı performans etkisini görüntüleme hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="edee3-124">See [Query Performance Insights](sql-database-query-performance.md) to learn about viewing the performance impact of your top queries.</span></span>
