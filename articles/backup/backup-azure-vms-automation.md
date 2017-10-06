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
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a>Sanal makineler yukarı AzureRM.RecoveryServices.Backup cmdlet'leri tooback kullanın
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-vms-automation.md)
> * [Klasik](backup-azure-vms-classic-automation.md)
>
>

Bu makalede nasıl toouse Azure PowerShell cmdlet'leri tooback yedeklemek ve kurtarmak bir Azure sanal makineden (VM) bir kurtarma Hizmetleri kasası gösterilmektedir. Kurtarma Hizmetleri kasası bir Azure Resource Manager kaynak ve kullanılan tooprotect veri ve varlıkların Azure Backup ve Azure Site Recovery Services. Kurtarma Hizmetleri kasası tooprotect Azure Service Manager tarafından dağıtılan VM'ler ve Azure Resource Manager tarafından dağıtılan VM'ler kullanabilirsiniz.

> [!NOTE]
> Azure'da kaynak oluşturmaya ve kaynaklarla çalışmaya yönelik iki dağıtım modeli mevcuttur: [Resource Manager ve Klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede hello Resource Manager modeli kullanılarak oluşturulan VM ile birlikte kullanılır.
>
>

Bu makalede PowerShell tooprotect kullanarak bir VM ve verileri geri yüklemek bir kurtarma noktasından anlatılmaktadır.

## <a name="concepts"></a>Kavramlar
Merhaba hello hizmeti, genel bir bakış için Azure Backup hizmeti hakkında bilgi sahibi değilseniz kullanıma [Azure Backup nedir?](backup-introduction-to-azure-backup.md) Başlamadan önce Azure yedekleme ile Merhaba gerekli Önkoşullar toowork hakkında hello essentials kapsar ve hello geçerli VM yedekleme çözümü sınırlamaları hello emin olun.

toouse PowerShell etkili bir şekilde, gerekli toounderstand hello hiyerarşi nesnelerin ve nerede olduğunu toostart.

![Kurtarma Hizmetleri nesne hiyerarşisi](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet başvurusunun bkz hello [Azure Backup - kurtarma Hizmetleri cmdlet'leri](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) hello Azure kitaplığı içinde.

## <a name="setup-and-registration"></a>Kurulumu'nu ve kaydı
toobegin:

1. [Merhaba PowerShell'in en son sürümünü indirme](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (gerekli hello minimum sürüm: 1.4.0)
2. Hello Azure yedekleme PowerShell cmdlet'leri kullanılabilir hello aşağıdaki komutu yazarak bulabilirsiniz:

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


Merhaba görevleri aşağıdaki PowerShell ile otomatik olarak yapılabilir:

* Kurtarma Hizmetleri kasası oluşturma
* Azure VM'lerini yedekleme
* Bir yedekleme işi tetikleyeceğinden
* İzleyici bir yedekleme işi
* Bir Azure VM geri yükleme

## <a name="create-a-recovery-services-vault"></a>Kurtarma hizmetleri kasası oluşturma
Aşağıdaki adımları hello kurtarma Hizmetleri kasası oluşturmada size yol açar. Kurtarma Hizmetleri kasasına yedekleme Kasası ' farklıdır.

1. Azure Backup hello için ilk kez kullanıyorsanız hello kullanmalısınız  **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  cmdlet tooregister hello Azure Recovery hizmeti sağlayıcısı aboneliğinizle.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. tooplace ihtiyacınız hello kurtarma Hizmetleri kasası bir Resource Manager kaynak olduğundan, bir kaynak grubu içinde. Varolan bir kaynak grubunu kullanın veya bir kaynak grubu ile Merhaba oluşturmak  **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet'i. Bir kaynak grubu oluştururken hello kaynak grubu için hello ad ve konum belirtin.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Kullanım hello  **[yeni AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  kurtarma Hizmetleri kasası cmdlet toocreate hello. Toospecify hello hello kasa için aynı konumu hello kaynak grubu için kullanıldığından emin olun.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. Depolama artıklık toouse Hello türünü belirtin; kullanabileceğiniz [yerel olarak yedekli depolama (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) veya [coğrafi olarak yedekli depolama (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). Merhaba aşağıdaki örnek tooGeoRedundant testvault için hello - BackupStorageRedundancy seçeneği ayarlanmış gösterir.

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > Çok sayıda Azure yedekleme cmdlet'lerini girdi olarak hello kurtarma Hizmetleri kasası nesnesi gerektirir. Bu nedenle, bu kullanışlı toostore hello yedekleme kurtarma Hizmetleri kasası, bir değişkende nesnesidir.
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a>Bir abonelikte görünüm hello kasaları
Kullanım  **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview hello hello geçerli Abonelikteki tüm kasalarının listesi. Bu komut toocheck yeni bir kasa oluşturulduğunu veya toosee hello hello Abonelikteki kullanılabilir kasalarını kullanabilirsiniz.

Merhaba komutu, Get-AzureRmRecoveryServicesVault tooview hello aboneliğindeki tüm kasalarını çalıştırın. Merhaba aşağıdaki örnekte her kasa için görüntülenen hello bilgiler gösterilmektedir.

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


## <a name="back-up-azure-vms"></a>Azure VM'lerini yedekleme
Kurtarma Hizmetleri kasası tooprotect sanal makinelerinizi kullanın. Merhaba koruma uygulamadan önce set hello kasası bağlam (Merhaba kasasına korunan verileri hello türü) ve hello koruma ilkesini doğrulayın. Merhaba koruma hello yedekleme işleri çalıştırdığınızda hello zamanlama ve her yedekleme anlık görüntüsünü ne kadar süreyle tutulduğunu ilkesidir.

### <a name="set-vault-context"></a>Set kasası bağlamı
Bir VM korumasını etkinleştirmeden önce kullanmak  **[kümesi AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset hello kasası bağlamı. Merhaba kasası bağlam ayarladıktan sonra tooall sonraki cmdlet'leri geçerlidir. Merhaba aşağıdaki örnek hello kasası bağlamı hello kasası için ayarlar *testvault*.

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a>Bir koruma ilkesi oluşturun
Kurtarma Hizmetleri kasası oluşturduğunuzda, varsayılan koruma ve bekletme ilkeleri ile birlikte gelir. Merhaba varsayılan koruma İlkesi, bir yedekleme işi her gün belirtilen zamanda tetikler. Merhaba varsayılan bekletme ilkesi hello günlük kurtarma noktası 30 gün boyunca korur. Merhaba varsayılan kullanabileceğiniz ilke tooquickly VM korumak ve daha sonra farklı ayrıntılarla hello İlkesi Düzenle.

Kullanım  **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview hello koruma ilkeleri hello kasasında. Bu cmdlet tooget belirli bir ilke veya bir iş yükü türüyle ilişkili tooview hello ilkelerini kullanabilirsiniz. Aşağıdaki örneğine hello iş yükü türünün AzureVM ilkelerini alır.

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> PowerShell'de hello BackupTime alanının Hello saat dilimi UTC değil. Merhaba yedekleme saati hello Azure portal gösterildiğinde, ancak hello ayarlanmış tooyour yerel saat dilimi saattir.
>
>

En az bir bekletme ilkesiyle ilişkili bir yedekleme koruma ilkesidir. Bekletme İlkesi silinmeden önce ne kadar bir kurtarma noktası tutulur tanımlar. Kullanım  **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  tooview hello varsayılan bekletme ilkesi.  Benzer şekilde kullanabilirsiniz  **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  tooobtain hello varsayılan zamanlama ilkesi. Merhaba  **[yeni AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet'i, yedekleme ilkesi bilgilerini tutan bir PowerShell nesnesi oluşturur. Merhaba zamanlama ve Bekletme İlkesi nesneleri toohello girdi olarak kullanılan  **[yeni AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet'i. Merhaba aşağıdaki örnek hello zamanlama ilkesi ve hello bekletme ilkesi değişkenleri depolar. Merhaba örnek, bir koruma ilkesi oluşturulurken bu değişkenleri toodefine hello parametreleri kullanır *NewPolicy*.

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a>Korumayı etkinleştir
Merhaba yedekleme koruma İlkesi tanımladıktan sonra bir öğe için hello İlkesi hala etkinleştirmeniz gerekir. Kullanım  **[etkinleştir AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable koruma. Koruma etkinleştirme iki nesne - hello öğesi ve hello İlkesi gerektirir. Hello İlkesi hello kasası ile ilişkilendirildikten sonra hello yedekleme iş akışı hello İlkesi zamanlamasında tanımlanan hello zaman tetiklenir.

Hello İlkesi, NewPolicy kullanarak örnek etkinleştirir korumayı hello öğesi, V2VM, için aşağıdaki hello. Resource Manager vm'lerde şifrelenmemiş tooenable hello koruma

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

(BEK ve KEK kullanılarak şifrelenmiş) VM'ler tooenable hello koruması şifreli, toogive hello Azure Backup hizmeti izni tooread anahtarları ve gizli anahtar Kasası'ndan gerekir.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

(yalnızca BEK kullanılarak şifrelenmiş) VM'ler tooenable hello koruması şifreli, toogive hello Azure Backup hizmeti izni tooread gizli anahtar Kasası'ndan gerekir.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> Hello Azure Bulutu kullanıyorsanız, hello değeri ff281ffe-705c-4f53-9f37-a40e6f2c68f3 hello parametre için kullanmak **- ServicePrincipalName** içinde [kümesi AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet'i .
>
>

Klasik VM'ler için

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a>Bir koruma ilkesini değiştirme
toomodify hello koruma İlkesi, kullanım [kümesi AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy veya RetentionPolicy nesne.

Merhaba aşağıdaki örnek hello kurtarma noktası bekletme too365 gün değiştirir.

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a>Bir yedeklemeyi tetikleyin
Kullanabileceğiniz  **[yedekleme AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger bir yedekleme işi. Bunu hello ilk yedekleme ise, tam yedekleme olur. Sonraki yedek bir artımlı kopya alabilir. Emin toouse olması  **[kümesi AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  hello yedekleme işini tetiklemeden önce tooset hello kasası bağlamı. Aşağıdaki örnek hello kasası bağlamını ayarlayın varsayar.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> PowerShell hello StartTime ve EndTime alanların Hello saat dilimi UTC değil. Hello zaman hello Azure portal gösterilir, ancak hello zaman ayarlanmış tooyour yerel saat dilimi zamandır.
>
>

## <a name="monitoring-a-backup-job"></a>Bir yedekleme işi izleme
Hello Azure portalını kullanmadan yedekleme işleri gibi uzun süre çalışan işlemleri izleyebilirsiniz. tooget hello kullan hello bir devam eden işin durumunu  **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet'i. Merhaba yedekleme işleri belirli bir kasa için bu cmdlet'i alır ve bu kasası hello kasası bağlamda belirtilir. Hello aşağıdaki örnekte bir dizi olarak devam eden işi hello durumunu alır ve hello durum hello $joblist değişkeninde depolar.

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Bu işleri - gereksiz ek kod olan - tamamlanması için yoklama yerine hello kullan  **[bekleme AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet'i. Bu cmdlet hello yürütme hello işi tamamlar veya hello belirtilen zaman aşımı değerine ulaşılana kadar duraklar.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a>Bir Azure VM geri yükleme
Hello Azure portal kullanarak ve PowerShell kullanarak bir VM'i geri VM geri hello arasındaki en önemli fark yoktur. PowerShell ile Merhaba diskleri ve yapılandırma bilgilerini hello kurtarma noktasından oluşturulduktan sonra hello geri yükleme işlemi tamamlanır.

> [!NOTE]
> Merhaba geri yükleme işlemi, bir sanal makine oluşturmaz.
>
>

disk, sanal makineden toocreate hello bölümüne bakın [saklı disklerden oluşturma hello VM](backup-azure-vms-automation.md#create-a-vm-from-stored-disks). Merhaba temel adımlar toorestore bir Azure VM şunlardır:

* Merhaba VM seçin
* Bir kurtarma noktası seçin
* Merhaba disklerini geri yükle
* Saklı disklerden Hello VM oluşturma

Merhaba aşağıdaki grafikte hello nesne hello RecoveryServicesVault toohello BackupRecoveryPoint aşağı hiyerarşiden gösterir.

![Kurtarma Hizmetleri nesne hiyerarşisi BackupContainer gösterme](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

toorestore yedekleme verilerini hello yedeklenen öğesi ve hello zaman içinde nokta verilerini tutan hello kurtarma noktası belirleyin. Kullanım hello  **[geri yükleme AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  hello cmdlet toorestore verileri kasa toohello müşterinin hesap.

### <a name="select-hello-vm"></a>Merhaba VM seçin
sağ hello tanımlayan tooget hello PowerShell nesnesi öğesi yedekleme, hello kasasında hello kapsayıcısından Başlat ve yolunuzu hello nesne hiyerarşisi aşağı çalışma. Merhaba VM, kullanım hello temsil eden tooselect hello kapsayıcı  **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet'i ve o toohello kanal  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet'i.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a>Bir kurtarma noktası seçin
Kullanım hello  **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  tüm kurtarma noktaları için yedekleme öğesi hello cmdlet toolist. Ardından hello kurtarma noktası toorestore seçin. Hangi kurtarma noktası toouse konusunda emin değilseniz, iyi bir uygulama toochoose hello en son RecoveryPointType olduğu AppConsistent noktası hello listesinde =.

Değişken, komut dosyası izleyen hello hello **$rp**, hello yedekleme öğesi hello son yedi gün seçilen için kurtarma noktaları dizisidir. Merhaba dizisi hello en son kurtarma noktası dizin 0 konumunda ile süreyi ters sırada sıralanır. Standart PowerShell dizi toopick hello kurtarma noktası dizin kullanın. Merhaba örnekte $rp [0] hello en son kurtarma noktası seçer.

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



### <a name="restore-hello-disks"></a>Merhaba disklerini geri yükle
Kullanım hello  **[geri yükleme AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore bir yedekleme öğesi'nin veri ve yapılandırma tooa kurtarma noktası. Bir kurtarma noktası belirledikten sonra Merhaba hello değeri olarak kullanma **- RecoveryPoint** parametresi. Merhaba önceki örnek kodda **$rp [0]** hello kurtarma noktası toouse oluştu. Örnek kod, aşağıdaki hello içinde **$rp [0]** hello disk geri yüklemek için hello kurtarma noktası toouse değil.

toorestore hello diskleri ve yapılandırma bilgileri:

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Kullanım hello  **[bekleme AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  hello geri yükleme işi toocomplete için cmdlet toowait.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

Merhaba geri yükleme işi tamamlandıktan sonra hello kullan  **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  cmdlet tooget hello hello ayrıntılarını geri yükleme işlemi. Merhaba JobDetails özelliği hello bilgi gerekli toorebuild hello VM sahiptir.

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

Merhaba diskleri geri sonra toohello sonraki bölümde toocreate hello VM gidin.

## <a name="create-a-vm-from-restored-disks"></a>Geri yüklenen disklerden bir VM oluşturma
Merhaba diskleri geri yükledikten sonra bu adımları toocreate kullanın ve diskten hello sanal makine yapılandırın.

> [!NOTE]
> geri yüklenen disklerden toocreate şifreli VM'ler, Azure rolünüzün izin tooperform hello eylem olmalıdır **Microsoft.KeyVault/vaults/deploy/action**. Özel bir rol rolünüzün bu izne sahip değilse bu eylemle oluşturun. Daha fazla bilgi için bkz: [Azure rbac'de özel roller](../active-directory/role-based-access-control-custom-roles.md).
>
>

1. Sorgu hello hello iş ayrıntılarını disk özelliklerini geri.

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. Hello Azure depolama bağlamını ayarlayın ve hello JSON yapılandırma dosyasını geri yükleyin.

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. Merhaba JSON yapılandırma dosyası toocreate hello VM yapılandırması kullanın.

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. Merhaba işletim sistemi diski ve veri diskleri ekleyin. Vm'leriniz Hello yapılandırmasına bağlı olarak hello ilgili bağlantı tooview ilgili cmdlet'leri tıklatın: 
    - [Yönetilmeyen, şifrelenmemiş VM'ler](#non-managed-non-encrypted-vms)
    - [Yönetilmeyen, şifrelenmiş VM'ler (yalnızca BEK)](#non-managed-encrypted-vms-bek-only)
    - [Yönetilmeyen, şifrelenmiş VM'ler (BEK ve KEK)](#non-managed-encrypted-vms-bek-and-kek)
    - [Yönetilen, şifrelenmemiş VM'ler](#managed-non-encrypted-vms)
    - [Yönetilen, şifrelenmiş VM'ler (BEK ve KEK)](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a>Yönetilmeyen, şifrelenmemiş VM'ler

    Yönetilmeyen, şifrelenmemiş VM'ler için örnek aşağıdaki hello kullanın.

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a>Yönetilmeyen, şifrelenmiş VM'ler (yalnızca BEK)

    Diskleri ekleyebilirsiniz (BEK yalnızca kullanılarak şifrelenmiş) yönetilmeyen, şifrelenmiş VM'ler için toorestore hello gizli toohello anahtar kasası olması gerekir. Daha fazla bilgi için lütfen hello makalesine bakın [şifrelenmiş bir sanal makine bir Azure yedekleme kurtarma noktasından geri](backup-azure-restore-key-secret.md). Aşağıdaki örnek hello nasıl VM'ler tooattach işletim sistemi ve veri diskleri için şifrelenmiş gösterir.

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a>Yönetilmeyen, şifrelenmiş VM'ler (BEK ve KEK)

    Diskleri eklemeden önce (BEK ve KEK kullanılarak şifrelenmiş) yönetilmeyen, şifrelenmiş VM'ler için toorestore hello anahtarı ve gizli toohello anahtar kasası gerekir. Daha fazla bilgi için lütfen hello makalesine bakın [şifrelenmiş bir sanal makine bir Azure yedekleme kurtarma noktasından geri](backup-azure-restore-key-secret.md). Aşağıdaki örnek hello nasıl VM'ler tooattach işletim sistemi ve veri diskleri için şifrelenmiş gösterir.

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

    #### <a name="managed-non-encrypted-vms"></a>Yönetilen, şifrelenmemiş VM'ler

    Yönetilen şifrelenmemiş VM'ler için blob depolama biriminden yönetilen toocreate diskiniz olması gerekir ve hello diskleri bağlamanız. Ayrıntılı bilgi için hello makalesine bakın [bir veri diski tooa Windows VM ekleme PowerShell kullanarak](../virtual-machines/windows/attach-disk-ps.md). Aşağıdaki örnek kod hello nasıl tooattach hello veri diskleri yönetilen şifrelenmemiş VM'ler için gösterir.

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a>Yönetilen, şifrelenmiş VM'ler (BEK ve KEK)

    (BEK ve KEK kullanılarak şifrelenmiş), şifrelenmiş yönetilen VM'ler blob depolama biriminden yönetilen toocreate diskiniz olması gerekir ve hello diskleri bağlamanız. Ayrıntılı bilgi için hello makalesine bakın [bir veri diski tooa Windows VM ekleme PowerShell kullanarak](../virtual-machines/windows/attach-disk-ps.md). Merhaba aşağıdaki örnek kod nasıl tooattach hello veri diskleri yönetilen şifrelenmiş VM'ler için gösterir.

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

5. Merhaba ağ ayarlarını belirleyin.

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. Merhaba sanal makine oluşturun.

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a>Sonraki adımlar
Azure kaynaklarınızı toouse PowerShell tooengage tercih ederseniz, bkz: hello PowerShell makale [dağıtma ve yönetme yedekleme için Windows Server](backup-client-automation.md). DPM yedeklemelerini yönetme, hello makalesine bakın. [dağıtma ve yönetme yedekleme DPM için](backup-dpm-automation.md). Bu makaleler her ikisi de Resource Manager dağıtımları ve klasik dağıtımları için bir sürümüne sahipsiniz.  
