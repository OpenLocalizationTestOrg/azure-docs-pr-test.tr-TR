---
title: "aaaAutomated yedekleme için SQL Server sanal makineler (Klasik) | Microsoft Docs"
description: "SQL Server Kaynak Yöneticisi'ni kullanarak Azure sanal makinelerde çalışan Hello otomatik yedekleme özelliğini açıklar. "
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a>Azure sanal makinelerde (Klasik) SQL Server için otomatik yedekleme
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [Klasik](../classic/sql-automated-backup.md)
> 
> 

Otomatik yedekleme otomatik olarak yapılandırır [yönetilen yedekleme tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) SQL Server 2014 Standard veya Enterprise çalıştıran bir Azure VM üzerindeki tüm mevcut ve yeni veritabanları için. Bu, dayanıklı Azure blob depolama alanını tooconfigure normal veritabanı yedeklemeleri sağlar. Otomatik yedekleme bağlıdır hello üzerinde [SQL Server Iaas Aracısı uzantısı](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Bu makalenin tooview hello Resource Manager sürümü bkz [otomatik yedekleme SQL Server Azure sanal makineleri Kaynak Yöneticisi'nde](../sql/virtual-machines-windows-sql-automated-backup.md).

## <a name="prerequisites"></a>Ön koşullar
toouse otomatik yedekleme önkoşulları aşağıdaki hello göz önünde bulundurun:

**İşletim sistemi**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**SQL Server sürümü/yayını**:

* SQL Server 2014 Standard
* SQL Server 2014 Enterprise

> [!NOTE]
> SQL Server 2016 için otomatik yedekleme henüz desteklenmiyor.
> 
> 

**Veritabanı yapılandırması**:

* Hedef veritabanlarına hello tam kurtarma modeli kullanmanız gerekir.

**Azure PowerShell**:

* [Merhaba en son Azure PowerShell komutlarını yüklemek](/powershell/azure/overview).

**SQL Server Iaas uzantısı**:

* [SQL Server Iaas uzantısı Hello yüklemek](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Ayarlar
Merhaba aşağıdaki tabloda otomatik yedekleme için yapılandırılmış hello seçenekleri açıklanmaktadır. Klasik VM'ler için bu ayarları PowerShell tooconfigure kullanmanız gerekir.

| Ayar | Aralık (varsayılan) | Açıklama |
| --- | --- | --- |
| **Otomatik Yedekleme** |Etkinleştir/devre dışı bırak (devre dışı) |Etkinleştirir veya SQL Server 2014 Standard veya Enterprise çalıştıran bir Azure VM için otomatik yedekleme devre dışı bırakır. |
| **Saklama süresi** |1-30 gün (30 gün) |gün tooretain bir yedekleme Hello sayısı. |
| **Depolama hesabı** |Azure depolama hesabı (Merhaba VM belirtilen için oluşturulan hello depolama hesabı) |Blob depolama alanına otomatik yedekleme dosyalarını depolamak için bir Azure depolama hesabı toouse. Bir kapsayıcı sırasında bu konumu toostore tüm yedekleme dosyaları oluşturulur. Merhaba yedekleme dosyası adlandırma hello tarih, saat ve makine adını içerir. |
| **Şifreleme** |Etkinleştir/devre dışı bırak (devre dışı) |Etkinleştirir veya şifreleme devre dışı bırakır. Şifreleme etkinleştirildiğinde, depolama hesabı kullanılan toorestore hello yedekleme hello bulunan hello sertifikaları belirtilen hello aynı adlandırma kuralı hello kapsayıcı kullanarak automaticbackup aynı. Merhaba parola değişirse, bu parola ile yeni bir sertifika oluşturulur, ancak toorestore önceki yedeklemeleri hello eski sertifika kalır. |
| **Parola** |Parola metin (yok) |Şifreleme anahtarları için bir parola. Yalnızca budur şifreleme etkin olup olmadığını gerekli. Sipariş toorestore şifreli bir yedekleme hello doğru parolayı ve hello yedeğin alındığı hello zamanında kullanılan ilgili sertifika olmalıdır. | **Yedekleme sistem veritabanları** | Etkinleştir/devre dışı bırak (devre dışı) | Master, Model ve MSDB tam yedekleme gerçekleştirin |
| **Yedekleme zamanlaması yapılandırma** | El ile otomatik / (otomatik) | Seçin **otomatik** tooautomatically tam alabilir ve oturum Günlük büyüme üzerinde bağlı olarak yedeklemeler. Seçin **el ile** tam toospecify hello zamanlamasını ve günlük yedekleri. |

## <a name="configuration-with-powershell"></a>PowerShell ile yapılandırma
Aşağıdaki PowerShell örneğine hello otomatik yedekleme için mevcut bir SQL Server 2014 VM'yi yapılandırılır. Merhaba **yeni AzureVMSqlServerAutoBackupConfig** komut hello $storageaccount değişkeni tarafından belirtilen hello Azure depolama hesabında hello otomatik yedekleme ayarlarını toostore yedeklemeler yapılandırır. Bu yedeklemeler 10 gün boyunca saklanır. Merhaba **kümesi AzureVMSqlServerExtension** güncelleştirmeleri hello Azure VM bu ayarlarla belirtilen komutu.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

Birkaç dakika tooinstall alın ve hello SQL Server Iaas Aracısı Yapılandırma.

tooenable şifreleme hello önceki betik toopass hello EnableEncryption parametresi bir parola (güvenli dize) ile birlikte hello CertificatePassword parametresi için değiştirin. Merhaba aşağıdaki betiği hello önceki örnekte hello otomatik yedekleme ayarlarını etkinleştirir ve şifreleme ekler.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

toodisable otomatik yedekleme hello aynı komut dosyası çalıştırma hello **-etkinleştirmek** parametresi toohello **yeni AzureVMSqlServerAutoBackupConfig**. Yüklemesine gibi birkaç dakika toodisable otomatik yedekleme alabilir.

> [!NOTE]
> Önceden yapılandırılmış hello yönetilen Yedekleme ayarlarını devre dışı bırakma ve hello SQL Server Iaas aracısı kaldırma kaldırmaz. Devre dışı bırakma veya SQL Server Iaas Aracısı hello kaldırmadan önce otomatik yedekleme devre dışı bırakmalısınız.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Otomatik yedekleme yönetilen yedekleme Azure Vm'lerinde yapılandırır. Çok önemlidir[yönetilen yedekleme hello belgelerini gözden geçirin](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello davranışı ve etkileri.

Ek yedekleme bulmak ve izleyen konu hello Azure Vm'lerde SQL Server için kılavuzunda geri yükleyebilirsiniz: [yedekleme ve geri yükleme Azure Virtual Machines'de SQL Server için](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](../classic/sql-server-agent-extension.md).

Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

