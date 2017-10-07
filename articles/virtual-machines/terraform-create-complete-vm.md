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
ms.openlocfilehash: 916a838c118f28b3fbd373188e0acb2afc655081
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="7331a-103">Terraform kullanarak temel altyapı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7331a-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="7331a-104">Bu makalede, Azure'da tootake tooprovision temel altyapı ile birlikte bir sanal makine gereken hello adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7331a-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="7331a-105">Nasıl toowrite Terraform komut dosyaları ve toovisualize hello önce nasıl değiştiğini bulut altyapınızda olmalarını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7331a-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="7331a-106">Ayrıca öğreneceksiniz nasıl Terraform kullanarak toocreate altyapısında Azure.</span><span class="sxs-lookup"><span data-stu-id="7331a-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="7331a-107">başlatıldı, tooget \terraform_azure101.tf metin düzenleyicinizde tercih (Visual Studio kod/Sublime/VIM/vs.) adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7331a-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="7331a-108">Terraform hello klasör adı bir parametre olarak kabul ettiğinden hello dosyasının tam adı Hello önemli değil: hello klasöründeki tüm betikler yürütülen.</span><span class="sxs-lookup"><span data-stu-id="7331a-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="7331a-109">Merhaba yeni dosyasındaki kodu aşağıdaki hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="7331a-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group 
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="7331a-110">Merhaba, `provider` hello bölümünü komut dosyası, Terraform toouse hello komut dosyasında bir Azure sağlayıcısı tooprovision kaynakları söyleyin.</span><span class="sxs-lookup"><span data-stu-id="7331a-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="7331a-111">ABONELİK_KİMLİĞİ, AppID, parola ve tenant_id, tooget değerlerini görmek hello [yükleyin ve Terraform yapılandırma](terraform-install-configure.md) Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="7331a-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="7331a-112">Bu bloğa hello değerleri için ortam değişkenleri oluşturduysanız tooinclude gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7331a-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="7331a-113">Merhaba `azurerm_resource_group` kaynak Terraform toocreate yeni bir kaynak grubu bildirir.</span><span class="sxs-lookup"><span data-stu-id="7331a-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="7331a-114">Bu makalenin sonraki bölümlerinde Terraform içinde kullanılabilir daha fazla kaynak türlerini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7331a-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="7331a-115">Merhaba komut dosyası yürütme</span><span class="sxs-lookup"><span data-stu-id="7331a-115">Execute hello script</span></span>
<span data-ttu-id="7331a-116">Merhaba betik kaydettikten sonra toohello konsol/komut satırı çıkmak ve hello aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="7331a-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
<span data-ttu-id="7331a-117">Azure tooinitialize Terraform sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7331a-117">tooinitialize Terraform provider for Azure.</span></span> <span data-ttu-id="7331a-118">Merhaba aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="7331a-118">Then type hello following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="7331a-119">Varsayıyoruz `terraformscripts` hello betik kaydedildiği hello klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="7331a-119">We assume that `terraformscripts` is hello folder where hello script was saved.</span></span> <span data-ttu-id="7331a-120">Merhaba kullandık `plan` hello komut dosyalarında tanımlanan hello kaynaklara bakan Terraform komutu.</span><span class="sxs-lookup"><span data-stu-id="7331a-120">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="7331a-121">Bu Terraform tarafından kaydedilen toohello durum bilgilerini karşılaştırır ve ardından çıkışları planlı yürütme hello _olmadan_ gerçekten Azure kaynakları oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7331a-121">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="7331a-122">Merhaba önceki komutu yürüttükten sonra ekran aşağıdaki hello gibi bir şey görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="7331a-122">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Terraform planı](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="7331a-124">Her şeyin doğru görünüyorsa, bu yeni kaynak grubu azure'da hello aşağıdakini yürüterek sağlayın:</span><span class="sxs-lookup"><span data-stu-id="7331a-124">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="7331a-125">Hello Azure portal, hello adlı yeni boş bir kaynak grubu görmelisiniz `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="7331a-125">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="7331a-126">Bölümden hello içinde bir sanal makine ve tüm bu sanal makine toohello kaynak grubu için destekleyici altyapının hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7331a-126">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="7331a-127">Bir Ubuntu VM Terraform ile sağlama</span><span class="sxs-lookup"><span data-stu-id="7331a-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="7331a-128">Şimdi gerekli tooprovision olan hello ayrıntılarla oluşturduk hello Terraform betik Ubuntu çalışan bir sanal makine genişletir.</span><span class="sxs-lookup"><span data-stu-id="7331a-128">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="7331a-129">Aşağıdaki bölümlerde hello sağlamak hello kaynaklar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7331a-129">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="7331a-130">Tek bir alt ağla</span><span class="sxs-lookup"><span data-stu-id="7331a-130">A network with a single subnet</span></span>
* <span data-ttu-id="7331a-131">Bir ağ arabirimi kartı</span><span class="sxs-lookup"><span data-stu-id="7331a-131">A network interface card</span></span> 
* <span data-ttu-id="7331a-132">Bir depolama kapsayıcısı ile bir depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="7331a-132">A storage account with a storage container</span></span>
* <span data-ttu-id="7331a-133">Bir ortak IP</span><span class="sxs-lookup"><span data-stu-id="7331a-133">A public IP</span></span>
* <span data-ttu-id="7331a-134">Tüm hello önceki kaynakları kullanan bir sanal makine</span><span class="sxs-lookup"><span data-stu-id="7331a-134">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="7331a-135">Merhaba hello Azure Terraform kaynakların her biri için kapsamlı belgelere bakın [Terraform belgelerine](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="7331a-135">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="7331a-136">Merhaba tam sürümünü Hello [betik sağlama](#complete-terraform-script) ayrıca kolaylık sağlaması açısından sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="7331a-136">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="7331a-137">Merhaba Terraform betik genişletme</span><span class="sxs-lookup"><span data-stu-id="7331a-137">Extend hello Terraform script</span></span>
<span data-ttu-id="7331a-138">Kaynakları aşağıdaki hello ile oluşturulmuş hello betik genişletin:</span><span class="sxs-lookup"><span data-stu-id="7331a-138">Extend hello script that was created with hello following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="7331a-139">Merhaba önceki komut dosyası, sanal ağ ve bir alt ağ, sanal ağ içinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7331a-139">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="7331a-140">Önceden oluşturduğunuz aracılığıyla hello sanal ağ ve hello alt ağ tanımı "${azurerm_resource_group.helloterraform.name}" Merhaba başvuru toohello kaynak grubunu not alın.</span><span class="sxs-lookup"><span data-stu-id="7331a-140">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
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
}
~~~~
<span data-ttu-id="7331a-141">Merhaba önceki kod parçacıkları, bir ortak IP ve oluşturulan hello genel IP'sini kullanın sağlayan bir ağ arabirimi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7331a-141">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="7331a-142">Merhaba başvuruları toosubnet_id ve public_ip_address_id unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7331a-142">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="7331a-143">Terraform bu hello yerleşik zekaya toounderstand sahip ağ arabirimi hello ağ arabirimi hello oluşturması işleminden önce oluşturulan bu gereksinimi toobe hello kaynaklardaki bir bağımlılığa sahip.</span><span class="sxs-lookup"><span data-stu-id="7331a-143">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}
~~~~
<span data-ttu-id="7331a-144">Burada, bir depolama hesabı oluşturuldu ve bu depolama hesabı depolama kapsayıcıda tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="7331a-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="7331a-145">Bu depolama hesabı, oluşturulan toobe hakkında hello sanal makine için sanal sabit diskleri (VHD) depoladığınız gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="7331a-145">This storage account is where you store virtual hard disks (VHDs) for hello virtual machine about toobe created.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
~~~~
<span data-ttu-id="7331a-146">Son olarak, hello önceki kod parçacığında zaten sağlanan tüm hello kaynakları kullanan bir sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7331a-146">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="7331a-147">Bir depolama hesabı ve kapsayıcı için bir VHD, bir ağ arabirimi genel IP ve belirtilen alt ağ olan ve hello kaynak grubu, zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="7331a-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="7331a-148">Burada bir Azure A0 SKU hello betik belirtir hello vm_size özelliğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7331a-148">Note hello vm_size property, where hello script specifies an Azure A0 SKU.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="7331a-149">Merhaba komut dosyası yürütme</span><span class="sxs-lookup"><span data-stu-id="7331a-149">Execute hello script</span></span>
<span data-ttu-id="7331a-150">Kaydedilen hello tam komut dosyası ile toohello konsol/komut satırı çıkmak ve hello aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="7331a-150">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="7331a-151">Bir süre sonra bir sanal makine gibi hello kaynaklarına hello görünür `terraformtest` hello Azure portal kaynak grubunda.</span><span class="sxs-lookup"><span data-stu-id="7331a-151">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="7331a-152">Tam Terraform komut dosyası</span><span class="sxs-lookup"><span data-stu-id="7331a-152">Complete Terraform script</span></span>

<span data-ttu-id="7331a-153">Size kolaylık olması için aşağıdaki tüm hello altyapısının bu makalede ele alınan bu hükümleri hello tam Terraform komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="7331a-153">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

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

# create virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "tfvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "tfsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}


# create public IPs
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
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
}

# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="7331a-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7331a-154">Next steps</span></span>
<span data-ttu-id="7331a-155">Terraform kullanarak Azure'da temel altyapı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="7331a-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="7331a-156">Daha karmaşık senaryolar için kullanım yük dengeleyicileri ve sanal makine ölçekleme örnekler dahil olmak üzere kümeleri, bkz: çok sayıda [Terraform örnekler Azure için](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="7331a-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="7331a-157">Merhaba desteklenen Azure sağlayıcılar güncel bir listesi için bkz [Terraform belgelerine](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="7331a-157">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
