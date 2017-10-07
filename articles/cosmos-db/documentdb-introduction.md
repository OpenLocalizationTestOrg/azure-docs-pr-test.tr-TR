---
title: "Azure Cosmos DB: DocumentDB API’si | Microsoft Docs"
description: "SQL ve JavaScript kullanarak düşük gecikme süresine sahip Azure Cosmos DB toostore ve sorgu büyük birimleri JSON belgelerinin nasıl kullanabileceğinizi öğrenin."
keywords: "json veritabanı, belge veritabanı"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 686cdd2b-704a-4488-921e-8eefb70d5c63
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/22/2017
ms.author: mimig
ms.openlocfilehash: c96dfa5e2685782a99d2bcaf992f88dd2bef920b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-documentdb-api"></a>Giriş tooAzure Cosmos DB: DocumentDB API

[Azure Cosmos DB](introduction.md), Microsoft'un görev açısından kritik uygulamalar için genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Azure Cosmos DB sağlar [anahtar teslim genel dağıtım](distribute-data-globally.md), [üretilen iş ve depolama esnek ölçeklendirme](partition-data.md) dünya, tek basamaklı milisaniyelik gecikme hello 99, adresindeki [beş iyi tanımlanmış tutarlılık düzeylerini](consistency-levels.md), yüksek oranda kullanılabilirlik, tarafından yedeklenen tüm garanti [endüstri lideri SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure Cosmos DB [verileri otomatik olarak dizinler](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) toodeal şema ve dizin yönetimi ile gerektirmeden. Çok modelli olan bu hizmet belge, anahtar-değer, grafik ve sütunlu veri modellerini destekler. 

![Azure DocumentDB API’si](./media/documentdb-introduction/cosmosdb-documentdb.png) 

Zengin ve tanıdık Azure Cosmos DB Hello DocumentDB API sağlayan [SQL sorgu özellikleri](documentdb-sql-query.md) şema daha az JSON veriler üzerinde tutarlı düşük gecikme süreleriyle. Bu makalede, hello Azure Cosmos veritabanı DocumentDB API, ve nasıl JSON veri toostore yoğun birimler kullanmak, milisaniye gecikme sırasını içinde sorgu ve hello şema kolayca gelişmesi genel bakış sağlar. 

## <a name="what-capabilities-and-key-features-does-azure-cosmos-db-offer"></a>Azure Cosmos DB’nin sunduğu yetenekler ve önemli özellikler nelerdir?
Merhaba DocumentDB API'si aracılığıyla Azure Cosmos DB hello aşağıdaki temel işlevleri ve avantajları sunar:

* **Esnek bir şekilde ölçeklenebilir işleme ve Depolama:** kolayca yukarı veya, JSON veritabanı toomeet uygulamanız ölçeği gerekir. Verileriniz düşük tahmin edilebilirliğe sahip gecikme süreleri sağlamak için katı hal disklerinde (SSD) depolanır. Azure Cosmos DB adlı toovirtually ölçeklendirebilirsiniz koleksiyonlar JSON verilerini depolamak için kapsayıcıları destekler sınırsız depolama boyutlarına ve sağlanan işleme. Uygulamanız büyüdükçe, Azure Cosmos DB'yi tahmin edilebilir performansla sorunsuz ve esnek bir şekilde ölçeklendirebilirsiniz. 


* **Bölgeli çoğaltma:** Azure Cosmos DB saydam olarak çoğaltır, ilişkili Azure Cosmos DB hesabınızla sağlarken genel erişim toodata gerektiren toodevelop uygulamalar etkinleştirme, veri tooall bölgeleri bileşim tutarlılık, kullanılabilirlik ve performans, tüm ilgili garanti ile arasında. Azure Cosmos DB saydam bölgesel yük devretmesi çok girişli API'leri ve hello özelliği tooelastically ölçek işleme ve depolama ile Merhaba Dünya çapında sağlar. [Azure Cosmos DB ile verileri küresel ölçekte dağıtma](distribute-data-globally.md) bölümünde daha fazla bilgi edinin.

* **Tanıdık SQL söz dizimi ile geçici sorgular:** Heterojen JSON belgelerini depolayın ve bilindik bir SQL söz dizimi aracılığıyla bu belgeleri sorgulayın. Azure Cosmos DB bir derecede eşzamanlı, kilitsiz, günlük dizin oluşturma teknolojisi tooautomatically dizin tüm belge içeriğinin yapılandırılmış. Bu, gerçek zamanlı zengin sorgulara hello gerek toospecify şema ipuçları, ikincil dizinler veya görünümler olmadan sağlar. [Azure Cosmos DB’yi sorgulama](documentdb-sql-query.md) bölümünden daha fazla bilgi edinin. 
* **Merhaba veritabanı içinde JavaScript yürütme:** Express uygulama mantığını saklı yordamlar, tetikleyiciler ve standart JavaScript'i kullanarak kullanıcı tanımlı işlevler (UDF'ler). Bu, uygulama mantığını toooperate verilerin üzerine Merhaba uygulaması hello veritabanı şeması arasındaki hello uyuşmazlığı hakkında endişelenmeden sağlar. Merhaba DocumentDB API doğrudan hello veritabanı altyapısının içinde JavaScript uygulama mantığının tam işlem tabanlı olarak yürütülmesini sağlar. JavaScript derin tümleştirmesi Hello hello yürütülmesini ekleme, değiştirme, silme ve seçme işlemlerinin bir JavaScript programı içinden yalıtılmış bir işlem olarak sağlar. Daha fazla bilgi için bkz. [DocumentDB sunucu tarafı programlama](programming.md).

* **İnce ayarlanabilir tutarlılık düzeyleri:** iyi tanımlanmış tutarlılık düzeyleri tooachieve tutarlılık ve performans arasında en iyi dengeyi beş seçin. Azure Cosmos DB sorgular ve okuma işlemleri için beş farklı tutarlılık düzeyi sunar: güçlü, sınırlanmış eskime durumu, oturum, tutarlı ön ek ve son. Bu ayrıntılı ve iyi tanımlanmış tutarlılık düzeyleri toomake ses dengelemeler tutarlılık, kullanılabilirlik ve gecikme süresi arasında izin verin. Daha fazla bilgi edinin [toomaximize kullanılabilirlik ve performans düzeyleri tutarlılık kullanarak](consistency-levels.md).

* **Tam olarak yönetilen:** Merhaba, gerek toomanage veritabanı ve makine kaynaklarını ortadan kaldırmak. Bir tam olarak yönetilen Microsoft Azure hizmet olarak değil gerek toomanage sanal makineleri yapın, dağıtmak ve yazılım yapılandırma ölçeklendirmeyi yönetmeniz veya karmaşık veri katmanı yükseltmeleriyle uğraşmanız. Tüm veritabanları otomatik olarak yedeklenir ve bölgesel arızalara karşı korunur. Kolayca Azure Cosmos DB hesap eklemek ve kapasite, çalıştırma ve veritabanınızı yönetmek yerine, uygulamanızın üzerinde toofocus izin vererek gerektiği sağlayın. 

* **Tasarımı gereği açık:** Var olan becerileri ve araçları kullanarak hızlı bir şekilde çalışmaya başlayın. DocumentDB API basittir, ulaşılabilirdir ve tooadopt yeni araçlar gerektirmez veya toocustom uzantıları tooJSON veya JavaScript uyması hello karşı programlama. Tüm CRUD, sorgu ve JavaScript basit bir RESTful HTTP arabirimi üzerinden işleme gibi hello veritabanı işlevselliği erişebilir. Merhaba DocumentDB API var olan biçimleri, dilleri ve standartları yüksek değerli bunları veritabanı işlevleri benimserken.

* **Otomatik dizin oluşturma:** varsayılan olarak, Azure Cosmos DB otomatik olarak hello veritabanındaki tüm hello belgeleri dizinler ve beklediğiniz veya herhangi bir şemayı ya da ikincil dizinlerin oluşturulmasını gerektirir. Tooindex her şeyi istiyor mu? Merak etmeyin, [JSON dosyalarınızda yolları iptal de edebilirsiniz](indexing-policies.md).

* **Değişiklik akış desteği:** değişiklik akış belgeleri hello sırada bunlar değiştiren bir Azure Cosmos DB koleksiyonundaki sıralanmış bir listesini sağlar. Bu akışın sipariş tooreplicate verilerdeki değişiklikleri toodata için kullanılan toolisten olması, API çağrıları tetiklemek veya güncelleştirmeleri akış işleme gerçekleştirin. Değişiklik akış olan otomatik olarak etkinleştirilmiş ve kolay toouse: [akış değiştirme hakkında daha fazla bilgi edinin](https://docs.microsoft.com/azure/cosmos-db/change-feed). 

## <a name="data-management"></a>Hello DocumentDB API ile verileri yönetme?
Merhaba DocumentDB API iyi tanımlanmış veritabanı kaynakları aracılığıyla JSON verilerini yönetmenize yardımcı olur. Bu kaynaklar yüksek kullanılabilirlik için çoğaltılır ve mantıksal URI'leri ile benzersiz olarak adreslenebilir. Basit bir HTTP tabanlı RESTful programlama modeli tüm kaynaklar için Hello DocumentDB API sunar. 


Hello Azure Cosmos DB veritabanı size sağladığı benzersiz bir ad alanı erişim tooAzure Cosmos DB hesabıdır. Veritabanı hesabı oluşturabilmeniz için önce sağlayan bir Azure aboneliğine sahip olmalıdır tooa çeşitli Azure hizmetlerine erişim. 

Azure Cosmos DB içindeki tüm kaynaklar JSON belgeleri olarak modellenir ve depolanır. Kaynaklar meta veriler içeren JSON belgeleri olan öğeler şeklinde, aynı zamanda öğe koleksiyonları olan akışlar şeklinde yönetilir. Öğe kümeleri ilgili akışlarının içinde yer alır.

Aşağıdaki Hello görüntü hello hello Azure Cosmos DB kaynakları arasındaki ilişkiler gösterilmektedir:

![Hello Azure Cosmos veritabanı kaynaklar arasındaki hiyerarşi ilişkisi][1] 

Bir veritabanı hesabı, her biri saklı yordamlar, tetikleyiciler, UDF'ler, belgeler ve ilgili ekler içerebilen birden çok koleksiyonu kapsayan bir veritabanları kümesinden oluşur. Bir veritabanı Ayrıca kullanıcılar, her bir dizi izinleri tooaccess çeşitli diğer koleksiyonları, saklı yordamlar, Tetikleyiciler, UDF'ler, belgeler veya ekleri ilişkilendirilir. Veritabanları, kullanıcılar, izinler ve koleksiyonlar iyi bilinen şemalar sahip sistem tanımlı kaynaklardır; belgeler, saklı yordamlar, tetikleyiciler, UDF'ler ve eklerde ise rastgele ve kullanıcı tanımlı JSON içeriği bulunur.  

> [!NOTE]
> Merhaba DocumentDB API Azure DocumentDB hizmetinin hello daha önce mevcut olduğundan, tooprovision, izlemek ve hello Azure kaynak yönetimi REST API'si oluşturulan hesapların yönetmek veya araçları kullanarak Azure DocumentDB Merhaba devam edebilirsiniz ya da Azure Cosmos DB kaynak adları. Merhaba adları birbirinin yerine toohello Azure DocumentDB API'leri başvururken kullanırız. 

## <a name="develop"></a>Merhaba DocumentDB API uygulamalarla nasıl geliştirme yapabilirsiniz?

Azure Cosmos DB hello herhangi bir dil tarafından HTTP/HTTPS istekleri çağrılabilen REST API'leri aracılığıyla kaynaklarını kullanıma sunar. Ayrıca, hello DocumentDB API için birkaç popüler dilde programlama kitaplıkları sunar. Hello istemci kitaplıklar adresi önbelleğe alma, özel durum yönetimi, otomatik yeniden denemeler ve diğerleri gibi ayrıntıları işleyerek hello API ile çalışmanın çoğu yönünü basitleştirir. Kitaplıkları hello için şu anda kullanılabilir diller ve platformlar aşağıdaki:  

| İndir | Belgeler |
| --- | --- |
| [.NET SDK](http://go.microsoft.com/fwlink/?LinkID=402989) |[.NET kitaplığı](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) |
| [Node.js SDK’sı](http://go.microsoft.com/fwlink/?LinkID=402990) |[Node.js kitaplığı](http://azure.github.io/azure-documentdb-node/) |
| [Java SDK](http://go.microsoft.com/fwlink/?LinkID=402380) |[Java kitaplığı](/java/api/com.microsoft.azure.documentdb) |
| [JavaScript SDK'sı](http://go.microsoft.com/fwlink/?LinkID=402991) |[JavaScript kitaplığı](http://azure.github.io/azure-documentdb-js/) |
| yok |[Sunucu tarafı JavaScript SDK'sı](http://azure.github.io/azure-documentdb-js-server/) |
| [Python SDK'sı](https://pypi.python.org/pypi/pydocumentdb) |[Python kitaplığı](http://azure.github.io/azure-documentdb-python/) |
| yok | [MongoDB API’si](mongodb-introduction.md)


Hello kullanarak [Azure Cosmos DB öykünücüsü](local-emulator.md), geliştirmek ve bir Azure aboneliği oluşturmak veya herhangi bir maliyet olmadan uygulamanızı yerel olarak hello DocumentDB API ile test. Uygulamanızı hello öykünücüsünde nasıl çalıştığını ile memnun kaldığınızda, toousing hello buluttaki bir Azure Cosmos DB hesabını geçiş yapabilirsiniz.

Basic ötesinde oluşturma, okuma, güncelleştirme ve silme işlemleri, hello DocumentDB API'si, JSON belgelerini ve JavaScript uygulama mantığının işlem tabanlı olarak yürütülmesi için sunucu tarafı desteği almak için zengin bir SQL sorgu arabirimi sağlar. Merhaba sorgu ve betik yürütme arabirimleri tüm platform kitaplıkları kullanılabilir yanı sıra REST API'leri hello. 

### <a name="sql-query"></a>SQL sorgusu
belgeleri sorgulama hello DocumentDB API destekler hello kökü belirtilmiş bir SQL dilini kullanarak JavaScript türü sistem ve ilişkisel, hiyerarşik ve uzamsal sorguları destekleyen ifadeleri. Basit ancak güçlü arabirimi tooquery JSON belgelerini Hello DocumentDB sorgu dildir. Hello dil, ANSI SQL dil bilgisinin kümesini destekler ve JavaScript nesnesi, dizileri, nesne oluşturması ve işlev çağrısını derin tümleştirme ekler. Merhaba DocumentDB API hello geliştiriciden herhangi bir açık şema veya dizin oluşturma ipuçları almadan kendi sorgu modelini sağlar.

Kullanıcı tanımlı işlevler (UDF'ler) hello DocumentDB API ile kayıtlı ve dolayısıyla hello dilbilgisi toosupport özel uygulama mantığını genişletme bir SQL sorgusu bir parçası olarak başvurulabilir. Bu UDF'ler JavaScript programları olarak yazılır ve hello veritabanı içinde yürütülür. 

.NET geliştiricileri için DocumentDB API hello [.NET SDK'sı](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.aspx) bir LINQ Sorgu sağlayıcısı da sunar. 

### <a name="transactions-and-javascript-execution"></a>İşlemler ve JavaScript yürütme
Merhaba DocumentDB API toowrite uygulama mantığını tamamen JavaScript'te yazılmış adlandırılmış programlar olarak sağlar. Bu programlar bir koleksiyon için kaydedilir ve belirli bir koleksiyon içindeki hello belgelerde veritabanı işlemlerini verebilir. JavaScript bir tetikleyici, saklı yordam veya kullanıcı tanımlı işlev olarak yürütme için kaydedilebilir. Tetikleyiciler ve saklı yordamlar oluşturabilir, okuma, güncelleştirme ve yazma erişimi toohello koleksiyonu olmaksızın hello sorgu yürütme mantığının parçası olarak kullanıcı tanımlı işlevler yürütme ise belgeleri silme.

Merhaba Cosmos DB içinde JavaScript yürütme, JavaScript Transact-SQL için modern bir ardılı ile ilişkisel veritabanı sistemleri tarafından desteklenen hello kavramları sonra modellenir. Tüm JavaScript mantığı, anlık görüntü yalıtımıyla çevresel ACID işlemi içinde yürütülür. Merhaba, yürütme sürecinde JavaScript bir özel durum oluşturur hello sonra Merhaba, tüm işlem iptal edildi.

## <a name="are-there-any-online-courses-on-azure-cosmos-db"></a>Azure Cosmos DB ile ilgili çevrimiçi kurslar var mı?

Evet, Azure DocumentDB’de [Microsoft Sanal Akademi](https://mva.microsoft.com/en-US/training-courses/azure-documentdb-planetscale-nosql-16847) kursu mevcuttur. 

>[!VIDEO https://mva.microsoft.com/en-US/training-courses-embed/azure-documentdb-planetscale-nosql-16847]
>
>

## <a name="next-steps"></a>Sonraki adımlar
Zaten bir Azure hesabınız var mı? Bundan sonra, hesap oluşturma ve Cosmos DB ile çalışmaya başlama konusunda size kılavuzluk edecek [hızlı başlangıçlarımızı](../cosmos-db/create-documentdb-dotnet.md) takip ederek Azure Cosmos DB’yi kullanmaya başlayabilirsiniz.

[1]: ./media/documentdb-introduction/json-database-resources1.png

