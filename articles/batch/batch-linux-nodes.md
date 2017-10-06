---
title: "Sanal makinedeki aaaRun Linux işlem düğümlerini - Azure Batch | Microsoft Docs"
description: "Nasıl tooprocess, paralel işlem iş yükleri hakkında bilgi edinin Linux sanal makinelerin Azure Batch havuzları."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3daabd5c577baaafd0544f9f7913cb7b116d74d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a>Batch havuzlarında Linux işlem düğümlerini sağlama

Azure Batch toorun paralel işlem iş yükleri hem Linux hem de Windows sanal makinelerde kullanabilirsiniz. Bu makalede nasıl toocreate havuzları Linux hello Batch hizmetindeki her iki hello kullanarak işlem düğümleri ayrıntıları [Batch Python] [ py_batch_package] ve [Batch .NET] [ api_net] istemci kitaplıkları.

> [!NOTE]
> Uygulama paketleri 5 Temmuz 2017’den sonra oluşturulmuş tüm Batch havuzlarında desteklenir. Bunlar yalnızca hello havuzu, bir bulut Hizmeti Yapılandırması kullanılarak oluşturulduysa 10 Mart 2016 ve 5 Temmuz 2017 arasında oluşturulan Batch havuzu üzerinde desteklenir. Önceki too10 Mart 2016 oluşturulan batch havuzları, uygulama paketleri desteklemez. Uygulama hakkında daha fazla bilgi toodeploy uygulamaları tooyour toplu düğümleriniz paketleri için bkz: [Batch uygulama paketleriyle uygulama toocompute düğümlerini dağıtmak](batch-application-packages.md).
>
>

## <a name="virtual-machine-configuration"></a>Sanal Makine Yapılandırması
Toplu işlem düğümleri havuzu oluşturduğunuzda, hangi tooselect hello düğüm boyutu ve işletim sistemi iki seçeneğiniz vardır: Bulut Hizmetleri Yapılandırması ve sanal makine yapılandırma.

**Cloud Services Yapılandırması** *yalnızca* Windows işlem düğümleri sağlar. Kullanılabilir işlem düğümü boyutları içinde listelenen [Cloud Services boyutları](../cloud-services/cloud-services-sizes-specs.md), ve kullanılabilir işletim sistemlerine hello listelenen [Azure konuk işletim sistemi sürümleri ve SDK uyumluluk matrisi](../cloud-services/cloud-services-guestos-update-matrix.md). Azure Cloud Services düğümleri içeren bir havuz oluşturduğunuzda, hello düğüm boyutu belirtin ve hello hello açıklanan işletim sistemi ailesi önceden makaleleri belirtiliyor. Bulut Hizmetleri, Windows havuzları işlem düğümleri için en yaygın olarak kullanılır.

**Sanal Makine Yapılandırması** işlem düğümleri için hem Linux hem de Windows görüntüleri sağlar. Kullanılabilir işlem düğümü boyutları içinde listelenen [azure'da sanal makineler için Boyutlar](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) ve [azure'da sanal makineler için Boyutlar](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows). Sanal Makine Yapılandırması düğümleri içeren bir havuz oluşturduğunuzda hello düğümleri, hello sanal makine görüntü başvurusunu ve hello toplu işlem düğüm Aracısı SKU toobe hello düğümlerinde yüklü hello boyutunu belirtmeniz gerekir.

### <a name="virtual-machine-image-reference"></a>Sanal makine görüntü başvurusunu
Batch hizmetini kullanan hello [sanal makine ölçek kümeleri](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux işlem düğümlerini. Merhaba görüntüden belirtebilirsiniz [Azure Marketi][vm_marketplace], veya hazırladığınız özel bir görüntü sağlayın. Özel görüntüler hakkında daha fazla ayrıntı için bkz. [Batch ile büyük ölçekli paralel işlem çözümleri geliştirme](batch-api-basics.md#pool).

Bir sanal makine görüntü başvurusunu yapılandırdığınızda hello sanal makine görüntüsünün hello özelliklerini belirtin. bir sanal makine görüntü başvurusunu oluşturduğunuzda, aşağıdaki özelliklere hello gereklidir:

| **Resim başvurusu özellikleri** | **Örnek** |
| --- | --- |
| Yayımcı |Canonical |
| Sunduğu |UbuntuServer |
| SKU |14.04.4-LTS |
| Sürüm |en son |

> [!TIP]
> Bu özellikler ve nasıl içinde toolist Market görüntüleri hakkında daha fazla bilgiyi [gidin ve Azure CLI veya PowerShell ile select Linux sanal makine görüntüleri](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Tüm Market görüntülerini Batch ile şu anda uyumlu olduğunu unutmayın. Daha fazla bilgi için bkz: [düğümü aracı SKU'sunu](#node-agent-sku).
>
>

### <a name="node-agent-sku"></a>Düğüm Aracısı SKU
Merhaba toplu işlem düğüm Aracısı hello havuzdaki her düğüme çalışır ve hello düğümü hello Batch hizmeti arasında hello komut ve denetim arabirimi sağlayan bir programdır. Farklı işletim sistemleri için SKU'ları bilinen hello düğüm Aracısı'nın farklı uygulamaları vardır. Esas olarak, bir sanal makine yapılandırması oluşturduğunuzda, ilk hello sanal makine görüntü başvurusunu belirtin ve ardından hello görüntüde hello düğüm Aracısı tooinstall belirtin. Genellikle, her düğüm Aracısı SKU birden çok sanal makine görüntüsü ile uyumludur. Düğüm Aracısı SKU'ları bazı örnekleri şunlardır:

* Batch.node.ubuntu 14.04
* Batch.node.centos 7
* Batch.node.Windows amd64

> [!IMPORTANT]
> Merhaba Market kullanılabilir tüm sanal makine görüntülerini hello şu anda kullanılabilir toplu düğümü aracıları ile uyumlu değildir. Sanal makine görüntülerini uyumlu oldukları hello ve Hello Batch SDK'ları toolist hello kullanılabilir düğüm Aracısı SKU'ları kullanın. Hello bkz [listesi, sanal makine görüntülerini](#list-of-virtual-machine-images) daha fazla bilgi ve örnekler için bu makalenin sonraki tooretrieve çalışma zamanında geçerli görüntüleri listesi.
>
>

## <a name="create-a-linux-pool-batch-python"></a>Bir Linux havuzu oluşturun: Batch Python
Merhaba aşağıdaki kod parçacığını bir örnek nasıl gösterir toouse hello [Python için Microsoft Azure Batch istemci Kitaplığı] [ py_batch_package] toocreate Ubuntu Server havuzu işlem düğümlerini. Başvuru belgelerini Batch Python modülü bulunabilir hello için [azure.batch paket] [ py_batch_docs] okuma hello belgeleri üzerinde.

Bu kod parçacığında oluşturur bir [Imagereference] [ py_imagereference] açıkça ve her (yayımcı, teklif, SKU, sürüm) özelliklerini belirtir. Üretim kodunda ancak hello kullanmanızı öneririz [list_node_agent_skus] [ py_list_skus] yöntemi toodetermine ve hello kullanılabilir görüntü ve düğüm Aracısı SKU birleşimlerini çalışma zamanında seçin.

```python
# Import hello required modules from the
# Azure Batch Client Library for Python
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify Batch account credentials
account = "<batch-account-name>"
key = "<batch-account-key>"
batch_url = "<batch-account-url>"

# Pool settings
pool_id = "LinuxNodesSamplePoolPython"
vm_size = "STANDARD_A1"
node_count = 1

# Initialize hello Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create hello unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure hello start task for hello pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies hello Marketplace
# virtual machine image tooinstall on hello nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create hello VirtualMachineConfiguration, specifying
# hello VM image reference and hello Batch node agent to
# be installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign hello virtual machine configuration toohello pool
new_pool.virtual_machine_configuration = vmc

# Create pool in hello Batch service
client.pool.add(new_pool)
```

Daha önce belirtildiği gibi hello oluşturmak yerine öneririz [Imagereference] [ py_imagereference] hello açıkça kullandığınız [list_node_agent_skus] [ py_list_skus] hello yöntemi toodynamically seçin, düğüm Aracısı/Market görüntü birleşimleri şu anda desteklenmiyor. Python kod parçacığında gösterildiği nasıl aşağıdaki hello toouse bu yöntem.

```python
# Get hello list of node agents from hello Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain hello desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick hello first image reference from hello list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create hello VirtualMachineConfiguration, specifying hello VM image
# reference and hello Batch node agent toobe installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a>Bir Linux havuzu oluşturun: Batch .NET
Merhaba aşağıdaki kod parçacığını bir örnek nasıl gösterir toouse hello [Batch .NET] [ nuget_batch_net] istemci kitaplığı toocreate Ubuntu Server havuzu işlem düğümlerini. Merhaba bulabilirsiniz [Batch .NET başvuru belgeleri] [ api_net] konusuna bakın.

Merhaba aşağıdaki kod parçacığını kullanan hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] şu anda desteklenen Market görüntü ve düğüm Aracısı SKU birleşimlerini hello listesinden yöntemi tooselect. Bu teknik arzu çünkü desteklenen birleşimlerin Hello listesi zaman tootime değişebilir. En yaygın olarak desteklenen birleşimlerin eklenir.

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us tooselect from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image
// that we wish toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello VirtualMachineConfiguration for use when actually
// creating hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create hello unbound pool object using hello VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit hello pool toohello Batch service
await pool.CommitAsync();
```

Merhaba önceki kod parçacığında hello kullansa [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] yöntemi toodynamically listesi ve arasından seçim desteklenmez (önerilen) görüntüsü ve düğüm Aracısı SKU birleşimleri, ayrıca yapılandırabilirsiniz bir [Imagereference] [ net_imagereference] açıkça:

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a>Sanal makine görüntülerini listesi
Merhaba aşağıdaki tabloda bu makalenin en son güncelleştirildiği hello kullanılabilir toplu düğümü aracıları ile uyumlu olan hello Market sanal makine görüntüleri listeler. Önemli toonote görüntüleri ve aracılarını veya herhangi bir anda kaldırılamaz bu listeyi kesin olmadığından emin olur. Toplu işlem uygulamaları ve Hizmetleri zaman kullanmanızı öneririz [list_node_agent_skus] [ py_list_skus] (Python) ve [ListNodeAgentSkus] [ net_list_skus] Şu anda kullanılabilir SKU'ları (batch .NET) toodetermine ve arasından seçim hello.

> [!WARNING]
> liste aşağıdaki hello herhangi bir zamanda değişebilir. Her zaman hello kullan **listesi düğüm Aracısı SKU** hello Batch API'lerini toolist kullanılabilir yöntemleri, uyumlu bir sanal makine ve düğüm Aracısı SKU'ları, Batch işleriniz çalıştırdığınızda hello.
>
>

| **Yayımcı** | **Teklif** | **Görüntü SKU** | **Sürüm** | **Düğüm Aracısı SKU kimliği** |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| Canonical | UbuntuServer | 14.04.5-LTS | en son | Batch.node.ubuntu 14.04 |
| Canonical | UbuntuServer | 16.04.0-LTS | en son | Batch.node.ubuntu 16.04 |
| Credativ | Debian | 8 | en son | Batch.node.debian 8 |
| OpenLogic | CentOS | 7.0 | en son | Batch.node.centos 7 |
| OpenLogic | CentOS | 7.1 | en son | Batch.node.centos 7 |
| OpenLogic | CentOS HPC | 7.1 | en son | Batch.node.centos 7 |
| OpenLogic | CentOS | 7.2 | en son | Batch.node.centos 7 |
| Oracle | Oracle Linux | 7.0 | en son | Batch.node.centos 7 |
| Oracle | Oracle Linux | 7.2 | en son | Batch.node.centos 7 |
| SUSE | openSUSE | 13.2 | en son | Batch.node.opensuse 13.2 |
| SUSE | openSUSE artık | 42.1 | en son | Batch.node.opensuse 42.1 |
| SUSE | SLES | 12 SP1 | en son | Batch.node.opensuse 42.1 |
| SUSE | SLES HPC | 12 SP1 | en son | Batch.node.opensuse 42.1 |
| Microsoft reklam | Linux veri bilimi vm | linuxdsvm | en son | Batch.node.centos 7 |
| Microsoft reklam | Standart veri bilimi vm | Standart veri bilimi vm | en son | Batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2008 R2 SP1 | en son | Batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-Datacenter | en son | Batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-R2-Datacenter | en son | Batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016 Datacenter | en son | Batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | Kapsayıcılar ile 2016 Datacenter | en son | Batch.node.Windows amd64 |

## <a name="connect-toolinux-nodes-using-ssh"></a>SSH kullanarak tooLinux düğümler Bağlan
Geliştirme sırasında veya sorun giderme sırasında bu gerekli toosign toohello düğümlerdeki havuzunuzdaki bulabilirsiniz. Windows işlem düğümleri, Uzak Masaüstü Protokolü (RDP) tooconnect tooLinux düğümleri kullanamazsınız. Bunun yerine, hello Batch hizmeti uzak bağlantı için her düğümde SSH erişimini etkinleştirir.

Merhaba aşağıdaki Python kod parçacığını bir kullanıcı uzak bağlantı için bir havuzdaki her düğümde oluşturur. Ardından, her düğüm için hello güvenli Kabuk (SSH) bağlantı bilgilerini yazdırır.

```python
import datetime
import getpass
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify your own account credentials
batch_account_name = ''
batch_account_key = ''
batch_account_url = ''

# Specify hello ID of an existing pool containing Linux nodes
# currently in hello 'idle' state
pool_id = ''

# Specify hello username and prompt for a password
username = 'linuxuser'
password = getpass.getpass()

# Create a BatchClient
credentials = batchauth.SharedKeyCredentials(
    batch_account_name,
    batch_account_key
)
batch_client = batch.BatchServiceClient(
        credentials,
        base_url=batch_account_url
)

# Create hello user that will be added tooeach node in hello pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get hello list of nodes in hello pool
nodes = batch_client.compute_node.list(pool_id)

# Add hello user tooeach node in hello pool and print
# hello connection information for hello node
for node in nodes:
    # Add hello user toohello node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for hello node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print hello connection info for hello node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

Merhaba önceki kodu dört Linux düğümleri içeren bir havuz için örnek çıktı aşağıda verilmiştir:

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

Bir düğümde bir kullanıcı oluşturduğunuzda, bir parola yerine bir SSH ortak anahtarı belirtebilirsiniz. Hello Python SDK'sı, hello kullan **ssh_public_key** parametresini [ComputeNodeUser][py_computenodeuser]. .NET içinde hello kullan [ComputeNodeUser][net_computenodeuser].[ SshPublicKey] [ net_ssh_key] özelliği.

## <a name="pricing"></a>Fiyatlandırma
Azure Batch Azure Cloud Services ve Azure sanal makineleri teknolojisi üzerine kurulmuştur. Merhaba Batch hizmeti kendisi yalnızca hello için ücretlendirilirsiniz anlamına gelir işlem Batch hesaplarınızın kaynaklarını hiçbir ücret ödemeden sunulur. Seçtiğinizde **Cloud Services Yapılandırması**, temel hello üzerinde ücretlendirilirsiniz [bulut Hizmetleri fiyatlandırma] [ cloud_services_pricing] yapısı. Seçtiğinizde **sanal makine yapılandırması**, temel hello üzerinde ücretlendirilirsiniz [sanal makineler fiyatlandırma] [ vm_pricing] yapısı. 

Uygulamaları tooyour toplu işlem düğümleri kullanarak dağıtırsanız [uygulama paketleri](batch-application-packages.md), uygulama paketlerinizi kullandığını hello Azure Storage kaynakları için ücretlendirilirsiniz. Genel olarak, hello Azure Storage maliyetleri en az. 

## <a name="next-steps"></a>Sonraki adımlar
### <a name="batch-python-tutorial"></a>Batch Python öğreticisi
Konusunda daha ayrıntılı bir öğretici için Python, kullanıma kullanarak Batch ile toowork [hello Azure Batch Python istemcisini kullanmaya başlama](batch-python-tutorial.md). Kendi yardımcı [kod örneği] [ github_samples_pyclient] yardımcı bir işlev içerir `get_vm_config_for_distro`, başka bir teknik tooobtain bir sanal makine yapılandırmasını gösterir.

### <a name="batch-python-code-samples"></a>Batch Python kod örnekleri
Merhaba [Python kod örnekleri] [ github_samples_py] hello içinde [azure-batch-samples] [ github_samples] github'daki nasıl Göster komut dosyaları içeren tooperform havuz, iş ve görev oluşturma gibi ortak toplu işlemleri. Merhaba [Benioku] [ github_py_readme] hello Python örnekleri eşlik nasıl tooinstall hello paketleri gerekli hakkında ayrıntılar bulunur.

### <a name="batch-forum"></a>Toplu İşlem forumu
Merhaba [Azure toplu işlem Forumu] [ forum] MSDN'de mükemmel toodiscuss toplu yerleştirin ve hello hizmeti hakkında soru sorun olduğunu. "Okuma yararlı sabitlenmiş" yazılarını ve Batch çözümlerinizi derleme sırasında çıktıkları anda sorularınızı gönderin.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_py_readme]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/README.md
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_py]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[github_samples_pyclient]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/python_tutorial_client.py
[portal]: https://portal.azure.com
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_computenodeuser]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.aspx
[net_imagereference]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.imagereference.aspx
[net_list_skus]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listnodeagentskus.aspx
[net_pool_ops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.aspx
[net_ssh_key]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.sshpublickey.aspx
[nuget_batch_net]: https://www.nuget.org/packages/Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
