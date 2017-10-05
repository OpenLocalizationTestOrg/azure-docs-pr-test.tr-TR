---
title: "Mobility hizmetinin (VMware veya fiziksel Azure) yükleme | Microsoft Docs"
description: "Şirket içi bilgisayarları korumak için Mobility hizmeti aracısı yüklemeyi öğrenin."
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
ms.openlocfilehash: 848284f37ae2470a169d8f8a8c9c0bb5b926abe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a><span data-ttu-id="fb0f6-103">Mobility hizmetinin (VMware veya fiziksel Azure) yükleyin</span><span class="sxs-lookup"><span data-stu-id="fb0f6-103">Install Mobility Service (VMware or physical to Azure)</span></span>
<span data-ttu-id="fb0f6-104">Azure Site Recovery Mobility hizmeti, bir bilgisayardaki veri yazma yakalar ve bunları işlem sunucusuna gönderir.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them to the process server.</span></span> <span data-ttu-id="fb0f6-105">Azure'a çoğaltmak istediğiniz her bilgisayarda (VMware VM veya fiziksel sunucu) için Mobility hizmetini dağıtın.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-105">Deploy Mobility Service to every computer (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="fb0f6-106">Mobility hizmeti aşağıdaki yöntemleri kullanarak korumak istediğiniz sunucuları dağıtabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-106">You can deploy Mobility Service to the servers that you want to protect by using the following methods:</span></span>


* [<span data-ttu-id="fb0f6-107">Mobility hizmeti yazılım dağıtım araçları gibi System Center Configuration Manager kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="fb0f6-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="fb0f6-108">Mobility hizmeti Azure Automation ve istenen durum yapılandırması (Automation DSC) kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="fb0f6-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="fb0f6-109">Grafik kullanıcı arabirimi (GUI) kullanarak Mobility hizmeti el ile yükleyin</span><span class="sxs-lookup"><span data-stu-id="fb0f6-109">Install Mobility Service manually by using the graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="fb0f6-110">Mobility hizmeti el ile bir komut isteminden yükleme</span><span class="sxs-lookup"><span data-stu-id="fb0f6-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="fb0f6-111">Azure Site Recovery anında yüklemesinden tarafından Mobility hizmetini yükleme</span><span class="sxs-lookup"><span data-stu-id="fb0f6-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="fb0f6-112">Mobility hizmeti sürümü 9.7.0.0, Windows sanal makinelerde (VM'ler) başlayarak yükleyici de en son kullanılabilir yükler [Azure VM Aracısı](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span><span class="sxs-lookup"><span data-stu-id="fb0f6-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), the Mobility Service installer also installs the latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="fb0f6-113">Bir bilgisayar üzerinden Azure'a başarısız olduğunda, bilgisayarın tüm VM uzantısı kullanılarak için önkoşul aracı yüklemesi karşılar.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-113">When a computer fails over to Azure, the computer meets the agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb0f6-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fb0f6-114">Prerequisites</span></span>
<span data-ttu-id="fb0f6-115">Sunucunuzda el ile Mobility hizmetini yüklemeden önce önkoşul adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="fb0f6-116">Yapılandırma sunucusunda oturum açın ve ardından yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-116">Sign in to your configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="fb0f6-117">Bin klasörüne dizini değiştirin ve ardından bir parola dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-117">Change the directory to the bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="fb0f6-118">Parola dosyasını güvenli bir konumda depolayın.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-118">Store the passphrase file in a secure location.</span></span> <span data-ttu-id="fb0f6-119">Mobility hizmeti yüklemesi sırasında dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-119">You use the file during the Mobility Service installation.</span></span>
4. <span data-ttu-id="fb0f6-120">Tüm desteklenen işletim sistemleri için Mobility hizmeti yükleyiciler %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-120">Mobility Service installers for all supported operating systems are in the %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="fb0f6-121">Mobility hizmeti işletim yükleyici sistem eşlemesi</span><span class="sxs-lookup"><span data-stu-id="fb0f6-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="fb0f6-122">Yükleyici dosyası şablonu adı</span><span class="sxs-lookup"><span data-stu-id="fb0f6-122">Installer file template name</span></span>| <span data-ttu-id="fb0f6-123">İşletim sistemi</span><span class="sxs-lookup"><span data-stu-id="fb0f6-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="fb0f6-124">Microsoft ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="fb0f6-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="fb0f6-125">Windows Server 2008 R2 SP1 (64 bit)</span><span class="sxs-lookup"><span data-stu-id="fb0f6-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="fb0f6-126">Windows Server 2012 (64 bit)</span><span class="sxs-lookup"><span data-stu-id="fb0f6-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="fb0f6-127">Windows Server 2012 R2 (64 bit)</span><span class="sxs-lookup"><span data-stu-id="fb0f6-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="fb0f6-128">Microsoft ASR\_UA\*RHEL6 64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="fb0f6-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="fb0f6-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6,8 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="fb0f6-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="fb0f6-130">CentOS 6.4 6.5, 6.6, 6.7, 6,8 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="fb0f6-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="fb0f6-131">Microsoft ASR\_UA\*RHEL7 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="fb0f6-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="fb0f6-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="fb0f6-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="fb0f6-133">CentOS 7.0, 7.1, 7.2 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="fb0f6-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="fb0f6-134">CentOs 7.3 (yalnızca geçiş)</span><span class="sxs-lookup"><span data-stu-id="fb0f6-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="fb0f6-135">Microsoft ASR\_UA\*SLES11 SP3 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="fb0f6-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="fb0f6-136">SUSE Linux Enterprise Server 11 SP3 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="fb0f6-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="fb0f6-137">Microsoft ASR\_UA\*SLES11 SP4 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="fb0f6-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="fb0f6-138">SUSE Linux Enterprise Server 11 SP4 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="fb0f6-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="fb0f6-139">Microsoft ASR\_UA\*OL6 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="fb0f6-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="fb0f6-140">Oracle Enterprise Linux 6.4, 6.5 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="fb0f6-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="fb0f6-141">Microsoft ASR\_UA\*UBUNTU 14.04 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="fb0f6-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="fb0f6-142">Ubuntu Linux 14.04 (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="fb0f6-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-the-gui"></a><span data-ttu-id="fb0f6-143">GUI kullanarak Mobility hizmeti el ile yükleyin</span><span class="sxs-lookup"><span data-stu-id="fb0f6-143">Install Mobility Service manually by using the GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="fb0f6-144">Kullanıyorsanız bir **yapılandırma sunucusu** çoğaltmak için **Azure Iaas sanal makineleri** gelen bir Azure aboneliği/bölge sonra başka bir **komut satırı tabanlı yükleme kullanmak** yöntemi</span><span class="sxs-lookup"><span data-stu-id="fb0f6-144">If you are using a **Configuration Server** to replicate **Azure IaaS virtual machines** from one Azure Subscription/Region to another then **use the Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="fb0f6-145">Mobility hizmeti el ile bir komut isteminden yükleme</span><span class="sxs-lookup"><span data-stu-id="fb0f6-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="fb0f6-146">Bir Windows bilgisayarda komut satırı yüklemesi</span><span class="sxs-lookup"><span data-stu-id="fb0f6-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="fb0f6-147">Linux bilgisayarda komut satırı yükleme</span><span class="sxs-lookup"><span data-stu-id="fb0f6-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="fb0f6-148">Azure Site Recovery anında yüklemesinden tarafından Mobility hizmetini yükleme</span><span class="sxs-lookup"><span data-stu-id="fb0f6-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="fb0f6-149">Site RECOVERY'yi kullanarak mobilite hizmetinin göndermeli yüklemesi yapmak için tüm hedef bilgisayarlar aşağıdaki önkoşulları karşılamalıdır.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-149">To do a push installation of Mobility Service by using Site Recovery, all target computers must meet the following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="fb0f6-150">Mobility hizmeti, Azure portalında yükledikten sonra seçin **çoğaltmak** bu sanal makineleri korumaya başlamak için Başlat.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-150">After Mobility Service is installed, in the Azure portal, select the **Replicate** button to start protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="fb0f6-151">Bir Windows Server bilgisayarında Mobility hizmetini kaldırma</span><span class="sxs-lookup"><span data-stu-id="fb0f6-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="fb0f6-152">Bir Windows Server bilgisayarında Mobility hizmetini kaldırmak için aşağıdaki yöntemlerden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-152">Use one of the following methods to uninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-the-gui"></a><span data-ttu-id="fb0f6-153">GUI kullanarak kaldırma</span><span class="sxs-lookup"><span data-stu-id="fb0f6-153">Uninstall by using the GUI</span></span>
1. <span data-ttu-id="fb0f6-154">Denetim Masası'nda seçin **programlar**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="fb0f6-155">Seçin **Microsoft Azure Site Recovery Mobility hizmeti/ana hedef sunucu**ve ardından **kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="fb0f6-156">Bir komut isteminde kaldırma</span><span class="sxs-lookup"><span data-stu-id="fb0f6-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="fb0f6-157">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="fb0f6-158">Mobility hizmetini kaldırmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-158">To uninstall Mobility Service, run the following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="fb0f6-159">Bir Linux bilgisayarda Mobility hizmetini kaldırma</span><span class="sxs-lookup"><span data-stu-id="fb0f6-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="fb0f6-160">Linux sunucunuzda olarak oturum açın bir **kök** kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="fb0f6-161">Bir terminale için /user/local/ASR gidin.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="fb0f6-162">Mobility hizmetini kaldırmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-162">To uninstall Mobility Service, run the following command:</span></span>

```
uninstall.sh -Y
```
