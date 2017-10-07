---
title: "bir Azure Data Factory işlem hattı aaaUse özel etkinlikleri"
description: "Bilgi nasıl toocreate özel etkinlikler ve bunları bir Azure Data Factory işlem hattı kullanabilirsiniz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a>Bir Azure Data Factory işlem hattında özel etkinlikler kullanma

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive etkinliği](data-factory-hive-activity.md) 
> * [Pig etkinliği](data-factory-pig-activity.md)
> * [MapReduce etkinliği](data-factory-map-reduce.md)
> * [Hadoop akış etkinliği](data-factory-hadoop-streaming-activity.md)
> * [Spark etkinliği](data-factory-spark.md)
> * [Machine Learning Batch Yürütme Etkinliği](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning Kaynak Güncelleştirme Etkinliği](data-factory-azure-ml-update-resource-activity.md)
> * [Saklı Yordam Etkinliği](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL Etkinliği](data-factory-usql-activity.md)
> * [.NET özel etkinlik](data-factory-use-custom-activities.md)

İki tür kullanabileceğiniz bir Azure Data Factory ardışık düzeninde etkinlik yok.

- [Veri taşıma etkinlikleri](data-factory-data-movement-activities.md) arasında toomove veri [desteklenen kaynak ve havuz veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- [Veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) kullanarak tootransform Veri Hizmetleri Azure Hdınsight, Azure Batch ve Azure Machine Learning gibi işlem. 

Veri Fabrikası desteklemiyor, bir veri deposu/toomove verileri oluşturma bir **özel etkinlik** kendi veri taşıma mantığı ve kullanım hello etkinliği ile bir ardışık düzende. Benzer şekilde, tootransform/işlemi verileri veri fabrikası tarafından desteklenmeyen bir şekilde kendi veri dönüştürme mantığı ile özel bir etkinlik oluşturmak ve bir ardışık düzende hello etkinliği kullanın. 

Özel Etkinlik toorun yapılandırabileceğiniz bir **Azure Batch** sanal makine ya da Windows tabanlı bir havuzu **Azure Hdınsight** küme. Azure Batch kullanırken, mevcut bir Azure Batch havuzu kullanabilirsiniz. Oysa Hdınsight kullanırken, mevcut bir Hdınsight kümesine ya da otomatik olarak oluşturulan bir küme, isteğe bağlı çalışma zamanında için kullanabilirsiniz.  

Merhaba aşağıdaki örneklerde özel bir .NET etkinlik oluşturmak ve bir ardışık düzende hello özel etkinlik kullanmak için adım adım yönergeler sağlar. Merhaba izlenecek kullanan bir **Azure Batch** bağlı hizmeti. toouse Azure Hdınsight bağlı hizmeti bunun yerine, türü bağlı hizmet oluşturma **Hdınsight** (kendi Hdınsight kümenizi) veya **HDInsightOnDemand** (Data Factory oluşturduğu bir Hdınsight kümesi İsteğe bağlı). Ardından, özel etkinlik toouse hello Hdınsight bağlı hizmeti yapılandırın. Bkz: [kullanım Azure Hdınsight bağlantılı Hizmetleri](#use-hdinsight-compute-service) Azure Hdınsight toorun hello özel etkinlik kullanımıyla ilgili ayrıntılar için bölüm.

> [!IMPORTANT]
> - Merhaba özel .NET etkinlikler yalnızca Windows tabanlı Hdınsight kümelerinde çalıştırın. Bu sınırlama aşağıdaki haller için geçici çözüm toouse hello harita azaltmak etkinlik toorun özel Java kod Linux tabanlı Hdınsight kümesi üzerinde ' dir. Toouse VM'ler toorun özel etkinlikler bir Hdınsight kümesi yerine bir Azure Batch havuzu başka bir seçenektir.
> - Olası toouse veri yönetimi ağ geçidi bir özel etkinlik tooaccess şirket içi veri kaynaklarından değil. Şu anda [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) yalnızca hello kopyalama etkinliği ve saklı yordam etkinliği veri fabrikasında destekler.   

## <a name="walkthrough-create-a-custom-activity"></a>İzlenecek yol: özel etkinlik oluşturma
### <a name="prerequisites"></a>Ön koşullar
* Visual Studio 2012/2013/2015
* [Azure .NET SDK](https://azure.microsoft.com/downloads/)’yı indirip yükleyin

### <a name="azure-batch-prerequisites"></a>Azure Batch önkoşulları
Merhaba kılavuzda Azure toplu işlem kaynağı olarak kullanan özel .NET etkinliklerinizi çalıştırın. **Azure Batch** büyük ölçekli paralel çalıştırmak için hizmet ve yüksek performanslı bilgi işlem (HPC) uygulamalarında verimli bir şekilde hello bulut platformudur. Azure toplu işlem yoğunluklu iş toorun yönetilen üzerinde zamanlar **sanal makineler koleksiyonunda**, ve ölçek kaynakları toomeet hello işleriniz ihtiyaçlarını işlem otomatik olarak. Bkz: [Azure Batch temel bilgileri] [ batch-technical-overview] hello Azure Batch hizmeti için ayrıntılı bir genel bakış makalesi.

Merhaba öğretici için VM'ler havuzuyla Azure Batch hesabı oluşturun. Merhaba adımlar şunlardır:

1. Oluşturma bir **Azure Batch hesabı** hello kullanarak [Azure portal](http://portal.azure.com). Bkz: [oluşturma ve bir Azure Batch hesabını yönetmek] [ batch-create-account] makale yönergeler için.
2. Hello Azure toplu işlem hesabı adı, hesap anahtarı, URI ve havuz adı unutmayın. Bunları toocreate bir Azure Batch bağlantılı hizmeti gerekir.
    1. Gördüğünüz Hello giriş sayfasında Azure toplu işlem hesabı için bir **URL** biçimini izleyen hello içinde: `https://myaccount.westus.batch.azure.com`. Bu örnekte, **myaccount** hello Azure Batch hesabı hello adıdır. Merhaba bağlantılı hizmet tanımında kullandığınız URI hello hesabının hello adı olmadan hello URL'dir. Örneğin: `https://<region>.batch.azure.com`.
    2. Tıklatın **anahtarları** hello soldaki menüden ve kopyalama hello **birincil erişim ANAHTARINI**.
    3. toouse var olan bir havuzu tıklatın **havuzları** hello menü ve hello Not **kimliği** hello havuzunun. Var olan bir havuzu sahip değilseniz, sonraki adıma toohello taşıyın.     
2. Oluşturma bir **Azure Batch havuzu**.

   1. Merhaba, [Azure portal](https://portal.azure.com), tıklatın **Gözat** hello soldaki menüden ve'ı tıklatın **toplu işlem hesaplarını**.
   2. Azure Batch hesabı tooopen hello seçin **toplu işlem hesabı** dikey.
   3. Tıklatın **havuzları** döşeme.
   4. Merhaba, **havuzları** dikey penceresinde hello araç tooadd bir havuzu Ekle düğmesine tıklayın.
      1. Bir kimlik hello havuzu (havuzu kimliği) girin. Not hello **hello havuzun kimliği**; hello Data Factory çözüm oluşturulurken gerekir.
      2. Belirtin **Windows Server 2012 R2** hello işletim sistemi ailesi ayarı için.
      3. Seçin bir **düğüm fiyatlandırma katmanı**.
      4. Girin **2** hello için değer olarak **hedef ayrılmış** ayarı.
      5. Girin **2** hello için değer olarak **en fazla düğüm başına görevleri** ayarı.
   5. Tıklatın **Tamam** toocreate hello havuzu.
   6. Merhaba Not **kimliği** hello havuzunun. 



### <a name="high-level-steps"></a>Üst düzey adımlar
Bu kılavuz kapsamında gerçekleştirme hello iki üst düzey adımlar şunlardır: 

1. Basit veri dönüştürme/işleme mantığı içeren özel bir aktivite oluşturun.
2. Bir Azure data factory hello özel etkinlik kullanan bir sahip işlem hattı oluşturacaksınız.

### <a name="create-a-custom-activity"></a>Özel etkinlik oluşturma
toocreate .NET özel etkinlik oluşturmak bir **.NET sınıf kitaplığı** uygulayan bir sınıf projeyle **IDotNetActivity** arabirimi. Bu arabirim yalnızca bir yöntemi vardır: [yürütme](https://msdn.microsoft.com/library/azure/mt603945.aspx) ve imzası:

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


Merhaba yöntemi dört parametreleri alır:

- **linkedServices**. Bu özellik, veri deposu bağlı Hizmetleri hello etkinlik için giriş/çıkış veri kümesi tarafından başvurulan numaralandırılabilir listesidir.   
- **veri kümeleri**. Bu özellik hello etkinlik için giriş/çıkış veri kümesi numaralandırılabilir bir listesi verilmiştir. Bu parametre tooget hello konumları ve girdi ve çıktı veri kümeleri tarafından tanımlanan şemaları kullanabilir.
- **Etkinlik**. Bu özellik hello geçerli etkinliği temsil eder. Kullanılan tooaccess genişletilmiş özellikler hello özel etkinlik ile ilişkili olabilir. Bkz: [genişletilmiş özellikler erişim](#access-extended-properties) Ayrıntılar için.
- **Günlükçü**. Bu nesne hello ardışık düzeni için başlangıç kullanıcı günlüğünde bu yüzeyini hata ayıklama açıklamaları yazmanızı sağlar.

Merhaba yöntemi kullanılan toochain özel etkinlikler birlikte hello gelecekte olabilir bir sözlüğü döndürür. Bu özellik henüz uygulanmadı, bu nedenle boş bir sözlük hello döndürme.  

### <a name="procedure"></a>Yordam
1. Oluşturma bir **.NET sınıf kitaplığı** projesi.
   <ol type="a">
     <li>Başlatma <b>Visual Studio 2017</b> veya <b>Visual Studio 2015</b> veya <b>Visual Studio 2013'ün</b> veya <b>Visual Studio 2012</b>.</li>
     <li>Tıklatın <b>dosya</b>, çok noktası<b>yeni</b>, tıklatıp <b>proje</b>.</li>
     <li><b>Şablonlar</b>’ı genişletin ve <b>Visual C#</b> seçeneğini belirleyin. Bu kılavuzda, C# kullanın, ancak .NET dil toodevelop hello özel etkinlik kullanabilirsiniz.</li>
     <li>Seçin <b>sınıf kitaplığı</b> hello sağ proje türlerinde hello listesinden. VS 2017 ' seçin <b>sınıf kitaplığı (.NET Framework)</b> </li>
     <li>Girin <b>MyDotNetActivity</b> hello için <b>adı</b>.</li>
     <li>Seçin <b>C:\ADFGetStarted</b> hello için <b>konumu</b>.</li>
     <li>Tıklatın <b>Tamam</b> toocreate hello projesi.</li>
   </ol>
2.Tıklatın **Araçları**, çok noktası**NuGet Paket Yöneticisi**, tıklatıp **Paket Yöneticisi Konsolu**.
3. Komut tooimport aşağıdaki hello Hello Paket Yöneticisi konsolu, yürütme **Microsoft.Azure.Management.DataFactories**.

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. İçeri aktarma hello **Azure Storage** toohello projesinde NuGet paketi.

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > Veri Fabrikası Başlatıcı WindowsAzure.Storage hello 4.3 sürümünü gerektirir. Bir başvuru tooa eklerseniz, sonraki bir sürümünü özel etkinlik projenizdeki Azure Storage derlemenin hata hello etkinlik yürüttüğünde bakın. tooresolve hello hata bkz [Appdomain yalıtım](#appdomain-isolation) bölümü. 
5. Merhaba aşağıdakileri ekleyin **kullanarak** deyimleri toohello kaynak hello proje dosyasında.

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Değişiklik hello hello adını **ad alanı** çok**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Merhaba sınıfı Hello adı çok değiştirmek**MyDotNetActivity** ve hello türetilen **IDotNetActivity** arabirim hello aşağıdaki kod parçacığında gösterildiği gibi:

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Uygulama (Ekle) hello **yürütme** hello yöntemi **IDotNetActivity** toohello arabirim **MyDotNetActivity** örnek kodu toohello yöntemi aşağıdaki sınıf ve kopyalama hello.

    Merhaba aşağıdaki örnek hello hello arama terimi ("Microsoft") oluşumları veri dilimi ile ilişkili her bir blob içinde sayar.

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
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
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
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
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
9. Yardımcı yöntemler aşağıdaki hello ekleyin: 

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

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
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
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
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

    dataset hello hello GetFolderPath yöntemi döndürür hello yolu toohello klasörü tooand hello GetFileName yöntemi döndürür hello hello blob/dataset noktalarına hello dosyasının adını işaret eder. {Year} gibi değişkenler kullanarak, havefolderPath tanımlıyorsa {Month}, {Day} vb., hello yöntemi döndürür hello dizesi çalışma zamanı değerlerle değiştirmeden olduğu gibi. Bkz: [genişletilmiş özellikler erişim](#access-extended-properties) erişme SliceStart, SliceEnd, vb. ile ilgili ayrıntılar için bölüm.    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    Merhaba hesapla yöntemi hello anahtar sözcüğü hello giriş dosyaları (BLOB hello klasöründe) Microsoft örneklerinin sayısını hesaplar. Merhaba kodda sabit kodlanmış Hello arama terimi ("Microsoft").
10. Merhaba projeyi derleyin. Tıklatın **yapı** hello menüsüne ve ardından gelen **yapı çözümü**.

    > [!IMPORTANT]
    > Projeniz için hello hedef çerçeve olarak .NET Framework 4.5.2 kümesi sürümü: hello projesine sağ tıklayın ve **özellikleri** tooset hello hedef çerçevesi. Veri Fabrikası karşı .NET Framework sürüm 4.5.2 daha sonra derlenmiş özel etkinlikler desteklemez.

11. Başlatma **Windows Explorer**, giderek çok**bin\debug** veya **bin\release** klasör yapısının hello türüne bağlı olarak.
12. Zip dosyası oluşturma **MyDotNetActivity.zip** hello içindeki tüm hello ikili dosyaları içeren <project folder>\bin\Debug klasörünü. Merhaba dahil **MyDotNetActivity.pdb** başarısız olduysa, hello soruna neden hello kaynak kodunda satır numarası gibi ek ayrıntıları almak için dosya. 

    > [!IMPORTANT]
    > Merhaba özel etkinlik hello olmalıdır tüm dosyaları hello zip dosyasında hello **üst düzey** hiçbir alt klasörler ile.

    ![İkili çıktı dosyaları](./media/data-factory-use-custom-activities/Binaries.png)
14. Adlı bir blob kapsayıcı oluşturun **customactivitycontainer** zaten yoksa. 
15. İçinde bir blob toohello customactivitycontainer olarak MyDotNetActivity.zip karşıya bir **genel amaçlı** AzureStorageLinkedService tarafından başvurulan Azure blob storage (değil seyrek/cool Blob Depolama).  

> [!IMPORTANT]
> Visual Studio'da bir Data Factory projesi içeren bu .NET etkinliği proje tooa çözümü ekleyin ve bir başvuru too.NET etkinlik proje hello Data Factory uygulama projeden eklerseniz, el ile oluşturma tooperform hello son iki adımı gerekmez Merhaba zip dosyası ve toohello genel amaçlı Azure blob depolama karşıya yükleme. Visual Studio kullanarak Data Factory varlıklarını yayımladığınızda, şu adımları yayımlama hello işlem tarafından otomatik olarak yapılır. Daha fazla bilgi için bkz: [Visual Studio Data Factory projesindeki](#data-factory-project-in-visual-studio) bölümü.

## <a name="create-a-pipeline-with-custom-activity"></a>Özel etkinliği ile işlem hattı oluşturma
Özel bir aktivite oluşturulur ve hello ZIP dosyasının ikilileri tooa blob kapsayıcısında ile karşıya bir **genel amaçlı** Azure depolama hesabı. Bu bölümde, bir Azure data factory hello özel etkinlik kullanan sahip işlem hattı oluşturun.

Merhaba hello özel etkinlik için giriş veri kümesi hello blob depolamada adftutorial kapsayıcısının hello customactivityinput klasöründeki BLOB'lar (dosyaları) temsil eder. Merhaba çıktı veri kümesi hello etkinliğinin çıkış BLOB'lar hello blob depolamada adftutorial kapsayıcısının hello customactivityoutput klasöründeki temsil eder.

Oluşturma **dosya.txt'yi** aşağıdaki içerik ve çok karşıya hello dosyasıyla**customactivityinput** hello klasörünü **adftutorial** kapsayıcı. Zaten yoksa hello adftutorial kapsayıcı oluşturun. 

```
test custom activity Microsoft test custom activity Microsoft
```

Başlangıç klasörü iki veya daha fazla dosya olsa bile hello giriş klasörü Azure Data Factory tooa dilimi karşılık gelir. Her dilim hello ardışık düzen tarafından işlendiğinde hello özel etkinlik bu dilim için hello giriş klasöründeki tüm hello BLOB'lar dolaşır.

Bir veya daha fazla satırlara sahip (Merhaba giriş klasörü blobları sayısı ile aynı) dosyası ile Merhaba adftutorial\customactivityoutput klasöründe bir çıkış bakın:

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


Bu bölümde gerçekleştirmek hello adımlar şunlardır:

1. Oluşturma bir **veri fabrikası**.
2. Oluşturma **bağlantılı Hizmetleri** hello Azure Batch havuzu Hangi hello özel etkinlik çalıştırır ve giriş/çıkış BLOB'lar hello tutan Azure Storage hello VM'ler için.
3. Giriş ve çıkış oluşturma **veri kümeleri** giriş ve çıkış hello özel etkinliği temsil eden.
4. Oluşturma bir **ardışık düzen** hello özel etkinlik kullanır.

> [!NOTE]
> Merhaba oluşturma **dosya.txt'yi** ve zaten yapmadıysanız tooa blob kapsayıcısı yükleyin. Önceki bölümde hello bulunan yönergelere bakın.   

### <a name="step-1-create-hello-data-factory"></a>1. adım: hello veri fabrikası oluşturma
1. Azure portalı içinde toohello oturum sonra aşağıdaki adımları hello:
   1. Tıklatın **yeni** hello sol menüdeki.
   2. Tıklatın **veri + analiz** hello içinde **yeni** dikey.
   3. Tıklatın **Data Factory** hello üzerinde **veri analizi** dikey.
   
    ![Yeni Azure Data Factory menüsü](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. Merhaba, **yeni data factory** dikey penceresinde girin **CustomActivityFactory** hello adı için. Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir. Merhaba hatayı alırsanız: **veri fabrikası adı "CustomActivityFactory" kullanılabilir değil**, hello veri fabrikası hello adını değiştirin (örneğin, **yournameCustomActivityFactory**) ve oluşturmayı deneyin yeniden.

    ![Yeni Azure Data Factory dikey penceresi](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. Tıklatın **kaynak grubu adı**, varolan bir kaynak grubu seçin veya bir kaynak grubu oluşturun.
4. Merhaba doğru kullandığınızdan emin olun **abonelik** ve **bölge** oluşturulan hello veri fabrikası toobe istediğiniz.
5. Tıklatın **oluşturma** hello üzerinde **yeni data factory** dikey.
6. Hello oluşturulmakta hello veri fabrikası gördüğünüz **Pano** hello Azure portal.
7. Merhaba veri fabrikası başarıyla oluşturulduktan sonra gösterir hello Data Factory dikey bkz hello hello data Factory içeriği.
    
    ![Data Factory dikey penceresi](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a>2. adım: bağlı hizmetler oluşturma
Bağlı hizmetler veri depolarını veya hizmetleri tooan Azure data factory işlem. Bu adımda, Azure Storage hesabını ve Azure Batch hesabı tooyour veri fabrikası bağlayın.

#### <a name="create-azure-storage-linked-service"></a>Azure Storage bağlı hizmeti oluşturma
1. Merhaba tıklatın **yazar ve dağıtma** döşeme hello üzerinde **DATA FACTORY** dikey **CustomActivityFactory**. Merhaba Data Factory Düzenleyici bakın.
2. Tıklatın **yeni veri deposu** hello komut çubuğu ve seçin **Azure depolama**. Görmeniz gerekir hello Azure depolama alanı oluşturmak için JSON betiği bağlantılı hizmeti hello düzenleyicisinde.
    
    ![Yeni veri deposu - Azure depolama](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. Değiştir `<accountname>` Azure depolama hesabınızın adıyla ve `<accountkey>` hello Azure depolama hesabı erişim anahtarı ile. toolearn tooget depolama alanınızın nasıl erişim anahtar, bkz: [erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma depolama](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

    ![Azure depolama hizmeti beğendiğinizi](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.

#### <a name="create-azure-batch-linked-service"></a>Azure Batch bağlı hizmet oluşturma
1. Hello Data Factory Düzenleyici'de, tıklatın **... Daha fazla** hello komut çubuğunda **yeni işlem**ve ardından **Azure Batch** hello menüsünde.

    ![Yeni işlem - Azure toplu işlem](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. Değişiklikleri toohello JSON betiği aşağıdaki hello olun:

   1. Hello için Azure Batch hesabı adı belirtin **accountName** özelliği. Merhaba **URL** hello gelen **Azure Batch hesabı dikey** biçimini izleyen hello olduğu: `http://accountname.region.batch.azure.com`. Hello için **batchUri** özelliğinde hello JSON, tooremove gerek `accountname.` hello URL ve kullanım hello gelen `accountname` hello için `accountName` JSON özelliği.
   2. Merhaba Hello Azure Batch hesabı anahtar belirtmeniz **accessKey** özelliği.
   3. Merhaba önkoşulları bir parçası olarak oluşturduğunuz hello havuzunu Hello adını belirtin **poolName** özelliği. Hello hello havuzu hello havuzunun hello adı yerine Kimliğini de belirtebilirsiniz.
   4. Azure Batch URI Merhaba belirtin **batchUri** özelliği. Örnek: `https://westus.batch.azure.com`.  
   5. Merhaba belirtin **AzureStorageLinkedService** hello için **linkedServiceName** özelliği.

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       Hello için **poolName** özelliği, hello hello havuzu hello havuzunun hello adı yerine Kimliğini de belirtebilirsiniz.

      > [!IMPORTANT]
      > Hdınsight için yaptığı gibi hello Data Factory hizmeti Azure toplu işlem için bir isteğe bağlı seçeneği desteklemiyor. Bu gibi durumlarda, kendi Azure Batch havuzu yalnızca bir Azure data factory kullanabilirsiniz.   
    

### <a name="step-3-create-datasets"></a>3. adım: veri kümeleri oluşturma
Bu adımda, veri kümeleri toorepresent girişi oluşturun ve çıktı verilerini.

#### <a name="create-input-dataset"></a>Girdi veri kümesi oluşturma
1. Merhaba, **Düzenleyicisi** hello Data Factory tıklatın **... Daha fazla** hello komut çubuğunda **yeni veri kümesi**ve ardından **Azure Blob Depolama** hello açılan menüsünden.
2. Merhaba JSON hello sağ bölmedeki JSON parçacığı aşağıdaki hello ile değiştirin:

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
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

   Başlangıç saati ile bu kılavuzda daha sonra bir işlem hattı oluşturma: 2016-11-16T00:00:00Z ve bitiş zamanı: 2016-11-16T05:00:00Z. Beş giriş/çıkış dilimler olduklarından, zamanlanmış tooproduce saatlik, verilerdir (arasında **00**: 00:00 -> **05**: 00:00).

   Merhaba **sıklığı** ve **aralığı** hello girdi veri kümesi çok ayarlamak için**saat** ve **1**, o hello başka bir deyişle, dilim kullanılabilir giriş saatlik. Bu örnekte, aynı hello olduğu hello intputfolder (dosya.txt'yi) dosyasında.

   Burada, JSON parçacığı yukarıda hello SliceStart sistem değişkeni tarafından temsil edilen her dilim için hello başlangıç zamanlarını bulunmaktadır.
3. Tıklatın **dağıtma** araç toocreate hello ve hello dağıtmak **InputDataset**. Merhaba gördüğünüzü onaylayın **tablo başarıyla oluşturuldu** hello başlık çubuğundaki hello Düzenleyicisi ileti.

#### <a name="create-an-output-dataset"></a>Çıktı veri kümesi oluşturma
1. Merhaba, **Data Factory düzenleyici**, tıklatın **... Daha fazla** hello komut çubuğunda **yeni veri kümesi**ve ardından **Azure Blob Depolama**.
2. Merhaba JSON betiği hello sağ bölmedeki JSON betiği aşağıdaki hello ile değiştirin:

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
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

     Çıktı konumu **adftutorial/customactivityoutput/** ve çıktı dosyası adını yyyy-aa-gg-HH.txt yyyy-aa-gg-HH hello yıl, ay, tarih ve saat üretilen hello dilimin olduğu. Bkz: [Geliştirici Başvurusu] [ adf-developer-reference] Ayrıntılar için.

    Bir çıkış blob/dosyası, her girdi dilimi için oluşturulur. İşte bir çıktı dosyası için her dilimi nasıl adlandırılır. Bir çıkış klasöründe oluşturulan tüm hello çıktı dosyaları: **adftutorial\customactivityoutput**.

   | Dilim | Başlangıç zamanı | Çıkış dosyası |
   |:--- |:--- |:--- |
   | 1 |2016-11-16T00:00:00 |2016-11-16-00.txt |
   | 2 |2016-11-16T01:00:00 |2016-11-16-01.txt |
   | 3 |2016-11-16T02:00:00 |2016-11-16-02.txt |
   | 4 |2016-11-16T03:00:00 |2016-11-16-03.txt |
   | 5 |2016-11-16T04:00:00 |2016-11-16-04.txt |

    Giriş bir klasördeki tüm hello dosyaları hello başlangıç zamanlarını yukarıda belirtilen dilimle parçası olduğunu unutmayın. Bu dilim işlendiğinde hello özel etkinlik her dosyası aracılığıyla tarar ve arama terimi ("Microsoft") oluşumları hello sayısıyla hello çıkış dosyasındaki bir satır üretir. Merhaba inputfolder üç dosya varsa vardır üç satır hello çıktı dosyasında her saat dilimi: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, vs.
3. toodeploy hello **OutputDataset**, tıklatın **dağıtma** hello komut çubuğunda.

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a>Oluşturma ve hello özel etkinlik kullanan bir ardışık düzen çalıştırma
1. Hello Data Factory Düzenleyici'de, tıklatın **... Daha fazla**ve ardından **yeni işlem hattı** hello komut çubuğunda. 
2. Merhaba JSON hello sağ bölmedeki JSON betiği aşağıdaki hello ile değiştirin:

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    Hello aşağıdaki noktaları göz önünde bulundurun:

   * **Eşzamanlılık** çok ayarlanır**2** böylece iki dilimler hello Azure Batch havuzunda 2 VM tarafından paralel olarak işlenir.
   * Merhaba etkinlikler bölümünde bir etkinlik olduğunu ve türü: **DotNetActivity**.
   * **AssemblyName** hello DLL toohello adına ayarlanır: **MyDotnetActivity.dll**.
   * **EntryPoint** çok ayarlanır**MyDotNetActivityNS.MyDotNetActivity**.
   * **PackageLinkedService** çok ayarlanır**AzureStorageLinkedService** hello özel etkinlik zip dosyasını içeren toohello blob depolama işaret eder. Kullanıyorsanız farklı Azure depolama hesapları için giriş/çıkış dosyalarını ve hello özel etkinlik zip dosyası, başka bir Azure depolama bağlantılı hizmeti oluşturun. Bu makalede, kullanmakta olduğunuz varsayılmaktadır hello aynı Azure depolama hesabı.
   * **PackageFile** çok ayarlanır**customactivitycontainer/MyDotNetActivity.zip**. Merhaba biçimdedir: containerforthezip/nameofthezip.zip.
   * Merhaba özel etkinlik alır **InputDataset** giriş olarak ve **OutputDataset** çıktı olarak.
   * Merhaba linkedServiceName hello özel etkinlik özelliğinin işaret toohello **AzureBatchLinkedService**, o hello özel etkinliği Azure Data Factory söyleyen Azure toplu işlemi vm'lerinde toorun gerekir.
   * **isPaused** özelliği çok ayarlanmış**false** varsayılan olarak. Hello dilimler hello geçmiş başlatmak için hello ardışık düzen hemen bu örnekte çalışır. Bu özellik tootrue toopause hello ardışık düzen ve geri toofalse toorestart ayarlayın.
   * Merhaba **Başlat** zaman ve **son** sürelerinin **beş** hello ardışık düzen tarafından beş dilimlerinin şekilde birbirinden saatleri ve dilimler saatlik, üretilmektedir.
3. toodeploy hello ardışık tıklatın **dağıtma** hello komut çubuğunda.

### <a name="monitor-hello-pipeline"></a>Merhaba işlem hattını izleme
1. Hello Azure portal'ın Hello Data Factory dikey penceresinde tıklayın **diyagramı**.

    ![Diyagram kutucuğu](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. Hello diyagram Görünümü'da, artık hello OutputDataset'ı tıklatın.

    ![Diyagram görünümü](./media/data-factory-use-custom-activities/diagram.png)
3. Merhaba beş çıkış dilimler hello hazır durumda olduğunu görmeniz gerekir. Bunlar hello hazır durumda değilse, bunlar henüz üretilmiş henüz. 

   ![Çıktı dilimleri](./media/data-factory-use-custom-activities/OutputSlices.png)
4. Merhaba çıktı dosyaları hello hello blob depolamada oluşturulan doğrulayın **adftutorial** kapsayıcı.

   ![Özel etkinliğinden çıktı][image-data-factory-ouput-from-custom-activity]
5. Merhaba çıktı dosyası açarsanız, çıktı aşağıdaki benzer toohello hello çıktı görmeniz gerekir:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. Kullanım hello [Azure portal] [ azure-preview-portal] ya da Azure PowerShell cmdlet'leri toomonitor veri fabrikası, ardışık düzen ve veri kümeleri. Merhaba gelen iletileri görebilirsiniz **ActivityLogger** ' hello kodunda hello özel etkinlik hello portal veya cmdlet'ler kullanarak indirebilir hello günlüklerinde (özellikle kullanıcı-0.log).

   ![Özel etkinliğinden günlüklerini indirin][image-data-factory-download-logs-from-custom-activity]

Bkz: [izleme ve yönetme ardışık düzen](data-factory-monitor-manage-pipelines.md) veri kümelerini ve işlem hatlarını izleme için ayrıntılı adımlar için.      

## <a name="data-factory-project-in-visual-studio"></a>Visual Studio Data Factory projesi  
Oluşturma ve Azure portalını kullanarak yerine Visual Studio kullanarak Data Factory varlıklarını yayımlama. Visual Studio kullanarak Data Factory varlıklarını yayımlama, bakın ve ayrıntılı oluşturma hakkında daha fazla bilgi için [Visual Studio kullanarak ilk işlem hattınızı oluşturma](data-factory-build-your-first-pipeline-using-vs.md) ve [SQL Azure Blob tooAzure veri kopyalama](data-factory-copy-activity-tutorial-using-visual-studio.md) makaleler.

Visual Studio'da veri fabrikası proje oluşturuyorsanız, aşağıdaki ek adımları hello:
 
1. Merhaba Data Factory projesi toohello hello özel etkinlik projeyi içeren Visual Studio çözümü ekleyin. 
2. Bir başvuru toohello .NET etkinliği proje hello Data Factory projeden ekleyin. Data Factory projesine sağ tıklayın, çok noktası**Ekle**ve ardından **başvuru**. 
3. Merhaba, **Başvuru Ekle** iletişim kutusu, select hello **MyDotNetActivity** proje öğesini tıklatıp **Tamam**.
4. Derleme ve hello çözüm yayımlayın.

    > [!IMPORTANT]
    > Data Factory varlıklarını yayımladığınızda, ZIP dosyası sizin için otomatik olarak oluşturulur ve karşıya yüklenen toohello blob kapsayıcı: customactivitycontainer. Merhaba blob kapsayıcısı mevcut değilse otomatik olarak çok oluşturulur.  


## <a name="data-factory-and-batch-integration"></a>Veri Fabrikası ve toplu tümleştirmesi
Hello Data Factory hizmetinin hello adı ile Azure toplu işleminde bir işi oluşturur: **adf poolname: iş xxx**. Tıklatın **işleri** hello sol menüden. 

![Azure Data Factory - toplu işler](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

Bir görev, her bir dilim etkinlik çalıştırması için oluşturulur. İşlenen beş dilim hazır toobe varsa, beş görev alanında bu işin oluşturulur. Merhaba Batch havuzu birden çok işlem düğümleri varsa, iki veya daha fazla dilim paralel olarak çalıştırılabilir. İşlem başına en fazla görevlerini Hello düğüm kümesi varsa çok > 1, ayrıca hello üzerinde çalışan birden fazla dilim sağlayabilirsiniz aynı işlem.

![Azure Data Factory - toplu iş görevleri](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

Diyagram aşağıdaki hello hello Azure Data Factory ve toplu işlem görevlerini arasındaki ilişki gösterilmektedir.

![Veri Fabrikası & toplu işlem](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a>Hatalarını giderme
Sorun giderme birkaç temel teknikleri oluşur:

1. Aşağıdaki hata hello görürseniz, bir etkin/Cool blob depolama genel amaçlı Azure blob storage kullanarak yerine kullanıyor olabilir. Merhaba zip dosyası tooa karşıya **genel amaçlı Azure depolama hesabı**. 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. Aşağıdaki hata hello görürseniz, bu hello adını hello CS dosya eşleşen hello adı hello için belirttiğiniz hello sınıfının onaylayın **EntryPoint** JSON hello düzenindeki özelliği. Merhaba kılavuzda hello sınıfı adıdır: MyDotNetActivity ve hello JSON hello EntryPoint: MyDotNetActivityNS. **MyDotNetActivity**.

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   Merhaba adları eşleşiyorsa, bu tüm hello ikili dosyaları hello doğrulayın **kök klasörü** hello ZIP dosyasının. Diğer bir deyişle, hello zip dosyası açtığınızda, tüm hello dosyaları hello kök klasöründe, tüm alt klasörlerde görmeniz gerekir.   
3. Merhaba girdi dilimi çok ayarlanmamışsa**hazır**, hello giriş klasör yapısı doğru olduğunu onaylayın ve **dosya.txt'yi** hello giriş klasörlerde bulunmaktadır.
3. Merhaba, **yürütme** özel etkinliklerinizi, kullanım hello yöntemi **IActivityLogger** yardımcı olan nesne toolog bilgileri sorunları giderme. oturum hello iletileri göster hello kullanıcı günlük dosyalarında (adlı bir veya daha fazla: kullanıcı 0.log, kullanıcı 1.log, kullanıcı 2.log vb..).

   Merhaba, **OutputDataset** dikey penceresinde hello dilim toosee hello tıklatın **veri DİLİMİ** dikey penceresinde, dilim için. Gördüğünüz **etkinlik çalışması** bu dilim için. Merhaba dilim için bir etkinlik görmeniz gerekir. Merhaba komut çubuğunda Çalıştır'ı tıklatın, hello için başka bir etkinlik başlatabilirsiniz aynı dilim.

   Merhaba etkinlik tıklattığınızda hello bkz **etkinlik çalışma ayrıntıları** günlük dosyalarının listesini içeren dikey. Merhaba user_0.log dosyasında günlüğe kaydedilen iletilere bakın. Hata oluştuğunda hello yeniden deneme sayısı hello ardışık düzen/JSON etkinliğinde too3 ayarlandığından üç Etkinlik çalışması bakın. Merhaba etkinlik tıklattığınızda tootroubleshoot hello hata inceleyebilirsiniz hello günlük dosyalarına bakın.

   Günlük dosyaları Hello listesinde hello tıklayın **kullanıcı 0.log**. Merhaba sağ panelde hello kullanarak hello sonucu olan **IActivityLogger.Write** yöntemi. Tüm iletileri görmüyorsanız adlı daha fazla günlük dosyaları olup olmadığını denetleyin: user_1.log, user_2.log vs. Son oturum açan ileti Hello sonra Aksi takdirde hello kod başarısız olmuş olabilir.

   Ayrıca, denetleme **sistem 0.log** sistem hata iletileri ve özel durumlar için.
4. Merhaba dahil **PDB** hello hata ayrıntıları bilgileri gibi böylece hello zip dosyasında dosya **çağrı yığını** bir hata oluştuğunda.
5. Merhaba özel etkinlik hello olmalıdır tüm dosyaları hello zip dosyasında hello **üst düzey** hiçbir alt klasörler ile.
6. Bu hello olun **assemblyName** (MyDotNetActivity.dll) **entryPoint**(MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) ve **packageLinkedService** (toohello işaret etmelidir **genel amaçlı**hello zip dosyasını içeren Azure blob depolama) toocorrect değerlerini ayarlayın.
7. Bir hata ve istediğiniz tooreprocess hello dilim sabit, hello hello dilimi sağ **OutputDataset** tıklayın ve dikey **çalıştırmak**.
8. Aşağıdaki hata hello görürseniz, hello Azure Storage paketi sürümü > 4.3.0 kullanıyor. Veri Fabrikası Başlatıcı WindowsAzure.Storage hello 4.3 sürümünü gerektirir. Bkz: [Appdomain yalıtım](#appdomain-isolation) bölümünde bir iş-geçici bir çözüm için hello kullanmanız gerekiyorsa Azure Storage derlemenin sonraki bir sürümü. 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    Azure Storage paket hello 4.3.0 sürümünü kullanabilirsiniz, hello varolan başvuru tooAzure depolama paketi sürümü > 4.3.0 kaldırın. Ardından, NuGet Paket Yöneticisi Konsolu'ndan komutu aşağıdaki hello çalıştırın. 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    Merhaba projeyi oluşturun. Sürüm > 4.3.0 Azure.Storage bütünleştirilmiş hello klasörüne silin. Bir zip dosyası ikili dosyaları ve hello PDB dosyası oluşturun. Bu bir hello blob kapsayıcısında (customactivitycontainer) Hello eski zip dosyasını değiştirin. Yeniden çalıştırılan hello başarısız olan dilimler (dilim sağ tıklatın ve Çalıştır'ı tıklatın).   
8. Merhaba özel etkinlik hello kullanmaz **app.config** paketinizi dosyasından. Bu nedenle, kodunuzu hello yapılandırma dosyasından bağlantı dizelerini yazıyorsa, çalışma zamanında çalışmıyor. Azure Batch kullanarak toohold olduğunda en iyi yöntem herhangi parolalarında hello bir **Azure KeyVault**, sertifika tabanlı hizmet asıl tooprotect hello kullan **keyvault**ve hello sertifika dağıtın tooAzure Batch havuzu. .NET özel etkinlik hello sonra gizli hello KeyVault çalışma zamanında erişebilirsiniz. Bu çözüm genel bir çözümdür ve gizli anahtarı, yalnızca bağlantı dizesi tooany türü ölçeklendirebilirsiniz.

   Daha kolay bir çözüm (ancak en iyi yöntem değildir): oluşturabileceğiniz bir **Azure SQL bağlı hizmeti** bağlantı dizesi ayarlarıyla kullanır bağlantılı hizmet ve sahte bir giriş veri kümesi olarak zinciri hello dataset hello bir veri kümesi oluşturma toohello özel .NET etkinlik. Hizmetin bağlantı dizesi hello özel etkinlik kodda erişim hello bağlı sonra kullanabilirsiniz.  

## <a name="update-custom-activity"></a>Özel Etkinlik güncelleştirme
Merhaba özel etkinlik hello kodunu güncelleştirirseniz, onu oluşturmak ve yeni ikili dosyaları toohello blob depolama içeren hello zip dosyasını karşıya yükleyin.

## <a name="appdomain-isolation"></a>Uygulama etki alanı yalıtımı
Bkz: [arası AppDomain örnek](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) , nasıl toocreate değil özel bir aktivite hello Data Factory başlatıcısı tarafından kullanılan tooassembly sürümleri kısıtlı gösterir (örnek: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x vb..).

## <a name="access-extended-properties"></a>Genişletilmiş özellikler erişim
Hello örnek aşağıdaki gösterildiği gibi JSON hello etkinliğinde genişletilmiş özellikler bildirimini yapabilir:

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


Merhaba örnekte iki genişletilmiş özelliği vardır: **SliceStart** ve **DataFactoryName**. Merhaba değer SliceStart için hello SliceStart sistem değişkeni temel alır. Bkz: [sistem değişkenleri](data-factory-functions-variables.md) desteklenen sistem değişkenleri listesi. Merhaba DataFactoryName sabit kodlanmış tooCustomActivityFactory değeridir.

tooaccess, bu genişletilmiş hello özelliklerinde **yürütme** yöntemi, kullanım kodunu benzer toohello koddan:

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a>Azure batch otomatik olarak ölçeklendirme
Bir Azure Batch havuzuyla oluşturabilirsiniz **otomatik ölçeklendirme** özelliği. Örneğin, 0 özel VM'ler ve bekleyen görevler, hello sayısına dayalı bir otomatik ölçeklendirme formülü ile bir azure batch havuzu oluşturabilirsiniz. 

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

## <a name="use-hdinsight-compute-service"></a>Hdınsight işlem hizmeti kullanın
Merhaba kılavuzda Azure toplu işlem toorun hello özel etkinlik kullanılır. Ayrıca, kendi Windows tabanlı Hdınsight kümesi kullanın veya hello özel etkinlik hello Hdınsight kümesi üzerinde çalışan bir isteğe bağlı Windows tabanlı Hdınsight kümesi oluşturursanız ve veri fabrikası sahip. Hdınsight kümesi kullanma için hello üst düzey adımları şunlardır.

> [!IMPORTANT]
> Merhaba özel .NET etkinlikler yalnızca Windows tabanlı Hdınsight kümelerinde çalıştırın. Bu sınırlama aşağıdaki haller için geçici çözüm toouse hello harita azaltmak etkinlik toorun özel Java kod Linux tabanlı Hdınsight kümesi üzerinde ' dir. Toouse VM'ler toorun özel etkinlikler bir Hdınsight kümesi yerine bir Azure Batch havuzu başka bir seçenektir.
 

1. Bir Azure Hdınsight bağlı hizmeti oluşturma.   
2. Kullanım Hdınsight bağlantılı hizmeti yerine **AzureBatchLinkedService** hello JSON kanalı.

Tootest istiyorsanız bunu hello kılavuza, değişiklik **Başlat** ve **son** böylece hello Azure Hdınsight hizmeti ile Merhaba senaryosu test hello ardışık düzeni için zaman.

#### <a name="create-azure-hdinsight-linked-service"></a>Azure HDInsight bağlı hizmeti oluşturma
Hello Azure Data Factory hizmetine bir istek üzerine küme oluşturmayı destekler ve tooprocess giriş tooproduce çıktı verileri kullanın. Ayrıca kendi kümenizi kullanabilirsiniz tooperform hello aynı. İsteğe bağlı Hdınsight kümesi kullandığınızda, bir küme için her bir dilim oluşturulan. Kendi Hdınsight kümenizi kullanırsanız, hello küme hazır iken tooprocess dilim hemen hello. İsteğe bağlı küme kullandığınızda, bu nedenle, hello çıktı verilerini kendi kümenizi kullandığınızda, olabildiğince çabuk göremeyebilirsiniz.

> [!NOTE]
> Çalışma zamanında .NET etkinliği bir örneği yalnızca bir çalışan düğümünde hello Hdınsight kümesi çalıştırılır; birden çok düğümde ölçeklendirilmiş toorun olamaz. .NET etkinliği birden çok örneğini farklı hello Hdınsight küme düğümlerinde paralel olarak çalıştırılabilir.
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a>toouse isteğe bağlı Hdınsight kümesi
1. Merhaba, **Azure portal**, tıklatın **geliştir ve Dağıt** hello Data Factory giriş sayfasında.
2. Hello Data Factory Düzenleyici'de, tıklatın **yeni işlem** hello komut çubuğu ve select **isteğe bağlı Hdınsight kümesi** hello menüsünde.
3. Değişiklikleri toohello JSON betiği aşağıdaki hello olun:

   1. Hello için **clusterSize** özelliği, hello hello Hdınsight küme boyutunu belirtin.
   2. Hello için **timeToLive** özelliği, silinmeden önce ne kadar süreyle hello müşteri süreyle boşta kalabileceğini belirtin.
   3. Hello için **sürüm** özelliği, toouse istediğiniz hello Hdınsight sürüm belirtin. Bu özellik bıraksanız hello en son sürümü kullanılır.  
   4. Hello için **linkedServiceName**, belirtin **AzureStorageLinkedService**.

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > Merhaba özel .NET etkinlikler yalnızca Windows tabanlı Hdınsight kümelerinde çalıştırın. Bu sınırlama aşağıdaki haller için geçici çözüm toouse hello harita azaltmak etkinlik toorun özel Java kod Linux tabanlı Hdınsight kümesi üzerinde ' dir. Toouse VM'ler toorun özel etkinlikler bir Hdınsight kümesi yerine bir Azure Batch havuzu başka bir seçenektir.

4. Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.

##### <a name="toouse-your-own-hdinsight-cluster"></a>toouse kendi Hdınsight kümenizi:
1. Merhaba, **Azure portal**, tıklatın **geliştir ve Dağıt** hello Data Factory giriş sayfasında.
2. Merhaba, **Data Factory düzenleyici**, tıklatın **yeni işlem** hello komut çubuğu seçin ve **Hdınsight kümesi** hello menüsünde.
3. Değişiklikleri toohello JSON betiği aşağıdaki hello olun:

   1. Hello için **clusterUri** özelliği, Hdınsight için hello URL'sini girin. Örneğin: https://<clustername>.azurehdinsight.net/     
   2. Hello için **kullanıcıadı** özelliği, erişim toohello Hdınsight kümesine sahip hello kullanıcı adı girin.
   3. Hello için **parola** özelliği, hello kullanıcı için hello parola girin.
   4. Hello için **LinkedServiceName** özelliği girin **AzureStorageLinkedService**.
4. Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.

Bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md) Ayrıntılar için.

Merhaba, **JSON kanal**, Hdınsight kullanma (isteğe bağlı veya kendi) bağlantılı hizmeti:

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a>.NET SDK kullanarak bir özel etkinlik oluşturma
Bu makalede Hello kılavuzda hello Azure portal kullanarak hello özel etkinlik kullanan bir ardışık düzen ile bir veri fabrikası oluşturun. koddan hello nasıl toocreate hello veri fabrikası .NET SDK kullanarak gösterir. SDK tooprogrammatically kullanma hakkında daha fazla ayrıntı hello işlem hatlarını oluşturmak bulabilirsiniz [.NET API kullanarak kopyalama etkinliği ile işlem hattı oluşturma](data-factory-copy-activity-tutorial-using-dotnet-api.md) makalesi. 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a>Özel Etkinlik Visual Studio'da hata ayıklama
Merhaba [Azure Data Factory - yerel ortamınıza](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) örneği github'daki toodebug özel .NET etkinlikler Visual Studio içinde sağlayan bir araç içerir.  


## <a name="sample-custom-activities-on-github"></a>Github'da örnek özel etkinlikler
| Örnek | Hangi özel etkinlik mu |
| --- | --- |
| [HTTP veri yükleyici](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample). |Bir HTTP uç noktası tooAzure veri fabrikasında özel C# etkinlik kullanarak Blob depolama alanından veri yükler. |
| [Twitter düşünceleri çözümleme örneği](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Bir Azure ML model ve düşünceleri analiz, Puanlama, tahmin vb. çağırır. |
| [R betiği Çalıştır](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample). |R betiği Hdınsight kümenize zaten R yüklü üzerinde olan RScript.exe çalıştırarak çağırır. |
| [AppDomain .NET etkinliği arası](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Olanları hello Data Factory başlatıcısı tarafından kullanılan farklı derleme sürümlerini kullanır |
| [Azure Analysis Services modelinde yeniden işleyin](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  Azure Analysis Services modelinde yeniden işler. |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
