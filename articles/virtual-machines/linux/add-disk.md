---
title: Azure CLI kullanarak bir disk tooLinux VM aaaAdd hello | Microsoft Docs
description: "Tooadd hello Azure CLI 1.0 ve 2. 0 ile kalıcı disk tooyour Linux VM öğrenin."
keywords: Linux sanal makine, kaynak disk ekleme
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 3005a066-7a84-4dc5-bdaa-574c75e6e411
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 02/02/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0dc5236be62d96b70dd47a7f621f626a037e22aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-disk-tooa-linux-vm"></a>Disk tooa Linux VM ekleme
Bu makalede nasıl tooattach kalıcı bir disk tooyour VM verilerinizi - koruyabilmeniz için VM'yi yeniden sağlaması yapılana toomaintenance veya yeniden boyutlandırma olsa bile gösterilmektedir. 

## <a name="quick-commands"></a>Hızlı Komutlar
Örnek ekler Hello bir `50`GB disk toohello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:

Yönetilen toouse diskler:

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

Yönetilmeyen toouse diskler:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a>Yönetilen bir diski kullanıma açın

Yönetilen diskleri kullanarak Azure Storage hesapları hakkında endişelenmeden Vm'leriniz ve bunların diskleri toofocus sağlar. Hızlı bir şekilde oluşturmak ve yönetilen bir diski kullanıma açın VM tooa kullanarak hello aynı Azure kaynak grubu veya herhangi bir sayıda diskleri oluşturun ve ardından bunları ekleyin.


### <a name="attach-a-new-disk-tooa-vm"></a>Yeni bir disk tooa VM ekleme

Yeni bir disk üzerinde VM yeterlidir, hello kullanabilirsiniz `az vm disk attach` komutu.

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a>Var olan bir diski ekleme 

Çoğu durumda, önceden oluşturduğunuz diskleri ekleyebilir. İlk hello disk kimliği bulun ve sonra o toohello geçirin `az vm disk attach` komutu. Merhaba aşağıdaki örnek ile oluşturulan bir diski kullanan `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

Merhaba çıktı hello aşağıdaki gibi görünüyor (Merhaba kullanabilirsiniz `-o table` seçeneği tooany komut tooformat hello çıktısında):

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Empty",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": null,
    "storageAccountId": null
  },
  "diskSizeGb": 50,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/rasquill-script/providers/Microsoft.Compute/disks/myDataDisk",
  "location": "westus",
  "name": "myDataDisk",
  "osType": null,
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-02T23:35:47.708082+00:00",
  "type": "Microsoft.Compute/disks"
}
```


## <a name="attach-an-unmanaged-disk"></a>Yönetilmeyen bir diski kullanıma açın

Yeni bir disk ekleme hello bir disk oluşturma olmayacaksa hızlı aynı depolama hesabı, VM olarak. Tür `azure vm disk attach-new` toocreate ve VM için yeni bir GB disk ekleyin. Bir depolama hesabı açıkça belirtmeyen, oluşturduğunuz herhangi bir disk hello aynı yerleştirildiğinde, işletim sistemi diski bulunduğu depolama hesabı. Örnek ekler Hello bir `50`GB disk toohello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a>Linux VM toomount hello yeni disk toohello Bağlan
> [!NOTE]
> Bu konuda tooa VM bağlanan kullanıcı adları ve parolaları kullanarak. toouse ortak ve özel anahtar çiftlerini toocommunicate, VM ile bkz [nasıl tooUse Linux Azure üzerinde SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
> 
> 

TooSSH gerekir, Azure VM toopartition içine biçimlendirmek ve Linux VM kullanabilmesi için yeni diski bağlayabilir. Bağlayarak ile hakkında bilgi sahibi değilseniz **ssh**, hello komutu alır hello form `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`ve hello aşağıdaki gibi görünür:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

Çıktı

```bash
hello authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) toohello list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome tooUbuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

* Documentation:  https://help.ubuntu.com/

System information as of Fri May 22 21:02:32 UTC 2015

System load: 0.37              Memory usage: 2%   Processes:       207
Usage of /:  41.4% of 1.94GB   Swap usage:   0%   Users logged in: 0

Graph this data and manage this system at:
  https://landscape.canonical.com/

Get cloud support with Ubuntu Advantage Cloud Guest:
  http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

ops@myVM:~$
```

Bağlandınız, şimdi tooyour VM, hazır tooattach bir disk.  İlk hello Bul kullanarak, disk `dmesg | grep SCSI` (Merhaba yöntemi kullandığınız yeni diskinizin değişebilir toodiscover). Bu durumda, onu şöyle görünür:

```bash
dmesg | grep SCSI
```

Çıktı

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

ve bu konuda hello durumda hello `sdc` hello istiyoruz bir disktir. Şimdi bölüm hello diskle `sudo fdisk /dev/sdc` --disk, servis talebi hello olduğu varsayılarak `sdc`, birincil disk bölüm 1 yapın ve kabul diğer Varsayılanları hello.

```bash
sudo fdisk /dev/sdc
```

Çıktı

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide toowrite them.
After that, of course, hello previous content won't be recoverable.

Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-10485759, default 2048):
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-10485759, default 10485759):
Using default value 10485759
```

Merhaba bölüm yazarak oluşturmak `p` hello isteminde:

```bash
Command (m for help): p

Disk /dev/sdc: 5368 MB, 5368709120 bytes
255 heads, 63 sectors/track, 652 cylinders, total 10485760 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x2a59b123

   Device Boot      Start         End      Blocks   Id  System
/dev/sdc1            2048    10485759     5241856   83  Linux

Command (m for help): w
hello partition table has been altered!

Calling ioctl() toore-read partition table.
Syncing disks.
```

Ve hello kullanarak bir dosya sistemi toohello bölümü yazma **mkfs** dosya sistemi türü ve hello aygıt adı belirterek komutu. Bu konuda, biz kullanmakta olduğunuz `ext4` ve `/dev/sdc1` üstten:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Çıktı

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for hello super user
First data block=0
Maximum filesystem blocks=1342177280
40 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
    32768, 98304, 163840, 229376, 294912, 819200, 884736
Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

Bir dizin toomount hello kullanarak dosya sistemini oluşturmak üzere, şimdi `mkdir`:

```bash
sudo mkdir /datadrive
```

Ve dizin hello kullanarak bağlayın `mount`:

```bash
sudo mount /dev/sdc1 /datadrive
```

Merhaba veri diski olduğu şimdi hazır toouse olarak `/datadrive`.

```bash
ls
```

Çıktı

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

olması gereken yeniden başlatma toohello /etc/fstab dosya ekleninceye sonra tooensure hello sürücü otomatik olarak yeniden. Ayrıca, önerilir hello UUID (evrensel benzersiz tanıtıcı) / etc içinde kullanılan/fstab toorefer toohello sürücü yalnızca hello aygıt adı yerine (gibi `/dev/sdc1`). Merhaba işletim sistemi önyükleme sırasında disk hatası algılarsa, hello UUID kullanarak hello hatalı disk konumu verilen takılı tooa olan önler. Veri diskleri kalan sonra bu aynı aygıt kimlikleri atanması. toofind hello yeni sürücü UUID Merhaba, hello kullan **blkid** yardımcı programı:

```bash
sudo -i blkid
```

Merhaba çıkış benzer toohello aşağıdaki gibidir:

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> Yanlış hello düzenleme **/etc/fstab** dosya önyüklenemez bir sisteme neden. Emin değilseniz, bu dosyayı tooproperly düzenleme nasıl bilgi toohello dağıtım'ın belgelerine başvurun. Ayrıca, düzenlemeye başlamadan önce hello /etc/fstab dosyanızın bir yedeğini oluşturduğunuz önerilir.
> 
> 

Ardından, hello'ı açmak **/etc/fstab** dosyasını bir metin düzenleyicisinde:

```bash
sudo vi /etc/fstab
```

Bu örnekte, hello UUID değeri Merhaba yeni kullanırız **/dev/sdc1** oluşturulduğu hello önceki adımları ve hello mountpoint aygıt **/datadrive**. Satır toohello hello sonuna aşağıdaki hello eklemek **/etc/fstab** dosyası:

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> Daha sonra bir veri diski fstab düzenlemeden kaldırma hello VM toofail tooboot neden olabilir. Çoğu dağıtımları ya da hello sağlamak `nofail` ve/veya `nobootwait` fstab seçenekleri. Merhaba disk toomount önyükleme sırasında başarısız olsa bile bu seçenekler sistem tooboot izin verir. Bu parametreler hakkında daha fazla bilgi için dağıtım ait belgelere bakın.
> 
> Merhaba **nofail** seçeneği, VM başlatır hello dosya sistemi bozuk veya hello disk önyükleme sırasında yok olsa bile bu hello sağlar. Bu seçenek olmadan, davranış açıklandığı gibi karşılaşabilirsiniz [olamaz SSH tooLinux VM tooFSTAB hatalar nedeniyle](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)

### <a name="trimunmap-support-for-linux-in-azure"></a>KIRPMA/UNMAP Azure Linux desteği
Bazı Linux tekrar KIRPMA/UNMAP işlemleri toodiscard destek hello diskte kullanılmayan engeller. Bu sayfa silinmiş Azure artık geçerli değil ve iptal edilecek standart depolama tooinform özellikle yararlıdır. Büyük dosyaları oluşturmak ve bunları silerseniz bu maliyet tasarrufu sağlar.

Tooenable KIRPMA desteği, Linux VM'NİZDE iki yolu vardır. Her zamanki gibi dağıtımınız için önerilen yaklaşımı hello bakın:

* Kullanım hello `discard` bağlama seçeneği `/etc/fstab`, örneğin:

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* Bazı durumlarda hello içinde `discard` seçeneği performans etkileri olabilir. Alternatif olarak, hello çalıştırabilirsiniz `fstrim` komutunu el ile Merhaba komut satırından veya tooyour crontab toorun düzenli olarak ekleyin:
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>Sorun giderme
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Sonraki Adımlar
* Unutmayın, bu bilgileri tooyour yazma sürece bunu yeniden başlatılırsa, yeni disk kullanılabilir toohello VM olmadığını [fstab](http://en.wikipedia.org/wiki/Fstab) dosya.
* Linux VM tooensure yapılandırılmış doğru gözden geçirme hello [Linux makine performansı en iyi duruma](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) öneriler.
* İlave diskler eklenerek, depolama kapasitesi ve [RAID yapılandırma](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ek performans.

