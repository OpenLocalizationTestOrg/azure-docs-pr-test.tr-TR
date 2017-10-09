---
title: "aaaAzure Data Factory - örnekleri"
description: "Azure Data Factory hizmetine hello ile birlikte örnekleri hakkında ayrıntılar sağlar."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c0538b90-2695-4c4c-a6c8-82f59111f4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: aa1c15eca21b34b7bcc64358b685d7606baaf691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---samples"></a>Azure Data Factory - örnekleri
## <a name="samples-on-github"></a>Github'da örnekleri
Merhaba [GitHub Azure-DataFactory depo](https://github.com/azure/azure-datafactory) yardımcı birkaç örnekleri kolayca artırma Azure Data Factory hizmetiyle içerir (veya) hello komut dosyaları değiştirebilirsiniz ve kendi uygulamada kullanabilirsiniz. Merhaba Samples\JSON klasörü ortak senaryolar için JSON parçacıklarını içerir.

| Örnek | Açıklama |
|:--- |:--- |
| [ADF gözden geçirme](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFWalkthrough) |Bu örnek, günlük dosyalarından tooinsights Azure Data Factory tooturn verileri kullanarak günlük dosyalarını işlemek için bir uçtan uca kılavuz sağlar. <br/><br/>Bu kılavuzda hello Data Factory işlem hattı örnek günlükleri, işlemleri toplar ve günlükleri hello verileri başvuru verileri ile aşağıdakilere zenginleştirir ve hello veri tooevaluate hello kısa süre önce başlatılan bir pazarlama kampanyası verimliliğini dönüştürür. |
| [JSON örnekleri](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON) |Bu örnek için genel senaryolar JSON örnekler verilmektedir. |
| [HTTP veri yükleyici örneği](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |Bu örnek showcases HTTP uç noktası tooAzure Blob Storage verilerden indirme özel .NET etkinliğini kullanma. |
| [AppDomain Dot Net etkinlik örnek arası](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Bu örnek tooassembly sürümleri (örneğin, WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, vb.) hello ADF başlatıcısı tarafından kullanılan değil özel bir .NET etkinlik kısıtlı tooauthor sağlar. |
| [R betiği çalıştırın](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |Bu örnekte kullanılan tooinvoke RScript.exe olabilir hello Data Factory özel etkinlik içerir. Bu örnek yalnızca R yüklü üzerinde zaten kendi (değil isteğe bağlı) Hdınsight kümesi ile çalışır. |
| [Hdınsight Hadoop kümesi üzerinde Spark işlerinin çağırma](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/Spark) |Bu örnek göstermektedir nasıl toouse MapReduce etkinliği tooinvoke Spark program. Merhaba spark program, yalnızca bir Azure Blob kapsayıcı tooanother veri kopyalar. |
| [Azure Machine Learning toplu iş Puanlama etkinliği kullanılarak twitter İnceleme](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-AzureMLBatchScoringActivity) |Bu örnek nasıl toouse AzureMLBatchScoringActivity tooinvoke bir Azure Machine Learning modeli gösterir Puanlama, tahmin vb. twitter düşünceleri çözümlemesi gerçekleştirir. |
| [Özel Etkinlik kullanılarak twitter İnceleme](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Bu örnekte, nasıl özel bir .NET etkinliği tooinvoke gerçekleştiren bir Azure Machine Learning modeli toouse twitter düşünceleri analiz, Puanlama, tahmin vb. gösterilmektedir. |
| [Azure Machine Learning için parametreli komut zincirleri](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ParameterizedPipelinesForAzureML/) |Merhaba örnek Puanlama ve her hello bölgelerin listesi ile bu örnek bulunan bir dosyadan parameters.txt geldiği yere farklı bir bölgeye parametresiyle yeniden eğitme bir uçtan uca C# kod toodeploy N ardışık düzen sağlar. |
| [Başvuru verileri yenilemek için Azure Stream Analytics işleri](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs) |Bu örnekte, nasıl bir zamanlamaya göre başvuru verileri için başvuru verileri ve Kurulum hello ile toouse Azure Data Factory ve Azure akış analizi birlikte toorun hello sorguları Yenile gösterilmektedir. |
| [Şirket içi Hortonworks Hadoop ile karma ardışık düzen](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HybridPipelineWithOnPremisesHortonworksHadoop) |Merhaba örnek bir şirket içi Hadoop kümesi yalnızca bir Hdınsight Hadoop kümesinde bulut tabanlı gibi diğer işlem hedefleri eklediğiniz gibi işleri veri fabrikasında çalıştırmak için bir işlem hedefi olarak kullanır. |
| [JSON dönüştürme aracı](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSONConversionTool) |Bu araç, tooconvert JSONs sürüm önceki too2015-07-01-Önizleme toolatest veya 2015-07-01-Önizleme (varsayılan) sağlar. |
| [U-SQL örnek giriş dosyası](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/U-SQL%20Sample%20Input%20File) |Bu dosya, U-SQL etkinlik tarafından kullanılan örnek bir dosyadır. |
| [BLOB dosya silme](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity) | Bu örnek hello dosyaları kopyalandıktan sonra ADF özel .net etkinliği toodelete dosyaları Azure Blob konumu hello kaynağından bir parçası olarak kullanılan bir C# dosyası gösterir.|

## <a name="azure-resource-manager-templates"></a>Azure Resource Manager şablonları
Azure Resource Manager şablonları veri fabrikası için Github'da aşağıdaki hello bulabilirsiniz.

| Şablon | Açıklama |
| --- | --- |
| [Azure Blob Storage tooAzure SQL veritabanını kopyalama](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) |Bu şablon dağıtımı Azure data factory hello kopya verileri Azure blob depolama toohello Azure SQL veritabanı belirtilen sahip işlem hattı oluşturur |
| [Salesforce tooAzure Blob Depolama kopyalama](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) |Bu şablon dağıtımı Azure data factory hello kopyaları verilerden Salesforce hesabınızın toohello Azure blob depolama alanı belirtilen sahip işlem hattı oluşturur. |
| [Bir Azure Hdınsight kümesinde Hive betiği çalıştırılarak verileri dönüştürün](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) |Bu şablon dağıtımı Azure data factory Azure Hdınsight Hadoop kümesinde hello örnek Hive betiği çalıştırılarak verileri dönüştüren bir işlem hattı oluşturur. |

## <a name="samples-in-azure-portal"></a>Azure portalında örnekleri
Merhaba kullanabilirsiniz **örnek ardışık düzen** tooyour veri fabrikasında veri fabrikası toodeploy örnek hatlarınızı ve bunların ilişkili varlıkların (veri kümeleri ve bağlantılı Hizmetleri) hello giriş sayfasında döşeme.

1. Veri Fabrikası oluşturun veya varolan bir veri fabrikası açın. Bkz: [veritabanını Data Factory kullanarak Blob Storage tooSQL veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adımları toocreate veri fabrikası için.
2. Merhaba, **DATA FACTORY** hello veri fabrikası dikey penceresinde hello tıklatın **örnek ardışık düzen** döşeme.

    ![Örnek komut zincirleri döşeme](./media/data-factory-samples/SamplePipelinesTile.png)
3. Merhaba, **örnek ardışık düzen** dikey penceresinde hello tıklatın **örnek** toodeploy istediğiniz.

    ![Örnek komut zincirleri dikey penceresi](./media/data-factory-samples/SampleTile.png)
4. Merhaba örnek için yapılandırma ayarlarını belirtin. Örneğin, Azure depolama hesabı adı ve hesap anahtarını, Azure SQL sunucu adı, veritabanı, kullanıcı kimliği ve parola, vb.

    ![Örnek dikey penceresi](./media/data-factory-samples/SampleBlade.png)
5. Merhaba yapılandırma ayarlarını belirtme ile tamamladıktan sonra tıklatın **oluşturma** örnek ardışık düzen ve hello ardışık düzen tarafından kullanılan bağlı hizmetler/tablolar hello toocreate ve dağıtın.
6. Tıklattığınız önceki üzerinde hello hello örnek kutucuğuna dağıtım hello durumunu görmek **örnek ardışık düzen** dikey.

    ![Dağıtım durumu](./media/data-factory-samples/DeploymentStatus.png)
7. Merhaba gördüğünüzde **dağıtım başarılı** hello bölme hello örnek, Kapat hello için iletide **örnek ardışık düzen** dikey.  
8. Üzerinde **DATA FACTORY** dikey penceresinde, gördüğünüz bağlı hizmetler, veri kümeleri ve işlem hatlarını tooyour veri fabrikası eklenir.  

    ![Data Factory dikey penceresi](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="samples-in-visual-studio"></a>Visual Studio Örnekleri
### <a name="prerequisites"></a>Ön koşullar
Merhaba aşağıdakilerin yüklü olması gerekir:

* Visual Studio 2013 veya Visual Studio 2015
* Visual Studio 2013 veya Visual Studio 2015 için Azure SDK’sını indirin. Çok gidin[Azure indirme sayfası](https://azure.microsoft.com/downloads/) tıklatıp **VS 2013** veya **VS 2015** hello içinde **.NET** bölümü.
* Visual Studio için Hello en son Azure Data Factory eklentisini indirin: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) veya [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Visual Studio 2013 kullanıyorsanız, ayrıca hello eklentisi aşağıdaki adımları hello yaparak güncelleştirebilirsiniz: hello menüsünde **Araçları** -> **Uzantılar ve güncelleştirmeler**  ->  **Çevrimiçi** -> **Visual Studio Galerisi** -> **Visual Studio için Microsoft Azure Data Factory Araçları**  ->  **Güncelleştirme**.

### <a name="use-data-factory-templates"></a>Veri Fabrikası şablonları kullanın.
1. Tıklatın **dosya** Merhaba, Çok menüsünde**yeni**, tıklatıp **proje**.
2. Merhaba, **yeni proje** iletişim kutusunda, adımları hello:

   1. Seçin **DataFactory** altında **şablonları**.
   2. Seçin **veri fabrikası şablonları** hello sağ bölmedeki.
   3. Girin bir **adı** hello projesi için.
   4. Seçin bir **konumu** hello projesi için.
   5. **Tamam** düğmesine tıklayın.

      ![Yeni proje iletişim kutusu](./media/data-factory-samples/vs-new-project-adf-templates.png)
3. Merhaba, **veri fabrikası şablonları** iletişim kutusu, select hello örnek hello şablondan **kullanım örneği şablonları** bölümünde ve tıklatın **sonraki**. Merhaba aşağıdaki adımlar hello kullanarak yol **müşteri profil** şablonu. Adımları için benzer diğer örnekleri hello.

    ![Veri Fabrikası Şablonları iletişim kutusu](./media/data-factory-samples/vs-data-factory-templates-dialog.png)
4. Merhaba, **veri fabrikası Yapılandırması** iletişim kutusunda, tıklatın **sonraki** hello üzerinde **veri fabrikası Temelleri** sayfası.
5. Merhaba üzerinde **data factory Yapılandır** sayfasında, adımları hello:
   1. Seçin **yeni veri fabrikası oluşturma**. Öğesini de seçebilirsiniz **mevcut veri fabrikası kullanmak**.
   2. Girin bir **adı** hello veri fabrikası için.
   3. Select hello **Azure aboneliği** oluşturulan hello veri fabrikası toobe istediğiniz içinde.
   4. Select hello **kaynak grubu** hello veri fabrikası için.
   5. Select hello **Batı ABD**, **Doğu ABD**, veya **Kuzey Avrupa** hello için **bölge**.
   6. **İleri**’ye tıklayın.
6. Merhaba, **yapılandırma veri depolarına** sayfasında, varolan bir belirtin **Azure SQL veritabanı** ve **Azure depolama hesabı** (veya) veritabanı/depolama alanı oluşturun ve İleri'yi tıklatın.
7. Merhaba, **işlem yapılandırma** sayfasında, Varsayılanları seçin ve tıklayın **sonraki**.
8. Merhaba, **Özet** sayfasında, tüm ayarları gözden geçirin ve tıklayın **sonraki**.
9. Merhaba, **dağıtım durumu** sayfasında hello dağıtım işlemi tamamlanana kadar bekleyin ve tıklayın **son**.
10. Merhaba Çözüm Gezgini'nde projeye sağ tıklayın ve **Yayımla**.
11. Görürseniz **tooyour Microsoft hesabı oturum** iletişim kutusunda, Azure aboneliği olan hello hesabı için kimlik bilgilerinizi girin ve tıklayın **oturum**.
12. İletişim kutusu aşağıdaki hello görmeniz gerekir:

    ![Yayımla iletişim kutusu](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
13. Merhaba, **data factory Yapılandır** sayfasında, adımları hello:

    1. Onaylayın **mevcut veri fabrikası kullanmak** seçeneği.
    2. Select hello **veri fabrikası** hello şablon kullanırken seçin vardı.
    3. Tıklatın **sonraki** tooswitch toohello **öğeleri Yayımla** sayfası. (Tuşuna **sekmesini** hello ad alanı tooif hello dışında toomove **sonraki** düğmesi devre dışıdır.)
14. Merhaba, **öğeleri Yayımla** sayfasında, tüm veri varlıkları seçilir ve tıklatın fabrikaları hello olun **sonraki** tooswitch toohello **Özet** sayfası.     
15. Merhaba özeti gözden geçirin ve tıklatın **sonraki** toostart, hello dağıtım işlemi ve görünüm hello **dağıtım durumu**.
16. Merhaba, **dağıtım durumu** sayfasında hello hello dağıtım işleminin durumunu görmeniz gerekir. Merhaba dağıtımını gerçekleştirdikten sonra Son'a tıklayın.

Bkz: [ilk data factory'nizi (Visual Studio) derleme](data-factory-build-your-first-pipeline-using-vs.md) Visual Studio tooauthor Data Factory varlıklarını kullanma ve tooAzure yayımlama hakkında ayrıntılar için.          
