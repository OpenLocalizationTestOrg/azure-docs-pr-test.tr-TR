---
title: "aaaCreate ve Linux sanal makineleri yönetme hello Azure CLI | Microsoft Docs"
description: "Öğretici - oluşturmak ve yönetmek Linux VM'ler ile hello Azure CLI"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a>Oluşturma ve yönetme Linux VM'ler ile Azure CLI hello

Azure sanal makineler tam olarak yapılandırılabilir ve esnek bir bilgi işlem ortamı sağlar. Bu öğretici, bir VM boyutu seçerek, bir VM görüntüsü seçme ve bir VM dağıtma gibi temel Azure sanal makine dağıtım öğeleri kapsar. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Oluştur ve tooa VM Bağlan
> * Seçin ve VM görüntüleri kullanmak
> * Görüntüleme ve belirli VM boyutları kullanma
> * VM’yi yeniden boyutlandırma
> * Görüntüleyin ve VM durumunu anlamak


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="create-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) komutu. 

Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. Bir kaynak grubu bir sanal makine önce oluşturulması gerekir. Bu örnekte, bir kaynak grubu adında *myResourceGroupVM* hello oluşturulan *eastus* bölge. 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

Merhaba kaynak grubu oluştururken veya değiştirirken Bu öğretici görülebilir bir VM belirtilir.

## <a name="create-virtual-machine"></a>Sanal makine oluşturma

Merhaba ile bir sanal makine oluşturmak [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create) komutu. 

Bir sanal makine oluştururken, işletim sistemi görüntüsü, disk boyutlandırma ve yönetici kimlik bilgileri gibi birkaç seçenek bulunur. Bu örnekte, bir sanal makine adı ile oluşturulan *myVM* Ubuntu Server çalıştıran. 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

Bir kez hello VM oluşturulduktan sonra hello Azure CLI hello VM bilgilerini çıkarır. Merhaba not edin `publicIpAddress`, bu adres kullanılan tooaccess hello sanal makineye bağlanabilir... 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a>TooVM Bağlan

Şimdi toohello VM bağlanabilir SSH kullanarak. Merhaba örnek IP adresi ile hello yerine `publicIpAddress` hello önceki adımda not ettiğiniz.

```bash
ssh 52.174.34.95
```

Merhaba VM ile işlemi tamamladıktan sonra hello SSH oturumu kapatın. 

```bash
exit
```

## <a name="understand-vm-images"></a>VM görüntüleri anlama

Hello Azure Market kullanılan toocreate VM'ler olabilecek çok sayıda görüntü içerir. Merhaba önceki adımlarda, bir sanal makine bir Ubuntu görüntü kullanılarak oluşturuldu. Bu adımda, Azure CLI ise bir CentOS görüntü için kullanılan toosearch hello Market olduğu hello toodeploy ikinci bir sanal makinede kullanılır.  

toosee hello listesi en yaygın olarak kullanılan görüntüleri, hello kullan [az vm görüntü listesi](/cli/azure/vm/image#list) komutu.

```azurecli-interactive 
az vm image list --output table
```

Merhaba komutu çıktısı Azure'da hello en popüler VM görüntüleri döndürür.

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

Merhaba ekleyerek tam bir listesi görülebilir `--all` bağımsız değişkeni. Merhaba resim listesi ayrıca göre filtrelenmiş `--publisher` veya `–-offer`. Bu örnekte, tüm görüntüleri için eşleşen bir teklif ile Merhaba listesi filtrelenir *CentOS*. 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

Kısmi çıktı:

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

belirli bir görüntü kullanarak bir VM'i toodeploy hello hello değeri not alın *Urn* sütun. Merhaba görüntü belirtirken, hello görüntü sürüm numarası ile "son", hangi hello dağıtım en son sürümünü hello seçer değiştirilebilir. Bu örnekte, hello `--image` kullanılan toospecify hello en son sürümünü CentOS 6.5 görüntü değişkendir.  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a>VM boyutları anlama

Bir sanal makine boyutu, kullanılabilir toohello sanal makine yapılan işlem kaynaklarını CPU, GPU ve bellek gibi hello miktarını belirler. Sanal makinelerin beklendiği hello iş yükü için uygun şekilde boyutlandırılmış toobe gerekir. İş yükü artarsa, var olan bir sanal makine yeniden boyutlandırılabilir.

### <a name="vm-sizes"></a>VM boyutları

Aşağıdaki tablonun hello boyutları kullanım örneklerine kategorilere ayırır.  

| Tür                     | Boyutlar           |    Açıklama       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Genel amaçlı](sizes-general.md)         |Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7| Dengeli CPU bellekten. Geliştirme için ideal / test ve küçük toomedium uygulamaları ve verileri çözümler.  |
| [İşlem için iyileştirilmiş](sizes-compute.md)   | FS, F             | Yüksek CPU bellekten. Orta düzey trafik uygulamalar, ağ uygulamaları ve toplu işlemler için iyidir.        |
| [Bellek için iyileştirilmiş](../virtual-machines-windows-sizes-memory.md)    | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Yüksek bellek için-çekirdek. İlişkisel veritabanları, Orta toolarge önbellekleri ve bellek içi analizi için mükemmel.                 |
| [Depolama için iyileştirilmiş](../virtual-machines-windows-sizes-storage.md)      | Ls                | Yüksek disk aktarım hızı ve GÇ. Büyük Veri, SQL ve NoSQL veritabanları için ideal.                                                         |
| [GPU](sizes-gpu.md)          | NV, NC            | Yoğun Grafik işleme ve video düzenleme için hedeflenen özel VM'ler.       |
| [Yüksek performans](sizes-hpc.md) | H, A8-11          | Bizim en güçlü CPU VM'ler isteğe bağlı yüksek verimlilik ağ arabirimlerine (RDMA) sahip. 


### <a name="find-available-vm-sizes"></a>Kullanılabilir VM boyutları Bul

toosee VM listesi boyutları kullanılabilen belirli bir bölgede, hello kullan [az vm listesi-boyutları](/cli/azure/vm#list-sizes) komutu. 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

Kısmi çıktı:

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a>Belirli boyutuyla VM oluşturma

Merhaba önceki VM oluşturma örnekte, bir boyut değil sağlanmadığından, varsayılan boyutu sonuçlanır. Oluşturma zamanı kullanarak bir VM boyutu seçilebilir [az vm oluşturma](/cli/azure/vm#create) ve hello `--size` bağımsız değişkeni. 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a>VM’yi yeniden boyutlandırma

Bir VM dağıtıldıktan sonra onu yeniden boyutlandırılan tooincrease olması veya kaynak ayırma azaltın.

Merhaba istenen boyuta hello geçerli Azure kümede kullanılabilir durumdaysa bir VM'yi yeniden boyutlandırılırken önce denetleyin. Merhaba [az vm listesi-vm-yeniden boyutlandırma-seçenekleri](/cli/azure/vm#list-vm-resize-options) döndürür hello boyutlarının listesi komutu. 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
Merhaba boyutu kullanılabilir isterseniz, hello işlemi sırasında yeniden başlatılıncaya kadar ancak hello VM bir gücü açma durumundan yeniden boyutlandırılabilir. Kullanım hello [az VM'yi yeniden boyutlandırın]( /cli/azure/vm#resize) komutu tooperform hello yeniden boyutlandırın.

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

Merhaba istenen boyut hello geçerli kümede hello VM hello yeniden boyutlandırma önce işlemi serbest toobe oluşabilir gereksinimlerini değildir. Kullanım hello [az vm serbest bırakma]( /cli/azure/vm#deallocate) komut toostop ve hello VM serbest bırakma. Merhaba, Not VM geri desteklenir, hello geçici diskteki tüm verilerin kaldırılmış olabilir. Merhaba genel IP adresi statik bir IP adresi kullanılmadığı sürece da değişir. 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

Serbest sonra hello boyutlandırma ortaya çıkabilir. 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

Merhaba yeniden boyutlandırıldıktan sonra hello VM başlatılabilir.

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a>VM güç durumları

Bir Azure VM birçok güç durumlarını birine sahip. Bu durum hello hiper yönetici hello açısından hello VM hello geçerli durumunu temsil eder. 

### <a name="power-states"></a>Güç durumları

| Güç durumu | Açıklama
|----|----|
| Başlangıç | Merhaba sanal makinenin başlatıldığı gösterir. |
| Çalışıyor | Merhaba sanal makinenin çalışmadığını gösterir. |
| Durduruluyor | Bu hello sanal makinenin durdurulması gösterir. | 
| Durduruldu | Bu hello sanal makine durdurulduğunda gösterir. Sanal makineler hello durdurulmuş durumda hala işlem ücretleri.  |
| Ayırmayı kaldırma | Merhaba sanal makinenin serbest gösterir. |
| Serbest bırakıldı | Merhaba sanal makinenin hello hiper Yöneticisi'nden kaldırıldı ancak hello denetim düzlemi hala kullanılabilir olduğunu gösterir. Merhaba Deallocated durumu içindeki sanal makineler bilgi işlem ücretleri değil. |
| - | Merhaba güç hello sanal makinenin durumunu bilinmediğini gösterir. |

### <a name="find-power-state"></a>Güç durumu Bul

belirli bir VM, kullanım hello tooretrieve hello durumu [az vm örnek görünümünü Al](/cli/azure/vm#get-instance-view) komutu. Emin toospecify bir sanal makine ve kaynak grubu için geçerli bir ad olabilir. 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

Çıktı:

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a>Yönetim görevleri

Merhaba yaşam döngüsü sırasında sanal makinenin, başlatma, durdurma veya bir sanal makine silme gibi yönetim görevleri toorun isteyebilirsiniz. Ayrıca, toocreate, komut dosyaları tooautomate yineleyen veya karmaşık görevleri isteyebilirsiniz. Hello Azure CLI kullanarak, birçok ortak yönetim görevlerinin hello komut satırından veya komut dosyalarında çalıştırabilirsiniz. 

### <a name="get-ip-address"></a>IP adresi al

Bu komut, bir sanal makinenin hello özel ve genel IP adresleri döndürür.  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a>Sanal makineyi durdurma

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a>Sanal makineyi Başlat

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a>Kaynak grubunu silme

Bir kaynak grubunu silme içinde içerdiği tüm kaynaklar da siler.

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, temel VM oluşturmayı ve yönetmeyi nasıl gibi hakkında öğrenilen:

> [!div class="checklist"]
> * Oluştur ve tooa VM Bağlan
> * Seçin ve VM görüntüleri kullanmak
> * Görüntüleme ve belirli VM boyutları kullanma
> * VM’yi yeniden boyutlandırma
> * Görüntüleyin ve VM durumunu anlamak

Toohello sonraki öğretici toolearn VM disklerle ilgili ilerleyin.  

> [!div class="nextstepaction"]
> [Oluşturma ve yönetme VM diskleri](./tutorial-manage-disks.md)
