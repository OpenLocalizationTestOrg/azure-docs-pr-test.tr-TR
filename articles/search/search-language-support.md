---
title: "aaaAzure arama çoklu dil | Microsoft Docs"
description: "Azure arama, dil Çözümleyicileri Lucene ve doğal dil işleme teknolojisi Microsoft'tan gelen yararlanarak 56 dilleri destekler."
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a>Azure Search'te birden çok dilde belgeler için dizin oluşturma
> [!div class="op_single_selector"]
>
> * [Portal](search-language-support.md)
> * [REST](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

Dil Çözümleyicileri unleashing hello gücünü hello dizin tanımı aranabilir alanında bulunan bir özellik ayarı olarak kadar kolaydır. Şimdi bu adımı hello portalında yapabilirsiniz.

Azure Portal dikey penceresi ekran görüntüleri hello Azure arama için bir dizin şemasını kullanıcılar toodefine izin aşağıda verilmiştir. Bu dikey pencereden kullanıcılar hello alanların tümünü oluşturabilir ve bunların her biri için hello Çözümleyicisi özelliğini ayarlayın.

> [!IMPORTANT]
> Yalnızca bir dil Çözümleyicisi alan tanımı sırasında gibi hello yeni bir dizin oluşturma plan veya yeni bir alan tooan var olan dizini eklerken ayarlayabilirsiniz. Hello alan oluşturulurken hello Çözümleyicisi de dahil olmak üzere tüm özniteliklerin tam olarak belirttiğinizden emin olun. Merhaba özniteliklerin mümkün tooedit olması veya değişiklikleri kaydettikten sonra hello Çözümleyicisi türünü değiştirin olmaz.
>
>

## <a name="define-a-new-field-definition"></a>Yeni bir alan tanımı tanımlayın
1. İçinde toohello oturum [Azure portal](https://portal.azure.com) ve açık hello hizmeti dikey search hizmetinizin.
2. ' I tıklatın **Ekle dizin** hello komut yeni bir dizin hello hizmet Pano toostart hello üstünde çubuk veya varolan bir dizin tooset bir Çözümleyicisi ekleyeceğiniz yeni alanlar açın tooan varolan bir dizini.
3. Merhaba alanları dikey penceresi görünür hello dizin hello şemasını tanımlamak için seçenekler sunan hello Çözümleyicisi sekmesinde de dahil olmak üzere bir dil Çözümleyicisi seçmek için kullanılır.
4. Alanlarda alan tanımı sağlayan bir adı hello veri türü seçme ve öznitelikleri toomark hello alan tam metin aranabilir, arama sonuçlarında, model Gezinti yapılarda kullanılabilir alınabilir sıralanabilir vb. ayarı başlatın.
5. Toohello sonraki alan taşımadan önce hello açmak **Çözümleyicisi** sekmesi.

![][1]
*tooselect bir Çözümleyicisi hello alanları dikey penceresinde hello Çözümleyicisi sekmesini tıklatın*

## <a name="choose-an-analyzer"></a>Bir analyzer'ı seçin
1. Tanımladığınız toofind hello alan kaydırın.
2. Merhaba alan aranabilir olarak işaretlenmiş henüz yoksa, hello onay kutusu şimdi toomark tıklatın olarak **aranabilir**.
3. Merhaba Çözümleyicisi alanı toodisplay hello listesi kullanılabilir çözümleyiciler tıklatın.
4. Merhaba Çözümleyicisi seçin toouse istiyor.

![][2]
*Her bir alan için desteklenen hello çözümleyiciler birini seçin*

Varsayılan olarak, tüm aranabilir alanları hello kullan [standart Lucene Çözümleyicisi](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) dil belirsiz olduğu. tooview hello tam listesini desteklenen çözümleyiciler bkz [dil desteği Azure Search'te](https://msdn.microsoft.com/library/azure/dn879793.aspx).

Merhaba dil Çözümleyicisi için bir alan seçtikten sonra bu alan için dizin oluşturma ve arama her istek ile kullanılır. Bir sorgu farklı çözümleyicilerini kullanarak birden çok alan karşı verildiğinde hello sorgu bağımsız olarak her bir alan için doğru çözümleyiciler hello tarafından işlenir.

Birçok web ve mobil uygulamalar kullanıcılar farklı diller kullanılarak Merhaba Dünya geçici hizmet. Bu senaryo için dizin gibi desteklenen her dil için bir alan oluşturarak olası toodefine olur.

![][3]
*Desteklenen her dil için bir açıklama alanı ile dizin tanımı*

Bir sorgu verme hello Aracısı Hello dilinin bilinen, arama isteği hello kullanarak kapsamlı tooa belirli alan olabilir **searchFields** sorgu parametresi. Merhaba aşağıdaki sorguyu yalnızca Lehçe hello açıklamasında karşı verilir:

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

Dizininizi hello portalından sorgulayabilirsiniz kullanarak **arama Gezgini** bir sorgu benzer toohello yukarıda gösterilenle toopaste. Arama Gezgini hello hizmeti dikey hello komut çubuğunda kullanılabilir. Bkz: [hello portalındaki Azure Search dizininizi sorgulama](search-explorer.md) Ayrıntılar için.

Bazen hello bir sorgu verme hello Aracısı'nın dil bilinmiyor, hangi servis talebi hello sorgu karşı tüm alanlar aynı anda verilebilir. Gerekirse, belirli bir dilde sonuçları için tercih kullanılarak tanımlanabilir [profilleri Puanlama](https://msdn.microsoft.com/library/azure/dn798928.aspx). Merhaba aşağıdaki örnekte, Lehçe ve Fransızca yüksek göreli toomatches İngilizce hello açıklamasında bulunan eşleşmeler skoru:

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

.NET Geliştirici değilseniz, dil Çözümleyicileri hello kullanarak yapılandırabileceğinize dikkat edin [Azure Search .NET SDK'sı](http://www.nuget.org/packages/Microsoft.Azure.Search). Merhaba en son sürüm hello Microsoft dil Çözümleyicileri de destekler.

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
