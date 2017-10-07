---
title: "aaaAzure depolama tablo Tasarım Kılavuzu | Microsoft Docs"
description: "Tasarım ölçeklenebilir ve kullanıcı tablolarında Azure tablo depolaması"
services: cosmos-db
documentationcenter: na
author: mimig1
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 059f05a1d20e4d9537034b7ca133c5334bbefa04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a>Azure depolama tablo Tasarım Kılavuzu: Ölçeklenebilir tasarlama ve kullanıcı tabloları
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

toodesign ölçeklenebilir ve kullanıcı tabloları bir dizi etkene performans, ölçeklenebilirlik ve maliyet gibi dikkate almanız gerekir. Daha önce şemaları ilişkisel veritabanları için tasarlanmış, bu noktalar tanıdık tooyou olacaktır, ancak bazı benzerlikler hello Azure Table hizmet depolama modeli ve ilişkisel modelleri arasında olsa da, de vardır birçok önemli farkları. Bu farklılıklar, genellikle counter-intuitive veya yanlış toosomeone ilişkisel veritabanları ile tanıdık görünebilir, ancak hello Azure tablo hizmeti gibi bir NoSQL anahtar/değer deposu için tanımlıyorsanız, iyi bir fikir hale getirmeyin toovery farklı tasarımları yol açar. Tasarım farklar çoğunu hello tablo hizmeti varlıkları (ilişkisel veritabanı terminolojisi bulunan satırlar) veri veya çok yüksek desteklemelidir veri kümeleri için milyarlarca içerebilir tasarlanmış toosupport bulut ölçekli uygulamalar olduğunu hello olgu yansıtır işlem hacmi: Bu nedenle, verilerinizi depolamak nasıl hakkında farklı toothink gerekir ve hello tablo hizmeti nasıl çalıştığını anlayın. İyi tasarlanmış bir NoSQL veri deposu, çözüm tooscale çok daha fazla (ve daha düşük maliyetle) etkinleştirebilirsiniz bir çözümden bir ilişkisel veritabanı kullanır. Bu kılavuz, bu konularda yardımcı olur.  

## <a name="about-hello-azure-table-service"></a>Azure tablo hizmeti Hello hakkında
Bu bölümde bazı performans ve ölçeklenebilirlik için özellikle ilgili toodesigning olan hello anahtar özelliklerinden biri hello tablo hizmeti vurgular. Yeni tooAzure depolama ve hello tablo hizmeti varsa, ilk okuma [giriş tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) ve [.NET kullanarak Azure Table Storage ile çalışmaya başlama](table-storage-how-to-use-dotnet.md) hello geri kalanında bu okuma önce makale. Bu kılavuzun Hello odak hello tablo hizmeti üzerinde olsa da, bazı tartışma hello Azure kuyruk ve Blob Hizmetleri ve hello tablo hizmeti bir çözümde yanı sıra bunları nasıl kullanacağınızı içerecektir.  

Merhaba tablo hizmeti nedir? Merhaba adından beklediğiniz gibi hello tablo hizmeti bir tablo biçiminde toostore verileri kullanır. Merhaba standart terminoloji, Merhaba tablonun her satırında bir varlığı temsil eden ve hello sütun deposu hello çeşitli özelliklerini varlık. Her varlık anahtarları toouniquely tanımlamak çifti vardır ve hello varlık son güncelleştirildiği tablo hizmeti hello bir zaman damgası sütunu tootrack kullanır (Bu otomatik olarak gerçekleşir ve el ile rastgele bir değerle hello zaman damgası üzerine yazılamıyor). Bu son değiştirilen zaman damgası (LMT) toomanage iyimser eşzamanlılık Hello tablo hizmeti kullanır.  

> [!NOTE]
> Merhaba tablo hizmeti REST API işlemleri aynı zamanda sonuç bir **ETag** hello son değiştirilen timestamp (LMT) türetilen değeri. Toohello başvurduğundan kullanacağız bu belgede hello ETag ve LMT birbirinin yerine koşulları aynı alttaki verileri.  
> 
> 

Merhaba aşağıdaki örnekte basit bir tablo Tasarım toostore çalışan ve departman varlıkları gösterilmektedir. Bu kılavuzda gösterilen hello örnekler çoğunu basit bu tasarım temel alır.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>zaman damgası</th>
<th></th>
</tr>
<tr>
<td>Pazarlama</td>
<td>00001</td>
<td>2014-08-22T00:50:32Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>Soyadı</th>
<th>Yaş</th>
<th>E-posta</th>
</tr>
<tr>
<td>Tan</td>
<td>Hall</td>
<td>34</td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Pazarlama</td>
<td>00002</td>
<td>2014-08-22T00:50:34Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>Soyadı</th>
<th>Yaş</th>
<th>E-posta</th>
</tr>
<tr>
<td>Haz</td>
<td>CAO</td>
<td>47</td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Pazarlama</td>
<td>Bölüm</td>
<td>2014-08-22T00:50:30Z</td>
<td>
<table>
<tr>
<th>departmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>Pazarlama</td>
<td>153</td>
</tr>
</table>
</td>
</tr>
<tr>
<td>Satış</td>
<td>00010</td>
<td>2014-08-22T00:50:44Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>Soyadı</th>
<th>Yaş</th>
<th>E-posta</th>
</tr>
<tr>
<td>Ken</td>
<td>Kwok</td>
<td>23</td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


Şu ana kadar bu çok benzer tooa tablo bir ilişkisel veritabanı hello zorunlu sütunları olan hello anahtar farklılıklar arar ve hello özelliği toostore birden çok varlık hello türleri aynı tablo. Ayrıca, her biri hello kullanıcı tanımlı özellikler gibi **FirstName** veya **yaş** tamsayı veya dize, yalnızca gibi ilişkisel bir veritabanındaki sütun gibi bir veri türüne sahip. Aksine hello şema daha az yapısı hello bir özellik değil olmak zorunda tablo hizmeti anlamına gelir, bir ilişkisel veritabanı içinde hello rağmen aynı her varlıkta veri türü. tek bir özellik toostore karmaşık veri türleri, JSON veya XML gibi bir seri hale getirilmiş biçimi kullanmalıdır. Hello tablo hizmeti gibi desteklenen veri türleri, desteklenen bir tarih aralıkları, adlandırma kuralları ve boyutu kısıtlamaları hakkında daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Göreceğiniz gibi tercih ettiğiniz **PartitionKey** ve **RowKey** temel toogood tablo tasarımdır. Bir tablodaki her varlığın benzersiz bir birleşimi olmalıdır **PartitionKey** ve **RowKey**. Anahtarlarla gibi bir ilişkisel veritabanı tablosundaki, hello **PartitionKey** ve **RowKey** değerler dizinli toocreate hızlı göz atmayı sağlayan bir kümelenmiş dizin, ancak tablo hizmeti hello herhangi oluşturmaz. Bunlar hello; bu nedenle ikincil dizinler yalnızca iki özellikleri (daha sonra açıklanan hello desenleri bazıları görünen bu sınırlamaya geçici nasıl çalışabileceğini Göster) dizini.  

Bir tablo bir veya daha fazla bölümlerini yapılır ve göreceğiniz gibi birçok hello uygun bir seçme geçici olması kararları tasarım **PartitionKey** ve **RowKey** toooptimize çözümünüzü. Tablonun tüm varlıklar bölümlere düzenlenmiş içeren yalnızca tek bir çözüm oluşabilir, ancak bir çözüm, birden çok tablo genellikle sahip olacaktır. Tabloları yardımcı toologically varlıklarınızı düzenlemek, yönettiğiniz erişim toohello verileri kullanarak Yardım erişim denetim listeleri ve tek bir depolama işlemi kullanarak tüm bir tabloyu düşürebilir.  

### <a name="table-partitions"></a>Tablo bölümleri
Merhaba hesap adı, tablo adı ve **PartitionKey** birlikte hello bölümü hello tablo hizmeti hello varlık depoladığı hello depolama hizmeti içinde tanımlayın. Bölüm işlemleri için kapsam tanımlayın adresleme düzeni varlıklar için hello parçası olmasının yanı sıra, (bkz [varlık Grup hareketleri](#entity-group-transactions) aşağıda) ve nasıl hello tablo hizmeti ölçekler, form hello temel. Bölümleri hakkında daha fazla bilgi için bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](../storage/common/storage-scalability-targets.md).  

Hello tablo hizmeti, hizmetlerini tek tek bir düğüm tek tek veya daha fazla bölümleri tamamlayın ve dinamik Yük Dengeleme tarafından hizmet ölçekler hello düğümleri arasında bölümler. Bir düğümü yük altında ise hello tablo hizmeti için *bölme* bölümleri hello aralığı hizmet farklı düğümleri üzerine bu düğüm tarafından; trafiği subsides hello hizmet yapabilirsiniz *birleştirme* hello bölüm aralıkları Sessiz düğümlerini tek bir düğüme yedekleyin.  

Merhaba hakkında daha fazla bilgi için iç ayrıntılarını hello tablo hizmeti ve bölümler, hello hizmet yöneten nasıl özellikle hello incelemesine bakın [Microsoft Azure Storage: yüksek oranda kullanılabilir bulut depolama hizmet güçlü tutarlılık](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).  

### <a name="entity-group-transactions"></a>Varlık Grup işlemleri
Hello tablo hizmeti, varlık Grup hareketleri (EGTs) birden çok varlık arasında atomik güncelleştirmeleri gerçekleştirme hello yalnızca yerleşik sistemdir. EGTs olan de başvurulan tooas *toplu işlemler* bazı belgelerde. EGTs yalnızca çalışabilir hello saklanan varlıkları aynı bölüme (paylaşım hello verilen bir tablodaki aynı bölüm anahtarı), birden çok varlık arasında atomik işlem davranışı gereken herhangi bir zamanda bu varlıklardır hello tooensure gerekir böylece aynı bölüm. Genellikle birden fazla tablo farklı varlık türlerine yönelik kullanmayan ve birden çok varlık türleri aynı tablo (ve bölüm) hello tutulması için bir neden de budur. Tek bir EGT en fazla 100 varlık üzerinde çalışabilir.  Bu EGTs işlemeyi önemli tooensure için birden çok eşzamanlı EGTs gönderirseniz, aksi takdirde işleme Gecikmeli olarak EGTs arasında ortak olan varlıklar üzerinde çalıştırmayın.

EGTs Ayrıca, tooevaluate tasarımınızda için olası dengelemeyi tanıtmak: daha fazla bölüm kullanarak artıracaktır hello ölçeklenebilirlik, uygulamanızın Azure düğümleri arasında dengelemesini istekleri için daha fazla fırsatlarını sahiptir, ancak bu hello sınırlayabilir Uygulama tooperform atomik işlemleri yeteneklerini ve verileriniz için güçlü tutarlılık sağlamak. Ayrıca, vardır belirli ölçeklenebilirlik hedefleri için tek bir düğüm beklediğiniz işlemleri hello verimini sınırlayabilir bir bölümün hello düzeyinde: Azure depolama hesapları ve hello tablo için hello ölçeklenebilirlik hedefleri hakkında daha fazla bilgi hizmet için bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](../storage/common/storage-scalability-targets.md). Bu kılavuzun sonraki bölümlerde ele çeşitli tasarım yardımcı stratejileri dengelemeler gibi bu yönetmek ve en iyi şekilde nasıl toochoose bölüm anahtarı hello belirli istemci uygulamanızın gereksinimlerine göre tartışın.  

### <a name="capacity-considerations"></a>Kapasite dikkat edilecek noktalar
Merhaba aşağıdaki tabloda bazı hello anahtar değerleri toobe ne zaman, bir tablo hizmeti çözümü tasarlarken farkında içerir:  

| Bir Azure depolama hesabının toplam kapasite | 500 TB |
| --- | --- |
| Bir Azure depolama hesabı tablo sayısı |Merhaba hello depolama hesabı kapasitesini yalnızca sınırlıdır |
| Bir tabloda bölüm sayısı |Merhaba hello depolama hesabı kapasitesini yalnızca sınırlıdır |
| Bir bölümdeki varlıkların sayısı |Merhaba hello depolama hesabı kapasitesini yalnızca sınırlıdır |
| Tek bir varlık boyutu |Yukarı too1 MB ile en fazla 255 özellikleri (Merhaba dahil olmak üzere **PartitionKey**, **RowKey**, ve **zaman damgası**) |
| Merhaba boyutunu **PartitionKey** |Too1 KB boyutunda bir dize |
| Merhaba boyutunu **RowKey** |Too1 KB boyutunda bir dize |
| Bir varlık grubu işlem boyutu |Bir işlem en fazla 100 varlık içerebilir ve hello yükü boyutu 4 MB'den az olmalıdır. Bir EGT yalnızca bir kez bir varlık güncelleştirebilirsiniz. |

Daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini](http://msdn.microsoft.com/library/azure/dd179338.aspx).  

### <a name="cost-considerations"></a>Maliyet dikkat edilecek noktalar
Tablo depolama oldukça masrafsız, ancak her iki kapasite kullanımı ve hello miktarını işlemleri için maliyet tahminleri değerlendirmenize hello tablo hizmeti kullanan herhangi bir çözümünün bir parçası olarak içermelidir. Ancak, sipariş tooimprove hello Normalleştirilmemiş veya yinelenen veri depolama Çoğu senaryoda performans ve ölçeklenebilirliği çözümünüzün geçerli bir yaklaşım tootake olur. Fiyatlandırma hakkında daha fazla bilgi için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/).  

## <a name="guidelines-for-table-design"></a>Tablo Tasarımı için yönergeler
Bu listeler hello anahtar yönergeleri tablolarınızı tasarlarken göz önünde bulundurmanız gereken bazı özetlemek ve bu kılavuzda bunları daha ayrıntılı daha sonra da değerlendirecektir. Bu yönergeler, ilişkisel veritabanı tasarımı için genellikle izlersiniz hello yönergeleri çok farklıdır.  

Tablo hizmeti çözüm toobe tasarlama *okuma* verimli:

* ***Okuma ağır uygulamalarda sorgulamaya tasarlayın.*** Tabloları tasarlarken, yürütecek hello sorguları hakkında (özellikle hello gecikme önemli olanları) düşündüğünüz varlıklarınızı nasıl güncelleştirecektir hakkında düşünmek önce. Bu genellikle bir verimli ve kullanıcı çözümde sonuçlanır.  
* ***PartitionKey ve RowKey sorgularınızda belirtin.*** *Noktası sorguları* hello en verimli tablo hizmeti sorguları bunlar gibi.  
* ***Varlıkları yinelenen kopyalarını depolamayı düşünün.*** Tablo depolama ucuz böylece göz önünde bulundurun birden çok kez (anahtarları farklı) hello aynı varlığa depolama tooenable daha verimli sorgular.  
* ***Verilerinizi denormalizing göz önünde bulundurun.*** Tablo depolama ucuz böylece verilerinizi denormalizing göz önünde bulundurun. Örneğin, veri toplama için sorgular yalnızca tek bir varlık tooaccess gerekir böylece Özet varlıklar depolayın.  
* ***Bileşik anahtar değerlerini kullanın.*** Merhaba yalnızca sahip olduğunuz anahtarları olan **PartitionKey** ve **RowKey**. Örneğin, bileşik anahtar değerlerinden tooenable diğer anahtarlı erişim yolları tooentities kullanın.  
* ***Sorgu projeksiyon kullanın.*** Merhaba yalnızca gereksinim duyduğunuz hello alanları seçin sorgularını kullanarak hello ağ üzerinden aktarım veri miktarını azaltır.  

Tablo hizmeti çözüm toobe tasarlama *yazma* verimli:  

* ***Sık kullanılan bölümleri oluşturmayın.*** Toospread etkinleştirme anahtarları isteklerinizi zaman herhangi bir noktada birden çok bölüm arasında seçin.  
* ***Ani trafiğinin kaçının.*** Merhaba trafik makul bir süre boyunca kesintisiz ve ani trafiğinin kaçının.
* ***Her varlık türü için ayrı bir tablo mutlaka oluşturmayın.*** Varlık türlerine atomik işlemleri gerektiğinde, bu birden çok varlık türleri aynı bölüm hello hello depolayabilirsiniz aynı tablo.
* ***Merhaba en yüksek verimlilik elde gerekir göz önünde bulundurun.*** Merhaba tablo hizmeti için hello ölçeklenebilirlik hedefleri unutmayın ve tasarımınızı, tooexceed neden olmak bunları.  

Bu kılavuzu okumadan gibi tüm bu ilkeler uygulamaya koymanın örnekler görürsünüz.  

## <a name="design-for-querying"></a>Sorgulama için Tasarım
Tablo hizmeti çözümleri yoğun, yazma yoğun ya da bir karışımını hello iki okuyabilirsiniz. Okuma işlemleri verimli bir şekilde, tablo hizmeti toosupport tasarlarken Bu bölümde hello şeyler toobear aklınızda odaklanır. Genellikle, desteklediği işlemleri verimli bir şekilde okuma tasarım de yazma işlemleri için verimli olur. Ancak, alırken ek hususlar toobear göz önünde tasarlama toosupport yazma işlemleri, hello sonraki bölümde açıklanan [veri değişikliği için tasarım](#design-for-data-modification).

"Tablo hizmeti çözüm tooenable tasarlamak için iyi bir başlangıç noktası, tooread veri verimli bir şekilde tooask sorguları tablo hizmeti hello gereken uygulama gereksinimi tooexecute tooretrieve hello verilerimi uygulamak?" olacaktır  

> [!NOTE]
> Merhaba tablo hizmeti zor ve pahalı toochange olduğundan tooget tasarım doğru Önden hello. önemlidir, daha sonra. Örneğin, genellikle olmasından ilişkisel bir veritabanında ekleyerek yalnızca olası tooaddress performans sorunlarını dizinler tooan varolan bir veritabanını: Bu hello tablo hizmeti ile bir seçenek değil.  
> 
> 

Bu bölümde hello anahtar sorunları sorgulamak için tabloları tasarlarken çözülmesi gereken odaklanır. Bu bölümde yer alan hello konular şunlardır:

* [PartitionKey ve RowKey seçiminizi sorgu performansını nasıl etkilediğini](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [Uygun bir PartitionKey seçme](#choosing-an-appropriate-partitionkey)
* [Sorguları hello tablo hizmeti için en iyi duruma getirme](#optimizing-queries-for-the-table-service)
* [Merhaba tablo hizmeti veri sıralama](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a>PartitionKey ve RowKey seçiminizi sorgu performansını nasıl etkilediğini
Merhaba aşağıdaki örneklerde hello tablo hizmeti ile Merhaba yapı izlenerek çalışan varlıkları depolamak varsayılmaktadır (Merhaba örnekler çoğunu atlayın hello **zaman damgası** özelliği daha anlaşılır olması için):  

| *Sütun adı* | *Veri türü* |
| --- | --- |
| **PartitionKey** (bölüm adı) |Dize |
| **RowKey** (çalışan kimliği) |Dize |
| **FirstName** |Dize |
| **Soyadı** |Dize |
| **Geçerlilik süresi** |Tamsayı |
| **EmailAddress** |Dize |

Merhaba önceki bölümde [Azure Table hizmetine genel bakış](#overview) sorgu tasarlama üzerinde doğrudan etkisi olan hello anahtar özelliklerini hello Azure tablo hizmeti bazıları açıklanmaktadır. Bunlar, tablo hizmeti sorguları tasarlama genel yönergeleri izleyerek hello sonuçlanır. Merhaba örneklerde kullanılan hello filtresi sözdizimi daha fazla bilgi için hello tablo hizmetinden REST API olduğuna dikkat edin [sorgu varlıklar](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

* A ***noktası sorgusu*** hello en verimli arama toouse noktasıdır ve yüksek hacimli aramaları veya en düşük gecikme gerektiren aramalar için kullanılan toobe önerilir. Böyle bir sorguyu hello dizinleri toolocate tek bir varlık çok verimli bir şekilde her ikisi de hello belirterek kullanabilirsiniz **PartitionKey** ve **RowKey** değerleri. Örneğin: $filter (PartitionKey eq 'Satış') = ve (RowKey eq '2')  
* İkinci en iyi olan bir ***aralık sorgusu*** hello kullanan **PartitionKey** ve bir dizi filtreleri **RowKey** tooreturn birden fazla varlık değerleri. Hello **PartitionKey** değerini tanımlayan belirli bir bölüm ve hello **RowKey** değerleri bu bölümdeki hello varlıklar kümesini tanımlayın. Örneğin: $filter PartitionKey eq 'Satış ve RowKey ge'nın ' ve RowKey lt 'T ='  
* Üçüncü iyi bir ***bölüm tarama*** hello kullanan **PartitionKey** ve başka bir anahtar dışı özelliği ve, filtreleri, birden fazla varlık döndürebilir. Merhaba **PartitionKey** değer belirli bir bölüm tanımlar ve hello özellik değerlerinin o bölümün hello varlıklarda alt kümeleri için seçin. Örneğin: $filter PartitionKey eq 'Satış' ve LastName eq 'Smith' =  
* A ***tablo tarama*** hello içermez **PartitionKey** ve tüm tablonuzu sırayla eşleşen tüm varlıkların oluşturan hello bölümlerinin arar çok verimli değildir. Olsun veya olmasın, filtre hello kullanır, bağımsız olarak bir tablo taraması gerçekleştirecek **RowKey**. Örneğin: $filter LastName eq 'Can' =  
* Birden çok varlık döndüren sorgular bunları içinde sıralanmış dönmek **PartitionKey** ve **RowKey** sırası. tooavoid yeniden ayırma hello istemci hello varlıklarda seçin bir **RowKey** hello en yaygın sıralama tanımlar.  

Bu kullanarak not bir "**veya**" bir filtre temel alarak toospecify **RowKey** değerleri bir bölüm tarama sonuçları ve aralığı sorgu olarak işlenmez. Bu nedenle, filtreleri gibi kullanan sorguları kaçınmanız gerekir: $filter PartitionKey eq 'Satış' ve RowKey eq '121' = (veya RowKey eq '322')  

Merhaba depolama istemci kitaplığı tooexecute verimli sorguları kullanan istemci-tarafı kod örnekleri için bkz:  

* [Merhaba depolama istemci kitaplığı kullanılarak noktası sorgusu yürütme](#executing-a-point-query-using-the-storage-client-library)
* [LINQ kullanarak birden çok varlık alma](#retrieving-multiple-entities-using-linq)
* [Sunucu tarafı projeksiyonu](#server-side-projection)  

Türleri birden çok varlık işleyebilir istemci-tarafı kod örnekleri için hello aynı depolanan tablo, bkz:  

* [Heterojen varlık türleri ile çalışma](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a>Uygun bir PartitionKey seçme
Tercih ettiğiniz **PartitionKey** hello gerek tooenables hello EGTs (tooensure tutarlılık) kullanımını hello gereksinim toodistribute karşı varlıklarınızı birden çok bölüm (tooensure ölçeklenebilir bir çözüm) dengelemeniz.  

Bir extreme adresindeki tüm varlıkları tek bir bölüm saklayabilirsiniz, ancak bu hello ölçeklenebilirlik çözümünüzün sınırlayabilir ve hello tablo hizmeti mümkün tooload Dengeleme isteklerini engellemek. Merhaba diğer uç bu yüksek oranda ölçeklenebilir olur ve hello tablo tooload bakiye istekleri sağlar, ancak hangi, varlık Grup hareketleri kullanmasını önler bölüm başına tek bir varlık saklayabilirsiniz.  

İdeal **PartitionKey** toouse verimli sorgularını sağlayan biridir ve çözümünüzü yeterli bölümleri tooensure sahip ölçeklenebilir. Genellikle, varlıklarınızı varlıklarınızı yeterli bölümler dağıtır uygun bir özellik olduğunu bulabilirsiniz.

> [!NOTE]
> Örneğin, kullanıcılar veya çalışanlar ilgili bilgileri depoladığı bir sistemde, iyi PartitionKey UserID olabilir. Merhaba bölüm anahtarı olarak belirli bir kullanıcı kimliği kullanan birden fazla varlık sahip. Bir kullanıcı hakkında verilerini depolayan her varlığın tek bir bölümde gruplandırılır ve bu nedenle bu varlıkları hala yüksek oranda ölçeklenebilir devam ederken varlık Grup hareketleri erişilebilir.
> 
> 

Tercih ettiğiniz hususlar vardır **PartitionKey** Ekle, Güncelleştir ve varlıkları silme toohow ilişkilidir: hello bölümüne bakın [veri değişikliği için tasarım](#design-for-data-modification) aşağıda.  

### <a name="optimizing-queries-for-hello-table-service"></a>Sorguları hello tablo hizmeti için en iyi duruma getirme
Merhaba tablo hizmeti otomatik olarak dizinler hello kullanarak varlıklarınızı **PartitionKey** ve **RowKey** tek bir kümelenmiş dizin değerleri, bu nedenle noktası sorgular olan hello olduğunu en verimli toouse neden hello . Ancak, hiçbir dizinlerinde farklı hello hello kümelenmiş dizini vardır **PartitionKey** ve **RowKey**.

Çoğu tasarımları gereksinimleri tooenable arama birden çok ölçüte dayalı varlıkların karşılaması gerekir. Örneğin, e-postalar, temel çalışan varlıkları bulma çalışan kimliği ya da son adı. Merhaba desenleri hello bölümünde aşağıdaki [tablo Tasarım desenleri](#table-design-patterns) gereksinim bu tür adres ve hello tablo hizmet ikincil dizinler sağlamaz hello olgu çözümüne yolları açıklanmaktadır:  

* [İçi bölüm ikincil dizin düzeni](#intra-partition-secondary-index-pattern) -her varlık kullanan birden çok kopyalarını farklı depolama **RowKey** değerleri (Merhaba içinde aynı bölüme) tooenable hızlı ve verimli aramaları ve diğer sıralama siparişleri kullanarak farklı **RowKey** değerleri.  
* [İkincil dizin arası bölüm düzeni](#inter-partition-secondary-index-pattern) - farklı RowKey değerlerini ayrı bölümlere veya ayrı tablolarda tooenable hızlı kullanarak her bir varlık birden çok kopyasını depolamak ve verimli aramaları ve diğer sıralama siparişleri farklı kullanarak**RowKey** değerleri.  
* [Dizin varlıkları düzeni](#index-entities-pattern) -varlıklar listesi döndüren dizin varlıkları tooenable verimli aramalar korumak.  

### <a name="sorting-data-in-hello-table-service"></a>Merhaba tablo hizmeti veri sıralama
Merhaba tablo hizmeti döndürür göre artan düzende sıralandı varlıklar **PartitionKey** ve sonra **RowKey**. Bu anahtarları dize değerlerini ve sayısal değerleri doğru sıralamak tooensure olan tooa sabit uzunluk dönüştürmek ve sıfırlarla doldurur. Örneğin, hello çalışan kimlik değeri hello kullanmanızı **RowKey** bir tamsayı değeri çalışan kimliği dönüştürmeniz gerekir **123** çok**00000123**.  

Birçok uygulama toouse veri sıralanmış farklı siparişler gereksinimlerin: Örneğin, çalışanlar ada göre ya da tarih katılarak sıralama. Merhaba desenleri hello bölümünde aşağıdaki [tablo Tasarım desenleri](#table-design-patterns) nasıl tooalternate sıralama varlıklar için siparişleri adresi:  

* [İçi bölüm ikincil dizin düzeni](#intra-partition-secondary-index-pattern) -farklı RowKey değerleri kullanarak her bir varlık birden çok kopyasını saklamak (Merhaba içinde aynı bölüme) tooenable hızlı ve verimli aramaları ve diğer sıralama siparişleri farklı RowKey değerleri kullanarak.  
* [İkincil dizin arası bölüm düzeni](#inter-partition-secondary-index-pattern) - farklı RowKey değerlerini ayrı ayrı tablolarda tooenable bölümlerinde hızlı kullanarak her bir varlık birden çok kopyasını depolamak ve verimli aramaları ve diğer sıralama siparişleri farklı RowKey kullanarak değerler.
* [Günlük tail düzeni](#log-tail-pattern) -alma hello  *n*  eklenen en son tooa bölüm varlıklar kullanarak bir **RowKey** ters tarihi ve saati sipariş sıralar değeri.  

## <a name="design-for-data-modification"></a>Veri değişikliği için Tasarım
Bu bölümde ekler, güncelleştirmeleri, en iyi duruma getirme için hello tasarım konuları odaklanır ve siler. Bazı durumlarda (Merhaba teknikleri yönetmek için tasarım hello rağmen tasarımlarına ilişkisel veritabanları için yaptığınız gibi veri değişikliği için en iyi duruma getirme tasarımlarını karşı sorgulamak için en iyi duruma getirme tasarımları arasındaki tooevaluate hello dengelemeyi gerekir dengelemeler ilişkisel bir veritabanında farklı). Merhaba bölüm [tablo Tasarım desenleri](#table-design-patterns) hello tablo hizmeti için bazı ayrıntılı tasarım desenleri açıklar ve bazı bu dengelemeler vurgular. Uygulamada, varlıkları iyi değiştirmek için varlıkları sorgulamak için en iyi duruma getirilmiş çoğu tasarımları da iş bulacaksınız.  

### <a name="optimizing-hello-performance-of-insert-update-and-delete-operations"></a>Hello performansı en iyi duruma getirme, ekleme, güncelleştirme ve silme işlemleri
tooupdate veya bir varlığı silmek, mümkün tooidentify olmalıdır hello kullanarak **PartitionKey** ve **RowKey** değerleri. Bu açısından, tercih ettiğiniz **PartitionKey** ve **RowKey** varlıklar değiştirme izlemeniz gereken için benzer ölçütleri tooyour seçim toosupport tooidentify varlıklar olarak istediğinden, sorguları noktası mümkün olduğunca verimli şekilde. Toouse bir verimsiz bölüm veya tablo taraması toolocate sipariş toodiscover hello varlık istemediğiniz **PartitionKey** ve **RowKey** değerleri tooupdate gerekir veya silin.  

Merhaba desenleri hello bölümünde aşağıdaki [tablo Tasarım desenleri](#table-design-patterns) yönelik en iyi duruma getirme hello performans veya ekleme, güncelleştirme ve silme işlemleri:  

* [Yüksek hacimli silme düzeni](#high-volume-delete-pattern) -tüm hello varlıklar eşzamanlı silme işlemi için kendi ayrı tabloda depolayarak varlıklar yüksek hacimli etkinleştir hello silinmesini; hello tablo silerek hello varlıkları silin.  
* [Veri serisi deseni](#data-series-pattern) -deposu tam veri serisi yaptığınız isteklerini tek bir varlık toominimize hello sayısı.  
* [Geniş varlıklar düzeni](#wide-entities-pattern) -birden çok fiziksel varlıkların toostore mantıksal varlık ile birden çok 252 özellik kullanın.  
* [Büyük varlıklar düzeni](#large-entities-pattern) -kullanım blob depolama toostore büyük özellik değerleri.  

### <a name="ensuring-consistency-in-your-stored-entities"></a>Saklı varlıklarınızı tutarlılık sağlama
veri değişiklikleri en iyi duruma getirme için tercih ettiğiniz anahtarların etkilediğini diğer anahtar faktörü hello nasıl atomik işlemleri kullanarak tooensure tutarlılık. Yalnızca bir EGT toooperate hello depolanan varlıklar üzerinde kullanabileceğiniz aynı bölüm.  

Merhaba desenleri hello bölümünde aşağıdaki [tablo Tasarım desenleri](#table-design-patterns) tutarlılık yönetme adresi:  

* [İçi bölüm ikincil dizin düzeni](#intra-partition-secondary-index-pattern) -her varlık kullanan birden çok kopyalarını farklı depolama **RowKey** değerleri (Merhaba içinde aynı bölüme) tooenable hızlı ve verimli aramaları ve diğer sıralama siparişleri kullanarak farklı **RowKey** değerleri.  
* [İkincil dizin arası bölüm düzeni](#inter-partition-secondary-index-pattern) - farklı RowKey değerlerini ayrı bölümlere veya ayrı tablolarda tooenable hızlı kullanarak her bir varlık birden çok kopyasını depolamak ve verimli aramaları ve diğer sıralama siparişleri farklı kullanarak**RowKey** değerleri.  
* [Sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern) -etkinleştirmek sonuçta tutarlı davranış bölüm sınırları veya depolama sistemi sınırları boyunca Azure sıraları kullanarak.
* [Dizin varlıkları düzeni](#index-entities-pattern) -varlıklar listesi döndüren dizin varlıkları tooenable verimli aramalar korumak.  
* [Denormalization deseni](#denormalization-pattern) -birleştirme ilgili verileri birlikte tek bir varlık tooenable tüm hello tek nokta sorguyla verileri tooretrieve.  
* [Veri serisi deseni](#data-series-pattern) -deposu tam veri serisi yaptığınız isteklerini tek bir varlık toominimize hello sayısı.  

Varlık Grup işlemler hakkında daha fazla bilgi için hello bölümüne bakın [varlık Grup hareketleri](#entity-group-transactions).  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a>Tasarımınız etkili değişiklikler için sağlama verimli sorguları kolaylaştırır
Bu belirli senaryonuza hello durumdur kullanıp kullanmadığını çoğu durumda, her zaman etkili değişiklikler, ancak sorgulama verimli sonuçlar için bir tasarım belirlemelidir. Merhaba desenleri hello bölümünde bazıları [tablo Tasarım desenleri](#table-design-patterns) açıkça sorgulama ve varlıkları değiştirme arasındaki dengelemeler değerlendirin ve hesap hello sayıya işlemi her tür her zaman uygulamanız.  

Merhaba desenleri hello bölümünde aşağıdaki [tablo Tasarım desenleri](#table-design-patterns) adres için verimli sorguları tasarlama ve verimli veri değişikliği için tasarlama arasındaki dengelemeler:  

* [Bileşik anahtar düzeni](#compound-key-pattern) -kullanım bileşik **RowKey** değerleri tooenable istemci toolookup tek nokta sorgu verilerle ilgili.  
* [Günlük tail düzeni](#log-tail-pattern) -alma hello  *n*  eklenen en son tooa bölüm varlıklar kullanarak bir **RowKey** ters tarihi ve saati sipariş sıralar değeri.  

## <a name="encrypting-table-data"></a>Tablo verileri şifreleme
dize varlığı Özellikleri Ekle için .NET Azure Storage istemci kitaplığı destekler şifrelenmesi hello ve değiştirme işlemlerini. şifrelenmiş hello dizeleri hello hizmette ikili özellikleri olarak depolanır ve şifre çözme sonra geri toostrings dönüştürülür.    

Tablolar için ayrıca toohello şifreleme ilkesi, kullanıcıların şifrelenmiş hello özellikleri toobe belirtmeniz gerekir. Bu, ya da bir [EncryptProperty] özniteliği (için TableEntity türetilen POCO varlıklar) veya bir şifreleme çözümleyici isteği seçenekleri belirterek yapılabilir. Bir şifreleme çözümleyici bölüm anahtarı, satır anahtarını ve özellik adını alır ve bu özellik şifrelenmesi gerekip gerekmediğini belirten bir Boole değeri döndüren bir temsilci ' dir. Bir özellik toohello kablo yazılırken şifrelenmesi gerekip gerekmediğini şifreleme sırasında bu bilgileri toodecide hello istemci kitaplığını kullanın. Merhaba temsilci özellikler nasıl şifrelenir geçici mantığı hello olasılığı için de sağlar. (Örneğin, X ise ardından özelliği A şifrelemek; Aksi takdirde özellikleri A ve b şifreleme) Bu BT Not gerekli tooprovide okurken veya varlıklar sorgulama bu bilgilerdir.

Bu birleştirme şu anda desteklenmeyen unutmayın. Bir alt özellikler kümesini daha önce farklı bir anahtar kullanılarak şifrelenmiş olabilecek olduğundan, sadece hello yeni özellikleri birleştirme ve hello meta verilerini güncelleştirme veri kaybına neden olur. Ya da birleştirme ek hizmet yapma tooread hello önceden var olan varlık hello hizmetinden çağıran veya yeni bir anahtar özellik başına kullanarak, her ikisi de performansı artırmak için uygun olmayan gerektirir.     

Tablo verisi şifreleme hakkında daha fazla bilgi için bkz: [istemci tarafı şifreleme ve Microsoft Azure depolama için Azure anahtar kasası](../storage/common/storage-client-side-encryption.md).  

## <a name="modelling-relationships"></a>İlişkileri modelleme
Etki alanı model oluşturmaya, karmaşık sistemlerinin hello tasarımındaki önemli bir adımdır. Genellikle, işlem tooidentify varlıklar modelleme hello kullanın ve bir şekilde toounderstand olarak aralarında hello ilişkiler iş etki alanı hello ve sisteminizin hello tasarımını bildirin. Bu bölüm, nasıl, etki alanı modelleri toodesigns hello tablo hizmeti için bulunan hello ortak ilişki türlerinden bazıları çevirebilir üzerinde odaklanmıştır. bir mantıksal veri modeli tooa fiziksel dayalı NoSQL veri modeli eşleme Hello işlemi ilişkisel veritabanı tasarlarken kullanılan çok farklı olur. İlişkisel veritabanları tasarımı, genellikle artıklık – ve özetleri nasıl hello veritabanı nasıl çalıştığını uygulama hello bildirim temelli bir sorgulama yeteneği en aza indirmek için en iyi duruma getirilmiş veri normalleştirme işlemi varsayar.  

### <a name="one-to-many-relationships"></a>Bir-çok ilişkileri
İş etki alanı nesneler arasındaki bir-çok ilişkileri ortaya çok sık: Örneğin, bir bölümü çok sayıda çalışan vardır. Merhaba tablo hizmetiyle her Artıları ve eksileri ilgili toohello belirli senaryoları olabilir birkaç yolu tooimplement-çok ilişkileri vardır.  

On binlerce Departmanlar ve her departman çok sayıda çalışan ve her çalışan belirli bir bölüm ile ilişkili olarak sahip olduğu çalışan varlıkları içeren büyük bir çok Ulusal kuruluşa ait Hello örneği göz önünde bulundurun. Bir yaklaşım toostore ayrı departmanı ve bunlar gibi çalışan varlıkları ise:  

![][1]

Bu örnek üzerinde hello dayalı hello türleri arasında örtük bir bir-çok ilişkisi gösterir **PartitionKey** değeri. Her bölüm çok sayıda çalışan olabilir.  

İlgili çalışan varlıklarını aynı bölüme hello ve bu örnek ayrıca bir departman varlık gösterir. Toouse farklı bölümleri, tablolar veya hatta depolama hesapları hello farklı varlık türleri için tercih edebilirsiniz.  

Alternatif bir yaklaşım hello örnek aşağıdaki gösterildiği gibi verileri ve mağaza yalnızca çalışan varlıklarınızı Normalleştirilmemiş Departman verileri ile toodenormalize olur. İçin bir bölüm Yöneticisi'ni bir gereksinim toobe mümkün toochange hello ayrıntılarını varsa bu belirli bir senaryoda, bu Normalleştirilmemiş bir yaklaşım hello en iyi olmayabilir toodo bu hello departmanındaki her çalışan tooupdate gerekir.  

![][2]

Merhaba daha fazla bilgi için bkz: [Denormalization düzeni](#denormalization-pattern) bu kılavuzda daha sonra.  

Merhaba aşağıdaki tabloda hello Artıları ve eksileri her çalışan ve bir-çok ilişkisi departmanı varlıkları depolamak için yukarıda özetlenen hello yaklaşımlardan biri özetlenmektedir. Çeşitli işlemleri tooperform ne sıklıkta yapılacağı düşünmelisiniz: kabul edilebilir toohave pahalı bir işlem bu işlemi yalnızca seyrek durumda içeren bir tasarıma olabilir.  

<table>
<tr>
<th>Yaklaşım</th>
<th>Uzmanları</th>
<th>Simgeler</th>
</tr>
<tr>
<td>Ayrı bir varlık türleri, aynı bölüm, aynı tablosu</td>
<td>
<ul>
<li>Tek bir işlemle bir departman varlık güncelleştirebilirsiniz.</li>
<li>Bir bölüm varlık gereksinim toomodify varsa EGT toomaintain tutarlılık kullanabilirsiniz olduğunda, güncelleştirme/ekleme/silme çalışan varlık. Örneğin, bir departman çalışan sayısı her bölüm için sahipseniz.</li>
</ul>
</td>
<td>
<ul>
<li>Bazı istemci etkinlikler için bir çalışan ve departman varlık tooretrieve gerekebilir.</li>
<li>Depolama işlemleri durum hello aynı bölüm. Yüksek işlem birimlerinin, bu bir etkin nokta neden olabilir.</li>
<li>Bir EGT kullanarak bir çalışan tooa yeni bir bölüm taşınamıyor.</li>
</ul>
</td>
</tr>
<tr>
<td>Ayrı bir varlık türleri, farklı bölümleri veya tablolar veya depolama hesapları</td>
<td>
<ul>
<li>Tek bir işlemle bir departman varlık veya çalışan varlık güncelleştirebilirsiniz.</li>
<li>Yüksek işlem birimlerinin, bu yardımcı olabilecek daha fazla bölüm üzerinden yayılan hello yük.</li>
</ul>
</td>
<td>
<ul>
<li>Bazı istemci etkinlikler için bir çalışan ve departman varlık tooretrieve gerekebilir.</li>
<li>EGTs toomaintain tutarlılık kullanamazsınız olduğunda, güncelleştirme/ekleme/silme bir çalışan ve güncelleştirme bir bölüm. Örneğin, bir çalışan sayısı departmanı varlıktaki güncelleştiriliyor.</li>
<li>Bir EGT kullanarak bir çalışan tooa yeni bir bölüm taşınamıyor.</li>
</ul>
</td>
</tr>
<tr>
<td>Tek varlık türüne denormalize</td>
<td>
<ul>
<li>Tek bir istekle gerek duyduğunuz tüm hello bilgi alabilirsiniz.</li>
</ul>
</td>
<td>
<ul>
<li>(Bu, tooupdate bir departmandaki tüm hello çalışanlar gerekir) tooupdate bölüm bilgileri gerekiyorsa pahalı toomaintain tutarlılık olabilir.</li>
</ul>
</td>
</tr>
</table>

Nasıl Bu seçenekler ve hello uzmanları hangisinin arasında seçim ve dezavantajlarını en önemli belirli uygulama senaryolarınızı bağlıdır. Örneğin, ne sıklıkta, departman varlıklar değiştirmeyin; Tüm çalışan sorguları hello ek departman bilgi gerekir; ne kadar yakın toohello ölçeklenebilirlik sınırları, bölüm veya depolama hesabınız misiniz?  

### <a name="one-to-one-relationships"></a>Bire bir ilişkiler
Etki alanı modelleri varlıklar arasındaki birebir ilişkileri içerebilir. Tooimplement hello tablo hizmeti bire bir ilişkide gerekiyorsa, nasıl toolink hello iki ilgili varlık tooretrieve her ikisinin de gerektiğinde da seçmeniz gerekir. Bu bağlantıyı hello biçiminde bir bağlantı depolayarak örtük, bir kural hello anahtar değerleri göre veya açık olabilir **PartitionKey** ve **RowKey** her varlık tooits değerleri ilgili varlık. Varlıkları hello depolamanız gerekir, bir tartışma için ilgili olarak Merhaba aynı bölüm, hello bölümüne bakın [-çok ilişkileri](#one-to-many-relationships).  

Olduğunu da hello tablo hizmetinde tooimplement bire bir ilişkiler açabilecek uygulama konuları göz önünde bulundurun:  

* Büyük varlıklar işleme (daha fazla bilgi için bkz: [büyük varlıklar düzeni](#large-entities-pattern)).  
* Erişim denetimleri uygulama (daha fazla bilgi için bkz: [paylaşılan erişim imzaları ile erişimi denetleme](#controlling-access-with-shared-access-signatures)).  

### <a name="join-in-hello-client"></a>Merhaba istemcisinde katılma
Merhaba tablo hizmeti yolları toomodel ilişkileri olsa, hello tablo hizmeti kullanmak için hello iki prime nedenler ölçeklenebilirlik ve performans olduğunu unuttunuz değil. Merhaba performans ve ölçeklenebilirlik çözümünüzün tehlikeye birçok ilişki modelleme bulursanız, gerekli toobuild ise, tüm veri ilişkileri Tablo Tasarımı içine hello kendiniz istemeniz gerekir. Mümkün toosimplify hello tasarımı ve istemci uygulamanızı gerekli tüm birleştirmeler gerçekleştirme izin verirseniz hello ölçeklenebilirlik ve çözümünüzün performansını artırmak.  

Örneğin, çok sık değişmeyen veriler içeren küçük tablolar sahip yaparsanız, ardından bu verileri bir kez ve hello istemcide önbelleğe. Bu yinelenen gidiş-dönüş önleyebilirsiniz tooretrieve hello aynı veri. Bu kılavuzda inceledik hello örneklerde hello küçük bir kuruluşta Departmanlar büyük olasılıkla toobe küçük ve seyrek veri ara olarak istemci uygulamasını bir kez indirebilirsiniz verileri ve önbellek için iyi bir aday yapmadan değişiklik kümesidir.  

### <a name="inheritance-relationships"></a>Devralma ilişkisi
İstemci uygulamanız bir devralma ilişkisi toorepresent iş varlıkları parçasını sınıflar kümesini kullanıyorsa, bu varlıkları hello tablo hizmeti kolayca devam edebilir. Örneğin, istemci uygulamanızda tanımlanmış sınıfları kümesi aşağıdaki hello olabilir nerede **kişi** bir Özet sınıf.

![][3]

Merhaba iki somut sınıflarda hello görünüm bu gibi varlıkları kullanarak tek bir kişi tablosunu kullanarak tablo hizmeti örneklerini devam edebilir:  

![][4]

Aynı tablo istemci kodda hello birden çok varlık türleri ile çalışma hakkında daha fazla bilgi için hello bölümüne bakın [heterojen varlık türleriyle çalışma](#working-with-heterogeneous-entity-types) bu kılavuzda daha sonra. Bu, nasıl toorecognize hello varlık türü istemci kod örnekleri sağlar.  

## <a name="table-design-patterns"></a>Tablo Tasarım desenleri
Önceki bölümlerde nasıl toooptimize tablonuz tasarım sorgularını kullanarak her iki varlık verileri için ve ekleme, güncelleştirme ve varlık verilerini silme hakkında ayrıntılı bazı tartışmalara gördünüz. Bu bölümde tablo hizmeti çözümleri ile kullanım için uygun bazı desenleri açıklar. Ayrıca, nasıl, pratikte hello sorunlar ve bu kılavuzda daha önce oluşturulan dengelemeler bazıları karşılayabilirsiniz görürsünüz. Merhaba Aşağıdaki diyagramda hello farklı desenleri arasındaki hello ilişkileri özetlenmektedir:  

![][5]

Yukarıda Hello desenini eşleme desenleri (mavi) ve bu kılavuzda belgelenen koruma desenleri (turuncu) arasında bazı ilişkiler vurgular. Elbette dikkate değer olan diğer birçok desenleri de vardır. Örneğin, tablo hizmeti yönelik temel senaryolar hello toouse hello biri [gerçekleştirilip görünüm düzeni](https://msdn.microsoft.com/library/azure/dn589782.aspx) hello gelen [komutu sorgu sorumluluk ayrımı (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) düzeni.  

### <a name="intra-partition-secondary-index-pattern"></a>Bölüm içi ikincil dizin düzeni
Her varlık kullanan birden çok kopyalarını farklı depolama **RowKey** değerleri (Merhaba içinde aynı bölüme) tooenable hızlı ve verimli aramaları ve diğer sıralama siparişleri farklı kullanarak **RowKey** değerleri. Güncelleştirmeleri kopyaları arasında saklanması tutarlı EGT'ın kullanma.  

#### <a name="context-and-problem"></a>İçerik ve sorunu
Merhaba tablo hizmeti otomatik olarak dizinler hello kullanarak varlıkları **PartitionKey** ve **RowKey** değerleri. Bu bir istemci uygulama tooretrieve verimli bir şekilde bu değerleri kullanarak bir varlık sağlar. Örneğin, aşağıda gösterilen hello tablo yapısı kullanarak bir istemci uygulaması noktası sorgu tooretrieve tek çalışan varlık hello bölüm adı ve hello çalışan kimliği kullanarak kullanabilirsiniz (Merhaba **PartitionKey** ve  **RowKey** değerleri). Bir istemci, her bölüm içinde çalışan kimliğine göre sıralanmış varlıklar de alabilirsiniz.

![][6]

Ayrıca toobe mümkün toofind e-posta adresi gibi başka bir özellik hello değere göre bir çalışan varlık istiyorsanız, daha az verimli bir bölüm tarama toofind bir eşleşme kullanmanız gerekir. Bu durum, ikincil dizinler Hello tablo hizmet sağlamaz çünkü. Ayrıca, yoktur hiçbir seçeneği toorequest çalışanların farklı bir düzende sıralanmış bir listesini **RowKey** sırası.  

#### <a name="solution"></a>Çözüm
toowork ikincil dizinler hello eksikliği geçici her varlık farklı bir kullanarak her bir kopya ile birden çok kopyasını saklayabilir **RowKey** değeri. Aşağıda gösterilen hello yapıları içeren bir varlık depolarsanız, e-posta adresi veya çalışan kimliği temel alarak çalışan varlıkları verimli bir şekilde alabilir. Merhaba hello için önek değerleri **RowKey**, "empid_" ve "email_" etkinleştirmek, tooquery tek bir çalışan veya bir dizi çalışanlar için bir aralığı e-posta adresleri ya da çalışan kimlikleri kullanarak.  

![][7]

(bir çalışan kimliği ve bir e-posta adresiyle bakan bakan) iki filtre ölçütünü aşağıdaki hello her ikisi de noktası sorguları belirtin:  

* $filter (PartitionKey eq 'Satış') = ve (RowKey eq 'empid_000223')  
* $filter (PartitionKey eq 'Satış') = ve (RowKey eq 'email_jonesj@contoso.com')  

Çalışan varlıklar için bir aralığı sorgu, çalışan kimliği düzende sıralanmış bir aralık veya hello hello uygun öneke sahip varlıklar için sorgulayarak e-posta adresi düzende sıralanmış bir aralığı belirtebilirsiniz **RowKey**.  

* Tüm hello çalışanlarla hello satış departmanında hello aralığı 000100 too000199 çalışan kimliğinde toofind kullanın: $filter (PartitionKey eq 'Satış') = ve (RowKey ge 'empid_000100') ve (RowKey le 'empid_000199')  
* Tüm hello hello satış departmanı çalışanları hello ile başlayarak, bir e-posta adresi ile toofind harf 'bir' kullanımı: $filter (PartitionKey eq 'Satış') = ve (RowKey ge 'email_a') ve (RowKey lt 'email_b')  
  
  Merhaba Yukarıdaki örneklerde kullanılan hello filtresi sözdizimi daha fazla bilgi için hello tablo hizmetinden REST API olduğuna dikkat edin [sorgu varlıklar](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Sorunları ve dikkat edilmesi gerekenler
Merhaba karar verirken aşağıdaki noktaları göz önünde bulundurun nasıl tooimplement bu deseni:  

* Tablo depolama görece ucuz toouse olduğundan, yinelenen verileri depolama yükünü maliyet hello başlıca sorunlardan olmamalıdır. Ancak, her zaman beklenen depolama gereksinimlerinize göre tasarımınızı hello maliyetini değerlendirmek ve yalnızca istemci uygulamanızı yürütecek yinelenen varlıklar toosupport hello sorguları ekleme.  
* Merhaba ikincil dizin varlıkları aynı hello özgün varlıklar bölüm hello depolandığından, tek bir bölüm için hello ölçeklenebilirlik hedefleri aşmamasını sağlayın.  
* EGTs tooupdate hello iki kopyasını hello varlık otomatik olarak kullanarak, yinelenen varlıklarınızı birbiriyle tutarlı tutabilirsiniz. Bu varlıkta tüm kopyalarını hello saklamalısınız anlamına gelir. aynı bölüm. Daha fazla bilgi için hello bölümüne bakın [kullanarak varlık Grup hareketleri](#entity-group-transactions).  
* Merhaba hello için kullanılan değer **RowKey** her bir varlık için benzersiz olmalıdır. Bileşik anahtar değerlerinden kullanmayı düşünün.  
* Merhaba sayısal değerleri doldurma **RowKey** (örneğin, hello çalışan kimliği 000223), sıralama ve filtreleme göre üst ve alt sınırlarını etkinleştirir düzeltin.  
* Mutlaka varlığınız tüm hello özelliklerini tooduplicate gerekmez. Örneğin, hello arama hello varlıkları hello kullanarak e-posta sorgularını hello adres **RowKey** hiçbir zaman, hello çalışanın yaşı gerekir, bu varlıkları yapı izlenerek hello olabilir:

![][8]

* Bu genellikle daha iyi toostore yinelenen verileri ve tek bir sorgu ile gereksinim duyduğunuz tüm hello veri alabilir, gerekli bir varlık ve başka bir toolookup hello veri toouse bir sorgu toolocate emin olun.  

#### <a name="when-toouse-this-pattern"></a>Zaman toouse bu deseni
İstemci uygulamanızın istemci farklı sıralamalar tooretrieve varlıklarda gerektiğinde farklı anahtarlar, çeşitli kullanarak tooretrieve varlıkları gerektiğinde ve benzersiz değerler çeşitli kullanarak her bir varlık tanımlayabilirsiniz bu deseni kullanır. Bununla birlikte, varlık aramalarını hello farklı kullanarak gerçekleştirirken hello bölüm ölçeklenebilirlik sınırları aşmadığından emin olmalıdır **RowKey** değerleri.  

#### <a name="related-patterns-and-guidance"></a>İlgili desenleri ve Kılavuzu
Merhaba aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:  

* [İkincil dizin arası bölüm düzeni](#inter-partition-secondary-index-pattern)
* [Bileşik anahtar düzeni](#compound-key-pattern)
* [Varlık Grup işlemleri](#entity-group-transactions)
* [Heterojen varlık türleri ile çalışma](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a>İkincil dizin arası bölüm düzeni
Her varlık kullanan birden çok kopyalarını farklı depolama **RowKey** ayrı bölümlere veya ayrı tablolarda tooenable hızlı ve verimli aramaları ve farklı kullanarak diğer sıralamalar değerleri **RowKey**değerleri.  

#### <a name="context-and-problem"></a>İçerik ve sorunu
Merhaba tablo hizmeti otomatik olarak dizinler hello kullanarak varlıkları **PartitionKey** ve **RowKey** değerleri. Bu bir istemci uygulama tooretrieve verimli bir şekilde bu değerleri kullanarak bir varlık sağlar. Örneğin, aşağıda gösterilen hello tablo yapısı kullanarak bir istemci uygulaması noktası sorgu tooretrieve tek çalışan varlık hello bölüm adı ve hello çalışan kimliği kullanarak kullanabilirsiniz (Merhaba **PartitionKey** ve  **RowKey** değerleri). Bir istemci, her bölüm içinde çalışan kimliğine göre sıralanmış varlıklar de alabilirsiniz.  

![][9]

Ayrıca toobe mümkün toofind e-posta adresi gibi başka bir özellik hello değere göre bir çalışan varlık istiyorsanız, daha az verimli bir bölüm tarama toofind bir eşleşme kullanmanız gerekir. Bu durum, ikincil dizinler Hello tablo hizmet sağlamaz çünkü. Ayrıca, yoktur hiçbir seçeneği toorequest çalışanların farklı bir düzende sıralanmış bir listesini **RowKey** sırası.  

Bu varlıklar karşı işlemleri çok yüksek hacimli bekleme ve toominimize hello hello tablo hizmeti istemci azaltma riskini istiyor.  

#### <a name="solution"></a>Çözüm
toowork ikincil dizinler hello eksikliği geçici birden çok kopyası her kopyalama kullanarak her bir varlık farklı saklayabilir **PartitionKey** ve **RowKey** değerleri. Aşağıda gösterilen hello yapıları içeren bir varlık depolarsanız, e-posta adresi veya çalışan kimliği temel alarak çalışan varlıkları verimli bir şekilde alabilir. Merhaba hello için önek değerleri **PartitionKey**, "empid_" ve "email_" etkinleştirmek, bir sorgu için dizin tooidentify istediğiniz toouse.  

![][10]

(bir çalışan kimliği ve bir e-posta adresiyle bakan bakan) iki filtre ölçütünü aşağıdaki hello her ikisi de noktası sorguları belirtin:  

* $filter (PartitionKey eq ' empid_Sales') = ve (RowKey eq '000223')
* $filter (PartitionKey eq ' email_Sales') = ve (RowKey eq 'jonesj@contoso.com')  

Çalışan varlıklar için bir aralığı sorgu, çalışan kimliği düzende sıralanmış bir aralık veya hello hello uygun öneke sahip varlıklar için sorgulayarak e-posta adresi düzende sıralanmış bir aralığı belirtebilirsiniz **RowKey**.  

* tüm çalışanlara hello toofind hello satış departmanı hello aralıktaki çalışan kimliğine **000100** çok**000199** çalışan kimliği sipariş kullanımda sıralanır: $filter (PartitionKey eq ' empid_Sales') = ve (RowKey ge ' 000100') ve (RowKey le '000199')  
* toofind hello satış departmanı içinde sıralanmış 'a' ile başlayan e-posta adresi olan tüm hello çalışanların adresi sipariş kullanım e-posta: $filter (PartitionKey eq ' email_Sales') = ve (RowKey ge 'bir') ve (RowKey lt 'b')  

Merhaba Yukarıdaki örneklerde kullanılan hello filtresi sözdizimi daha fazla bilgi için hello tablo hizmetinden REST API olduğuna dikkat edin [sorgu varlıklar](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Sorunları ve dikkat edilmesi gerekenler
Merhaba karar verirken aşağıdaki noktaları göz önünde bulundurun nasıl tooimplement bu deseni:  

* Hello kullanarak, yinelenen varlıklarınızı birbiriyle sonunda tutarlı tutabilirsiniz [sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern) toomaintain hello birincil ve ikincil dizin varlıklar.  
* Tablo depolama görece ucuz toouse olduğundan, yinelenen verileri depolama yükünü maliyet hello başlıca sorunlardan olmamalıdır. Ancak, her zaman beklenen depolama gereksinimlerinize göre tasarımınızı hello maliyetini değerlendirmek ve yalnızca istemci uygulamanızı yürütecek yinelenen varlıklar toosupport hello sorguları ekleme.  
* Merhaba hello için kullanılan değer **RowKey** her bir varlık için benzersiz olmalıdır. Bileşik anahtar değerlerinden kullanmayı düşünün.  
* Merhaba sayısal değerleri doldurma **RowKey** (örneğin, hello çalışan kimliği 000223), sıralama ve filtreleme göre üst ve alt sınırlarını etkinleştirir düzeltin.  
* Mutlaka varlığınız tüm hello özelliklerini tooduplicate gerekmez. Örneğin, hello arama hello varlıkları hello kullanarak e-posta sorgularını hello adres **RowKey** hiçbir zaman, hello çalışanın yaşı gerekir, bu varlıkları yapı izlenerek hello olabilir:
  
  ![][11]
* Genellikle toostore yinelenen verileri daha iyi ve toouse bir sorgu toolocate kullanarak bir varlık hello daha ikincil dizin ile tek bir sorgu gereksinim duyduğunuz tüm hello veri alabilirsiniz emin olan ve başka bir toolookup hello hello birincil dizin gerekli verileri.  

#### <a name="when-toouse-this-pattern"></a>Zaman toouse bu deseni
İstemci uygulamanızın istemci farklı sıralamalar tooretrieve varlıklarda gerektiğinde farklı anahtarlar, çeşitli kullanarak tooretrieve varlıkları gerektiğinde ve benzersiz değerler çeşitli kullanarak her bir varlık tanımlayabilirsiniz bu deseni kullanır. Varlık aramalarını hello farklı kullanarak gerçekleştirirken hello bölüm ölçeklenebilirlik sınırları aşan tooavoid istediğinizde bu deseni kullanın **RowKey** değerleri.  

#### <a name="related-patterns-and-guidance"></a>İlgili desenleri ve Kılavuzu
Merhaba aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:  

* [Sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern)  
* [Bölüm içi ikincil dizin düzeni](#intra-partition-secondary-index-pattern)  
* [Bileşik anahtar düzeni](#compound-key-pattern)  
* [Varlık Grup işlemleri](#entity-group-transactions)  
* [Heterojen varlık türleri ile çalışma](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a>Sonuçta tutarlı işlemleri düzeni
Sonuçta tutarlı davranışı, Azure sıraları kullanarak bölüm sınırları veya depolama sistemi sınırları boyunca etkinleştirin.  

#### <a name="context-and-problem"></a>İçerik ve sorunu
EGTs etkinleştirmek atomik işlemleri hello paylaşan birden çok varlık arasında aynı bölüm anahtarı. Performans ve ölçeklenebilirlik için ayrı bölümlere veya ayrı bir depolama sistemi tutarlılık gereksinimlerin toostore varlıklar karar verebilirsiniz: Böyle bir senaryoda EGTs toomaintain tutarlılık kullanamazsınız. Örneğin, bir gereksinim toomaintain nihai tutarlılık arasında olabilir:  

* Varlıklar iki farklı bölüm aynı, farklı tablolarda farklı depolama hesaplarında tablosundaki hello olarak depolanır.  
* Bir varlık hello tablo hizmeti depolanan ve blob hello Blob hizmetinde depolanır.  
* Merhaba tablo hizmeti ve bir dosya bir dosya sisteminde depolanan bir varlık.  
* Bir varlık hello tablo hizmeti depolamak henüz hello Azure Search hizmeti kullanarak dizini.  

#### <a name="solution"></a>Çözüm
Azure sıralar kullanarak, iki veya daha fazla bölüm ya da depolama sistemleri arasında nihai tutarlılık teslim bir çözüm uygulayabilirsiniz.
tooillustrate bu yaklaşımını, gereksinim toobe mümkün tooarchive eski çalışan varlıkları olduğunu varsayın. Eski çalışan varlıkları nadiren seçmeleri istenir ve geçerli çalışanlar ile ilgili tüm etkinlikleri dışında tutulması. tooimplement hello etkin çalışanlara depolamak bu gereksinim **geçerli** tablo ve hello eski çalışanların **arşiv** tablo. Bir çalışan arşivleme gerektirir toodelete hello hello varlıktan **geçerli** tablo ve hello varlık toohello ekleyin **arşiv** tablosu, ancak kullanamaz EGT tooperform bu iki işlem. bir hata hem veya hiçbiri tablolarda bir varlık tooappear neden tooavoid hello risk hello Arşiv işlemi sonunda tutarlı olması gerekir. Merhaba aşağıdaki sıralı diyagram hello adımlar bu işlemde açıklanır. Daha fazla ayrıntı hello metin aşağıdaki özel durum yollar için sağlanır.  

![][12]

Bir istemci, bu örnek tooarchive çalışan #456 bir Azure sırada bir ileti yerleştirmek tarafından hello Arşiv işlemi başlatır. Çalışan rolü hello sıra yeni iletiler için yoklar; bir bulduğunda, selamlama iletisine okur ve gizli bir kopyasını hello sırasına bırakır. Merhaba çalışan rolü hello sonraki hello varlık bir kopyasını getirir **geçerli** tablo, hello bir kopya ekler **arşiv** tablo ve siler hello hello özgün **geçerli**tablo. Son olarak, hiçbir hata hello önceki adımlardan olsaydı, hello çalışan rolü hello gizli ileti hello sırasından kaldırır.  

Bu örnekte, 4. adım hello çalışan hello ekler **arşiv** tablo. Bir dosya sistemi hello Blob hizmeti hello çalışan tooa blob veya bir dosya ekleyebilirsiniz.  

#### <a name="recovering-from-failures"></a>Hatalardan kurtarma
Önemli adımları işlemlerinde hello **4** ve **5** olmalıdır *ıdempotent* hello çalışan rolü toorestart hello Arşiv işlemi gerekebileceği. Adım için hello tablo hizmeti kullanıyorsanız, **4** "Ekle veya Değiştir" işlemi kullanmanız gerekir; adım için **5** kullanması gereken bir "silin var" işlemi kullanmakta olduğunuz hello istemci Kitaplığı'nda. Başka bir depolama sistemi kullanıyorsanız, uygun ıdempotent işlemi kullanmanız gerekir.  

Merhaba çalışan rolü asla adım tamamlarsa **6**, hello sırada bir zaman aşımı hello ileti yeniden görünür sonra sonra hello çalışan rolü tootry tooreprocess için bunu hazır. Merhaba çalışan rolü hello sıraya ileti okuma kaç kez kontrol edebilirsiniz ve gerekirse, sıra tooa göndererek "zarar" iletisi araştırma için olan bayrağı ayırın. Dequeue sayısı sıra iletileri okumak ve hello denetimi hakkında daha fazla bilgi için bkz: [iletileri almak](https://msdn.microsoft.com/library/azure/dd179474.aspx).  

Bazı hatalar hello tablo ve kuyruk Hizmetleri geçici hataları ve istemci uygulamanızı uygun yeniden deneme mantığı toohandle içermelidir bunları.  

#### <a name="issues-and-considerations"></a>Sorunları ve dikkat edilmesi gerekenler
Merhaba karar verirken aşağıdaki noktaları göz önünde bulundurun nasıl tooimplement bu deseni:  

* Bu çözüm için işlem yalıtım sağlamaz. Örneğin, bir istemci hello okuyabilir **geçerli** ve **arşiv** tabloları arasında adımları hello çalışan rolü olduğu zaman **4** ve **5**ve bir Merhaba verilerinin tutarsız görünümü. Merhaba veri sonunda tutarlı olacağını unutmayın.  
* Adım 4 ve 5 sipariş tooensure nihai tutarlılık ıdempotent emin olması gerekir.  
* Birden çok kuyruklar ve çalışan rolü örnekleri kullanarak hello çözüm ölçeklendirebilirsiniz.  

#### <a name="when-toouse-this-pattern"></a>Zaman toouse bu deseni
Farklı bölümleri veya tablo mevcut varlıklar arasındaki tooguarantee nihai tutarlılık istediğinizde bu deseni kullanır. Merhaba tablo ve hello Blob hizmeti ve veritabanı veya hello dosya sistemi gibi diğer Azure Storage veri kaynakları arasında işlemleri için bu deseni tooensure nihai tutarlılık genişletebilirsiniz.  

#### <a name="related-patterns-and-guidance"></a>İlgili desenleri ve Kılavuzu
Merhaba aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:  

* [Varlık Grup işlemleri](#entity-group-transactions)  
* [Birleştirme ya da değiştirme](#merge-or-replace)  

> [!NOTE]
> İşlem yalıtım önemli tooyour çözüm varsa, tablolar tooenable yeniden düşünmelisiniz, toouse EGTs.  
> 
> 

### <a name="index-entities-pattern"></a>Dizin varlıkları düzeni
Varlıklar listesi döndüren dizin varlıkları tooenable verimli aramalar korur.  

#### <a name="context-and-problem"></a>İçerik ve sorunu
Merhaba tablo hizmeti otomatik olarak dizinler hello kullanarak varlıkları **PartitionKey** ve **RowKey** değerleri. Bu, bir istemci uygulama tooretrieve verimli bir şekilde noktası sorgusu kullanarak bir varlık sağlar. Örneğin, aşağıda gösterilen hello tablo yapısı kullanarak, bir istemci uygulaması verimli bir şekilde bir tek çalışan varlık hello bölüm adı ve hello çalışan kimliği kullanarak alabilirsiniz (Merhaba **PartitionKey** ve **RowKey** ).  

![][13]

Merhaba özelliğinin değeri başka bir benzersiz olmayan, son kullanıcıların adı gibi temel çalışan varlıklar listesi toobe mümkün tooretrieve de istiyorsanız daha az verimli bir bölüm kullanmalısınız bir dizin toolook kullanmak yerine toofind eşleşen tarama bunları doğrudan yukarı. Bu durum, ikincil dizinler Hello tablo hizmet sağlamaz çünkü.  

#### <a name="solution"></a>Çözüm
Yukarıda gösterilen çalışan kimlikleri listesini korumalıdır hello varlık yapısına sahip son ada göre arama tooenable. Tooretrieve hello çalışan CAN gibi belirli bir son adı varlıklarıyla istiyorsanız, ilk kendi son adıyla Etikan olan çalışanlar için hello çalışan kimliklerinin listesini bulun ve bu çalışan varlıkların almak gerekir. Merhaba listelerini çalışan kimliklerini depolamak için üç ana seçeneği vardır:  

* BLOB storage'ı kullanın.  
* Dizin varlıkları aynı hello çalışan varlıklar bölüm hello oluşturun.  
* Dizin varlıkları ayrı bölüm ya da tablo oluşturun.  

<u>#1. seçenek: Blob storage'ı kullanma</u>  

Merhaba ilk seçenek hello listesini her benzersiz son adı için bir blob'un, her blob deposu oluşturmak **PartitionKey** (bölüm) ve **RowKey** bu son olan çalışanlar için (çalışan kimliği) değerleri adı. Eklemek veya bir çalışan sildiğinizde hello ilgili blob Merhaba içeriğine hello çalışan varlıklarıyla sonuçta tutarlı olduğundan emin olmanız gerekir.  

<u>#2. seçenek:</u> oluşturma dizini varlıklarda hello aynı bölüm  

Hello ikinci seçeneği için veri izleyen hello depolamak dizin varlıkları kullanın:  

![][14]

Merhaba **EmployeeIDs** özelliği hello depolanan hello Soyadı ile çalışanlar için çalışan kimlikleri listesini içeren **RowKey**.  

Merhaba aşağıdaki adımları hello ikinci seçeneği kullanıyorsanız, yeni bir çalışan ekleme yapıyorsanız izlemeniz gereken hello süreci ana hatlarıyla anlatılır. Bu örnekte, bir çalışan kimliği 000152 ve hello satış departmanında son adıyla Etikan ekliyoruz:  

1. Merhaba dizin varlıkla almak bir **PartitionKey** "Satış" ve hello değeri **RowKey** "Can" değeri Bu varlık toouse ETag Hello 2. adımda kaydedin.  
2. Merhaba yeni çalışan varlık ekleyen bir varlık Grup hareketi (diğer bir deyişle, toplu işlem) oluşturma (**PartitionKey** "Satış" değeri ve **RowKey** değer "000152"), ve güncelleştirmeleri hello dizin varlık ( **PartitionKey** "Satış" değeri ve **RowKey** "Can" değer) hello yeni çalışan kimliği toohello listesi hello EmployeeIDs alanında ekleyerek düzenleyin. Varlık Grup işlemler hakkında daha fazla bilgi için bkz: [varlık Grup hareketleri](#entity-group-transactions).  
3. Merhaba varlık grubu işlem (birisi yalnızca hello dizin varlık değiştirdi) iyimser eşzamanlılık hata nedeniyle başarısız olursa, daha sonra toostart üzerinden 1. adımda yeniden gerekir.  

Merhaba ikinci seçeneği kullanıyorsanız, benzer bir yaklaşım toodeleting bir çalışan kullanabilirsiniz. Bir çalışanın soyadını değiştirme olduğundan biraz daha karmaşık tooexecute üç varlık güncelleştirmeleri bir varlık Grup hareketi gerekir: Merhaba çalışan varlık, başlangıç dizini varlık hello eski soyadı ve hello dizin varlığı hello yeni soyadı. İyimser eşzamanlılık kullanarak tooperform hello güncelleştirmeleri sonra kullanabileceğiniz tooretrieve hello ETag değerlerin sırayla herhangi bir değişiklik yapmadan önce her bir varlık almanız gerekir.  

Merhaba aşağıdaki adımları hello ikinci seçeneği kullanıyorsanız, verilen Soyadı bir departmandaki tüm hello çalışanlarla yukarı toolook gerektiğinde izlemeniz gereken hello süreci ana hatlarıyla anlatılır. Bu örnekte, tüm hello çalışanlar hello satış departmanında son adıyla Etikan yukarı arıyoruz:  

1. Merhaba dizin varlıkla almak bir **PartitionKey** "Satış" ve hello değeri **RowKey** "Can" değeri  
2. Çalışan kimliklerini hello EmployeeIDs alanında Hello listesi ayrıştırılamıyor.  
3. (Örneğin, e-postaları) bu çalışanların her hakkında ek bilgi gerekirse, her kullanarak hello çalışan varlıkları almak **PartitionKey** "Satış" değeri ve **RowKey** gelen değerleri 2. adımda elde ettiğiniz çalışanların Hello listesi.  

<u>#3. seçenek:</u> ayrı bölüm veya tablo içinde dizin varlıkları oluşturma  

Merhaba üçüncü seçenek için veri izleyen hello depolamak dizin varlıkları kullanın:  

![][15]

Merhaba **EmployeeIDs** özelliği hello depolanan hello Soyadı ile çalışanlar için çalışan kimlikleri listesini içeren **RowKey**.  

Merhaba üçüncü seçeneğiyle Hello dizin varlıkları gelen hello çalışan ayrı bir bölüme olduğundan EGTs toomaintain tutarlılık kullanamazsınız. Merhaba dizin varlıkları hello çalışan varlıklarıyla sonuçta tutarlı olduğundan emin olun.  

#### <a name="issues-and-considerations"></a>Sorunları ve dikkat edilmesi gerekenler
Merhaba karar verirken aşağıdaki noktaları göz önünde bulundurun nasıl tooimplement bu deseni:  

* Bu çözüm varlıklar eşleşen en az iki sorguları tooretrieve gerektirir: bir tooquery hello dizin varlıkları tooobtain hello listesi **RowKey** değerleri ve daha sonra her varlık hello listesinde tooretrieve sorgular.  
* Tek tek bir varlık seçeneği #2 1 MB maksimum boyuta sahip ve seçenek #3 hello çözümde varsayın hello listesini verilen Soyadı çalışanı kimlikleri düşünüldüğünde hiçbir zaman 1 MB'den daha büyük. Çalışan kimliklerinin Hello listesi boyutu 1 MB'den büyük olasılıkla toobe ise, #1 seçeneğini kullanın ve blob depolama alanına hello dizin verileri depolar.  
* Seçenek #2 kullanıyorsanız hello toplu işlemler hello ölçeklenebilirlik sınırları belli bir bölüm yaklaşımını varsa (ekleme ve çalışanlar silme ve bir çalışanın soyadını değiştirme EGTs toohandle kullanarak), değerlendirmeniz gerekir. Merhaba Durum buysa, kuyruklar toohandle hello güncelleştirme kullanan sonuçta tutarlı çözümünü (#1 veya seçeneği #3) istekleri ve dizin varlıklarınızı gelen hello çalışan ayrı bir bölümünde, toostore sağlar düşünmelisiniz.  
* Bu çözüm #2 seçeneğinde varsayar toolook oluşturan bir bölüm içinde son ada göre istediğiniz: Örneğin, tooretrieve son adıyla Etikan hello satış departmanında çalışan listesini istediğiniz. Toobe mümkün toolook son adıyla Etikan hello tüm kuruluş genelinde tüm hello çalışanlar yedeklemek istiyorsanız seçeneği #1 veya seçenek #3 kullanın.
* Nihai tutarlılık sunar sıra tabanlı bir çözüm uygulayabilirsiniz (Merhaba bkz [sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern) daha fazla ayrıntı için).  

#### <a name="when-toouse-this-pattern"></a>Zaman toouse bu deseni
Toolookup tüm hello Soyadı Can olan tüm çalışanlar gibi ortak bir özellik değeri paylaşır varlık kümesi istediğinizde bu deseni kullanır.  

#### <a name="related-patterns-and-guidance"></a>İlgili desenleri ve Kılavuzu
Merhaba aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:  

* [Bileşik anahtar düzeni](#compound-key-pattern)  
* [Sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern)  
* [Varlık Grup işlemleri](#entity-group-transactions)  
* [Heterojen varlık türleri ile çalışma](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a>Denormalization deseni
İlgili verileri tek bir varlık tooenable de birlikte birleştirmek tüm hello tek nokta sorguyla verileri tooretrieve.  

#### <a name="context-and-problem"></a>İçerik ve sorunu
İlişkisel bir veritabanında genellikle birden çok tablodan veri sorgularda kaynaklanan veri tooremove çoğaltma normalleştirin. Verilerinizi Azure tablolardaki normalleştirin gerekirse, ilgili verilerinizi hello istemci toohello sunucu tooretrieve gelen birden çok gidiş dönüş yapmanız gerekir. Örneğin, aşağıda gösterilen hello tablo yapısı ile iki dönüşleri tooretrieve hello Ayrıntılar bir bölüm için yuvarlak: bir çalışan hello Yöneticisi'nin kimlik ve ardından başka bir istek toofetch hello Yöneticisi'nin ayrıntılar içeren bir toofetch hello departmanı varlık varlık.  

![][16]

#### <a name="solution"></a>Çözüm
İki ayrı varlıklarda hello veri depolama, yerine hello veri denormalize ve hello departmanı varlık hello Yöneticisi'nin ayrıntılar kopyasını tutun. Örneğin:  

![][17]

Bu özellikleri depolanan departmanı varlıklarıyla noktası sorgusu kullanarak bir bölüm hakkında gereken tüm hello ayrıntıları alabilirsiniz.  

#### <a name="issues-and-considerations"></a>Sorunları ve dikkat edilmesi gerekenler
Merhaba karar verirken aşağıdaki noktaları göz önünde bulundurun nasıl tooimplement bu deseni:  

* Ek yükü bazı verileri iki kez saklamanın bazı maliyet yoktur. Merhaba performans avantajı (daha az istekleri toohello Depolama hizmetinden kaynaklanan) genellikle ağır hello Marjinal depolama maliyetleri artış (ve bu maliyet kısmen uzaklığı hello sayısındaki azalma tarafından toofetch hello ayrıntıları gerektirir. bir bölümünü).  
* Yöneticileri hakkında bilgi depolamak hello iki varlık hello tutarlılığını bulundurmanız gerekir. Merhaba tutarlılık sorunu EGTs tooupdate kullanarak tek bir atomik işlemle birden çok varlık işleyebilir: hello departmanı varlık ve hello çalışan varlık hello Bölüm Yöneticisi için hello bu durumda, depolanan aynı bölüm.  

#### <a name="when-toouse-this-pattern"></a>Zaman toouse bu deseni
Sık toolook ilgili bilgileri ihtiyacınız olduğunda bu deseni kullanır. Bu desen istemciniz gerektirdiği tooretrieve hello veri olmalısınız sorguları hello sayısını azaltır.  

#### <a name="related-patterns-and-guidance"></a>İlgili desenleri ve Kılavuzu
Merhaba aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:  

* [Bileşik anahtar düzeni](#compound-key-pattern)  
* [Varlık Grup işlemleri](#entity-group-transactions)  
* [Heterojen varlık türleri ile çalışma](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a>Bileşik anahtar düzeni
Kullanım bileşik **RowKey** değerleri tooenable istemci toolookup tek nokta sorgu verilerle ilgili.  

#### <a name="context-and-problem"></a>İçerik ve sorunu
İsteğe bağlı olarak bir ilişkisel veritabanı sorguları oldukça doğal toouse birleşimlerde olması tooreturn ilgili veri toohello istemcisi tek sorgu parçaları. Örneğin, bu çalışan için verileri gözden geçirin ve performans içeren ilgili varlıklar listesini hello çalışan kimliği toolook kullanabilirsiniz.  

Yapı izlenerek hello kullanarak hello tablo hizmetinde çalışan varlıkları depolayan varsayın:  

![][18]

Tooreviews ilgili toostore geçmiş verileri de gerekir ve her yıl hello çalışan için performans, kuruluşunuz için çalışmıştır ve bu bilgileri yıla göre toobe mümkün tooaccess gerekir. Bir seçenek toocreate yapı izlenerek hello ile varlıkları depolayan başka bir tablodur:  

![][19]

Bu, yaklaşımını dikkat edin (örneğin, ad ve Soyadı) hello yeni varlık tooenable bazı bilgileri tooduplicate karar, tooretrieve verilerinizin tek bir istek. Ancak, otomatik olarak bir EGT tooupdate hello iki varlık kullanamadığından güçlü tutarlılık korunamaz.  

#### <a name="solution"></a>Çözüm
Yeni bir varlık türü varlıkları yapı izlenerek hello ile kullanarak özgün tablonuzu saklayın:  

![][20]

Nasıl hello fark **RowKey** şimdi bileşik anahtar hello çalışan kimliği ve sağlar hello gözden geçirme verilerini hello yılın çalışanın performans hello ve verileri tek bir varlık için tek bir istekle gözden tooretrieve oluşur.  

Aşağıdaki örneğine hello (örneğin, hello satış departmanında çalışan 000123) belirli bir çalışana ait tüm hello gözden geçirme verilerini nasıl alabilir özetlenmektedir:  

$filter (PartitionKey eq 'Satış') = ve (RowKey ge 'empid_000123') ve (RowKey lt 'empid_000124') & $select = RowKey, Yöneticisi derecelendirme, eş derecelendirme, Yorumlar  

#### <a name="issues-and-considerations"></a>Sorunları ve dikkat edilmesi gerekenler
Merhaba karar verirken aşağıdaki noktaları göz önünde bulundurun nasıl tooimplement bu deseni:  

* Kolay tooparse hello kolaylaştırır uygun ayırıcı karakter kullanması gereken **RowKey** değeri: Örneğin, **000123_2012**.  
* Aynı bölüm hello ilgili verileri içeren diğer varlıklar olarak Merhaba, bu varlık depoluyorsanız aynı çalışan, EGTs toomaintain güçlü tutarlılık kullanabileceğiniz anlamına gelir.
* Bu desen uygun olup olmadığını ne sıklıkta hello veri toodetermine sorgulayacak göz önünde bulundurmalısınız.  Örneğin, erişim sağlarsa gözden geçirme verilerini seyrek hello ve hello genellikle ana çalışan verilerini ayrı varlıklar olarak tutmanız gerekir.  

#### <a name="when-toouse-this-pattern"></a>Zaman toouse bu deseni
Bu deseni toostore biri gerekir veya ilgili daha fazla varlıklar, sorgu sık kullanır.  

#### <a name="related-patterns-and-guidance"></a>İlgili desenleri ve Kılavuzu
Merhaba aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:  

* [Varlık Grup işlemleri](#entity-group-transactions)  
* [Heterojen varlık türleri ile çalışma](#working-with-heterogeneous-entity-types)  
* [Sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a>Günlük tail düzeni
Merhaba almak  *n*  eklenen en son tooa bölüm varlıklar kullanarak bir **RowKey** ters tarihi ve saati sipariş sıralar değeri.  

#### <a name="context-and-problem"></a>İçerik ve sorunu
En son oluşturulan hello varlıkları, bir çalışan tarafından gönderilen örneğin hello on en son gider talep edebilir tooretrieve olması ortak gerekli değildir. Tablo sorguları destek bir **$top** işlemi tooreturn hello önce sorgu  *n*  bir kümesindeki varlıkların: kümesindeki eşdeğer sorgu işlemi tooreturn hello son n varlık yok.  

#### <a name="solution"></a>Çözüm
Kullanarak deposu hello varlıklar bir **RowKey** doğal olarak ters sıralar sırası böylece hello en son giriş her zaman hello kullanarak Merhaba tablonun ilk yapısıyla tarih olduğunu.  

Örneğin, toobe mümkün tooretrieve en son on gider talep bir çalışan tarafından gönderilen Merhaba, geçerli tarih hello türetilmiş bir ters onay değeri kullanabilirsiniz. Merhaba aşağıdaki C# kod örneği bir yolu toocreate uygun "çizgilerine ters" değeri için gösteren bir **RowKey** hello en son toohello eski sıralar:  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

Koddan hello kullanarak toohello tarih saat değerine geri alabilirsiniz:  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

Merhaba Tablo sorgusu şöyle görünür:  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a>Sorunları ve dikkat edilmesi gerekenler
Merhaba karar verirken aşağıdaki noktaları göz önünde bulundurun nasıl tooimplement bu deseni:  

* Merhaba ters onay değeri sıfır eklenerek paneli tooensure hello dize değeri, beklenen şekilde sıralar.  
* Bir bölümün hello düzeyinde hello ölçeklenebilirlik hedefleri farkında olması gerekir. Dikkatli olun etkin nokta bölümleri oluşturma değil.  

#### <a name="when-toouse-this-pattern"></a>Zaman toouse bu deseni
Ters tarih sırası tooaccess varlıklarda gerektiğinde veya tooaccess hello en son ihtiyacınız olduğunda bu deseni kullanım varlıklar eklendi.  

#### <a name="related-patterns-and-guidance"></a>İlgili desenleri ve Kılavuzu
Merhaba aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:  

* [Başına / koruma düzeni ekleme](#prepend-append-anti-pattern)  
* [Varlıkları alma](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a>Yüksek hacimli delete düzeni
Yüksek hacimli varlıkların Hello silinmesini kendi ayrı tabloda eşzamanlı silme işlemi için tüm hello varlıklar depolayarak etkinleştirmek; Merhaba tablo silerek hello varlıkları silin.  

#### <a name="context-and-problem"></a>İçerik ve sorunu
Birçok uygulama artık toobe kullanılabilir tooa istemci uygulaması gereken eski verileri silmek veya hello uygulama tooanother depolama ortamına arşivlenmiş. Genellikle bu tür veriler tarihe göre belirleyin: Örneğin, bir gereksinim toodelete kayıtları 60 günden eski olan tüm oturum açma isteklerinin sahip.  

Bir olası tasarımdır toouse hello tarih ve saat hello hello oturum açma isteğinin **RowKey**:  

![][21]

Merhaba uygulaması eklemek ve ayrı bir bölüme her kullanıcı için oturum açma varlıkları silmek için bu yaklaşım bölüm etkin önler. Ancak, bu yaklaşım maliyetli olabilir ve zaman alıcı ilk tooperform gerektiğinden çok sayıda varlık varsa bir tablo tarama sipariş tooidentify tüm hello varlıklar toodelete ve eski her varlık silmeniz gerekir. Not EGTs birden çok silme isteklerinin'toplu işleme gidiş dönüş toohello gerekli sunucu toodelete hello eski varlıkları hello sayısını azaltabilirsiniz.  

#### <a name="solution"></a>Çözüm
Oturum açma denemesi her gün için ayrı bir tablo kullanın. Varlıklar ekleme ve eski varlıkları silmek şimdi her gün bir tablo silme yalnızca bir soru olduğunda hello varlık tasarım tooavoid etkin yukarıda kullanabilirsiniz (tek bir depolama işlemi) yerine bulma ve yüzlerce ve binlerce silme tek tek oturum açma varlıklar her gün.  

#### <a name="issues-and-considerations"></a>Sorunları ve dikkat edilmesi gerekenler
Merhaba karar verirken aşağıdaki noktaları göz önünde bulundurun nasıl tooimplement bu deseni:  

* Tasarımınızın, uygulamanızın belirli varlıklar, diğer veri ya da oluşturma toplama bilgisi ile bağlama bakarak gibi hello verileri kullanacak diğer yolları destekliyor mu?  
* Yeni varlıklar eklerken tasarımınızı etkin noktalar önlenir?  
* Tooreuse istiyorsanız bir gecikme hello aynı beklediğiniz silmeden sonra tablo adı. Bu, daha iyi tooalways benzersiz tablo adları kullan olur.  
* Merhaba tablo hizmeti hello erişimi desenleri öğrenir ve düğümlere hello bölümlerini dağıtır yeni bir tablo ilk kez kullandığınızda, bazı azaltma bekler. Toocreate yeni tablolar ne sıklıkta ihtiyacınız göz önünde bulundurmalısınız.  

#### <a name="when-toouse-this-pattern"></a>Zaman toouse bu deseni
Hello silmelisiniz varlıklar hacmi yüksek olduğunda bu deseni kullanarak aynı anda.  

#### <a name="related-patterns-and-guidance"></a>İlgili desenleri ve Kılavuzu
Merhaba aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:  

* [Varlık Grup işlemleri](#entity-group-transactions)
* [Varlıkları değiştirme](#modifying-entities)  

### <a name="data-series-pattern"></a>Veri serisi deseni
Mağaza tam veri serisi yaptığınız isteklerini tek bir varlık toominimize hello sayısı.  

#### <a name="context-and-problem"></a>İçerik ve sorunu
Yaygın bir senaryo için bir uygulama toostore, genellikle tooretrieve tümünü bir defada ihtiyaç duyduğu veri dizisidir. Örneğin, uygulamanız her çalışan her saat gönderir kaç anlık ileti iletileri kaydetmek ve önceki 24 saat üzerinden gönderilen her kullanıcı kaç iletileri hello bu bilgileri tooplot kullanın. Bir tasarım toostore 24 varlıklar her çalışana ait olabilir:  

![][22]

Bu tasarım ile kolayca bulmanıza ve Merhaba uygulaması tooupdate hello ileti sayısı değeri her gerektiğinde Merhaba varlık tooupdate her çalışan için güncelleştirin. Ancak, tooretrieve Merhaba bilgi tooplot hello etkinlik hello önceki 24 saat için bir grafik, 24 varlıklar almanız gerekir.  

#### <a name="solution"></a>Çözüm
Her saat için ayrı özellik toostore hello ileti sayısı ile tasarım aşağıdaki hello kullan:  

![][23]

Bu tasarımla, bir birleştirme işlemi tooupdate hello ileti sayısı çalışana ait belirli bir saat için kullanabilirsiniz. Şimdi, tek bir varlık için bir istek kullanarak tooplot hello grafik gerek duyduğunuz tüm hello bilgi alabilirsiniz.  

#### <a name="issues-and-considerations"></a>Sorunları ve dikkat edilmesi gerekenler
Merhaba karar verirken aşağıdaki noktaları göz önünde bulundurun nasıl tooimplement bu deseni:  

* Tam veri dizileriniz (bir varlık too252 özelliklerini olabilir) tek bir varlık içine uygun değilse, alternatif veri deposu blob gibi kullanın.  
* Bir varlık aynı anda güncelleştirme birden fazla istemciniz varsa toouse hello gerekir **ETag** tooimplement iyimser eşzamanlılık. Birçok istemciniz varsa, yüksek çakışma karşılaşabilirsiniz.  

#### <a name="when-toouse-this-pattern"></a>Zaman toouse bu deseni
Tooupdate gerekir ve tek bir varlık ile ilişkili bir veri serisi almak olduğunda bu deseni kullanır.  

#### <a name="related-patterns-and-guidance"></a>İlgili desenleri ve Kılavuzu
Merhaba aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:  

* [Büyük varlıklar düzeni](#large-entities-pattern)  
* [Birleştirme ya da değiştirme](#merge-or-replace)  
* [Sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern) (, hello veri serisi bir blob'a depoladığınız varsa)  

### <a name="wide-entities-pattern"></a>Geniş varlıklar düzeni
Birden çok fiziksel varlıkların toostore mantıksal varlık ile birden çok 252 özellik kullanın.  

#### <a name="context-and-problem"></a>İçerik ve sorunu
Tek bir varlık (Merhaba zorunlu sistem özellikleri dışında) en çok 252 özellik olabilir ve birden fazla 1 MB veri toplama depolanamıyor. İlişkisel bir veritabanında, genellikle bir satır hello boyutu üzerinde herhangi bir sınır round yeni bir tablo ekleyerek ve aralarında 1-1 ilişkisi zorlamayı elde edebileceğiniz.  

#### <a name="solution"></a>Çözüm
Merhaba tablo hizmetini kullanarak, birden çok varlık toorepresent birden çok 252 özellik tek büyük iş nesnesiyle depolayabilirsiniz. Örneğin, toostore bir sayısını hello her çalışan hello için son 365 gün gönderilen IM iletilerini isterseniz, iki varlık farklı şemalarda kullanan tasarım aşağıdaki hello kullanabilirsiniz:  

![][24]

Toomake birbirleri ile eşitlenen hem varlıklar tookeep güncelleştirilmesi için bir değişiklik gerekirse bir EGT kullanabilirsiniz. Aksi halde, bir tek birleştirme işlemi tooupdate hello ileti sayısı için belirli bir gün kullanabilirsiniz. Tüm hello veri hem kullanan iki verimli istekleri ile yapmak için her iki varlıkları almak gerekir belirli bir çalışan tooretrieve bir **PartitionKey** ve **RowKey** değeri.  

#### <a name="issues-and-considerations"></a>Sorunları ve dikkat edilmesi gerekenler
Merhaba karar verirken aşağıdaki noktaları göz önünde bulundurun nasıl tooimplement bu deseni:  

* Eksiksiz bir mantıksal varlık alma, en az iki depolama işlemleri içerir: bir tooretrieve fiziksel varlık.  

#### <a name="when-toouse-this-pattern"></a>Zaman toouse bu deseni
Gereksinim toostore varlıklar, boyutunu veya sayısını özelliklerinin hello tek tek bir varlık için hello sınırlarını aşıyor tablo hizmeti olduğunda bu deseni kullanır.  

#### <a name="related-patterns-and-guidance"></a>İlgili desenleri ve Kılavuzu
Merhaba aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:  

* [Varlık Grup işlemleri](#entity-group-transactions)
* [Birleştirme ya da değiştirme](#merge-or-replace)

### <a name="large-entities-pattern"></a>Büyük varlıklar düzeni
BLOB Depolama toostore büyük özellik değerlerini kullanın.  

#### <a name="context-and-problem"></a>İçerik ve sorunu
Tek bir varlık 1 MB'tan fazla veri toplama depolanamıyor. Bir veya birkaç özelliklerinizin hello toplam boyutu, varlık tooexceed bu değeri neden değerleri depolarsanız, hello tablo hizmeti hello tüm varlık depolanamıyor.  

#### <a name="solution"></a>Çözüm
Bir veya daha fazla özellikleri büyük miktarda veri içerdiğinden varlığınız 1 MB boyutunda aşarsa, hello Blob hizmeti verileri depolamak ve ardından hello varlık özelliğinde hello blob hello adresini depolamak. Örneğin, bir çalışanın hello fotoğraf blob storage'da depolamak ve bağlantı toohello fotoğraf hello depolamak **fotoğraf** çalışan varlığınız özelliği:  

![][25]

#### <a name="issues-and-considerations"></a>Sorunları ve dikkat edilmesi gerekenler
Merhaba karar verirken aşağıdaki noktaları göz önünde bulundurun nasıl tooimplement bu deseni:  

* Merhaba tablo hizmeti hello varlık ve hello Blob hizmeti hello verileri arasında toomaintain nihai tutarlılık kullanmak hello [sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern) toomaintain varlıklarınızı.
* Eksiksiz bir varlık alma, en az iki depolama işlemleri içerir: bir tooretrieve hello varlık ve bir tooretrieve hello blob veri.  

#### <a name="when-toouse-this-pattern"></a>Zaman toouse bu deseni
Büyüklüğü hello tablo hizmetinde tek bir varlık için hello sınırlarını aşıyor toostore varlıklar ihtiyacınız olduğunda bu deseni kullanır.  

#### <a name="related-patterns-and-guidance"></a>İlgili desenleri ve Kılavuzu
Merhaba aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:  

* [Sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern)  
* [Geniş varlıklar düzeni](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a>Koruma deseni başına ve ekleme
Birden çok bölüm arasında hello eklemeleri yayarak eklemeleri hacmi yüksek olduğunda ölçeklenebilirliği artırmak.  

#### <a name="context-and-problem"></a>İçerik ve sorunu
Eklenmesini veya varlıklar depolanan tooyour varlıklar genellikle ekleme sonuçları yeni varlıklar toohello eklenmediği hello uygulamada veya son bölümü, bir dizi bölümler. Bu durumda, tüm hello eklemeleri verilen herhangi bir zamanda birden fazla düğümleri arasında Yük Dengeleme hello tablo hizmeti engelleyen bir etkin nokta oluşturma aynı bölüme ekler hello yerinde alma ve büyük olasılıkla, uygulama toohit hello ölçeklenebilirlik neden bölüm için hedefler. Örneğin, aşağıda gösterildiği gibi bir varlık yapısı neden sonra çalışanlar tarafından erişim günlükleri ağ ve kaynak bir uygulamanız varsa hello toplu işlemler için hello ölçeklenebilirlik hedef ulaşırsa bir etkin nokta olmadan geçerli saatlik bölüm hello tek bir bölümü:  

![][26]

#### <a name="solution"></a>Çözüm
Merhaba aşağıdaki alternatif varlık yapısı herhangi bir bölümü etkin nokta hello uygulama günlükleri olayları ortadan kaldırır:  

![][27]

Bu örnek ile nasıl her ikisi de hello dikkat edin **PartitionKey** ve **RowKey** bileşik anahtarlar. Merhaba **PartitionKey** hello departman ve çalışan kimliği toodistribute hello günlüğü arasında birden çok bölüm kullanır.  

#### <a name="issues-and-considerations"></a>Sorunları ve dikkat edilmesi gerekenler
Merhaba karar verirken aşağıdaki noktaları göz önünde bulundurun nasıl tooimplement bu deseni:  

* Dinamik bölümleri ekler üzerinde verimli bir şekilde destek hello sorgular oluşturma engelleyen mu hello alternatif anahtar yapısı istemci uygulamanızı yapar?  
* Beklenen biriminiz hareketlerinin hello ölçeklenebilirlik hedefleri tek tek bir bölüm için büyük olasılıkla tooreach olan ve hello depolama hizmeti tarafından kısıtlanan anlama geliyor?  

#### <a name="when-toouse-this-pattern"></a>Zaman toouse bu deseni
Biriminiz hareketlerinin etkin bölüm eriştiğinizde hello depolama hizmeti tarafından azaltma, büyük olasılıkla tooresult olduğunda hello başına/append koruma düzeni kaçının.  

#### <a name="related-patterns-and-guidance"></a>İlgili desenleri ve Kılavuzu
Merhaba aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:  

* [Bileşik anahtar düzeni](#compound-key-pattern)  
* [Günlük tail düzeni](#log-tail-pattern)  
* [Varlıkları değiştirme](#modifying-entities)  

### <a name="log-data-anti-pattern"></a>Günlük veri koruma düzeni
Genellikle, tablo hizmeti toostore günlük verilerini hello yerine hello Blob hizmeti kullanmanız gerekir.  

#### <a name="context-and-problem"></a>İçerik ve sorunu
Günlük verileri tooretrieve belirli tarih aralığı için günlük girişlerini seçimi için ortak bir kullanım örneği: Örneğin, tüm hello 15:04 15:06 belirli bir tarihte arasındaki uygulamanız oturum hata ve kritik iletileri toofind istiyorsunuz. Toouse hello tarih ve saat hello günlük iletisi toodetermine hello bölümün günlük varlıklara kaydetmek istiyor musunuz: belirli bir zamanda, tüm hello günlük varlıklar paylaşacak çünkü etkin bölüm sonuçlarında aynı hello olduğunu **PartitionKey** değer (Merhaba bölümüne bakın [Prepend ve append koruma düzeni](#prepend-append-anti-pattern)). Örneğin, Merhaba uygulaması toohello bölüm hello geçerli tarih ve saat için tüm günlük iletilerini yazdığından bir günlük iletisi için varlık Şeması aşağıdaki hello etkin bir bölümünde sonuçları:  

![][28]

Bu örnekte, hello **RowKey** başlangıç tarihi ve saati hello günlük iletisi tooensure günlüğü iletileri, tarih/saat düzende sıralanmış olarak depolanır içerir ve birden çok günlük iletilerini aynı tarih ve saat hello paylaşmak durumunda bir ileti kimliği içerir.  

Başka bir yaklaşımdır toouse bir **PartitionKey** sağlar hello uygulama bölümleri aralığı iletileri yazar. Örneğin, Hello hello günlüğü kaynağı iletisi birçok bölümler iletileri yolu toodistribute sağlıyorsa, varlık şema aşağıdaki hello kullanabilirsiniz:  

![][29]

Ancak, tüm hello gerekir arama günlüğü iletileri belirli bir süre için o tooretrieve Bu şemayı hello sorun mu hello tablosundaki her bölüm.

#### <a name="solution"></a>Çözüm
toouse çalışırken hello önceki bölümünde vurgulanan hello sorununu tablo hizmeti toostore günlük girişlerini Merhaba ve iki, yetersiz önerilen, tasarlar. Günlük iletileri yazma performansının düşük hello riskini ile neden bir çözüm tooa etkin bölüm; Merhaba başka bir çözümü zayıf sorgu performansı hello gereksinim tooscan nedeniyle hello tablo tooretrieve günlük iletilerini belirli bir süre için her bölümün sonuçlandı. BLOB storage bu tür senaryosu için daha iyi bir çözüm sunar ve bu topladığı nasıl Azure depolama çözümlemeleri hello günlük veriyi depolar.  

Bu bölümde, nasıl Storage Analytics bir aralık tarafından genellikle sorgu bu yaklaşım toostoring veri çizimi olarak blob depolama alanına günlük verilerini depolar özetlenmektedir.  

Storage Analytics günlük iletilerini birden çok BLOB'ları sınırlandırılmış biçimde depolar. Merhaba sınırlandırılmış biçimi için bir istemci uygulama tooparse hello verileri hello günlük iletisinde kolaylaştırır.  

Storage Analytics bir adlandırma kuralı, aradığınız hello günlük iletilerini içeren toolocate hello blob (veya BLOB) sağlayan BLOB'lar için kullanır. Örneğin, "queue/2014/07/31/1800/000001.log" adlı bir blob hello saat 18:00 31 Temmuz 2014 üzerinde başlayarak toohello sıra hizmeti ile ilgili günlük iletilerini içerir. Merhaba "000001" Bu hello ilk günlük dosyası bu dönem için gösterir. Storage Analytics ayrıca hello hello damgalarının ilk kaydeder ve son hello blob'un meta verilerinin bir parçası hello dosyasında depolanan iletilerini günlüğe kaydet. Merhaba API adı ön ekini temel alarak bir kapsayıcıdaki blobları bulmanıza blob depolama etkinleştirir: toolocate sıra içeren tüm hello BLOB'lar günlük veri hello saat 18: 00'dan başlayarak, hello önek "sıra/2014/07/31/1800." kullanabilirsiniz  

Storage Analytics günlük iletilerini dahili arabelleğe alır ve hello uygun blob düzenli olarak güncelleştirir veya hello en son toplu günlük girişlerinin ile yeni bir tane oluşturur. Bu hello azaltır yazma toohello blob hizmeti gerçekleştirmeniz gerekir.  

Benzer bir çözüm, kendi uygulamanızda uyguluyorsanız, nasıl toomanage hello (olduğu sürece her günlük girişi tooblob depolama yazma) güvenilirlik ve maliyet ve ölçeklenebilirlik arasındaki dengelemeyi dikkate almanız gerekir (güncelleştirmeler, uygulamanızda arabelleğe alma ve bunları tooblob depolama toplu olarak yazma).  

#### <a name="issues-and-considerations"></a>Sorunları ve dikkat edilmesi gerekenler
Merhaba nasıl toostore oturum veri karar verirken aşağıdaki noktaları göz önünde bulundurun:  

* Olası dinamik bölümleri önler bir tablo tasarımı oluşturursanız, günlük verilerinizi verimli bir şekilde erişemiyor bulabilirsiniz.  
* tooprocess verilerini günlüğe, bir istemci, genellikle tooload çok sayıda kayıt gerekiyor.  
* Günlük verileri genellikle yapılandırılmış olsa da, blob depolama daha iyi bir çözüm olabilir.  

### <a name="implementation-considerations"></a>Uygulama konuları
Merhaba önceki bölümlerde açıklanan hello desenleri uyguladığınızda bu bölümde hello konuları toobear aklınızda bazıları açıklanmaktadır. Bu bölümde çoğunu hello depolama istemci kitaplığı (sürüm 4.3.0 yazma hello zamanında) kullanan C# ile yazılmış örnekler kullanır.  

### <a name="retrieving-entities"></a>Varlıkları alma
Merhaba bölümünde açıklandığı gibi [sorgulamak için tasarım](#design-for-querying), hello en verimli sorgudur noktası sorgusu. Ancak, bazı senaryolarda birden çok varlık tooretrieve gerekebilir. Bu bölümde hello depolama istemci kitaplığı kullanılarak bazı ortak yaklaşımlar tooretrieving varlıklar açıklanmaktadır.  

#### <a name="executing-a-point-query-using-hello-storage-client-library"></a>Merhaba depolama istemci kitaplığı kullanılarak noktası sorgusu yürütme
Merhaba en kolay yolu tooexecute noktası sorgusu olduğundan toouse hello **almak** sahip bir varlık alır, C# kod parçacığını aşağıdaki hello gösterildiği gibi işlemi tablo bir **PartitionKey** değer "Satış" ve bir  **RowKey** "212" değerinin:  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

Bu örnek hello varlık nasıl bekliyor fark toobe türü alır **EmployeeEntity**.  

#### <a name="retrieving-multiple-entities-using-linq"></a>LINQ kullanarak birden çok varlık alma
LINQ ile depolama istemci kitaplığı kullanılarak ve bir sorgu belirterek birden çok varlık almak bir **burada** yan tümcesi. tooavoid bir tablo taraması, hello her zaman içermelidir **PartitionKey** hello değerinde burada yan tümcesi ve mümkünse hello **RowKey** tooavoid tablo ve bölüm taramalar değeri. Merhaba tablo hizmeti Karşılaştırma işleçleri (büyük, daha büyük veya eşit, daha az daha küçüktür veya eşit, eşit ve eşit değil) toouse sınırlı sayıda hello destekler nerede yan tümcesi. Merhaba aşağıdaki C# kod parçacığını tüm hello çalışanlar, son adı ile başlayan, "B" bulur (Bu hello varsayılarak **RowKey** depoları hello Soyadı) hello satış departmanında (Merhaba varsayılarak **PartitionKey** depoları hello bölüm adı):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

Nasıl hello sorgu her ikisi de belirtiyor fark bir **RowKey** ve **PartitionKey** tooensure daha iyi performans.  

Merhaba aşağıdaki kod örneği hello fluent API kullanılarak eşdeğer işlevselliğini göstermektedir (genel olarak, akıcı API'ler hakkında daha fazla bilgi için bkz [Fluent API tasarlamak için en iyi yöntemler](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> Merhaba örnek katmandan birden çok **CombineFilters** yöntemleri tooinclude hello üç filtre koşulu.  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a>Sorgudan çok sayıda varlık alma
En iyi sorgu göre tek bir varlık döndüren bir **PartitionKey** değeri ve **RowKey** değeri. Bununla birlikte, bazı senaryolarda aynı bölüm ve hatta birçok bölümlerden hello birçok varlıklardan gereksinim tooreturn olabilir.  

Her zaman tam gibi senaryolarda hello uygulamanızın performansını test etmeniz gerekir.  

Bir sorgu hello tablo hizmeti en çok 1.000 varlıkları aynı anda döndürebilir ve en fazla beş saniyede için yürütür. Merhaba sonuç kümesi 1. 000'den fazla varlıklar içeriyorsa, hello sorgu beş saniye içinde tamamlanmadı veya hello sorgu hello bölüm sınır kestiği, hello tablo hizmeti verir. devamlılık belirteci tooenable hello istemci uygulaması toorequest hello varlıkları sonraki kümesi. İş devamlılığı nasıl belirteçleri hakkında daha fazla bilgi için bkz: [sorgu zaman aşımı ve sayfa numaralandırma](http://msdn.microsoft.com/library/azure/dd135718.aspx).  

Merhaba depolama istemci kitaplığı kullanıyorsanız, tablo hizmeti hello varlıklar döndürüyor gibi otomatik olarak devamlılık belirteçleri sizin için işleyebilir. Merhaba tablo hizmeti bunları bir yanıt döndürürse hello hello depolama istemci kitaplığı kullanılarak otomatik olarak aşağıdaki C# kod örneği devamlılık belirteçleri işler:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

C# kod aşağıdaki hello devamlılık belirteçleri açıkça işler:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

Devamlılık belirteçleri açıkça kullanarak uygulamanızı hello sonraki segment veri zaman alır kontrol edebilirsiniz. İstemci uygulamanız bir tabloda depolanan hello varlıklar aracılığıyla kullanıcılar toopage etkinleştirirse, bir kullanıcı değil, uygulamanızın yalnızca bir devamlılık belirteci tooretrieve hello sonraki kullanırsınız şekilde hello sorgu tarafından alınan tüm hello varlıklar aracılığıyla toopage Örneğin, karar verebilirsiniz Merhaba kullanıcı hello geçerli kesimindeki tüm hello varlıklar sayfalama bittiğinde kesimi. Bu yaklaşımın birkaç avantaj vardır:  

* Merhaba tablo hizmeti gelen veri tooretrieve toolimit hello miktarını ve hello ağ üzerinden taşıması sağlar.  
* Bu, tooperform zaman uyumsuz g/ç .NET içinde sağlar.  
* Bir uygulama kilitlenme hello olayda devam edebilmek için tooserialize hello devamlılık belirteci toopersistent depolama sağlar.  

> [!NOTE]
> Daha az olabilir ancak bir devamlılık belirteci 1.000 varlık içeren bir kesimi genellikle döndürür. Bir sorgunun döndürdüğü kullanarak girişleri hello sayısı sınırı, aynı zamanda hello böyledir **ele** arama ölçütlerinizle eşleşen tooreturn hello ilk n varlıklar: hello tablo hizmeti n varlıklar taneden içeren bir segment döndürebilir devamlılık belirteci tooenable ile tooretrieve hello kalan varlıklar.  
> 
> 

Merhaba aşağıdaki C# kod toomodify hello varlıkların sayısı bir kesim içinde nasıl döndürülen gösterir:  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a>Sunucu tarafı projeksiyonu
Tek bir varlık too255 özelliklerini sahip ve too1 MB boyutunda olabilir. Sorgu hello tablo ve varlıkları almak yaptığınızda, tüm hello özellikleri gerekli değildir ve veri gereksiz yere aktarılmasını önlemek (toohelp azaltmak gecikme süresi ve maliyet). Gereksinim sunucu tarafı projeksiyon tootransfer yalnızca hello özellikleri kullanabilirsiniz. Merhaba aşağıdaki alır yalnızca hello örnektir **e-posta** özelliği (ile birlikte **PartitionKey**, **RowKey**, **zaman damgası**ve  **ETag**) hello sorgu tarafından seçilen hello gelen.  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

Nasıl hello fark **RowKey** değeri, hello özellikleri tooretrieve listesinde eklenmemiş olsa da kullanılabilir.  

### <a name="modifying-entities"></a>Varlıkları değiştirme
Merhaba depolama istemci kitaplığı, varlıklarınızı hello tablo hizmetinde ekleme, silme ve güncelleştirme varlıkları tarafından depolanan toomodify sağlar. Birden çok INSERT, update ve birlikte tooreduce hello gidiş dönüş sayısı gerekli ve çözümünüzü hello performansını silme işlemleri EGTs toobatch kullanabilirsiniz.  

Merhaba depolama istemci kitaplığı bir EGT genellikle yürüttüğünde oluşturulan özel durumları hello toplu toofail neden hello varlık hello dizini içerdiğini unutmayın. EGTs kullanan kodu ayıklarken bu yararlıdır.  

İstemci uygulamanızı eşzamanlılık ve güncelleştirme işlemlerinin nasıl işlediğini tasarımınızı nasıl etkileyeceğini de dikkate almalısınız.  

#### <a name="managing-concurrency"></a>Eşzamanlılık yönetme
Merhaba tablo hizmeti varsayılan olarak, iyimser eşzamanlılık denetler için tek tek varlıkların hello düzeyinde uygulayan **Ekle**, **birleştirme**, ve **silmek** işlemleri Bu denetimler hizmet toobypass istemci tooforce hello tablo için bu mümkün olsa da. Merhaba tablo hizmeti eşzamanlılık nasıl yönettiği hakkında daha fazla bilgi için bkz: [yönetme eşzamanlılık Microsoft Azure depolama alanında](../storage/common/storage-concurrency.md).  

#### <a name="merge-or-replace"></a>Birleştirme ya da değiştirme
Merhaba **Değiştir** hello yöntemi **TableOperation** sınıfı her zaman tam varlık hello tablo hizmeti hello yerini alır. Bu özellik depolanan hello varlık mevcut olduğunda, bir özellik hello istekte içermiyorsa, hello isteği hello özelliğinden varlık depolanan kaldırır. Tooremove bir özellikten açıkça saklı varlık istemediğiniz sürece hello istekte her özellik eklemeniz gerekir.  

Merhaba kullanabilirsiniz **birleştirme** hello yöntemi **TableOperation** sınıfı tooreduce hello tooupdate istediğinizde bir varlık toohello tablo hizmeti gönderme veri miktarı. Merhaba **birleştirme** yöntemi hello isteğinde hello varlıktan özelliği değerlerle depolanan hello varlıktaki tüm özelliklerini değiştirir, ancak olduğu gibi bırakır hello herhangi özelliklerinde saklanan hello istekte dahil edilmeyen varlık. Büyük varlıklar varsa ve yalnızca küçük bir istek özelliklerinde çeşitli tooupdate gerekir, bu yararlı olur.  

> [!NOTE]
> Merhaba **Değiştir** ve **birleştirme** yöntemler başarısız hello varlık mevcut değilse. Alternatif olarak, hello kullanabilirsiniz **Yerleştir veya Değiştir** ve **InsertOrMerge** yoksa, yeni varlık oluşturma yöntemleri.  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a>Heterojen varlık türleri ile çalışma
Merhaba tablo hizmeti olan bir *şema daha az* tasarımınızda büyük esneklik sağlayan birden çok tür varlıklarının tek bir tabloyu depolayabilir anlamına gelir tablo deposu. Merhaba aşağıdaki örnekte çalışan ve departman varlıkları depolayan bir tablo gösterilmektedir:  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>zaman damgası</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>Soyadı</th>
<th>Yaş</th>
<th>E-posta</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>Soyadı</th>
<th>Yaş</th>
<th>E-posta</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>departmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>Soyadı</th>
<th>Yaş</th>
<th>E-posta</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

Her varlığın hala olmalıdır Not **PartitionKey**, **RowKey**, ve **zaman damgası** değerleri, ancak herhangi bir özellikler kümesi olabilir. Ayrıca, bir şey yok tooindicate hello bu bilgileri bir yerde toostore seçmediğiniz sürece bir varlığın türü. Merhaba varlık türünü tanımlamak için iki seçenek vardır:  

* Merhaba varlık türü toohello başına **RowKey** (veya büyük olasılıkla hello **PartitionKey**). Örneğin, **EMPLOYEE_000123** veya **DEPARTMENT_SALES** olarak **RowKey** değerleri.  
* Merhaba aşağıdaki tabloda gösterildiği gibi bir ayrı özellik toorecord hello varlık türü kullanın.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>zaman damgası</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>FirstName</th>
<th>Soyadı</th>
<th>Yaş</th>
<th>E-posta</th>
</tr>
<tr>
<td>Çalışan</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>FirstName</th>
<th>Soyadı</th>
<th>Yaş</th>
<th>E-posta</th>
</tr>
<tr>
<td>Çalışan</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>departmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>Bölüm</td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>FirstName</th>
<th>Soyadı</th>
<th>Yaş</th>
<th>E-posta</th>
</tr>
<tr>
<td>Çalışan</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

Merhaba varlık türü toohello eklenmesini hello ilk seçenek **RowKey**, iki varlık farklı türlerde hello olabilir olasılığı varsa aynı anahtar değerini yararlıdır. Ayrıca, aynı birlikte hello bölümünde yazın hello varlıklarının gruplandırır.  

Merhaba Bu bölümde açıklanan teknikleri olan özellikle ilgili toohello tartışma [devralma ilişkileri](#inheritance-relationships) hello bölümünde bu kılavuzun önceki bölümlerinde [ilişkileri modelleme](#modelling-relationships).  

> [!NOTE]
> Merhaba varlık türü değeri tooenable istemci uygulamaları tooevolve POCO nesneleri bir sürüm numarası dahil etmeyi düşünün ve farklı sürümleri ile çalışması gerekir.  
> 
> 

Merhaba Bu bölüm geri kalanı hello depolama istemci kitaplığı içindeki hello içindeki birden çok varlık türleriyle aynı çalışma kolaylaştırmak hello özelliklerinden bazıları açıklanmaktadır tablo.  

#### <a name="retrieving-heterogeneous-entity-types"></a>Heterojen varlık türleri alınıyor
Merhaba depolama istemci kitaplığı kullanıyorsanız, birden çok varlık türleri ile çalışmak için üç seçeneğiniz vardır.  

Belirli bir ile depolanan hello varlığın hello türü biliyorsanız **RowKey** ve **PartitionKey** hello önceki iki örneklerde gösterildiği gibi hello varlık aldığınızda hello varlık türünü belirtebilirsiniz ardından değerleri türündeki varlıklar almak **EmployeeEntity**: [hello depolama istemci kitaplığı kullanılarak noktası sorgusu yürütme](#executing-a-point-query-using-the-storage-client-library) ve [LINQkullanarakbirdençokvarlıkalma](#retrieving-multiple-entities-using-linq).  

Merhaba ikinci seçenektir toouse hello **DynamicTableEntity** türü (bir özellik paketi) somut bir POCO varlık türü yerine (Bu seçenek gerek tooserialize olduğundan performansı da hello varlık çok seri durumdan. NET türleri için). C# kodu potansiyel olarak aşağıdaki hello farklı türlerde birden çok varlık hello tablosundan alır, ancak tüm varlıklar olarak döndürür **DynamicTableEntity** örnekleri. Daha sonra hello kullanır **EntityType** özelliği toodetermine hello her varlık türü:  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

Bu tooretrieve hello kullanmaları gereken diğer özellikleri Not **TryGetValue** hello yöntemi **özellikleri** hello özelliğinin **DynamicTableEntity** sınıfı.  

Hello kullanarak toocombine üçüncü seçenek olan **DynamicTableEntity** türü ve bir **Varlıkçözümleyicisi** örneği. Bu tooresolve toomultiple POCO hello türlerinde sağlar aynı sorgu. Bu örnekte, hello **Varlıkçözümleyicisi** temsilci hello kullanarak **EntityType** özelliği toodistinguish hello iki sorgunun döndürdüğü hello varlık türleri arasında. Merhaba **gidermek** yöntemi kullanan hello **çözümleyici** temsilci tooresolve **DynamicTableEntity** çok örnekleri**TableEntity** örnekleri.  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a>Heterojen varlık türlerini değiştirme
Bir varlık toodelete tooknow hello türü ve size, eklediğinizde her zaman bir varlığın hello türü gerekmez. Ancak, kullanabileceğiniz **DynamicTableEntity** tooupdate bir varlık türünü bilerek ve bir POCO varlık sınıfı kullanarak olmadan yazın. Merhaba aşağıdaki kod örneği tek bir varlık alır ve denetler hello **EmployeeCount** özellik var güncelleştirmeden önce.  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a>Paylaşılan erişim imzaları ile erişimi denetleme
Paylaşılan erişim imzası (SAS) belirteçleri tooenable istemci uygulamaları toomodify (ve kullanabileceğiniz sorgu) tablo varlıkları hello gerek tooauthenticate hello tablo hizmeti ile doğrudan olmadan doğrudan. Genellikle, üç ana faydası toousing SAS uygulamanızda vardır:  

* Toodistribute gerekmez depolama alanınızı (örneğin, bir mobil cihaz) anahtar tooan güvenli platform sipariş tooallow o aygıtı tooaccess hesap ve hello tablo hizmeti varlıklarda değiştirin.  
* Hello iş bazıları bu web boşaltabilir ve çalışan rolleri varlıklar tooclient aygıtlarınızı örneğin son kullanıcı bilgisayarlar ve mobil cihazları yönetme de gerçekleştirebilirsiniz.  
* Bir kısıtlanmış atayabilir ve izinleri tooa istemci (örneğin, salt okunur erişime izin verme toospecific kaynakları) kümesini zaman sınırlıdır.  

SAS belirteci hello tablo hizmeti ile kullanma hakkında daha fazla bilgi için bkz: [kullanarak paylaşılan erişim imzaları (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md).  

Ancak, yine bir istemci uygulama toohello varlıkları hello tablo hizmetinde vermek hello SAS belirteci oluşturmanız gerekir: tooyour depolama hesabı anahtarlarını güvenli erişim sahip bir ortamda yapmalısınız. Genellikle, SAS belirteçler ve bunları tooyour varlıklar erişmesi toohello istemci uygulamaları ileten bir web veya çalışan rolü toogenerate hello kullanın. Olduğundan hala bir ek yük oluşturma ve SAS belirteçleri tooclients teslim etmek, yüksek hacimli senaryolarda özellikle bu ek yükü en iyi nasıl tooreduce göz önünde bulundurmalısınız.  

Bu, olası toogenerate verir tooa alt tabloda hello varlıkların erişim bir SAS belirteci olur. Varsayılan olarak, tüm tablo için bir SAS belirteci oluşturur, ancak aynı zamanda bu hello SAS belirteci grant erişim tooeither bir dizi olası toospecify olan **PartitionKey** değerleri veya bir dizi **PartitionKey** ve  **RowKey** değerleri. Her kullanıcının SAS belirteci yalnızca erişim veren şekilde toogenerate sisteminizin bireysel kullanıcılar için SAS belirteci seçebilirsiniz tootheir kendi hello varlıklarda tablo hizmeti.  

### <a name="asynchronous-and-parallel-operations"></a>Zaman uyumsuz ve paralel işlemleri
İsteklerinizi birden çok bölüm arasında yayılmak sağlanan zaman uyumsuz veya paralel sorguları kullanarak verimlilik ve istemci yanıt hızını artırabilir.
Örneğin, tablolarınızı paralel erişme iki veya daha fazla çalışan rolü örneklerine sahip olabilir. Ayrı ayrı çalışan rolleri bölümler belirli kümeleri için sorumlu olan veya yalnızca sahip birden çok çalışan rolü örnekleri, her mümkün tooaccess tüm bir tabloda bölümler hello.  

Bir istemci örneği içinde depolama işlemlerini zaman uyumsuz olarak yürüterek üretilen işi artırabilir. Merhaba depolama istemci kitaplığı kolay toowrite zaman uyumsuz sorgular ve değişiklikleri yapar. Örneğin, C# kod aşağıdaki hello gösterildiği gibi tüm hello varlıkları bir bölüme alır hello zaman uyumlu yöntemi ile başlayabilirsiniz:  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

Zaman uyumsuz şekilde hello sorgu çalıştığında bu kodu kolayca değiştirebilirsiniz:  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

Zaman uyumsuz Bu örnekte, hello zaman uyumlu sürümünden hello aşağıdaki değişiklikler görebilirsiniz:  

* Merhaba yöntemi imza şimdi hello içeren **zaman uyumsuz** değiştiricisini ve döndürür bir **görev** örneği.  
* Arama hello yerine **ExecuteSegmented** yöntemi tooretrieve sonuçları, hello yöntemi şimdi çağrıları hello **ExecuteSegmentedAsync** yöntemi ve kullandığı hello **await** değiştiricisi zaman uyumsuz olarak tooretrieve sonuçlanır.  

Merhaba istemci uygulaması, bu yöntem birden çok kez çağırabilir (Merhaba farklı değerlere sahip **departmanı** parametresi), ve her sorgu ayrı bir iş parçacığı üzerinde çalışır.  

Merhaba hiçbir zaman uyumsuz sürümü olduğuna dikkat edin **yürütme** hello yönteminde **TableQuery** çünkü sınıf hello **IEnumerable** arabirimi zaman uyumsuz desteklemiyor sabit listesi.  

Ekle, Güncelleştir ve varlıkları zaman uyumsuz olarak silin. Aşağıdaki C# örneğine hello basit, zaman uyumlu yöntemi tooinsert gösterir veya bir çalışan varlığı değiştirme:  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

Merhaba güncelleştirme aşağıdaki gibi zaman uyumsuz çalışır kolayca bu kodu değiştirebilirsiniz:  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

Zaman uyumsuz Bu örnekte, hello zaman uyumlu sürümünden hello aşağıdaki değişiklikler görebilirsiniz:  

* Merhaba yöntemi imza şimdi hello içeren **zaman uyumsuz** değiştiricisini ve döndürür bir **görev** örneği.  
* Arama hello yerine **yürütme** yöntemi tooupdate hello varlık, hello yöntemi şimdi çağrıları hello **ExecuteAsync** yöntemi ve kullandığı hello **await** değiştiricisi tooretrieve zaman uyumsuz olarak sonuçlanır.  

Merhaba istemci uygulaması bunun gibi birden çok zaman uyumsuz yöntemleri çağırabilir ve her yöntem çağırma ayrı bir iş parçacığı üzerinde çalışır.  

### <a name="credits"></a>KREDİLERİ
Merhaba Katkıları için Azure ekibi üyeleri aşağıdaki toothank hello isteriz: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah ve Serdar Ozler yanı sıra Microsoft DX gelen zel Hollander. 

Ayrıca Microsoft MVP ait değerli görüşlerini gözden geçirme döngüsü sırasında aşağıdaki toothank hello isteriz: Igor Papirov ve Edward Bakker.

[1]: ./media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: ./media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: ./media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: ./media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: ./media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: ./media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: ./media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: ./media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: ./media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: ./media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: ./media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: ./media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: ./media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: ./media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: ./media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: ./media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: ./media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: ./media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: ./media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: ./media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: ./media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: ./media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: ./media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: ./media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: ./media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: ./media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: ./media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: ./media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: ./media/storage-table-design-guide/storage-table-design-IMAGE29.png

