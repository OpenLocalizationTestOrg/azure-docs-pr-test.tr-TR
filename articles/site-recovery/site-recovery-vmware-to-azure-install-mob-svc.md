---
title: aaaInstall Mobility hizmetinin (VMware veya fiziksel tooAzure) | Microsoft Docs
description: "Nasıl tooinstall hello Mobility Hizmeti Aracısı tooprotect şirket içi bilgisayarlarınızı öğrenin."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a><span data-ttu-id="adf6b-103">Mobility hizmetinin (VMware veya fiziksel tooAzure) yükleyin</span><span class="sxs-lookup"><span data-stu-id="adf6b-103">Install Mobility Service (VMware or physical tooAzure)</span></span>
<span data-ttu-id="adf6b-104">Azure Site Recovery Mobility hizmeti, bir bilgisayardaki veri yazma yakalar ve bunları toohello işlem sunucusuna iletir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them toohello process server.</span></span> <span data-ttu-id="adf6b-105">Tooreplicate tooAzure istediğiniz Mobility hizmeti tooevery bilgisayar (VMware VM veya fiziksel sunucu) dağıtın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-105">Deploy Mobility Service tooevery computer (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="adf6b-106">Mobility hizmeti toohello sunucuları hello aşağıdaki yöntemleri kullanarak tooprotect istediğiniz dağıtabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="adf6b-106">You can deploy Mobility Service toohello servers that you want tooprotect by using hello following methods:</span></span>


* [<span data-ttu-id="adf6b-107">Mobility hizmeti yazılım dağıtım araçları gibi System Center Configuration Manager kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="adf6b-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="adf6b-108">Mobility hizmeti Azure Automation ve istenen durum yapılandırması (Automation DSC) kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="adf6b-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="adf6b-109">Merhaba grafik kullanıcı arabirimi (GUI) kullanarak Mobility hizmeti el ile yükleyin</span><span class="sxs-lookup"><span data-stu-id="adf6b-109">Install Mobility Service manually by using hello graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="adf6b-110">Mobility hizmeti el ile bir komut isteminden yükleme</span><span class="sxs-lookup"><span data-stu-id="adf6b-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="adf6b-111">Azure Site Recovery anında yüklemesinden tarafından Mobility hizmetini yükleme</span><span class="sxs-lookup"><span data-stu-id="adf6b-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="adf6b-112">Sürüm 9.7.0.0, Windows sanal makinelerde (VM'ler) ile başlayan hello Mobility Hizmeti Yükleyici de hello en son kullanılabilir yükler [Azure VM Aracısı](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span><span class="sxs-lookup"><span data-stu-id="adf6b-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), hello Mobility Service installer also installs hello latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="adf6b-113">Bir bilgisayar tooAzure başarısız olduğunda, hello bilgisayar hello aracı yüklemesi VM uzantıyı kullanmak için önkoşul karşılar.</span><span class="sxs-lookup"><span data-stu-id="adf6b-113">When a computer fails over tooAzure, hello computer meets hello agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="adf6b-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="adf6b-114">Prerequisites</span></span>
<span data-ttu-id="adf6b-115">Sunucunuzda el ile Mobility hizmetini yüklemeden önce önkoşul adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="adf6b-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="adf6b-116">Tooyour yapılandırma sunucusunda oturum açın ve ardından yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-116">Sign in tooyour configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="adf6b-117">Merhaba dizin toohello bin klasörü değiştirin ve ardından bir parola dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="adf6b-117">Change hello directory toohello bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="adf6b-118">Merhaba parola dosyasını güvenli bir konumda depolayın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-118">Store hello passphrase file in a secure location.</span></span> <span data-ttu-id="adf6b-119">Merhaba Mobility hizmeti yüklemesi sırasında hello dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-119">You use hello file during hello Mobility Service installation.</span></span>
4. <span data-ttu-id="adf6b-120">Tüm desteklenen işletim sistemleri için Mobility hizmeti yükleyiciler hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository klasöründe yer alır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-120">Mobility Service installers for all supported operating systems are in hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="adf6b-121">Mobility hizmeti işletim yükleyici sistem eşlemesi</span><span class="sxs-lookup"><span data-stu-id="adf6b-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="adf6b-122">Yükleyici dosyası şablonu adı</span><span class="sxs-lookup"><span data-stu-id="adf6b-122">Installer file template name</span></span>| <span data-ttu-id="adf6b-123">İşletim sistemi</span><span class="sxs-lookup"><span data-stu-id="adf6b-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="adf6b-124">Microsoft ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="adf6b-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="adf6b-125">Windows Server 2008 R2 SP1 (64 bit)</span><span class="sxs-lookup"><span data-stu-id="adf6b-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="adf6b-126">Windows Server 2012 (64 bit)</span><span class="sxs-lookup"><span data-stu-id="adf6b-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="adf6b-127">Windows Server 2012 R2 (64 bit)</span><span class="sxs-lookup"><span data-stu-id="adf6b-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="adf6b-128">Microsoft ASR\_UA\*RHEL6 64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="adf6b-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="adf6b-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6,8 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="adf6b-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="adf6b-130">CentOS 6.4 6.5, 6.6, 6.7, 6,8 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="adf6b-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="adf6b-131">Microsoft ASR\_UA\*RHEL7 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="adf6b-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="adf6b-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="adf6b-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="adf6b-133">CentOS 7.0, 7.1, 7.2 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="adf6b-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="adf6b-134">CentOs 7.3 (yalnızca geçiş)</span><span class="sxs-lookup"><span data-stu-id="adf6b-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="adf6b-135">Microsoft ASR\_UA\*SLES11 SP3 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="adf6b-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="adf6b-136">SUSE Linux Enterprise Server 11 SP3 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="adf6b-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="adf6b-137">Microsoft ASR\_UA\*SLES11 SP4 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="adf6b-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="adf6b-138">SUSE Linux Enterprise Server 11 SP4 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="adf6b-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="adf6b-139">Microsoft ASR\_UA\*OL6 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="adf6b-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="adf6b-140">Oracle Enterprise Linux 6.4, 6.5 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="adf6b-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="adf6b-141">Microsoft ASR\_UA\*UBUNTU 14.04 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="adf6b-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="adf6b-142">Ubuntu Linux 14.04 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="adf6b-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a><span data-ttu-id="adf6b-143">Merhaba GUI kullanarak Mobility hizmeti el ile yükleyin</span><span class="sxs-lookup"><span data-stu-id="adf6b-143">Install Mobility Service manually by using hello GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="adf6b-144">Kullanıyorsanız bir **yapılandırma sunucusu** tooreplicate **Azure Iaas sanal makineleri** bir Azure aboneliği/bölge tooanother sonra gelen **hello komut satırı tabanlı yükleme kullanmak**  yöntemi</span><span class="sxs-lookup"><span data-stu-id="adf6b-144">If you are using a **Configuration Server** tooreplicate **Azure IaaS virtual machines** from one Azure Subscription/Region tooanother then **use hello Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="adf6b-145">Mobility hizmeti el ile bir komut isteminden yükleme</span><span class="sxs-lookup"><span data-stu-id="adf6b-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="adf6b-146">Bir Windows bilgisayarda komut satırı yüklemesi</span><span class="sxs-lookup"><span data-stu-id="adf6b-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="adf6b-147">Linux bilgisayarda komut satırı yükleme</span><span class="sxs-lookup"><span data-stu-id="adf6b-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="adf6b-148">Azure Site Recovery anında yüklemesinden tarafından Mobility hizmetini yükleme</span><span class="sxs-lookup"><span data-stu-id="adf6b-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="adf6b-149">toodo Site Recovery kullanarak bir itme yüklemesini Mobility hizmeti, tüm hedef bilgisayarlar aşağıdaki önkoşulları hello karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-149">toodo a push installation of Mobility Service by using Site Recovery, all target computers must meet hello following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="adf6b-150">Mobility hizmeti, hello Azure portal yükledikten sonra hello seçin **çoğaltmak** düğmesini toostart bu Vm'leri koruma.</span><span class="sxs-lookup"><span data-stu-id="adf6b-150">After Mobility Service is installed, in hello Azure portal, select hello **Replicate** button toostart protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="adf6b-151">Bir Windows Server bilgisayarında Mobility hizmetini kaldırma</span><span class="sxs-lookup"><span data-stu-id="adf6b-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="adf6b-152">Bir Windows Server bilgisayarında yöntemleri toouninstall Mobility hizmeti aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-152">Use one of hello following methods toouninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-hello-gui"></a><span data-ttu-id="adf6b-153">Merhaba GUI kullanarak kaldırma</span><span class="sxs-lookup"><span data-stu-id="adf6b-153">Uninstall by using hello GUI</span></span>
1. <span data-ttu-id="adf6b-154">Denetim Masası'nda seçin **programlar**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="adf6b-155">Seçin **Microsoft Azure Site Recovery Mobility hizmeti/ana hedef sunucu**ve ardından **kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="adf6b-156">Bir komut isteminde kaldırma</span><span class="sxs-lookup"><span data-stu-id="adf6b-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="adf6b-157">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="adf6b-158">Mobility hizmeti toouninstall hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="adf6b-158">toouninstall Mobility Service, run hello following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="adf6b-159">Bir Linux bilgisayarda Mobility hizmetini kaldırma</span><span class="sxs-lookup"><span data-stu-id="adf6b-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="adf6b-160">Linux sunucunuzda olarak oturum açın bir **kök** kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="adf6b-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="adf6b-161">Bir terminale çok/kullanıcı/yerel/ASR gidin.</span><span class="sxs-lookup"><span data-stu-id="adf6b-161">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="adf6b-162">Mobility hizmeti toouninstall hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="adf6b-162">toouninstall Mobility Service, run hello following command:</span></span>

```
uninstall.sh -Y
```
