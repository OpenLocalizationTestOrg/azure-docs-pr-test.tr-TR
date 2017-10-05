---
title: "Dağıtma ve PowerShell kullanarak Resource Manager tarafından dağıtılan VM'ler için yedeklemeleri yönetme | Microsoft Docs"
description: "Dağıtma yedeklemeler ve Azure Resource Manager tarafından dağıtılan VM'ler için yönetmek için PowerShell kullanma"
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
ms.openlocfilehash: 861346a50df6641abb9e454644228146e14b4078
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="3c548-103">Sanal makineleri yedeklemek için AzureRM.RecoveryServices.Backup cmdlet'leri kullanın</span><span class="sxs-lookup"><span data-stu-id="3c548-103">Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c548-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3c548-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="3c548-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="3c548-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="3c548-106">Bu makalede Azure PowerShell cmdlet'leri yedekleme ve kurtarma Hizmetleri Kasası'nı bir Azure sanal makinesini (VM) kurtarmak için nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3c548-106">This article shows you how to use Azure PowerShell cmdlets to back up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="3c548-107">Kurtarma Hizmetleri kasası bir Azure Resource Manager kaynaktır ve veri ve varlıkların Azure Backup ve Azure Site Recovery Services korumak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3c548-107">A Recovery Services vault is an Azure Resource Manager resource and is used to protect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="3c548-108">Azure Service Manager tarafından dağıtılan VM'ler ve Azure Resource Manager tarafından dağıtılan Vm'leri korumak için bir kurtarma Hizmetleri kasası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c548-108">You can use a Recovery Services vault to protect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="3c548-109">Azure'da kaynak oluşturmaya ve kaynaklarla çalışmaya yönelik iki dağıtım modeli mevcuttur: [Resource Manager ve Klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3c548-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3c548-110">Bu makalede Resource Manager modeli kullanılarak oluşturulan VM ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3c548-110">This article is for use with VMs created using the Resource Manager model.</span></span>
>
>

<span data-ttu-id="3c548-111">Bu makalede bir VM korumak ve verileri bir kurtarma noktasından geri yüklemek için PowerShell kullanılarak üzerinden anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3c548-111">This article walks you through using PowerShell to protect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="3c548-112">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="3c548-112">Concepts</span></span>
<span data-ttu-id="3c548-113">Hizmeti genel bir bakış için Azure Backup hizmeti hakkında bilgi sahibi değilseniz kullanıma [Azure Backup nedir?](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="3c548-113">If you are not familiar with the Azure Backup service, for an overview of the service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="3c548-114">Başlamadan önce Azure Backup ve geçerli VM yedekleme çözümü sınırlamaları ile çalışmak için gereken önkoşulları hakkında essentials kapak emin olun.</span><span class="sxs-lookup"><span data-stu-id="3c548-114">Before you start, ensure that you cover the essentials about the prerequisites needed to work with Azure Backup, and the limitations of the current VM backup solution.</span></span>

<span data-ttu-id="3c548-115">PowerShell etkili bir şekilde kullanmak için nesnelerin ve başlangıç nereden hiyerarşisini anlamak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3c548-115">To use PowerShell effectively, it is necessary to understand the hierarchy of objects and from where to start.</span></span>

![Kurtarma Hizmetleri nesne hiyerarşisi](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="3c548-117">AzureRm.RecoveryServices.Backup PowerShell cmdlet başvurusunun görüntülemek için bkz: [Azure Backup - kurtarma Hizmetleri cmdlet'leri](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) Azure Kitaplığı'nda.</span><span class="sxs-lookup"><span data-stu-id="3c548-117">To view the AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see the [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in the Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="3c548-118">Kurulumu'nu ve kaydı</span><span class="sxs-lookup"><span data-stu-id="3c548-118">Setup and Registration</span></span>
<span data-ttu-id="3c548-119">Başlamak için:</span><span class="sxs-lookup"><span data-stu-id="3c548-119">To begin:</span></span>

1. <span data-ttu-id="3c548-120">[PowerShell en son sürümünü indirme](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (gerekli en düşük sürüm: 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="3c548-120">[Download the latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (the minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="3c548-121">Azure yedekleme PowerShell cmdlet'leri kullanılabilir, aşağıdaki komutu yazarak bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3c548-121">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

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


<span data-ttu-id="3c548-122">Aşağıdaki görevleri PowerShell ile otomatik olarak yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="3c548-122">The following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="3c548-123">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="3c548-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="3c548-124">Azure VM'lerini yedekleme</span><span class="sxs-lookup"><span data-stu-id="3c548-124">Back up Azure VMs</span></span>
* <span data-ttu-id="3c548-125">Bir yedekleme işi tetikleyeceğinden</span><span class="sxs-lookup"><span data-stu-id="3c548-125">Trigger a backup job</span></span>
* <span data-ttu-id="3c548-126">İzleyici bir yedekleme işi</span><span class="sxs-lookup"><span data-stu-id="3c548-126">Monitor a backup job</span></span>
* <span data-ttu-id="3c548-127">Bir Azure VM geri yükleme</span><span class="sxs-lookup"><span data-stu-id="3c548-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="3c548-128">Kurtarma hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="3c548-128">Create a recovery services vault</span></span>
<span data-ttu-id="3c548-129">Aşağıdaki adımlar bir kurtarma Hizmetleri kasası oluşturmada size yol açar.</span><span class="sxs-lookup"><span data-stu-id="3c548-129">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="3c548-130">Kurtarma Hizmetleri kasasına yedekleme Kasası ' farklıdır.</span><span class="sxs-lookup"><span data-stu-id="3c548-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="3c548-131">Azure Backup ilk kez kullanıyorsanız, kullanmalısınız  **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  aboneliğinizle Azure Recovery hizmeti sağlayıcısını kaydetmek için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c548-131">If you are using Azure Backup for the first time, you must use the **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="3c548-132">Kurtarma Hizmetleri kasası bir Resource Manager kaynak olduğundan, bir kaynak grubu içindeki yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c548-132">The Recovery Services vault is a Resource Manager resource, so you need to place it within a resource group.</span></span> <span data-ttu-id="3c548-133">Varolan bir kaynak grubunu kullanın veya bir kaynak grubu ile oluşturmak  **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3c548-133">You can use an existing resource group, or create a resource group with the **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="3c548-134">Bir kaynak grubu oluştururken, ad ve kaynak grubu için konum belirtin.</span><span class="sxs-lookup"><span data-stu-id="3c548-134">When creating a resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="3c548-135">Kullanım  **[yeni AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  kurtarma Hizmetleri kasası oluşturmak için cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3c548-135">Use the **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet to create the Recovery Services vault.</span></span> <span data-ttu-id="3c548-136">Kaynak grubu için kullanılan kasa için aynı konumu belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3c548-136">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="3c548-137">Kullanılacak depolama artıklığı türünü belirtin; kullanabileceğiniz [yerel olarak yedekli depolama (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) veya [coğrafi olarak yedekli depolama (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="3c548-137">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="3c548-138">Aşağıdaki örnek, testvault - BackupStorageRedundancy seçeneği GeoRedundant için ayarlanmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="3c548-138">The following example shows the -BackupStorageRedundancy option for testvault is set to GeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="3c548-139">Çok sayıda Azure yedekleme cmdlet'lerini girdi olarak kurtarma Hizmetleri kasası nesnesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3c548-139">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="3c548-140">Bu nedenle, bir değişkende yedekleme kurtarma Hizmetleri kasası nesne depolamak uygundur.</span><span class="sxs-lookup"><span data-stu-id="3c548-140">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="3c548-141">Bir abonelikte kasalarını görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="3c548-141">View the vaults in a subscription</span></span>
<span data-ttu-id="3c548-142">Kullanım  **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  geçerli abonelikte tüm kasalarının listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="3c548-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="3c548-143">Bu komut, yeni bir kasa oluşturulduğunu denetleyin veya abonelik kullanılabilir kasalarında görmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c548-143">You can use this command to check that a new vault was created, or to see the available vaults in the subscription.</span></span>

<span data-ttu-id="3c548-144">Abonelikteki tüm kasalarını görüntülemek için Get-AzureRmRecoveryServicesVault komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3c548-144">Run the command, Get-AzureRmRecoveryServicesVault, to view all vaults in the subscription.</span></span> <span data-ttu-id="3c548-145">Aşağıdaki örnekte, her kasa için görüntülenen bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="3c548-145">The following example shows the information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="3c548-146">Azure VM'lerini yedekleme</span><span class="sxs-lookup"><span data-stu-id="3c548-146">Back up Azure VMs</span></span>
<span data-ttu-id="3c548-147">Sanal makinelerinizi korumak için bir kurtarma Hizmetleri kasası kullanın.</span><span class="sxs-lookup"><span data-stu-id="3c548-147">Use a Recovery Services vault to protect your virtual machines.</span></span> <span data-ttu-id="3c548-148">Koruma uygulamadan önce set kasası bağlam (kasaya korumalı veri türü) ve koruma ilkesini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3c548-148">Before you apply the protection, set the vault context (the type of data protected in the vault), and verify the protection policy.</span></span> <span data-ttu-id="3c548-149">Koruma İlkesi yedekleme işleri çalıştırdığınızda, zamanlama ve her yedekleme anlık görüntüsünü ne kadar süreyle tutulduğunu ' dir.</span><span class="sxs-lookup"><span data-stu-id="3c548-149">The protection policy is the schedule when the backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="3c548-150">Set kasası bağlamı</span><span class="sxs-lookup"><span data-stu-id="3c548-150">Set vault context</span></span>
<span data-ttu-id="3c548-151">Bir VM korumasını etkinleştirmeden önce kullanmak  **[kümesi AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  kasası bağlam ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="3c548-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context.</span></span> <span data-ttu-id="3c548-152">Kasa bağlam ayarladıktan sonra sonraki tüm cmdlet'ler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="3c548-152">Once the vault context is set, it applies to all subsequent cmdlets.</span></span> <span data-ttu-id="3c548-153">Aşağıdaki örnek, kasa için kasa bağlamı ayarlar *testvault*.</span><span class="sxs-lookup"><span data-stu-id="3c548-153">The following example sets the vault context for the vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="3c548-154">Bir koruma ilkesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="3c548-154">Create a protection policy</span></span>
<span data-ttu-id="3c548-155">Kurtarma Hizmetleri kasası oluşturduğunuzda, varsayılan koruma ve bekletme ilkeleri ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="3c548-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="3c548-156">Varsayılan koruma İlkesi, bir yedekleme işi her gün belirtilen zamanda tetikler.</span><span class="sxs-lookup"><span data-stu-id="3c548-156">The default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="3c548-157">Varsayılan saklama İlkesi 30 gün boyunca günlük kurtarma noktası korur.</span><span class="sxs-lookup"><span data-stu-id="3c548-157">The default retention policy retains the daily recovery point for 30 days.</span></span> <span data-ttu-id="3c548-158">Varsayılan ilke, VM hızlı bir şekilde korumak ve daha sonra farklı ayrıntılarla ilkesini düzenlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c548-158">You can use the default policy to quickly protect your VM and edit the policy later with different details.</span></span>

<span data-ttu-id="3c548-159">Kullanım  **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  koruma ilkeleri kasaya görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="3c548-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** to view the protection policies in the vault.</span></span> <span data-ttu-id="3c548-160">Belirli bir ilke alma veya bir iş yükü türü ile ilişkili ilkeler görüntülemek için bu cmdlet'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c548-160">You can use this cmdlet to get a specific policy, or to view the policies associated with a workload type.</span></span> <span data-ttu-id="3c548-161">Aşağıdaki örnek iş yükü türünün AzureVM ilkelerini alır.</span><span class="sxs-lookup"><span data-stu-id="3c548-161">The following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="3c548-162">PowerShell BackupTime alanın saat dilimi UTC değil.</span><span class="sxs-lookup"><span data-stu-id="3c548-162">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="3c548-163">Ancak, Azure portalında yedekleme saati gösterildiğinde zaman, yerel saat dilimine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3c548-163">However, when the backup time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

<span data-ttu-id="3c548-164">En az bir bekletme ilkesiyle ilişkili bir yedekleme koruma ilkesidir.</span><span class="sxs-lookup"><span data-stu-id="3c548-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="3c548-165">Bekletme İlkesi silinmeden önce ne kadar bir kurtarma noktası tutulur tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3c548-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="3c548-166">Kullanım  **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  varsayılan bekletme ilkesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="3c548-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** to view the default retention policy.</span></span>  <span data-ttu-id="3c548-167">Benzer şekilde kullanabilirsiniz  **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  varsayılan zamanlama ilkesi elde edilir.</span><span class="sxs-lookup"><span data-stu-id="3c548-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** to obtain the default schedule policy.</span></span> <span data-ttu-id="3c548-168"> **[Yeni AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet'i, yedekleme ilkesi bilgilerini tutan bir PowerShell nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3c548-168">The **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="3c548-169">Zamanlama ve Bekletme İlkesi nesneleri giriş olarak kullanılan  **[yeni AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3c548-169">The schedule and retention policy objects are used as inputs to the **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="3c548-170">Aşağıdaki örnek zamanlama ilkesini ve bekletme ilkesini değişkenleri depolar.</span><span class="sxs-lookup"><span data-stu-id="3c548-170">The following example stores the schedule policy and the retention policy in variables.</span></span> <span data-ttu-id="3c548-171">Örnek, bir koruma ilkesi oluşturulurken parametreleri tanımlamak için bu değişkenleri kullanır. *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="3c548-171">The example uses those variables to define the parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="3c548-172">Korumayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="3c548-172">Enable protection</span></span>
<span data-ttu-id="3c548-173">Yedekleme koruma İlkesi tanımladıktan sonra bir öğe için ilke hala etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c548-173">Once you have defined the backup protection policy, you still must enable the policy for an item.</span></span> <span data-ttu-id="3c548-174">Kullanım  **[etkinleştir AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  korumasını etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3c548-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** to enable protection.</span></span> <span data-ttu-id="3c548-175">Koruma etkinleştirme iki nesne - öğesini ve ilke gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3c548-175">Enabling protection requires two objects - the item and the policy.</span></span> <span data-ttu-id="3c548-176">İlke kasayla ilişkili silindikten sonra yedekleme iş akışı ilke zamanlama içinde tanımlı zaman tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="3c548-176">Once the policy has been associated with the vault, the backup workflow is triggered at the time defined in the policy schedule.</span></span>

<span data-ttu-id="3c548-177">Aşağıdaki örnek NewPolicy ilke kullanılarak koruma V2VM, öğe için etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="3c548-177">The following example enables protection for the item, V2VM, using the policy, NewPolicy.</span></span> <span data-ttu-id="3c548-178">Resource Manager vm'lerde şifrelenmemiş korumasını etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="3c548-178">To enable the protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="3c548-179">(BEK ve KEK kullanılarak şifrelenmiş) şifrelenmiş vm'lerinde korumayı etkinleştirmek için anahtarlar ve gizli anahtar Kasası'nı okuyun Azure Backup hizmeti izni vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c548-179">To enable the protection on encrypted VMs (encrypted using BEK and KEK), you need to give the Azure Backup service permission to read keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="3c548-180">Şifrelenmiş (yalnızca BEK kullanılarak şifrelenmiş) VM'ler korumayı etkinleştirmek için gizli anahtar Kasası'nı okumak için Azure Backup hizmeti izni vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c548-180">To enable the protection on encrypted VMs (encrypted using BEK only), you need to give the Azure Backup service permission to read secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="3c548-181">Azure Bulutu kullanıyorsanız, parametre için değer ff281ffe-705c-4f53-9f37-a40e6f2c68f3 kullanmak **- ServicePrincipalName** içinde [kümesi AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3c548-181">If you are using the Azure Government cloud, then use the value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for the parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="3c548-182">Klasik VM'ler için</span><span class="sxs-lookup"><span data-stu-id="3c548-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="3c548-183">Bir koruma ilkesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="3c548-183">Modify a protection policy</span></span>
<span data-ttu-id="3c548-184">Koruma ilkesini değiştirmek için kullanmak [kümesi AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) SchedulePolicy veya RetentionPolicy nesneleri değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3c548-184">To modify the protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) to modify the SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="3c548-185">Aşağıdaki örnek, kurtarma noktası bekletme 365 gün olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="3c548-185">The following example changes the recovery point retention to 365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="3c548-186">Bir yedeklemeyi tetikleyin</span><span class="sxs-lookup"><span data-stu-id="3c548-186">Trigger a backup</span></span>
<span data-ttu-id="3c548-187">Kullanabileceğiniz  **[yedekleme AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  yedekleme işini tetikleyecek.</span><span class="sxs-lookup"><span data-stu-id="3c548-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** to trigger a backup job.</span></span> <span data-ttu-id="3c548-188">Bu ilk yedekleme ise, tam yedekleme olur.</span><span class="sxs-lookup"><span data-stu-id="3c548-188">If it is the initial backup, it is a full backup.</span></span> <span data-ttu-id="3c548-189">Sonraki yedek bir artımlı kopya alabilir.</span><span class="sxs-lookup"><span data-stu-id="3c548-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="3c548-190">Kullandığınızdan emin olun  **[kümesi AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  yedekleme işini tetiklemeden önce kasası bağlam ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="3c548-190">Be sure to use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context before triggering the backup job.</span></span> <span data-ttu-id="3c548-191">Aşağıdaki örnek, kasa bağlamını ayarlayın varsayar.</span><span class="sxs-lookup"><span data-stu-id="3c548-191">The following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="3c548-192">PowerShell'de StartTime ve EndTime alanlarının saat dilimi UTC değil.</span><span class="sxs-lookup"><span data-stu-id="3c548-192">The timezone of the StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="3c548-193">Ancak, zaman zaman Azure portalında gösterildiğinde yerel saat dilimi olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3c548-193">However, when the time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="3c548-194">Bir yedekleme işi izleme</span><span class="sxs-lookup"><span data-stu-id="3c548-194">Monitoring a backup job</span></span>
<span data-ttu-id="3c548-195">Azure portalını kullanmadan yedekleme işleri gibi uzun süre çalışan işlemleri izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c548-195">You can monitor long-running operations, such as backup jobs, without using the Azure portal.</span></span> <span data-ttu-id="3c548-196">Devam eden işin durumunu almak için  **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3c548-196">To get the status of an in-progress job, use the **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="3c548-197">Belirli bir kasa yönelik yedekleme işleri Bu cmdlet'i alır ve bu kasası kasası bağlamda belirtilir.</span><span class="sxs-lookup"><span data-stu-id="3c548-197">This cmdlet gets the backup jobs for a specific vault, and that vault is specified in the vault context.</span></span> <span data-ttu-id="3c548-198">Aşağıdaki örnek, bir dizi olarak devam eden işin durumunu alır ve durum $joblist değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="3c548-198">The following example gets the status of an in-progress job as an array, and stores the status in the $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="3c548-199">Bu işleri - gereksiz ek kod olan - tamamlanması için yoklama yerine kullanmak  **[bekleme AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3c548-199">Instead of polling these jobs for completion - which is unnecessary additional code - use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="3c548-200">Bu cmdlet yürütme iş tamamlandığında veya belirtilen zaman aşımı değerine ulaşılana kadar duraklar.</span><span class="sxs-lookup"><span data-stu-id="3c548-200">This cmdlet pauses the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="3c548-201">Bir Azure VM geri yükleme</span><span class="sxs-lookup"><span data-stu-id="3c548-201">Restore an Azure VM</span></span>
<span data-ttu-id="3c548-202">Azure Portalı'nı kullanarak bir VM geri yükleme ve PowerShell kullanarak bir VM'i geri arasındaki en önemli fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="3c548-202">There is a key difference between the restoring a VM using the Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="3c548-203">PowerShell ile diskleri ve yapılandırma bilgilerini kurtarma noktasından oluşturulduktan sonra geri yükleme işlemi tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="3c548-203">With PowerShell, the restore operation is complete once the disks and configuration information from the recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="3c548-204">Geri yükleme işlemi, bir sanal makine oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="3c548-204">The restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="3c548-205">Diskten bir sanal makine oluşturmak için bölümüne bakın [saklı disklerden VM oluşturmak](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="3c548-205">To create a virtual machine from disk, see the section, [Create the VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="3c548-206">Bir Azure VM geri yüklemek için temel adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3c548-206">The basic steps to restore an Azure VM are:</span></span>

* <span data-ttu-id="3c548-207">VM seçin</span><span class="sxs-lookup"><span data-stu-id="3c548-207">Select the VM</span></span>
* <span data-ttu-id="3c548-208">Bir kurtarma noktası seçin</span><span class="sxs-lookup"><span data-stu-id="3c548-208">Choose a recovery point</span></span>
* <span data-ttu-id="3c548-209">Diskleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="3c548-209">Restore the disks</span></span>
* <span data-ttu-id="3c548-210">Saklı disklerden VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="3c548-210">Create the VM from stored disks</span></span>

<span data-ttu-id="3c548-211">Aşağıdaki grafikte nesne hiyerarşisi BackupRecoveryPoint aşağıya doğru RecoveryServicesVault gelen gösterir.</span><span class="sxs-lookup"><span data-stu-id="3c548-211">The following graphic shows the object hierarchy from the RecoveryServicesVault down to the BackupRecoveryPoint.</span></span>

![Kurtarma Hizmetleri nesne hiyerarşisi BackupContainer gösterme](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="3c548-213">Yedekleme verilerini geri yüklemek için yedeklenen öğesi ve zaman içinde nokta verilerini tutan bir kurtarma noktası belirleyin.</span><span class="sxs-lookup"><span data-stu-id="3c548-213">To restore backup data, identify the backed-up item and the recovery point that holds the point-in-time data.</span></span> <span data-ttu-id="3c548-214">Kullanım  **[geri yükleme AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  verileri kasadan müşterinin hesabına geri yüklemek için cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3c548-214">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="3c548-215">VM seçin</span><span class="sxs-lookup"><span data-stu-id="3c548-215">Select the VM</span></span>
<span data-ttu-id="3c548-216">Doğru yedekleme öğesi tanımlayan PowerShell nesnesini almak için kasadaki kapsayıcısından başlatın ve nesne hiyerarşide aşağı, şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="3c548-216">To get the PowerShell object that identifies the right backup item, start from the container in the vault, and work your way down the object hierarchy.</span></span> <span data-ttu-id="3c548-217">VM'yi temsil kapsayıcı seçmek için kullanın  **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet'i ve için kanal  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3c548-217">To select the container that represents the VM, use the **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that to the **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="3c548-218">Bir kurtarma noktası seçin</span><span class="sxs-lookup"><span data-stu-id="3c548-218">Choose a recovery point</span></span>
<span data-ttu-id="3c548-219">Kullanım  **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  yedekleme öğesi için tüm kurtarma noktalarını listelemek için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c548-219">Use the **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet to list all recovery points for the backup item.</span></span> <span data-ttu-id="3c548-220">Daha sonra geri yüklemek için kurtarma noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="3c548-220">Then choose the recovery point to restore.</span></span> <span data-ttu-id="3c548-221">Kullanılacak olan kurtarma noktasını konusunda emin değilseniz, en son RecoveryPointType seçmek için iyi bir uygulamadır AppConsistent noktası listesinde =.</span><span class="sxs-lookup"><span data-stu-id="3c548-221">If you are unsure which recovery point to use, it is a good practice to choose the most recent RecoveryPointType = AppConsistent point in the list.</span></span>

<span data-ttu-id="3c548-222">Aşağıdaki komut, değişken **$rp**, seçili yedek öğesini, son yedi gün için kurtarma noktalarını dizisidir.</span><span class="sxs-lookup"><span data-stu-id="3c548-222">In the following script, the variable, **$rp**, is an array of recovery points for the selected backup item, from the past seven days.</span></span> <span data-ttu-id="3c548-223">Dizi en son kurtarma noktası dizin 0 konumunda ile süreyi ters sırada sıralanır.</span><span class="sxs-lookup"><span data-stu-id="3c548-223">The array is sorted in reverse order of time with the latest recovery point at index 0.</span></span> <span data-ttu-id="3c548-224">Standart PowerShell dizi dizin kurtarma noktası seçmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="3c548-224">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="3c548-225">Örnekte, $rp [0], en son kurtarma noktası seçer.</span><span class="sxs-lookup"><span data-stu-id="3c548-225">In the example, $rp[0] selects the latest recovery point.</span></span>

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



### <a name="restore-the-disks"></a><span data-ttu-id="3c548-226">Diskleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="3c548-226">Restore the disks</span></span>
<span data-ttu-id="3c548-227">Kullanım  **[geri yükleme AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  bir yedekleme öğesi'nin veri ve yapılandırmaları bir kurtarma noktasına geri yüklemek için cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3c548-227">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore a backup item's data and configuration to a recovery point.</span></span> <span data-ttu-id="3c548-228">Bir kurtarma noktası belirledikten sonra değeri olarak kullanın **- RecoveryPoint** parametresi.</span><span class="sxs-lookup"><span data-stu-id="3c548-228">Once you have identified a recovery point, use it as the value for the **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="3c548-229">Önceki örnek kodda **$rp [0]** kullanılacak olan kurtarma noktasını oluştu.</span><span class="sxs-lookup"><span data-stu-id="3c548-229">In the previous sample code, **$rp[0]** was the recovery point to use.</span></span> <span data-ttu-id="3c548-230">Aşağıdaki örnek kodda **$rp [0]** disk geri yüklemek için kullanılacak bir kurtarma noktası.</span><span class="sxs-lookup"><span data-stu-id="3c548-230">In the following sample code, **$rp[0]** is the recovery point to use for restoring the disk.</span></span>

<span data-ttu-id="3c548-231">Diskleri ve yapılandırma bilgilerini geri yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="3c548-231">To restore the disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="3c548-232">Kullanım  **[bekleme AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet'ini tamamlamak geri yükleme işi bekleyin.</span><span class="sxs-lookup"><span data-stu-id="3c548-232">Use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet to wait for the Restore job to complete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="3c548-233">Geri yükleme işi tamamlandıktan sonra kullanmak  **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  geri yükleme işleminin ayrıntılarını almak için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c548-233">Once the Restore job has completed, use the **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet to get the details of the restore operation.</span></span> <span data-ttu-id="3c548-234">JobDetails özelliği VM yeniden oluşturmak için gereken bilgileri topladı.</span><span class="sxs-lookup"><span data-stu-id="3c548-234">The JobDetails property has the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="3c548-235">Diskleri geri sonra VM'yi oluşturmak için sonraki bölüme gidin.</span><span class="sxs-lookup"><span data-stu-id="3c548-235">Once you restore the disks, go to the next section to create the VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="3c548-236">Geri yüklenen disklerden bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="3c548-236">Create a VM from restored disks</span></span>
<span data-ttu-id="3c548-237">Diskleri geri yükledikten sonra oluşturup diskten sanal makine yapılandırmak için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="3c548-237">After you have restored the disks, use these steps to create and configure the virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="3c548-238">Geri yüklenen disklerden şifrelenmiş VM'ler oluşturmak için Azure rolünüze eylemi gerçekleştirmek için izni olmalıdır **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="3c548-238">To create encrypted VMs from restored disks, your Azure role must have permission to perform the action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="3c548-239">Özel bir rol rolünüzün bu izne sahip değilse bu eylemle oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3c548-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="3c548-240">Daha fazla bilgi için bkz: [Azure rbac'de özel roller](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="3c548-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="3c548-241">İş ayrıntılarını geri yüklenen disk özelliklerini sorgu.</span><span class="sxs-lookup"><span data-stu-id="3c548-241">Query the restored disk properties for the job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="3c548-242">Azure depolama bağlamını ayarlayın ve JSON yapılandırma dosyasını geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3c548-242">Set the Azure storage context and restore the JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="3c548-243">VM yapılandırması oluşturmak için JSON yapılandırma dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="3c548-243">Use the JSON configuration file to create the VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="3c548-244">İşletim sistemi diski ve veri diskleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3c548-244">Attach the OS disk and data disks.</span></span> <span data-ttu-id="3c548-245">Vm'leriniz yapılandırmasına bağlı olarak, ilgili cmdlet'ler görüntülemek için ilgili bağlantıyı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="3c548-245">Depending on the configuration of your VMs, click on the relevant link to view respective cmdlets:</span></span> 
    - [<span data-ttu-id="3c548-246">Yönetilmeyen, şifrelenmemiş VM'ler</span><span class="sxs-lookup"><span data-stu-id="3c548-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="3c548-247">Yönetilmeyen, şifrelenmiş VM'ler (yalnızca BEK)</span><span class="sxs-lookup"><span data-stu-id="3c548-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="3c548-248">Yönetilmeyen, şifrelenmiş VM'ler (BEK ve KEK)</span><span class="sxs-lookup"><span data-stu-id="3c548-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="3c548-249">Yönetilen, şifrelenmemiş VM'ler</span><span class="sxs-lookup"><span data-stu-id="3c548-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="3c548-250">Yönetilen, şifrelenmiş VM'ler (BEK ve KEK)</span><span class="sxs-lookup"><span data-stu-id="3c548-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="3c548-251">Yönetilmeyen, şifrelenmemiş VM'ler</span><span class="sxs-lookup"><span data-stu-id="3c548-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="3c548-252">Aşağıdaki örnek, yönetilmeyen, şifrelenmemiş VM'ler için kullanın.</span><span class="sxs-lookup"><span data-stu-id="3c548-252">Use the following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="3c548-253">Yönetilmeyen, şifrelenmiş VM'ler (yalnızca BEK)</span><span class="sxs-lookup"><span data-stu-id="3c548-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="3c548-254">(Yalnızca BEK kullanılarak şifrelenmiş) yönetilmeyen, şifrelenmiş VM'ler için diskler ekleyebilmek için gizli anahtar Kasası'na geri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c548-254">For non-managed, encrypted VMs (encrypted using BEK only), you need to restore the secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="3c548-255">Daha fazla bilgi için lütfen makalesine bakın [şifrelenmiş bir sanal makine bir Azure yedekleme kurtarma noktasından geri](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="3c548-255">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="3c548-256">Aşağıdaki örnek, şifrelenmiş VM'ler için işletim sistemi ve veri diskleri ekleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3c548-256">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="3c548-257">Yönetilmeyen, şifrelenmiş VM'ler (BEK ve KEK)</span><span class="sxs-lookup"><span data-stu-id="3c548-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="3c548-258">(BEK ve KEK kullanılarak şifrelenmiş) yönetilmeyen, şifrelenmiş VM'ler için diskleri eklemeden önce anahtarı ve gizli anahtar Kasası'na geri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c548-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need to restore the key and secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="3c548-259">Daha fazla bilgi için lütfen makalesine bakın [şifrelenmiş bir sanal makine bir Azure yedekleme kurtarma noktasından geri](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="3c548-259">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="3c548-260">Aşağıdaki örnek, şifrelenmiş VM'ler için işletim sistemi ve veri diskleri ekleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3c548-260">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="3c548-261">Yönetilen, şifrelenmemiş VM'ler</span><span class="sxs-lookup"><span data-stu-id="3c548-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="3c548-262">Yönetilen şifrelenmemiş VM'ler için blob depolama alanından yönetilen diskleri oluşturma ve diskleri bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c548-262">For managed non-encrypted VMs, you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="3c548-263">Ayrıntılı bilgi için makalesine bakın [bir veri diski bir Windows PowerShell kullanarak VM'e](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3c548-263">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="3c548-264">Aşağıdaki örnek kod, yönetilen şifrelenmemiş VM'ler için veri diski ekleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3c548-264">The following sample code shows how to attach the data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="3c548-265">Yönetilen, şifrelenmiş VM'ler (BEK ve KEK)</span><span class="sxs-lookup"><span data-stu-id="3c548-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="3c548-266">(BEK ve KEK kullanılarak şifrelenmiş) yönetilen şifrelenmiş VM'ler için blob depolama alanından yönetilen diskleri oluşturma ve diskleri bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c548-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="3c548-267">Ayrıntılı bilgi için makalesine bakın [bir veri diski bir Windows PowerShell kullanarak VM'e](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3c548-267">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="3c548-268">Aşağıdaki örnek kod, yönetilen şifrelenmiş VM'ler için veri diski ekleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3c548-268">The following sample code shows how to attach the data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="3c548-269">Ağ ayarları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3c548-269">Set the Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="3c548-270">Sanal makineyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3c548-270">Create the virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="3c548-271">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3c548-271">Next steps</span></span>
<span data-ttu-id="3c548-272">Azure kaynaklarınızı bulunmaya PowerShell kullanmayı tercih ederseniz, PowerShell makalesine bakın. [dağıtma ve yönetme yedekleme için Windows Server](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="3c548-272">If you prefer to use PowerShell to engage with your Azure resources, see the PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="3c548-273">DPM yedeklemelerini yönetiyorsanız makalesine bakın [dağıtma ve yönetme yedekleme DPM için](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="3c548-273">If you manage DPM backups, see the article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="3c548-274">Bu makaleler her ikisi de Resource Manager dağıtımları ve klasik dağıtımları için bir sürümüne sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c548-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
