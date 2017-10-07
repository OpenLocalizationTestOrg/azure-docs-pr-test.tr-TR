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
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a>Azure sanal makineleri için ağ verimliliğini en iyi duruma getirme

Azure sanal makineler (VM) daha fazla ağ verimliliği için iyileştirilmiş varsayılan ağ ayarları vardır. Bu makalede nasıl toooptimize ağ verimliliği Microsoft Azure Windows ve Linux VM'ler, Ubuntu ve CentOS Red Hat gibi büyük dağıtımlar dahil olmak üzere açıklanmaktadır.

## <a name="windows-vm"></a>Windows VM

Windows VM ile destekleniyorsa [hızlandırılmış ağ](virtual-network-create-vm-accelerated-networking.md), bu özelliğin etkinleştirilmesi verimliliği için en uygun yapılandırma hello olacaktır. Diğer tüm Windows VM'ler için Alma Tarafı Ölçeklendirmesi (RSS) kullanarak bir VM RSS olmadan daha yüksek düzeyde verimlilik ulaşabilir. Varsayılan olarak bir Windows VM RSS devre dışı olabilir. RSS etkin olup olmadığını adımları toodetermine aşağıdaki hello ve tooenable tamamlamak onu devre dışı ise.

1. Merhaba girin `Get-NetAdapterRss` RSS bir ağ bağdaştırıcısı için etkinse, PowerShell komut toosee. Hello örnek çıktı aşağıdaki hello döndürülen `Get-NetAdapterRss`, RSS etkin değil.

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. Komut tooenable RSS aşağıdaki hello girin:

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    Merhaba önceki komut çıktısı yok. Merhaba komutu geçici bağlantı kaybı yaklaşık bir dakika boyunca neden NIC ayarları değiştirildi. Merhaba bağlantı kaybı sırasında bir Reconnecting iletişim kutusu görüntülenir. Bağlantı genellikle hello üçüncü girişiminden sonra geri yüklendi.
3. RSS hello VM hello girerek etkinleştirildiğini onaylayın `Get-NetAdapterRss` yeniden komutu. Başarılı olursa, aşağıdaki örnek çıkış hello verilir:

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a>Linux VM

RSS, her zaman bir Azure Linux VM'de varsayılan olarak etkindir. Linux tekrar Ocak 2017 bu yana yayımlanan bir Linux VM tooachieve daha yüksek ağ verimliliği sağlayan yeni ağ en iyi duruma getirme seçenekleri içerir.

### <a name="ubuntu"></a>Ubuntu

Sipariş tooget hello iyileştirme ilk olduğu Haziran 2017'dan sonra en son desteklenen toohello sürüm güncelleştirin:
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
Merhaba Güncelleştirme tamamlandıktan sonra aşağıdaki komutları tooget hello son çekirdek hello girin:

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

İsteğe bağlı komut:

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a>Ubuntu Azure Önizleme çekirdek
> [!WARNING]
> Bu Azure Linux çekirdek olmayabilir Önizleme hello aynı düzeyde kullanılabilirlik ve güvenilirlik Market görüntülerini ve genel kullanılabilirlik sürümü olan çekirdekler olarak. Merhaba özelliği desteklenmiyor, yetenekleri kısıtlı ve hello varsayılan çekirdek olarak güvenilir olmayabilir. Bu çekirdek üretim iş yükleri için kullanmayın.

Önemli verimliliği performansından Azure Linux çekirdek önerilen hello yükleyerek elde edilebilir. tootry bu çekirdek bu satırı too/etc/apt/sources.list Ekle

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

Daha sonra bu komutları kök olarak çalıştırın.
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a>CentOS

Sipariş tooget hello iyileştirme ilk olan Temmuz 2017'dan sonra en son desteklenen toohello sürüm güncelleştirin:
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
Merhaba Güncelleştirme tamamlandıktan sonra yükleme son Linux Tümleştirme hizmetleri (LIS) hello.
Merhaba üretilen iş iyileştirme 4.2.2-2 başlayarak LIS kullanılıyor. Aşağıdaki komutları tooinstall LIS hello girin:

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a>Red Hat

Sipariş tooget hello iyileştirme ilk olan Temmuz 2017'dan sonra en son desteklenen toohello sürüm güncelleştirin:
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
Merhaba Güncelleştirme tamamlandıktan sonra yükleme son Linux Tümleştirme hizmetleri (LIS) hello.
4.2 başlayarak LIS Hello üretilen iş iyileştirme kullanılıyor. Aşağıdaki komutları toodownload hello girin ve LIS yükleyin:

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

Merhaba görüntüleyerek Hyper-V için Linux Tümleştirme hizmetleri sürüm 4.2 hakkında daha fazla bilgi [indirme sayfasının](https://www.microsoft.com/download/details.aspx?id=55106).

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba VM en iyi duruma getirilmiş, hello sonuçla bkz [bant genişliği/verimlilik Azure VM sınama](virtual-network-bandwidth-testing.md) senaryonuz için.
* Daha fazla bilgi edinin [Azure Virtual Network sık sorulan sorular (SSS)](virtual-networks-faq.md)
