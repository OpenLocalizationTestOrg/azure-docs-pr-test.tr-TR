---
title: "aaaAutomated SQL Server Vm'lerinin (Klasik) için düzeltme eki uygulama | Microsoft Docs"
description: "Merhaba otomatik düzeltme eki uygulama özelliği için SQL Server hello Klasik dağıtım modunu kullanarak Azure'da çalışan sanal makineler açıklanmıştır."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a>Otomatik Azure sanal makinelerde (Klasik) SQL Server için düzeltme eki uygulama
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [Klasik](../classic/sql-automated-patching.md)
> 
> 

Otomatik düzeltme eki bir Azure SQL Server çalıştıran sanal makine için bir bakım penceresi oluşturur. Otomatik Güncelleştirmeler, yalnızca bu bakım penceresi sırasında yüklenebilir. SQL Server için bu sistem güncelleştirmelerini ve ilişkili tüm yeniden başlatmalar hello veritabanı için en iyi olası zaman hello gerçekleşmesini sağlar. Otomatik düzeltme eki bağlıdır hello üzerinde [SQL Server Iaas Aracısı uzantısı](../classic/sql-server-agent-extension.md).

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Bu makalenin tooview hello Resource Manager sürümü bkz [otomatik düzeltme eki uygulama SQL Server Azure sanal makineleri Kaynak Yöneticisi'nde](../sql/virtual-machines-windows-sql-automated-patching.md).

## <a name="prerequisites"></a>Ön koşullar
toouse Önkoşullar aşağıdaki hello otomatik düzeltme eki uygulama, göz önünde bulundurun:

**İşletim sistemi**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**SQL Server sürümü**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**:

* [Merhaba en son Azure PowerShell komutlarını yüklemek](/powershell/azure/overview).

**SQL Server Iaas uzantısı**:

* [SQL Server Iaas uzantısı Hello yüklemek](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Ayarlar
Merhaba aşağıdaki tabloda otomatik düzeltme eki uygulama için yapılandırılabilir hello seçenekleri açıklanmaktadır. Klasik VM'ler için bu ayarları PowerShell tooconfigure kullanmanız gerekir.

| Ayar | Olası değerler | Açıklama |
| --- | --- | --- |
| **Otomatik Düzeltme Eki Uygulama** |Etkinleştir/devre dışı bırak (devre dışı) |Etkinleştirir veya bir Azure sanal makine için otomatik düzeltme eki uygulamayı devre dışı bırakır. |
| **Bakım zamanlaması** |Her gün, Pazartesi, Salı, Çarşamba, Perşembe, Cuma, Cumartesi Pazar |Sanal makineniz için Windows, SQL Server ve Microsoft güncelleştirmeler indiriliyor ve yükleniyor için hello zamanlama. |
| **Bakım başlangıç saati** |0-24 |Merhaba yerel başlatma zamanı tooupdate hello sanal makine. |
| **Bakım penceresinin süresi** |30-180 |Merhaba süreyi dakika cinsinden izin verilen toocomplete hello indirme ve güncelleştirmeleri yükleme. |
| **Düzeltme eki kategorisi** |Önemli |güncelleştirmeleri toodownload ve yükleme Hello kategorisi. |

## <a name="configuration-with-powershell"></a>PowerShell ile yapılandırma
Aşağıdaki örneğine hello kullanılan tooconfigure powershell'dir otomatik düzeltme eki uygulama mevcut bir SQL Server VM üzerinde. Merhaba **yeni AzureVMSqlServerAutoPatchingConfig** komut, otomatik güncelleştirmeler için yeni bir bakım penceresi yapılandırır.

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

Bu örneği temel alarak, hello aşağıdaki tabloda hello pratik hello hedef Azure VM etkisi açıklanmaktadır:

| Parametre | Etki |
| --- | --- |
| **DayOfWeek** |Her Perşembe düzeltme ekleri yüklenmemiş. |
| **MaintenanceWindowStartingHour** |Begin 11: 00'da güncelleştirir. |
| **MaintenanceWindowsDuration** |Düzeltme ekleri 120 dakika içinde yüklü olması gerekir. Merhaba başlangıç zamanı temel alınarak, 1:00 pm tarafından tamamlamalıdır. |
| **PatchCategory** |Merhaba yalnızca olası için bu parametreyi "Önemli" ayardır. |

Birkaç dakika tooinstall alın ve hello SQL Server Iaas Aracısı Yapılandırma.

toodisable otomatik düzeltme eki uygulama, aynı komut dosyası olmadan çalıştırma hello hello - Enable parametresini toohello yeni AzureVMSqlServerAutoPatchingConfig. Yükleme ile birkaç dakika toodisable sürebilir gibi otomatik düzeltme eki uygulama.

## <a name="next-steps"></a>Sonraki adımlar
Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](../classic/sql-server-agent-extension.md).

Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

