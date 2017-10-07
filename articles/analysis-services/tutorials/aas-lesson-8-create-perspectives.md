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
# <a name="lesson-8-create-perspectives"></a>8. Ders: Perspektif oluşturma

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu derste Internet Sales adlı bir perspektif oluşturacaksınız. Perspektif odaklanmış, işe özgü veya uygulamaya özgü bakış açılarını sağlayan bir modelin görüntülenebilir bir alt kümesini tanımlar. Bir kullanıcı, bir perspektif kullanarak tooa modeli bağlandığında, o perspektifte tanımlanan alanları olarak bunlar yalnızca model nesneleri (tablolar, sütunları, ölçüleri, hiyerarşileri ve KPI'leri) bakın. toolearn daha, fazla [Perspektifler](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).
  
Merhaba bu ders oluşturduğunuz Internet satış perspektif hello DimCustomer tablo nesnesi dışlar. Belirli nesneleri görünümden hariç bir perspektif oluşturduğunuzda, söz konusu nesne hello modelinde hala bulunmaktadır. Ancak bir raporlama istemcisi alan listesinde görünmez. Perspektife eklenip eklenmemelerinden bağımsız olarak, hesaplanmış sütunlar ve ölçüler, dışlanan nesne verilerinden hesaplama yapmaya devam edebilir.  
  
Bu ders Hello amacı toodescribe nasıl toocreate perspektifler ve hello tablolu model yazma araçları ile bilgi edinin. Daha sonra bu modeli tooinclude ek tablolar genişletirseniz, ek Perspektifler toodefine farklı görüşlerini stok ve satış hello modelinin oluşturabilirsiniz.  
  
Bu ders zaman toocomplete tahmini: **beş dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır. Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 7: anahtar performans göstergelerini oluşturma](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Perspektif oluşturma  
  
#### <a name="toocreate-an-internet-sales-perspective"></a>toocreate Internet satış perspektifi  
  
1.  Merhaba tıklatın **modeli** menü > **Perspektifler** > **oluştur ve Yönet**.  
  
2.  Merhaba, **Perspektifler** iletişim kutusu, tıklatın **yeni bir perspektife**.  
  
3.  Merhaba çift **yeni bir perspektife** sütun başlığı ve adlandırın **Internet satış**.  
  
4.  Select hello tüm hello tabloları *dışında* **DimCustomer**.  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    Bir sonraki Ders içinde bu perspektifin hello Çözümle Excel özelliği tootest kullanın. Merhaba DimCustomer tablo dışındaki her bir tablo Hello Excel PivotTable Alan listesini içerir.  

## <a name="whats-next"></a>Sırada ne var?
[9. Ders: Hiyerarşi oluşturma](../tutorials/aas-lesson-9-create-hierarchies.md).
  
  
  
  
