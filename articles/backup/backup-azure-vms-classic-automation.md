---
title: "aaaDeploy ve PowerShell kullanarak Azure VM'ler için yedekleme yönetme | Microsoft Docs"
description: "Bilgi nasıl toodeploy ve Azure PowerShell kullanarak yedekleme yönetin."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3ecd3f94c5e3e8fc8018e8786302edd4847744b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="c260d-103">Sanal makineler yukarı AzureRM.Backup cmdlet'leri tooback kullanın</span><span class="sxs-lookup"><span data-stu-id="c260d-103">Use AzureRM.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c260d-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c260d-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="c260d-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="c260d-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="c260d-106">Bu makale size nasıl gösterir yedekleme ve kurtarma Azure VM'ler için Azure PowerShell toouse.</span><span class="sxs-lookup"><span data-stu-id="c260d-106">This article shows you how toouse Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="c260d-107">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır: Resource Manager ve Klasik.</span><span class="sxs-lookup"><span data-stu-id="c260d-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="c260d-108">Bu makalede hello Klasik dağıtım modeli tooback veri tooa yedekleme kasası yukarı kullanmayı ele alır.</span><span class="sxs-lookup"><span data-stu-id="c260d-108">This article covers using hello Classic deployment model tooback up data tooa Backup vault.</span></span> <span data-ttu-id="c260d-109">Aboneliğinizde bir yedekleme kasası oluşturmadıysanız, bu makalede, Resource Manager sürümü hello bkz [kullanım AzureRM.RecoveryServices.Backup cmdlet'leri tooback sanal makineleri yedeklemek](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="c260d-109">If you have not created a Backup vault in your subscription, see hello Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="c260d-110">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="c260d-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c260d-111">Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c260d-111">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="c260d-112">Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="c260d-112">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="c260d-113">Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.</span><span class="sxs-lookup"><span data-stu-id="c260d-113">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="c260d-114">15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="c260d-114">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="c260d-115">**1 Kasım 2017’ye kadar**:</span><span class="sxs-lookup"><span data-stu-id="c260d-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="c260d-116">Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c260d-116">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="c260d-117">Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="c260d-117">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="c260d-118">Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="c260d-118">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="c260d-119">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="c260d-119">Concepts</span></span>
<span data-ttu-id="c260d-120">Bu makalede belirli toohello PowerShell cmdlet'leri sanal makineleri yedeklemek tooback kullanılan bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c260d-120">This article provides information specific toohello PowerShell cmdlets used tooback up virtual machines.</span></span> <span data-ttu-id="c260d-121">Azure sanal makinelerini koruma hakkında giriş bilgileri için lütfen bkz [azure'da VM yedekleme altyapınızı planlama](backup-azure-vms-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c260d-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c260d-122">Başlamadan önce hello okuma [Önkoşullar](backup-azure-vms-prepare.md) Azure Backup ve hello gerekli toowork [sınırlamalar](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) hello geçerli VM yedekleme çözümünün.</span><span class="sxs-lookup"><span data-stu-id="c260d-122">Before you start, read hello [prerequisites](backup-azure-vms-prepare.md) required toowork with Azure Backup, and hello [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of hello current VM backup solution.</span></span>
>
>

<span data-ttu-id="c260d-123">toouse PowerShell etkili bir şekilde ele şu anda toounderstand hello hiyerarşi nesnelerin ve nereden toostart.</span><span class="sxs-lookup"><span data-stu-id="c260d-123">toouse PowerShell effectively, take a moment toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Nesne hiyerarşisi](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="c260d-125">Merhaba iki en önemli akışı VM korumasını etkinleştirmek ve bir kurtarma noktasından geri yüklenmesi.</span><span class="sxs-lookup"><span data-stu-id="c260d-125">hello two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="c260d-126">Bu makalenin Hello odak bu iki senaryo hello PowerShell cmdlet'leri tooenable ile çalışma sırasında adept hale toohelp noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="c260d-126">hello focus of this article is toohelp you become adept at working with hello PowerShell cmdlets tooenable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="c260d-127">Kurulumu'nu ve kaydı</span><span class="sxs-lookup"><span data-stu-id="c260d-127">Setup and Registration</span></span>
<span data-ttu-id="c260d-128">toobegin:</span><span class="sxs-lookup"><span data-stu-id="c260d-128">toobegin:</span></span>

1. <span data-ttu-id="c260d-129">[En son PowerShell indirme](https://github.com/Azure/azure-powershell/releases) (gerekli minimum sürüm: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="c260d-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="c260d-130">Hello Azure yedekleme PowerShell cmdlet'leri kullanılabilir hello aşağıdaki komutu yazarak bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c260d-130">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

<span data-ttu-id="c260d-131">Merhaba aşağıdaki Kurulum ve kayıt görevler PowerShell ile otomatik olarak yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="c260d-131">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="c260d-132">Yedekleme kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="c260d-132">Create a backup vault</span></span>
* <span data-ttu-id="c260d-133">Merhaba VM'ler hello Azure Backup hizmeti ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="c260d-133">Registering hello VMs with hello Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="c260d-134">Yedekleme kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="c260d-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="c260d-135">Azure Backup hello için ilk kez kullanan müşteriler için aboneliğiniz ile birlikte kullanılan tooregister hello Azure Backup sağlayıcı toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c260d-135">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="c260d-136">Bu komutu aşağıdaki hello çalıştırarak yapılabilir: Register-AzureRmResourceProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="c260d-136">This can be done by running hello following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="c260d-137">Hello kullanarak yeni bir yedekleme kasası oluşturma **yeni AzureRmBackupVault** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c260d-137">You can create a new backup vault using hello **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="c260d-138">Merhaba yedekleme kasası olan bir ARM kaynak tooplace gereken şekilde bir kaynak grubu içinde.</span><span class="sxs-lookup"><span data-stu-id="c260d-138">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="c260d-139">Yükseltilmiş bir Azure PowerShell konsolunda hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c260d-139">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="c260d-140">Tüm hello yedekleme kasalarının listesi hello kullanarak belirli bir abonelikte alabilirsiniz **Get-AzureRmBackupVault** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c260d-140">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="c260d-141">Uygun toostore hello yedekleme kasası nesnesine bir değişken değil.</span><span class="sxs-lookup"><span data-stu-id="c260d-141">It is convenient toostore hello backup vault object into a variable.</span></span> <span data-ttu-id="c260d-142">Merhaba kasası nesne birçok Azure yedekleme cmdlet'lerini için bir giriş olarak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c260d-142">hello vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-hello-vms"></a><span data-ttu-id="c260d-143">Merhaba VM'ler kaydetme</span><span class="sxs-lookup"><span data-stu-id="c260d-143">Registering hello VMs</span></span>
<span data-ttu-id="c260d-144">Merhaba ilk adım yapılandırma doğrultusunda Azure Backup ile yedekleme tooregister makine ya da VM Azure yedek kasası ile değil.</span><span class="sxs-lookup"><span data-stu-id="c260d-144">hello first step towards configuring backup with Azure Backup is tooregister your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="c260d-145">Merhaba **Register-AzureRmBackupContainer** cmdlet'i bir Azure Iaas sanal makinenin hello giriş bilgilerini alır ve hello belirtilen kasası ile kaydeder.</span><span class="sxs-lookup"><span data-stu-id="c260d-145">hello **Register-AzureRmBackupContainer** cmdlet takes hello input information of an Azure IaaS virtual machine and registers it with hello specified vault.</span></span> <span data-ttu-id="c260d-146">Merhaba kayıt işlemi hello Azure sanal makinesi hello yedek kasası ile ilişkilendirir ve parçaları VM hello yedekleme yaşam döngüsü ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="c260d-146">hello register operation associates hello Azure virtual machine with hello backup vault and tracks hello VM through hello backup lifecycle.</span></span>

<span data-ttu-id="c260d-147">VM hello Azure Backup hizmeti ile kaydetme bir üst düzey kapsayıcısı nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c260d-147">Registering your VM with hello Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="c260d-148">Bir kapsayıcı genellikle yedeklenebilir birden çok öğe içeriyor, ancak sanal makineleri hello durumda olacaktır hello kapsayıcısı için yalnızca bir yedekleme öğesi.</span><span class="sxs-lookup"><span data-stu-id="c260d-148">A container typically contains multiple items that can be backed up, but in hello case of VMs there will be only one backup item for hello container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="c260d-149">Azure sanal makinelerini yedekleme</span><span class="sxs-lookup"><span data-stu-id="c260d-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="c260d-150">Bir koruma ilkesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="c260d-150">Create a protection policy</span></span>
<span data-ttu-id="c260d-151">Zorunlu toocreate yeni bir koruma İlkesi toostart yedeğini Vm'leriniz değil.</span><span class="sxs-lookup"><span data-stu-id="c260d-151">It is not mandatory toocreate a new protection policy toostart backup of your VMs.</span></span> <span data-ttu-id="c260d-152">bir 'varsayılan kullanılan tooquickly etkinleştir koruma olabilir ve daha sonra hello sağ ayrıntılarla düzenlenen ilke' Hello kasası gelir.</span><span class="sxs-lookup"><span data-stu-id="c260d-152">hello vault comes with a 'Default Policy' that can be used tooquickly enable protection, and then edited later with hello right details.</span></span> <span data-ttu-id="c260d-153">Hello kullanarak hello kasasına kullanılabilir hello ilkelerinin bir listesini alabilirsiniz **Get-AzureRmBackupProtectionPolicy** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c260d-153">You can get a list of hello policies available in hello vault by using hello **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="c260d-154">PowerShell'de hello BackupTime alanının Hello saat dilimi UTC değil.</span><span class="sxs-lookup"><span data-stu-id="c260d-154">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="c260d-155">Merhaba yedekleme saati hello Azure portal gösterildiğinde, ancak hello saat dilimi hizalanmış tooyour yerel hello UTC uzaklığı birlikte sistemidir.</span><span class="sxs-lookup"><span data-stu-id="c260d-155">However, when hello backup time is shown in hello Azure portal, hello timezone is aligned tooyour local system along with hello UTC offset.</span></span>
>
>

<span data-ttu-id="c260d-156">Bir yedekleme İlkesi, en az bir bekletme ilkesi ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="c260d-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="c260d-157">Merhaba bekletme ilkesi ne kadar bir kurtarma noktası Azure yedekleme ile tutulan tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c260d-157">hello retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="c260d-158">Merhaba **yeni AzureRmBackupRetentionPolicy** cmdlet bekletme ilkesi bilgileri tutun PowerShell nesneler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c260d-158">hello **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="c260d-159">Bu bekletme ilkesi nesneler toohello girdi olarak kullanılır *yeni AzureRmBackupProtectionPolicy* cmdlet'ini veya doğrudan hello *etkinleştir AzureRmBackupProtection* cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c260d-159">These retention policy objects are used as inputs toohello *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with hello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="c260d-160">Bir yedekleme İlkesi zaman ve ne sıklıkta hello öğenin yedekleme yapılır tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c260d-160">A backup policy defines when and how often hello backup of an item is done.</span></span> <span data-ttu-id="c260d-161">Merhaba **yeni AzureRmBackupProtectionPolicy** cmdlet'i, yedekleme ilkesi bilgilerini tutan bir PowerShell nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c260d-161">hello **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="c260d-162">Merhaba yedekleme İlkesi bir giriş toohello kullanılan *etkinleştir AzureRmBackupProtection* cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c260d-162">hello backup policy is used as an input toohello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="c260d-163">Korumayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c260d-163">Enable protection</span></span>
<span data-ttu-id="c260d-164">Koruma etkinleştirme işlemi iki nesne kapsar - hello öğesi ve hello İlkesi ve her iki gereksinim toobelong toohello aynı Kasa.</span><span class="sxs-lookup"><span data-stu-id="c260d-164">Enabling protection involves two objects - hello Item and hello Policy, and both need toobelong toohello same vault.</span></span> <span data-ttu-id="c260d-165">Hello İlkesi hello öğeyle ilişkili silindikten sonra hello yedekleme iş akışı hello tanımlı zamanlamasında ilkenin etkisini gösterip.</span><span class="sxs-lookup"><span data-stu-id="c260d-165">Once hello policy has been associated with hello item, hello backup workflow will kick in at hello defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="c260d-166">İlk yedekleme</span><span class="sxs-lookup"><span data-stu-id="c260d-166">Initial backup</span></span>
<span data-ttu-id="c260d-167">Merhaba yedekleme zamanlaması hello tam ilk kopya hello öğesi için ve hello artımlı kopya hello sonraki yedeklemeler için yapma ilgilenebilmek.</span><span class="sxs-lookup"><span data-stu-id="c260d-167">hello backup schedule will take care of doing hello full initial copy for hello item and hello incremental copy for hello subsequent backups.</span></span> <span data-ttu-id="c260d-168">Ancak, tooforce hello ilk yedekleme toohappen belirli bir zamanda veya hatta hemen istiyorsanız sonra hello kullanın **yedekleme AzureRmBackupItem** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c260d-168">However, if you want tooforce hello initial backup toohappen at a certain time or even immediately then use hello **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="c260d-169">hello StartTime saat dilimini hello ve PowerShell içinde gösterilen EndTime alan UTC değil.</span><span class="sxs-lookup"><span data-stu-id="c260d-169">hello timezone of hello StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="c260d-170">Ancak, Hello benzer bilgiler hello Azure portal gösterildiğinde hello saat dilimi hizalanmış tooyour yerel sistem saatini ' dir.</span><span class="sxs-lookup"><span data-stu-id="c260d-170">However, when hello similar information is shown in hello Azure portal, hello timezone is aligned tooyour local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="c260d-171">Bir yedekleme işi izleme</span><span class="sxs-lookup"><span data-stu-id="c260d-171">Monitoring a backup job</span></span>
<span data-ttu-id="c260d-172">Azure Backup çoğu uzun süre çalışan işlemleri, bir iş olarak modelled.</span><span class="sxs-lookup"><span data-stu-id="c260d-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="c260d-173">Bu işlem, her zaman tookeep hello Azure portal açık gerek kalmadan kolay tootrack ilerleme kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="c260d-173">This makes it easy tootrack progress without having tookeep hello Azure portal open at all times.</span></span>

<span data-ttu-id="c260d-174">tooget hello son bir devam eden işin durumunu, kullanım hello **Get-AzureRmBackupJob** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c260d-174">tooget hello latest status of an in-progress job, use hello **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="c260d-175">Bu işleri - gereksiz, ek kod olan - tamamlanması için yoklama yerine basit toouse hello olan **bekleme AzureRmBackupJob** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c260d-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler toouse hello **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="c260d-176">Bir komut dosyası kullanıldığında, hello cmdlet hello işi tamamlar veya hello belirtilen zaman aşımı değerine ulaşılana kadar hello yürütme duraklatılır.</span><span class="sxs-lookup"><span data-stu-id="c260d-176">When used in a script, hello cmdlet will pause hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="c260d-177">Bir Azure VM geri yükleme</span><span class="sxs-lookup"><span data-stu-id="c260d-177">Restore an Azure VM</span></span>
<span data-ttu-id="c260d-178">Sipariş toorestore yedekleme verilerini, hello zaman içinde nokta verilerini tutan hello kurtarma noktası ve madde yedeklenen tooidentify hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="c260d-178">In order toorestore backup data, you need tooidentify hello backed-up Item and hello Recovery Point that holds hello point-in-time data.</span></span> <span data-ttu-id="c260d-179">Bu bilgiler sağlanan toohello geri yükleme-AzureRmBackupItem cmdlet'i tooinitiate hello kasa toohello müşterinin hesap verilerini geri yükleme olur.</span><span class="sxs-lookup"><span data-stu-id="c260d-179">This information is supplied toohello Restore-AzureRmBackupItem cmdlet tooinitiate a restore of data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="c260d-180">Merhaba VM seçin</span><span class="sxs-lookup"><span data-stu-id="c260d-180">Select hello VM</span></span>
<span data-ttu-id="c260d-181">tanımlayan tooget hello PowerShell nesnesi Merhaba doğru yedekleme öğesi, hello kapsayıcı hello kasasında gelen toostart gerekir ve nesne hiyerarşisi aşağı, şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="c260d-181">tooget hello PowerShell object that identifies hello right backup Item, you need toostart from hello Container in hello vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="c260d-182">Merhaba VM, kullanım hello temsil eden tooselect hello kapsayıcı **Get-AzureRmBackupContainer** cmdlet'i ve o toohello kanal **Get-AzureRmBackupItem** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c260d-182">tooselect hello container that represents hello VM, use hello **Get-AzureRmBackupContainer** cmdlet and pipe that toohello **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="c260d-183">Bir kurtarma noktası seçin</span><span class="sxs-lookup"><span data-stu-id="c260d-183">Choose a recovery point</span></span>
<span data-ttu-id="c260d-184">Hello kullanarak hello yedekleme öğesi için tüm hello kurtarma noktalarını şimdi listeleyebilirsiniz **Get-AzureRmBackupRecoveryPoint** cmdlet'ini ve hello kurtarma noktası toorestore'i seçin.</span><span class="sxs-lookup"><span data-stu-id="c260d-184">You can now list all hello recovery points for hello backup item using hello **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose hello recovery point toorestore.</span></span> <span data-ttu-id="c260d-185">Genellikle hello en son kullanıcıların çekme *AppConsistent* noktası hello listesinde.</span><span class="sxs-lookup"><span data-stu-id="c260d-185">Typically users pick hello most recent *AppConsistent* point in hello list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="c260d-186">Merhaba değişkeni ```$rp``` kurtarma noktaları dizisidir hello ters sırada süresini sıralanmış yedekleme öğesi seçili - hello en son kurtarma noktası dizini 0 için.</span><span class="sxs-lookup"><span data-stu-id="c260d-186">hello variable ```$rp``` is an array of recovery points for hello selected backup item, sorted in reverse order of time - hello latest recovery point is at index 0.</span></span> <span data-ttu-id="c260d-187">Standart PowerShell dizi toopick hello kurtarma noktası dizin kullanın.</span><span class="sxs-lookup"><span data-stu-id="c260d-187">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="c260d-188">Örneğin: ```$rp[0]``` hello en son kurtarma noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="c260d-188">For example: ```$rp[0]``` will select hello latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="c260d-189">Diskleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="c260d-189">Restoring disks</span></span>
<span data-ttu-id="c260d-190">Azure PowerShell ve hello Azure portal aracılığıyla yapılır hello geri yükleme işlemleri arasındaki en önemli fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="c260d-190">There is a key difference between hello restore operations done through hello Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="c260d-191">PowerShell ile Merhaba diskleri ve yapılandırma bilgilerini hello kurtarma noktasından geri yükleme sırasında hello geri yükleme işlemi durdurur.</span><span class="sxs-lookup"><span data-stu-id="c260d-191">With PowerShell, hello restore operation stops at restoring hello disks and config information from hello recovery point.</span></span> <span data-ttu-id="c260d-192">Bir sanal makine oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="c260d-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="c260d-193">Merhaba geri yükleme AzureRmBackupItem VM oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="c260d-193">hello Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="c260d-194">Yalnızca hello diskleri geri yükler toohello belirtilen depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="c260d-194">It only restores hello disks toohello specified storage account.</span></span> <span data-ttu-id="c260d-195">Bu olduğu değil hello aynı davranışı hello Azure portal karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="c260d-195">This is not hello same behavior you will experience in hello Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="c260d-196">Hello kullanarak hello geri yükleme işlemi hello ayrıntılarını alabilirsiniz **Get-AzureRmBackupJobDetails** hello geri yükleme işi tamamlandıktan sonra cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c260d-196">You can get hello details of hello restore operation using hello **Get-AzureRmBackupJobDetails** cmdlet once hello Restore job has completed.</span></span> <span data-ttu-id="c260d-197">Merhaba *ErrorDetails* özelliği, toorebuild hello VM hello bilgileri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c260d-197">hello *ErrorDetails* property will have hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a><span data-ttu-id="c260d-198">Merhaba VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="c260d-198">Build hello VM</span></span>
<span data-ttu-id="c260d-199">Yapı hello VM geri hello diskleri dışında yapılabilir hello eski Azure Service Management PowerShell cmdlet'leri, yeni Azure Resource Manager şablonları hello veya hatta hello Azure portal kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c260d-199">Building hello VM out of hello restored disks can be done using hello older Azure Service Management PowerShell cmdlets, hello new Azure Resource Manager templates, or even using hello Azure portal.</span></span> <span data-ttu-id="c260d-200">Hızlı bir örnekte göstereceğiz nasıl tooget hello Azure Hizmet Yönetimi cmdlet'lerini kullanarak vardır.</span><span class="sxs-lookup"><span data-stu-id="c260d-200">In a quick example, we will show how tooget there using hello Azure Service Management cmdlets.</span></span>

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

<span data-ttu-id="c260d-201">Toobuild geri hello disklerden VM hakkında daha fazla bilgi için aşağıdaki cmdlet'leri hello hakkında okuyun:</span><span class="sxs-lookup"><span data-stu-id="c260d-201">For more information on how toobuild a VM from hello restored disks, read about hello following cmdlets:</span></span>

* [<span data-ttu-id="c260d-202">Ekleme AzureDisk</span><span class="sxs-lookup"><span data-stu-id="c260d-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="c260d-203">AzureVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="c260d-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="c260d-204">Yeni-AzureVM</span><span class="sxs-lookup"><span data-stu-id="c260d-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="c260d-205">Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="c260d-205">Code samples</span></span>
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a><span data-ttu-id="c260d-206">1. İş alt görevleri Hello tamamlanma durumunu Al</span><span class="sxs-lookup"><span data-stu-id="c260d-206">1. Get hello completion status of job sub-tasks</span></span>
<span data-ttu-id="c260d-207">tootrack hello tamamlanma durumunu tek tek alt görevler, kullanabileceğiniz hello **Get-AzureRmBackupJobDetails** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c260d-207">tootrack hello completion status of individual sub-tasks, you can use hello **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="c260d-208">2. Yedekleme işleri günlük/haftalık raporunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c260d-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="c260d-209">Yöneticiler genellikle hangi yedekleme işleri hello son 24 saat çalışan tooknow Bu yedekleme işlerini hello durumunu istiyor.</span><span class="sxs-lookup"><span data-stu-id="c260d-209">Administrators typically want tooknow what backup jobs ran in hello last 24 hours, hello status of those backup jobs.</span></span> <span data-ttu-id="c260d-210">Ayrıca, aktarılan veri miktarını hello yolu tooestimate yöneticilere sunar aylık veri kullanımı.</span><span class="sxs-lookup"><span data-stu-id="c260d-210">Additionally, hello amount of data transferred gives administrators a way tooestimate their monthly data usage.</span></span> <span data-ttu-id="c260d-211">Aşağıdaki Hello komut dosyası hello Azure Backup hizmeti hello ham veri çeker ve hello PowerShell konsolunda hello bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c260d-211">hello script below pulls hello raw data from hello Azure Backup service and displays hello information in hello PowerShell console.</span></span>

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -too$enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for hello last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract hello information for hello reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

<span data-ttu-id="c260d-212">Özellikleri toothis rapor çıktısı grafik tooadd istiyorsanız, hello TechNet blog gönderisi öğrenin [PowerShell ile Grafikleme](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="c260d-212">If you want tooadd charting capabilities toothis report output, learn from hello TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c260d-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c260d-213">Next steps</span></span>
<span data-ttu-id="c260d-214">Windows Server, koruma için hello PowerShell makale PowerShell tooengage Azure kaynaklarınızı ile kullanmayı tercih ediyorsanız kullanıma [dağıtma ve yönetme yedekleme için Windows Server](backup-client-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="c260d-214">If you prefer using PowerShell tooengage with your Azure resources, check out hello PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="c260d-215">Ayrıca DPM yedeklemelerini yönetmek için PowerShell makale olduğu [dağıtma ve yönetme yedekleme DPM için](backup-dpm-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="c260d-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="c260d-216">Bu makaleler her ikisi de Resource Manager dağıtımları ve bunun yanı sıra klasik dağıtımlar için bir sürümüne sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="c260d-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
