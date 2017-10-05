---
title: "Azure Backup - DPM iş yüklerini yedeklemeye kullanım PowerShell | Microsoft Docs"
description: "Dağıtma ve Data Protection Manager (PowerShell kullanarak DPM için) Azure Backup yönetme hakkında bilgi edinin"
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 2e3b4a094511a59cfa02917efc2e3e053840af0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="42b99-103">PowerShell kullanarak Data Protection Manager (DPM) sunucuları için Azure’a yedekleme dağıtma ve yönetme</span><span class="sxs-lookup"><span data-stu-id="42b99-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="42b99-104">ARM</span><span class="sxs-lookup"><span data-stu-id="42b99-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="42b99-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="42b99-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="42b99-106">Bu makalede, bir DPM sunucusunda Azure yedekleme kurulumu için PowerShell kullanın ve yedekleme ve kurtarma yönetmek için nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="42b99-106">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span></span>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="42b99-107">PowerShell ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="42b99-107">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="42b99-108">Yedeklemeler için Azure Data Protection Manager'dan yönetmek için PowerShell kullanmadan önce PowerShell'de sağ ortama sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="42b99-108">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you need to have the right environment in PowerShell.</span></span> <span data-ttu-id="42b99-109">PowerShell oturumu başlangıcında sağ modülleri alın ve doğru DPM cmdlet başvuru izin vermek için aşağıdaki komutu çalıştırdığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="42b99-109">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="42b99-110">Kurulumu'nu ve kaydı</span><span class="sxs-lookup"><span data-stu-id="42b99-110">Setup and Registration</span></span>
<span data-ttu-id="42b99-111">Başlamak için:</span><span class="sxs-lookup"><span data-stu-id="42b99-111">To begin:</span></span>

1. <span data-ttu-id="42b99-112">[En son PowerShell indirme](https://github.com/Azure/azure-powershell/releases) (gerekli minimum sürüm: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="42b99-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="42b99-113">Azure Backup cmdlet'leri geçerek etkinleştirmek *AzureResourceManager* kullanarak moduna **Switch-AzureMode** komutunu:</span><span class="sxs-lookup"><span data-stu-id="42b99-113">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="42b99-114">Aşağıdaki kurulumunu ve kaydını görevleri PowerShell ile otomatik olarak yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="42b99-114">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="42b99-115">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="42b99-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="42b99-116">Azure Backup aracısını yükleme</span><span class="sxs-lookup"><span data-stu-id="42b99-116">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="42b99-117">Azure Backup hizmeti ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="42b99-117">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="42b99-118">Ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="42b99-118">Networking settings</span></span>
* <span data-ttu-id="42b99-119">Şifreleme ayarları</span><span class="sxs-lookup"><span data-stu-id="42b99-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="42b99-120">Kurtarma hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="42b99-120">Create a recovery services vault</span></span>
<span data-ttu-id="42b99-121">Aşağıdaki adımlar bir kurtarma Hizmetleri kasası oluşturmada size yol açar.</span><span class="sxs-lookup"><span data-stu-id="42b99-121">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="42b99-122">Kurtarma Hizmetleri kasasına yedekleme Kasası ' farklıdır.</span><span class="sxs-lookup"><span data-stu-id="42b99-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="42b99-123">Azure Backup ilk kez kullanıyorsanız, kullanmalısınız **Register-AzureRMResourceProvider** aboneliğinizle Azure Recovery hizmeti sağlayıcısını kaydetmek için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="42b99-123">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="42b99-124">Kurtarma Hizmetleri kasası bir ARM kaynak olduğundan, bir kaynak grubu içindeki yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="42b99-124">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="42b99-125">Varolan bir kaynak grubunu kullanın veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="42b99-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="42b99-126">Yeni bir kaynak grubu oluştururken, ad ve kaynak grubu için konum belirtin.</span><span class="sxs-lookup"><span data-stu-id="42b99-126">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="42b99-127">Kullanım **yeni AzureRmRecoveryServicesVault** cmdlet yeni bir kasa oluşturun.</span><span class="sxs-lookup"><span data-stu-id="42b99-127">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create a new vault.</span></span> <span data-ttu-id="42b99-128">Kaynak grubu için kullanılan kasa için aynı konumu belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="42b99-128">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="42b99-129">Kullanılacak depolama artıklığı türünü belirtin; kullanabileceğiniz [yerel olarak yedekli depolama (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) veya [coğrafi olarak yedekli depolama (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="42b99-129">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="42b99-130">Aşağıdaki örnek, testVault - BackupStorageRedundancy seçeneği GeoRedundant için ayarlanmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="42b99-130">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="42b99-131">Çok sayıda Azure yedekleme cmdlet'lerini girdi olarak kurtarma Hizmetleri kasası nesnesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="42b99-131">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="42b99-132">Bu nedenle, bir değişkende yedekleme kurtarma Hizmetleri kasası nesne depolamak uygundur.</span><span class="sxs-lookup"><span data-stu-id="42b99-132">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="42b99-133">Bir abonelikte kasalarını görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="42b99-133">View the vaults in a subscription</span></span>
<span data-ttu-id="42b99-134">Kullanım **Get-AzureRmRecoveryServicesVault** geçerli abonelikte tüm kasalarının listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="42b99-134">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="42b99-135">Bu komut, yeni bir kasa oluşturulduğunu denetleyin veya hangi kasalarını abonelikte bulunan görmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="42b99-135">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="42b99-136">Get-AzureRmRecoveryServicesVault komutunu çalıştırın ve Abonelikteki tüm kasalarını listelenir.</span><span class="sxs-lookup"><span data-stu-id="42b99-136">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="42b99-137">Bir DPM sunucusu üzerinde Azure Backup aracısını yükleme</span><span class="sxs-lookup"><span data-stu-id="42b99-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="42b99-138">Azure Backup aracısını yüklemeden önce Windows Server yükleyici indirildi ve mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="42b99-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="42b99-139">Yükleyicisi'nden en son sürümünü almak [Microsoft Download Center](http://aka.ms/azurebackup_agent) veya kurtarma Hizmetleri Kasası'nın Pano sayfası.</span><span class="sxs-lookup"><span data-stu-id="42b99-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="42b99-140">Yükleyici gibi kolay erişilebilir bir konuma kaydedin * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="42b99-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="42b99-141">Aracıyı yüklemek için yükseltilmiş bir PowerShell konsolunda aşağıdaki komutu çalıştırın **DPM sunucusundaki**:</span><span class="sxs-lookup"><span data-stu-id="42b99-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="42b99-142">Bu, tüm varsayılan seçeneklerle Aracısı'nı yükler.</span><span class="sxs-lookup"><span data-stu-id="42b99-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="42b99-143">Yükleme arka planda birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="42b99-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="42b99-144">Belirtmezseniz, */nu* seçeneği **Windows Update** tüm güncelleştirmeleri denetlemek için yükleme işleminin sonunda penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="42b99-144">If you do not specify the */nu* option the **Windows Update** window opens at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="42b99-145">Aracı yüklü programlar listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="42b99-145">The agent shows up in the list of installed programs.</span></span> <span data-ttu-id="42b99-146">Yüklü programların listesini görmek için şu adrese gidin **Denetim Masası** > **programları** > **programlar ve Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="42b99-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Yüklü aracı](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="42b99-148">Yükleme Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="42b99-148">Installation options</span></span>
<span data-ttu-id="42b99-149">Komut satırı kullanılabilir tüm seçenekleri görmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="42b99-149">To see all the options available via the commandline, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="42b99-150">Mevcut seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="42b99-150">The available options include:</span></span>

| <span data-ttu-id="42b99-151">Seçenek</span><span class="sxs-lookup"><span data-stu-id="42b99-151">Option</span></span> | <span data-ttu-id="42b99-152">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="42b99-152">Details</span></span> | <span data-ttu-id="42b99-153">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="42b99-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="42b99-154">/q</span><span class="sxs-lookup"><span data-stu-id="42b99-154">/q</span></span> |<span data-ttu-id="42b99-155">Sessiz yükleme</span><span class="sxs-lookup"><span data-stu-id="42b99-155">Quiet installation</span></span> |- |
| <span data-ttu-id="42b99-156">p: "Konum"</span><span class="sxs-lookup"><span data-stu-id="42b99-156">/p:"location"</span></span> |<span data-ttu-id="42b99-157">Azure Backup Aracısı yükleme klasörünün yolu.</span><span class="sxs-lookup"><span data-stu-id="42b99-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="42b99-158">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Aracısı</span><span class="sxs-lookup"><span data-stu-id="42b99-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="42b99-159">/ s: "Konum"</span><span class="sxs-lookup"><span data-stu-id="42b99-159">/s:"location"</span></span> |<span data-ttu-id="42b99-160">Azure Backup aracısı için önbellek klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="42b99-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="42b99-161">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="42b99-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="42b99-162">/m</span><span class="sxs-lookup"><span data-stu-id="42b99-162">/m</span></span> |<span data-ttu-id="42b99-163">Microsoft Update'e kabulü</span><span class="sxs-lookup"><span data-stu-id="42b99-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="42b99-164">/nu</span><span class="sxs-lookup"><span data-stu-id="42b99-164">/nu</span></span> |<span data-ttu-id="42b99-165">Yükleme tamamlandıktan sonra güncelleştirmeleri denetleme</span><span class="sxs-lookup"><span data-stu-id="42b99-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="42b99-166">/d</span><span class="sxs-lookup"><span data-stu-id="42b99-166">/d</span></span> |<span data-ttu-id="42b99-167">Microsoft Azure kurtarma Hizmetleri Aracısı kaldırır</span><span class="sxs-lookup"><span data-stu-id="42b99-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="42b99-168">/ph</span><span class="sxs-lookup"><span data-stu-id="42b99-168">/ph</span></span> |<span data-ttu-id="42b99-169">Proxy konağı adresi</span><span class="sxs-lookup"><span data-stu-id="42b99-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="42b99-170">/PO</span><span class="sxs-lookup"><span data-stu-id="42b99-170">/po</span></span> |<span data-ttu-id="42b99-171">Proxy ana bilgisayar bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="42b99-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="42b99-172">/PU</span><span class="sxs-lookup"><span data-stu-id="42b99-172">/pu</span></span> |<span data-ttu-id="42b99-173">Proxy konağı kullanıcı</span><span class="sxs-lookup"><span data-stu-id="42b99-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="42b99-174">/pw</span><span class="sxs-lookup"><span data-stu-id="42b99-174">/pw</span></span> |<span data-ttu-id="42b99-175">Proxy parolası</span><span class="sxs-lookup"><span data-stu-id="42b99-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-to-a-recovery-services-vault"></a><span data-ttu-id="42b99-176">Kasa kayıt DPM bir kurtarma Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="42b99-176">Registering DPM to a Recovery Services Vault</span></span>
<span data-ttu-id="42b99-177">Kurtarma Hizmetleri kasası oluşturduktan sonra en son aracı ve kasa kimlik bilgilerini indirin ve C:\Downloads gibi uygun bir konumda saklayın.</span><span class="sxs-lookup"><span data-stu-id="42b99-177">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="42b99-178">DPM sunucusunda çalıştırın [başlangıç OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) makine kasaya kaydetmek için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="42b99-178">On the DPM server, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="42b99-179">İlk yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="42b99-179">Initial configuration settings</span></span>
<span data-ttu-id="42b99-180">DPM sunucusu kurtarma Hizmetleri kasası ile kaydedildiğinde, varsayılan abonelik ayarlarını başlatır.</span><span class="sxs-lookup"><span data-stu-id="42b99-180">Once the DPM Server is registered with the Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="42b99-181">Bu abonelik ayarlar, ağ, şifreleme ve hazırlama alanı içerir.</span><span class="sxs-lookup"><span data-stu-id="42b99-181">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="42b99-182">Önce bir tanıtıcı kullanarak mevcut (varsayılan) ayarları almanız abonelik ayarlarını değiştirmek için [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="42b99-182">To change subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="42b99-183">Bu yerel PowerShell nesneye yapılan değişikliklerden ```$setting``` ve ardından tam nesne DPM ve bunları kaydetmek için Azure Backup için kararlıdır kullanarak [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-183">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="42b99-184">Kullanmanız gereken ```–Commit``` değişiklikler kalıcı emin olmak için bayrak.</span><span class="sxs-lookup"><span data-stu-id="42b99-184">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="42b99-185">Ayarları değil uygulanan ve olması kaydedilen sürece Azure yedekleme tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="42b99-185">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="42b99-186">Ağ</span><span class="sxs-lookup"><span data-stu-id="42b99-186">Networking</span></span>
<span data-ttu-id="42b99-187">Azure Backup hizmeti internet üzerindeki DPM makineye bağlantısını bir proxy sunucu üzerinden ise, Ara sunucu ayarlarını başarılı yedeklemeler için sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="42b99-187">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="42b99-188">Bu kullanılarak yapılır ```-ProxyServer```ve ```-ProxyPort```, ```-ProxyUsername``` ve ```ProxyPassword``` parametrelerle [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-188">This is done by using the ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="42b99-189">Bu örnekte, olmadığından hiçbir Ara sunucunun biz açıkça herhangi bir proxy ile ilgili bilgi temizleme.</span><span class="sxs-lookup"><span data-stu-id="42b99-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="42b99-190">Bant genişliği kullanımı ile seçenekleri de denetlenebilir ```-WorkHourBandwidth``` ve ```-NonWorkHourBandwidth``` haftanın belirli bir dizi için.</span><span class="sxs-lookup"><span data-stu-id="42b99-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="42b99-191">Bu örnekte, biz herhangi azaltma ayarlıyorsanız değil.</span><span class="sxs-lookup"><span data-stu-id="42b99-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-the-staging-area"></a><span data-ttu-id="42b99-192">Hazırlama alanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="42b99-192">Configuring the staging Area</span></span>
<span data-ttu-id="42b99-193">DPM sunucusunda çalışan Azure Yedekleme aracısı, (yerel hazırlama alanı) buluttan geri yüklenen veriler için geçici depolama gerekir.</span><span class="sxs-lookup"><span data-stu-id="42b99-193">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="42b99-194">Hazırlama alanı kullanarak yapılandırma [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i ve ```-StagingAreaPath``` parametresi.</span><span class="sxs-lookup"><span data-stu-id="42b99-194">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="42b99-195">Yukarıdaki örnekte, hazırlama alanı ayarlanacak *C:\StagingArea* PowerShell nesnesindeki ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="42b99-195">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="42b99-196">Belirtilen klasör zaten var, aksi takdirde Abonelik ayarları son yürütme başarısız olur emin olun.</span><span class="sxs-lookup"><span data-stu-id="42b99-196">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="42b99-197">Şifreleme ayarları</span><span class="sxs-lookup"><span data-stu-id="42b99-197">Encryption settings</span></span>
<span data-ttu-id="42b99-198">Yedekleme verilerini Azure Backup için gönderilen veri gizliliğini korumak için şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="42b99-198">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="42b99-199">Şifreleme Parolası "geri yükleme sırasındaki verileri şifrelemek için parola" dir.</span><span class="sxs-lookup"><span data-stu-id="42b99-199">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="42b99-200">Ayarlandıktan sonra bu bilgileri güvenli tutmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="42b99-200">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="42b99-201">Aşağıdaki örnekte, ilk komut dizesini sayıya dönüştürür ```passphrase123456789``` güvenli bir dize ve güvenli dize değişkenine adlı atar ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="42b99-201">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="42b99-202">İkinci komut güvenli dize ayarlar ```$Passphrase``` yedeklemeleri şifrelemek için parolayı olarak.</span><span class="sxs-lookup"><span data-stu-id="42b99-202">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="42b99-203">Ayarlandıktan sonra parola bilgilerini güvenli ve güvenli tutar.</span><span class="sxs-lookup"><span data-stu-id="42b99-203">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="42b99-204">Bu parola Azure kaynağından veri geri olmaz.</span><span class="sxs-lookup"><span data-stu-id="42b99-204">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="42b99-205">Bu noktada, tüm gerekli değişiklikleri yaptınız ```$setting``` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="42b99-205">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="42b99-206">Değişiklikleri kaydetmek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="42b99-206">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="42b99-207">Azure yedekleme verilerini koruma</span><span class="sxs-lookup"><span data-stu-id="42b99-207">Protect data to Azure Backup</span></span>
<span data-ttu-id="42b99-208">Bu bölümde, bir üretim sunucusunu DPM sunucusuna Ekle ve ardından yerel DPM depolama ve ardından Azure yedekleme verileri koruyun.</span><span class="sxs-lookup"><span data-stu-id="42b99-208">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="42b99-209">Örneklerde, dosyaları ve klasörleri yedeklemek göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="42b99-209">In the examples, we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="42b99-210">Mantığı, herhangi bir DPM desteklenen veri kaynağı yedeklemek için kolayca genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="42b99-210">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="42b99-211">Tüm DPM yedeklemelerini dört bölümden ile koruma grubu (PG) tarafından yönetilir:</span><span class="sxs-lookup"><span data-stu-id="42b99-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="42b99-212">**Grup üyeleri** korunabilir tüm nesnelerin bir listesi verilmiştir (olarak da bilinen *veri kaynakları* dpm'de) aynı koruma grubunda korumak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="42b99-212">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="42b99-213">Örneğin, farklı yedekleme gereksinimleri olabilir olarak üretim sanal makineleri bir koruma grubu ve SQL Server veritabanlarını başka bir koruma grubunda korumak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="42b99-213">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="42b99-214">Herhangi bir veri kaynağı emin olmak için gereken bir üretim sunucusunda yedeklenmeden önce DPM aracısını sunucuda yüklü ve DPM tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="42b99-214">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="42b99-215">Adımları için [DPM aracısını yüklemeye](https://technet.microsoft.com/library/bb870935.aspx) ve uygun DPM sunucusuna bağlama.</span><span class="sxs-lookup"><span data-stu-id="42b99-215">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="42b99-216">**Veri koruma yöntemini** hedef yedekleme konumları - bant, disk ve bulut belirtir.</span><span class="sxs-lookup"><span data-stu-id="42b99-216">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="42b99-217">Bizim örneğimizde biz verileri yerel diske ve bulut için koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="42b99-217">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="42b99-218">A **yedekleme zamanlaması** yedeklemeler yapılması gerektiğinde ve verileri DPM sunucusu ve üretim sunucusu arasında ne sıklıkla eşitlenmesi gerektiği belirtir.</span><span class="sxs-lookup"><span data-stu-id="42b99-218">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="42b99-219">A **bekletme zamanlaması** belirleyen ne kadar süreyle Azure kurtarma noktalarını korumak için.</span><span class="sxs-lookup"><span data-stu-id="42b99-219">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="42b99-220">Koruma grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="42b99-220">Creating a protection group</span></span>
<span data-ttu-id="42b99-221">Başlangıç kullanarak yeni bir koruma grubu oluşturarak [yeni DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-221">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="42b99-222">Yukarıdaki cmdlet adlı bir koruma grubu oluşturacak *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="42b99-222">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="42b99-223">Mevcut bir koruma grubunun de daha sonra Azure bulut yedekleme eklemek için değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="42b99-223">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="42b99-224">Ancak, koruma grubuna - herhangi bir değişiklik yapmak için yeni veya varolan - bir tanıtıcı almaya ihtiyacımız bir *değiştirilebilir* kullanarak nesne [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-224">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="42b99-225">Grup üyeleri koruma grubuna ekleniyor</span><span class="sxs-lookup"><span data-stu-id="42b99-225">Adding group members to the Protection Group</span></span>
<span data-ttu-id="42b99-226">Her DPM aracısının yüklü olduğu sunucuda veri kaynakları listesi bilir.</span><span class="sxs-lookup"><span data-stu-id="42b99-226">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="42b99-227">Bir veri kaynağını koruma grubuna eklemek için DPM Aracısı önce veri kaynaklarının listesini DPM sunucusuna geri göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="42b99-227">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="42b99-228">Bir veya daha fazla veri kaynakları sonra seçili ve koruma grubuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="42b99-228">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="42b99-229">Bunu başarmak için gerekli olan PowerShell adımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="42b99-229">The PowerShell steps needed to achieve this are:</span></span>

1. <span data-ttu-id="42b99-230">DPM Aracısı üzerinden DPM tarafından yönetilen tüm sunucuların listesi getirilemedi.</span><span class="sxs-lookup"><span data-stu-id="42b99-230">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="42b99-231">Belirli bir sunucu seçin.</span><span class="sxs-lookup"><span data-stu-id="42b99-231">Choose a specific server.</span></span>
3. <span data-ttu-id="42b99-232">Tüm veri kaynakları listesini sunucuda getirin.</span><span class="sxs-lookup"><span data-stu-id="42b99-232">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="42b99-233">Bir veya daha fazla veri kaynakları seçin ve bunları koruma grubuna Ekle</span><span class="sxs-lookup"><span data-stu-id="42b99-233">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="42b99-234">DPM aracısının yüklü olduğundan ve DPM sunucusu tarafından yönetilen sunucuları listesi ile edinilen [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-234">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="42b99-235">Biz filtrelemek ve yalnızca PS adıyla yapılandırın, bu örnekte *productionserver01* yedekleme için.</span><span class="sxs-lookup"><span data-stu-id="42b99-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="42b99-236">Şimdi üzerinde veri kaynaklarının listesini getirme ```$server``` kullanarak [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-236">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="42b99-237">Bu örnekte şu birim için filtre * D:\* biz yedekleme için yapılandırmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="42b99-237">In this example we are filtering for the volume *D:\* that we want to configure for backup.</span></span> <span data-ttu-id="42b99-238">Bu veri kaynağı sonra koruma grubuna eklenen kullanarak [Ekle DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-238">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="42b99-239">Kullanmayı unutmayın *değiştirilebilir* koruma grubu nesnesi ```$MPG``` eklemeleri yapma.</span><span class="sxs-lookup"><span data-stu-id="42b99-239">Remember to use the *modifiable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="42b99-240">Tüm seçilen veri kaynakları koruma grubuna ekleyene kadar gerektiği gibi birçok kez bu adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="42b99-240">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="42b99-241">Yalnızca bir datasource ile başlatın ve koruma grubunu oluşturmak için iş akışı tamamlamak ve sonraki bir noktada daha fazla veri kaynakları koruma grubuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="42b99-241">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="42b99-242">Veri koruma yöntemini seçme</span><span class="sxs-lookup"><span data-stu-id="42b99-242">Selecting the data protection method</span></span>
<span data-ttu-id="42b99-243">Veri kaynakları koruma grubuna eklendikten sonra sonraki adım koruma yöntemini kullanarak belirtmektir [kümesi DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-243">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="42b99-244">Bu örnekte, kurulumu yerel disk ve bulut yedekleme için koruma grubudur.</span><span class="sxs-lookup"><span data-stu-id="42b99-244">In this example, the Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="42b99-245">Ayrıca kullanarak buluta korumak istediğiniz veri kaynağını belirtmek zorunda [Ekle DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet'iyle - çevrimiçi bayrağı.</span><span class="sxs-lookup"><span data-stu-id="42b99-245">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="42b99-246">Bekletme aralığını ayarlama</span><span class="sxs-lookup"><span data-stu-id="42b99-246">Setting the retention range</span></span>
<span data-ttu-id="42b99-247">Kullanarak yedekleme noktaları için bekletme ayarlamak [kümesi DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-247">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="42b99-248">Kullanarak yedekleme zamanlaması tanımlanmış önce bekletme ayarlamak tek görünebilir ancak ```Set-DPMPolicyObjective``` cmdlet'i sonra değiştirilebilen varsayılan yedekleme zamanlaması otomatik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="42b99-248">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="42b99-249">Yedeklemeyi zamanlama ilk kümesi ve sonra bekletme ilkesi için her zaman mümkündür.</span><span class="sxs-lookup"><span data-stu-id="42b99-249">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="42b99-250">Aşağıdaki örnek cmdlet disk yedeklemeleri bekletme parametreleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="42b99-250">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="42b99-251">Bu yedeklemeler 10 gün ve eşitleme verileri için 6 saatte bir ve üretim sunucusu DPM sunucusu arasında korur.</span><span class="sxs-lookup"><span data-stu-id="42b99-251">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="42b99-252">```SynchronizationFrequencyMinutes``` Ne sıklıkta bir yedekleme noktasının, ancak nasıl oluşturulduğunu tanımlamıyor genellikle verileri DPM sunucusuna kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="42b99-252">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server.</span></span>  <span data-ttu-id="42b99-253">Bu ayar, yedeklemeler çok büyük hale gelmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="42b99-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="42b99-254">Azure'a giden yedeklemeler için (DPM başvuruyor onlara çevrimiçi yedeklemeler) için bekletme aralıkları yapılandırılabilir [üst öğe Son şeması (GFS) kullanarak bekletme'uzun süreli](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="42b99-254">For backups going to Azure (DPM refers to them as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="42b99-255">Diğer bir deyişle, günlük, haftalık, aylık ve yıllık bekletme ilkeleri içeren bir birleşik bekletme ilkesi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="42b99-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="42b99-256">Bu örnekte, biz istiyoruz karmaşık bekletme düzeni temsil eden bir dizi oluşturmak ve bekletme aralığı kullanarak yapılandırma [kümesi DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-256">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="42b99-257">Yedekleme zamanlamasını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="42b99-257">Set the backup schedule</span></span>
<span data-ttu-id="42b99-258">Koruma hedefi kullanarak belirtirseniz, DPM bir varsayılan yedekleme zamanlaması otomatik olarak ayarlar. ```Set-DPMPolicyObjective``` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-258">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="42b99-259">Varsayılan zamanlamaların değiştirmek için kullanın [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet arkasından [kümesi DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-259">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="42b99-260">Yukarıdaki örnekte, ```$onlineSch``` GFS düzeni koruma grubunda varolan çevrimiçi koruma zamanlamasını içeren bir dizi dört öğelerle:</span><span class="sxs-lookup"><span data-stu-id="42b99-260">In the above example, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="42b99-261">```$onlineSch[0]```Günlük Zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="42b99-261">```$onlineSch[0]``` contains the daily schedule</span></span>
2. <span data-ttu-id="42b99-262">```$onlineSch[1]```Haftalık Zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="42b99-262">```$onlineSch[1]``` contains the weekly schedule</span></span>
3. <span data-ttu-id="42b99-263">```$onlineSch[2]```Aylık zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="42b99-263">```$onlineSch[2]``` contains the monthly schedule</span></span>
4. <span data-ttu-id="42b99-264">```$onlineSch[3]```Yıllık çizelge içerir</span><span class="sxs-lookup"><span data-stu-id="42b99-264">```$onlineSch[3]``` contains the yearly schedule</span></span>

<span data-ttu-id="42b99-265">Haftalık Zamanlama değiştirmeniz gerekiyorsa, başvurmanız gerekir böylece ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="42b99-265">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="42b99-266">İlk yedekleme</span><span class="sxs-lookup"><span data-stu-id="42b99-266">Initial backup</span></span>
<span data-ttu-id="42b99-267">Bir veri kaynağı bir yedekleme DPM gereksinimlerini ilk kez ilk çoğaltma, oluşturduğunda DPM çoğaltma biriminde korunması için veri kaynağını tam bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="42b99-267">When backing up a datasource for the first time, DPM needs creates initial replica that creates a full copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="42b99-268">Bu etkinlik için belirli bir saat ya da zamanlanabilir veya kullanarak el ile tetiklenebilir [kümesi DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) parametresi cmdlet'iyle ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="42b99-268">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="42b99-269">DPM çoğaltma ve kurtarma noktası biriminin boyutunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="42b99-269">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="42b99-270">Ayrıca DPM çoğaltma birimi ve birim gölge kopya kullanarak boyutunu değiştirebilirsiniz [kümesi DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet'i aşağıdaki örnekteki gibi: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Veri kaynağı $DS - Protectiongroup'u $MPG-el ile - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="42b99-270">You can also change the size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="42b99-271">Koruma grubu değişiklikleri işleme</span><span class="sxs-lookup"><span data-stu-id="42b99-271">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="42b99-272">Son olarak, değişiklikleri DPM yeni koruma grubu yapılandırması başına yedek almadan önce kaydedilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="42b99-272">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="42b99-273">Bu kullanılarak sağlanabilir [kümesi DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-273">This can be achieved using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="42b99-274">Yedekleme noktaları görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="42b99-274">View the backup points</span></span>
<span data-ttu-id="42b99-275">Kullanabileceğiniz [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) bir veri kaynağı için tüm kurtarma noktalarının bir listesini almak için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="42b99-275">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="42b99-276">Bu örnekte, şunları yapacağız:</span><span class="sxs-lookup"><span data-stu-id="42b99-276">In this example, we will:</span></span>

* <span data-ttu-id="42b99-277">DPM sunucusundaki tüm PGs getirebilir ve bir dizide saklanan```$PG```</span><span class="sxs-lookup"><span data-stu-id="42b99-277">fetch all the PGs on the DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="42b99-278">karşılık gelen veri kaynakları alma```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="42b99-278">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="42b99-279">veri kaynağı için tüm kurtarma noktalarının alın.</span><span class="sxs-lookup"><span data-stu-id="42b99-279">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="42b99-280">Azure üzerinde korunan verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="42b99-280">Restore data protected on Azure</span></span>
<span data-ttu-id="42b99-281">Verileri geri birleşimidir bir ```RecoverableItem``` nesne ve ```RecoveryOption``` nesne.</span><span class="sxs-lookup"><span data-stu-id="42b99-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="42b99-282">Önceki bölümde biz bir veri kaynağı için yedekleme noktalarının bir listesini aldı.</span><span class="sxs-lookup"><span data-stu-id="42b99-282">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="42b99-283">Aşağıdaki örnekte, kurtarma için hedef yedekleme noktaları birleştirerek bir Hyper-V sanal makinesi Azure Yedekleme'den geri yükleme göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="42b99-283">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="42b99-284">Bu örnek içerir:</span><span class="sxs-lookup"><span data-stu-id="42b99-284">This example includes:</span></span>

* <span data-ttu-id="42b99-285">Kurtarma seçeneğini kullanarak oluşturma [yeni DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-285">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="42b99-286">Kullanarak yedekleme noktaları dizisi getirme ```Get-DPMRecoveryPoint``` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="42b99-286">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="42b99-287">Geri yüklemek için bir yedekleme noktasının seçme.</span><span class="sxs-lookup"><span data-stu-id="42b99-287">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="42b99-288">Komutları, herhangi bir veri kaynağı türü için kolayca genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="42b99-288">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42b99-289">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="42b99-289">Next steps</span></span>
* <span data-ttu-id="42b99-290">Azure yedekleme DPM hakkında daha fazla bilgi için bkz: [DPM yedekleme giriş](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="42b99-290">For more information about DPM to Azure Backup see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
