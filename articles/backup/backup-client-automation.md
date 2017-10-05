---
title: "Azure için Windows Server'ı Yedekle için PowerShell kullanma | Microsoft Docs"
description: "Dağıtma ve Azure PowerShell kullanarak yedekleme yönetme hakkında bilgi edinin"
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
ms.openlocfilehash: d3f165c749af0553c4918b33b0d24cc1e21af2a9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="2c343-103">PowerShell kullanarak Windows Server/Windows İstemcisi için Azure’a yedekleme dağıtma ve yönetme</span><span class="sxs-lookup"><span data-stu-id="2c343-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c343-104">ARM</span><span class="sxs-lookup"><span data-stu-id="2c343-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="2c343-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="2c343-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="2c343-106">Bu makalede Azure yedekleme Windows Server veya Windows İstemcisi ayarlama ve yedekleme ve kurtarma yönetmek için PowerShell kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="2c343-106">This article shows you how to use PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="2c343-107">Azure PowerShell'i yükleme</span><span class="sxs-lookup"><span data-stu-id="2c343-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="2c343-108">Bu makalede Azure Resource Manager (ARM) ve bir kaynak grubu bir kurtarma Hizmetleri kasası kullanmanızı sağlamak MS çevrimiçi yedekleme PowerShell cmdlet'leri odaklanır.</span><span class="sxs-lookup"><span data-stu-id="2c343-108">This article focuses on the Azure Resource Manager (ARM) and the MS Online Backup PowerShell cmdlets that enable you to use a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="2c343-109">Azure PowerShell 1.0 Ekim 2015'te yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2c343-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="2c343-110">Bu sürüm 0.9.8 başarılı bir şekilde serbest bırakır ve bazı önemli değişiklikler hakkında özellikle cmdlet'leri adlandırma desenini getirildi.</span><span class="sxs-lookup"><span data-stu-id="2c343-110">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="2c343-111">1.0 cmdlet'leri {fiil}-AzureRm{isim} adlandırma desenini izler; Buna karşın, 0.9.8 adlarında **Rm** bulunmaz (örneğin, New- AzureResourceGroup yerine New-AzureRmResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="2c343-111">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="2c343-112">Azure PowerShell 0.9.8 kullanıldığında, önce **Switch-AzureMode AzureResourceManager** komutunu çalıştırarak Resource Manager modunu etkinleştirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="2c343-112">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="2c343-113">Bu komut 1.0 veya üstü gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="2c343-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="2c343-114">0.9.8 için yazılan komut dosyalarınızı kullanmak isteyip istemediğinizi ortamında 1.0 veya üstü ortamı dikkatlice güncelleştirmek ve komut dosyalarını üretimde beklenmeyen etkiyi önlemek için kullanmadan önce bir ön üretim ortamında test.</span><span class="sxs-lookup"><span data-stu-id="2c343-114">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully update and test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="2c343-115">[En son PowerShell sürümü indirme](https://github.com/Azure/azure-powershell/releases) (gerekli minimum sürüm: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="2c343-115">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="2c343-116">Kurtarma hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c343-116">Create a recovery services vault</span></span>
<span data-ttu-id="2c343-117">Aşağıdaki adımlar bir kurtarma Hizmetleri kasası oluşturmada size yol açar.</span><span class="sxs-lookup"><span data-stu-id="2c343-117">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="2c343-118">Kurtarma Hizmetleri kasasına yedekleme Kasası ' farklıdır.</span><span class="sxs-lookup"><span data-stu-id="2c343-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="2c343-119">Azure Backup ilk kez kullanıyorsanız, kullanmalısınız **Register-AzureRMResourceProvider** aboneliğinizle Azure Recovery hizmeti sağlayıcısını kaydetmek için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2c343-119">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="2c343-120">Kurtarma Hizmetleri kasası bir ARM kaynak olduğundan, bir kaynak grubu içindeki yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c343-120">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="2c343-121">Varolan bir kaynak grubunu kullanın veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c343-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="2c343-122">Yeni bir kaynak grubu oluştururken, ad ve kaynak grubu için konum belirtin.</span><span class="sxs-lookup"><span data-stu-id="2c343-122">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="2c343-123">Kullanım **yeni AzureRmRecoveryServicesVault** yeni kasası oluşturmak için cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2c343-123">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create the new vault.</span></span> <span data-ttu-id="2c343-124">Kaynak grubu için kullanılan kasa için aynı konumu belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="2c343-124">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="2c343-125">Kullanılacak depolama artıklığı türünü belirtin; kullanabileceğiniz [yerel olarak yedekli depolama (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) veya [coğrafi olarak yedekli depolama (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="2c343-125">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="2c343-126">Aşağıdaki örnek, testVault - BackupStorageRedundancy seçeneği GeoRedundant için ayarlanmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="2c343-126">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="2c343-127">Çok sayıda Azure yedekleme cmdlet'lerini girdi olarak kurtarma Hizmetleri kasası nesnesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2c343-127">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="2c343-128">Bu nedenle, bir değişkende yedekleme kurtarma Hizmetleri kasası nesne depolamak uygundur.</span><span class="sxs-lookup"><span data-stu-id="2c343-128">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="2c343-129">Bir abonelikte kasalarını görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="2c343-129">View the vaults in a subscription</span></span>
<span data-ttu-id="2c343-130">Kullanım **Get-AzureRmRecoveryServicesVault** geçerli abonelikte tüm kasalarının listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="2c343-130">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="2c343-131">Bu komut, yeni bir kasa oluşturulduğunu denetleyin veya hangi kasalarını abonelikte bulunan görmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c343-131">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="2c343-132">Komutu çalıştırmak **Get-AzureRmRecoveryServicesVault**, ve Abonelikteki tüm kasalarını listelenir.</span><span class="sxs-lookup"><span data-stu-id="2c343-132">Run the command, **Get-AzureRmRecoveryServicesVault**, and all vaults in the subscription are listed.</span></span>

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


## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="2c343-133">Azure Backup aracısını yükleme</span><span class="sxs-lookup"><span data-stu-id="2c343-133">Installing the Azure Backup agent</span></span>
<span data-ttu-id="2c343-134">Azure Backup aracısını yüklemeden önce Windows Server yükleyici indirildi ve mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c343-134">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="2c343-135">Yükleyicisi'nden en son sürümünü almak [Microsoft Download Center](http://aka.ms/azurebackup_agent) veya kurtarma Hizmetleri Kasası'nın Pano sayfası.</span><span class="sxs-lookup"><span data-stu-id="2c343-135">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="2c343-136">Yükleyici gibi kolay erişilebilir bir konuma kaydedin * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="2c343-136">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="2c343-137">Alternatif olarak, yükleyici almak için PowerShell kullanın:</span><span class="sxs-lookup"><span data-stu-id="2c343-137">Alternatively, use PowerShell to get the downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="2c343-138">Aracıyı yüklemek için yükseltilmiş bir PowerShell konsolunda aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2c343-138">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="2c343-139">Bu, tüm varsayılan seçeneklerle Aracısı'nı yükler.</span><span class="sxs-lookup"><span data-stu-id="2c343-139">This installs the agent with all the default options.</span></span> <span data-ttu-id="2c343-140">Yükleme arka planda birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="2c343-140">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="2c343-141">Belirtmezseniz, */nu* seçeneği sonra **Windows Update** tüm güncelleştirmeleri denetlemek için yükleme işleminin sonunda penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="2c343-141">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="2c343-142">Yüklendikten sonra aracı yüklü programlar listesinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="2c343-142">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="2c343-143">Yüklü programların listesini görmek için şu adrese gidin **Denetim Masası** > **programları** > **programlar ve Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="2c343-143">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Yüklü aracı](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="2c343-145">Yükleme Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="2c343-145">Installation options</span></span>
<span data-ttu-id="2c343-146">Komut satırı kullanılabilir tüm seçenekleri görmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="2c343-146">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="2c343-147">Mevcut seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2c343-147">The available options include:</span></span>

| <span data-ttu-id="2c343-148">Seçenek</span><span class="sxs-lookup"><span data-stu-id="2c343-148">Option</span></span> | <span data-ttu-id="2c343-149">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="2c343-149">Details</span></span> | <span data-ttu-id="2c343-150">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="2c343-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2c343-151">/q</span><span class="sxs-lookup"><span data-stu-id="2c343-151">/q</span></span> |<span data-ttu-id="2c343-152">Sessiz yükleme</span><span class="sxs-lookup"><span data-stu-id="2c343-152">Quiet installation</span></span> |- |
| <span data-ttu-id="2c343-153">p: "Konum"</span><span class="sxs-lookup"><span data-stu-id="2c343-153">/p:"location"</span></span> |<span data-ttu-id="2c343-154">Azure Backup Aracısı yükleme klasörünün yolu.</span><span class="sxs-lookup"><span data-stu-id="2c343-154">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="2c343-155">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Aracısı</span><span class="sxs-lookup"><span data-stu-id="2c343-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="2c343-156">/ s: "Konum"</span><span class="sxs-lookup"><span data-stu-id="2c343-156">/s:"location"</span></span> |<span data-ttu-id="2c343-157">Azure Backup aracısı için önbellek klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="2c343-157">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="2c343-158">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="2c343-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="2c343-159">/m</span><span class="sxs-lookup"><span data-stu-id="2c343-159">/m</span></span> |<span data-ttu-id="2c343-160">Microsoft Update'e kabulü</span><span class="sxs-lookup"><span data-stu-id="2c343-160">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="2c343-161">/nu</span><span class="sxs-lookup"><span data-stu-id="2c343-161">/nu</span></span> |<span data-ttu-id="2c343-162">Yükleme tamamlandıktan sonra güncelleştirmeleri denetleme</span><span class="sxs-lookup"><span data-stu-id="2c343-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="2c343-163">/d</span><span class="sxs-lookup"><span data-stu-id="2c343-163">/d</span></span> |<span data-ttu-id="2c343-164">Microsoft Azure kurtarma Hizmetleri Aracısı kaldırır</span><span class="sxs-lookup"><span data-stu-id="2c343-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="2c343-165">/ph</span><span class="sxs-lookup"><span data-stu-id="2c343-165">/ph</span></span> |<span data-ttu-id="2c343-166">Proxy konağı adresi</span><span class="sxs-lookup"><span data-stu-id="2c343-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="2c343-167">/PO</span><span class="sxs-lookup"><span data-stu-id="2c343-167">/po</span></span> |<span data-ttu-id="2c343-168">Proxy ana bilgisayar bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="2c343-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="2c343-169">/PU</span><span class="sxs-lookup"><span data-stu-id="2c343-169">/pu</span></span> |<span data-ttu-id="2c343-170">Proxy konağı kullanıcı</span><span class="sxs-lookup"><span data-stu-id="2c343-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="2c343-171">/pw</span><span class="sxs-lookup"><span data-stu-id="2c343-171">/pw</span></span> |<span data-ttu-id="2c343-172">Proxy parolası</span><span class="sxs-lookup"><span data-stu-id="2c343-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-to-a-recovery-services-vault"></a><span data-ttu-id="2c343-173">Windows Server veya Windows istemci makinesi bir kurtarma Hizmetleri kasasına kaydetme</span><span class="sxs-lookup"><span data-stu-id="2c343-173">Registering Windows Server or Windows client machine to a Recovery Services Vault</span></span>
<span data-ttu-id="2c343-174">Kurtarma Hizmetleri kasası oluşturduktan sonra en son aracı ve kasa kimlik bilgilerini indirin ve C:\Downloads gibi uygun bir konumda saklayın.</span><span class="sxs-lookup"><span data-stu-id="2c343-174">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="2c343-175">Windows Server veya Windows istemci makinesi üzerinde çalıştırmak [başlangıç OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) makine kasaya kaydetmek için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2c343-175">On the Windows Server or Windows client machine, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>
<span data-ttu-id="2c343-176">Bu ve diğer cmdlet'leri yedekleme için kullanılan Mars AgentInstaller yükleme işleminin bir parçası olarak eklenen MSONLINE modülü arasındadır.</span><span class="sxs-lookup"><span data-stu-id="2c343-176">This, and other cmdlets used for backup, are from the MSONLINE module which the Mars AgentInstaller added as part of the installation process.</span></span> 

<span data-ttu-id="2c343-177">Aracı yükleyici $Env güncelleştirmez: PSModulePath değişkeni.</span><span class="sxs-lookup"><span data-stu-id="2c343-177">The Agent installer does not update the $Env:PSModulePath variable.</span></span> <span data-ttu-id="2c343-178">Bu modül otomatik-yüklemesi başarısız anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2c343-178">This means module auto-load fails.</span></span> <span data-ttu-id="2c343-179">Bu sorunu çözmek için aşağıdakileri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2c343-179">To resolve this you can do the following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="2c343-180">Alternatif olarak, el ile modülü betiğinizde şu şekilde yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2c343-180">Alternatively, you can manually load the module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="2c343-181">Çevrimiçi Yedekleme cmdlet'leri yükledikten sonra kasa kimlik bilgilerini Kaydet:</span><span class="sxs-lookup"><span data-stu-id="2c343-181">Once you load the Online Backup cmdlets, you register the vault credentials:</span></span>


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
> <span data-ttu-id="2c343-182">Kasa kimlik bilgileri dosyası belirtmek için göreli yolların kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2c343-182">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="2c343-183">Cmdlet'i bir girdi olarak mutlak bir yol sağlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="2c343-183">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="2c343-184">Ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="2c343-184">Networking settings</span></span>
<span data-ttu-id="2c343-185">Windows makine internet bağlantısını bir proxy sunucu üzerinden olduğunda, proxy ayarlarını aracıya de girilebilir.</span><span class="sxs-lookup"><span data-stu-id="2c343-185">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="2c343-186">Bu örnekte, olmadığından hiçbir Ara sunucunun biz açıkça herhangi bir proxy ile ilgili bilgi temizleme.</span><span class="sxs-lookup"><span data-stu-id="2c343-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="2c343-187">Bant genişliği kullanımı seçeneklerle da denetlenebilir ```work hour bandwidth``` ve ```non-work hour bandwidth``` haftanın belirli bir dizi için.</span><span class="sxs-lookup"><span data-stu-id="2c343-187">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="2c343-188">Proxy ve bant ayrıntılarını ayarlama yapılır kullanarak [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2c343-188">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="2c343-189">Şifreleme ayarları</span><span class="sxs-lookup"><span data-stu-id="2c343-189">Encryption settings</span></span>
<span data-ttu-id="2c343-190">Yedekleme verilerini Azure Backup için gönderilen veri gizliliğini korumak için şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="2c343-190">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="2c343-191">Şifreleme Parolası "geri yükleme sırasındaki verileri şifrelemek için parola" dir.</span><span class="sxs-lookup"><span data-stu-id="2c343-191">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="2c343-192">Ayarlandıktan sonra parola bilgilerini güvenli ve güvenli tutar.</span><span class="sxs-lookup"><span data-stu-id="2c343-192">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="2c343-193">Olan değil veri bu parolayı Azure'dan geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c343-193">You are not be able to restore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="2c343-194">Dosya ve klasörleri yedekleme</span><span class="sxs-lookup"><span data-stu-id="2c343-194">Back up files and folders</span></span>
<span data-ttu-id="2c343-195">Windows sunucularını ve istemcilerini tüm yedeklemeleri Azure yedekleme için bir ilke tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="2c343-195">All backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="2c343-196">İlke üç bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="2c343-196">The policy comprises three parts:</span></span>

1. <span data-ttu-id="2c343-197">A **yedekleme zamanlaması** yedeklemeler alınır ve hizmeti ile eşitlenmiş gerektiğinde belirtir.</span><span class="sxs-lookup"><span data-stu-id="2c343-197">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="2c343-198">A **bekletme zamanlaması** belirleyen ne kadar süreyle Azure kurtarma noktalarını korumak için.</span><span class="sxs-lookup"><span data-stu-id="2c343-198">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="2c343-199">A **dosya ekleme/çıkarma belirtimi** belirleyen ne yedeklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="2c343-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="2c343-200">Yedekleme, otomatikleştirme beri bu belgede, hiçbir şey yapılandırılmış varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="2c343-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="2c343-201">Kullanarak yeni bir yedekleme ilkesi oluşturarak başlayın [yeni OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2c343-201">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="2c343-202">İlke şu anda boş olur ve diğer cmdlet'ler öğeleri tanımlamak için kapsanan veya dışlanan, ne zaman yedeklemeleri çalışacağını ve yedeklemeleri depolanacak burada.</span><span class="sxs-lookup"><span data-stu-id="2c343-202">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="2c343-203">Yedekleme zamanlamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2c343-203">Configuring the backup schedule</span></span>
<span data-ttu-id="2c343-204">Bir ilke 3 bölümlerinin ilk kullanılarak oluşturulan yedekleme zamanlaması olan [yeni OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2c343-204">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="2c343-205">Yedekleme zamanlaması yedeklemeleri yapılması gerektiğinde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2c343-205">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="2c343-206">Bir zamanlama oluştururken 2 giriş parametreleri belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="2c343-206">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="2c343-207">**Haftanın günleri** , yedekleme çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c343-207">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="2c343-208">Yedekleme işi yalnızca bir gün veya haftanın her gün veya arasındaki herhangi bir birleşimini çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c343-208">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="2c343-209">**Günün kez** yedeklemenin ne zaman çalışmalı.</span><span class="sxs-lookup"><span data-stu-id="2c343-209">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="2c343-210">Yedekleme harekete geçirildiğinde günün en fazla 3 farklı saatleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c343-210">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="2c343-211">Örneğin, 4'e her Cumartesi ve Pazar çalışan bir yedekleme ilkesi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c343-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="2c343-212">Yedekleme zamanlaması bir ilkesiyle ilişkilendirilmesi gerekir ve bu kullanarak elde [kümesi OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2c343-212">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="2c343-213">Bir bekletme ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2c343-213">Configuring a retention policy</span></span>
<span data-ttu-id="2c343-214">Bekletme İlkesi yedekleme işlerini oluşturulan kurtarma noktaları ne kadar süreyle saklanacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2c343-214">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="2c343-215">Kullanarak yeni bir bekletme ilkesi oluşturulurken [yeni OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, yedekleme kurtarma noktalarının Azure yedekleme ile korunması gereken gün sayısını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c343-215">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="2c343-216">Aşağıdaki örnek bir bekletme ilkesi 7 gün olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2c343-216">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="2c343-217">Bekletme İlkesi cmdlet'ini kullanarak ana ilkesiyle ilişkili olmalıdır [kümesi OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="2c343-217">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="2c343-218">Dahil ve yedeklenecek dosyaları dışlama</span><span class="sxs-lookup"><span data-stu-id="2c343-218">Including and excluding files to be backed up</span></span>
<span data-ttu-id="2c343-219">Bir ```OBFileSpec``` nesnesi bulunan ve bir yedek dışlanan dosyaları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2c343-219">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="2c343-220">Bu, korumalı dosyaları ve klasörleri bir makinede kullanıma kapsam kurallar kümesidir.</span><span class="sxs-lookup"><span data-stu-id="2c343-220">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="2c343-221">Birçok ekleme veya hariç tutma kuralları gerektiği gibi dosya ve bir ilke ile ilişkilendirmek gibi sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="2c343-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="2c343-222">Yeni bir OBFileSpec nesnesi oluştururken şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2c343-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="2c343-223">Dosyaları ve dahil edilecek klasörleri belirtin</span><span class="sxs-lookup"><span data-stu-id="2c343-223">Specify the files and folders to be included</span></span>
* <span data-ttu-id="2c343-224">Dosya ve klasörleri dışarıda belirtin</span><span class="sxs-lookup"><span data-stu-id="2c343-224">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="2c343-225">Özyinelemeli bir klasör (veya) olup yalnızca üst düzey dosyaları belirtilen klasöre yedeklenmelidir verilerin yedeğini yukarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="2c343-225">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="2c343-226">İkinci yeni OBFileSpec komutta - özyinelemesiz bayrağı kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="2c343-226">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="2c343-227">Aşağıdaki örnekte, biz birimi yedekleyin C: ve D: ve işletim sistemi ikili dosyaları Windows klasöründeki ve geçici klasörleri dışarıda.</span><span class="sxs-lookup"><span data-stu-id="2c343-227">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="2c343-228">Oluşturacağız Bunu yapmak için iki belirtimleri kullanarak dosya [yeni OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - eklenmesi, diğeri dışarıda bırakma için.</span><span class="sxs-lookup"><span data-stu-id="2c343-228">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="2c343-229">Dosya belirtimleri oluşturduktan sonra ilkeyi kullanarak ilişkili oldukları [Ekle OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2c343-229">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-the-policy"></a><span data-ttu-id="2c343-230">İlke uygulama</span><span class="sxs-lookup"><span data-stu-id="2c343-230">Applying the policy</span></span>
<span data-ttu-id="2c343-231">Şimdi İlkesi tamamlandıktan ve ilişkili bir yedekleme zamanlaması, bekletme ilkesi ve dosyaların bir ekleme/çıkarma listesi vardır.</span><span class="sxs-lookup"><span data-stu-id="2c343-231">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="2c343-232">Bu ilkeyi şimdi kullanmak Azure Backup için kaydedilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="2c343-232">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="2c343-233">Yeni oluşturulan İlkesi, uygulamadan önce mevcut hiçbir yedekleme ilkeleri kullanılarak sunucu ile ilişkilendirilen olduğundan emin olun [Kaldır OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2c343-233">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="2c343-234">İlkeyi kaldırmayı onay ister.</span><span class="sxs-lookup"><span data-stu-id="2c343-234">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="2c343-235">Onay Kullan'ı atlamanızı ```-Confirm:$false``` bayrağı cmdlet ile.</span><span class="sxs-lookup"><span data-stu-id="2c343-235">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="2c343-236">İlke nesnesi yürüten yapılır kullanarak [kümesi OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2c343-236">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="2c343-237">Bu ayrıca onaylamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="2c343-237">This will also ask for confirmation.</span></span> <span data-ttu-id="2c343-238">Onay Kullan'ı atlamanızı ```-Confirm:$false``` bayrağı cmdlet ile.</span><span class="sxs-lookup"><span data-stu-id="2c343-238">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

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

<span data-ttu-id="2c343-239">Kullanarak varolan yedekleme ilkesi ayrıntılarını görüntüleyebilirsiniz [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2c343-239">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="2c343-240">Kullanarak daha fazla ayrıntıya [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet'i için yedekleme zamanlamasını ve [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) bekletme ilkeleri için cmdlet</span><span class="sxs-lookup"><span data-stu-id="2c343-240">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="2c343-241">Bir geçici yedekleme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="2c343-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="2c343-242">Bir yedekleme İlkesi ayarladıktan sonra yedeklemeler zamanlama meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="2c343-242">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="2c343-243">Bir geçici yedekleme tetikleme olduğunu da olası kullanarak [başlangıç OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2c343-243">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing the metadata VHD...
Data transfer is in progress. It might take longer since it is the first backup and all data needs to be transferred...
Data transfer completed and all backed up data is in the cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="2c343-244">Verileri Azure yedekten geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="2c343-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="2c343-245">Bu bölümde, veri kurtarma Azure Backup otomatikleştirmek için adımlarda size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="2c343-245">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="2c343-246">Bunun yapılması, aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="2c343-246">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="2c343-247">Kaynak birim seçin</span><span class="sxs-lookup"><span data-stu-id="2c343-247">Pick the source volume</span></span>
2. <span data-ttu-id="2c343-248">Geri yüklemek için bir yedekleme noktası seçin</span><span class="sxs-lookup"><span data-stu-id="2c343-248">Choose a backup point to restore</span></span>
3. <span data-ttu-id="2c343-249">Geri yüklemek için bir öğe seçin</span><span class="sxs-lookup"><span data-stu-id="2c343-249">Choose an item to restore</span></span>
4. <span data-ttu-id="2c343-250">Tetikleyici geri yükleme işlemi</span><span class="sxs-lookup"><span data-stu-id="2c343-250">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="2c343-251">Kaynak birim çekme</span><span class="sxs-lookup"><span data-stu-id="2c343-251">Picking the source volume</span></span>
<span data-ttu-id="2c343-252">Bir öğeyi Azure yedeklemeden geri yüklemek için ilk öğenin kaynağını tanımlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c343-252">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="2c343-253">Biz Windows Server veya Windows İstemcisi bağlamında komutları yürütülürken bu yana makine zaten tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="2c343-253">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="2c343-254">Kaynağı tanımlayan bir sonraki adım, onu içeren birim belirlemektir.</span><span class="sxs-lookup"><span data-stu-id="2c343-254">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="2c343-255">Bu makineden yedeklenen alınabilir yürüterek kaynakları veya birimlerin listesini [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2c343-255">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="2c343-256">Bu komut, bu sunucu/istemciden yedeklenen tüm kaynakları bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="2c343-256">This command returns an array of all the sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-from-which-to-restore"></a><span data-ttu-id="2c343-257">Geri yüklemek yedek bir noktası seçme</span><span class="sxs-lookup"><span data-stu-id="2c343-257">Choosing a backup point from which to restore</span></span>
<span data-ttu-id="2c343-258">Çalıştırarak yedekleme noktalarının bir listesini alma [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) uygun parametreleri cmdlet'iyle.</span><span class="sxs-lookup"><span data-stu-id="2c343-258">You retreive a list of backup points by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="2c343-259">Bizim örneğimizde, en son yedekleme noktası kaynak birimin seçeceğiz *D:* ve belirli bir dosya kurtarmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="2c343-259">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

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
<span data-ttu-id="2c343-260">Nesne ```$rps``` yedekleme noktaları dizisidir.</span><span class="sxs-lookup"><span data-stu-id="2c343-260">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="2c343-261">En son noktası ilk öğedir ve eski noktası n. öğedir.</span><span class="sxs-lookup"><span data-stu-id="2c343-261">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="2c343-262">En son noktası seçmek için kullanacağız ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="2c343-262">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="2c343-263">Geri yüklemek için bir öğe seçme</span><span class="sxs-lookup"><span data-stu-id="2c343-263">Choosing an item to restore</span></span>
<span data-ttu-id="2c343-264">Tam dosya ya da geri yüklemek için yinelemeli kullanım klasörü tanımlamak için [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2c343-264">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="2c343-265">Klasör hiyerarşisi göz atabilirsiniz yalnızca kullanarak bu şekilde ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="2c343-265">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="2c343-266">Biz dosyayı geri yüklemek istiyorsanız, bu örnekte, *finances.xls* biz nesne kullanan başvurabilir ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="2c343-266">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="2c343-267">Kullanarak geri yüklemek öğeler için arama yapabilirsiniz ```Get-OBRecoverableItem``` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2c343-267">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="2c343-268">Aranacak örneğimizde *finances.xls* biz şu komutu çalıştırarak dosyayı bir tanıtıcı alabilir:</span><span class="sxs-lookup"><span data-stu-id="2c343-268">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="2c343-269">Geri yükleme işlemini tetikler</span><span class="sxs-lookup"><span data-stu-id="2c343-269">Triggering the restore process</span></span>
<span data-ttu-id="2c343-270">Geri yükleme işlemi tetiklemek için öncelikle kurtarma seçeneklerini belirtmek ihtiyacımız.</span><span class="sxs-lookup"><span data-stu-id="2c343-270">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="2c343-271">Bu kullanılarak yapılabilir [yeni OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2c343-271">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="2c343-272">Bu örnek için dosyaları geri yüklemek istiyoruz varsayalım *C:\temp*. Ayrıca hedef klasörde zaten mevcut dosyaların atlamak istiyoruz varsayalım *C:\temp*. Bu tür bir kurtarma seçeneğini oluşturmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="2c343-272">For this example, let's assume that we want to restore the files to *C:\temp*. Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*. To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="2c343-273">Kullanarak geri yükleme işlemi şimdi tetikleyebilir [başlangıç OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) seçilen komutu ```$item``` çıktısından ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2c343-273">Now trigger the restore process by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="2c343-274">Azure Backup aracısını kaldırma</span><span class="sxs-lookup"><span data-stu-id="2c343-274">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="2c343-275">Azure Backup aracısını kaldırma, aşağıdaki komutu kullanarak gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="2c343-275">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="2c343-276">Aracısı ikili dosyalarının makineden kaldırma dikkate alınması gereken bazı sonuçları vardır:</span><span class="sxs-lookup"><span data-stu-id="2c343-276">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="2c343-277">Dosya Filtresi makineden kaldırır ve değişiklikleri izleme durduruldu.</span><span class="sxs-lookup"><span data-stu-id="2c343-277">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="2c343-278">Tüm ilke bilgilerine makineden kaldırıldı, ancak hizmetinde depolanması ilke bilgilerini sürdürür.</span><span class="sxs-lookup"><span data-stu-id="2c343-278">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="2c343-279">Tüm yedekleme zamanlamaları kaldırılır ve daha fazla yedekleme alınır.</span><span class="sxs-lookup"><span data-stu-id="2c343-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="2c343-280">Ancak, verileri Azure kalırken depolanır ve bekletme ilkesi Kurulum göredir, tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="2c343-280">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="2c343-281">Eski noktalarını otomatik olarak eski.</span><span class="sxs-lookup"><span data-stu-id="2c343-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="2c343-282">Uzaktan Yönetim</span><span class="sxs-lookup"><span data-stu-id="2c343-282">Remote management</span></span>
<span data-ttu-id="2c343-283">Azure Yedekleme aracısı, ilkeler ve veri kaynakları çevresinde tüm yönetim uzaktan PowerShell aracılığıyla gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="2c343-283">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="2c343-284">Uzaktan yönetilecek makine doğru hazırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c343-284">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="2c343-285">Varsayılan olarak, WinRM hizmeti el ile başlatma için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="2c343-285">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="2c343-286">Başlangıç türünü ayarlamak *otomatik* ve hizmetin başlatılması.</span><span class="sxs-lookup"><span data-stu-id="2c343-286">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="2c343-287">WinRM hizmetinin çalıştığından emin olun, durum özelliğinin değeri olmalıdır *çalıştıran*.</span><span class="sxs-lookup"><span data-stu-id="2c343-287">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="2c343-288">PowerShell uzaktan iletişim için yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c343-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="2c343-289">Makine artık uzaktan - aracı yüklemesinden başlatma yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="2c343-289">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="2c343-290">Örneğin, aşağıdaki komut dosyası Aracısı uzak makineye kopyalar ve onu yükler.</span><span class="sxs-lookup"><span data-stu-id="2c343-290">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="2c343-291">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c343-291">Next steps</span></span>
<span data-ttu-id="2c343-292">Azure yedekleme için Windows Server/istemcisi bakın hakkında daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="2c343-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="2c343-293">Azure Backup'a giriş</span><span class="sxs-lookup"><span data-stu-id="2c343-293">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="2c343-294">Windows sunucularını yedekleme</span><span class="sxs-lookup"><span data-stu-id="2c343-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
