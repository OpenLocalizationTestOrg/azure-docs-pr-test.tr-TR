---
title: " Yapılandırma sunucusu Azure Site kurtarma yönetme | Microsoft Docs"
description: "Bu makalede, ayarlama ve yapılandırma sunucusunu yönetmek açıklar."
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
ms.openlocfilehash: 36da8c7d0f3ace194522e5288f26069cf46d470e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="ba5bb-103">Yapılandırma sunucusu yönetme</span><span class="sxs-lookup"><span data-stu-id="ba5bb-103">Manage a Configuration Server</span></span>

<span data-ttu-id="ba5bb-104">Yapılandırma sunucusu Site kurtarma Hizmetleri ile şirket içi altyapınızı arasında bir düzenleyici gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-104">Configuration Server acts as a coordinator between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="ba5bb-105">Bu makalede nasıl ayarlamak, yapılandırabilir ve yapılandırma sunucusunu yönetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-105">This article describes how you can set up, configure, and manage the Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba5bb-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ba5bb-106">Prerequisites</span></span>
<span data-ttu-id="ba5bb-107">En düşük donanım, yazılım ve yapılandırma sunucusu kurmak için gerekli ağ yapılandırması şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ba5bb-107">The following are the minimum hardware, software, and network configuration required to set up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="ba5bb-108">[Kapasite planlama](site-recovery-capacity-planner.md) yapılandırmasıyla yapılandırma sunucusu bu paketleri dağıtmak emin olmak için önemli bir adım yük gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="ba5bb-109">Daha fazla bilgi edinin [yapılandırma sunucusu için gereksinimleri boyutlandırma](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="ba5bb-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-configuration-server-software"></a><span data-ttu-id="ba5bb-110">Yapılandırma sunucusu yazılım indirme</span><span class="sxs-lookup"><span data-stu-id="ba5bb-110">Downloading the Configuration Server software</span></span>
1. <span data-ttu-id="ba5bb-111">Azure portalında oturum açın ve kurtarma Hizmetleri Kasası'na göz atın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="ba5bb-112">Gözat **Site Recovery altyapısı** > **yapılandırma sunucularına** (altında VMware ve fiziksel makineler için).</span><span class="sxs-lookup"><span data-stu-id="ba5bb-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Sunucuları Sayfası Ekle](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="ba5bb-114">Tıklatın **+ sunucuları** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-114">Click the **+Servers** button.</span></span>
4. <span data-ttu-id="ba5bb-115">Üzerinde **Sunucu Ekle** sayfasında, kayıt anahtarını indirin için karşıdan yükleme düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-115">On the **Add Server** page, click the Download button to download the Registration key.</span></span> <span data-ttu-id="ba5bb-116">Azure Site Recovery hizmeti ile kaydetmek için yapılandırma sunucusu yüklemesi sırasında bu anahtar gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-116">You need this key during the Configuration Server installation to register it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="ba5bb-117">Tıklatın **Microsoft Azure Site Recovery birleşik Kurulumu karşıdan** yapılandırma sunucusunun en son sürümünü indirmek için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Configuration Server.</span></span>

  ![Sayfayı Yükle](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="ba5bb-119">Yapılandırma sunucusunun en son sürümünü, doğrudan indirilebilir [Microsoft Download Center indirme sayfası](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="ba5bb-119">Latest version of the Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="ba5bb-120">Yükleme ve yapılandırma sunucusu GUI'den kaydetme</span><span class="sxs-lookup"><span data-stu-id="ba5bb-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="ba5bb-121">Yükleme ve komut satırını kullanarak bir yapılandırma sunucusu kaydetme</span><span class="sxs-lookup"><span data-stu-id="ba5bb-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="ba5bb-122">Örnek Kullanım</span><span class="sxs-lookup"><span data-stu-id="ba5bb-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="ba5bb-123">Yapılandırma sunucusu Yükleyici komut satırı bağımsız değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="ba5bb-124">Bir MySql kimlik bilgileri dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba5bb-124">Create a MySql credentials file</span></span>
<span data-ttu-id="ba5bb-125">MySQLCredsFilePath parametresi bir dosya girdi olarak alır.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="ba5bb-126">Aşağıdaki biçimi kullanarak dosya oluşturma ve giriş MySQLCredsFilePath parametresi olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-126">Create the file using the following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="ba5bb-127">Proxy ayarlarını yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba5bb-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="ba5bb-128">ProxySettingsFilePath parametresi bir dosya girdi olarak alır.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="ba5bb-129">Aşağıdaki biçimi kullanarak dosya oluşturma ve giriş ProxySettingsFilePath parametresi olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-129">Create the file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="ba5bb-130">Yapılandırma sunucusu için proxy ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="ba5bb-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="ba5bb-131">Yapılandırma sunucusu oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-131">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="ba5bb-132">Kısayol kullanarak cspsconfigtool.exe başlatın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-132">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
3. <span data-ttu-id="ba5bb-133">Tıklatın **kasa kayıt** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-133">Click the **Vault Registration** tab.</span></span>
4. <span data-ttu-id="ba5bb-134">Portaldan yeni bir kasa kayıt dosyasını indirin ve aracı giriş olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-134">Download a new Vault Registration file from the portal and provide it as input to the tool.</span></span>

  ![YAZMAÇ yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="ba5bb-136">Yeni Proxy sunucu bilgileri sağlayın ve tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-136">Provide the new Proxy Server details and click the **Register** button.</span></span>
6. <span data-ttu-id="ba5bb-137">Bir yönetici PowerShell komut penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="ba5bb-138">Aşağıdaki komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="ba5bb-138">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="ba5bb-139">Bu yapılandırma sunucusuna bağlı genişleme işlem sunucularınız varsa, gerek [proxy ayarları tüm genişleme işlem sunucularındaki düzeltme](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) dağıtımınızdaki.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-139">If you have Scale-out Process servers attached to this Configuration Server, you need to [fix the proxy settings on all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-the-same-recovery-services-vault"></a><span data-ttu-id="ba5bb-140">Aynı kurtarma Hizmetleri kasası ile yapılandırma sunucusunu yeniden kaydedin</span><span class="sxs-lookup"><span data-stu-id="ba5bb-140">Re-register a Configuration Server with the same Recovery Services Vault</span></span>
  1. <span data-ttu-id="ba5bb-141">Yapılandırma sunucusu oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-141">Login to your Configuration Server.</span></span>
  2. <span data-ttu-id="ba5bb-142">Masaüstünde kısayol kullanarak cspsconfigtool.exe başlatın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-142">Launch the cspsconfigtool.exe using the shortcut on your desktop.</span></span>
  3. <span data-ttu-id="ba5bb-143">Tıklatın **kasa kayıt** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-143">Click the **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="ba5bb-144">Yeni bir kayıt dosyası portaldan indirmenizi ve aracı giriş olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-144">Download a new Registration file from the portal and provide it as input to the tool.</span></span>
        <span data-ttu-id="ba5bb-145">![YAZMAÇ yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="ba5bb-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="ba5bb-146">Proxy sunucu bilgileri sağlayın ve tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-146">Provide the Proxy Server details and click the **Register** button.</span></span>  
  6. <span data-ttu-id="ba5bb-147">Bir yönetici PowerShell komut penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="ba5bb-148">Aşağıdaki komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="ba5bb-148">Run the following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="ba5bb-149">Bu yapılandırma sunucusuna bağlı genişleme işlem sunucularınız varsa, gerek [tüm genişleme işlem sunucuların yeniden kaydettirin](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) dağıtımınızdaki.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-149">If you have Scale-out Process servers attached to this Configuration Server, you need to [re-register all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="ba5bb-150">Yapılandırma sunucusu farklı bir kurtarma Hizmetleri kasası ile kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="ba5bb-151">Yapılandırma sunucusu oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-151">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="ba5bb-152">bir yönetici komut isteminden komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="ba5bb-152">from an admin command prompt, run the command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="ba5bb-153">Kısayol kullanarak cspsconfigtool.exe başlatın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-153">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
4. <span data-ttu-id="ba5bb-154">Tıklatın **kasa kayıt** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-154">Click the **Vault Registration** tab.</span></span>
5. <span data-ttu-id="ba5bb-155">Yeni bir kayıt dosyası portaldan indirmenizi ve aracı giriş olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-155">Download a new Registration file from the portal and provide it as input to the tool.</span></span>

    ![YAZMAÇ yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="ba5bb-157">Proxy sunucu bilgileri sağlayın ve tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-157">Provide the Proxy Server details and click the **Register** button.</span></span>  
7. <span data-ttu-id="ba5bb-158">Bir yönetici PowerShell komut penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="ba5bb-159">Aşağıdaki komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="ba5bb-159">Run the following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="ba5bb-160">Yapılandırma sunucusu yetkisini alma</span><span class="sxs-lookup"><span data-stu-id="ba5bb-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="ba5bb-161">Yapılandırma sunucusu yetkisini başlamadan önce aşağıdakilerden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-161">Ensure the following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="ba5bb-162">Bu yapılandırma sunucusu altındaki tüm sanal makineler için korumayı devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="ba5bb-163">Yapılandırma sunucusundan tüm çoğaltma ilkelerinin ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-163">Disassociate all Replication policies from the Configuration Server.</span></span>
3. <span data-ttu-id="ba5bb-164">Yapılandırma sunucusu ilişkili tüm Vcenter sunucularını/vSphere ana silin.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-164">Delete all vCenters servers/vSphere hosts that are associated to the Configuration Server.</span></span>

### <a name="delete-the-configuration-server-from-azure-portal"></a><span data-ttu-id="ba5bb-165">Yapılandırma sunucusu Azure portalından Sil</span><span class="sxs-lookup"><span data-stu-id="ba5bb-165">Delete the Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="ba5bb-166">Azure Portal'da Gözat **Site Recovery altyapısı** > **yapılandırma sunucularına** kasa menüsünden.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-166">In Azure portal, browse to **Site Recovery Infrastructure** > **Configuration Servers** from the Vault menu.</span></span>
2. <span data-ttu-id="ba5bb-167">Yetkisini istediğiniz yapılandırma sunucuya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-167">Click the Configuration Server that you want to decommission.</span></span>
3. <span data-ttu-id="ba5bb-168">Yapılandırma sunucusunun Ayrıntıları sayfasında Sil düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-168">On the Configuration Server's details page, click the Delete button.</span></span>

  ![Delete yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="ba5bb-170">Tıklatın **Evet** sunucu silme işlemini onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-170">Click **Yes** to confirm the deletion of the server.</span></span>

  >[!WARNING]
  <span data-ttu-id="ba5bb-171">Herhangi bir sanal makine, çoğaltma ilkesi veya vCenter sunucuları/vSphere ana bu yapılandırma sunucusu ile ilişkili varsa, sunucu silinemez.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete the server.</span></span> <span data-ttu-id="ba5bb-172">Kasa silmeye çalışmadan önce bu varlıkları silin.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-172">Delete these entities before you try to delete the vault.</span></span>

### <a name="uninstall-the-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="ba5bb-173">Yapılandırma sunucusu yazılım ve bağımlılıklarını kaldırma</span><span class="sxs-lookup"><span data-stu-id="ba5bb-173">Uninstall the Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="ba5bb-174">Yapılandırma sunucusu Azure Site Recovery ile yeniden yeniden kullanmayı planlıyorsanız, daha sonra adım 4 doğrudan atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-174">If you plan to reuse the Configuration Server with Azure Site Recovery again, then you can skip to step 4 directly</span></span>

1. <span data-ttu-id="ba5bb-175">Yapılandırma sunucusunda bir yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-175">Log on to the Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="ba5bb-176">Denetim Masası açın > Program > programları Kaldır</span><span class="sxs-lookup"><span data-stu-id="ba5bb-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="ba5bb-177">Aşağıdaki sırayla programları kaldırın:</span><span class="sxs-lookup"><span data-stu-id="ba5bb-177">Uninstall the programs in the following sequence:</span></span>
  * <span data-ttu-id="ba5bb-178">Microsoft Azure Kurtarma Hizmetleri Aracısı</span><span class="sxs-lookup"><span data-stu-id="ba5bb-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="ba5bb-179">Microsoft Azure Site Recovery Mobility hizmeti/ana hedef sunucu</span><span class="sxs-lookup"><span data-stu-id="ba5bb-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="ba5bb-180">Microsoft Azure Site Recovery sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="ba5bb-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="ba5bb-181">Microsoft Azure Site kurtarma yapılandırması sunucu/işlem sunucusu</span><span class="sxs-lookup"><span data-stu-id="ba5bb-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="ba5bb-182">Microsoft Azure Site kurtarma yapılandırması sunucu bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="ba5bb-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="ba5bb-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="ba5bb-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="ba5bb-184">Yönetici komut istemi ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-184">Run the following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="ba5bb-185">Yapılandırma sunucusu Güvenli Yuva Layer(SSL) sertifikaları yenile</span><span class="sxs-lookup"><span data-stu-id="ba5bb-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="ba5bb-186">Yapılandırma sunucusu yapılandırma sunucusuna bağlı Mobility hizmeti, işlemi sunucuları ve ana hedef sunucular etkinliklerini düzenler bir yerleşik Web sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-186">The Configuration Server has an inbuilt webserver, which orchestrates the activities of the Mobility Service, Process Servers, and Master Target servers connected to the Configuration Server.</span></span> <span data-ttu-id="ba5bb-187">Yapılandırma sunucusunun Web sunucusu, istemcilerin kimliğini doğrulamak için bir SSL sertifikası kullanır.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-187">The Configuration Server's webserver uses an SSL certificate to authenticate its clients.</span></span> <span data-ttu-id="ba5bb-188">Bu sertifika geçerlilik süresi üç yıl sahiptir ve aşağıdaki yöntemi kullanarak herhangi bir zamanda yenilenebilir:</span><span class="sxs-lookup"><span data-stu-id="ba5bb-188">This certificate has an expiry of three years and can be renewed at any time using the following method:</span></span>

> [!WARNING]
<span data-ttu-id="ba5bb-189">Sertifika süre sonu yalnızca sürümünde gerçekleştirilebilir 9.4.XXXX. X veya daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="ba5bb-190">Tüm Azure Site Recovery bileşenleri (yapılandırma sunucusu, işlem sunucusu, ana hedef sunucusu, Mobility hizmeti) yükseltme sertifikaları yenilemek iş akışı başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-190">Upgrade all the Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start the Renew Certificates workflow.</span></span>

1. <span data-ttu-id="ba5bb-191">Kasanız için Azure Portal'da Gözat > Site Recovery altyapısı > yapılandırma sunucusu.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-191">On the Azure portal, browse to your Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="ba5bb-192">SSL sertifikasını yenilemek gereken yapılandırma sunucusu tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-192">Click the Configuration Server for which you need to renew the SSL Certificate for.</span></span>
3. <span data-ttu-id="ba5bb-193">Yapılandırma sunucusu durumu altında için SSL sertifikası süre sonu tarihi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-193">Under the Configuration Server health, you can see the expiry date for the SSL Certificate.</span></span>
4. <span data-ttu-id="ba5bb-194">Tıklayarak sertifikayı **sertifikaları yenilemek** aşağıdaki görüntüde gösterildiği gibi eylem:</span><span class="sxs-lookup"><span data-stu-id="ba5bb-194">Renew the certificate by clicking the **Renew Certificates** action as shown in the following image:</span></span>

  ![Delete yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="ba5bb-196">Güvenli Yuva Katmanı sertifika süre sonu uyarısı</span><span class="sxs-lookup"><span data-stu-id="ba5bb-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="ba5bb-197">SSL sertifika geçerlilik Mayıs 2016 önce gerçekleşen tüm yüklemeleri için bir yıl ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-197">The SSL Certificate's validity for all installations that happened before May 2016 was set to one year.</span></span> <span data-ttu-id="ba5bb-198">Sertifika süre sonu bildirimleri Azure portalında gösteren görmesini başlattığınız.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-198">you have started seeing certificate expiry notifications showing up in the Azure portal.</span></span>

1. <span data-ttu-id="ba5bb-199">Yapılandırma sunucusunun SSL sertifikası sonraki iki ay içinde süresi dolacak şekilde olacaksa, Azure portal & (Azure Site Recovery bildirimlerine abone gerekir) e-posta aracılığıyla kullanıcılara bildirme hizmetini başlatır.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-199">If the Configuration Server's SSL certificate is going to expire in the next two months, the service starts notifying users via the Azure portal & email (you need to be subscribed to Azure Site Recovery notifications).</span></span> <span data-ttu-id="ba5bb-200">Size bir bildirim başlığı Kasası'nın kaynak sayfasında görmeye başlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-200">You start seeing a notification banner on the Vault's resource page.</span></span>

  ![Sertifika bildirim](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="ba5bb-202">Sertifika süre sonu hakkında ek ayrıntıları almak için başlığını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-202">Click the banner to get additional details on the Certificate expiry.</span></span>

  ![Sertifika ayrıntıları](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="ba5bb-204">Eğer yerine bir **Şimdi Yenile** gördüğünüz düğmesi bir **Şimdi Yükselt** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="ba5bb-205">Bu henüz 9.4.xxxx.x veya daha sonraki sürümler için yükseltilmemiş bazı bileşenler, ortamınızdaki gelir.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-205">This means that there are some components in your environment that have not yet been upgraded to 9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="ba5bb-206">Yapılandırma sunucusu için gereksinimleri boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="ba5bb-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="ba5bb-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="ba5bb-207">**CPU**</span></span> | <span data-ttu-id="ba5bb-208">**Bellek**</span><span class="sxs-lookup"><span data-stu-id="ba5bb-208">**Memory**</span></span> | <span data-ttu-id="ba5bb-209">**Önbellek disk boyutu**</span><span class="sxs-lookup"><span data-stu-id="ba5bb-209">**Cache disk size**</span></span> | <span data-ttu-id="ba5bb-210">**Veri değişikliği oranı**</span><span class="sxs-lookup"><span data-stu-id="ba5bb-210">**Data change rate**</span></span> | <span data-ttu-id="ba5bb-211">**Korumalı makineler**</span><span class="sxs-lookup"><span data-stu-id="ba5bb-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="ba5bb-212">8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek)</span><span class="sxs-lookup"><span data-stu-id="ba5bb-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="ba5bb-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="ba5bb-213">16 GB</span></span> |<span data-ttu-id="ba5bb-214">300 GB</span><span class="sxs-lookup"><span data-stu-id="ba5bb-214">300 GB</span></span> |<span data-ttu-id="ba5bb-215">500 GB veya daha az</span><span class="sxs-lookup"><span data-stu-id="ba5bb-215">500 GB or less</span></span> |<span data-ttu-id="ba5bb-216">100'den az makineler çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="ba5bb-217">12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek)</span><span class="sxs-lookup"><span data-stu-id="ba5bb-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="ba5bb-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="ba5bb-218">18 GB</span></span> |<span data-ttu-id="ba5bb-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="ba5bb-219">600 GB</span></span> |<span data-ttu-id="ba5bb-220">1 TB ' 500 GB</span><span class="sxs-lookup"><span data-stu-id="ba5bb-220">500 GB to 1 TB</span></span> |<span data-ttu-id="ba5bb-221">100-150 makineler arasında çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="ba5bb-222">16 Vcpu (2 yuva * 2,5 GHz @ 8 çekirdek)</span><span class="sxs-lookup"><span data-stu-id="ba5bb-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="ba5bb-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="ba5bb-223">32 GB</span></span> |<span data-ttu-id="ba5bb-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="ba5bb-224">1 TB</span></span> |<span data-ttu-id="ba5bb-225">1 TB ile 2 TB</span><span class="sxs-lookup"><span data-stu-id="ba5bb-225">1 TB to 2 TB</span></span> |<span data-ttu-id="ba5bb-226">150-200 makineler arasında çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="ba5bb-227">Günlük veri dalgalanmasına 2 TB aşıyor veya 200'den fazla sanal makineleri çoğaltmak planlama, çoğaltma trafiği dengelemek için ek işlem sunucusu dağıtmayı önerilir.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-227">If your daily data churn exceeds 2 TB, or you plan to replicate more than 200 virtual machines, it is recommended to deploy additional process servers to load balance the replication traffic.</span></span> <span data-ttu-id="ba5bb-228">Sunucularının genişleme işlem dağıtma hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="ba5bb-228">Learn more about How to deploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="ba5bb-229">Genel sorunlar</span><span class="sxs-lookup"><span data-stu-id="ba5bb-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
