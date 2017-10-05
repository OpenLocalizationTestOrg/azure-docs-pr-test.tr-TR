---
title: "Mantıksal uygulamaları 2015-08-01-önizleme şema sürümüne geçirme | Microsoft Belgeleri"
description: "Mantıksal uygulamalarınızı en son şema sürümüne kolayca geçirebilirsiniz. Şu adımları izlemeniz yeterlidir."
services: logic-apps
documentationcenter: 
author: MSFTMAN
manager: erikre
editor: 
tags: connectors
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: a5a73a9f124e5339b61dbc49021444a208a471f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-logic-apps-to-schema-version-2015-08-01-preview"></a><span data-ttu-id="0e026-104">Mantıksal uygulamaları şema sürümü 2015-08-01-önizlemeye geçirme</span><span class="sxs-lookup"><span data-stu-id="0e026-104">How to migrate logic apps to schema version 2015-08-01-preview</span></span>
<span data-ttu-id="0e026-105">Mevcut mantıksal uygulamalarınızı yeni şemaya taşımak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="0e026-105">To move your existing logic apps to the new schema, do the following:</span></span>  

1. <span data-ttu-id="0e026-106">Azure portalda mantıksal uygulamanızı açın</span><span class="sxs-lookup"><span data-stu-id="0e026-106">Open your logic app in the Azure portal</span></span>  
2. <span data-ttu-id="0e026-107">Şemayı Güncelleştir’e tıklayın:</span><span class="sxs-lookup"><span data-stu-id="0e026-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="0e026-108">![API Icon][step1] </span><span class="sxs-lookup"><span data-stu-id="0e026-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="0e026-109">Şemayı Güncelleştir sayfası, yeni şemadaki geliştirmelerin ayrıntılarını sağlayan bir belgeyi görüntüler ve buna ilişkin bir bağlantı sağlar: ![API Icon][step2]</span><span class="sxs-lookup"><span data-stu-id="0e026-109">The Update Schema page displays and provides a link to a document that provide details on the improvements in the new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="0e026-110">**Şemayı Güncelleştir**’i seçtiğinizde, otomatik olarak geçiş adımlarını çalıştırırız ve size kod çıkışı sağlarız.</span><span class="sxs-lookup"><span data-stu-id="0e026-110">When you select **Update Schema**, we automatically run the migration steps and provide the code output for you.</span></span> <span data-ttu-id="0e026-111">Bunu tanımınızı güncelleştirmek için kullanabilirsiniz, ancak aşağıda **En İyi Uygulamalar** bölümünde belirtilenler gibi iyi kodlama uygulamalarını izlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="0e026-111">You can use this to update your definition, however, ensure you follow good coding practices such as those outlined in the **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-to-the-latest-schema-version"></a><span data-ttu-id="0e026-112">Mantıksal uygulamalarınızı en son şema sürümüne geçirirken en iyi uygulamalar:</span><span class="sxs-lookup"><span data-stu-id="0e026-112">Best practices when migrating your Logic apps to the latest schema version:</span></span>
* <span data-ttu-id="0e026-113">Geçirilen betiği yeni Mantıksal Uygulamaya kopyalayın; testinizi tamamlayıncaya ve geçirilen uygulamalarının beklendiği gibi çalıştığını onaylayıncaya kadar eskisinin üzerine yazmayın.</span><span class="sxs-lookup"><span data-stu-id="0e026-113">Copy the migrated script to a new Logic App - don't overwrite the old one until you've completed your testing and confirmed the migrated app works as expected.</span></span>
* <span data-ttu-id="0e026-114">Üretime geçmeden **önce** Mantıksal uygulamanızı test edin</span><span class="sxs-lookup"><span data-stu-id="0e026-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="0e026-115">Geçiş işlemi tamamlandığında, mümkün olduğunda [yönetilen API’leri](apis-list.md) kullanmak için Mantıksal uygulamalarınızı güncelleştirmeye başlayın.</span><span class="sxs-lookup"><span data-stu-id="0e026-115">After migration completes, start updating your Logic apps to use the [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="0e026-116">Örneğin, DropBox v1 kullandığınız durumda Dropbox v2 kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e026-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="0e026-117">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="0e026-117">What's next</span></span>
* [<span data-ttu-id="0e026-118">Mantıksal uygulamalarınızı el ile geçirmeyi öğrenme</span><span class="sxs-lookup"><span data-stu-id="0e026-118">Learn how to manually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






