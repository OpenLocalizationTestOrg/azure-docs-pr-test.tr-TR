---
title: "Linux için aaaAzure N-serisi sürücü kurulumu | Microsoft Docs"
description: "Nasıl tooset NVIDIA GPU sürücüleri Linux Azure'da çalışan N-serisi VM'ler için ayarlama"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d91695d0-64b9-4e6b-84bd-18401eaecdde
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7db1b3859f9075c6d9f0319f39418946ea08743f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a>Linux çalıştıran N-serisi Vm'lerinde NVIDIA GPU sürücüleri yükleyin

tootake yeteneklerinden hello GPU Azure N serisinin Linux çalıştıran sanal makineleri, yükleme desteklenen NVIDIA grafik sürücüleri. N-serisi VM dağıttıktan sonra bu makalede sürücü kurulum adımlarını sağlar. Sürücü Kurulum bilgileri de için kullanılabilir [Windows VM'ler](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


N-serisi VM özellikleri, depolama kapasitesi ve disk Ayrıntılar için bkz: [GPU Linux VM boyutları](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a>NV VM'ler için kılavuz sürücüleri yükleyin

tooinstall NVIDIA kılavuz sürücüleri NV vm'lerinde bir SSH bağlantısı tooeach VM yapın ve Linux dağıtımınız için hello adımları izleyin. 

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Merhaba çalıştırmak `lspci` komutu. Hello NVIDIA M60 kartı veya kartları PCI cihaz olarak görünür olduğunu doğrulayın.

2. Güncelleştirmeleri yükleyin.

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. Merhaba NVIDIA sürücüsüyle uyumsuz hello Nouveau çekirdek sürücüsü devre dışı bırakın. (Yalnızca NV Vm'lerinde hello NVIDIA sürücüsü kullanın.) toodo Bu, bir dosyada oluşturmak `/etc/modprobe.d `adlı `nouveau.conf` içeriği aşağıdaki hello ile:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. Merhaba VM yeniden başlatın ve yeniden bağlayın. Çıkış X sunucusu:

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. Karşıdan yükleyip hello kılavuz sürücüsü:

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. Toorun hello NVIDIA xconfig yardımcı programı tooupdate X yapılandırma dosyanızı isteyip istemediğiniz sorulduğunda, seçin **Evet**.

7. Yükleme tamamlandıktan sonra /etc/nvidia/gridd.conf.template tooa konum/etc/NVIDIA/en yeni dosya gridd.conf kopyalama

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. Çok Hello ekleyin`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Merhaba VM yeniden başlatın ve tooverify hello yükleme devam edin.


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>CentOS tabanlı 7.3 veya Red Hat Enterprise Linux 7.3


1. Merhaba çekirdek ve DKMS güncelleştirin.
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. Merhaba NVIDIA sürücüsüyle uyumsuz hello Nouveau çekirdek sürücüsü devre dışı bırakın. (Yalnızca NV Vm'lerinde hello NVIDIA sürücüsü kullanın.) toodo Bu, bir dosyada oluşturmak `/etc/modprobe.d `adlı `nouveau.conf` içeriği aşağıdaki hello ile:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. Merhaba VM yeniden başlatma, yeniden bağlanma ve yükleme son Linux Tümleştirme hizmetleri Hyper-V: hello
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. Toohello VM yeniden bağlanın ve hello çalıştırmak `lspci` komutu. Hello NVIDIA M60 kartı veya kartları PCI cihaz olarak görünür olduğunu doğrulayın.
 
5. Karşıdan yükleyip hello kılavuz sürücüsü:

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. Toorun hello NVIDIA xconfig yardımcı programı tooupdate X yapılandırma dosyanızı isteyip istemediğiniz sorulduğunda, seçin **Evet**.

7. Yükleme tamamlandıktan sonra /etc/nvidia/gridd.conf.template tooa konum/etc/NVIDIA/en yeni dosya gridd.conf kopyalama
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. Çok Hello ekleyin`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Merhaba VM yeniden başlatın ve tooverify hello yükleme devam edin.

### <a name="verify-driver-installation"></a>Sürücü yükleme doğrulayın


tooquery hello GPU cihaz durumu, SSH toohello VM ve çalışma hello [NVIDIA SMI](https://developer.nvidia.com/nvidia-system-management-interface) komut satırı yardımcı programının hello sürücüsüyle yüklü. 

Çıktı benzer toohello aşağıdaki görünür:

![NVIDIA cihaz durumu](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a>X11 sunucu
Bir X11 gerekiyorsa sunucu uzak bağlantıları tooan NV VM için [x11vnc](http://www.karlrunge.com/x11vnc/) donanım hızlandırmasını grafik izin verdiği için önerilir. Merhaba BusID hello M60 aygıtının el ile eklenmesi gerekiyor toohello xconfig dosyası (`etc/X11/xorg.conf` Ubuntu 16.04 LTS üzerinde `/etc/X11/XF86config` CentOS 7.3 veya Red Hat Enterprise Server 7.3). Ekleme bir `"Device"` bölümüne benzer toohello aşağıdaki:
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
Ayrıca, güncelleştirme, `"Screen"` toouse bu cihaz bölüm.
 
Merhaba BusID çalıştırarak bulunabilir.

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
bir VM bırakılan veya yeniden hello BusID değiştirebilirsiniz. Bu nedenle, bir VM yeniden başlatıldığında toouse hello X11 yapılandırmasında bir komut dosyası tooupdate hello BusID isteyebilirsiniz. Örneğin:

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

Bu dosya önyüklemede kök olarak içinde için bir giriş oluşturarak çağrılabilir `/etc/rc.d/rc3.d`.


## <a name="install-cuda-drivers-for-nc-vms"></a>NC VM'ler için CUDA sürücüleri yükleyin

NVIDIA CUDA Araç Seti 8.0 hello Linux NC Vm'lerinde adımları tooinstall NVIDIA sürücülerini şunlardır. 

C ve C++ geliştiriciler isteğe bağlı olarak hello tam Araç Seti toobuild GPU hızlandırılmış uygulamaları yükleyebilir. Daha fazla bilgi için bkz: Merhaba [CUDA Yükleme Kılavuzu'na](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).


> [!NOTE]
> CUDA sürücü yükleme bağlantıları burada geçerli yayın zamanında sağlanır. Merhaba Hello son CUDA sürücüleri için ziyaret [NVIDIA](http://www.nvidia.com/) Web sitesi.
>

tooinstall CUDA araç seti, bir SSH bağlantısı tooeach VM olun. Sistem hello tooverify komutu aşağıdaki hello çalıştırmak bir CUDA özellikli GPU sahiptir:

```bash
lspci | grep -i NVIDIA
```
(Bir NVIDIA Tesla K80 kartı gösteren) örnek aşağıdaki çıktı benzer toohello görürsünüz:

![lspci komut çıktısı](./media/n-series-driver-setup/lspci.png)

Sonra dağıtım için belirli çalışma yükleme komutları.

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Merhaba CUDA sürücüleri yükleyip yeniden açın.
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  Merhaba yükleme birkaç dakika sürebilir.

2. toooptionally yükleme hello tam CUDA araç seti, türü:

  ```bash
  sudo apt-get install cuda
  ```

3. Merhaba VM yeniden başlatın ve tooverify hello yükleme devam edin.

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>CentOS tabanlı 7.3 veya Red Hat Enterprise Linux 7.3

1. Güncelleştirmeleri alın. 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. Toohello VM yeniden bağlanın ve yükleme hello son Linux Tümleştirme hizmetleri Hyper-V için.

  > [!IMPORTANT]
  > CentOS tabanlı HPC görüntü NC24r VM üzerinde yüklü değilse, tooStep 3 atlayın. Merhaba görüntüde önceden Azure RDMA sürücüleri ve Linux Tümleştirme hizmetleri yüklü olmadığından LIS yükseltilmez ve çekirdek güncelleştirmeler varsayılan olarak devre dışıdır.
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. Toohello VM yeniden bağlanın ve yükleme komutları aşağıdaki hello ile devam edin:

  ```bash
  sudo yum install kernel-devel

  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

  sudo yum install dkms

  CUDA_REPO_PKG=cuda-repo-rhel7-8.0.61-1.x86_64.rpm

  wget http://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/${CUDA_REPO_PKG} -O /tmp/${CUDA_REPO_PKG}

  sudo rpm -ivh /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo yum install cuda-drivers
  ```

  Merhaba yükleme birkaç dakika sürebilir. 

4. toooptionally yükleme hello tam CUDA araç seti, türü:

  ```bash
  sudo yum install cuda
  ```

5. Merhaba VM yeniden başlatın ve tooverify hello yükleme devam edin.


### <a name="verify-driver-installation"></a>Sürücü yükleme doğrulayın


tooquery hello GPU cihaz durumu, SSH toohello VM ve çalışma hello [NVIDIA SMI](https://developer.nvidia.com/nvidia-system-management-interface) komut satırı yardımcı programının hello sürücüsüyle yüklü. 

Çıktı benzer toohello aşağıdaki görünür:

![NVIDIA cihaz durumu](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a>CUDA sürücü güncelleştirmesi

CUDA sürücüleri düzenli aralıklarla dağıtımdan sonra güncelleştirmenizi öneririz.

#### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>CentOS tabanlı 7.3 veya Red Hat Enterprise Linux 7.3

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a>Sorun giderme

* Merhaba 4.4.0-75 Linux çekirdek Ubuntu 16.04 LTS üzerinde çalışan Azure N-serisi Vm'leri CUDA sürücüleri bilinen bir sorun yoktur. Çekirdek bir sürümden yükseltme yapıyorsanız, tooat yükseltme en az çekirdek sürüm 4.4.0-77. 



## <a name="next-steps"></a>Sonraki adımlar

* Merhaba N-serisi VM'ler hello NVIDIA GPU hakkında daha fazla bilgi için bkz:
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (için Azure NC VM'ler)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (için Azure NV VM'ler)

* toocapture yüklü NVIDIA sürücülerinizi içeren bir Linux VM görüntüsüne bkz [nasıl toogeneralize ve Linux sanal makine yakalama](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
