---
title: "Github'dan Azure Linux Aracısı güncelleştirme | Microsoft Docs"
description: "Azure Linux Aracısı, Azure Linux VM'de için en son sürüme Github'dan güncelleştirme konusunda bilgi edinin"
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
ms.openlocfilehash: c79e37976a58ae5384b5856e0f7f258a773ef0fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-update-the-azure-linux-agent-on-a-vm"></a><span data-ttu-id="db064-103">Bir VM üzerinde Azure Linux Aracısı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="db064-103">How to update the Azure Linux Agent on a VM</span></span>

<span data-ttu-id="db064-104">Güncelleştirmek için [Azure Linux Aracısı](https://github.com/Azure/WALinuxAgent) azure'da bir Linux VM üzerinde önceden olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="db064-104">To update your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="db064-105">Azure'da çalışan bir Linux VM.</span><span class="sxs-lookup"><span data-stu-id="db064-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="db064-106">SSH kullanarak, Linux VM bağlantı.</span><span class="sxs-lookup"><span data-stu-id="db064-106">A connection to that Linux VM using SSH.</span></span>

<span data-ttu-id="db064-107">Her zaman Linux distro depodaki bir paket için ilk denetlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="db064-107">You should always check for a package in the Linux distro repository first.</span></span> <span data-ttu-id="db064-108">Kullanılabilir paketi otomatik güncelleştirme'yi etkinleştirme en son sürümü, ancak, Linux Aracısı'nı her zaman en son güncelleştirmeleri al sağlayacak olmayabilir mümkündür.</span><span class="sxs-lookup"><span data-stu-id="db064-108">It is possible the package available may not be the latest version, however, enabling autoupdate will ensure the Linux Agent will always get the latest update.</span></span> <span data-ttu-id="db064-109">Paket yöneticileri yüklerken sorunlarla olmalıdır, destek distro satıcıdan arama.</span><span class="sxs-lookup"><span data-stu-id="db064-109">Should you have issues installing from the package managers, you should seek support from the distro vendor.</span></span>

## <a name="updating-the-azure-linux-agent"></a><span data-ttu-id="db064-110">Azure Linux Aracısı'nı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="db064-110">Updating the Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="db064-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="db064-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db064-112">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="db064-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="db064-113">Güncelleştirme paketi önbelleği</span><span class="sxs-lookup"><span data-stu-id="db064-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db064-114">Son paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="db064-114">Install the latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db064-115">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="db064-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="db064-116">İlk olarak, etkin olup olmadığını denetleyin:</span><span class="sxs-lookup"><span data-stu-id="db064-116">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db064-117">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="db064-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db064-118">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="db064-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db064-119">Çalışma etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="db064-119">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="db064-120">Waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="db064-120">Restart the waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="db064-121">14.04 için aracıyı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="db064-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="db064-122">Aracı 16.04 için yeniden başlatma / 17.04</span><span class="sxs-lookup"><span data-stu-id="db064-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="db064-123">Debian</span><span class="sxs-lookup"><span data-stu-id="db064-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="db064-124">Debian 7 "Wheezy"</span><span class="sxs-lookup"><span data-stu-id="db064-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db064-125">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="db064-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="db064-126">Güncelleştirme paketi önbelleği</span><span class="sxs-lookup"><span data-stu-id="db064-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db064-127">Son paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="db064-127">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="db064-128">Aracı için otomatik güncelleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="db064-128">Enable agent auto update</span></span>
<span data-ttu-id="db064-129">Debian bu sürümü bir sürümü mevcut değil > = 2.0.16, bu nedenle edinebilmeleri için kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="db064-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="db064-130">Yukarıdaki komut çıktısı paket güncel olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="db064-130">The output from the above command will show you if the package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="db064-131">Debian 8 "Jessie" / "Debian 9 uzatma"</span><span class="sxs-lookup"><span data-stu-id="db064-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db064-132">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="db064-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="db064-133">Güncelleştirme paketi önbelleği</span><span class="sxs-lookup"><span data-stu-id="db064-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db064-134">Son paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="db064-134">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db064-135">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="db064-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="db064-136">İlk olarak, etkin olup olmadığını denetleyin:</span><span class="sxs-lookup"><span data-stu-id="db064-136">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db064-137">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="db064-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db064-138">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="db064-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db064-139">Çalışma etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="db064-139">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="db064-140">Waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="db064-140">Restart the waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="db064-141">RedHat / CentOS</span><span class="sxs-lookup"><span data-stu-id="db064-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="db064-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="db064-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db064-143">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="db064-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="db064-144">Kullanılabilir güncelleştirmeleri denetle</span><span class="sxs-lookup"><span data-stu-id="db064-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db064-145">Son paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="db064-145">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db064-146">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="db064-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="db064-147">İlk olarak, etkin olup olmadığını denetleyin:</span><span class="sxs-lookup"><span data-stu-id="db064-147">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db064-148">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="db064-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db064-149">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="db064-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db064-150">Çalışma etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="db064-150">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="db064-151">Waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="db064-151">Restart the waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="db064-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="db064-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db064-153">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="db064-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="db064-154">Kullanılabilir güncelleştirmeleri denetle</span><span class="sxs-lookup"><span data-stu-id="db064-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db064-155">Son paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="db064-155">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db064-156">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="db064-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="db064-157">İlk olarak, etkin olup olmadığını denetleyin:</span><span class="sxs-lookup"><span data-stu-id="db064-157">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db064-158">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="db064-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db064-159">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="db064-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db064-160">Çalışma etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="db064-160">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="db064-161">Waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="db064-161">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="db064-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="db064-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="db064-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="db064-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db064-164">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="db064-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="db064-165">Kullanılabilir güncelleştirmeleri denetle</span><span class="sxs-lookup"><span data-stu-id="db064-165">Check available updates</span></span>

<span data-ttu-id="db064-166">Yukarıdaki çıkış paketi güncel olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="db064-166">The above output will show you if the package is up to date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db064-167">Son paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="db064-167">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db064-168">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="db064-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="db064-169">İlk olarak, etkin olup olmadığını denetleyin:</span><span class="sxs-lookup"><span data-stu-id="db064-169">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db064-170">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="db064-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db064-171">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="db064-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db064-172">Çalışma etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="db064-172">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="db064-173">Waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="db064-173">Restart the waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="db064-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="db064-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db064-175">Geçerli paket sürümü denetleyin</span><span class="sxs-lookup"><span data-stu-id="db064-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="db064-176">Kullanılabilir güncelleştirmeleri denetle</span><span class="sxs-lookup"><span data-stu-id="db064-176">Check available updates</span></span>

<span data-ttu-id="db064-177">Yukarıdaki çıktıda Bu, paket değerine kadar tarih olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="db064-177">In the output from the above, this will show you if the package is upto date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db064-178">Son paket sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="db064-178">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db064-179">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="db064-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="db064-180">İlk olarak, etkin olup olmadığını denetleyin:</span><span class="sxs-lookup"><span data-stu-id="db064-180">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db064-181">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="db064-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db064-182">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="db064-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db064-183">Çalışma etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="db064-183">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="db064-184">Waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="db064-184">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="db064-185">Oracle 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="db064-185">Oracle 6 and 7</span></span>

<span data-ttu-id="db064-186">Oracle Linux için olduğundan emin olun `Addons` depo etkindir.</span><span class="sxs-lookup"><span data-stu-id="db064-186">For Oracle Linux, make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="db064-187">Dosyayı düzenlemek seçin `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) veya `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), satır değiştirip `enabled=0` için `enabled=1` altında **[ol6_addons]** veya **[ol7_addons]** bu dosyadaki.</span><span class="sxs-lookup"><span data-stu-id="db064-187">Choose to edit the file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="db064-188">Ardından, Azure Linux Aracısı'nın en son sürümünü yüklemek için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="db064-188">Then, to install the latest version of the Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="db064-189">Eklenti deposu bulamazsanız, Oracle Linux sürüme göre .repo dosyanızı sonunda bu satırları yalnızca ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="db064-189">If you don't find the add-on repository you can simply add these lines at the end of your .repo file according to your Oracle Linux release:</span></span>

<span data-ttu-id="db064-190">Oracle Linux 6 sanal makineler için:</span><span class="sxs-lookup"><span data-stu-id="db064-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="db064-191">Oracle Linux 7 sanal makineler için:</span><span class="sxs-lookup"><span data-stu-id="db064-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="db064-192">Ardından yazın:</span><span class="sxs-lookup"><span data-stu-id="db064-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="db064-193">Genellikle tüm gerekir, ancak herhangi bir nedenden dolayı doğrudan https://github.com yüklemeniz gerekiyorsa, aşağıdaki adımları kullanın budur.</span><span class="sxs-lookup"><span data-stu-id="db064-193">Typically this is all you need, but if for some reason you need to install it from https://github.com directly, use the following steps.</span></span>


## <a name="update-the-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="db064-194">Dağıtım için hiçbir aracı paketi mevcut olduğunda Linux aracısını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="db064-194">Update the Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="db064-195">(Varsayılan olarak, Redhat, CentOS ve Oracle Linux sürümleri 6.4 ve 6.5 gibi yüklemeyin bazı distro'lar vardır) wget yazarak yüklemek `sudo yum install wget` komut satırında.</span><span class="sxs-lookup"><span data-stu-id="db064-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on the command line.</span></span>

### <a name="1-download-the-latest-version"></a><span data-ttu-id="db064-196">1. En son sürümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="db064-196">1. Download the latest version</span></span>
<span data-ttu-id="db064-197">Açık [github'da Azure Linux Aracısı sürüm](https://github.com/Azure/WALinuxAgent/releases) bir web sayfası ve en son sürüm numarasını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="db064-197">Open [the release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out the latest version number.</span></span> <span data-ttu-id="db064-198">(Geçerli sürümünüzü yazarak bulabilirsiniz `waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="db064-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="db064-199">Sürüm için 2.2.x veya daha sonra yazın:</span><span class="sxs-lookup"><span data-stu-id="db064-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="db064-200">Aşağıdaki satırı sürüm 2.2.0 örnek olarak kullanılmıştır:</span><span class="sxs-lookup"><span data-stu-id="db064-200">The following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-the-azure-linux-agent"></a><span data-ttu-id="db064-201">2. Azure Linux Aracısı'nı yükleme</span><span class="sxs-lookup"><span data-stu-id="db064-201">2. Install the Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="db064-202">Sürüm için 2.2.x, kullanın:</span><span class="sxs-lookup"><span data-stu-id="db064-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="db064-203">Paket yüklemeniz gerekebilir `setuptools` ilk--bkz [burada](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="db064-203">You may need to install the package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="db064-204">Ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="db064-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db064-205">Otomatik güncelleştirme etkinleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="db064-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="db064-206">İlk olarak, etkin olup olmadığını denetleyin:</span><span class="sxs-lookup"><span data-stu-id="db064-206">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db064-207">'AutoUpdate.Enabled' bulun.</span><span class="sxs-lookup"><span data-stu-id="db064-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db064-208">Bu çıktı görürseniz etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="db064-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db064-209">Çalışma etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="db064-209">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-the-waagent-service"></a><span data-ttu-id="db064-210">3. Waagent hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="db064-210">3. Restart the waagent service</span></span>
<span data-ttu-id="db064-211">Linux distro'lar çoğu için:</span><span class="sxs-lookup"><span data-stu-id="db064-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="db064-212">Ubuntu için kullanın:</span><span class="sxs-lookup"><span data-stu-id="db064-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="db064-213">CoreOS için kullanın:</span><span class="sxs-lookup"><span data-stu-id="db064-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-the-azure-linux-agent-version"></a><span data-ttu-id="db064-214">4. Azure Linux Aracısı sürüm onaylayın</span><span class="sxs-lookup"><span data-stu-id="db064-214">4. Confirm the Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="db064-215">CoreOS için yukarıdaki komut çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="db064-215">For CoreOS, the above command may not work.</span></span>

<span data-ttu-id="db064-216">Azure Linux Aracısı sürüm yeni sürüme güncelleştirilip güncelleştirilmediğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="db064-216">You will see that the Azure Linux Agent version has been updated to the new version.</span></span>

<span data-ttu-id="db064-217">Azure Linux Aracısı ile ilgili daha fazla bilgi için bkz: [Azure Linux Aracısı Benioku](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="db064-217">For more information regarding the Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>