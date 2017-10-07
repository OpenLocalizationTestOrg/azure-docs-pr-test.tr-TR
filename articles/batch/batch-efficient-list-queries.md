---
title: "aaaDesign verimli listesi sorguları - Azure Batch | Microsoft Docs"
description: "Havuzlar, işler, görevler gibi Batch kaynaklarını hakkında bilgi isterken sorgularınızı filtreleyerek performansını artırmak ve işlem düğümleri."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7e554119ec9d0e9e8007ccfb1ca80fe142a5e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-queries-toolist-batch-resources-efficiently"></a>Sorgular toolist Batch kaynaklarını verimli bir şekilde oluşturun

Burada tooincrease hello işleri sorguladığınızda hello hizmet tarafından döndürülen veri miktarını azaltarak Azure Batch uygulamanızın performansını nasıl görevler ve işlem düğümlerini hello ile öğreneceksiniz [Batch .NET] [ api_net] kitaplığı.

Neredeyse tüm Batch uygulamaları tooperform hello Batch hizmeti düzenli aralıklarla genellikle sorgular izleme ya da başka işlem bazı türü gerekir. Örneğin, toodetermine bir işi kalan tüm kuyruğa alınmış görevlerin olsanız da, hello işteki her görevde veri almanız gerekir. havuzunuzdaki düğümler toodetermine hello durumu, hello havuzdaki her düğümde veri almanız gerekir. Bu makalede, nasıl tooexecute gibi hello sorgular açıklanmaktadır en verimli şekilde.

> [!NOTE]
> Merhaba toplu işlem hizmetinin işteki görevler sayım hello yaygın bir senaryo için özel API desteği sağlar. Bir liste sorgusu için kullanmak yerine, hello çağırabilirsiniz [alma görev sayar] [ rest_get_task_counts] işlemi. Get görev sayıları kaç görevleri bekleyen, çalışan veya tamamlamak ve kaç tane görevlerin başarılı veya başarısız olduğunu gösterir. Görev Get sayar, liste sorgusu daha etkilidir. Daha fazla bilgi için bkz: [saymak durumuna (Önizleme) göre bir iş için görevleri](batch-get-task-counts.md). 
>
> Merhaba görev sayar alma işlemi 2017 06 01.5.1'den önceki toplu işlem hizmeti sürümlerinde kullanılabilir değildir. Merhaba hizmeti daha eski bir sürümü kullanıyorsanız, ardından bir liste sorgu toocount görevleri bir işi kullanın.
>
> 

## <a name="meet-hello-detaillevel"></a>Karşılayan hello DetailLevel
Bir üretim toplu uygulama, işler, görevler ve işlem düğümü gibi varlıkları hello binlerce sayı. Bu kaynaklar hakkında bilgi istediklerinde, potansiyel olarak büyük miktarda veri "Merhaba kablo hello Batch hizmeti tooyour uygulamadan her sorguda geçmelidir". Öğe Hello sayısı ve türü bir sorgu tarafından döndürülen bilgilerin kısıtlayarak, sorgularınızı hello hızını artırmak ve bu nedenle, uygulamanızın performansını hello.

Bu [Batch .NET] [ api_net] API kod parçacığını listeleri *her* ile birlikte bir işlemle ilişkili görev *tüm* her hello özellikleri Görev:

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

Ancak, bir "ayrıntı düzeyi" tooyour sorgu uygulayarak çok daha verimli bir liste sorgusu gerçekleştirebilirsiniz. Sağlayarak bunu bir [ODATADetailLevel] [ odata] toohello nesne [JobOperations.ListTasks] [ net_list_tasks] yöntemi. Bu kod parçacığında, yalnızca hello kimliği, komut satırı ve işlem düğümü bilgi tamamlanan görevler özelliklerini döndürür:

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties tooreturn
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply hello ODATADetailLevel toohello ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

Bu örnek senaryoda hello işteki görevleri binlerce varsa hello ikinci sorgudan hello sonuçlar genellikle olacaktır hello çok hızlı ilk döndürdü. Merhaba Batch .NET API'si öğeleriyle listelediğinizde ODATADetailLevel kullanma hakkında daha fazla bilgi bulunmaktadır [aşağıda](#efficient-querying-in-batch-net).

> [!IMPORTANT]
> Yüksek oranda öneririz, *her zaman* bir ODATADetailLevel nesne tooyour .NET API listesi çağırır tooensure en yüksek verimlilik ve uygulamanızın performansını sağlar. Ayrıntı düzeyi belirterek, hizmet yanıt sürelerini toplu işlem, ağ kullanımı iyileştirirsiniz ve istemci uygulamaları tarafından bellek kullanımını en aza indirmek toolower yardımcı olabilir.
> 
> 

## <a name="filter-select-and-expand"></a>Filtre, seçin ve genişletin
Merhaba [Batch .NET] [ api_net] ve [Batch REST] [ api_rest] API'leri hem bir listede, döndürülen öğe hello sayısı hello özelliği tooreduce sağlayın aynı zamanda her biri için döndürülen bilgi tutarını hello. Belirterek bunu **filtre**, **seçin**, ve **dizeleri genişletin** listesi sorguları gerçekleştirirken.

### <a name="filter"></a>Filtre
Merhaba filtre dizesi hello döndürülen öğe sayısını azaltan bir ifadedir. Çalışan görevlerin bir iş ya da hazır toorun görevler listesi tek işlem düğümleri için örneğin, liste yalnızca hello.

* Merhaba filtre dizesi olan bir veya daha fazla ifade, bir özellik adı, işleç ve değer oluşan bir ifade oluşur. Her bir özellik için desteklenen hello işleçleri olarak belirtilebilecek Merhaba, sorgu, belirli tooeach varlık türü özelliklerdir.
* Merhaba mantıksal işleçler kullanarak birden çok ifadeleri birleştirilebilir `and` ve `or`.
* Bu örnek filtre dizesi listelerini görevleri çalıştıran hello "işleme yalnızca": `(state eq 'running') and startswith(id, 'renderTask')`.

### <a name="select"></a>Şunu seçin:
Merhaba select dize her öğe için döndürülen hello özellik değerlerini sınırlar. Özellik adlarının bir listesini belirtin ve yalnızca bu özellik değerlerini hello sorgu sonuçlarındaki hello öğeleri için döndürülür.

* Merhaba select dize virgülle ayrılmış listesini özellik adlarının oluşur. Merhaba varlık türü, sorgulama için hello özelliklerinden herhangi birini belirtebilirsiniz.
* Bu örnek Seç dize her görev için yalnızca üç özellik değerlerini döndürülmelidir belirtir: `id, state, stateTransitionTime`.

### <a name="expand"></a>Genişlet
Merhaba genişletin dize belirli bilgileri hello gerekli tooobtain olan API çağrıları azaltır. Genişletme dizisi kullandığınızda, her öğe hakkında daha fazla bilgi alınabilir tek bir API çağrısı ile. İlk alma hello listesi varlıklar sonra hello listesindeki her bir öğe için bilgi isteyen yerine, genişletilecek dize kullanın tooobtain hello tek bir API çağrısı aynı bilgileri. Daha az API çağrıları daha iyi performans anlamına gelir.

* Benzer toohello select dize, hello genişletin dize denetimleri belirli veri listesi sorgu sonuçlarında dahil olup olmayacağını.
* Merhaba genişletin dize işleri, iş zamanlamalarını, görevler ve havuzları liste kullanıldığında, yalnızca desteklenir. Şu anda, istatistik bilgileri yalnızca destekler.
* Tüm özellikleri gereklidir ve belirtilen bir select dize, dize genişletin hello *gerekir* kullanılan tooget istatistik bilgileri olabilir. Select dize kullanılan tooobtain özelliklerinin bir alt sonra olup olmadığını `stats` hello select dizesinde belirtilen ve hello genişletin dize belirtilen toobe gerekli değildir.
* Bu örnek genişletin dize istatistik bilgileri hello listesindeki her bir öğe için döndürülmelidir belirtir: `stats`.

> [!NOTE]
> Merhaba hiçbirini oluşturulurken üç sorgu dize türleri (filtre, seçin ve genişletin) hello özellik adları ve çalışması, REST API öğesi dekiler eşleştiğinden emin olun. Örneğin, .NET ile çalışırken hello [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) sınıfı, belirtmelisiniz **durumu** yerine **durumu**, hello .NET özelliği olsa bile [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state). Merhaba .NET ve REST API'lerinin arasında özellik eşlemeleri için aşağıdaki Hello tablolara bakın.
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a>Filtre için kuralları seçin ve dizeleri genişletin
* Filtre, Özellikler adlarında seçin ve dizeleri genişletin hello yaptıkları gibi görünmelidir [Batch REST] [ api_rest] kullandığınızda da API-- [Batch .NET] [ api_net] veya diğer toplu SDK hello biri.
* Tüm özellik adları büyük/küçük harfe duyarlıdır, ancak özellik değerleri büyük küçük harfe duyarlı.
* Tarih/saat dizeleri iki biçimlerden birinde olabilir ve ile gelmelidir `DateTime`.
  
  * W3C DTF biçimi örneği:`creationTime gt DateTime'2011-05-08T08:49:37Z'`
  * RFC 1123 biçimi örneği:`creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`
* Boole dizelerdir ya da `true` veya `false`.
* Bir geçersiz özellik ya da operatör belirtilirse, bir `400 (Bad Request)` hata neden olur.

## <a name="efficient-querying-in-batch-net"></a>Verimli Batch .NET içinde sorgulama
Merhaba içinde [Batch .NET] [ api_net] API, hello [ODATADetailLevel] [ odata] sınıfı, filtre sağlama için kullanılır, seçin ve dizeleri genişletin toolist işlemleri. Merhaba ODataDetailLevel sınıfı hello oluşturucuda belirtilen veya doğrudan hello nesnesinde ayarlanan üç genel dize özellikleri vardır. Ardından hello ODataDetailLevel nesnesi parametresi toohello çeşitli listeleme işlemleri gibi geçirdiğiniz [ListPools][net_list_pools], [ListJobs][net_list_jobs], ve [ListTasks][net_list_tasks].

* [ODATADetailLevel][odata].[ FilterClause][odata_filter]: hello döndürülen öğe sayısını sınırla.
* [ODATADetailLevel][odata].[ SelectClause][odata_select]: hangi özellik değerlerini her bir öğeyle döndürülür belirtin.
* [ODATADetailLevel][odata].[ ExpandClause][odata_expand]: tek bir API tüm öğeleri için verileri almak yerine ayrı çağrıları her öğe için çağırın.

Merhaba aşağıdaki kod parçacığını hello Batch .NET API'si tooefficiently sorgu hello Batch hizmeti havuzları belirli bir dizi hello istatistiklerini için kullanır. Bu senaryoda, test ve Üretim havuzları hello toplu kullanıcı sahiptir. Merhaba test havuzu kimlikleri "ile bir test" öneki ve hello üretim havuzu kimlikleri "ile üretim" öneki. Merhaba parçacığında bulunan *myBatchClient* hello düzgün başlatılmadı örneğidir [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) sınıfı.

```csharp
// First we need an ODATADetailLevel instance on which tooset hello filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want toopull only hello "test" pools, so we limit hello number of items returned
// by using a FilterClause and specifying that hello pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// toofurther limit hello data that crosses hello wire, configure hello SelectClause to
// limit hello properties that are returned on each CloudPool object tooonly
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify hello ExpandClause so that hello .NET API pulls hello statistics for the
// CloudPools in a single underlying REST API call. Note that we use hello pool's
// REST API element name "stats" here as opposed too"Statistics" as it appears in
// hello .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing hello amount of data that is returned
// by specifying hello detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> Örneği [ODATADetailLevel] [ odata] seçin ile yapılandırılmış ve genişletme yan tümceleri de geçirilebilir tooappropriate Get yöntemleri gibi [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx) , toolimit hello döndürülen veri miktarı.
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a>Toplu işlem REST too.NET API eşlemeleri
Filtre, özellik adlarını seçin ve dizeleri genişletin *gerekir* REST API'dekiler, hem adı ve durum yansıtır. Merhaba tablolar aşağıdaki hello .NET ve REST API ortaklarınıza arasındaki eşlemeleri sağlar.

### <a name="mappings-for-filter-strings"></a>Filtre dizeleri eşlemeleri
* **.NET listesi yöntemleri**: Bu sütunda hello .NET API yöntemlerin her biri kabul eden bir [ODATADetailLevel] [ odata] nesnesini parametre olarak.
* **REST listesi istekleri**: her REST API sayfasında izin bu sütunu içeren hello özelliklerini ve işlemlerini belirten bir tablo bağlantılı tooin *filtre* dizeleri. Oluşturmak, bu özellik adları ve işlemleri için kullanacağı bir [ODATADetailLevel.FilterClause] [ odata_filter] dize.

| .NET listesi yöntemleri | REST listesi istekleri |
| --- | --- |
| [CertificateOperations.ListCertificates][net_list_certs] |[Bir hesap hello sertifikalarını listele][rest_list_certs] |
| [CloudTask.ListNodeFiles][net_list_task_files] |[Bir görev ile ilişkili hello dosyaları listeleme][rest_list_task_files] |
| [JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status] |[Merhaba iş hazırlama ve iş sürüm görevleri bir iş için Hello durumu listesi][rest_list_jobprep_status] |
| [JobOperations.ListJobs][net_list_jobs] |[Bir hesap listesi hello işleri][rest_list_jobs] |
| [JobOperations.ListNodeFiles][net_list_nodefiles] |[Bir düğümde hello dosyaları listeleme][rest_list_nodefiles] |
| [JobOperations.ListTasks][net_list_tasks] |[Bir işle ilişkili listesi hello görevleri][rest_list_tasks] |
| [JobScheduleOperations.ListJobSchedules][net_list_job_schedules] |[Bir hesap listesi hello iş zamanlamaları][rest_list_job_schedules] |
| [JobScheduleOperations.ListJobs][net_list_schedule_jobs] |[Bir iş zamanlaması ile ilişkili listesi hello işleri][rest_list_schedule_jobs] |
| [PoolOperations.ListComputeNodes][net_list_compute_nodes] |[Liste hello işlem düğümleri havuzunda][rest_list_compute_nodes] |
| [PoolOperations.ListPools][net_list_pools] |[Bir hesap listesi hello havuzları][rest_list_pools] |

### <a name="mappings-for-select-strings"></a>Select dizeleri eşlemeleri
* **Batch .NET türleri**: Batch .NET API'si türleri.
* **REST API varlıklar**: hello REST API özellik adları hello türünün listesinde bir veya daha fazla tablo bu sütundaki her bir sayfa içerir. Bu özellik adları, yapısı oluştururken kullanılan *seçin* dizeleri. Oluşturmak, bu aynı özellik adları için kullanacağı bir [ODATADetailLevel.SelectClause] [ odata_select] dize.

| Batch .NET türleri | REST API varlıklar |
| --- | --- |
| [Sertifika][net_cert] |[Bir sertifika hakkında bilgi edinin][rest_get_cert] |
| [CloudJob][net_job] |[Bir iş hakkında bilgi edinin][rest_get_job] |
| [CloudJobSchedule][net_schedule] |[Bir iş zamanlaması hakkında bilgi edinin][rest_get_schedule] |
| [ComputeNode][net_node] |[Bir düğüm hakkında bilgi edinin][rest_get_node] |
| [CloudPool][net_pool] |[Bir havuzu hakkında bilgi edinin][rest_get_pool] |
| [CloudTask][net_task] |[Bir görev hakkında bilgi edinin][rest_get_task] |

## <a name="example-construct-a-filter-string"></a>Örnek: bir filtre dizesi oluşturun
Bir filtre dizesi oluşturmak zaman [ODATADetailLevel.FilterClause][odata_filter], karşılık gelen "Eşlemeleri filtre dizeleri için" toofind hello REST API belge sayfasının altında Merhaba tablonun üzerinde başvurun toohello liste işlemi tooperform istiyor. Merhaba ilk tablodaki çok satırlı o sayfadaki hello filtrelenebilir özellikleri ve bunların desteklenen işleçleri bulacaksınız. Çıkış kodu sıfır olmayan tüm görevler tooretrieve isterseniz, örneğin, bu satırın üzerinde [listesinde bir işlemle ilişkili hello görevleri] [ rest_list_tasks] hello geçerli özellik dizesi ve izin verilen işleçleri belirtir:

| Özellik | İzin verilen işlemler | Tür |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

Bu nedenle, sıfır olmayan çıkış kodu ile tüm görevleri listeleme için filtre dizesini hello olacaktır:

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a>Örnek: select dizesi oluşturun
tooconstruct [ODATADetailLevel.SelectClause][odata_select], "Select dizeleri eşlemeleri" altında Merhaba tablonun üzerinde başvurun ve karşılık gelen varlık toohello türü toohello REST API sayfasına gidin, listeliyorsanız. Merhaba ilk tablodaki çok satırlı o sayfadaki hello seçilebilir özellikleri ve bunların desteklenen işleçleri bulacaksınız. Bir listede tooretrieve yalnızca hello kimliği ve her görev için komut satırı isterseniz, örneğin, bu satırı hello geçerli tabloda üzerinde bulacaksınız [bir görev hakkında bilgi alma][rest_get_task]:

| Özellik | Tür | Notlar |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

yalnızca hello kimliği ve listelenen her görev komut satırıyla dahil etmek için hello select dizesi sonra aşağıdaki gibi olmalıdır:

`id, commandLine`

## <a name="code-samples"></a>Kod örnekleri
### <a name="efficient-list-queries-code-sample"></a>Verimli listesi sorguları kod örneği
Merhaba denetleyin [EfficientListQueries] [ efficient_query_sample] GitHub toosee nasıl verimli üzerinde örnek proje listesi sorgulama uygulama performansını etkileyebilir. Bu C# konsol uygulaması oluşturur ve çok sayıda görevleri tooa iş ekler. Sonra birden çok çağrıları toohello yapar [JobOperations.ListTasks] [ net_list_tasks] yöntemi ve geçişleri [ODATADetailLevel] [ odata] nesneleri farklı özellik değerleri toovary hello miktarını döndürülen veri toobe ile yapılandırılmış. Toohello aşağıdaki benzer bir çıktı üretir:

```
Adding 5000 tasks toojob jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER tooquery tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER toocontinue...
```

Merhaba geçen kez gösterildiği gibi hello özellikleri ve hello döndürülen öğe sayısını sınırlayarak sorgusu yanıt sürelerini önemli ölçüde düşürebilirsiniz. Bu ve diğer örnek projelerine hello bulabilirsiniz [azure-batch-samples] [ github_samples] github'daki.

### <a name="batchmetrics-library-and-code-sample"></a>BatchMetrics kitaplığı ve kod örneği
Ayrıca toohello EfficientListQueries kod örneği yukarıdaki, hello bulabileceğiniz [BatchMetrics] [ batch_metrics] hello bir projede [azure-batch-samples] [ github_samples] GitHub depo. Merhaba BatchMetrics örnek proje nasıl tooefficiently izlemek hello Batch API'sini kullanarak Azure Batch iş ilerleme durumunu gösterir.

Merhaba [BatchMetrics] [ batch_metrics] örnek içeren, kendi projeleri ve basit bir komut satırı dahil edebilirsiniz .NET sınıf kitaplığı proje program tooexercise ve hello hello kullanımını gösterir Kitaplığı.

Merhaba örnek uygulaması hello proje içindeki operations aşağıdaki hello gösterir:

1. Özel öznitelikler sipariş toodownload yalnızca hello özelliklerinde seçerek gerekir
2. Durum geçişi kez sipariş toodownload süzme yalnızca bu yana hello son sorgu değiştirir

Örneğin, yöntem aşağıdaki hello hello BatchMetrics kitaplığı görüntülenir. Bu yalnızca hello belirten bir ODATADetailLevel döndürür `id` ve `state` özellikleri sorgulanır hello varlıklar için elde. Ayrıca, belirtir, durumu, belirtilen hello bu yana değişti yalnızca varlıklar `DateTime` parametresi döndürülmesi.

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a>Sonraki adımlar
### <a name="parallel-node-tasks"></a>Paralel düğüm görevleri
[Eşzamanlı düğüm görevleri ile Azure toplu işlem kaynak kullanımını en üst düzeye](batch-parallel-node-tasks.md) başka bir makale ilgili tooBatch uygulama performansı. İş yüklerinin bazı türleri üzerinde Paralel Görevler yürütülürken yararlanabilir büyük--ancak daha az--işlem düğümlerini. Merhaba denetleyin [Örnek senaryo](batch-parallel-node-tasks.md#example-scenario) hello makalede böyle bir senaryo hakkında ayrıntılı bilgi için.

### <a name="batch-forum"></a>Toplu işlem Forumu
Merhaba [Azure toplu işlem Forumu] [ forum] MSDN'de mükemmel toodiscuss toplu yerleştirin ve hello hizmeti hakkında soru sorun olduğunu. HEAD üzerinde üzerinden faydalı "Yapışkan" gönderiler için ve Batch çözümlerinizi derleme sırasında çıktıkları anda sorularınızı gönderin.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job