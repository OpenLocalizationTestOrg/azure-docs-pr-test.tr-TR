---
title: "aaaTutorial - Node.js için kullanım hello Azure Batch istemci kitaplığı | Microsoft Docs"
description: "Azure Batch temel kavramlarını Hello öğrenin ve Node.js kullanarak basit bir çözüm oluşturun."
services: batch
author: shwetams
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: nodejs
ms.topic: hero-article
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: shwetams
ms.openlocfilehash: d2b0ecbe764e7100affd7b02839aef3077b073cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a>Node.js için Batch SDK'sını kullanmaya başlama

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Node.js kullanarak Batch istemci oluşturmanın hello temellerini öğrenin [Azure Batch Node.js SDK'sı](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/). Batch uygulaması için bir senaryoyu anlayıp ardından bir Node.js istemcisi kullanarak bu senaryoyu ayarlama adımlarından oluşan bir yaklaşım uyguluyoruz.  

## <a name="prerequisites"></a>Ön koşullar
Bu makalede, Node.js hakkında bilgi sahibi olduğunuz ve Linux kullanmaya alışkın olduğunuz varsayılmaktadır. Ayrıca, erişim hakları toocreate toplu işlem ve depolama hizmetleri ile bir Azure hesabı kurulumu sahip olduğunuzu varsayar.

Okuma öneririz [Azure Batch teknik genel bakış](batch-technical-overview.md) geçmeden önce hello adımları bu makalede açıklanan.

## <a name="hello-tutorial-scenario"></a>Merhaba öğretici senaryo
Bize hello toplu iş akışı senaryo anlayın. Tüm csv tooJSON dönüştürür ve bir Azure Blob Depolama kapsayıcıdan dosyaları indirir Python içinde yazılmış basit bir komut dosyası sunuyoruz. tooprocess birden çok depolama hesabı paralel kapsayıcılar, biz hello betik bir Azure toplu iş olarak dağıtabilirsiniz.

## <a name="azure-batch-architecture"></a>Azure Batch Mimarisi
Merhaba Aşağıdaki diyagramda nasıl biz Azure Batch ve Node.js istemci kullanılarak hello Python komut ölçeklendirebilirsiniz gösterilmektedir.

![Azure Batch Senaryosu](./media/batch-nodejs-get-started/BatchScenario.png)

Merhaba node.js istemci toplu iş hazırlama göreve (daha sonra ayrıntılı olarak açıklanmıştır) ve bir dizi görevi hello depolama hesabı kapsayıcı hello sayısı bağlı olarak dağıtır. Merhaba github'da depodan hello betikleri indirebilirsiniz.

* [Node.js istemcisi](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [Hazırlık görevi kabuk betikleri](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [Python csv tooJSON işlemci](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> Merhaba Node.js istemci belirtilen hello bağlantısında bir Azure işlevi uygulama olarak dağıtılan belirli bir kod toobe içermiyor. Bağlantıları yönergeleri toocreate biri için aşağıdaki toohello başvurabilir.
> - [İşlev uygulaması oluşturma](../azure-functions/functions-create-first-azure-function.md)
> - [Zamanlayıcı tetikleyicisi işlevi oluşturma](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a>Merhaba uygulaması oluşturma

Şimdi, bize hello işlemi adım adım hello Node.js istemci oluşturmakla izleyin:

### <a name="step-1-install-azure-batch-sdk"></a>1. Adım: Azure Batch SDK’sını yükleme

Merhaba npm yükleme komutunu kullanarak Node.js için Azure Batch SDK'sı yükleyebilirsiniz.

`npm install azure-batch`

Bu komut hello azure toplu işlem düğüm SDK en son sürümünü yükler.

>[!Tip]
> Bir Azure işlevi uygulamada gittiğiniz çok "Kudu konsolunda" Merhaba Azure işlevi ait ayarları sekmesinde toorun hello npm yükleme komutlarını. Bu örneği tooinstall Node.js için Azure Batch SDK.
>
>

### <a name="step-2-create-an-azure-batch-account"></a>2. Adım: Azure Batch hesabı oluşturma

Hello oluşturma [Azure portal](batch-account-create-portal.md) veya komut satırından ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure CLI](https://docs.microsoft.com/cli/azure/overview)).

Merhaba komutları toocreate bir Azure CLI aracılığıyla aşağıda verilmiştir.

Bir kaynak grubu oluşturmak, bir toplu işlem hesabı toocreate hello istediğiniz zaten varsa bu adımı atlayın:

`az group create -n "<resource-group-name>" -l "<location>"`

Ardından bir Azure Batch hesabı oluşturun.

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

Her Batch hesabının ilgili erişim anahtarları vardır. Bu anahtarları gerekli toocreate başka Azure batch hesabında kaynaklardır. Üretim ortamı için iyi bir uygulama bu anahtarları toouse Azure anahtar kasası toostore değil. Bir hizmet asıl hello uygulama için daha sonra oluşturabilirsiniz. Bu hizmet asıl hello uygulamasını kullanarak bir OAuth belirteç tooaccess anahtarları hello anahtar Kasası'nı oluşturabilirsiniz.

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

Kopyalayın ve hello anahtar toobe hello sonraki adımlarda kullanılan saklayın.

### <a name="step-3-create-an-azure-batch-service-client"></a>3. Adım: Azure Batch hizmet istemcisi oluşturma
Aşağıdaki kod parçacığını ilk hello azure-batch Node.js modülü içe aktarır ve ardından bir Batch hizmeti istemci oluşturur. Toofirst ihtiyacınız hello önceki adımda kopyaladığınız hello Batch hesabınızın anahtarıyla SharedKeyCredentials nesnesi oluşturun.

```nodejs
// Initializing Azure Batch variables

var batch = require('azure-batch');

var accountName = '<azure-batch-account-name>';

var accountKey = '<account-key-downloaded>';

var accountUrl = '<account-url>'

// Create Batch credentials object using account name and account key

var credentials = new batch.SharedKeyCredentials(accountName,accountKey);

// Create Batch service client

var batch_client = new batch.ServiceClient(credentials,accountUrl);

```

Hello Azure Batch URI'hello Azure portal hello genel bakış sekmesinde bulunabilir. Merhaba biçimi şöyledir:

`https://accountname.location.batch.azure.com`

Toohello ekran bakın:

![Azure batch uri](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a>4. Adım: Azure Batch havuzu oluşturma
Bir Azure Batch havuzu birden çok VM’den (Batch Düğümleri olarak da bilinir) oluşur. Azure Batch hizmeti hello görevler bu düğümler üzerinde dağıtır ve bunları yönetir. Havuzunuz için yapılandırma parametreleri aşağıdaki hello tanımlayabilirsiniz.

* Sanal Makine Türü görüntüsü
* Sanal Makine düğümlerinin boyutu
* Sanal Makine düğümlerinin sayısı

> [!Tip]
> Merhaba boyutu ve sanal makine düğüm sayısını büyük ölçüde toorun içinde paralel ve ayrıca hello görev kendisini istediğiniz görevlerin hello sayısına bağlıdır. Toodetermine hello ideal sayısını ve boyutunu sınama öneririz.
>
>

Merhaba aşağıdaki kod parçacığını hello yapılandırma parametresi nesneleri oluşturur.

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating hello VM configuration object with hello SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting hello VM size tooStandard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in hello pool too4
var numVMs = 4
```

> [!Tip]
> Linux VM görüntüleri Azure Batch ve SKU kimlikleri için kullanılabilir Hello listesi için bkz [sanal makine görüntülerini listesi](batch-linux-nodes.md#list-of-virtual-machine-images).
>
>

Merhaba havuzu yapılandırması tanımlandığında hello Azure Batch havuzu oluşturabilirsiniz. Merhaba Batch havuzu komutu Azure sanal makine düğümleri oluşturur ve toobe hazır tooreceive görevleri tooexecute hazırlayabilirsiniz. Her havuz, sonraki adımlarda başvuru için benzersiz bir kimliğe sahip olmalıdır.

Aşağıdaki kod parçacığını hello bir Azure Batch havuzu oluşturur.

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

Oluşturulan hello havuzu hello durumunu denetleyin ve bir iş toothat havuzu teslimini ile devam geçmeden önce hello durumu "etkin" olduğundan emin olun.

```nodejs
var cloudPool = batch_client.pool.get(poolid,function(error,result,request,response){
        if(error == null)
        {

            if(result.state == "active")
            {
                console.log("Pool is active");
            }
        }
        else
        {
            if(error.statusCode==404)
            {
                console.log("Pool not found yet returned 404...");    

            }
            else
            {
                console.log("Error occurred while retrieving pool data");
            }
        }
        });
```

Merhaba pool.get işlevi tarafından döndürülen örnek bir sonuç nesnesi aşağıdadır.

```
{ id: 'processcsv_201721152',
  displayName: 'processcsv_201721152',
  url: 'https://<batch-account-name>.centralus.batch.azure.com/pools/processcsv_201721152',
  eTag: '<eTag>',
  lastModified: 2017-03-27T10:28:02.398Z,
  creationTime: 2017-03-27T10:28:02.398Z,
  state: 'active',
  stateTransitionTime: 2017-03-27T10:28:02.398Z,
  allocationState: 'resizing',
  allocationStateTransitionTime: 2017-03-27T10:28:02.398Z,
  vmSize: 'standard_a1',
  virtualMachineConfiguration:
   { imageReference:
      { publisher: 'Canonical',
        offer: 'UbuntuServer',
        sku: '14.04.2-LTS',
        version: 'latest' },
     nodeAgentSKUId: 'batch.node.ubuntu 14.04' },
  resizeTimeout:
   { [Number: 900000]
     _milliseconds: 900000,
     _days: 0,
     _months: 0,
     _data:
      { milliseconds: 0,
        seconds: 0,
        minutes: 15,
        hours: 0,
        days: 0,
        months: 0,
        years: 0 },
     _locale:
      Locale {
        _calendar: [Object],
        _longDateFormat: [Object],
        _invalidDate: 'Invalid date',
        ordinal: [Function: ordinal],
        _ordinalParse: /\d{1,2}(th|st|nd|rd)/,
        _relativeTime: [Object],
        _months: [Object],
        _monthsShort: [Object],
        _week: [Object],
        _weekdays: [Object],
        _weekdaysMin: [Object],
        _weekdaysShort: [Object],
        _meridiemParse: /[ap]\.?m?\.?/i,
        _abbr: 'en',
        _config: [Object],
        _ordinalParseLenient: /\d{1,2}(th|st|nd|rd)|\d{1,2}/ } },
  currentDedicated: 0,
  targetDedicated: 4,
  enableAutoScale: false,
  enableInterNodeCommunication: false,
  maxTasksPerNode: 1,
  taskSchedulingPolicy: { nodeFillType: 'Spread' } }
```


### <a name="step-4-submit-an-azure-batch-job"></a>4. Adım: Azure Batch işi gönderme
Azure Batch işi, benzer görevlerden oluşan bir mantıksal gruptur. Senaryomuzda olmasından "İşlem csv tooJSON." Burada her görev her Azure Depolama kapsayıcısında bulunan csv dosyalarını işliyor olabilir.

Bu görevleri paralel olarak çalışır ve hello Azure Batch hizmeti tarafından düzenlenmiş birden çok düğüm arasında dağıtılır.

> [!Tip]
> Merhaba kullanabilirsiniz [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) özelliği toospecify en fazla sayıda eşzamanlı olarak tek bir düğümde çalışan görev.
>
>

#### <a name="preparation-task"></a>Hazırlık görevi

oluşturulan hello VM düğümleri boş Ubuntu düğümler var. Genellikle, önkoşul olarak tooinstall programlar kümesi gerekir.
Genellikle, Linux düğümleri için çalışan hello gerçek görevler önce hello Önkoşullar yükleyen bir kabuk betiği olabilir. Ancak bu, programlanabilir herhangi bir yürütülebilir dosya da olabilir.
Merhaba [Kabuk komut dosyası](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) Bu örnekte, Python için Python PIP ve hello Azure depolama SDK'sını yükler.

Azure Storage hesabını hello komut dosyasını karşıya yükleyin ve bir SAS URI'sini tooaccess hello komut dosyası oluştur. Bu işlem ayrıca hello Azure depolama Node.js SDK'sını kullanarak otomatik olarak yapılabilir.

> [!Tip]
> Bir iş hazırlama görevi burada hello belirli görev toorun gereken yalnızca hello VM düğümler üzerinde çalışır. Üzerinde çalışan hello görevler bağımsız olarak tüm düğümlerde yüklü Önkoşullar toobe istiyorsanız hello kullanabilirsiniz [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) sırasında bir havuzu ekleme özelliği. Başvuru için hazırlık görevi tanımı aşağıdaki hello kullanabilirsiniz.
>
>

Hazırlık görevi Azure toplu işlem hello gönderme sırasında belirtilir. Aşağıdaki hazırlık görevi yapılandırma parametreleri hello:

* **Kimliği**: hello hazırlık görev için benzersiz bir tanımlayıcı
* **komut satırı**: komut satırı tooexecute hello görev çalıştırılabilir
* **resourceFiles**: dosyaları ayrıntılarını sağlayın nesneler dizisi gerektiği için bu görev toorun indirilen toobe.  Seçenekleri aşağıda verilmiştir.
    - blobSource: hello dosya SAS URI'sini hello
    - filePath: yerel yol toodownload ve hello dosyasını kaydedin
    - fileMode: Yalnızca Linux düğümlerinde kullanılan fileMode, sekizli biçimdedir ve varsayılan değeri 0770’tir.
* **waitForSuccess**: kümesi tootrue, hello görev hazırlık görevi hatalarında çalışmazsa
* **runElevated**: yükseltilmiş ayrıcalıklar gerekli toorun hello görev varsa tootrue ayarlayın.

Aşağıdaki kod parçacığını hello hazırlık görev komut dosyası yapılandırma örneği gösterilir:

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

Varsa, görevleri toorun için yüklü hiçbir Önkoşullar toobe hello hazırlama görevleri atlayabilirsiniz. Aşağıdaki kod görünen adı "process csv files" olan bir iş oluşturur.

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job toohello pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a>5. Adım: Bir iş için Azure Batch görevlerini gönderme

İşlem csv işimiz oluşturulduğuna göre bu iş için görevleri oluşturabiliriz. Dört kapsayıcıları sahibiz varsayıldığında, biz toocreate dört görevleri, her kapsayıcı için bir tane vardır.

Şu hello bakarsanız [Python betiği](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), iki parametre kabul eder:

* kapsayıcı adı: depolama kapsayıcısı toodownload dosyalarından hello
* desen: Dosya adı için isteğe bağlı bir desen parametresi

Biz dört kapsayıcıları "con1", "con2", "con3" varsayarak, "con4" aşağıdaki "daha önce oluşturduğumuz görevleri toohello Azure toplu iş işlem için csv" gönderme gösterir kod.

```nodejs
// storing container names in an array
var container_list = ["con1","con2","con3","con4"]
    container_list.forEach(function(val,index){           

           var container_name = val;
           var taskID = container_name + "_process";
           var task_config = {id:taskID,displayName:'process csv in ' + container_name,commandLine:'python processcsv.py --container ' + container_name,resourceFiles:[{'blobSource':'<blob SAS URI>','filePath':'processcsv.py'}]}
           var task = batch_client.task.add(poolid,task_config,function(error,result){
                if(error != null)
                {
                    console.log(error.response);     
                }
                else
                {
                    console.log("Task for container : " + container_name + "submitted successfully");
                }



           });

    });
```

Merhaba kod birden çok görevleri toohello havuzu ekler. Ve her bir hello görev oluşturulan VM'ler hello havuzu düğümünde çalıştırılır. Hello sayıda görev havuzu veya hello maxTasksPerNode özelliğinde hello VM'lerin sayısını aşarsa, bir düğüm kullanılabilir duruma getirilene kadar hello görevleri bekleyin. Bu düzenleme Azure Batch tarafından otomatik olarak gerçekleştirilir.

Merhaba portal hello görevleri ve iş durumlar görünümleri açıklanmıştır. Merhaba listesini kullanın ve işlevleri hello Azure düğümü SDK'sını alın. Ayrıntılar hello belgelerde sağlanan [bağlantı](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).

## <a name="next-steps"></a>Sonraki adımlar

- Gözden geçirme hello [genel bakış Azure Batch özelliklerine](batch-api-basics.md) yeni toohello hizmeti olup olmadığınızı öneririz makalesi.
- Merhaba bkz [toplu Node.js başvuru](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello toplu API.

