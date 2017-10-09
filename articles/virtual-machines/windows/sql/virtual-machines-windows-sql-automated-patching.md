---
title: "aaaAutomated SQL Server Vm'lerinin (Resource Manager) için düzeltme eki uygulama | Microsoft Docs"
description: "Merhaba otomatik düzeltme eki uygulama özelliği için SQL Server Kaynak Yöneticisi'ni kullanarak Azure'da çalışan sanal makineler açıklanmıştır."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a>Azure Virtual Machines’de (Resource Manager) SQL Server için Otomatik Düzeltme Eki Uygulama
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-automated-patching.md)
> * [Klasik](../classic/sql-automated-patching.md)
> 
> 

Otomatik düzeltme eki bir Azure SQL Server çalıştıran sanal makine için bir bakım penceresi oluşturur. Otomatik Güncelleştirmeler, yalnızca bu bakım penceresi sırasında yüklenebilir. SQL Server için bu rescriction sistem güncelleştirmelerini ve ilişkili tüm yeniden başlatmalar hello veritabanı için en iyi olası zaman hello gerçekleşmesini sağlar. Otomatik düzeltme eki bağlıdır hello üzerinde [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Bu makalenin tooview hello Klasik sürümü bkz [otomatik düzeltme eki uygulama için Azure sanal makineleri Klasik SQL Server'da](../classic/sql-automated-patching.md).

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

* [Merhaba en son Azure PowerShell komutlarını yüklemek](/powershell/azure/overview) tooconfigure düşünüyorsanız, otomatik düzeltme eki uygulama PowerShell ile.

> [!NOTE]
> Otomatik düzeltme eki hello üzerinde SQL Server Iaas Aracısı uzantısı kullanır. Geçerli SQL sanal makineye Galerisi görüntülerini varsayılan olarak bu uzantı ekleyin. Daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).
> 
> 

## <a name="settings"></a>Ayarlar
Merhaba aşağıdaki tabloda otomatik düzeltme eki uygulama için yapılandırılabilir hello seçenekleri açıklanmaktadır. Merhaba gerçek yapılandırma adımlarını hello Azure portalında veya Azure Windows PowerShell komutlarını kullanmadığınıza bağlı olarak farklılık gösterir.

| Ayar | Olası değerler | Açıklama |
| --- | --- | --- |
| **Otomatik Düzeltme Eki Uygulama** |Etkinleştir/devre dışı bırak (devre dışı) |Etkinleştirir veya bir Azure sanal makine için otomatik düzeltme eki uygulamayı devre dışı bırakır. |
| **Bakım zamanlaması** |Her gün, Pazartesi, Salı, Çarşamba, Perşembe, Cuma, Cumartesi Pazar |Sanal makineniz için Windows, SQL Server ve Microsoft güncelleştirmeler indiriliyor ve yükleniyor için hello zamanlama. |
| **Bakım başlangıç saati** |0-24 |Merhaba yerel başlatma zamanı tooupdate hello sanal makine. |
| **Bakım penceresinin süresi** |30-180 |Merhaba süreyi dakika cinsinden izin verilen toocomplete hello indirme ve güncelleştirmeleri yükleme. |
| **Düzeltme eki kategorisi** |Önemli |güncelleştirmeleri toodownload ve yükleme Hello kategorisi. |

## <a name="configuration-in-hello-portal"></a>Merhaba Portal Yapılandırması
Hello Azure portal tooconfigure kullanabileceğiniz otomatik düzeltme eki uygulama sağlama sırasında veya var olan VM'ler için.

### <a name="new-vms"></a>Yeni sanal makineleri
Kullanım hello Azure portal tooconfigure otomatik hello Resource Manager dağıtım modelinde yeni bir SQL Server sanal makine oluşturduğunuzda, düzeltme eki uygulama.

Merhaba, **SQL Server ayarları** dikey penceresinde, select **otomatik düzeltme eki uygulama**. Merhaba aşağıdaki Azure portal ekran görüntüsü gösterir hello **SQL otomatik düzeltme eki uygulama** dikey.

![SQL otomatik düzeltme eki Azure portalında](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

Bağlam için hello tam üzerinde konusuna [azure'da bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Var olan sanal makineleri
Var olan SQL Server sanal makineler için SQL Server sanal makine seçin. Merhaba seçip **SQL Server yapılandırma** hello bölümünü **ayarları** dikey.

![SQL otomatik düzeltme eki uygulama var olan VM'ler için](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

Merhaba, **SQL Server yapılandırma** dikey penceresinde hello tıklatın **Düzenle** hello düğmesini otomatik düzeltme eki uygulama bölümü.

![SQL otomatik düzeltme eki uygulama var olan VM'ler için yapılandırma](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

Tamamlandığında, hello tıklatın **Tamam** hello hello alt düğmesinde **SQL Server yapılandırma** dikey toosave değişikliklerinizi.

Otomatik düzeltme eki uygulama hello için ilk kez etkinleştiriyorsanız, Azure SQL Server Iaas Aracısı hello hello arka planda yapılandırır. Bu süre boyunca, otomatik düzeltme eki uygulama yapılandırıldığını hello Azure portal gösterilmeyebilir. Merhaba Aracısı toobe yüklü, birkaç dakika bekleyin yapılandırılmış. Bu hello sonra Azure portalı hello yeni ayarlarını yansıtır.

> [!NOTE]
> Bir şablon kullanarak otomatik düzeltme eki uygulama da yapılandırabilirsiniz. Daha fazla bilgi için bkz: [otomatik düzeltme eki uygulama için Azure Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).
> 
> 

## <a name="configuration-with-powershell"></a>PowerShell ile yapılandırma
SQL VM'nizi sağladıktan sonra PowerShell tooconfigure kullanın otomatik düzeltme eki uygulama.

Aşağıdaki örneğine hello kullanılan tooconfigure powershell'dir otomatik düzeltme eki uygulama mevcut bir SQL Server VM üzerinde. Merhaba **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** komut, otomatik güncelleştirmeler için yeni bir bakım penceresi yapılandırır.

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

Bu örneği temel alarak, hello aşağıdaki tabloda hello pratik hello hedef Azure VM etkisi açıklanmaktadır:

| Parametre | Etki |
| --- | --- |
| **DayOfWeek** |Her Perşembe düzeltme ekleri yüklenmemiş. |
| **MaintenanceWindowStartingHour** |Begin 11: 00'da güncelleştirir. |
| **MaintenanceWindowsDuration** |Düzeltme ekleri 120 dakika içinde yüklü olması gerekir. Merhaba başlangıç zamanı temel alınarak, 1:00 pm tarafından tamamlamalıdır. |
| **PatchCategory** |Bu parametre yalnızca olası ayarı hello **önemli**. |

Birkaç dakika tooinstall alın ve hello SQL Server Iaas Aracısı Yapılandırma.

toodisable otomatik düzeltme eki uygulama, hello aynı komut dosyası çalıştırma hello **-etkinleştirmek** parametresi toohello **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**. Merhaba hello yokluğu **-etkinleştirmek** parametresi sinyalleri hello komutu toodisable hello özelliği.

## <a name="next-steps"></a>Sonraki adımlar
Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).

Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).

