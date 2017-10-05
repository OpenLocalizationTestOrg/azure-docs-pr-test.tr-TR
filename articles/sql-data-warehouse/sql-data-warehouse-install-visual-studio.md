---
title: "SQL Data Warehouse için Visual Studio'yu ve SSDT'yi yükleme | Microsoft Docs"
description: "Azure SQL Data Warehouse için Visual Studio'yu ve SQL Server Veri Araçları'nı (SSDT) Yükleme"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: f7023b78c241a7bc8014276cd0bfa455165b42cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="54d16-103">SQL Data Warehouse için Visual Studio ve SSDT yükleme</span><span class="sxs-lookup"><span data-stu-id="54d16-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="54d16-104">SQL Data Warehouse için uygulama geliştirmek için en son sürümünü Visual Studio ile SQL Server veri Araçları (SSDT) en son sürümünü kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="54d16-104">To develop applications for SQL Data Warehouse, we recommend using the most recent version of Visual Studio with the most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="54d16-105">Geriye dönük uyumluluk için SSDT ile Visual Studio 2013 Güncelleştirme 5 de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="54d16-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="54d16-106">Visual Studio'yu SSDT ile kullanmak; sorgu çalıştırmanın yanı sıra, SQL Server Nesne Gezgini'ni kullanarak SQL Data Warehouse'unuzda bulunan tabloları, görünümleri, saklı yordamları ve daha birçok nesneyi görsel olarak araştırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="54d16-106">Using Visual Studio with SSDT will allow you to use the SQL Server Object Explorer to visually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="54d16-107">SQL Data Warehouse, henüz Visual Studio Veritabanı Projelerini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="54d16-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="54d16-108">Bu özellik sonraki bir sürümde eklenecek.</span><span class="sxs-lookup"><span data-stu-id="54d16-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="54d16-109">1. adım: Visual Studio yükleme</span><span class="sxs-lookup"><span data-stu-id="54d16-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="54d16-110">Karşıdan yükleyip Visual Studio'yu yüklemek için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="54d16-110">Follow these links to download and install Visual Studio.</span></span> <span data-ttu-id="54d16-111">Visual Studio 2013 zaten varsa veya sonraki bir sürümü yüklüyse, adım 2'ye atlayabilirsiniz SSDT yükleyin.</span><span class="sxs-lookup"><span data-stu-id="54d16-111">If you already have Visual Studio 2013 or later installed, you can skip to Step 2, install SSDT.</span></span>

1. <span data-ttu-id="54d16-112">[Visual Studio indirme][].</span><span class="sxs-lookup"><span data-stu-id="54d16-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="54d16-113">İzleyin [Visual Studio'yu yükleme] [ Installing Visual Studio] Kılavuzu MSDN'de ve varsayılan yapılandırmaları seçin.</span><span class="sxs-lookup"><span data-stu-id="54d16-113">Follow the [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose the default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="54d16-114">2. Adım: SSDT'yi yükleme</span><span class="sxs-lookup"><span data-stu-id="54d16-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="54d16-115">Visual Studio için SSDT yüklemek üzere aşağıdaki adımları izleyerek Visual Studio'da bir SSDT güncelleştirmesinin olup olmadığını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="54d16-115">To install SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="54d16-116">Visual Studio tıklayın **Araçları** / **Uzantılar ve güncelleştirmeler...**</span><span class="sxs-lookup"><span data-stu-id="54d16-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="54d16-117"> / **Güncelleştirmeleri**</span><span class="sxs-lookup"><span data-stu-id="54d16-117"> / **Updates**</span></span>
2. <span data-ttu-id="54d16-118">**Ürün Güncelleştirmeleri**'ni seçip **Veritabanı araçları için Microsoft SQL Server Güncelleştirmesi** olup olmadığına bakın.</span><span class="sxs-lookup"><span data-stu-id="54d16-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="54d16-119">Güncelleştirme yoksa en son sürümün yüklü olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="54d16-119">If an update is not found, then you should have the latest version installed.</span></span>  <span data-ttu-id="54d16-120">SSDT'nin yüklendiğini doğrulamak **Yardım** / **Microsoft Visual Studio Hakkında**'ya tıklayın ve SQL Server Veri Araçları'nın listede olup olmadığına bakın.</span><span class="sxs-lookup"><span data-stu-id="54d16-120">To confirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in the list.</span></span>  <span data-ttu-id="54d16-121">14.0.60525.0 SSDT'nin en son sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="54d16-121">The latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="54d16-122">Yükleme seçeneğini Visual Studio'dan kullanılabilir durumda değilse, ziyaret edebilirsiniz [SSDT indirme] [ SSDT Download] indirmek ve SSDT'yi el ile yüklemek için sayfa.</span><span class="sxs-lookup"><span data-stu-id="54d16-122">If the option to install is not available from Visual Studio, alternatively you can visit the [SSDT Download][SSDT Download] page to download and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54d16-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54d16-123">Next steps</span></span>
<span data-ttu-id="54d16-124">SSDT'nin en son sürümüne sahip olduğunuza göre hazır [bağlanmak] [ connect] SQL veri ambarı için.</span><span class="sxs-lookup"><span data-stu-id="54d16-124">Now that you have the latest version of SSDT, you are ready to [connect][connect] to your SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
<span data-ttu-id="54d16-125">[Visual Studio indirme]: https://www.visualstudio.com/downloads/</span><span class="sxs-lookup"><span data-stu-id="54d16-125">[Download Visual Studio]: https://www.visualstudio.com/downloads/</span></span>
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
