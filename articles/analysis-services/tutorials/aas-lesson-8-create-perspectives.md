---
title: "aaa \"Azure Analysis Services öğretici Ders 8 oluşturma Perspektifler | Microsoft Docs\""
description: "Öğretici Azure Analysis Services projesi toocreate açılardan nasıl hello açıklar."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="46524-103">8. Ders: Perspektif oluşturma</span><span class="sxs-lookup"><span data-stu-id="46524-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="46524-104">Bu derste Internet Sales adlı bir perspektif oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="46524-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="46524-105">Perspektif odaklanmış, işe özgü veya uygulamaya özgü bakış açılarını sağlayan bir modelin görüntülenebilir bir alt kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="46524-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="46524-106">Bir kullanıcı, bir perspektif kullanarak tooa modeli bağlandığında, o perspektifte tanımlanan alanları olarak bunlar yalnızca model nesneleri (tablolar, sütunları, ölçüleri, hiyerarşileri ve KPI'leri) bakın.</span><span class="sxs-lookup"><span data-stu-id="46524-106">When a user connects tooa model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="46524-107">toolearn daha, fazla [Perspektifler](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="46524-107">toolearn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="46524-108">Merhaba bu ders oluşturduğunuz Internet satış perspektif hello DimCustomer tablo nesnesi dışlar.</span><span class="sxs-lookup"><span data-stu-id="46524-108">hello Internet Sales perspective you create in this lesson excludes hello DimCustomer table object.</span></span> <span data-ttu-id="46524-109">Belirli nesneleri görünümden hariç bir perspektif oluşturduğunuzda, söz konusu nesne hello modelinde hala bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="46524-109">When you create a perspective that excludes certain objects from view, that object still exists in hello model.</span></span> <span data-ttu-id="46524-110">Ancak bir raporlama istemcisi alan listesinde görünmez.</span><span class="sxs-lookup"><span data-stu-id="46524-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="46524-111">Perspektife eklenip eklenmemelerinden bağımsız olarak, hesaplanmış sütunlar ve ölçüler, dışlanan nesne verilerinden hesaplama yapmaya devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="46524-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="46524-112">Bu ders Hello amacı toodescribe nasıl toocreate perspektifler ve hello tablolu model yazma araçları ile bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="46524-112">hello purpose of this lesson is toodescribe how toocreate perspectives and become familiar with hello tabular model authoring tools.</span></span> <span data-ttu-id="46524-113">Daha sonra bu modeli tooinclude ek tablolar genişletirseniz, ek Perspektifler toodefine farklı görüşlerini stok ve satış hello modelinin oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46524-113">If you later expand this model tooinclude additional tables, you can create additional perspectives toodefine different viewpoints of hello model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="46524-114">Bu ders zaman toocomplete tahmini: **beş dakika**</span><span class="sxs-lookup"><span data-stu-id="46524-114">Estimated time toocomplete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="46524-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="46524-115">Prerequisites</span></span>  
<span data-ttu-id="46524-116">Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="46524-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="46524-117">Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 7: anahtar performans göstergelerini oluşturma](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="46524-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="46524-118">Perspektif oluşturma</span><span class="sxs-lookup"><span data-stu-id="46524-118">Create perspectives</span></span>  
  
#### <a name="toocreate-an-internet-sales-perspective"></a><span data-ttu-id="46524-119">toocreate Internet satış perspektifi</span><span class="sxs-lookup"><span data-stu-id="46524-119">toocreate an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="46524-120">Merhaba tıklatın **modeli** menü > **Perspektifler** > **oluştur ve Yönet**.</span><span class="sxs-lookup"><span data-stu-id="46524-120">Click hello **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="46524-121">Merhaba, **Perspektifler** iletişim kutusu, tıklatın **yeni bir perspektife**.</span><span class="sxs-lookup"><span data-stu-id="46524-121">In hello **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="46524-122">Merhaba çift **yeni bir perspektife** sütun başlığı ve adlandırın **Internet satış**.</span><span class="sxs-lookup"><span data-stu-id="46524-122">Double-click hello **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="46524-123">Select hello tüm hello tabloları *dışında* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="46524-123">Select hello all hello tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="46524-125">Bir sonraki Ders içinde bu perspektifin hello Çözümle Excel özelliği tootest kullanın.</span><span class="sxs-lookup"><span data-stu-id="46524-125">In a later lesson, you use hello Analyze in Excel feature tootest this perspective.</span></span> <span data-ttu-id="46524-126">Merhaba DimCustomer tablo dışındaki her bir tablo Hello Excel PivotTable Alan listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="46524-126">hello Excel PivotTable Fields List includes each table except hello DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="46524-127">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="46524-127">What's next?</span></span>
<span data-ttu-id="46524-128">[9. Ders: Hiyerarşi oluşturma](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="46524-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
