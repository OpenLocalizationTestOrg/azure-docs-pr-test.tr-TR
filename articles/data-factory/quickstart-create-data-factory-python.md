---
title: "Python kullanarak Azure veri fabrikası oluşturma | Microsoft Docs"
description: "Aynı Azure Blob Depolama alanındaki bir konumdan başka bir konuma veri kopyalamak için bir Azure veri fabrikası oluşturun."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: 
ms.devlang: python
ms.topic: hero-article
ms.date: 01/22/2018
ms.author: shlo
ms.openlocfilehash: 33ccecee82617dc53e597165c708c2bf67cdabe1
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/23/2018
---
# <a name="create-a-data-factory-and-pipeline-using-python"></a>Python kullanarak veri fabrikası ve işlem hattı oluşturma
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Sürüm 1 - Genel Kullanım](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Sürüm 2 - Önizleme](quickstart-create-data-factory-python.md)

Azure Data Factory, bulutta veri hareketi ve veri dönüştürmeyi düzenleyip otomatikleştirmek için veri odaklı iş akışları oluşturmanıza olanak tanıyan, bulut tabanlı bir veri tümleştirme hizmetidir. Azure Data Factory’yi kullanarak, farklı veri depolarından veri alabilen, Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics ve Azure Machine Learning gibi işlem hizmetlerini kullanarak verileri işleyebilen/dönüştürebilen ve çıktı verilerini iş zekası (BI) uygulamaları tarafından kullanılabilmesi için Azure SQL Veri Ambarı gibi veri depolarında yayımlayabilen veri odaklı iş akışları (işlem hatları olarak adlandırılır) oluşturup zamanlayabilirsiniz.

Bu hızlı başlangıç, Python kullanarak bir Azure veri fabrikası oluşturma işlemini açıklar. Bu veri fabrikasındaki işlem hattı, verileri Azure blob depolama alanındaki bir klasörden başka bir klasöre kopyalar.

> [!NOTE]
> Bu makale şu anda önizleme sürümünde olan Data Factory sürüm 2 için geçerlidir. Data Factory hizmetinin genel kullanıma açık (GA) 1. sürümünü kullanıyorsanız [Data Factory sürüm 1 ile çalışmaya başlama](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) konusunu inceleyin.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.

## <a name="prerequisites"></a>Ön koşullar

* **Azure Depolama hesabı**. Blob depolama alanını **kaynak** ve **havuz** veri deposu olarak kullanabilirsiniz. Azure depolama hesabınız yoksa, oluşturma adımları için [Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) makalesine bakın.
* **Azure Active Directory’de** [bu yönergeyi](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) izleyerek bir uygulama oluşturun. Sonraki adımlarda kullandığınız şu değerleri not edin: **uygulama kimliği**, **kimlik doğrulama anahtarı** ve **kiracı kimliği**. Aynı makalede bulunan yönergeleri izleyerek uygulamayı "**Katkıda bulunan**" rolüne atayın.

### <a name="create-and-upload-an-input-file"></a>Giriş dosyası oluşturma ve yükleme

1. Not Defteri'ni başlatın. Aşağıdaki metni kopyalayıp diskinizde **input.txt** dosyası olarak kaydedin.

    ```
    John|Doe
    Jane|Doe
    ```
2.  [Azure Depolama Gezgini](http://storageexplorer.com/) gibi araçları kullanarak **adfv2tutorial** kapsayıcısı ve kapsayıcı içinde **input** klasörü oluşturun. Sonra, **input.txt** dosyasını **input** klasörüne yükleyin.

## <a name="install-the-python-package"></a>Python paketi yükleme
1. Yönetici ayrıcalıklarıyla bir terminal veya komut istemi açın. 
2. İlk olarak, Azure yönetim kaynakları için Python paketini yükleyin:

    ```
    pip install azure-mgmt-resource
    ```
3. Data Factory için Python paketini yüklemek üzere aşağıdaki komutu çalıştırın:

    ```
    pip install azure-mgmt-datafactory
    ```

    [Data Factory için Python SDK’sı](https://github.com/Azure/azure-sdk-for-python), Python 2.7, 3.3, 3.4, 3.5 ve 3.6 sürümlerini destekler.

## <a name="create-a-data-factory-client"></a>Veri fabrikası istemcisi oluşturma

1. **datafactory.py** adlı bir dosya oluşturun. Ad alanlarına başvurular eklemek için aşağıdaki deyimleri ekleyin.

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.datafactory import DataFactoryManagementClient
    from azure.mgmt.datafactory.models import *
    from datetime import datetime, timedelta
    import time
    ```
2. Bilgileri yazdıran aşağıdaki işlevleri ekleyin.

    ```python
    def print_item(group):
        """Print an Azure object instance."""
        print("\tName: {}".format(group.name))
        print("\tId: {}".format(group.id))
        if hasattr(group, 'location'):
            print("\tLocation: {}".format(group.location))
        if hasattr(group, 'tags'):
            print("\tTags: {}".format(group.tags))
        if hasattr(group, 'properties'):
            print_properties(group.properties)

    def print_properties(props):
        """Print a ResourceGroup properties instance."""
        if props and hasattr(props, 'provisioning_state') and props.provisioning_state:
            print("\tProperties:")
            print("\t\tProvisioning State: {}".format(props.provisioning_state))
        print("\n\n")

    def print_activity_run_details(activity_run):
        """Print activity run details."""
        print("\n\tActivity run details\n")
        print("\tActivity run status: {}".format(activity_run.status))    
        if activity_run.status == 'Succeeded':
            print("\tNumber of bytes read: {}".format(activity_run.output['dataRead']))       
            print("\tNumber of bytes written: {}".format(activity_run.output['dataWritten']))           
            print("\tCopy duration: {}".format(activity_run.output['copyDuration']))           
        else:
            print("\tErrors: {}".format(activity_run.error['message']))

    ```
3. Aşağıdaki kodu DataFactoryManagementClient sınıfının bir örneğini oluşturan **Main** yöntemine ekleyin. Veri fabrikası, bağlı hizmet, veri kümeleri ve işlem hattı oluşturmak için bu nesneyi kullanırsınız. Bu nesneyi ayrıca işlem hattı ayrıntılarını izlemek için kullanabilirsiniz. **subscription_id** değişkenini Azure aboneliğinizin kimliğine ayarlayın. Data Factory V2 şu anda Doğu ABD, Doğu ABD 2 ve Batı Avrupa bölgelerinde veri fabrikası oluşturmanıza olanak sağlar. Veri fabrikası tarafından kullanılan verileri depoları (Azure Depolama, Azure SQL Veritabanı vb.) ve işlemler (HDInsight vb.) başka bölgelerde olabilir.

    ```python   
    def main():

        # Azure subscription ID
        subscription_id = '<Specify your Azure Subscription ID>'

        # This program creates this resource group. If it's an existing resource group, comment out the code that creates the resource group
        rg_name = 'ADFTutorialResourceGroup'

        # The data factory name. It must be globally unique.
        df_name = '<Specify a name for the data factory. It must be globally unique>'

        # Specify your Active Directory client ID, client secret, and tenant ID
        credentials = ServicePrincipalCredentials(client_id='<Active Directory application/client ID>', secret='<client secret>', tenant='<Active Directory tenant ID>')
        resource_client = ResourceManagementClient(credentials, subscription_id)
        adf_client = DataFactoryManagementClient(credentials, subscription_id)

        rg_params = {'location':'eastus'}
        df_params = {'location':'eastus'}    
    ```

## <a name="create-a-data-factory"></a>Veri fabrikası oluşturma

Aşağıdaki kodu **veri fabrikası** oluşturan **Main** yöntemine ekleyin. Kaynak grubunuz zaten varsa, birinci `create_or_update` deyimine açıklama ekleyin.

```python
    # create the resource group
    # comment out if the resource group already exits
    resource_client.resource_groups.create_or_update(rg_name, rg_params)

    #Create a data factory
    df_resource = Factory(location='eastus')
    df = adf_client.factories.create_or_update(rg_name, df_name, df_resource)
    print_item(df)
    while df.provisioning_state != 'Succeeded':
        df = adf_client.factories.get(rg_name, df_name)
        time.sleep(1)
```

## <a name="create-a-linked-service"></a>Bağlı hizmet oluşturma

Aşağıdaki kodu bir **Azure Depolama bağlı hizmeti** oluşturan **Main** yöntemine ekleyin.

Veri depolarınızı ve işlem hizmetlerinizi veri fabrikasına bağlamak için veri fabrikasında bağlı hizmetler oluşturursunuz. Bu hızlı başlangıçta yalnızca bir Azure Depolama bağlı hizmetini örnekte "AzureStorageLinkedService" olarak adlandırılmış bir kopyalama kaynağı ve havuz deposu olarak oluşturmanız gerekir. `<storageaccountname>` ve `<storageaccountkey>` değerlerini Azure Depolama hesabınızın adı ve anahtarıyla değiştirin.

```python
    # Create an Azure Storage linked service
    ls_name = 'storageLinkedService'

    # IMPORTANT: specify the name and key of your Azure Storage account.
    storage_string = SecureString('DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<storageaccountkey>')

    ls_azure_storage = AzureStorageLinkedService(connection_string=storage_string)
    ls = adf_client.linked_services.create_or_update(rg_name, df_name, ls_name, ls_azure_storage)
    print_item(ls)
```
## <a name="create-datasets"></a>Veri kümeleri oluşturma
Bu bölümde biri kaynak, diğeri havuz için olmak üzere iki veri kümesi oluşturacaksınız.

### <a name="create-a-dataset-for-source-azure-blob"></a>Kaynak Azure Blob için veri kümesi oluşturma
Aşağıdaki kodu bir Azure blob veri kümesi oluşturan Main yöntemine ekleyin. Bir Azure Blob veri kümesinin özellikleri hakkında bilgi için [Azure blob bağlayıcısı](connector-azure-blob-storage.md#dataset-properties) makalesine bakın.

Azure Blob’da kaynak verilerini temsil eden bir veri kümesi tanımlayın. Bu Blob veri kümesi, önceki adımda oluşturduğunuz Azure Depolama bağlı hizmetini ifade eder.

```python
    # Create an Azure blob dataset (input)
    ds_name = 'ds_in'
    ds_ls = LinkedServiceReference(ls_name)
    blob_path= 'adfv2tutorial/input'
    blob_filename = 'input.txt'
    ds_azure_blob= AzureBlobDataset(ds_ls, folder_path=blob_path, file_name = blob_filename)
    ds = adf_client.datasets.create_or_update(rg_name, df_name, ds_name, ds_azure_blob)
    print_item(ds)
```

### <a name="create-a-dataset-for-sink-azure-blob"></a>Havuz Azure Blob için veri kümesi oluşturma
Aşağıdaki kodu bir Azure blob veri kümesi oluşturan Main yöntemine ekleyin. Bir Azure Blob veri kümesinin özellikleri hakkında bilgi için [Azure blob bağlayıcısı](connector-azure-blob-storage.md#dataset-properties) makalesine bakın.

Azure Blob’da kaynak verilerini temsil eden bir veri kümesi tanımlayın. Bu Blob veri kümesi, önceki adımda oluşturduğunuz Azure Depolama bağlı hizmetini ifade eder.

```python
    # Create an Azure blob dataset (output)
    dsOut_name = 'ds_out'
    output_blobpath = 'adfv2tutorial/output'
    dsOut_azure_blob = AzureBlobDataset(ds_ls, folder_path=output_blobpath)
    dsOut = adf_client.datasets.create_or_update(rg_name, df_name, dsOut_name, dsOut_azure_blob)
    print_item(dsOut)
```

## <a name="create-a-pipeline"></a>İşlem hattı oluşturma

Aşağıdaki kodu **bir kopyalama etkinliği ile işlem hattı** oluşturan **Main** yöntemine ekleyin.

```python
    # Create a copy activity
    act_name =  'copyBlobtoBlob'
    blob_source = BlobSource()
    blob_sink = BlobSink()
    dsin_ref = DatasetReference(ds_name)
    dsOut_ref = DatasetReference(dsOut_name)
    copy_activity = CopyActivity(act_name,inputs=[dsin_ref], outputs=[dsOut_ref], source=blob_source, sink=blob_sink)

    #Create a pipeline with the copy activity
    p_name =  'copyPipeline'
    params_for_pipeline = {}
    p_obj = PipelineResource(activities=[copy_activity], parameters=params_for_pipeline)
    p = adf_client.pipelines.create_or_update(rg_name, df_name, p_name, p_obj)
    print_item(p)
```


## <a name="create-a-pipeline-run"></a>İşlem hattı çalıştırması oluşturma

Aşağıdaki kodu **bir işlem hattı çalıştırması tetikleyen** **Main** yöntemine ekleyin.

```python
    #Create a pipeline run.
    run_response = adf_client.pipelines.create_run(rg_name, df_name, p_name,
        {
        }
    )
```

## <a name="monitor-a-pipeline-run"></a>İşlem hattı çalıştırmasını izleme
İşlem hattını izlemek için, aşağıdaki kodu **Main** yöntemine ekleyin:

```python
    #Monitor the pipeline run
    time.sleep(30)
    pipeline_run = adf_client.pipeline_runs.get(rg_name, df_name, run_response.run_id)
    print("\n\tPipeline run status: {}".format(pipeline_run.status))
    activity_runs_paged = list(adf_client.activity_runs.list_by_pipeline_run(rg_name, df_name, pipeline_run.run_id, datetime.now() - timedelta(1),  datetime.now() + timedelta(1)))
    print_activity_run_details(activity_runs_paged[0])
```

Şimdi, program çalıştırıldığında **main** yöntemini çağırmak için aşağıdaki deyimi ekleyin:

```python
# Start the main method
main()
```

## <a name="full-script"></a>Tam betik
Tam Python kodu aşağıdaki gibidir:

```python
from azure.common.credentials import ServicePrincipalCredentials
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.datafactory import DataFactoryManagementClient
from azure.mgmt.datafactory.models import *
from datetime import datetime, timedelta
import time

def print_item(group):
    """Print an Azure object instance."""
    print("\tName: {}".format(group.name))
    print("\tId: {}".format(group.id))
    if hasattr(group, 'location'):
        print("\tLocation: {}".format(group.location))
    if hasattr(group, 'tags'):
        print("\tTags: {}".format(group.tags))
    if hasattr(group, 'properties'):
        print_properties(group.properties)
    print("\n")        

def print_properties(props):
    """Print a ResourceGroup properties instance."""
    if props and hasattr(props, 'provisioning_state') and props.provisioning_state:
        print("\tProperties:")
        print("\t\tProvisioning State: {}".format(props.provisioning_state))
    print("\n")

def print_activity_run_details(activity_run):
    """Print activity run details."""
    print("\n\tActivity run details\n")
    print("\tActivity run status: {}".format(activity_run.status))    
    if activity_run.status == 'Succeeded':
        print("\tNumber of bytes read: {}".format(activity_run.output['dataRead']))       
        print("\tNumber of bytes written: {}".format(activity_run.output['dataWritten']))           
        print("\tCopy duration: {}".format(activity_run.output['copyDuration']))           
    else:
        print("\tErrors: {}".format(activity_run.error['message']))

def main():

    # Azure subscription ID
    subscription_id = '<your Azure subscription ID>'

    # This program creates this resource group. If it's an existing resource group, comment out the code that creates the resource group
    rg_name = '<Azure resource group name>'

    # The data factory name. It must be globally unique.
    df_name = '<Your data factory name>'        

    # Specify your Active Directory client ID, client secret, and tenant ID
    credentials = ServicePrincipalCredentials(client_id='<Active Directory client ID>', secret='<client secret>', tenant='<tenant ID>')
    resource_client = ResourceManagementClient(credentials, subscription_id)
    adf_client = DataFactoryManagementClient(credentials, subscription_id)

    rg_params = {'location':'eastus'}
    df_params = {'location':'eastus'}

    # create the resource group
    # comment out if the resource group already exits
    resource_client.resource_groups.create_or_update(rg_name, rg_params)

    # Create a data factory
    df_resource = Factory(location='eastus')
    df = adf_client.factories.create_or_update(rg_name, df_name, df_resource)
    print_item(df)
    while df.provisioning_state != 'Succeeded':
        df = adf_client.factories.get(rg_name, df_name)
        time.sleep(1)

    # Create an Azure Storage linked service
    ls_name = 'storageLinkedService'

    # Specify the name and key of your Azure Storage account
    storage_string = SecureString('DefaultEndpointsProtocol=https;AccountName=<storage account name>;AccountKey=<storage account key>')

    ls_azure_storage = AzureStorageLinkedService(connection_string=storage_string)
    ls = adf_client.linked_services.create_or_update(rg_name, df_name, ls_name, ls_azure_storage)
    print_item(ls)

    # Create an Azure blob dataset (input)
    ds_name = 'ds_in'
    ds_ls = LinkedServiceReference(ls_name)
    blob_path= 'adftutorial/input'
    blob_filename = 'input.txt'
    ds_azure_blob= AzureBlobDataset(ds_ls, folder_path=blob_path, file_name = blob_filename)
    ds = adf_client.datasets.create_or_update(rg_name, df_name, ds_name, ds_azure_blob)
    print_item(ds)

    # Create an Azure blob dataset (output)
    dsOut_name = 'ds_out'
    output_blobpath = 'adftutorial/output'
    dsOut_azure_blob = AzureBlobDataset(ds_ls, folder_path=output_blobpath)
    dsOut = adf_client.datasets.create_or_update(rg_name, df_name, dsOut_name, dsOut_azure_blob)
    print_item(dsOut)

    # Create a copy activity
    act_name =  'copyBlobtoBlob'
    blob_source = BlobSource()
    blob_sink = BlobSink()
    dsin_ref = DatasetReference(ds_name)
    dsOut_ref = DatasetReference(dsOut_name)
    copy_activity = CopyActivity(act_name,inputs=[dsin_ref], outputs=[dsOut_ref], source=blob_source, sink=blob_sink)

    # Create a pipeline with the copy activity
    p_name =  'copyPipeline'
    params_for_pipeline = {}
    p_obj = PipelineResource(activities=[copy_activity], parameters=params_for_pipeline)
    p = adf_client.pipelines.create_or_update(rg_name, df_name, p_name, p_obj)
    print_item(p)

    # Create a pipeline run
    run_response = adf_client.pipelines.create_run(rg_name, df_name, p_name,
        {
        }
    )

    # Monitor the pipeilne run
    time.sleep(30)
    pipeline_run = adf_client.pipeline_runs.get(rg_name, df_name, run_response.run_id)
    print("\n\tPipeline run status: {}".format(pipeline_run.status))
    activity_runs_paged = list(adf_client.activity_runs.list_by_pipeline_run(rg_name, df_name, pipeline_run.run_id, datetime.now() - timedelta(1),  datetime.now() + timedelta(1)))
    print_activity_run_details(activity_runs_paged[0])

# Start the main method
main()
```

## <a name="run-the-code"></a>Kodu çalıştırma
Uygulamayı derleyip başlatın, ardından işlem hattı yürütmesini doğrulayın.

Konsol; veri fabrikası, bağlı hizmet, veri kümeleri, işlem hattı ve işlem hattı çalıştırmasının ilerleme durumunu yazdırır. Okunan/yazılan veri boyutunu içeren kopyalama etkinliği ayrıntılarını görene kadar bekleyin. Ardından, [Azure Depolama gezgini](https://azure.microsoft.com/features/storage-explorer/) gibi araçlar kullanarak, blobların değişkenlerde belirttiğiniz şekilde "inputBlobPath" yolundan "outputBlobPath" yoluna kopyalandığını doğrulayın.

Örnek çıktı aşağıdaki gibidir:

```json
Name: <data factory name>
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.DataFactory/factories/<data factory name>
Location: eastus
Tags: {}

Name: storageLinkedService
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.DataFactory/factories/<data factory name>/linkedservices/storageLinkedService

Name: ds_in
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.DataFactory/factories/<data factory name>/datasets/ds_in

Name: ds_out
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.DataFactory/factories/<data factory name>/datasets/ds_out

Name: copyPipeline
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.DataFactory/factories/<data factory name>/pipelines/copyPipeline

Pipeline run status: Succeeded
Datetime with no tzinfo will be considered UTC.
Datetime with no tzinfo will be considered UTC.

Activity run details

Activity run status: Succeeded
Number of bytes read: 18
Number of bytes written: 18
Copy duration: 4
```


## <a name="clean-up-resources"></a>Kaynakları temizleme
Veri fabrikasını silmek için aşağıdaki kodu programa ekleyin:

```python
adf_client.factories.delete(rg_name,df_name)
```

## <a name="next-steps"></a>Sonraki adımlar
Bu örnekteki işlem hattı, verileri bir konumdan Azure blob depolama alanındaki başka bir konuma kopyalar. Daha fazla senaryoda Data Factory’yi kullanma hakkında bilgi almak için [öğreticileri](tutorial-copy-data-dot-net.md) okuyun.
