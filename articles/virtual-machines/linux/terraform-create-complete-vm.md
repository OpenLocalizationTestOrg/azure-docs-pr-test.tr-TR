---
title: "Terraform kullanarak aaaCreate temel altyapı azure'da | Microsoft Docs"
description: "Bilgi nasıl toocreate Azure Terraform kullanarak kaynakları"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 52591009ee7cb906402b8bca2ce63794ac7afcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>Terraform kullanarak temel altyapı oluşturma
Bu makalede, Azure'da tootake tooprovision temel altyapı ile birlikte bir sanal makine gereken hello adımları açıklanmaktadır. Nasıl toowrite Terraform komut dosyaları ve toovisualize hello önce nasıl değiştiğini bulut altyapınızda olmalarını öğreneceksiniz. Ayrıca öğreneceksiniz nasıl Terraform kullanarak toocreate altyapısında Azure.

başlatıldı, tooget \terraform_azure101.tf metin düzenleyicinizde tercih (Visual Studio kod/Sublime/VIM/vs.) adlı bir dosya oluşturun. Terraform hello klasör adı bir parametre olarak kabul ettiğinden hello dosyasının tam adı Hello önemli değil: hello klasöründeki tüm betikler yürütülen. Merhaba yeni dosyasındaki kodu aşağıdaki hello yapıştırın:

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
Merhaba, `provider` hello bölümünü komut dosyası, Terraform toouse hello komut dosyasında bir Azure sağlayıcısı tooprovision kaynakları söyleyin. ABONELİK_KİMLİĞİ, AppID, parola ve tenant_id, tooget değerlerini görmek hello [yükleyin ve Terraform yapılandırma](terraform-install-configure.md) Kılavuzu. Bu bloğa hello değerleri için ortam değişkenleri oluşturduysanız tooinclude gerekmez. 

Merhaba `azurerm_resource_group` kaynak Terraform toocreate yeni bir kaynak grubu bildirir. Bu makalenin sonraki bölümlerinde Terraform içinde kullanılabilir daha fazla kaynak türlerini görebilirsiniz.

## <a name="execute-hello-script"></a>Merhaba komut dosyası yürütme
Merhaba betik kaydettikten sonra toohello konsol/komut satırı çıkmak ve hello aşağıdakileri yazın:
```
terraform init
```
 Azure için tooinitialize hello Terraform sağlayıcı. Merhaba dizini çok değiştirmek**terraformscripts**, sorunu hello izleyerek komutu:
```
terraform plan
```
Merhaba kullandık `plan` hello komut dosyalarında tanımlanan hello kaynaklara bakan Terraform komutu. Bu Terraform tarafından kaydedilen toohello durum bilgilerini karşılaştırır ve ardından çıkışları planlı yürütme hello _olmadan_ gerçekten Azure kaynakları oluşturma. 

Merhaba önceki komutu yürüttükten sonra ekran aşağıdaki hello gibi bir şey görmeniz gerekir:

![Terraform planı](./media/terraform/tf_plan2.png)

Her şeyin doğru görünüyorsa, bu yeni kaynak grubu azure'da hello aşağıdakini yürüterek sağlayın: 
```
terraform apply
```
Hello Azure portal, hello adlı yeni boş bir kaynak grubu görmelisiniz `terraformtest`. Bölümden hello içinde bir sanal makine ve tüm bu sanal makine toohello kaynak grubu için destekleyici altyapının hello ekleyin.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Bir Ubuntu VM Terraform ile sağlama
Şimdi gerekli tooprovision olan hello ayrıntılarla oluşturduk hello Terraform betik Ubuntu çalışan bir sanal makine genişletir. Aşağıdaki bölümlerde hello sağlamak hello kaynaklar şunlardır:

* Tek bir alt ağla
* Bir ağ arabirimi kartı 
* Merhaba sanal makine tanılama için bir depolama hesabı
* Bir ortak IP
* Tüm hello önceki kaynakları kullanan bir sanal makine 

Merhaba hello Azure Terraform kaynakların her biri için kapsamlı belgelere bakın [Terraform belgelerine](https://www.terraform.io/docs/providers/azurerm/index.html).

Merhaba tam sürümünü Hello [betik sağlama](#complete-terraform-script) ayrıca kolaylık sağlaması açısından sunulmuştur.

### <a name="extend-hello-terraform-script"></a>Merhaba Terraform betik genişletme
Kaynakları aşağıdaki hello ile oluşturulmuş hello betik genişletin: 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
Merhaba önceki komut dosyası, sanal ağ ve bir alt ağ, sanal ağ içinde oluşturur. Önceden oluşturduğunuz aracılığıyla hello sanal ağ ve hello alt ağ tanımı "${azurerm_resource_group.helloterraform.name}" Merhaba başvuru toohello kaynak grubunu not alın.

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
Merhaba önceki kod parçacıkları, bir ortak IP ve oluşturulan hello genel IP'sini kullanın sağlayan bir ağ arabirimi oluşturun. Merhaba başvuruları toosubnet_id ve public_ip_address_id unutmayın. Terraform bu hello yerleşik zekaya toounderstand sahip ağ arabirimi hello ağ arabirimi hello oluşturması işleminden önce oluşturulan bu gereksinimi toobe hello kaynaklardaki bir bağımlılığa sahip.

~~~~
# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
Burada, bir depolama hesabı oluşturuldu. Merhaba sanal makine tanılama ayrıntılarını depolayacağınız bu depolama hesabıdır.

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
Son olarak, hello önceki kod parçacığında zaten sağlanan tüm hello kaynakları kullanan bir sanal makine oluşturur. Merhaba sanal makine tanılamaları, bir ağ arabirimi genel IP ve belirtilen alt ağ için bir depolama hesabı olan ve hello kaynak grubu, zaten oluşturulmuş. Burada bir Azure standart DS1v2 SKU hello betik belirtir hello vm_size özelliğine dikkat edin.

Gerekli toosupply bir SSH ortak anahtarı var. Merhaba ortak anahtar değeri hello bölüme yerleştirin **... BURADA ORTAK ANAHTARI OPENSSH EKLE...**  üstünde. Ssh varolan kullanabileceğiniz anahtar çifti ya da hello izleyerek [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) veya [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) belgelerine toogenerate hello anahtar çifti.

### <a name="execute-hello-script"></a>Merhaba komut dosyası yürütme
Kaydedilen hello tam komut dosyası ile toohello konsol/komut satırı çıkmak ve hello aşağıdakileri yazın:
```
terraform apply
```
Bir süre sonra bir sanal makine gibi hello kaynaklarına hello görünür `terraformtest` hello Azure portal kaynak grubunda.

## <a name="complete-terraform-script"></a>Tam Terraform komut dosyası

Size kolaylık olması için aşağıdaki tüm hello altyapısının bu makalede ele alınan bu hükümleri hello tam Terraform komut dosyasıdır.

```
# Configure hello Microsoft Azure Provider
provider "azurerm" {
  subscription_id = "XXX"
  client_id       = "XXX"
  client_secret   = "XXX"
  tenant_id       = "XXX"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}

# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}

# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }

    tags {
        environment = "Terraform Demo"
    }
}

# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
```

## <a name="next-steps"></a>Sonraki adımlar
Terraform kullanarak Azure'da temel altyapı oluşturdunuz. Daha karmaşık senaryolar için kullanım yük dengeleyicileri ve sanal makine ölçekleme örnekler dahil olmak üzere kümeleri, bkz: çok sayıda [Terraform örnekler Azure için](https://github.com/hashicorp/terraform/tree/master/examples). Merhaba desteklenen Azure sağlayıcılar güncel bir listesi için bkz [Terraform belgelerine](https://www.terraform.io/docs/providers/azurerm/index.html).
