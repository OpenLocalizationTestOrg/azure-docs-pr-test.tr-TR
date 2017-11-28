---
title: "Azure SQL veritabanı için ayarlama otomatik aaaEnable | Microsoft Docs"
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
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="e849b-103">Otomatik ayarlamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e849b-103">Enable automatic tuning</span></span>

<span data-ttu-id="e849b-104">Azure SQL veritabanı sürekli sorgularınızı izler ve İş yükünüzün performansını tooimprove gerçekleştirebileceğiniz hello işlem tanımlayan bir otomatik olarak yönetilen veri hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="e849b-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies hello action that you can perform tooimprove performance of your workload.</span></span> <span data-ttu-id="e849b-105">Önerileri gözden geçirin ve el ile uygulamadan veya için otomatik olarak düzeltme eylemleri uygulamak Azure SQL veritabanı sağlar - bu olarak bilinir **otomatik ayarlama modu**.</span><span class="sxs-lookup"><span data-stu-id="e849b-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="e849b-106">Otomatik ayarlama hello sunucu veya hello veritabanı düzeyinde etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e849b-106">Automatic tuning can be enabled at hello server or hello database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="e849b-107">Otomatik sunucu üzerinde ayarlama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="e849b-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="e849b-108">tooenable otomatik Azure portal ve ardından toohello Server'da gidin Azure SQL veritabanı sunucusunda ayarlama **otomatik ayarlama** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e849b-108">tooenable automatic tuning on Azure SQL Database server, navigate toohello server in Azure portal and then select **Automatic tuning** in hello menu.</span></span> <span data-ttu-id="e849b-109">Select hello tooenable istediğiniz ve seçin otomatik ayarlama seçenekleri **Uygula**:</span><span class="sxs-lookup"><span data-stu-id="e849b-109">Select hello automatic tuning options you want tooenable and select **Apply**:</span></span>

![Sunucu](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="e849b-111">Merhaba sunucudaki uygulanan tooall veritabanları sunucusunda seçeneklerini ayarlama otomatik olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="e849b-111">Automatic tuning options on server are applied tooall databases on hello server.</span></span> <span data-ttu-id="e849b-112">Varsayılan olarak, tüm veritabanları, kendi üst sunucusundan hello yapılandırmasını devralmak, ancak bu kullanılabilir geçersiz kılındı ve tek tek her veritabanı için belirtilen.</span><span class="sxs-lookup"><span data-stu-id="e849b-112">By default, all databases inherit hello configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="e849b-113">Otomatik veritabanı ayarlama yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e849b-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="e849b-114">Merhaba, tooindividually belirtin hello otomatik ayarlama yapılandırma her veritabanını Azure portal sağlar.</span><span class="sxs-lookup"><span data-stu-id="e849b-114">hello Azure portal enables you tooindividually specify hello automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="e849b-115">Merhaba genel öneri yapılandırmadır toomanage hello otomatik ayarlama sunucu düzeyinde aynı yapılandırma ayarları uygulanabilir her veritabanı üzerinde otomatik olarak bunu hello.</span><span class="sxs-lookup"><span data-stu-id="e849b-115">hello general recommendation is toomanage hello automatic tuning configuration at server level so hello same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="e849b-116">Merhaba veritabanı bazılarında aynı sunucu hello farklı ise tek bir veritabanının üzerine otomatik ayarlama yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e849b-116">Configure automatic tuning on an individual database if hello database is different that others on hello same server.</span></span>
>

<span data-ttu-id="e849b-117">tek bir veritabanı üzerinde ayarlama otomatik tooenable toohello veritabanında hello Azure portal gidin ve sonra hem de seçin **otomatik ayarlama**.</span><span class="sxs-lookup"><span data-stu-id="e849b-117">tooenable automatic tuning on a single database, navigate toohello database in hello Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="e849b-118">Ayrı ayrı bir veritabanı için başlangıç yapılandırması belirtin veya hello onay kutusunu seçerek hello veritabanından tek veritabanı tooinherit hello ayarlarını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e849b-118">You can configure a single database tooinherit hello settings from hello database by selecting hello checkbox or you can specify hello configuration for a database individually.</span></span>

![Database](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="e849b-120">Uygun yapılandırma seçtikten sonra tıklatın **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="e849b-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e849b-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e849b-121">Next steps</span></span>
* <span data-ttu-id="e849b-122">Okuma hello [otomatik ayarlama makale](sql-database-automatic-tuning.md) toolearn nasıl performansınızı geliştirmenize yardımcı olabilir ve otomatik ayarlama hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="e849b-122">Read hello [Automatic tuning article](sql-database-automatic-tuning.md) toolearn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="e849b-123">Bkz: [performans önerileri](sql-database-advisor.md) Azure SQL veritabanı performans önerileri genel bakış.</span><span class="sxs-lookup"><span data-stu-id="e849b-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="e849b-124">Bkz: [sorgu performansı öngörüleri](sql-database-query-performance.md) üst sorgularınızı hello performans etkisini görüntüleme hakkında toolearn.</span><span class="sxs-lookup"><span data-stu-id="e849b-124">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>
