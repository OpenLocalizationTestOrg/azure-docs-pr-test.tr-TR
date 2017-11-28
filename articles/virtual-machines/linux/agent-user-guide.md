---
title: "aaaAzure Linux VM Aracısı genel bakış | Microsoft Docs"
description: "Bilgi nasıl tooinstall ve Linux Aracısı (waagent) toomanage Azure yapı denetleyicisi ile sanal makinenizin etkileşimi yapılandırın."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a><span data-ttu-id="cc98d-103">Anlama ve hello Azure Linux Aracısı kullanma</span><span class="sxs-lookup"><span data-stu-id="cc98d-103">Understanding and using hello Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="cc98d-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="cc98d-104">Introduction</span></span>
<span data-ttu-id="cc98d-105">Merhaba Microsoft Azure Linux Aracısı, Linux ve FreeBSD sağlama ve hello Azure yapı denetleyicisi VM etkileşim (waagent) yönetir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-105">hello Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="cc98d-106">Linux ve FreeBSD Iaas dağıtımları için işlevselliği aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="cc98d-106">It provides hello following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="cc98d-107">Bkz: Hello Azure Linux Aracısı [Benioku](https://github.com/Azure/WALinuxAgent/blob/master/README.md) ek ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="cc98d-107">See hello Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="cc98d-108">**Görüntü sağlama**</span><span class="sxs-lookup"><span data-stu-id="cc98d-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="cc98d-109">Kullanıcı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc98d-109">Creation of a user account</span></span>
  * <span data-ttu-id="cc98d-110">SSH kimlik doğrulama türlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cc98d-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="cc98d-111">SSH ortak anahtarları ve anahtar çiftleri dağıtımı</span><span class="sxs-lookup"><span data-stu-id="cc98d-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="cc98d-112">Ayar hello ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="cc98d-112">Setting hello host name</span></span>
  * <span data-ttu-id="cc98d-113">Yayımlama hello ana bilgisayar adı toohello platform DNS</span><span class="sxs-lookup"><span data-stu-id="cc98d-113">Publishing hello host name toohello platform DNS</span></span>
  * <span data-ttu-id="cc98d-114">Raporlama SSH ana anahtar parmak izi toohello platformu</span><span class="sxs-lookup"><span data-stu-id="cc98d-114">Reporting SSH host key fingerprint toohello platform</span></span>
  * <span data-ttu-id="cc98d-115">Kaynak Disk Yönetimi</span><span class="sxs-lookup"><span data-stu-id="cc98d-115">Resource Disk Management</span></span>
  * <span data-ttu-id="cc98d-116">Biçimlendirme ve hello kaynak diski takma</span><span class="sxs-lookup"><span data-stu-id="cc98d-116">Formatting and mounting hello resource disk</span></span>
  * <span data-ttu-id="cc98d-117">Takas alanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cc98d-117">Configuring swap space</span></span>
* <span data-ttu-id="cc98d-118">**Ağ**</span><span class="sxs-lookup"><span data-stu-id="cc98d-118">**Networking**</span></span>
  
  * <span data-ttu-id="cc98d-119">Platform DHCP sunucularıyla yollar tooimprove uyumluluğu yönetir</span><span class="sxs-lookup"><span data-stu-id="cc98d-119">Manages routes tooimprove compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="cc98d-120">Merhaba ağ arabirimi adı Hello kararlılığını sağlar</span><span class="sxs-lookup"><span data-stu-id="cc98d-120">Ensures hello stability of hello network interface name</span></span>
* <span data-ttu-id="cc98d-121">**Çekirdek**</span><span class="sxs-lookup"><span data-stu-id="cc98d-121">**Kernel**</span></span>
  
  * <span data-ttu-id="cc98d-122">Sanal NUMA yapılandırır (çekirdek için devre dışı < 2.6.37)</span><span class="sxs-lookup"><span data-stu-id="cc98d-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="cc98d-123">Hyper-V entropi /dev/random için kullanır</span><span class="sxs-lookup"><span data-stu-id="cc98d-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="cc98d-124">SCSI zaman aşımı (uzak olabilir) hello kök aygıt için yapılandırır</span><span class="sxs-lookup"><span data-stu-id="cc98d-124">Configures SCSI timeouts for hello root device (which could be remote)</span></span>
* <span data-ttu-id="cc98d-125">**Tanılama**</span><span class="sxs-lookup"><span data-stu-id="cc98d-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="cc98d-126">Konsol yeniden yönlendirme toohello seri bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="cc98d-126">Console redirection toohello serial port</span></span>
* <span data-ttu-id="cc98d-127">**SCVMM dağıtımları**</span><span class="sxs-lookup"><span data-stu-id="cc98d-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="cc98d-128">Algılar ve Linux için hello VMM aracısının System Center Virtual Machine Manager 2012 R2 ortamında çalıştırırken bootstraps</span><span class="sxs-lookup"><span data-stu-id="cc98d-128">Detects and bootstraps hello VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="cc98d-129">**VM uzantısı**</span><span class="sxs-lookup"><span data-stu-id="cc98d-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="cc98d-130">Linux VM (Iaas) tooenable yazılım ve yapılandırma automation'a Microsoft ve iş ortakları tarafından yazılan Bileşen Ekle</span><span class="sxs-lookup"><span data-stu-id="cc98d-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) tooenable software and configuration automation</span></span>
  * <span data-ttu-id="cc98d-131">VM uzantısı başvurusu mantığınız [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="cc98d-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="cc98d-132">İletişim</span><span class="sxs-lookup"><span data-stu-id="cc98d-132">Communication</span></span>
<span data-ttu-id="cc98d-133">Merhaba bilgi akışını hello platform toohello aracısından iki kanallar oluşur:</span><span class="sxs-lookup"><span data-stu-id="cc98d-133">hello information flow from hello platform toohello agent occurs via two channels:</span></span>

* <span data-ttu-id="cc98d-134">Önyükleme zamanında DVD Iaas dağıtımları için eklendi.</span><span class="sxs-lookup"><span data-stu-id="cc98d-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="cc98d-135">Bu DVD hello gerçek SSH keypairs dışındaki tüm sağlama bilgilerini içeren bir OVF uyumlu yapılandırma dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than hello actual SSH keypairs.</span></span>
* <span data-ttu-id="cc98d-136">Bir REST API gösterme TCP uç noktası tooobtain dağıtım ve topoloji yapılandırması kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc98d-136">A TCP endpoint exposing a REST API used tooobtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="cc98d-137">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="cc98d-137">Requirements</span></span>
<span data-ttu-id="cc98d-138">Merhaba aşağıdaki sistemleri test edilmiş ve hello Azure Linux Aracısı ile toowork bilinen:</span><span class="sxs-lookup"><span data-stu-id="cc98d-138">hello following systems have been tested and are known toowork with hello Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="cc98d-139">Bu liste hello resmi hello Microsoft Azure platformu, desteklenen sistemlerinde listesi burada açıklandığı gibi farklı olabilir: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="cc98d-139">This list may differ from hello official list of supported systems on hello Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="cc98d-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="cc98d-140">CoreOS</span></span>
* <span data-ttu-id="cc98d-141">CentOS 6.3 +</span><span class="sxs-lookup"><span data-stu-id="cc98d-141">CentOS 6.3+</span></span>
* <span data-ttu-id="cc98d-142">Red Hat Enterprise Linux 6.7 +</span><span class="sxs-lookup"><span data-stu-id="cc98d-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="cc98d-143">Debian 7.0 +</span><span class="sxs-lookup"><span data-stu-id="cc98d-143">Debian 7.0+</span></span>
* <span data-ttu-id="cc98d-144">Ubuntu 12.04 +</span><span class="sxs-lookup"><span data-stu-id="cc98d-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="cc98d-145">openSUSE 12.3 +</span><span class="sxs-lookup"><span data-stu-id="cc98d-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="cc98d-146">SLES 11 SP3 +</span><span class="sxs-lookup"><span data-stu-id="cc98d-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="cc98d-147">Oracle Linux 6.4 +</span><span class="sxs-lookup"><span data-stu-id="cc98d-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="cc98d-148">Desteklenen diğer sistemleri:</span><span class="sxs-lookup"><span data-stu-id="cc98d-148">Other Supported Systems:</span></span>

* <span data-ttu-id="cc98d-149">FreeBSD 10 + (Azure Linux Aracısı v2.0.10 +)</span><span class="sxs-lookup"><span data-stu-id="cc98d-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="cc98d-150">Merhaba Linux Aracısı sipariş toofunction bazı sistem paketler düzgün bir şekilde bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="cc98d-150">hello Linux agent depends on some system packages in order toofunction properly:</span></span>

* <span data-ttu-id="cc98d-151">Python 2.6 +</span><span class="sxs-lookup"><span data-stu-id="cc98d-151">Python 2.6+</span></span>
* <span data-ttu-id="cc98d-152">OpenSSL 1.0 +</span><span class="sxs-lookup"><span data-stu-id="cc98d-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="cc98d-153">OpenSSH 5.3 +</span><span class="sxs-lookup"><span data-stu-id="cc98d-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="cc98d-154">Dosya sistemi yardımcı programları: sfdisk, fdisk, mkfs, parted</span><span class="sxs-lookup"><span data-stu-id="cc98d-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="cc98d-155">Parola araçları: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="cc98d-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="cc98d-156">Araçlar işleme metin: azaltılabilir, grep</span><span class="sxs-lookup"><span data-stu-id="cc98d-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="cc98d-157">Ağ araçları: IP yönlendirme</span><span class="sxs-lookup"><span data-stu-id="cc98d-157">Network tools: ip-route</span></span>
* <span data-ttu-id="cc98d-158">Çekirdek desteği UDF bağlanan dosya sistemlerinin bağlanması için.</span><span class="sxs-lookup"><span data-stu-id="cc98d-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="cc98d-159">Yükleme</span><span class="sxs-lookup"><span data-stu-id="cc98d-159">Installation</span></span>
<span data-ttu-id="cc98d-160">Bir RPM ya da bir DEB paketi dağıtımınızı ait paket depodan kullanarak yükleme hello Azure Linux Aracısı yükseltme ve yükleme hello tercih edilen yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-160">Installation using an RPM or a DEB package from your distribution's package repository is hello preferred method of installing and upgrading hello Azure Linux Agent.</span></span> <span data-ttu-id="cc98d-161">Tüm hello [dağıtım sağlayıcıları destekli](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello Azure Linux Aracısı paketi depoları ve görüntüleri tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="cc98d-161">All hello [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate hello Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="cc98d-162">Merhaba toohello belgelerine başvurun [Azure Linux Aracısı bağlantıların github'da](https://github.com/Azure/WALinuxAgent) kaynak veya toocustom konumu veya ön yükleme gibi gelişmiş yükleme seçenekleri için.</span><span class="sxs-lookup"><span data-stu-id="cc98d-162">Refer toohello documentation in hello [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or toocustom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="cc98d-163">Komut satırı seçenekleri</span><span class="sxs-lookup"><span data-stu-id="cc98d-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="cc98d-164">Bayrakları</span><span class="sxs-lookup"><span data-stu-id="cc98d-164">Flags</span></span>
* <span data-ttu-id="cc98d-165">ayrıntılı: Belirtilen komut dosyasının ayrıntı düzeyini artırın</span><span class="sxs-lookup"><span data-stu-id="cc98d-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="cc98d-166">Zorla: Bazı komutlar için etkileşimli Onayı Atla</span><span class="sxs-lookup"><span data-stu-id="cc98d-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="cc98d-167">Komutlar</span><span class="sxs-lookup"><span data-stu-id="cc98d-167">Commands</span></span>
* <span data-ttu-id="cc98d-168">Yardım: desteklenen hello komutları ve bayrakları listeler.</span><span class="sxs-lookup"><span data-stu-id="cc98d-168">help: Lists hello supported commands and flags.</span></span>
* <span data-ttu-id="cc98d-169">deprovision: tooclean hello sistem deneyin ve yeniden sağlama için uygun yapın.</span><span class="sxs-lookup"><span data-stu-id="cc98d-169">deprovision: Attempt tooclean hello system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="cc98d-170">Bu işlem hello aşağıdaki silindi:</span><span class="sxs-lookup"><span data-stu-id="cc98d-170">This operation deleted hello following:</span></span>
  
  * <span data-ttu-id="cc98d-171">(Provisioning.RegenerateSshHostKeyPair hello yapılandırma dosyasındaki ' y' ise) tüm SSH konak anahtarları</span><span class="sxs-lookup"><span data-stu-id="cc98d-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="cc98d-172">/Etc/resolv.conf ad sunucusu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cc98d-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="cc98d-173">Kök paroladan (Provisioning.DeleteRootPassword hello yapılandırma dosyasındaki ' y' ise) eşitleme</span><span class="sxs-lookup"><span data-stu-id="cc98d-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="cc98d-174">Önbelleğe alınan DHCP istemci kiraları</span><span class="sxs-lookup"><span data-stu-id="cc98d-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="cc98d-175">Sıfırlama ana bilgisayar adı toolocalhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="cc98d-175">Resets host name toolocalhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="cc98d-176">Sağlama kaldırma, hello görüntü tüm hassas bilgilerin temizlenmiş ve yeniden dağıtım için uygun olacağını garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="cc98d-176">Deprovisioning does not guarantee that hello image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="cc98d-177">deprovision + kullanıcı: altında - deprovision (yukarıda) her şeyi gerçekleştirir ve ayrıca (/var/lib/waagent elde edilen) hello son sağlanan kullanıcının hesabını siler ve veri ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="cc98d-177">deprovision+user: Performs everything under -deprovision (above) and also deletes hello last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="cc98d-178">Bu parametre, yakalanan ve yeniden kullanılabilir, böylece Azure üzerinde önceden sağlama bir görüntü XML'deki sağlamada olur.</span><span class="sxs-lookup"><span data-stu-id="cc98d-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="cc98d-179">Sürüm: görüntüler hello waagent sürümü</span><span class="sxs-lookup"><span data-stu-id="cc98d-179">version: Displays hello version of waagent</span></span>
* <span data-ttu-id="cc98d-180">serialconsole: kaz toomark ttyS0 yapılandırır (Merhaba ilk seri bağlantı noktası) hello önyükleme konsolu olarak.</span><span class="sxs-lookup"><span data-stu-id="cc98d-180">serialconsole: Configures GRUB toomark ttyS0 (hello first serial port) as hello boot console.</span></span> <span data-ttu-id="cc98d-181">Bu çekirdek önyükleme günlüklerini toothe seri bağlantı noktasına gönderilen ve hata ayıklama için kullanılabilir hale sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc98d-181">This ensures that kernel bootup logs are sent toothe serial port and made available for debugging.</span></span>
* <span data-ttu-id="cc98d-182">arka plan programı: arka plan programı toomanage etkileşim hello platform olarak waagent çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cc98d-182">daemon: Run waagent as a daemon toomanage interaction with hello platform.</span></span> <span data-ttu-id="cc98d-183">Bu değişken hello waagent init komut dosyasında belirtilen toowaagent değeri.</span><span class="sxs-lookup"><span data-stu-id="cc98d-183">This argument is specified toowaagent in hello waagent init script.</span></span>
* <span data-ttu-id="cc98d-184">Başlat: waagent arka plan işlemi olarak çalıştır</span><span class="sxs-lookup"><span data-stu-id="cc98d-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="cc98d-185">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cc98d-185">Configuration</span></span>
<span data-ttu-id="cc98d-186">Bir yapılandırma dosyası (/ etc/waagent.conf) denetimleri hello waagent eylemler.</span><span class="sxs-lookup"><span data-stu-id="cc98d-186">A configuration file (/etc/waagent.conf) controls hello actions of waagent.</span></span> <span data-ttu-id="cc98d-187">Örnek bir yapılandırma dosyası aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="cc98d-187">A sample configuration file is shown below:</span></span>

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

<span data-ttu-id="cc98d-188">Merhaba çeşitli yapılandırma seçenekleri aşağıda ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="cc98d-188">hello various configuration options are described in detail below.</span></span> <span data-ttu-id="cc98d-189">Yapılandırma seçenekleri üç tür içindedir; Boolean, String veya tamsayı.</span><span class="sxs-lookup"><span data-stu-id="cc98d-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="cc98d-190">Merhaba Boolean yapılandırma seçenekleri "y" veya "n" belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-190">hello Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="cc98d-191">özel anahtar sözcüğü "Hiçbiri" bazı dize türü için yapılandırma girdileri ayrıntılı olarak aşağıdaki kullanılabilir hello.</span><span class="sxs-lookup"><span data-stu-id="cc98d-191">hello special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="cc98d-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="cc98d-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="cc98d-193">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="cc98d-193">Type: Boolean</span></span>  
<span data-ttu-id="cc98d-194">Varsayılan: y</span><span class="sxs-lookup"><span data-stu-id="cc98d-194">Default: y</span></span>

<span data-ttu-id="cc98d-195">Bu hello kullanıcı tooenable izin verir veya hello Aracısı işlevleri sağlama hello devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="cc98d-195">This allows hello user tooenable or disable hello provisioning functionality in hello agent.</span></span> <span data-ttu-id="cc98d-196">"Y" veya "n" değerler geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="cc98d-197">Sağlama devre dışıysa, SSH ana bilgisayar ve kullanıcı anahtarları hello görüntüsündeki korunur ve hello Azure sağlama API belirtilen herhangi bir yapılandırma yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="cc98d-197">If provisioning is disabled, SSH host and user keys in hello image are preserved and any configuration specified in hello Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="cc98d-198">Merhaba `Provisioning.Enabled` parametre Varsayılanları çok "n" Ubuntu bulut görüntülerde, bulut init sağlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc98d-198">hello `Provisioning.Enabled` parameter defaults too"n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="cc98d-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="cc98d-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="cc98d-200">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="cc98d-200">Type: Boolean</span></span>  
<span data-ttu-id="cc98d-201">Varsayılan: n</span><span class="sxs-lookup"><span data-stu-id="cc98d-201">Default: n</span></span>

<span data-ttu-id="cc98d-202">Sağlama işlemi sırasında kümesi, hello kök dosyasında parolasını hello/etc/gölge silinmesi durumunda hello.</span><span class="sxs-lookup"><span data-stu-id="cc98d-202">If set, hello root password in hello /etc/shadow file is erased during hello provisioning process.</span></span>

<span data-ttu-id="cc98d-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="cc98d-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="cc98d-204">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="cc98d-204">Type: Boolean</span></span>  
<span data-ttu-id="cc98d-205">Varsayılan: y</span><span class="sxs-lookup"><span data-stu-id="cc98d-205">Default: y</span></span>

<span data-ttu-id="cc98d-206">Merhaba işlemden/etc/ssh/sağlama sırasında kümesi, tüm SSH ana anahtar çifti (ecdsa, dsa ve rsa) silinmişse.</span><span class="sxs-lookup"><span data-stu-id="cc98d-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during hello provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="cc98d-207">Ve tek bir yeni anahtar çifti oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cc98d-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="cc98d-208">Merhaba şifreleme türü hello yeni anahtar çifti için Provisioning.SshHostKeyPairType girişi hello tarafından yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-208">hello encryption type for hello fresh key pair is configurable by hello Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="cc98d-209">Merhaba SSH arka plan programı (örneğin, bir yeniden başlatma sırasında) yeniden başlatıldığında bazı dağıtımları eksik herhangi bir şifreleme türü için anahtar çiftleri SSH yeniden oluşturacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cc98d-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when hello SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="cc98d-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="cc98d-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="cc98d-211">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="cc98d-211">Type: String</span></span>  
<span data-ttu-id="cc98d-212">Varsayılan: rsa</span><span class="sxs-lookup"><span data-stu-id="cc98d-212">Default: rsa</span></span>

<span data-ttu-id="cc98d-213">Bu hello SSH arka plan hello sanal makine tarafından desteklenen tooan şifreleme algoritması türü ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc98d-213">This can be set tooan encryption algorithm type that is supported by hello SSH daemon on hello virtual machine.</span></span> <span data-ttu-id="cc98d-214">genellikle desteklenen hello "rsa", "dsa" ve "ecdsa" değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-214">hello typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="cc98d-215">"Putty.exe" Windows "ecdsa" desteklemediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cc98d-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="cc98d-216">Bu nedenle, Windows tooconnect tooa Linux dağıtım üzerinde toouse putty.exe düşünüyorsanız, lütfen "rsa" veya "dsa" kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc98d-216">So, if you intend toouse putty.exe on Windows tooconnect tooa Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="cc98d-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="cc98d-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="cc98d-218">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="cc98d-218">Type: Boolean</span></span>  
<span data-ttu-id="cc98d-219">Varsayılan: y</span><span class="sxs-lookup"><span data-stu-id="cc98d-219">Default: y</span></span>

<span data-ttu-id="cc98d-220">Ayarlama, waagent hello Linux sanal makine ana bilgisayar adı değişiklikleri (Merhaba "hostname" komutu tarafından döndürülen gibi) izleyen ve otomatik olarak hello görüntü tooreflect hello değişikliği hello ağ yapılandırmasını güncelleştirin durumunda.</span><span class="sxs-lookup"><span data-stu-id="cc98d-220">If set, waagent will monitor hello Linux virtual machine for hostname changes (as returned by hello "hostname" command) and automatically update hello networking configuration in hello image tooreflect hello change.</span></span> <span data-ttu-id="cc98d-221">Toohello DNS sunucuları sipariş toopush hello adını değiştirmek için ağ hello sanal makine yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="cc98d-221">In order toopush hello name change toohello DNS servers, networking will be restarted in hello virtual machine.</span></span> <span data-ttu-id="cc98d-222">Bu kısaca Internet bağlantısı kaybedilmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="cc98d-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="cc98d-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="cc98d-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="cc98d-224">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="cc98d-224">Type: Boolean</span></span>  
<span data-ttu-id="cc98d-225">Varsayılan: n</span><span class="sxs-lookup"><span data-stu-id="cc98d-225">Default: n</span></span>

<span data-ttu-id="cc98d-226">Ayarlama, waagent CustomData Base64 gelen kod çözme varsa.</span><span class="sxs-lookup"><span data-stu-id="cc98d-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="cc98d-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="cc98d-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="cc98d-228">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="cc98d-228">Type: Boolean</span></span>  
<span data-ttu-id="cc98d-229">Varsayılan: n</span><span class="sxs-lookup"><span data-stu-id="cc98d-229">Default: n</span></span>

<span data-ttu-id="cc98d-230">Ayarlama, waagent CustomData sağladıktan sonra yürütecek varsa.</span><span class="sxs-lookup"><span data-stu-id="cc98d-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="cc98d-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="cc98d-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="cc98d-232">Türü: dize</span><span class="sxs-lookup"><span data-stu-id="cc98d-232">Type:String</span></span>  
<span data-ttu-id="cc98d-233">Varsayılan: 6</span><span class="sxs-lookup"><span data-stu-id="cc98d-233">Default:6</span></span>

<span data-ttu-id="cc98d-234">Parola karmasını oluştururken crypt tarafından kullanılan algoritma.</span><span class="sxs-lookup"><span data-stu-id="cc98d-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="cc98d-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="cc98d-235">1 - MD5</span></span>  
 <span data-ttu-id="cc98d-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="cc98d-236">2a - Blowfish</span></span>  
 <span data-ttu-id="cc98d-237">5 - SHA-256</span><span class="sxs-lookup"><span data-stu-id="cc98d-237">5 - SHA-256</span></span>  
 <span data-ttu-id="cc98d-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="cc98d-238">6 - SHA-512</span></span>  

<span data-ttu-id="cc98d-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="cc98d-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="cc98d-240">Türü: dize</span><span class="sxs-lookup"><span data-stu-id="cc98d-240">Type:String</span></span>  
<span data-ttu-id="cc98d-241">Varsayılan: 10</span><span class="sxs-lookup"><span data-stu-id="cc98d-241">Default:10</span></span>

<span data-ttu-id="cc98d-242">Parola Karması oluşturulurken kullanılan rastgele salt uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="cc98d-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="cc98d-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="cc98d-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="cc98d-244">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="cc98d-244">Type: Boolean</span></span>  
<span data-ttu-id="cc98d-245">Varsayılan: y</span><span class="sxs-lookup"><span data-stu-id="cc98d-245">Default: y</span></span>

<span data-ttu-id="cc98d-246">Ayarlama, hello platform tarafından sağlanan hello kaynak disk biçimlendirilmiş ve olması hello filesystem türü "ResourceDisk.Filesystem" Merhaba kullanıcı tarafından istenen "ntfs" dışında bir şey ise waagent tarafından oluşturulmuş durumunda.</span><span class="sxs-lookup"><span data-stu-id="cc98d-246">If set, hello resource disk provided by hello platform will be formatted and mounted by waagent if hello filesystem type requested by hello user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="cc98d-247">Linux (83) türünde tek bir bölüm hello diskte kullanıma sunulacaktır.</span><span class="sxs-lookup"><span data-stu-id="cc98d-247">A single partition of type Linux (83) will be made available on hello disk.</span></span> <span data-ttu-id="cc98d-248">Başarıyla bağlanabiliyorsa'nın bu bölüm biçimlendirilmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cc98d-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="cc98d-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="cc98d-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="cc98d-250">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="cc98d-250">Type: String</span></span>  
<span data-ttu-id="cc98d-251">Varsayılan: ext4</span><span class="sxs-lookup"><span data-stu-id="cc98d-251">Default: ext4</span></span>

<span data-ttu-id="cc98d-252">Bu hello kaynak disk hello filesystem türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-252">This specifies hello filesystem type for hello resource disk.</span></span> <span data-ttu-id="cc98d-253">Desteklenen değerler Linux dağıtım göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="cc98d-254">Merhaba dize X, ardından mkfs ise. X hello Linux görüntüde mevcut olması.</span><span class="sxs-lookup"><span data-stu-id="cc98d-254">If hello string is X, then mkfs.X should be present on hello Linux image.</span></span> <span data-ttu-id="cc98d-255">SLES 11 görüntüleri genellikle 'ext3' kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="cc98d-256">FreeBSD görüntüleri 'ufs2' burada kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="cc98d-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="cc98d-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="cc98d-258">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="cc98d-258">Type: String</span></span>  
<span data-ttu-id="cc98d-259">Varsayılan: / mnt/kaynak</span><span class="sxs-lookup"><span data-stu-id="cc98d-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="cc98d-260">Bu hello kaynak disk bağlı hello yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-260">This specifies hello path at which hello resource disk is mounted.</span></span> <span data-ttu-id="cc98d-261">Bu hello kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-261">Note that hello resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span>

<span data-ttu-id="cc98d-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="cc98d-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="cc98d-263">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="cc98d-263">Type: String</span></span>  
<span data-ttu-id="cc98d-264">Varsayılan: yok</span><span class="sxs-lookup"><span data-stu-id="cc98d-264">Default: None</span></span>

<span data-ttu-id="cc98d-265">Disk bağlama seçenekleri geçirilen toobe toohello mount -o komutu belirtir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-265">Specifies disk mount options toobe passed toohello mount -o command.</span></span> <span data-ttu-id="cc98d-266">Değer, virgülle ayrılmış listesi ex budur.</span><span class="sxs-lookup"><span data-stu-id="cc98d-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="cc98d-267">'nodev, nosuid'.</span><span class="sxs-lookup"><span data-stu-id="cc98d-267">'nodev,nosuid'.</span></span> <span data-ttu-id="cc98d-268">Mount(8) Ayrıntılar için bkz.</span><span class="sxs-lookup"><span data-stu-id="cc98d-268">See mount(8) for details.</span></span>

<span data-ttu-id="cc98d-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="cc98d-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="cc98d-270">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="cc98d-270">Type: Boolean</span></span>  
<span data-ttu-id="cc98d-271">Varsayılan: n</span><span class="sxs-lookup"><span data-stu-id="cc98d-271">Default: n</span></span>

<span data-ttu-id="cc98d-272">Varsa bir takas dosyası ayarı (/ swapfile) hello kaynak disk üzerinde oluşturulur ve toohello sistem takas alanı eklenir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-272">If set, a swap file (/swapfile) is created on hello resource disk and added toohello system swap space.</span></span>

<span data-ttu-id="cc98d-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="cc98d-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="cc98d-274">Türü: tamsayı</span><span class="sxs-lookup"><span data-stu-id="cc98d-274">Type: Integer</span></span>  
<span data-ttu-id="cc98d-275">Varsayılan: 0</span><span class="sxs-lookup"><span data-stu-id="cc98d-275">Default: 0</span></span>

<span data-ttu-id="cc98d-276">Merhaba hello takas dosyası megabayt cinsinden büyüklüğü.</span><span class="sxs-lookup"><span data-stu-id="cc98d-276">hello size of hello swap file in megabytes.</span></span>

<span data-ttu-id="cc98d-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="cc98d-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="cc98d-278">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="cc98d-278">Type: Boolean</span></span>  
<span data-ttu-id="cc98d-279">Varsayılan: n</span><span class="sxs-lookup"><span data-stu-id="cc98d-279">Default: n</span></span>

<span data-ttu-id="cc98d-280">Kümesi, günlük ayrıntı boosted durumunda.</span><span class="sxs-lookup"><span data-stu-id="cc98d-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="cc98d-281">Waagent too/var/log/waagent.log günlüğe kaydeder ve hello sistem logrotate işlevselliği toorotate günlüklerini yararlanır.</span><span class="sxs-lookup"><span data-stu-id="cc98d-281">Waagent logs too/var/log/waagent.log and leverages hello system logrotate functionality toorotate logs.</span></span>

<span data-ttu-id="cc98d-282">**İŞLETİM SİSTEMİ. EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="cc98d-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="cc98d-283">Tür: Boolean</span><span class="sxs-lookup"><span data-stu-id="cc98d-283">Type: Boolean</span></span>  
<span data-ttu-id="cc98d-284">Varsayılan: n</span><span class="sxs-lookup"><span data-stu-id="cc98d-284">Default: n</span></span>

<span data-ttu-id="cc98d-285">Ayarlama, hello aracı tooinstall denemek ve donanım temel hello hello bellenimini hello sürümüyle eşleşen bir RDMA çekirdek sürücüsü yüklemek durumunda.</span><span class="sxs-lookup"><span data-stu-id="cc98d-285">If set, hello agent will attempt tooinstall and then load an RDMA kernel driver that matches hello version of hello firmware on hello underlying hardware.</span></span>

<span data-ttu-id="cc98d-286">**İŞLETİM SİSTEMİ. RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="cc98d-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="cc98d-287">Türü: tamsayı</span><span class="sxs-lookup"><span data-stu-id="cc98d-287">Type: Integer</span></span>  
<span data-ttu-id="cc98d-288">Varsayılan: 300</span><span class="sxs-lookup"><span data-stu-id="cc98d-288">Default: 300</span></span>

<span data-ttu-id="cc98d-289">Bu, hello SCSI zaman aşımı saniye hello işletim sistemi diski ve veri sürücülerinde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="cc98d-289">This configures hello SCSI timeout in seconds on hello OS disk and data drives.</span></span> <span data-ttu-id="cc98d-290">Aksi durumda ayarlamak, hello sistem varsayılan değerler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc98d-290">If not set, hello system defaults are used.</span></span>

<span data-ttu-id="cc98d-291">**İŞLETİM SİSTEMİ. OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="cc98d-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="cc98d-292">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="cc98d-292">Type: String</span></span>  
<span data-ttu-id="cc98d-293">Varsayılan: yok</span><span class="sxs-lookup"><span data-stu-id="cc98d-293">Default: None</span></span>

<span data-ttu-id="cc98d-294">Bu, kullanılan toospecify hello openssl ikili toouse şifreleme işlemleri için alternatif bir yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="cc98d-294">This can be used toospecify an alternate path for hello openssl binary toouse for cryptographic operations.</span></span>

<span data-ttu-id="cc98d-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="cc98d-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="cc98d-296">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="cc98d-296">Type: String</span></span>  
<span data-ttu-id="cc98d-297">Varsayılan: yok</span><span class="sxs-lookup"><span data-stu-id="cc98d-297">Default: None</span></span>

<span data-ttu-id="cc98d-298">Ayarlama, hello Aracısı bu proxy kullanıp kullanmayacağını sunucu tooaccess hello Internet.</span><span class="sxs-lookup"><span data-stu-id="cc98d-298">If set, hello agent will use this proxy server tooaccess hello internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="cc98d-299">Ubuntu bulut görüntüleri</span><span class="sxs-lookup"><span data-stu-id="cc98d-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="cc98d-300">Ubuntu bulut görüntüleri kullanma Not [bulut init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform tarafından yönetilmesi birçok yapılandırma görevleri hello Azure Linux Aracısı.</span><span class="sxs-lookup"><span data-stu-id="cc98d-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform many configuration tasks that would otherwise be managed by hello Azure Linux Agent.</span></span>  <span data-ttu-id="cc98d-301">Lütfen aşağıdaki farkları hello dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="cc98d-301">Please note hello following differences:</span></span>

* <span data-ttu-id="cc98d-302">**Provisioning.Enabled** Varsayılanları "Çok Ubuntu bulut görüntülerinde görevleri sağlama bulut init tooperform kullanan n".</span><span class="sxs-lookup"><span data-stu-id="cc98d-302">**Provisioning.Enabled** defaults too"n" on Ubuntu Cloud Images that use cloud-init tooperform provisioning tasks.</span></span>
* <span data-ttu-id="cc98d-303">yapılandırma parametreleri aşağıdaki hello Ubuntu bulut görüntüleri'de, disk ve takas bulut init toomanage hello kaynak alanı kullanmak üzerinde hiçbir etkisi yoktur:</span><span class="sxs-lookup"><span data-stu-id="cc98d-303">hello following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init toomanage hello resource disk and swap space:</span></span>
  
  * <span data-ttu-id="cc98d-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="cc98d-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="cc98d-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="cc98d-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="cc98d-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="cc98d-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="cc98d-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="cc98d-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="cc98d-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="cc98d-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="cc98d-309">Lütfen kaynakları tooconfigure hello kaynak disk bağlama noktası aşağıdaki hello bakın ve sağlama işlemi sırasında değiştirme alanı Ubuntu bulut görüntülerinde:</span><span class="sxs-lookup"><span data-stu-id="cc98d-309">Please see hello following resources tooconfigure hello resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="cc98d-310">Ubuntu Wiki: Takas bölümlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cc98d-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="cc98d-311">Bir Azure sanal makinesine özel veri injecting</span><span class="sxs-lookup"><span data-stu-id="cc98d-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

