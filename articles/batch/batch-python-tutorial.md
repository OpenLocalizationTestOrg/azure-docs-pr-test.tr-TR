---
title: "aaaTutorial - kullanım hello Python için Azure Batch SDK'sı | Microsoft Docs"
description: "Azure Batch temel kavramlarını Hello öğrenin ve Python kullanarak basit bir çözüm oluşturun."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a>Python için Hello Batch SDK'sı ile çalışmaya başlama

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Merhaba temel bilgileri öğrenmek [Azure Batch] [ azure_batch] ve hello [Batch Python] [ py_azure_sdk] istemci Python'da yazılmış küçük bir Batch uygulamasından aşağıdakiler ele gibi. İki hello buluttaki Linux sanal makinelerde paralel iş yükünü betikleri kullanım hello Batch hizmeti tooprocess nasıl örnek ve ile nasıl etkileşim kurduklarını ele [Azure Storage](../storage/common/storage-introduction.md) dosya hazırlığı ve alımı için. Ortak Batch uygulama iş akışı öğrenin ve hello başlıca Batch bileşenleri işler, görevler, havuzlar gibi temel bir anlayış edinmek ve işlem düğümleri.

![Batch çözümü iş akışı (temel)][11]<br/>

## <a name="prerequisites"></a>Ön koşullar
Bu makalede, Python ve Linux alışkanlığına sahip olduğunuz varsayılmaktadır. Aşağıda Azure ve hello toplu işlem ve depolama hizmetleri için belirtilen mümkün toosatisfy hello hesap oluşturma gerekliliklerini olduğunuzu varsayar.

### <a name="accounts"></a>Hesaplar
* **Azure hesabı**: Henüz bir Azure aboneliğiniz yoksa, [ücretsiz Azure hesabı oluşturun][azure_free_account].
* **Batch hesabı**: Azure aboneliğiniz olduktan sonra, [Azure Batch hesabı oluşturun](batch-account-create-portal.md).
* **Storage hesabı**: Bkz. [Azure Storage hesapları hakkında](../storage/common/storage-create-storage-account.md) sayfası, [Storage hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) bölümü.

### <a name="code-sample"></a>Kod örneği
Merhaba Python Eğitmen [kod örneği] [ github_article_samples] birçok Batch kod örnekleri bulunan hello hello biri [azure-batch-samples] [ github_samples] havuzda GitHub. Tüm hello örnekleri tıklayarak indirebileceğiniz **Kopyala veya indir > ZIP'i indir** hello depo giriş sayfasındaki veya hello tıklatarak [azure-batch-samples-master.zip] [ github_samples_zip]doğrudan indirme bağlantısına. Merhaba hello ZIP dosyasının içeriğini ayıkladıktan sonra Bu öğretici için hello iki betikleri hello bulunan `article_samples` dizini:

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a>Python ortamı
toorun hello *python_tutorial_client.py* örnek betik, yerel iş istasyonunda ihtiyacınız bir **Python yorumlayıcı** sürümüyle uyumlu **2.7** veya **3.3 +**. Merhaba betik Linux ve Windows'da test edilmiştir.

### <a name="cryptography-dependencies"></a>şifreleme bağımlılıkları
Merhaba hello bağımlılıkları yüklemelisiniz [şifreleme] [ crypto] hello tarafından gerekli Kitaplığı `azure-batch` ve `azure-storage` Python paketlerini. Platformunuz için uygun işlemleri aşağıdaki hello birini gerçekleştirin veya toohello başvurun [şifreleme yükleme] [ crypto_install] daha fazla bilgi için ayrıntıları:

* Ubuntu

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* CentOS

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* SLES/OpenSUSE

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* Windows

    `pip install cryptography`

> [!NOTE]
> Python 3.3 + Linux'ta için yüklüyorsanız, hello python3 eşdeğerleri hello Python bağımlılıkları için kullanın. Örneğin, Ubuntu üzerinde: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`
>
>

### <a name="azure-packages"></a>Azure paketleri
Ardından, hello yüklemek **Azure Batch** ve **Azure Storage** Python paketlerini. Kullanarak her iki paketi yükleyebilirsiniz **PIP** ve hello *requirements.txt* burada bulundu:

`/azure-batch-samples/Python/Batch/requirements.txt`

Sorunu aşağıdaki **PIP** komut tooinstall hello Batch ve Storage paketlerini:

`pip install -r requirements.txt`

Veya hello yükleyebilirsiniz [azure-batch] [ pypi_batch] ve [azure depolama] [ pypi_storage] Python paketlerini el ile:

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> Ayrıcalıksız bir hesap kullanıyorsanız, komutlarınıza tooprefix gerekebilir `sudo`. Örneğin, `sudo pip install -r requirements.txt`. Python paketlerini yükleme hakkında daha fazla bilgi için python.org sayfasındaki [Paketleri Yükleme][pypi_install] bölümüne bakın.
>
>

## <a name="batch-python-tutorial-code-sample"></a>Batch Python eğitmen kodu örneği
Merhaba Batch Python Eğitmen kodu örneği, iki Python betiği ve birkaç veri dosyasından oluşur.

* **python_tutorial_client.PY**: (sanal makineler) işlem düğümlerinde paralel iş yükünü hello toplu işlem ve depolama hizmetleri tooexecute ile etkileşim kurar. Merhaba *python_tutorial_client.py* komut dosyası yerel iş istasyonunda çalışır.
* **python_tutorial_task.PY**: çalıştığı hello betik işlem düğümlerini Azure tooperform hello gerçek çalışma. Merhaba örneğinde, *python_tutorial_task.py* hello metni (girdi dosyası hello) Azure Storage'dan indirilen dosyada ayrıştırıyor. Bir metin dosyası oluşturur sonra (Merhaba çıktı dosyası) hello giriş dosyasında görünen hello ilk üç sözcük listesini içerir. Merhaba çıktı dosyasını oluşturduktan sonra *python_tutorial_task.py* karşıya dosya tooAzure depolama hello. İndirme toohello istemci komut dosyası iş istasyonunuza çalıştıran için kullanılabilir yapar. Merhaba *python_tutorial_task.py* işlem hello Batch hizmeti düğümünde birden fazla paralel betik çalışır.
* **./Data/taskdata\*.txt**: hello üzerinde çalıştırmak hello görevleri işlem düğümleri için bu üç metin dosyaları hello girin.

Aşağıdaki diyagramda hello hello istemci ve görev betikleri tarafından gerçekleştirilen birincil işlemleri hello gösterilmektedir. Bu temel iş akışı, Batch’le oluşturulan çok sayıda işlem çözümünün tipik halidir. Bu her özelliğe hello Batch hizmeti uygun olmadığı belirtilirken, neredeyse her Batch senaryosu iş akışının bölümlerini içerir.

![Batch örnek iş akışı][8]<br/>

[**1. Adım.**](#step-1-create-storage-containers) Azure Blob Storage’da **kapsayıcılar** oluşturun.<br/>
[**2. Adım.**](#step-2-upload-task-script-and-data-files) Görev betiğini ve girdi dosyalarını toocontainers karşıya yükleyin.<br/>
[**3. Adım.**](#step-3-create-batch-pool) Batch **havuzu** oluşturun.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Merhaba havuzu **StartTask** yüklemeleri hello görev betiğini (python_tutorial_task.py) toonodes hello havuzuna Katıl gibi.<br/>
[**4. Adım.**](#step-4-create-batch-job) Batch **işi** oluşturun.<br/>
[**5. Adım**](#step-5-add-tasks-to-job) Ekleme **görevleri** toohello işi.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** Merhaba, düğümlerde zamanlanmış tooexecute görevlerdir.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Her görev kendi girdi verilerini Azure Storage’dan indirip yürütmeye başlar.<br/>
[**6. Adım**](#step-6-monitor-tasks) Görevleri izleyin.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Görevlerin tamamlanmasıyla, kendi çıktı veri tooAzure depolama karşıya yükleyin.<br/>
[**7. Adım**](#step-7-download-task-output) Storage’dan görev çıktısını indirin.

Yukarıda belirtildiği gibi, her Batch çözümü tam olarak bu adımları gerçekleştirmese ve çok daha fazlasını içerebilse de; bu örnek, Batch çözümünde bulunan ortak işlemleri göstermektedir.

## <a name="prepare-client-script"></a>İstemci komut dosyasını hazırlama
Merhaba örneği çalıştırmadan önce Batch ve Storage hesabı kimlik bilgilerinizi çok eklemek*python_tutorial_client.py*. Henüz yapmadıysanız, kimlik bilgilerinizle izleyerek, sık kullanılan Düzenleyicisi ve güncelleştirme hello hello dosyasını açın.

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

Batch ve Storage hesabı kimlik bilgilerinizi her hizmetin hesap dikey hello hello bulabilirsiniz [Azure portal][azure_portal]:

![Merhaba portalda batch kimlik bilgileri][9]
![hello portalda Storage kimlik bilgileri][10]<br/>

Aşağıdaki bölümlerde hello biz tarafından kullanılan hello adımları analiz hello tooprocess hello Batch hizmeti iş yükünü komut dosyaları. Düzenli olarak çalışırken toohello betiklere yolunuzu hello makalenin hello rest aracılığıyla iş toorefer öneririz.

Aşağıdaki satırda toohello gidin **python_tutorial_client.py** toostart adım 1:

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a>1. Adım: Storage kapsayıcıları oluşturma
![Azure Depolama'da kapsayıcı oluşturma][1]
<br/>

Azure Storage ilet etkileşimde bulunmak için Batch’te yerleşik destek bulunur. Storage hesabınızdaki kapsayıcılar, Batch hesabınızda çalışan hello görevler için gerekli hello dosyaları sağlar. Merhaba kapsayıcılara hello görevlerin oluşturduğu bir yerde toostore hello çıktı verilerini de sağlar. ilk şey hello hello *python_tutorial_client.py* komut dosyasının yaptığını üç kapsayıcı oluşturmaktır [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):

* **Uygulama**: Bu kapsayıcı hello görevleriniz tarafından çalıştırılan hello Python betiğini depolayacaktır *python_tutorial_task.py*.
* **Giriş**: görevler hello hello veri dosyaları tooprocess yükleyecek *giriş* kapsayıcı.
* **Çıktı**: görevler girdi dosyası işlemeyi tamamladıklarında hello sonuçları toohello karşıya yükleyecek *çıkış* kapsayıcı.

Sipariş toointeract bir depolama hesabı ve kapsayıcı, oluşturma hello kullanırız [azure depolama] [ pypi_storage] toocreate paketini bir [BlockBlobService] [ py_blockblobservice] nesne--hello "blob istemcisi" Ardından üç kapsayıcı hello blob istemcisini kullanarak hello depolama hesabında oluşturuyoruz.

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

Merhaba kapsayıcılara oluşturduktan sonra Merhaba uygulaması artık hello görevler tarafından kullanılacak hello dosyaları karşıya yükleyebilir.

> [!TIP]
> [Nasıl toouse python'dan Azure Blob storage](../storage/blobs/storage-python-how-to-use-blob-storage.md) Azure Storage kapsayıcıları ve blob'larla çalışma hakkında kapsamlı bilgi sağlar. Batch ile çalışmaya başladığınızda okuma listenizin hello yukarıya yakın olması gerekir.
>
>

## <a name="step-2-upload-task-script-and-data-files"></a>2. Adım: Görev betiğini ve veri dosyalarını karşıya yükleme
![Karşıya yükleme görev uygulamasını ve girdi (veri) toocontainers dosyaları][2]
<br/>

Merhaba dosyayı karşıya yükleme işlemi, *python_tutorial_client.py* ilk tanımlar **uygulama** ve **giriş** hello yerel makinede oldukları gibi dosya yolları. Sonra hello önceki adımda oluşturduğunuz bu dosyaları toohello kapsayıcıları yükler.

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

Liste anlamayı kullanarak, hello `upload_file_to_container` çağrıldığında her dosya hello koleksiyonlarda ve iki [ResourceFile] [ py_resource_file] koleksiyonu doldurulur. Merhaba `upload_file_to_container` işlevi aşağıda görünür:

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a>ResourceFiles
A [ResourceFile] [ py_resource_file] hello URL tooa indirilen tooa Azure depolama alanı dosyasında toplu görevlerle işlem düğümü, görev çalıştırılmadan önce sağlar. Merhaba [ResourceFile][py_resource_file].** blob_source** özelliği, Azure Storage'da yer aldığından hello hello dosyanın tam URL'sini belirtir. Merhaba URL ayrıca güvenli erişim toohello dosya sağlayan bir paylaşılan erişim imzası (SAS) içerebilir. Batch’teki çoğu görev türünde *ResourceFiles* özelliği vardır; bu özellikte şunlar bulunur:

* [CloudTask][py_task]
* [StartTask][py_starttask]
* [JobPreparationTask][py_jobpreptask]
* [JobReleaseTask][py_jobreltask]

Bu örnek hello JobPreparationTask veya JobReleaseTask görev türlerini kullanmaz, ancak daha fazla bilgiyi ilgili [iş hazırlama ve tamamlama görevlerini çalıştırma Azure Batch işlem düğümlerinde](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Paylaşılan erişim imzası (SAS)
Paylaşılan erişim imzaları güvenli erişim toocontainers ve Azure Storage blobları sağlayan dizelerdir. Merhaba *python_tutorial_client.py* betiği hem blob kullanır ve kapsayıcı paylaşılan erişim imzası ve nasıl tooobtain bu paylaşılan erişim imzası dizeleri depolama hizmeti hello gösterir.

* **Blob paylaşılan erişim imzaları**: depolama biriminden hello görev betiğini ve girdi veri dosyalarını indirdiğinde blob paylaşılan erişim imzaları hello havuza ait StartTask kullanır (bkz [3. adım](#step-3-create-batch-pool) aşağıda). Merhaba `upload_file_to_container` işlevi *python_tutorial_client.py* her blob'un paylaşılan erişim imzasını alan hello kodunu içerir. Bunu çağırarak yapar [BlockBlobService.make_blob_url] [ py_make_blob_url] hello depolama modülü.
* **Kapsayıcı paylaşılan erişim imzası**: her görev hello işlem düğümü işini bitirdiğinde, kendi çıktı dosyasını toohello yükler *çıkış* Azure storage'da kapsayıcı. toodo bunu *python_tutorial_task.py* toohello kapsayıcısına yazma erişimi sağlayan kapsayıcı paylaşılan erişim imzasını kullanır. Merhaba `get_container_sas_token` işlevi *python_tutorial_client.py* daha sonra bir komut satırı bağımsız değişkeni toohello görevleri olarak geçirilir hello kapsayıcının paylaşılan erişim imzasını alır. #5. adım [Ekle görevleri tooa iş](#step-5-add-tasks-to-job), hello hello kapsayıcı SAS kullanımını açıklar.

> [!TIP]
> Hello iki parçalı seriyi kullanıma paylaşılan erişim imzalarındaki [1. Bölüm: Merhaba SAS modelini anlama](../storage/common/storage-dotnet-shared-access-signature-part-1.md) ve [Kısım 2: oluşturma ve bir SAS hello Blob hizmeti ile kullanma](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn güvenli erişim sağlama hakkında daha fazla bilgi Depolama hesabınızdaki toodata.
>
>

## <a name="step-3-create-batch-pool"></a>3. Adım: Batch havuzu oluşturma
![Batch havuzu oluşturma][3]
<br/>

Batch **havuzu**, Batch’in işe ait görevleri yürüttüğü işlem düğümlerinin (sanal makineler) koleksiyonudur.

Merhaba görev betiğini ve veri dosyalarını toohello depolama hesabı, gönderildikten sonra *python_tutorial_client.py* hello Batch Python modülünü kullanarak hello Batch hizmetiyle etkileşimi başlatır. toodo bunu bir [BatchServiceClient] [ py_batchserviceclient] oluşturulur:

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

Ardından, işlem düğümleri havuzu hello çağrısıyla Batch hesabında çok oluşturulan`create_pool`.

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Bir havuz oluşturduğunuzda, tanımladığınız bir [PoolAddParameter] [ py_pooladdparam] hello havuz için bazı özellikler belirtir:

* **Kimliği** hello havuzunun (*kimliği* - gerekli)<p/>Batch’deki çoğu varlık gibi, yeni havuzunuzda da, Batch hesabınızın içinde benzersiz bir kimlik olmalıdır. Kodunuzu toothis havuz Kimliğini kullanarak ifade eder ve hello Azure hello havuzunda şekilde tanımlarsınız [portal][azure_portal].
* **İşlem düğümleri sayısı** (*target_dedicated* - gerekli)<p/>Bu özellik hello havuzda kaç VM dağıtılması gerekir belirtir. Tüm Batch hesaplarının bir varsayılan olması önemli toonote olan **kota** sınırları sayısı hello **çekirdek** (ve dolayısıyla işlem düğümleriyle) bir Batch hesabında. Merhaba varsayılan kotalar ve yönergeleri hakkında çok bulabileceğiniz[kota artırma](batch-quota-limit.md#increase-a-quota) (örneğin, çekirdek Batch hesabınızdaki en yüksek sayısı hello) içinde [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md). Kendinizi "Neden havuzum X düğümden fazlasına ulaşamıyor?" sorusunu sorarken bulursanız Bu çekirdek kotası hello neden olabilir.
* Düğümler için **işletim sistemi** (*virtual_machine_configuration***veya***cloud_service_configuration* - gerekli)<p/>*python_tutorial_client.py* öğesinde [VirtualMachineConfiguration][py_vm_config] kullanarak Linux için havuz oluşturuyoruz. Merhaba `select_latest_verified_vm_image_with_node_agent_sku` işlevi `common.helpers` çalışmak basitleştirir [Azure Virtual Machines Marketi] [ vm_marketplace] görüntüler. Market görüntülerini kullanma hakkında daha fazla bilgi için bkz. [Azure Batch havuzlarında Linux işlem düğümlerini hazırlama](batch-linux-nodes.md).
* **İşlem düğümlerinin boyutu** (*vm_size* - gerekli)<p/>[VirtualMachineConfiguration][py_vm_config] için Linux düğümleri belirlediğimizden, bir VM boyutunu (bu örnekte `STANDARD_A1`) [Azure’de sanal makine boyutları](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)’nda belirttik. Bir kez daha, daha fazla bilgi için bkz. [Azure Batch havuzlarında Linux işlem düğümlerini hazırlama](batch-linux-nodes.md).
* **Görev Başlat** (*start_task* - gerekli değil)<p/>Yukarıdaki fiziksel düğüm özellikleri Hello yanı sıra siz de belirtebilir bir [StartTask] [ py_starttask] hello havuzu (gerekli değildir). Bu düğüme hello havuzuna katılır ve her bir düğümü yeniden Hello StartTask her düğümde yürütür. Merhaba StartTask özellikle Merhaba, görevlerinizin çalıştığı hello uygulamaları yükleme gibi görevlerini yürütülmesi için işlem düğümlerinin hazırlanmasında yararlıdır.<p/>Bu örnek uygulamasında hello StartTask, Storage'dan indirilen hello dosyaları kopyalar (hangi belirtilen hello StartTask'ın kullanarak **resource_files** özelliği) hello StartTask gelen *çalışma dizini* toohello *paylaşılan* hello düğüm üzerinde çalışan tüm görevlerin dizin. Esas olarak, bu kopyalar `python_tutorial_task.py` toohello paylaşılan her düğüme hello düğümü hello havuza katılmış olduğundan hello düğümü üzerinde çalışacak herhangi bir görevi erişebilmesi.

Merhaba çağrısı toohello karşılaşabilirsiniz `wrap_commands_in_shell` yardımcı işlevi. Bu işlev ayrı komutların koleksiyonunu alır ve görevin komut satırı özelliğine uygun tek bir komut satırı oluşturur.

Ayrıca içinde yukarıdaki hello kod parçacığında dikkat çeken bir şey hello hello iki ortam değişkenleri kullanımıdır **command_line** hello StartTask özelliğinin: `AZ_BATCH_TASK_WORKING_DIR` ve `AZ_BATCH_NODE_SHARED_DIR`. Batch havuzundaki her işlem düğümü belirli tooBatch olan birkaç ortam değişkenlerini otomatik olarak yapılandırılır. Bir görev tarafından yürütülen herhangi bir işlem toothese ortam değişkenlerine erişim vardır.

> [!TIP]
> bir Batch havuzu yanı sıra görev çalışma dizinleri hakkında bilgilerin işlem düğümlerinde kullanılabilir hello ortam değişkenleri hakkında daha fazla toofind bkz **görevler için ortam ayarları** ve **dosyalar ve dizinler ** hello içinde [Azure Batch özelliklerine genel bakış](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>4. Adım: Batch işi oluşturma
![Batch işi oluşturma][4]<br/>

Batch **işi**, görevler koleksiyonudur ve işlem düğümlerinin bir havuzuyla ilişkilidir. Merhaba görevleri bir işlemle ilişkili hello havuzun işlem düğümleri üzerinde yürütün.

İş önceliği, ilişkisi tooother işlerini hello toplu işlem hesabı ve bir işi yalnızca ilgili iş yüklerinde görevlerin düzenlenmesi ve için aynı zamanda hello en fazla çalışma hello işin (ve uzantılarının, görevleri) gibi bazı kısıtlamalar izlenmesi için kullanabilirsiniz. Bu örnekte, ancak hello iş #3. adımda oluşturulan hello havuzu ile ilişkilidir. Yapılandırılmış başka ek özellik yoktur.

Tüm Batch işleri belirli bir havuzla ilişkilidir. Bu ilişkilendirme hello işin görevlerinin hangi düğümleri gösterir. Hello kullanarak hello havuzu belirtin [Poolınformation] [ py_poolinfo] hello aşağıdaki kod parçacığında gösterildiği gibi özelliği.

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Bir işi oluşturuldu, görevler tooperform hello iş eklenir.

## <a name="step-5-add-tasks-toojob"></a>5. adım: görevleri toojob ekleme
![Görevleri toojob Ekle][5]<br/>
*(1) görevler toohello iş eklenir, düğümlerde zamanlanmış toorun (2) hello görevlerdir ve (3) hello görevleri hello veri dosyaları tooprocess indirme*

Toplu **görevleri** hello üzerinde yürütülen hello tek tek iş birimleri işlem düğümlerini şunlardır. Bir görev, bir komut satırı ve hello komut dosyaları veya bu komut satırında belirttiğiniz yürütülebilir dosyaları çalıştırır.

tooactually gerçekleştirmek iş, görevleri tooa iş eklenmesi gerekir. Her [CloudTask] [ py_task] komut satırı özelliğiyle birlikte yapılandırılan ve [ResourceFiles] [ py_resource_file] (Merhaba havuza ait startTask gibi) bu hello komut satırı otomatik olarak yürütülmeden önce görevin toohello düğümü indirir. Merhaba örnekte, her görev yalnızca bir dosya işler. Bu nedenle, kendi ResourceFiles koleksiyonunda tek bir öğe bulunmaktadır.

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> Ortam değişkenlerine eriştiklerinde gibi `$AZ_BATCH_NODE_SHARED_DIR` veya hello düğümün bulunmayan bir uygulama yürüttüklerinde `PATH`, görev komut satırları hello çağırma gerekir açıkça gibi kabuğunda `/bin/sh -c MyTaskApplication $MY_ENV_VAR`. Bu gereksinim, görevlerinizin hello düğümün bir uygulama yürütüyorsa gereksizdir `PATH` ve herhangi bir ortam değişkeni başvurusu değil.
>
>

Merhaba içinde `for` Yukarıdaki kod parçacığında hello döngüde hello komut satırı hello görev için çok geçirilen beş komut satırı bağımsız değişkenlerini ile oluşturulur görebilirsiniz*python_tutorial_task.py*:

1. **FilePath**: hello düğümde yer aldığından bu hello yerel yol toohello dosyasıdır. ResourceFile nesnesi'ne zaman hello `upload_file_to_container` oluşturulduğu yukarıdaki adım 2'de hello dosya adı bu özellik için kullanılır (Merhaba `file_path` hello ResourceFile oluşturucuda parametresinde). Bu, hello dosya bulunabilir hello aynı gösterir hello düğümü olarak dizininde *python_tutorial_task.py*.
2. **NumWords**: hello üst *N* sözcükler toohello çıktı dosyasına yazılması gerekir.
3. **storageaccount**: hello hello hello kapsayıcı toowhich hello görev çıktısını sahibi depolama hesabı adını karşıya yüklenebilir.
4. **storagecontainer**: hello depolama kapsayıcısı toowhich hello hello adını çıktı dosyaları karşıya yüklenebilir.
5. **sastoken**: yazma erişimi toohello sağlayan hello paylaşılan erişim imzası (SAS) **çıkış** Azure storage'da kapsayıcı. Merhaba *python_tutorial_task.py* komut dosyası bu paylaşılan erişim imzasını kullanır, kendi BlockBlobService başvurusunu oluşturduğunda. Bu, yazma erişimi toohello kapsayıcı hello depolama hesabı için erişim anahtarı gerekmeden sağlar.

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a>6. Adım: Görevleri izleme
![Görevleri izleme][6]<br/>
*komut dosyası (1) izleyiciler hello görevleri tamamlama durumu için hello ve (2) hello görevler de sonuç verilerini tooAzure depolama yükler*

Görevleri tooa iş eklendiğinde bunlar otomatik olarak kuyruğa ve hello işle ilişkili hello havuzundaki işlem düğümlerinde yürütülmesi için zamanlanan. Belirttiğiniz hello ayarlarına bağlı olarak, Batch tüm kuyruğa alınan, zamanlama, yeniden deneniyor ve diğer görev yönetimi görevlerini işler.

Toomonitoring görev yürütme birçok yaklaşım vardır. Merhaba `wait_for_tasks_to_complete` işlevi *python_tutorial_client.py* hello bu durumda, belirli bir durumu için görevleri izlemenin basit bir örnek sağlar [tamamlandı] [ py_taskstate] durumu.

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a>7. Adım: Görev çıktısı indirme
![Storage'dan görev çıktısını indirme][7]<br/>

Merhaba iş tamamlandığında, hello görevleri hello çıktısını Azure Storage'dan indirilebilir. Bu çağrı çok yapılır`download_blobs_from_container` içinde *python_tutorial_client.py*:

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> Çağrı çok hello`download_blobs_from_container` içinde *python_tutorial_client.py* hello dosyaları indirilen tooyour giriş dizini olması gerektiğini belirtir. Ücretsiz toomodify düşünüyorsanız bu konumu çıktı.
>
>

## <a name="step-8-delete-containers"></a>8. Adım: Sil kapsayıcıları
Azure Storage'da yer alan veriler için ücretlendirildiğinizden, Batch işleriniz için artık BLOB'lar gerekli bir fikir tooremove her zaman olduğu. İçinde *python_tutorial_client.py*, bu çok sahip üç çağrı yapılır[BlockBlobService.delete_container][py_delete_container]:

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>9. adım: hello işi ve hello havuzu silme
Merhaba tarafından oluşturulan istendiğinde toodelete hello iş ve hello havuzu olduğunuz Hello son adımda *python_tutorial_client.py* komut dosyası. İşlerin ve görevlerin kendileri için sizden ücret istenmese de, işlem düğümleri için *ücret* istenecektir. Bu nedenle, düğümleri yalnızca gerektiğinde ayırmanız önerilir. Kullanılmayan havuzların silinmesi bakım işleminizin bir parçası olabilir.

Merhaba BatchServiceClient's [JobOperations] [ py_job] ve [PoolOperations] [ py_pool] her ikisi de olan ilgili silme yöntemleri vardır silme işlemini onaylamak olursa çağrılır:

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> İşlem kaynaklarının ücretli olduğunu unutmayın; kullanılmayan havuzların silinmesi masrafları azaltacaktır. Ayrıca, bir havuzun silinmesinin Bu havuz içindeki tüm işlem düğümlerini siler ve hello havuz silindikten sonra hello düğümlerinde tüm veriler kurtarılamaz olacağını unutmayın.
>
>

## <a name="run-hello-sample-script"></a>Merhaba örnek betiği çalıştırma
Merhaba çalıştırdığınızda *python_tutorial_client.py* hello öğretici betikten [kod örneği][github_article_samples], hello konsol çıktısı benzer toohello aşağıdaki verilir. Konumunda bir duraklama yoktur `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` hello havuzun işlem düğümleri oluşturulur, başlatıldığından ve hello havuzun görev başlatma hello komutlarda çalıştırılır. Kullanım hello [Azure portal] [ azure_portal] toomonitor havuzu, işlem düğümleri, işi ve görevleri yürütme sırasında ve sonrasında. Kullanım hello [Azure portal] [ azure_portal] veya hello [Microsoft Azure Storage Gezgini] [ storage_explorer] tooview hello depolama kaynaklarını (kapsayıcılar ve bloblar) Merhaba uygulama tarafından oluşturulur.

> [!TIP]
> Merhaba çalıştırmak *python_tutorial_client.py* hello içinde komut gelen `azure-batch-samples/Python/Batch/article_samples` dizin. Merhaba göreli bir yol kullanır `common.helpers` görebilirsiniz için modülü içe aktarma `ImportError: No module named 'common'` bu dizin içinde hello betikten çalıştırmazsanız.
>
>

Tipik yürütme süresi **yaklaşık 5-7 dakika** çalıştırdığınızda hello örnek varsayılan yapılandırmasında.

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a>Sonraki adımlar
Ücretsiz toomake değişiklikleri çok eşitleyerek*python_tutorial_client.py* ve *python_tutorial_task.py* tooexperiment farklı olan işlem senaryoları. Örneğin, bir yürütme gecikmesi çok eklemeyi deneyin*python_tutorial_task.py* uzun süre çalışan toosimulate görevler ve bunları hello Portalı'nda izleyebilirsiniz. Deneyin daha fazla görev eklemeye veya işlem düğümleri hello sayısını ayarlama. İçin mantığı toocheck eklemek ve varolan bir havuzu toospeed yürütme saati hello kullanılmasına izin verin.

Merhaba temel iş akışı Batch çözümünün ile tanıdık, zaman toodig hello Batch hizmetinin ek özelliklerinin toohello içinde olduğu.

* Gözden geçirme hello [genel bakış Azure Batch özelliklerine](batch-api-basics.md) yeni toohello hizmeti olup olmadığınızı öneririz makalesi.
* Başlat'hello altında diğer Batch geliştirmesi makalelerine **geliştirme ayrıntılı** hello içinde [Batch öğrenme yolu][batch_learning_path].
* Merhaba toplu ile Merhaba "ilk N sözcük" iş yükünü işlemenin farklı bir uygulama kullanıma [TopNWords] [ github_topnwords] örnek.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Azure Depolama’da kapsayıcı oluşturma"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Karşıya yükleme görev uygulamasını ve girdi (veri) toocontainers dosyaları"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Batch havuzu oluşturma"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Batch işi oluşturma"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Görevleri toojob Ekle"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Görevleri izleme"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Depolama’dan görev çıkışını indirme"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Batch çözümü iş akışı (tam diyagram)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Portalda Batch kimlik bilgileri"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Portalda Depolama kimlik bilgileri"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Batch çözümü iş akışı (minimal diyagram)"
