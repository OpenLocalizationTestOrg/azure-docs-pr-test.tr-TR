---
title: "aaaCreate ve karşıya yükleme OpenBSD VM görüntü tooAzure | Microsoft Docs"
description: "Toocreate ve karşıya yükleme sanal sabit içeren bir disk (VHD) OpenBSD işletim sistemi toocreate bir Azure sanal makinesini Azure CLI aracılığıyla nasıl hello öğrenin"
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
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a><span data-ttu-id="91c43-103">Oluşturun ve bir OpenBSD disk görüntü tooAzure yükleyin</span><span class="sxs-lookup"><span data-stu-id="91c43-103">Create and Upload an OpenBSD disk image tooAzure</span></span>
<span data-ttu-id="91c43-104">Bu makalede OpenBSD işletim sistemi toocreate ve karşıya yükleme sanal sabit içeren bir disk (VHD) nasıl hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="91c43-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello OpenBSD operating system.</span></span> <span data-ttu-id="91c43-105">Karşıya yüklediğiniz sonra kendi görüntü toocreate Azure CLI aracılığıyla azure'da sanal makine (VM) olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91c43-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="91c43-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="91c43-106">Prerequisites</span></span>
<span data-ttu-id="91c43-107">Bu makalede aşağıdaki öğelerindeki hello olduğunu varsayar:</span><span class="sxs-lookup"><span data-stu-id="91c43-107">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="91c43-108">**Bir Azure aboneliği** -bir hesabınız yoksa yalnızca birkaç dakika içinde bir oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91c43-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="91c43-109">Bir MSDN aboneliğiniz varsa, bkz: [Visual Studio aboneleri için aylık Azure kredi](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="91c43-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="91c43-110">Aksi takdirde nasıl çok öğrenin[ücretsiz bir deneme hesabı oluşturma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91c43-110">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="91c43-111">**Azure CLI 2.0** -son hello sahip olduğunuzdan emin olun [Azure CLI 2.0](/cli/azure/install-azure-cli) yüklü ve tooyour içinde Azure hesabı ile oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="91c43-111">**Azure CLI 2.0** - Make sure you have hello latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in tooyour Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="91c43-112">**Bir .vhd dosyası yüklü OpenBSD işletim sistemi** -desteklenen bir OpenBSD işletim sistemine (sürüm 6.1) yüklü tooa sanal sabit diski olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="91c43-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="91c43-113">Birden çok araç toocreate .vhd dosyaları mevcut.</span><span class="sxs-lookup"><span data-stu-id="91c43-113">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="91c43-114">Örneğin, Hyper-V toocreate hello .vhd dosyası gibi bir sanallaştırma çözümü kullanın ve hello işletim sistemi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="91c43-114">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="91c43-115">Tooinstall ve kullanım Hyper-V, nasıl görürüm hakkında yönergeler için [Hyper-V yükleyin ve sanal makine oluşturma](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="91c43-115">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="91c43-116">Azure için OpenBSD görüntüsünü hazırlama</span><span class="sxs-lookup"><span data-stu-id="91c43-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="91c43-117">Merhaba hello OpenBSD işletim sistemi 6.1, Hyper-V desteği eklendi, yüklediğiniz VM üzerinde hello yordamları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="91c43-117">On hello VM where you installed hello OpenBSD operating system 6.1, which added Hyper-V support, complete hello following procedures:</span></span>

1. <span data-ttu-id="91c43-118">DHCP yükleme sırasında etkin değilse hello hizmeti aşağıdaki gibi etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="91c43-118">If DHCP is not enabled during installation, enable hello service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="91c43-119">Bir seri Konsolu aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="91c43-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="91c43-120">Paket yükleme işlemi aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="91c43-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="91c43-121">Varsayılan olarak, hello `root` kullanıcı azure'daki sanal makinelerde devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="91c43-121">By default, hello `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="91c43-122">Kullanıcılar çalışma komutları yükseltilmiş ayrıcalıklarla hello kullanarak `doas` OpenBSD VM'de komutu.</span><span class="sxs-lookup"><span data-stu-id="91c43-122">Users can run commands with elevated privileges by using hello `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="91c43-123">Doas varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="91c43-123">Doas is enabled by default.</span></span> <span data-ttu-id="91c43-124">Daha fazla bilgi için bkz: [doas.conf](http://man.openbsd.org/doas.conf.5).</span><span class="sxs-lookup"><span data-stu-id="91c43-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="91c43-125">Yükleyin ve hello Azure Aracısı önkoşulları aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="91c43-125">Install and configure prerequisites for hello Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="91c43-126">Merhaba hello Azure Aracısı en son sürümü her zaman bulunabilir üzerinde [Github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="91c43-126">hello latest release of hello Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="91c43-127">Merhaba aracıyı aşağıdaki gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="91c43-127">Install hello agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="91c43-128">Azure aracısını yükledikten sonra şu şekilde çalışan bir fikir tooverify şöyledir:</span><span class="sxs-lookup"><span data-stu-id="91c43-128">After you install Azure Agent, it's a good idea tooverify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="91c43-129">Deprovision hello sistem tooclean ve yapma, sağlama işleminin için uygun.</span><span class="sxs-lookup"><span data-stu-id="91c43-129">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="91c43-130">Hello aşağıdaki komut da hello son sağlanan kullanıcı hesabını ve ilişkili hello verileri siler:</span><span class="sxs-lookup"><span data-stu-id="91c43-130">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="91c43-131">Şimdi, VM kapatma.</span><span class="sxs-lookup"><span data-stu-id="91c43-131">Now you can shut down your VM.</span></span>


## <a name="prepare-hello-vhd"></a><span data-ttu-id="91c43-132">Merhaba VHD hazırlama</span><span class="sxs-lookup"><span data-stu-id="91c43-132">Prepare hello VHD</span></span>
<span data-ttu-id="91c43-133">Merhaba VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**.</span><span class="sxs-lookup"><span data-stu-id="91c43-133">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="91c43-134">Hyper-V Yöneticisi'ni kullanarak hello disk toofixed VHD biçimine Dönüştür veya Powershell hello [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="91c43-134">You can convert hello disk toofixed VHD format using Hyper-V Manager or hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="91c43-135">Örnek olarak verilebilir aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="91c43-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="91c43-136">Depolama kaynaklarını oluşturma ve yükleme</span><span class="sxs-lookup"><span data-stu-id="91c43-136">Create storage resources and upload</span></span>
<span data-ttu-id="91c43-137">İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="91c43-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="91c43-138">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="91c43-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="91c43-139">tooupload, VHD ile depolama hesabı oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="91c43-139">tooupload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="91c43-140">Depolama hesabı adları benzersiz olması gerekir, böylece kendi adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="91c43-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="91c43-141">Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="91c43-141">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="91c43-142">toocontrol erişim toohello depolama hesabı, hello depolama anahtarla elde [az depolama hesabı anahtarları listesi](/cli/azure/storage/account/keys#list) gibi:</span><span class="sxs-lookup"><span data-stu-id="91c43-142">toocontrol access toohello storage account, obtain hello storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="91c43-143">toologically ayrı hello karşıya yüklediğiniz, VHD oluşturma hello depolama hesabıyla kapsayıcıda [az depolama kapsayıcısı oluşturmak](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="91c43-143">toologically separate hello VHDs you upload, create a container within hello storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="91c43-144">Son olarak, VHD ile karşıya [az depolama blob karşıya yükleme](/cli/azure/storage/blob#upload) gibi:</span><span class="sxs-lookup"><span data-stu-id="91c43-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="91c43-145">VM, VHD'den oluştur</span><span class="sxs-lookup"><span data-stu-id="91c43-145">Create VM from your VHD</span></span>
<span data-ttu-id="91c43-146">Bir VM ile oluşturabileceğiniz bir [örnek komut dosyası](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) veya doğrudan [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="91c43-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="91c43-147">toospecify hello OpenBSD karşıya yüklediğiniz, VHD kullanım hello `--image` şekilde parametre:</span><span class="sxs-lookup"><span data-stu-id="91c43-147">toospecify hello OpenBSD VHD you uploaded, use hello `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="91c43-148">OpenBSD VM ile için başlangıç IP adresi al [az vm listesi-ip-addresses](/cli/azure/vm#list-ip-addresses) gibi:</span><span class="sxs-lookup"><span data-stu-id="91c43-148">Obtain hello IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="91c43-149">Artık normal olarak SSH tooyour OpenBSD VM yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="91c43-149">Now you can SSH tooyour OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="91c43-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91c43-150">Next steps</span></span>
<span data-ttu-id="91c43-151">Hyper-V hakkında daha fazla destek OpenBSD6.1 üzerinde tooknow istiyorsanız, okuma [OpenBSD 6.1](https://www.openbsd.org/61.html) ve [hyperv.4](http://man.openbsd.org/hyperv.4).</span><span class="sxs-lookup"><span data-stu-id="91c43-151">If you want tooknow more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="91c43-152">Toocreate yönetilen diskten VM istiyorsanız, okuma [az disk](/cli/azure/disk).</span><span class="sxs-lookup"><span data-stu-id="91c43-152">If you want toocreate a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 
