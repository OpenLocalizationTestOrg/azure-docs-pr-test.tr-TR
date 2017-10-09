---
title: "Azure Search'te aaaHow toomodel karmaşık veri türleri | Microsoft Docs"
description: "İç içe geçmiş veya hiyerarşik veri yapılarını düzleştirilmiş satır kümesi ve koleksiyonları veri türünü kullanarak Azure Search dizini içinde modellenebilir."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a>Azure Search'te nasıl toomodel karmaşık veri türleri
Dış veri kümeleri, Azure Search dizini bazen düzgünce tablo satır kümesine bozmadığını hiyerarşik veya iç içe substructures dahil toopopulate kullanılır. Bu tür yapıları örnekleri birden çok konumda ve telefon numaraları, tek bir rehberi birden çok yazar gibi tek bir SKU için tek bir müşteri, birden çok renkleri ve boyutları içerir ve benzeri. Koşulları modelleme içinde bu yapıları başvurulan tooas görebilirsiniz *karmaşık veri türlerini*, *bileşik veri türleri*, *bileşik veri türleri*, veya *toplama veri türleri*, az bir tooname.

Karmaşık veri türleri yerel olarak Azure arama desteklenmez, ancak kanıtlanmış bir geçici çözüm hello yapısı düzleştirme ve ardından kullanarak iki adımlı bir işlem içerir bir **koleksiyonu** veri türü tooreconstitute hello iç yapısı. Bu makalede açıklanan hello tekniği aşağıdaki hello içerik toobe Aranan, modellenmiş, filtre ve sıralanmış sağlar.

## <a name="example-of-a-complex-data-structure"></a>Karmaşık veri yapısı örneği
Genellikle, söz konusu hello veri JSON veya XML belgeleri kümesi olarak ya da Azure Cosmos DB gibi bir NoSQL deposundaki öğeleri olarak bulunur. Yapısal olarak, arama ve filtre toobe gereken birden çok alt öğe olmaktan hello sınama kaynaklandığını.  Merhaba geçici çözüm gösteren için başlangıç noktası olarak kişiler bir dizi örnek olarak listeler JSON belgesi aşağıdaki hello alın:

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

'ID' Hello alanları adlı olsa da, 'name' ve 'şirket' kolayca bire bir Azure Search dizini içinde alanlar olarak eşlenebilir, hem bir dizi konumu açıklamaları yanı sıra konumu kimlikleri sahip konumları, bir dizi hello 'konumları' alan içerir. Azure Search bu destekleyen bir veri türü yok koşuluyla, farklı bir şekilde toomodel Azure Search'te gerekli. 

> [!NOTE]
> Bu teknik de blog postasına Kirk Evans tarafından açıklanan [Azure Search dizini oluşturma DocumentDB](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), "yapabildiği sahip olduğunuz adlı bir alan düzleştirme hello verilerin", adında bir teknik gösterir `locationsID` ve `locationsDescription` her ikisi de olan [koleksiyonları](https://msdn.microsoft.com/library/azure/dn798938.aspx) (veya bir dizeler dizisi).   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a>1. Kısım: hello dizi tek tek alanlarına düzleştirmek
toocreate bu veri kümesi düzenler bir Azure Search dizini oluşturma hello iç içe geçmiş düzeltilebilmenize alanları tek tek: `locationsID` ve `locationsDescription` veri türüne sahip [koleksiyonları](https://msdn.microsoft.com/library/azure/dn798938.aspx) (veya bir dizeler dizisi). Bu alanları hello '1' ve '2' hello değerlerini dizin `locationsID` alanında Hasan Aydın ve başlangıç değerleri '3' & '4' hello içine `locationsID` Jen Campbell için alan.  

Verilerinizi Azure Search içinde şöyle olabilir: 

![Örnek veriler, 2 satır](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a>2. Bölüm: Merhaba dizin tanımında koleksiyonu alan ekleme
Merhaba dizin şemasında benzer toothis örnek hello alan başvuruları görünebilir.

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a>Arama davranışlarını doğrulamak ve isteğe bağlı olarak hello dizin genişletme
Oluşturulan hello dizin ve yüklenen hello veri varsayıldığında, artık hello çözüm tooverify arama sorgusu yürütme hello dataset karşı test edebilirsiniz. Her **koleksiyonu** alan olmalıdır **aranabilir**, **filtrelenebilir** ve **modellenebilir**. Mümkün toorun sorguları gibi olmalıdır:

* 'Adventureworks Genel merkez' hello sırasında çalışan tüm kişilerin bulun.
* 'Giriş Office' çalışan kişilerin hello sayısı sayısını alır.  
* Çalışan bir 'giriş ofiste' hello kişiler her yerde hello kişi sayısı ile birlikte çalıştıkları diğer ofislerdeki gösterir.  

Toodo hem hello konum kimliği, hem de hello konum açıklaması birleştiren bir arama gerektiğinde burada bu yöntem parçalayın döner ' dir. Örneğin:

* Bir giriş Office sahip oldukları tüm kişileri Bul ve 4'ün bir konum kimliği vardır.  

Aşağıdaki gibi görünen hello özgün içerik geri çağırma varsa:

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

Biz hello veri farklı alanlara ayrılmış, ancak hiçbir şekilde bilinmesiyle hello Jen Campbell için giriş Office çok ile ilişkili ise sahibiz`locationsID 3` veya `locationsID 4`.  

Bu durumda toohandle hello verilerin tümü tek bir koleksiyona birleştirir hello dizindeki başka bir alan tanımlayın.  Bizim örneğimizde, biz Bu alan çağıracak `locationsCombined` ve biz hello içerikle ayıracak bir `||` düşündüğünüz ayırıcı karakter içeriğiniz için benzersiz bir dizi olacaktır seçebilmenize rağmen. Örneğin: 

![Örnek veriler, 2 satır ayırıcı ile](./media/search-howto-complex-data-types/sample-data-2.png)

Bu kullanarak `locationsCombined` alan, biz şimdi uyum sağlayacak daha da fazla sorguları gibi:

* Bir 'giriş ofiste' konum kimliği ile '4' ın çalışan kişilerin sayısını gösterir.  
* Kimliği '4' konumu ile bir 'giriş ofiste' çalışan kişilerin arayın. 

## <a name="limitations"></a>Sınırlamalar
Bu teknik senaryolar sayısı için yararlıdır, ancak her durumda geçerli değil.  Örneğin:

1. Karmaşık veri türünüz alanları statik kümesine sahip değil ve hiçbir şekilde toomap vardı tüm hello olası tooa tek alan türleri. 
2. İç içe geçmiş hello nesnelerini güncelleştirme bazı ek çalışmalar toodetermine tam olarak ne hello Azure Search dizinine güncelleştirilmiş toobe gerektiğini gerektirir.

## <a name="sample-code"></a>Örnek kod
Nasıl tooindex karmaşık bir JSON verilerini Azure Search ayarlandığında örneği görmek ve bu veri kümesi bu üzerinden sorguları bir dizi yerine [GitHub deposuna](https://github.com/liamca/AzureSearchComplexTypes).

## <a name="next-step"></a>Sonraki adım
[Karmaşık veri türleri için yerel destek için oy](https://feedback.azure.com/forums/263029-azure-search) hello Azure arama UserVoice üzerinde sayfasında ve herhangi bir ek giriş sağlamak göndermemizi istediğinizi tooconsider özellik uygulama ile ilgili. Doğrudan Twitter'da toome çıkışı de ulaşabilir @liamca.

