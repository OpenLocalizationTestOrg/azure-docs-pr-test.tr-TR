---
title: "Azure Search hakkında sık sorulan sorular (SSS) | Microsoft Docs"
description: "Microsoft Azure arama hizmeti ilgili sık sorulan soruların yanıtlarını alın"
services: search
author: HeidiSteen
manager: jhubbard
ms.service: search
ms.technology: search
ms.topic: article
ms.date: 08/03/2017
ms.author: heidist
ms.openlocfilehash: 02d5fac8cf9067ec544668f306fe49b805b3d164
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-search---frequently-asked-questions-faq"></a>Azure Search - sık sorulan sorular (SSS)
 
 Kavramları, kod ve Azure Search ilgili senaryoları hakkında sık sorulan soruların yanıtlarını bulun.

## <a name="platform"></a>Platform

### <a name="how-is-azure-search-different-from-full-text-search-in-my-dbms"></a>Azure Search my DBMS tam metin aramasını farklı mı?

Azure arama destekleyen birden çok veri kaynağı, [birçok diller için dil analiz](https://docs.microsoft.com/rest/api/searchservice/language-support), [ilginç ve olağan dışı veri girişlerini özel analize](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search), ara sıra denetimlerde [profilleri Puanlama](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)ve kullanıcı deneyimi özellikleri typeahead, isabet vurgulama ve çok yönlü gezinmeyi gibi. Ayrıca eş anlamlıları ve zengin sorgu sözdizimi gibi diğer özellikler içerir, ancak bunlar genellikle özellikleri ayrım değil.

### <a name="what-is-the-difference-between-azure-search-and-elasticsearch"></a>Azure Search Elasticsearch arasındaki fark nedir?

Arama teknolojileri karşılaştırıldığında, müşterilerin Azure Search ile Elasticsearch nasıl karşılaştırır özellikleri için sık isteyin. Azure Search Elasticsearch kendi arama uygulaması projeleri genellikle Seç müşteriler anahtar görev daha kolay yaptık veya diğer Microsoft teknolojileri ile dahili tümleştirmeyi gerekir çünkü bunu:

+ Yeterli artıklık (2 çoğaltma okuma erişimi için okuma-yazma için 3 çoğaltmalarını) ile sağlanan olduğunda, Azure arama % 99,9 Hizmet düzeyi sözleşmelerine (SLA) ile tam olarak yönetilen bulut hizmeti kullanır.
+ Microsoft'un [doğal dil işlemciler](https://docs.microsoft.com/rest/api/searchservice/language-support) önde gelen inguistic analiz sunar.  
+ [Azure Search dizin oluşturucular](search-indexer-overview.md) ilk ve artımlı dizin oluşturma için Azure veri kaynaklarının çeşitli gezinme.
+ Sorgu veya birimleri dizinini dalgalanmalara hızlı yanıta gerekiyorsa, kullanabileceğiniz [kaydırıcı denetimlerini](search-manage.md#scale-up-or-down) Azure portal ya da çalışma bir [PowerShell Betiği](search-manage-powershell.md), parça yönetim doğrudan atlama.  
+ [Puanlama ve özelliklerini ayarlama](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) arama ne tek başına arama motoru sağlayabilir ötesinde derecelendirme puanlarını etkileyen için yöntemler sağlar. 

### <a name="can-i-pause-azure-search-service-and-stop-billing"></a>I Azure Search Hizmeti durdurabilir ve faturalama Durdur?

Hizmeti duraklatma olamaz. Hizmet oluşturulduğunda, hesaplama ve depolama kaynakları özel kullanım için ayrılır. Serbest bırakır ve bu kaynakları isteğe bağlı geri mümkün değil. 

## <a name="indexing-operations"></a>Dizin oluşturma işlemleri

### <a name="backup-and-restore-or-download-and-move-indexes-or-index-snapshots"></a>Yedekleme ve geri yükleme (veya indirme ve taşıma) dizinleri ve dizin anlık görüntüleri?

Ancak [dizin tanımı Al](https://docs.microsoft.com/rest/api/searchservice/get-index) herhangi bir zamanda olduğundan hiçbir Dizin ayıklama, anlık görüntü veya karşıdan yüklemek için Yedekleme Geri Yükleme özelliği bir *doldurulmuş* yerel sistemde bulutta çalışan ya da başka bir Azure Search hizmetini taşımadan dizin. 

Dizin oluşturulmuş ve yazma ve yalnızca Azure Search bulutta çalışan kodundan doldurulur. Genellikle, başka bir hizmete bir dizin taşımak istediğiniz müşteriler kendi kodu yeni bir uç noktası kullanacak şekilde düzenleyerek bunu ve yeniden dizin oluşturma işlemi yeniden çalıştırın. Bir anlık görüntüsünü veya bir dizin Yedekleme olanağı istiyorsanız, bir oy cast [kullanıcı sesi](https://feedback.azure.com/forums/263029-azure-search/suggestions/8021610-backup-snapshot-of-index).

### <a name="can-i-index-from-sql-database-replicas-applies-to-azure-sql-database-indexershttpsdocsmicrosoftcomazuresearchsearch-howto-connecting-azure-sql-database-to-azure-search-using-indexers"></a>SQL veritabanı çoğaltmalardan dizin oluşturabilirsiniz (uygulandığı [Azure SQL veritabanı dizin oluşturucular](https://docs.microsoft.com/azure/search/search-howto-connecting-azure-sql-database-to-azure-search-using-indexers))

 Kısıtlama yoktur kullanımı birincil veya ikincil çoğaltmaların bir veri kaynağı olarak bir dizini sıfırdan oluştururken. Ancak, artımlı güncelleştirmeler (değiştirilen kayıtlarda dayanarak) sahip bir dizin yenileme birincil çoğaltma gerektirir. Bu gereksinim SQL veritabanı, değişiklik izleme, yalnızca birincil çoğaltmalar üzerinde hangi garanti gelir. Bir dizin yenileme iş yükü için ikincil çoğaltmaları kullanmayı deneyin, tüm verileri almak garanti yoktur.

## <a name="search-operations"></a>Arama işlemleri

### <a name="can-i-search-across-multiple-indexes"></a>Birden çok dizin arasında arama yapabilirsiniz?

Hayır, bu işlem desteklenmiyor. Arama her zaman tek bir dizin kapsamlıdır.

### <a name="can-i-restrict-search-corpus-access-by-user-identity"></a>Kullanıcı kimliğine göre arama gövde erişimi kısıtlayabilir miyiz?

Azure arama, kullanıcı başına veri erişimi için bir rol tabanlı güvenlik modeli yok. Kimlik doğrulaması ya da tam hakları olduğundan veya salt okunur hizmet düzeyinde. Bazı müşteriler göre çözümleri uyguladık [ `$filter` arama parametresi](https://docs.microsoft.com/rest/api/searchservice/search-documents), ancak en iyi bir çözüm olabilir. Bu özellik istiyorsanız, bir oy cast [kullanıcı sesi](https://feedback.azure.com/forums/263029-azure-search/category/86074-security).

### <a name="why-are-there-zero-matches-on-terms-i-know-to-be-valid"></a>Neden sıfır vardır, geçerli olması için bilebilirim koşullarınızda eşleşen?

En yaygın durumda her sorgu türü farklı arama davranışlarını ve dil çözümlemeler düzeylerini destekler bilmektir değil. Baskın iş yükü olan tam metin arama terimleri kök forms aşağıya doğru keser dil analiz aşaması içerir. Daha fazla sayıda çeşitlemesi parçalanmış terimini içerdiğinden sorgu ayrıştırma bu nokta daha geniş bir net olası eşleşmeler çevirir.

Çağırmayı varsa [diğer sorgu türleri](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (joker karakter arama, benzer arama, yakınlık araması, diğerlerinin yanı sıra öneriler), hiçbir dil analiz yoktur. Koşulları sorgu ağaç olarak eklenir-değil. 

### <a name="why-is-the-search-rank-a-constant-or-equal-score-of-10-for-every-hit"></a>Neden arama sıralamasını sabit ya da eşit skoru 1.0 her isabet için mi?

Varsayılan olarak, arama sonuçları göre puanlanır [koşulları eşleşen istatistiksel özellikleri](search-lucene-query-architecture.md#stage-4-scoring)ve yüksek düşük sonuç kümesi sipariş. Ancak, bazı türleri (joker karakter öneki, regex) sorgu her zaman genel belge puan için sabit bir puan katkıda bulunun. Bu davranış tasarım gereğidir. Azure arama sonuçlarında derecelendirme etkilemeden dahil edilecek sorgu genişletme bulunan eşleşmeler izin vermek için sabit bir puan uygular. 

Örneğin, "tur", "tourettes" ve "tourmaline" eşleşmeleri girişi "tur *" joker karakter aramaya üreten varsayalım. Bu sonuçları yapısını verildiğinde, hangi koşulları diğerlerinden daha değerli makul çıkarsamak için bir yolu yoktur. Bu nedenle, biz terim sıklıklarını sonuçları türleri joker karakter, önek ve regex sorgularda Puanlama zaman yoksay. Kısmi girişinize göre arama sonuçları, büyük olasılıkla beklenmeyen eşleşen doğru sapması önlemek için sabit bir puan verilir.

## <a name="design-patterns"></a>Tasarım desenleri

### <a name="what-is-the-best-approach-for-implementing-localized-search"></a>Yerelleştirilmiş arama uygulamak için en iyi yaklaşımı nedir?

Aynı dizinde farklı yerel ayarlara (dilleri) destek geldiğinde müşterilerin çoğu ayrılmış alanlar içinde bir koleksiyon seçin. Yerel ayarlara özgü alanlarını uygun Çözümleyicisi Ata mümkün kılar. Örneğin, Microsoft Fransızca Çözümleyicisi Fransızca dizeleri içeren bir alana atama. Ayrıca, filtreleme basitleştirir. Bir sorgu fr-fr sayfasında başlatılan biliyorsanız, bu alan için arama sonuçları sınırlayabilir. Ya da oluşturma bir [profil Puanlama](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) alan daha fazla göreli ağırlık vermek için.

## <a name="next-steps"></a>Sonraki adımlar

Eksik bir özellik veya işlev hakkında soru mi? Özellik üzerinde istek [kullanıcı sesi web sitesi](https://feedback.azure.com/forums/263029-azure-search).

## <a name="see-also"></a>Ayrıca bkz.

 [StackOverflow: Azure arama](https://stackoverflow.com/questions/tagged/azure-search)   
 [Azure Search'te nasıl tam metin araması çalışır](search-lucene-query-architecture.md)  
 [Azure Search nedir?](search-what-is-azure-search.md)

 