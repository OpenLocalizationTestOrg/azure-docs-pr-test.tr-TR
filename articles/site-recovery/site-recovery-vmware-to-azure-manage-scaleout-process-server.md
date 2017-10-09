---
title: " Bir genişleme işlem sunucusu Azure Site kurtarma yönetme | Microsoft Docs"
description: "Bu makalede nasıl tooset ayarlama ve bir genişleme işlem sunucusu Azure Site kurtarma yönetme."
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="278b0-103">Bir genişleme işlem sunucusu yönetme</span><span class="sxs-lookup"><span data-stu-id="278b0-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="278b0-104">Genişleme işlem sunucusu hello Site kurtarma Hizmetleri ve şirket içi altyapınızı arasında veri aktarmak için bir düzenleyici gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="278b0-104">Scale-out Process Server acts as a coordinator for data transfer between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="278b0-105">Bu makalede nasıl ayarlamak, yapılandırabilir ve bir genişleme işlem sunucusu yönetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="278b0-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="278b0-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="278b0-106">Prerequisites</span></span>
<span data-ttu-id="278b0-107">Merhaba önerilen donanım, yazılım ve ağ yapılandırma gerekli tooset bir genişleme işlem sunucusu Hello aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="278b0-107">hello following are hello recommended hardware, software, and network configuration required tooset up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="278b0-108">[Kapasite planlama](site-recovery-capacity-planner.md) hello genişleme işlem sunucusu bir yapılandırma ile bu paketleri dağıtmak için önemli adım tooensure olan yük gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="278b0-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="278b0-109">Daha fazla bilgi edinin [özellikleri için bir genişleme işlem sunucusu ölçeklendirme](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="278b0-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a><span data-ttu-id="278b0-110">Merhaba genişleme işlem sunucusu yazılım indirme</span><span class="sxs-lookup"><span data-stu-id="278b0-110">Downloading hello Scale-out Process Server software</span></span>
1. <span data-ttu-id="278b0-111">Toohello üzerinde Azure portal ve göz atma tooyour kurtarma Hizmetleri kasası oturum açın.</span><span class="sxs-lookup"><span data-stu-id="278b0-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="278b0-112">Çok Gözat**Site Recovery altyapısı** > **yapılandırma sunucularına** (altında For VMware ve fiziksel makineler).</span><span class="sxs-lookup"><span data-stu-id="278b0-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="278b0-113">Yapılandırma sunucusu toodrill aşağı hello yapılandırma sunucunun ayrıntıları sayfasına seçin.</span><span class="sxs-lookup"><span data-stu-id="278b0-113">Select your configuration server toodrill down into hello configuration server's details page.</span></span>
4. <span data-ttu-id="278b0-114">Merhaba tıklatın **+ işlem sunucusu** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="278b0-114">Click hello **+ Process Server** button.</span></span>
5. <span data-ttu-id="278b0-115">Merhaba, **eklemek işlem sunucusu** sayfasında, **dağıtma bir genişleme işlem sunucusu şirket içi** hello seçeneğinden **istediğiniz toodeploy işlem sunucunuzu seçin** aşağı açılır.</span><span class="sxs-lookup"><span data-stu-id="278b0-115">In hello **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from hello **Choose where you want toodeploy your process server** drop-down.</span></span>

  ![Sunucuları Sayfası Ekle](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="278b0-117">Merhaba tıklatın **indirme hello Microsoft Azure Site Recovery birleşik Kurulumu** bağlantı toodownload hello en son sürümünü hello genişleme işlem sunucusu yükleme.</span><span class="sxs-lookup"><span data-stu-id="278b0-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="278b0-118">Merhaba, genişleme işlem sunucusu sürümü aynı olmalıdır tooor ortamınızda çalışan hello yapılandırma sunucusu sürümden daha düşük.</span><span class="sxs-lookup"><span data-stu-id="278b0-118">hello version of your Scale-out Process Server should be equal tooor lesser than hello Configuration Server version running in your environment.</span></span> <span data-ttu-id="278b0-119">Basit bir yol tooensure sürüm uyumluluğu toouse olan hello tooinstall/güncelleştirme son yapılandırma sunucunuz kullanılan aynı yükleyici BITS.</span><span class="sxs-lookup"><span data-stu-id="278b0-119">A simple way tooensure version compatibility is toouse hello same installer bits that you recently used tooinstall/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="278b0-120">Yükleme ve bir genişleme işlem sunucusu GUI'den kaydetme</span><span class="sxs-lookup"><span data-stu-id="278b0-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="278b0-121">Dağıtımınızı 200 kaynak makinelerden ötesinde çıkışı tooscale varsa veya toplam günlük karmaşıklığı 2 TB'den fazla oranını ek işlem sunucuları toohandle hello trafik hacmi gerekir.</span><span class="sxs-lookup"><span data-stu-id="278b0-121">If you have tooscale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers toohandle hello traffic volume.</span></span>

<span data-ttu-id="278b0-122">Merhaba denetleyin [boyut işlem sunucuları için öneriler](#size-recommendations-for-the-process-server)ve ardından bu yönergeleri tooset hello işlem sunucusu izleyin.</span><span class="sxs-lookup"><span data-stu-id="278b0-122">Check hello [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions tooset up hello process server.</span></span> <span data-ttu-id="278b0-123">Kaynak makine toouse geçirmek Hello sunucuyu ayarladıktan sonra onu.</span><span class="sxs-lookup"><span data-stu-id="278b0-123">After setting up hello server, you migrate source machines toouse it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="278b0-124">Yükleme ve komut satırı kullanarak bir genişleme işlem sunucusu kaydetme</span><span class="sxs-lookup"><span data-stu-id="278b0-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="278b0-125">Örnek Kullanım</span><span class="sxs-lookup"><span data-stu-id="278b0-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="278b0-126">Genişleme işlem sunucusu Yükleyici komut satırı bağımsız değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="278b0-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="278b0-127">Proxy ayarlarını yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="278b0-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="278b0-128">ProxySettingsFilePath parametresi bir dosya girdi olarak alır.</span><span class="sxs-lookup"><span data-stu-id="278b0-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="278b0-129">Aşağıdaki biçimlendirmek ve giriş ProxySettingsFilePath parametre olarak geçirmek hello kullanarak dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="278b0-129">Create file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="278b0-130">Genişleme işlem sunucusu için proxy ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="278b0-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="278b0-131">Genişleme işlem sunucusu uygulamasına oturum açın.</span><span class="sxs-lookup"><span data-stu-id="278b0-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="278b0-132">Bir yönetici PowerShell komut penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="278b0-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="278b0-133">Merhaba aşağıdaki komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="278b0-133">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="278b0-134">Sonraki toohello dizin taraması **%PROGRAMDATA%\ASR\Agent** ve çalışma hello aşağıdaki komutu</span><span class="sxs-lookup"><span data-stu-id="278b0-134">Next browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="278b0-135">Bir genişleme işlem sunucusu yeniden kaydetme</span><span class="sxs-lookup"><span data-stu-id="278b0-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="278b0-136">Sonraki bir yönetici komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="278b0-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="278b0-137">Toohello dizin taraması **%PROGRAMDATA%\ASR\Agent** ve hello komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="278b0-137">Browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="278b0-138">Bir genişleme işlem sunucusu yükseltme</span><span class="sxs-lookup"><span data-stu-id="278b0-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="278b0-139">Bir genişleme işlem sunucusu yetkisini alma</span><span class="sxs-lookup"><span data-stu-id="278b0-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="278b0-140">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="278b0-140">Ensure that:</span></span>
  - <span data-ttu-id="278b0-141">Yapılandırma sunucusunun bağlantı durumunu gösterir olarak **bağlı** hello Azure portal'ın</span><span class="sxs-lookup"><span data-stu-id="278b0-141">Configuration Server's connection state shows as **Connected** in hello Azure portal</span></span>
  - <span data-ttu-id="278b0-142">İşlem sunucusunun hello yapılandırma sunucusu ile koruyabilmeyi toocommunicate ' dir.</span><span class="sxs-lookup"><span data-stu-id="278b0-142">Process Server's is still able toocommunicate with hello Configuration server.</span></span>
2. <span data-ttu-id="278b0-143">Toohello işlem sunucusunda bir yönetici olarak oturum</span><span class="sxs-lookup"><span data-stu-id="278b0-143">Log in toohello process server as an administrator</span></span>
3. <span data-ttu-id="278b0-144">Denetim Masası açın > Program > programları Kaldır</span><span class="sxs-lookup"><span data-stu-id="278b0-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="278b0-145">Merhaba programları aşağıdaki verilen hello sırayla kaldırın:</span><span class="sxs-lookup"><span data-stu-id="278b0-145">Uninstall hello programs in hello sequence given following:</span></span>
  * <span data-ttu-id="278b0-146">Microsoft Azure Site kurtarma yapılandırması sunucu/işlem sunucusu</span><span class="sxs-lookup"><span data-stu-id="278b0-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="278b0-147">Microsoft Azure Site kurtarma yapılandırması sunucu bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="278b0-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="278b0-148">Microsoft Azure Kurtarma Hizmetleri Aracısı</span><span class="sxs-lookup"><span data-stu-id="278b0-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="278b0-149">Hello Azure portal, hello işlem sunucusu silme tooreflect yukarı too15 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="278b0-149">It can take up-too15 minutes for hello Process Server deletion tooreflect in hello Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="278b0-150">Merhaba işlem sunucusu hello yapılandırma sunucusu ile oluşturulamıyor toocommunicate olup olmadığını (Portalı'nda bağlantı durumu kesilir) yeniden toofollow gerekiyor hello adımları toopurge, yapılandırma sunucusu hello.</span><span class="sxs-lookup"><span data-stu-id="278b0-150">If hello Process server is unable toocommunicate with hello Configuration Server (Connection State in portal is Disconnected), then you need toofollow hello following steps toopurge it from hello Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="278b0-151">Bağlantısı kesilmiş bir genişleme işlem sunucusu bir yapılandırma sunucusundan kaydını silme</span><span class="sxs-lookup"><span data-stu-id="278b0-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="278b0-152">Bir genişleme işlem sunucusu için gereksinimleri boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="278b0-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="278b0-153">**Ek işlem sunucusu**</span><span class="sxs-lookup"><span data-stu-id="278b0-153">**Additional process server**</span></span> | <span data-ttu-id="278b0-154">**Önbellek disk boyutu**</span><span class="sxs-lookup"><span data-stu-id="278b0-154">**Cache disk size**</span></span> | <span data-ttu-id="278b0-155">**Veri değişikliği oranı**</span><span class="sxs-lookup"><span data-stu-id="278b0-155">**Data change rate**</span></span> | <span data-ttu-id="278b0-156">**Korumalı makineler**</span><span class="sxs-lookup"><span data-stu-id="278b0-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="278b0-157">4 Vcpu (2 yuva * 2,5 GHz @ 2 Çekirdek), 8 GB bellek</span><span class="sxs-lookup"><span data-stu-id="278b0-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="278b0-158">300 GB</span><span class="sxs-lookup"><span data-stu-id="278b0-158">300 GB</span></span> |<span data-ttu-id="278b0-159">250 GB veya daha az</span><span class="sxs-lookup"><span data-stu-id="278b0-159">250 GB or less</span></span> |<span data-ttu-id="278b0-160">85 veya daha az makine çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="278b0-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="278b0-161">8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek), 12 GB bellek</span><span class="sxs-lookup"><span data-stu-id="278b0-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="278b0-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="278b0-162">600 GB</span></span> |<span data-ttu-id="278b0-163">250 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="278b0-163">250 GB too1 TB</span></span> |<span data-ttu-id="278b0-164">85 150 makineler arasında çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="278b0-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="278b0-165">12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek) 24 GB bellek</span><span class="sxs-lookup"><span data-stu-id="278b0-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="278b0-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="278b0-166">1 TB</span></span> |<span data-ttu-id="278b0-167">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="278b0-167">1 TB too2 TB</span></span> |<span data-ttu-id="278b0-168">150-225 makineler arasında çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="278b0-168">Replicate between 150-225 machines.</span></span> |
