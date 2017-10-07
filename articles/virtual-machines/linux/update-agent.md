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
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a><span data-ttu-id="ed9c1-103">Nasıl tooupdate hello Azure Linux Aracısı'nı bir VM</span><span class="sxs-lookup"><span data-stu-id="ed9c1-103">How tooupdate hello Azure Linux Agent on a VM</span></span>

<span data-ttu-id="ed9c1-104">tooupdate, [Azure Linux Aracısı](https://github.com/Azure/WALinuxAgent) azure'da bir Linux VM üzerinde önceden olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-104">tooupdate your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="ed9c1-105">Azure'da çalışan bir Linux VM.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="ed9c1-106">Bağlantı toothat Linux VM SSH kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-106">A connection toothat Linux VM using SSH.</span></span>

<span data-ttu-id="ed9c1-107">Her zaman hello Linux distro deposundaki bir paket için ilk denetlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-107">You should always check for a package in hello Linux distro repository first.</span></span> <span data-ttu-id="ed9c1-108">Mümkünse kullanılabilir hello paketi hello en son sürümünü değil olabilir, ancak, Otomatik Güncelleştirme'yi etkinleştirme hello Linux Aracısı her zaman hello en son güncelleştirmeyi alın garanti eder.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-108">It is possible hello package available may not be hello latest version, however, enabling autoupdate will ensure hello Linux Agent will always get hello latest update.</span></span> <span data-ttu-id="ed9c1-109">Merhaba paket yöneticileri yüklerken sorunlarla olmalıdır, destek hello distro satıcıdan arama.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-109">Should you have issues installing from hello package managers, you should seek support from hello distro vendor.</span></span>

## <a name="updating-hello-azure-linux-agent"></a><span data-ttu-id="ed9c1-110">Hello Azure Linux Aracısı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ed9c1-110">Updating hello Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="ed9c1-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ed9c1-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ed9c1-112">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="ed9c1-113">Güncelleştirme paketi önbelleği</span><span class="sxs-lookup"><span data-stu-id="ed9c1-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ed9c1-114">Merhaba son Paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-114">Install hello latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ed9c1-115">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="ed9c1-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="ed9c1-116">Etkinleştirilirse, ilk olarak, toosee denetleyin:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-116">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ed9c1-117">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ed9c1-118">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ed9c1-119">tooenable çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-119">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="ed9c1-120">Merhaba waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="ed9c1-120">Restart hello waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="ed9c1-121">14.04 için aracıyı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="ed9c1-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="ed9c1-122">Aracı 16.04 için yeniden başlatma / 17.04</span><span class="sxs-lookup"><span data-stu-id="ed9c1-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="ed9c1-123">Debian</span><span class="sxs-lookup"><span data-stu-id="ed9c1-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="ed9c1-124">Debian 7 "Wheezy"</span><span class="sxs-lookup"><span data-stu-id="ed9c1-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ed9c1-125">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="ed9c1-126">Güncelleştirme paketi önbelleği</span><span class="sxs-lookup"><span data-stu-id="ed9c1-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ed9c1-127">Merhaba son Paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-127">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="ed9c1-128">Aracı için otomatik güncelleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ed9c1-128">Enable agent auto update</span></span>
<span data-ttu-id="ed9c1-129">Debian bu sürümü bir sürümü mevcut değil > = 2.0.16, bu nedenle edinebilmeleri için kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="ed9c1-130">Merhaba komutu yukarıda Hello çıktısını hello paket güncel olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-130">hello output from hello above command will show you if hello package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="ed9c1-131">Debian 8 "Jessie" / "Debian 9 uzatma"</span><span class="sxs-lookup"><span data-stu-id="ed9c1-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ed9c1-132">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="ed9c1-133">Güncelleştirme paketi önbelleği</span><span class="sxs-lookup"><span data-stu-id="ed9c1-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ed9c1-134">Merhaba son Paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-134">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ed9c1-135">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="ed9c1-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="ed9c1-136">Etkinleştirilirse, ilk olarak, toosee denetleyin:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-136">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ed9c1-137">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ed9c1-138">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ed9c1-139">tooenable çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-139">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="ed9c1-140">Merhaba waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="ed9c1-140">Restart hello waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="ed9c1-141">RedHat / CentOS</span><span class="sxs-lookup"><span data-stu-id="ed9c1-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="ed9c1-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="ed9c1-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ed9c1-143">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="ed9c1-144">Kullanılabilir güncelleştirmeleri denetle</span><span class="sxs-lookup"><span data-stu-id="ed9c1-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ed9c1-145">Merhaba son Paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-145">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ed9c1-146">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="ed9c1-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="ed9c1-147">Etkinleştirilirse, ilk olarak, toosee denetleyin:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-147">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ed9c1-148">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ed9c1-149">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ed9c1-150">tooenable çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-150">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="ed9c1-151">Merhaba waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="ed9c1-151">Restart hello waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="ed9c1-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="ed9c1-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ed9c1-153">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="ed9c1-154">Kullanılabilir güncelleştirmeleri denetle</span><span class="sxs-lookup"><span data-stu-id="ed9c1-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ed9c1-155">Merhaba son Paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-155">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ed9c1-156">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="ed9c1-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="ed9c1-157">Etkinleştirilirse, ilk olarak, toosee denetleyin:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-157">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ed9c1-158">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ed9c1-159">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ed9c1-160">tooenable çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-160">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="ed9c1-161">Merhaba waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="ed9c1-161">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="ed9c1-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="ed9c1-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="ed9c1-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="ed9c1-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ed9c1-164">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="ed9c1-165">Kullanılabilir güncelleştirmeleri denetle</span><span class="sxs-lookup"><span data-stu-id="ed9c1-165">Check available updates</span></span>

<span data-ttu-id="ed9c1-166">Çıktı yukarıda Hello hello paket toodate olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-166">hello above output will show you if hello package is up toodate.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ed9c1-167">Merhaba son Paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-167">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ed9c1-168">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="ed9c1-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="ed9c1-169">Etkinleştirilirse, ilk olarak, toosee denetleyin:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-169">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ed9c1-170">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ed9c1-171">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ed9c1-172">tooenable çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-172">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="ed9c1-173">Merhaba waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="ed9c1-173">Restart hello waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="ed9c1-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="ed9c1-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ed9c1-175">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="ed9c1-176">Kullanılabilir güncelleştirmeleri denetle</span><span class="sxs-lookup"><span data-stu-id="ed9c1-176">Check available updates</span></span>

<span data-ttu-id="ed9c1-177">Yukarıdaki hello gelen Hello çıktısında, bu, hello paket değerine kadar tarih olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-177">In hello output from hello above, this will show you if hello package is upto date.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ed9c1-178">Merhaba son Paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="ed9c1-178">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ed9c1-179">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="ed9c1-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="ed9c1-180">Etkinleştirilirse, ilk olarak, toosee denetleyin:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-180">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ed9c1-181">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ed9c1-182">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ed9c1-183">tooenable çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-183">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="ed9c1-184">Merhaba waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="ed9c1-184">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="ed9c1-185">Oracle 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="ed9c1-185">Oracle 6 and 7</span></span>

<span data-ttu-id="ed9c1-186">Oracle Linux için bu hello emin `Addons` depo etkindir.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-186">For Oracle Linux, make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="ed9c1-187">Tooedit hello dosya `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) veya `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) hello satır değiştirip `enabled=0` çok`enabled=1` altında **[ol6_addons]** veya **[ol7_addons]** Bu dosyada.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-187">Choose tooedit hello file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="ed9c1-188">Ardından, tooinstall hello en son sürümünü hello Azure Linux Aracısı, türü:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-188">Then, tooinstall hello latest version of hello Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="ed9c1-189">Merhaba eklenti deposu bulamazsanız hello tooyour Oracle Linux sürüm göre .repo dosyanızı sonunda bu satırları yalnızca ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-189">If you don't find hello add-on repository you can simply add these lines at hello end of your .repo file according tooyour Oracle Linux release:</span></span>

<span data-ttu-id="ed9c1-190">Oracle Linux 6 sanal makineler için:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="ed9c1-191">Oracle Linux 7 sanal makineler için:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="ed9c1-192">Ardından yazın:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="ed9c1-193">Genellikle tüm tooinstall gereken herhangi bir nedenden dolayı doğrudan https://github.com aşağıdaki kullanım hello ondan adımlar varsa ancak, gereken budur.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-193">Typically this is all you need, but if for some reason you need tooinstall it from https://github.com directly, use hello following steps.</span></span>


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="ed9c1-194">Dağıtım için hiçbir aracı paketi mevcut olduğunda hello Linux Aracısı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ed9c1-194">Update hello Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="ed9c1-195">(Varsayılan olarak, Redhat, CentOS ve Oracle Linux sürümleri 6.4 ve 6.5 gibi yüklemeyin bazı distro'lar vardır) wget yazarak yüklemek `sudo yum install wget` hello komut satırında.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on hello command line.</span></span>

### <a name="1-download-hello-latest-version"></a><span data-ttu-id="ed9c1-196">1. Merhaba en son sürümünü indirme</span><span class="sxs-lookup"><span data-stu-id="ed9c1-196">1. Download hello latest version</span></span>
<span data-ttu-id="ed9c1-197">Açık [hello github'da Azure Linux Aracısı sürümü](https://github.com/Azure/WALinuxAgent/releases) bir web sayfası ve hello en son sürüm numarasını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-197">Open [hello release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out hello latest version number.</span></span> <span data-ttu-id="ed9c1-198">(Geçerli sürümünüzü yazarak bulabilirsiniz `waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="ed9c1-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="ed9c1-199">Sürüm için 2.2.x veya daha sonra yazın:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="ed9c1-200">Merhaba aşağıdaki satırı sürüm 2.2.0 örnek olarak kullanılmıştır:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-200">hello following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a><span data-ttu-id="ed9c1-201">2. Hello Azure Linux Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="ed9c1-201">2. Install hello Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="ed9c1-202">Sürüm için 2.2.x, kullanın:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="ed9c1-203">Tooinstall hello paket gerekebilir `setuptools` ilk--bkz [burada](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="ed9c1-203">You may need tooinstall hello package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="ed9c1-204">Ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ed9c1-205">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="ed9c1-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="ed9c1-206">Etkinleştirilirse, ilk olarak, toosee denetleyin:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-206">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ed9c1-207">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ed9c1-208">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ed9c1-209">tooenable çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-209">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a><span data-ttu-id="ed9c1-210">3. Merhaba waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="ed9c1-210">3. Restart hello waagent service</span></span>
<span data-ttu-id="ed9c1-211">Linux distro'lar çoğu için:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="ed9c1-212">Ubuntu için kullanın:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="ed9c1-213">CoreOS için kullanın:</span><span class="sxs-lookup"><span data-stu-id="ed9c1-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a><span data-ttu-id="ed9c1-214">4. Hello Azure Linux Aracısı sürüm onaylayın</span><span class="sxs-lookup"><span data-stu-id="ed9c1-214">4. Confirm hello Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="ed9c1-215">CoreOS için yukarıdaki komut hello çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-215">For CoreOS, hello above command may not work.</span></span>

<span data-ttu-id="ed9c1-216">Bu hello Azure Linux Aracısı sürüm toohello yeni sürümü güncelleştirilmiş görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ed9c1-216">You will see that hello Azure Linux Agent version has been updated toohello new version.</span></span>

<span data-ttu-id="ed9c1-217">Hello Azure Linux Aracısı ile ilgili daha fazla bilgi için bkz: [Azure Linux Aracısı Benioku](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="ed9c1-217">For more information regarding hello Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>
