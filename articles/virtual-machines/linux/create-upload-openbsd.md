---
title: "Oluşturun ve Azure'a OpenBSD VM görüntüyü karşıya | Microsoft Docs"
description: "Oluşturun ve sanal sabit bir Azure sanal makinesini Azure CLI aracılığıyla oluşturmak için OpenBSD işletim sistemi içeren bir disk (VHD) karşıya yükleme hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 716c07f6a738189d6cf2b3caafa16b753927d182
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-to-azure"></a><span data-ttu-id="20c6c-103">Oluşturun ve Azure'a bir OpenBSD disk görüntüsü yükleyin</span><span class="sxs-lookup"><span data-stu-id="20c6c-103">Create and Upload an OpenBSD disk image to Azure</span></span>
<span data-ttu-id="20c6c-104">Bu makalede nasıl oluşturulacağı ve bir sanal sabit OpenBSD işletim sistemini içeren disk (VHD) yüklemek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="20c6c-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the OpenBSD operating system.</span></span> <span data-ttu-id="20c6c-105">Karşıya yüklediğiniz sonra bunu kendi görüntünüzü Azure CLI aracılığıyla azure'da sanal makine (VM) oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20c6c-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="20c6c-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="20c6c-106">Prerequisites</span></span>
<span data-ttu-id="20c6c-107">Bu makalede, aşağıdaki öğelerin bulunduğunu varsayar:</span><span class="sxs-lookup"><span data-stu-id="20c6c-107">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="20c6c-108">**Bir Azure aboneliği** -bir hesabınız yoksa yalnızca birkaç dakika içinde bir oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20c6c-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="20c6c-109">Bir MSDN aboneliğiniz varsa, bkz: [Visual Studio aboneleri için aylık Azure kredi](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="20c6c-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="20c6c-110">Aksi takdirde, bilgi nasıl [ücretsiz bir deneme hesabı oluşturma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="20c6c-110">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="20c6c-111">**Azure CLI 2.0** -son olduğundan emin olun [Azure CLI 2.0](/cli/azure/install-azure-cli) yüklü ve Azure hesabınızla oturum açmış [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="20c6c-111">**Azure CLI 2.0** - Make sure you have the latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in to your Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="20c6c-112">**Bir .vhd dosyası yüklü OpenBSD işletim sistemi** -bir sanal sabit disk için desteklenen bir OpenBSD işletim sistemine (6.1 sürümü) yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="20c6c-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed to a virtual hard disk.</span></span> <span data-ttu-id="20c6c-113">Birden çok araç, .vhd dosyaları oluşturmak için mevcut.</span><span class="sxs-lookup"><span data-stu-id="20c6c-113">Multiple tools exist to create .vhd files.</span></span> <span data-ttu-id="20c6c-114">Örneğin, .vhd dosyası oluşturun ve işletim sistemini yüklemek için Hyper-V gibi bir sanallaştırma çözümü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20c6c-114">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span></span> <span data-ttu-id="20c6c-115">Yükleme ve Hyper-V kullanma hakkında yönergeler için bkz: [Hyper-V yükleyin ve sanal makine oluşturma](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="20c6c-115">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="20c6c-116">Azure için OpenBSD görüntüsünü hazırlama</span><span class="sxs-lookup"><span data-stu-id="20c6c-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="20c6c-117">OpenBSD işletim Hyper-V eklenen sistem 6.1, yüklediğiniz VM'de desteği, aşağıdaki yordamları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="20c6c-117">On the VM where you installed the OpenBSD operating system 6.1, which added Hyper-V support, complete the following procedures:</span></span>

1. <span data-ttu-id="20c6c-118">DHCP yükleme sırasında etkin değilse, hizmeti aşağıdaki gibi etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="20c6c-118">If DHCP is not enabled during installation, enable the service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="20c6c-119">Bir seri Konsolu aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="20c6c-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="20c6c-120">Paket yükleme işlemi aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="20c6c-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="20c6c-121">Varsayılan olarak, `root` kullanıcı azure'daki sanal makinelerde devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="20c6c-121">By default, the `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="20c6c-122">Kullanıcılar çalışma komutları yükseltilmiş ayrıcalıklarla kullanarak `doas` OpenBSD VM'de komutu.</span><span class="sxs-lookup"><span data-stu-id="20c6c-122">Users can run commands with elevated privileges by using the `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="20c6c-123">Doas varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="20c6c-123">Doas is enabled by default.</span></span> <span data-ttu-id="20c6c-124">Daha fazla bilgi için bkz: [doas.conf](http://man.openbsd.org/doas.conf.5).</span><span class="sxs-lookup"><span data-stu-id="20c6c-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="20c6c-125">Yükleyin ve Azure Aracısı önkoşulları aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="20c6c-125">Install and configure prerequisites for the Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="20c6c-126">En son sürümü Azure Aracısı'nın her zaman bulunabilir [Github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="20c6c-126">The latest release of the Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="20c6c-127">Aracıyı aşağıdaki gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="20c6c-127">Install the agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="20c6c-128">Azure aracısını yükledikten sonra şu şekilde çalıştığını doğrulamak için iyi bir fikirdir:</span><span class="sxs-lookup"><span data-stu-id="20c6c-128">After you install Azure Agent, it's a good idea to verify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="20c6c-129">Temizlemeyi ve sağlama işleminin için uygun hale sisteme sağlamayı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="20c6c-129">Deprovision the system to clean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="20c6c-130">Aşağıdaki komut, son sağlanan kullanıcı hesabını ve ilişkili veriler de siler:</span><span class="sxs-lookup"><span data-stu-id="20c6c-130">The following command also deletes the last provisioned user account and the associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="20c6c-131">Şimdi, VM kapatma.</span><span class="sxs-lookup"><span data-stu-id="20c6c-131">Now you can shut down your VM.</span></span>


## <a name="prepare-the-vhd"></a><span data-ttu-id="20c6c-132">VHD hazırlama</span><span class="sxs-lookup"><span data-stu-id="20c6c-132">Prepare the VHD</span></span>
<span data-ttu-id="20c6c-133">VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**.</span><span class="sxs-lookup"><span data-stu-id="20c6c-133">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="20c6c-134">Diski Hyper-V Yöneticisi'ni veya Powershell kullanarak sabit VHD biçimine dönüştürebilirsiniz [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="20c6c-134">You can convert the disk to fixed VHD format using Hyper-V Manager or the Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="20c6c-135">Örnek olarak verilebilir aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="20c6c-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="20c6c-136">Depolama kaynaklarını oluşturma ve yükleme</span><span class="sxs-lookup"><span data-stu-id="20c6c-136">Create storage resources and upload</span></span>
<span data-ttu-id="20c6c-137">İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="20c6c-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="20c6c-138">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroup* içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="20c6c-138">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="20c6c-139">VHD yüklemek için bir depolama hesabıyla oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="20c6c-139">To upload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="20c6c-140">Depolama hesabı adları benzersiz olması gerekir, böylece kendi adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="20c6c-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="20c6c-141">Aşağıdaki örnek adlı bir depolama hesabı oluşturur *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="20c6c-141">The following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="20c6c-142">Depolama hesabına erişimi denetlemek için depolama anahtarla elde [az depolama hesabı anahtarları listesi](/cli/azure/storage/account/keys#list) gibi:</span><span class="sxs-lookup"><span data-stu-id="20c6c-142">To control access to the storage account, obtain the storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="20c6c-143">Karşıya yüklediğiniz VHD'ler mantıksal olarak ayırmak için depolama hesabıyla içinde bir kapsayıcı oluşturmak [az depolama kapsayıcısı oluşturmak](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="20c6c-143">To logically separate the VHDs you upload, create a container within the storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="20c6c-144">Son olarak, VHD ile karşıya [az depolama blob karşıya yükleme](/cli/azure/storage/blob#upload) gibi:</span><span class="sxs-lookup"><span data-stu-id="20c6c-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="20c6c-145">VM, VHD'den oluştur</span><span class="sxs-lookup"><span data-stu-id="20c6c-145">Create VM from your VHD</span></span>
<span data-ttu-id="20c6c-146">Bir VM ile oluşturabileceğiniz bir [örnek komut dosyası](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) veya doğrudan [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="20c6c-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="20c6c-147">Karşıya yüklediğiniz OpenBSD VHD belirtmek için kullanın `--image` şekilde parametre:</span><span class="sxs-lookup"><span data-stu-id="20c6c-147">To specify the OpenBSD VHD you uploaded, use the `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="20c6c-148">OpenBSD VM ile için IP adresini elde [az vm listesi-ip-addresses](/cli/azure/vm#list-ip-addresses) gibi:</span><span class="sxs-lookup"><span data-stu-id="20c6c-148">Obtain the IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="20c6c-149">Şimdi, OpenBSD VM normal olarak SSH yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="20c6c-149">Now you can SSH to your OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="20c6c-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20c6c-150">Next steps</span></span>
<span data-ttu-id="20c6c-151">OpenBSD6.1 üzerinde Hyper-V desteği hakkında daha fazla bilgi edinmek istiyorsanız, okuma [OpenBSD 6.1](https://www.openbsd.org/61.html) ve [hyperv.4](http://man.openbsd.org/hyperv.4).</span><span class="sxs-lookup"><span data-stu-id="20c6c-151">If you want to know more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="20c6c-152">Yönetilen diskten bir VM oluşturmak istiyorsanız, okuma [az disk](/cli/azure/disk).</span><span class="sxs-lookup"><span data-stu-id="20c6c-152">If you want to create a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 