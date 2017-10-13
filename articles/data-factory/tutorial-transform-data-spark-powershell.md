---
title: "Azure Data Factory’de Spark kullanarak verileri dönüştürme | Microsoft Docs"
description: "Bu öğretici, Azure Data Factory'de Spart Etkinliğini kullanarak verileri dönüştürmeye ilişkin adım adım yönergeler sağlar."
services: data-factory
documentationcenter: 
author: shengcmsft
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/10/2017
ms.author: shengc
ms.openlocfilehash: 93031615b271e542d8832b980a40ca25d1cd6d5c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="transform-data-in-the-cloud-by-using-spark-activity-in-azure-data-factory"></a>Azure Data Factory'de Spark etkinliğini kullanarak verileri bulutta dönüştürme
Azure Data Factory, bulutta veri hareketi ve veri dönüştürmeyi düzenleyip otomatikleştirmek için veri odaklı iş akışları oluşturmanıza olanak tanıyan, bulut tabanlı bir veri tümleştirme hizmetidir. Azure Data Factory’yi kullanarak, farklı veri depolarından veri alabilen, Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics ve Azure Machine Learning gibi işlem hizmetlerini kullanarak verileri işleyebilen/dönüştürebilen ve çıktı verilerini iş zekası (BI) uygulamaları tarafından kullanılabilmesi için Azure SQL Veri Ambarı gibi veri depolarında yayımlayabilen veri odaklı iş akışları (işlem hatları olarak adlandırılır) oluşturup zamanlayabilirsiniz. 

Bu öğreticide, Azure PowerShell kullanarak verileri Spark Etkinliği ve talep üzerine HDInsight bağlı hizmeti ile dönüştüren bir Data Factory işlem hattı oluşturacaksınız. Bu öğreticide aşağıdaki adımları gerçekleştireceksiniz:

> [!div class="checklist"]
> * Veri fabrikası oluşturma. 
> * Bağlantılı hizmetler yazma ve dağıtma.
> * İşlem hattı oluşturma ve dağıtma. 
> * Bir işlem hattı çalıştırması başlatma.
> * İşlem hattı çalıştırmasını izleme.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.

## <a name="prerequisites"></a>Ön koşullar
* **Azure Depolama hesabı**. Bir python betiği ve giriş dosyası oluşturup Azure depolama alanına yükleyin. Spark programının çıktısı bu depolama hesabında depolanır. İsteğe bağlı Spark kümesi, birincil depolama alanıyla aynı depolama hesabını kullanır.  
* **Azure PowerShell**. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/install-azurerm-ps) bölümündeki yönergeleri izleyin.


### <a name="upload-python-script-to-your-blob-storage-account"></a>Python betiğini Blob Depolama hesabınıza yükleme
1. Aşağıdaki içeriğe sahip **WordCount_Spark.py** adlı bir python dosyası oluşturun: 

    ```python
    import sys
    from operator import add
    
    from pyspark.sql import SparkSession
    
    def main():
        spark = SparkSession\
            .builder\
            .appName("PythonWordCount")\
            .getOrCreate()
            
        lines = spark.read.text("wasbs://adftutorial@<storageaccountname>.blob.core.windows.net/spark/inputfiles/minecraftstory.txt").rdd.map(lambda r: r[0])
        counts = lines.flatMap(lambda x: x.split(' ')) \
            .map(lambda x: (x, 1)) \
            .reduceByKey(add)
        counts.saveAsTextFile("wasbs://adftutorial@<storageaccountname>.blob.core.windows.net/spark/outputfiles/wordcount")
        
        spark.stop()
    
    if __name__ == "__main__":
        main()
    ```
2. **&lt;storageAccountName&gt;**’i Azure Depolama hesabınızın adıyla değiştirin. Ardından dosyayı kaydedin. 
3. Azure Blob depolama alanınızda henüz yoksa **adftutorial** adlı bir kapsayıcı oluşturun. 
4. **Spark** adlı bir klasör oluşturun.
5. **Spark** klasörünün altında **script** adlı bir alt klasör oluşturun. 
6. **WordCount_Spark.py** dosyasını **script** alt klasörüne yükleyin. 


### <a name="upload-the-input-file"></a>Girdi dosyasını yükleme
1. Bazı metinlerle **minecraftstory.txt** adlı bir dosya oluşturun. Spark programı bu metindeki sözcükleri sayar. 
2. `spark` klasöründe `inputfiles` adlı bir alt klasör oluşturun. 
3. `minecraftstory.txt` dosyasını `inputfiles` alt klasörüne yükleyin. 

## <a name="author-linked-services"></a>Bağlı hizmetler oluşturma
Bu bölümde iki Bağlı Hizmet oluşturacaksınız: 
    
- Bir Azure Depolama hesabını veri fabrikasına bağlayan Azure Depolama Bağlı Hizmeti. Bu depolama alanı, isteğe bağlı HDInsight kümesi tarafından kullanılır. Ayrıca, yürütülecek Spark betiğini içerir. 
- İsteğe bağlı HDInsight Bağlı Hizmeti. Azure Data Factory otomatik olarak bir HDInsight kümesi oluşturur, Spark programını çalıştırır ve önceden yapılandırılmış bir süre boyunca boşta kaldıktan sonra HDInsight kümesini siler. 

### <a name="azure-storage-linked-service"></a>Azure Storage bağlı hizmeti
Tercih ettiğiniz düzenleyiciyi kullanarak bir JSON dosyası oluşturun, Azure Depolama bağlı hizmetinin aşağıdaki JSON tanımını kopyalayın ve ardından dosyayı **MyStorageLinkedService.json** olarak kaydedin.  

```json
{
    "name": "MyStorageLinkedService",
    "properties": {
      "type": "AzureStorage",
      "typeProperties": {
        "connectionString": {
          "value": "DefaultEndpointsProtocol=https;AccountName=<storageAccountName>;AccountKey=<storageAccountKey>",
          "type": "SecureString"
        }
      }
    }
}
```
&lt;storageAccountName&gt; ve &lt;storageAccountKey&gt; değerlerini Azure Depolama hesabınızın adı ve anahtarıyla güncelleştirin. 


### <a name="on-demand-hdinsight-linked-service"></a>İsteğe bağlı HDInsight bağlı hizmeti
Tercih ettiğiniz düzenleyiciyi kullanarak bir JSON dosyası oluşturun, Azure HDInsight bağlı hizmetinin aşağıdaki JSON tanımını kopyalayın ve dosyayı **MyOnDemandSparkLinkedService.json** olarak kaydedin.  

```json
{
    "name": "MyOnDemandSparkLinkedService",
    "properties": {
      "type": "HDInsightOnDemand",
      "typeProperties": {
        "clusterSize": 2,
        "clusterType": "spark",
        "timeToLive": "00:15:00",
        "hostSubscriptionId": "<subscriptionID> ",
        "servicePrincipalId": "<servicePrincipalID>",
        "servicePrincipalKey": {
          "value": "<servicePrincipalKey>",
          "type": "SecureString"
        },
        "tenant": "<tenant ID>",
        "clusterResourceGroup": "<resourceGroupofHDICluster>",
        "version": "3.6",
        "osType": "Linux",
        "clusterNamePrefix":"ADFSparkSample",
        "linkedServiceName": {
          "referenceName": "MyStorageLinkedService",
          "type": "LinkedServiceReference"
        }
      }
    }
}
```
Bağlı hizmet tanımında aşağıdaki özelliklerin değerlerini güncelleştirin: 

- **hostSubscriptionId**. &lt;SubscriptionID&gt;’yi Azure aboneliğinizin kimliği ile değiştirin. İsteğe bağlı HDInsight kümesi bu abonelikte oluşturulur. 
- **tenant**. &lt;tenantID&gt; değerini Azure kiracınızın kimliği ile değiştirin. 
- **servicePrincipalId**, **servicePrincipalKey**. &lt;servicePrincipalID&gt; ve &lt;servicePrincipalKey&gt; değerini Azure Active Directory’deki hizmet sorumlunuzun kimliği ve anahtarıyla değiştirin. Bu hizmet sorumlusu, abonelikte ya da kümenin oluşturulduğu kaynak grubunda Katkıda Bulunan rolünün bir üyesi olmalıdır. Ayrıntılar için bkz. [Azure Active Directory uygulaması ve hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-create-service-principal-portal.md). 
- **clusterResourceGroup**. &lt;resourceGroupOfHDICluster&gt; değerini HDInsight kümesinin oluşturulması gereken kaynak grubunun adıyla değiştirin. 

> [!NOTE]
> Azure HDInsight, desteklediği her bir Azure bölgesinde kullanabileceğiniz toplam çekirdek sayısıyla ilgili sınırlamaya sahiptir. İsteğe Bağlı HDInsight Bağlı Hizmeti için HDInsight kümesi, birincil depolama olarak kullanılan Azure Depolama konumunda oluşturulur. Kümenin başarıyla oluşturulabilmesi için yeterince çekirdek kotanızın olduğundan emin olun. Daha fazla bilgi için bkz. [HDInsight’ta Hadoop, Spark, Kafka ve daha fazlası ile küme ayarlama](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md). 


## <a name="author-a-pipeline"></a>İşlem hattı oluşturma 
Bu adımda, Spark etkinliği ile bir işlem hattı oluşturacaksınız. Etkinlik, **sözcük sayısı** örneğini kullanır. Henüz yapmadıysanız bu konumdan içeriği indirin.

Tercih ettiğiniz düzenleyicide bir JSON dosyası oluşturun, aşağıdaki işlem hattı JSON tanımını kopyalayın ve **MySparkOnDemandPipeline.json** olarak kaydedin. 

```json
{
  "name": "MySparkOnDemandPipeline",
  "properties": {
    "activities": [
      {
        "name": "MySparkActivity",
        "type": "HDInsightSpark",
        "linkedServiceName": {
            "referenceName": "MyOnDemandSparkLinkedService",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
          "rootPath": "adftutorial/spark",
          "entryFilePath": "script/WordCount_Spark.py",
          "getDebugInfo": "Failure",
          "sparkJobLinkedService": {
            "referenceName": "MyStorageLinkedService",
            "type": "LinkedServiceReference"
          }
        }
      }
    ]
  }
}
```

Aşağıdaki noktalara dikkat edin: 

- rootPath, adftutorial kapsayıcısının spark klasörünü işaret eder. 
- entryFilePath, spark klasörünün script alt klasöründeki WordCount_Spark.py dosyasını işaret eder. 


## <a name="create-a-data-factory"></a>Veri fabrikası oluşturma 
JSON dosyalarında bağlı hizmet ve işlem hattı tanımları oluşturdunuz. Şimdi bir veri fabrikası oluşturalım ve bağlı Hizmet ile işlem hattı JSON dosyalarını PowerShell cmdlet'leri kullanarak dağıtalım. Aşağıdaki PowerShell komutlarını tek tek çalıştırın: 

1. Değişkenleri tek tek ayarlayın.

    ```powershell
    $subscriptionID = "<subscription ID>" # Your Azure subscription ID
    $resourceGroupName = "ADFTutorialResourceGroup" # Name of the resource group
    $dataFactoryName = "MyDataFactory09102017" # Globally unique name of the data factory
    $pipelineName = "MySparkOnDemandPipeline" # Name of the pipeline
    ```
2. **PowerShell**’i başlatın. Bu hızlı başlangıcın sonuna kadar Azure PowerShell’i açık tutun. Kapatıp yeniden açarsanız komutları yeniden çalıştırmanız gerekir.

    Aşağıdaki komutu çalıştırın ve Azure portalda oturum açmak için kullandığınız kullanıcı adı ve parolayı girin:
        
    ```powershell
    Login-AzureRmAccount
    ```        
    Bu hesapla ilgili tüm abonelikleri görmek için aşağıdaki komutu çalıştırın:

    ```powershell
    Get-AzureRmSubscription
    ```
    Çalışmak isteğiniz aboneliği seçmek için aşağıdaki komutu çalıştırın. **SubscriptionId**’yi Azure aboneliğinizin kimliği ile değiştirin:

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"    
    ```  
3. ADFTutorialResourceGroup kaynak grubunu oluşturun. 

    ```powershell
    New-AzureRmResourceGroup -Name $resourceGroupName -Location "East Us" 
    ```
4. Veri fabrikasını oluşturun. 

    ```powershell
     $df = Set-AzureRmDataFactoryV2 -Location EastUS -Name $dataFactoryName -ResourceGroupName $resourceGroupName
    ```

    Çıktıyı görmek için aşağıdaki komutu yürütün: 

    ```powershell
    $df
    ```
5. JSON dosyalarını oluşturduğunuz klasöre geçin ve Azure Depolama bağlı hizmetlerini dağıtmak için aşağıdaki komutu çalıştırın: 
       
    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "MyStorageLinkedService" -File "MyStorageLinkedService.json"
    ```
6. İsteğe bağlı Spark bağlı hizmetinde aşağıdaki komutu çalıştırın: 
       
    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "MyOnDemandSparkLinkedService" -File "MyOnDemandSparkLinkedService.json"
    ```
7. Bir işlem hattını dağıtmak için aşağıdaki komutu çalıştırın: 
       
    ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name $pipelineName -File "MySparkOnDemandPipeline.json"
    ```
    
## <a name="start-and-monitor-a-pipeline-run"></a>İşlem hattı çalıştırmasını başlatma ve izleme  

1. Bir işlem hattı çalıştırması başlatma. Ayrıca, gelecekte izlemek üzere işlem hattı çalıştırma kimliğini yakalar.

    ```powershell
    $runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName $pipelineName  
    ```
2. İşlem hattı çalıştırma durumunu tamamlanıncaya kadar sürekli olarak denetlemek için aşağıdaki betiği çalıştırın.

    ```powershell
    while ($True) {
        $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)
    
        if(!$result) {
            Write-Host "Waiting for pipeline to start..." -foregroundcolor "Yellow"
        }
        elseif (($result | Where-Object { $_.Status -eq "InProgress" } | Measure-Object).count -ne 0) {
            Write-Host "Pipeline run status: In Progress" -foregroundcolor "Yellow"
        }
        else {
            Write-Host "Pipeline '"$pipelineName"' run finished. Result:" -foregroundcolor "Yellow"
            $result
            break
        }
        ($result | Format-List | Out-String)
        Start-Sleep -Seconds 15
    }

    Write-Host "Activity `Output` section:" -foregroundcolor "Yellow"
    $result.Output -join "`r`n"

    Write-Host "Activity `Error` section:" -foregroundcolor "Yellow"
    $result.Error -join "`r`n" 
    ```  
3. Örnek çalıştırmanın çıktısı aşağıdaki gibidir: 

    ```
    Pipeline run status: In Progress
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : 
    ActivityName      : MySparkActivity
    PipelineRunId     : 94e71d08-a6fa-4191-b7d1-cf8c71cb4794
    PipelineName      : MySparkOnDemandPipeline
    Input             : {rootPath, entryFilePath, getDebugInfo, sparkJobLinkedService}
    Output            : 
    LinkedServiceName : 
    ActivityRunStart  : 9/20/2017 6:33:47 AM
    ActivityRunEnd    : 
    DurationInMs      : 
    Status            : InProgress
    Error             :
    …
    
    Pipeline ' MySparkOnDemandPipeline' run finished. Result:
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : MyDataFactory09102017
    ActivityName      : MySparkActivity
    PipelineRunId     : 94e71d08-a6fa-4191-b7d1-cf8c71cb4794
    PipelineName      : MySparkOnDemandPipeline
    Input             : {rootPath, entryFilePath, getDebugInfo, sparkJobLinkedService}
    Output            : {clusterInUse, jobId, ExecutionProgress, effectiveIntegrationRuntime}
    LinkedServiceName : 
    ActivityRunStart  : 9/20/2017 6:33:47 AM
    ActivityRunEnd    : 9/20/2017 6:46:30 AM
    DurationInMs      : 763466
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    Activity Output section:
    "clusterInUse": "https://ADFSparkSamplexxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.azurehdinsight.net/"
    "jobId": "0"
    "ExecutionProgress": "Succeeded"
    "effectiveIntegrationRuntime": "DefaultIntegrationRuntime (East US)"
    Activity Error section:
    "errorCode": ""
    "message": ""
    "failureType": ""
    "target": "MySparkActivity"
    ```
4. Spark programının çıktısı ile adftutorial kapsayıcısının `spark` klasöründe `outputfiles` adlı bir klasörün oluşturulduğunu onaylayın. 


## <a name="next-steps"></a>Sonraki adımlar
Bu örnekteki işlem hattı, verileri bir konumdan Azure blob depolama alanındaki başka bir konuma kopyalar. Şunları öğrendiniz: 

> [!div class="checklist"]
> * Veri fabrikası oluşturma. 
> * Bağlantılı hizmetler yazma ve dağıtma.
> * İşlem hattı oluşturma ve dağıtma. 
> * Bir işlem hattı çalıştırması başlatma.
> * İşlem hattı çalıştırmasını izleme.

Sanal ağdaki bir Azure HDInsight kümesinde Hive betiği çalıştırarak verileri dönüştürme hakkında bilgi almak için sonraki öğreticiye ilerleyin. 

> [!div class="nextstepaction"]
> [Öğretici: Azure Sanal Ağ’da Hive kullanarak verileri dönüştürme](tutorial-transform-data-hive-virtual-network.md).





