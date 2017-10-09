---
title: " Yapılandırma sunucusu Azure Site kurtarma yönetme | Microsoft Docs"
description: "Bu makalede nasıl tooset ve yapılandırma sunucusunu yönetebilirsiniz."
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
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="bc80a-103">Yapılandırma sunucusu yönetme</span><span class="sxs-lookup"><span data-stu-id="bc80a-103">Manage a Configuration Server</span></span>

<span data-ttu-id="bc80a-104">Yapılandırma sunucusu hello Site kurtarma Hizmetleri ile şirket içi altyapınızı arasında bir düzenleyici gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="bc80a-104">Configuration Server acts as a coordinator between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="bc80a-105">Bu makalede nasıl ayarlamak, yapılandırabilir ve hello yapılandırma sunucusu yönetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bc80a-105">This article describes how you can set up, configure, and manage hello Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc80a-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bc80a-106">Prerequisites</span></span>
<span data-ttu-id="bc80a-107">Merhaba en düşük donanım, yazılım ve ağ yapılandırma gerekli tooset bir yapılandırma sunucusu Hello aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bc80a-107">hello following are hello minimum hardware, software, and network configuration required tooset up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="bc80a-108">[Kapasite planlama](site-recovery-capacity-planner.md) hello yapılandırma sunucusu bir yapılandırma ile bu paketleri dağıtmak için önemli adım tooensure olan yük gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="bc80a-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="bc80a-109">Daha fazla bilgi edinin [yapılandırma sunucusu için gereksinimleri boyutlandırma](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="bc80a-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a><span data-ttu-id="bc80a-110">Merhaba yapılandırma sunucusu yazılım indirme</span><span class="sxs-lookup"><span data-stu-id="bc80a-110">Downloading hello Configuration Server software</span></span>
1. <span data-ttu-id="bc80a-111">Toohello üzerinde Azure portal ve göz atma tooyour kurtarma Hizmetleri kasası oturum açın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="bc80a-112">Çok Gözat**Site Recovery altyapısı** > **yapılandırma sunucularına** (altında For VMware ve fiziksel makineler).</span><span class="sxs-lookup"><span data-stu-id="bc80a-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Sunucuları Sayfası Ekle](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="bc80a-114">Merhaba tıklatın **+ sunucuları** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bc80a-114">Click hello **+Servers** button.</span></span>
4. <span data-ttu-id="bc80a-115">Merhaba üzerinde **Sunucu Ekle** sayfasında, hello karşıdan yükleme düğmesini toodownload hello kayıt anahtar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-115">On hello **Add Server** page, click hello Download button toodownload hello Registration key.</span></span> <span data-ttu-id="bc80a-116">Merhaba yapılandırma sunucusu yükleme tooregister sırasında bu anahtar gerekir Azure Site Recovery hizmeti ile.</span><span class="sxs-lookup"><span data-stu-id="bc80a-116">You need this key during hello Configuration Server installation tooregister it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="bc80a-117">Merhaba tıklatın **indirme hello Microsoft Azure Site Recovery birleşik Kurulumu** bağlantı toodownload hello en son sürümünü hello yapılandırma sunucusu.</span><span class="sxs-lookup"><span data-stu-id="bc80a-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Configuration Server.</span></span>

  ![Sayfayı Yükle](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="bc80a-119">Merhaba yapılandırma sunucusunun en son sürümünü, doğrudan indirilebilir [Microsoft Download Center indirme sayfası](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="bc80a-119">Latest version of hello Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="bc80a-120">Yükleme ve yapılandırma sunucusu GUI'den kaydetme</span><span class="sxs-lookup"><span data-stu-id="bc80a-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="bc80a-121">Yükleme ve komut satırını kullanarak bir yapılandırma sunucusu kaydetme</span><span class="sxs-lookup"><span data-stu-id="bc80a-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="bc80a-122">Örnek Kullanım</span><span class="sxs-lookup"><span data-stu-id="bc80a-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="bc80a-123">Yapılandırma sunucusu Yükleyici komut satırı bağımsız değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="bc80a-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="bc80a-124">Bir MySql kimlik bilgileri dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc80a-124">Create a MySql credentials file</span></span>
<span data-ttu-id="bc80a-125">MySQLCredsFilePath parametresi bir dosya girdi olarak alır.</span><span class="sxs-lookup"><span data-stu-id="bc80a-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="bc80a-126">Aşağıdaki biçimlendirmek ve giriş MySQLCredsFilePath parametre olarak geçirmek hello kullanarak hello dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bc80a-126">Create hello file using hello following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="bc80a-127">Proxy ayarlarını yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc80a-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="bc80a-128">ProxySettingsFilePath parametresi bir dosya girdi olarak alır.</span><span class="sxs-lookup"><span data-stu-id="bc80a-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="bc80a-129">Aşağıdaki biçimlendirmek ve giriş ProxySettingsFilePath parametre olarak geçirmek hello kullanarak hello dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bc80a-129">Create hello file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="bc80a-130">Yapılandırma sunucusu için proxy ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="bc80a-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="bc80a-131">Oturum açma tooyour yapılandırma sunucusu.</span><span class="sxs-lookup"><span data-stu-id="bc80a-131">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="bc80a-132">Merhaba kısayolunu kullanarak hello cspsconfigtool.exe başlatın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-132">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
3. <span data-ttu-id="bc80a-133">Merhaba tıklatın **kasa kayıt** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="bc80a-133">Click hello **Vault Registration** tab.</span></span>
4. <span data-ttu-id="bc80a-134">Yeni bir kasa kayıt dosyası hello portalından indirin ve giriş toohello aracı olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-134">Download a new Vault Registration file from hello portal and provide it as input toohello tool.</span></span>

  ![YAZMAÇ yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="bc80a-136">Merhaba yeni Proxy sunucusu ayrıntılarını sağlayın ve hello tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bc80a-136">Provide hello new Proxy Server details and click hello **Register** button.</span></span>
6. <span data-ttu-id="bc80a-137">Bir yönetici PowerShell komut penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="bc80a-138">Merhaba aşağıdaki komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bc80a-138">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="bc80a-139">Varsa genişleme işlem sunucuları toothis yapılandırma sunucusu bağlı, çok gerek[hello proxy ayarları tüm hello genişleme işlem sunucularında düzeltme](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) dağıtımınızdaki.</span><span class="sxs-lookup"><span data-stu-id="bc80a-139">If you have Scale-out Process servers attached toothis Configuration Server, you need too[fix hello proxy settings on all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a><span data-ttu-id="bc80a-140">Merhaba yapılandırma sunucusuyla yeniden kaydettirin aynı kurtarma Hizmetleri kasası</span><span class="sxs-lookup"><span data-stu-id="bc80a-140">Re-register a Configuration Server with hello same Recovery Services Vault</span></span>
  1. <span data-ttu-id="bc80a-141">Oturum açma tooyour yapılandırma sunucusu.</span><span class="sxs-lookup"><span data-stu-id="bc80a-141">Login tooyour Configuration Server.</span></span>
  2. <span data-ttu-id="bc80a-142">Merhaba cspsconfigtool.exe masaüstünüzde Hello kısayolunu kullanarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-142">Launch hello cspsconfigtool.exe using hello shortcut on your desktop.</span></span>
  3. <span data-ttu-id="bc80a-143">Merhaba tıklatın **kasa kayıt** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="bc80a-143">Click hello **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="bc80a-144">Yeni bir kayıt dosyası hello portalından indirin ve giriş toohello aracı olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-144">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>
        <span data-ttu-id="bc80a-145">![YAZMAÇ yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="bc80a-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="bc80a-146">Merhaba Proxy sunucusu detayları sağlayın ve hello tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bc80a-146">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
  6. <span data-ttu-id="bc80a-147">Bir yönetici PowerShell komut penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="bc80a-148">Merhaba aşağıdaki komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bc80a-148">Run hello following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="bc80a-149">Varsa genişleme işlem sunucuları toothis yapılandırma sunucusu bağlı, çok gerek[tüm hello genişleme işlem sunucuların yeniden kaydettirin](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) dağıtımınızdaki.</span><span class="sxs-lookup"><span data-stu-id="bc80a-149">If you have Scale-out Process servers attached toothis Configuration Server, you need too[re-register all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="bc80a-150">Yapılandırma sunucusu farklı bir kurtarma Hizmetleri kasası ile kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="bc80a-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="bc80a-151">Oturum açma tooyour yapılandırma sunucusu.</span><span class="sxs-lookup"><span data-stu-id="bc80a-151">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="bc80a-152">bir yönetici komut isteminden hello komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bc80a-152">from an admin command prompt, run hello command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="bc80a-153">Merhaba kısayolunu kullanarak hello cspsconfigtool.exe başlatın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-153">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
4. <span data-ttu-id="bc80a-154">Merhaba tıklatın **kasa kayıt** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="bc80a-154">Click hello **Vault Registration** tab.</span></span>
5. <span data-ttu-id="bc80a-155">Yeni bir kayıt dosyası hello portalından indirin ve giriş toohello aracı olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-155">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>

    ![YAZMAÇ yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="bc80a-157">Merhaba Proxy sunucusu detayları sağlayın ve hello tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bc80a-157">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
7. <span data-ttu-id="bc80a-158">Bir yönetici PowerShell komut penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="bc80a-159">Merhaba aşağıdaki komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bc80a-159">Run hello following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="bc80a-160">Yapılandırma sunucusu yetkisini alma</span><span class="sxs-lookup"><span data-stu-id="bc80a-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="bc80a-161">Yapılandırma sunucusu yetkisini başlamadan önce hello aşağıdakilerden emin olun.</span><span class="sxs-lookup"><span data-stu-id="bc80a-161">Ensure hello following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="bc80a-162">Bu yapılandırma sunucusu altındaki tüm sanal makineler için korumayı devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="bc80a-163">Merhaba yapılandırma sunucusu gelen tüm çoğaltma ilkelerinin ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-163">Disassociate all Replication policies from hello Configuration Server.</span></span>
3. <span data-ttu-id="bc80a-164">İlişkili toohello yapılandırma sunucusu olan tüm Vcenter sunucularını/vSphere ana bilgisayarları silin.</span><span class="sxs-lookup"><span data-stu-id="bc80a-164">Delete all vCenters servers/vSphere hosts that are associated toohello Configuration Server.</span></span>

### <a name="delete-hello-configuration-server-from-azure-portal"></a><span data-ttu-id="bc80a-165">Merhaba yapılandırma sunucusu Azure portalından Sil</span><span class="sxs-lookup"><span data-stu-id="bc80a-165">Delete hello Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="bc80a-166">Azure portalında çok Gözat**Site Recovery altyapısı** > **yapılandırma sunucularına** hello kasa menüsünden.</span><span class="sxs-lookup"><span data-stu-id="bc80a-166">In Azure portal, browse too**Site Recovery Infrastructure** > **Configuration Servers** from hello Vault menu.</span></span>
2. <span data-ttu-id="bc80a-167">Hello yapılandırma toodecommission istediğiniz Server'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-167">Click hello Configuration Server that you want toodecommission.</span></span>
3. <span data-ttu-id="bc80a-168">Merhaba yapılandırma sunucunun Ayrıntıları sayfasında hello Sil düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-168">On hello Configuration Server's details page, click hello Delete button.</span></span>

  ![Delete yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="bc80a-170">Tıklatın **Evet** hello sunucusunun tooconfirm hello silme.</span><span class="sxs-lookup"><span data-stu-id="bc80a-170">Click **Yes** tooconfirm hello deletion of hello server.</span></span>

  >[!WARNING]
  <span data-ttu-id="bc80a-171">Herhangi bir sanal makine, çoğaltma ilkesi veya vCenter sunucuları/vSphere ana bu yapılandırma sunucusu ile ilişkili varsa, hello sunucu silinemez.</span><span class="sxs-lookup"><span data-stu-id="bc80a-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete hello server.</span></span> <span data-ttu-id="bc80a-172">Toodelete hello kasası çalışmadan önce bu varlıkları silin.</span><span class="sxs-lookup"><span data-stu-id="bc80a-172">Delete these entities before you try toodelete hello vault.</span></span>

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="bc80a-173">Merhaba yapılandırma sunucusu yazılım ve bağımlılıklarını kaldırma</span><span class="sxs-lookup"><span data-stu-id="bc80a-173">Uninstall hello Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="bc80a-174">Tooreuse hello yapılandırma sunucusu Azure Site Recovery ile yeniden düşünüyorsanız, daha sonra toostep 4 doğrudan atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc80a-174">If you plan tooreuse hello Configuration Server with Azure Site Recovery again, then you can skip toostep 4 directly</span></span>

1. <span data-ttu-id="bc80a-175">Yapılandırma sunucusu toohello üzerinde bir yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-175">Log on toohello Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="bc80a-176">Denetim Masası açın > Program > programları Kaldır</span><span class="sxs-lookup"><span data-stu-id="bc80a-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="bc80a-177">Sıra aşağıdaki hello Hello programlarda kaldırın:</span><span class="sxs-lookup"><span data-stu-id="bc80a-177">Uninstall hello programs in hello following sequence:</span></span>
  * <span data-ttu-id="bc80a-178">Microsoft Azure Kurtarma Hizmetleri Aracısı</span><span class="sxs-lookup"><span data-stu-id="bc80a-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="bc80a-179">Microsoft Azure Site Recovery Mobility hizmeti/ana hedef sunucu</span><span class="sxs-lookup"><span data-stu-id="bc80a-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="bc80a-180">Microsoft Azure Site Recovery sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="bc80a-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="bc80a-181">Microsoft Azure Site kurtarma yapılandırması sunucu/işlem sunucusu</span><span class="sxs-lookup"><span data-stu-id="bc80a-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="bc80a-182">Microsoft Azure Site kurtarma yapılandırması sunucu bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="bc80a-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="bc80a-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="bc80a-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="bc80a-184">Komutunu aşağıdaki hello ve yönetici komut isteminden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-184">Run hello following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="bc80a-185">Yapılandırma sunucusu Güvenli Yuva Layer(SSL) sertifikaları yenile</span><span class="sxs-lookup"><span data-stu-id="bc80a-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="bc80a-186">Merhaba mobilite hizmeti işlem sunucuları hello etkinliklerini düzenler bir yerleşik Web Hello yapılandırma sunucusu vardır ve ana hedef sunucuları toohello yapılandırma sunucusu bağlı.</span><span class="sxs-lookup"><span data-stu-id="bc80a-186">hello Configuration Server has an inbuilt webserver, which orchestrates hello activities of hello Mobility Service, Process Servers, and Master Target servers connected toohello Configuration Server.</span></span> <span data-ttu-id="bc80a-187">Merhaba yapılandırma sunucusunun Web sunucusu bir SSL sertifikası tooauthenticate istemcilerine kullanır.</span><span class="sxs-lookup"><span data-stu-id="bc80a-187">hello Configuration Server's webserver uses an SSL certificate tooauthenticate its clients.</span></span> <span data-ttu-id="bc80a-188">Bu sertifika geçerlilik süresi üç yıl sahiptir ve yöntemi aşağıdaki hello kullanarak herhangi bir zamanda yenilenebilir:</span><span class="sxs-lookup"><span data-stu-id="bc80a-188">This certificate has an expiry of three years and can be renewed at any time using hello following method:</span></span>

> [!WARNING]
<span data-ttu-id="bc80a-189">Sertifika süre sonu yalnızca sürümünde gerçekleştirilebilir 9.4.XXXX. X veya daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="bc80a-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="bc80a-190">Tüm hello Azure Site Recovery bileşenleri (yapılandırma sunucusu, işlem sunucusu, ana hedef sunucusu, Mobility hizmeti) yükseltme hello sertifikaları yenilemek iş akışı başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="bc80a-190">Upgrade all hello Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start hello Renew Certificates workflow.</span></span>

1. <span data-ttu-id="bc80a-191">Üzerinde Azure portal Merhaba, tooyour kasası Gözat > Site Recovery altyapısı > yapılandırma sunucusu.</span><span class="sxs-lookup"><span data-stu-id="bc80a-191">On hello Azure portal, browse tooyour Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="bc80a-192">Hello yapılandırma toorenew ihtiyacınız sunucusu için SSL sertifikası hello.</span><span class="sxs-lookup"><span data-stu-id="bc80a-192">Click hello Configuration Server for which you need toorenew hello SSL Certificate for.</span></span>
3. <span data-ttu-id="bc80a-193">Yapılandırma sunucusu durumu Hello altında hello SSL sertifikası süre sonu tarihini hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc80a-193">Under hello Configuration Server health, you can see hello expiry date for hello SSL Certificate.</span></span>
4. <span data-ttu-id="bc80a-194">Merhaba tıklayarak yenileme hello sertifika **sertifikaları yenilemek** hello görüntü aşağıdaki gösterildiği gibi eylem:</span><span class="sxs-lookup"><span data-stu-id="bc80a-194">Renew hello certificate by clicking hello **Renew Certificates** action as shown in hello following image:</span></span>

  ![Delete yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="bc80a-196">Güvenli Yuva Katmanı sertifika süre sonu uyarısı</span><span class="sxs-lookup"><span data-stu-id="bc80a-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="bc80a-197">Merhaba Mayıs 2016 önce gerçekleşen tüm yüklemeleri için SSL sertifikasının geçerlilik ayarlandı tooone yıl.</span><span class="sxs-lookup"><span data-stu-id="bc80a-197">hello SSL Certificate's validity for all installations that happened before May 2016 was set tooone year.</span></span> <span data-ttu-id="bc80a-198">Sertifika süre sonu bildirimleri hello Azure portal gösteren görmesini başlattığınız.</span><span class="sxs-lookup"><span data-stu-id="bc80a-198">you have started seeing certificate expiry notifications showing up in hello Azure portal.</span></span>

1. <span data-ttu-id="bc80a-199">Merhaba yapılandırma sunucunun SSL sertifikası sonraki iki ay hello tooexpire olacaksa, Azure portal hello & (abone toobe tooAzure Site Recovery bildirimleri gerekir) e-posta aracılığıyla kullanıcılara bildirme hello hizmetini başlatır.</span><span class="sxs-lookup"><span data-stu-id="bc80a-199">If hello Configuration Server's SSL certificate is going tooexpire in hello next two months, hello service starts notifying users via hello Azure portal & email (you need toobe subscribed tooAzure Site Recovery notifications).</span></span> <span data-ttu-id="bc80a-200">Size bir bildirim başlığı hello kasasının kaynak sayfasında görmeye başlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="bc80a-200">You start seeing a notification banner on hello Vault's resource page.</span></span>

  ![Sertifika bildirim](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="bc80a-202">Merhaba başlık tooget hello sertifika süre sonu ilgili ek Ayrıntılar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bc80a-202">Click hello banner tooget additional details on hello Certificate expiry.</span></span>

  ![Sertifika ayrıntıları](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="bc80a-204">Eğer yerine bir **Şimdi Yenile** gördüğünüz düğmesi bir **Şimdi Yükselt** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bc80a-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="bc80a-205">Bu, henüz yükseltilmiş too9.4.xxxx.x ya da daha yüksek sürüm edilmemiş bazı bileşenler, ortamınızdaki gelir.</span><span class="sxs-lookup"><span data-stu-id="bc80a-205">This means that there are some components in your environment that have not yet been upgraded too9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="bc80a-206">Yapılandırma sunucusu için gereksinimleri boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="bc80a-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="bc80a-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="bc80a-207">**CPU**</span></span> | <span data-ttu-id="bc80a-208">**Bellek**</span><span class="sxs-lookup"><span data-stu-id="bc80a-208">**Memory**</span></span> | <span data-ttu-id="bc80a-209">**Önbellek disk boyutu**</span><span class="sxs-lookup"><span data-stu-id="bc80a-209">**Cache disk size**</span></span> | <span data-ttu-id="bc80a-210">**Veri değişikliği oranı**</span><span class="sxs-lookup"><span data-stu-id="bc80a-210">**Data change rate**</span></span> | <span data-ttu-id="bc80a-211">**Korumalı makineler**</span><span class="sxs-lookup"><span data-stu-id="bc80a-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="bc80a-212">8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek)</span><span class="sxs-lookup"><span data-stu-id="bc80a-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="bc80a-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="bc80a-213">16 GB</span></span> |<span data-ttu-id="bc80a-214">300 GB</span><span class="sxs-lookup"><span data-stu-id="bc80a-214">300 GB</span></span> |<span data-ttu-id="bc80a-215">500 GB veya daha az</span><span class="sxs-lookup"><span data-stu-id="bc80a-215">500 GB or less</span></span> |<span data-ttu-id="bc80a-216">100'den az makineler çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="bc80a-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="bc80a-217">12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek)</span><span class="sxs-lookup"><span data-stu-id="bc80a-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="bc80a-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="bc80a-218">18 GB</span></span> |<span data-ttu-id="bc80a-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="bc80a-219">600 GB</span></span> |<span data-ttu-id="bc80a-220">500 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="bc80a-220">500 GB too1 TB</span></span> |<span data-ttu-id="bc80a-221">100-150 makineler arasında çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="bc80a-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="bc80a-222">16 Vcpu (2 yuva * 2,5 GHz @ 8 çekirdek)</span><span class="sxs-lookup"><span data-stu-id="bc80a-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="bc80a-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="bc80a-223">32 GB</span></span> |<span data-ttu-id="bc80a-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="bc80a-224">1 TB</span></span> |<span data-ttu-id="bc80a-225">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="bc80a-225">1 TB too2 TB</span></span> |<span data-ttu-id="bc80a-226">150-200 makineler arasında çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="bc80a-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="bc80a-227">Günlük veri dalgalanmasına 2 TB aşıyor veya 200'den fazla sanal makine tooreplicate planlama, toodeploy ek işlem sunucuları tooload hello çoğaltma trafiği dengelemek önerilir.</span><span class="sxs-lookup"><span data-stu-id="bc80a-227">If your daily data churn exceeds 2 TB, or you plan tooreplicate more than 200 virtual machines, it is recommended toodeploy additional process servers tooload balance hello replication traffic.</span></span> <span data-ttu-id="bc80a-228">Nasıl toodeploy genişleme işlem sunucular hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="bc80a-228">Learn more about How toodeploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="bc80a-229">Genel sorunlar</span><span class="sxs-lookup"><span data-stu-id="bc80a-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
