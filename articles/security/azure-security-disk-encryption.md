---
title: "Windows ve Linux Iaas VM'ler için Disk şifrelemesi aaaAzure | Microsoft Docs"
description: "Bu makale için Microsoft Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler genel bakış sağlar."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="cbafa-103">Windows ve Linux Iaas VM'ler için Azure Disk şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="cbafa-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="cbafa-104">Microsoft Azure veri gizliliğinizi veri egemenliği kesinlikle taahhüt tooensuring olduğundan ve Azure barındırılan toocontrol sağlayan gelişmiş teknolojiler tooencrypt çeşitli verilerine denetlemek ve şifreleme anahtarlarını yönetmek veri denetim & Denetim erişimi.</span><span class="sxs-lookup"><span data-stu-id="cbafa-104">Microsoft Azure is strongly committed tooensuring your data privacy, data sovereignty and enables you toocontrol your Azure hosted data through a range of advanced technologies tooencrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="cbafa-105">Bu Azure müşterilerin kendi iş ihtiyaçlarına en iyi karşılayan hello esneklik toochoose hello çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="cbafa-105">This provides Azure customers hello flexibility toochoose hello solution that best meets their business needs.</span></span> <span data-ttu-id="cbafa-106">Bu yazıda, biz, tooa yeni teknoloji çözümü "Windows ve Linux Iaas VM'in Azure Disk şifrelemesi" tanıtılacaktır toohelp korumak ve veri toomeet, kuruluş güvenlik ve uyumluluk taahhüt koruyun.</span><span class="sxs-lookup"><span data-stu-id="cbafa-106">In this paper, we will introduce you tooa new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” toohelp protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="cbafa-107">Merhaba kağıt senaryoları ve hello kullanıcı deneyimleri hello dahil olmak üzere toouse hello Azure disk şifrelemesi özelliklerini nasıl desteklenmiyor ayrıntılı kılavuz sunar.</span><span class="sxs-lookup"><span data-stu-id="cbafa-107">hello paper provides detailed guidance on how toouse hello Azure disk encryption features including hello supported scenarios and hello user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-108">Bazı öneriler verileri, ağ veya ek lisans ya da abonelik maliyetlerinizi kaynaklanan hesaplama kaynak kullanımını artırabilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="cbafa-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cbafa-109">Overview</span></span>
<span data-ttu-id="cbafa-110">Azure Disk şifrelemesi, Windows ve Linux Iaas sanal makine disklerinizi şifrelemek yardımcı olan yeni bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="cbafa-111">Azure Disk şifrelemesi yararlanır hello endüstri standardı [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) özelliği Windows hello ve [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) hello işletim sistemi ve hello veri diskleri için Linux tooprovide birim şifrelemesi özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-111">Azure Disk Encryption leverages hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux tooprovide volume encryption for hello OS and hello data disks.</span></span> <span data-ttu-id="cbafa-112">Merhaba çözümü ile tümleştirildiğinde [Azure anahtar kasası](https://azure.microsoft.com/documentation/services/key-vault/) denetlemek ve hello disk şifreleme anahtarları ve gizli anahtar kasası aboneliğinizi yönetmek toohelp.</span><span class="sxs-lookup"><span data-stu-id="cbafa-112">hello solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp you control and manage hello disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="cbafa-113">Merhaba çözüm ayrıca hello sanal makine disklerdeki tüm veriler Azure depolama alanınızı bekleyen şifrelenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="cbafa-113">hello solution also ensures that all data on hello virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="cbafa-114">Azure disk şifrelemesi Windows ve Linux Iaas VM'ler için şimdi olan **genel kullanılabilirlik** tüm Azure genel bölgeler ve premium depolama ile standart VM'ler ve sanal makineleri için AzureGov bölgeler.</span><span class="sxs-lookup"><span data-stu-id="cbafa-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="cbafa-115">Şifreleme senaryosu</span><span class="sxs-lookup"><span data-stu-id="cbafa-115">Encryption scenarios</span></span>
<span data-ttu-id="cbafa-116">Hello Azure Disk şifrelemesi çözüm müşteri senaryoları aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="cbafa-116">hello Azure Disk Encryption solution supports hello following customer scenarios:</span></span>

* <span data-ttu-id="cbafa-117">Önceden şifrelenmiş VHD ve şifreleme anahtarlarını oluşturulan yeni Iaas VM'ler şifrelemeyi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="cbafa-118">Desteklenen hello Azure galeri görüntüleri kullanılarak oluşturulan yeni Iaas VM'ler şifrelemeyi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-118">Enable encryption on new IaaS VMs created from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="cbafa-119">Azure'da çalışan Iaas VM'ler şifrelemeyi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="cbafa-120">Windows Iaas Vm'leri üzerinde şifrelemeyi devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="cbafa-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="cbafa-121">Veri sürücülerini şifreleme Linux Iaas VM'ler için devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="cbafa-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="cbafa-122">Yönetilen diskin VM'ler şifrelemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="cbafa-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="cbafa-123">Mevcut şifrelenmiş premium olmayan depolama VM şifreleme ayarlarını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="cbafa-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="cbafa-124">Yedekleme ve geri yükleme anahtar şifreleme anahtarıyla şifrelenir şifrelenmiş VM'ler</span><span class="sxs-lookup"><span data-stu-id="cbafa-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="cbafa-125">Microsoft Azure'da etkinleştirildiğinde senaryoları Iaas VM'ler için aşağıdaki hello Hello çözümünü destekler:</span><span class="sxs-lookup"><span data-stu-id="cbafa-125">hello solution supports hello following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="cbafa-126">Azure anahtar kasası ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="cbafa-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="cbafa-127">Standart katmanı VMs: [A, D, DS, G, GS, F ve benzeri serisi Iaas VM'ler](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="cbafa-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="cbafa-128">Windows ve Linux Iaas Vm'leri ve hello yönetilen diskten VM'ler etkinleştir şifreleme Azure galeri görüntüleri desteklenen</span><span class="sxs-lookup"><span data-stu-id="cbafa-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="cbafa-129">Windows Iaas Vm'leri ve yönetilen disk VM'ler için işletim sistemi ve veri sürücülerde şifreleme devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="cbafa-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="cbafa-130">Veri sürücülerini şifreleme Linux Iaas Vm'leri ve yönetilen disk VM'ler için devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="cbafa-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="cbafa-131">Iaas Windows istemci işletim sistemi çalıştıran VM'ler şifrelemeyi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="cbafa-132">Bağlama yolları birimlerle şifrelemeyi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="cbafa-133">Linux VM diskle yapılandırılmış şifrelemeyi etkinleştirin mdadm kullanarak şeritleme (RAID)</span><span class="sxs-lookup"><span data-stu-id="cbafa-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="cbafa-134">Veri diskleri için LVM kullanarak Linux VM'ler şifrelemeyi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="cbafa-135">Windows VM depolama alanları ile yapılandırılmış şifrelemeyi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="cbafa-136">Mevcut şifrelenmiş premium olmayan depolama VM şifreleme ayarlarını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="cbafa-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="cbafa-137">Tüm Azure genel ve AzureGov bölgeleri desteklenir</span><span class="sxs-lookup"><span data-stu-id="cbafa-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="cbafa-138">Merhaba çözüm senaryoları, özellikleri ve teknoloji aşağıdaki hello desteklemez:</span><span class="sxs-lookup"><span data-stu-id="cbafa-138">hello solution does not support hello following scenarios, features, and technology:</span></span>

* <span data-ttu-id="cbafa-139">Temel katman Iaas VM'ler</span><span class="sxs-lookup"><span data-stu-id="cbafa-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="cbafa-140">Bir işletim sistemi sürücüsünde Linux Iaas VM'ler için şifrelemeyi devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="cbafa-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="cbafa-141">Merhaba işletim sistemi sürücüsü Linux Iaas VM'ler için şifreliyse, şifreleme veri sürücüsünde devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="cbafa-141">Disabling encryption on a data drive if hello OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="cbafa-142">Merhaba Klasik VM oluşturma yöntemini kullanarak oluşturduğunuz Iaas VM'ler</span><span class="sxs-lookup"><span data-stu-id="cbafa-142">IaaS VMs that are created by using hello classic VM creation method</span></span>
* <span data-ttu-id="cbafa-143">Windows ve Linux Iaas VM'ler müşteri özel resimler desteklenmiyor şifrelemeyi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="cbafa-144">Enccryption etkinleştirmek Linux LVM işletim sisteminde disk şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="cbafa-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="cbafa-145">Bu destek yakında gelecektir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-145">This support will come soon.</span></span>
* <span data-ttu-id="cbafa-146">Şirket içi anahtar yönetimi hizmeti ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="cbafa-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="cbafa-147">Azure dosyaları (paylaşılan dosya sistemi), ağ dosya sistemi (NFS), dinamik birimler ve yazılım tabanlı RAID sistemler ile yapılandırılmış Windows VM'ler</span><span class="sxs-lookup"><span data-stu-id="cbafa-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="cbafa-148">Yedekleme ve geri yükleme anahtar şifreleme anahtarı olmadan şifrelenmiş şifrelenmiş VM'lerin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="cbafa-149">Varolan bir şifrelenmiş premium Storage VM şifreleme ayarlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-150">Yedekleme ve geri yükleme şifrelenmiş VM'lerin hello KEK yapılandırmayla şifrelenmiş VM'ler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="cbafa-151">KEK şifrelenmiş vm'lerde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="cbafa-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="cbafa-152">KEK VM şifreleme sağlayan isteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="cbafa-153">Bu desteği yakında geliyor.</span><span class="sxs-lookup"><span data-stu-id="cbafa-153">This support is coming soon.</span></span>
> <span data-ttu-id="cbafa-154">VM desteklenmez varolan bir şifrelenmiş premium Storage şifreleme ayarlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="cbafa-155">Bu desteği yakında geliyor.</span><span class="sxs-lookup"><span data-stu-id="cbafa-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="cbafa-156">Şifreleme özellikleri</span><span class="sxs-lookup"><span data-stu-id="cbafa-156">Encryption features</span></span>
<span data-ttu-id="cbafa-157">Etkinleştirme ve Azure Iaas VM'ler için Azure Disk şifrelemesi dağıtma hello aşağıdaki özellikleri, sağlanan hello yapılandırmasına bağlı olarak etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="cbafa-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, hello following capabilities are enabled, depending on hello configuration provided:</span></span>

* <span data-ttu-id="cbafa-158">Merhaba işletim sistemi birimi tooprotect hello önyükleme biriminin depolama alanınızın bekleyen şifreleme</span><span class="sxs-lookup"><span data-stu-id="cbafa-158">Encryption of hello OS volume tooprotect hello boot volume at rest in your storage</span></span>
* <span data-ttu-id="cbafa-159">Veri birimleri tooprotect hello veri birimleri depolama alanınızın bekleyen şifreleme</span><span class="sxs-lookup"><span data-stu-id="cbafa-159">Encryption of data volumes tooprotect hello data volumes at rest in your storage</span></span>
* <span data-ttu-id="cbafa-160">Windows Iaas VM'ler için sürücüleri hello işletim sistemi ve veri şifreleme devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="cbafa-160">Disabling encryption on hello OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="cbafa-161">(Yalnızca işletim sistemi şifreli değil sürücü varsa) hello veriler üzerinde şifrelemeyi devre dışı bırakma Linux Iaas VM'ler için sürücüler</span><span class="sxs-lookup"><span data-stu-id="cbafa-161">Disabling encryption on hello data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="cbafa-162">Merhaba şifreleme anahtarları ve gizli anahtar kasası aboneliğinizde koruma</span><span class="sxs-lookup"><span data-stu-id="cbafa-162">Safeguarding hello encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="cbafa-163">Iaas VM şifrelenmiş hello Hello şifreleme durumu raporlama</span><span class="sxs-lookup"><span data-stu-id="cbafa-163">Reporting hello encryption status of hello encrypted IaaS VM</span></span>
* <span data-ttu-id="cbafa-164">Disk şifrelemesi yapılandırma ayarlarını hello Iaas sanal makinesinden kaldırılması</span><span class="sxs-lookup"><span data-stu-id="cbafa-164">Removal of disk-encryption configuration settings from hello IaaS virtual machine</span></span>
* <span data-ttu-id="cbafa-165">Yedekleme ve geri yükleme hello Azure Yedekleme hizmetini kullanarak şifrelenmiş VM'ler</span><span class="sxs-lookup"><span data-stu-id="cbafa-165">Backup and restore of encrypted VMs by using hello Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-166">Yedekleme ve geri yükleme şifrelenmiş VM'lerin hello KEK yapılandırmayla şifrelenmiş VM'ler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="cbafa-167">KEK şifrelenmiş vm'lerde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="cbafa-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="cbafa-168">KEK VM şifreleme sağlayan isteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="cbafa-169">Windows ve Linux çözüm için Iaas VM'ler için Azure Disk şifrelemesi içerir:</span><span class="sxs-lookup"><span data-stu-id="cbafa-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="cbafa-170">için Windows Hello disk şifrelemesi uzantısı.</span><span class="sxs-lookup"><span data-stu-id="cbafa-170">hello disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="cbafa-171">Linux için Hello disk şifrelemesi uzantısı.</span><span class="sxs-lookup"><span data-stu-id="cbafa-171">hello disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="cbafa-172">Merhaba disk şifrelemesi PowerShell cmdlet'leri.</span><span class="sxs-lookup"><span data-stu-id="cbafa-172">hello disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="cbafa-173">disk şifrelemesi Azure komut satırı arabirimi (CLI) cmdlet'leri hello.</span><span class="sxs-lookup"><span data-stu-id="cbafa-173">hello disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="cbafa-174">Merhaba disk şifrelemesi Azure Resource Manager şablonları.</span><span class="sxs-lookup"><span data-stu-id="cbafa-174">hello disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="cbafa-175">Hello Azure Disk şifrelemesi çözüm Iaas Vm'leri üzerinde Windows veya Linux işletim sistemi çalıştıran desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-175">hello Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="cbafa-176">Merhaba desteklenen işletim sistemleri hakkında daha fazla bilgi için bkz: hello "Önkoşullar" bölümü.</span><span class="sxs-lookup"><span data-stu-id="cbafa-176">For more information about hello supported operating systems, see hello "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-177">VM diskleri Azure Disk şifrelemesi ile şifrelemek için ek ücret yoktur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="cbafa-178">Değer önerisi</span><span class="sxs-lookup"><span data-stu-id="cbafa-178">Value proposition</span></span>
<span data-ttu-id="cbafa-179">Hello Azure Disk şifrelemesi yönetimi çözümü uyguladığınızda, hello aşağıdaki iş gereksinimlerini karşılayabilen:</span><span class="sxs-lookup"><span data-stu-id="cbafa-179">When you apply hello Azure Disk Encryption-management solution, you can satisfy hello following business needs:</span></span>

* <span data-ttu-id="cbafa-180">Endüstri standardı şifreleme teknolojisi tooaddress kuruluş güvenlik ve uyumluluk gereksinimleri kullanabileceğinizden Iaas Vm'leri, bekleyen güvenli hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology tooaddress organizational security and compliance requirements.</span></span>
* <span data-ttu-id="cbafa-181">Iaas Vm'leri önyükleme müşteri denetlenen anahtarlar ve ilkeleri ve altında kullanımları anahtar kasanızdaki denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="cbafa-182">Şifreleme iş akışı</span><span class="sxs-lookup"><span data-stu-id="cbafa-182">Encryption workflow</span></span>
<span data-ttu-id="cbafa-183">Windows ve Linux VM'ler için tooenable disk şifrelemesi hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="cbafa-183">tooenable disk encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="cbafa-184">Bir şifreleme senaryosu şifreleme senaryosu önceki hello kümelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-184">Choose an encryption scenario from among hello preceding encryption scenarios.</span></span>
2. <span data-ttu-id="cbafa-185">Tooenabling disk şifrelemesi'hello Azure Disk şifrelemesi Resource Manager şablonu, PowerShell cmdlet'lerini veya CLI komutu aracılığıyla kabul ve hello şifreleme yapılandırması belirtin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-185">Opt in tooenabling disk encryption via hello Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify hello encryption configuration.</span></span>

   * <span data-ttu-id="cbafa-186">Merhaba müşteri şifrelenmiş VHD senaryosu için şifrelenmiş hello VHD tooyour depolama hesabı ve hello şifreleme anahtar malzeme tooyour anahtar kasası karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-186">For hello customer-encrypted VHD scenario, upload hello encrypted VHD tooyour storage account and hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="cbafa-187">Sonra yeni bir Iaas VM hello şifreleme yapılandırması tooenable şifreleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="cbafa-187">Then, provide hello encryption configuration tooenable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="cbafa-188">Market hello oluşturulan yeni VM'ler ve Azure'da zaten çalıştıran var olan VM'ler için hello Iaas VM üzerinde hello şifreleme yapılandırması tooenable şifreleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="cbafa-188">For new VMs that are created from hello Marketplace and existing VMs that are already running in Azure, provide hello encryption configuration tooenable encryption on hello IaaS VM.</span></span>

3. <span data-ttu-id="cbafa-189">GRANT erişim toohello Azure platformu tooread hello şifreleme anahtar malzemesini (BitLocker şifreleme anahtarları Windows sistemleri için) ve Linux için parola hello Iaas VM, anahtar kasası tooenable şifreleme.</span><span class="sxs-lookup"><span data-stu-id="cbafa-189">Grant access toohello Azure platform tooread hello encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault tooenable encryption on hello IaaS VM.</span></span>

4. <span data-ttu-id="cbafa-190">Hello Azure Active Directory (Azure AD) uygulama kimliği toowrite hello şifreleme anahtar malzeme tooyour anahtar kasası sağlar.</span><span class="sxs-lookup"><span data-stu-id="cbafa-190">Provide hello Azure Active Directory (Azure AD) application identity toowrite hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="cbafa-191">Bunun yapılması, 2. adımda bahsedilen hello senaryoları için hello Iaas VM üzerinde şifrelemeyi etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-191">Doing so enables encryption on hello IaaS VM for hello scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="cbafa-192">Azure hello VM hizmet modeli hello anahtar kasası yapılandırma ve şifreleme ile güncelleştirir ve şifrelenmiş VM'nizi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="cbafa-192">Azure updates hello VM service model with encryption and hello key vault configuration, and sets up your encrypted VM.</span></span>

 ![Azure’da Microsoft Kötü Amaçlı Yazılımdan Koruma](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="cbafa-194">Şifre çözme iş akışı</span><span class="sxs-lookup"><span data-stu-id="cbafa-194">Decryption workflow</span></span>
<span data-ttu-id="cbafa-195">toodisable disk şifrelemesi Iaas VM'ler, aşağıdaki üst düzey adımları tam hello için:</span><span class="sxs-lookup"><span data-stu-id="cbafa-195">toodisable disk encryption for IaaS VMs, complete hello following high-level steps:</span></span>

1. <span data-ttu-id="cbafa-196">Hello Azure Disk şifrelemesi Resource Manager şablonu veya PowerShell cmdlet'leri aracılığıyla azure'da çalışan bir Iaas VM üzerinde toodisable şifreleme (şifre çözme) seçin ve hello şifre çözme yapılandırma belirtin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-196">Choose toodisable encryption (decryption) on a running IaaS VM in Azure via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify hello decryption configuration.</span></span>

 <span data-ttu-id="cbafa-197">Bu adım hello işletim sistemi veya hello veri biriminin veya hem de Windows Iaas VM çalıştıran hello şifreleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-197">This step disables encryption of hello OS or hello data volume or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="cbafa-198">Ancak, hello önceki bölümünde belirtildiği gibi Linux işletim sistemi disk şifrelemesi devre dışı bırakma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="cbafa-198">However, as mentioned in hello previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="cbafa-199">Merhaba işletim sistemi diski şifrelenmemiş sürece hello şifre çözme adım yalnızca Linux VM'ler veri sürücülerinde izin verilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-199">hello decryption step is allowed only for data drives on Linux VMs as long as hello OS disk is not encrypted.</span></span>
2. <span data-ttu-id="cbafa-200">VM hizmet modeli Azure güncelleştirmeleri hello ve hello Iaas VM şifresi çözülmüş işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-200">Azure updates hello VM service model, and hello IaaS VM is marked decrypted.</span></span> <span data-ttu-id="cbafa-201">Merhaba VM Merhaba içeriğine artık bekleyen şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-201">hello contents of hello VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-202">Merhaba şifreleme devre dışı bırakma işlemi, anahtar kasasını ve hello şifreleme anahtar malzemesi (BitLocker şifreleme anahtarları Windows sistemleri için) veya Linux için parola silmez.</span><span class="sxs-lookup"><span data-stu-id="cbafa-202">hello disable-encryption operation does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="cbafa-203">Linux işletim sistemi disk şifrelemesi devre dışı bırakma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="cbafa-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="cbafa-204">Merhaba şifre çözme adım yalnızca Linux VM'ler veri sürücülerinde izin verilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-204">hello decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="cbafa-205">Merhaba işletim sistemi sürücüsü şifrelenmiş verileri disk şifrelemesi Linux için devre dışı bırakma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="cbafa-205">Disabling data disk encryption for Linux is not supported if hello OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbafa-206">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cbafa-206">Prerequisites</span></span>
<span data-ttu-id="cbafa-207">Merhaba "Genel bakış" bölümünde ele alınan hello desteklenen senaryolar için Azure Disk şifrelemesi Azure Iaas Vm'leri üzerinde etkinleştirmeden önce önkoşulları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for hello supported scenarios that were discussed in hello "Overview" section, see hello following prerequisites:</span></span>

* <span data-ttu-id="cbafa-208">Geçerli etkin Azure aboneliği toocreate kaynakları Azure desteklenen hello bölgelerde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-208">You must have a valid active Azure subscription toocreate resources in Azure in hello supported regions.</span></span>
* <span data-ttu-id="cbafa-209">Azure Disk şifrelemesi, Windows Server sürümleri aşağıdaki hello üzerinde desteklenir: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 ve Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="cbafa-209">Azure Disk Encryption is supported on hello following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="cbafa-210">Azure Disk şifrelemesi, Windows istemci sürümleri aşağıdaki hello üzerinde desteklenir: Windows 8 istemci ve Windows 10 istemci.</span><span class="sxs-lookup"><span data-stu-id="cbafa-210">Azure Disk Encryption is supported on hello following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-211">Windows Server 2008 R2 için .NET Framework 4.5 Azure şifreleme etkinleştirmeden önce yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="cbafa-212">Windows Update'ten hello isteğe bağlı güncelleştirme Windows Server 2008 R2 x64 tabanlı sistemler için Microsoft .NET Framework 4.5.2 yükleyerek yükleyebilirsiniz ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="cbafa-212">You can install it from Windows Update by installing hello optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="cbafa-213">Azure Disk şifrelemesi desteklenir üzerinde hello Azure Galerisi aşağıdaki Linux sunucu dağıtımları ve sürümleri göre:</span><span class="sxs-lookup"><span data-stu-id="cbafa-213">Azure Disk Encryption is supported on hello following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="cbafa-214">Linux dağıtım</span><span class="sxs-lookup"><span data-stu-id="cbafa-214">Linux Distribution</span></span> | <span data-ttu-id="cbafa-215">Sürüm</span><span class="sxs-lookup"><span data-stu-id="cbafa-215">Version</span></span> | <span data-ttu-id="cbafa-216">Şifreleme için desteklenen birim türü</span><span class="sxs-lookup"><span data-stu-id="cbafa-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="cbafa-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cbafa-217">Ubuntu</span></span> | <span data-ttu-id="cbafa-218">16.04 GÜNLÜK LTS</span><span class="sxs-lookup"><span data-stu-id="cbafa-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="cbafa-219">İşletim sistemi ve veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-219">OS and Data disk</span></span> |
| <span data-ttu-id="cbafa-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cbafa-220">Ubuntu</span></span> | <span data-ttu-id="cbafa-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="cbafa-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="cbafa-222">İşletim sistemi ve veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-222">OS and Data disk</span></span> |
| <span data-ttu-id="cbafa-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cbafa-223">Ubuntu</span></span> | <span data-ttu-id="cbafa-224">12.10</span><span class="sxs-lookup"><span data-stu-id="cbafa-224">12.10</span></span> | <span data-ttu-id="cbafa-225">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-225">Data disk</span></span> |
| <span data-ttu-id="cbafa-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cbafa-226">Ubuntu</span></span> | <span data-ttu-id="cbafa-227">12.04</span><span class="sxs-lookup"><span data-stu-id="cbafa-227">12.04</span></span> | <span data-ttu-id="cbafa-228">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-228">Data disk</span></span> |
| <span data-ttu-id="cbafa-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="cbafa-229">RHEL</span></span> | <span data-ttu-id="cbafa-230">7.3</span><span class="sxs-lookup"><span data-stu-id="cbafa-230">7.3</span></span> | <span data-ttu-id="cbafa-231">İşletim sistemi ve veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-231">OS and Data disk</span></span> |
| <span data-ttu-id="cbafa-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="cbafa-232">RHEL</span></span> | <span data-ttu-id="cbafa-233">7.2</span><span class="sxs-lookup"><span data-stu-id="cbafa-233">7.2</span></span> | <span data-ttu-id="cbafa-234">İşletim sistemi ve veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-234">OS and Data disk</span></span> |
| <span data-ttu-id="cbafa-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="cbafa-235">RHEL</span></span> | <span data-ttu-id="cbafa-236">6.8</span><span class="sxs-lookup"><span data-stu-id="cbafa-236">6.8</span></span> | <span data-ttu-id="cbafa-237">İşletim sistemi ve veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-237">OS and Data disk</span></span> |
| <span data-ttu-id="cbafa-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="cbafa-238">RHEL</span></span> | <span data-ttu-id="cbafa-239">6.7</span><span class="sxs-lookup"><span data-stu-id="cbafa-239">6.7</span></span> | <span data-ttu-id="cbafa-240">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-240">Data disk</span></span> |
| <span data-ttu-id="cbafa-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="cbafa-241">CentOS</span></span> | <span data-ttu-id="cbafa-242">7.3</span><span class="sxs-lookup"><span data-stu-id="cbafa-242">7.3</span></span> | <span data-ttu-id="cbafa-243">İşletim sistemi ve veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-243">OS and Data disk</span></span> |
| <span data-ttu-id="cbafa-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="cbafa-244">CentOS</span></span> | <span data-ttu-id="cbafa-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="cbafa-245">7.2n</span></span> | <span data-ttu-id="cbafa-246">İşletim sistemi ve veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-246">OS and Data disk</span></span> |
| <span data-ttu-id="cbafa-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="cbafa-247">CentOS</span></span> | <span data-ttu-id="cbafa-248">6.8</span><span class="sxs-lookup"><span data-stu-id="cbafa-248">6.8</span></span> | <span data-ttu-id="cbafa-249">İşletim sistemi ve veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-249">OS and Data disk</span></span> |
| <span data-ttu-id="cbafa-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="cbafa-250">CentOS</span></span> | <span data-ttu-id="cbafa-251">7.1</span><span class="sxs-lookup"><span data-stu-id="cbafa-251">7.1</span></span> | <span data-ttu-id="cbafa-252">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-252">Data disk</span></span> |
| <span data-ttu-id="cbafa-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="cbafa-253">CentOS</span></span> | <span data-ttu-id="cbafa-254">7.0</span><span class="sxs-lookup"><span data-stu-id="cbafa-254">7.0</span></span> | <span data-ttu-id="cbafa-255">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-255">Data disk</span></span> |
| <span data-ttu-id="cbafa-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="cbafa-256">CentOS</span></span> | <span data-ttu-id="cbafa-257">6.7</span><span class="sxs-lookup"><span data-stu-id="cbafa-257">6.7</span></span> | <span data-ttu-id="cbafa-258">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-258">Data disk</span></span> |
| <span data-ttu-id="cbafa-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="cbafa-259">CentOS</span></span> | <span data-ttu-id="cbafa-260">6.6</span><span class="sxs-lookup"><span data-stu-id="cbafa-260">6.6</span></span> | <span data-ttu-id="cbafa-261">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-261">Data disk</span></span> |
| <span data-ttu-id="cbafa-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="cbafa-262">CentOS</span></span> | <span data-ttu-id="cbafa-263">6.5</span><span class="sxs-lookup"><span data-stu-id="cbafa-263">6.5</span></span> | <span data-ttu-id="cbafa-264">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-264">Data disk</span></span> |
| <span data-ttu-id="cbafa-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="cbafa-265">openSUSE</span></span> | <span data-ttu-id="cbafa-266">13.2</span><span class="sxs-lookup"><span data-stu-id="cbafa-266">13.2</span></span> | <span data-ttu-id="cbafa-267">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-267">Data disk</span></span> |
| <span data-ttu-id="cbafa-268">SLES</span><span class="sxs-lookup"><span data-stu-id="cbafa-268">SLES</span></span> | <span data-ttu-id="cbafa-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="cbafa-269">12 SP1</span></span> | <span data-ttu-id="cbafa-270">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-270">Data disk</span></span> |
| <span data-ttu-id="cbafa-271">SLES</span><span class="sxs-lookup"><span data-stu-id="cbafa-271">SLES</span></span> | <span data-ttu-id="cbafa-272">12-SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="cbafa-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="cbafa-273">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-273">Data disk</span></span> |
| <span data-ttu-id="cbafa-274">SLES</span><span class="sxs-lookup"><span data-stu-id="cbafa-274">SLES</span></span> | <span data-ttu-id="cbafa-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="cbafa-275">HPC 12</span></span> | <span data-ttu-id="cbafa-276">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-276">Data disk</span></span> |
| <span data-ttu-id="cbafa-277">SLES</span><span class="sxs-lookup"><span data-stu-id="cbafa-277">SLES</span></span> | <span data-ttu-id="cbafa-278">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="cbafa-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="cbafa-279">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-279">Data disk</span></span> |
| <span data-ttu-id="cbafa-280">SLES</span><span class="sxs-lookup"><span data-stu-id="cbafa-280">SLES</span></span> | <span data-ttu-id="cbafa-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="cbafa-281">11 SP4</span></span> | <span data-ttu-id="cbafa-282">Veri diski</span><span class="sxs-lookup"><span data-stu-id="cbafa-282">Data disk</span></span> |

* <span data-ttu-id="cbafa-283">Azure Disk şifrelemesi gerektirir anahtar kasası ve VM'lerin hello aynı bulunması Azure bölgesi ve abonelik.</span><span class="sxs-lookup"><span data-stu-id="cbafa-283">Azure Disk Encryption requires that your key vault and VMs reside in hello same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-284">Bir hata, ayrı bölgelerde Hello kaynaklarını yapılandırma hello Azure Disk Şifrelemesi özelliğini etkinleştirme neden olur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-284">Configuring hello resources in separate regions causes a failure in enabling hello Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="cbafa-285">tooset yukarı ve anahtar kasanızı Azure Disk şifrelemesi için yapılandırma, bölümüne bakın **ayarlamak ayarlama ve Azure Disk şifrelemesi için anahtar kasanızı yapılandırma** hello içinde *Önkoşullar* bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-285">tooset up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="cbafa-286">tooset yukarı ve Azure AD uygulaması, Azure Disk şifrelemesi için Azure Active Directory'de yapılandırmak, bölümüne bakın **hello Azure AD uygulama Azure Active Directory'de ayarlama** hello içinde *Önkoşullar* Bu makalede bölümü.</span><span class="sxs-lookup"><span data-stu-id="cbafa-286">tooset up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up hello Azure AD application in Azure Active Directory** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="cbafa-287">tooset yukarı ve Merhaba Azure AD uygulaması için hello anahtar kasası erişim ilkesini yapılandırmak için bölümüne bakın **Merhaba Azure AD uygulaması için hello anahtar kasası erişim ilkesi ayarlama** hello içinde *Önkoşullar* bölümü Bu makalede.</span><span class="sxs-lookup"><span data-stu-id="cbafa-287">tooset up and configure hello key vault access policy for hello Azure AD application, see section **Set up hello key vault access policy for hello Azure AD application** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="cbafa-288">tooprepare önceden şifrelenmiş bir Windows VHD bölümüne bakın **önceden şifrelenmiş Windows VHD hazırlama** hello içinde *ek*.</span><span class="sxs-lookup"><span data-stu-id="cbafa-288">tooprepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="cbafa-289">tooprepare önceden şifrelenmiş bir Linux VHD bölümüne bakın **önceden şifrelenmiş Linux VHD hazırlama** hello içinde *ek*.</span><span class="sxs-lookup"><span data-stu-id="cbafa-289">tooprepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="cbafa-290">Hello Azure platformu erişim toohello şifreleme anahtarları veya anahtar kasası toomake parolalarında gereken bunları kullanılabilir toohello sanal makine önyüklenir ve hello sanal makine işletim sistemi birimi şifresini çözer.</span><span class="sxs-lookup"><span data-stu-id="cbafa-290">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello virtual machine when it boots and decrypts hello virtual machine OS volume.</span></span> <span data-ttu-id="cbafa-291">toogrant izinleri tooAzure platform, kümesi hello **EnabledForDiskEncryption** hello anahtar kasası özelliği.</span><span class="sxs-lookup"><span data-stu-id="cbafa-291">toogrant permissions tooAzure platform, set hello **EnabledForDiskEncryption** property in hello key vault.</span></span> <span data-ttu-id="cbafa-292">Daha fazla bilgi için bkz: **ayarlamak ayarlama ve Azure Disk şifrelemesi için anahtar kasanızı yapılandırma** hello ek olarak.</span><span class="sxs-lookup"><span data-stu-id="cbafa-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in hello Appendix.</span></span>
* <span data-ttu-id="cbafa-293">Anahtar kasası gizliliği ve KEK URL'leri sürümlü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="cbafa-294">Azure, bu sürüm kısıtlamasını zorlar.</span><span class="sxs-lookup"><span data-stu-id="cbafa-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="cbafa-295">Geçerli gizli ve KEK URL'ler için örnek hello bakın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-295">For valid secret and KEK URLs, see hello following examples:</span></span>

  * <span data-ttu-id="cbafa-296">Geçerli bir gizli URL örneği: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="cbafa-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="cbafa-297">Geçerli bir KEK URL örneği: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="cbafa-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="cbafa-298">Azure Disk şifrelemesi anahtar kasasına gizli anahtarları ve KEK URL'leri parçası olarak belirterek bağlantı noktası numaralarını desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="cbafa-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="cbafa-299">Desteklenmeyen ve desteklenen anahtar kasası URL'leri örnekler için hello aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-299">For examples of non-supported and supported key vault URLs, see hello following:</span></span>

  * <span data-ttu-id="cbafa-300">Kabul edilebilir anahtar kasası URL'si *https://contosovault.vault.azure.net:443/gizli/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="cbafa-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="cbafa-301">Kabul edilebilir anahtar kasası URL'si: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="cbafa-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="cbafa-302">tooenable hello Azure Disk şifrelemesi özelliği, ağ uç noktası yapılandırması gereksinimleri aşağıdaki hello hello Iaas VM'ler karşılaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="cbafa-302">tooenable hello Azure Disk Encryption feature, hello IaaS VMs must meet hello following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="cbafa-303">tooget bir belirteç tooconnect tooyour anahtar kasası, hello Iaas VM mümkün tooconnect tooan Azure Active Directory uç noktası, olmalıdır \[login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="cbafa-303">tooget a token tooconnect tooyour key vault, hello IaaS VM must be able tooconnect tooan Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="cbafa-304">toowrite hello şifreleme anahtarları tooyour anahtar kasası, hello Iaas VM mümkün tooconnect toohello anahtar kasası uç noktası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-304">toowrite hello encryption keys tooyour key vault, hello IaaS VM must be able tooconnect toohello key vault endpoint.</span></span>
  * <span data-ttu-id="cbafa-305">Merhaba Iaas VM konakları Azure uzantısı depo ve ana VHD dosyaları hello Azure storage hesabı hello mümkün tooconnect tooan Azure storage uç olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-305">hello IaaS VM must be able tooconnect tooan Azure storage endpoint that hosts hello Azure extension repository and an Azure storage account that hosts hello VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="cbafa-306">Güvenlik ilkeniz Azure Vm'leri toohello Internet erişimi sınırlar, URI önceki hello çözün ve bir özel kural tooallow giden bağlantı toohello IP'leri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-306">If your security policy limits access from Azure VMs toohello Internet, you can resolve hello preceding URI and configure a specific rule tooallow outbound connectivity toohello IPs.</span></span>
  >
  ><span data-ttu-id="cbafa-307">tooconfigure ve erişim Azure anahtar kasası (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall) bir güvenlik duvarının arkasında</span><span class="sxs-lookup"><span data-stu-id="cbafa-307">tooconfigure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="cbafa-308">Azure PowerShell SDK sürüm tooconfigure Azure Disk şifrelemesi Hello en son sürümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-308">Use hello latest version of Azure PowerShell SDK version tooconfigure Azure Disk Encryption.</span></span> <span data-ttu-id="cbafa-309">Merhaba en son sürümünü indirme [Azure PowerShell sürüm](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="cbafa-309">Download hello latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="cbafa-310">Azure Disk şifrelemesi desteklenmiyor [Azure PowerShell SDK sürüm 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="cbafa-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="cbafa-311">Bir hata alıyorsanız toousing Azure PowerShell 1.1.0, ilgili görmek [Azure Disk şifrelemesi ilgili hata tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbafa-311">If you are receiving an error related toousing Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="cbafa-312">toorun herhangi bir Azure CLI komutu ve Azure aboneliğinizle ilişkilendirmek, Azure CLI yüklemelisiniz:</span><span class="sxs-lookup"><span data-stu-id="cbafa-312">toorun any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="cbafa-313">tooinstall Azure CLI ve Azure aboneliğinizle ilişkilendirmek için bkz: [nasıl tooinstall ve Azure CLI yapılandırma](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cbafa-313">tooinstall Azure CLI and associate it with your Azure subscription, see [How tooinstall and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="cbafa-314">toouse Mac, Linux ve Windows Azure Resource Manager ile Azure CLI bkz [Kaynak Yöneticisi modunda Azure CLI komutları](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="cbafa-314">toouse Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="cbafa-315">Yönetilen bir disk şifreleme zorunlu önkoşul tootake yönetilen hello diskin anlık görüntüsünü veya Azure Disk şifrelemesi önceki tooenabling şifreleme dışında hello disk yedeğini olur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-315">When encrypting a managed disk, it is mandatory prerequisite tootake a snapshot of hello managed disk or a backup of hello disk outside of Azure Disk Encryption prior tooenabling encryption.</span></span>  <span data-ttu-id="cbafa-316">Yerinde bir yedekleme olmadan şifreleme sırasında beklenmeyen bir hata hello disk ve VM kurtarma seçeneği olmaksızın erişilemez hale getirebilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-316">Without a backup in place, any unexpected failure during encryption may render hello disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="cbafa-317">Set-AzureRmVMDiskEncryptionExtension şu anda yönetilen diskleri yedekleme ve hata hello - skipVmBackup parametresini belirtmediyseniz yönetilen bir diske karşı kullandıysanız çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless hello -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="cbafa-318">Bir yedekleme Azure Disk şifrelemesi dışında kılmadığınız sürece bu parametre güvensiz toouse olur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-318">This parameter is unsafe toouse unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="cbafa-319">Merhaba - skipVmBackup parametresi belirtildiğinde, hello cmdlet yönetilen hello disk önceki tooencryption yedeğini yapmaz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-319">When hello -skipVmBackup parameter is specified, hello cmdlet will not make a backup of hello managed disk prior tooencryption.</span></span>  <span data-ttu-id="cbafa-320">Bu nedenle, bir zorunlu önkoşul toomake kurtarma sonraki olması durumunda VM yer önceki tooenabling Azure Disk şifrelemesi hello yönetilen disk yedeğini gerekli emin olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-320">For this reason, it is considered a mandatory prerequisite toomake sure a backup of hello managed disk VM is in place prior tooenabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="cbafa-321">Azure Disk şifrelemesi dışında bir anlık görüntü veya yedekleme zaten yapılmış sürece hello - skipVmBackup parametresi hiçbir zaman kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-321">hello -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="cbafa-322">Hello Azure Disk şifrelemesi çözüm hello BitLocker dış anahtar koruyucusu Windows Iaas VM'ler için kullanır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-322">hello Azure Disk Encryption solution uses hello BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="cbafa-323">Etki alanı için TPM koruyucusu zorla tüm grup ilkeleri birleştirilmiş VM'ler, vermeyin iletin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="cbafa-324">"Uyumlu TPM'siz BitLocker izin ver" Merhaba Grup İlkesi hakkında bilgi için bkz: [BitLocker Grup İlkesi başvurusu](https://technet.microsoft.com/library/ee706521).</span><span class="sxs-lookup"><span data-stu-id="cbafa-324">For information about hello group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="cbafa-325">Özel Grup İlkesi ile etki alanına katılmış sanal makinelerde BitLocker İlkesi ayarı aşağıdaki hello içermelidir: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` Bitlocker için özel Grup İlkesi ayarları uyumsuz olduğunda Azure Disk şifrelemesi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-325">Bitlocker policy on domain joined virtual machines with custom group policy must include hello following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="cbafa-326">Merhaba sahip değilse makinelerde hello yeni ilke tooupdate (gpupdate.exe/Force) zorlama ve yeniden başlatarak hello yeni ilke, uygulama doğru ilke ayarı, gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-326">On machines that did not have hello correct policy setting, applying hello new policy, forcing hello new policy tooupdate (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="cbafa-327">toocreate Azure AD uygulaması, bir anahtar kasası oluşturma veya varolan bir anahtar kasasını oluşturup ve şifrelemeyi etkinleştirmek, hello bkz [Azure Disk şifrelemesi önkoşul PowerShell Betiği](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="cbafa-327">toocreate an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see hello [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="cbafa-328">Hello Azure CLI kullanarak tooconfigure disk şifrelemesi önkoşulları bkz [bu Bash betik](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="cbafa-328">tooconfigure disk-encryption prerequisites using hello Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="cbafa-329">toouse hello Azure Backup hizmeti tooback yukarı ve şifreleme Azure Disk şifrelemesi ile etkinleştirilmişse, şifrelenmiş geri yükleme VM'ler Vm'leriniz hello Azure Disk şifrelemesi anahtar yapılandırmayı kullanarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="cbafa-329">toouse hello Azure Backup service tooback up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using hello Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="cbafa-330">Merhaba Backup hizmeti yalnızca KEK yapılandırma kullanılarak şifrelenmiş Vm'leri destekler.</span><span class="sxs-lookup"><span data-stu-id="cbafa-330">hello Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="cbafa-331">Bkz: [tooback yedeklemek ve geri yükleme Azure yedekleme şifreleme ile sanal makineleri nasıl şifrelenmiş](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="cbafa-331">See [How tooback up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="cbafa-332">Linux işletim sistemi birimi şifrelerken VM yeniden başlatma hello hello işleminin sonunda şu anda gerekli olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-332">When encrypting a Linux OS volume, note that a VM restart is currently required at hello end of hello process.</span></span> <span data-ttu-id="cbafa-333">Bu hello portal, powershell veya CLI yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-333">This can be done via hello portal, powershell, or CLI.</span></span>   <span data-ttu-id="cbafa-334">Şifreleme tootrack hello ilerlemesini, Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus tarafından döndürülen hello durum iletisi düzenli aralıklarla yoklar.</span><span class="sxs-lookup"><span data-stu-id="cbafa-334">tootrack hello progress of encryption, periodically poll hello status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="cbafa-335">Şifreleme işlemi tamamlandıktan sonra bu komutu tarafından döndürülen hello hello durum iletisi bunun belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-335">Once encryption is complete, hello hello status message returned by this command will indicate this.</span></span>  <span data-ttu-id="cbafa-336">Örneğin, "ProgressMessage: işletim sistemi diski başarıyla şifrelendi, lütfen hello VM yeniden başlatma" VM yeniden ve kullanılan bu noktası hello adresindeki.</span><span class="sxs-lookup"><span data-stu-id="cbafa-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot hello VM"  At this point hello VM can be restarted and used.</span></span>  

* <span data-ttu-id="cbafa-337">Veri diskleri toohave Linux önceki tooencryption bağlı dosya sisteminde Linux için Azure Disk şifrelemesi gerektirir</span><span class="sxs-lookup"><span data-stu-id="cbafa-337">Azure Disk Encryption for Linux requires data disks toohave a mounted file system in Linux prior tooencryption</span></span>

* <span data-ttu-id="cbafa-338">Yinelemeli olarak bağlı veri diskleri için Linux hello Azure Disk Şifrelemesi tarafından desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="cbafa-338">Recursively mounted data disks are not supported by hello Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="cbafa-339">Örneğin, Merhaba, hedef sistemin bir disk üzerinde /foo/bar bağladı ve ardından başka bir /foo/bar/baz, /foo/bar/baz hello şifrelenmesi başarılı olur ancak şifreleme/foo/çubuğunun başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-339">For example, if hello target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, hello encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="cbafa-340">Azure Disk şifrelemesi yalnızca hello daha önce bahsedilen önkoşulları karşılayan desteklenen Azure galeri görüntüleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet hello aforementioned prerequisites.</span></span> <span data-ttu-id="cbafa-341">Müşteri özel resimler son toocustom bölümleme şeması ve bu görüntülerinde bulunabilecek işlemi davranışları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="cbafa-341">Customer custom images are not supported due toocustom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="cbafa-342">Ayrıca, hatta galeri görüntüsü başlangıçta önkoşulların ancak oluşturma uyumsuz sonra değiştirilmiş VM'in temel.</span><span class="sxs-lookup"><span data-stu-id="cbafa-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="cbafa-343">İçin nedeni, bir Linux VM şifrelemek için yordamı hello önerilen bir temiz galeri görüntüsünden toostart olduğundan, hello VM şifrelemek ve ardından özel yazılım ya da veri toohello gerektiği gibi VM ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-343">For that reason, hello suggested procedure for encrypting a Linux VM is toostart from a clean gallery image, encrypt hello VM, and then add custom software or data toohello VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="cbafa-344">Yedekleme ve geri yükleme şifrelenmiş VM'lerin hello KEK yapılandırmayla şifrelenmiş VM'ler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="cbafa-345">KEK şifrelenmiş vm'lerde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="cbafa-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="cbafa-346">KEK VM sağlayan isteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="cbafa-347">Hello Azure Active Directory'de Azure AD uygulaması ayarlayın</span><span class="sxs-lookup"><span data-stu-id="cbafa-347">Set up hello Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="cbafa-348">Azure'da çalışan bir VM etkin şifreleme toobe gerektiğinde Azure Disk şifrelemesi oluşturur ve hello şifreleme anahtarları tooyour anahtar kasası yazar.</span><span class="sxs-lookup"><span data-stu-id="cbafa-348">When you need encryption toobe enabled on a running VM in Azure, Azure Disk Encryption generates and writes hello encryption keys tooyour key vault.</span></span> <span data-ttu-id="cbafa-349">Anahtar kasanızı şifreleme anahtarlarını yönetme, Azure AD kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="cbafa-350">Bu amaç için Azure AD uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbafa-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="cbafa-351">Uygulama hello "Merhaba uygulama için bir kimlik Get" bölümünde hello blog gönderisi kaydetme için ayrıntılı adımlar bulabilirsiniz [Azure anahtar kasası - adım adım](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbafa-351">You can find detailed steps for registering an application in hello “Get an Identity for hello Application” section of hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="cbafa-352">Bu post ayarlama ve anahtar kasanızı yapılandırma için yararlı örnekler sayısı da içerir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="cbafa-353">Kimlik doğrulama amacıyla istemci gizli anahtarı tabanlı kimlik doğrulaması veya istemci Azure AD sertifika tabanlı kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="cbafa-354">Azure AD için istemci gizli anahtarı tabanlı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cbafa-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="cbafa-355">izleyin hello bölümler bir istemci gizli anahtarı tabanlı kimlik doğrulaması için Azure AD yapılandırmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-355">hello sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="cbafa-356">Azure PowerShell kullanarak Azure AD uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbafa-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="cbafa-357">PowerShell cmdlet toocreate Azure AD uygulaması aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="cbafa-357">Use hello following PowerShell cmdlet toocreate an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="cbafa-358">$azureAdApplication.ApplicationId hello Azure AD ClientID ve $aadClientSecret hello istemci parolası sonraki tooenable Azure Disk şifrelemesi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-358">$azureAdApplication.ApplicationId is hello Azure AD ClientID and $aadClientSecret is hello client secret that you should use later tooenable Azure Disk Encryption.</span></span> <span data-ttu-id="cbafa-359">Hello Azure AD gizli uygun şekilde koruyun.</span><span class="sxs-lookup"><span data-stu-id="cbafa-359">Safeguard hello Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a><span data-ttu-id="cbafa-360">Hello Azure AD istemci kimliği ve parolası hello Klasik Azure Portalı ' ayarlama</span><span class="sxs-lookup"><span data-stu-id="cbafa-360">Setting up hello Azure AD client ID and secret from hello Azure classic portal</span></span>
<span data-ttu-id="cbafa-361">Hello kullanarak Azure AD İstemci Kimliğini ve parolasını de ayarlayabilirsiniz [Klasik Azure portalı]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="cbafa-361">You can also set up your Azure AD client ID and secret by using hello [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="cbafa-362">tooperform bu görev, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="cbafa-362">tooperform this task, do hello following:</span></span>

1. <span data-ttu-id="cbafa-363">Merhaba tıklatın **Active Directory** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="cbafa-363">Click hello **Active Directory** tab.</span></span>

 ![Azure Disk Şifrelemesi](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="cbafa-365">Tıklatın **uygulama Ekle**ve ardından türü hello uygulama adı.</span><span class="sxs-lookup"><span data-stu-id="cbafa-365">Click **Add Application**, and then type hello application name.</span></span>

 ![Azure Disk Şifrelemesi](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="cbafa-367">Hello ok düğmesine tıklayın ve ardından hello uygulama özelliklerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-367">Click hello arrow button, and then configure hello application properties.</span></span>

 ![Azure Disk Şifrelemesi](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="cbafa-369">Merhaba alt sol köşe toofinish Hello onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-369">Click hello check mark in hello lower left corner toofinish.</span></span> <span data-ttu-id="cbafa-370">Merhaba uygulama yapılandırma sayfası görünür ve hello Azure AD istemci kimliği hello sayfasının hello altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-370">hello application configuration page appears, and hello Azure AD client ID is displayed at hello bottom of hello page.</span></span>

 ![Azure Disk Şifrelemesi](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="cbafa-372">Merhaba tıklayarak Hello Azure AD gizli Kaydet **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cbafa-372">Save hello Azure AD client secret by clicking hello **Save** button.</span></span> <span data-ttu-id="cbafa-373">Merhaba anahtarları metin kutusuna Hello Azure AD gizli unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-373">Note hello Azure AD client secret in hello keys text box.</span></span> <span data-ttu-id="cbafa-374">Uygun şekilde koruyun.</span><span class="sxs-lookup"><span data-stu-id="cbafa-374">Safeguard it appropriately.</span></span>

 ![Azure Disk Şifrelemesi](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="cbafa-376">Akış önceki hello hello Klasik Azure portalı üzerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="cbafa-376">hello preceding flow is not supported on hello Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="cbafa-377">Varolan bir uygulama kullanın</span><span class="sxs-lookup"><span data-stu-id="cbafa-377">Use an existing application</span></span>
<span data-ttu-id="cbafa-378">tooexecute komutları aşağıdaki Merhaba, elde edilir ve hello [Azure AD PowerShell Modülü](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbafa-378">tooexecute hello following commands, obtain and use hello [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-379">Merhaba aşağıdaki komutları yeni bir PowerShell penceresinden yürütülmelidir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-379">hello following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="cbafa-380">Azure PowerShell veya hello Azure Resource Manager penceresi tooexecute hello komutları kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-380">Do not use Azure PowerShell or hello Azure Resource Manager window tooexecute hello commands.</span></span> <span data-ttu-id="cbafa-381">Bu cmdlet'ler hello MSOnline modül veya Azure AD PowerShell olduğundan bu yaklaşım öneririz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-381">We recommend this approach because these cmdlets are in hello MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="cbafa-382">Azure AD için sertifika tabanlı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cbafa-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="cbafa-383">Azure AD sertifika tabanlı kimlik doğrulaması Linux VM'ler üzerinde şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="cbafa-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="cbafa-384">Merhaba Göster nasıl izleyen bölümlerde tooconfigure bir sertifika tabanlı kimlik doğrulaması için Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbafa-384">hello sections that follow show how tooconfigure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="cbafa-385">Azure AD uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="cbafa-385">Create an Azure AD application</span></span>
<span data-ttu-id="cbafa-386">toocreate Azure AD uygulaması, PowerShell cmdlet'leri aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="cbafa-386">toocreate an Azure AD application, execute hello following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-387">Merhaba aşağıdaki değiştirin `yourpassword` , güvenli parola ve koruma hello parolayı dize.</span><span class="sxs-lookup"><span data-stu-id="cbafa-387">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="cbafa-388">Bu adımı tamamladıktan sonra bir PFX dosyası tooyour anahtar kasası karşıya yükleyin ve bu sertifikayı tooa VM hello erişim gerektirdiği ilke toodeploy etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-388">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy needed toodeploy that certificate tooa VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="cbafa-389">Var olan Azure AD uygulaması kullanın</span><span class="sxs-lookup"><span data-stu-id="cbafa-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="cbafa-390">Sertifika tabanlı kimlik doğrulaması olan bir uygulamanın yapılandırıyorsanız, burada gösterilen hello PowerShell cmdlet'lerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-390">If you are configuring certificate-based authentication for an existing application, use hello PowerShell cmdlets shown here.</span></span> <span data-ttu-id="cbafa-391">Emin tooexecute olması atamalarını yeni bir PowerShell penceresi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-391">Be sure tooexecute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="cbafa-392">Bu adımı tamamladıktan sonra bir PFX dosyası tooyour anahtar kasası karşıya yükleme ve toodeploy hello sertifika tooa VM gerekli olan hello erişim ilkesini etkinleştir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-392">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy that's needed toodeploy hello certificate tooa VM.</span></span>

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a><span data-ttu-id="cbafa-393">Bir PFX dosyası tooyour anahtar kasası karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="cbafa-393">Upload a PFX file tooyour key vault</span></span>
<span data-ttu-id="cbafa-394">Bu işlem ayrıntılı bir açıklaması için bkz: [resmi Azure anahtar kasası ekip blogu hello](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbafa-394">For a detailed explanation of this process, see [hello Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="cbafa-395">Ancak, PowerShell cmdlet'leri aşağıdaki hello hello görev için gereken her şeyi değildir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-395">However, hello following PowerShell cmdlets are all you need for hello task.</span></span> <span data-ttu-id="cbafa-396">Emin tooexecute olması bunları Azure PowerShell konsolundan.</span><span class="sxs-lookup"><span data-stu-id="cbafa-396">Be sure tooexecute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-397">Merhaba aşağıdaki değiştirin `yourpassword` , güvenli parola ve koruma hello parolayı dize.</span><span class="sxs-lookup"><span data-stu-id="cbafa-397">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a><span data-ttu-id="cbafa-398">Var olan VM, anahtar kasası tooan sertifikada dağıtma</span><span class="sxs-lookup"><span data-stu-id="cbafa-398">Deploy a certificate in your key vault tooan existing VM</span></span>
<span data-ttu-id="cbafa-399">Merhaba PFX yüklemeyi tamamladıktan sonra VM hello aşağıdakilerle varolan hello anahtar kasası tooan sertifikada dağıtın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-399">After you finish uploading hello PFX, deploy a certificate in hello key vault tooan existing VM with hello following:</span></span>
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a><span data-ttu-id="cbafa-400">Merhaba Azure AD uygulaması için hello anahtar kasası erişim ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="cbafa-400">Set up hello key vault access policy for hello Azure AD application</span></span>
<span data-ttu-id="cbafa-401">Azure AD uygulaması hakları tooaccess hello anahtarları veya hello kasadaki gizli anahtarları gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="cbafa-401">Your Azure AD application needs rights tooaccess hello keys or secrets in hello vault.</span></span> <span data-ttu-id="cbafa-402">Kullanım hello [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) (Merhaba uygulaması kaydolurken oluşturuldu) hello istemci kimliği hello kullanarak cmdlet toogrant izinleri toohello uygulaması, _– ServicePrincipalName_ parametre değeri.</span><span class="sxs-lookup"><span data-stu-id="cbafa-402">Use hello [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissions toohello application, using hello client ID (which was generated when hello application was registered) as hello _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="cbafa-403">toolearn daha hello blog yayınına bakın [Azure anahtar kasası - adım adım](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbafa-403">toolearn more, see hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="cbafa-404">İşte tooperform bu nasıl görev aracılığıyla, bir örnek PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cbafa-404">Here is an example of how tooperform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="cbafa-405">Azure Disk şifrelemesi erişim ilkeleri tooyour Azure AD istemci uygulaması aşağıdaki tooconfigure hello gerektirir: _WrapKey_ ve _ayarlamak_ izinleri.</span><span class="sxs-lookup"><span data-stu-id="cbafa-405">Azure Disk Encryption requires you tooconfigure hello following access policies tooyour Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="cbafa-406">Terminoloji</span><span class="sxs-lookup"><span data-stu-id="cbafa-406">Terminology</span></span>
<span data-ttu-id="cbafa-407">Merhaba Ortak terimleri bazıları bu teknoloji, aşağıdaki terimler tablonun kullanım hello tarafından kullanılan toounderstand:</span><span class="sxs-lookup"><span data-stu-id="cbafa-407">toounderstand some of hello common terms used by this technology, use hello following terminology table:</span></span>

| <span data-ttu-id="cbafa-408">Terminoloji</span><span class="sxs-lookup"><span data-stu-id="cbafa-408">Terminology</span></span> | <span data-ttu-id="cbafa-409">Tanım</span><span class="sxs-lookup"><span data-stu-id="cbafa-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="cbafa-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbafa-410">Azure AD</span></span> | <span data-ttu-id="cbafa-411">Azure ad [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="cbafa-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="cbafa-412">Bir Azure AD hesabının kimlik doğrulaması, depolama ve gizli anahtar Kasası'nı almak için bir önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="cbafa-413">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="cbafa-413">Azure Key Vault</span></span> | <span data-ttu-id="cbafa-414">Anahtar kasası, şifreleme anahtarlarını ve gizli gizli korumaya yardımcı olmak Federal Bilgi işleme standartları FIPS doğrulamalı donanım güvenlik modülleri üzerinde temel bir şifreleme, anahtar yönetim hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="cbafa-415">Daha fazla bilgi için bkz: [anahtar kasası](https://azure.microsoft.com/services/key-vault/) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="cbafa-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="cbafa-416">ARM</span><span class="sxs-lookup"><span data-stu-id="cbafa-416">ARM</span></span> | <span data-ttu-id="cbafa-417">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cbafa-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="cbafa-418">BitLocker'ı</span><span class="sxs-lookup"><span data-stu-id="cbafa-418">BitLocker</span></span> |<span data-ttu-id="cbafa-419">[BitLocker'ı](https://technet.microsoft.com/library/hh831713.aspx) tooenable disk şifrelemesi Windows Iaas sanal makinelerin kullandığı bir endüstri tanınan Windows birim şifreleme teknolojisidir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used tooenable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="cbafa-420">BEK</span><span class="sxs-lookup"><span data-stu-id="cbafa-420">BEK</span></span> | <span data-ttu-id="cbafa-421">BitLocker şifreleme anahtarları kullanılan tooencrypt hello işletim sistemi önyükleme birimi ve veri birimlerini ' dir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-421">BitLocker encryption keys are used tooencrypt hello OS boot volume and data volumes.</span></span> <span data-ttu-id="cbafa-422">Merhaba BitLocker anahtarları anahtar kasasına gizli korunur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-422">hello BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="cbafa-423">CLI</span><span class="sxs-lookup"><span data-stu-id="cbafa-423">CLI</span></span> | <span data-ttu-id="cbafa-424">Bkz: [Azure komut satırı arabirimi](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cbafa-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="cbafa-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="cbafa-425">DM-Crypt</span></span> |<span data-ttu-id="cbafa-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) tooenable disk şifrelemesi Linux Iaas VM'ler üzerinde kullanılan hello Linux tabanlı, saydam disk şifreleme alt sistemi.</span><span class="sxs-lookup"><span data-stu-id="cbafa-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is hello Linux-based, transparent disk-encryption subsystem that's used tooenable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="cbafa-427">KEK</span><span class="sxs-lookup"><span data-stu-id="cbafa-427">KEK</span></span> | <span data-ttu-id="cbafa-428">Anahtar şifreleme anahtarı tooprotect kullanın veya hello gizli sarmalamak hello asimetrik (RSA 2048) anahtardır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-428">Key encryption key is hello asymmetric key (RSA 2048) that you can use tooprotect or wrap hello secret.</span></span> <span data-ttu-id="cbafa-429">Bir donanım güvenlik modülleri (HSM) sağlayabilir-korumalı anahtar veya yazılım korumalı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="cbafa-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="cbafa-430">Daha fazla ayrıntı için bkz: [Azure anahtar kasası](https://azure.microsoft.com/services/key-vault/) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="cbafa-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="cbafa-431">PS cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="cbafa-431">PS cmdlets</span></span> | <span data-ttu-id="cbafa-432">Bkz: [Azure PowerShell cmdlet'lerini](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cbafa-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="cbafa-433">Ayarlama ve anahtar kasanızı Azure Disk şifrelemesi için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cbafa-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="cbafa-434">Azure Disk şifrelemesi koruma hello disk şifreleme anahtarları ve anahtar kasanızdaki gizli anahtarları yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-434">Azure Disk Encryption helps safeguard hello disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="cbafa-435">tooset anahtar kasanızı Azure Disk şifrelemesi için yukarı tam hello her hello bölümleri aşağıdaki adımları.</span><span class="sxs-lookup"><span data-stu-id="cbafa-435">tooset up your key vault for Azure Disk Encryption, complete hello steps in each of hello following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="cbafa-436">Bir anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbafa-436">Create a key vault</span></span>
<span data-ttu-id="cbafa-437">toocreate bir anahtar kasası seçenekleri aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-437">toocreate a key vault, use one of hello following options:</span></span>

* [<span data-ttu-id="cbafa-438">"101-anahtar-kasa-" Resource Manager şablonu oluştur</span><span class="sxs-lookup"><span data-stu-id="cbafa-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="cbafa-439">Azure PowerShell anahtar kasası cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="cbafa-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="cbafa-440">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cbafa-440">Azure Resource Manager</span></span>
* <span data-ttu-id="cbafa-441">Nasıl çok[anahtar kasanızı güvenli](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="cbafa-441">How too[Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-442">Aboneliğiniz için bir anahtar kasasını zaten ayarladıysanız toohello sonraki bölüme atlayın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-442">If you have already set up a key vault for your subscription, skip toohello next section.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="cbafa-444">Bir anahtar şifreleme anahtarı (isteğe bağlı) ayarlama</span><span class="sxs-lookup"><span data-stu-id="cbafa-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="cbafa-445">Ek bir hello BitLocker şifreleme anahtarları için güvenlik katmanı için toouse bir KEK istiyorsanız bir KEK tooyour anahtar kasası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-445">If you want toouse a KEK for an additional layer of security for hello BitLocker encryption keys, add a KEK tooyour key vault.</span></span> <span data-ttu-id="cbafa-446">Kullanım hello [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate hello anahtar kasasına bir anahtar şifreleme anahtarı.</span><span class="sxs-lookup"><span data-stu-id="cbafa-446">Use hello [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate a key encryption key in hello key vault.</span></span> <span data-ttu-id="cbafa-447">Ayrıca, şirket içi Anahtar Yönetimi'nden HSM bir KEK içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="cbafa-448">Daha fazla ayrıntı için bkz: [anahtar kasası belgelerine](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="cbafa-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="cbafa-449">Anahtar kasası arabirimi kullanarak veya tooAzure Resource Manager giderek hello KEK ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-449">You can add hello KEK by going tooAzure Resource Manager or by using your key vault interface.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="cbafa-451">Anahtar kasası izinleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="cbafa-451">Set key vault permissions</span></span>
<span data-ttu-id="cbafa-452">Hello Azure platformu erişim toohello şifreleme anahtarları veya anahtar kasası toomake parolalarında gereken bunları kullanılabilir toohello önyüklenmesini ve hello birimleri şifresini çözmek için VM.</span><span class="sxs-lookup"><span data-stu-id="cbafa-452">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello VM for booting and decrypting hello volumes.</span></span> <span data-ttu-id="cbafa-453">toogrant izinleri toohello Azure platformu kümesi hello **EnabledForDiskEncryption** hello anahtar özelliğinde kasa hello anahtar kasası PowerShell cmdlet'ini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="cbafa-453">toogrant permissions toohello Azure platform, set hello **EnabledForDiskEncryption** property in hello key vault by using hello key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="cbafa-454">Merhaba de ayarlayabilirsiniz **EnabledForDiskEncryption** hello ziyaret özelliğini [Azure kaynak Gezgini](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cbafa-454">You can also set hello **EnabledForDiskEncryption** property by visiting hello [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="cbafa-455">Daha önce belirtildiği gibi hello ayarlamalısınız **EnabledForDiskEncryption** anahtar kasanızı özelliği.</span><span class="sxs-lookup"><span data-stu-id="cbafa-455">As mentioned earlier, you must set hello **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="cbafa-456">Aksi takdirde hello dağıtım başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-456">Otherwise, hello deployment will fail.</span></span>

<span data-ttu-id="cbafa-457">Aşağıda gösterildiği gibi Azure AD uygulamanız hello anahtar kasası arabiriminden için erişim ilkeleri ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cbafa-457">You can set up access policies for your Azure AD application from hello key vault interface, as shown here:</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="cbafa-460">Merhaba üzerinde **Gelişmiş erişim ilkeleri** sekmesinde, anahtar kasanızı Azure Disk şifrelemesi için etkinleştirildiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="cbafa-460">On hello **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Azure anahtar kasası](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="cbafa-462">Disk şifrelemesi dağıtım senaryoları ve kullanıcı deneyimleri</span><span class="sxs-lookup"><span data-stu-id="cbafa-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="cbafa-463">Çok sayıda disk şifrelemesi senaryolarına olanak sağlayabilirsiniz ve hello adımlar according toohello senaryo değişebilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-463">You can enable many disk-encryption scenarios, and hello steps may vary according toohello scenario.</span></span> <span data-ttu-id="cbafa-464">Merhaba aşağıdaki bölümlerde daha ayrıntılı hello senaryoları kapsar.</span><span class="sxs-lookup"><span data-stu-id="cbafa-464">hello following sections cover hello scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a><span data-ttu-id="cbafa-465">Market hello oluşturulan yeni Iaas VM'ler şifrelemeyi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-465">Enable encryption on new IaaS VMs that are created from hello Marketplace</span></span>
<span data-ttu-id="cbafa-466">Disk şifrelemesi'hello Azure Marketi'nde yeni Iaas Windows VM'den hello kullanarak etkinleştirebilirsiniz [Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="cbafa-466">You can enable disk encryption on new IaaS Windows VM from hello Marketplace in Azure by using hello  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="cbafa-467">Hello Azure hızlı başlangıç şablonuna tıklayın **tooAzure dağıtmak**, hello şifreleme yapılandırması üzerinde hello girin **parametreleri** dikey ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="cbafa-467">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="cbafa-468">Merhaba abonelik, kaynak grubu, kaynak grubu konumu, yasal koşulları ve anlaşma seçin ve ardından **oluşturma** yeni bir Iaas VM tooenable şifreleme.</span><span class="sxs-lookup"><span data-stu-id="cbafa-468">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-469">Bu şablon, yeni bir şifrelenmiş Windows hello Windows Server 2012 galeri görüntüsü kullanan VM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-469">This template creates a new encrypted Windows VM that uses hello Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="cbafa-470">Bu kullanarak yeni bir Iaas RedHat Linux 7.2 VM 200 GB RAID-0 diziye sahip disk şifrelemeyi etkinleştirebilirsiniz [Resource Manager şablonu](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="cbafa-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="cbafa-471">Merhaba şablon dağıttıktan sonra hello kullanarak hello VM şifreleme durumunu doğrulamak `Get-AzureRmVmDiskEncryptionStatus` açıklandığı gibi cmdlet [şifreleme işletim sistemi üzerinde çalışan bir Linux VM sürücü](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="cbafa-471">After you deploy hello template, verify hello VM encryption status by using hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="cbafa-472">Merhaba makine durumu döndüğünde _VMRestartPending_, hello VM yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-472">When hello machine returns a status of _VMRestartPending_, restart hello VM.</span></span>

<span data-ttu-id="cbafa-473">Merhaba aşağıdaki tabloda hello Resource Manager şablonu parametreleri hello Market senaryodan Azure AD İstemci Kimliğini kullanarak yeni VM'ler listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="cbafa-473">hello following table lists hello Resource Manager template parameters for new VMs from hello Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="cbafa-474">Parametre</span><span class="sxs-lookup"><span data-stu-id="cbafa-474">Parameter</span></span> | <span data-ttu-id="cbafa-475">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cbafa-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cbafa-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="cbafa-476">adminUserName</span></span> | <span data-ttu-id="cbafa-477">Merhaba sanal makine için yönetici kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="cbafa-477">Admin user name for hello virtual machine.</span></span> |
| <span data-ttu-id="cbafa-478">Admınpassword</span><span class="sxs-lookup"><span data-stu-id="cbafa-478">adminPassword</span></span> | <span data-ttu-id="cbafa-479">Merhaba sanal makine için yönetici kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="cbafa-479">Admin user password for hello virtual machine.</span></span> |
| <span data-ttu-id="cbafa-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="cbafa-480">newStorageAccountName</span></span> | <span data-ttu-id="cbafa-481">Merhaba depolama hesabı toostore işletim sistemi ve veri VHD'ler adı.</span><span class="sxs-lookup"><span data-stu-id="cbafa-481">Name of hello storage account toostore OS and data VHDs.</span></span> |
| <span data-ttu-id="cbafa-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="cbafa-482">vmSize</span></span> | <span data-ttu-id="cbafa-483">Merhaba VM boyutu.</span><span class="sxs-lookup"><span data-stu-id="cbafa-483">Size of hello VM.</span></span> <span data-ttu-id="cbafa-484">Şu anda yalnızca standart bir, D ve G serisi desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="cbafa-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="cbafa-485">virtualNetworkName</span></span> | <span data-ttu-id="cbafa-486">Merhaba VNet bu hello VM NIC adını ait.</span><span class="sxs-lookup"><span data-stu-id="cbafa-486">Name of hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="cbafa-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="cbafa-487">subnetName</span></span> | <span data-ttu-id="cbafa-488">Merhaba VNet bu hello VM NIC hello alt ağ adı için ait olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-488">Name of hello subnet in hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="cbafa-489">Aadclientıd</span><span class="sxs-lookup"><span data-stu-id="cbafa-489">AADClientID</span></span> | <span data-ttu-id="cbafa-490">İzinleri toowrite gizli tooyour anahtar kasası olan hello Azure AD uygulama istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="cbafa-490">Client ID of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="cbafa-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="cbafa-491">AADClientSecret</span></span> | <span data-ttu-id="cbafa-492">İzinleri toowrite gizli tooyour anahtar kasası olan hello Azure AD uygulama istemci gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="cbafa-492">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="cbafa-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="cbafa-493">keyVaultURL</span></span> | <span data-ttu-id="cbafa-494">Başlangıç anahtarı URL'sini kasa bu hello BitLocker anahtarını karşıya yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-494">URL of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="cbafa-495">Merhaba cmdlet'ini kullanarak elde edebilirsiniz `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="cbafa-495">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="cbafa-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="cbafa-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="cbafa-497">Kullanılan tooencrypt hello hello anahtar şifreleme anahtarı URL'sini (isteğe bağlı) BitLocker anahtarı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-497">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="cbafa-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cbafa-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="cbafa-499">Merhaba anahtar kasasının kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="cbafa-499">Resource group of hello key vault.</span></span> |
| <span data-ttu-id="cbafa-500">vmName</span><span class="sxs-lookup"><span data-stu-id="cbafa-500">vmName</span></span> | <span data-ttu-id="cbafa-501">Üzerinde gerçekleştirilen toobe hello şifreleme işlemi hello VM adıdır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-501">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="cbafa-502">_KeyEncryptionKeyURL_ isteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="cbafa-503">Anahtar kasanızı kendi KEK toofurther koruma hello veri şifreleme anahtarı (parola gizli) kullanıma sunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-503">You can bring your own KEK toofurther safeguard hello data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="cbafa-504">VHD müşteri şifrelenmiş ve şifreleme anahtarlarını oluşturulan yeni Iaas VM'ler şifrelemeyi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="cbafa-505">Bu senaryoda, hello Resource Manager şablonu, PowerShell cmdlet'leri veya CLI komutları kullanarak şifreleme etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-505">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="cbafa-506">Merhaba aşağıdaki bölümlerde daha fazla ayrıntı hello Resource Manager şablonu ve CLI komutları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-506">hello following sections explain in greater detail hello Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="cbafa-507">Azure'da kullanılabilen önceden şifrelenmiş görüntüleri hazırlama için bu bölümleri birinden Hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-507">Follow hello instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="cbafa-508">Merhaba görüntü oluşturulduktan sonra hello sonraki bölümde toocreate içinde şifrelenmiş bir Azure VM hello adımları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-508">After hello image is created, you can use hello steps in hello next section toocreate an encrypted Azure VM.</span></span>

* [<span data-ttu-id="cbafa-509">Önceden şifrelenmiş Windows VHD hazırlama</span><span class="sxs-lookup"><span data-stu-id="cbafa-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="cbafa-510">Önceden şifrelenmiş Linux VHD hazırlama</span><span class="sxs-lookup"><span data-stu-id="cbafa-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="cbafa-511">Merhaba Resource Manager şablonu kullanarak</span><span class="sxs-lookup"><span data-stu-id="cbafa-511">Using hello Resource Manager template</span></span>
<span data-ttu-id="cbafa-512">Hello kullanarak, şifrelenmiş VHD disk şifrelemesi etkinleştirebilirsiniz [Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="cbafa-512">You can enable disk encryption on your encrypted VHD by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="cbafa-513">Hello Azure hızlı başlangıç şablonuna tıklayın **tooAzure dağıtmak**, hello şifreleme yapılandırması üzerinde hello girin **parametreleri** dikey ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="cbafa-513">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="cbafa-514">Merhaba abonelik, kaynak grubu, kaynak grubu konumu, yasal koşulları ve anlaşma seçin ve ardından **oluşturma** tooenable şifreleme hello yeni Iaas VM.</span><span class="sxs-lookup"><span data-stu-id="cbafa-514">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello new IaaS VM.</span></span>

<span data-ttu-id="cbafa-515">Merhaba aşağıdaki tabloda hello Resource Manager şablonu parametreleri, şifrelenmiş VHD için listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="cbafa-515">hello following table lists hello Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="cbafa-516">Parametre</span><span class="sxs-lookup"><span data-stu-id="cbafa-516">Parameter</span></span> | <span data-ttu-id="cbafa-517">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cbafa-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cbafa-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="cbafa-518">newStorageAccountName</span></span> | <span data-ttu-id="cbafa-519">Merhaba depolama hesabı toostore hello adını OS VHD şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-519">Name of hello storage account toostore hello encrypted OS VHD.</span></span> <span data-ttu-id="cbafa-520">Bu depolama hesabı zaten hello aynı oluşturulmuş kaynak grubu ve hello VM ile aynı konumda.</span><span class="sxs-lookup"><span data-stu-id="cbafa-520">This storage account should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="cbafa-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="cbafa-521">osVhdUri</span></span> | <span data-ttu-id="cbafa-522">Merhaba depolama hesabından hello OS VHD URI'si.</span><span class="sxs-lookup"><span data-stu-id="cbafa-522">URI of hello OS VHD from hello storage account.</span></span> |
| <span data-ttu-id="cbafa-523">osType</span><span class="sxs-lookup"><span data-stu-id="cbafa-523">osType</span></span> | <span data-ttu-id="cbafa-524">İşletim sistemi ürün türü (Windows/Linux).</span><span class="sxs-lookup"><span data-stu-id="cbafa-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="cbafa-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="cbafa-525">virtualNetworkName</span></span> | <span data-ttu-id="cbafa-526">Merhaba VNet bu hello VM NIC adını ait.</span><span class="sxs-lookup"><span data-stu-id="cbafa-526">Name of hello VNet that hello VM NIC should belong to.</span></span> <span data-ttu-id="cbafa-527">Merhaba adı zaten hello aynı oluşturulmuş olmalıdır kaynak grubu ve hello VM ile aynı konumda.</span><span class="sxs-lookup"><span data-stu-id="cbafa-527">hello name should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="cbafa-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="cbafa-528">subnetName</span></span> | <span data-ttu-id="cbafa-529">Merhaba VNet bu hello VM NIC üzerinde hello alt ağ adı için ait olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-529">Name of hello subnet on hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="cbafa-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="cbafa-530">vmSize</span></span> | <span data-ttu-id="cbafa-531">Merhaba VM boyutu.</span><span class="sxs-lookup"><span data-stu-id="cbafa-531">Size of hello VM.</span></span> <span data-ttu-id="cbafa-532">Şu anda yalnızca standart bir, D ve G serisi desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="cbafa-533">Keyvaultresourceıd</span><span class="sxs-lookup"><span data-stu-id="cbafa-533">keyVaultResourceID</span></span> | <span data-ttu-id="cbafa-534">Merhaba hello anahtar kasası kaynağı Azure Kaynak Yöneticisi'nde tanımlayan ResourceId.</span><span class="sxs-lookup"><span data-stu-id="cbafa-534">hello ResourceID that identifies hello key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="cbafa-535">Merhaba PowerShell cmdlet'ini kullanarak elde edebilirsiniz `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="cbafa-535">You can get it by using hello PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="cbafa-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="cbafa-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="cbafa-537">Merhaba anahtar kasasına ayarlamak hello disk şifreleme anahtarı URL'si.</span><span class="sxs-lookup"><span data-stu-id="cbafa-537">URL of hello disk-encryption key that's set up in hello key vault.</span></span> |
| <span data-ttu-id="cbafa-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="cbafa-538">keyVaultKekUrl</span></span> | <span data-ttu-id="cbafa-539">Oluşturulan hello disk şifreleme anahtarı şifrelemek için anahtar şifreleme anahtarı hello URL'si.</span><span class="sxs-lookup"><span data-stu-id="cbafa-539">URL of hello key encryption key for encrypting hello generated disk-encryption key.</span></span> |
| <span data-ttu-id="cbafa-540">vmName</span><span class="sxs-lookup"><span data-stu-id="cbafa-540">vmName</span></span> | <span data-ttu-id="cbafa-541">Merhaba Iaas VM adıdır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-541">Name of hello IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="cbafa-542">PowerShell cmdlet'lerini kullanarak</span><span class="sxs-lookup"><span data-stu-id="cbafa-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="cbafa-543">Merhaba PowerShell cmdlet'ini kullanarak, şifrelenmiş VHD disk şifrelemesi etkinleştirebilirsiniz [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="cbafa-543">You can enable disk encryption on your encrypted VHD by using hello PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="cbafa-544">CLI komutları kullanarak</span><span class="sxs-lookup"><span data-stu-id="cbafa-544">Using CLI commands</span></span>
<span data-ttu-id="cbafa-545">CLI komutları kullanarak bu senaryo için tooenable disk şifrelemesi hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="cbafa-545">tooenable disk encryption for this scenario by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="cbafa-546">Erişim ilkeleri, anahtar kasanızı ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="cbafa-547">Set hello **EnabledForDiskEncryption** bayrağı:</span><span class="sxs-lookup"><span data-stu-id="cbafa-547">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="cbafa-548">İzinleri tooAzure AD uygulama toowrite gizli tooyour anahtar kasası ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-548">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="cbafa-549">bir var olan veya çalışan VM türü tooenable şifreleme:</span><span class="sxs-lookup"><span data-stu-id="cbafa-549">tooenable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="cbafa-550">Şifreleme durumu alın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="cbafa-551">Yeni bir VM, şifrelenmiş VHD'den hello parametrelerle aşağıdaki kullanım hello tooenable şifreleme `azure vm create` komutu:</span><span class="sxs-lookup"><span data-stu-id="cbafa-551">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="cbafa-552">Var olan veya Iaas Windows VM Azure'da çalışan şifrelemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="cbafa-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="cbafa-553">Bu senaryoda, hello Resource Manager şablonu, PowerShell cmdlet'leri veya CLI komutları kullanarak şifreleme etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-553">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="cbafa-554">Merhaba aşağıdaki bölümlerde açıklanmıştır daha ayrıntılı biçimde nasıl Resource Manager şablonu ve CLI komutları kullanarak hello tooenable.</span><span class="sxs-lookup"><span data-stu-id="cbafa-554">hello following sections explain in greater detail how tooenable it by using hello Resource Manager template and CLI commands.</span></span>

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="cbafa-555">Merhaba Resource Manager şablonu kullanarak</span><span class="sxs-lookup"><span data-stu-id="cbafa-555">Using hello Resource Manager template</span></span>
<span data-ttu-id="cbafa-556">Var olan veya hello kullanarak Iaas Windows Vm'lerini Azure'da çalışan disk şifrelemesi etkinleştirebilirsiniz [Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="cbafa-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="cbafa-557">Hello Azure hızlı başlangıç şablonuna tıklayın **tooAzure dağıtmak**, hello şifreleme yapılandırması üzerinde hello girin **parametreleri** dikey ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="cbafa-557">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="cbafa-558">Merhaba abonelik, kaynak grubu, kaynak grubu konumu, yasal koşulları ve anlaşma seçin ve ardından **oluşturma** varolan veya Iaas VM çalıştıran hello tooenable şifreleme.</span><span class="sxs-lookup"><span data-stu-id="cbafa-558">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="cbafa-559">Merhaba aşağıdaki tabloda hello Resource Manager şablonu parametrelerinin varolan veya bir Azure AD İstemci Kimliğini kullanan sanal makineleri çalıştıran listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="cbafa-559">hello following table lists hello Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="cbafa-560">Parametre</span><span class="sxs-lookup"><span data-stu-id="cbafa-560">Parameter</span></span> | <span data-ttu-id="cbafa-561">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cbafa-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cbafa-562">Aadclientıd</span><span class="sxs-lookup"><span data-stu-id="cbafa-562">AADClientID</span></span> | <span data-ttu-id="cbafa-563">İzinleri toowrite gizli toohello anahtar kasası olan hello Azure AD uygulama istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="cbafa-563">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="cbafa-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="cbafa-564">AADClientSecret</span></span> | <span data-ttu-id="cbafa-565">İzinleri toowrite gizli toohello anahtar kasası olan hello Azure AD uygulama istemci gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="cbafa-565">Client secret of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="cbafa-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="cbafa-566">keyVaultName</span></span> | <span data-ttu-id="cbafa-567">Merhaba anahtarın adını kasa bu hello BitLocker anahtarını karşıya yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-567">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="cbafa-568">Merhaba cmdlet'ini kullanarak elde edebilirsiniz `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="cbafa-568">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="cbafa-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="cbafa-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="cbafa-570">Kullanılan tooencrypt hello hello anahtar şifreleme anahtarı URL'sini BitLocker anahtarı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-570">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="cbafa-571">Bu seçerseniz isteğe bağlı bir parametredir **nokek** hello UseExistingKek aşağı açılan listesinde.</span><span class="sxs-lookup"><span data-stu-id="cbafa-571">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="cbafa-572">Seçerseniz **kek** hello UseExistingKek aşağı açılan listesinde, hello girmelisiniz _keyEncryptionKeyURL_ değeri.</span><span class="sxs-lookup"><span data-stu-id="cbafa-572">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="cbafa-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="cbafa-573">volumeType</span></span> | <span data-ttu-id="cbafa-574">Merhaba şifreleme işlemi gerçekleştirilir birim türü.</span><span class="sxs-lookup"><span data-stu-id="cbafa-574">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="cbafa-575">Geçerli değerler _OS_, _veri_, ve _tüm_.</span><span class="sxs-lookup"><span data-stu-id="cbafa-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="cbafa-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="cbafa-576">sequenceVersion</span></span> | <span data-ttu-id="cbafa-577">Merhaba BitLocker işlemi sürümü dizisi.</span><span class="sxs-lookup"><span data-stu-id="cbafa-577">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="cbafa-578">Disk şifrelemesi işlemi hello üzerinde gerçekleştirilen her zaman bu sürüm numarasını Artır aynı VM.</span><span class="sxs-lookup"><span data-stu-id="cbafa-578">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="cbafa-579">vmName</span><span class="sxs-lookup"><span data-stu-id="cbafa-579">vmName</span></span> | <span data-ttu-id="cbafa-580">Üzerinde gerçekleştirilen toobe hello şifreleme işlemi hello VM adıdır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-580">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="cbafa-581">_KeyEncryptionKeyURL_ isteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="cbafa-582">Merhaba anahtar kasasına kendi KEK toofurther koruma hello veri şifreleme anahtarı (BitLocker şifreleme gizli) kullanıma sunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-582">You can bring your own KEK toofurther safeguard hello data encryption key (BitLocker encryption secret) in hello key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="cbafa-583">PowerShell cmdlet'lerini kullanarak</span><span class="sxs-lookup"><span data-stu-id="cbafa-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="cbafa-584">Merhaba blog gönderileri PowerShell cmdlet'lerini kullanarak şifreleme Azure Disk şifrelemesi ile etkinleştirme hakkında daha fazla bilgi için bkz: [keşfedin Azure Disk şifrelemesi Azure PowerShell - bölüm 1 ile](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) ve [Azure Disk şifrelemesi keşfedin Azure PowerShell ile - bölüm 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbafa-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="cbafa-585">CLI komutları kullanarak</span><span class="sxs-lookup"><span data-stu-id="cbafa-585">Using CLI commands</span></span>
<span data-ttu-id="cbafa-586">var olan veya Iaas Windows VM CLI komutları kullanarak Azure'da çalışan tooenable şifreleme hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="cbafa-586">tooenable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="cbafa-587">Merhaba anahtar kasası erişim ilkelerini tooset:</span><span class="sxs-lookup"><span data-stu-id="cbafa-587">tooset access policies in hello key vault:</span></span>
   * <span data-ttu-id="cbafa-588">Set hello **EnabledForDiskEncryption** bayrağı:</span><span class="sxs-lookup"><span data-stu-id="cbafa-588">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="cbafa-589">İzinleri tooAzure AD uygulama toowrite gizli tooyour anahtar kasası ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-589">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="cbafa-590">var olan veya çalışan VM tooenable şifreleme:</span><span class="sxs-lookup"><span data-stu-id="cbafa-590">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="cbafa-591">tooget şifreleme durumu:</span><span class="sxs-lookup"><span data-stu-id="cbafa-591">tooget encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="cbafa-592">Yeni bir VM, şifrelenmiş VHD'den hello parametrelerle aşağıdaki kullanım hello tooenable şifreleme `azure vm create` komutu:</span><span class="sxs-lookup"><span data-stu-id="cbafa-592">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="cbafa-593">Azure'da bir var olan veya çalışan Iaas Linux VM şifrelemeyi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="cbafa-594">Hello kullanarak var olan veya çalışan Iaas Linux VM'de Azure disk şifrelemesi etkinleştirebilirsiniz [Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="cbafa-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="cbafa-595">Tıklatın **tooAzure dağıtmak** hello Azure hızlı başlangıç şablona hello şifreleme yapılandırması üzerinde hello girin **parametreleri** dikey ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="cbafa-595">Click **Deploy tooAzure** on hello Azure quick-start template, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="cbafa-596">Merhaba abonelik, kaynak grubu, kaynak grubu konumu, yasal koşulları ve anlaşma seçin ve ardından **oluşturma** varolan veya Iaas VM çalıştıran hello tooenable şifreleme.</span><span class="sxs-lookup"><span data-stu-id="cbafa-596">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="cbafa-597">Aşağıdaki tablonun hello Resource Manager şablonu parametrelerinin varolan veya bir Azure AD İstemci Kimliğini kullanan sanal makineleri çalıştıran listeler:</span><span class="sxs-lookup"><span data-stu-id="cbafa-597">hello following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="cbafa-598">Parametre</span><span class="sxs-lookup"><span data-stu-id="cbafa-598">Parameter</span></span> | <span data-ttu-id="cbafa-599">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cbafa-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cbafa-600">Aadclientıd</span><span class="sxs-lookup"><span data-stu-id="cbafa-600">AADClientID</span></span> | <span data-ttu-id="cbafa-601">İzinleri toowrite gizli toohello anahtar kasası olan hello Azure AD uygulama istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="cbafa-601">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="cbafa-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="cbafa-602">AADClientSecret</span></span> | <span data-ttu-id="cbafa-603">İzinleri toowrite gizli tooyour anahtar kasası olan hello Azure AD uygulama istemci gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="cbafa-603">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="cbafa-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="cbafa-604">keyVaultName</span></span> | <span data-ttu-id="cbafa-605">Merhaba anahtarın adını kasa bu hello BitLocker anahtarını karşıya yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-605">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="cbafa-606">Merhaba cmdlet'ini kullanarak elde edebilirsiniz `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="cbafa-606">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="cbafa-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="cbafa-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="cbafa-608">Kullanılan tooencrypt hello hello anahtar şifreleme anahtarı URL'sini BitLocker anahtarı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-608">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="cbafa-609">Bu seçerseniz isteğe bağlı bir parametredir **nokek** hello UseExistingKek aşağı açılan listesinde.</span><span class="sxs-lookup"><span data-stu-id="cbafa-609">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="cbafa-610">Seçerseniz **kek** hello UseExistingKek aşağı açılan listesinde, hello girmelisiniz _keyEncryptionKeyURL_ değeri.</span><span class="sxs-lookup"><span data-stu-id="cbafa-610">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="cbafa-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="cbafa-611">volumeType</span></span> | <span data-ttu-id="cbafa-612">Merhaba şifreleme işlemi gerçekleştirilir birim türü.</span><span class="sxs-lookup"><span data-stu-id="cbafa-612">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="cbafa-613">Geçerli desteklenen değerler _OS_ veya _tüm_ (için RHEL 7.2, CentOS 7.2 ve Ubuntu 16.04), ve _veri_ (için tüm diğer dağıtımlar için).</span><span class="sxs-lookup"><span data-stu-id="cbafa-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="cbafa-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="cbafa-614">sequenceVersion</span></span> | <span data-ttu-id="cbafa-615">Merhaba BitLocker işlemi sürümü dizisi.</span><span class="sxs-lookup"><span data-stu-id="cbafa-615">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="cbafa-616">Disk şifrelemesi işlemi hello üzerinde gerçekleştirilen her zaman bu sürüm numarasını Artır aynı VM.</span><span class="sxs-lookup"><span data-stu-id="cbafa-616">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="cbafa-617">vmName</span><span class="sxs-lookup"><span data-stu-id="cbafa-617">vmName</span></span> | <span data-ttu-id="cbafa-618">Üzerinde gerçekleştirilen toobe hello şifreleme işlemi hello VM adıdır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-618">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |
| <span data-ttu-id="cbafa-619">Parola</span><span class="sxs-lookup"><span data-stu-id="cbafa-619">passPhrase</span></span> | <span data-ttu-id="cbafa-620">Merhaba veri şifreleme anahtarı güçlü bir parola yazın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-620">Type a strong passphrase as hello data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="cbafa-621">_KeyEncryptionKeyURL_ isteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="cbafa-622">Anahtar kasanızı kendi KEK toofurther koruma hello veri şifreleme anahtarı (parola gizli) kullanıma sunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-622">You can bring your own KEK toofurther safeguard hello data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="cbafa-623">CLI komutları</span><span class="sxs-lookup"><span data-stu-id="cbafa-623">CLI commands</span></span>
<span data-ttu-id="cbafa-624">Disk şifrelemesi yükleme ve hello kullanma, şifreli VHD etkinleştirebilirsiniz [CLI komutu](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cbafa-624">You can enable disk encryption on your encrypted VHD by installing and using hello [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="cbafa-625">var olan veya CLI komutları kullanarak Azure Iaas Linux VM'ler çalıştıran tooenable şifreleme hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="cbafa-625">tooenable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="cbafa-626">Erişim ilkeleri hello anahtar kasasına ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-626">Set access policies in hello key vault:</span></span>

 * <span data-ttu-id="cbafa-627">Set hello **EnabledForDiskEncryption** bayrağı:</span><span class="sxs-lookup"><span data-stu-id="cbafa-627">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="cbafa-628">İzinleri tooAzure AD uygulama toowrite gizli tooyour anahtar kasası ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-628">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="cbafa-629">var olan veya çalışan VM tooenable şifreleme:</span><span class="sxs-lookup"><span data-stu-id="cbafa-629">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="cbafa-630">Şifreleme durumu alın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="cbafa-631">Yeni bir VM, şifrelenmiş VHD'den hello parametrelerle aşağıdaki kullanım hello tooenable şifreleme `azure vm create` komutu:</span><span class="sxs-lookup"><span data-stu-id="cbafa-631">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="cbafa-632">Şifrelenmiş bir Iaas VM'nin Hello şifreleme durumunu Al</span><span class="sxs-lookup"><span data-stu-id="cbafa-632">Get hello encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="cbafa-633">Azure Resource Manager kullanarak hello şifreleme durumu alabilirsiniz [PowerShell cmdlet'leri](/powershell/azure/overview), veya CLI komutları.</span><span class="sxs-lookup"><span data-stu-id="cbafa-633">You can get hello encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="cbafa-634">Aşağıdaki bölümlerde hello nasıl toouse hello Klasik Azure portalı ve CLI komutları tooget şifreleme durumu hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-634">hello following sections explain how toouse hello Azure classic portal and CLI commands tooget hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="cbafa-635">Azure Resource Manager kullanılarak şifrelenmiş bir Windows VM Hello şifreleme durumunu Al</span><span class="sxs-lookup"><span data-stu-id="cbafa-635">Get hello encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="cbafa-636">Merhaba Iaas VM hello şifreleme durumu hello aşağıdakileri yaparak Azure Kaynak Yöneticisi'nden alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cbafa-636">You can get hello encryption status of hello IaaS VM from Azure Resource Manager by doing hello following:</span></span>

1. <span data-ttu-id="cbafa-637">İçinde toohello oturum [Klasik Azure portalı](https://portal.azure.com/)ve ardından **sanal makineleri** hello sol bölmede toosee hello sanal makineleri aboneliğinizde Özet görünümünü de.</span><span class="sxs-lookup"><span data-stu-id="cbafa-637">Sign in toohello [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in hello left pane toosee a summary view of hello virtual machines in your subscription.</span></span> <span data-ttu-id="cbafa-638">Hello hello abonelik adını seçerek hello sanal makineleri görünümünü filtreleyebilirsiniz **abonelik** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="cbafa-638">You can filter hello virtual machines view by selecting hello subscription name in hello **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="cbafa-639">Merhaba hello üstündeki **sanal makineleri** sayfasında, **sütunları**.</span><span class="sxs-lookup"><span data-stu-id="cbafa-639">At hello top of hello **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="cbafa-640">Merhaba üzerinde **Seç sütun** dikey penceresinde, select **Disk şifrelemesi**ve ardından **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="cbafa-640">On hello **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="cbafa-641">Merhaba disk şifrelemesi sütun gösteren hello şifreleme durumunu görmelisiniz _etkin_ veya _etkin_ hello aşağıdaki şekilde gösterildiği gibi her VM için:</span><span class="sxs-lookup"><span data-stu-id="cbafa-641">You should see hello disk-encryption column showing hello encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in hello following figure:</span></span>

 ![Azure’da Microsoft Kötü Amaçlı Yazılımdan Koruma](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="cbafa-643">Merhaba disk şifrelemesi PowerShell cmdlet'ini kullanarak bir şifrelenmiş (Windows/Linux) Iaas VM Hello şifreleme durumunu Al</span><span class="sxs-lookup"><span data-stu-id="cbafa-643">Get hello encryption status of an encrypted (Windows/Linux) IaaS VM by using hello disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="cbafa-644">Merhaba disk şifrelemesi PowerShell cmdlet'inden hello Iaas VM hello şifreleme durumu alabilirsiniz `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="cbafa-644">You can get hello encryption status of hello IaaS VM from hello disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="cbafa-645">tooget hello şifreleme ayarları, VM için hello aşağıdakileri girin:</span><span class="sxs-lookup"><span data-stu-id="cbafa-645">tooget hello encryption settings for your VM, enter hello following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="cbafa-646">Merhaba çıktısını inceleyebilirsiniz _Get-AzureRmVMDiskEncryptionStatus_ URL'ler için şifreleme anahtarı.</span><span class="sxs-lookup"><span data-stu-id="cbafa-646">You can inspect hello output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

<span data-ttu-id="cbafa-647">Merhaba OSVolumeEncrypted ve DataVolumesEncrypted ayarlarının değerleri her iki birimin Azure Disk şifrelemesi kullanılarak şifrelenmiş olduğunu gösteren too_Encrypted_ ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-647">hello OSVolumeEncrypted and DataVolumesEncrypted settings values are set too_Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="cbafa-648">Merhaba blog gönderileri PowerShell cmdlet'lerini kullanarak şifreleme Azure Disk şifrelemesi ile etkinleştirme hakkında daha fazla bilgi için bkz: [keşfedin Azure Disk şifrelemesi Azure PowerShell - bölüm 1 ile](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) ve [Azure Disk şifrelemesi keşfedin Azure PowerShell ile - bölüm 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbafa-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-649">İsteğe bağlı olarak Linux VM'ler üzerinde hello üç toofour dakika sürer `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello şifreleme durumu.</span><span class="sxs-lookup"><span data-stu-id="cbafa-649">On Linux VMs, it takes three toofour minutes for hello `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a><span data-ttu-id="cbafa-650">Hello disk şifrelemesi CLI komuttan hello Iaas VM Hello şifreleme durumunu Al</span><span class="sxs-lookup"><span data-stu-id="cbafa-650">Get hello encryption status of hello IaaS VM from hello disk-encryption CLI command</span></span>
<span data-ttu-id="cbafa-651">Merhaba Iaas VM hello şifreleme durumu hello disk şifrelemesi CLI komutunu kullanarak alabileceğiniz `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="cbafa-651">You can get hello encryption status of hello IaaS VM by using hello disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="cbafa-652">tooget hello şifreleme ayarları, VM için Azure CLI oturumunuz girin:</span><span class="sxs-lookup"><span data-stu-id="cbafa-652">tooget hello encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="cbafa-653">Windows Iaas VM çalıştıran üzerinde şifrelemeyi devre dışı</span><span class="sxs-lookup"><span data-stu-id="cbafa-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="cbafa-654">Hello Azure Disk şifrelemesi Resource Manager şablonu veya PowerShell cmdlet'leri üzerinden çalışan bir Windows ya da Linux Iaas VM üzerinde şifrelemeyi devre dışı bırakabilir ve hello şifre çözme yapılandırması belirtin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-654">You can disable encryption on a running Windows or Linux IaaS VM via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify hello decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="cbafa-655">Windows VM</span><span class="sxs-lookup"><span data-stu-id="cbafa-655">Windows VM</span></span>
<span data-ttu-id="cbafa-656">Merhaba şifreleme devre dışı bırakma adımı hello işletim sistemi, hello veri birimi ya da hem de Windows Iaas VM çalıştıran hello şifreleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-656">hello disable-encryption step disables encryption of hello OS, hello data volume, or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="cbafa-657">Merhaba işletim sistemi birimi devre dışı bırakın ve şifrelenmiş hello veri birimi bırakın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-657">You cannot disable hello OS volume and leave hello data volume encrypted.</span></span> <span data-ttu-id="cbafa-658">Merhaba devre dışı bırak-şifreleme adım gerçekleştirildiğinde, hello Azure Klasik dağıtım modeli hello VM hizmet modeli güncelleştirir ve hello Windows Iaas VM şifresi çözülmüş işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-658">When hello disable-encryption step is performed, hello Azure classic deployment model updates hello VM service model, and hello Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="cbafa-659">Merhaba VM Merhaba içeriğine artık bekleyen şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-659">hello contents of hello VM are no longer encrypted at rest.</span></span> <span data-ttu-id="cbafa-660">Merhaba şifre çözme, anahtar kasasını ve hello şifreleme anahtar malzemesi (Windows ve Linux için parola için BitLocker şifreleme anahtarları) silmez.</span><span class="sxs-lookup"><span data-stu-id="cbafa-660">hello decryption does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="cbafa-661">Linux VM</span><span class="sxs-lookup"><span data-stu-id="cbafa-661">Linux VM</span></span>
<span data-ttu-id="cbafa-662">Merhaba şifreleme devre dışı bırakma adımı Linux Iaas VM çalıştıran hello hello veri birimi şifreleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-662">hello disable-encryption step disables encryption of hello data volume on hello running Linux IaaS VM.</span></span> <span data-ttu-id="cbafa-663">Bu adım yalnızca Hello işletim sistemi diski şifreli değilse çalışır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-663">This step only works if hello OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-664">Merhaba işletim sistemi diski şifreleme devre dışı bırakma Linux VM'ler üzerinde izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="cbafa-664">Disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="cbafa-665">Var olan veya çalışan bir Iaas VM üzerinde şifrelemeyi devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="cbafa-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="cbafa-666">Hello kullanarak Windows Iaas Vm'leri çalıştırma disk şifrelemesi devre dışı bırakabilirsiniz [Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="cbafa-666">You can disable disk encryption on running Windows IaaS VMs by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="cbafa-667">Hello Azure hızlı başlangıç şablonuna tıklayın **tooAzure dağıtmak**, üzerinde hello hello şifre çözme yapılandırma girin **parametreleri** dikey ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="cbafa-667">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello decryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="cbafa-668">Merhaba abonelik, kaynak grubu, kaynak grubu konumu, yasal koşulları ve anlaşma seçin ve ardından **oluşturma** yeni bir Iaas VM tooenable şifreleme.</span><span class="sxs-lookup"><span data-stu-id="cbafa-668">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="cbafa-669">Linux VM'ler için şifreleme hello kullanarak devre dışı bırakabilirsiniz [çalışan bir Linux VM üzerinde şifrelemeyi devre dışı bırakma](https://aka.ms/decrypt-linuxvm) şablonu.</span><span class="sxs-lookup"><span data-stu-id="cbafa-669">For Linux VMs, you can disable encryption by using hello [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="cbafa-670">Merhaba aşağıdaki tabloda çalışan bir Iaas VM üzerinde şifrelemeyi devre dışı bırakmak için Resource Manager şablonu parametreleri listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="cbafa-670">hello following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="cbafa-671">Parametre</span><span class="sxs-lookup"><span data-stu-id="cbafa-671">Parameter</span></span> | <span data-ttu-id="cbafa-672">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cbafa-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cbafa-673">vmName</span><span class="sxs-lookup"><span data-stu-id="cbafa-673">vmName</span></span> | <span data-ttu-id="cbafa-674">Üzerinde gerçekleştirilen toobe hello şifreleme işlemi hello VM adıdır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-674">Name of hello VM that hello encryption operation is toobe performed on.</span></span>
| <span data-ttu-id="cbafa-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="cbafa-675">volumeType</span></span> | <span data-ttu-id="cbafa-676">Bir şifre çözme işlemi gerçekleştirilir birim türü.</span><span class="sxs-lookup"><span data-stu-id="cbafa-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="cbafa-677">Geçerli değerler _OS_, _veri_, ve _tüm_.</span><span class="sxs-lookup"><span data-stu-id="cbafa-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="cbafa-678">Windows Iaas VM OS/önyükleme birimi hello şifreleme devre dışı bırakmadan çalıştırma şifreleme devre dışı bırakamazsınız _veri_ birim.</span><span class="sxs-lookup"><span data-stu-id="cbafa-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on hello _Data_ volume.</span></span> <span data-ttu-id="cbafa-679">Ayrıca hello işletim sistemi diski şifreleme devre dışı bırakma Linux VM'ler verilmiyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-679">Also note that disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="cbafa-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="cbafa-680">sequenceVersion</span></span> | <span data-ttu-id="cbafa-681">Merhaba BitLocker işlemi sürümü dizisi.</span><span class="sxs-lookup"><span data-stu-id="cbafa-681">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="cbafa-682">Merhaba her bir disk şifre çözme işlemi gerçekleştirildiğinde bu sürüm numarasını Artır aynı VM.</span><span class="sxs-lookup"><span data-stu-id="cbafa-682">Increment this version number every time a disk decryption operation is performed on hello same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="cbafa-683">Var olan veya çalışan bir Iaas VM üzerinde şifrelemeyi devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="cbafa-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="cbafa-684">bkz: hello PowerShell cmdlet'ini kullanarak var olan veya çalışan Iaas VM'de toodisable şifreleme [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="cbafa-684">toodisable encryption on an existing or running IaaS VM by using hello PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="cbafa-685">Bu cmdlet, Windows ve Linux VM'ler destekler.</span><span class="sxs-lookup"><span data-stu-id="cbafa-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="cbafa-686">toodisable şifreleme, bir uzantı hello sanal makineye yükler.</span><span class="sxs-lookup"><span data-stu-id="cbafa-686">toodisable encryption, it installs an extension on hello virtual machine.</span></span> <span data-ttu-id="cbafa-687">Merhaba, _adı_ parametresi belirtilmezse, hello varsayılan ad olan uzantı _Windows VM'ler için AzureDiskEncryption_ oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-687">If hello _Name_ parameter is not specified, an extension with hello default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="cbafa-688">Linux VM'ler üzerinde hello AzureDiskEncryptionForLinux uzantısı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-688">On Linux VMs, hello AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="cbafa-689">Bu cmdlet hello sanal makine yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-689">This cmdlet reboots hello virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="cbafa-690">Azure yönetilen diski ile önceden şifrelenmiş Iaas VM şifrelemeyi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="cbafa-691">Merhaba ARM şablonunu kullanarak önceden şifrelenmiş bir VHD şifrelenmiş bir VM'den konumundaki hello Azure yönetilen Disk ARM şablonu toocreate kullanın</span><span class="sxs-lookup"><span data-stu-id="cbafa-691">Use hello Azure Managed Disk ARM template toocreate a encrypted VM from a pre-encrypted VHD using hello ARM template located at</span></span>   
<span data-ttu-id="cbafa-692">[Yeni bir şifrelenmiş yönetilen disk önceden şifrelenmiş bir VHD/depolama blobundan Oluştur] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="cbafa-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="cbafa-693">Azure yönetilen diski olan yeni bir Linux Iaas VM şifrelemeyi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="cbafa-694">Yeni bir konumda bulunan hello ARM şablonu kullanarak Linux Iaas VM şifrelenmiş hello Azure yönetilen Disk ARM şablonu toocreate kullanın</span><span class="sxs-lookup"><span data-stu-id="cbafa-694">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
<span data-ttu-id="cbafa-695">[Tam disk şifrelemesi ile RHEL 7.2 dağıtım] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="cbafa-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="cbafa-696">Azure yönetilen diski olan yeni bir Windows Iaas VM şifrelemeyi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="cbafa-697">Yeni bir konumda bulunan hello ARM şablonu kullanarak Linux Iaas VM şifrelenmiş hello Azure yönetilen Disk ARM şablonu toocreate kullanın</span><span class="sxs-lookup"><span data-stu-id="cbafa-697">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
 <span data-ttu-id="cbafa-698">[Yeni bir şifrelenmiş Windows Iaas yönetilen Disk VM galeri görüntüden oluşturun] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="cbafa-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="cbafa-699">Bu zorunlu toosnapshot ve/veya yedekleme yönetilen bir disk dışında VM örneği ve önceki tooenabling Azure Disk şifrelemesi göre.</span><span class="sxs-lookup"><span data-stu-id="cbafa-699">It is mandatory toosnapshot and/or backup a managed disk based VM instance outside of and prior tooenabling Azure Disk Encryption.</span></span>  <span data-ttu-id="cbafa-700">Merhaba yönetilen diskin anlık görüntüsünü hello portalından alınabilir veya Azure yedekleme kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-700">A snapshot of hello managed disk can be taken from hello portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="cbafa-701">Yedeklemeleri kurtarma seçeneğini şifreleme sırasında beklenmeyen bir hata hello durumda mümkün olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cbafa-701">Backups ensure that a recovery option is possible in hello case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="cbafa-702">Bir yedekleme yapıldıktan sonra hello kümesi AzureRmVMDiskEncryptionExtension cmdlet hello - skipVmBackup parametresini belirterek yönetilen kullanılan tooencrypt diskler olabilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-702">Once a backup is made, hello Set-AzureRmVMDiskEncryptionExtension cmdlet can be used tooencrypt managed disks by specifying hello -skipVmBackup parameter.</span></span>  <span data-ttu-id="cbafa-703">Bu komut, yönetilen disk tabanlı VM'in karşı bir yedekleme yaptıysanız ve bu parametre belirtilen kadar başarısız olacak.</span><span class="sxs-lookup"><span data-stu-id="cbafa-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="cbafa-704">Mevcut bir şifrelenmiş premium olmayan VM'yi şifreleme ayarlarını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="cbafa-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="cbafa-705">VM [PS cmdlet'leri, CLI veya ARM şablonlarını] tooupdate hello şifreleme ayarları çalıştırmak için kullanım hello mevcut Azure disk desteklenen şifreleme arabirimleri AAD istemci kimliği/gizli anahtar şifreleme anahtarı [KEK] BitLocker şifreleme anahtarı Windows VM veya için parolayı ister Linux VM vb. hello güncelleştirme şifreleme ayarını, yalnızca premium olmayan Depolama tarafından yedeklenen VM'ler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-705">Use hello existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] tooupdate hello encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. hello update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="cbafa-706">Premium Depolama tarafından yedeklenen VM'ler için desteklenen NNOT olur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="cbafa-707">Ek</span><span class="sxs-lookup"><span data-stu-id="cbafa-707">Appendix</span></span>
### <a name="connect-tooyour-subscription"></a><span data-ttu-id="cbafa-708">Tooyour. abonelik'e bağlanma</span><span class="sxs-lookup"><span data-stu-id="cbafa-708">Connect tooyour subscription</span></span>
<span data-ttu-id="cbafa-709">Devam etmeden önce hello gözden *Önkoşullar* bu makalenin bölümünde.</span><span class="sxs-lookup"><span data-stu-id="cbafa-709">Before you proceed, review hello *Prerequisites* section in this article.</span></span> <span data-ttu-id="cbafa-710">Tüm önkoşulların karşılandığından emin olduktan sonra tooyour abonelik hello aşağıdakileri yaparak Bağlan:</span><span class="sxs-lookup"><span data-stu-id="cbafa-710">After you ensure that all prerequisites have been met, connect tooyour subscription by doing hello following:</span></span>

1. <span data-ttu-id="cbafa-711">Bir Azure PowerShell oturumu Başlat ve tooyour Azure hesabı komutu aşağıdaki hello ile oturum açın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-711">Start an Azure PowerShell session, and sign in tooyour Azure account with hello following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="cbafa-712">Birden çok aboneliğiniz varsa ve toospecify bir toouse istediğiniz, hesabınız için toosee hello abonelikleri aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-712">If you have multiple subscriptions and want toospecify one toouse, type hello following toosee hello subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="cbafa-713">toouse, istediğiniz toospecify hello abonelik türü:</span><span class="sxs-lookup"><span data-stu-id="cbafa-713">toospecify hello subscription you want toouse, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="cbafa-714">yapılandırılmış hello aboneliği doğru olduğunu tooverify, türü:</span><span class="sxs-lookup"><span data-stu-id="cbafa-714">tooverify that hello subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="cbafa-715">tooconfirm hello Azure Disk cmdlet'leri yüklenir, şifreleme türü:</span><span class="sxs-lookup"><span data-stu-id="cbafa-715">tooconfirm hello Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="cbafa-716">Çıktı aşağıdaki hello hello Azure Disk şifrelemesi PowerShell yükleme onaylar:</span><span class="sxs-lookup"><span data-stu-id="cbafa-716">hello following output confirms hello Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="cbafa-717">Önceden şifrelenmiş Windows VHD hazırlama</span><span class="sxs-lookup"><span data-stu-id="cbafa-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="cbafa-718">izleyen hello gerekli tooprepare Azure Iaas şifrelenmiş bir VHD olarak dağıtım için önceden şifrelenmiş Windows VHD bölümleridir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-718">hello sections that follow are necessary tooprepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="cbafa-719">Azure Site Recovery veya Azure yeni Windows VM (VHD) önyükleme ve Hello bilgi tooprepare kullanın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-719">Use hello information tooprepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a><span data-ttu-id="cbafa-720">Grup İlkesi tooallow TPM olmayan işletim sistemi koruma için güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="cbafa-720">Update group policy tooallow non-TPM for OS protection</span></span>
<span data-ttu-id="cbafa-721">Merhaba BitLocker Grup İlkesi ayarını yapılandırma **BitLocker Sürücü Şifrelemesi**, hangi altında bulabilirsiniz **yerel bilgisayar ilkesi** > **Bilgisayar Yapılandırması**  >  **Yönetim Şablonları** > **Windows bileşenleri**.</span><span class="sxs-lookup"><span data-stu-id="cbafa-721">Configure hello BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="cbafa-722">Bu ayar çok değiştirmek**işletim sistemi sürücüleri** > **başlangıçta ek kimlik doğrulamasını gerektiren** > **uyumluTPM'sizBitLockerizinver**hello aşağıdaki şekilde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="cbafa-722">Change this setting too**Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in hello following figure:</span></span>

![Azure’da Microsoft Kötü Amaçlı Yazılımdan Koruma](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="cbafa-724">BitLocker özelliği bileşenlerini yükle</span><span class="sxs-lookup"><span data-stu-id="cbafa-724">Install BitLocker feature components</span></span>
<span data-ttu-id="cbafa-725">Windows Server 2012 ve daha sonra komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="cbafa-725">For Windows Server 2012 and later, use hello following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="cbafa-726">Windows Server 2008 R2 için komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="cbafa-726">For Windows Server 2008 R2, use hello following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="cbafa-727">Hello işletim sistemi birimi için BitLocker'ı kullanarak hazırlama`bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="cbafa-727">Prepare hello OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="cbafa-728">toocompress işletim sistemi bölümü Merhaba ve hello makineyi BitLocker için hazırlama, hello aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="cbafa-728">toocompress hello OS partition and prepare hello machine for BitLocker, execute hello following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a><span data-ttu-id="cbafa-729">BitLocker'ı kullanarak Hello işletim sistemi birimi koruma</span><span class="sxs-lookup"><span data-stu-id="cbafa-729">Protect hello OS volume by using BitLocker</span></span>
<span data-ttu-id="cbafa-730">Kullanım hello [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) komutu tooenable şifreleme dış bir anahtar koruyucusu kullanarak hello önyükleme birimi.</span><span class="sxs-lookup"><span data-stu-id="cbafa-730">Use hello [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command tooenable encryption on hello boot volume using an external key protector.</span></span> <span data-ttu-id="cbafa-731">Ayrıca hello dış sürücü veya birim üzerinde hello dış anahtar (.bek dosyası) yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-731">Also place hello external key (.bek file) on hello external drive or volume.</span></span> <span data-ttu-id="cbafa-732">Şifreleme hello sistem/önyükleme birimini hello sonraki yeniden başlatmanın ardından etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-732">Encryption is enabled on hello system/boot volume after hello next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="cbafa-733">BitLocker'ı kullanarak hello dış anahtar almak için ayrı bir veri/kaynak VHD ile VM Hello hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-733">Prepare hello VM with a separate data/resource VHD for getting hello external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="cbafa-734">Çalışan bir Linux VM işletim sistemi sürücüsünde şifreleme</span><span class="sxs-lookup"><span data-stu-id="cbafa-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="cbafa-735">Çalışan bir Linux VM işletim sistemi sürücüsünde şifrelenmesi dağıtımları aşağıdaki hello üzerinde desteklenir:</span><span class="sxs-lookup"><span data-stu-id="cbafa-735">Encryption of an OS drive on a running Linux VM is supported on hello following distributions:</span></span>

* <span data-ttu-id="cbafa-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="cbafa-736">RHEL 7.2</span></span>
* <span data-ttu-id="cbafa-737">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="cbafa-737">CentOS 7.2</span></span>
* <span data-ttu-id="cbafa-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="cbafa-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="cbafa-739">İşletim sistemi disk şifrelemesi önkoşulları</span><span class="sxs-lookup"><span data-stu-id="cbafa-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="cbafa-740">Azure Kaynak Yöneticisi'nde hello Market görüntüsünden Hello VM yeniden oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-740">hello VM must be created from hello Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="cbafa-741">Azure VM ile en az 4 GB RAM (boyutu 7 GB önerilir).</span><span class="sxs-lookup"><span data-stu-id="cbafa-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="cbafa-742">(RHEL ve CentOS) SELinux devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="cbafa-743">toodisable SELinux, bkz: "4.4.2.</span><span class="sxs-lookup"><span data-stu-id="cbafa-743">toodisable SELinux, see "4.4.2.</span></span> <span data-ttu-id="cbafa-744">SELinux hello devre dışı bırakma" [SELinux kullanıcının ve Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) hello VM üzerinde.</span><span class="sxs-lookup"><span data-stu-id="cbafa-744">Disabling SELinux" in hello [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on hello VM.</span></span>
* <span data-ttu-id="cbafa-745">Merhaba VM SELinux devre dışı bıraktıktan sonra en az bir kez yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-745">After you disable SELinux, reboot hello VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="cbafa-746">Adımlar</span><span class="sxs-lookup"><span data-stu-id="cbafa-746">Steps</span></span>
1. <span data-ttu-id="cbafa-747">Daha önce belirtilen hello dağıtımları birini kullanarak bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbafa-747">Create a VM by using one of hello distributions specified previously.</span></span>

 <span data-ttu-id="cbafa-748">CentOS 7.2 için işletim sistemi disk şifrelemesi özel görüntüsü aracılığıyla desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="cbafa-749">toouse bu görüntü, "7.2n" Merhaba VM oluşturduğunuzda SKU hello gibi belirtin:</span><span class="sxs-lookup"><span data-stu-id="cbafa-749">toouse this image, specify "7.2n" as hello SKU when you create hello VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="cbafa-750">Merhaba VM according tooyour gereksinimlerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-750">Configure hello VM according tooyour needs.</span></span> <span data-ttu-id="cbafa-751">Tüm hello (işletim sistemi + veri) sürücüleri tooencrypt kullanacaksanız, hello veri sürücüleri belirtilen ve /etc/fstab gelen edilebilme toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-751">If you are going tooencrypt all hello (OS + data) drives, hello data drives need toobe specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="cbafa-752">UUID kullanmak... veri sürücüleri hello blok aygıt adı (örneğin, /dev/sdb1) belirtme yerine/etc/fstab toospecify =.</span><span class="sxs-lookup"><span data-stu-id="cbafa-752">Use UUID=... toospecify data drives in /etc/fstab instead of specifying hello block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="cbafa-753">Şifreleme sırasında VM hello üzerinde sürücüleri hello sırasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-753">During encryption, hello order of drives changes on hello VM.</span></span> <span data-ttu-id="cbafa-754">VM engelleme aygıtları belirli bir sırada dayalıysa, toomount başarısız olur şifreleme sonra bunları.</span><span class="sxs-lookup"><span data-stu-id="cbafa-754">If your VM relies on a specific order of block devices, it will fail toomount them after encryption.</span></span>

3. <span data-ttu-id="cbafa-755">Merhaba SSH oturumları dışında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-755">Sign out of hello SSH sessions.</span></span>

4. <span data-ttu-id="cbafa-756">tooencrypt hello işletim sistemi, belirtin volumeType olarak **tüm** veya **OS** olduğunda, [şifrelemeyi etkinleştirmek](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="cbafa-756">tooencrypt hello OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="cbafa-757">Olarak çalışan tüm kullanıcı alanı işlemleri `systemd` Hizmetleri sonlandırıldı ile bir `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="cbafa-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="cbafa-758">Merhaba VM yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-758">Reboot hello VM.</span></span> <span data-ttu-id="cbafa-759">İşletim sistemi disk şifrelemesi çalışan bir VM üzerinde etkinleştirdiğinizde, VM kapalı kalma süresi üzerinde planlayın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="cbafa-760">Düzenli aralıklarla hello hello yönergeleri kullanarak şifreleme hello ilerlemesini izlemek [sonraki bölümde](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="cbafa-760">Periodically monitor hello progress of encryption by using hello instructions in hello [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="cbafa-761">Get-AzureRmVmDiskEncryptionStatus "VMRestartPending" gösterir sonra VM tooit imzalama veya hello portal, PowerShell veya CLI kullanarak yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in tooit or by using hello portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
<span data-ttu-id="cbafa-762">Yeniden önce kaydetmeniz önerilir [önyükleme tanılama](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) hello VM.</span><span class="sxs-lookup"><span data-stu-id="cbafa-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of hello VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="cbafa-763">İşletim sistemi şifreleme ilerlemesini izleme</span><span class="sxs-lookup"><span data-stu-id="cbafa-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="cbafa-764">Üç yolla işletim sistemi şifreleme ilerleme durumunu izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cbafa-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="cbafa-765">Kullanım hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet'i ve hello ProgressMessage alan inceleyin:</span><span class="sxs-lookup"><span data-stu-id="cbafa-765">Use hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect hello ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="cbafa-766">"Şifreleme başlatılan işletim sistemi diski" Merhaba VM ulaştıktan sonra yaklaşık 40 sürdüğünü too50 dakika Premium depolama yedeklenen VM.</span><span class="sxs-lookup"><span data-stu-id="cbafa-766">After hello VM reaches "OS disk encryption started," it takes about 40 too50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="cbafa-767">Nedeniyle [sorun #388](https://github.com/Azure/WALinuxAgent/issues/388) WALinuxAgent içinde `OsVolumeEncrypted` ve `DataVolumesEncrypted` olarak görünmesini `Unknown` bazı dağıtımları içinde.</span><span class="sxs-lookup"><span data-stu-id="cbafa-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="cbafa-768">WALinuxAgent sürüm 2.1.5 ile ve daha sonra bu sorunu otomatik olarak sabit.</span><span class="sxs-lookup"><span data-stu-id="cbafa-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="cbafa-769">Görürseniz `Unknown` hello çıktısında hello Azure kaynak Gezgini'ni kullanarak disk şifrelemesi durumu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-769">If you see `Unknown` in hello output, you can verify disk-encryption status by using hello Azure Resource Explorer.</span></span>

 <span data-ttu-id="cbafa-770">Çok Git[Azure kaynak Gezgini](https://resources.azure.com/)ve ardından bu hiyerarşide hello Seçim Bölmesi Sol tarafta genişletin:</span><span class="sxs-lookup"><span data-stu-id="cbafa-770">Go too[Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in hello selection panel on left:</span></span>

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 <span data-ttu-id="cbafa-771">Hello InstanceView, Itanium tabanlı sistemler için toosee hello şifreleme durumu sürücünüz kaydırın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-771">In hello InstanceView, scroll down toosee hello encryption status of your drives.</span></span>

 ![VM örnek görünümü](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="cbafa-773">Bakmak [önyükleme tanılama](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="cbafa-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="cbafa-774">Merhaba ADE uzantısı iletilerden önekiyle `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="cbafa-774">Messages from hello ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="cbafa-775">Toohello VM SSH aracılığıyla imzalamak ve hello uzantısı günlüğü'nden alın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-775">Sign in toohello VM via SSH, and get hello extension log from:</span></span>

    <span data-ttu-id="cbafa-776">/var/log/Azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="cbafa-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="cbafa-777">İşletim sistemi şifreleme işlemi devam ederken toohello VM oturumunuzu değil, öneririz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-777">We recommend that you do not sign in toohello VM while OS encryption is in progress.</span></span> <span data-ttu-id="cbafa-778">Yalnızca hello diğer iki yöntemden yanıt vermediğinde hello günlüklerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-778">Copy hello logs only when hello other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="cbafa-779">Önceden şifrelenmiş Linux VHD hazırlama</span><span class="sxs-lookup"><span data-stu-id="cbafa-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="cbafa-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="cbafa-780">Ubuntu 16</span></span>
<span data-ttu-id="cbafa-781">Şifreleme hello dağıtım yüklemesi sırasında hello aşağıdakileri yaparak yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-781">Configure encryption during hello distribution installation by doing hello following:</span></span>

1. <span data-ttu-id="cbafa-782">Seçin **yapılandırma şifrelenmiş birimler** hello diskleri bölümlemek zaman.</span><span class="sxs-lookup"><span data-stu-id="cbafa-782">Select **Configure encrypted volumes** when you partition hello disks.</span></span>

 ![Ubuntu 16.04 Kurulumu](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="cbafa-784">Şifrelenmemiş olması bir ayrı önyükleme sürücüsü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbafa-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="cbafa-785">Kök sürücüsünde şifreleyin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-785">Encrypt your root drive.</span></span>

 ![Ubuntu 16.04 Kurulumu](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="cbafa-787">Bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-787">Provide a passphrase.</span></span> <span data-ttu-id="cbafa-788">Merhaba parola toohello anahtar kasası karşıya budur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-788">This is hello passphrase that you upload toohello key vault.</span></span>

 ![Ubuntu 16.04 Kurulumu](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="cbafa-790">Bölümleme tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-790">Finish partitioning.</span></span>

 ![Ubuntu 16.04 Kurulumu](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="cbafa-792">Merhaba VM önyükleme için bir parola istendiğinde, adım 3'te sağlanan hello parolası kullanın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-792">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Ubuntu 16.04 Kurulumu](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="cbafa-794">Merhaba VM Azure kullanarak yüklemek için hazırlama [bu yönergeleri](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="cbafa-794">Prepare hello VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="cbafa-795">Merhaba son adım (sağlamayı hello VM) henüz çalıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-795">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="cbafa-796">Şifreleme toowork hello aşağıdakileri yaparak Azure ile yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-796">Configure encryption toowork with Azure by doing hello following:</span></span>

1. <span data-ttu-id="cbafa-797">Komut dosyası izleyen hello hello içerikle /usr/local/sbin/azure_crypt_key.sh altında bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbafa-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with hello content in hello following script.</span></span> <span data-ttu-id="cbafa-798">Azure tarafından kullanılan hello parola dosya adı olduğundan dikkat toohello KeyFileName, ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-798">Pay attention toohello KeyFileName, because it is hello passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="cbafa-799">Değiştirme hello crypt yapılandırmada */etc/crypttab*.</span><span class="sxs-lookup"><span data-stu-id="cbafa-799">Change hello crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="cbafa-800">Şu şekilde görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="cbafa-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="cbafa-801">Düzenlemekte olduğunuz varsa *azure_crypt_key.sh* Windows ve, tooLinux çalıştırmak, kopyalanan `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="cbafa-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it tooLinux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="cbafa-802">Yürütülebilir izinleri toohello komut dosyası ekleyin:</span><span class="sxs-lookup"><span data-stu-id="cbafa-802">Add executable permissions toohello script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="cbafa-803">Düzen */etc/initramfs-tools/modules* satırları ekleyerek:</span><span class="sxs-lookup"><span data-stu-id="cbafa-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="cbafa-804">Çalıştırma `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` etkili.</span><span class="sxs-lookup"><span data-stu-id="cbafa-804">Run `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` take effect.</span></span>

7. <span data-ttu-id="cbafa-805">Şimdi hello VM yetkisini kaldırma.</span><span class="sxs-lookup"><span data-stu-id="cbafa-805">Now you can deprovision hello VM.</span></span>

 ![Ubuntu 16.04 Kurulumu](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="cbafa-807">Toohello sonraki adıma devam etmek ve [, VHD'yi karşıya](#upload-encrypted-vhd-to-an-azure-storage-account) Azure içine.</span><span class="sxs-lookup"><span data-stu-id="cbafa-807">Continue toohello next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="cbafa-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="cbafa-808">openSUSE 13.2</span></span>
<span data-ttu-id="cbafa-809">tooconfigure şifreleme hello dağıtım yüklemesi sırasında hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="cbafa-809">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="cbafa-810">Merhaba diskleri ayırırken seçin **şifrelemek birim grubu**ve ardından bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-810">When you partition hello disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="cbafa-811">Bu, tooyour anahtar kasası karşıya hello paroladır.</span><span class="sxs-lookup"><span data-stu-id="cbafa-811">This is hello password that you will upload tooyour key vault.</span></span>

 ![openSUSE 13.2 Kurulumu](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="cbafa-813">Önyükleme hello parolanızı kullanarak VM.</span><span class="sxs-lookup"><span data-stu-id="cbafa-813">Boot hello VM using your password.</span></span>

 ![openSUSE 13.2 Kurulumu](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="cbafa-815">Prepare hello yönergeleri takip ederek tooAzure yüklemek için VM hello [SLES veya openSUSE bir sanal makine için Azure hazırlama](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="cbafa-815">Prepare hello VM for uploading tooAzure by following hello instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="cbafa-816">Merhaba son adım (sağlamayı hello VM) henüz çalıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-816">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="cbafa-817">tooconfigure şifreleme toowork, Azure ile Merhaba aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="cbafa-817">tooconfigure encryption toowork with Azure, do hello following:</span></span>
1. <span data-ttu-id="cbafa-818">Merhaba /etc/dracut.conf düzenleyin ve hello aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="cbafa-818">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="cbafa-819">Açıklama tarafından hello hello sonuna şu satırları /usr/lib/dracut/modules.d/90crypt/module-setup.sh dosya:</span><span class="sxs-lookup"><span data-stu-id="cbafa-819">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. <span data-ttu-id="cbafa-820">Satır hello dosya /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh hello başında aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="cbafa-820">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="cbafa-821">Ve tüm oluşumlarını değiştirin:</span><span class="sxs-lookup"><span data-stu-id="cbafa-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="cbafa-822">yerine şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="cbafa-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="cbafa-823">/Usr/lib/dracut/Modules.d/90crypt/cryptroot-ASK.sh düzenleyin ve çok Ekle "# açık LUKS aygıt":</span><span class="sxs-lookup"><span data-stu-id="cbafa-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it too“# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. <span data-ttu-id="cbafa-824">Çalıştırma `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span><span class="sxs-lookup"><span data-stu-id="cbafa-824">Run `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span></span>

6. <span data-ttu-id="cbafa-825">VM yetkisini kaldırma artık hello ve [, VHD'yi karşıya](#upload-encrypted-vhd-to-an-azure-storage-account) Azure içine.</span><span class="sxs-lookup"><span data-stu-id="cbafa-825">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="cbafa-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="cbafa-826">CentOS 7</span></span>
<span data-ttu-id="cbafa-827">tooconfigure şifreleme hello dağıtım yüklemesi sırasında hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="cbafa-827">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="cbafa-828">Seçin **verilerimi şifrelemek** diskleri bölümlemek zaman.</span><span class="sxs-lookup"><span data-stu-id="cbafa-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![CentOS 7 Kurulumu](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="cbafa-830">Emin olun **şifrele** kök bölüm için seçilir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![CentOS 7 Kurulumu](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="cbafa-832">Bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="cbafa-832">Provide a passphrase.</span></span> <span data-ttu-id="cbafa-833">Merhaba parola tooyour anahtar kasası karşıya yükleyecek budur.</span><span class="sxs-lookup"><span data-stu-id="cbafa-833">This is hello passphrase that you will upload tooyour key vault.</span></span>

 ![CentOS 7 Kurulumu](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="cbafa-835">Merhaba VM önyükleme için bir parola istendiğinde, adım 3'te sağlanan hello parolası kullanın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-835">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![CentOS 7 Kurulumu](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="cbafa-837">Azure'da hello "CentOS 7.0 +" konusundaki yönergeleri kullanarak karşıya yükleme için hazırlık hello VM [CentOS tabanlı sanal makine için Azure hazırlama](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="cbafa-837">Prepare hello VM for uploading into Azure by using hello "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="cbafa-838">Merhaba son adım (sağlamayı hello VM) henüz çalıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="cbafa-838">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

6. <span data-ttu-id="cbafa-839">VM yetkisini kaldırma artık hello ve [, VHD'yi karşıya](#upload-encrypted-vhd-to-an-azure-storage-account) Azure içine.</span><span class="sxs-lookup"><span data-stu-id="cbafa-839">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="cbafa-840">tooconfigure şifreleme toowork, Azure ile Merhaba aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="cbafa-840">tooconfigure encryption toowork with Azure, do hello following:</span></span>

1. <span data-ttu-id="cbafa-841">Merhaba /etc/dracut.conf düzenleyin ve hello aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="cbafa-841">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="cbafa-842">Açıklama tarafından hello hello sonuna şu satırları /usr/lib/dracut/modules.d/90crypt/module-setup.sh dosya:</span><span class="sxs-lookup"><span data-stu-id="cbafa-842">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. <span data-ttu-id="cbafa-843">Satır hello dosya /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh hello başında aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="cbafa-843">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="cbafa-844">Ve tüm oluşumlarını değiştirin:</span><span class="sxs-lookup"><span data-stu-id="cbafa-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="cbafa-845">-</span><span class="sxs-lookup"><span data-stu-id="cbafa-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="cbafa-846">/Usr/lib/dracut/Modules.d/90crypt/cryptroot-ASK.sh düzenleyin ve bu "# açık LUKS aygıt" Merhaba sonra Ekle:</span><span class="sxs-lookup"><span data-stu-id="cbafa-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after hello “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. <span data-ttu-id="cbafa-847">Merhaba Çalıştır "/ sbin/usr/dracut - f - v" tooupdate hello initrd.</span><span class="sxs-lookup"><span data-stu-id="cbafa-847">Run hello “/usr/sbin/dracut -f -v” tooupdate hello initrd.</span></span>

![CentOS 7 Kurulumu](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a><span data-ttu-id="cbafa-849">Şifrelenmiş VHD tooan Azure depolama hesabı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="cbafa-849">Upload encrypted VHD tooan Azure storage account</span></span>
<span data-ttu-id="cbafa-850">BitLocker şifrelemesi veya DM-Crypt şifreleme etkinleştirildikten sonra hello yerel VHD gereksinimlerini karşıya toobe tooyour depolama hesabı şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-850">After BitLocker encryption or DM-Crypt encryption is enabled, hello local encrypted VHD needs toobe uploaded tooyour storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a><span data-ttu-id="cbafa-851">Merhaba disk şifrelemesi gizli hello önceden şifrelenmiş VM tooyour anahtar kasası için karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="cbafa-851">Upload hello disk-encryption secret for hello pre-encrypted VM tooyour key vault</span></span>
<span data-ttu-id="cbafa-852">elde ettiğiniz hello disk şifrelemesi gizli anahtar kasanızdaki gizli olarak daha önce yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-852">hello disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="cbafa-853">Merhaba anahtar kasası toohave disk şifrelemesi ve Azure AD istemciniz etkin izinleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbafa-853">hello key vault needs toohave disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="cbafa-854">Disk şifreleme parolası ile KEK şifrelenmez</span><span class="sxs-lookup"><span data-stu-id="cbafa-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="cbafa-855">anahtar kasanızı, kullanım hello gizliliği yukarı tooset [kümesi AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="cbafa-855">tooset up hello secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="cbafa-856">Windows sanal makine varsa, hello bek dosya kodlanmış bir base64 dizesi ve tooyour anahtar kasası hello kullanarak karşıya `Set-AzureKeyVaultSecret` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="cbafa-856">If you have a Windows virtual machine, hello bek file is encoded as a base64 string and then uploaded tooyour key vault using hello `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="cbafa-857">Linux için hello parola base64 dizesi olarak kodlanmış ve toohello anahtar kasası karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="cbafa-857">For Linux, hello passphrase is encoded as a base64 string and then uploaded toohello key vault.</span></span> <span data-ttu-id="cbafa-858">Ayrıca, emin olun etiketleri aşağıdaki o hello ayarlanır hello anahtar kasasına hello gizli oluşturduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="cbafa-858">In addition, make sure that hello following tags are set when you create hello secret in hello key vault.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="cbafa-859">Kullanım hello `$secretUrl` için hello sonraki adımda [KEK kullanmadan bağlanmasını hello işletim sistemi disk](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="cbafa-859">Use hello `$secretUrl` in hello next step for [attaching hello OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="cbafa-860">KEK ile şifrelenmiş disk şifreleme parolası</span><span class="sxs-lookup"><span data-stu-id="cbafa-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="cbafa-861">Merhaba gizli toohello anahtar kasası karşıya yüklemeden önce bir anahtar şifreleme anahtarı kullanarak isteğe bağlı olarak şifreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbafa-861">Before you upload hello secret toohello key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="cbafa-862">Kullanım hello kaydırma [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst şifrelemek hello anahtar şifreleme anahtarı kullanılarak hello gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="cbafa-862">Use hello wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst encrypt hello secret using hello key encryption key.</span></span> <span data-ttu-id="cbafa-863">Merhaba bu kaydırma işlemi hello kullanarak ardından bir gizlilik olarak yükleyebilirsiniz Base64 ile kodlanmış URL dizesi çıkışıdır [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="cbafa-863">hello output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using hello [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

<span data-ttu-id="cbafa-864">Kullanım `$KeyEncryptionKey` ve `$secretUrl` için hello sonraki adımda [KEK kullanarak bağlanmasını hello işletim sistemi diski](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="cbafa-864">Use `$KeyEncryptionKey` and `$secretUrl` in hello next step for [attaching hello OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="cbafa-865">İşletim sistemi diski taktığınızda gizli bir URL belirtin</span><span class="sxs-lookup"><span data-stu-id="cbafa-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="cbafa-866">Bir KEK kullanmadan</span><span class="sxs-lookup"><span data-stu-id="cbafa-866">Without using a KEK</span></span>
<span data-ttu-id="cbafa-867">Merhaba işletim sistemi disk ekleme olsa da, toopass gerek `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="cbafa-867">While you are attaching hello OS disk, you need toopass `$secretUrl`.</span></span> <span data-ttu-id="cbafa-868">Merhaba URL hello "ile bir KEK şifrelenmez Disk şifrelemesi gizli" bölümünde oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cbafa-868">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="cbafa-869">Bir KEK kullanma</span><span class="sxs-lookup"><span data-stu-id="cbafa-869">Using a KEK</span></span>
<span data-ttu-id="cbafa-870">Merhaba işletim sistemi disk taktığınızda geçirmek `$KeyEncryptionKey` ve `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="cbafa-870">When you attach hello OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="cbafa-871">Merhaba URL hello "ile bir KEK şifrelenmez Disk şifrelemesi gizli" bölümünde oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cbafa-871">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a><span data-ttu-id="cbafa-872">Bu Kılavuzu'nu indirin</span><span class="sxs-lookup"><span data-stu-id="cbafa-872">Download this guide</span></span>
<span data-ttu-id="cbafa-873">Bu kılavuz hello indirebilirsiniz [TechNet Galerisi](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="cbafa-873">You can download this guide from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="cbafa-874">Daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="cbafa-874">For more information</span></span>
[<span data-ttu-id="cbafa-875">Azure PowerShell - bölüm 1 ile Azure Disk şifrelemesi keşfedin</span><span class="sxs-lookup"><span data-stu-id="cbafa-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="cbafa-876">Azure PowerShell - bölüm 2 ile Azure Disk şifrelemesi keşfedin</span><span class="sxs-lookup"><span data-stu-id="cbafa-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
