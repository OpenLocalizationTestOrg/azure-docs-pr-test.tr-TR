---
title: "Veri Fabrikası ve toplu işlemi kullanarak aaaProcess büyük ölçekli veri kümeleri | Microsoft Docs"
description: "Azure Batch paralel işleme yeteneğini kullanarak tooprocess büyük miktarlarda verinin bir Azure Data factory'de nasıl kanal açıklar."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a>Data Factory ve Batch kullanarak büyük ölçekli veri kümelerini işleme
Bu makalede bir taşır ve büyük ölçekli veri kümeleri otomatik ve zamanlanmış bir şekilde işleyen örnek bir çözüm mimarisini açıklar. Ayrıca, Azure Data Factory ve Azure Batch kullanarak bir uçtan uca kılavuz tooimplement hello çözümü sağlar.

Bu makalede bizim tipik makale uzun çünkü tüm örnek çözümünü bir kılavuz içerir. Bu hizmetler hakkında bilgi edinebilirsiniz yeni tooBatch ve Data Factory varsa ve nasıl birlikte çalışır. Bir şey hello hizmetleri hakkında bilmeniz ve tasarlama/çözüm mimarisi oluşturma, yalnızca hello üzerinde odaklanmak [mimarisi bölümüne](#architecture-of-sample-solution) hello makale ve prototip ya da bir çözüm geliştirme varsa, da tootry isteyebilirsiniz Merhaba içindeki adım adım yönergeleri [izlenecek](#implementation-of-sample-solution). Bu içerik ve bunu nasıl kullandığı hakkında yorumlarınızı davet ediyoruz.

İlk olarak, nasıl veri fabrikası ve toplu işlem Hizmetleri ile Merhaba bulut büyük veri kümelerinde işleme yardımcı olabilir bakalım.     

## <a name="why-azure-batch"></a>Neden Azure toplu işlem?
Azure Batch toorun büyük ölçekli paralel ve yüksek performanslı) bilgi işlem (HPC uygulamaları hello bulutta verimli bir şekilde etkinleştirir. Sanal makineler yönetilen koleksiyonu üzerinde işlem yoğunluklu iş toorun zamanlar bir platform hizmetidir ve ölçek kaynakları toomeet hello işleriniz ihtiyaçlarını işlem otomatik olarak.

Merhaba Batch hizmeti, Azure işlem kaynakları tooexecute uygulamalarınızı paralel olarak ve ölçekte tanımlarsınız. İsteğe bağlı veya zamanlanmış çalıştırabilirsiniz işler ve toomanually gerekmez oluşturmak, yapılandırmak ve HPC Kümesi, tek tek sanal makineleri, sanal ağlar veya karmaşık iş yönetmek ve görev zamanlama altyapısını.

Bu makalede açıklanan hello çözümünü hello mimarisi/uygulaması anlamaya yardımcı olması gibi Azure Batch ile bilmiyorsanız makaleleri aşağıdaki hello bakın.   

* [Azure Batch temel bilgileri](../batch/batch-technical-overview.md)
* [Batch özelliklerine genel bakış](../batch/batch-api-basics.md)

(isteğe bağlı) toolearn Azure Batch hakkında daha fazla bilgi görmek hello [için Azure Batch öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/batch/).

## <a name="why-azure-data-factory"></a>Neden Azure Data Factory?
Veri Fabrikası düzenler ve hello taşınmasını ve dönüştürülmesini veri otomatikleştiren bir bulut tabanlı veri tümleştirme hizmetidir. Merhaba Data Factory hizmeti kullanıldığında, şirket içi veri taşıma ve bulut veri depoları tooa merkezi veri deposu yönetilen veri ardışık oluşturabilirsiniz (örneğin: Azure Blob Storage) ve işlem/dönüştürme Azure Hdınsight ve Azure gibi hizmetleri kullanarak verileri Machine Learning. Veri ardışık düzen toorun zamanlanmış şekilde (saatlik, günlük, haftalık, vb.) ve İzleyicisi'nde zamanlayabilir ve bir bakışta tooidentify sorunu yönetmek ve eylemi gerçekleştirin.

Bu makalede açıklanan hello çözümünü hello mimarisi/uygulaması anlamaya yardımcı olması gibi Azure Data Factory ile bilmiyorsanız makaleleri aşağıdaki hello bakın.  

* [Azure Data Factory giriş](data-factory-introduction.md)
* [İlk veri hattınızı oluşturma](data-factory-build-your-first-pipeline.md)   

(isteğe bağlı) toolearn Azure Data Factory hakkında daha fazla bilgi görmek hello [Azure Data Factory öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/data-factory/).

## <a name="data-factory-and-batch-together"></a>Veri Fabrikası ve birlikte toplu işlem
Veri Fabrikası tooa hedef veri deposuna ve Hive etkinliği tooprocess verilerini Azure üzerinde Hadoop kümeleri (Hdınsight) kullanarak kopyalama etkinliği toocopy/taşıma veri kaynağına veri depolamak gibi yerleşik etkinlikler içerir. Bkz: [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) desteklenen dönüştürme etkinliklerinin listesi.

Ayrıca, toocreate özel .NET etkinliklerini kendi mantığınızı toomove ya da işlem verilerle sağlar ve bu etkinlikler Azure Hdınsight kümesinde veya bir Azure Batch havuzunda VM'lerin çalıştırın. Azure Batch kullandığınızda hello havuzu tooauto ölçekli yapılandırabilirsiniz (ekleyip hello iş yüküne göre VM'ler) sağladığınız bir formüle dayanarak.     

## <a name="architecture-of-sample-solution"></a>Örnek çözümü mimarisi
Bu makalede açıklanan hello mimarisi için basit bir çözüm olsa da, finansal hizmetler, görüntü işleme ve işleme ve genomic analiz tarafından modelleme risk gibi ilgili toocomplex senaryoları olur.

Merhaba diyagram gösterir; 1) nasıl Data Factory veri taşıma düzenler ve işleme ve Azure Batch 2) nasıl işlediği hello verileri paralel bir biçimde. Karşıdan yükleme ve kolay başvuru (11 x 17 inç yazdırma hello diyagramı. veya A3 boyutu): [Azure Batch ve Data Factory kullanarak HPC ve veriler orchestration](http://go.microsoft.com/fwlink/?LinkId=717686).

[![Büyük ölçekli veri işleme diyagramı](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)

Merhaba aşağıdaki listede hello işleminin hello temel adımları sağlar. Merhaba çözüm toobuild hello uçtan uca çözüm kodu ve açıklamaları içerir.

1. **Azure Batch (VM'ler) işlem düğümlerinin bir havuzuyla yapılandırma**. Merhaba düğüm sayısını ve her düğümün boyutu belirtebilirsiniz.
2. **Azure Data Factory örneğini oluşturabilir** Azure blob depolama, Azure toplu işlem hizmeti, girdi/çıktı verilerini ve iş akışı/ardışık taşıyın ve veri dönüştürme etkinlikleri ile temsil eden varlık ile yapılandırılmış.
3. **Özel bir .NET etkinliği hello Data Factory işlem hattı oluşturma**. Merhaba, hello Azure Batch havuzu üzerinde çalışır, kullanıcı kodu etkinliktir.
4. **Azure depolama alanında bloblar büyük miktarlarda giriş veri depolamak**. Veriler (genellikle zamanına göre) mantıksal dilimlere bölünür.
5. **Veri Fabrikası paralel olarak işlenir verileri kopyalar** toohello ikincil konum.
6. **Veri Fabrikası çalışan toplu işi tarafından ayrılan hello havuzunu kullanan hello özel etkinlik**. Veri Fabrikası etkinlikleri birlikte çalışabilir. Her etkinlik veri dilimini işler. Merhaba sonuçları Azure depolama alanında depolanır.
7. **Veri Fabrikası taşır hello son sonuçları tooa üçüncü konumunu**, bir uygulama aracılığıyla dağıtım için veya diğer araçları tarafından işlenmesi için.

## <a name="implementation-of-sample-solution"></a>Örnek çözümü uygulaması
Merhaba örnek çözümü kasıtlı olarak basit ve tooshow, nasıl toouse Data Factory ve toplu birlikte tooprocess veri kümeleri. Merhaba çözüm yalnızca hello bir arama terimi ("Microsoft") oluşumları bir zaman serisinin düzenlenmiş giriş dosyalarında sayar. Merhaba sayısı toooutput dosyalarını çıkarır.

**Zaman**: Azure, veri fabrikası ve Batch temelleri ile tanıdık ve tamamlanan hello Önkoşullar aşağıda listelenen sahip, bu çözüm alır 1-2 saat toocomplete tahmin ediyoruz.

### <a name="prerequisites"></a>Ön koşullar
#### <a name="azure-subscription"></a>Azure aboneliği
Bir Azure aboneliğiniz yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Bkz: [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="azure-storage-account"></a>Azure depolama hesabı
Bu öğreticide hello verileri depolamak için bir Azure depolama hesabı kullanın. Bir Azure depolama hesabınız yoksa bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account). Merhaba örnek çözümü blob depolama kullanır.

#### <a name="azure-batch-account"></a>Azure toplu işlem hesabı
Hello kullanarak bir Azure Batch hesabı oluşturma [Azure portal](http://manage.windowsazure.com/). Bkz: [oluşturma ve bir Azure Batch hesabını yönetmek](../batch/batch-account-create-portal.md). Merhaba, Azure Batch hesabı adını ve hesap anahtarını unutmayın. Aynı zamanda [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate bir Azure Batch hesabı. Bkz: [Azure Batch PowerShell cmdlet'leri kullanmaya başlama](../batch/batch-powershell-cmdlets-get-started.md) bu cmdlet'in kullanımı hakkında ayrıntılı yönergeler için.

Merhaba örnek çözümü Azure Batch (üzerinden dolaylı olarak bir Azure Data Factory işlem hattı) tooprocess verileri paralel şekilde havuzunda işlem düğümlerinin (sanal makineler yönetilen koleksiyonu) kullanır.

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a>Azure Batch havuzundaki sanal makineler (VM'ler)
Oluşturma bir **Azure Batch havuzu** en az 2 ile işlem düğümleri.

1. Merhaba, [Azure portal](https://portal.azure.com), tıklatın **Gözat** hello soldaki menüden ve'ı tıklatın **toplu işlem hesaplarını**.
2. Azure Batch hesabı tooopen hello seçin **toplu işlem hesabı** dikey.
3. Tıklatın **havuzları** döşeme.
4. Merhaba, **havuzları** dikey penceresinde hello araç tooadd bir havuzu Ekle düğmesine tıklayın.
   1. Merhaba havuzu için bir kimlik girin (**havuzu kimliği**). Not hello **hello havuzun kimliği**; hello Data Factory çözüm oluşturulurken gerekir.
   2. Belirtin **Windows Server 2012 R2** hello işletim sistemi ailesi ayarı için.
   3. Seçin bir **düğüm fiyatlandırma katmanı**.
   4. Girin **2** hello için değer olarak **hedef ayrılmış** ayarı.
   5. Girin **2** hello için değer olarak **en fazla düğüm başına görevleri** ayarı.
   6. Tıklatın **Tamam** toocreate hello havuzu.

#### <a name="azure-storage-explorer"></a>Azure Depolama Gezgini
[Azure Depolama Gezgini 6 (aracı)](https://azurestorageexplorer.codeplex.com/) veya [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (ClumsyLeaf yazılımından). İnceleme veya bulutta barındırılan uygulamalarınızın hello günlükleri de dahil olmak üzere Azure Storage projelerinizi hello verileri değiştirme için bu araçları kullanın.

1. Adlı bir kapsayıcı oluşturmak **mycontainer** özel erişim (anonim erişimi yok)
2. Kullanıyorsanız **CloudXplorer**, klasörleri oluşturun ve alt klasörler ile Merhaba yapı izlenerek:

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   `Inputfolder`ve `outputfolder` en üst düzey klasörlerde bulunan `mycontainer`. Merhaba `inputfolder` tarih-saat Damgalar (YYYY-AA-GG-ss) ile klasörleri varsa.

   Kullanıyorsanız **Azure Storage Gezgini**, hello sonraki adımda adlara sahip tooupload dosyaları gerekir: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` ve benzeri. Bu adım, hello klasörleri otomatik olarak oluşturur.
3. Bir metin dosyası oluşturun **dosya.txt'yi** hello anahtar sözcüğü sahip içerikle makinenizde **Microsoft**. Örneğin: "Özel Etkinlik Microsoft test özel etkinlik Microsoft test".
4. Azure blob depolama alanındaki giriş klasörleri aşağıdaki hello dosya toohello karşıya yükleyin.

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   Kullanıyorsanız **Azure Storage Gezgini**, hello dosyayı karşıya yüklemeyi **dosya.txt'yi** çok**mycontainer**. Tıklatın **kopyalama** hello araç toocreate hello blob bir kopyası üzerinde. Merhaba, **kopyalama Blob** iletişim kutusu, değişiklik hello **hedef blob adı** çok`inputfolder/2015-11-16-00/file.txt`. Bu adım toocreate yineleyin `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` ve benzeri. Bu eylemin hello klasörleri otomatik olarak oluşturur.
5. Adlı başka bir kapsayıcı oluşturma: `customactivitycontainer`. Merhaba özel etkinlik ZIP dosyası toothis kapsayıcısı karşıya yükleyin.

#### <a name="visual-studio"></a>Visual Studio
Microsoft Visual Studio 2012 veya hello Data Factory çözüm kullanılan sonraki toocreate hello özel toplu iş etkinliği toobe yükleyin.

### <a name="high-level-steps-toocreate-hello-solution"></a>Üst düzey adımları toocreate hello çözümü
1. Merhaba veri işleme mantığı içeren özel bir aktivite oluşturun.
2. Merhaba özel etkinlik kullanan bir Azure data factory oluşturun:

### <a name="create-hello-custom-activity"></a>Merhaba özel etkinlik oluşturma
Bu örnek çözümün hello Kalp Hello Data Factory özel etkinlik olur. Merhaba örnek çözümü Azure Batch toorun hello özel etkinlik kullanır. Bkz: [bir Azure Data Factory ardışık düzeninde özel etkinlikleri kullanmak](data-factory-use-custom-activities.md) hello temel bilgileri toodevelop özel etkinlikler ve kullanımı için bunları Azure Data Factory öğesinde ardışık düzenleri.

bir Azure Data Factory ardışık düzeninde kullanabileceğiniz bir .NET özel etkinlik toocreate, gereksinim duyduğunuz toocreate bir **.NET sınıf kitaplığı** uygulayan bir sınıf projeyle **IDotNetActivity** arabirimi. Bu arabirim yalnızca bir yöntemi vardır: **yürütme**. Merhaba yöntemi hello imzası şöyledir:

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

Merhaba yöntemi toounderstand gereken birkaç anahtar bileşenleri içerir.

* Merhaba yöntemi dört parametreleri alır:

  1. **linkedServices**. Giriş/Çıkış veri kaynakları bağlantı bağlı hizmetler numaralandırılabilir bir listesini (örneğin: Azure Blob Storage) toohello veri fabrikası. Bu örnekte, yalnızca bir bağlantılı hizmet türü girdi ve çıktı için kullanılan Azure Storage yok.
  2. **veri kümeleri**. Bu veri kümeleri numaralandırılabilir bir listesidir. Bu parametre tooget hello konumları ve girdi ve çıktı veri kümeleri tarafından tanımlanan şemaları kullanabilir.
  3. **Etkinlik**. Bu parametre hello geçerli işlem varlık - bu durumda, bir Azure Batch hizmetini temsil eder.
  4. **Günlükçü**. ardışık düzeni için "Kullanıcı" oturum hello olarak o yüzeyini hata ayıklama yorum yazmak hello Günlükçü sağlar hello.
* Merhaba yöntemi kullanılan toochain özel etkinlikler birlikte hello gelecekte olabilir bir sözlüğü döndürür. Bu özellik henüz uygulanmadı, bu nedenle boş bir sözlük hello döndürme.

#### <a name="procedure-create-hello-custom-activity"></a>Yordam: hello özel etkinlik oluşturma
1. Visual Studio'da .NET sınıf kitaplığı proje oluşturun.

   1. Başlatma **Visual Studio 2012**/**2013/2015**.
   2. Tıklatın **dosya**, çok noktası**yeni**, tıklatıp **proje**.
   3. Genişletme **şablonları**seçip **Visual C\#**. Bu kılavuzda, kullandığınız C\#, ancak .NET dil toodevelop hello özel etkinlik kullanabilirsiniz.
   4. Seçin **sınıf kitaplığı** hello sağ proje türlerinde hello listesinden.
   5. Girin **MyDotNetActivity** hello için **adı**.
   6. Seçin **C:\\ADF** hello için **konumu**. Başlangıç klasörü oluşturmak **ADF** henüz yoksa.
   7. Tıklatın **Tamam** toocreate hello projesi.
2. Tıklatın **Araçları**, çok noktası**NuGet Paket Yöneticisi**, tıklatıp **Paket Yöneticisi Konsolu**.
3. Merhaba, **Paket Yöneticisi Konsolu**, komut tooimport aşağıdaki hello yürütme **Microsoft.Azure.Management.DataFactories**.

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. İçeri aktarma hello **Azure Storage** toohello projesinde NuGet paketi. Bu örnekte hello Blob Depolama API kullandığından, bu paketi gerekir.

    ```powershell
    Install-Package Azure.Storage
    ```
5. Merhaba aşağıdakileri ekleyin **kullanarak** yönergeleri toohello kaynak hello proje dosyasında.

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Değişiklik hello hello adını **ad alanı** çok**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Merhaba sınıfı Hello adı çok değiştirmek**MyDotNetActivity** ve hello türetilen **IDotNetActivity** arabirim aşağıda gösterildiği gibi.

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Uygulama (Ekle) hello **yürütme** hello yöntemi **IDotNetActivity** toohello arabirim **MyDotNetActivity** örnek kodu toohello yöntemi aşağıdaki sınıf ve kopyalama hello. Merhaba bkz [yöntemi Çalıştır](#execute-method) Bu yöntemde kullanılan hello mantığı için bir açıklama için bölüm.

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass hello connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize hello continuation token before using it in hello do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get hello list of input blobs from hello input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns hello number of occurrences of
           // hello search term (“Microsoft”) in each blob associated
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload hello output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} toohello output blob", output);
       outputBlob.UploadText(output);
    
       // hello dictionary can be used toochain custom activities together in hello future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. Yardımcı yöntemler toohello sınıfı aşağıdaki hello ekleyin. Bu yöntemler hello tarafından çağrılan **yürütme** yöntemi. En önemlisi, hello **Hesapla** yöntemi her bir blob tekrarlanan hello kod yalıtır.

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    Merhaba **GetFolderPath** yöntemi döndürür hello yolu toohello klasöründe bu hello dataset noktaları tooand hello **GetFileName** yöntemi dataset noktalarına hello hello blob/dosya hello adını döndürür.

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    Merhaba **Hesapla** yöntemi hesaplar hello anahtar sözcüğü örneklerinin sayısını **Microsoft** hello giriş dosyalarında (BLOB hello klasöründe). Merhaba kodda sabit kodlanmış Hello arama terimi ("Microsoft").

1. Merhaba projeyi derleyin. Tıklatın **yapı** hello menüsüne ve ardından gelen **yapı çözümü**.
2. Başlatma **Windows Explorer**ve çok gidin**bin\\hata ayıklama** veya **bin\\yayın** klasör yapısının hello türüne bağlı olarak.
3. Zip dosyası oluşturun **MyDotNetActivity.zip** hello içindeki tüm hello ikili dosyaları içeren  **\\bin\\hata ayıklama** klasör. Tooinclude hello MyDotNetActivity isteyebilirsiniz. **pdb** bir hata oluştuğunda, hello soruna neden hello kaynak kodunda satır numarası gibi ek ayrıntıları almak için dosya.

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. Karşıya yükleme **MyDotNetActivity.zip** blob toohello blob kapsayıcı olarak: `customactivitycontainer` bu hello hello Azure blob depolama **StorageLinkedService** bağlı hello hizmetinde  **ADFTutorialDataFactory** kullanır. Merhaba blob kapsayıcı oluşturun `customactivitycontainer` zaten yoksa.

#### <a name="execute-method"></a>Execute yöntemi
Bu bölümde daha fazla ayrıntı ve hello yürütme yönteminin hello kodda hakkında notlar sağlanmaktadır.

1. Merhaba giriş koleksiyonu yineleme için hello üyeleri hello bulunduğunda [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) ad alanı. Merhaba blob koleksiyonu yineleme yapma gerektirir hello kullanarak **BlobContinuationToken** sınıfı. Esas olarak, bir kullanın-while döngüsünü hello döngüden çıkma için hello mekanizması olarak hello belirteci ile. Daha fazla bilgi için bkz: [nasıl toouse Blob depolama alanından .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Temel bir döngü burada gösterilir:

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   Merhaba Hello belgelerine bakın [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) Ayrıntılar için yöntem.
2. Merhaba kod içinde hello gider BLOB'lar hello kümesi aracılığıyla mantıksal olarak çalışmak için yapın-while döngüsünü. Merhaba, **yürütme** yöntemi, hello-döngü BLOB'lar hello listesi adlı tooa yöntemi geçirir **Hesapla**. Merhaba yöntemi döndürür adlı bir dize değişkeni **çıkış** hello kesimindeki tüm hello BLOB'lar aracılığıyla yinelendiğinde başka bir deyişle hello sonucu.

   Merhaba arama terimi oluşumları hello sayısını döndürür (**Microsoft**) hello blob toohello geçirilen **Hesapla** yöntemi.

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. Bir kez hello **Hesapla** yöntemi hello iş Bitti, bu tooa yeni blob yazılmış olmalıdır. Bu nedenle her işlenen BLOB'lar kümesi için yeni blob hello sonuçlarıyla yazılabilir. toowrite tooa yeni blob, Bul hello ilk çıkış veri kümesi.

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. Merhaba kod de yardımcı yöntemini çağırır: **GetFolderPath** tooretrieve hello klasör yolu (Merhaba depolama kapsayıcısı adı).

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   Merhaba **GetFolderPath** atamaları hello veri kümesi nesnesi tooan FolderPath adlı bir özellik olan AzureBlobDataSet.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. Merhaba kod çağrıları hello **GetFileName** yöntemi tooretrieve hello dosya adı (blob adı). Merhaba, kod tooget hello klasör yolu yukarıda benzer toohello kodudur.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. bir URI nesnesinden oluşturarak hello dosyasının Hello adı yazılır. Merhaba URI Oluşturucusu kullanan hello **BlobEndpoint** özelliği tooreturn hello kapsayıcı adı. Merhaba klasör yolu ve dosya adı tooconstruct hello çıkış blob URI'si eklenir.  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. Merhaba dosyasının Hello adı yazılmış ve şimdi hello hello çıkış dizesi yazabilirsiniz **Hesapla** yöntemi tooa yeni blob:

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a>Merhaba veri fabrikası oluşturma
Merhaba, [hello özel etkinlik oluşturmak](#create-the-custom-activity) bölümünde oluşturduğunuz özel etkinlik ve karşıya yüklenen hello zip dosyasıyla ikili dosyaları ve hello PDB dosya tooan Azure blob kapsayıcısı. Bu bölümde, oluşturduğunuz Azure **veri fabrikası** ile bir **ardışık düzen** hello kullanan **özel etkinlik**.

Merhaba girdi veri kümesi hello özel etkinlik hello BLOB'ları (dosyaları) hello giriş klasöründe gösterir (`mycontainer\\inputfolder`) blob depolama. Merhaba çıkış veri kümesi hello çıkış BLOB'lar hello çıkış klasöründe hello etkinliği gösterir (`mycontainer\\outputfolder`) blob depolama.

Bir veya daha fazla hello giriş klasörlerde bırak:

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

Örneğin, içeriği her hello klasörler aşağıdaki hello ile bir dosya (dosya.txt'yi) bırakın.

```
test custom activity Microsoft test custom activity Microsoft
```

Başlangıç klasörü 2 veya daha fazla dosya olsa bile her giriş klasörü Azure Data Factory tooa dilimi karşılık gelir. Her dilim hello ardışık düzen tarafından işlendiğinde hello özel etkinlik bu dilim için hello giriş klasöründeki tüm hello BLOB'lar dolaşır.

Beş çıktı hello ile aynı içerik dosyaları bakın. Örneğin, hello 2015-11-16-00 klasöründeki hello dosyasını işlemesini hello çıktı dosyası içeriği aşağıdaki hello sahiptir:

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

Birden çok dosya (dosya.txt'yi, file2.txt, file3.txt) düşüş hello ile aynı toohello giriş klasörü içerik, içerik hello çıktı dosyasında aşağıdaki hello bakın. Her bir klasör (2015-11-16-00, vb.) birden fazla girdi dosyası hello klasörü olmasına rağmen bu örnekteki tooa dilim karşılık gelir.

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

Merhaba çıktı dosyası üç satır artık, her girdi dosyasında (blob) hello dilim (2015-11-16-00) ile ilişkilendirilmiş hello klasör için bir tane var.

Bir görev çalıştırmak her etkinlik için oluşturulur. Bu örnekte, hello ardışık düzeninde yalnızca bir etkinlik yok. Bir dilim hello ardışık düzen tarafından işlendiğinde hello özel etkinlik Azure Batch tooprocess hello dilim üzerinde çalışır. Beş dilimleri (her dilim birden çok BLOB veya dosya olabilir) olduğundan, Azure Batch oluşturulan beş görevler vardır. Bir görev toplu olarak çalıştığında, onu çalıştıran gerçekte hello özel etkinliktir.

izlenecek yol aşağıdaki hello ek ayrıntılar sağlar.

#### <a name="step-1-create-hello-data-factory"></a>1. adım: hello veri fabrikası oluşturma
1. İçinde toohello oturum sonra [Azure portal](https://portal.azure.com/), adımları hello:

   1. Tıklatın **yeni** hello sol menüdeki.
   2. Tıklatın **veri + analiz** hello içinde **yeni** dikey.
   3. Tıklatın **Data Factory** hello üzerinde **veri analizi** dikey.
2. Merhaba, **yeni data factory** dikey penceresinde girin **CustomActivityFactory** hello adı için. Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir. Merhaba hatayı alırsanız: **veri fabrikası adı "CustomActivityFactory" kullanılabilir değil**, hello veri fabrikası hello adını değiştirin (örneğin, **yournameCustomActivityFactory**) ve oluşturmayı deneyin yeniden.
3. Tıklatın **kaynak grubu adı**, varolan bir kaynak grubu seçin veya bir kaynak grubu oluşturun.
4. Merhaba doğru abonelikte ve bölgede oluşturulan hello veri fabrikası toobe istediğiniz kullandığınızdan emin olun.
5. Tıklatın **oluşturma** hello üzerinde **yeni data factory** dikey.
6. Hello oluşturulmakta hello veri fabrikası gördüğünüz **Pano** hello Azure portal.
7. Merhaba veri fabrikası başarıyla oluşturulduktan sonra gösterir hello veri fabrikası sayfasına bakın hello hello data Factory içeriği.

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a>2. adım: bağlı hizmetler oluşturma
Bağlı hizmetler veri depolarını veya hizmetleri tooan Azure data factory işlem. Bu adımda, bağlantı, **Azure Storage** hesabı ve **Azure Batch** hesap tooyour veri fabrikası.

#### <a name="create-azure-storage-linked-service"></a>Azure Storage bağlı hizmeti oluşturma
1. Merhaba tıklatın **yazar ve dağıtma** döşeme hello üzerinde **DATA FACTORY** dikey **CustomActivityFactory**. Merhaba Data Factory Düzenleyici bakın.
2. Tıklatın **yeni veri deposu** hello komut çubuğu ve seçin **Azure depolama.** Görmeniz gerekir hello Azure depolama alanı oluşturmak için JSON betiği bağlantılı hizmeti hello düzenleyicisinde.

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. Değiştir **hesap adı** hello Azure depolama hesabınızın adını içeren ve **hesap anahtarı** hello erişim anahtarı hello Azure depolama hesabı olan. toolearn tooget depolama alanınızın nasıl erişim anahtar, bkz: [erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma depolama](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

4. Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a>Azure Batch bağlı hizmet oluşturma
Bu adımda oluşturduğunuz için bağlı hizmet, **Azure Batch** kullanılan toorun hello Data Factory özel etkinlik olan hesap.

1. Tıklatın **yeni işlem** hello komut çubuğu ve seçin **Azure Batch.** Görmeniz gerekir hello bir Azure Batch oluşturmak için JSON betiği bağlantılı hizmeti hello düzenleyicisinde.
2. Merhaba JSON betiği:

   1. Değiştir **hesap adı** Azure Batch hesabınızın hello ada sahip.
   2. Değiştir **erişim tuşu** hello Azure Batch hesabı hello erişim anahtarı ile.
   3. Merhaba Hello hello havuz Kimliğini girin **poolName** özelliği**.** Bu özellik için ya da havuz adı belirtin veya Havuz kimliği.
   4. Hello için Hello toplu URI girin **batchUri** JSON özelliği.

      > [!IMPORTANT]
      > Merhaba **URL** hello gelen **Azure Batch hesabı dikey** biçimini izleyen hello olduğu: \<accountname\>.\< Bölge\>. batch.azure.com. Hello için **batchUri** hello JSON özelliğinde ihtiyacınız çok**"accountname." Kaldır** Merhaba URL'den. Örnek: `"batchUri": "https://eastus.batch.azure.com"`.
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      Hello için **poolName** özelliği, hello hello havuzu hello havuzunun hello adı yerine Kimliğini de belirtebilirsiniz.

      > [!NOTE]
      > Hdınsight için yaptığı gibi hello Data Factory hizmeti Azure toplu işlem için bir isteğe bağlı seçeneği desteklemiyor. Bu gibi durumlarda, kendi Azure Batch havuzu yalnızca bir Azure data factory kullanabilirsiniz.
      >
      >
   5. Belirtin **StorageLinkedService** hello için **linkedServiceName** özelliği. Bu bağlı hizmetin hello önceki adımda oluşturduğunuz. Bu depolama dosyaları ve günlükleri için hazırlama alanı kullanılır.
3. Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.

#### <a name="step-3-create-datasets"></a>3. adım: veri kümeleri oluşturma
Bu adımda, veri kümeleri toorepresent girişi oluşturun ve çıktı verilerini.

#### <a name="create-input-dataset"></a>Girdi veri kümesi oluşturma
1. Merhaba, **Düzenleyicisi** hello veri fabrikası'ı tıklatın **yeni veri kümesi** hello araç ve tıklatın düğmesinde **Azure Blob Depolama** hello açılan menüsünden.
2. Merhaba JSON hello sağ bölmedeki JSON parçacığı aşağıdaki hello ile değiştirin:

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    Başlangıç saati ile bu kılavuzda daha sonra bir işlem hattı oluşturma: 2015-11-16T00:00:00Z ve bitiş zamanı: 2015-11-16T05:00:00Z. Zamanlanmış tooproduce verilerdir **saatlik**, 5 giriş/çıkış dilimler olduklarından (arasında **00**: 00:00 -\> **05**: 00:00).

    Merhaba **sıklığı** ve **aralığı** hello girdi veri kümesi çok ayarlamak için**saat** ve **1**, o hello başka bir deyişle, dilim kullanılabilir giriş saatlik.

    Hangi tarafından temsil edilen hello başlangıç zamanlarını her dilim için işte **SliceStart** JSON parçacığı yukarıda hello sistem değişkeninde.

    | **Dilim** | **Başlangıç zamanı**          |
    |-----------|-------------------------|
    | 1         | 2015 11 16T**00**: 00:00 |
    | 2         | 2015 11 16T**01**: 00:00 |
    | 3         | 2015 11 16T**02**: 00:00 |
    | 4         | 2015 11 16T**03**: 00:00 |
    | 5         | 2015 11 16T**04**: 00:00 |

    Merhaba **folderPath** hello yıl, ay, gün ve saat parçası hello dilim başlangıç saati kullanılarak hesaplanır (**SliceStart**). Bu nedenle, işte nasıl bir giriş eşlenen tooa dilim klasörüdür.

    | **Dilim** | **Başlangıç zamanı**          | **Giriş klasörü**  |
    |-----------|-------------------------|-------------------|
    | 1         | 2015 11 16T**00**: 00:00 | 2015-11-16-**00** |
    | 2         | 2015 11 16T**01**: 00:00 | 2015-11-16-**01** |
    | 3         | 2015 11 16T**02**: 00:00 | 2015-11-16-**02** |
    | 4         | 2015 11 16T**03**: 00:00 | 2015-11-16-**03** |
    | 5         | 2015 11 16T**04**: 00:00 | 2015-11-16-**04** |

1. Tıklatın **dağıtma** araç toocreate hello ve hello dağıtmak **InputDataset** tablo.

#### <a name="create-output-dataset"></a>Çıktı veri kümesi oluşturma
Bu adımda, başka bir veri kaynağının veri türü AzureBlob toorepresent hello çıkış veri kümesi oluşturun.

1. Merhaba, **Düzenleyicisi** hello veri fabrikası'ı tıklatın **yeni veri kümesi** hello araç ve tıklatın düğmesinde **Azure Blob Depolama** hello açılan menüsünden.
2. Merhaba JSON hello sağ bölmedeki JSON parçacığı aşağıdaki hello ile değiştirin:

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           }
       }
    }
    ```

    Bir çıkış blob/dosyası, her girdi dilimi için oluşturulur. İşte bir çıktı dosyası için her dilimi nasıl adlandırılır. Bir çıkış klasöründe oluşturulan tüm hello çıktı dosyaları: `mycontainer\\outputfolder`.

    | **Dilim** | **Başlangıç zamanı**          | **Çıkış dosyası**       |
    |-----------|-------------------------|-----------------------|
    | 1         | 2015 11 16T**00**: 00:00 | 2015-11-16 -**00. txt** |
    | 2         | 2015 11 16T**01**: 00:00 | 2015-11-16 -**01. txt** |
    | 3         | 2015 11 16T**02**: 00:00 | 2015-11-16 -**02. txt** |
    | 4         | 2015 11 16T**03**: 00:00 | 2015-11-16 -**03. txt** |
    | 5         | 2015 11 16T**04**: 00:00 | 2015-11-16 -**04. txt** |

    Tüm giriş klasöründeki dosyaları hello unutmayın (örneğin: 2015-11-16-00) hello başlangıç saatine sahip bir dilim parçasıdır: 2015-11-16-00. Bu dilim işlendiğinde hello özel etkinlik her dosyası aracılığıyla tarar ve arama terimi ("Microsoft") oluşumları hello sayısıyla hello çıkış dosyasındaki bir satır üretir. Başlangıç klasörü 2015-11-16-00 üç dosya varsa vardır üç satır hello çıktı dosyasına: 2015-11-16-00.txt.

1. Tıklatın **dağıtma** araç toocreate hello ve hello dağıtmak **OutputDataset**.

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a>4. adım: Oluşturma ve hello ardışık düzen özel etkinliği ile çalıştırma
Bu adımda, bir etkinlik, daha önce oluşturduğunuz hello özel etkinliği ile işlem hattı oluşturma.

> [!IMPORTANT]
> Merhaba yüklemediniz varsa **dosya.txt'yi** tooinput klasörleri hello blob kapsayıcısında, bunu hello işlem hattı oluşturmadan önce. Merhaba **isPaused** özelliği ayarlanmış toofalse hello ile JSON işlem hattında, hello ardışık düzen hemen hello çalıştığında **Başlat** hello son tarihidir.
>
>

1. Hello Data Factory Düzenleyici'de, tıklatın **yeni işlem hattı** hello komut çubuğunda. Merhaba komutu görmüyorsanız tıklatın **... (Üç nokta)**  toosee onu.
2. Merhaba JSON hello sağ bölmedeki JSON betiği aşağıdaki hello ile değiştirin:

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   Hello aşağıdaki noktaları göz önünde bulundurun:

   * Hello ardışık düzeninde yalnızca bir etkinlik olduğu ve bu tür: **DotNetActivity**.
   * **AssemblyName** hello DLL toohello adına ayarlanır: **MyDotNetActivity.dll**.
   * **EntryPoint** çok ayarlanır**MyDotNetActivityNS.MyDotNetActivity**. Temelde olan \<ad alanı\>.\< ClassName\> kodunuzda.
   * **PackageLinkedService** çok ayarlanır**StorageLinkedService** hello özel etkinlik zip dosyasını içeren toohello blob depolama işaret eder. Giriş/çıkış dosyaları ve hello özel etkinlik zip dosyası için farklı Azure depolama hesapları kullanıyorsanız, başka bir Azure Storage toocreate sahip bağlı hizmeti. Bu makalede, kullanmakta olduğunuz varsayılmaktadır hello aynı Azure depolama hesabı.
   * **PackageFile** çok ayarlanır**customactivitycontainer/MyDotNetActivity.zip**. Merhaba biçimdedir: \<containerforthezip\>/\<nameofthezip.zip\>.
   * Merhaba özel etkinlik alır **InputDataset** giriş olarak ve **OutputDataset** çıktı olarak.
   * Merhaba **linkedServiceName** hello özel etkinlik özelliğinin işaret toohello **AzureBatchLinkedService**, o hello özel etkinliği Azure Data Factory söyleyen Azure batch toorun gerekiyor.
   * Merhaba **eşzamanlılık** ayarı önemlidir. 1, 2 veya daha fazla işlem düğümleri hello Azure Batch havuzunda olsa dahi, hello varsayılan değeri kullanırsanız hello dilimler işlenir birbiri ardından. Bu nedenle, Azure batch hello paralel işleme yeteneğinden olmuyor. Ayarlarsanız **eşzamanlılık** tooa daha yüksek değer, deyin 2 geldiğini iki dilimler (Azure Batch tootwo görevlerinde karşılık gelir) hello işlenen aynı zaman; bu durumda hem hello Vm'lerde hello Azure Batch havuzu kullanıldığı. Bu nedenle, hello eşzamanlılık özelliğini uygun şekilde ayarlayın.
   * Yalnızca bir görev (dilim) varsayılan olarak, varsayılan olarak herhangi bir noktada bir VM üzerinde yürütülür. Merhaba, varsayılan olarak, hello nedeni **maksimum VM başına görevleri** too1 bir Azure Batch havuzu için ayarlanır. İki veri fabrikası dilimler hello konumundaki bir VM'de çalıştıran için Önkoşullar bir parçası olarak, bir havuz bu özellik kümesi too2 ile oluşturduğunuz aynı anda.

    -   **isPaused** özelliği toofalse varsayılan olarak ayarlanır. Hello dilimler hello geçmiş başlatmak için hello ardışık düzen hemen bu örnekte çalışır. Bu özellik tootrue toopause hello ardışık düzen ve geri toofalse toorestart ayarlayın.

    -   Merhaba **Başlat** zaman ve **son** kez beş saatten birbirinden olur ve dilimlerinin saatlik, beş dilimler hello ardışık düzen tarafından üretilen şekilde.

1. Tıklatın **dağıtma** toodeploy hello ardışık çubuğu hello komutu.

#### <a name="step-5-test-hello-pipeline"></a>5. adım: Test hello ardışık düzen
Bu adımda, hello giriş klasörler halinde dosyaları bırakarak hello ardışık düzen sınayın. Sınama hello ardışık düzen ile bir giriş klasörü başına bir dosyayı ile başlayalım.

1. Hello Azure portal'ın Hello Data Factory dikey penceresinde tıklayın **diyagramı**.

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. Girdi veri kümesi Hello diyagram görünümünde çift: **InputDataset**.

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. Merhaba görmelisiniz **InputDataset** beş dikey dilimi hazır. Bildirim hello **DİLİM başlangıç saati** ve **DİLİM bitiş saati** her dilim için.

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. Merhaba, **diyagram görünümü**, şimdi **OutputDataset**.
5. Bunlar zaten oluşturulmuş olduğunu hello beş çıkış dilimler hello hazır durumda olduğunu görmeniz gerekir.

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. Kullanım Azure portal tooview hello **görevleri** hello ile ilişkili **dilimler** ve her dilim çalıştırdı hangi VM bakın. Bkz: [Data Factory ve toplu tümleştirme](#data-factory-and-batch-integration) ayrıntıları bölümü.
7. Merhaba hello Çıkış dosyalarını görmelisiniz `outputfolder` , `mycontainer` , Azure blob depolamada.

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   Bir giriş her dilim için beş çıktı dosyalarını görmeniz gerekir. Her hello dosyasının çıkışı aşağıdaki içerik benzer toohello olmalıdır çıktı:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   Merhaba Aşağıdaki diyagramda nasıl hello Data Factory dilimler Azure Batch tootasks eşleme gösterilmektedir. Bu örnekte, yalnızca bir çalışma bir dilimi var.

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. Şimdi, bir klasördeki birden çok dosyalarla deneyelim. Dosyaları oluşturun: **file2.txt**, **file3.txt**, **file4.txt**, ve **file5.txt** hello ile aynı hello klasöründeki dosya.txt'yi olduğu gibi içerik: **2015-11-06-01**.
9. Merhaba çıkış klasöründe **silmek** hello çıktı dosyası: **2015-11-16-01.txt**.
10. Şimdi hello içinde **OutputDataset** dikey penceresinde, sağ hello dilimle **DİLİM başlangıç saati** çok ayarlamak**11/16/2015 01:00:00 AM**, tıklatıp **çalıştırmak**toorerun/yeniden-process hello dilim. Şimdi, hello dilim beş dosya yerine bir dosya vardır.

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. Durumunu Hello dilim çalıştırır ve sonra **hazır**, bu dilim için hello çıktı dosyasında hello içeriği doğrulayın (**2015-11-16-01.txt**) hello içinde `outputfolder` , `mycontainer` blob depolama alanınızın içinde. Merhaba dilimin her dosya için bir satır olması gerekir.

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> Beş giriş dosyalarıyla denemeden önce hello çıktı dosyası 2015-11-16-01.txt silmedi varsa bir satırından hello önceki dilim çalıştırın ve Çalıştır hello geçerli dilimin beş satırlarından bakın. Zaten varsa, varsayılan olarak, hello içerik eklenmiş toooutput dosyasıdır.
>
>

#### <a name="data-factory-and-batch-integration"></a>Veri Fabrikası ve toplu tümleştirmesi
Hello Data Factory hizmetinin hello adı ile Azure toplu işleminde bir işi oluşturur: `adf-poolname:job-xxx`.

![Azure Data Factory - toplu işler](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

Bir görev hello işteki her bir dilim etkinlik çalıştırması için oluşturulur. İşlenen 10 dilim hazır toobe varsa, 10 görevleri hello işinde oluşturulur. Birden çok işlem düğümleri hello havuzunda varsa paralel olarak çalışan birden fazla dilim olabilir. Merhaba maksimum başına düğüm çok kümesi işlem görevlerini durumunda > 1, olabilir birden fazla bir dilim hello üzerinde çalışan aynı işlem.

Bu örnekte, beş dilimler, Azure Batch kadar beş görevleri vardır. Merhaba ile **eşzamanlılık** çok ayarlamak**5** hello Azure Data Factory JSON'de kanal ve **maksimum VM başına görevleri** çok ayarlamak**2** Azure toplu ile havuz **2** VM'ler, (görevler için başlangıç ve bitiş zamanlarını denetleyin) hello görevleri çalıştırır hızlı.

Merhaba portal tooview hello toplu ve hello ile ilişkili görevleri kullanma **dilimler** ve her dilim çalıştırdı hangi VM bakın.

![Azure Data Factory - toplu iş görevleri](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a>Merhaba ardışık hata ayıklama
Hata ayıklama birkaç temel teknikten oluşur:

1. Merhaba girdi dilimi çok ayarlanmamışsa**hazır**, hello giriş klasör yapısı doğru olduğundan ve dosya.txt'yi hello giriş klasörlerde var olduğunu doğrulayın.

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. Merhaba, **yürütme** özel etkinliklerinizi, kullanım hello yöntemi **IActivityLogger** yardımcı olan nesne toolog bilgileri sorunları giderme. oturum karışılama iletileri hello kullanıcı görünmesini\_0. günlük dosyası.

   Merhaba, **OutputDataset** dikey penceresinde hello dilim toosee hello tıklatın **veri DİLİMİ** dikey penceresinde, dilim için. Gördüğünüz **etkinlik çalışması** bu dilim için. Merhaba dilim için bir etkinlik görmeniz gerekir. Tıklatırsanız **çalıştırmak** hello komut çubuğunda hello için başka bir etkinlik başlatabilirsiniz aynı dilim.

   Merhaba etkinlik tıklattığınızda hello bkz **etkinlik çalışma ayrıntıları** günlük dosyalarının listesini içeren dikey. Merhaba, günlüğe kaydedilen iletilere bakın **kullanıcı\_0. günlük** dosya. Hata oluştuğunda hello yeniden deneme sayısı hello ardışık düzen/JSON etkinliğinde too3 ayarlandığından üç Etkinlik çalışması bakın. Merhaba etkinlik tıklattığınızda tootroubleshoot hello hata inceleyebilirsiniz hello günlük dosyalarına bakın.

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   Günlük dosyaları Hello listesinde hello tıklayın **kullanıcı 0.log**. Merhaba sağ panelde hello kullanarak hello sonucu olan **IActivityLogger.Write** yöntemi.

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   Sistem hata iletileri ve özel durumlar için sistem 0.log denetleyin.

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. Merhaba dahil **PDB** hello hata ayrıntıları bilgileri gibi böylece hello zip dosyasında dosya **çağrı yığını** bir hata oluştuğunda.
4. Merhaba özel etkinlik hello olmalıdır tüm dosyaları hello zip dosyasında hello **üst düzey** klasörsüz ile.

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. Bu hello olun **assemblyName** (MyDotNetActivity.dll) **entryPoint** (MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) ve **packageLinkedService** (noktası toohello Azure hello zip dosyasını içeren depolama blob) toocorrect değerlerini ayarlayın.
6. Bir hata ve istediğiniz tooreprocess hello dilim sabit, hello hello dilimi sağ **OutputDataset** tıklayın ve dikey **çalıştırmak**.

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > Gördüğünüz bir **kapsayıcı** adlı Azure Blob storage'da: `adfjobs`. Bu kapsayıcı otomatik olarak silinmez, ancak test hello çözüm tamamladıktan sonra güvenle silebilirsiniz. Benzer şekilde, bir Azure Batch hello Data Factory çözüm oluşturur **iş** adlı: `adf-\<pool ID/name\>:job-0000000001`. Merhaba çözüm isterseniz, test ettikten sonra bu iş silebilirsiniz.
   >
   >
7. Merhaba özel etkinlik hello kullanmaz **app.config** paketinizi dosyasından. Bu nedenle, kodunuzu hello yapılandırma dosyasından bağlantı dizelerini yazıyorsa, çalışma zamanında çalışmıyor. Azure Batch kullanarak toohold olduğunda en iyi yöntem herhangi parolalarında hello bir **Azure KeyVault**, sertifika tabanlı hizmet asıl tooprotect hello keyvault kullanın ve hello sertifika tooAzure Batch havuzu dağıtın. .NET özel etkinlik hello sonra gizli hello KeyVault çalışma zamanında erişebilirsiniz. Bu çözüm genel bir ve gizli anahtarı, yalnızca bağlantı dizesi tooany türü ölçeklendirebilirsiniz.

    Daha kolay bir çözüm (ancak en iyi yöntem değildir): oluşturabileceğiniz bir **Azure SQL bağlı hizmeti** bağlantı dizesi ayarlarıyla kullanır bağlantılı hizmet ve sahte bir giriş veri kümesi olarak zinciri hello dataset hello bir veri kümesi oluşturma toohello özel .NET etkinlik. Hizmetin bağlantı dizesi hello özel etkinlik kodda erişim hello bağlı ve çalışma zamanında düzgün çalışması gerekir. ardından kullanabilirsiniz.  

#### <a name="extend-hello-sample"></a>Merhaba örnek genişletme
Bu örnek toolearn Azure Data Factory ve Azure Batch özellikler hakkında daha fazla genişletebilirsiniz. Örneğin, farklı bir zaman aralığı tooprocess dilimleri hello aşağıdaki adımları:

1. Merhaba klasörlerdeki aşağıdaki hello eklemek `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 ve Yerleştir bu klasörlerdeki girişi dosyaları. Değiştirme hello bitiş saati başlangıç ardışık düzen tarafından `2015-11-16T05:00:00Z` çok`2015-11-16T10:00:00Z`. Merhaba, **diyagram görünümü**, hello çift **InputDataset**ve hello girdi dilimlerinin hazır olduğunu doğrulayın. Çift **OuptutDataset** çıkış dilimler toosee hello durumu. Hazır durumda olmaları durumunda hello çıkış dosyaları için hello çıkış klasörünü denetleyin.
2. Artırma veya azaltma hello **eşzamanlılık** ayarı toounderstand Merhaba, çözümünüzün performansını etkiler nasıl özellikle hello işleme Azure Batch oluşan. (Bkz. adım 4: oluşturup hello hakkında daha fazla bilgi için hello ardışık düzen çalıştırmak **eşzamanlılık** ayarı.)
3. Küçük daha yüksek bir havuz oluşturma **maksimum VM başına görevleri**. Merhaba, oluşturduğunuz yeni havuz güncelleştirme hello hello Data Factory çözüm bağlı Azure Batch hizmetinde toouse. (Bkz. adım 4: oluşturup hello hakkında daha fazla bilgi için hello ardışık düzen çalıştırmak **maksimum VM başına görevleri** ayarı.)
4. Bir Azure Batch havuzu oluşturma **otomatik ölçeklendirme** özelliği. Bir Azure Batch havuzunda işlem düğümlerini otomatik olarak ölçeklendirme, uygulamanız tarafından kullanılan güç işleme hello dinamik ayarlanmasıdır. 

    Merhaba formül örneği burada başarır davranış aşağıdaki hello: hello havuzu başlangıçta oluşturulduğunda 1 VM ile başlar. Çalışan + (kuyruğa alınmış) etkin $PendingTasks ölçüm tanımlar hello sayıda görev durumu.  Merhaba formül hello ortalama sayısı Bekleyen Görevler hello Son 180 saniye bulur ve TargetDedicated uygun şekilde ayarlar. TargetDedicated hiçbir zaman 25 VM'ler gider sağlar. Bu nedenle, yeni görevler gönderildiği haliyle havuzu otomatik olarak büyür ve görevler tamamlanınca VM'ler boş bir birer birer hale ve bu VM'lerin hello otomatik ölçeklendirmeyi küçültür. startingNumberOfVMs ve maxNumberofVMs ayarlanmış tooyour gereksinimleri olabilir.
 
    Otomatik ölçeklendirme formülü:

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   Bkz: [ölçek işlem düğümlerini Azure Batch havuzunda otomatik olarak](../batch/batch-automatic-scaling.md) Ayrıntılar için.

   Merhaba havuzu hello varsayılan kullanıyorsanız [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch hizmeti, 15-30 dakika tooprepare hello VM hello özel etkinlik çalıştırmadan önce sürebilir.  Merhaba havuzu farklı autoScaleEvaluationInterval kullanıyorsanız, hello Batch hizmeti autoScaleEvaluationInterval + 10 dakika sürebilir.
5. Merhaba örnek çözümde hello **yürütme** yöntemini çağırır hello **Hesapla** bir giriş veri dilimi tooproduce bir çıktı veri dilimi işler yöntemi. Kendi yöntemi tooprocess verileri girin ve bir çağrı tooyour yöntemiyle hello hesapla yöntem çağrısı hello Execute yöntemi Değiştir yazabilirsiniz.

### <a name="next-steps-consume-hello-data"></a>Sonraki adımlar: hello verileri kullanmak
Veri işleme sonra onu gibi çevrimiçi araçlarla tüketebileceği **Microsoft Power BI**. Power BI anlamak bağlantılar toohelp işte ve nasıl toouse Azure içinde:

* [Power BI kümesinde keşfedin](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [Merhaba Power BI Desktop ile çalışmaya başlama](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [Power bı'da veri yenileme](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [Azure ve Power BI - temel genel bakış](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a>Başvurular
* [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)

  * [Giriş tooAzure Data Factory hizmeti](data-factory-introduction.md)
  * [Azure Data Factory ile çalışmaya başlama](data-factory-build-your-first-pipeline.md)
  * [Bir Azure Data Factory işlem hattında özel etkinlikler kullanma](data-factory-use-custom-activities.md)
* [Azure toplu işlem](https://azure.microsoft.com/documentation/services/batch/)

  * [Azure Batch temel bilgileri](../batch/batch-technical-overview.md)
  * [Azure Batch özelliklerine genel bakış](../batch/batch-api-basics.md)
  * [Hello Azure portal, Azure Batch hesabı oluşturabilir ve yönetebilirsiniz](../batch/batch-account-create-portal.md)
  * [Azure Batch kitaplığını .NET ile çalışmaya başlama](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
