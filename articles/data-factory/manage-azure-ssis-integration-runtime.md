---
title: "Bir Azure SSIS tümleştirmesi çalışma zamanı yeniden | Microsoft Docs"
description: "Zaten sağlanmış sonra Azure Data Factory bir Azure SSIS tümleştirmesi çalışma zamanı yeniden öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/22/2018
ms.author: spelluru
ms.openlocfilehash: b4b777a858febb4b601c038508e4fc313c189ac2
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/24/2018
---
# <a name="manage-an-azure-ssis-integration-runtime"></a>Bir Azure SSIS tümleştirmesi çalışma zamanı yönetme
[Azure SSIS tümleştirmesi çalışma zamanı oluşturma](create-azure-ssis-integration-runtime.md) makalede Azure Data Factory kullanarak bir Azure SSIS tümleştirmesi çalışma zamanı (IR) oluşturma gösterilmektedir. Bu makalede, var olan bir Azure SSIS tümleştirmesi çalışma zamanı yeniden yapılandırma hakkında bilgi sağlar.  

> [!NOTE]
> Bu makale şu anda önizleme sürümünde olan Data Factory sürüm 2 için geçerlidir. Data Factory hizmetinin genel kullanıma açık 1. sürümünü kullanıyorsanız bkz. [Data Factory sürüm 1 belgeleri](v1/data-factory-introduction.md).


## <a name="data-factory-ui"></a>Data Factory Kullanıcı Arabirimi (UI) 
Veri Fabrikası UI durdurmak, düzenleme/yeniden yapılandırın veya bir Azure SSIS IR silmek için kullanabileceğiniz 

1. İçinde **veri fabrikası UI**, geçiş **Düzenle** sekmesi. Veri Fabrikası UI başlatmak için tıklatın **Yazar & İzleyici** veri fabrikanızın giriş sayfasında.
2. Sol bölmede **bağlantıları**.
3. Sağ bölmede geçmek **tümleştirme çalışma zamanları**. 
4. Eylemler sütununda düğmeleri kullanabilirsiniz **durdurmak**, **Düzenle**, veya **silmek** tümleştirmesi çalışma zamanı. **Kod** düğmesini **Eylemler** sütun tümleştirmesi çalışma zamanı ile ilişkili JSON tanımını görüntüleme olanak sağlar.  
    
    ![Azure SSIS IR eylemleri](./media/manage-azure-ssis-integration-runtime/actions-for-azure-ssis-ir.png)

### <a name="to-reconfigure-an-azure-ssis-ir"></a>Bir Azure SSIS IR yeniden yapılandırmak için
1. Tümleştirme çalışma zamanı tıklayarak durdurun **durdurmak** içinde **Eylemler** sütun. Liste görünümü yenilemek için tıklatın **yenileme** araç çubuğunda. IR durdurulduktan sonra ilk eylem IR başlatmanıza olanak tanır bakın 

    ![Azure SSIS durduruldu sonra IR - eylemleri](./media/manage-azure-ssis-integration-runtime/actions-after-ssis-ir-stopped.png)
2. Düzenle/tıklayarak RECONFIGURE IR **Düzenle** düğmesini **Eylemler** sütun. İçinde **tümleştirmesi çalışma zamanı Kurulum** penceresinde, (örneğin, düğüm veya düğüm başına en fazla paralel yürütmeleri sayısı, düğüm boyutu) ayarlarını değiştirin. 
3. IR yeniden başlatmak için tıklatın **Başlat** düğmesini **Eylemler** sütun.     

## <a name="azure-powershell"></a>Azure PowerShell
Sağlamak ve bir örneğini Azure SSIS Integration zamanının başlatmak sonra onu bir dizi çalıştırarak yeniden yapılandırabilirsiniz `Stop`  -  `Set`  -  `Start` PowerShell cmdlet öğelerini ardışık. Örneğin, aşağıdaki PowerShell betiğini beş Azure SSIS tümleştirmesi çalışma zamanı örneği için ayrılan düğüm sayısını değiştirir.

### <a name="reconfigure-an-azure-ssis-ir"></a>Bir Azure SSIS IR yeniden yapılandırın

1. İlk olarak, Azure SSIS tümleştirmesi çalışma zamanı kullanarak durdurmak [Stop-AzureRmDataFactoryV2IntegrationRuntime](/powershell/module/azurerm.datafactoryv2/stop-azurermdatafactoryv2integrationruntime?view=azurermps-4.4.1) cmdlet'i. Bu komut tüm düğümlerinin serbest bırakır ve faturalama durdurur.

    ```powershell
    Stop-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSSISName -ResourceGroupName $ResourceGroupName 
    ```
2. Ardından, Azure SSIS IR kullanarak yeniden [kümesi AzureRmDataFactoryV2IntegrationRuntime](/powershell/module/azurerm.datafactoryv2/set-azurermdatafactoryv2integrationruntime?view=azurermps-4.4.1) cmdlet'i. Aşağıdaki örnek komut, bir Azure SSIS tümleştirmesi çalışma zamanı beş düğümlere çıkışı ölçeklendirir.

    ```powershell
    Set-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSSISName -ResourceGroupName $ResourceGroupName -NodeCount 5
    ```  
3. Sonra Azure SSIS tümleştirmesi çalışma zamanı başlamayı [başlangıç AzureRmDataFactoryV2IntegrationRuntime](/powershell/module/azurerm.datafactoryv2/start-azurermdatafactoryv2integrationruntime?view=azurermps-4.4.1) cmdlet'i. Bu komut tüm düğümlerinin SSIS paketleri çalıştırmak için ayırır.   

    ```powershell
    Start-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSSISName -ResourceGroupName $ResourceGroupName
    ```

### <a name="delete-an-azure-ssis-ir"></a>Bir Azure SSIS IR Sil
1. İlk olarak, tüm mevcut Azure SSIS IRS data factory'nizi altında listeleyin.

    ```powershell
    Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -ResourceGroupName $ResourceGroupName -Status
    ```
2. Ardından, veri fabrikası'nda tüm mevcut Azure SSIS IRS durdurun.

    ```powershell
    Stop-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSSISName -ResourceGroupName $ResourceGroupName -Force
    ```
3. Ardından, tüm mevcut Azure SSIS IRS, veri fabrikası tek tek kaldırın.

    ```powershell
    Remove-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSSISName -ResourceGroupName $ResourceGroupName -Force
    ```
4. Son olarak, veri fabrikası kaldırın.

    ```powershell
    Remove-AzureRmDataFactoryV2 -Name $DataFactoryName -ResourceGroupName $ResourceGroupName -Force
    ```
5. Yeni bir kaynak grubu oluşturduysanız, kaynak grubunu kaldırın.

    ```powershell
    Remove-AzureRmResourceGroup -Name $ResourceGroupName -Force 
    ```

## <a name="next-steps"></a>Sonraki adımlar
Azure SSIS çalışma zamanı hakkında daha fazla bilgi için aşağıdaki konulara bakın: 

- [Azure SSIS tümleştirmesi çalışma zamanı](concepts-integration-runtime.md#azure-ssis-integration-runtime). Bu makalede Azure SSIS IR genel dahil tümleştirme çalışma zamanları hakkında kavramsal bilgiler sağlar 
- [Öğretici: SSIS paketlerini Azure’a dağıtma](tutorial-deploy-ssis-packages-azure.md). Bu makale bir Azure-SSIS IR oluşturmaya ilişkin adım adım yönergeler sağlar ve SSIS kataloğunu barındırmak için bir Azure SQL veritabanı kullanır. 
- [Nasıl yapılır: Azure-SSIS tümleştirme çalışma zamanı oluşturma](create-azure-ssis-integration-runtime.md). Bu makale, öğreticiyi genişletip Azure SQL Yönetilen Örneğini (özel önizleme) kullanma ve IR’yi bir sanal ağa ekleme hakkında yönergeler sağlar. 
- [Azure-SSIS IR’yi bir sanal ağa ekleme](join-azure-ssis-integration-runtime-virtual-network.md). Bu makale Azure-SSIS IR’yi bir Azure sanal ağına (VNet) ekleme hakkında kavramsal bilgiler sağlar. Ayrıca, Azure portalını kullanarak Azure-SSIS IR’nin sanal ağa katılmasını sağlayacak şekilde sanal ağı yapılandırma adımları sunar. 
- [Azure-SSIS IR’yi izleme](monitor-integration-runtime.md#azure-ssis-integration-runtime). Bu makalede bir Azure-SSIS IR ile ilgili bilgileri ve döndürülen bilgilerdeki durumların açıklamalarını alma işlemi gösterilmektedir. 
 
