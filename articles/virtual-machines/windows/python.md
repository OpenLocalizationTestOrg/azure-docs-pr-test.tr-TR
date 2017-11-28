---
title: "aaaCreate ve Python kullanarak Azure Windows VM yönetme | Microsoft Docs"
description: "Toouse Python toocreate öğrenin ve bir Windows VM Azure ile yönetin."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: davidmu
ms.openlocfilehash: c5553e4e7361e6b9a7183cd935be382f967160cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="996de-103">Oluşturma ve Python kullanarak azure'da Windows sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="996de-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="996de-104">Bir [Azure sanal makine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) çeşitli destekleyici Azure kaynakları gerekir.</span><span class="sxs-lookup"><span data-stu-id="996de-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="996de-105">Bu makalede, oluşturma, yönetme ve Python kullanarak VM kaynakları silme yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="996de-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="996de-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="996de-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="996de-107">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="996de-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="996de-108">Paket yüklemek için</span><span class="sxs-lookup"><span data-stu-id="996de-108">Install packages</span></span>
> * <span data-ttu-id="996de-109">Kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="996de-109">Create credentials</span></span>
> * <span data-ttu-id="996de-110">Kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="996de-110">Create resources</span></span>
> * <span data-ttu-id="996de-111">Yönetim görevlerini gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="996de-111">Perform management tasks</span></span>
> * <span data-ttu-id="996de-112">Kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="996de-112">Delete resources</span></span>
> * <span data-ttu-id="996de-113">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="996de-113">Run hello application</span></span>

<span data-ttu-id="996de-114">Bu adımları toodo yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="996de-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="996de-115">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="996de-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="996de-116">Henüz yapmadıysanız, yükleme [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="996de-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="996de-117">Seçin **Python geliştirme** üzerinde iş yükleri sayfa hello ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="996de-117">Select **Python development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="996de-118">Hello Özet, görebilirsiniz **Python 3 64-bit (3.6.0)** sizin için otomatik olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="996de-118">In hello summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="996de-119">Visual Studio'nun zaten yüklediyseniz, hello Python iş yükü hello Visual Studio Başlatıcısı kullanarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="996de-119">If you have already installed Visual Studio, you can add hello Python workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="996de-120">Yükleme ve Visual Studio Başlangıç sonra tıklatın **dosya** > **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="996de-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="996de-121">Tıklatın **şablonları** > **Python** > **Python uygulama**, girin *myPythonProject* hello adı Merhaba projenin hello projesinin hello konumunu seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="996de-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="996de-122">Paket yüklemek için</span><span class="sxs-lookup"><span data-stu-id="996de-122">Install packages</span></span>

1. <span data-ttu-id="996de-123">Çözüm Gezgini'nde, altında *myPythonProject*, sağ **Python ortamları**ve ardından **Ekle sanal ortam**.</span><span class="sxs-lookup"><span data-stu-id="996de-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="996de-124">Merhaba sanal ortama ekleme ekranda hello varsayılan adını kabul edin *env*, olduğundan emin olun *Python 3.6 (64 bit)* hello temel yorumlayıcı için seçilir ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="996de-124">On hello Add Virtual Environment screen, accept hello default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for hello base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="996de-125">Sağ hello *env* , oluşturduğunuz ortama tıklayın **Python paketini Yükle**, girin *azure* hello arama kutusuna ve ardından Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="996de-125">Right-click hello *env* environment that you created, click **Install Python Package**, enter *azure* in hello search box, and then press Enter.</span></span>

<span data-ttu-id="996de-126">Merhaba çıkış windows hello azure paketleri başarıyla yüklenen görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="996de-126">You should see in hello output windows that hello azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="996de-127">Kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="996de-127">Create credentials</span></span>

<span data-ttu-id="996de-128">Bu adım başlamadan önce sahip olduğunuzdan emin olun bir [Active Directory hizmet asıl](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="996de-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="996de-129">Ayrıca bir sonraki adımda hello uygulama kimliği, hello kimlik doğrulama anahtarı ve ihtiyacınız hello Kiracı kimliği kaydetmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="996de-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="996de-130">Açık *myPythonProject.py* oluşturuldu, dosya ve ardından bu kodu tooenable uygulama toorun ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-130">Open *myPythonProject.py* file that was created, and then add this code tooenable your application toorun:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="996de-131">gereken tooimport hello kodu hello .py dosyanın bu deyimleri toohello üstüne ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-131">tooimport hello code that is needed, add these statements toohello top of hello .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="996de-132">Sonraki kod toospecify ortak değerleri kullanılan hello içeri aktarma deyimlerini hello sonra hello .py dosyasında değişkenleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-132">Next in hello .py file, add variables after hello import statements toospecify common values used in hello code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="996de-133">Değiştir **abonelik kimliği** , abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="996de-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="996de-134">toocreate hello Active Directory kimlik bilgileri toomake istekleri gereksinim hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-134">toocreate hello Active Directory credentials that you need toomake requests, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="996de-135">Değiştir **uygulama kimliği**, **kimlik doğrulama anahtarı**, ve **Kiracı kimliği** Azure Active Directory'yi oluşturduğunuzda, daha önce toplanan hello değerlerle Hizmet sorumlusu.</span><span class="sxs-lookup"><span data-stu-id="996de-135">Replace **application-id**, **authentication-key**, and **tenant-id** with hello values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="996de-136">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-136">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="996de-137">Kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="996de-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="996de-138">Yönetim istemcilerini başlatır</span><span class="sxs-lookup"><span data-stu-id="996de-138">Initialize management clients</span></span>

<span data-ttu-id="996de-139">Yönetim istemcileri gerekli toocreate olan ve Azure'da hello Python SDK'sını kullanarak kaynakları yönetin.</span><span class="sxs-lookup"><span data-stu-id="996de-139">Management clients are needed toocreate and manage resources using hello Python SDK in Azure.</span></span> <span data-ttu-id="996de-140">toocreate hello yönetim istemcileri, bu kod hello altında ekleyin **varsa** sonra hello .py dosya sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-140">toocreate hello management clients, add this code under hello **if** statement at then end of hello .py file:</span></span>

```python
resource_group_client = ResourceManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
network_client = NetworkManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
compute_client = ComputeManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
```

### <a name="create-hello-vm-and-supporting-resources"></a><span data-ttu-id="996de-141">Merhaba VM oluşturmak ve kaynakları destekleme</span><span class="sxs-lookup"><span data-stu-id="996de-141">Create hello VM and supporting resources</span></span>

<span data-ttu-id="996de-142">Tüm kaynaklar içinde bulunması gereken bir [kaynak grubu](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="996de-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="996de-143">bir kaynak grubu toocreate hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-143">toocreate a resource group, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="996de-144">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-144">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

<span data-ttu-id="996de-145">[Kullanılabilirlik kümeleri](tutorial-availability-sets.md) sizin için toomaintain hello sanal makineler, uygulamanız tarafından kullanılan kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="996de-145">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

1. <span data-ttu-id="996de-146">toocreate kullanılabilirlik ayarlayın, bu işlev hello .py dosyasındaki hello değişkenleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-146">toocreate an availability set, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def create_availability_set(compute_client):
        avset_params = {
            'location': LOCATION,
            'sku': { 'name': 'Aligned' },
            'platform_fault_domain_count': 3
        }
        availability_set_result = compute_client.availability_sets.create_or_update(
            GROUP_NAME,
            'myAVSet',
            avset_params
        )
    ```

2. <span data-ttu-id="996de-147">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-147">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

<span data-ttu-id="996de-148">A [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) hello sanal makineyle gerekli toocommunicate değil.</span><span class="sxs-lookup"><span data-stu-id="996de-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

1. <span data-ttu-id="996de-149">toocreate hello sanal makine için genel bir IP adresi hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-149">toocreate a public IP address for hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_public_ip_address(network_client):
        public_ip_addess_params = {
            'location': LOCATION,
            'public_ip_allocation_method': 'Dynamic'
        }
        creation_result = network_client.public_ip_addresses.create_or_update(
            GROUP_NAME,
            'myIPAddress',
            public_ip_addess_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="996de-150">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-150">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="996de-151">Bir sanal makine bir alt ağda olmalıdır bir [sanal ağ](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="996de-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="996de-152">toocreate bir sanal ağ hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-152">toocreate a virtual network, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_vnet(network_client):
        vnet_params = {
            'location': LOCATION,
            'address_space': {
                'address_prefixes': ['10.0.0.0/16']
            }
        }
        creation_result = network_client.virtual_networks.create_or_update(
            GROUP_NAME,
            'myVNet',
            vnet_params
        )
        return creation_result.result()
    ```

2. <span data-ttu-id="996de-153">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-153">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. <span data-ttu-id="996de-154">tooadd bir alt toohello sanal ağ hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-154">tooadd a subnet toohello virtual network, add this function after hello variables in hello .py file:</span></span>
    
    ```python
    def create_subnet(network_client):
        subnet_params = {
            'address_prefix': '10.0.0.0/24'
        }
        creation_result = network_client.subnets.create_or_update(
            GROUP_NAME,
            'myVNet',
            'mySubnet',
            subnet_params
        )

        return creation_result.result()
    ```
        
4. <span data-ttu-id="996de-155">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-155">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="996de-156">Bir sanal makine bir ağ arabirimi toocommunicate hello sanal ağda gerekir.</span><span class="sxs-lookup"><span data-stu-id="996de-156">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

1. <span data-ttu-id="996de-157">toocreate bir ağ arabirimi hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-157">toocreate a network interface, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_nic(network_client):
        subnet_info = network_client.subnets.get(
            GROUP_NAME, 
            'myVNet', 
            'mySubnet'
        )
        publicIPAddress = network_client.public_ip_addresses.get(
            GROUP_NAME,
            'myIPAddress'
        )
        nic_params = {
            'location': LOCATION,
            'ip_configurations': [{
                'name': 'myIPConfig',
                'public_ip_address': publicIPAddress,
                'subnet': {
                    'id': subnet_info.id
                }
            }]
        }
        creation_result = network_client.network_interfaces.create_or_update(
            GROUP_NAME,
            'myNic',
            nic_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="996de-158">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-158">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="996de-159">Kaynakları destekleyen tüm hello oluşturduğunuza göre bir sanal makine oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="996de-159">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="996de-160">toocreate Merhaba sanal makine, bu işlev hello .py dosyasındaki hello değişkenleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-160">toocreate hello virtual machine, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def create_vm(network_client, compute_client):  
        nic = network_client.network_interfaces.get(
            GROUP_NAME, 
            'myNic'
        )
        avset = compute_client.availability_sets.get(
            GROUP_NAME,
            'myAVSet'
        )
        vm_parameters = {
            'location': LOCATION,
            'os_profile': {
                'computer_name': VM_NAME,
                'admin_username': 'azureuser',
                'admin_password': 'Azure12345678'
            },
            'hardware_profile': {
                'vm_size': 'Standard_DS1'
            },
            'storage_profile': {
                'image_reference': {
                    'publisher': 'MicrosoftWindowsServer',
                    'offer': 'WindowsServer',
                    'sku': '2012-R2-Datacenter',
                    'version': 'latest'
                }
            },
            'network_profile': {
                'network_interfaces': [{
                    'id': nic.id
                }]
            },
            'availability_set': {
                'id': avset.id
            }
        }
        creation_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm_parameters
        )
    
        return creation_result.result()
    ```

    > [!NOTE]
    > <span data-ttu-id="996de-161">Bu öğretici hello Windows Server işletim sistemi sürümünü çalıştıran bir sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="996de-161">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="996de-162">diğer görüntüleri seçme hakkında daha fazla toolearn bkz [erişin ve seçin, Windows PowerShell ve Azure CLI hello Azure sanal makine görüntülerini](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="996de-162">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="996de-163">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-163">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="996de-164">Yönetim görevlerini gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="996de-164">Perform management tasks</span></span>

<span data-ttu-id="996de-165">Bir sanal makine Hello yaşam döngüsü sırasında başlatma, durdurma veya bir sanal makine silme gibi yönetim görevleri toorun isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="996de-165">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="996de-166">Ayrıca, toocreate, kod tooautomate yineleyen veya karmaşık görevleri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="996de-166">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="996de-167">Merhaba VM hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="996de-167">Get information about hello VM</span></span>

1. <span data-ttu-id="996de-168">Merhaba sanal makine hakkında tooget bilgi hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-168">tooget information about hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME, expand='instanceView')
        print("hardwareProfile")
        print("   vmSize: ", vm.hardware_profile.vm_size)
        print("\nstorageProfile")
        print("  imageReference")
        print("    publisher: ", vm.storage_profile.image_reference.publisher)
        print("    offer: ", vm.storage_profile.image_reference.offer)
        print("    sku: ", vm.storage_profile.image_reference.sku)
        print("    version: ", vm.storage_profile.image_reference.version)
        print("  osDisk")
        print("    osType: ", vm.storage_profile.os_disk.os_type.value)
        print("    name: ", vm.storage_profile.os_disk.name)
        print("    createOption: ", vm.storage_profile.os_disk.create_option.value)
        print("    caching: ", vm.storage_profile.os_disk.caching.value)
        print("\nosProfile")
        print("  computerName: ", vm.os_profile.computer_name)
        print("  adminUsername: ", vm.os_profile.admin_username)
        print("  provisionVMAgent: {0}".format(vm.os_profile.windows_configuration.provision_vm_agent))
        print("  enableAutomaticUpdates: {0}".format(vm.os_profile.windows_configuration.enable_automatic_updates))
        print("\nnetworkProfile")
        for nic in vm.network_profile.network_interfaces:
            print("  networkInterface id: ", nic.id)
        print("\nvmAgent")
        print("  vmAgentVersion", vm.instance_view.vm_agent.vm_agent_version)
        print("    statuses")
        for stat in vm_result.instance_view.vm_agent.statuses:
            print("    code: ", stat.code)
            print("    displayStatus: ", stat.display_status)
            print("    message: ", stat.message)
            print("    time: ", stat.time)
        print("\ndisks");
        for disk in vm.instance_view.disks:
            print("  name: ", disk.name)
            print("  statuses")
            for stat in disk.statuses:
                print("    code: ", stat.code)
                print("    displayStatus: ", stat.display_status)
                print("    time: ", stat.time)
        print("\nVM general status")
        print("  provisioningStatus: ", vm.provisioning_state)
        print("  id: ", vm.id)
        print("  name: ", vm.name)
        print("  type: ", vm.type)
        print("  location: ", vm.location)
        print("\nVM instance status")
        for stat in vm.instance_view.statuses:
            print("  code: ", stat.code)
            print("  displayStatus: ", stat.display_status)
    ```
2. <span data-ttu-id="996de-169">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-169">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a><span data-ttu-id="996de-170">Merhaba VM Durdur</span><span class="sxs-lookup"><span data-stu-id="996de-170">Stop hello VM</span></span>

<span data-ttu-id="996de-171">Bir sanal makineyi durdurmak ve tüm ayarları korumak, ancak toobe için sizden ücret veya bir sanal makineyi durdurun ve bunu serbest bırakma devam edin.</span><span class="sxs-lookup"><span data-stu-id="996de-171">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="996de-172">Bir sanal makine serbest bırakıldığında, kendisiyle ilişkili tüm kaynakları da deallocated ve fatura onun için edilir.</span><span class="sxs-lookup"><span data-stu-id="996de-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="996de-173">serbest bırakma olmadan toostop hello sanal makine hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-173">toostop hello virtual machine without deallocating it, add this function after hello variables in hello .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="996de-174">Toodeallocate hello sanal makine istiyorsanız hello power_off çağrısı toothis kodu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="996de-174">If you want toodeallocate hello virtual machine, change hello power_off call toothis code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="996de-175">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-175">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a><span data-ttu-id="996de-176">Merhaba VM Başlat</span><span class="sxs-lookup"><span data-stu-id="996de-176">Start hello VM</span></span>

1. <span data-ttu-id="996de-177">toostart Merhaba sanal makine, bu işlev hello .py dosyasındaki hello değişkenleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-177">toostart hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="996de-178">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-178">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a><span data-ttu-id="996de-179">Merhaba VM yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="996de-179">Resize hello VM</span></span>

<span data-ttu-id="996de-180">Dağıtım pek çok görünüşünün sanal makineniz için bir boyut karar verirken dikkate alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="996de-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="996de-181">Daha fazla bilgi için bkz: [VM boyutları](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="996de-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="996de-182">toochange hello hello sanal makine boyutunu hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-182">toochange hello size of hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def update_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        vm.hardware_profile.vm_size = 'Standard_DS3'
        update_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm
        )

    return update_result.result()
    ```

2. <span data-ttu-id="996de-183">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-183">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="996de-184">Bir veri diski toohello VM ekleme</span><span class="sxs-lookup"><span data-stu-id="996de-184">Add a data disk toohello VM</span></span>

<span data-ttu-id="996de-185">Sanal makineler, bir veya daha fazla olabilir [veri diskleri](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) VHD'ler olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="996de-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="996de-186">bir veri diski toohello sanal makine tooadd hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-186">tooadd a data disk toohello virtual machine, add this function after hello variables in hello .py file:</span></span> 

    ```python
    def add_datadisk(compute_client):
        disk_creation = compute_client.disks.create_or_update(
            GROUP_NAME,
            'myDataDisk1',
            {
                'location': LOCATION,
                'disk_size_gb': 1,
                'creation_data': {
                    'create_option': DiskCreateOption.empty
                }
            }
        )
        data_disk = disk_creation.result()
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        add_result = vm.storage_profile.data_disks.append({
            'lun': 1,
            'name': 'myDataDisk1',
            'create_option': DiskCreateOption.attach,
            'managed_disk': {
                'id': data_disk.id
            }
        })
        add_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME,
            VM_NAME,
            vm)

        return add_result.result()
    ```

2. <span data-ttu-id="996de-187">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-187">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="996de-188">Kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="996de-188">Delete resources</span></span>

<span data-ttu-id="996de-189">Azure'da kullanılan kaynaklar için ücretlendirildiğinizden, her zaman artık gerekli olmayan bir iyi bir uygulama toodelete kaynaklarını aşıyor.</span><span class="sxs-lookup"><span data-stu-id="996de-189">Because you are charged for resources used in Azure, it's always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="996de-190">Toodelete hello sanal makinelerin istediğiniz ve kaynakları destekleyen tüm hello tüm toodo varsa silme hello kaynak grubudur.</span><span class="sxs-lookup"><span data-stu-id="996de-190">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="996de-191">toodelete hello kaynak grubunu ve tüm kaynakları hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="996de-191">toodelete hello resource group and all resources, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="996de-192">daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:</span><span class="sxs-lookup"><span data-stu-id="996de-192">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="996de-193">Kaydet *myPythonProject.py*.</span><span class="sxs-lookup"><span data-stu-id="996de-193">Save *myPythonProject.py*.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="996de-194">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="996de-194">Run hello application</span></span>

1. <span data-ttu-id="996de-195">toorun hello konsol uygulaması tıklatın **Başlat** Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="996de-195">toorun hello console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="996de-196">Tuşuna **Enter** sonra her bir kaynağın hello durum döndürdü.</span><span class="sxs-lookup"><span data-stu-id="996de-196">Press **Enter** after hello status of each resource is returned.</span></span> <span data-ttu-id="996de-197">Merhaba durumunu görmelisiniz bir **başarılı** sağlama durumu.</span><span class="sxs-lookup"><span data-stu-id="996de-197">In hello status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="996de-198">Merhaba sanal makine oluşturulduktan sonra oluşturduğunuz tüm hello kaynaklar hello fırsat toodelete sahiptir.</span><span class="sxs-lookup"><span data-stu-id="996de-198">After hello virtual machine is created, you have hello opportunity toodelete all hello resources that you create.</span></span> <span data-ttu-id="996de-199">Tuşuna önce **Enter** toostart silme kaynakları, sürebilir birkaç dakika tooverify oluşumlarını hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="996de-199">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify their creation in hello Azure portal.</span></span> <span data-ttu-id="996de-200">Azure portal açık olan hello varsa toorefresh hello dikey toosee yeni kaynaklar olabilir.</span><span class="sxs-lookup"><span data-stu-id="996de-200">If you have hello Azure portal open, you might have toorefresh hello blade toosee new resources.</span></span>  

    <span data-ttu-id="996de-201">Bu konsol uygulaması toorun başlangıç toofinish itibaren tümüyle yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="996de-201">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> <span data-ttu-id="996de-202">Merhaba uygulaması önce tüm hello kaynakların sona erdi ve hello kaynak grubu silindi sonra birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="996de-202">It may take several minutes after hello application has finished before all hello resources and hello resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="996de-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="996de-203">Next steps</span></span>

- <span data-ttu-id="996de-204">Hello dağıtımı ile ilgili sorunlar varsa, bir sonraki adım, toolook olacaktır [Azure portalı ile kaynak grubu dağıtımı sorunlarını giderme](../../resource-manager-troubleshoot-deployments-portal.md)</span><span class="sxs-lookup"><span data-stu-id="996de-204">If there were issues with hello deployment, a next step would be toolook at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="996de-205">Merhaba hakkında daha fazla bilgi [Azure Python kitaplığı](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="996de-205">Learn more about hello [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

