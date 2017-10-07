---
title: "Azure Search aaaImport verisine hello portalında | Microsoft Docs"
description: "Azure Vm'lerinde hello Azure Portal toocrawl NoSQL Azure Cosmos DB, Blob Depolama, tablo depolama, SQL Database ve SQL Server Azure verilerini Hello Azure arama verilerini İçeri Aktar Sihirbazı kullanın."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: Azure Portal
ms.assetid: f40fe07a-0536-485d-8dfa-8226eb72e2cd
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 00b0e59594560c0cdaea748df196518e9fba3834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-tooazure-search-using-hello-portal"></a>Veri tooAzure arama alma hello portal kullanma
Hello Azure portal sağlayan bir **veri içeri aktarma** bir dizine veri yükleme için hello Azure Search panosunda Sihirbazı. 

  ![Merhaba komut çubuğunda Veri Al][1]

Dahili olarak, Başlangıç Sihirbazı'nı yapılandırır ve çağıran bir *dizin oluşturucu*, dizin oluşturma işlemi hello birkaç adımdan otomatikleştirme: 

* Merhaba tooan dış veri kaynağına bağlanma aynı Azure aboneliği
* Merhaba kaynak veri yapısında değiştirilebilir dizin şemasını oluştur
* Yük JSON belgelerine hello veri kaynağından alınan bir satır kümesi kullanarak dizini

Azure Cosmos DB’deki örnek verileri kullanarak bu iş akışını deneyebilirsiniz. Ziyaret [hello Azure Portal'da Azure Search ile çalışmaya başlama](search-get-started-portal.md) yönergeler için.

> [!NOTE]
> Merhaba başlatabilirsiniz **veri içeri aktarma** gelen hello Azure Cosmos DB Pano toosimplify bu veri kaynağı için Dizin Oluşturma Sihirbazı. Sol gezinti bölmesinde, çok Git**koleksiyonları** > **Azure arama Ekle** tooget başlatıldı.

## <a name="data-sources-supported-by-hello-import-data-wizard"></a>Veri Alma Sihirbazı Hello tarafından desteklenen veri kaynakları
veri kaynakları aşağıdaki hello Hello veri içeri aktarma Sihirbazı'nı destekler: 

* Azure SQL Database
* Azure VM’lerdeki SQL Server ilişkisel verileri
* Azure Cosmos DB
* Azure Blob depolama
* Azure Tablo depolama

Düzleştirilmiş veri kümesi gerekli bir giriştir. Yalnızca tek bir tablo, veritabanı görünümü veya eşdeğeri veri yapısından aktarabilirsiniz. Başlangıç Sihirbazı'nı çalıştırmadan önce bu veri yapısını oluşturmanız gerekir.

## <a name="connect-tooyour-data"></a>Tooyour veri Bağlan
1. İçinde toohello oturum [Azure portal](https://portal.azure.com) ve açık hello hizmet panosunu. Tıklayabilirsiniz **daha fazla hizmet** hello atlama çubuğu toosearch varolan "arama hizmetleri için" Merhaba geçerli abonelikte içinde. 
2. Tıklatın **veri içeri aktarma** tooslide açık hello veri içeri aktar dikey çubuk hello komutu.  
3. Tıklatın **tooyour veri bağlanmak** toospecify bir dizin oluşturucu tarafından kullanılan bir veri kaynağı tanımını. Abonelik içi veri kaynakları için Başlangıç Sihirbazı'nı genellikle algılayabilir ve genel yapılandırma gereksinimleri en aza bağlantı bilgilerini okuyun.

|  |  |
| --- | --- |
| **Mevcut veri kaynağı** |Arama hizmetinizde önceden tanımlanmış dizin oluşturuculara sahipseniz başka bir içeri aktarma için var olan bir veri kaynağı seçebilirsiniz. |
| **Azure SQL Veritabanı** |Hizmet adı, okuma izni olan bir veritabanı kullanıcısı için kimlik bilgilerini ve bir veritabanı adı hello sayfasında ya da bir ADO.NET bağlantı dizesi yoluyla belirtilebilir. Merhaba bağlantı dizesi seçeneği tooview seçin veya özelliklerini özelleştirebilirsiniz. <br/><br/>Merhaba tablo ya da hello satır kümesi sağlar görünüm hello sayfasında belirtilmelidir. Bu seçenek Hello bağlantı, böylece bir seçim yapabileceğiniz bir açılır liste vermiş başarılı olduktan sonra görünür. |
| **Azure VM’lerde SQL Server** |Bağlantı dizesi olarak tam hizmet adı, kullanıcı kimliği ve parola ile veritabanı belirtin. toouse bu veri kaynağı, daha önce bir sertifika, hello bağlantı şifreler hello yerel deposunda yüklemiş olmalısınız. Yönergeler için bkz: [SQL VM bağlantı tooAzure arama](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md). <br/><br/>Merhaba tablo ya da hello satır kümesi sağlar görünüm hello sayfasında belirtilmelidir. Bu seçenek Hello bağlantı, böylece bir seçim yapabileceğiniz bir açılır liste vermiş başarılı olduktan sonra görünür. |
| **Azure Cosmos DB** |Gereksinimleri hello hesap, veritabanı ve koleksiyonu içerir. Merhaba koleksiyonundaki tüm belgeleri hello dizinde dahil edilir. Bir sorgu tooflatten tanımlayın veya hello satır kümesi filtre ya da belgeler için sonraki veri yenileme işlemleri toodetect değiştirildi. |
| **Azure Blob Depolama** |Gereksinimleri hello depolama hesabı ve kapsayıcı içerir. İsteğe bağlı olarak, BLOB adları gruplandırma amaçları için sanal bir adlandırma kuralı izlerseniz, kapsayıcı altında bir klasör olarak hello adının hello sanal dizin bölümü belirtebilirsiniz. Daha fazla bilgi için bkz. [Blob Depolama Dizini Oluşturma](search-howto-indexing-azure-blob-storage.md). |
| **Azure Table Storage** |Gereksinimleri hello depolama hesabı ve bir tablo adı içerir. İsteğe bağlı olarak, bir sorgu tooretrieve hello tablolar kümesini belirtebilirsiniz. Daha fazla bilgi için bkz. [Tablo Depolama Dizini Oluşturma](search-howto-indexing-azure-tables.md). |

## <a name="customize-target-index"></a>Hedef dizini özelleştirme
Bir başlangıç dizini genellikle hello kümesinden algılanır. Eklemek, düzenlemek veya alanları toocomplete hello şema silin. Ayrıca, özniteliklerini hello alan düzeyi toodetermine kendi sonraki arama davranışlarını ayarlayın.

1. İçinde **hedef dizini Özelleştir**, hello adı belirtin ve bir **anahtar** kullanılan toouniquely her belge tanımlayın. başlangıç anahtarı bir dize olmalıdır. Alan değerleri boşluklar veya tireler dahil ederseniz olması emin tooset Gelişmiş Seçenekler **verilerinizi içeri** toosuppress hello bu karakterler için doğrulama denetimi.
2. Gözden geçirin ve alanları kalan hello gözden geçirin. Alan adı ve türü genellikle sizin için doldurulur. Merhaba dizini oluşturulan kadar hello veri türünü değiştirebilirsiniz. Daha sonra değiştirmeniz için yeniden derleme gerekir.
3. Her bir alan için dizin özniteliklerini ayarlayın:
   
   * Alınabilir, arama sonuçlarında hello alanı döndürür.
   * Filtrelenebilir filtre ifadelerinde hello alan toobe sağlar.
   * Sıralanabilir hello alan toobe bir sıralamada kullanılabilmesini sağlar.
   * Modellenebilir, alanın modellenmiş gezinmesine hello sağlar.
   * Aranabilir, tam metin aramayı etkinleştirir.
4. Merhaba tıklatın **Çözümleyicisi** toospecify hello alan düzeyinde bir dil Çözümleyicisi istiyorsanız sekmesinde. Şu anda yalnızca dil çözümleyicileri belirtilebilir. Özel bir çözümleyici veya Keyword, Pattern gibi dil dışı bir çözümleyici kullanılması kod gerektirir.
   
   * Tıklatın **aranabilir** toodesignate tam metin arama hello alanında bulunan ve hello Çözümleyicisi açılan listesini etkinleştir.
   * İstediğiniz hello Çözümleyicisi'ni seçin. Ayrıntılı bilgi için bkz. [Birden çok dildeki belgeler için dizin oluşturma](search-language-support.md).
5. Merhaba tıklatın **öneri aracı** tooenable yazarken tamamlanan Sorgu önerileri seçilen alanlar.

## <a name="import-your-data"></a>Verilerinizi içeri aktarma
1. İçinde **verilerinizi içeri**, hello dizin oluşturucu için bir ad sağlayın. Bu hello ürün geri çağırma hello veri içeri aktarma bir dizin oluşturucu sihirbazıdır. Tooview istediğiniz ya da düzenlemek, daha sonra hello portalından yerine hello sihirbazını yeniden seçmeniz. 
2. Merhaba bölgesel zaman hello hizmet sağlandı bölgeye göre hello zamanlamasını belirtin.
3. Gelişmiş Seçenekleri toospecify eşikleri olup dizin belge bırakılır devam edebilirsiniz üzerinde ayarlayın. Ayrıca, belirtebilirsiniz olup olmadığını **anahtar** toocontain boşluk ve eğik çizgi alanları izin verilir.  
4. Tıklatın **Tamam** toocreate hello dizin ve hello veri içeri aktarın.

Merhaba Portalı'nda dizin izleyebilirsiniz. Belgeleri yüklenen olarak hello belge sayısı için tanımladığınız hello dizin büyüyecektir. Bazen hello portal sayfası toopick hello en son güncelleştirmeleri kurmak için birkaç dakika sürer.

Merhaba dizin tüm hello belgelerini yüklenen hazır tooquery olur.

## <a name="query-an-index-using-search-explorer"></a>Arama Gezgini kullanarak dizin sorgulama

Merhaba portalı içerir **arama Gezgini** böylece herhangi bir kod toowrite gerek kalmadan bir dizini sorgulama yapabilirsiniz. [Arama Gezgini](search-explorer.md)'ni herhangi bir dizinde kullanabilirsiniz.

Merhaba arama deneyimi hello gibi varsayılan ayarları dayanır [basit sözdizimi](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) ve varsayılan [searchMode sorgu parametresi (https://docs.microsoft.com/rest/api/searchservice/search-documents). 

Böylece hello tüm belgeyi inceleyebilirsiniz sonuçları ayrıntılı bir biçimde JSON döndürülür.

## <a name="edit-an-existing-indexer"></a>Var olan bir dizin oluşturucuyu düzenleme
Belirtildiği gibi hello verilerini İçeri Aktar Sihirbazı oluşturur bir **dizin oluşturucu**, hangi hello Portalı'nda bir tek başına yapısı olarak değiştirebilirsiniz.

Merhaba hizmet panosunda, aboneliğiniz için oluşturulan tüm dizin oluşturucuların listesini hello dizin oluşturucu Döşe tooslide çift tıklayın. Merhaba dizin oluşturucular toorun birini çift tıklatın, düzenleyin veya silin. Merhaba dizin başka bir var olan bir öğe ile değiştirmek, hello veri kaynağını değiştirin ve dizin oluşturma sırasında hata eşikleri için seçenekleri ayarlayın.

## <a name="edit-an-existing-index"></a>Var olan bir dizini düzenleme
Merhaba sihirbaz tarafından oluşturulan aynı zamanda bir **dizin**. Azure Search'te yapısal güncelleştirmeleri tooan dizini yeniden oluşturma bu dizinin gerektirir. Bir yeniden oluşturma kullanarak istediğiniz hello değişiklikleri sahip yeniden düzenlenen bir şema ve verileri yeniden yükleme hello dizini yeniden oluşturma, silme hello dizin kapsar. Yapısal güncelleştirmeler bir veri türünün değiştirilmesini ve bir alanın yeniden adlandırılmasını ya da silinmesini içerir.

Yeni bir alan ekleme, puanlama profillerini değiştirme, öneri araçlarını değiştirme veya dil çözümleyicileri değiştirme gibi işlemler yeniden derleme gerektirmeyen düzenlemelerdir. Daha fazla bilgi için bkz. [Dizin Güncelleştirme](https://msdn.microsoft.com/library/azure/dn800964.aspx).


## <a name="next-steps"></a>Sonraki adımlar
Dizin oluşturucular hakkında daha fazla bu bağlantılar toolearn gözden geçirin:

* [Azure SQL Veritabanı dizini oluşturma](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB’yi dizine ekleme](search-howto-index-documentdb.md)
* [Blob Depolama dizini oluşturma](search-howto-indexing-azure-blob-storage.md)
* [Tablo Depolama dizini oluşturma](search-howto-indexing-azure-tables.md)

<!--Image references-->
[1]: ./media/search-import-data-portal/search-import-data-command.png

