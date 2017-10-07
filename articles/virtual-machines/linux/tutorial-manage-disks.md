---
title: aaaManage Azure diskleri hello Azure CLI ile | Microsoft Docs
description: "Öğretici - hello Azure CLI ile Azure diskleri yönetme"
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
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a>Hello Azure CLI ile Azure diskleri yönetme

Azure sanal makineleri diskleri toostore hello VM'ler işletim sistemi, uygulamaları ve verileri kullanın. Bir VM oluştururken önemli toochoose disk boyutu ve yapılandırma beklenen uygun toohello iş yüküne bağlıdır. Bu öğretici, dağıtma ve VM diskleri yönetme kapsar. Hakkında bilgi edinin:

> [!div class="checklist"]
> * İşletim sistemi ve geçici disklerle
> * Veri diskleri
> * Standart ve Premium diskleri
> * Disk performansı
> * Ekleme ve veri diskleri hazırlama
> * Diskleri yeniden boyutlandırma
> * Disk anlık görüntüler


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="default-azure-disks"></a>Azure diskleri varsayılan

Bir Azure sanal makine oluşturulduğunda, iki diskleri otomatik olarak eklenen toohello sanal makine içindir. 

**İşletim sistemi diski** - işletim sistemi disklerinde too1 terabayt boyutta ve ana hello VM'ler işletim sistemi. Merhaba işletim sistemi diski olarak etiketlenmiş */dev/sda* varsayılan olarak. Merhaba işletim sistemi disk yapılandırması önbelleğe alma hello disk işletim sistemi performans için optimize edilmiştir. Bu yapılandırma nedeniyle, işletim sistemi diski hello **vermemelisiniz** konak uygulamalar veya veri. Uygulamalar ve veriler için bu makalenin sonraki bölümlerinde ayrıntılı veri diskleri kullanın. 

**Geçici disk** -geçici diskler hello üzerinde bulunan bir katı hal sürücüsü kullanan aynı Azure ana bilgisayar hello VM olarak. Temp disklerinin yüksek oranda kullanıcı durumda ve geçici veri işleme gibi işlemler için kullanılabilir. Ancak, Hello VM taşınan tooa yeni ana bilgisayar ise, geçici bir diskte depolanan tüm verileri kaldırılır. Merhaba hello geçici disk boyutunu hello VM boyutu tarafından belirlenir. Geçici diskleri etiketli */dev/sdb* ve mountpoint, */mnt*.

### <a name="temporary-disk-sizes"></a>Geçici disk boyutları

| Tür | VM boyutu | En büyük geçici disk boyutu (GB) |
|----|----|----|
| [Genel amaçlı](sizes-general.md) | A ve D serisi | 800 |
| [İşlem için iyileştirilmiş](sizes-compute.md) | F serisi | 800 |
| [Bellek için iyileştirilmiş](../virtual-machines-windows-sizes-memory.md) | D ve G serisi | 6144 |
| [Depolama için iyileştirilmiş](../virtual-machines-windows-sizes-storage.md) | L serisi | 5630 |
| [GPU](sizes-gpu.md) | N serisi | 1440 |
| [Yüksek performans](sizes-hpc.md) | A ve H serisi | 2000 |

## <a name="azure-data-disks"></a>Azure veri diski

Uygulama yükleme ve verilerini depolamak için ek veri disklerinin eklenebilir. Veri diskleri sağlam ve esnek veri depolama burada istenen herhangi bir durumda kullanılmalıdır. Her veri diski 1 terabayttan küçük maksimum kapasitesine sahiptir. kaç tane veri diskleri ekli tooa VM olabilir hello sanal makine Hello boyutunu belirler. Her VM çekirdek için iki veri diskleri eklenebilir. 

### <a name="max-data-disks-per-vm"></a>VM başına en fazla veri diski

| Tür | VM boyutu | VM başına en fazla veri diski |
|----|----|----|
| [Genel amaçlı](sizes-general.md) | A ve D serisi | 32 |
| [İşlem için iyileştirilmiş](sizes-compute.md) | F serisi | 32 |
| [Bellek için iyileştirilmiş](../virtual-machines-windows-sizes-memory.md) | D ve G serisi | 64 |
| [Depolama için iyileştirilmiş](../virtual-machines-windows-sizes-storage.md) | L serisi | 64 |
| [GPU](sizes-gpu.md) | N serisi | 48 |
| [Yüksek performans](sizes-hpc.md) | A ve H serisi | 32 |

## <a name="vm-disk-types"></a>VM disk türleri

Azure disk iki tür sağlar.

### <a name="standard-disk"></a>Standart disk

Standart Depolama, HDD’ler ile desteklenir ve yüksek performans sunarken uygun maliyetli depolama sağlar. Standart diskler için uygun maliyetli geliştirme idealdir ve iş yükü test.

### <a name="premium-disk"></a>Premium disk

Premium diskler, SSD tabanlı yüksek performanslı, düşük gecikme süreli disk tarafından desteklenir. Üretim iş yükü çalıştıran VM'ler için mükemmel. Premium depolama destekleyen DS serisi, DSv2 serisi, GS serisi ve FS-serisi VM'ler. Üç tür (P10, P20, P30) Premium diskleri gelir, hello disk türü hello hello diskin boyutunu belirler. Seçerken, bir disk boyutu hello değeri toohello sonraki türü yuvarlanır. Merhaba disk boyutu 128 GB daha az ise, örneğin, hello disk P10 türüdür. Merhaba disk boyutu 129 GB ile 512 GB arasında ise, hello bir P20 boyutudur. Hiçbir şey üzerinde 512 GB hello boyutudur bir P30.

### <a name="premium-disk-performance"></a>Premium disk performansı

|Premium depolama disk türü | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Disk boyutu (yukarı yuvarlar) | 128 GB | 512 GB | 1.024 GB (1 TB) |
| Disk başına en fazla IOPS | 500 | 2,300 | 5,000 |
Disk başına aktarım hızı | 100 MB/s | 150 MB/s | 200 MB/sn |

Disk başına maksimum IOPS Merhaba tablonun yukarısındaki tanımlayan olsa da, daha yüksek düzeyde performans birden çok veri diskleri bölümlemesine tarafından elde edilebilir. Örneğin, bir Standard_GS5 VM en 80.000 IOPS elde edebilirsiniz. VM başına maksimum IOPS hakkında ayrıntılı bilgi için bkz: [Linux VM boyutları](sizes.md).

## <a name="create-and-attach-disks"></a>Oluşturma ve diskleri ekleme

Veri diskleri oluşturulan ve VM oluşturma zamanı veya var olan VM tooan bağlı.

### <a name="attach-disk-at-vm-creation"></a>VM oluşturulurken diski kullanıma açın

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) komutu. 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

Hello kullanarak bir VM oluşturma [az vm oluşturma]( /cli/azure/vm#create) komutu. Merhaba `--datadisk-sizes-gb` olmayan bir ek disk oluşturulması gerektiğini ve toohello sanal makineye bağlı kullanılan toospecify bağımsız değişken. toocreate ve birden fazla disk ekleyin, disk boyutu değerleri boşlukla ayrılmış bir listesini kullanın. Aşağıdaki örneğine hello VM iki veri disklerinde, her iki 128 GB oluşturulur. Merhaba disk boyutları 128 GB olduğundan, bu diskleri hem de disk başına en fazla 500 IOPS sağlar P10s olarak yapılandırılır.

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a>Disk tooexisting VM ekleme

toocreate ve yeni disk tooan var olan bir sanal makine ekleme, hello kullanma [az vm diskini](/cli/azure/vm/disk#attach) komutu. Merhaba aşağıdaki örnekte bir premium disk boyutu, 128 gigabayt oluşturur ve VM hello son adımda oluşturduğunuz toohello ekler.

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a>Veri diskleri hazırlama

Bir disk ekli toohello sanal makine sağlandıktan sonra yapılandırılmış toobe toouse hello disk hello işletim sistemi gerekir. Aşağıdaki örnek hello nasıl toomanually yapılandırmak bir disk gösterir. Bu işlem ayrıca içinde ele bulut-init, kullanarak otomatik olarak yapılabilir bir [sonraki öğretici](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>El ile yapılandırma

Bir SSH bağlantısı ile Merhaba sanal makine oluşturun. Merhaba örnek IP adresinin hello genel IP hello sanal makinenin ile değiştirin.

```azurecli-interactive 
ssh 52.174.34.95
```

Bölüm hello diskle `fdisk`.

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

Hello kullanarak bir dosya sistemi toohello bölümü yazma `mkfs` komutu.

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Böylece hello işletim sisteminde erişilebilir hello yeni diski bağlayın.

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

Merhaba disk şimdi hello erişilebilir *datadrive* hello çalıştırarak doğrulanabilir mountpoint `df -h` komutu. 

```bash
df -h
```

Merhaba çıktısını gösterir hello yeni sürücü üzerinde takılı */datadrive*.

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

Sürücü hello tooensure bir yeniden başlatmadan sonra yeniden, toohello eklenmelidir */etc/fstab* dosya. toodo, bu nedenle, hello hello disk UUID'si hello ile almak `blkid` yardımcı programı.

```bash
sudo -i blkid
```

Merhaba çıktısını görüntüler hello hello sürücü UUID'si `/dev/sdc1` bu durumda.

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

Toohello aşağıdaki satırı benzer toohello ekleme */etc/fstab* dosya. Ayrıca engelleri yazma Not kullanarak devre dışı bırakılabilir *engel = 0*, bu yapılandırma disk performansını artırabilir. 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

Merhaba disk yapılandırıldı, hello SSH oturumu kapatın.

```bash
exit
```

## <a name="resize-vm-disk"></a>VM disk yeniden boyutlandırma

Bir VM dağıtıldıktan sonra hello işletim sistemi diski veya hiçbir bağlı veri diski boyutu artırılabilir. Bir diskin Hello boyutunu artırmayı daha fazla depolama alanı ya da daha yüksek düzeyde performans (P10, P20, P30) ihtiyacı olduğunda faydalıdır. Disk boyutu azaltılamaz unutmayın.

Disk boyutunun artırılması önce kimliği hello veya hello disk adı gereklidir. Kullanım hello [az disk listesi](/cli/azure/vm/disk#list) komutu tooreturn tüm diskler bir kaynak grubunda. Merhaba disk adı tooresize istediğiniz not edin.

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

Merhaba VM deallocated olmalıdır. Kullanım hello [az vm serbest bırakma]( /cli/azure/vm#deallocate) komut toostop ve hello VM serbest bırakma.

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

Kullanım hello [az disk güncelleştirme](/cli/azure/vm/disk#update) komutu tooresize hello disk. Bu örnek adlı bir disk yeniden boyutlandırır *myDataDisk* too1 terabayt.

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

Merhaba yeniden boyutlandırma işlemi tamamlandıktan sonra hello VM başlatın.

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

İşletim sistemi diski hello boyutlandırdıysanız hello bölüm otomatik olarak olması genişletilmiştir. Bir veri diski yeniden boyutlandırılabilir, geçerli tüm bölümler hello VM'ler işletim sisteminde genişletilmiş toobe gerekir.

## <a name="snapshot-azure-disks"></a>Azure diskleri anlık görüntüsünü alın

Bir disk anlık hello disk okuma yalnızca, zaman noktası kopyasını oluşturur. Azure VM anlık görüntüler, yapılandırma değişiklikleri yapmadan önce bir VM hello durumunu hızlı bir şekilde kaydetmek için kullanışlıdır. Merhaba olay hello yapılandırma değişiklikleri kanıtlanmasına istenmeden toobe, VM durumunu hello anlık görüntü kullanılarak geri yüklenebilir. Birden fazla disk bir VM'ye sahip olduğu bir anlık görüntü hello bağımsız olarak her disk oluşturulduğunda diğerleri. Uygulama tutarlı yedek almak için disk anlık görüntüler çıkarmadan önce hello VM durdurma göz önünde bulundurun. Alternatif olarak, hello kullanın [Azure Backup hizmeti](/azure/backup/), hangi etkinleştirir, tooperform VM çalıştıran hello sırasında yedeklemeleri otomatik.

### <a name="create-snapshot"></a>Anlık görüntü oluşturma

Bir sanal makine disk anlık oluşturmadan önce hello kimliği veya hello disk adı gerekli. Kullanım hello [az vm Göster](https://docs.microsoft.com/en-us/cli/azure/vm#show) komutu tooreturn hello disk kimliği. Bu örnekte, böylece daha sonraki bir adımda kullanılabilir hello disk kimliği bir değişkende depolanır.

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

Merhaba sanal makine diski hello kimliğini sahip olduğunuza göre hello aşağıdaki komut hello diskin anlık görüntüsünü oluşturur.

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a>Disk anlık görüntüden oluşturma

Bu anlık görüntü sonra kullanılan toorecreate hello sanal makineye bağlanabilir bir diske dönüştürülebilir.

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a>Sanal makine anlık görüntüden geri yükleme

toodemonstrate sanal makine kurtarması, delete hello varolan sanal makine. 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

Başlangıç anlık görüntü diskten yeni bir sanal makine oluşturun.

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a>Veri diski yeniden bağlayın

Tüm veri diskleri yeniden toobe toohello sanal makine gerekir.

İlk hello kullanarak hello veri disk adı Bul [az disk listesi](https://docs.microsoft.com/cli/azure/disk#list) komutu. Bu örnek yerler hello adlı bir değişkende hello diskin adını *datadisk*, hello sonraki adımda kullanılır.

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

Kullanım hello [az vm diskini](https://docs.microsoft.com/cli/azure/vm/disk#attach) komutu tooattach hello disk.

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, VM diskleri konuları hakkında gibi öğrenilen:

> [!div class="checklist"]
> * İşletim sistemi ve geçici disklerle
> * Veri diskleri
> * Standart ve Premium diskleri
> * Disk performansı
> * Ekleme ve veri diskleri hazırlama
> * Diskleri yeniden boyutlandırma
> * Disk anlık görüntüler

VM yapılandırması otomatikleştirme hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [VM yapılandırmasını otomatikleştirme](./tutorial-automate-vm-deployment.md)
