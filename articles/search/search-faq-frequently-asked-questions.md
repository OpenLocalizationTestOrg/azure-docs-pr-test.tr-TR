---
title: "Azure Search hakkında sorulan sorular (SSS) aaaFrequently | Microsoft Docs"
description: "Microsoft Azure arama hizmeti hakkında toocommon soruların yanıtlarını alın"
services: search
author: HeidiSteen
manager: jhubbard
ms.service: search
ms.technology: search
ms.topic: article
ms.date: 08/03/2017
ms.author: heidist
ms.openlocfilehash: 2c573750600d80585b746bfce20d6c0f8df5a262
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search---frequently-asked-questions-faq"></a>Azure Search - sık sorulan sorular (SSS)
 
 Yanıtlar toocommonly ilgili kavramları, kod ve senaryoları tooAzure arama ile ilgili sorular bulun.

## <a name="platform"></a>Platform

### <a name="how-is-azure-search-different-from-full-text-search-in-my-dbms"></a>Azure Search my DBMS tam metin aramasını farklı mı?

Azure arama destekleyen birden çok veri kaynağı, [birçok diller için dil analiz](https://docs.microsoft.com/rest/api/searchservice/language-support), [ilginç ve olağan dışı veri girişlerini özel analize](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search), ara sıra denetimlerde [profilleri Puanlama](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)ve kullanıcı deneyimi özellikleri typeahead, isabet vurgulama ve çok yönlü gezinmeyi gibi. Ayrıca eş anlamlıları ve zengin sorgu sözdizimi gibi diğer özellikler içerir, ancak bunlar genellikle özellikleri ayrım değil.

### <a name="what-is-hello-difference-between-azure-search-and-elasticsearch"></a>Azure Search Elasticsearch arasındaki hello fark nedir?

Arama teknolojileri karşılaştırıldığında, müşterilerin Azure Search ile Elasticsearch nasıl karşılaştırır özellikleri için sık isteyin. Azure Search Elasticsearch kendi arama uygulaması projeleri genellikle Seç müşteriler anahtar görev daha kolay yaptık veya diğer Microsoft teknolojileri ile Merhaba yerleşik tümleştirme gerekir çünkü bunu:

+ Yeterli artıklık (2 çoğaltma okuma erişimi için okuma-yazma için 3 çoğaltmalarını) ile sağlanan olduğunda, Azure arama % 99,9 Hizmet düzeyi sözleşmelerine (SLA) ile tam olarak yönetilen bulut hizmeti kullanır.
+ Microsoft'un [doğal dil işlemciler](https://docs.microsoft.com/rest/api/searchservice/language-support) önde gelen inguistic analiz sunar.  
+ [Azure Search dizin oluşturucular](search-indexer-overview.md) ilk ve artımlı dizin oluşturma için Azure veri kaynaklarının çeşitli gezinme.
+ Sorgu veya birimleri dizin hızlı yanıt toofluctuations gerekiyorsa, kullanabileceğiniz [kaydırıcı denetimlerini](search-manage.md#scale-up-or-down) hello Azure portal ya da çalışma içinde bir [PowerShell Betiği](search-manage-powershell.md), parça yönetim doğrudan atlama.  
+ [Puanlama ve özelliklerini ayarlama](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) hello hangi hello arama motoru başına sağlayabilir ötesinde arama derece puanları etkileyen sunar. 

### <a name="can-i-pause-azure-search-service-and-stop-billing"></a>I Azure Search Hizmeti durdurabilir ve faturalama Durdur?

Merhaba hizmetini duraklatmak olamaz. Merhaba hizmet oluşturulduğunda, hesaplama ve depolama kaynakları özel kullanım için ayrılır. Olası toorelease değildir ve bu kaynakları isteğe bağlı geri alma. 

## <a name="indexing-operations"></a>Dizin oluşturma işlemleri

### <a name="backup-and-restore-or-download-and-move-indexes-or-index-snapshots"></a>Yedekleme ve geri yükleme (veya indirme ve taşıma) dizinleri ve dizin anlık görüntüleri?

Ancak [dizin tanımı Al](https://docs.microsoft.com/rest/api/searchservice/get-index) herhangi bir zamanda olduğundan hiçbir Dizin ayıklama, anlık görüntü veya karşıdan yüklemek için Yedekleme Geri Yükleme özelliği bir *doldurulmuş* hello bulut tooa yerel sistem, dizin veya tooanother Azure Search Hizmeti taşıma. 

Dizin oluşturulmuş ve yazma ve yalnızca Azure Search hello bulutta çalışan kodundan doldurulur. Genellikle, toomove bir dizini tooanother hizmeti isteyen müşteriler kendi kod toouse yeni bir uç noktası düzenleyerek bunu ve yeniden dizin oluşturma işlemi yeniden çalıştırın. Merhaba özelliği tootake bir anlık görüntü istediğiniz veya bir dizin yedekleme, bir oy cast [kullanıcı sesi](https://feedback.azure.com/forums/263029-azure-search/suggestions/8021610-backup-snapshot-of-index).

### <a name="can-i-index-from-sql-database-replicas-applies-tooazure-sql-database-indexershttpsdocsmicrosoftcomazuresearchsearch-howto-connecting-azure-sql-database-to-azure-search-using-indexers"></a>SQL veritabanı çoğaltmalardan dizin oluşturabilirsiniz (çok geçerlidir[Azure SQL veritabanı dizin oluşturucular](https://docs.microsoft.com/azure/search/search-howto-connecting-azure-sql-database-to-azure-search-using-indexers))

 Kısıtlama yoktur hello kullanımda birincil veya ikincil çoğaltmaların bir veri kaynağı olarak bir dizini sıfırdan oluştururken. Ancak, artımlı güncelleştirmeler (değiştirilen kayıtlarda dayanarak) sahip bir dizin yenileme hello birincil çoğaltma gerektirir. Bu gereksinim SQL veritabanı, değişiklik izleme, yalnızca birincil çoğaltmalar üzerinde hangi garanti gelir. Bir dizin yenileme iş yükü için ikincil çoğaltmaları kullanmayı deneyin, tüm hello veri almak garanti yoktur.

## <a name="search-operations"></a>Arama işlemleri

### <a name="can-i-search-across-multiple-indexes"></a>Birden çok dizin arasında arama yapabilirsiniz?

Hayır, bu işlem desteklenmiyor. Arama her zaman kapsamlı tooa tek dizinidir.

### <a name="can-i-restrict-search-corpus-access-by-user-identity"></a>Kullanıcı kimliğine göre arama gövde erişimi kısıtlayabilir miyiz?

Azure arama, kullanıcı başına veri erişimi için bir rol tabanlı güvenlik modeli yok. Kimlik doğrulaması ya da tam hakları olduğundan veya salt okunur hello hizmeti düzeyinde. Bazı müşteriler göre çözümleri uyguladık [ `$filter` arama parametresi](https://docs.microsoft.com/rest/api/searchservice/search-documents), ancak en iyi bir çözüm olabilir. Bu özellik istiyorsanız, bir oy cast [kullanıcı sesi](https://feedback.azure.com/forums/263029-azure-search/category/86074-security).

### <a name="why-are-there-zero-matches-on-terms-i-know-toobe-valid"></a>Neden sıfır vardır, geçerli toobe bilmeniz koşullarınızda eşleşen?

Merhaba en yaygın durumda her sorgu türü farklı arama davranışlarını ve dil çözümlemeler düzeylerini destekler bilmektir değil. Merhaba baskın iş yükü olan tam metin arama terimleri tooroot forms aşağı keser dil analiz aşaması içerir. Merhaba parçalanmış çeşitleri daha fazla sayıda terimini içerdiğinden sorgu ayrıştırma bu nokta daha geniş bir net olası eşleşmeler çevirir.

Çağırmayı varsa [diğer sorgu türleri](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (joker karakter arama, benzer arama, yakınlık araması, diğerlerinin yanı sıra öneriler), hiçbir dil analiz yoktur. Koşulları toohello sorgu ağaç olarak eklenen-değil. 

### <a name="why-is-hello-search-rank-a-constant-or-equal-score-of-10-for-every-hit"></a>Neden hello arama sıralamasını sabit ya da eşit skoru 1.0 her isabet için mi?

Varsayılan olarak, arama sonuçları tabanlı hello üzerinde puanlanır [koşulları eşleşen istatistiksel özellikleri](search-lucene-query-architecture.md#stage-4-scoring)ve yüksek toolow hello sonuç kümesinde sipariş. Ancak, bazı türleri (joker karakter öneki, regex) sorgu her zaman sabit bir puan katkıda toohello genel belge puanı. Bu davranış tasarım gereğidir. Azure arama uygular bir sabit hello derecelendirme etkilemeden hello sonuçlara dahil sorgu genişletme toobe aracılığıyla bulunan tooallow eşleşmeler puan. 

Örneğin, "tur", "tourettes" ve "tourmaline" eşleşmeleri girişi "tur *" joker karakter aramaya üreten varsayalım. Bu sonuçları Hello yapısını verildiğinde, hangi koşulları diğerlerinden daha değerli tooreasonably Infer yolu yoktur. Bu nedenle, biz terim sıklıklarını sonuçları türleri joker karakter, önek ve regex sorgularda Puanlama zaman yoksay. Kısmi girişinize göre arama sonuçları bir sabit verilen puan tooavoid sapması büyük olasılıkla beklenmeyen eşleşmeleri bulunun.

## <a name="design-patterns"></a>Tasarım desenleri

### <a name="what-is-hello-best-approach-for-implementing-localized-search"></a>Yerelleştirilmiş arama uygulama için en iyi yaklaşımı hello nedir?

Toosupporting farklı yerlerde (dilleri) hello geldiğinde müşterilerin çoğu ayrılmış alanlar içinde bir koleksiyon seçin. aynı dizin. Yerel ayarlara özgü alanları olası tooassign uygun Çözümleyicisi kolaylaştırır. Örneğin, Fransızca dizeleri içeren hello Microsoft Fransızca Çözümleyicisi tooa alan atama. Ayrıca, filtreleme basitleştirir. Bir sorgu fr-fr sayfasında başlatılan biliyorsanız, arama sonuçları toothis alanı sınırlayabilir. Ya da oluşturma bir [profil Puanlama](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) toogive hello alan daha fazla göreli ağırlık.

## <a name="next-steps"></a>Sonraki adımlar

Eksik bir özellik veya işlev hakkında soru mi? Merhaba Hello özelliğini isteği [kullanıcı sesi web sitesi](https://feedback.azure.com/forums/263029-azure-search).

## <a name="see-also"></a>Ayrıca bkz.

 [StackOverflow: Azure arama](https://stackoverflow.com/questions/tagged/azure-search)   
 [Azure Search'te nasıl tam metin araması çalışır](search-lucene-query-architecture.md)  
 [Azure Search nedir?](search-what-is-azure-search.md)

 