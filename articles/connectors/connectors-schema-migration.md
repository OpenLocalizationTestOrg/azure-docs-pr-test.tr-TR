---
title: "aaaHow toomigrate logic apps tooschema sürüm 2015-08-01-Önizleme | Microsoft Docs"
description: "Logic apps toohello en son şema sürümü kolayca geçirebilirsiniz. Şu adımları izlemeniz yeterlidir."
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
ms.openlocfilehash: c7b42aaec547eddd28b0c649a3c0625047f9f805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a><span data-ttu-id="923e4-104">Nasıl toomigrate logic apps tooschema sürüm 2015-08-01-Önizleme</span><span class="sxs-lookup"><span data-stu-id="923e4-104">How toomigrate logic apps tooschema version 2015-08-01-preview</span></span>
<span data-ttu-id="923e4-105">toomove varolan logic apps toohello yeni şemanızı, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="923e4-105">toomove your existing logic apps toohello new schema, do hello following:</span></span>  

1. <span data-ttu-id="923e4-106">Hello Azure portalda mantıksal uygulamanızı açın</span><span class="sxs-lookup"><span data-stu-id="923e4-106">Open your logic app in hello Azure portal</span></span>  
2. <span data-ttu-id="923e4-107">Şemayı Güncelleştir’e tıklayın:</span><span class="sxs-lookup"><span data-stu-id="923e4-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="923e4-108">![API Icon][step1] </span><span class="sxs-lookup"><span data-stu-id="923e4-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="923e4-109">Merhaba Şemayı Güncelleştir sayfası görüntüler ve hello yeni şemadaki hello iyileştirmeleri hakkında bilgi sağlayan bir bağlantı tooa belge sağlar: ![API simgesi][step2]</span><span class="sxs-lookup"><span data-stu-id="923e4-109">hello Update Schema page displays and provides a link tooa document that provide details on hello improvements in hello new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="923e4-110">Seçtiğinizde, **Şemayı Güncelleştir**, biz otomatik olarak hello geçiş adımlarını çalıştırırız ve hello kod çıkışı sağlar.</span><span class="sxs-lookup"><span data-stu-id="923e4-110">When you select **Update Schema**, we automatically run hello migration steps and provide hello code output for you.</span></span> <span data-ttu-id="923e4-111">Bu tooupdate tanımınızı, ancak kullanır, bu hello özetlendiği gibi iyi kodlama uygulamalarını izlediğinizden emin olun **en iyi uygulamalar** bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="923e4-111">You can use this tooupdate your definition, however, ensure you follow good coding practices such as those outlined in hello **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a><span data-ttu-id="923e4-112">Logic apps toohello en son şema sürümü geçirirken en iyi uygulamalar:</span><span class="sxs-lookup"><span data-stu-id="923e4-112">Best practices when migrating your Logic apps toohello latest schema version:</span></span>
* <span data-ttu-id="923e4-113">Kopya hello geçirilen komut dosyası tooa yeni Logic App - yok üzerine hello eski beklendiği gibi bir sınama ve onaylanan hello geçirilen uygulamanızı tamamlayana kadar çalışır.</span><span class="sxs-lookup"><span data-stu-id="923e4-113">Copy hello migrated script tooa new Logic App - don't overwrite hello old one until you've completed your testing and confirmed hello migrated app works as expected.</span></span>
* <span data-ttu-id="923e4-114">Üretime geçmeden **önce** Mantıksal uygulamanızı test edin</span><span class="sxs-lookup"><span data-stu-id="923e4-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="923e4-115">Geçiş tamamlandıktan sonra Logic apps toouse hello güncelleştirmeye başlayın [yönetilen API'ler](apis-list.md) mümkün olduğunda.</span><span class="sxs-lookup"><span data-stu-id="923e4-115">After migration completes, start updating your Logic apps toouse hello [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="923e4-116">Örneğin, DropBox v1 kullandığınız durumda Dropbox v2 kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="923e4-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="923e4-117">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="923e4-117">What's next</span></span>
* [<span data-ttu-id="923e4-118">Nasıl toomanually geçirmek mantıksal uygulamalarınızı bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="923e4-118">Learn how toomanually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






