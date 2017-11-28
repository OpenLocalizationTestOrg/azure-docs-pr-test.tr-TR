---
title: " Bir genişleme işlem sunucusu Azure Site kurtarma yönetme | Microsoft Docs"
description: "Bu makalede, bir genişleme işlem sunucusu Azure Site kurtarma ayarlamanıza açıklar."
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
ms.openlocfilehash: e5c01de19917235c34c035415df86291b9152bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="018bd-103">Bir genişleme işlem sunucusu yönetme</span><span class="sxs-lookup"><span data-stu-id="018bd-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="018bd-104">Genişleme işlem sunucusu Site kurtarma Hizmetleri ve şirket içi altyapınızı arasında veri aktarmak için bir düzenleyici gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="018bd-104">Scale-out Process Server acts as a coordinator for data transfer between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="018bd-105">Bu makalede nasıl ayarlamak, yapılandırabilir ve bir genişleme işlem sunucusu yönetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="018bd-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="018bd-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="018bd-106">Prerequisites</span></span>
<span data-ttu-id="018bd-107">Önerilen donanım, yazılım ve bir genişleme işlem sunucusu kurmak için gereken ağ yapılandırması şunlardır:</span><span class="sxs-lookup"><span data-stu-id="018bd-107">The following are the recommended hardware, software, and network configuration required to set up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="018bd-108">[Kapasite planlama](site-recovery-capacity-planner.md) yapılandırmasıyla genişleme işlem sunucusu bu paketleri dağıtmak emin olmak için önemli bir adım yük gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="018bd-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="018bd-109">Daha fazla bilgi edinin [özellikleri için bir genişleme işlem sunucusu ölçeklendirme](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="018bd-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-scale-out-process-server-software"></a><span data-ttu-id="018bd-110">Genişleme işlem sunucusu yazılım indirme</span><span class="sxs-lookup"><span data-stu-id="018bd-110">Downloading the Scale-out Process Server software</span></span>
1. <span data-ttu-id="018bd-111">Azure portalında oturum açın ve kurtarma Hizmetleri Kasası'na göz atın.</span><span class="sxs-lookup"><span data-stu-id="018bd-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="018bd-112">Gözat **Site Recovery altyapısı** > **yapılandırma sunucularına** (altında VMware ve fiziksel makineler için).</span><span class="sxs-lookup"><span data-stu-id="018bd-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="018bd-113">Yapılandırma sunucusunun ayrıntıları sayfasına detaya gitmek için yapılandırma sunucunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="018bd-113">Select your configuration server to drill down into the configuration server's details page.</span></span>
4. <span data-ttu-id="018bd-114">Tıklatın **+ işlem sunucusu** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="018bd-114">Click the **+ Process Server** button.</span></span>
5. <span data-ttu-id="018bd-115">İçinde **eklemek işlem sunucusu** sayfasında, **dağıtma bir genişleme işlem sunucusu şirket içi** gelen seçeneği **işlem sunucunuzu dağıtmak istediğiniz yeri seçin** açılır.</span><span class="sxs-lookup"><span data-stu-id="018bd-115">In the **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from the **Choose where you want to deploy your process server** drop-down.</span></span>

  ![Sunucuları Sayfası Ekle](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="018bd-117">Tıklatın **Microsoft Azure Site Recovery birleşik Kurulumu karşıdan** genişleme işlem sunucusu yükleme en son sürümünü indirmek için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="018bd-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="018bd-118">Genişleme işlem sunucusu sürümü eşit veya ortamınızda çalışan yapılandırma sunucusu sürümden daha düşük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="018bd-118">The version of your Scale-out Process Server should be equal to or lesser than the Configuration Server version running in your environment.</span></span> <span data-ttu-id="018bd-119">Sürüm uyumluluğu sağlamak için basit bir yol, yapılandırma sunucusu yüklemek/güncelleştirmek için kullanılan aynı yükleyici BITS kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="018bd-119">A simple way to ensure version compatibility is to use the same installer bits that you recently used to install/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="018bd-120">Yükleme ve bir genişleme işlem sunucusu GUI'den kaydetme</span><span class="sxs-lookup"><span data-stu-id="018bd-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="018bd-121">Varsa dağıtımınızı 200 kaynak makine ya da birden fazla 2 TB toplam günlük karmaşıklık oranı ötesine genişletmek için trafik hacmi işlemek için ek işlem sunucuları gerekir.</span><span class="sxs-lookup"><span data-stu-id="018bd-121">If you have to scale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers to handle the traffic volume.</span></span>

<span data-ttu-id="018bd-122">Denetleme [boyut işlem sunucuları için öneriler](#size-recommendations-for-the-process-server)ve işlem sunucusu kurmak için bu yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="018bd-122">Check the [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions to set up the process server.</span></span> <span data-ttu-id="018bd-123">Sunucuyu ayarladıktan sonra bunu kullanmak için kaynak makineleri geçirin.</span><span class="sxs-lookup"><span data-stu-id="018bd-123">After setting up the server, you migrate source machines to use it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="018bd-124">Yükleme ve komut satırı kullanarak bir genişleme işlem sunucusu kaydetme</span><span class="sxs-lookup"><span data-stu-id="018bd-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="018bd-125">Örnek Kullanım</span><span class="sxs-lookup"><span data-stu-id="018bd-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="018bd-126">Genişleme işlem sunucusu Yükleyici komut satırı bağımsız değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="018bd-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="018bd-127">Proxy ayarlarını yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="018bd-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="018bd-128">ProxySettingsFilePath parametresi bir dosya girdi olarak alır.</span><span class="sxs-lookup"><span data-stu-id="018bd-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="018bd-129">Aşağıdaki biçimi kullanarak dosya oluşturma ve giriş ProxySettingsFilePath parametresi olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="018bd-129">Create file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="018bd-130">Genişleme işlem sunucusu için proxy ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="018bd-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="018bd-131">Genişleme işlem sunucusu uygulamasına oturum açın.</span><span class="sxs-lookup"><span data-stu-id="018bd-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="018bd-132">Bir yönetici PowerShell komut penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="018bd-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="018bd-133">Aşağıdaki komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="018bd-133">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="018bd-134">Dizine'yanındaki Gözat **%PROGRAMDATA%\ASR\Agent** ve aşağıdaki komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="018bd-134">Next browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="018bd-135">Bir genişleme işlem sunucusu yeniden kaydetme</span><span class="sxs-lookup"><span data-stu-id="018bd-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="018bd-136">Sonraki bir yönetici komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="018bd-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="018bd-137">Dizine gözatın **%PROGRAMDATA%\ASR\Agent** ve şu komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="018bd-137">Browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="018bd-138">Bir genişleme işlem sunucusu yükseltme</span><span class="sxs-lookup"><span data-stu-id="018bd-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="018bd-139">Bir genişleme işlem sunucusu yetkisini alma</span><span class="sxs-lookup"><span data-stu-id="018bd-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="018bd-140">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="018bd-140">Ensure that:</span></span>
  - <span data-ttu-id="018bd-141">Yapılandırma sunucusunun bağlantı durumunu gösterir olarak **bağlı** Azure portalında</span><span class="sxs-lookup"><span data-stu-id="018bd-141">Configuration Server's connection state shows as **Connected** in the Azure portal</span></span>
  - <span data-ttu-id="018bd-142">İşlem sunucusunun yapılandırma sunucusu ile iletişim kurmak hala yapabiliyor.</span><span class="sxs-lookup"><span data-stu-id="018bd-142">Process Server's is still able to communicate with the Configuration server.</span></span>
2. <span data-ttu-id="018bd-143">İşlem sunucusu için bir yönetici olarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="018bd-143">Log in to the process server as an administrator</span></span>
3. <span data-ttu-id="018bd-144">Denetim Masası açın > Program > programları Kaldır</span><span class="sxs-lookup"><span data-stu-id="018bd-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="018bd-145">Aşağıdaki verilen dizisi programlarda kaldırın:</span><span class="sxs-lookup"><span data-stu-id="018bd-145">Uninstall the programs in the sequence given following:</span></span>
  * <span data-ttu-id="018bd-146">Microsoft Azure Site kurtarma yapılandırması sunucu/işlem sunucusu</span><span class="sxs-lookup"><span data-stu-id="018bd-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="018bd-147">Microsoft Azure Site kurtarma yapılandırması sunucu bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="018bd-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="018bd-148">Microsoft Azure Kurtarma Hizmetleri Aracısı</span><span class="sxs-lookup"><span data-stu-id="018bd-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="018bd-149">Azure portalında yansıtacak şekilde işlem sunucusu silme işlemi için 15 dakika kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="018bd-149">It can take up-to 15 minutes for the Process Server deletion to reflect in the Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="018bd-150">İşlem sunucusu yapılandırma sunucusuyla iletişim kuramıyor olup olmadığını (Portalı'nda bağlantı durumu bağlantı kesildi), sonra da yapılandırma sunucusundan temizlemek için aşağıdaki adımları izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="018bd-150">If the Process server is unable to communicate with the Configuration Server (Connection State in portal is Disconnected), then you need to follow the following steps to purge it from the Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="018bd-151">Bağlantısı kesilmiş bir genişleme işlem sunucusu bir yapılandırma sunucusundan kaydını silme</span><span class="sxs-lookup"><span data-stu-id="018bd-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="018bd-152">Bir genişleme işlem sunucusu için gereksinimleri boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="018bd-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="018bd-153">**Ek işlem sunucusu**</span><span class="sxs-lookup"><span data-stu-id="018bd-153">**Additional process server**</span></span> | <span data-ttu-id="018bd-154">**Önbellek disk boyutu**</span><span class="sxs-lookup"><span data-stu-id="018bd-154">**Cache disk size**</span></span> | <span data-ttu-id="018bd-155">**Veri değişikliği oranı**</span><span class="sxs-lookup"><span data-stu-id="018bd-155">**Data change rate**</span></span> | <span data-ttu-id="018bd-156">**Korumalı makineler**</span><span class="sxs-lookup"><span data-stu-id="018bd-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="018bd-157">4 Vcpu (2 yuva * 2,5 GHz @ 2 Çekirdek), 8 GB bellek</span><span class="sxs-lookup"><span data-stu-id="018bd-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="018bd-158">300 GB</span><span class="sxs-lookup"><span data-stu-id="018bd-158">300 GB</span></span> |<span data-ttu-id="018bd-159">250 GB veya daha az</span><span class="sxs-lookup"><span data-stu-id="018bd-159">250 GB or less</span></span> |<span data-ttu-id="018bd-160">85 veya daha az makine çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="018bd-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="018bd-161">8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek), 12 GB bellek</span><span class="sxs-lookup"><span data-stu-id="018bd-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="018bd-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="018bd-162">600 GB</span></span> |<span data-ttu-id="018bd-163">1 TB ' 250 GB</span><span class="sxs-lookup"><span data-stu-id="018bd-163">250 GB to 1 TB</span></span> |<span data-ttu-id="018bd-164">85 150 makineler arasında çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="018bd-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="018bd-165">12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek) 24 GB bellek</span><span class="sxs-lookup"><span data-stu-id="018bd-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="018bd-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="018bd-166">1 TB</span></span> |<span data-ttu-id="018bd-167">1 TB ile 2 TB</span><span class="sxs-lookup"><span data-stu-id="018bd-167">1 TB to 2 TB</span></span> |<span data-ttu-id="018bd-168">150-225 makineler arasında çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="018bd-168">Replicate between 150-225 machines.</span></span> |
