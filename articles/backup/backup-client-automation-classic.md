---
title: "Windows Server Yedekleme Azure yönetmek için PowerShell kullanma | Microsoft Docs"
description: "Dağıtın ve PowerShell kullanarak Windows Server Yedekleme yönetin."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: e7e269e2-1f11-41a9-957b-a2155de6a1e0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: saurse;markgal;nkolli;trinadhk
ms.openlocfilehash: a8e20356ae383ee4fa2158ea544d5d0905028124
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="947e8-103">PowerShell kullanarak Windows Server/Windows İstemcisi için Azure’a yedekleme dağıtma ve yönetme</span><span class="sxs-lookup"><span data-stu-id="947e8-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="947e8-104">ARM</span><span class="sxs-lookup"><span data-stu-id="947e8-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="947e8-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="947e8-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="947e8-106">Bu makalede PowerShell Windows Server veya Windows iş istasyonu veri için bir yedekleme kasası yedekleme için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="947e8-106">This article explains how to use PowerShell to back up Windows Server or Windows workstation data to a backup vault.</span></span> <span data-ttu-id="947e8-107">Microsoft, tüm yeni dağıtımlar için kurtarma Hizmetleri kasalarının kullanılmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="947e8-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="947e8-108">Yeni bir Azure yedekleme kullanıcı yoksa ve bir yedekleme kasası, aboneliğinizde oluşturmadıysanız, makale kullanırsınız [dağıtma ve PowerShell kullanarak Azure Data Protection Manager verilerini yönetmek](backup-client-automation.md) bir kurtarma Hizmetleri kasasına verilerinizi depolamak için.</span><span class="sxs-lookup"><span data-stu-id="947e8-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="947e8-109">Artık Backup kasalarınızı Kurtarma Hizmetleri kasalarına yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="947e8-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="947e8-110">Ayrıntılı bilgi için [Backup kasasını Kurtarma Hizmetleri kasasına yükseltme](backup-azure-upgrade-backup-to-recovery-services.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="947e8-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="947e8-111">Microsoft, Backup kasalarınızı Kurtarma Hizmetleri kasalarına yükseltmenizi önerir.</span><span class="sxs-lookup"><span data-stu-id="947e8-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="947e8-112">15 Ekim 2017’den itibaren, PowerShell kullanarak Backup kasaları oluşturamayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="947e8-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="947e8-113">**1 Kasım 2017’ye kadar**:</span><span class="sxs-lookup"><span data-stu-id="947e8-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="947e8-114">Yükseltilmemiş olan tüm Backup kasaları Kurtarma Hizmetleri kasalarına otomatik olarak yükseltilecektir.</span><span class="sxs-lookup"><span data-stu-id="947e8-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="947e8-115">Klasik portalda yedekleme verilerinize erişemeyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="947e8-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="947e8-116">Bunun yerine, Kurtarma Hizmetleri kasalarındaki yedekleme verilerinize erişmek için Azure portalını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="947e8-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="947e8-117">Azure PowerShell'i yükleme</span><span class="sxs-lookup"><span data-stu-id="947e8-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="947e8-118">Azure PowerShell 1.0 Ekim 2015'te yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="947e8-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="947e8-119">Bu sürüm 0.9.8 başarılı bir şekilde serbest bırakır ve bazı önemli değişiklikler hakkında özellikle cmdlet'leri adlandırma desenini getirildi.</span><span class="sxs-lookup"><span data-stu-id="947e8-119">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="947e8-120">1.0 cmdlet'leri {fiil}-AzureRm{isim} adlandırma desenini izler; Buna karşın, 0.9.8 adlarında **Rm** bulunmaz (örneğin, New- AzureResourceGroup yerine New-AzureRmResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="947e8-120">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="947e8-121">Azure PowerShell 0.9.8 kullanıldığında, önce **Switch-AzureMode AzureResourceManager** komutunu çalıştırarak Resource Manager modunu etkinleştirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="947e8-121">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="947e8-122">Bu komut 1.0 veya üstü gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="947e8-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="947e8-123">0.9.8 için yazılan komut dosyalarınızı kullanmak isterseniz, 1.0 veya üstü ortamında, dikkatle sınama ortamında bir üretim öncesi ortamda komut dosyalarını üretimde beklenmeyen etkiyi önlemek için kullanmadan önce.</span><span class="sxs-lookup"><span data-stu-id="947e8-123">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="947e8-124">[En son PowerShell sürümü indirme](https://github.com/Azure/azure-powershell/releases) (gerekli minimum sürüm: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="947e8-124">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="947e8-125">Yedekleme kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="947e8-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="947e8-126">İlk olarak Azure Yedekleme'yi kullanarak müşteriler için aboneliğiniz ile birlikte kullanılacak Azure Backup sağlayıcı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="947e8-126">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="947e8-127">Bu aşağıdaki komutu çalıştırarak yapılabilir: Register-AzureProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="947e8-127">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="947e8-128">Kullanarak yeni bir yedekleme kasası oluşturma **yeni AzureRMBackupVault** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="947e8-128">You can create a new backup vault using the **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="947e8-129">Yedekleme kasası bir ARM kaynak olduğundan, bir kaynak grubu içindeki yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="947e8-129">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="947e8-130">Yükseltilmiş bir Azure PowerShell konsolunda aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="947e8-130">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="947e8-131">Kullanım **Get-AzureRMBackupVault** cmdlet'ini bir abonelikte yedekleme kasalarının listesi.</span><span class="sxs-lookup"><span data-stu-id="947e8-131">Use the **Get-AzureRMBackupVault** cmdlet to list the backup vaults in a subscription.</span></span>

## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="947e8-132">Azure Backup aracısını yükleme</span><span class="sxs-lookup"><span data-stu-id="947e8-132">Installing the Azure Backup agent</span></span>
<span data-ttu-id="947e8-133">Azure Backup aracısını yüklemeden önce Windows Server yükleyici indirildi ve mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="947e8-133">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="947e8-134">Yükleyicisi'nden en son sürümünü almak [Microsoft Download Center](http://aka.ms/azurebackup_agent) veya yedekleme kasasının Pano sayfası.</span><span class="sxs-lookup"><span data-stu-id="947e8-134">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="947e8-135">Yükleyici gibi kolay erişilebilir bir konuma kaydedin * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="947e8-135">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="947e8-136">Aracıyı yüklemek için yükseltilmiş bir PowerShell konsolunda aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="947e8-136">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="947e8-137">Bu, tüm varsayılan seçeneklerle Aracısı'nı yükler.</span><span class="sxs-lookup"><span data-stu-id="947e8-137">This installs the agent with all the default options.</span></span> <span data-ttu-id="947e8-138">Yükleme arka planda birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="947e8-138">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="947e8-139">Belirtmezseniz, */nu* seçeneği sonra **Windows Update** tüm güncelleştirmeleri denetlemek için yükleme işleminin sonunda penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="947e8-139">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="947e8-140">Yüklendikten sonra aracı yüklü programlar listesinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="947e8-140">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="947e8-141">Yüklü programların listesini görmek için şu adrese gidin **Denetim Masası** > **programları** > **programlar ve Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="947e8-141">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Yüklü aracı](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="947e8-143">Yükleme Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="947e8-143">Installation options</span></span>
<span data-ttu-id="947e8-144">Komut satırı kullanılabilir tüm seçenekleri görmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="947e8-144">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="947e8-145">Mevcut seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="947e8-145">The available options include:</span></span>

| <span data-ttu-id="947e8-146">Seçenek</span><span class="sxs-lookup"><span data-stu-id="947e8-146">Option</span></span> | <span data-ttu-id="947e8-147">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="947e8-147">Details</span></span> | <span data-ttu-id="947e8-148">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="947e8-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="947e8-149">/q</span><span class="sxs-lookup"><span data-stu-id="947e8-149">/q</span></span> |<span data-ttu-id="947e8-150">Sessiz yükleme</span><span class="sxs-lookup"><span data-stu-id="947e8-150">Quiet installation</span></span> |- |
| <span data-ttu-id="947e8-151">p: "Konum"</span><span class="sxs-lookup"><span data-stu-id="947e8-151">/p:"location"</span></span> |<span data-ttu-id="947e8-152">Azure Backup Aracısı yükleme klasörünün yolu.</span><span class="sxs-lookup"><span data-stu-id="947e8-152">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="947e8-153">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Aracısı</span><span class="sxs-lookup"><span data-stu-id="947e8-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="947e8-154">/ s: "Konum"</span><span class="sxs-lookup"><span data-stu-id="947e8-154">/s:"location"</span></span> |<span data-ttu-id="947e8-155">Azure Backup aracısı için önbellek klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="947e8-155">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="947e8-156">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="947e8-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="947e8-157">/m</span><span class="sxs-lookup"><span data-stu-id="947e8-157">/m</span></span> |<span data-ttu-id="947e8-158">Microsoft Update'e kabulü</span><span class="sxs-lookup"><span data-stu-id="947e8-158">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="947e8-159">/nu</span><span class="sxs-lookup"><span data-stu-id="947e8-159">/nu</span></span> |<span data-ttu-id="947e8-160">Yükleme tamamlandıktan sonra güncelleştirmeleri denetleme</span><span class="sxs-lookup"><span data-stu-id="947e8-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="947e8-161">/d</span><span class="sxs-lookup"><span data-stu-id="947e8-161">/d</span></span> |<span data-ttu-id="947e8-162">Microsoft Azure kurtarma Hizmetleri Aracısı kaldırır</span><span class="sxs-lookup"><span data-stu-id="947e8-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="947e8-163">/ph</span><span class="sxs-lookup"><span data-stu-id="947e8-163">/ph</span></span> |<span data-ttu-id="947e8-164">Proxy konağı adresi</span><span class="sxs-lookup"><span data-stu-id="947e8-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="947e8-165">/PO</span><span class="sxs-lookup"><span data-stu-id="947e8-165">/po</span></span> |<span data-ttu-id="947e8-166">Proxy ana bilgisayar bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="947e8-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="947e8-167">/PU</span><span class="sxs-lookup"><span data-stu-id="947e8-167">/pu</span></span> |<span data-ttu-id="947e8-168">Proxy konağı kullanıcı</span><span class="sxs-lookup"><span data-stu-id="947e8-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="947e8-169">/pw</span><span class="sxs-lookup"><span data-stu-id="947e8-169">/pw</span></span> |<span data-ttu-id="947e8-170">Proxy parolası</span><span class="sxs-lookup"><span data-stu-id="947e8-170">Proxy Password</span></span> |- |

## <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="947e8-171">Azure Backup hizmeti ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="947e8-171">Registering with the Azure Backup service</span></span>
<span data-ttu-id="947e8-172">Azure Backup hizmeti ile kaydedebilmek için emin olmak gereken [Önkoşullar](backup-configure-vault.md) karşılanır.</span><span class="sxs-lookup"><span data-stu-id="947e8-172">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="947e8-173">Yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="947e8-173">You must:</span></span>

* <span data-ttu-id="947e8-174">Geçerli bir Azure aboneliğiniz</span><span class="sxs-lookup"><span data-stu-id="947e8-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="947e8-175">Bir yedekleme kasası sahip</span><span class="sxs-lookup"><span data-stu-id="947e8-175">Have a backup vault</span></span>

<span data-ttu-id="947e8-176">Kasa kimlik bilgilerini indirmek için çalıştırın **Get-AzureRMBackupVaultCredentials** cmdlet'i, uygun bir konumda gibi bir Azure PowerShell konsolunda ve deposu * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="947e8-176">To download the vault credentials, run the **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="947e8-177">Makine kasası ile kaydediliyor yapılır kullanarak [başlangıç OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="947e8-177">Registering the machine with the vault is done using the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration -VaultCredentials $cred -Confirm:$false

CertThumbprint      : 7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName : test-vault
Region              : West US

Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="947e8-178">Kasa kimlik bilgileri dosyası belirtmek için göreli yolların kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="947e8-178">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="947e8-179">Cmdlet'i bir girdi olarak mutlak bir yol sağlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="947e8-179">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="947e8-180">Ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="947e8-180">Networking settings</span></span>
<span data-ttu-id="947e8-181">Windows makine internet bağlantısını bir proxy sunucu üzerinden olduğunda, proxy ayarlarını aracıya de girilebilir.</span><span class="sxs-lookup"><span data-stu-id="947e8-181">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="947e8-182">Bu örnekte, olmadığından hiçbir Ara sunucunun biz açıkça herhangi bir proxy ile ilgili bilgi temizleme.</span><span class="sxs-lookup"><span data-stu-id="947e8-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="947e8-183">Bant genişliği kullanımı seçeneklerle da denetlenebilir ```work hour bandwidth``` ve ```non-work hour bandwidth``` haftanın belirli bir dizi için.</span><span class="sxs-lookup"><span data-stu-id="947e8-183">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="947e8-184">Proxy ve bant ayrıntılarını ayarlama yapılır kullanarak [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="947e8-184">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="947e8-185">Şifreleme ayarları</span><span class="sxs-lookup"><span data-stu-id="947e8-185">Encryption settings</span></span>
<span data-ttu-id="947e8-186">Yedekleme verilerini Azure Backup için gönderilen veri gizliliğini korumak için şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="947e8-186">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="947e8-187">Şifreleme Parolası "geri yükleme sırasındaki verileri şifrelemek için parola" dir.</span><span class="sxs-lookup"><span data-stu-id="947e8-187">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="947e8-188">Ayarlandıktan sonra parola bilgilerini güvenli ve güvenli tutar.</span><span class="sxs-lookup"><span data-stu-id="947e8-188">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="947e8-189">Bu parola Azure kaynağından veri geri olmaz.</span><span class="sxs-lookup"><span data-stu-id="947e8-189">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="947e8-190">Dosya ve klasörleri yedekleme</span><span class="sxs-lookup"><span data-stu-id="947e8-190">Back up files and folders</span></span>
<span data-ttu-id="947e8-191">Tüm Yedeklemelerinizin Windows sunucuları ve istemcileri Azure yedekleme için bir ilke tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="947e8-191">All your backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="947e8-192">İlke üç bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="947e8-192">The policy comprises three parts:</span></span>

1. <span data-ttu-id="947e8-193">A **yedekleme zamanlaması** yedeklemeler alınır ve hizmeti ile eşitlenmiş gerektiğinde belirtir.</span><span class="sxs-lookup"><span data-stu-id="947e8-193">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="947e8-194">A **bekletme zamanlaması** belirleyen ne kadar süreyle Azure kurtarma noktalarını korumak için.</span><span class="sxs-lookup"><span data-stu-id="947e8-194">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="947e8-195">A **dosya ekleme/çıkarma belirtimi** belirleyen ne yedeklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="947e8-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="947e8-196">Yedekleme, otomatikleştirme beri bu belgede, hiçbir şey yapılandırılmış varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="947e8-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="947e8-197">Kullanarak yeni bir yedekleme ilkesi oluşturarak başlayın [yeni OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet'i ve bunu kullanma.</span><span class="sxs-lookup"><span data-stu-id="947e8-197">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="947e8-198">İlke şu anda boş olur ve diğer cmdlet'ler öğeleri tanımlamak için kapsanan veya dışlanan, ne zaman yedeklemeleri çalışacağını ve yedeklemeleri depolanacak burada.</span><span class="sxs-lookup"><span data-stu-id="947e8-198">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="947e8-199">Yedekleme zamanlamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="947e8-199">Configuring the backup schedule</span></span>
<span data-ttu-id="947e8-200">Bir ilke 3 bölümlerinin ilk kullanılarak oluşturulan yedekleme zamanlaması olan [yeni OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="947e8-200">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="947e8-201">Yedekleme zamanlaması yedeklemeleri yapılması gerektiğinde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="947e8-201">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="947e8-202">Bir zamanlama oluştururken 2 giriş parametreleri belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="947e8-202">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="947e8-203">**Haftanın günleri** , yedekleme çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="947e8-203">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="947e8-204">Yedekleme işi yalnızca bir gün veya haftanın her gün veya arasındaki herhangi bir birleşimini çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="947e8-204">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="947e8-205">**Günün kez** yedeklemenin ne zaman çalışmalı.</span><span class="sxs-lookup"><span data-stu-id="947e8-205">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="947e8-206">Yedekleme harekete geçirildiğinde günün en fazla 3 farklı saatleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="947e8-206">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="947e8-207">Örneğin, 4'e her Cumartesi ve Pazar çalışan bir yedekleme ilkesi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="947e8-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="947e8-208">Yedekleme zamanlaması bir ilkesiyle ilişkilendirilmesi gerekir ve bu kullanarak elde [kümesi OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="947e8-208">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="947e8-209">Bir bekletme ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="947e8-209">Configuring a retention policy</span></span>
<span data-ttu-id="947e8-210">Bekletme İlkesi yedekleme işlerini oluşturulan kurtarma noktaları ne kadar süreyle saklanacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="947e8-210">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="947e8-211">Kullanarak yeni bir bekletme ilkesi oluşturulurken [yeni OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, yedekleme kurtarma noktalarının Azure yedekleme ile korunması gereken gün sayısını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="947e8-211">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="947e8-212">Aşağıdaki örnek bir bekletme ilkesi 7 gün olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="947e8-212">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="947e8-213">Bekletme İlkesi cmdlet'ini kullanarak ana ilkesiyle ilişkili olmalıdır [kümesi OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="947e8-213">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="947e8-214">Dahil ve yedeklenecek dosyaları dışlama</span><span class="sxs-lookup"><span data-stu-id="947e8-214">Including and excluding files to be backed up</span></span>
<span data-ttu-id="947e8-215">Bir ```OBFileSpec``` nesnesi bulunan ve bir yedek dışlanan dosyaları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="947e8-215">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="947e8-216">Bu, korumalı dosyaları ve klasörleri bir makinede kullanıma kapsam kurallar kümesidir.</span><span class="sxs-lookup"><span data-stu-id="947e8-216">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="947e8-217">Birçok ekleme veya hariç tutma kuralları gerektiği gibi dosya ve bir ilke ile ilişkilendirmek gibi sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="947e8-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="947e8-218">Yeni bir OBFileSpec nesnesi oluştururken şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="947e8-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="947e8-219">Dosyaları ve dahil edilecek klasörleri belirtin</span><span class="sxs-lookup"><span data-stu-id="947e8-219">Specify the files and folders to be included</span></span>
* <span data-ttu-id="947e8-220">Dosya ve klasörleri dışarıda belirtin</span><span class="sxs-lookup"><span data-stu-id="947e8-220">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="947e8-221">Özyinelemeli bir klasör (veya) olup yalnızca üst düzey dosyaları belirtilen klasöre yedeklenmelidir verilerin yedeğini yukarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="947e8-221">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="947e8-222">İkinci yeni OBFileSpec komutta - özyinelemesiz bayrağı kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="947e8-222">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="947e8-223">Aşağıdaki örnekte, biz birimi yedekleyin C: ve D: ve işletim sistemi ikili dosyaları Windows klasöründeki ve geçici klasörleri dışarıda.</span><span class="sxs-lookup"><span data-stu-id="947e8-223">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="947e8-224">Oluşturacağız Bunu yapmak için iki belirtimleri kullanarak dosya [yeni OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - eklenmesi, diğeri dışarıda bırakma için.</span><span class="sxs-lookup"><span data-stu-id="947e8-224">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="947e8-225">Dosya belirtimleri oluşturduktan sonra ilkeyi kullanarak ilişkili oldukları [Ekle OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="947e8-225">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-the-policy"></a><span data-ttu-id="947e8-226">İlke uygulama</span><span class="sxs-lookup"><span data-stu-id="947e8-226">Applying the policy</span></span>
<span data-ttu-id="947e8-227">Şimdi İlkesi tamamlandıktan ve ilişkili bir yedekleme zamanlaması, bekletme ilkesi ve dosyaların bir ekleme/çıkarma listesi vardır.</span><span class="sxs-lookup"><span data-stu-id="947e8-227">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="947e8-228">Bu ilkeyi şimdi kullanmak Azure Backup için kaydedilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="947e8-228">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="947e8-229">Yeni oluşturulan İlkesi, uygulamadan önce mevcut hiçbir yedekleme ilkeleri kullanılarak sunucu ile ilişkilendirilen olduğundan emin olun [Kaldır OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="947e8-229">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="947e8-230">İlkeyi kaldırmayı onay ister.</span><span class="sxs-lookup"><span data-stu-id="947e8-230">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="947e8-231">Onay Kullan'ı atlamanızı ```-Confirm:$false``` bayrağı cmdlet ile.</span><span class="sxs-lookup"><span data-stu-id="947e8-231">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="947e8-232">İlke nesnesi yürüten yapılır kullanarak [kümesi OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="947e8-232">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="947e8-233">Bu ayrıca onaylamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="947e8-233">This will also ask for confirmation.</span></span> <span data-ttu-id="947e8-234">Onay Kullan'ı atlamanızı ```-Confirm:$false``` bayrağı cmdlet ile.</span><span class="sxs-lookup"><span data-stu-id="947e8-234">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want to save this backup policy ? [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

<span data-ttu-id="947e8-235">Kullanarak varolan yedekleme ilkesi ayrıntılarını görüntüleyebilirsiniz [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="947e8-235">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="947e8-236">Kullanarak daha fazla ayrıntıya [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet'i için yedekleme zamanlamasını ve [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) bekletme ilkeleri için cmdlet</span><span class="sxs-lookup"><span data-stu-id="947e8-236">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="947e8-237">Bir geçici yedekleme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="947e8-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="947e8-238">Bir yedekleme İlkesi ayarladıktan sonra yedeklemeler zamanlama meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="947e8-238">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="947e8-239">Bir geçici yedekleme tetikleme olduğunu da olası kullanarak [başlangıç OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="947e8-239">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="947e8-240">Verileri Azure yedekten geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="947e8-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="947e8-241">Bu bölümde, veri kurtarma Azure Backup otomatikleştirmek için adımlarda size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="947e8-241">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="947e8-242">Bunun yapılması, aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="947e8-242">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="947e8-243">Kaynak birim seçin</span><span class="sxs-lookup"><span data-stu-id="947e8-243">Pick the source volume</span></span>
2. <span data-ttu-id="947e8-244">Geri yüklemek için bir yedekleme noktası seçin</span><span class="sxs-lookup"><span data-stu-id="947e8-244">Choose a backup point to restore</span></span>
3. <span data-ttu-id="947e8-245">Geri yüklemek için bir öğe seçin</span><span class="sxs-lookup"><span data-stu-id="947e8-245">Choose an item to restore</span></span>
4. <span data-ttu-id="947e8-246">Tetikleyici geri yükleme işlemi</span><span class="sxs-lookup"><span data-stu-id="947e8-246">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="947e8-247">Kaynak birim çekme</span><span class="sxs-lookup"><span data-stu-id="947e8-247">Picking the source volume</span></span>
<span data-ttu-id="947e8-248">Bir öğeyi Azure yedeklemeden geri yüklemek için ilk öğenin kaynağını tanımlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="947e8-248">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="947e8-249">Biz Windows Server veya Windows İstemcisi bağlamında komutları yürütülürken bu yana makine zaten tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="947e8-249">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="947e8-250">Kaynağı tanımlayan bir sonraki adım, onu içeren birim belirlemektir.</span><span class="sxs-lookup"><span data-stu-id="947e8-250">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="947e8-251">Bu makineden yedeklenen alınabilir yürüterek kaynakları veya birimlerin listesini [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="947e8-251">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="947e8-252">Bu komut, bu sunucu/istemciden yedeklenen tüm kaynakları bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="947e8-252">This command returns an array of all the sources backed up from this server/client.</span></span>

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-to-restore"></a><span data-ttu-id="947e8-253">Geri yüklemek için bir yedekleme noktasının seçme</span><span class="sxs-lookup"><span data-stu-id="947e8-253">Choosing a backup point to restore</span></span>
<span data-ttu-id="947e8-254">Yedekleme noktaları listesi yürüterek alınabilir [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) uygun parametreleri cmdlet'iyle.</span><span class="sxs-lookup"><span data-stu-id="947e8-254">The list of backup points can be retrieved by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="947e8-255">Bizim örneğimizde, en son yedekleme noktası kaynak birimin seçeceğiz *D:* ve belirli bir dosya kurtarmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="947e8-255">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
<span data-ttu-id="947e8-256">Nesne ```$rps``` yedekleme noktaları dizisidir.</span><span class="sxs-lookup"><span data-stu-id="947e8-256">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="947e8-257">En son noktası ilk öğedir ve eski noktası n. öğedir.</span><span class="sxs-lookup"><span data-stu-id="947e8-257">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="947e8-258">En son noktası seçmek için kullanacağız ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="947e8-258">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="947e8-259">Geri yüklemek için bir öğe seçme</span><span class="sxs-lookup"><span data-stu-id="947e8-259">Choosing an item to restore</span></span>
<span data-ttu-id="947e8-260">Tam dosya ya da geri yüklemek için yinelemeli kullanım klasörü tanımlamak için [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="947e8-260">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="947e8-261">Klasör hiyerarşisi göz atabilirsiniz yalnızca kullanarak bu şekilde ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="947e8-261">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="947e8-262">Biz dosyayı geri yüklemek istiyorsanız, bu örnekte, *finances.xls* biz nesne kullanan başvurabilir ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="947e8-262">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

<span data-ttu-id="947e8-263">Kullanarak geri yüklemek öğeler için arama yapabilirsiniz ```Get-OBRecoverableItem``` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="947e8-263">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="947e8-264">Aranacak örneğimizde *finances.xls* biz şu komutu çalıştırarak dosyayı bir tanıtıcı alabilir:</span><span class="sxs-lookup"><span data-stu-id="947e8-264">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="947e8-265">Geri yükleme işlemini tetikler</span><span class="sxs-lookup"><span data-stu-id="947e8-265">Triggering the restore process</span></span>
<span data-ttu-id="947e8-266">Geri yükleme işlemi tetiklemek için öncelikle kurtarma seçeneklerini belirtmek ihtiyacımız.</span><span class="sxs-lookup"><span data-stu-id="947e8-266">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="947e8-267">Bu kullanılarak yapılabilir [yeni OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="947e8-267">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="947e8-268">Bu örnek için dosyaları geri yüklemek istiyoruz varsayalım *C:\temp*.</span><span class="sxs-lookup"><span data-stu-id="947e8-268">For this example, let's assume that we want to restore the files to *C:\temp*.</span></span> <span data-ttu-id="947e8-269">Ayrıca hedef klasörde zaten mevcut dosyaların atlamak istiyoruz varsayalım *C:\temp*.</span><span class="sxs-lookup"><span data-stu-id="947e8-269">Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*.</span></span> <span data-ttu-id="947e8-270">Bu tür bir kurtarma seçeneğini oluşturmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="947e8-270">To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="947e8-271">Şimdi kullanarak geri yüklemeyi tetikleyecek [başlangıç OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) seçilen komutu ```$item``` çıktısından ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="947e8-271">Now trigger restore by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="947e8-272">Azure Backup aracısını kaldırma</span><span class="sxs-lookup"><span data-stu-id="947e8-272">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="947e8-273">Azure Backup aracısını kaldırma, aşağıdaki komutu kullanarak gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="947e8-273">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="947e8-274">Aracısı ikili dosyalarının makineden kaldırma dikkate alınması gereken bazı sonuçları vardır:</span><span class="sxs-lookup"><span data-stu-id="947e8-274">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="947e8-275">Dosya Filtresi makineden kaldırır ve değişiklikleri izleme durduruldu.</span><span class="sxs-lookup"><span data-stu-id="947e8-275">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="947e8-276">Tüm ilke bilgilerine makineden kaldırıldı, ancak hizmetinde depolanması ilke bilgilerini sürdürür.</span><span class="sxs-lookup"><span data-stu-id="947e8-276">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="947e8-277">Tüm yedekleme zamanlamaları kaldırılır ve daha fazla yedekleme alınır.</span><span class="sxs-lookup"><span data-stu-id="947e8-277">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="947e8-278">Ancak, verileri Azure kalırken depolanır ve bekletme ilkesi Kurulum göredir, tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="947e8-278">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="947e8-279">Eski noktalarını otomatik olarak eski.</span><span class="sxs-lookup"><span data-stu-id="947e8-279">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="947e8-280">Uzaktan Yönetim</span><span class="sxs-lookup"><span data-stu-id="947e8-280">Remote management</span></span>
<span data-ttu-id="947e8-281">Azure Yedekleme aracısı, ilkeler ve veri kaynakları çevresinde tüm yönetim uzaktan PowerShell aracılığıyla gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="947e8-281">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="947e8-282">Uzaktan yönetilecek makine doğru hazırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="947e8-282">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="947e8-283">Varsayılan olarak, WinRM hizmeti el ile başlatma için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="947e8-283">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="947e8-284">Başlangıç türünü ayarlamak *otomatik* ve hizmetin başlatılması.</span><span class="sxs-lookup"><span data-stu-id="947e8-284">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="947e8-285">WinRM hizmetinin çalıştığından emin olun, durum özelliğinin değeri olmalıdır *çalıştıran*.</span><span class="sxs-lookup"><span data-stu-id="947e8-285">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="947e8-286">PowerShell uzaktan iletişim için yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="947e8-286">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="947e8-287">Makine artık uzaktan - aracı yüklemesinden başlatma yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="947e8-287">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="947e8-288">Örneğin, aşağıdaki komut dosyası Aracısı uzak makineye kopyalar ve onu yükler.</span><span class="sxs-lookup"><span data-stu-id="947e8-288">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="947e8-289">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="947e8-289">Next steps</span></span>
<span data-ttu-id="947e8-290">Azure yedekleme için Windows Server/istemcisi bakın hakkında daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="947e8-290">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="947e8-291">Azure Backup'a giriş</span><span class="sxs-lookup"><span data-stu-id="947e8-291">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="947e8-292">Windows sunucularını yedekleme</span><span class="sxs-lookup"><span data-stu-id="947e8-292">Back up Windows Servers</span></span>](backup-configure-vault.md)
