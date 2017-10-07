---
title: "aaaHow tooview ilgili Azure veri Kataloğu veri varlıklarını | Microsoft Docs"
description: "Bu makalede tooview seçilen veri varlığını Azure veri Kataloğu'nda, veri varlıklarını nasıl ilişkilendirileceğini açıklar."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a>Azure veri Kataloğu veri varlıklarını tooview ilişkisini?
Azure veri Kataloğu tooview veri varlıklarını Seçili ilgili tooa veri varlık ve görünüm aralarındaki ilişkilerin sağlar. 

## <a name="supported-data-sources"></a>Desteklenen veri kaynakları 
Veri kaynakları aşağıdaki hello veri varlıklarından kaydolduğunuzda, Azure veri Kataloğu seçili hello veri varlıklarını birleştirme ilişkilerini hakkındaki meta verileri otomatik olarak kaydeder. 

- SQL Server
- Azure SQL Database
- MySQL
- Oracle

## <a name="view-related-data-assets"></a>İlgili veri varlıklarını görüntülemek
Seçili ilgili tooa dataset olan tooview veri varlıklarını kullanmak hello **ilişkileri** sekmesinde hello görüntü aşağıdaki gösterildiği gibi: 

![Azure veri Kataloğu - veri varlıklarını ilgili görüntüleyin](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

Bu örnekte, seçili Merhaba için iki ilişkisi vardır **ProductSubcategory** veri varlığına: 

- Merhaba ürün tablosunun ProductSubcategoryID sütunu seçili hello ProductSubcategory tablosunun ProductSubcategoryID sütunla yabancı anahtar ilişkisi vardır. 
- Merhaba ProductSubCategory tablosunun ProductCategoryID sütunu seçili hello ProductCategory tablosunun ProductCategoryID sütunla yabancı anahtar ilişkisi vardır.

> [!NOTE]
> Merhaba ok hello ilişkileri ağaç görünümünde Hello yönünü dikkat edin.  

toosee hello sütunun hello tam adı gibi daha fazla ayrıntı hello fare üzerine getirin ve görüntü aşağıdaki açılan benzer toohello bakın: 

![Azure veri Kataloğu - ilişki açılan](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

önceden kaydedilmiş olan varlıklar arasındaki ilişkiler tooinclude, bu varlıkları yeniden kaydedin.

## <a name="next-steps"></a>Sonraki adımlar
- [Nasıl toomanage veri varlıklarını](data-catalog-how-to-manage.md)
