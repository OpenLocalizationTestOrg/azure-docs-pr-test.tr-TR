---
title: "aaaInstall Visual Studio ve SSDT SQL Data Warehouse için | Microsoft Docs"
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
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="ea1c4-103">SQL Data Warehouse için Visual Studio ve SSDT yükleme</span><span class="sxs-lookup"><span data-stu-id="ea1c4-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="ea1c4-104">toodevelop uygulamalar SQL Data Warehouse için Visual Studio en son sürümünü hello hello en son sürümü SQL Server veri Araçları (SSDT) ile kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-104">toodevelop applications for SQL Data Warehouse, we recommend using hello most recent version of Visual Studio with hello most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="ea1c4-105">Geriye dönük uyumluluk için SSDT ile Visual Studio 2013 Güncelleştirme 5 de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="ea1c4-106">SSDT ile Visual Studio kullanarak etmenizi sağlar toouse hello SQL Server Nesne Gezgini toovisually tabloları, görünümleri, saklı yordamları ve daha birçok nesneyi SQL veri ambarı keşfedin yanı sıra sorgular çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-106">Using Visual Studio with SSDT will allow you toouse hello SQL Server Object Explorer toovisually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="ea1c4-107">SQL Data Warehouse, henüz Visual Studio Veritabanı Projelerini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="ea1c4-108">Bu özellik sonraki bir sürümde eklenecek.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="ea1c4-109">1. adım: Visual Studio yükleme</span><span class="sxs-lookup"><span data-stu-id="ea1c4-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="ea1c4-110">Bu bağlantılar toodownload izleyin ve Visual Studio yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-110">Follow these links toodownload and install Visual Studio.</span></span> <span data-ttu-id="ea1c4-111">Zaten Visual Studio 2013 veya sonraki bir sürümü yüklü olduğunda tooStep 2 Atla, SSDT'yi yükleme.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-111">If you already have Visual Studio 2013 or later installed, you can skip tooStep 2, install SSDT.</span></span>

1. <span data-ttu-id="ea1c4-112">[Visual Studio indirme][].</span><span class="sxs-lookup"><span data-stu-id="ea1c4-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="ea1c4-113">Merhaba izleyin [Visual Studio'yu yükleme] [ Installing Visual Studio] Kılavuzu MSDN'de ve hello varsayılan yapılandırmaları seçin.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-113">Follow hello [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose hello default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="ea1c4-114">2. Adım: SSDT'yi yükleme</span><span class="sxs-lookup"><span data-stu-id="ea1c4-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="ea1c4-115">Visual Studio için SSDT tooinstall işaretlemeniz yeterli Visual Studio'da bir SSDT güncelleştirmesinin için aşağıdaki adımları izleyerek.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-115">tooinstall SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="ea1c4-116">Visual Studio tıklayın **Araçları** / **Uzantılar ve güncelleştirmeler...**</span><span class="sxs-lookup"><span data-stu-id="ea1c4-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="ea1c4-117"> / **Güncelleştirmeleri**</span><span class="sxs-lookup"><span data-stu-id="ea1c4-117"> / **Updates**</span></span>
2. <span data-ttu-id="ea1c4-118">**Ürün Güncelleştirmeleri**'ni seçip **Veritabanı araçları için Microsoft SQL Server Güncelleştirmesi** olup olmadığına bakın.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="ea1c4-119">Bir güncelleştirme bulunmazsa, hello en son sürümü yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-119">If an update is not found, then you should have hello latest version installed.</span></span>  <span data-ttu-id="ea1c4-120">tooconfirm SSDT yüklü tıklayın **yardımcı** / **Microsoft Visual Studio hakkında** ve SQL Server veri araçları için hello listede olup olmadığına bakın.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-120">tooconfirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in hello list.</span></span>  <span data-ttu-id="ea1c4-121">14.0.60525.0 SSDT'nin en son sürümüne Hello olur.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-121">hello latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="ea1c4-122">Alternatif olarak Hello seçeneği tooinstall Visual Studio'dan kullanılabilir durumda değilse, hello ziyaret edebilirsiniz [SSDT indirme] [ SSDT Download] sayfasında toodownload ve SSDT'yi el ile yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-122">If hello option tooinstall is not available from Visual Studio, alternatively you can visit hello [SSDT Download][SSDT Download] page toodownload and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea1c4-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea1c4-123">Next steps</span></span>
<span data-ttu-id="ea1c4-124">Merhaba SSDT'nin en son sürümüne sahip olduğunuza göre çok hazır olduğunuz[bağlanmak] [ connect] tooyour SQL veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="ea1c4-124">Now that you have hello latest version of SSDT, you are ready too[connect][connect] tooyour SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Visual Studio indirme]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
