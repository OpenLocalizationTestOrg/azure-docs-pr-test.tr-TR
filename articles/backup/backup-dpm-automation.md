---
title: "aaaAzure yedekleme - kullanım PowerShell tooback DPM iş yüklerini | Microsoft Docs"
description: "Bilgi nasıl toodeploy ve Data Protection Manager (PowerShell kullanarak DPM için) Azure Backup yönetme"
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
ms.openlocfilehash: 27d2b4b3127b68c9da564697eb61dc3ccbc34b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="5ce3f-103">Dağıtma ve PowerShell kullanarak Data Protection Manager (DPM) sunucuları için yedekleme tooAzure yönetme</span><span class="sxs-lookup"><span data-stu-id="5ce3f-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ce3f-104">ARM</span><span class="sxs-lookup"><span data-stu-id="5ce3f-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="5ce3f-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="5ce3f-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="5ce3f-106">Bu makale size nasıl gösterir toouse PowerShell toosetup Azure yedekleme, bir DPM sunucusu ve toomanage yedekleme ve kurtarma.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-106">This article shows you how toouse PowerShell toosetup Azure Backup on a DPM server, and toomanage backup and recovery.</span></span>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="5ce3f-107">Merhaba PowerShell ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="5ce3f-107">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="5ce3f-108">Data Protection Manager tooAzure PowerShell toomanage yedeklemelerden kullanabilmeniz için önce toohave hello sağ ortamında PowerShell gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-108">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="5ce3f-109">Merhaba PowerShell oturumu Hello başlangıcında komutu tooimport hello sağ modülleri aşağıdaki hello çalıştırın ve toocorrectly başvuru hello DPM cmdlet'leri izin emin olun:</span><span class="sxs-lookup"><span data-stu-id="5ce3f-109">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="5ce3f-110">Kurulumu'nu ve kaydı</span><span class="sxs-lookup"><span data-stu-id="5ce3f-110">Setup and Registration</span></span>
<span data-ttu-id="5ce3f-111">toobegin:</span><span class="sxs-lookup"><span data-stu-id="5ce3f-111">toobegin:</span></span>

1. <span data-ttu-id="5ce3f-112">[En son PowerShell indirme](https://github.com/Azure/azure-powershell/releases) (gerekli minimum sürüm: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="5ce3f-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="5ce3f-113">Çok geçerek Hello Azure yedekleme cmdlet'leri etkinleştirmek*AzureResourceManager* hello kullanarak moduna **Switch-AzureMode** komutunu:</span><span class="sxs-lookup"><span data-stu-id="5ce3f-113">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="5ce3f-114">Merhaba aşağıdaki Kurulum ve kayıt görevler PowerShell ile otomatik olarak yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="5ce3f-114">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="5ce3f-115">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ce3f-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="5ce3f-116">Hello Azure Backup aracısını yükleme</span><span class="sxs-lookup"><span data-stu-id="5ce3f-116">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="5ce3f-117">Hello Azure Backup hizmeti ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="5ce3f-117">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="5ce3f-118">Ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="5ce3f-118">Networking settings</span></span>
* <span data-ttu-id="5ce3f-119">Şifreleme ayarları</span><span class="sxs-lookup"><span data-stu-id="5ce3f-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="5ce3f-120">Kurtarma hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ce3f-120">Create a recovery services vault</span></span>
<span data-ttu-id="5ce3f-121">Aşağıdaki adımları hello kurtarma Hizmetleri kasası oluşturmada size yol açar.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-121">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="5ce3f-122">Kurtarma Hizmetleri kasasına yedekleme Kasası ' farklıdır.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="5ce3f-123">Azure Backup hello için ilk kez kullanıyorsanız hello kullanmalısınız **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery hizmeti sağlayıcısı aboneliğinizle.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-123">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="5ce3f-124">tooplace ihtiyacınız hello kurtarma Hizmetleri kasası bir ARM kaynak olduğundan, bir kaynak grubu içinde.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-124">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="5ce3f-125">Varolan bir kaynak grubunu kullanın veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="5ce3f-126">Yeni bir kaynak grubu oluştururken hello kaynak grubu için hello ad ve konum belirtin.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-126">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="5ce3f-127">Kullanım hello **yeni AzureRmRecoveryServicesVault** cmdlet toocreate yeni bir kasa.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-127">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate a new vault.</span></span> <span data-ttu-id="5ce3f-128">Toospecify hello hello kasa için aynı konumu hello kaynak grubu için kullanıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-128">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="5ce3f-129">Depolama artıklık toouse Hello türünü belirtin; kullanabileceğiniz [yerel olarak yedekli depolama (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) veya [coğrafi olarak yedekli depolama (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="5ce3f-129">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="5ce3f-130">Merhaba aşağıdaki örnek tooGeoRedundant testVault için hello - BackupStorageRedundancy seçeneği ayarlanmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-130">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="5ce3f-131">Çok sayıda Azure yedekleme cmdlet'lerini girdi olarak hello kurtarma Hizmetleri kasası nesnesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-131">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="5ce3f-132">Bu nedenle, bu kullanışlı toostore hello yedekleme kurtarma Hizmetleri kasası, bir değişkende nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-132">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="5ce3f-133">Bir abonelikte görünüm hello kasaları</span><span class="sxs-lookup"><span data-stu-id="5ce3f-133">View hello vaults in a subscription</span></span>
<span data-ttu-id="5ce3f-134">Kullanım **Get-AzureRmRecoveryServicesVault** tooview hello hello geçerli Abonelikteki tüm kasalarının listesi.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-134">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="5ce3f-135">Yeni bir kasa oluşturulduğunu bu komutu toocheck veya toosee kullanabilirsiniz hangi kasalarını hello abonelikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-135">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="5ce3f-136">Get-AzureRmRecoveryServicesVault Hello komutunu çalıştırın ve hello Abonelikteki tüm kasalarını listelenir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-136">Run hello command, Get-AzureRmRecoveryServicesVault, and all vaults in hello subscription are listed.</span></span>

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


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="5ce3f-137">Bir DPM sunucusu üzerinde Hello Azure Backup aracısını yükleme</span><span class="sxs-lookup"><span data-stu-id="5ce3f-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="5ce3f-138">Hello Azure Backup aracısını yüklemeden önce indirildi ve Windows Server hello mevcut toohave hello yükleyici gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="5ce3f-139">Hello hello Installer hello en son sürümünü elde edebilirsiniz [Microsoft Download Center](http://aka.ms/azurebackup_agent) veya hello kurtarma Hizmetleri Kasası'nın Pano sayfası.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="5ce3f-140">Kolay erişilebilecek bir konuma tooan gibi Hello yükleyici Kaydet * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="5ce3f-141">komutu yükseltilmiş bir PowerShell konsolunda aşağıdaki hello çalıştırmak tooinstall hello Aracısı **hello DPM sunucusunda**:</span><span class="sxs-lookup"><span data-stu-id="5ce3f-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="5ce3f-142">Bu, tüm hello varsayılan seçeneklerle hello aracı yükler.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="5ce3f-143">Merhaba yükleme hello arka planda birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="5ce3f-144">Merhaba belirtmezseniz */nu* seçeneği hello **Windows Update** hello yükleme toocheck herhangi bir güncelleştirme için hello sonunda penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-144">If you do not specify hello */nu* option hello **Windows Update** window opens at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="5ce3f-145">Merhaba Aracısı hello yüklü programlar listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-145">hello agent shows up in hello list of installed programs.</span></span> <span data-ttu-id="5ce3f-146">toosee hello listesi yüklü programlar, çok Git**Denetim Masası** > **programları** > **programlar ve Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Yüklü aracı](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="5ce3f-148">Yükleme Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="5ce3f-148">Installation options</span></span>
<span data-ttu-id="5ce3f-149">toosee aşağıdaki kullanım hello hello commandline kullanılabilir tüm hello seçenekleri komutu:</span><span class="sxs-lookup"><span data-stu-id="5ce3f-149">toosee all hello options available via hello commandline, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="5ce3f-150">Merhaba mevcut Seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5ce3f-150">hello available options include:</span></span>

| <span data-ttu-id="5ce3f-151">Seçenek</span><span class="sxs-lookup"><span data-stu-id="5ce3f-151">Option</span></span> | <span data-ttu-id="5ce3f-152">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="5ce3f-152">Details</span></span> | <span data-ttu-id="5ce3f-153">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="5ce3f-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5ce3f-154">/q</span><span class="sxs-lookup"><span data-stu-id="5ce3f-154">/q</span></span> |<span data-ttu-id="5ce3f-155">Sessiz yükleme</span><span class="sxs-lookup"><span data-stu-id="5ce3f-155">Quiet installation</span></span> |- |
| <span data-ttu-id="5ce3f-156">p: "Konum"</span><span class="sxs-lookup"><span data-stu-id="5ce3f-156">/p:"location"</span></span> |<span data-ttu-id="5ce3f-157">Yol toohello yükleme klasörünü hello Azure Yedekleme aracısı.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="5ce3f-158">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Aracısı</span><span class="sxs-lookup"><span data-stu-id="5ce3f-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="5ce3f-159">/ s: "Konum"</span><span class="sxs-lookup"><span data-stu-id="5ce3f-159">/s:"location"</span></span> |<span data-ttu-id="5ce3f-160">Hello Azure Backup aracısı için yol toohello Önbellek klasörü.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="5ce3f-161">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="5ce3f-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="5ce3f-162">/m</span><span class="sxs-lookup"><span data-stu-id="5ce3f-162">/m</span></span> |<span data-ttu-id="5ce3f-163">Katılımı tooMicrosoft güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="5ce3f-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="5ce3f-164">/nu</span><span class="sxs-lookup"><span data-stu-id="5ce3f-164">/nu</span></span> |<span data-ttu-id="5ce3f-165">Yükleme tamamlandıktan sonra güncelleştirmeleri denetleme</span><span class="sxs-lookup"><span data-stu-id="5ce3f-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="5ce3f-166">/d</span><span class="sxs-lookup"><span data-stu-id="5ce3f-166">/d</span></span> |<span data-ttu-id="5ce3f-167">Microsoft Azure kurtarma Hizmetleri Aracısı kaldırır</span><span class="sxs-lookup"><span data-stu-id="5ce3f-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="5ce3f-168">/ph</span><span class="sxs-lookup"><span data-stu-id="5ce3f-168">/ph</span></span> |<span data-ttu-id="5ce3f-169">Proxy konağı adresi</span><span class="sxs-lookup"><span data-stu-id="5ce3f-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="5ce3f-170">/PO</span><span class="sxs-lookup"><span data-stu-id="5ce3f-170">/po</span></span> |<span data-ttu-id="5ce3f-171">Proxy ana bilgisayar bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="5ce3f-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="5ce3f-172">/PU</span><span class="sxs-lookup"><span data-stu-id="5ce3f-172">/pu</span></span> |<span data-ttu-id="5ce3f-173">Proxy konağı kullanıcı</span><span class="sxs-lookup"><span data-stu-id="5ce3f-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="5ce3f-174">/pw</span><span class="sxs-lookup"><span data-stu-id="5ce3f-174">/pw</span></span> |<span data-ttu-id="5ce3f-175">Proxy parolası</span><span class="sxs-lookup"><span data-stu-id="5ce3f-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-tooa-recovery-services-vault"></a><span data-ttu-id="5ce3f-176">DPM tooa kurtarma Hizmetleri kasası kaydetme</span><span class="sxs-lookup"><span data-stu-id="5ce3f-176">Registering DPM tooa Recovery Services Vault</span></span>
<span data-ttu-id="5ce3f-177">Merhaba kurtarma Hizmetleri kasası oluşturduktan sonra hello en son aracı hello kasa kimlik bilgilerini indirin ve C:\Downloads gibi uygun bir konuma depolayın.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-177">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="5ce3f-178">Merhaba Hello DPM sunucusunda çalıştırın [başlangıç OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello makine hello kasası ile.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-178">On hello DPM server, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="5ce3f-179">İlk yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="5ce3f-179">Initial configuration settings</span></span>
<span data-ttu-id="5ce3f-180">Merhaba DPM sunucusu ile Merhaba kaydedildikten sonra kurtarma Hizmetleri kasası, varsayılan abonelik ayarlarını başlatır.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-180">Once hello DPM Server is registered with hello Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="5ce3f-181">Bu abonelik ayarlar, ağ, şifreleme ve hello hazırlama alanı içerir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-181">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="5ce3f-182">gereksinim duyduğunuz toofirst toochange abonelik ayarlarını almak bir tanıtıcı (hello kullanarak hello varolan varsayılan) ayarları [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5ce3f-182">toochange subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="5ce3f-183">Tüm değişiklikleri yapılmış toothis yerel PowerShell nesnesi olan ```$setting``` ve ardından hello tam nesne taahhüt tooDPM ve Azure Backup toosave hello kullanarak bunları [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-183">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="5ce3f-184">Toouse hello gereksinim ```–Commit``` değişiklikleri hello bayrağı tooensure kaldı.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-184">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="5ce3f-185">Hello ayarları değil uygulanan ve olması kaydedilen sürece Azure yedekleme tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-185">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="5ce3f-186">Ağ</span><span class="sxs-lookup"><span data-stu-id="5ce3f-186">Networking</span></span>
<span data-ttu-id="5ce3f-187">Merhaba bağlantı hello DPM makine toohello hello Azure Backup hizmeti, bir proxy sunucu üzerinden internet ise, hello proxy sunucusu ayarları başarılı yedeklemeler için sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-187">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="5ce3f-188">Bu hello kullanarak yapılır ```-ProxyServer```ve ```-ProxyPort```, ```-ProxyUsername``` ve hello ```ProxyPassword``` hello parametrelerle [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-188">This is done by using hello ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="5ce3f-189">Bu örnekte, olmadığından hiçbir Ara sunucunun biz açıkça herhangi bir proxy ile ilgili bilgi temizleme.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="5ce3f-190">Bant genişliği kullanımı ile seçenekleri de denetlenebilir ```-WorkHourBandwidth``` ve ```-NonWorkHourBandwidth``` hello haftanın belirli bir dizi için.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="5ce3f-191">Bu örnekte, biz herhangi azaltma ayarlıyorsanız değil.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a><span data-ttu-id="5ce3f-192">Merhaba hazırlama alanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5ce3f-192">Configuring hello staging Area</span></span>
<span data-ttu-id="5ce3f-193">Merhaba DPM sunucusunda çalışan hello Azure Yedekleme aracısı, (yerel hazırlama alanı) hello buluttan geri yüklenen veriler için geçici depolama gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-193">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="5ce3f-194">Merhaba hazırlama alanı hello kullanarak yapılandırma [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i ve hello ```-StagingAreaPath``` parametresi.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-194">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="5ce3f-195">Merhaba yukarıdaki örnekte, hello hazırlama alanı çok ayarlanacak*C:\StagingArea* hello PowerShell nesnesindeki ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-195">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="5ce3f-196">Merhaba belirtilen klasör zaten var, aksi takdirde hello abonelik ayarlarını hello son yürütme başarısız olur emin olun.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-196">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="5ce3f-197">Şifreleme ayarları</span><span class="sxs-lookup"><span data-stu-id="5ce3f-197">Encryption settings</span></span>
<span data-ttu-id="5ce3f-198">Merhaba gönderilen yedekleme verileri tooAzure yedekleme şifrelenmiş tooprotect hello hello veri gizliliğini ' dir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-198">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="5ce3f-199">Merhaba şifreleme parolası hello "parola" toodecrypt hello geri yükleme hello aynı anda verilerdir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-199">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="5ce3f-200">Önemli tookeep bu bilgileri güvenlidir ve ayarlandıktan sonra güvenli.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-200">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="5ce3f-201">Merhaba aşağıdaki örnekte, hello ilk komut hello dizesini sayıya dönüştürür ```passphrase123456789``` adlı tooa güvenli dize atar hello güvenli dize toohello değişkeni ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-201">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="5ce3f-202">İkinci komut Hello ayarlar hello güvenli dize ```$Passphrase``` yedeklemeleri şifrelemek için başlangıç parolası.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-202">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="5ce3f-203">Ayarlandıktan sonra hello parola bilgilerini güvenli ve güvenli tutar.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-203">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="5ce3f-204">Bu parola olmadan mümkün toorestore verileri azure'dan olmaz.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-204">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="5ce3f-205">Bu noktada, tüm gerekli hello değişiklikleri toohello yaptığınız ```$setting``` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-205">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="5ce3f-206">Toocommit hello değişiklikleri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-206">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="5ce3f-207">Veri tooAzure yedekleme koruma</span><span class="sxs-lookup"><span data-stu-id="5ce3f-207">Protect data tooAzure Backup</span></span>
<span data-ttu-id="5ce3f-208">Bu bölümde, bir üretim sunucusu tooDPM ekleyin ve hello veri toolocal DPM depolama ve ardından tooAzure yedekleme daha sonra koruyun.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-208">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="5ce3f-209">Merhaba örneklerde, biz gösterilmektedir nasıl tooback dosya ve klasörler.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-209">In hello examples, we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="5ce3f-210">Merhaba mantığı kolayca genişletilmiş toobackup herhangi bir DPM desteklenen veri kaynağı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-210">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="5ce3f-211">Tüm DPM yedeklemelerini dört bölümden ile koruma grubu (PG) tarafından yönetilir:</span><span class="sxs-lookup"><span data-stu-id="5ce3f-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="5ce3f-212">**Grup üyeleri** tüm hello korunabilir nesneler listesi (olarak da bilinen *veri kaynakları* dpm'de) hello tooprotect istediğiniz aynı koruma grubunda.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-212">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="5ce3f-213">Örneğin, yedekleme farklı gereksinimlere sahip, bir koruma grubu ve SQL Server veritabanlarını başka bir koruma grubunda tooprotect üretim VM'ler isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-213">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="5ce3f-214">Üretim sunucusundaki herhangi bir veri kaynağı yedekleyebilirsiniz önce DPM Aracısı hello sunucuda yüklü olduğundan ve DPM tarafından yönetilen toomake emin hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-214">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="5ce3f-215">Merhaba adımlarını izleyin [yükleme, DPM Aracısı hello](https://technet.microsoft.com/library/bb870935.aspx) ve toohello bağlama uygun DPM sunucusu.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-215">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="5ce3f-216">**Veri koruma yöntemini** hello hedef yedekleme konumları - bant, disk ve bulut belirtir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-216">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="5ce3f-217">Bizim örneğimizde biz veri toohello yerel disk ve toohello bulut korur.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-217">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="5ce3f-218">A **yedekleme zamanlaması** yedeklemeler gerçekleştirilecek toobe gerektiğinde ve ne sıklıkta hello verilerin hello DPM sunucusu ile Merhaba üretim sunucusu arasında eşitlenmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-218">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="5ce3f-219">A **bekletme zamanlaması** Azure'da ne kadar süreyle tooretain hello kurtarma noktaları belirtir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-219">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="5ce3f-220">Koruma grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ce3f-220">Creating a protection group</span></span>
<span data-ttu-id="5ce3f-221">Başlangıç hello kullanarak yeni bir koruma grubu oluşturarak [yeni DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-221">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="5ce3f-222">cmdlet'i yukarıdaki Hello koruma adlı bir grup oluşturur *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-222">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="5ce3f-223">Mevcut bir koruma grubunun ayrıca sonraki tooadd yedekleme toohello Azure bulut değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-223">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="5ce3f-224">Ancak, toomake herhangi bir değişiklik toohello koruma grubu - yeni veya varolan - ihtiyacımız tooget bir tanıtıcı üzerinde bir *değiştirilebilir* hello kullanarak nesnesi [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-224">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="5ce3f-225">Grup üyeleri toohello koruma grubu ekleme</span><span class="sxs-lookup"><span data-stu-id="5ce3f-225">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="5ce3f-226">Her DPM aracısının yüklü olduğu hello sunucusunda veri kaynakları listesi hello bilir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-226">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="5ce3f-227">tooadd datasource toohello koruma grubu, DPM Aracısı gereksinimlerini toofirst hello hello veri kaynakları geri toohello DPM sunucusu listesini gönderin.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-227">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="5ce3f-228">Seçili ve toohello koruma grubuna eklenen bir veya daha fazla veri kaynakları olan.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-228">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="5ce3f-229">Bu olan tooachieve Hello PowerShell adımlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="5ce3f-229">hello PowerShell steps needed tooachieve this are:</span></span>

1. <span data-ttu-id="5ce3f-230">DPM Aracısı hello DPM tarafından yönetilen tüm sunucuların listesi getirilemedi.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-230">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="5ce3f-231">Belirli bir sunucu seçin.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-231">Choose a specific server.</span></span>
3. <span data-ttu-id="5ce3f-232">Merhaba sunucusundaki tüm veri kaynakları listesi getirilemedi.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-232">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="5ce3f-233">Bir veya daha fazla veri kaynakları seçin ve bunları toohello koruma grubu Ekle</span><span class="sxs-lookup"><span data-stu-id="5ce3f-233">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="5ce3f-234">hangi hello DPM aracısının yüklü olduğundan ve hello DPM sunucusu tarafından yönetilen sunucuları Hello listesi ile Merhaba edinilen [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-234">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="5ce3f-235">Biz filtrelemek ve yalnızca PS adıyla yapılandırın, bu örnekte *productionserver01* yedekleme için.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="5ce3f-236">Şimdi üzerinde hello veri kaynaklarının listesini getirme ```$server``` hello kullanarak [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-236">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="5ce3f-237">Bu örnekte, biz hello birim için filtre * D:\* tooconfigure yedekleme için istediğimizi.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-237">In this example we are filtering for hello volume *D:\* that we want tooconfigure for backup.</span></span> <span data-ttu-id="5ce3f-238">Bu veri kaynağı sonra toohello koruma grubuna eklenen hello kullanarak [Ekle DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-238">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="5ce3f-239">Toouse hello unutmayın *değiştirilebilir* koruma grubu nesnesi ```$MPG``` toomake hello ekler.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-239">Remember toouse hello *modifiable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="5ce3f-240">Veri kaynakları toohello koruma grubu seçilen tüm hello ekleyene kadar gerektiği gibi birçok kez bu adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-240">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="5ce3f-241">Yalnızca bir datasource ve hello koruma grubunu oluşturmak için tam hello iş akışı ile başlayın ve daha sonraki bir noktada daha fazla veri kaynakları toohello koruma grubuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-241">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="5ce3f-242">Merhaba veri koruma yöntemi seçme</span><span class="sxs-lookup"><span data-stu-id="5ce3f-242">Selecting hello data protection method</span></span>
<span data-ttu-id="5ce3f-243">Merhaba datasources toohello koruma grubuna eklendikten sonra hello sonraki hello kullanarak toospecify hello koruma yöntemini adımdır [kümesi DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-243">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="5ce3f-244">Bu örnekte, hello koruma grubu yerel disk ve bulut yedekleme için kurulur.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-244">In this example, hello Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="5ce3f-245">Hello kullanarak tooprotect toocloud istediğiniz toospecify hello datasource etmeniz [Ekle DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet'iyle - çevrimiçi bayrağı.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-245">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="5ce3f-246">Merhaba bekletme aralığını ayarlama</span><span class="sxs-lookup"><span data-stu-id="5ce3f-246">Setting hello retention range</span></span>
<span data-ttu-id="5ce3f-247">Ayarlama hello bekletme hello kullanarak hello yedekleme noktaları için [kümesi DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-247">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="5ce3f-248">Hello kullanarak Hello yedekleme zamanlaması tanımlanmış önce tek tooset hello bekletme görünebilir ancak ```Set-DPMPolicyObjective``` cmdlet'i sonra değiştirilebilen varsayılan yedekleme zamanlaması otomatik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-248">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="5ce3f-249">Bu her zaman mümkün tooset hello yedekleme zamanlaması önce ve sonra bekletme ilkesi hello.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-249">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="5ce3f-250">Merhaba aşağıdaki örnekte, hello cmdlet'i disk yedeklemeleri hello bekletme parametreleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-250">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="5ce3f-251">Bu yedeklemeler 10 gün ve eşitleme verileri için 6 saatte bir hello üretim sunucusu ve hello DPM sunucusu arasındaki korur.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-251">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="5ce3f-252">Merhaba ```SynchronizationFrequencyMinutes``` ne sıklıkta bir yedekleme noktasının, ancak nasıl oluşturulduğunu tanımlamıyor genellikle veri kopyalanan toohello DPM sunucusu değil.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-252">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server.</span></span>  <span data-ttu-id="5ce3f-253">Bu ayar, yedeklemeler çok büyük hale gelmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="5ce3f-254">(DPM başvuruyor toothem çevrimiçi yedeklemeler) tooAzure giderek yedeklemeler için hello bekletme aralıkları için yapılandırılabilir [üst öğe Son şeması (GFS) kullanarak bekletme'uzun süreli](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="5ce3f-254">For backups going tooAzure (DPM refers toothem as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="5ce3f-255">Diğer bir deyişle, günlük, haftalık, aylık ve yıllık bekletme ilkeleri içeren bir birleşik bekletme ilkesi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="5ce3f-256">Bu örnekte, biz istiyoruz hello karmaşık bekletme düzeni temsil eden bir dizi oluşturmak ve ardından hello kullanarak hello bekletme aralığı yapılandırın [kümesi DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-256">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="5ce3f-257">Set hello yedekleme zamanlaması</span><span class="sxs-lookup"><span data-stu-id="5ce3f-257">Set hello backup schedule</span></span>
<span data-ttu-id="5ce3f-258">Merhaba koruma hedefi hello kullanarak belirtirseniz, DPM bir varsayılan yedekleme zamanlaması otomatik olarak ayarlar. ```Set-DPMPolicyObjective``` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-258">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="5ce3f-259">toochange hello varsayılan zamanlamaların kullanmak hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet hello tarafından izlenen [kümesi DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-259">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="5ce3f-260">Örneğin, yukarıdaki hello içinde ```$onlineSch``` hello varolan çevrimiçi koruma zamanlamasını hello GFS düzeni hello koruma grubu için içeren bir dizi dört öğelerle:</span><span class="sxs-lookup"><span data-stu-id="5ce3f-260">In hello above example, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="5ce3f-261">```$onlineSch[0]```Merhaba günlük zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="5ce3f-261">```$onlineSch[0]``` contains hello daily schedule</span></span>
2. <span data-ttu-id="5ce3f-262">```$onlineSch[1]```Merhaba haftalık zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="5ce3f-262">```$onlineSch[1]``` contains hello weekly schedule</span></span>
3. <span data-ttu-id="5ce3f-263">```$onlineSch[2]```Merhaba aylık zamanlama içerir</span><span class="sxs-lookup"><span data-stu-id="5ce3f-263">```$onlineSch[2]``` contains hello monthly schedule</span></span>
4. <span data-ttu-id="5ce3f-264">```$onlineSch[3]```Merhaba yıllık çizelge içerir</span><span class="sxs-lookup"><span data-stu-id="5ce3f-264">```$onlineSch[3]``` contains hello yearly schedule</span></span>

<span data-ttu-id="5ce3f-265">Bu nedenle toomodify hello haftalık zamanlama gerekiyorsa, toorefer toohello gerekir ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-265">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="5ce3f-266">İlk yedekleme</span><span class="sxs-lookup"><span data-stu-id="5ce3f-266">Initial backup</span></span>
<span data-ttu-id="5ce3f-267">Hello için veri kaynağı ilk kez, DPM gereksinimlerini yedekleme ilk çoğaltma, oluşturduğunda DPM çoğaltma birimi korumalı hello datasource toobe tam bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-267">When backing up a datasource for hello first time, DPM needs creates initial replica that creates a full copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="5ce3f-268">Bu etkinlik için belirli bir saat ya da zamanlanabilir veya hello kullanarak el ile tetiklenebilir [kümesi DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) hello parametre cmdlet'iyle ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-268">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="5ce3f-269">DPM çoğaltma ve kurtarma noktası birimi Hello boyutunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="5ce3f-269">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="5ce3f-270">Ayrıca DPM çoğaltma birimi ve birim gölge kopya kullanarak hello boyutunu değiştirebilirsiniz [kümesi DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) aşağıdaki örneğine hello olduğu gibi cmdlet: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - Protectiongroup'u $MPG-el ile - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="5ce3f-270">You can also change hello size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="5ce3f-271">Uygulanıyor hello değişiklikleri toohello koruma grubu</span><span class="sxs-lookup"><span data-stu-id="5ce3f-271">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="5ce3f-272">Son olarak, DPM hello yeni koruma grubu yapılandırması başına hello yedek almadan önce kaydedilmiş toobe hello değişiklikleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-272">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="5ce3f-273">Bu hello kullanarak elde [kümesi DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-273">This can be achieved using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="5ce3f-274">Görünüm hello yedekleme noktaları</span><span class="sxs-lookup"><span data-stu-id="5ce3f-274">View hello backup points</span></span>
<span data-ttu-id="5ce3f-275">Merhaba kullanabilirsiniz [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget bir veri kaynağı için tüm kurtarma noktalarının bir listesi.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-275">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="5ce3f-276">Bu örnekte, şunları yapacağız:</span><span class="sxs-lookup"><span data-stu-id="5ce3f-276">In this example, we will:</span></span>

* <span data-ttu-id="5ce3f-277">Fetch tüm PGs hello DPM sunucusunda hello ve bir dizide saklanan```$PG```</span><span class="sxs-lookup"><span data-stu-id="5ce3f-277">fetch all hello PGs on hello DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="5ce3f-278">Merhaba datasources karşılık gelen toohello Al```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="5ce3f-278">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="5ce3f-279">Tüm hello kurtarma noktaları için bir veri kaynağı alın.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-279">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="5ce3f-280">Azure üzerinde korunan verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="5ce3f-280">Restore data protected on Azure</span></span>
<span data-ttu-id="5ce3f-281">Verileri geri birleşimidir bir ```RecoverableItem``` nesne ve ```RecoveryOption``` nesne.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="5ce3f-282">Merhaba önceki bölümde, biz bir veri kaynağı için hello yedekleme noktalarının bir listesini aldı.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-282">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="5ce3f-283">Merhaba aşağıdaki örnekte, toorestore bir Hyper-V sanal makineden Azure yedekleme hello ile Birleşen yedekleme noktaları tarafından hedef kurtarma için nasıl ekleyebileceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-283">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="5ce3f-284">Bu örnek içerir:</span><span class="sxs-lookup"><span data-stu-id="5ce3f-284">This example includes:</span></span>

* <span data-ttu-id="5ce3f-285">Hello kullanarak bir kurtarma seçeneği oluşturma [yeni DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-285">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="5ce3f-286">Hello kullanarak yedekleme noktaları getirilirken hello dizisi ```Get-DPMRecoveryPoint``` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-286">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="5ce3f-287">Gelen bir yedekleme noktası toorestore seçme.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-287">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="5ce3f-288">Merhaba komutları herhangi bir veri kaynağı türü için kolayca genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="5ce3f-288">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ce3f-289">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5ce3f-289">Next steps</span></span>
* <span data-ttu-id="5ce3f-290">DPM hakkında daha fazla bilgi için bkz: tooAzure yedekleme [giriş tooDPM yedekleme](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="5ce3f-290">For more information about DPM tooAzure Backup see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
