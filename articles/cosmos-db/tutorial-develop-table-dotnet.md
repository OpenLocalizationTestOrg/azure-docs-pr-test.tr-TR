---
title: "Azure Cosmos DB: Merhaba tablo API .NET geliştirme | Microsoft Docs"
description: "Bilgi nasıl toodevelop .NET kullanarak Azure Cosmos veritabanı tablo API ile"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a>Azure Cosmos DB: hello .NET tablo API ile geliştirme

Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.

Bu öğretici hello aşağıdaki görevleri içerir: 

> [!div class="checklist"] 
> * Azure Cosmos DB hesabı oluşturma 
> * Merhaba app.config dosyasında işlevselliğini etkinleştirmek 
> * Hello kullanarak bir tablo oluşturma [tablo API](table-introduction.md) (Önizleme)
> * Bir varlık tooa tablo ekleme 
> * Toplu işlem varlık yerleştirme 
> * Tek bir varlık alma 
> * Otomatik ikincil dizinler kullanarak sorgu varlıklar 
> * Bir varlığı değiştirme 
> * Bir varlığı silme 
> * Bir tablo silme
 
## <a name="tables-in-azure-cosmos-db"></a>Azure Cosmos DB tablolarında 

Azure Cosmos DB sağlar hello [tablo API](table-introduction.md) (Önizleme) bir anahtar-değer deposu Şeması daha az bir tasarım gereken uygulamalar için. [Azure Table storage](../storage/common/storage-introduction.md) SDK'lar ve REST API'leri Azure Cosmos DB ile kullanılan toowork olabilir. Yüksek verimlilik gereksinimleriyle Azure Cosmos DB toocreate tabloları kullanabilir. Azure Cosmos DB, şu anda genel önizlemede olan, aktarım hızı açısından iyileştirilmiş tabloları (resmi olmayan adı "premium tablolar"dır) destekler. 

Toouse Azure Table storage yüksek depolama ve daha düşük işleme gereksinimlerine sahip tablolar için devam edebilirsiniz. Azure Cosmos DB gelecekteki bir güncelleştirme depolama için iyileştirilmiş tablolar için destek getirir ve var olan ve yeni Azure depolama hesapları sorunsuz olacaktır tablo tooAzure Cosmos DB yükseltilecektir.

Şu anda Azure Table storage kullanıyorsanız, aşağıdaki yararları hello "premium tablo" preview ile Merhaba elde:

- Anahtar teslim [genel dağıtım](distribute-data-globally.md) birden çok giriş ile ve [otomatik ve el ile yük devretme](regional-failover.md)
- Otomatik şema tüm özelliklerini ("ikincil dizinler") ve hızlı sorguları karşı dizin belirsiz desteği 
- Desteği [depolama ve işleme bağımsız ölçeklendirme](partition-data.md), herhangi bir sayıda bölgeler arasında
- Desteği [tablo başına ayrılmış işleme](request-units.md) , ölçeklendirilmiş yüzlerce toomillions saniyedeki istek
- Desteği [beş ince ayarlanabilir tutarlılık düzeyleri](consistency-levels.md) tootrade kapatma kullanılabilirlik, gecikme ve tutarlılık tabanlı uygulama gereksinimlerinize göre
- tek bir bölge ve yeteneği tooadd daha fazla içinde % 99,99 kullanılabilirlik yüksek kullanılabilirlik için bölgeler ve [endüstri lideri kapsamlı SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/) genel kullanılabilirliğine
- Merhaba mevcut Azure depolama .NET SDK'sı ile çalışma ve kod değişiklikleri tooyour uygulama

Merhaba Önizleme sırasında Azure Cosmos DB destekler tablo hello .NET SDK kullanarak API hello. Merhaba indirebilirsiniz [Azure depolama Preview SDK](https://aka.ms/premiumtablenuget) hello olan Nuget'ten, aynı sınıfları ve yöntem imzaları hello olarak [Azure depolama SDK'sı](https://www.nuget.org/packages/WindowsAzure.Storage), ancak hello kullanarak tooAzure Cosmos DB hesaplarına da bağlanabilirsiniz Tablo API.

karmaşık Azure Table depolama görevleri hakkında daha fazla toolearn bakın:

* [Giriş tooAzure Cosmos DB: Tablo API](table-introduction.md)
* Tablo hizmeti başvuru belgelerini kullanılabilir API'ler ile ilgili tam Ayrıntılar için hello [.NET başvurusu için depolama istemci kitaplığı](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

### <a name="about-this-tutorial"></a>Bu öğretici hakkında
Bu öğretici, Azure Cosmos DB hello Azure Table depolama SDK'sı ile bilgi sahibiyseniz ve toouse hello premium özellikleri kullanılabilir istediğiniz geliştiriciler için kullanıyor. Bağlı olduğu [.NET kullanarak Azure Table storage ile çalışmaya başlama](table-storage-how-to-use-dotnet.md) ve nasıl ek yeteneklerinden tootake ikincil dizinler, sağlanan işleme ve gibi birden çok giriş gösterir. Biz nasıl toouse Azure portal toocreate bir Azure Cosmos DB hesap hello oluşturmak ve bir tablo uygulamasını dağıtmak kapsar. Biz de .NET örnekleri oluşturma ve tablo, silme ve ekleme, güncelleştirme, silme ve tablo verileri Sorgulama yol. 

Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve hello kullan **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Etkinleştirdiğinizden emin olun **Azure geliştirme** hello Visual Studio Kurulumu sırasında.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Veritabanı hesabı oluşturma

Hello Azure portalında bir Azure Cosmos DB hesabı oluşturarak başlayalım.  

> [!TIP]
> * Zaten Azure Cosmos DB hesabınız var mı? Bu durumda, İleri çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS).
> * Bir Azure DocumentDB hesabına sahip miydiniz? Bu nedenle, hesabınızı şimdi bir Azure Cosmos DB hesabı ise ve şimdi çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS).  
> * Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) toosetup öykünücüsü hello ve İleri çok atlayabilirsiniz[, Visual Studio çözümünü kurmak](#SetupVS).
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a>Merhaba örnek uygulaması kopyalama

Şimdi şimdi kopyalama tablo uygulama github'dan hello bağlantı dizesini ayarlamak ve çalıştırın.

1. Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.  

2. Çalışma hello aşağıdaki tooclone hello örnek depo komutu. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. Ardından Visual Studio'da hello çözüm dosyasını açın.

## <a name="update-your-connection-string"></a>Bağlantı dizenizi güncelleştirme

Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.

1. Merhaba, [Azure portal](http://portal.azure.com/), Azure Cosmos DB hesap, sol gezinti hello tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**. Merhaba sonraki adımda hello app.config dosyasına hello sağ tarafında Merhaba ekranında toocopy hello bağlantı dizesi hello Kopyala düğmesi kullanacaksınız.

2. Visual Studio'da hello app.config dosyasını açın. 

3. URI değeri (Merhaba Kopyala düğmesini kullanarak) hello Portal'dan kopyalayın ve hale hello app.config hello hesabı-anahtar değeri. App.config hesap adı için daha önce oluşturduğunuz hello hesap adı kullanın.
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> toouse bu uygulama standart Azure tablo depolaması ile toochange hello bağlantı dizesinde gereken `app.config file`. Merhaba hesap adı, Azure depolama birincil anahtarı olarak tablo hesap adı ve anahtar kullanın. <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a>Derleme ve hello uygulama dağıtma
1. Visual Studio'da hello projeye sağ tıklayın **Çözüm Gezgini** ve ardından **NuGet paketlerini Yönet**. 

2. Merhaba NuGet içinde **Gözat** kutusuna ***WindowsAzure.Storage PremiumTable***. Denetleme **yayın öncesi sürümler dahil**.

3. Merhaba sonuçlarından hello yüklemek **WindowsAzure.Storage PremiumTable** ve hello Önizleme derlemesinin seçin `0.0.1-preview`. Bu eylemin hello Azure Table depolama paketi ve tüm bağımlılıkları yükler.

4. CTRL + F5'e tıklayın toorun Merhaba uygulaması. 

Şimdi tooData Explorer geri dönün ve sorgu görmek değiştirmek ve bu tablo verilerle çalışmak. 

> [!NOTE]
> toouse bu uygulama ile bir Azure Cosmos DB öykünücü, yalnızca size gereken toochange hello bağlantı dizesinde `app.config file`. Değerin altında Hello öykünücüsü kullanın. <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a>Azure Cosmos DB özellikleri
Azure Cosmos DB hello Azure Table storage API'si kullanılamaz özelliklerini destekler. Merhaba yeni işlevsellik hello aşağıdaki aracılığıyla etkinleştirilebilir `appSettings` yapılandırma değerlerini. Biz herhangi yeni imzalar veya aşırı toohello Önizleme Azure depolama SDK'sını tanıtmak değil. Bu, tooconnect tooboth standart ve premium tablolar ve Bloblar ve kuyruklarda olduğu gibi diğer Azure Storage Hizmetleri ile iş sağlar. 


| Anahtar | Açıklama |
| --- | --- |
| TableConnectionMode  | Azure Cosmos DB iki bağlantı modunu destekler. İçinde `Gateway` modu, istekleri her zaman yapılan toohello karşılık gelen veri bölümlerini iletir toohello Azure Cosmos DB gateway. İçinde `Direct` bağlantı modunu hello istemci tabloları toopartitions hello eşlenmesini getirir ve istekleri doğrudan veri bölümlerini karşı yapılır. Öneririz `Direct`, hello varsayılan.  |
| TableConnectionProtocol | Azure Cosmos DB destekleyen iki bağlantı protokol - `Https` ve `Tcp`. `Tcp`Merhaba varsayılandır ve daha basit olduğu için önerilir. |
| TablePreferredLocations | Tercih edilen (çok girişli) konumları okuma için virgülle ayrılmış listesi. Her Azure Cosmos DB hesabı 1 ile ilişkili olabilir-30 + bölgeleri. Her istemci örneği, düşük gecikme süresi okumalar için tercih edilen hello sırayla Bu bölgeler kümesini belirtebilirsiniz. Merhaba bölgeler gerekir adlı kullanarak kendi [görünen adları](https://msdn.microsoft.com/library/azure/gg441293.aspx), örneğin, `West US`. Ayrıca bkz. [birden çok giriş API'leri](tutorial-global-distribution-table.md).
| TableConsistencyLevel | Devre dışı gecikme, tutarlılık ve kullanılabilirlik arasında beş iyi tanımlanmış tutarlılık düzeyleri arasında seçerek ticari: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, ve `Eventual`. Varsayılan değer `Session`. Tutarlılık düzeyi Hello seçimine önemli performans farkı bölgeli kurulumlarında yapar. Bkz: [tutarlılık düzeylerini](consistency-levels.md) Ayrıntılar için. |
| TableThroughput | Saniye başına istek birimleri (RU) cinsinden hello tablo için ayrılmış işleme. Tek tablolar 100s-RU/s milyonlarca destekleyebilir. Bkz: [istek birimleri](request-units.md). Varsayılan değer`400` |
| TableIndexingPolicy | Tutarlı ve otomatik ikincil tablo içindeki tüm sütunların dizin oluşturma | JSON İlkesi belirtimi dizin uyumlu toohello dize. Bkz: [dizin oluşturma ilkesi](indexing-policies.md) toosee dizin oluşturma ilkesi tooinclude/çıkarma belirli sütunlardaki nasıl değiştirebilirsiniz. | Tüm özellikleri (dizeler için karma) ve numaraları aralığını otomatik dizin oluşturma |
| TableQueryMaxItemCount | Merhaba maksimum tek gidiş dönüş tablosu sorgu başına döndürülen öğe sayısını yapılandırın. Varsayılan değer `-1`, Azure Cosmos hello değer çalışma zamanında dinamik olarak belirleyen DB olanak sağlar. |
| TableQueryEnableScan | Merhaba sorgu hello dizin için herhangi bir filtre kullanamıyorsanız, ardından çalıştırın yine de bir tarama. Varsayılan değer `false`.|
| TableQueryMaxDegreeOfParallelism | Çapraz bölüm sorgusu yürütme için paralellik derecesi Hello. `0`hiçbir önceden getirme ile seri olduğu `1` önceden getirme ile seri ve daha yüksek değerlerini tutan paralellik artış hello oranı. Varsayılan değer `-1`, Azure Cosmos hello değer çalışma zamanında dinamik olarak belirleyen DB olanak sağlar. |

toochange hello varsayılan değer, açık hello `app.config` Visual Studio'daki Çözüm Gezgini'nden dosya. Merhaba Merhaba içeriğine Ekle `<appSettings>` aşağıda gösterilen öğesi. Değiştir `account-name` depolama hesabınızın hello adla ve `account-key` hesap erişim anahtarı ile. 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım. Açık hello `Program.cs` dosyanız varsa ve bulma Bu kod satırları hello tablo kaynakları oluşturun. 

## <a name="create-hello-table-client"></a>Merhaba tablo istemcisi oluşturma
Başlatır bir `CloudTableClient` tooconnect toohello tablo hesabı.

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
Bu istemci hello kullanarak başlatılır `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, ve `TablePreferredLocations` hello uygulama ayarlarında belirtilen yapılandırma değerleri.
    
## <a name="create-a-table"></a>Bir tablo oluşturma
Ardından, kullanarak bir tablo oluşturun `CloudTable`. Azure Cosmos DB tablolarında depolama ve işleme açısından bağımsız olarak ölçeklendirebilirsiniz ve bölümleme hello hizmeti tarafından otomatik olarak gerçekleştirilir. Azure Cosmos DB sabit boyutlu ve sınırsız tabloları destekler. Bkz: [Azure Cosmos DB'de bölümleme](partition-data.md) Ayrıntılar için. 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

Tabloları nasıl oluşturulduğunu, önemli bir fark yoktur. Azure Cosmos DB işlemleri için Azure storage'nın tüketim tabanlı modeli farklı verimlilik ayırır. Merhaba ayırma modeli iki önemli faydası vardır:

* Üretilen iş ayrılmış /, istek hızı düzeyinde veya altında sağlanan işleme ise, hiçbir zaman kısıtlanan için ayrılmıştır
* Merhaba ayırma modeli daha fazla [verimlilik yoğun iş yükleri için düşük maliyetli](key-value-store-cost.md)

Merhaba ayarını yapılandırarak hello varsayılan işleme yapılandırabilirsiniz `TableThroughput` RU (istek birimleri) / saniye cinsinden. 

Bir 1 KB varlığı okuma 1 olarak normalleştirilmiş RU ve diğer işlemlerin, CPU, bellek ve IOPS tüketime dayanarak RU değeri sabit normalleştirilmiş tooa olan. Daha fazla bilgi edinmek [istek birimleri Azure Cosmos veritabanı](request-units.md).

> [!NOTE]
> Tablo depolama SDK'sı şu anda değiştirme verimlilik desteklemez, ancak hello verimlilik eşzamanlı olarak hello Azure portalında veya Azure CLI kullanarak dilediğiniz zaman değiştirebilirsiniz.

Ardından, biz hello basit okuyun, yol ve hello Azure Table depolama SDK'sını kullanarak (CRUD) işlemleridir yazma. Bu öğretici, tahmin edilebilir düşük tek basamaklı milisaniyelik gecikme ve Azure Cosmos DB tarafından sağlanan hızlı sorguları gösterir.

## <a name="add-an-entity-tooa-table"></a>Bir varlık tooa tablo ekleme
Azure Table depolama varlıklarda genişletmek hello `TableEntity` sınıfı ve olmalıdır `PartitionKey` ve `RowKey` özellikleri. Bir müşteri varlığı için örnek tanımı aşağıda verilmiştir.

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

Aşağıdaki kod parçacığında hello nasıl tooinsert varlıkla bir hello Azure depolama SDK'sı gösterir. Azure Cosmos DB herhangi ölçekli, düşük gecikme süresi Merhaba dünya genelindeki garanti için tasarlanmıştır.

Yazma tamamlamak < 15 ms p99 ve çalışan uygulamalar için p50 adresindeki ~ 6 ms hello hello Azure Cosmos DB hesabı ile aynı bölgeye. Ve bu süre Yazar hello bulgusunun hesapları geri toohello istemci yalnızca bunlar zaman uyumlu olarak, bir işlemi tamamlandıktan sonra çoğaltılır ve tüm içeriğini dizine sonra onaylanan.

Hello Azure Cosmos DB için tablo API önizlemede değil. Genel kullanılabilirliğine hello p99 gecikme garanti SLA'lar gibi diğer Azure Cosmos DB API'leri tarafından desteklenir. 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>Toplu işlem varlık yerleştirme
Azure tablo depolama destekler olanak sağlayan bir toplu işlem API güncelleştirmeleri, siler, birleştirme ve ekleme aynı tek toplu işlem hello. Azure Cosmos DB hello sınırlamaları bazıları hello toplu işlem API Azure Table storage yok. Örneğin, bir toplu iş içinde birden çok okuma yapabilirsiniz, birden çok yazma toohello gerçekleştirebileceğiniz bir yığın içindeki aynı varlık ve toplu iş başına 100 işlemlerini sınırı yoktur. 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a>Tek bir varlık alma
Tam Azure Cosmos DB'de (alır) alır < 10 ms p99 ve ~ 1 ms içinde p50 adresindeki hello aynı Azure bölgesi. Düşük gecikme süresi okumalar sayıda bölgeleri tooyour hesabını ekleyin ve kendi yerel bölgesinden ("çok konaklı") uygulamaları tooread ayarlayarak dağıtmak `TablePreferredLocations`. 

Aşağıdaki kod parçacığında hello kullanarak tek bir varlık alabilirsiniz:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> Çok girişli API'leri hakkında bilgi edinin [birden çok bölgeye ile geliştirme](tutorial-global-distribution-table.md)
>

## <a name="query-entities-using-automatic-secondary-indexes"></a>Otomatik ikincil dizinler kullanarak sorgu varlıklar
Tablolar sorgulanan hello kullanarak `TableQuery` sınıfı. Azure Cosmos DB tablonuz içindeki tüm sütunlar otomatik olarak dizinler bir yazma iyileştirilmiş veritabanı altyapısı vardır. Azure Cosmos DB'de dizin belirsiz tooschema olur. Bu nedenle, şemanızı satırlar arasında farklı olsa bile veya hello şema zamanla dönüşmesi varsa, otomatik olarak dizine alınır. Azure Cosmos DB otomatik ikincil dizinler desteklediğinden, herhangi bir özellik sorguları hello dizini kullanabilir ve verimli bir şekilde sunulması.

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

Önizleme'de, Azure Cosmos DB hello destekler aynı sorgu Azure Table storage'hello tablo API için işlevselliği. Azure Cosmos DB, sıralama, toplamalar, Jeo-uzamsal sorgu, hiyerarşi ve çok çeşitli yerleşik işlevler de destekler. Merhaba ek işlevsellik gelecekteki hizmet güncelleştirmesi hello tablo API sağlanacaktır. Bkz: [Azure Cosmos DB sorgusu](documentdb-sql-query.md) bu özelliklere genel bakış. 

## <a name="replace-an-entity"></a>Bir varlığı değiştirme
bir varlık tooupdate hello tablo hizmetinden alın, hello varlık nesnesini değiştirin ve ardından hello Değişiklikleri Kaydet toohello tablo hizmeti yeniden. Merhaba aşağıdaki kod mevcut bir müşterinin telefon numarasını değiştirir. 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
Benzer şekilde, gerçekleştirebileceğiniz `InsertOrMerge` veya `Merge` işlemleri.  

## <a name="delete-an-entity"></a>Bir varlığı silme
Hello kullanarak aldıktan sonra bir varlık kolayca silebilirsiniz bir varlığı güncelleştirmek için gösterilen aynı düzeni. koddan hello alır ve bir müşteri varlığı siler.

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a>Bir tablo silme
Son olarak, aşağıdaki kod örneğine hello bir depolama hesabından bir tablo siler. Silin ve hemen Azure Cosmos DB içeren bir tablo oluşturun.

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a>Kaynakları temizleme 

Bu uygulama toocontinue toouse denetlemeyecekseniz tüm kaynaklar Bu öğreticide hello Azure portal tarafından oluşturulan adımları toodelete aşağıdaki hello kullanın.   

1. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.  
2. Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**. 

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide tooget hello tablo API ile Azure Cosmos DB kullanarak çalışmaya nasıl ele ve hello aşağıdakileri yaptığınızdan: 

> [!div class="checklist"] 
> * Bir Azure Cosmos DB hesabı oluşturuldu 
> * Merhaba app.config dosyasında etkin işlevi 
> * Bir tablo oluşturuldu 
> * Bir varlık tooa tablo eklendi 
> * Toplu işlem varlık eklenen 
> * Tek bir varlık alınan 
> * Otomatik ikincil dizinler kullanılarak sorgulanan varlıklar 
> * Bir varlık değiştirildi 
> * Bir varlık silindi 
> * Bir tablo silindi  

Şimdi toohello sonraki öğretici devam ve tablo verileri sorgulama hakkında daha fazla bilgi edinin. 

> [!div class="nextstepaction"]
> [Tablo API Hello ile sorgulama](tutorial-query-table.md)
