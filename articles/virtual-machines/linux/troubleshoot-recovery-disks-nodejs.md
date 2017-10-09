---
title: bir Linux VM hello Azure CLI 1.0 ile sorun giderme aaaUse | Microsoft Docs
description: "Nasıl bağlanan hello işletim sistemi diski tooa kurtarma VM kullanarak Linux VM sorunları tootroubleshoot hello Azure CLI 1.0 öğrenin"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a>Bir Linux VM hello işletim sistemi disk tooa kurtarma VM ekleyerek sorun giderme kullanarak hello Azure CLI 1.0
Linux sanal makine (VM) önyükleme veya disk bir hatayla karşılaştığında, sorun giderme adımları hello sanal sabit diske kendisini tooperform gerekebilir. Geçersiz bir giriş yaygın bir örnek olacaktır `/etc/fstab` engelleyen hello VM mümkün tooboot başarıyla bırakılıyor. Bu makale ayrıntıları toouse hello nasıl Azure CLI 1.0 tooconnect, sanal sabit hataları tooanother Linux VM toofix disk sonra özgün VM'yi yeniden oluşturun.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#recovery-process-overview) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için


## <a name="recovery-process-overview"></a>Kurtarma işlemine genel bakış
sorun giderme işlemi hello aşağıdaki gibidir:

1. Merhaba sanal sabit diskleri tutmak hello VM karşılaşmadan sorunları, silin.
2. Ekleme ve sorun giderme amacıyla hello sanal sabit disk tooanother Linux VM bağlayın.
3. VM sorun giderme toohello bağlayın. Dosyaları düzenleyin veya herhangi bir aracı toofix sorunları hello özgün sanal sabit disk üzerinde çalıştırın.
4. Çıkarın ve VM sorun giderme hello hello sanal sabit diski kullanımdan çıkarın.
5. Merhaba özgün sanal sabit disk kullanan bir VM oluşturun.

Bilgisayarınızda yüklü olduğundan emin olun [en son Azure CLI 1.0 hello](../../cli-install-nodejs.md) yüklü ve oturum açmış ve Resource Manager modunu kullanma:

```azurecli
azure config mode arm
```

Hello aşağıdaki örneklerde, parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında `myResourceGroup`, `mystorageaccount`, ve `myVM`.


## <a name="determine-boot-issues"></a>Önyükleme sorunlarını belirleme
Merhaba seri çıkış toodetermine neden VM mümkün tooboot doğru değil inceleyin. Yaygın bir örnek, geçersiz bir giriş olduğunu `/etc/fstab`, veya sanal sabit diski olan silindiğini veya taşındığını temel hello.

Merhaba aşağıdaki örnek hello seri çıkış adlı VM hello alır `myVM` adlı hello kaynak grubunda `myResourceGroup`:

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

Merhaba seri çıkış toodetermine neden hello VM tooboot başarısız oluyor gözden geçirin. Merhaba seri çıkış herhangi bir gösterge sağlayan değil, tooreview günlük dosyalarında gerekebilir `/var/log` hello sanal olduktan sonra sabit disk VM sorun giderme tooa bağlı.


## <a name="view-existing-virtual-hard-disk-details"></a>Var olan sanal sabit disk ayrıntılarını görüntüleyin
Sanal sabit disk tooanother VM ekleyebilmek için tooidentify hello adı hello sanal sabit disk (VHD) gerekir. 

Merhaba aşağıdaki örnek alır bilgi hello adlı VM için `myVM` adlı hello kaynak grubunda `myResourceGroup`:

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

Ara `Vhd URI` komutu önceki hello hello çıktısını içinde. Merhaba aşağıdaki kesilmiş örnek çıkış gösterir hello `Vhd URI` hello son satırında:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a>Var olan VM silme
Sanal sabit diskler ve sanal makineler Azure'da iki ayrı kaynaktır. Bir sanal sabit disk hello işletim sisteminin kendisi, uygulamalar ve yapılandırmalar depolandığı ' dir. Merhaba VM kendisini hello boyutunu veya konumunu tanımlar ve bir sanal sabit disk veya sanal ağ arabirim kartı (NIC) gibi kaynakları başvuran meta verilerdir. Her sanal sabit diske bağlı olduğunda atanmış bir kira sahip tooa VM. Veri diskleri bağlı ve hatta hello VM çalışırken ayrılmış olsa da, hello VM kaynak silinmedikçe hello işletim sistemi diski ayrılamıyor. Bu VM durduruldu ve deallocated durumda olduğunda bile hello kira tooassociate hello işletim sistemi diski bir VM ile devam eder.

İlk adım toorecover hello VM toodelete hello VM kendisini kaynaktır. Silme hello VM hello sanal sabit diskleri depolama hesabınızdaki bırakır. Merhaba, VM silinmiş sonra hello sanal sabit disk tooanother VM tootroubleshoot ekleme ve hello hataları çözümleyin.

Aşağıdaki örnek siler hello hello adlı VM `myVM` adlı hello kaynak grubundan `myResourceGroup`:

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

Merhaba VM hello sanal sabit disk tooanother VM eklemeden önce silme tamamlanana kadar bekleyin. Merhaba kira hello sanal sabit diskte hello VM ile ilişkilendiren hello sanal sabit disk tooanother VM iliştirebilirsiniz önce yayınlanan toobe gerekir.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Var olan sanal sabit disk tooanother VM ekleme
Sonraki birkaç adımda için Merhaba, sorun giderme amacıyla başka bir VM kullanın. VM toobrowse sorun giderme hello varolan sanal sabit disk toothis ekleme ve hello diskin içeriği düzenleyin. Bu işlem toocorrect sağlar herhangi bir yapılandırma hataları veya gözden geçirme ek uygulama veya sistem günlük dosyaları, örneğin. Seçin veya sorun giderme amacıyla başka bir VM toouse oluşturun.

Merhaba varolan bir sanal sabit diski taktığınızda hello URL toohello disk hello önceki elde belirtin `azure vm show` komutu. Merhaba aşağıdaki örnek iliştirir adlı VM sorun giderme var olan bir sanal sabit disk toohello `myVMRecovery` adlı hello kaynak grubunda `myResourceGroup`:

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a>Merhaba bağlı veri diski bağlama

> [!NOTE]
> Merhaba Aşağıdaki örnekler bir Ubuntu VM gerekli hello adımları ayrıntılı olarak açıklanmaktadır. Red Hat Enterprise Linux veya SUSE, gibi farklı Linux distro kullanıyorsanız hello günlük dosyası konumları ve `mount` komutları biraz farklı olabilir. Belirli distro hello uygun değişiklikleri komutları için toohello belgelerine başvurun.

1. SSH tooyour VM Hello uygun kimlik bilgilerini kullanarak sorun giderme. Bu disk VM sorun giderme hello ilk veri bağlı disk tooyour ise, hello disk büyük olasılıkla çok bağlı`/dev/sdc`. Kullanım `dmseg` tooview bağlı diskler:

    ```bash
    dmesg | grep SCSI
    ```

    Merhaba, benzer toohello aşağıdaki örneğine çıktı:

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    Örnek önceki hello hello işletim sistemi disk altındadır `/dev/sda` ve hello geçici disk, her VM için belirtilen `/dev/sdb`. Birden fazla veri diski varsa, bunlar adresindeki olmalıdır `/dev/sdd`, `/dev/sde`ve benzeri.

2. Bir dizin toomount, varolan bir sanal sabit diski oluşturun. Merhaba aşağıdaki örnek adlı bir dizin oluşturur `troubleshootingdisk`:

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. Var olan sanal sabit diskin birden çok bölüm varsa, gerekli hello bölüm bağlayın. Merhaba aşağıdaki örnek bağlar hello ilk birincil bölüm adresindeki `/dev/sdc1`:

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > Evrensel benzersiz tanımlayıcı (UUID) hello sanal sabit disk kullanarak Azure'daki sanal makineleri üzerinde toomount veri diskleri hello en iyi uygulamadır. Bu kısa sorun giderme senaryosu için bağlama hello sanal sabit disk hello UUID kullanarak gerekli değildir. Bununla birlikte, normal kullanım altında düzenleme `/etc/fstab` toomount sanal sabit diskleri yerine UUID neden olabilir, aygıt adı kullanılarak hello VM toofail tooboot.


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Özgün sanal sabit diskinde ilgili sorunları giderme
Merhaba varolan bir sanal sabit takılı diski ile tüm bakım ve sorun giderme adımları gereken şekilde artık gerçekleştirebilirsiniz. Merhaba sorunlar ele sonra aşağıdaki adımları hello ile devam edin.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Çıkarın ve özgün sanal sabit disk ayırma
Hatalarınızı çözüldükten sonra çıkarın ve sorun giderme VM'den hello varolan sanal sabit disk ayırma. VM sorun giderme hello sanal sabit disk toohello ekleme hello kira serbest kadar herhangi bir VM ile sanal sabit disk kullanamazsınız.

1. SSH oturumu tooyour VM sorun giderme hello hello varolan bir sanal sabit diski çıkarın. Merhaba ana dizin, bağlama noktası için dışında ilk değiştirin:

    ```bash
    cd /
    ```

    Şimdi hello varolan bir sanal sabit diski çıkarın. Merhaba aşağıdaki örnek çıkarır hello aygıt `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Şimdi hello VM hello sanal sabit diski kullanımdan çıkarın. VM sorun giderme hello SSH oturumu tooyour çıkın. Hello Azure CLI'da, ilk liste hello VM sorun giderme veri diskleri tooyour bağlı. Merhaba listeleri hello veri diskleri aşağıdaki örnek bağlı toohello adlı VM `myVMRecovery` adlı hello kaynak grubunda `myResourceGroup`:

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    Not hello `Lun` , varolan bir sanal sabit disk için değer. Merhaba aşağıdaki örnek komut çıktısı hello varolan sanal diski LUN 0 ekli gösterilmektedir:

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    Geçerli hello kullanarak VM Hello veri diski kullanımdan çıkarın `Lun` değeri:

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a>Özgün sabit diskten VM oluşturma
bir VM, özgün sanal sabit diskten toocreate kullanmak [bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). Merhaba gerçek JSON şablon bağlantıyı izleyerek hello şöyledir:

- https://RAW.githubusercontent.com/Azure/Azure-QuickStart-Templates/master/201-VM-Specialized-VHD/azuredeploy.JSON

Merhaba şablon hello VHD URL'si hello gelen kullanarak mevcut sanal ağda, bir VM dağıtır önceki komutu. Merhaba aşağıdaki örnek dağıtır hello şablon toohello kaynak grubu adında `myResourceGroup`:

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

Yanıt hello ister VM adı gibi hello şablonunun (`myDeployedVM` hello örnek), işletim sistemi türü (`Linux`) ve VM boyutu (`Standard_DS1_v2`). Merhaba `osDiskVhdUri` olduğundan, hello aynı VM sorun giderme hello varolan sanal sabit disk toohello eklerken daha önce kullanılan. Merhaba komutu çıktısı ve istemleri örneği aşağıdaki gibidir:

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a>Önyükleme tanılaması yeniden etkinleştirin

Merhaba varolan sanal sabit diskten VM'nizi oluşturduğunuzda, önyükleme tanılaması otomatik olarak etkinleştirilmemiş olabilir. Merhaba aşağıdaki örnek hello tanılama uzantısını hello adlı VM üzerinde etkinleştirir `myDeployedVM` adlı hello kaynak grubunda `myResourceGroup`:

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Sonraki adımlar
Tooyour VM bağlantı sorunları yaşıyorsanız, bkz: [sorun giderme SSH bağlantıları tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). VM üzerinde çalışan uygulamalara erişim sorunları için bkz: [bir Linux VM üzerinde uygulama bağlantı sorunlarını giderme](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
