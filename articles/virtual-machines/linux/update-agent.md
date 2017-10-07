---
title: "aaaUpdate hello Azure Linux Aracısı github'dan | Microsoft Docs"
description: "Bilgi nasıl tooupdate github'dan Azure toohello en son sürümünde, Linux VM için Azure Linux Aracısı"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a>Nasıl tooupdate hello Azure Linux Aracısı'nı bir VM

tooupdate, [Azure Linux Aracısı](https://github.com/Azure/WALinuxAgent) azure'da bir Linux VM üzerinde önceden olmanız gerekir:

- Azure'da çalışan bir Linux VM.
- Bağlantı toothat Linux VM SSH kullanarak.

Her zaman hello Linux distro deposundaki bir paket için ilk denetlemelisiniz. Mümkünse kullanılabilir hello paketi hello en son sürümünü değil olabilir, ancak, Otomatik Güncelleştirme'yi etkinleştirme hello Linux Aracısı her zaman hello en son güncelleştirmeyi alın garanti eder. Merhaba paket yöneticileri yüklerken sorunlarla olmalıdır, destek hello distro satıcıdan arama.

## <a name="updating-hello-azure-linux-agent"></a>Hello Azure Linux Aracısı güncelleştirme

## <a name="ubuntu"></a>Ubuntu

#### <a name="check-your-current-package-version"></a>Geçerli paket sürümü denetleyin

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Güncelleştirme paketi önbelleği

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Merhaba son Paket sürümü yükleyin

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a>Otomatik güncelleştirme etkinleştirildiğinden emin olun

Etkinleştirilirse, ilk olarak, toosee denetleyin:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' bulun. Bu çıktı görürseniz etkinleştirilir:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable çalıştırın:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Merhaba waagent hizmetini yeniden başlatın

#### <a name="restart-agent-for-1404"></a>14.04 için aracıyı yeniden başlatın

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a>Aracı 16.04 için yeniden başlatma / 17.04

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a>Debian

### <a name="debian-7-wheezy"></a>Debian 7 "Wheezy"

#### <a name="check-your-current-package-version"></a>Geçerli paket sürümü denetleyin

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a>Güncelleştirme paketi önbelleği

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Merhaba son Paket sürümü yükleyin

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a>Aracı için otomatik güncelleştirmeyi etkinleştir
Debian bu sürümü bir sürümü mevcut değil > = 2.0.16, bu nedenle edinebilmeleri için kullanılamıyor. Merhaba komutu yukarıda Hello çıktısını hello paket güncel olup olmadığını gösterir.

### <a name="debian-8-jessie--debian-9-stretch"></a>Debian 8 "Jessie" / "Debian 9 uzatma"

#### <a name="check-your-current-package-version"></a>Geçerli paket sürümü denetleyin

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Güncelleştirme paketi önbelleği

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Merhaba son Paket sürümü yükleyin

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a>Otomatik güncelleştirme etkinleştirildiğinden emin olun 

Etkinleştirilirse, ilk olarak, toosee denetleyin:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' bulun. Bu çıktı görürseniz etkinleştirilir:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable çalıştırın:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Merhaba waagent hizmetini yeniden başlatın

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a>RedHat / CentOS

### <a name="rhelcentos-6"></a>RHEL/CentOS 6

#### <a name="check-your-current-package-version"></a>Geçerli paket sürümü denetleyin

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Kullanılabilir güncelleştirmeleri denetle

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Merhaba son Paket sürümü yükleyin

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a>Otomatik güncelleştirme etkinleştirildiğinden emin olun 

Etkinleştirilirse, ilk olarak, toosee denetleyin:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' bulun. Bu çıktı görürseniz etkinleştirilir:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable çalıştırın:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Merhaba waagent hizmetini yeniden başlatın

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a>RHEL/CentOS 7

#### <a name="check-your-current-package-version"></a>Geçerli paket sürümü denetleyin

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Kullanılabilir güncelleştirmeleri denetle

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Merhaba son Paket sürümü yükleyin

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a>Otomatik güncelleştirme etkinleştirildiğinden emin olun 

Etkinleştirilirse, ilk olarak, toosee denetleyin:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' bulun. Bu çıktı görürseniz etkinleştirilir:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable çalıştırın:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Merhaba waagent hizmetini yeniden başlatın

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a>SUSE SLES

### <a name="suse-sles-11-sp4"></a>SUSE SLES 11 SP4

#### <a name="check-your-current-package-version"></a>Geçerli paket sürümü denetleyin

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Kullanılabilir güncelleştirmeleri denetle

Çıktı yukarıda Hello hello paket toodate olup olmadığını gösterir.

#### <a name="install-hello-latest-package-version"></a>Merhaba son Paket sürümü yükleyin

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Otomatik güncelleştirme etkinleştirildiğinden emin olun 

Etkinleştirilirse, ilk olarak, toosee denetleyin:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' bulun. Bu çıktı görürseniz etkinleştirilir:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable çalıştırın:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Merhaba waagent hizmetini yeniden başlatın

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a>SUSE SLES 12 SP2

#### <a name="check-your-current-package-version"></a>Geçerli paket sürümü denetleyin

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Kullanılabilir güncelleştirmeleri denetle

Yukarıdaki hello gelen Hello çıktısında, bu, hello paket değerine kadar tarih olup olmadığını gösterir.

#### <a name="install-hello-latest-package-version"></a>Merhaba son Paket sürümü yükleyin

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Otomatik güncelleştirme etkinleştirildiğinden emin olun 

Etkinleştirilirse, ilk olarak, toosee denetleyin:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' bulun. Bu çıktı görürseniz etkinleştirilir:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable çalıştırın:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Merhaba waagent hizmetini yeniden başlatın

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a>Oracle 6 ve 7

Oracle Linux için bu hello emin `Addons` depo etkindir. Tooedit hello dosya `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) veya `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) hello satır değiştirip `enabled=0` çok`enabled=1` altında **[ol6_addons]** veya **[ol7_addons]** Bu dosyada.

Ardından, tooinstall hello en son sürümünü hello Azure Linux Aracısı, türü:

```bash
sudo yum install WALinuxAgent
```

Merhaba eklenti deposu bulamazsanız hello tooyour Oracle Linux sürüm göre .repo dosyanızı sonunda bu satırları yalnızca ekleyebilirsiniz:

Oracle Linux 6 sanal makineler için:

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

Oracle Linux 7 sanal makineler için:

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

Ardından yazın:

```bash
sudo yum update WALinuxAgent
```

Genellikle tüm tooinstall gereken herhangi bir nedenden dolayı doğrudan https://github.com aşağıdaki kullanım hello ondan adımlar varsa ancak, gereken budur.


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a>Dağıtım için hiçbir aracı paketi mevcut olduğunda hello Linux Aracısı güncelleştirme

(Varsayılan olarak, Redhat, CentOS ve Oracle Linux sürümleri 6.4 ve 6.5 gibi yüklemeyin bazı distro'lar vardır) wget yazarak yüklemek `sudo yum install wget` hello komut satırında.

### <a name="1-download-hello-latest-version"></a>1. Merhaba en son sürümünü indirme
Açık [hello github'da Azure Linux Aracısı sürümü](https://github.com/Azure/WALinuxAgent/releases) bir web sayfası ve hello en son sürüm numarasını öğrenin. (Geçerli sürümünüzü yazarak bulabilirsiniz `waagent --version`.)

#### <a name="for-version-22x-or-later-type"></a>Sürüm için 2.2.x veya daha sonra yazın:
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

Merhaba aşağıdaki satırı sürüm 2.2.0 örnek olarak kullanılmıştır:

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a>2. Hello Azure Linux Aracısı yükleme

#### <a name="for-version-22x-use"></a>Sürüm için 2.2.x, kullanın:
Tooinstall hello paket gerekebilir `setuptools` ilk--bkz [burada](https://pypi.python.org/pypi/setuptools). Ardından çalıştırın:

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a>Otomatik güncelleştirme etkinleştirildiğinden emin olun

Etkinleştirilirse, ilk olarak, toosee denetleyin:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' bulun. Bu çıktı görürseniz etkinleştirilir:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable çalıştırın:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a>3. Merhaba waagent hizmetini yeniden başlatın
Linux distro'lar çoğu için:

```bash
sudo service waagent restart
```

Ubuntu için kullanın:

```bash
sudo service walinuxagent restart
```

CoreOS için kullanın:

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a>4. Hello Azure Linux Aracısı sürüm onaylayın
    
```bash
waagent -version
```

CoreOS için yukarıdaki komut hello çalışmayabilir.

Bu hello Azure Linux Aracısı sürüm toohello yeni sürümü güncelleştirilmiş görürsünüz.

Hello Azure Linux Aracısı ile ilgili daha fazla bilgi için bkz: [Azure Linux Aracısı Benioku](https://github.com/Azure/WALinuxAgent).
