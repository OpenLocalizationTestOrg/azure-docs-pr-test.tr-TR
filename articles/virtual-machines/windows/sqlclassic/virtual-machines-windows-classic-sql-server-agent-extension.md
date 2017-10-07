---
title: "SQL VM'ler (Klasik) aaaAutomate yönetim görevleri | Microsoft Docs"
description: "Bu konuda nasıl toomanage hello belirli SQL Server yönetim görevlerini otomatikleştirir SQL Server Aracısı uzantısı açıklanmaktadır. Bunlar otomatik yedekleme, otomatik düzeltme eki uygulama ve Azure anahtar kasası tümleştirmeyi içerir. Bu konuda hello Klasik dağıtım modunu kullanır."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a>Merhaba SQL Server Aracısı uzantısı (Klasik) ile Azure sanal makineler üzerinde yönetim görevleri otomatik hale getirme
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [Klasik](../classic/sql-server-agent-extension.md)
> 
>
 
SQL Server Iaas Aracısı uzantısı (Sqlıaasagent) Hello Azure sanal makineleri tooautomate yönetim görevlerini üzerinde çalışır. Bu konu, yükleme, durum ve kaldırma yönergeleri yanı sıra hello uzantısı tarafından desteklenen hello hizmetlerine genel bakış sağlar.

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Bu makalenin tooview hello Resource Manager sürümü bkz [SQL Server Aracısı uzantısı için SQL Server VM'ler Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).

## <a name="supported-services"></a>Desteklenen hizmetler
SQL Server Iaas Aracısı uzantısı Hello hello aşağıdaki yönetim görevlerini destekler:

| Yönetim özelliği | Açıklama |
| --- | --- |
| **SQL otomatik yedekleme** |Merhaba hello varsayılan SQL Server'ın örneğinde hello VM tüm veritabanları için yedekleme zamanlaması otomatikleştirir. Daha fazla bilgi için bkz: [Azure Virtual Machines'de (Klasik) SQL Server için otomatik yedeklemeyi](../classic/sql-automated-backup.md). |
| **SQL otomatik düzeltme eki uygulama** |Güncelleştirmeleri, iş yükü için yoğun saatlerde kaçınmak için bir bakım penceresi sırasında hangi güncelleştirmelerin VM sürebilir tooyour yerleştirin, yapılandırır. Daha fazla bilgi için bkz: [otomatik Azure Virtual Machines'de (Klasik) SQL Server için düzeltme eki uygulama](../classic/sql-automated-patching.md). |
| **Azure Anahtar Kasası Tümleştirmesi** |Tooautomatically yükleme ve SQL Server VM'nize üzerinde Azure anahtar kasası yapılandırma sağlar. Daha fazla bilgi için bkz: [(Klasik) Azure vm'lerinde SQL Server için Azure anahtar kasası tümleştirmeyi yapılandırmak](../classic/ps-sql-keyvault.md). |

## <a name="prerequisites"></a>Ön koşullar
SQL Server Iaas Aracısı uzantısını VM toouse hello gereksinimleri:

### <a name="operating-system"></a>İşletim Sistemi:
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

### <a name="sql-server-versions"></a>SQL Server sürümleri:
* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

### <a name="azure-powershell"></a>Azure PowerShell:
[İndirme ve hello en son Azure PowerShell komutlarının yapılandırma](/powershell/azure/overview).

Windows PowerShell'i başlatın ve tooyour Azure aboneliği ile Merhaba bağlamak **Add-AzureAccount** komutu.

    Add-AzureAccount

Birden çok aboneliğiniz varsa, kullanmak **Select-AzureSubscription** hedef içeren tooselect hello abonelik Klasik VM.

    Select-AzureSubscription -SubscriptionName <subscriptionname>

Bu noktada, hello Klasik sanal makineleri ve ilişkili hizmet adlarını hello listesini almak **Get-AzureVM** komutu.

    Get-AzureVM

## <a name="installation"></a>Yükleme
Klasik VM'ler için PowerShell tooinstall hello SQL Server Iaas Aracısı uzantısı kullanın ve ilişkili hizmetlerini yapılandırmanız gerekir. Kullanım hello **kümesi AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello uzantısı. Örneğin, komutu aşağıdaki hello hello uzantısı bir Windows Server VM'ye (Klasik) yükler ve bunu "SQLIaaSExtension" adları.

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

Merhaba SQL Iaas Aracısı uzantısı en son sürümünü toohello güncelleştirirseniz, hello uzantısı güncelleştirdikten sonra sanal makinenizi yeniden başlatmanız gerekir.

> [!NOTE]
> Klasik sanal makineleri olmayan bir seçenek tooinstall sahip ve hello SQL Iaas Aracısı uzantısı hello portal üzerinden yapılandırın.
> 
> 

## <a name="status"></a>Durum
Tek yönlü tooverify Hello uzantısı yüklenir tooview hello aracı durumunu hello Azure Portal ' dir. Merhaba sanal makine dikey penceresinde listelenen bir sanal makineyi seçin ve ardından tıklatın **uzantıları**. Merhaba görmelisiniz **Sqlıaasagent** listelenen uzantısı.

![SQL Server Iaas Aracısı uzantısı Azure portalında](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

Merhaba de kullanabilirsiniz **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet'i.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a>Temizleme
Hello Azure Portal, hello üzerindeki hello üç nokta düğmesine tıklayarak hello uzantısını kaldırabilirsiniz **uzantıları** dikey penceresinde, sanal makine özellikleri. Ardından **kaldırma**.

![Hello Azure Portalı'nda SQL Server Iaas Aracısı uzantısı kaldırma](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

Merhaba de kullanabilirsiniz **Kaldır AzureVMSqlServerExtension** Powershell cmdlet'i.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a>Sonraki Adımlar
Merhaba uzantısı tarafından desteklenen hello hizmetlerini birini kullanarak başlayın. Daha fazla ayrıntı için bkz: hello başvurulan hello konular [desteklenen Hizmetleri](#supported-services) bu makalenin.

SQL Server Azure sanal makinelerde çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

