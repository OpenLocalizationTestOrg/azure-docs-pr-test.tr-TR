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
# <a name="add-a-disk-tooa-linux-vm"></a><span data-ttu-id="96abe-104">Disk tooa Linux VM ekleme</span><span class="sxs-lookup"><span data-stu-id="96abe-104">Add a disk tooa Linux VM</span></span>
<span data-ttu-id="96abe-105">Bu makalede nasıl tooattach kalıcı bir disk tooyour VM verilerinizi - koruyabilmeniz için VM'yi yeniden sağlaması yapılana toomaintenance veya yeniden boyutlandırma olsa bile gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="96abe-105">This article shows how tooattach a persistent disk tooyour VM so that you can preserve your data - even if your VM is reprovisioned due toomaintenance or resizing.</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="96abe-106">Hızlı Komutlar</span><span class="sxs-lookup"><span data-stu-id="96abe-106">Quick Commands</span></span>
<span data-ttu-id="96abe-107">Örnek ekler Hello bir `50`GB disk toohello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="96abe-107">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

<span data-ttu-id="96abe-108">Yönetilen toouse diskler:</span><span class="sxs-lookup"><span data-stu-id="96abe-108">toouse managed disks:</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

<span data-ttu-id="96abe-109">Yönetilmeyen toouse diskler:</span><span class="sxs-lookup"><span data-stu-id="96abe-109">toouse unmanaged disks:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a><span data-ttu-id="96abe-110">Yönetilen bir diski kullanıma açın</span><span class="sxs-lookup"><span data-stu-id="96abe-110">Attach a managed disk</span></span>

<span data-ttu-id="96abe-111">Yönetilen diskleri kullanarak Azure Storage hesapları hakkında endişelenmeden Vm'leriniz ve bunların diskleri toofocus sağlar.</span><span class="sxs-lookup"><span data-stu-id="96abe-111">Using managed disks enables you toofocus on your VMs and their disks without worrying about Azure Storage accounts.</span></span> <span data-ttu-id="96abe-112">Hızlı bir şekilde oluşturmak ve yönetilen bir diski kullanıma açın VM tooa kullanarak hello aynı Azure kaynak grubu veya herhangi bir sayıda diskleri oluşturun ve ardından bunları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="96abe-112">You can quickly create and attach a managed disk tooa VM using hello same Azure resource group, or you can create any number of disks and then attach them.</span></span>


### <a name="attach-a-new-disk-tooa-vm"></a><span data-ttu-id="96abe-113">Yeni bir disk tooa VM ekleme</span><span class="sxs-lookup"><span data-stu-id="96abe-113">Attach a new disk tooa VM</span></span>

<span data-ttu-id="96abe-114">Yeni bir disk üzerinde VM yeterlidir, hello kullanabilirsiniz `az vm disk attach` komutu.</span><span class="sxs-lookup"><span data-stu-id="96abe-114">If you just need a new disk on your VM, you can use hello `az vm disk attach` command.</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a><span data-ttu-id="96abe-115">Var olan bir diski ekleme</span><span class="sxs-lookup"><span data-stu-id="96abe-115">Attach an existing disk</span></span> 

<span data-ttu-id="96abe-116">Çoğu durumda, önceden oluşturduğunuz diskleri ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="96abe-116">In many cases you attach disks that have already been created.</span></span> <span data-ttu-id="96abe-117">İlk hello disk kimliği bulun ve sonra o toohello geçirin `az vm disk attach` komutu.</span><span class="sxs-lookup"><span data-stu-id="96abe-117">You first find hello disk id and then pass that toohello `az vm disk attach` command.</span></span> <span data-ttu-id="96abe-118">Merhaba aşağıdaki örnek ile oluşturulan bir diski kullanan `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span><span class="sxs-lookup"><span data-stu-id="96abe-118">hello following example uses a disk created with `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span></span>

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

<span data-ttu-id="96abe-119">Merhaba çıktı hello aşağıdaki gibi görünüyor (Merhaba kullanabilirsiniz `-o table` seçeneği tooany komut tooformat hello çıktısında):</span><span class="sxs-lookup"><span data-stu-id="96abe-119">hello output looks something like hello following (you can use hello `-o table` option tooany command tooformat hello output in ):</span></span>

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


## <a name="attach-an-unmanaged-disk"></a><span data-ttu-id="96abe-120">Yönetilmeyen bir diski kullanıma açın</span><span class="sxs-lookup"><span data-stu-id="96abe-120">Attach an unmanaged disk</span></span>

<span data-ttu-id="96abe-121">Yeni bir disk ekleme hello bir disk oluşturma olmayacaksa hızlı aynı depolama hesabı, VM olarak.</span><span class="sxs-lookup"><span data-stu-id="96abe-121">Attaching a new disk is quick if you do not mind creating a disk in hello same storage account as your VM.</span></span> <span data-ttu-id="96abe-122">Tür `azure vm disk attach-new` toocreate ve VM için yeni bir GB disk ekleyin.</span><span class="sxs-lookup"><span data-stu-id="96abe-122">Type `azure vm disk attach-new` toocreate and attach a new GB disk for your VM.</span></span> <span data-ttu-id="96abe-123">Bir depolama hesabı açıkça belirtmeyen, oluşturduğunuz herhangi bir disk hello aynı yerleştirildiğinde, işletim sistemi diski bulunduğu depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="96abe-123">If you do not explicitly identify a storage account, any disk you create is placed in hello same storage account where your OS disk resides.</span></span> <span data-ttu-id="96abe-124">Örnek ekler Hello bir `50`GB disk toohello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="96abe-124">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a><span data-ttu-id="96abe-125">Linux VM toomount hello yeni disk toohello Bağlan</span><span class="sxs-lookup"><span data-stu-id="96abe-125">Connect toohello Linux VM toomount hello new disk</span></span>
> [!NOTE]
> <span data-ttu-id="96abe-126">Bu konuda tooa VM bağlanan kullanıcı adları ve parolaları kullanarak.</span><span class="sxs-lookup"><span data-stu-id="96abe-126">This topic connects tooa VM using usernames and passwords.</span></span> <span data-ttu-id="96abe-127">toouse ortak ve özel anahtar çiftlerini toocommunicate, VM ile bkz [nasıl tooUse Linux Azure üzerinde SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96abe-127">toouse public and private key pairs toocommunicate with your VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
> 
> 

<span data-ttu-id="96abe-128">TooSSH gerekir, Azure VM toopartition içine biçimlendirmek ve Linux VM kullanabilmesi için yeni diski bağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="96abe-128">You need tooSSH into your Azure VM toopartition, format, and mount your new disk so your Linux VM can use it.</span></span> <span data-ttu-id="96abe-129">Bağlayarak ile hakkında bilgi sahibi değilseniz **ssh**, hello komutu alır hello form `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`ve hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="96abe-129">If you're not familiar with connecting with **ssh**, hello command takes hello form `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`, and looks like hello following:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

<span data-ttu-id="96abe-130">Çıktı</span><span class="sxs-lookup"><span data-stu-id="96abe-130">Output</span></span>

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

<span data-ttu-id="96abe-131">Bağlandınız, şimdi tooyour VM, hazır tooattach bir disk.</span><span class="sxs-lookup"><span data-stu-id="96abe-131">Now that you're connected tooyour VM, you're ready tooattach a disk.</span></span>  <span data-ttu-id="96abe-132">İlk hello Bul kullanarak, disk `dmesg | grep SCSI` (Merhaba yöntemi kullandığınız yeni diskinizin değişebilir toodiscover).</span><span class="sxs-lookup"><span data-stu-id="96abe-132">First find hello disk, using `dmesg | grep SCSI` (hello method you use toodiscover your new disk may vary).</span></span> <span data-ttu-id="96abe-133">Bu durumda, onu şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="96abe-133">In this case, it looks something like:</span></span>

```bash
dmesg | grep SCSI
```

<span data-ttu-id="96abe-134">Çıktı</span><span class="sxs-lookup"><span data-stu-id="96abe-134">Output</span></span>

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

<span data-ttu-id="96abe-135">ve bu konuda hello durumda hello `sdc` hello istiyoruz bir disktir.</span><span class="sxs-lookup"><span data-stu-id="96abe-135">and in hello case of this topic, hello `sdc` disk is hello one that we want.</span></span> <span data-ttu-id="96abe-136">Şimdi bölüm hello diskle `sudo fdisk /dev/sdc` --disk, servis talebi hello olduğu varsayılarak `sdc`, birincil disk bölüm 1 yapın ve kabul diğer Varsayılanları hello.</span><span class="sxs-lookup"><span data-stu-id="96abe-136">Now partition hello disk with `sudo fdisk /dev/sdc` -- assuming that in your case hello disk was `sdc`, and make it a primary disk on partition 1, and accept hello other defaults.</span></span>

```bash
sudo fdisk /dev/sdc
```

<span data-ttu-id="96abe-137">Çıktı</span><span class="sxs-lookup"><span data-stu-id="96abe-137">Output</span></span>

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

<span data-ttu-id="96abe-138">Merhaba bölüm yazarak oluşturmak `p` hello isteminde:</span><span class="sxs-lookup"><span data-stu-id="96abe-138">Create hello partition by typing `p` at hello prompt:</span></span>

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

<span data-ttu-id="96abe-139">Ve hello kullanarak bir dosya sistemi toohello bölümü yazma **mkfs** dosya sistemi türü ve hello aygıt adı belirterek komutu.</span><span class="sxs-lookup"><span data-stu-id="96abe-139">And write a file system toohello partition by using hello **mkfs** command, specifying your filesystem type and hello device name.</span></span> <span data-ttu-id="96abe-140">Bu konuda, biz kullanmakta olduğunuz `ext4` ve `/dev/sdc1` üstten:</span><span class="sxs-lookup"><span data-stu-id="96abe-140">In this topic, we're using `ext4` and `/dev/sdc1` from above:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="96abe-141">Çıktı</span><span class="sxs-lookup"><span data-stu-id="96abe-141">Output</span></span>

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

<span data-ttu-id="96abe-142">Bir dizin toomount hello kullanarak dosya sistemini oluşturmak üzere, şimdi `mkdir`:</span><span class="sxs-lookup"><span data-stu-id="96abe-142">Now we create a directory toomount hello file system using `mkdir`:</span></span>

```bash
sudo mkdir /datadrive
```

<span data-ttu-id="96abe-143">Ve dizin hello kullanarak bağlayın `mount`:</span><span class="sxs-lookup"><span data-stu-id="96abe-143">And you mount hello directory using `mount`:</span></span>

```bash
sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="96abe-144">Merhaba veri diski olduğu şimdi hazır toouse olarak `/datadrive`.</span><span class="sxs-lookup"><span data-stu-id="96abe-144">hello data disk is now ready toouse as `/datadrive`.</span></span>

```bash
ls
```

<span data-ttu-id="96abe-145">Çıktı</span><span class="sxs-lookup"><span data-stu-id="96abe-145">Output</span></span>

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

<span data-ttu-id="96abe-146">olması gereken yeniden başlatma toohello /etc/fstab dosya ekleninceye sonra tooensure hello sürücü otomatik olarak yeniden.</span><span class="sxs-lookup"><span data-stu-id="96abe-146">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="96abe-147">Ayrıca, önerilir hello UUID (evrensel benzersiz tanıtıcı) / etc içinde kullanılan/fstab toorefer toohello sürücü yalnızca hello aygıt adı yerine (gibi `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="96abe-147">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="96abe-148">Merhaba işletim sistemi önyükleme sırasında disk hatası algılarsa, hello UUID kullanarak hello hatalı disk konumu verilen takılı tooa olan önler.</span><span class="sxs-lookup"><span data-stu-id="96abe-148">If hello OS detects a disk error during boot, using hello UUID avoids hello incorrect disk being mounted tooa given location.</span></span> <span data-ttu-id="96abe-149">Veri diskleri kalan sonra bu aynı aygıt kimlikleri atanması.</span><span class="sxs-lookup"><span data-stu-id="96abe-149">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="96abe-150">toofind hello yeni sürücü UUID Merhaba, hello kullan **blkid** yardımcı programı:</span><span class="sxs-lookup"><span data-stu-id="96abe-150">toofind hello UUID of hello new drive, use hello **blkid** utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="96abe-151">Merhaba çıkış benzer toohello aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="96abe-151">hello output looks similar toohello following:</span></span>

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> <span data-ttu-id="96abe-152">Yanlış hello düzenleme **/etc/fstab** dosya önyüklenemez bir sisteme neden.</span><span class="sxs-lookup"><span data-stu-id="96abe-152">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="96abe-153">Emin değilseniz, bu dosyayı tooproperly düzenleme nasıl bilgi toohello dağıtım'ın belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="96abe-153">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="96abe-154">Ayrıca, düzenlemeye başlamadan önce hello /etc/fstab dosyanızın bir yedeğini oluşturduğunuz önerilir.</span><span class="sxs-lookup"><span data-stu-id="96abe-154">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>
> 
> 

<span data-ttu-id="96abe-155">Ardından, hello'ı açmak **/etc/fstab** dosyasını bir metin düzenleyicisinde:</span><span class="sxs-lookup"><span data-stu-id="96abe-155">Next, open hello **/etc/fstab** file in a text editor:</span></span>

```bash
sudo vi /etc/fstab
```

<span data-ttu-id="96abe-156">Bu örnekte, hello UUID değeri Merhaba yeni kullanırız **/dev/sdc1** oluşturulduğu hello önceki adımları ve hello mountpoint aygıt **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="96abe-156">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="96abe-157">Satır toohello hello sonuna aşağıdaki hello eklemek **/etc/fstab** dosyası:</span><span class="sxs-lookup"><span data-stu-id="96abe-157">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> <span data-ttu-id="96abe-158">Daha sonra bir veri diski fstab düzenlemeden kaldırma hello VM toofail tooboot neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="96abe-158">Later removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="96abe-159">Çoğu dağıtımları ya da hello sağlamak `nofail` ve/veya `nobootwait` fstab seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="96abe-159">Most distributions provide either hello `nofail` and/or `nobootwait` fstab options.</span></span> <span data-ttu-id="96abe-160">Merhaba disk toomount önyükleme sırasında başarısız olsa bile bu seçenekler sistem tooboot izin verir.</span><span class="sxs-lookup"><span data-stu-id="96abe-160">These options allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="96abe-161">Bu parametreler hakkında daha fazla bilgi için dağıtım ait belgelere bakın.</span><span class="sxs-lookup"><span data-stu-id="96abe-161">Consult your distribution's documentation for more information on these parameters.</span></span>
> 
> <span data-ttu-id="96abe-162">Merhaba **nofail** seçeneği, VM başlatır hello dosya sistemi bozuk veya hello disk önyükleme sırasında yok olsa bile bu hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="96abe-162">hello **nofail** option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="96abe-163">Bu seçenek olmadan, davranış açıklandığı gibi karşılaşabilirsiniz [olamaz SSH tooLinux VM tooFSTAB hatalar nedeniyle](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span><span class="sxs-lookup"><span data-stu-id="96abe-163">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="96abe-164">KIRPMA/UNMAP Azure Linux desteği</span><span class="sxs-lookup"><span data-stu-id="96abe-164">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="96abe-165">Bazı Linux tekrar KIRPMA/UNMAP işlemleri toodiscard destek hello diskte kullanılmayan engeller.</span><span class="sxs-lookup"><span data-stu-id="96abe-165">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="96abe-166">Bu sayfa silinmiş Azure artık geçerli değil ve iptal edilecek standart depolama tooinform özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="96abe-166">This is primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="96abe-167">Büyük dosyaları oluşturmak ve bunları silerseniz bu maliyet tasarrufu sağlar.</span><span class="sxs-lookup"><span data-stu-id="96abe-167">This can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="96abe-168">Tooenable KIRPMA desteği, Linux VM'NİZDE iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="96abe-168">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="96abe-169">Her zamanki gibi dağıtımınız için önerilen yaklaşımı hello bakın:</span><span class="sxs-lookup"><span data-stu-id="96abe-169">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="96abe-170">Kullanım hello `discard` bağlama seçeneği `/etc/fstab`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="96abe-170">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* <span data-ttu-id="96abe-171">Bazı durumlarda hello içinde `discard` seçeneği performans etkileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="96abe-171">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="96abe-172">Alternatif olarak, hello çalıştırabilirsiniz `fstrim` komutunu el ile Merhaba komut satırından veya tooyour crontab toorun düzenli olarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="96abe-172">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="96abe-173">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="96abe-173">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="96abe-174">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="96abe-174">**RHEL/CentOS**</span></span>

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="96abe-175">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="96abe-175">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="96abe-176">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="96abe-176">Next Steps</span></span>
* <span data-ttu-id="96abe-177">Unutmayın, bu bilgileri tooyour yazma sürece bunu yeniden başlatılırsa, yeni disk kullanılabilir toohello VM olmadığını [fstab](http://en.wikipedia.org/wiki/Fstab) dosya.</span><span class="sxs-lookup"><span data-stu-id="96abe-177">Remember, that your new disk is not available toohello VM if it reboots unless you write that information tooyour [fstab](http://en.wikipedia.org/wiki/Fstab) file.</span></span>
* <span data-ttu-id="96abe-178">Linux VM tooensure yapılandırılmış doğru gözden geçirme hello [Linux makine performansı en iyi duruma](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) öneriler.</span><span class="sxs-lookup"><span data-stu-id="96abe-178">tooensure your Linux VM is configured correctly, review hello [Optimize your Linux machine performance](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommendations.</span></span>
* <span data-ttu-id="96abe-179">İlave diskler eklenerek, depolama kapasitesi ve [RAID yapılandırma](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ek performans.</span><span class="sxs-lookup"><span data-stu-id="96abe-179">Expand your storage capacity by adding additional disks and [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional performance.</span></span>

