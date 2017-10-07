---
title: aaaUse PowerShell toomanage Windows Server Yedekleme azure'da | Microsoft Docs
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
ms.openlocfilehash: 72292e510b0f059102440bd49a195be4ef700a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="ed26e-103">Dağıtma ve PowerShell kullanarak Windows Server/Windows İstemcisi için yedekleme tooAzure yönetme</span><span class="sxs-lookup"><span data-stu-id="ed26e-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed26e-104">ARM</span><span class="sxs-lookup"><span data-stu-id="ed26e-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="ed26e-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="ed26e-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="ed26e-106">Bu makalede, Windows Server veya Windows iş istasyonu veri tooa toouse PowerShell tooback yedekleme kasası nasıl açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ed26e-106">This article explains how toouse PowerShell tooback up Windows Server or Windows workstation data tooa backup vault.</span></span> <span data-ttu-id="ed26e-107">Microsoft, tüm yeni dağıtımlar için kurtarma Hizmetleri kasalarının kullanılmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="ed26e-108">Yeni bir Azure yedekleme kullanıcı yoksa ve bir yedekleme kasası, aboneliğinizde oluşturmadıysanız, hello makale kullanırsınız [dağıtma ve PowerShell kullanarak Data Protection Manager veri tooAzure yönetmek](backup-client-automation.md) bir kurtarma Hizmetleri kasasına verilerinizi depolamak için.</span><span class="sxs-lookup"><span data-stu-id="ed26e-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ed26e-109">Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed26e-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="ed26e-110">Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="ed26e-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="ed26e-111">Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.</span><span class="sxs-lookup"><span data-stu-id="ed26e-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="ed26e-112">15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="ed26e-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="ed26e-113">**1 Kasım 2017’ye kadar**:</span><span class="sxs-lookup"><span data-stu-id="ed26e-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="ed26e-114">Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ed26e-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="ed26e-115">Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="ed26e-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="ed26e-116">Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ed26e-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="ed26e-117">Azure PowerShell'i yükleme</span><span class="sxs-lookup"><span data-stu-id="ed26e-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="ed26e-118">Azure PowerShell 1.0 Ekim 2015'te yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ed26e-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="ed26e-119">Bu sürüm hello 0.9.8 yayın başarılı oldu ve bazı önemli değişiklikler hakkında özellikle hello adlandırma deseni hello cmdlet'lerinin getirildi.</span><span class="sxs-lookup"><span data-stu-id="ed26e-119">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="ed26e-120">1.0 cmdlet'leri izleyin hello adlandırma deseni {fiil}-AzureRm {isim}; Merhaba 0.9.8 adlarında değil ancak **Rm** (örneğin, New-Azureresourcegroup yerine New-Azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="ed26e-120">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="ed26e-121">Azure PowerShell 0.9.8 kullanıldığında, önce hello Resource Manager moduna hello çalıştırarak etkinleştirmelisiniz **Switch-AzureMode AzureResourceManager** komutu.</span><span class="sxs-lookup"><span data-stu-id="ed26e-121">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="ed26e-122">Bu komut 1.0 veya üstü gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="ed26e-123">Merhaba 0.9.8 ortamında hello 1.0 veya sonraki ortamı için yazılan komut dosyalarınızı toouse istiyorsanız, dikkatlice hello komut bir ön üretim ortamında üretim tooavoid kullanmadan önce sınamanız beklenmeyen etkisi.</span><span class="sxs-lookup"><span data-stu-id="ed26e-123">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="ed26e-124">[Merhaba son PowerShell yayın indirme](https://github.com/Azure/azure-powershell/releases) (gerekli minimum sürüm: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="ed26e-124">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="ed26e-125">Yedekleme kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ed26e-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="ed26e-126">Azure Backup hello için ilk kez kullanan müşteriler için aboneliğiniz ile birlikte kullanılan tooregister hello Azure Backup sağlayıcı toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-126">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="ed26e-127">Bu komutu aşağıdaki hello çalıştırarak yapılabilir: Register-AzureProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="ed26e-127">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="ed26e-128">Hello kullanarak yeni bir yedekleme kasası oluşturma **yeni AzureRMBackupVault** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ed26e-128">You can create a new backup vault using hello **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="ed26e-129">Merhaba yedekleme kasası olan bir ARM kaynak tooplace gereken şekilde bir kaynak grubu içinde.</span><span class="sxs-lookup"><span data-stu-id="ed26e-129">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="ed26e-130">Yükseltilmiş bir Azure PowerShell konsolunda hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ed26e-130">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="ed26e-131">Kullanım hello **Get-AzureRMBackupVault** cmdlet toolist hello yedekleme kasaları bir abonelik.</span><span class="sxs-lookup"><span data-stu-id="ed26e-131">Use hello **Get-AzureRMBackupVault** cmdlet toolist hello backup vaults in a subscription.</span></span>

## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="ed26e-132">Hello Azure Backup aracısını yükleme</span><span class="sxs-lookup"><span data-stu-id="ed26e-132">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="ed26e-133">Hello Azure Backup aracısını yüklemeden önce indirildi ve Windows Server hello mevcut toohave hello yükleyici gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-133">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="ed26e-134">Hello hello Installer hello en son sürümünü elde edebilirsiniz [Microsoft Download Center](http://aka.ms/azurebackup_agent) veya hello yedekleme kasasının Pano sayfası.</span><span class="sxs-lookup"><span data-stu-id="ed26e-134">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="ed26e-135">Kolay erişilebilecek bir konuma tooan gibi Hello yükleyici Kaydet * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="ed26e-135">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="ed26e-136">tooinstall hello Aracısı, komutu yükseltilmiş bir PowerShell konsolunda aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ed26e-136">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="ed26e-137">Bu, tüm hello varsayılan seçeneklerle hello aracı yükler.</span><span class="sxs-lookup"><span data-stu-id="ed26e-137">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="ed26e-138">Merhaba yükleme hello arka planda birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="ed26e-138">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="ed26e-139">Merhaba belirtmezseniz */nu* seçeneği sonra hello **Windows Update** hello yükleme toocheck herhangi bir güncelleştirme için hello sonunda penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="ed26e-139">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="ed26e-140">Bir kez yüklendikten sonra hello Aracısı hello yüklü programlar listesinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-140">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="ed26e-141">toosee hello listesi yüklü programlar, çok Git**Denetim Masası** > **programları** > **programlar ve Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="ed26e-141">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Yüklü aracı](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="ed26e-143">Yükleme Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="ed26e-143">Installation options</span></span>
<span data-ttu-id="ed26e-144">Tüm seçeneklerin aracılığıyla hello toosee komut satırı Merhaba, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ed26e-144">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="ed26e-145">Merhaba mevcut Seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ed26e-145">hello available options include:</span></span>

| <span data-ttu-id="ed26e-146">Seçenek</span><span class="sxs-lookup"><span data-stu-id="ed26e-146">Option</span></span> | <span data-ttu-id="ed26e-147">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ed26e-147">Details</span></span> | <span data-ttu-id="ed26e-148">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="ed26e-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed26e-149">/q</span><span class="sxs-lookup"><span data-stu-id="ed26e-149">/q</span></span> |<span data-ttu-id="ed26e-150">Sessiz yükleme</span><span class="sxs-lookup"><span data-stu-id="ed26e-150">Quiet installation</span></span> |- |
| <span data-ttu-id="ed26e-151">p: "Konum"</span><span class="sxs-lookup"><span data-stu-id="ed26e-151">/p:"location"</span></span> |<span data-ttu-id="ed26e-152">Yol toohello yükleme klasörünü hello Azure Yedekleme aracısı.</span><span class="sxs-lookup"><span data-stu-id="ed26e-152">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="ed26e-153">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Aracısı</span><span class="sxs-lookup"><span data-stu-id="ed26e-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="ed26e-154">/ s: "Konum"</span><span class="sxs-lookup"><span data-stu-id="ed26e-154">/s:"location"</span></span> |<span data-ttu-id="ed26e-155">Hello Azure Backup aracısı için yol toohello Önbellek klasörü.</span><span class="sxs-lookup"><span data-stu-id="ed26e-155">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="ed26e-156">C:\Program Files\Microsoft Azure kurtarma Hizmetleri Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="ed26e-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="ed26e-157">/m</span><span class="sxs-lookup"><span data-stu-id="ed26e-157">/m</span></span> |<span data-ttu-id="ed26e-158">Katılımı tooMicrosoft güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ed26e-158">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="ed26e-159">/nu</span><span class="sxs-lookup"><span data-stu-id="ed26e-159">/nu</span></span> |<span data-ttu-id="ed26e-160">Yükleme tamamlandıktan sonra güncelleştirmeleri denetleme</span><span class="sxs-lookup"><span data-stu-id="ed26e-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="ed26e-161">/d</span><span class="sxs-lookup"><span data-stu-id="ed26e-161">/d</span></span> |<span data-ttu-id="ed26e-162">Microsoft Azure kurtarma Hizmetleri Aracısı kaldırır</span><span class="sxs-lookup"><span data-stu-id="ed26e-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="ed26e-163">/ph</span><span class="sxs-lookup"><span data-stu-id="ed26e-163">/ph</span></span> |<span data-ttu-id="ed26e-164">Proxy konağı adresi</span><span class="sxs-lookup"><span data-stu-id="ed26e-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="ed26e-165">/PO</span><span class="sxs-lookup"><span data-stu-id="ed26e-165">/po</span></span> |<span data-ttu-id="ed26e-166">Proxy ana bilgisayar bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="ed26e-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="ed26e-167">/PU</span><span class="sxs-lookup"><span data-stu-id="ed26e-167">/pu</span></span> |<span data-ttu-id="ed26e-168">Proxy konağı kullanıcı</span><span class="sxs-lookup"><span data-stu-id="ed26e-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="ed26e-169">/pw</span><span class="sxs-lookup"><span data-stu-id="ed26e-169">/pw</span></span> |<span data-ttu-id="ed26e-170">Proxy parolası</span><span class="sxs-lookup"><span data-stu-id="ed26e-170">Proxy Password</span></span> |- |

## <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="ed26e-171">Hello Azure Backup hizmeti ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="ed26e-171">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="ed26e-172">Hello Azure Backup hizmeti ile kaydedebilmek için o hello tooensure gerek [Önkoşullar](backup-configure-vault.md) karşılanır.</span><span class="sxs-lookup"><span data-stu-id="ed26e-172">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="ed26e-173">Yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ed26e-173">You must:</span></span>

* <span data-ttu-id="ed26e-174">Geçerli bir Azure aboneliğiniz</span><span class="sxs-lookup"><span data-stu-id="ed26e-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="ed26e-175">Bir yedekleme kasası sahip</span><span class="sxs-lookup"><span data-stu-id="ed26e-175">Have a backup vault</span></span>

<span data-ttu-id="ed26e-176">toodownload hello kasa kimlik bilgileri Hello çalıştırmak, **Get-AzureRMBackupVaultCredentials** cmdlet'i, uygun bir konumda gibi bir Azure PowerShell konsolunda ve deposu * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="ed26e-176">toodownload hello vault credentials, run hello **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="ed26e-177">Merhaba kasası ile kaydediliyor hello makine yapılır hello kullanarak [başlangıç OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ed26e-177">Registering hello machine with hello vault is done using hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

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
> <span data-ttu-id="ed26e-178">Göreli yollar toospecify hello kasa kimlik bilgileri dosyası kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ed26e-178">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="ed26e-179">Bir giriş toohello cmdlet'ini olarak mutlak bir yol sağlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="ed26e-179">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="ed26e-180">Ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="ed26e-180">Networking settings</span></span>
<span data-ttu-id="ed26e-181">Internet proxy sunucu üzerinden gerçekleşir toohello Windows hello Hello bağlantısını makine olduğunda hello proxy ayarlarını toohello aracı da sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-181">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="ed26e-182">Bu örnekte, olmadığından hiçbir Ara sunucunun biz açıkça herhangi bir proxy ile ilgili bilgi temizleme.</span><span class="sxs-lookup"><span data-stu-id="ed26e-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="ed26e-183">Bant genişliği kullanımı ile Merhaba seçenekleri de denetlenebilir ```work hour bandwidth``` ve ```non-work hour bandwidth``` hello haftanın belirli bir dizi için.</span><span class="sxs-lookup"><span data-stu-id="ed26e-183">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="ed26e-184">Ayar Hello proxy ve bant genişliği ayrıntıları yapılır hello kullanarak [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ed26e-184">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="ed26e-185">Şifreleme ayarları</span><span class="sxs-lookup"><span data-stu-id="ed26e-185">Encryption settings</span></span>
<span data-ttu-id="ed26e-186">Merhaba gönderilen yedekleme verileri tooAzure yedekleme şifrelenmiş tooprotect hello hello veri gizliliğini ' dir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-186">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="ed26e-187">Merhaba şifreleme parolası hello "parola" toodecrypt hello geri yükleme hello aynı anda verilerdir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-187">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="ed26e-188">Ayarlandıktan sonra hello parola bilgilerini güvenli ve güvenli tutar.</span><span class="sxs-lookup"><span data-stu-id="ed26e-188">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="ed26e-189">Bu parola olmadan mümkün toorestore verileri azure'dan olmaz.</span><span class="sxs-lookup"><span data-stu-id="ed26e-189">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="ed26e-190">Dosya ve klasörleri yedekleme</span><span class="sxs-lookup"><span data-stu-id="ed26e-190">Back up files and folders</span></span>
<span data-ttu-id="ed26e-191">Tüm yedeklemelerinizi Windows sunucularını ve istemcilerini tooAzure yedekleme İlkesi tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-191">All your backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="ed26e-192">Hello İlkesi üç bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="ed26e-192">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="ed26e-193">A **yedekleme zamanlaması** yedeklemeler alınır ve hello hizmeti ile eşitlenmiş toobe gerektiğinde belirtir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-193">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="ed26e-194">A **bekletme zamanlaması** Azure'da ne kadar süreyle tooretain hello kurtarma noktaları belirtir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-194">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="ed26e-195">A **dosya ekleme/çıkarma belirtimi** belirleyen ne yedeklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="ed26e-196">Yedekleme, otomatikleştirme beri bu belgede, hiçbir şey yapılandırılmış varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="ed26e-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="ed26e-197">Hello kullanarak yeni bir yedekleme ilkesi oluşturarak başlayın [yeni OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet'i ve bunu kullanma.</span><span class="sxs-lookup"><span data-stu-id="ed26e-197">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="ed26e-198">Bu zaman hello İlkesi boş olduğunu ve diğer cmdlet'ler gerekli toodefine ne öğeleri dahil etmek veya hariç, yedeklemeler çalışacak ve burada hello yedeklemeleri depolanacak.</span><span class="sxs-lookup"><span data-stu-id="ed26e-198">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="ed26e-199">Merhaba yedekleme zamanlamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ed26e-199">Configuring hello backup schedule</span></span>
<span data-ttu-id="ed26e-200">ilk Merhaba hello İlkesi 3 bölümleri hale hello kullanılarak oluşturulan hello yedekleme zamanlaması [yeni OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ed26e-200">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="ed26e-201">Merhaba yedekleme zamanlaması yedeklemeleri gerçekleştirilecek toobe gerektiğinde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ed26e-201">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="ed26e-202">Bir zamanlama oluştururken toospecify 2 giriş parametreleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="ed26e-202">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="ed26e-203">**Merhaba haftanın günlerini** hello yedekleme çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-203">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="ed26e-204">Merhaba yedekleme işi yalnızca bir gün veya her gün hello haftanın veya arasındaki herhangi bir birleşimini çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed26e-204">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="ed26e-205">**Merhaba saatlerinde** hello yedekleme ne zaman çalışmalı.</span><span class="sxs-lookup"><span data-stu-id="ed26e-205">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="ed26e-206">Too3 hello yedekleme harekete geçirildiğinde hello günün farklı saatlerinde tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed26e-206">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="ed26e-207">Örneğin, 4'e her Cumartesi ve Pazar çalışan bir yedekleme ilkesi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed26e-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="ed26e-208">Merhaba yedekleme zamanlaması bir ilkeyle ilişkilendirilmiş toobe gerekir ve bu hello kullanarak elde [kümesi OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ed26e-208">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="ed26e-209">Bir bekletme ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ed26e-209">Configuring a retention policy</span></span>
<span data-ttu-id="ed26e-210">Merhaba Bekletme İlkesi yedekleme işlerini oluşturulan noktaları korunur ne kadar süreyle kurtarma tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ed26e-210">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="ed26e-211">Hello kullanarak yeni bir bekletme ilkesi oluşturulurken [yeni OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet'ini hello yedekleme kurtarma noktalarının hello gün sayısı gereken Azure yedekleme ile korunduğunu toobe belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed26e-211">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="ed26e-212">Aşağıdaki Hello örnek bir bekletme ilkesi 7 gün olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ed26e-212">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="ed26e-213">Merhaba bekletme ilkesi hello cmdlet'ini kullanarak hello ana ilkesiyle ilişkili olmalıdır [kümesi OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="ed26e-213">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="ed26e-214">Yedeklenen dosyaları toobe hariç ve dahil</span><span class="sxs-lookup"><span data-stu-id="ed26e-214">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="ed26e-215">Bir ```OBFileSpec``` nesnesi eklenen ve bir yedek dışlanan hello dosyaları toobe tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ed26e-215">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="ed26e-216">Bu bir kapsam hello çıkışı dosya ve klasörlerin bir makinede korumalı kurallar kümesidir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-216">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="ed26e-217">Birçok ekleme veya hariç tutma kuralları gerektiği gibi dosya ve bir ilke ile ilişkilendirmek gibi sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="ed26e-218">Yeni bir OBFileSpec nesnesi oluştururken şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ed26e-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="ed26e-219">Merhaba dosya ve klasörleri toobe dahil belirtin</span><span class="sxs-lookup"><span data-stu-id="ed26e-219">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="ed26e-220">Dışlanan dosya ve klasörleri toobe hello belirtin</span><span class="sxs-lookup"><span data-stu-id="ed26e-220">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="ed26e-221">Özyinelemeli bir klasör (veya) olup yalnızca üst düzey dosyalarında hello belirtilen klasör hello yedeklenmelidir verilerin yedeğini yukarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="ed26e-221">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="ed26e-222">Merhaba ikinci hello yeni OBFileSpec komutta hello - özyinelemesiz bayrağı kullanılarak elde edilir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-222">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="ed26e-223">Merhaba aşağıdaki örnekte, biz birimi yedekleyin C: ve D: ve hello OS ikili hello Windows klasöründeki ve herhangi bir geçici klasörde dosyaları hariç.</span><span class="sxs-lookup"><span data-stu-id="ed26e-223">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="ed26e-224">hello kullanarak iki dosya belirtimleri oluşturacağız şekilde toodo [yeni OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - eklenmesi, diğeri dışarıda bırakma için.</span><span class="sxs-lookup"><span data-stu-id="ed26e-224">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="ed26e-225">Merhaba Dosya belirtimleri oluşturduktan sonra hello kullanarak hello İlkesi ile ilişkili [Ekle OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ed26e-225">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="ed26e-226">Hello İlkesi uygulama</span><span class="sxs-lookup"><span data-stu-id="ed26e-226">Applying hello policy</span></span>
<span data-ttu-id="ed26e-227">Şimdi hello İlkesi tamamlandıktan ve ilişkili bir yedekleme zamanlaması, bekletme ilkesi ve dosyaların bir ekleme/çıkarma listesi vardır.</span><span class="sxs-lookup"><span data-stu-id="ed26e-227">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="ed26e-228">Bu ilkeyi şimdi için Azure Backup toouse kaydedilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-228">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="ed26e-229">İlke, yeni oluşturulan hello uygulamadan önce mevcut hiçbir yedekleme ilkeleri hello kullanarak hello sunucuyla ilişkili olduğundan emin olun [Kaldır OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ed26e-229">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="ed26e-230">Hello ilkesi kaldırma için onay ister.</span><span class="sxs-lookup"><span data-stu-id="ed26e-230">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="ed26e-231">tooskip hello onay kullanmak hello ```-Confirm:$false``` hello cmdlet ile bayrağı.</span><span class="sxs-lookup"><span data-stu-id="ed26e-231">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="ed26e-232">Uygulanıyor hello İlkesi yapılır hello kullanarak [kümesi OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ed26e-232">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="ed26e-233">Bu ayrıca onaylamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-233">This will also ask for confirmation.</span></span> <span data-ttu-id="ed26e-234">tooskip hello onay kullanmak hello ```-Confirm:$false``` hello cmdlet ile bayrağı.</span><span class="sxs-lookup"><span data-stu-id="ed26e-234">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

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

<span data-ttu-id="ed26e-235">Hello kullanarak hello mevcut bir yedekleme İlkesi hello ayrıntılarını görüntüleyebilirsiniz [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ed26e-235">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="ed26e-236">Daha fazla hello kullanarak ayrıntıya [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet'i hello yedekleme zamanlamasını ve hello için [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) hello bekletme ilkeleri için cmdlet</span><span class="sxs-lookup"><span data-stu-id="ed26e-236">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="ed26e-237">Bir geçici yedekleme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="ed26e-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="ed26e-238">Bir yedekleme İlkesi ayarladıktan sonra hello yedeklemeleri hello zamanlama meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-238">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="ed26e-239">Bir geçici yedekleme tetikleme ayrıca hello kullanarak olası [başlangıç OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ed26e-239">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="ed26e-240">Verileri Azure yedekten geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="ed26e-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="ed26e-241">Bu bölümde, veri kurtarma Azure Backup otomatikleştirmek için hello adımlarında size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-241">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="ed26e-242">Bunu yapmak, böylece hello aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="ed26e-242">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="ed26e-243">Merhaba kaynak birimi seçin</span><span class="sxs-lookup"><span data-stu-id="ed26e-243">Pick hello source volume</span></span>
2. <span data-ttu-id="ed26e-244">Bir yedekleme noktası toorestore seçin</span><span class="sxs-lookup"><span data-stu-id="ed26e-244">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="ed26e-245">Bir öğe toorestore seçin</span><span class="sxs-lookup"><span data-stu-id="ed26e-245">Choose an item toorestore</span></span>
4. <span data-ttu-id="ed26e-246">Tetikleyici hello geri yükleme işlemi</span><span class="sxs-lookup"><span data-stu-id="ed26e-246">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="ed26e-247">Çekme hello kaynak birim</span><span class="sxs-lookup"><span data-stu-id="ed26e-247">Picking hello source volume</span></span>
<span data-ttu-id="ed26e-248">Sipariş toorestore öğeyi Azure Backup'da, ilk tooidentify hello kaynak hello öğesinin gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-248">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="ed26e-249">Biz hello bağlamında bir Windows Server veya Windows İstemcisi hello komutları yürütülürken bu yana hello makine zaten tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="ed26e-249">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="ed26e-250">Merhaba kaynağı tanımlayan bir hello sonraki adım içeren tooidentify hello birimdir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-250">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="ed26e-251">Bu makineden yedeklenen alınabilir hello yürüterek birimleri veya kaynakları listesini [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ed26e-251">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="ed26e-252">Bu komut, bu sunucu/istemciden yedeklenen tüm hello kaynakları bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ed26e-252">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-toorestore"></a><span data-ttu-id="ed26e-253">Bir yedekleme noktası toorestore seçme</span><span class="sxs-lookup"><span data-stu-id="ed26e-253">Choosing a backup point toorestore</span></span>
<span data-ttu-id="ed26e-254">Merhaba yedekleme noktaları listesi hello yürüterek alınabilir [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) uygun parametreleri cmdlet'iyle.</span><span class="sxs-lookup"><span data-stu-id="ed26e-254">hello list of backup points can be retrieved by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="ed26e-255">Bizim örneğimizde, son yedekleme noktası hello kaynak birim hello seçeceğiz *D:* ve toorecover belirli bir dosya kullanın.</span><span class="sxs-lookup"><span data-stu-id="ed26e-255">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="ed26e-256">Merhaba nesne ```$rps``` yedekleme noktaları dizisidir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-256">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="ed26e-257">Hello ilk öğe hello son noktası ve hello n. öğeyi hello eski noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="ed26e-257">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="ed26e-258">kullanacağız toochoose hello son noktası, ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="ed26e-258">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="ed26e-259">Bir öğe toorestore seçme</span><span class="sxs-lookup"><span data-stu-id="ed26e-259">Choosing an item toorestore</span></span>
<span data-ttu-id="ed26e-260">tooidentify hello tam dosya veya klasör toorestore, yinelemeli olarak kullanın hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ed26e-260">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="ed26e-261">Bu şekilde hello klasör hiyerarşisini yalnızca hello kullanarak gözatılabilir ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="ed26e-261">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="ed26e-262">Bu örnekte, biz toorestore hello dosyanın istiyorsanız *finances.xls* Biz bu kullanarak başvuru hello nesne ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="ed26e-262">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="ed26e-263">Hello kullanarak öğeleri toorestore için arama yapabilirsiniz ```Get-OBRecoverableItem``` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ed26e-263">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="ed26e-264">Örneğimizde, toosearch için *finances.xls* biz şu komutu çalıştırarak hello dosyada bir tanıtıcı alabilir:</span><span class="sxs-lookup"><span data-stu-id="ed26e-264">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="ed26e-265">Merhaba geri yükleme işlemini tetikler</span><span class="sxs-lookup"><span data-stu-id="ed26e-265">Triggering hello restore process</span></span>
<span data-ttu-id="ed26e-266">tootrigger hello geri yükleme işlemi, ilk toospecify hello kurtarma seçenekleri ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="ed26e-266">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="ed26e-267">Bu hello kullanarak yapılabilir [yeni OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ed26e-267">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="ed26e-268">Bu örnek, toorestore hello dosyaları çok istediğimizi varsayalım*C:\temp*. Ayrıca hello hedef klasörü zaten mevcut dosyalarda tooskip istiyoruz varsayalım *C:\temp*. toocreate böyle bir kurtarma seçeneği, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="ed26e-268">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="ed26e-269">Şimdi hello kullanarak geri yüklemeyi tetikleyecek [başlangıç OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) seçili hello komutunu ```$item``` hello hello çıktısından ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ed26e-269">Now trigger restore by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="ed26e-270">Hello Azure Backup aracısını kaldırma</span><span class="sxs-lookup"><span data-stu-id="ed26e-270">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="ed26e-271">Kaldırma hello Azure Yedekleme aracısı, komutu aşağıdaki hello kullanarak gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="ed26e-271">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="ed26e-272">Merhaba Aracısı ikili dosyalarının hello makineden kaldırma bazı sonuçları tooconsider sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ed26e-272">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="ed26e-273">Merhaba dosya filtresi hello makineden kaldırır ve değişiklikleri izleme durduruldu.</span><span class="sxs-lookup"><span data-stu-id="ed26e-273">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="ed26e-274">Tüm ilke bilgilerine hello makineden kaldırıldı, ancak hello ilkesi bilgileri hello hizmetinde depolanan toobe devam eder.</span><span class="sxs-lookup"><span data-stu-id="ed26e-274">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="ed26e-275">Tüm yedekleme zamanlamaları kaldırılır ve daha fazla yedekleme alınır.</span><span class="sxs-lookup"><span data-stu-id="ed26e-275">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="ed26e-276">Ancak, Azure kalırken depolanan verileri hello ve hello bekletme ilkesi Kurulum göredir, tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="ed26e-276">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="ed26e-277">Eski noktalarını otomatik olarak eski.</span><span class="sxs-lookup"><span data-stu-id="ed26e-277">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="ed26e-278">Uzaktan Yönetim</span><span class="sxs-lookup"><span data-stu-id="ed26e-278">Remote management</span></span>
<span data-ttu-id="ed26e-279">Tüm hello yönetim hello Azure Yedekleme aracısı, ilkeler ve veri kaynakları çevresinde uzaktan PowerShell aracılığıyla gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-279">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="ed26e-280">Uzaktan yönetilecek hello makine doğru şekilde hazırlanmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-280">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="ed26e-281">Varsayılan olarak, hello WinRM hizmeti el ile başlatma için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="ed26e-281">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="ed26e-282">Merhaba başlangıç türü çok ayarlanmalıdır*otomatik* ve hello hizmet başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-282">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="ed26e-283">WinRM hizmeti hello tooverify çalıştığından, hello Status özelliği hello değeri olmalıdır *çalıştıran*.</span><span class="sxs-lookup"><span data-stu-id="ed26e-283">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="ed26e-284">PowerShell uzaktan iletişim için yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-284">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="ed26e-285">Merhaba makine artık uzaktan - hello hello aracı yüklemesinden başlatma yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="ed26e-285">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="ed26e-286">Örneğin, komut dosyası izleyen hello hello aracı toohello uzak makine kopyalar ve onu yükler.</span><span class="sxs-lookup"><span data-stu-id="ed26e-286">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="ed26e-287">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ed26e-287">Next steps</span></span>
<span data-ttu-id="ed26e-288">Azure yedekleme için Windows Server/istemcisi bakın hakkında daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="ed26e-288">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="ed26e-289">Giriş tooAzure yedekleme</span><span class="sxs-lookup"><span data-stu-id="ed26e-289">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="ed26e-290">Windows sunucularını yedekleme</span><span class="sxs-lookup"><span data-stu-id="ed26e-290">Back up Windows Servers</span></span>](backup-configure-vault.md)
