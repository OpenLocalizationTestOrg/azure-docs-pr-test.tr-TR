---
title: "aaaOptimize VM ağ verimliliği | Microsoft Docs"
description: "Nasıl toooptimize Azure sanal makine ağ verimliliği öğrenin."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="4ce0b-103">Azure sanal makineleri için ağ verimliliğini en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="4ce0b-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="4ce0b-104">Azure sanal makineler (VM) daha fazla ağ verimliliği için iyileştirilmiş varsayılan ağ ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="4ce0b-105">Bu makalede nasıl toooptimize ağ verimliliği Microsoft Azure Windows ve Linux VM'ler, Ubuntu ve CentOS Red Hat gibi büyük dağıtımlar dahil olmak üzere açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-105">This article describes how toooptimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="4ce0b-106">Windows VM</span><span class="sxs-lookup"><span data-stu-id="4ce0b-106">Windows VM</span></span>

<span data-ttu-id="4ce0b-107">Windows VM ile destekleniyorsa [hızlandırılmış ağ](virtual-network-create-vm-accelerated-networking.md), bu özelliğin etkinleştirilmesi verimliliği için en uygun yapılandırma hello olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be hello optimal configuration for throughput.</span></span> <span data-ttu-id="4ce0b-108">Diğer tüm Windows VM'ler için Alma Tarafı Ölçeklendirmesi (RSS) kullanarak bir VM RSS olmadan daha yüksek düzeyde verimlilik ulaşabilir.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="4ce0b-109">Varsayılan olarak bir Windows VM RSS devre dışı olabilir.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="4ce0b-110">RSS etkin olup olmadığını adımları toodetermine aşağıdaki hello ve tooenable tamamlamak onu devre dışı ise.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-110">Complete hello following steps toodetermine whether RSS is enabled and tooenable it if it's disabled.</span></span>

1. <span data-ttu-id="4ce0b-111">Merhaba girin `Get-NetAdapterRss` RSS bir ağ bağdaştırıcısı için etkinse, PowerShell komut toosee.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-111">Enter hello `Get-NetAdapterRss` PowerShell command toosee if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="4ce0b-112">Hello örnek çıktı aşağıdaki hello döndürülen `Get-NetAdapterRss`, RSS etkin değil.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-112">In hello following example output returned from hello `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="4ce0b-113">Komut tooenable RSS aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="4ce0b-113">Enter hello following command tooenable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="4ce0b-114">Merhaba önceki komut çıktısı yok.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-114">hello previous command does not have an output.</span></span> <span data-ttu-id="4ce0b-115">Merhaba komutu geçici bağlantı kaybı yaklaşık bir dakika boyunca neden NIC ayarları değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-115">hello command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="4ce0b-116">Merhaba bağlantı kaybı sırasında bir Reconnecting iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-116">A Reconnecting dialog box appears during hello connectivity loss.</span></span> <span data-ttu-id="4ce0b-117">Bağlantı genellikle hello üçüncü girişiminden sonra geri yüklendi.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-117">Connectivity is typically restored after hello third attempt.</span></span>
3. <span data-ttu-id="4ce0b-118">RSS hello VM hello girerek etkinleştirildiğini onaylayın `Get-NetAdapterRss` yeniden komutu.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-118">Confirm that RSS is enabled in hello VM by entering hello `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="4ce0b-119">Başarılı olursa, aşağıdaki örnek çıkış hello verilir:</span><span class="sxs-lookup"><span data-stu-id="4ce0b-119">If successful, hello following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="4ce0b-120">Linux VM</span><span class="sxs-lookup"><span data-stu-id="4ce0b-120">Linux VM</span></span>

<span data-ttu-id="4ce0b-121">RSS, her zaman bir Azure Linux VM'de varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="4ce0b-122">Linux tekrar Ocak 2017 bu yana yayımlanan bir Linux VM tooachieve daha yüksek ağ verimliliği sağlayan yeni ağ en iyi duruma getirme seçenekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM tooachieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="4ce0b-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4ce0b-123">Ubuntu</span></span>

<span data-ttu-id="4ce0b-124">Sipariş tooget hello iyileştirme ilk olduğu Haziran 2017'dan sonra en son desteklenen toohello sürüm güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="4ce0b-124">In order tooget hello optimization, first update toohello latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="4ce0b-125">Merhaba Güncelleştirme tamamlandıktan sonra aşağıdaki komutları tooget hello son çekirdek hello girin:</span><span class="sxs-lookup"><span data-stu-id="4ce0b-125">After hello update is complete, enter hello following commands tooget hello latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="4ce0b-126">İsteğe bağlı komut:</span><span class="sxs-lookup"><span data-stu-id="4ce0b-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="4ce0b-127">Ubuntu Azure Önizleme çekirdek</span><span class="sxs-lookup"><span data-stu-id="4ce0b-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="4ce0b-128">Bu Azure Linux çekirdek olmayabilir Önizleme hello aynı düzeyde kullanılabilirlik ve güvenilirlik Market görüntülerini ve genel kullanılabilirlik sürümü olan çekirdekler olarak.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-128">This Azure Linux Preview kernel may not have hello same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="4ce0b-129">Merhaba özelliği desteklenmiyor, yetenekleri kısıtlı ve hello varsayılan çekirdek olarak güvenilir olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-129">hello feature is not supported, may have constrained capabilities, and may not be as reliable as hello default kernel.</span></span> <span data-ttu-id="4ce0b-130">Bu çekirdek üretim iş yükleri için kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="4ce0b-131">Önemli verimliliği performansından Azure Linux çekirdek önerilen hello yükleyerek elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-131">Significant throughput performance can be achieved by installing hello proposed Azure Linux kernel.</span></span> <span data-ttu-id="4ce0b-132">tootry bu çekirdek bu satırı too/etc/apt/sources.list Ekle</span><span class="sxs-lookup"><span data-stu-id="4ce0b-132">tootry this kernel, add this line too/etc/apt/sources.list</span></span>

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="4ce0b-133">Daha sonra bu komutları kök olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="4ce0b-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="4ce0b-134">CentOS</span></span>

<span data-ttu-id="4ce0b-135">Sipariş tooget hello iyileştirme ilk olan Temmuz 2017'dan sonra en son desteklenen toohello sürüm güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="4ce0b-135">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="4ce0b-136">Merhaba Güncelleştirme tamamlandıktan sonra yükleme son Linux Tümleştirme hizmetleri (LIS) hello.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-136">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="4ce0b-137">Merhaba üretilen iş iyileştirme 4.2.2-2 başlayarak LIS kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-137">hello throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="4ce0b-138">Aşağıdaki komutları tooinstall LIS hello girin:</span><span class="sxs-lookup"><span data-stu-id="4ce0b-138">Enter hello following commands tooinstall LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="4ce0b-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="4ce0b-139">Red Hat</span></span>

<span data-ttu-id="4ce0b-140">Sipariş tooget hello iyileştirme ilk olan Temmuz 2017'dan sonra en son desteklenen toohello sürüm güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="4ce0b-140">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="4ce0b-141">Merhaba Güncelleştirme tamamlandıktan sonra yükleme son Linux Tümleştirme hizmetleri (LIS) hello.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-141">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="4ce0b-142">4.2 başlayarak LIS Hello üretilen iş iyileştirme kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-142">hello throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="4ce0b-143">Aşağıdaki komutları toodownload hello girin ve LIS yükleyin:</span><span class="sxs-lookup"><span data-stu-id="4ce0b-143">Enter hello following commands toodownload and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="4ce0b-144">Merhaba görüntüleyerek Hyper-V için Linux Tümleştirme hizmetleri sürüm 4.2 hakkında daha fazla bilgi [indirme sayfasının](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="4ce0b-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing hello [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ce0b-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4ce0b-145">Next steps</span></span>
* <span data-ttu-id="4ce0b-146">Merhaba VM en iyi duruma getirilmiş, hello sonuçla bkz [bant genişliği/verimlilik Azure VM sınama](virtual-network-bandwidth-testing.md) senaryonuz için.</span><span class="sxs-lookup"><span data-stu-id="4ce0b-146">Now that hello VM is optimized, see hello result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="4ce0b-147">Daha fazla bilgi edinin [Azure Virtual Network sık sorulan sorular (SSS)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="4ce0b-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
