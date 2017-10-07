---
title: "SQL VM'ler (Resource Manager) aaaAutomate yönetim görevleri | Microsoft Docs"
description: "Bu konuda nasıl toomanage hello belirli SQL Server yönetim görevlerini otomatikleştirir SQL Server Aracısı uzantısı açıklanmaktadır. Bunlar otomatik yedekleme, otomatik düzeltme eki uygulama ve Azure anahtar kasası tümleştirmeyi içerir. Bu konuda hello Resource Manager dağıtım modunu kullanır."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a>Merhaba SQL Server Aracısı uzantısı (Resource Manager) ile Azure sanal makineler üzerinde yönetim görevleri otomatik hale getirme
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-server-agent-extension.md)
> * [Klasik](../classic/sql-server-agent-extension.md)
> 
> 

SQL Server Iaas Aracısı uzantısı (SQLIaaSExtension) Hello Azure sanal makineleri tooautomate yönetim görevlerini üzerinde çalışır. Bu konu, yükleme, durum ve kaldırma yönergeleri yanı sıra hello uzantısı tarafından desteklenen hello hizmetlerine genel bakış sağlar.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Bu makalenin tooview hello Klasik sürümü bkz [SQL Server Aracısı uzantısı için SQL Server sanal makineleri Klasik](../classic/sql-server-agent-extension.md).

## <a name="supported-services"></a>Desteklenen hizmetler
SQL Server Iaas Aracısı uzantısı Hello hello aşağıdaki yönetim görevlerini destekler:

| Yönetim özelliği | Açıklama |
| --- | --- |
| **SQL otomatik yedekleme** |Merhaba hello varsayılan SQL Server'ın örneğinde hello VM tüm veritabanları için yedekleme zamanlaması otomatikleştirir. Daha fazla bilgi için bkz: [Azure Virtual Machines'de (Resource Manager) SQL Server için otomatik yedeklemeyi](virtual-machines-windows-sql-automated-backup.md). |
| **SQL otomatik düzeltme eki uygulama** |Güncelleştirmeleri, iş yükü için yoğun saatlerde kaçınmak için bir bakım penceresi sırasında hangi güncelleştirmelerin VM sürebilir tooyour yerleştirin, yapılandırır. Daha fazla bilgi için bkz: [otomatik Azure Virtual Machines'de (Resource Manager) SQL Server için düzeltme eki uygulama](virtual-machines-windows-sql-automated-patching.md). |
| **Azure Anahtar Kasası Tümleştirmesi** |Tooautomatically yükleme ve SQL Server VM'nize üzerinde Azure anahtar kasası yapılandırma sağlar. Daha fazla bilgi için bkz: [(Resource Manager) Azure vm'lerinde SQL Server için Azure anahtar kasası tümleştirmeyi yapılandırmak](virtual-machines-windows-ps-sql-keyvault.md). |

Yüklü ve çalışan sonra hello SQL Server Iaas Aracısı uzantısı bu yönetim özellikleri hello SQL Server panosunda hello sanal makinenin hello Azure portalı ve Azure PowerShell aracılığıyla ve SQL Server Market görüntülerini için kullanılabilmesini sağlar Azure PowerShell hello uzantısı el ile yüklemeleri için. 

## <a name="prerequisites"></a>Ön koşullar
SQL Server Iaas Aracısı uzantısını VM toouse hello gereksinimleri:

**İşletim sistemi**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**SQL Server sürümleri**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**:

* [İndirme ve hello en son Azure PowerShell komutlarının yapılandırma](/powershell/azure/overview)

## <a name="installation"></a>Yükleme
Merhaba SQL Server sanal makineye Galerisi görüntülerden birini sağladığınızda hello SQL Server Iaas Aracısı uzantısı otomatik olarak yüklenir. Bu SQL Server Vm'lerinin birinde el ile tooreinstall hello uzantısı gerekiyorsa, hello aşağıdaki PowerShell komutunu kullanın:

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

Ayrıca, yalnızca işletim sistemi Windows Server sanal makinede SQL Server Iaas Aracısı uzantısı olası tooinstall hello olur. Bu, yalnızca bu makinede de el ile SQL Server yüklediyseniz desteklenir. Kullanarak el ile yükleme hello uzantısı hello sonra aynı **kümesi AzureVMSqlServerExtension** PowerShell cmdlet'i.

> [!NOTE]
> Bir yalnızca işletim sistemi Windows Server VM üzerinde SQL Server Iaas Aracısı uzantısı hello el ile yüklerseniz, hello SQL Server yapılandırma ayarları hello Azure portal aracılığıyla yönetebilirsiniz değil. Bu senaryoda, PowerShell ile tüm değişiklikler yapmanız gerekir.

## <a name="status"></a>Durum
Tek yönlü tooverify Hello uzantısı yüklenir tooview hello aracı durumunu hello Azure Portal ' dir. Seçin **tüm ayarları** hello sanal makine dikey ve tıklayın **uzantıları**. Merhaba görmelisiniz **SQLIaaSExtension** listelenen uzantısı.

![SQL Server Iaas Aracısı uzantısı Azure portalında](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

Merhaba de kullanabilirsiniz **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet'i.

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

Merhaba önceki komutu hello aracısı yüklü olduğundan ve genel durum bilgilerini sağlar onaylar. Aşağıdaki komutları hello ile otomatik yedekleme ve düzeltme eki ilgili özel durum bilgilerini de alabilirsiniz.

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a>Temizleme
Hello Azure Portal, hello üzerindeki hello üç nokta düğmesine tıklayarak hello uzantısını kaldırabilirsiniz **uzantıları** dikey penceresinde, sanal makine özellikleri. Ardından **silmek**.

![Hello Azure Portalı'nda SQL Server Iaas Aracısı uzantısı kaldırma](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

Merhaba de kullanabilirsiniz **Kaldır AzureRmVMSqlServerExtension** Powershell cmdlet'i.

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a>Sonraki Adımlar
Merhaba uzantısı tarafından desteklenen hello hizmetlerini birini kullanarak başlayın. Daha fazla ayrıntı için bkz: hello başvurulan hello konular [desteklenen Hizmetleri](#supported-services) bu makalenin.

SQL Server Azure sanal makinelerde çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).

