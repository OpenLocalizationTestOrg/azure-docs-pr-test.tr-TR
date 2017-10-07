---
title: Azure Data Lake Analytics aaaManage Python kullanarak | Microsoft Docs
description: "Bir Data Lake toouse Python toocreate nasıl depolamak öğrenin hesabını ve işleri göndermek. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: d4213a19-4d0f-49c9-871c-9cd6ed7cf731
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 3c0fff155db7c4fd4e84c2562816995eb156be16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a>Python kullanarak Azure Data Lake Analytics yönetme

## <a name="python-versions"></a>Python sürümleri

* Python 64-bit sürümünü kullanın.
* Bulunan hello standart Python dağıtım kullanabileceğiniz  **[Python.org indirmeleri](https://www.python.org/downloads/)**. 
* İsteğe bağlı olarak pek çok geliştirici uygun toouse hello bulur  **[Anaconda Python dağıtım](https://www.continuum.io/downloads)**.  
* Bu makalede, Python hello standart Python dağıtım 3.6 sürümünden kullanılarak yazılmıştır

## <a name="install-azure-python-sdk"></a>Azure Python SDK’yı yükleme

Modüller aşağıdaki hello yükleyin:

* Merhaba **azure mgmt kaynak** modülü, Active Directory, vb. için diğer Azure modüller içerir.
* Merhaba **mgmt datalake depolama azure** modülü hello Azure Data Lake Store hesabı yönetim işlemlerini içerir.
* Merhaba **azure datalake depolama** modülü hello Azure Data Lake Store dosya sistemi işlemleri içerir. 
* Merhaba **azure datalake analytics** modülü hello Azure Data Lake Analytics işlemlerini içerir. 

İlk olarak, hello son olduğundan emin olun `pip` hello aşağıdaki komutu çalıştırarak:

```
python -m pip install --upgrade pip
```

Bu belge kullanılarak yazılmıştır `pip version 9.0.1`.

Merhaba aşağıdaki kullanın `pip` tooinstall hello hello commandline modüllerden komutlar:

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a>Yeni bir Python komut dosyası oluşturma

Başlangıç komut dosyanıza koddan hello yapıştırın:

```python
## Use this only for Azure AD service-to-service authentication
#from azure.common.credentials import ServicePrincipalCredentials

## Use this only for Azure AD end-user authentication
#from azure.common.credentials import UserPassCredentials

## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

## Required for Azure Data Lake Analytics catalog management
from azure.mgmt.datalake.analytics.catalog import DataLakeAnalyticsCatalogManagementClient

## Use these as needed for your application
import logging, getpass, pprint, uuid, time
```

Bu komut dosyası tooverify modülleri içeri aktarılabilir, hello çalıştırın.

## <a name="authentication"></a>Kimlik Doğrulaması

### <a name="interactive-user-authentication-with-a-pop-up"></a>Açılır pencere ile etkileşimli kullanıcı kimlik doğrulaması

Bu yöntem desteklenmiyor.

### <a name="interactive-user-authentication-with-a-device-code"></a>Bir aygıt koduyla etkileşimli kullanıcı kimlik doğrulaması

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a>Etkileşimli olmayan kimlik doğrulamasıyla SPI ve gizlilik

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a>API ve bir sertifika ile etkileşimli olmayan kimlik doğrulaması

Bu yöntem desteklenmiyor.

## <a name="common-script-variables"></a>Genel komut dosyası değişkenleri

Bu değişkenler hello örneklerinde kullanılır.

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a>Merhaba istemcileri oluşturma

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a>Azure Kaynak Grubu oluşturma

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a>Data Lake Analytics hesabı oluşturma

Önce bir depolama hesabı oluşturun.

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```
Ardından, bu depoyu kullanan bir ADLA hesabı oluşturun.

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```

## <a name="submit-a-job"></a>Bir işi gönderin

```python
script = """
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

## <a name="wait-for-a-job-tooend"></a>Bir iş tooend bekle

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a>Liste ardışık düzen ve tekrarları
İşleriniz bağlı ardışık düzen veya yineleme meta verileri sahip olup olmadığınızı bağlı olarak, ardışık düzen ve tekrarları listeleyebilirsiniz.

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a>İşlem ilkelerini yönetme

bir Data Lake Analytics hesabı için ilkeler hello yönetme için yöntemleri işlem Hello DataLakeAnalyticsAccountManagementClient nesnesi sağlar.

### <a name="list-compute-policies"></a>Liste işlem ilkeleri

koddan hello Data Lake Analytics hesabı için işlem ilkelerinin bir listesini alır.

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a>Yeni bir işlem ilke oluşturun

bir Data Lake Analytics hesabı için yeni bir işlem İlkesi koddan hello oluşturur, ayarı hello maksimum Avustralya kullanılabilir toohello belirtilen kullanıcı too50 ve hello en düşük iş önceliği too250.

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a>Sonraki adımlar

- toosee hello aynı öğreticiyi diğer araçları kullanarak, hello sekmesini seçiciler hello sayfasının hello üstte'ı tıklatın.
- U-SQL, toolearn bkz [Azure Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).
- Yönetim görevleri için bkz. [Azure portalı kullanarak Azure Data Lake Analytics'i yönetme](data-lake-analytics-manage-use-portal.md).

