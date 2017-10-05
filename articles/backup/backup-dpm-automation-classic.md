---
title: "Azure yedekleme: DPM iş yüklerini yedeklemeye kullanım PowerShell | Microsoft Docs"
description: "Dağıtma ve Data Protection Manager (PowerShell kullanarak DPM için) Azure Backup yönetme hakkında bilgi edinin"
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
ms.openlocfilehash: 943a12dcba49a114d206b9dab968da332ea99926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="8f04f-103">PowerShell kullanarak Data Protection Manager (DPM) sunucuları için Azure’a yedekleme dağıtma ve yönetme</span><span class="sxs-lookup"><span data-stu-id="8f04f-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f04f-104">ARM</span><span class="sxs-lookup"><span data-stu-id="8f04f-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="8f04f-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="8f04f-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="8f04f-106">Bu makalede PowerShell yedeklemek ve bir yedekleme Kasası'nı DPM verileri kurtarmak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8f04f-106">This article explains how to use PowerShell to back up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="8f04f-107">Microsoft, tüm yeni dağıtımlar için kurtarma Hizmetleri kasalarının kullanılmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="8f04f-108">Yeni bir Azure yedekleme kullanıcı, makale kullanırsanız [dağıtma ve PowerShell kullanarak Azure Data Protection Manager verilerini yönetmek](backup-dpm-automation.md), bir kurtarma Hizmetleri kasasına verilerinizi depolamak için.</span><span class="sxs-lookup"><span data-stu-id="8f04f-108">If you are a new Azure Backup user, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8f04f-109">Artık Backup kasalarınızı Kurtarma Hizmetleri kasalarına yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f04f-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="8f04f-110">Ayrıntılı bilgi için [Backup kasasını Kurtarma Hizmetleri kasasına yükseltme](backup-azure-upgrade-backup-to-recovery-services.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="8f04f-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="8f04f-111">Microsoft, Backup kasalarınızı Kurtarma Hizmetleri kasalarına yükseltmenizi önerir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="8f04f-112">15 Ekim 2017’den itibaren, PowerShell kullanarak Backup kasaları oluşturamayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="8f04f-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="8f04f-113">**1 Kasım 2017’ye kadar**:</span><span class="sxs-lookup"><span data-stu-id="8f04f-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="8f04f-114">Yükseltilmemiş olan tüm Backup kasaları Kurtarma Hizmetleri kasalarına otomatik olarak yükseltilecektir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="8f04f-115">Klasik portalda yedekleme verilerinize erişemeyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8f04f-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="8f04f-116">Bunun yerine, Kurtarma Hizmetleri kasalarındaki yedekleme verilerinize erişmek için Azure portalını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f04f-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="8f04f-117">PowerShell ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="8f04f-117">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="8f04f-118">Yedeklemeler için Azure Data Protection Manager'dan yönetmek için PowerShell kullanmadan önce PowerShell'de sağ ortama sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-118">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you will need to have the right environment in PowerShell.</span></span> <span data-ttu-id="8f04f-119">PowerShell oturumu başlangıcında sağ modülleri alın ve doğru DPM cmdlet başvuru izin vermek için aşağıdaki komutu çalıştırdığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="8f04f-119">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome to the DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="8f04f-120">Kurulumu'nu ve kaydı</span><span class="sxs-lookup"><span data-stu-id="8f04f-120">Setup and Registration</span></span>
<span data-ttu-id="8f04f-121">Başlamak için:</span><span class="sxs-lookup"><span data-stu-id="8f04f-121">To begin:</span></span>

1. <span data-ttu-id="8f04f-122">[En son PowerShell indirme](https://github.com/Azure/azure-powershell/releases) (gerekli minimum sürüm: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="8f04f-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="8f04f-123">Azure Backup cmdlet'leri geçerek etkinleştirmek *AzureResourceManager* kullanarak moduna **Switch-AzureMode** komutunu:</span><span class="sxs-lookup"><span data-stu-id="8f04f-123">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="8f04f-124">Aşağıdaki kurulumunu ve kaydını görevleri PowerShell ile otomatik olarak yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="8f04f-124">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="8f04f-125">Yedekleme kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="8f04f-125">Create a backup vault</span></span>
* <span data-ttu-id="8f04f-126">Azure Backup aracısını yükleme</span><span class="sxs-lookup"><span data-stu-id="8f04f-126">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="8f04f-127">Azure Backup hizmeti ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="8f04f-127">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="8f04f-128">Ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="8f04f-128">Networking settings</span></span>
* <span data-ttu-id="8f04f-129">Şifreleme ayarları</span><span class="sxs-lookup"><span data-stu-id="8f04f-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="8f04f-130">Yedekleme kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="8f04f-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="8f04f-131">İlk olarak Azure Yedekleme'yi kullanarak müşteriler için aboneliğiniz ile birlikte kullanılacak Azure Backup sağlayıcı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-131">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="8f04f-132">Bu aşağıdaki komutu çalıştırarak yapılabilir: Register-AzureProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="8f04f-132">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="8f04f-133">Kullanarak yeni bir yedekleme kasası oluşturma **yeni AzureRMBackupVault** komutunu.</span><span class="sxs-lookup"><span data-stu-id="8f04f-133">You can create a new backup vault using the **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="8f04f-134">Yedekleme kasası bir ARM kaynak olduğundan, bir kaynak grubu içindeki yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-134">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="8f04f-135">Yükseltilmiş bir Azure PowerShell konsolunda aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8f04f-135">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="8f04f-136">Belirtilen abonelik kullanarak tüm yedekleme kasalarının listesi elde edebilirsiniz **Get-AzureRMBackupVault** komutunu.</span><span class="sxs-lookup"><span data-stu-id="8f04f-136">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="8f04f-137">Bir DPM sunucusu üzerinde Azure Backup aracısını yükleme</span><span class="sxs-lookup"><span data-stu-id="8f04f-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="8f04f-138">Azure Backup aracısını yüklemeden önce Windows Server yükleyici indirildi ve mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="8f04f-139">Yükleyicisi'nden en son sürümünü almak [Microsoft Download Center](http://aka.ms/azurebackup_agent) veya yedekleme kasasının Pano sayfası.</span><span class="sxs-lookup"><span data-stu-id="8f04f-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="8f04f-140">Yükleyici gibi kolay erişilebilir bir konuma kaydedin * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="8f04f-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="8f04f-141">Aracıyı yüklemek için yükseltilmiş bir PowerShell konsolunda aşağıdaki komutu çalıştırın **DPM sunucusundaki**:</span><span class="sxs-lookup"><span data-stu-id="8f04f-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="8f04f-142">Bu, tüm varsayılan seçeneklerle Aracısı'nı yükler.</span><span class="sxs-lookup"><span data-stu-id="8f04f-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="8f04f-143">Yükleme arka planda birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="8f04f-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="8f04f-144">Belirtmezseniz, */nu* seçeneği **Windows Update** tüm güncelleştirmeleri denetlemek için yükleme işleminin sonunda penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="8f04f-144">If you do not specify the */nu* option the **Windows Update** window will open at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="8f04f-145">Aracı yüklü programlar listesinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-145">The agent will show in the list of installed programs.</span></span> <span data-ttu-id="8f04f-146">Yüklü programların listesini görmek için şu adrese gidin **Denetim Masası** > **programları** > **programlar ve Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="8f04f-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Yüklü aracı](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="8f04f-148">Yükleme Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="8f04f-148">Installation options</span></span>
<span data-ttu-id="8f04f-149">Komut satırı kullanılabilir tüm seçenekleri görmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8f04f-149">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="8f04f-150">Mevcut seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8f04f-150">The available options include:</span></span>

| <span data-ttu-id="8f04f-151">Seçenek</span><span class="sxs-lookup"><span data-stu-id="8f04f-151">Option</span></span> | <span data-ttu-id="8f04f-152">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="8f04f-152">Details</span></span> | <span data-ttu-id="8f04f-153">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="8f04f-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8f04f-154">/q</span><span class="sxs-lookup"><span data-stu-id="8f04f-154">/q</span></span> |<span data-ttu-id="8f04f-155">Sessiz yükleme</span><span class="sxs-lookup"><span data-stu-id="8f04f-155">Quiet installation</span></span> |- |
| <span data-ttu-id="8f04f-156">p: "Konum"</span><span class="sxs-lookup"><span data-stu-id="8f04f-156">/p:"location"</span></span> |<span data-ttu-id="8f04f-157">Azure Backup Aracısı yükleme klasörünün yolu.</span><span class="sxs-lookup"><span data-stu-id="8f04f-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="8f04f-158">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Aracısı</span><span class="sxs-lookup"><span data-stu-id="8f04f-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="8f04f-159">/ s: "Konum"</span><span class="sxs-lookup"><span data-stu-id="8f04f-159">/s:"location"</span></span> |<span data-ttu-id="8f04f-160">Azure Backup aracısı için önbellek klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="8f04f-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="8f04f-161">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="8f04f-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="8f04f-162">/m</span><span class="sxs-lookup"><span data-stu-id="8f04f-162">/m</span></span> |<span data-ttu-id="8f04f-163">Microsoft Update'e kabulü</span><span class="sxs-lookup"><span data-stu-id="8f04f-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="8f04f-164">/nu</span><span class="sxs-lookup"><span data-stu-id="8f04f-164">/nu</span></span> |<span data-ttu-id="8f04f-165">Yükleme tamamlandıktan sonra güncelleştirmeleri denetleme</span><span class="sxs-lookup"><span data-stu-id="8f04f-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="8f04f-166">/d</span><span class="sxs-lookup"><span data-stu-id="8f04f-166">/d</span></span> |<span data-ttu-id="8f04f-167">Microsoft Azure kurtarma Hizmetleri Aracısı kaldırır</span><span class="sxs-lookup"><span data-stu-id="8f04f-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="8f04f-168">/ph</span><span class="sxs-lookup"><span data-stu-id="8f04f-168">/ph</span></span> |<span data-ttu-id="8f04f-169">Proxy konağı adresi</span><span class="sxs-lookup"><span data-stu-id="8f04f-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="8f04f-170">/PO</span><span class="sxs-lookup"><span data-stu-id="8f04f-170">/po</span></span> |<span data-ttu-id="8f04f-171">Proxy ana bilgisayar bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="8f04f-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="8f04f-172">/PU</span><span class="sxs-lookup"><span data-stu-id="8f04f-172">/pu</span></span> |<span data-ttu-id="8f04f-173">Proxy konağı kullanıcı</span><span class="sxs-lookup"><span data-stu-id="8f04f-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="8f04f-174">/pw</span><span class="sxs-lookup"><span data-stu-id="8f04f-174">/pw</span></span> |<span data-ttu-id="8f04f-175">Proxy parolası</span><span class="sxs-lookup"><span data-stu-id="8f04f-175">Proxy Password</span></span> |- |

### <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="8f04f-176">Azure Backup hizmeti ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="8f04f-176">Registering with the Azure Backup service</span></span>
<span data-ttu-id="8f04f-177">Azure Backup hizmeti ile kaydedebilmek için emin olmak gereken [Önkoşullar](backup-azure-dpm-introduction.md) karşılanır.</span><span class="sxs-lookup"><span data-stu-id="8f04f-177">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="8f04f-178">Yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8f04f-178">You must:</span></span>

* <span data-ttu-id="8f04f-179">Geçerli bir Azure aboneliğiniz</span><span class="sxs-lookup"><span data-stu-id="8f04f-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="8f04f-180">Bir yedekleme kasası sahip</span><span class="sxs-lookup"><span data-stu-id="8f04f-180">Have a backup vault</span></span>

<span data-ttu-id="8f04f-181">Kasa kimlik bilgilerini indirmek için çalıştırın **Get-AzureBackupVaultCredentials** uygun bir konumda ister bir Azure PowerShell konsolunda ve deposu komutunu * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="8f04f-181">To download the vault credentials, run the **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="8f04f-182">Makine kasası ile kaydediliyor yapılır kullanarak [başlangıç DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8f04f-182">Registering the machine with the vault is done using the [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="8f04f-183">Bu Microsoft Azure belirtilen kasa kimlik bilgilerini kullanarak kasası "TestingServer" adlı DPM sunucusuna kaydeder.</span><span class="sxs-lookup"><span data-stu-id="8f04f-183">This will register the DPM Server named “TestingServer” with Microsoft Azure Vault using the specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8f04f-184">Kasa kimlik bilgileri dosyası belirtmek için göreli yolların kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8f04f-184">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="8f04f-185">Cmdlet'i bir girdi olarak mutlak bir yol sağlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="8f04f-185">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="8f04f-186">İlk yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="8f04f-186">Initial configuration settings</span></span>
<span data-ttu-id="8f04f-187">DPM sunucusu Azure yedekleme kasası ile kaydedildikten sonra varsayılan abonelik ayarlarını başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="8f04f-187">Once the DPM Server is registered with the Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="8f04f-188">Bu abonelik ayarlar, ağ, şifreleme ve hazırlama alanı içerir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-188">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="8f04f-189">Önce bir tanıtıcı kullanarak mevcut (varsayılan) ayarları almanız abonelik ayarlarını değiştirme başlamaya [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8f04f-189">To begin changing the subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="8f04f-190">Bu yerel PowerShell nesneye yapılan değişikliklerden ```$setting``` ve ardından tam nesne DPM ve bunları kaydetmek için Azure Backup için kararlıdır kullanarak [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-190">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="8f04f-191">Kullanmanız gereken ```–Commit``` değişiklikler kalıcı emin olmak için bayrak.</span><span class="sxs-lookup"><span data-stu-id="8f04f-191">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="8f04f-192">Ayarları değil uygulanan ve olması kaydedilen sürece Azure yedekleme tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8f04f-192">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="8f04f-193">Ağ</span><span class="sxs-lookup"><span data-stu-id="8f04f-193">Networking</span></span>
<span data-ttu-id="8f04f-194">Azure Backup hizmeti internet üzerindeki DPM makineye bağlantısını bir proxy sunucu üzerinden ise, Ara sunucu ayarlarını yedeklemelerinin başarılı olması için sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8f04f-194">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for backups to succeed.</span></span> <span data-ttu-id="8f04f-195">Bu kullanılarak yapılır ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` ve ```ProxyPassword``` parametrelerle [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-195">This is done by using the ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="8f04f-196">Bu örnekte, olmadığından hiçbir Ara sunucunun biz açıkça herhangi bir proxy ile ilgili bilgi temizleme.</span><span class="sxs-lookup"><span data-stu-id="8f04f-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="8f04f-197">Bant genişliği kullanımı ile seçenekleri de denetlenebilir ```-WorkHourBandwidth``` ve ```-NonWorkHourBandwidth``` haftanın belirli bir dizi için.</span><span class="sxs-lookup"><span data-stu-id="8f04f-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="8f04f-198">Bu örnekte, biz herhangi azaltma ayarlıyorsanız değil.</span><span class="sxs-lookup"><span data-stu-id="8f04f-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-the-staging-area"></a><span data-ttu-id="8f04f-199">Hazırlama alanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8f04f-199">Configuring the staging Area</span></span>
<span data-ttu-id="8f04f-200">DPM sunucusunda çalışan Azure Yedekleme aracısı, (yerel hazırlama alanı) buluttan geri yüklenen veriler için geçici depolama gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-200">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="8f04f-201">Hazırlama alanı kullanarak yapılandırma [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i ve ```-StagingAreaPath``` parametresi.</span><span class="sxs-lookup"><span data-stu-id="8f04f-201">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="8f04f-202">Yukarıdaki örnekte, hazırlama alanı ayarlanacak *C:\StagingArea* PowerShell nesnesindeki ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="8f04f-202">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="8f04f-203">Belirtilen klasör zaten var, aksi takdirde Abonelik ayarları son yürütme başarısız olur emin olun.</span><span class="sxs-lookup"><span data-stu-id="8f04f-203">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="8f04f-204">Şifreleme ayarları</span><span class="sxs-lookup"><span data-stu-id="8f04f-204">Encryption settings</span></span>
<span data-ttu-id="8f04f-205">Yedekleme verilerini Azure Backup için gönderilen veri gizliliğini korumak için şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-205">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="8f04f-206">Şifreleme Parolası "geri yükleme sırasındaki verileri şifrelemek için parola" dir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-206">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="8f04f-207">Ayarlandıktan sonra bu bilgileri güvenli tutmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-207">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="8f04f-208">Aşağıdaki örnekte, ilk komut dizesini sayıya dönüştürür ```passphrase123456789``` güvenli bir dize ve güvenli dize değişkenine adlı atar ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="8f04f-208">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="8f04f-209">İkinci komut güvenli dize ayarlar ```$Passphrase``` yedeklemeleri şifrelemek için parolayı olarak.</span><span class="sxs-lookup"><span data-stu-id="8f04f-209">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="8f04f-210">Ayarlandıktan sonra parola bilgilerini güvenli ve güvenli tutar.</span><span class="sxs-lookup"><span data-stu-id="8f04f-210">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="8f04f-211">Bu parola Azure kaynağından veri geri olmaz.</span><span class="sxs-lookup"><span data-stu-id="8f04f-211">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="8f04f-212">Bu noktada, tüm gerekli değişiklikleri yaptınız ```$setting``` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8f04f-212">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="8f04f-213">Değişiklikleri kaydetmek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8f04f-213">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="8f04f-214">Azure yedekleme verilerini koruma</span><span class="sxs-lookup"><span data-stu-id="8f04f-214">Protect data to Azure Backup</span></span>
<span data-ttu-id="8f04f-215">Bu bölümde, bir üretim sunucusunu DPM sunucusuna Ekle ve ardından yerel DPM depolama ve ardından Azure yedekleme verileri koruyun.</span><span class="sxs-lookup"><span data-stu-id="8f04f-215">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="8f04f-216">Örneklerde dosyaları ve klasörleri yedeklemek göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="8f04f-216">In the examples we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="8f04f-217">Mantığı, herhangi bir DPM desteklenen veri kaynağı yedeklemek için kolayca genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-217">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="8f04f-218">Tüm DPM yedeklemelerini dört bölümden ile koruma grubu (PG) tarafından yönetilir:</span><span class="sxs-lookup"><span data-stu-id="8f04f-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="8f04f-219">**Grup üyeleri** korunabilir tüm nesnelerin bir listesi verilmiştir (olarak da bilinen *veri kaynakları* dpm'de) aynı koruma grubunda korumak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="8f04f-219">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="8f04f-220">Örneğin, farklı yedekleme gereksinimleri olabilir olarak üretim sanal makineleri bir koruma grubu ve SQL Server veritabanlarını başka bir koruma grubunda korumak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f04f-220">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="8f04f-221">Herhangi bir veri kaynağı emin olmak için gereken bir üretim sunucusunda yedeklenmeden önce DPM aracısını sunucuda yüklü ve DPM tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-221">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="8f04f-222">Adımları için [DPM aracısını yüklemeye](https://technet.microsoft.com/library/bb870935.aspx) ve uygun DPM sunucusuna bağlama.</span><span class="sxs-lookup"><span data-stu-id="8f04f-222">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="8f04f-223">**Veri koruma yöntemini** hedef yedekleme konumları - bant, disk ve bulut belirtir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-223">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="8f04f-224">Bizim örneğimizde biz verileri yerel diske ve bulut için koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="8f04f-224">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="8f04f-225">A **yedekleme zamanlaması** yedeklemeler yapılması gerektiğinde ve verileri DPM sunucusu ve üretim sunucusu arasında ne sıklıkla eşitlenmesi gerektiği belirtir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-225">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="8f04f-226">A **bekletme zamanlaması** belirleyen ne kadar süreyle Azure kurtarma noktalarını korumak için.</span><span class="sxs-lookup"><span data-stu-id="8f04f-226">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="8f04f-227">Koruma grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8f04f-227">Creating a protection group</span></span>
<span data-ttu-id="8f04f-228">Başlangıç kullanarak yeni bir koruma grubu oluşturarak [yeni DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-228">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="8f04f-229">Yukarıdaki cmdlet adlı bir koruma grubu oluşturacak *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="8f04f-229">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="8f04f-230">Mevcut bir koruma grubunun de daha sonra Azure bulut yedekleme eklemek için değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-230">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="8f04f-231">Ancak, koruma grubuna - herhangi bir değişiklik yapmak için yeni veya varolan - bir tanıtıcı almaya ihtiyacımız bir *değiştirilebilir* kullanarak nesne [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-231">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="8f04f-232">Grup üyeleri koruma grubuna ekleniyor</span><span class="sxs-lookup"><span data-stu-id="8f04f-232">Adding group members to the Protection Group</span></span>
<span data-ttu-id="8f04f-233">Her DPM aracısının yüklü olduğu sunucuda veri kaynakları listesi bilir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-233">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="8f04f-234">Bir veri kaynağını koruma grubuna eklemek için DPM Aracısı önce veri kaynaklarının listesini DPM sunucusuna geri göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-234">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="8f04f-235">Bir veya daha fazla veri kaynakları sonra seçili ve koruma grubuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-235">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="8f04f-236">Almak için gerekli olan PowerShell adımları elde etmek bu şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8f04f-236">The PowerShell steps needed to get achieve this are:</span></span>

1. <span data-ttu-id="8f04f-237">DPM Aracısı üzerinden DPM tarafından yönetilen tüm sunucuların listesi getirilemedi.</span><span class="sxs-lookup"><span data-stu-id="8f04f-237">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="8f04f-238">Belirli bir sunucu seçin.</span><span class="sxs-lookup"><span data-stu-id="8f04f-238">Choose a specific server.</span></span>
3. <span data-ttu-id="8f04f-239">Tüm veri kaynakları listesini sunucuda getirin.</span><span class="sxs-lookup"><span data-stu-id="8f04f-239">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="8f04f-240">Bir veya daha fazla veri kaynakları seçin ve bunları koruma grubuna Ekle</span><span class="sxs-lookup"><span data-stu-id="8f04f-240">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="8f04f-241">DPM aracısının yüklü olduğundan ve DPM sunucusu tarafından yönetilen sunucuları listesi ile edinilen [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-241">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="8f04f-242">Biz filtrelemek ve yalnızca PS adıyla yapılandırın, bu örnekte *productionserver01* yedekleme için.</span><span class="sxs-lookup"><span data-stu-id="8f04f-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="8f04f-243">Şimdi üzerinde veri kaynaklarının listesini getirme ```$server``` kullanarak [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-243">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="8f04f-244">Bu örnekte şu birim için filtre * D:\* yedekleme için yapılandırmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="8f04f-244">In this example we are filtering for the volume *D:\* which we want to configure for backup.</span></span> <span data-ttu-id="8f04f-245">Bu veri kaynağı sonra koruma grubuna eklenen kullanarak [Ekle DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-245">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="8f04f-246">Kullanmayı unutmayın *modifable* koruma grubu nesnesi ```$MPG``` eklemeleri yapma.</span><span class="sxs-lookup"><span data-stu-id="8f04f-246">Remember to use the *modifable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="8f04f-247">Tüm seçilen veri kaynakları koruma grubuna ekleyene kadar gerektiği gibi birçok kez bu adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="8f04f-247">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="8f04f-248">Yalnızca bir datasource ile başlatın ve koruma grubunu oluşturmak için iş akışı tamamlamak ve sonraki bir noktada daha fazla veri kaynakları koruma grubuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8f04f-248">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="8f04f-249">Veri koruma yöntemini seçme</span><span class="sxs-lookup"><span data-stu-id="8f04f-249">Selecting the data protection method</span></span>
<span data-ttu-id="8f04f-250">Veri kaynakları koruma grubuna eklendikten sonra sonraki adım koruma yöntemini kullanarak belirtmektir [kümesi DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-250">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="8f04f-251">Bu örnekte, kurulumu yerel disk ve bulut yedekleme için koruma grubu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8f04f-251">In this example, the Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="8f04f-252">Ayrıca kullanarak buluta korumak istediğiniz veri kaynağını belirtmek zorunda [Ekle DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet'iyle - çevrimiçi bayrağı.</span><span class="sxs-lookup"><span data-stu-id="8f04f-252">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="8f04f-253">Bekletme aralığını ayarlama</span><span class="sxs-lookup"><span data-stu-id="8f04f-253">Setting the retention range</span></span>
<span data-ttu-id="8f04f-254">Kullanarak yedekleme noktaları için bekletme ayarlamak [kümesi DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-254">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="8f04f-255">Kullanarak yedekleme zamanlaması tanımlanmış önce bekletme ayarlamak tek görünebilir ancak ```Set-DPMPolicyObjective``` cmdlet'i sonra değiştirilebilen varsayılan yedekleme zamanlaması otomatik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8f04f-255">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="8f04f-256">Yedeklemeyi zamanlama ilk kümesi ve sonra bekletme ilkesi için her zaman mümkündür.</span><span class="sxs-lookup"><span data-stu-id="8f04f-256">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="8f04f-257">Aşağıdaki örnek cmdlet disk yedeklemeleri bekletme parametreleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8f04f-257">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="8f04f-258">Bu yedeklemeler 10 gün ve eşitleme verileri için 6 saatte bir ve üretim sunucusu DPM sunucusu arasında korur.</span><span class="sxs-lookup"><span data-stu-id="8f04f-258">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="8f04f-259">```SynchronizationFrequencyMinutes``` Ne sıklıkta bir yedekleme noktasının, ancak nasıl oluşturulduğunu tanımlamıyor genellikle verileri DPM sunucusuna kopyalanır; bu yedeklemeler çok büyük hale gelmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="8f04f-259">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="8f04f-260">Azure'a giden yedeklemeleri (DPM başvurduğu çevrimiçi yedeklemeler olarak) bekletme aralıkları için yapılandırılabilir [üst öğe Son şeması (GFS) kullanarak bekletme'uzun süreli](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="8f04f-260">For backups going to Azure (DPM refers to these as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="8f04f-261">Diğer bir deyişle, günlük, haftalık, aylık ve yıllık bekletme ilkeleri içeren bir birleşik bekletme ilkesi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f04f-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="8f04f-262">Bu örnekte, biz istiyoruz karmaşık bekletme düzeni temsil eden bir dizi oluşturmak ve bekletme aralığı kullanarak yapılandırma [kümesi DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-262">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="8f04f-263">Yedekleme zamanlamasını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="8f04f-263">Set the backup schedule</span></span>
<span data-ttu-id="8f04f-264">Koruma hedefi kullanarak belirtirseniz, DPM bir varsayılan yedekleme zamanlaması otomatik olarak ayarlar. ```Set-DPMPolicyObjective``` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-264">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="8f04f-265">Varsayılan zamanlamaların değiştirmek için kullanın [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet arkasından [kümesi DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-265">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="8f04f-266">Yukarıdaki örnekte ```$onlineSch``` GFS düzeni koruma grubunda varolan çevrimiçi koruma zamanlamasını içeren bir dizi dört öğelerle:</span><span class="sxs-lookup"><span data-stu-id="8f04f-266">In the example above, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="8f04f-267">```$onlineSch[0]```Günlük Zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="8f04f-267">```$onlineSch[0]``` will contain the daily schedule</span></span>
2. <span data-ttu-id="8f04f-268">```$onlineSch[1]```Haftalık Zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="8f04f-268">```$onlineSch[1]``` will contain the weekly schedule</span></span>
3. <span data-ttu-id="8f04f-269">```$onlineSch[2]```Aylık zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="8f04f-269">```$onlineSch[2]``` will contain the monthly schedule</span></span>
4. <span data-ttu-id="8f04f-270">```$onlineSch[3]```Yıllık zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="8f04f-270">```$onlineSch[3]``` will contain the yearly schedule</span></span>

<span data-ttu-id="8f04f-271">Haftalık Zamanlama değiştirmeniz gerekiyorsa, başvurmanız gerekir böylece ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="8f04f-271">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="8f04f-272">İlk yedekleme</span><span class="sxs-lookup"><span data-stu-id="8f04f-272">Initial backup</span></span>
<span data-ttu-id="8f04f-273">Bir veri kaynağı için ilk kez yedeklerken, DPM DPM çoğaltma birimi üzerinde korunacak veri kaynağı bir kopyasını oluşturacak olan bir ilk çoğaltma oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-273">When backing up a datasource for the first time, DPM needs to create an initial replica which will create a copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="8f04f-274">Bu etkinlik için belirli bir saat ya da zamanlanabilir veya kullanarak el ile tetiklenebilir [kümesi DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) parametresi cmdlet'iyle ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="8f04f-274">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="8f04f-275">DPM çoğaltma ve kurtarma noktası biriminin boyutunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="8f04f-275">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="8f04f-276">Ayrıca DPM çoğaltma birimi yanı sıra birim gölge kopya kullanarak boyutunu değiştirebilirsiniz [kümesi DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet gibi örnek aşağıda: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - Protectiongroup'u $MPG-el ile - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="8f04f-276">You can also change the size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="8f04f-277">Koruma grubu değişiklikleri işleme</span><span class="sxs-lookup"><span data-stu-id="8f04f-277">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="8f04f-278">Son olarak, değişiklikleri DPM yeni koruma grubu yapılandırması başına yedek almadan önce kaydedilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-278">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="8f04f-279">Bu yapılır kullanarak [kümesi DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-279">This is done using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="8f04f-280">Yedekleme noktaları görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="8f04f-280">View the backup points</span></span>
<span data-ttu-id="8f04f-281">Kullanabileceğiniz [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) bir veri kaynağı için tüm kurtarma noktalarının bir listesini almak için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8f04f-281">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="8f04f-282">Bu örnekte, şunları yapacağız:</span><span class="sxs-lookup"><span data-stu-id="8f04f-282">In this example, we will:</span></span>

* <span data-ttu-id="8f04f-283">bir dizi depolanan DPM sunucusundaki tüm PGs getirme```$PG```</span><span class="sxs-lookup"><span data-stu-id="8f04f-283">fetch all the PGs on the DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="8f04f-284">karşılık gelen veri kaynakları alma```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="8f04f-284">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="8f04f-285">veri kaynağı için tüm kurtarma noktalarının alın.</span><span class="sxs-lookup"><span data-stu-id="8f04f-285">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="8f04f-286">Azure üzerinde korunan verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="8f04f-286">Restore data protected on Azure</span></span>
<span data-ttu-id="8f04f-287">Verileri geri birleşimidir bir ```RecoverableItem``` nesne ve ```RecoveryOption``` nesne.</span><span class="sxs-lookup"><span data-stu-id="8f04f-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="8f04f-288">Önceki bölümde biz bir veri kaynağı için yedekleme noktalarının bir listesini aldı.</span><span class="sxs-lookup"><span data-stu-id="8f04f-288">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="8f04f-289">Aşağıdaki örnekte, kurtarma için hedef yedekleme noktaları birleştirerek bir Hyper-V sanal makinesi Azure Yedekleme'den geri yükleme göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-289">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="8f04f-290">Buna aşağıdakiler dahildir:</span><span class="sxs-lookup"><span data-stu-id="8f04f-290">This includes:</span></span>

* <span data-ttu-id="8f04f-291">Kurtarma seçeneğini kullanarak oluşturma [yeni DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-291">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="8f04f-292">Kullanarak yedekleme noktaları dizisi getirme ```Get-DPMRecoveryPoint``` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8f04f-292">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="8f04f-293">Geri yüklemek için bir yedekleme noktasının seçme.</span><span class="sxs-lookup"><span data-stu-id="8f04f-293">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="8f04f-294">Komutları, herhangi bir veri kaynağı türü için kolayca genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="8f04f-294">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f04f-295">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8f04f-295">Next steps</span></span>
* <span data-ttu-id="8f04f-296">DPM Azure yedekleme hakkında daha fazla bilgi için bkz: [DPM yedekleme giriş](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="8f04f-296">For more information about Azure Backup for DPM see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
