---
title: "Azure yedekleme: Kullanım PowerShell tooback DPM iş yüklerini | Microsoft Docs"
description: "Bilgi nasıl toodeploy ve Data Protection Manager (PowerShell kullanarak DPM için) Azure Backup yönetme"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 48ebe6b520857836e89749ffb6fe83d1f14c5597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="bd475-103">Dağıtma ve PowerShell kullanarak Data Protection Manager (DPM) sunucuları için yedekleme tooAzure yönetme</span><span class="sxs-lookup"><span data-stu-id="bd475-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd475-104">ARM</span><span class="sxs-lookup"><span data-stu-id="bd475-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="bd475-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="bd475-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="bd475-106">Bu makalede açıklanır nasıl toouse PowerShell tooback ayarlama ve bir yedekleme Kasası'nı DPM verileri kurtarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd475-106">This article explains how toouse PowerShell tooback up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="bd475-107">Microsoft, tüm yeni dağıtımlar için kurtarma Hizmetleri kasalarının kullanılmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="bd475-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="bd475-108">Yeni bir Azure yedekleme kullanıcı, hello makale kullanırsanız [dağıtma ve PowerShell kullanarak Data Protection Manager veri tooAzure yönetmek](backup-dpm-automation.md), bir kurtarma Hizmetleri kasasına verilerinizi depolamak için.</span><span class="sxs-lookup"><span data-stu-id="bd475-108">If you are a new Azure Backup user, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd475-109">Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd475-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="bd475-110">Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="bd475-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="bd475-111">Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.</span><span class="sxs-lookup"><span data-stu-id="bd475-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="bd475-112">15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="bd475-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="bd475-113">**1 Kasım 2017’ye kadar**:</span><span class="sxs-lookup"><span data-stu-id="bd475-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="bd475-114">Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.</span><span class="sxs-lookup"><span data-stu-id="bd475-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="bd475-115">Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="bd475-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="bd475-116">Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd475-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="bd475-117">Merhaba PowerShell ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="bd475-117">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="bd475-118">Data Protection Manager tooAzure PowerShell toomanage yedeklemelerden kullanmadan önce toohave hello sağ ortamında PowerShell gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd475-118">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you will need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="bd475-119">Merhaba PowerShell oturumu Hello başlangıcında komutu tooimport hello sağ modülleri aşağıdaki hello çalıştırın ve toocorrectly başvuru hello DPM cmdlet'leri izin emin olun:</span><span class="sxs-lookup"><span data-stu-id="bd475-119">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="bd475-120">Kurulumu'nu ve kaydı</span><span class="sxs-lookup"><span data-stu-id="bd475-120">Setup and Registration</span></span>
<span data-ttu-id="bd475-121">toobegin:</span><span class="sxs-lookup"><span data-stu-id="bd475-121">toobegin:</span></span>

1. <span data-ttu-id="bd475-122">[En son PowerShell indirme](https://github.com/Azure/azure-powershell/releases) (gerekli minimum sürüm: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="bd475-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="bd475-123">Çok geçerek Hello Azure yedekleme cmdlet'leri etkinleştirmek*AzureResourceManager* hello kullanarak moduna **Switch-AzureMode** komutunu:</span><span class="sxs-lookup"><span data-stu-id="bd475-123">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="bd475-124">Merhaba aşağıdaki Kurulum ve kayıt görevler PowerShell ile otomatik olarak yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="bd475-124">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="bd475-125">Yedekleme kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd475-125">Create a backup vault</span></span>
* <span data-ttu-id="bd475-126">Hello Azure Backup aracısını yükleme</span><span class="sxs-lookup"><span data-stu-id="bd475-126">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="bd475-127">Hello Azure Backup hizmeti ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="bd475-127">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="bd475-128">Ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="bd475-128">Networking settings</span></span>
* <span data-ttu-id="bd475-129">Şifreleme ayarları</span><span class="sxs-lookup"><span data-stu-id="bd475-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="bd475-130">Yedekleme kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd475-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="bd475-131">Azure Backup hello için ilk kez kullanan müşteriler için aboneliğiniz ile birlikte kullanılan tooregister hello Azure Backup sağlayıcı toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd475-131">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="bd475-132">Bu komutu aşağıdaki hello çalıştırarak yapılabilir: Register-AzureProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="bd475-132">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="bd475-133">Hello kullanarak yeni bir yedekleme kasası oluşturma **yeni AzureRMBackupVault** komutunu.</span><span class="sxs-lookup"><span data-stu-id="bd475-133">You can create a new backup vault using hello **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="bd475-134">Merhaba yedekleme kasası olan bir ARM kaynak tooplace gereken şekilde bir kaynak grubu içinde.</span><span class="sxs-lookup"><span data-stu-id="bd475-134">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="bd475-135">Yükseltilmiş bir Azure PowerShell konsolunda hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bd475-135">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="bd475-136">Tüm hello yedekleme kasalarının listesi hello kullanarak belirli bir abonelikte alabilirsiniz **Get-AzureRMBackupVault** komutunu.</span><span class="sxs-lookup"><span data-stu-id="bd475-136">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="bd475-137">Bir DPM sunucusu üzerinde Hello Azure Backup aracısını yükleme</span><span class="sxs-lookup"><span data-stu-id="bd475-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="bd475-138">Hello Azure Backup aracısını yüklemeden önce indirildi ve Windows Server hello mevcut toohave hello yükleyici gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd475-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="bd475-139">Hello hello Installer hello en son sürümünü elde edebilirsiniz [Microsoft Download Center](http://aka.ms/azurebackup_agent) veya hello yedekleme kasasının Pano sayfası.</span><span class="sxs-lookup"><span data-stu-id="bd475-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="bd475-140">Kolay erişilebilecek bir konuma tooan gibi Hello yükleyici Kaydet * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="bd475-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="bd475-141">komutu yükseltilmiş bir PowerShell konsolunda aşağıdaki hello çalıştırmak tooinstall hello Aracısı **hello DPM sunucusunda**:</span><span class="sxs-lookup"><span data-stu-id="bd475-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="bd475-142">Bu, tüm hello varsayılan seçeneklerle hello aracı yükler.</span><span class="sxs-lookup"><span data-stu-id="bd475-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="bd475-143">Merhaba yükleme hello arka planda birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="bd475-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="bd475-144">Merhaba belirtmezseniz */nu* seçeneği hello **Windows Update** hello yükleme toocheck herhangi bir güncelleştirme için hello sonunda penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="bd475-144">If you do not specify hello */nu* option hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="bd475-145">Merhaba Aracısı hello yüklü programlar listesinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="bd475-145">hello agent will show in hello list of installed programs.</span></span> <span data-ttu-id="bd475-146">toosee hello listesi yüklü programlar, çok Git**Denetim Masası** > **programları** > **programlar ve Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="bd475-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Yüklü aracı](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="bd475-148">Yükleme Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="bd475-148">Installation options</span></span>
<span data-ttu-id="bd475-149">Tüm seçeneklerin aracılığıyla hello toosee komut satırı Merhaba, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="bd475-149">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="bd475-150">Merhaba mevcut Seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bd475-150">hello available options include:</span></span>

| <span data-ttu-id="bd475-151">Seçenek</span><span class="sxs-lookup"><span data-stu-id="bd475-151">Option</span></span> | <span data-ttu-id="bd475-152">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="bd475-152">Details</span></span> | <span data-ttu-id="bd475-153">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="bd475-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd475-154">/q</span><span class="sxs-lookup"><span data-stu-id="bd475-154">/q</span></span> |<span data-ttu-id="bd475-155">Sessiz yükleme</span><span class="sxs-lookup"><span data-stu-id="bd475-155">Quiet installation</span></span> |- |
| <span data-ttu-id="bd475-156">p: "Konum"</span><span class="sxs-lookup"><span data-stu-id="bd475-156">/p:"location"</span></span> |<span data-ttu-id="bd475-157">Yol toohello yükleme klasörünü hello Azure Yedekleme aracısı.</span><span class="sxs-lookup"><span data-stu-id="bd475-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="bd475-158">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Aracısı</span><span class="sxs-lookup"><span data-stu-id="bd475-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="bd475-159">/ s: "Konum"</span><span class="sxs-lookup"><span data-stu-id="bd475-159">/s:"location"</span></span> |<span data-ttu-id="bd475-160">Hello Azure Backup aracısı için yol toohello Önbellek klasörü.</span><span class="sxs-lookup"><span data-stu-id="bd475-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="bd475-161">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="bd475-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="bd475-162">/m</span><span class="sxs-lookup"><span data-stu-id="bd475-162">/m</span></span> |<span data-ttu-id="bd475-163">Katılımı tooMicrosoft güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="bd475-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="bd475-164">/nu</span><span class="sxs-lookup"><span data-stu-id="bd475-164">/nu</span></span> |<span data-ttu-id="bd475-165">Yükleme tamamlandıktan sonra güncelleştirmeleri denetleme</span><span class="sxs-lookup"><span data-stu-id="bd475-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="bd475-166">/d</span><span class="sxs-lookup"><span data-stu-id="bd475-166">/d</span></span> |<span data-ttu-id="bd475-167">Microsoft Azure kurtarma Hizmetleri Aracısı kaldırır</span><span class="sxs-lookup"><span data-stu-id="bd475-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="bd475-168">/ph</span><span class="sxs-lookup"><span data-stu-id="bd475-168">/ph</span></span> |<span data-ttu-id="bd475-169">Proxy konağı adresi</span><span class="sxs-lookup"><span data-stu-id="bd475-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="bd475-170">/PO</span><span class="sxs-lookup"><span data-stu-id="bd475-170">/po</span></span> |<span data-ttu-id="bd475-171">Proxy ana bilgisayar bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="bd475-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="bd475-172">/PU</span><span class="sxs-lookup"><span data-stu-id="bd475-172">/pu</span></span> |<span data-ttu-id="bd475-173">Proxy konağı kullanıcı</span><span class="sxs-lookup"><span data-stu-id="bd475-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="bd475-174">/pw</span><span class="sxs-lookup"><span data-stu-id="bd475-174">/pw</span></span> |<span data-ttu-id="bd475-175">Proxy parolası</span><span class="sxs-lookup"><span data-stu-id="bd475-175">Proxy Password</span></span> |- |

### <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="bd475-176">Hello Azure Backup hizmeti ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="bd475-176">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="bd475-177">Hello Azure Backup hizmeti ile kaydedebilmek için o hello tooensure gerek [Önkoşullar](backup-azure-dpm-introduction.md) karşılanır.</span><span class="sxs-lookup"><span data-stu-id="bd475-177">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="bd475-178">Yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="bd475-178">You must:</span></span>

* <span data-ttu-id="bd475-179">Geçerli bir Azure aboneliğiniz</span><span class="sxs-lookup"><span data-stu-id="bd475-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="bd475-180">Bir yedekleme kasası sahip</span><span class="sxs-lookup"><span data-stu-id="bd475-180">Have a backup vault</span></span>

<span data-ttu-id="bd475-181">toodownload hello kasa kimlik bilgileri Hello çalıştırmak, **Get-AzureBackupVaultCredentials** uygun bir konumda ister bir Azure PowerShell konsolunda ve deposu komutunu * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="bd475-181">toodownload hello vault credentials, run hello **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="bd475-182">Merhaba kasası ile kaydediliyor hello makine yapılır hello kullanarak [başlangıç DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bd475-182">Registering hello machine with hello vault is done using hello [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="bd475-183">Bu Microsoft Azure belirtilen hello kullanarak kasayla hello DPM "TestingServer" adlı sunucu kaydedeceksiniz kasa kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="bd475-183">This will register hello DPM Server named “TestingServer” with Microsoft Azure Vault using hello specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd475-184">Göreli yollar toospecify hello kasa kimlik bilgileri dosyası kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="bd475-184">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="bd475-185">Bir giriş toohello cmdlet'ini olarak mutlak bir yol sağlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="bd475-185">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="bd475-186">İlk yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="bd475-186">Initial configuration settings</span></span>
<span data-ttu-id="bd475-187">Merhaba DPM sunucusu hello Azure yedekleme kasası ile kaydedildiğinde, varsayılan abonelik ayarlarını başlar.</span><span class="sxs-lookup"><span data-stu-id="bd475-187">Once hello DPM Server is registered with hello Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="bd475-188">Bu abonelik ayarlar, ağ, şifreleme ve hello hazırlama alanı içerir.</span><span class="sxs-lookup"><span data-stu-id="bd475-188">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="bd475-189">toofirst ihtiyacınız toobegin değişen hello abonelik ayarlarını al tanıtıcı (hello kullanarak hello varolan varsayılan) ayarları [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bd475-189">toobegin changing hello subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="bd475-190">Tüm değişiklikleri yapılmış toothis yerel PowerShell nesnesi olan ```$setting``` ve ardından hello tam nesne taahhüt tooDPM ve Azure Backup toosave hello kullanarak bunları [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-190">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="bd475-191">Toouse hello gereksinim ```–Commit``` değişiklikleri hello bayrağı tooensure kaldı.</span><span class="sxs-lookup"><span data-stu-id="bd475-191">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="bd475-192">Hello ayarları değil uygulanan ve olması kaydedilen sürece Azure yedekleme tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bd475-192">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="bd475-193">Ağ</span><span class="sxs-lookup"><span data-stu-id="bd475-193">Networking</span></span>
<span data-ttu-id="bd475-194">Merhaba bağlantı hello DPM makine toohello hello Azure Backup hizmeti, bir proxy sunucu üzerinden internet ise, hello proxy sunucusu ayarları için yedeklemeler toosucceed sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bd475-194">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for backups toosucceed.</span></span> <span data-ttu-id="bd475-195">Bu hello kullanarak yapılır ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` ve hello ```ProxyPassword``` hello parametrelerle [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-195">This is done by using hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="bd475-196">Bu örnekte, olmadığından hiçbir Ara sunucunun biz açıkça herhangi bir proxy ile ilgili bilgi temizleme.</span><span class="sxs-lookup"><span data-stu-id="bd475-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="bd475-197">Bant genişliği kullanımı ile seçenekleri de denetlenebilir ```-WorkHourBandwidth``` ve ```-NonWorkHourBandwidth``` hello haftanın belirli bir dizi için.</span><span class="sxs-lookup"><span data-stu-id="bd475-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="bd475-198">Bu örnekte, biz herhangi azaltma ayarlıyorsanız değil.</span><span class="sxs-lookup"><span data-stu-id="bd475-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a><span data-ttu-id="bd475-199">Merhaba hazırlama alanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bd475-199">Configuring hello staging Area</span></span>
<span data-ttu-id="bd475-200">Merhaba DPM sunucusunda çalışan hello Azure Yedekleme aracısı, (yerel hazırlama alanı) hello buluttan geri yüklenen veriler için geçici depolama gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd475-200">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="bd475-201">Merhaba hazırlama alanı hello kullanarak yapılandırma [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i ve hello ```-StagingAreaPath``` parametresi.</span><span class="sxs-lookup"><span data-stu-id="bd475-201">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="bd475-202">Merhaba yukarıdaki örnekte, hello hazırlama alanı çok ayarlanacak*C:\StagingArea* hello PowerShell nesnesindeki ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="bd475-202">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="bd475-203">Merhaba belirtilen klasör zaten var, aksi takdirde hello abonelik ayarlarını hello son yürütme başarısız olur emin olun.</span><span class="sxs-lookup"><span data-stu-id="bd475-203">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="bd475-204">Şifreleme ayarları</span><span class="sxs-lookup"><span data-stu-id="bd475-204">Encryption settings</span></span>
<span data-ttu-id="bd475-205">Merhaba gönderilen yedekleme verileri tooAzure yedekleme şifrelenmiş tooprotect hello hello veri gizliliğini ' dir.</span><span class="sxs-lookup"><span data-stu-id="bd475-205">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="bd475-206">Merhaba şifreleme parolası hello "parola" toodecrypt hello geri yükleme hello aynı anda verilerdir.</span><span class="sxs-lookup"><span data-stu-id="bd475-206">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="bd475-207">Önemli tookeep bu bilgileri güvenlidir ve ayarlandıktan sonra güvenli.</span><span class="sxs-lookup"><span data-stu-id="bd475-207">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="bd475-208">Merhaba aşağıdaki örnekte, hello ilk komut hello dizesini sayıya dönüştürür ```passphrase123456789``` adlı tooa güvenli dize atar hello güvenli dize toohello değişkeni ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="bd475-208">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="bd475-209">İkinci komut Hello ayarlar hello güvenli dize ```$Passphrase``` yedeklemeleri şifrelemek için başlangıç parolası.</span><span class="sxs-lookup"><span data-stu-id="bd475-209">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="bd475-210">Ayarlandıktan sonra hello parola bilgilerini güvenli ve güvenli tutar.</span><span class="sxs-lookup"><span data-stu-id="bd475-210">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="bd475-211">Bu parola olmadan mümkün toorestore verileri azure'dan olmaz.</span><span class="sxs-lookup"><span data-stu-id="bd475-211">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="bd475-212">Bu noktada, tüm gerekli hello değişiklikleri toohello yaptığınız ```$setting``` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="bd475-212">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="bd475-213">Toocommit hello değişiklikleri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bd475-213">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="bd475-214">Veri tooAzure yedekleme koruma</span><span class="sxs-lookup"><span data-stu-id="bd475-214">Protect data tooAzure Backup</span></span>
<span data-ttu-id="bd475-215">Bu bölümde, bir üretim sunucusu tooDPM ekleyin ve hello veri toolocal DPM depolama ve ardından tooAzure yedekleme daha sonra koruyun.</span><span class="sxs-lookup"><span data-stu-id="bd475-215">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="bd475-216">Merhaba örneklerde biz gösterilmektedir nasıl tooback dosya ve klasörler.</span><span class="sxs-lookup"><span data-stu-id="bd475-216">In hello examples we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="bd475-217">Merhaba mantığı kolayca genişletilmiş toobackup herhangi bir DPM desteklenen veri kaynağı olabilir.</span><span class="sxs-lookup"><span data-stu-id="bd475-217">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="bd475-218">Tüm DPM yedeklemelerini dört bölümden ile koruma grubu (PG) tarafından yönetilir:</span><span class="sxs-lookup"><span data-stu-id="bd475-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="bd475-219">**Grup üyeleri** tüm hello korunabilir nesneler listesi (olarak da bilinen *veri kaynakları* dpm'de) hello tooprotect istediğiniz aynı koruma grubunda.</span><span class="sxs-lookup"><span data-stu-id="bd475-219">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="bd475-220">Örneğin, yedekleme farklı gereksinimlere sahip, bir koruma grubu ve SQL Server veritabanlarını başka bir koruma grubunda tooprotect üretim VM'ler isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd475-220">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="bd475-221">Üretim sunucusundaki herhangi bir veri kaynağı yedekleyebilirsiniz önce DPM Aracısı hello sunucuda yüklü olduğundan ve DPM tarafından yönetilen toomake emin hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd475-221">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="bd475-222">Merhaba adımlarını izleyin [yükleme, DPM Aracısı hello](https://technet.microsoft.com/library/bb870935.aspx) ve toohello bağlama uygun DPM sunucusu.</span><span class="sxs-lookup"><span data-stu-id="bd475-222">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="bd475-223">**Veri koruma yöntemini** hello hedef yedekleme konumları - bant, disk ve bulut belirtir.</span><span class="sxs-lookup"><span data-stu-id="bd475-223">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="bd475-224">Bizim örneğimizde biz veri toohello yerel disk ve toohello bulut korur.</span><span class="sxs-lookup"><span data-stu-id="bd475-224">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="bd475-225">A **yedekleme zamanlaması** yedeklemeler gerçekleştirilecek toobe gerektiğinde ve ne sıklıkta hello verilerin hello DPM sunucusu ile Merhaba üretim sunucusu arasında eşitlenmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="bd475-225">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="bd475-226">A **bekletme zamanlaması** Azure'da ne kadar süreyle tooretain hello kurtarma noktaları belirtir.</span><span class="sxs-lookup"><span data-stu-id="bd475-226">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="bd475-227">Koruma grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd475-227">Creating a protection group</span></span>
<span data-ttu-id="bd475-228">Başlangıç hello kullanarak yeni bir koruma grubu oluşturarak [yeni DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-228">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="bd475-229">cmdlet'i yukarıdaki Hello koruma adlı bir grup oluşturur *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="bd475-229">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="bd475-230">Mevcut bir koruma grubunun ayrıca sonraki tooadd yedekleme toohello Azure bulut değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="bd475-230">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="bd475-231">Ancak, toomake herhangi bir değişiklik toohello koruma grubu - yeni veya varolan - ihtiyacımız tooget bir tanıtıcı üzerinde bir *değiştirilebilir* hello kullanarak nesnesi [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-231">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="bd475-232">Grup üyeleri toohello koruma grubu ekleme</span><span class="sxs-lookup"><span data-stu-id="bd475-232">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="bd475-233">Her DPM aracısının yüklü olduğu hello sunucusunda veri kaynakları listesi hello bilir.</span><span class="sxs-lookup"><span data-stu-id="bd475-233">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="bd475-234">tooadd datasource toohello koruma grubu, DPM Aracısı gereksinimlerini toofirst hello hello veri kaynakları geri toohello DPM sunucusu listesini gönderin.</span><span class="sxs-lookup"><span data-stu-id="bd475-234">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="bd475-235">Seçili ve toohello koruma grubuna eklenen bir veya daha fazla veri kaynakları olan.</span><span class="sxs-lookup"><span data-stu-id="bd475-235">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="bd475-236">Merhaba PowerShell adımlar tooget elde bu şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bd475-236">hello PowerShell steps needed tooget achieve this are:</span></span>

1. <span data-ttu-id="bd475-237">DPM Aracısı hello DPM tarafından yönetilen tüm sunucuların listesi getirilemedi.</span><span class="sxs-lookup"><span data-stu-id="bd475-237">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="bd475-238">Belirli bir sunucu seçin.</span><span class="sxs-lookup"><span data-stu-id="bd475-238">Choose a specific server.</span></span>
3. <span data-ttu-id="bd475-239">Merhaba sunucusundaki tüm veri kaynakları listesi getirilemedi.</span><span class="sxs-lookup"><span data-stu-id="bd475-239">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="bd475-240">Bir veya daha fazla veri kaynakları seçin ve bunları toohello koruma grubu Ekle</span><span class="sxs-lookup"><span data-stu-id="bd475-240">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="bd475-241">hangi hello DPM aracısının yüklü olduğundan ve hello DPM sunucusu tarafından yönetilen sunucuları Hello listesi ile Merhaba edinilen [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-241">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="bd475-242">Biz filtrelemek ve yalnızca PS adıyla yapılandırın, bu örnekte *productionserver01* yedekleme için.</span><span class="sxs-lookup"><span data-stu-id="bd475-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="bd475-243">Şimdi üzerinde hello veri kaynaklarının listesini getirme ```$server``` hello kullanarak [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-243">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="bd475-244">Bu örnekte, biz hello birim için filtre * D:\* hangi istiyoruz tooconfigure yedekleme için.</span><span class="sxs-lookup"><span data-stu-id="bd475-244">In this example we are filtering for hello volume *D:\* which we want tooconfigure for backup.</span></span> <span data-ttu-id="bd475-245">Bu veri kaynağı sonra toohello koruma grubuna eklenen hello kullanarak [Ekle DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-245">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="bd475-246">Toouse hello unutmayın *modifable* koruma grubu nesnesi ```$MPG``` toomake hello ekler.</span><span class="sxs-lookup"><span data-stu-id="bd475-246">Remember toouse hello *modifable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="bd475-247">Veri kaynakları toohello koruma grubu seçilen tüm hello ekleyene kadar gerektiği gibi birçok kez bu adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="bd475-247">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="bd475-248">Yalnızca bir datasource ve hello koruma grubunu oluşturmak için tam hello iş akışı ile başlayın ve daha sonraki bir noktada daha fazla veri kaynakları toohello koruma grubuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd475-248">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="bd475-249">Merhaba veri koruma yöntemi seçme</span><span class="sxs-lookup"><span data-stu-id="bd475-249">Selecting hello data protection method</span></span>
<span data-ttu-id="bd475-250">Merhaba datasources toohello koruma grubuna eklendikten sonra hello sonraki hello kullanarak toospecify hello koruma yöntemini adımdır [kümesi DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-250">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="bd475-251">Bu örnekte, yerel disk ve bulut yedekleme için Kur hello koruma grubu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="bd475-251">In this example, hello Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="bd475-252">Hello kullanarak tooprotect toocloud istediğiniz toospecify hello datasource etmeniz [Ekle DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet'iyle - çevrimiçi bayrağı.</span><span class="sxs-lookup"><span data-stu-id="bd475-252">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="bd475-253">Merhaba bekletme aralığını ayarlama</span><span class="sxs-lookup"><span data-stu-id="bd475-253">Setting hello retention range</span></span>
<span data-ttu-id="bd475-254">Ayarlama hello bekletme hello kullanarak hello yedekleme noktaları için [kümesi DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-254">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="bd475-255">Hello kullanarak Hello yedekleme zamanlaması tanımlanmış önce tek tooset hello bekletme görünebilir ancak ```Set-DPMPolicyObjective``` cmdlet'i sonra değiştirilebilen varsayılan yedekleme zamanlaması otomatik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="bd475-255">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="bd475-256">Bu her zaman mümkün tooset hello yedekleme zamanlaması önce ve sonra bekletme ilkesi hello.</span><span class="sxs-lookup"><span data-stu-id="bd475-256">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="bd475-257">Merhaba aşağıdaki örnekte, hello cmdlet'i disk yedeklemeleri hello bekletme parametreleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="bd475-257">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="bd475-258">Bu yedeklemeler 10 gün ve eşitleme verileri için 6 saatte bir hello üretim sunucusu ve hello DPM sunucusu arasındaki korur.</span><span class="sxs-lookup"><span data-stu-id="bd475-258">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="bd475-259">Merhaba ```SynchronizationFrequencyMinutes``` ne sıklıkta bir yedekleme noktasının, ancak nasıl oluşturulduğunu tanımlamıyor genellikle verileri kopyalanan toohello DPM sunucusu; bu yedeklemeler çok büyük hale gelmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="bd475-259">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="bd475-260">(DPM başvuruyor toothese çevrimiçi yedeklemeler) tooAzure giderek yedeklemeler için hello bekletme aralıkları için yapılandırılabilir [üst öğe Son şeması (GFS) kullanarak bekletme'uzun süreli](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="bd475-260">For backups going tooAzure (DPM refers toothese as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="bd475-261">Diğer bir deyişle, günlük, haftalık, aylık ve yıllık bekletme ilkeleri içeren bir birleşik bekletme ilkesi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd475-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="bd475-262">Bu örnekte, biz istiyoruz hello karmaşık bekletme düzeni temsil eden bir dizi oluşturmak ve ardından hello kullanarak hello bekletme aralığı yapılandırın [kümesi DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-262">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="bd475-263">Set hello yedekleme zamanlaması</span><span class="sxs-lookup"><span data-stu-id="bd475-263">Set hello backup schedule</span></span>
<span data-ttu-id="bd475-264">Merhaba koruma hedefi hello kullanarak belirtirseniz, DPM bir varsayılan yedekleme zamanlaması otomatik olarak ayarlar. ```Set-DPMPolicyObjective``` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-264">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="bd475-265">toochange hello varsayılan zamanlamaların kullanmak hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet hello tarafından izlenen [kümesi DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-265">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="bd475-266">Yukarıdaki hello örnekte ```$onlineSch``` hello varolan çevrimiçi koruma zamanlamasını hello GFS düzeni hello koruma grubu için içeren bir dizi dört öğelerle:</span><span class="sxs-lookup"><span data-stu-id="bd475-266">In hello example above, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="bd475-267">```$onlineSch[0]```Merhaba günlük zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="bd475-267">```$onlineSch[0]``` will contain hello daily schedule</span></span>
2. <span data-ttu-id="bd475-268">```$onlineSch[1]```Merhaba haftalık zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="bd475-268">```$onlineSch[1]``` will contain hello weekly schedule</span></span>
3. <span data-ttu-id="bd475-269">```$onlineSch[2]```Merhaba aylık zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="bd475-269">```$onlineSch[2]``` will contain hello monthly schedule</span></span>
4. <span data-ttu-id="bd475-270">```$onlineSch[3]```Merhaba yıllık zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="bd475-270">```$onlineSch[3]``` will contain hello yearly schedule</span></span>

<span data-ttu-id="bd475-271">Bu nedenle toomodify hello haftalık zamanlama gerekiyorsa, toorefer toohello gerekir ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="bd475-271">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="bd475-272">İlk yedekleme</span><span class="sxs-lookup"><span data-stu-id="bd475-272">Initial backup</span></span>
<span data-ttu-id="bd475-273">Hello için veri kaynağı ilk kez yedeklerken, DPM toocreate DPM çoğaltma biriminde hello datasource toobe korumalı bir kopyasını oluşturacak olan bir başlangıç çoğaltması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd475-273">When backing up a datasource for hello first time, DPM needs toocreate an initial replica which will create a copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="bd475-274">Bu etkinlik için belirli bir saat ya da zamanlanabilir veya hello kullanarak el ile tetiklenebilir [kümesi DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) hello parametre cmdlet'iyle ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="bd475-274">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="bd475-275">DPM çoğaltma ve kurtarma noktası birimi Hello boyutunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="bd475-275">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="bd475-276">Ayrıca DPM çoğaltma birimi yanı sıra birim gölge kopya kullanarak hello boyutunu değiştirebilirsiniz [kümesi DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) hello örnek aşağıda olduğu gibi cmdlet: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - Protectiongroup'u $MPG-el ile - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="bd475-276">You can also change hello size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="bd475-277">Uygulanıyor hello değişiklikleri toohello koruma grubu</span><span class="sxs-lookup"><span data-stu-id="bd475-277">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="bd475-278">Son olarak, DPM hello yeni koruma grubu yapılandırması başına hello yedek almadan önce kaydedilmiş toobe hello değişiklikleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd475-278">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="bd475-279">Bu yapılır hello kullanarak [kümesi DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-279">This is done using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="bd475-280">Görünüm hello yedekleme noktaları</span><span class="sxs-lookup"><span data-stu-id="bd475-280">View hello backup points</span></span>
<span data-ttu-id="bd475-281">Merhaba kullanabilirsiniz [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget bir veri kaynağı için tüm kurtarma noktalarının bir listesi.</span><span class="sxs-lookup"><span data-stu-id="bd475-281">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="bd475-282">Bu örnekte, şunları yapacağız:</span><span class="sxs-lookup"><span data-stu-id="bd475-282">In this example, we will:</span></span>

* <span data-ttu-id="bd475-283">bir dizi depolanan hello DPM sunucusundaki tüm hello PGs getirme```$PG```</span><span class="sxs-lookup"><span data-stu-id="bd475-283">fetch all hello PGs on hello DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="bd475-284">Merhaba datasources karşılık gelen toohello Al```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="bd475-284">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="bd475-285">Tüm hello kurtarma noktaları için bir veri kaynağı alın.</span><span class="sxs-lookup"><span data-stu-id="bd475-285">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="bd475-286">Azure üzerinde korunan verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="bd475-286">Restore data protected on Azure</span></span>
<span data-ttu-id="bd475-287">Verileri geri birleşimidir bir ```RecoverableItem``` nesne ve ```RecoveryOption``` nesne.</span><span class="sxs-lookup"><span data-stu-id="bd475-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="bd475-288">Merhaba önceki bölümde, biz bir veri kaynağı için hello yedekleme noktalarının bir listesini aldı.</span><span class="sxs-lookup"><span data-stu-id="bd475-288">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="bd475-289">Merhaba aşağıdaki örnekte, toorestore bir Hyper-V sanal makineden Azure yedekleme hello ile Birleşen yedekleme noktaları tarafından hedef kurtarma için nasıl ekleyebileceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bd475-289">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="bd475-290">Buna aşağıdakiler dahildir:</span><span class="sxs-lookup"><span data-stu-id="bd475-290">This includes:</span></span>

* <span data-ttu-id="bd475-291">Hello kullanarak bir kurtarma seçeneği oluşturma [yeni DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-291">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="bd475-292">Hello kullanarak yedekleme noktaları getirilirken hello dizisi ```Get-DPMRecoveryPoint``` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd475-292">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="bd475-293">Gelen bir yedekleme noktası toorestore seçme.</span><span class="sxs-lookup"><span data-stu-id="bd475-293">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="bd475-294">Merhaba komutları herhangi bir veri kaynağı türü için kolayca genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="bd475-294">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd475-295">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd475-295">Next steps</span></span>
* <span data-ttu-id="bd475-296">DPM Azure yedekleme hakkında daha fazla bilgi için bkz: [giriş tooDPM yedekleme](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="bd475-296">For more information about Azure Backup for DPM see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
