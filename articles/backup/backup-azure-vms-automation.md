---
title: "aaaDeploy ve PowerShell kullanarak Resource Manager tarafından dağıtılan VM'ler için yedeklemeleri yönetme | Microsoft Docs"
description: "PowerShell toodeploy kullanma ve Resource Manager tarafından dağıtılan VM'ler için Azure yedeklemeleri yönetme"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 68606e4f-536d-4eac-9f80-8a198ea94d52
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/28/2017
ms.author: markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486fb3ae1902403fe6bf303df57244b76677ab17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="0e925-103">Sanal makineler yukarı AzureRM.RecoveryServices.Backup cmdlet'leri tooback kullanın</span><span class="sxs-lookup"><span data-stu-id="0e925-103">Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e925-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0e925-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="0e925-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="0e925-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="0e925-106">Bu makalede nasıl toouse Azure PowerShell cmdlet'leri tooback yedeklemek ve kurtarmak bir Azure sanal makineden (VM) bir kurtarma Hizmetleri kasası gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0e925-106">This article shows you how toouse Azure PowerShell cmdlets tooback up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="0e925-107">Kurtarma Hizmetleri kasası bir Azure Resource Manager kaynak ve kullanılan tooprotect veri ve varlıkların Azure Backup ve Azure Site Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0e925-107">A Recovery Services vault is an Azure Resource Manager resource and is used tooprotect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="0e925-108">Kurtarma Hizmetleri kasası tooprotect Azure Service Manager tarafından dağıtılan VM'ler ve Azure Resource Manager tarafından dağıtılan VM'ler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e925-108">You can use a Recovery Services vault tooprotect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="0e925-109">Azure'da kaynak oluşturmaya ve kaynaklarla çalışmaya yönelik iki dağıtım modeli mevcuttur: [Resource Manager ve Klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0e925-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0e925-110">Bu makalede hello Resource Manager modeli kullanılarak oluşturulan VM ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0e925-110">This article is for use with VMs created using hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="0e925-111">Bu makalede PowerShell tooprotect kullanarak bir VM ve verileri geri yüklemek bir kurtarma noktasından anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0e925-111">This article walks you through using PowerShell tooprotect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="0e925-112">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="0e925-112">Concepts</span></span>
<span data-ttu-id="0e925-113">Merhaba hello hizmeti, genel bir bakış için Azure Backup hizmeti hakkında bilgi sahibi değilseniz kullanıma [Azure Backup nedir?](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="0e925-113">If you are not familiar with hello Azure Backup service, for an overview of hello service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="0e925-114">Başlamadan önce Azure yedekleme ile Merhaba gerekli Önkoşullar toowork hakkında hello essentials kapsar ve hello geçerli VM yedekleme çözümü sınırlamaları hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="0e925-114">Before you start, ensure that you cover hello essentials about hello prerequisites needed toowork with Azure Backup, and hello limitations of hello current VM backup solution.</span></span>

<span data-ttu-id="0e925-115">toouse PowerShell etkili bir şekilde, gerekli toounderstand hello hiyerarşi nesnelerin ve nerede olduğunu toostart.</span><span class="sxs-lookup"><span data-stu-id="0e925-115">toouse PowerShell effectively, it is necessary toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Kurtarma Hizmetleri nesne hiyerarşisi](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="0e925-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet başvurusunun bkz hello [Azure Backup - kurtarma Hizmetleri cmdlet'leri](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) hello Azure kitaplığı içinde.</span><span class="sxs-lookup"><span data-stu-id="0e925-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see hello [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="0e925-118">Kurulumu'nu ve kaydı</span><span class="sxs-lookup"><span data-stu-id="0e925-118">Setup and Registration</span></span>
<span data-ttu-id="0e925-119">toobegin:</span><span class="sxs-lookup"><span data-stu-id="0e925-119">toobegin:</span></span>

1. <span data-ttu-id="0e925-120">[Merhaba PowerShell'in en son sürümünü indirme](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (gerekli hello minimum sürüm: 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="0e925-120">[Download hello latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="0e925-121">Hello Azure yedekleme PowerShell cmdlet'leri kullanılabilir hello aşağıdaki komutu yazarak bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0e925-121">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

```
PS C:\> Get-Command *azurermrecoveryservices*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmRecoveryServicesBackupItem           1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Disable-AzureRmRecoveryServicesBackupProtection    1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Enable-AzureRmRecoveryServicesBackupProtection     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupContainer         1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupItem              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJob               1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJobDetails        1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupManagementServer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRMRecoveryServicesBackupRecoveryPoint     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupRetentionPolic... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupSchedulePolicy... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesVaultSettingsFile       1.4.0      AzureRM.RecoveryServices
Cmdlet          New-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          New-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Remove-AzureRmRecoveryServicesProtectionPolicy     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Remove-AzureRmRecoveryServicesVault                1.4.0      AzureRM.RecoveryServices
Cmdlet          Restore-AzureRMRecoveryServicesBackupItem          1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Set-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesVaultContext            1.4.0      AzureRM.RecoveryServices
Cmdlet          Stop-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupContainer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupManagem... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Wait-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
```


<span data-ttu-id="0e925-122">Merhaba görevleri aşağıdaki PowerShell ile otomatik olarak yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="0e925-122">hello following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="0e925-123">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e925-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="0e925-124">Azure VM'lerini yedekleme</span><span class="sxs-lookup"><span data-stu-id="0e925-124">Back up Azure VMs</span></span>
* <span data-ttu-id="0e925-125">Bir yedekleme işi tetikleyeceğinden</span><span class="sxs-lookup"><span data-stu-id="0e925-125">Trigger a backup job</span></span>
* <span data-ttu-id="0e925-126">İzleyici bir yedekleme işi</span><span class="sxs-lookup"><span data-stu-id="0e925-126">Monitor a backup job</span></span>
* <span data-ttu-id="0e925-127">Bir Azure VM geri yükleme</span><span class="sxs-lookup"><span data-stu-id="0e925-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="0e925-128">Kurtarma hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e925-128">Create a recovery services vault</span></span>
<span data-ttu-id="0e925-129">Aşağıdaki adımları hello kurtarma Hizmetleri kasası oluşturmada size yol açar.</span><span class="sxs-lookup"><span data-stu-id="0e925-129">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="0e925-130">Kurtarma Hizmetleri kasasına yedekleme Kasası ' farklıdır.</span><span class="sxs-lookup"><span data-stu-id="0e925-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="0e925-131">Azure Backup hello için ilk kez kullanıyorsanız hello kullanmalısınız  **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  cmdlet tooregister hello Azure Recovery hizmeti sağlayıcısı aboneliğinizle.</span><span class="sxs-lookup"><span data-stu-id="0e925-131">If you are using Azure Backup for hello first time, you must use hello **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="0e925-132">tooplace ihtiyacınız hello kurtarma Hizmetleri kasası bir Resource Manager kaynak olduğundan, bir kaynak grubu içinde.</span><span class="sxs-lookup"><span data-stu-id="0e925-132">hello Recovery Services vault is a Resource Manager resource, so you need tooplace it within a resource group.</span></span> <span data-ttu-id="0e925-133">Varolan bir kaynak grubunu kullanın veya bir kaynak grubu ile Merhaba oluşturmak  **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0e925-133">You can use an existing resource group, or create a resource group with hello **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="0e925-134">Bir kaynak grubu oluştururken hello kaynak grubu için hello ad ve konum belirtin.</span><span class="sxs-lookup"><span data-stu-id="0e925-134">When creating a resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="0e925-135">Kullanım hello  **[yeni AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  kurtarma Hizmetleri kasası cmdlet toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="0e925-135">Use hello **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet toocreate hello Recovery Services vault.</span></span> <span data-ttu-id="0e925-136">Toospecify hello hello kasa için aynı konumu hello kaynak grubu için kullanıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="0e925-136">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="0e925-137">Depolama artıklık toouse Hello türünü belirtin; kullanabileceğiniz [yerel olarak yedekli depolama (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) veya [coğrafi olarak yedekli depolama (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="0e925-137">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="0e925-138">Merhaba aşağıdaki örnek tooGeoRedundant testvault için hello - BackupStorageRedundancy seçeneği ayarlanmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e925-138">hello following example shows hello -BackupStorageRedundancy option for testvault is set tooGeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="0e925-139">Çok sayıda Azure yedekleme cmdlet'lerini girdi olarak hello kurtarma Hizmetleri kasası nesnesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0e925-139">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="0e925-140">Bu nedenle, bu kullanışlı toostore hello yedekleme kurtarma Hizmetleri kasası, bir değişkende nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="0e925-140">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="0e925-141">Bir abonelikte görünüm hello kasaları</span><span class="sxs-lookup"><span data-stu-id="0e925-141">View hello vaults in a subscription</span></span>
<span data-ttu-id="0e925-142">Kullanım  **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview hello hello geçerli Abonelikteki tüm kasalarının listesi.</span><span class="sxs-lookup"><span data-stu-id="0e925-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="0e925-143">Bu komut toocheck yeni bir kasa oluşturulduğunu veya toosee hello hello Abonelikteki kullanılabilir kasalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e925-143">You can use this command toocheck that a new vault was created, or toosee hello available vaults in hello subscription.</span></span>

<span data-ttu-id="0e925-144">Merhaba komutu, Get-AzureRmRecoveryServicesVault tooview hello aboneliğindeki tüm kasalarını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e925-144">Run hello command, Get-AzureRmRecoveryServicesVault, tooview all vaults in hello subscription.</span></span> <span data-ttu-id="0e925-145">Merhaba aşağıdaki örnekte her kasa için görüntülenen hello bilgiler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0e925-145">hello following example shows hello information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="0e925-146">Azure VM'lerini yedekleme</span><span class="sxs-lookup"><span data-stu-id="0e925-146">Back up Azure VMs</span></span>
<span data-ttu-id="0e925-147">Kurtarma Hizmetleri kasası tooprotect sanal makinelerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e925-147">Use a Recovery Services vault tooprotect your virtual machines.</span></span> <span data-ttu-id="0e925-148">Merhaba koruma uygulamadan önce set hello kasası bağlam (Merhaba kasasına korunan verileri hello türü) ve hello koruma ilkesini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0e925-148">Before you apply hello protection, set hello vault context (hello type of data protected in hello vault), and verify hello protection policy.</span></span> <span data-ttu-id="0e925-149">Merhaba koruma hello yedekleme işleri çalıştırdığınızda hello zamanlama ve her yedekleme anlık görüntüsünü ne kadar süreyle tutulduğunu ilkesidir.</span><span class="sxs-lookup"><span data-stu-id="0e925-149">hello protection policy is hello schedule when hello backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="0e925-150">Set kasası bağlamı</span><span class="sxs-lookup"><span data-stu-id="0e925-150">Set vault context</span></span>
<span data-ttu-id="0e925-151">Bir VM korumasını etkinleştirmeden önce kullanmak  **[kümesi AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset hello kasası bağlamı.</span><span class="sxs-lookup"><span data-stu-id="0e925-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context.</span></span> <span data-ttu-id="0e925-152">Merhaba kasası bağlam ayarladıktan sonra tooall sonraki cmdlet'leri geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0e925-152">Once hello vault context is set, it applies tooall subsequent cmdlets.</span></span> <span data-ttu-id="0e925-153">Merhaba aşağıdaki örnek hello kasası bağlamı hello kasası için ayarlar *testvault*.</span><span class="sxs-lookup"><span data-stu-id="0e925-153">hello following example sets hello vault context for hello vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="0e925-154">Bir koruma ilkesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="0e925-154">Create a protection policy</span></span>
<span data-ttu-id="0e925-155">Kurtarma Hizmetleri kasası oluşturduğunuzda, varsayılan koruma ve bekletme ilkeleri ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="0e925-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="0e925-156">Merhaba varsayılan koruma İlkesi, bir yedekleme işi her gün belirtilen zamanda tetikler.</span><span class="sxs-lookup"><span data-stu-id="0e925-156">hello default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="0e925-157">Merhaba varsayılan bekletme ilkesi hello günlük kurtarma noktası 30 gün boyunca korur.</span><span class="sxs-lookup"><span data-stu-id="0e925-157">hello default retention policy retains hello daily recovery point for 30 days.</span></span> <span data-ttu-id="0e925-158">Merhaba varsayılan kullanabileceğiniz ilke tooquickly VM korumak ve daha sonra farklı ayrıntılarla hello İlkesi Düzenle.</span><span class="sxs-lookup"><span data-stu-id="0e925-158">You can use hello default policy tooquickly protect your VM and edit hello policy later with different details.</span></span>

<span data-ttu-id="0e925-159">Kullanım  **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview hello koruma ilkeleri hello kasasında.</span><span class="sxs-lookup"><span data-stu-id="0e925-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** tooview hello protection policies in hello vault.</span></span> <span data-ttu-id="0e925-160">Bu cmdlet tooget belirli bir ilke veya bir iş yükü türüyle ilişkili tooview hello ilkelerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e925-160">You can use this cmdlet tooget a specific policy, or tooview hello policies associated with a workload type.</span></span> <span data-ttu-id="0e925-161">Aşağıdaki örneğine hello iş yükü türünün AzureVM ilkelerini alır.</span><span class="sxs-lookup"><span data-stu-id="0e925-161">hello following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="0e925-162">PowerShell'de hello BackupTime alanının Hello saat dilimi UTC değil.</span><span class="sxs-lookup"><span data-stu-id="0e925-162">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="0e925-163">Merhaba yedekleme saati hello Azure portal gösterildiğinde, ancak hello ayarlanmış tooyour yerel saat dilimi saattir.</span><span class="sxs-lookup"><span data-stu-id="0e925-163">However, when hello backup time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

<span data-ttu-id="0e925-164">En az bir bekletme ilkesiyle ilişkili bir yedekleme koruma ilkesidir.</span><span class="sxs-lookup"><span data-stu-id="0e925-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="0e925-165">Bekletme İlkesi silinmeden önce ne kadar bir kurtarma noktası tutulur tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0e925-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="0e925-166">Kullanım  **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  tooview hello varsayılan bekletme ilkesi.</span><span class="sxs-lookup"><span data-stu-id="0e925-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** tooview hello default retention policy.</span></span>  <span data-ttu-id="0e925-167">Benzer şekilde kullanabilirsiniz  **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  tooobtain hello varsayılan zamanlama ilkesi.</span><span class="sxs-lookup"><span data-stu-id="0e925-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** tooobtain hello default schedule policy.</span></span> <span data-ttu-id="0e925-168">Merhaba  **[yeni AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet'i, yedekleme ilkesi bilgilerini tutan bir PowerShell nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0e925-168">hello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="0e925-169">Merhaba zamanlama ve Bekletme İlkesi nesneleri toohello girdi olarak kullanılan  **[yeni AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0e925-169">hello schedule and retention policy objects are used as inputs toohello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="0e925-170">Merhaba aşağıdaki örnek hello zamanlama ilkesi ve hello bekletme ilkesi değişkenleri depolar.</span><span class="sxs-lookup"><span data-stu-id="0e925-170">hello following example stores hello schedule policy and hello retention policy in variables.</span></span> <span data-ttu-id="0e925-171">Merhaba örnek, bir koruma ilkesi oluşturulurken bu değişkenleri toodefine hello parametreleri kullanır *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="0e925-171">hello example uses those variables toodefine hello parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="0e925-172">Korumayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="0e925-172">Enable protection</span></span>
<span data-ttu-id="0e925-173">Merhaba yedekleme koruma İlkesi tanımladıktan sonra bir öğe için hello İlkesi hala etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e925-173">Once you have defined hello backup protection policy, you still must enable hello policy for an item.</span></span> <span data-ttu-id="0e925-174">Kullanım  **[etkinleştir AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable koruma.</span><span class="sxs-lookup"><span data-stu-id="0e925-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** tooenable protection.</span></span> <span data-ttu-id="0e925-175">Koruma etkinleştirme iki nesne - hello öğesi ve hello İlkesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0e925-175">Enabling protection requires two objects - hello item and hello policy.</span></span> <span data-ttu-id="0e925-176">Hello İlkesi hello kasası ile ilişkilendirildikten sonra hello yedekleme iş akışı hello İlkesi zamanlamasında tanımlanan hello zaman tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="0e925-176">Once hello policy has been associated with hello vault, hello backup workflow is triggered at hello time defined in hello policy schedule.</span></span>

<span data-ttu-id="0e925-177">Hello İlkesi, NewPolicy kullanarak örnek etkinleştirir korumayı hello öğesi, V2VM, için aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="0e925-177">hello following example enables protection for hello item, V2VM, using hello policy, NewPolicy.</span></span> <span data-ttu-id="0e925-178">Resource Manager vm'lerde şifrelenmemiş tooenable hello koruma</span><span class="sxs-lookup"><span data-stu-id="0e925-178">tooenable hello protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="0e925-179">(BEK ve KEK kullanılarak şifrelenmiş) VM'ler tooenable hello koruması şifreli, toogive hello Azure Backup hizmeti izni tooread anahtarları ve gizli anahtar Kasası'ndan gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e925-179">tooenable hello protection on encrypted VMs (encrypted using BEK and KEK), you need toogive hello Azure Backup service permission tooread keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="0e925-180">(yalnızca BEK kullanılarak şifrelenmiş) VM'ler tooenable hello koruması şifreli, toogive hello Azure Backup hizmeti izni tooread gizli anahtar Kasası'ndan gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e925-180">tooenable hello protection on encrypted VMs (encrypted using BEK only), you need toogive hello Azure Backup service permission tooread secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="0e925-181">Hello Azure Bulutu kullanıyorsanız, hello değeri ff281ffe-705c-4f53-9f37-a40e6f2c68f3 hello parametre için kullanmak **- ServicePrincipalName** içinde [kümesi AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet'i .</span><span class="sxs-lookup"><span data-stu-id="0e925-181">If you are using hello Azure Government cloud, then use hello value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for hello parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="0e925-182">Klasik VM'ler için</span><span class="sxs-lookup"><span data-stu-id="0e925-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="0e925-183">Bir koruma ilkesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="0e925-183">Modify a protection policy</span></span>
<span data-ttu-id="0e925-184">toomodify hello koruma İlkesi, kullanım [kümesi AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy veya RetentionPolicy nesne.</span><span class="sxs-lookup"><span data-stu-id="0e925-184">toomodify hello protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="0e925-185">Merhaba aşağıdaki örnek hello kurtarma noktası bekletme too365 gün değiştirir.</span><span class="sxs-lookup"><span data-stu-id="0e925-185">hello following example changes hello recovery point retention too365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="0e925-186">Bir yedeklemeyi tetikleyin</span><span class="sxs-lookup"><span data-stu-id="0e925-186">Trigger a backup</span></span>
<span data-ttu-id="0e925-187">Kullanabileceğiniz  **[yedekleme AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger bir yedekleme işi.</span><span class="sxs-lookup"><span data-stu-id="0e925-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** tootrigger a backup job.</span></span> <span data-ttu-id="0e925-188">Bunu hello ilk yedekleme ise, tam yedekleme olur.</span><span class="sxs-lookup"><span data-stu-id="0e925-188">If it is hello initial backup, it is a full backup.</span></span> <span data-ttu-id="0e925-189">Sonraki yedek bir artımlı kopya alabilir.</span><span class="sxs-lookup"><span data-stu-id="0e925-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="0e925-190">Emin toouse olması  **[kümesi AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  hello yedekleme işini tetiklemeden önce tooset hello kasası bağlamı.</span><span class="sxs-lookup"><span data-stu-id="0e925-190">Be sure toouse **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context before triggering hello backup job.</span></span> <span data-ttu-id="0e925-191">Aşağıdaki örnek hello kasası bağlamını ayarlayın varsayar.</span><span class="sxs-lookup"><span data-stu-id="0e925-191">hello following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="0e925-192">PowerShell hello StartTime ve EndTime alanların Hello saat dilimi UTC değil.</span><span class="sxs-lookup"><span data-stu-id="0e925-192">hello timezone of hello StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="0e925-193">Hello zaman hello Azure portal gösterilir, ancak hello zaman ayarlanmış tooyour yerel saat dilimi zamandır.</span><span class="sxs-lookup"><span data-stu-id="0e925-193">However, when hello time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="0e925-194">Bir yedekleme işi izleme</span><span class="sxs-lookup"><span data-stu-id="0e925-194">Monitoring a backup job</span></span>
<span data-ttu-id="0e925-195">Hello Azure portalını kullanmadan yedekleme işleri gibi uzun süre çalışan işlemleri izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e925-195">You can monitor long-running operations, such as backup jobs, without using hello Azure portal.</span></span> <span data-ttu-id="0e925-196">tooget hello kullan hello bir devam eden işin durumunu  **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0e925-196">tooget hello status of an in-progress job, use hello **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="0e925-197">Merhaba yedekleme işleri belirli bir kasa için bu cmdlet'i alır ve bu kasası hello kasası bağlamda belirtilir.</span><span class="sxs-lookup"><span data-stu-id="0e925-197">This cmdlet gets hello backup jobs for a specific vault, and that vault is specified in hello vault context.</span></span> <span data-ttu-id="0e925-198">Hello aşağıdaki örnekte bir dizi olarak devam eden işi hello durumunu alır ve hello durum hello $joblist değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="0e925-198">hello following example gets hello status of an in-progress job as an array, and stores hello status in hello $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="0e925-199">Bu işleri - gereksiz ek kod olan - tamamlanması için yoklama yerine hello kullan  **[bekleme AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0e925-199">Instead of polling these jobs for completion - which is unnecessary additional code - use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="0e925-200">Bu cmdlet hello yürütme hello işi tamamlar veya hello belirtilen zaman aşımı değerine ulaşılana kadar duraklar.</span><span class="sxs-lookup"><span data-stu-id="0e925-200">This cmdlet pauses hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="0e925-201">Bir Azure VM geri yükleme</span><span class="sxs-lookup"><span data-stu-id="0e925-201">Restore an Azure VM</span></span>
<span data-ttu-id="0e925-202">Hello Azure portal kullanarak ve PowerShell kullanarak bir VM'i geri VM geri hello arasındaki en önemli fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="0e925-202">There is a key difference between hello restoring a VM using hello Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="0e925-203">PowerShell ile Merhaba diskleri ve yapılandırma bilgilerini hello kurtarma noktasından oluşturulduktan sonra hello geri yükleme işlemi tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="0e925-203">With PowerShell, hello restore operation is complete once hello disks and configuration information from hello recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="0e925-204">Merhaba geri yükleme işlemi, bir sanal makine oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="0e925-204">hello restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="0e925-205">disk, sanal makineden toocreate hello bölümüne bakın [saklı disklerden oluşturma hello VM](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="0e925-205">toocreate a virtual machine from disk, see hello section, [Create hello VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="0e925-206">Merhaba temel adımlar toorestore bir Azure VM şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0e925-206">hello basic steps toorestore an Azure VM are:</span></span>

* <span data-ttu-id="0e925-207">Merhaba VM seçin</span><span class="sxs-lookup"><span data-stu-id="0e925-207">Select hello VM</span></span>
* <span data-ttu-id="0e925-208">Bir kurtarma noktası seçin</span><span class="sxs-lookup"><span data-stu-id="0e925-208">Choose a recovery point</span></span>
* <span data-ttu-id="0e925-209">Merhaba disklerini geri yükle</span><span class="sxs-lookup"><span data-stu-id="0e925-209">Restore hello disks</span></span>
* <span data-ttu-id="0e925-210">Saklı disklerden Hello VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e925-210">Create hello VM from stored disks</span></span>

<span data-ttu-id="0e925-211">Merhaba aşağıdaki grafikte hello nesne hello RecoveryServicesVault toohello BackupRecoveryPoint aşağı hiyerarşiden gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e925-211">hello following graphic shows hello object hierarchy from hello RecoveryServicesVault down toohello BackupRecoveryPoint.</span></span>

![Kurtarma Hizmetleri nesne hiyerarşisi BackupContainer gösterme](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="0e925-213">toorestore yedekleme verilerini hello yedeklenen öğesi ve hello zaman içinde nokta verilerini tutan hello kurtarma noktası belirleyin.</span><span class="sxs-lookup"><span data-stu-id="0e925-213">toorestore backup data, identify hello backed-up item and hello recovery point that holds hello point-in-time data.</span></span> <span data-ttu-id="0e925-214">Kullanım hello  **[geri yükleme AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  hello cmdlet toorestore verileri kasa toohello müşterinin hesap.</span><span class="sxs-lookup"><span data-stu-id="0e925-214">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="0e925-215">Merhaba VM seçin</span><span class="sxs-lookup"><span data-stu-id="0e925-215">Select hello VM</span></span>
<span data-ttu-id="0e925-216">sağ hello tanımlayan tooget hello PowerShell nesnesi öğesi yedekleme, hello kasasında hello kapsayıcısından Başlat ve yolunuzu hello nesne hiyerarşisi aşağı çalışma.</span><span class="sxs-lookup"><span data-stu-id="0e925-216">tooget hello PowerShell object that identifies hello right backup item, start from hello container in hello vault, and work your way down hello object hierarchy.</span></span> <span data-ttu-id="0e925-217">Merhaba VM, kullanım hello temsil eden tooselect hello kapsayıcı  **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet'i ve o toohello kanal  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0e925-217">tooselect hello container that represents hello VM, use hello **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that toohello **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="0e925-218">Bir kurtarma noktası seçin</span><span class="sxs-lookup"><span data-stu-id="0e925-218">Choose a recovery point</span></span>
<span data-ttu-id="0e925-219">Kullanım hello  **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  tüm kurtarma noktaları için yedekleme öğesi hello cmdlet toolist.</span><span class="sxs-lookup"><span data-stu-id="0e925-219">Use hello **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet toolist all recovery points for hello backup item.</span></span> <span data-ttu-id="0e925-220">Ardından hello kurtarma noktası toorestore seçin.</span><span class="sxs-lookup"><span data-stu-id="0e925-220">Then choose hello recovery point toorestore.</span></span> <span data-ttu-id="0e925-221">Hangi kurtarma noktası toouse konusunda emin değilseniz, iyi bir uygulama toochoose hello en son RecoveryPointType olduğu AppConsistent noktası hello listesinde =.</span><span class="sxs-lookup"><span data-stu-id="0e925-221">If you are unsure which recovery point toouse, it is a good practice toochoose hello most recent RecoveryPointType = AppConsistent point in hello list.</span></span>

<span data-ttu-id="0e925-222">Değişken, komut dosyası izleyen hello hello **$rp**, hello yedekleme öğesi hello son yedi gün seçilen için kurtarma noktaları dizisidir.</span><span class="sxs-lookup"><span data-stu-id="0e925-222">In hello following script, hello variable, **$rp**, is an array of recovery points for hello selected backup item, from hello past seven days.</span></span> <span data-ttu-id="0e925-223">Merhaba dizisi hello en son kurtarma noktası dizin 0 konumunda ile süreyi ters sırada sıralanır.</span><span class="sxs-lookup"><span data-stu-id="0e925-223">hello array is sorted in reverse order of time with hello latest recovery point at index 0.</span></span> <span data-ttu-id="0e925-224">Standart PowerShell dizi toopick hello kurtarma noktası dizin kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e925-224">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="0e925-225">Merhaba örnekte $rp [0] hello en son kurtarma noktası seçer.</span><span class="sxs-lookup"><span data-stu-id="0e925-225">In hello example, $rp[0] selects hello latest recovery point.</span></span>

```
PS C:\> $startDate = (Get-Date).AddDays(-7)
PS C:\> $endDate = Get-Date
PS C:\> $rp = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $backupitem -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
PS C:\> $rp[0]
RecoveryPointAdditionalInfo :
SourceVMStorageType         : NormalStorage
Name                        : 15260861925810
ItemName                    : VM;iaasvmcontainer;RGName1;V2VM
RecoveryPointId             : /subscriptions/XX/resourceGroups/ RGName1/providers/Microsoft.RecoveryServices/vaults/testvault/backupFabrics/Azure/protectionContainers/IaasVMContainer;iaasvmcontainer;RGName1;V2VM/protectedItems/VM;iaasvmcontainer; RGName1;V2VM/recoveryPoints/15260861925810
RecoveryPointType           : AppConsistent
RecoveryPointTime           : 4/23/2016 5:02:04 PM
WorkloadType                : AzureVM
ContainerName               : IaasVMContainer;iaasvmcontainer; RGName1;V2VM
ContainerType               : AzureVM
BackupManagementType        : AzureVM
```



### <a name="restore-hello-disks"></a><span data-ttu-id="0e925-226">Merhaba disklerini geri yükle</span><span class="sxs-lookup"><span data-stu-id="0e925-226">Restore hello disks</span></span>
<span data-ttu-id="0e925-227">Kullanım hello  **[geri yükleme AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore bir yedekleme öğesi'nin veri ve yapılandırma tooa kurtarma noktası.</span><span class="sxs-lookup"><span data-stu-id="0e925-227">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore a backup item's data and configuration tooa recovery point.</span></span> <span data-ttu-id="0e925-228">Bir kurtarma noktası belirledikten sonra Merhaba hello değeri olarak kullanma **- RecoveryPoint** parametresi.</span><span class="sxs-lookup"><span data-stu-id="0e925-228">Once you have identified a recovery point, use it as hello value for hello **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="0e925-229">Merhaba önceki örnek kodda **$rp [0]** hello kurtarma noktası toouse oluştu.</span><span class="sxs-lookup"><span data-stu-id="0e925-229">In hello previous sample code, **$rp[0]** was hello recovery point toouse.</span></span> <span data-ttu-id="0e925-230">Örnek kod, aşağıdaki hello içinde **$rp [0]** hello disk geri yüklemek için hello kurtarma noktası toouse değil.</span><span class="sxs-lookup"><span data-stu-id="0e925-230">In hello following sample code, **$rp[0]** is hello recovery point toouse for restoring hello disk.</span></span>

<span data-ttu-id="0e925-231">toorestore hello diskleri ve yapılandırma bilgileri:</span><span class="sxs-lookup"><span data-stu-id="0e925-231">toorestore hello disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="0e925-232">Kullanım hello  **[bekleme AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  hello geri yükleme işi toocomplete için cmdlet toowait.</span><span class="sxs-lookup"><span data-stu-id="0e925-232">Use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet toowait for hello Restore job toocomplete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="0e925-233">Merhaba geri yükleme işi tamamlandıktan sonra hello kullan  **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  cmdlet tooget hello hello ayrıntılarını geri yükleme işlemi.</span><span class="sxs-lookup"><span data-stu-id="0e925-233">Once hello Restore job has completed, use hello **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet tooget hello details of hello restore operation.</span></span> <span data-ttu-id="0e925-234">Merhaba JobDetails özelliği hello bilgi gerekli toorebuild hello VM sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0e925-234">hello JobDetails property has hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="0e925-235">Merhaba diskleri geri sonra toohello sonraki bölümde toocreate hello VM gidin.</span><span class="sxs-lookup"><span data-stu-id="0e925-235">Once you restore hello disks, go toohello next section toocreate hello VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="0e925-236">Geri yüklenen disklerden bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e925-236">Create a VM from restored disks</span></span>
<span data-ttu-id="0e925-237">Merhaba diskleri geri yükledikten sonra bu adımları toocreate kullanın ve diskten hello sanal makine yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0e925-237">After you have restored hello disks, use these steps toocreate and configure hello virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="0e925-238">geri yüklenen disklerden toocreate şifreli VM'ler, Azure rolünüzün izin tooperform hello eylem olmalıdır **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="0e925-238">toocreate encrypted VMs from restored disks, your Azure role must have permission tooperform hello action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="0e925-239">Özel bir rol rolünüzün bu izne sahip değilse bu eylemle oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e925-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="0e925-240">Daha fazla bilgi için bkz: [Azure rbac'de özel roller](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0e925-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="0e925-241">Sorgu hello hello iş ayrıntılarını disk özelliklerini geri.</span><span class="sxs-lookup"><span data-stu-id="0e925-241">Query hello restored disk properties for hello job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="0e925-242">Hello Azure depolama bağlamını ayarlayın ve hello JSON yapılandırma dosyasını geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0e925-242">Set hello Azure storage context and restore hello JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="0e925-243">Merhaba JSON yapılandırma dosyası toocreate hello VM yapılandırması kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e925-243">Use hello JSON configuration file toocreate hello VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="0e925-244">Merhaba işletim sistemi diski ve veri diskleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e925-244">Attach hello OS disk and data disks.</span></span> <span data-ttu-id="0e925-245">Vm'leriniz Hello yapılandırmasına bağlı olarak hello ilgili bağlantı tooview ilgili cmdlet'leri tıklatın:</span><span class="sxs-lookup"><span data-stu-id="0e925-245">Depending on hello configuration of your VMs, click on hello relevant link tooview respective cmdlets:</span></span> 
    - [<span data-ttu-id="0e925-246">Yönetilmeyen, şifrelenmemiş VM'ler</span><span class="sxs-lookup"><span data-stu-id="0e925-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="0e925-247">Yönetilmeyen, şifrelenmiş VM'ler (yalnızca BEK)</span><span class="sxs-lookup"><span data-stu-id="0e925-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="0e925-248">Yönetilmeyen, şifrelenmiş VM'ler (BEK ve KEK)</span><span class="sxs-lookup"><span data-stu-id="0e925-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="0e925-249">Yönetilen, şifrelenmemiş VM'ler</span><span class="sxs-lookup"><span data-stu-id="0e925-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="0e925-250">Yönetilen, şifrelenmiş VM'ler (BEK ve KEK)</span><span class="sxs-lookup"><span data-stu-id="0e925-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="0e925-251">Yönetilmeyen, şifrelenmemiş VM'ler</span><span class="sxs-lookup"><span data-stu-id="0e925-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="0e925-252">Yönetilmeyen, şifrelenmemiş VM'ler için örnek aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e925-252">Use hello following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="0e925-253">Yönetilmeyen, şifrelenmiş VM'ler (yalnızca BEK)</span><span class="sxs-lookup"><span data-stu-id="0e925-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="0e925-254">Diskleri ekleyebilirsiniz (BEK yalnızca kullanılarak şifrelenmiş) yönetilmeyen, şifrelenmiş VM'ler için toorestore hello gizli toohello anahtar kasası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e925-254">For non-managed, encrypted VMs (encrypted using BEK only), you need toorestore hello secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="0e925-255">Daha fazla bilgi için lütfen hello makalesine bakın [şifrelenmiş bir sanal makine bir Azure yedekleme kurtarma noktasından geri](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="0e925-255">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="0e925-256">Aşağıdaki örnek hello nasıl VM'ler tooattach işletim sistemi ve veri diskleri için şifrelenmiş gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e925-256">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="0e925-257">Yönetilmeyen, şifrelenmiş VM'ler (BEK ve KEK)</span><span class="sxs-lookup"><span data-stu-id="0e925-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="0e925-258">Diskleri eklemeden önce (BEK ve KEK kullanılarak şifrelenmiş) yönetilmeyen, şifrelenmiş VM'ler için toorestore hello anahtarı ve gizli toohello anahtar kasası gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e925-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need toorestore hello key and secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="0e925-259">Daha fazla bilgi için lütfen hello makalesine bakın [şifrelenmiş bir sanal makine bir Azure yedekleme kurtarma noktasından geri](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="0e925-259">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="0e925-260">Aşağıdaki örnek hello nasıl VM'ler tooattach işletim sistemi ve veri diskleri için şifrelenmiş gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e925-260">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="0e925-261">Yönetilen, şifrelenmemiş VM'ler</span><span class="sxs-lookup"><span data-stu-id="0e925-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="0e925-262">Yönetilen şifrelenmemiş VM'ler için blob depolama biriminden yönetilen toocreate diskiniz olması gerekir ve hello diskleri bağlamanız.</span><span class="sxs-lookup"><span data-stu-id="0e925-262">For managed non-encrypted VMs, you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="0e925-263">Ayrıntılı bilgi için hello makalesine bakın [bir veri diski tooa Windows VM ekleme PowerShell kullanarak](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0e925-263">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="0e925-264">Aşağıdaki örnek kod hello nasıl tooattach hello veri diskleri yönetilen şifrelenmemiş VM'ler için gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e925-264">hello following sample code shows how tooattach hello data disks for managed non-encrypted VMs.</span></span>

    ```
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="0e925-265">Yönetilen, şifrelenmiş VM'ler (BEK ve KEK)</span><span class="sxs-lookup"><span data-stu-id="0e925-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="0e925-266">(BEK ve KEK kullanılarak şifrelenmiş), şifrelenmiş yönetilen VM'ler blob depolama biriminden yönetilen toocreate diskiniz olması gerekir ve hello diskleri bağlamanız.</span><span class="sxs-lookup"><span data-stu-id="0e925-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="0e925-267">Ayrıntılı bilgi için hello makalesine bakın [bir veri diski tooa Windows VM ekleme PowerShell kullanarak](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0e925-267">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="0e925-268">Merhaba aşağıdaki örnek kod nasıl tooattach hello veri diskleri yönetilen şifrelenmiş VM'ler için gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e925-268">hello following sample code shows how tooattach hello data disks for managed encrypted VMs.</span></span>

     ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

5. <span data-ttu-id="0e925-269">Merhaba ağ ayarlarını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="0e925-269">Set hello Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="0e925-270">Merhaba sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e925-270">Create hello virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="0e925-271">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e925-271">Next steps</span></span>
<span data-ttu-id="0e925-272">Azure kaynaklarınızı toouse PowerShell tooengage tercih ederseniz, bkz: hello PowerShell makale [dağıtma ve yönetme yedekleme için Windows Server](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="0e925-272">If you prefer toouse PowerShell tooengage with your Azure resources, see hello PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="0e925-273">DPM yedeklemelerini yönetme, hello makalesine bakın. [dağıtma ve yönetme yedekleme DPM için](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="0e925-273">If you manage DPM backups, see hello article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="0e925-274">Bu makaleler her ikisi de Resource Manager dağıtımları ve klasik dağıtımları için bir sürümüne sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e925-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
