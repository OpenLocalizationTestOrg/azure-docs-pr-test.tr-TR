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
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="eac99-103">Linux çalıştıran N-serisi Vm'lerinde NVIDIA GPU sürücüleri yükleyin</span><span class="sxs-lookup"><span data-stu-id="eac99-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="eac99-104">tootake yeteneklerinden hello GPU Azure N serisinin Linux çalıştıran sanal makineleri, yükleme desteklenen NVIDIA grafik sürücüleri.</span><span class="sxs-lookup"><span data-stu-id="eac99-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="eac99-105">N-serisi VM dağıttıktan sonra bu makalede sürücü kurulum adımlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="eac99-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="eac99-106">Sürücü Kurulum bilgileri de için kullanılabilir [Windows VM'ler](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eac99-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="eac99-107">N-serisi VM özellikleri, depolama kapasitesi ve disk Ayrıntılar için bkz: [GPU Linux VM boyutları](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eac99-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="eac99-108">NV VM'ler için kılavuz sürücüleri yükleyin</span><span class="sxs-lookup"><span data-stu-id="eac99-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="eac99-109">tooinstall NVIDIA kılavuz sürücüleri NV vm'lerinde bir SSH bağlantısı tooeach VM yapın ve Linux dağıtımınız için hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="eac99-109">tooinstall NVIDIA GRID drivers on NV VMs, make an SSH connection tooeach VM and follow hello steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="eac99-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="eac99-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="eac99-111">Merhaba çalıştırmak `lspci` komutu.</span><span class="sxs-lookup"><span data-stu-id="eac99-111">Run hello `lspci` command.</span></span> <span data-ttu-id="eac99-112">Hello NVIDIA M60 kartı veya kartları PCI cihaz olarak görünür olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="eac99-112">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="eac99-113">Güncelleştirmeleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="eac99-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="eac99-114">Merhaba NVIDIA sürücüsüyle uyumsuz hello Nouveau çekirdek sürücüsü devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="eac99-114">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="eac99-115">(Yalnızca NV Vm'lerinde hello NVIDIA sürücüsü kullanın.) toodo Bu, bir dosyada oluşturmak `/etc/modprobe.d `adlı `nouveau.conf` içeriği aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="eac99-115">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="eac99-116">Merhaba VM yeniden başlatın ve yeniden bağlayın.</span><span class="sxs-lookup"><span data-stu-id="eac99-116">Reboot hello VM and reconnect.</span></span> <span data-ttu-id="eac99-117">Çıkış X sunucusu:</span><span class="sxs-lookup"><span data-stu-id="eac99-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="eac99-118">Karşıdan yükleyip hello kılavuz sürücüsü:</span><span class="sxs-lookup"><span data-stu-id="eac99-118">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="eac99-119">Toorun hello NVIDIA xconfig yardımcı programı tooupdate X yapılandırma dosyanızı isteyip istemediğiniz sorulduğunda, seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="eac99-119">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="eac99-120">Yükleme tamamlandıktan sonra /etc/nvidia/gridd.conf.template tooa konum/etc/NVIDIA/en yeni dosya gridd.conf kopyalama</span><span class="sxs-lookup"><span data-stu-id="eac99-120">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="eac99-121">Çok Hello ekleyin`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="eac99-121">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="eac99-122">Merhaba VM yeniden başlatın ve tooverify hello yükleme devam edin.</span><span class="sxs-lookup"><span data-stu-id="eac99-122">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="eac99-123">CentOS tabanlı 7.3 veya Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="eac99-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="eac99-124">Merhaba çekirdek ve DKMS güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="eac99-124">Update hello kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="eac99-125">Merhaba NVIDIA sürücüsüyle uyumsuz hello Nouveau çekirdek sürücüsü devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="eac99-125">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="eac99-126">(Yalnızca NV Vm'lerinde hello NVIDIA sürücüsü kullanın.) toodo Bu, bir dosyada oluşturmak `/etc/modprobe.d `adlı `nouveau.conf` içeriği aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="eac99-126">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="eac99-127">Merhaba VM yeniden başlatma, yeniden bağlanma ve yükleme son Linux Tümleştirme hizmetleri Hyper-V: hello</span><span class="sxs-lookup"><span data-stu-id="eac99-127">Reboot hello VM, reconnect, and install hello latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="eac99-128">Toohello VM yeniden bağlanın ve hello çalıştırmak `lspci` komutu.</span><span class="sxs-lookup"><span data-stu-id="eac99-128">Reconnect toohello VM and run hello `lspci` command.</span></span> <span data-ttu-id="eac99-129">Hello NVIDIA M60 kartı veya kartları PCI cihaz olarak görünür olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="eac99-129">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="eac99-130">Karşıdan yükleyip hello kılavuz sürücüsü:</span><span class="sxs-lookup"><span data-stu-id="eac99-130">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="eac99-131">Toorun hello NVIDIA xconfig yardımcı programı tooupdate X yapılandırma dosyanızı isteyip istemediğiniz sorulduğunda, seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="eac99-131">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="eac99-132">Yükleme tamamlandıktan sonra /etc/nvidia/gridd.conf.template tooa konum/etc/NVIDIA/en yeni dosya gridd.conf kopyalama</span><span class="sxs-lookup"><span data-stu-id="eac99-132">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="eac99-133">Çok Hello ekleyin`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="eac99-133">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="eac99-134">Merhaba VM yeniden başlatın ve tooverify hello yükleme devam edin.</span><span class="sxs-lookup"><span data-stu-id="eac99-134">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="eac99-135">Sürücü yükleme doğrulayın</span><span class="sxs-lookup"><span data-stu-id="eac99-135">Verify driver installation</span></span>


<span data-ttu-id="eac99-136">tooquery hello GPU cihaz durumu, SSH toohello VM ve çalışma hello [NVIDIA SMI](https://developer.nvidia.com/nvidia-system-management-interface) komut satırı yardımcı programının hello sürücüsüyle yüklü.</span><span class="sxs-lookup"><span data-stu-id="eac99-136">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="eac99-137">Çıktı benzer toohello aşağıdaki görünür:</span><span class="sxs-lookup"><span data-stu-id="eac99-137">Output similar toohello following appears:</span></span>

![NVIDIA cihaz durumu](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="eac99-139">X11 sunucu</span><span class="sxs-lookup"><span data-stu-id="eac99-139">X11 server</span></span>
<span data-ttu-id="eac99-140">Bir X11 gerekiyorsa sunucu uzak bağlantıları tooan NV VM için [x11vnc](http://www.karlrunge.com/x11vnc/) donanım hızlandırmasını grafik izin verdiği için önerilir.</span><span class="sxs-lookup"><span data-stu-id="eac99-140">If you need an X11 server for remote connections tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="eac99-141">Merhaba BusID hello M60 aygıtının el ile eklenmesi gerekiyor toohello xconfig dosyası (`etc/X11/xorg.conf` Ubuntu 16.04 LTS üzerinde `/etc/X11/XF86config` CentOS 7.3 veya Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="eac99-141">hello BusID of hello M60 device must be manually added toohello xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="eac99-142">Ekleme bir `"Device"` bölümüne benzer toohello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="eac99-142">Add a `"Device"` section similar toohello following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="eac99-143">Ayrıca, güncelleştirme, `"Screen"` toouse bu cihaz bölüm.</span><span class="sxs-lookup"><span data-stu-id="eac99-143">Additionally, update your `"Screen"` section toouse this device.</span></span>
 
<span data-ttu-id="eac99-144">Merhaba BusID çalıştırarak bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="eac99-144">hello BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="eac99-145">bir VM bırakılan veya yeniden hello BusID değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eac99-145">hello BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="eac99-146">Bu nedenle, bir VM yeniden başlatıldığında toouse hello X11 yapılandırmasında bir komut dosyası tooupdate hello BusID isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eac99-146">Therefore, you may want toouse a script tooupdate hello BusID in hello X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="eac99-147">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="eac99-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="eac99-148">Bu dosya önyüklemede kök olarak içinde için bir giriş oluşturarak çağrılabilir `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="eac99-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="eac99-149">NC VM'ler için CUDA sürücüleri yükleyin</span><span class="sxs-lookup"><span data-stu-id="eac99-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="eac99-150">NVIDIA CUDA Araç Seti 8.0 hello Linux NC Vm'lerinde adımları tooinstall NVIDIA sürücülerini şunlardır.</span><span class="sxs-lookup"><span data-stu-id="eac99-150">Here are steps tooinstall NVIDIA drivers on Linux NC VMs from hello NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="eac99-151">C ve C++ geliştiriciler isteğe bağlı olarak hello tam Araç Seti toobuild GPU hızlandırılmış uygulamaları yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="eac99-151">C and C++ developers can optionally install hello full Toolkit toobuild GPU-accelerated applications.</span></span> <span data-ttu-id="eac99-152">Daha fazla bilgi için bkz: Merhaba [CUDA Yükleme Kılavuzu'na](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="eac99-152">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="eac99-153">CUDA sürücü yükleme bağlantıları burada geçerli yayın zamanında sağlanır.</span><span class="sxs-lookup"><span data-stu-id="eac99-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="eac99-154">Merhaba Hello son CUDA sürücüleri için ziyaret [NVIDIA](http://www.nvidia.com/) Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="eac99-154">For hello latest CUDA drivers, visit hello [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="eac99-155">tooinstall CUDA araç seti, bir SSH bağlantısı tooeach VM olun.</span><span class="sxs-lookup"><span data-stu-id="eac99-155">tooinstall CUDA Toolkit, make an SSH connection tooeach VM.</span></span> <span data-ttu-id="eac99-156">Sistem hello tooverify komutu aşağıdaki hello çalıştırmak bir CUDA özellikli GPU sahiptir:</span><span class="sxs-lookup"><span data-stu-id="eac99-156">tooverify that hello system has a CUDA-capable GPU, run hello following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="eac99-157">(Bir NVIDIA Tesla K80 kartı gösteren) örnek aşağıdaki çıktı benzer toohello görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="eac99-157">You will see output similar toohello following example (showing an NVIDIA Tesla K80 card):</span></span>

![lspci komut çıktısı](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="eac99-159">Sonra dağıtım için belirli çalışma yükleme komutları.</span><span class="sxs-lookup"><span data-stu-id="eac99-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="eac99-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="eac99-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="eac99-161">Merhaba CUDA sürücüleri yükleyip yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="eac99-161">Download and install hello CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="eac99-162">Merhaba yükleme birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="eac99-162">hello installation can take several minutes.</span></span>

2. <span data-ttu-id="eac99-163">toooptionally yükleme hello tam CUDA araç seti, türü:</span><span class="sxs-lookup"><span data-stu-id="eac99-163">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="eac99-164">Merhaba VM yeniden başlatın ve tooverify hello yükleme devam edin.</span><span class="sxs-lookup"><span data-stu-id="eac99-164">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="eac99-165">CentOS tabanlı 7.3 veya Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="eac99-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="eac99-166">Güncelleştirmeleri alın.</span><span class="sxs-lookup"><span data-stu-id="eac99-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="eac99-167">Toohello VM yeniden bağlanın ve yükleme hello son Linux Tümleştirme hizmetleri Hyper-V için.</span><span class="sxs-lookup"><span data-stu-id="eac99-167">Reconnect toohello VM and install hello latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="eac99-168">CentOS tabanlı HPC görüntü NC24r VM üzerinde yüklü değilse, tooStep 3 atlayın.</span><span class="sxs-lookup"><span data-stu-id="eac99-168">If you installed a CentOS-based HPC image on an NC24r VM, skip tooStep 3.</span></span> <span data-ttu-id="eac99-169">Merhaba görüntüde önceden Azure RDMA sürücüleri ve Linux Tümleştirme hizmetleri yüklü olmadığından LIS yükseltilmez ve çekirdek güncelleştirmeler varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="eac99-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in hello image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="eac99-170">Toohello VM yeniden bağlanın ve yükleme komutları aşağıdaki hello ile devam edin:</span><span class="sxs-lookup"><span data-stu-id="eac99-170">Reconnect toohello VM and continue installation with hello following commands:</span></span>

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

  <span data-ttu-id="eac99-171">Merhaba yükleme birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="eac99-171">hello installation can take several minutes.</span></span> 

4. <span data-ttu-id="eac99-172">toooptionally yükleme hello tam CUDA araç seti, türü:</span><span class="sxs-lookup"><span data-stu-id="eac99-172">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="eac99-173">Merhaba VM yeniden başlatın ve tooverify hello yükleme devam edin.</span><span class="sxs-lookup"><span data-stu-id="eac99-173">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="eac99-174">Sürücü yükleme doğrulayın</span><span class="sxs-lookup"><span data-stu-id="eac99-174">Verify driver installation</span></span>


<span data-ttu-id="eac99-175">tooquery hello GPU cihaz durumu, SSH toohello VM ve çalışma hello [NVIDIA SMI](https://developer.nvidia.com/nvidia-system-management-interface) komut satırı yardımcı programının hello sürücüsüyle yüklü.</span><span class="sxs-lookup"><span data-stu-id="eac99-175">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="eac99-176">Çıktı benzer toohello aşağıdaki görünür:</span><span class="sxs-lookup"><span data-stu-id="eac99-176">Output similar toohello following appears:</span></span>

![NVIDIA cihaz durumu](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="eac99-178">CUDA sürücü güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="eac99-178">CUDA driver updates</span></span>

<span data-ttu-id="eac99-179">CUDA sürücüleri düzenli aralıklarla dağıtımdan sonra güncelleştirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="eac99-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="eac99-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="eac99-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="eac99-181">CentOS tabanlı 7.3 veya Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="eac99-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="eac99-182">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="eac99-182">Troubleshooting</span></span>

* <span data-ttu-id="eac99-183">Merhaba 4.4.0-75 Linux çekirdek Ubuntu 16.04 LTS üzerinde çalışan Azure N-serisi Vm'leri CUDA sürücüleri bilinen bir sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="eac99-183">There is a known issue with CUDA drivers on Azure N-series VMs running hello 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="eac99-184">Çekirdek bir sürümden yükseltme yapıyorsanız, tooat yükseltme en az çekirdek sürüm 4.4.0-77.</span><span class="sxs-lookup"><span data-stu-id="eac99-184">If you are upgrading from an earlier kernel version, upgrade tooat least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="eac99-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eac99-185">Next steps</span></span>

* <span data-ttu-id="eac99-186">Merhaba N-serisi VM'ler hello NVIDIA GPU hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="eac99-186">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="eac99-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (için Azure NC VM'ler)</span><span class="sxs-lookup"><span data-stu-id="eac99-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="eac99-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (için Azure NV VM'ler)</span><span class="sxs-lookup"><span data-stu-id="eac99-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="eac99-189">toocapture yüklü NVIDIA sürücülerinizi içeren bir Linux VM görüntüsüne bkz [nasıl toogeneralize ve Linux sanal makine yakalama](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eac99-189">toocapture a Linux VM image with your installed NVIDIA drivers, see [How toogeneralize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
