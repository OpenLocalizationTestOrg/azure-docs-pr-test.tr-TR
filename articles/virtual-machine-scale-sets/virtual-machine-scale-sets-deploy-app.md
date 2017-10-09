---
title: "sanal makine ölçek üzerinde bir uygulama aaaDeploy ayarlar"
description: "Azure sanal makine ölçek kümeleri üzerinde uzantıları toodepoy bir uygulama kullanın."
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a>Sanal makine ölçek kümeleri, uygulamanızda dağıtma

Bu makalede tooinstall yazılım hello zaman hello ölçekte nasıl kümesinin farklı şekilde sağlanır.

Tooreview hello isteyebilirsiniz [ölçek kümesi tasarım genel bakış](virtual-machine-scale-sets-design-overview.md) makalenin hello sınır sanal makine ölçek kümeleri tarafından uygulanmaz bazıları açıklanmaktadır.

## <a name="capture-and-reuse-an-image"></a>Yakalama ve görüntüyü yeniden

Azure tooprepare temel görüntü, Ölçek kümesindeki bir sanal makine kullanabilirsiniz. Bu işlem, hello temel görüntü ölçek kümesi için başvuru depolama hesabınızda yönetilen bir disk oluşturur. 

Adımları hello:

1. Bir Azure sanal makine oluşturma
   * [Linux][linux-vm-create]
   * [Windows][windows-vm-create]

2. Uzak içine hello sanal makine ve hello sistem tooyour istediğiniz özelleştirebilirsiniz.

   İsterseniz, uygulamanız şimdi yükleyebilirsiniz. Uygulamanızı şimdi yükleyerek uygulamanızı daha karmaşık tooremove gerekebileceğinden yükseltme yaptığınız ancak, bilinmesi, ilk. Bunun yerine, bu adım tooinstall uygulamanız gerekebilir, gibi belirli bir çalışma zamanı veya işletim sistemi özelliği tüm Önkoşullar kullanabilirsiniz.

3. Merhaba öğretici "bir makine yakalama" ya da izleyin [Linux] [ linux-vm-capture] veya [Windows][windows-vm-capture].

4. Oluşturma bir [sanal makine ölçek kümesi] [ vmss-create] ile Merhaba URI hello önceki adımda yakalanan görüntü.

Diskler hakkında daha fazla bilgi için bkz: [yönetilen diskleri genel bakış](../virtual-machines/windows/managed-disks-overview.md) ve [eklenen veri disklerini kullanmak](virtual-machine-scale-sets-attached-disks.md).

## <a name="install-when-hello-scale-set-is-provisioned"></a>Merhaba ölçek kümesini sağlandığında yükleme

Sanal makine uzantıları olabilir uygulanan tooa sanal makine ölçek kümesi. Bir sanal makine uzantısı ile tüm grup olarak ayarlanmış bir ölçek hello sanal makinelerde özelleştirebilirsiniz. Uzantıları hakkında daha fazla bilgi için bkz: [sanal makine uzantıları](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Kullanabileceğiniz üç ana uzantıları, Windows tabanlı veya Linux tabanlı açıksa işletim sisteminize bağlı olarak.

### <a name="windows"></a>Windows

Bir Windows tabanlı işletim sistemi için her iki hello kullanmak **özel komut dosyası v1.8** uzantısı veya hello **PowerShell DSC** uzantısı.

#### <a name="custom-script"></a>Özel bir komut dosyası

Merhaba özel betik uzantısı hello ölçek kümesindeki her sanal makine örneğindeki bir komut dosyasını çalıştırır. Bir yapılandırma dosyası veya değişken hangi dosyaların indirilen toohello sanal makine olduğunu ve ardından hangi komutu çalıştırır gösterir. Örneğin bu toorun bir yükleyici, bir komut dosyası, bir toplu iş dosyası, herhangi bir yürütülebilir dosya kullanabilirsiniz.

PowerShell hello ayarları için bir karma tablosu kullanır. Bu örnek hello özel betik uzantısı toorun IIS yükleyen bir PowerShell komut dosyası yapılandırır.

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Kullanım hello `-ProtectedSetting` geçiş için hassas bilgiler içerebilir ayarları.

---------


Azure CLI hello ayarları için bir json dosyası kullanır. Bu örnek hello özel betik uzantısı toorun IIS yükleyen bir PowerShell komut dosyası yapılandırır. JSON dosyası olarak aşağıdaki hello Kaydet _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

Ardından, bu Azure CLI komutunu çalıştırın.

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Kullanım hello `--protected-settings` geçiş için hassas bilgiler içerebilir ayarları.

### <a name="powershell-dsc"></a>PowerShell DSC

PowerShell DSC toocustomize hello ölçek kümesi vm örneklerini kullanabilirsiniz. Merhaba **DSC** uzantısı yayımlanan tarafından **Microsoft.Powershell** dağıtır ve her sanal makine örneğinde sağlanan hello DSC yapılandırması çalıştırılır. Bir yapılandırma dosyası veya değişken hello uzantısı söyler nerede *.zip* paketidir, hangilerinin _betik işlevi_ birleşimi toorun.

PowerShell hello ayarları için bir karma tablosu kullanır. Bu örnek, IIS yükleyen bir DSC paketi dağıtır.

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Kullanım hello `-ProtectedSetting` geçiş için hassas bilgiler içerebilir ayarları.

-----------

Azure CLI json hello ayarlarını kullanır. Bu örnek, IIS yükleyen bir DSC paketi dağıtır. JSON dosyası olarak aşağıdaki hello Kaydet _settings.json_.

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

Ardından, bu Azure CLI komutunu çalıştırın.

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Kullanım hello `--protected-settings` geçiş için hassas bilgiler içerebilir ayarları.

### <a name="linux"></a>Linux

Linux ya da hello kullanabileceğiniz **özel betik v2.0** uzantısı veya kullanım **bulut init** oluşturma sırasında.

Özel komut dosyaları toohello sanal makine örnekleri indirir ve bir komut çalıştıran basit bir uzantısıdır.

#### <a name="custom-script"></a>Özel bir komut dosyası

JSON dosyası olarak aşağıdaki hello Kaydet _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

Sanal makine ölçek kümesi varolan bu uzantı tooan Hello Azure CLI tooadd kullanın. Her bir sanal makine hello ölçeğinde çalıştırır hello uzantısı otomatik olarak ayarlanır.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Kullanım hello `--protected-settings` geçiş için hassas bilgiler içerebilir ayarları.

#### <a name="cloud-init"></a>Bulut başlatma

Bulut Init Hello ölçek kümesi oluşturulurken kullanılır. İlk olarak, adlı bir yerel dosya oluşturma _bulut init.txt_ ve yapılandırma tooit ekleyin. Örneğin, [bu gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)

Kullanım hello Azure CLI toocreate ölçeği ayarlayın. Merhaba `--custom-data` alan bir bulut init betik hello dosya adını kabul eder.

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a>Uygulama güncelleştirmeleri nasıl yönetebilirim?

Uygulamanızı bir uzantısı aracılığıyla dağıttıysanız, bazı şekilde hello uzantısı tanımı alter. Bu değişiklik hello uzantısı imzalanmasını toobe tooall sanal makine örnekleri neden olur. Bir şey **gerekir** değiştirilmesi başvurulan dosyayı, aksi takdirde, yeniden adlandırma gibi hello uzantı hakkında Azure mu uzantısı hello görme değil değişti.

Merhaba uygulaması kendi işletim sistemi görüntüsüne baked, bir otomatik dağıtım ardışık uygulama güncelleştirmelerini kullanın. Üretime ayarlayın aşamalı bir ölçek takas hızlı, mimarisi toofacilitate tasarlayın. Bu yaklaşımın iyi bir örnek hello olan [Azure Spinnaker sürücü iş](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).

[Packer](https://www.packer.io/) ve [Terraform](https://www.terraform.io/) destek Azure Kaynak Yöneticisi, ayrıca görüntülerinizi "code" tanımlamak ve Azure'da, yapı ardından kullanır, bu nedenle hello VHD ölçek kümenizdeki. Ancak, bunu yapmak bu nedenle burada Marketi'nden BITS doğrudan üzerinde değişiklik yapmazsınız beri uzantıları/özel komut dosyaları daha önemli hale Market görüntülerde sorunlu oluşur.

## <a name="what-happens-when-a-scale-set-scales-out"></a>Bir ölçek ölçekler ayarladığınızda ne olduğunu çıkışı?
Bir veya daha fazla sanal makine tooa ölçek kümesi eklediğinizde, hello uygulama otomatik olarak yüklenir. Örnek Hello ölçek kümesi uzantıları tanımlı sahipse için her oluşturulduğunda yeni bir sanal makinede çalıştırın. Merhaba ölçek kümesi üzerinde özel bir görüntü temel alıyorsa, yeni bir sanal makine hello kaynak özel görüntü kopyasıdır. Merhaba ölçek kümesi sanal makineleri kapsayıcı ana bilgisayar varsa, bir özel betik uzantısı'nda başlangıç kod tooload Merhaba kapsayıcılara sahip olabilir. Veya, bir uzantı Azure kapsayıcı hizmeti gibi bir küme orchestrator ile kaydeder bir aracı yükleyebilirsiniz.


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a>Nasıl bir işletim sistemi güncelleştirmeyi güncelleştirme etki alanları arasında alma?
Merhaba sanal makine ölçek kümesi çalıştıran tutarken, işletim sistemi görüntüsü tooupdate istediğinizi varsayalım. PowerShell ve Azure CLI hello hello sanal makine görüntüleri, aynı anda bir sanal makine güncelleştirebilirsiniz. Merhaba [bir sanal makine ölçek kümesi yükseltme](./virtual-machine-scale-sets-upgrade-scale-set.md) makale ayrıca işletim sistemini yükseltme bir sanal makine ölçek kümesi boyunca kullanılabilir tooperform hangi seçeneklerdir daha fazla bilgi sağlar.

## <a name="next-steps"></a>Sonraki adımlar

* [PowerShell toomanage kullanın, Ölçek kümesi.](virtual-machine-scale-sets-windows-manage.md)
* [Bir ölçek kümesi şablonu oluşturun.](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

