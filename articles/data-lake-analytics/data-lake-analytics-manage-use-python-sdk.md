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
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="529a5-103">Python kullanarak Azure Data Lake Analytics yönetme</span><span class="sxs-lookup"><span data-stu-id="529a5-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="529a5-104">Python sürümleri</span><span class="sxs-lookup"><span data-stu-id="529a5-104">Python versions</span></span>

* <span data-ttu-id="529a5-105">Python 64-bit sürümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="529a5-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="529a5-106">Bulunan hello standart Python dağıtım kullanabileceğiniz  **[Python.org indirmeleri](https://www.python.org/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="529a5-106">You can use hello standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="529a5-107">İsteğe bağlı olarak pek çok geliştirici uygun toouse hello bulur  **[Anaconda Python dağıtım](https://www.continuum.io/downloads)**.</span><span class="sxs-lookup"><span data-stu-id="529a5-107">Many developers find it convenient toouse hello **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="529a5-108">Bu makalede, Python hello standart Python dağıtım 3.6 sürümünden kullanılarak yazılmıştır</span><span class="sxs-lookup"><span data-stu-id="529a5-108">This article was written using Python version 3.6 from hello standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="529a5-109">Azure Python SDK’yı yükleme</span><span class="sxs-lookup"><span data-stu-id="529a5-109">Install Azure Python SDK</span></span>

<span data-ttu-id="529a5-110">Modüller aşağıdaki hello yükleyin:</span><span class="sxs-lookup"><span data-stu-id="529a5-110">Install hello following modules:</span></span>

* <span data-ttu-id="529a5-111">Merhaba **azure mgmt kaynak** modülü, Active Directory, vb. için diğer Azure modüller içerir.</span><span class="sxs-lookup"><span data-stu-id="529a5-111">hello **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="529a5-112">Merhaba **mgmt datalake depolama azure** modülü hello Azure Data Lake Store hesabı yönetim işlemlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="529a5-112">hello **azure-mgmt-datalake-store** module includes hello Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="529a5-113">Merhaba **azure datalake depolama** modülü hello Azure Data Lake Store dosya sistemi işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="529a5-113">hello **azure-datalake-store** module includes hello Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="529a5-114">Merhaba **azure datalake analytics** modülü hello Azure Data Lake Analytics işlemlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="529a5-114">hello **azure-datalake-analytics** module includes hello Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="529a5-115">İlk olarak, hello son olduğundan emin olun `pip` hello aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="529a5-115">First, ensure you have hello latest `pip` by running hello following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="529a5-116">Bu belge kullanılarak yazılmıştır `pip version 9.0.1`.</span><span class="sxs-lookup"><span data-stu-id="529a5-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="529a5-117">Merhaba aşağıdaki kullanın `pip` tooinstall hello hello commandline modüllerden komutlar:</span><span class="sxs-lookup"><span data-stu-id="529a5-117">Use hello following `pip` commands tooinstall hello modules from hello commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="529a5-118">Yeni bir Python komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="529a5-118">Create a new Python script</span></span>

<span data-ttu-id="529a5-119">Başlangıç komut dosyanıza koddan hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="529a5-119">Paste hello following code into hello script:</span></span>

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

<span data-ttu-id="529a5-120">Bu komut dosyası tooverify modülleri içeri aktarılabilir, hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="529a5-120">Run this script tooverify that hello modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="529a5-121">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="529a5-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="529a5-122">Açılır pencere ile etkileşimli kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="529a5-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="529a5-123">Bu yöntem desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="529a5-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="529a5-124">Bir aygıt koduyla etkileşimli kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="529a5-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="529a5-125">Etkileşimli olmayan kimlik doğrulamasıyla SPI ve gizlilik</span><span class="sxs-lookup"><span data-stu-id="529a5-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="529a5-126">API ve bir sertifika ile etkileşimli olmayan kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="529a5-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="529a5-127">Bu yöntem desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="529a5-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="529a5-128">Genel komut dosyası değişkenleri</span><span class="sxs-lookup"><span data-stu-id="529a5-128">Common script variables</span></span>

<span data-ttu-id="529a5-129">Bu değişkenler hello örneklerinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="529a5-129">These variables are used in hello samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a><span data-ttu-id="529a5-130">Merhaba istemcileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="529a5-130">Create hello clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="529a5-131">Azure Kaynak Grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="529a5-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="529a5-132">Data Lake Analytics hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="529a5-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="529a5-133">Önce bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="529a5-133">First create a store account.</span></span>

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
<span data-ttu-id="529a5-134">Ardından, bu depoyu kullanan bir ADLA hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="529a5-134">Then create an ADLA account that uses that store.</span></span>

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

## <a name="submit-a-job"></a><span data-ttu-id="529a5-135">Bir işi gönderin</span><span class="sxs-lookup"><span data-stu-id="529a5-135">Submit a job</span></span>

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

## <a name="wait-for-a-job-tooend"></a><span data-ttu-id="529a5-136">Bir iş tooend bekle</span><span class="sxs-lookup"><span data-stu-id="529a5-136">Wait for a job tooend</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="529a5-137">Liste ardışık düzen ve tekrarları</span><span class="sxs-lookup"><span data-stu-id="529a5-137">List pipelines and recurrences</span></span>
<span data-ttu-id="529a5-138">İşleriniz bağlı ardışık düzen veya yineleme meta verileri sahip olup olmadığınızı bağlı olarak, ardışık düzen ve tekrarları listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="529a5-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="529a5-139">İşlem ilkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="529a5-139">Manage compute policies</span></span>

<span data-ttu-id="529a5-140">bir Data Lake Analytics hesabı için ilkeler hello yönetme için yöntemleri işlem Hello DataLakeAnalyticsAccountManagementClient nesnesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="529a5-140">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="529a5-141">Liste işlem ilkeleri</span><span class="sxs-lookup"><span data-stu-id="529a5-141">List compute policies</span></span>

<span data-ttu-id="529a5-142">koddan hello Data Lake Analytics hesabı için işlem ilkelerinin bir listesini alır.</span><span class="sxs-lookup"><span data-stu-id="529a5-142">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="529a5-143">Yeni bir işlem ilke oluşturun</span><span class="sxs-lookup"><span data-stu-id="529a5-143">Create a new compute policy</span></span>

<span data-ttu-id="529a5-144">bir Data Lake Analytics hesabı için yeni bir işlem İlkesi koddan hello oluşturur, ayarı hello maksimum Avustralya kullanılabilir toohello belirtilen kullanıcı too50 ve hello en düşük iş önceliği too250.</span><span class="sxs-lookup"><span data-stu-id="529a5-144">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="529a5-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="529a5-145">Next steps</span></span>

- <span data-ttu-id="529a5-146">toosee hello aynı öğreticiyi diğer araçları kullanarak, hello sekmesini seçiciler hello sayfasının hello üstte'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="529a5-146">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
- <span data-ttu-id="529a5-147">U-SQL, toolearn bkz [Azure Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="529a5-147">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="529a5-148">Yönetim görevleri için bkz. [Azure portalı kullanarak Azure Data Lake Analytics'i yönetme](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="529a5-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

