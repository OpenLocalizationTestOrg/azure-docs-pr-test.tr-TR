---
title: "Windows Server tooAzure yukarı aaaUse PowerShell tooback | Microsoft Docs"
description: "Bilgi nasıl toodeploy ve Azure PowerShell kullanarak yedekleme yönetme"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="762ad-103">Dağıtma ve PowerShell kullanarak Windows Server/Windows İstemcisi için yedekleme tooAzure yönetme</span><span class="sxs-lookup"><span data-stu-id="762ad-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="762ad-104">ARM</span><span class="sxs-lookup"><span data-stu-id="762ad-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="762ad-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="762ad-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="762ad-106">Bu makale size nasıl gösterir toouse Azure yedekleme Windows Server veya Windows İstemcisi ayarlama ve yedekleme ve kurtarma yönetmek için PowerShell.</span><span class="sxs-lookup"><span data-stu-id="762ad-106">This article shows you how toouse PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="762ad-107">Azure PowerShell'i yükleme</span><span class="sxs-lookup"><span data-stu-id="762ad-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="762ad-108">Bu makalede hello Azure Resource Manager (ARM) ve hello bir kaynak grubu bir kurtarma Hizmetleri kasasına toouse etkinleştirmek MS çevrimiçi yedekleme PowerShell cmdlet'leri odaklanır.</span><span class="sxs-lookup"><span data-stu-id="762ad-108">This article focuses on hello Azure Resource Manager (ARM) and hello MS Online Backup PowerShell cmdlets that enable you toouse a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="762ad-109">Azure PowerShell 1.0 Ekim 2015'te yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="762ad-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="762ad-110">Bu sürüm hello 0.9.8 yayın başarılı oldu ve bazı önemli değişiklikler hakkında özellikle hello adlandırma deseni hello cmdlet'lerinin getirildi.</span><span class="sxs-lookup"><span data-stu-id="762ad-110">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="762ad-111">1.0 cmdlet'leri izleyin hello adlandırma deseni {fiil}-AzureRm {isim}; Merhaba 0.9.8 adlarında değil ancak **Rm** (örneğin, New-Azureresourcegroup yerine New-Azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="762ad-111">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="762ad-112">Azure PowerShell 0.9.8 kullanıldığında, önce hello Resource Manager moduna hello çalıştırarak etkinleştirmelisiniz **Switch-AzureMode AzureResourceManager** komutu.</span><span class="sxs-lookup"><span data-stu-id="762ad-112">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="762ad-113">Bu komut 1.0 veya üstü gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="762ad-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="762ad-114">Merhaba 0.9.8 ortamında hello 1.0 veya sonraki ortamı için yazılan komut dosyalarınızı toouse istiyorsanız dikkatle güncelleştirin ve test hello betikleri bir ön üretim ortamında üretim tooavoid kullanmadan önce beklenmeyen etkisi.</span><span class="sxs-lookup"><span data-stu-id="762ad-114">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully update and test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="762ad-115">[Merhaba son PowerShell yayın indirme](https://github.com/Azure/azure-powershell/releases) (gerekli minimum sürüm: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="762ad-115">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="762ad-116">Kurtarma hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="762ad-116">Create a recovery services vault</span></span>
<span data-ttu-id="762ad-117">Aşağıdaki adımları hello kurtarma Hizmetleri kasası oluşturmada size yol açar.</span><span class="sxs-lookup"><span data-stu-id="762ad-117">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="762ad-118">Kurtarma Hizmetleri kasasına yedekleme Kasası ' farklıdır.</span><span class="sxs-lookup"><span data-stu-id="762ad-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="762ad-119">Azure Backup hello için ilk kez kullanıyorsanız hello kullanmalısınız **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery hizmeti sağlayıcısı aboneliğinizle.</span><span class="sxs-lookup"><span data-stu-id="762ad-119">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="762ad-120">tooplace ihtiyacınız hello kurtarma Hizmetleri kasası bir ARM kaynak olduğundan, bir kaynak grubu içinde.</span><span class="sxs-lookup"><span data-stu-id="762ad-120">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="762ad-121">Varolan bir kaynak grubunu kullanın veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="762ad-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="762ad-122">Yeni bir kaynak grubu oluştururken hello kaynak grubu için hello ad ve konum belirtin.</span><span class="sxs-lookup"><span data-stu-id="762ad-122">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="762ad-123">Kullanım hello **yeni AzureRmRecoveryServicesVault** cmdlet toocreate hello yeni Kasa.</span><span class="sxs-lookup"><span data-stu-id="762ad-123">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate hello new vault.</span></span> <span data-ttu-id="762ad-124">Toospecify hello hello kasa için aynı konumu hello kaynak grubu için kullanıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="762ad-124">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="762ad-125">Depolama artıklık toouse Hello türünü belirtin; kullanabileceğiniz [yerel olarak yedekli depolama (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) veya [coğrafi olarak yedekli depolama (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="762ad-125">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="762ad-126">Merhaba aşağıdaki örnek tooGeoRedundant testVault için hello - BackupStorageRedundancy seçeneği ayarlanmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="762ad-126">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="762ad-127">Çok sayıda Azure yedekleme cmdlet'lerini girdi olarak hello kurtarma Hizmetleri kasası nesnesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="762ad-127">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="762ad-128">Bu nedenle, bu kullanışlı toostore hello yedekleme kurtarma Hizmetleri kasası, bir değişkende nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="762ad-128">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="762ad-129">Bir abonelikte görünüm hello kasaları</span><span class="sxs-lookup"><span data-stu-id="762ad-129">View hello vaults in a subscription</span></span>
<span data-ttu-id="762ad-130">Kullanım **Get-AzureRmRecoveryServicesVault** tooview hello hello geçerli Abonelikteki tüm kasalarının listesi.</span><span class="sxs-lookup"><span data-stu-id="762ad-130">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="762ad-131">Yeni bir kasa oluşturulduğunu bu komutu toocheck veya toosee kullanabilirsiniz hangi kasalarını hello abonelikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="762ad-131">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="762ad-132">Merhaba komutu çalıştırmak **Get-AzureRmRecoveryServicesVault**, ve hello Abonelikteki tüm kasalarını listelenir.</span><span class="sxs-lookup"><span data-stu-id="762ad-132">Run hello command, **Get-AzureRmRecoveryServicesVault**, and all vaults in hello subscription are listed.</span></span>

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


## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="762ad-133">Hello Azure Backup aracısını yükleme</span><span class="sxs-lookup"><span data-stu-id="762ad-133">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="762ad-134">Hello Azure Backup aracısını yüklemeden önce indirildi ve Windows Server hello mevcut toohave hello yükleyici gerekir.</span><span class="sxs-lookup"><span data-stu-id="762ad-134">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="762ad-135">Hello hello Installer hello en son sürümünü elde edebilirsiniz [Microsoft Download Center](http://aka.ms/azurebackup_agent) veya hello kurtarma Hizmetleri Kasası'nın Pano sayfası.</span><span class="sxs-lookup"><span data-stu-id="762ad-135">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="762ad-136">Kolay erişilebilecek bir konuma tooan gibi Hello yükleyici Kaydet * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="762ad-136">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="762ad-137">Alternatif olarak, PowerShell tooget hello Yükleyici'yi kullanın:</span><span class="sxs-lookup"><span data-stu-id="762ad-137">Alternatively, use PowerShell tooget hello downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="762ad-138">tooinstall hello Aracısı, komutu yükseltilmiş bir PowerShell konsolunda aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="762ad-138">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="762ad-139">Bu, tüm hello varsayılan seçeneklerle hello aracı yükler.</span><span class="sxs-lookup"><span data-stu-id="762ad-139">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="762ad-140">Merhaba yükleme hello arka planda birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="762ad-140">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="762ad-141">Merhaba belirtmezseniz */nu* seçeneği sonra hello **Windows Update** hello yükleme toocheck herhangi bir güncelleştirme için hello sonunda penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="762ad-141">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="762ad-142">Bir kez yüklendikten sonra hello Aracısı hello yüklü programlar listesinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="762ad-142">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="762ad-143">toosee hello listesi yüklü programlar, çok Git**Denetim Masası** > **programları** > **programlar ve Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="762ad-143">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Yüklü aracı](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="762ad-145">Yükleme Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="762ad-145">Installation options</span></span>
<span data-ttu-id="762ad-146">Tüm seçeneklerin aracılığıyla hello toosee komut satırı Merhaba, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="762ad-146">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="762ad-147">Merhaba mevcut Seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="762ad-147">hello available options include:</span></span>

| <span data-ttu-id="762ad-148">Seçenek</span><span class="sxs-lookup"><span data-stu-id="762ad-148">Option</span></span> | <span data-ttu-id="762ad-149">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="762ad-149">Details</span></span> | <span data-ttu-id="762ad-150">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="762ad-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="762ad-151">/q</span><span class="sxs-lookup"><span data-stu-id="762ad-151">/q</span></span> |<span data-ttu-id="762ad-152">Sessiz yükleme</span><span class="sxs-lookup"><span data-stu-id="762ad-152">Quiet installation</span></span> |- |
| <span data-ttu-id="762ad-153">p: "Konum"</span><span class="sxs-lookup"><span data-stu-id="762ad-153">/p:"location"</span></span> |<span data-ttu-id="762ad-154">Yol toohello yükleme klasörünü hello Azure Yedekleme aracısı.</span><span class="sxs-lookup"><span data-stu-id="762ad-154">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="762ad-155">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Aracısı</span><span class="sxs-lookup"><span data-stu-id="762ad-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="762ad-156">/ s: "Konum"</span><span class="sxs-lookup"><span data-stu-id="762ad-156">/s:"location"</span></span> |<span data-ttu-id="762ad-157">Hello Azure Backup aracısı için yol toohello Önbellek klasörü.</span><span class="sxs-lookup"><span data-stu-id="762ad-157">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="762ad-158">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="762ad-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="762ad-159">/m</span><span class="sxs-lookup"><span data-stu-id="762ad-159">/m</span></span> |<span data-ttu-id="762ad-160">Katılımı tooMicrosoft güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="762ad-160">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="762ad-161">/nu</span><span class="sxs-lookup"><span data-stu-id="762ad-161">/nu</span></span> |<span data-ttu-id="762ad-162">Yükleme tamamlandıktan sonra güncelleştirmeleri denetleme</span><span class="sxs-lookup"><span data-stu-id="762ad-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="762ad-163">/d</span><span class="sxs-lookup"><span data-stu-id="762ad-163">/d</span></span> |<span data-ttu-id="762ad-164">Microsoft Azure kurtarma Hizmetleri Aracısı kaldırır</span><span class="sxs-lookup"><span data-stu-id="762ad-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="762ad-165">/ph</span><span class="sxs-lookup"><span data-stu-id="762ad-165">/ph</span></span> |<span data-ttu-id="762ad-166">Proxy konağı adresi</span><span class="sxs-lookup"><span data-stu-id="762ad-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="762ad-167">/PO</span><span class="sxs-lookup"><span data-stu-id="762ad-167">/po</span></span> |<span data-ttu-id="762ad-168">Proxy ana bilgisayar bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="762ad-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="762ad-169">/PU</span><span class="sxs-lookup"><span data-stu-id="762ad-169">/pu</span></span> |<span data-ttu-id="762ad-170">Proxy konağı kullanıcı</span><span class="sxs-lookup"><span data-stu-id="762ad-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="762ad-171">/pw</span><span class="sxs-lookup"><span data-stu-id="762ad-171">/pw</span></span> |<span data-ttu-id="762ad-172">Proxy parolası</span><span class="sxs-lookup"><span data-stu-id="762ad-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a><span data-ttu-id="762ad-173">Windows Server veya Windows istemci makine tooa kurtarma Hizmetleri kasası kaydetme</span><span class="sxs-lookup"><span data-stu-id="762ad-173">Registering Windows Server or Windows client machine tooa Recovery Services Vault</span></span>
<span data-ttu-id="762ad-174">Merhaba kurtarma Hizmetleri kasası oluşturduktan sonra hello en son aracı hello kasa kimlik bilgilerini indirin ve C:\Downloads gibi uygun bir konuma depolayın.</span><span class="sxs-lookup"><span data-stu-id="762ad-174">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="762ad-175">Merhaba Windows Server veya Windows istemci makinesi üzerinde hello çalıştırmak [başlangıç OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello makine hello kasası ile.</span><span class="sxs-lookup"><span data-stu-id="762ad-175">On hello Windows Server or Windows client machine, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>
<span data-ttu-id="762ad-176">Bu ve diğer cmdlet'leri yedekleme için kullanılan hello MSONLINE modülünden Mars AgentInstaller hello yükleme işleminin bir parçası olarak eklenen hangi hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="762ad-176">This, and other cmdlets used for backup, are from hello MSONLINE module which hello Mars AgentInstaller added as part of hello installation process.</span></span> 

<span data-ttu-id="762ad-177">Merhaba aracı yükleyici hello $Env güncelleştirmez: PSModulePath değişkeni.</span><span class="sxs-lookup"><span data-stu-id="762ad-177">hello Agent installer does not update hello $Env:PSModulePath variable.</span></span> <span data-ttu-id="762ad-178">Bu modül otomatik-yüklemesi başarısız anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="762ad-178">This means module auto-load fails.</span></span> <span data-ttu-id="762ad-179">tooresolve bu yapabilirsiniz hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="762ad-179">tooresolve this you can do hello following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="762ad-180">Alternatif olarak, el ile hello modülü betiğinizde şu şekilde yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="762ad-180">Alternatively, you can manually load hello module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="762ad-181">Merhaba çevrimiçi yedekleme cmdlet'leri yük sonra hello kasa kimlik bilgilerini Kaydet:</span><span class="sxs-lookup"><span data-stu-id="762ad-181">Once you load hello Online Backup cmdlets, you register hello vault credentials:</span></span>


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="762ad-182">Göreli yollar toospecify hello kasa kimlik bilgileri dosyası kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="762ad-182">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="762ad-183">Bir giriş toohello cmdlet'ini olarak mutlak bir yol sağlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="762ad-183">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="762ad-184">Ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="762ad-184">Networking settings</span></span>
<span data-ttu-id="762ad-185">Internet proxy sunucu üzerinden gerçekleşir toohello Windows hello Hello bağlantısını makine olduğunda hello proxy ayarlarını toohello aracı da sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="762ad-185">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="762ad-186">Bu örnekte, olmadığından hiçbir Ara sunucunun biz açıkça herhangi bir proxy ile ilgili bilgi temizleme.</span><span class="sxs-lookup"><span data-stu-id="762ad-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="762ad-187">Bant genişliği kullanımı ile Merhaba seçenekleri de denetlenebilir ```work hour bandwidth``` ve ```non-work hour bandwidth``` hello haftanın belirli bir dizi için.</span><span class="sxs-lookup"><span data-stu-id="762ad-187">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="762ad-188">Ayar Hello proxy ve bant genişliği ayrıntıları yapılır hello kullanarak [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="762ad-188">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="762ad-189">Şifreleme ayarları</span><span class="sxs-lookup"><span data-stu-id="762ad-189">Encryption settings</span></span>
<span data-ttu-id="762ad-190">Merhaba gönderilen yedekleme verileri tooAzure yedekleme şifrelenmiş tooprotect hello hello veri gizliliğini ' dir.</span><span class="sxs-lookup"><span data-stu-id="762ad-190">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="762ad-191">Merhaba şifreleme parolası hello "parola" toodecrypt hello geri yükleme hello aynı anda verilerdir.</span><span class="sxs-lookup"><span data-stu-id="762ad-191">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="762ad-192">Ayarlandıktan sonra hello parola bilgilerini güvenli ve güvenli tutar.</span><span class="sxs-lookup"><span data-stu-id="762ad-192">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="762ad-193">Olan değil siz bu parolayı olmadan Azure mümkün toorestore verileri.</span><span class="sxs-lookup"><span data-stu-id="762ad-193">You are not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="762ad-194">Dosya ve klasörleri yedekleme</span><span class="sxs-lookup"><span data-stu-id="762ad-194">Back up files and folders</span></span>
<span data-ttu-id="762ad-195">Windows sunucularını ve istemcilerini tooAzure yedekleme tüm yedeklemeleri bir ilke tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="762ad-195">All backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="762ad-196">Hello İlkesi üç bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="762ad-196">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="762ad-197">A **yedekleme zamanlaması** yedeklemeler alınır ve hello hizmeti ile eşitlenmiş toobe gerektiğinde belirtir.</span><span class="sxs-lookup"><span data-stu-id="762ad-197">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="762ad-198">A **bekletme zamanlaması** Azure'da ne kadar süreyle tooretain hello kurtarma noktaları belirtir.</span><span class="sxs-lookup"><span data-stu-id="762ad-198">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="762ad-199">A **dosya ekleme/çıkarma belirtimi** belirleyen ne yedeklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="762ad-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="762ad-200">Yedekleme, otomatikleştirme beri bu belgede, hiçbir şey yapılandırılmış varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="762ad-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="762ad-201">Hello kullanarak yeni bir yedekleme ilkesi oluşturarak başlayın [yeni OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="762ad-201">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="762ad-202">Bu zaman hello İlkesi boş olduğunu ve diğer cmdlet'ler gerekli toodefine ne öğeleri dahil etmek veya hariç, yedeklemeler çalışacak ve burada hello yedeklemeleri depolanacak.</span><span class="sxs-lookup"><span data-stu-id="762ad-202">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="762ad-203">Merhaba yedekleme zamanlamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="762ad-203">Configuring hello backup schedule</span></span>
<span data-ttu-id="762ad-204">ilk Merhaba hello İlkesi 3 bölümleri hale hello kullanılarak oluşturulan hello yedekleme zamanlaması [yeni OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="762ad-204">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="762ad-205">Merhaba yedekleme zamanlaması yedeklemeleri gerçekleştirilecek toobe gerektiğinde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="762ad-205">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="762ad-206">Bir zamanlama oluştururken toospecify 2 giriş parametreleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="762ad-206">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="762ad-207">**Merhaba haftanın günlerini** hello yedekleme çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="762ad-207">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="762ad-208">Merhaba yedekleme işi yalnızca bir gün veya her gün hello haftanın veya arasındaki herhangi bir birleşimini çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="762ad-208">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="762ad-209">**Merhaba saatlerinde** hello yedekleme ne zaman çalışmalı.</span><span class="sxs-lookup"><span data-stu-id="762ad-209">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="762ad-210">Too3 hello yedekleme harekete geçirildiğinde hello günün farklı saatlerinde tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="762ad-210">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="762ad-211">Örneğin, 4'e her Cumartesi ve Pazar çalışan bir yedekleme ilkesi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="762ad-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="762ad-212">Merhaba yedekleme zamanlaması bir ilkeyle ilişkilendirilmiş toobe gerekir ve bu hello kullanarak elde [kümesi OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="762ad-212">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="762ad-213">Bir bekletme ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="762ad-213">Configuring a retention policy</span></span>
<span data-ttu-id="762ad-214">Merhaba Bekletme İlkesi yedekleme işlerini oluşturulan noktaları korunur ne kadar süreyle kurtarma tanımlar.</span><span class="sxs-lookup"><span data-stu-id="762ad-214">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="762ad-215">Hello kullanarak yeni bir bekletme ilkesi oluşturulurken [yeni OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet'ini hello yedekleme kurtarma noktalarının hello gün sayısı gereken Azure yedekleme ile korunduğunu toobe belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="762ad-215">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="762ad-216">Aşağıdaki Hello örnek bir bekletme ilkesi 7 gün olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="762ad-216">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="762ad-217">Merhaba bekletme ilkesi hello cmdlet'ini kullanarak hello ana ilkesiyle ilişkili olmalıdır [kümesi OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="762ad-217">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="762ad-218">Yedeklenen dosyaları toobe hariç ve dahil</span><span class="sxs-lookup"><span data-stu-id="762ad-218">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="762ad-219">Bir ```OBFileSpec``` nesnesi eklenen ve bir yedek dışlanan hello dosyaları toobe tanımlar.</span><span class="sxs-lookup"><span data-stu-id="762ad-219">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="762ad-220">Bu bir kapsam hello çıkışı dosya ve klasörlerin bir makinede korumalı kurallar kümesidir.</span><span class="sxs-lookup"><span data-stu-id="762ad-220">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="762ad-221">Birçok ekleme veya hariç tutma kuralları gerektiği gibi dosya ve bir ilke ile ilişkilendirmek gibi sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="762ad-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="762ad-222">Yeni bir OBFileSpec nesnesi oluştururken şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="762ad-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="762ad-223">Merhaba dosya ve klasörleri toobe dahil belirtin</span><span class="sxs-lookup"><span data-stu-id="762ad-223">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="762ad-224">Dışlanan dosya ve klasörleri toobe hello belirtin</span><span class="sxs-lookup"><span data-stu-id="762ad-224">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="762ad-225">Özyinelemeli bir klasör (veya) olup yalnızca üst düzey dosyalarında hello belirtilen klasör hello yedeklenmelidir verilerin yedeğini yukarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="762ad-225">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="762ad-226">Merhaba ikinci hello yeni OBFileSpec komutta hello - özyinelemesiz bayrağı kullanılarak elde edilir.</span><span class="sxs-lookup"><span data-stu-id="762ad-226">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="762ad-227">Merhaba aşağıdaki örnekte, biz birimi yedekleyin C: ve D: ve hello OS ikili hello Windows klasöründeki ve herhangi bir geçici klasörde dosyaları hariç.</span><span class="sxs-lookup"><span data-stu-id="762ad-227">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="762ad-228">hello kullanarak iki dosya belirtimleri oluşturacağız şekilde toodo [yeni OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - eklenmesi, diğeri dışarıda bırakma için.</span><span class="sxs-lookup"><span data-stu-id="762ad-228">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="762ad-229">Merhaba Dosya belirtimleri oluşturduktan sonra hello kullanarak hello İlkesi ile ilişkili [Ekle OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="762ad-229">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="762ad-230">Hello İlkesi uygulama</span><span class="sxs-lookup"><span data-stu-id="762ad-230">Applying hello policy</span></span>
<span data-ttu-id="762ad-231">Şimdi hello İlkesi tamamlandıktan ve ilişkili bir yedekleme zamanlaması, bekletme ilkesi ve dosyaların bir ekleme/çıkarma listesi vardır.</span><span class="sxs-lookup"><span data-stu-id="762ad-231">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="762ad-232">Bu ilkeyi şimdi için Azure Backup toouse kaydedilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="762ad-232">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="762ad-233">İlke, yeni oluşturulan hello uygulamadan önce mevcut hiçbir yedekleme ilkeleri hello kullanarak hello sunucuyla ilişkili olduğundan emin olun [Kaldır OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="762ad-233">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="762ad-234">Hello ilkesi kaldırma için onay ister.</span><span class="sxs-lookup"><span data-stu-id="762ad-234">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="762ad-235">tooskip hello onay kullanmak hello ```-Confirm:$false``` hello cmdlet ile bayrağı.</span><span class="sxs-lookup"><span data-stu-id="762ad-235">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="762ad-236">Uygulanıyor hello İlkesi yapılır hello kullanarak [kümesi OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="762ad-236">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="762ad-237">Bu ayrıca onaylamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="762ad-237">This will also ask for confirmation.</span></span> <span data-ttu-id="762ad-238">tooskip hello onay kullanmak hello ```-Confirm:$false``` hello cmdlet ile bayrağı.</span><span class="sxs-lookup"><span data-stu-id="762ad-238">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
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

<span data-ttu-id="762ad-239">Hello kullanarak hello mevcut bir yedekleme İlkesi hello ayrıntılarını görüntüleyebilirsiniz [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="762ad-239">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="762ad-240">Daha fazla hello kullanarak ayrıntıya [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet'i hello yedekleme zamanlamasını ve hello için [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) hello bekletme ilkeleri için cmdlet</span><span class="sxs-lookup"><span data-stu-id="762ad-240">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="762ad-241">Bir geçici yedekleme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="762ad-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="762ad-242">Bir yedekleme İlkesi ayarladıktan sonra hello yedeklemeleri hello zamanlama meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="762ad-242">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="762ad-243">Bir geçici yedekleme tetikleme ayrıca hello kullanarak olası [başlangıç OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="762ad-243">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="762ad-244">Verileri Azure yedekten geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="762ad-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="762ad-245">Bu bölümde, veri kurtarma Azure Backup otomatikleştirmek için hello adımlarında size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="762ad-245">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="762ad-246">Bunu yapmak, böylece hello aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="762ad-246">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="762ad-247">Merhaba kaynak birimi seçin</span><span class="sxs-lookup"><span data-stu-id="762ad-247">Pick hello source volume</span></span>
2. <span data-ttu-id="762ad-248">Bir yedekleme noktası toorestore seçin</span><span class="sxs-lookup"><span data-stu-id="762ad-248">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="762ad-249">Bir öğe toorestore seçin</span><span class="sxs-lookup"><span data-stu-id="762ad-249">Choose an item toorestore</span></span>
4. <span data-ttu-id="762ad-250">Tetikleyici hello geri yükleme işlemi</span><span class="sxs-lookup"><span data-stu-id="762ad-250">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="762ad-251">Çekme hello kaynak birim</span><span class="sxs-lookup"><span data-stu-id="762ad-251">Picking hello source volume</span></span>
<span data-ttu-id="762ad-252">Sipariş toorestore öğeyi Azure Backup'da, ilk tooidentify hello kaynak hello öğesinin gerekir.</span><span class="sxs-lookup"><span data-stu-id="762ad-252">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="762ad-253">Biz hello bağlamında bir Windows Server veya Windows İstemcisi hello komutları yürütülürken bu yana hello makine zaten tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="762ad-253">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="762ad-254">Merhaba kaynağı tanımlayan bir hello sonraki adım içeren tooidentify hello birimdir.</span><span class="sxs-lookup"><span data-stu-id="762ad-254">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="762ad-255">Bu makineden yedeklenen alınabilir hello yürüterek birimleri veya kaynakları listesini [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="762ad-255">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="762ad-256">Bu komut, bu sunucu/istemciden yedeklenen tüm hello kaynakları bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="762ad-256">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-from-which-toorestore"></a><span data-ttu-id="762ad-257">Hangi toorestore bir yedekleme noktasının seçme</span><span class="sxs-lookup"><span data-stu-id="762ad-257">Choosing a backup point from which toorestore</span></span>
<span data-ttu-id="762ad-258">Merhaba çalıştırarak yedekleme noktalarının bir listesini alma [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) uygun parametreleri cmdlet'iyle.</span><span class="sxs-lookup"><span data-stu-id="762ad-258">You retreive a list of backup points by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="762ad-259">Bizim örneğimizde, son yedekleme noktası hello kaynak birim hello seçeceğiz *D:* ve toorecover belirli bir dosya kullanın.</span><span class="sxs-lookup"><span data-stu-id="762ad-259">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="762ad-260">Merhaba nesne ```$rps``` yedekleme noktaları dizisidir.</span><span class="sxs-lookup"><span data-stu-id="762ad-260">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="762ad-261">Hello ilk öğe hello son noktası ve hello n. öğeyi hello eski noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="762ad-261">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="762ad-262">kullanacağız toochoose hello son noktası, ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="762ad-262">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="762ad-263">Bir öğe toorestore seçme</span><span class="sxs-lookup"><span data-stu-id="762ad-263">Choosing an item toorestore</span></span>
<span data-ttu-id="762ad-264">tooidentify hello tam dosya veya klasör toorestore, yinelemeli olarak kullanın hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="762ad-264">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="762ad-265">Bu şekilde hello klasör hiyerarşisini yalnızca hello kullanarak gözatılabilir ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="762ad-265">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="762ad-266">Bu örnekte, biz toorestore hello dosyanın istiyorsanız *finances.xls* Biz bu kullanarak başvuru hello nesne ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="762ad-266">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="762ad-267">Hello kullanarak öğeleri toorestore için arama yapabilirsiniz ```Get-OBRecoverableItem``` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="762ad-267">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="762ad-268">Örneğimizde, toosearch için *finances.xls* biz şu komutu çalıştırarak hello dosyada bir tanıtıcı alabilir:</span><span class="sxs-lookup"><span data-stu-id="762ad-268">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="762ad-269">Merhaba geri yükleme işlemini tetikler</span><span class="sxs-lookup"><span data-stu-id="762ad-269">Triggering hello restore process</span></span>
<span data-ttu-id="762ad-270">tootrigger hello geri yükleme işlemi, ilk toospecify hello kurtarma seçenekleri ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="762ad-270">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="762ad-271">Bu hello kullanarak yapılabilir [yeni OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="762ad-271">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="762ad-272">Bu örnek, toorestore hello dosyaları çok istediğimizi varsayalım*C:\temp*. Ayrıca hello hedef klasörü zaten mevcut dosyalarda tooskip istiyoruz varsayalım *C:\temp*. toocreate böyle bir kurtarma seçeneği, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="762ad-272">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="762ad-273">Hello kullanarak hello geri yükleme işlemi şimdi tetikleyebilir [başlangıç OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) seçili hello komutunu ```$item``` hello hello çıktısından ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="762ad-273">Now trigger hello restore process by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="762ad-274">Hello Azure Backup aracısını kaldırma</span><span class="sxs-lookup"><span data-stu-id="762ad-274">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="762ad-275">Kaldırma hello Azure Yedekleme aracısı, komutu aşağıdaki hello kullanarak gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="762ad-275">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="762ad-276">Merhaba Aracısı ikili dosyalarının hello makineden kaldırma bazı sonuçları tooconsider sahiptir:</span><span class="sxs-lookup"><span data-stu-id="762ad-276">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="762ad-277">Merhaba dosya filtresi hello makineden kaldırır ve değişiklikleri izleme durduruldu.</span><span class="sxs-lookup"><span data-stu-id="762ad-277">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="762ad-278">Tüm ilke bilgilerine hello makineden kaldırıldı, ancak hello ilkesi bilgileri hello hizmetinde depolanan toobe devam eder.</span><span class="sxs-lookup"><span data-stu-id="762ad-278">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="762ad-279">Tüm yedekleme zamanlamaları kaldırılır ve daha fazla yedekleme alınır.</span><span class="sxs-lookup"><span data-stu-id="762ad-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="762ad-280">Ancak, Azure kalırken depolanan verileri hello ve hello bekletme ilkesi Kurulum göredir, tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="762ad-280">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="762ad-281">Eski noktalarını otomatik olarak eski.</span><span class="sxs-lookup"><span data-stu-id="762ad-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="762ad-282">Uzaktan Yönetim</span><span class="sxs-lookup"><span data-stu-id="762ad-282">Remote management</span></span>
<span data-ttu-id="762ad-283">Tüm hello yönetim hello Azure Yedekleme aracısı, ilkeler ve veri kaynakları çevresinde uzaktan PowerShell aracılığıyla gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="762ad-283">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="762ad-284">Uzaktan yönetilecek hello makine doğru şekilde hazırlanmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="762ad-284">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="762ad-285">Varsayılan olarak, hello WinRM hizmeti el ile başlatma için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="762ad-285">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="762ad-286">Merhaba başlangıç türü çok ayarlanmalıdır*otomatik* ve hello hizmet başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="762ad-286">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="762ad-287">WinRM hizmeti hello tooverify çalıştığından, hello Status özelliği hello değeri olmalıdır *çalıştıran*.</span><span class="sxs-lookup"><span data-stu-id="762ad-287">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="762ad-288">PowerShell uzaktan iletişim için yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="762ad-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="762ad-289">Merhaba makine artık uzaktan - hello hello aracı yüklemesinden başlatma yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="762ad-289">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="762ad-290">Örneğin, komut dosyası izleyen hello hello aracı toohello uzak makine kopyalar ve onu yükler.</span><span class="sxs-lookup"><span data-stu-id="762ad-290">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="762ad-291">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="762ad-291">Next steps</span></span>
<span data-ttu-id="762ad-292">Azure yedekleme için Windows Server/istemcisi bakın hakkında daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="762ad-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="762ad-293">Giriş tooAzure yedekleme</span><span class="sxs-lookup"><span data-stu-id="762ad-293">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="762ad-294">Windows sunucularını yedekleme</span><span class="sxs-lookup"><span data-stu-id="762ad-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
