---
title: "Hello Azure CDN kurallar altyapısı kullanarak aaaOverride HTTP davranışı | Microsoft Docs"
description: "HTTP üstbilgileri değiştirmek ve önbellek ilkesi tanımlayın veya Hello kurallar altyapısı belirli içerik türlerini hello teslimini engelleme gibi HTTP isteklerini Azure CDN tarafından nasıl işleneceğini toocustomize sağlar."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a>Hello Azure CDN kurallar altyapısı kullanarak HTTP davranışı geçersiz kılma
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Genel Bakış
Merhaba kurallar altyapısı HTTP isteklerini, belirli türde bir içerik hello teslimini engelleme, önbellek ilkesi tanımlama ve HTTP üstbilgileri değiştirme gibi işlenme toocustomize sağlar.  Bu öğretici bir kural oluşturma önbelleğe alma davranışı CDN varlıklarını hello değiştirecek gösterilmektedir.  Ayrıca video içeriği hello kullanılabilir yok "[Ayrıca bkz.](#see-also)" bölümü.

   > [!TIP] 
   > Ayrıntılı bir başvuru toohello sözdizimi için bkz: [kuralları altyapısı başvurusu](cdn-rules-engine-reference.md).
   > 


## <a name="tutorial"></a>Öğretici
1. Merhaba CDN profili dikey penceresinden hello tıklayın **Yönet** düğmesi.
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    Merhaba CDN Yönetim Portalı açar.
2. Tıklatın hello üzerinde **HTTP büyük** sekmesini ve ardından, **kurallar altyapısı**.
   
    Yeni bir kural için seçenekler görüntülenir.
   
    ![CDN yeni kural seçenekleri](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > içinde birden çok kural listelenen hello sırasını nasıl işlendiğini etkiler. Bir sonraki kural önceki bir kural tarafından belirtilen hello Eylemler geçersiz kılabilir.
   > 
   > 
3. Hello bir ad girin **adı / açıklaması** metin kutusu.
4. Merhaba kuralın uygulanacağı istekleri Hello türünü tanımlayın.  Varsayılan olarak, hello **her zaman** eşleşme koşul seçilidir.  Kullanacağınız **her zaman** Bu öğretici için bu nedenle, seçili bırakın.
   
   ![CDN eşleşme koşulu](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > Koşullar hello açılır menüde kullanılabilir türlerde eşleşme vardır.  Merhaba mavi Bilgi simgesi toohello üzerinde tıklatarak hello eşleşme koşul solundaki şu anda seçili hello koşul ayrıntılı anlatılmıştır.
   > 
   >  Merhaba tam listesi için ayrıntılı koşullu ifadeler için bkz [kurallar altyapısı koşullu ifadeler](cdn-rules-engine-reference-match-conditions.md).
   >  
   > Hello tam listesi ayrıntılı eşleşme koşulları için bkz: [kurallar altyapısı eşleşen koşullar](cdn-rules-engine-reference-match-conditions.md).
   > 
   > 
5. Merhaba tıklatın  **+**  sonraki çok düğmesini**özellikleri** tooadd yeni bir özellik.  Merhaba soldaki Hello açılır menüde seçin **zorla iç Max-Age**.  Görüntülenen hello metin kutusuna girin **300**.  Varsayılan değerleri kalan hello bırakın.
   
   ![CDN özelliği](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > Eşleşme koşullarla hello mavi Bilgi simgesi toohello tıklatarak Merhaba yeni bıraktığınız özelliği bu özellik hakkındaki ayrıntıları görüntüler.  Merhaba durumda **zorla iç Max-Age**, biz hello varlığın geçersiz kılma **Cache-Control** ve **Expires** hello CDN kenar düğümüne hello yenilediğinizde üstbilgileri toocontrol Varlık hello kaynaktan.  Bizim örneğimizde, 300 saniye hello CDN kenar düğümüne hello varlık hello varlık kendi kaynaktan yenileme önce 5 dakika için önbelleğe anlamına gelir.
   > 
   > Merhaba özelliklerin tam listesini ayrıntılı için bkz: [kurallar altyapısı özellik ayrıntıları](cdn-rules-engine-reference-features.md).
   > 
   > 
6. Merhaba tıklatın **Ekle** düğmesini toosave hello yeni kural.  Merhaba yeni kural artık onayını bekliyor. Bunu onaylandıktan sonra hello durum değiştirilecek **bekleyen XML** çok**etkin XML**.
   
   > [!IMPORTANT]
   > Kuralları değişikliklerin too90 dakika toopropagate hello CDN aracılığıyla yukarı alabilir.
   > 
   > 

## <a name="see-also"></a>Ayrıca bkz.
* [Azure CDN'ye genel bakış](cdn-overview.md)
* [Kuralları altyapısı başvurusu](cdn-rules-engine-reference.md)
* [Kurallar altyapısı eşleşme koşulları](cdn-rules-engine-reference-match-conditions.md)
* [Kurallar altyapısı koşullu ifadeler](cdn-rules-engine-reference-conditional-expressions.md)
* [Kurallar altyapısı özellikleri](cdn-rules-engine-reference-features.md)
* [Merhaba kurallar altyapısı kullanarak varsayılan HTTP davranışı geçersiz kılma](cdn-rules-engine.md)
* [Azure Cuma: Azure CDN's güçlü yeni Premium özellikleri](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)