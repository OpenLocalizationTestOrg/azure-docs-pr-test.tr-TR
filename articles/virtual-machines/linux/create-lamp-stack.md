---
title: azure'da bir Linux sanal makinede AMPUL aaaDeploy | Microsoft Docs
description: "Nasıl tooinstall hello AMPUL yığın azure'da bir Linux VM hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="c6f49-103">Azure AMPUL yığında dağıtma</span><span class="sxs-lookup"><span data-stu-id="c6f49-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="c6f49-104">Bu makalede toodeploy Apache nasıl web sunucusu, MySQL ve Azure üzerinde PHP (Merhaba AMPUL yığını) aracılığıyla anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c6f49-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="c6f49-105">Bir Azure hesabınızın olması gerekir ([ücretsiz bir deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/)) ve hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="c6f49-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="c6f49-106">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6f49-106">You can also perform these steps with hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="c6f49-107">Hızlı komut Özet</span><span class="sxs-lookup"><span data-stu-id="c6f49-107">Quick command summary</span></span>

1. <span data-ttu-id="c6f49-108">Kaydetme ve hello düzenleme [azuredeploy.parameters.json dosya](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour tercih yerel makinenizde.</span><span class="sxs-lookup"><span data-stu-id="c6f49-108">Save and edit hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour preference on your local machine.</span></span>
2. <span data-ttu-id="c6f49-109">Bir kaynak grubu iki komutları toocreate aşağıdaki hello çalıştırın ve şablonunuzu dağıtma:</span><span class="sxs-lookup"><span data-stu-id="c6f49-109">Run hello following two commands toocreate a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="c6f49-110">Var olan VM üzerinde AMPUL dağıtma</span><span class="sxs-lookup"><span data-stu-id="c6f49-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="c6f49-111">Merhaba aşağıdaki güncelleştirmeleri paketleri komutları sonra Apache, MySQL ve PHP yükler:</span><span class="sxs-lookup"><span data-stu-id="c6f49-111">hello following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="c6f49-112">Yeni VM gözden geçirme üzerinde AMPUL dağıtma</span><span class="sxs-lookup"><span data-stu-id="c6f49-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="c6f49-113">Sahip bir kaynak grubu oluşturma [az grubu oluşturma](/cli/azure/group#create) toocontain yeni VM hello:</span><span class="sxs-lookup"><span data-stu-id="c6f49-113">Create a resource group with [az group create](/cli/azure/group#create) toocontain hello new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="c6f49-114">toocreate VM kendisini Merhaba, bulunan zaten yazılmış bir Azure Resource Manager şablonunu kullanabilirsiniz [github'da burada](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="c6f49-114">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="c6f49-115">Merhaba Kaydet [azuredeploy.parameters.json dosya](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour yerel makine.</span><span class="sxs-lookup"><span data-stu-id="c6f49-115">Save hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour local machine.</span></span>
3. <span data-ttu-id="c6f49-116">Merhaba Düzenle **azuredeploy.parameters.json** dosya tooyour girişleri tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="c6f49-116">Edit hello **azuredeploy.parameters.json** file tooyour preferred inputs.</span></span>
4. <span data-ttu-id="c6f49-117">Merhaba şablonla dağıtma [az grup dağıtımı Oluştur] hello başvuran indirilen json dosyası:</span><span class="sxs-lookup"><span data-stu-id="c6f49-117">Deploy hello template with [az group deployment create] referencing hello downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="c6f49-118">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="c6f49-118">hello output is similar toohello following example:</span></span>

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="c6f49-119">Bir Linux VM üzerinde zaten yüklü AMPUL ile oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="c6f49-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="c6f49-120">İsterseniz, aşağı çok atlayarak hello yükleme doğrulayabilirsiniz[doğrulayın AMPUL başarıyla yüklendi](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="c6f49-120">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="c6f49-121">AMPUL üzerinde var olan VM izlenecek dağıtma</span><span class="sxs-lookup"><span data-stu-id="c6f49-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="c6f49-122">Bir Linux VM oluşturma yardıma gereksinim duyarsanız, head [burada toolearn nasıl toocreate bir Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="c6f49-122">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="c6f49-123">Ardından, Linux VM hello tooSSH gerekir.</span><span class="sxs-lookup"><span data-stu-id="c6f49-123">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="c6f49-124">Bir SSH anahtarı oluşturma konusunda yardıma gereksinim duyarsanız, head [burada toolearn nasıl toocreate Linux/Mac üzerinde bir SSH anahtarı](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6f49-124">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="c6f49-125">Bir SSH anahtarı zaten varsa, şimdi SSH komut satırından Linux VM ile uygulamasına gidin ve `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="c6f49-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="c6f49-126">Linux VM içinde çalışan, biz hello AMPUL yığın Debian tabanlı dağıtımlar üzerinde yüklenmesinde size yol.</span><span class="sxs-lookup"><span data-stu-id="c6f49-126">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="c6f49-127">Merhaba tam komutları için diğer Linux distro'lar farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c6f49-127">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="c6f49-128">Debian/Ubuntu üzerinde yükleme</span><span class="sxs-lookup"><span data-stu-id="c6f49-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="c6f49-129">Yüklü olan paketleri aşağıdaki hello gerekir: `apache2`, `mysql-server`, `php5`, ve `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="c6f49-129">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="c6f49-130">Bu paketler, doğrudan bu paketleri kapmasını veya Tasksel kullanarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6f49-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="c6f49-131">Yüklemeden önce toodownload gerekir ve güncelleştirme paketini listeler.</span><span class="sxs-lookup"><span data-stu-id="c6f49-131">Before installing you need toodownload and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="c6f49-132">Tek paketler</span><span class="sxs-lookup"><span data-stu-id="c6f49-132">Individual packages</span></span>
<span data-ttu-id="c6f49-133">Get apt kullanma:</span><span class="sxs-lookup"><span data-stu-id="c6f49-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="c6f49-134">Tasksel kullanma</span><span class="sxs-lookup"><span data-stu-id="c6f49-134">Using tasksel</span></span>
<span data-ttu-id="c6f49-135">Alternatif olarak, Tasksel, birden çok ilişkili paketleri, sisteminize Eşgüdümlü "görev" olarak yükler Debian/Ubuntu aracı yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6f49-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="c6f49-136">Merhaba önceki seçeneklerinden birini çalıştırdıktan sonra şunları yapacaksınız istendiğinde tooinstall bu paketleri ve diğer çeşitli bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="c6f49-136">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="c6f49-137">tooset MySQL, bir yönetici parolası 'y', 'Enter' toocontinue basın ve diğer yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="c6f49-137">tooset an administrative password for MySQL, press 'y' and then 'Enter' toocontinue, and follow any other prompts.</span></span> <span data-ttu-id="c6f49-138">Bu işlem hello minimum gerekli PHP uzantıları gerekli toouse PHP MySQL ile yükler.</span><span class="sxs-lookup"><span data-stu-id="c6f49-138">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="c6f49-139">Komut toosee aşağıdaki hello paketleri olarak kullanılabilir olan diğer PHP uzantılarının çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c6f49-139">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="c6f49-140">İnfo.php belge oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6f49-140">Create info.php document</span></span>
<span data-ttu-id="c6f49-141">Şimdi, Apache, MySQL ve PHP sürümünü hello komut satırı yazarak elinizde mümkün toocheck olmalısınız `apache2 -v`, `mysql -v`, veya `php -v`.</span><span class="sxs-lookup"><span data-stu-id="c6f49-141">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="c6f49-142">Tootest gibi daha fazla, hızlı bir PHP bilgi sayfası tooview bir tarayıcıda oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6f49-142">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="c6f49-143">Bir dosya ile Nano metin düzenleyicisi bu komutla oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c6f49-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="c6f49-144">Merhaba GNU Nano metin düzenleyicisi içinde satırlardan hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c6f49-144">Within hello GNU Nano text editor, add hello following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="c6f49-145">Ardından kaydedin ve hello Metin Düzenleyicisi'nden çıkın.</span><span class="sxs-lookup"><span data-stu-id="c6f49-145">Then save and exit hello text editor.</span></span>

<span data-ttu-id="c6f49-146">Tüm yeni yüklemeler etkili şekilde Apache bu komutla yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="c6f49-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="c6f49-147">Başarılı bir şekilde AMPUL doğrulayın</span><span class="sxs-lookup"><span data-stu-id="c6f49-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="c6f49-148">Şimdi bir tarayıcı açıp toohttp://youruniqueDNS/info.php gidip oluşturduğunuz hello PHP bilgileri sayfasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6f49-148">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="c6f49-149">Benzer toothis görüntü görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="c6f49-149">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="c6f49-150">Merhaba Apache2 Ubuntu varsayılan sayfa tooyou http://youruniqueDNS/ giderek görüntüleyerek Apache yüklemenizi denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6f49-150">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="c6f49-151">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="c6f49-151">hello output is similar toohello following example:</span></span>

![][3]

<span data-ttu-id="c6f49-152">Tebrikler, yalnızca Kurulum, Azure VM'deki bir AMPUL yığınına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c6f49-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6f49-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c6f49-153">Next steps</span></span>
<span data-ttu-id="c6f49-154">Merhaba hello AMPUL yığında Ubuntu belgelerine bakın:</span><span class="sxs-lookup"><span data-stu-id="c6f49-154">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="c6f49-155">https://help.ubuntu.com/Community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="c6f49-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
