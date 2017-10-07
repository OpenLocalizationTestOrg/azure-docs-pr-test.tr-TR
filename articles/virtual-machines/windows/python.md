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
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a>Oluşturma ve Python kullanarak azure'da Windows sanal makineleri yönetme

Bir [Azure sanal makine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) çeşitli destekleyici Azure kaynakları gerekir. Bu makalede, oluşturma, yönetme ve Python kullanarak VM kaynakları silme yer almaktadır. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Visual Studio projesi oluşturma
> * Paket yüklemek için
> * Kimlik bilgileri oluşturun
> * Kaynak oluşturma
> * Yönetim görevlerini gerçekleştirme
> * Kaynakları silin
> * Merhaba uygulamayı çalıştırın

Bu adımları toodo yaklaşık 20 dakika sürer.

## <a name="create-a-visual-studio-project"></a>Visual Studio projesi oluşturma

1. Henüz yapmadıysanız, yükleme [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Seçin **Python geliştirme** üzerinde iş yükleri sayfa hello ve ardından **yükleme**. Hello Özet, görebilirsiniz **Python 3 64-bit (3.6.0)** sizin için otomatik olarak seçilir. Visual Studio'nun zaten yüklediyseniz, hello Python iş yükü hello Visual Studio Başlatıcısı kullanarak ekleyebilirsiniz.
2. Yükleme ve Visual Studio Başlangıç sonra tıklatın **dosya** > **yeni** > **proje**.
3. Tıklatın **şablonları** > **Python** > **Python uygulama**, girin *myPythonProject* hello adı Merhaba projenin hello projesinin hello konumunu seçin ve ardından **Tamam**.

## <a name="install-packages"></a>Paket yüklemek için

1. Çözüm Gezgini'nde, altında *myPythonProject*, sağ **Python ortamları**ve ardından **Ekle sanal ortam**.
2. Merhaba sanal ortama ekleme ekranda hello varsayılan adını kabul edin *env*, olduğundan emin olun *Python 3.6 (64 bit)* hello temel yorumlayıcı için seçilir ve ardından **oluşturma**.
3. Sağ hello *env* , oluşturduğunuz ortama tıklayın **Python paketini Yükle**, girin *azure* hello arama kutusuna ve ardından Enter tuşuna basın.

Merhaba çıkış windows hello azure paketleri başarıyla yüklenen görmeniz gerekir. 

## <a name="create-credentials"></a>Kimlik bilgileri oluşturun

Bu adım başlamadan önce sahip olduğunuzdan emin olun bir [Active Directory hizmet asıl](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Ayrıca bir sonraki adımda hello uygulama kimliği, hello kimlik doğrulama anahtarı ve ihtiyacınız hello Kiracı kimliği kaydetmelisiniz.

1. Açık *myPythonProject.py* oluşturuldu, dosya ve ardından bu kodu tooenable uygulama toorun ekleyin:

    ```python
    if __name__ == "__main__":
    ```

2. gereken tooimport hello kodu hello .py dosyanın bu deyimleri toohello üstüne ekleyin:

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. Sonraki kod toospecify ortak değerleri kullanılan hello içeri aktarma deyimlerini hello sonra hello .py dosyasında değişkenleri ekleyin:
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    Değiştir **abonelik kimliği** , abonelik tanımlayıcısı.

4. toocreate hello Active Directory kimlik bilgileri toomake istekleri gereksinim hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    Değiştir **uygulama kimliği**, **kimlik doğrulama anahtarı**, ve **Kiracı kimliği** Azure Active Directory'yi oluşturduğunuzda, daha önce toplanan hello değerlerle Hizmet sorumlusu.

5. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a>Kaynak oluşturma
 
### <a name="initialize-management-clients"></a>Yönetim istemcilerini başlatır

Yönetim istemcileri gerekli toocreate olan ve Azure'da hello Python SDK'sını kullanarak kaynakları yönetin. toocreate hello yönetim istemcileri, bu kod hello altında ekleyin **varsa** sonra hello .py dosya sonunda deyimi:

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

### <a name="create-hello-vm-and-supporting-resources"></a>Merhaba VM oluşturmak ve kaynakları destekleme

Tüm kaynaklar içinde bulunması gereken bir [kaynak grubu](../../azure-resource-manager/resource-group-overview.md).

1. bir kaynak grubu toocreate hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

[Kullanılabilirlik kümeleri](tutorial-availability-sets.md) sizin için toomaintain hello sanal makineler, uygulamanız tarafından kullanılan kolaylaştırır.

1. toocreate kullanılabilirlik ayarlayın, bu işlev hello .py dosyasındaki hello değişkenleri ekleyin:
   
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

2. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

A [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) hello sanal makineyle gerekli toocommunicate değil.

1. toocreate hello sanal makine için genel bir IP adresi hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:

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

2. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Bir sanal makine bir alt ağda olmalıdır bir [sanal ağ](../../virtual-network/virtual-networks-overview.md).

1. toocreate bir sanal ağ hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:

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

2. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. tooadd bir alt toohello sanal ağ hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:
    
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
        
4. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Bir sanal makine bir ağ arabirimi toocommunicate hello sanal ağda gerekir.

1. toocreate bir ağ arabirimi hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:

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

2. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Kaynakları destekleyen tüm hello oluşturduğunuza göre bir sanal makine oluşturabilirsiniz.

1. toocreate Merhaba sanal makine, bu işlev hello .py dosyasındaki hello değişkenleri ekleyin:
   
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
    > Bu öğretici hello Windows Server işletim sistemi sürümünü çalıştıran bir sanal makine oluşturur. diğer görüntüleri seçme hakkında daha fazla toolearn bkz [erişin ve seçin, Windows PowerShell ve Azure CLI hello Azure sanal makine görüntülerini](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

2. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a>Yönetim görevlerini gerçekleştirme

Bir sanal makine Hello yaşam döngüsü sırasında başlatma, durdurma veya bir sanal makine silme gibi yönetim görevleri toorun isteyebilirsiniz. Ayrıca, toocreate, kod tooautomate yineleyen veya karmaşık görevleri isteyebilirsiniz.

### <a name="get-information-about-hello-vm"></a>Merhaba VM hakkında bilgi edinin

1. Merhaba sanal makine hakkında tooget bilgi hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:

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
2. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a>Merhaba VM Durdur

Bir sanal makineyi durdurmak ve tüm ayarları korumak, ancak toobe için sizden ücret veya bir sanal makineyi durdurun ve bunu serbest bırakma devam edin. Bir sanal makine serbest bırakıldığında, kendisiyle ilişkili tüm kaynakları da deallocated ve fatura onun için edilir.

1. serbest bırakma olmadan toostop hello sanal makine hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    Toodeallocate hello sanal makine istiyorsanız hello power_off çağrısı toothis kodu değiştirin:

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a>Merhaba VM Başlat

1. toostart Merhaba sanal makine, bu işlev hello .py dosyasındaki hello değişkenleri ekleyin:

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a>Merhaba VM yeniden boyutlandırma

Dağıtım pek çok görünüşünün sanal makineniz için bir boyut karar verirken dikkate alınmalıdır. Daha fazla bilgi için bkz: [VM boyutları](sizes.md).

1. toochange hello hello sanal makine boyutunu hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:

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

2. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a>Bir veri diski toohello VM ekleme

Sanal makineler, bir veya daha fazla olabilir [veri diskleri](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) VHD'ler olarak depolanır.

1. bir veri diski toohello sanal makine tooadd hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin: 

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

2. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a>Kaynakları silin

Azure'da kullanılan kaynaklar için ücretlendirildiğinizden, her zaman artık gerekli olmayan bir iyi bir uygulama toodelete kaynaklarını aşıyor. Toodelete hello sanal makinelerin istediğiniz ve kaynakları destekleyen tüm hello tüm toodo varsa silme hello kaynak grubudur.

1. toodelete hello kaynak grubunu ve tüm kaynakları hello .py dosyasındaki hello değişkenleri sonra bu işlevi ekleyin:
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. daha önce eklediğiniz, toocall hello işlevi hello altında bu kodu ekleyin **varsa** hello .py dosya hello sonunda deyimi:
   
    ```python
    delete_resources(resource_group_client)
    ```

3. Kaydet *myPythonProject.py*.

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın

1. toorun hello konsol uygulaması tıklatın **Başlat** Visual Studio.

2. Tuşuna **Enter** sonra her bir kaynağın hello durum döndürdü. Merhaba durumunu görmelisiniz bir **başarılı** sağlama durumu. Merhaba sanal makine oluşturulduktan sonra oluşturduğunuz tüm hello kaynaklar hello fırsat toodelete sahiptir. Tuşuna önce **Enter** toostart silme kaynakları, sürebilir birkaç dakika tooverify oluşumlarını hello Azure portalı. Azure portal açık olan hello varsa toorefresh hello dikey toosee yeni kaynaklar olabilir.  

    Bu konsol uygulaması toorun başlangıç toofinish itibaren tümüyle yaklaşık beş dakika sürer. Merhaba uygulaması önce tüm hello kaynakların sona erdi ve hello kaynak grubu silindi sonra birkaç dakika sürebilir.


## <a name="next-steps"></a>Sonraki adımlar

- Hello dağıtımı ile ilgili sorunlar varsa, bir sonraki adım, toolook olacaktır [Azure portalı ile kaynak grubu dağıtımı sorunlarını giderme](../../resource-manager-troubleshoot-deployments-portal.md)
- Merhaba hakkında daha fazla bilgi [Azure Python kitaplığı](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)

