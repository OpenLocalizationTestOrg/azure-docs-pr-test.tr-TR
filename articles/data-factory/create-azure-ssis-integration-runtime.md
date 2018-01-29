---
title: "Azure Data Factory'de Azure SSIS tümleştirmesi çalışma zamanı oluşturma | Microsoft Docs"
description: "SSIS paketi Azure bulutunda çalıştırabilmeniz için bir Azure SSIS tümleştirmesi çalışma zamanı oluşturmayı öğrenin."
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
ms.openlocfilehash: 6eec344761df67fd8e8b3c6fceedb8ee68e85b9a
ms.sourcegitcommit: 99d29d0aa8ec15ec96b3b057629d00c70d30cfec
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="create-an-azure-ssis-integration-runtime-in-azure-data-factory"></a>Azure Data Factory'de bir Azure SSIS tümleştirmesi çalışma zamanı oluşturma
Bu makalede Azure Data Factory bir Azure SSIS tümleştirmesi çalışma zamanı sağlamak için adımları sağlar. Daha sonra, SQL Server Veri Araçları (SSDT) veya SQL Server Management Studio’yu (SSMS) kullanarak Azure’da bu çalışma zamanına SQL Server Integration Services (SSIS) paketleri dağıtabilirsiniz.

Öğretici: [Öğreticisi: SQL Server Integration Services (SSIS) Azure'a dağıtabilmeniz](tutorial-deploy-ssis-packages-azure.md) Azure SQL veritabanını depo olarak SSIS kataloğunu kullanarak Azure SSIS tümleştirmesi çalışma zamanı (IR) nasıl oluşturulacağını gösterir. Bu makalede öğreticiyi genişletir ve aşağıdakilerin nasıl yapılacağını gösterir: 

- Azure SQL yönetilen örneği (özel olarak incelenmektedir) SSIS katalog (SSISDB veritabanı) barındırmak için kullanın.
- Bir Azure sanal ağı (VNet) için Azure SSIS IR katılın. Bir sanal ağa bir Azure SSIS IR birleştirme ve Azure portalında VNet yapılandırma kavramsal bilgi için bkz: [katılma Azure SSIS IR vnet'e](join-azure-ssis-integration-runtime-virtual-network.md). 

> [!NOTE]
> Bu makale şu anda önizleme sürümünde olan Data Factory sürüm 2 için geçerlidir. Data Factory hizmetinin genel kullanıma açık (GA) 1. sürümünü kullanıyorsanız [Data Factory sürüm 1 belgeleri](v1/data-factory-introduction.md) konusunu inceleyin.


## <a name="overview"></a>Genel Bakış
Bu makalede Azure SSIS IR sağlama farklı yolu gösterilmektedir:

- [Azure portalı](#azure-portal)
- [Azure PowerShell](#azure-powershell)
- [Azure Resource Manager şablonu](#azure-resource-manager-template)

Bir Azure SSIS IR oluşturduğunuzda, veri fabrikası, Azure SQL SSIS Katalog veritabanı (SSISDB) hazırlamak için veritabanına bağlar. Betik ayrıca belirtilmişse sanal ağınıza ilişkin izin ve ayarları yapılandırır ve yeni Azure SSIS tümleştirme çalışma zamanı örneğini sanal ağa ekler.

Örneği, Azure SSIS IR sağladığınızda, SSIS ve erişim Redistributable için Azure özellik paketi de yüklenir. Bu bileşenler, Excel ve erişim dosyaları ve yerleşik bileşenler tarafından desteklenen veri kaynakları yanı sıra çeşitli Azure veri kaynakları için bağlantı sağlar. (Attunity Oracle ve Teradata bileşenleri ve SAP BI bileşenleri gibi Microsoft, üçüncü taraf bileşenler dahil) şu anda, üçüncü taraf bileşenler için SSIS yükleyemezsiniz.

## <a name="prerequisites"></a>Önkoşullar

- **Azure aboneliği**. Bir aboneliğiniz yoksa, bir [ücretsiz deneme](http://azure.microsoft.com/pricing/free-trial/) hesabı oluşturabilirsiniz.
- **Azure SQL Veritabanı sunucusu** veya **SQL Server Yönetilen Örneği (özel önizleme) (Genişletilmiş Özel Önizleme)**. Henüz bir veritabanı sunucunuz yoksa, başlamadan önce Azure portalında bir tane oluşturun. Bu sunucu, SSIS Katalog veritabanını (SSISDB) barındırır. Veritabanı sunucusunu tümleştirme çalışma zamanı ile aynı Azure bölgesinde oluşturmanız önerilir. Bu yapılandırma, tümleştirme çalışma zamanının Azure bölgelerinden geçmeden SSISDB’ye yürütme günlüklerini yazmasına olanak tanır. Azure SQL sunucusunun fiyatlandırma katmanı unutmayın. Azure SQL veritabanı için desteklenen fiyatlandırma katmanlarına listesi için bkz: [SQL veritabanı kaynak sınırları](../sql-database/sql-database-resource-limits.md).

    Azure SQL veritabanı sunucusu veya SQL Server örneği (Genişletilmiş özel Önizleme) yönetilen bir SSIS katalog (SSIDB veritabanı) olmadığından emin olun. Sağlama Azure SSIS IR varolan bir SSIS Kataloğu kullanımını desteklemez.
- **Klasik veya Azure Resource Manager sanal Network(VNet) (isteğe bağlı)**. Aşağıdaki koşulların en az biri geçerli ise bir Azure Sanal Ağınız (VNet) olmalıdır:
    - SSIS Katalog veritabanını bir sanal ağın parçası olan SQL Server Yönetilen Örneği (özel önizleme) üzerinde barındırıyorsanız.
    - Şirket içi veri depolarına bir Azure-SSIS tümleştirme çalışma zamanı üzerinde çalışan SSIS paketlerinden bağlanmak istiyorsanız.
- **Azure PowerShell**. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/install-azurerm-ps) bölümündeki yönergeleri izleyin. Bulutta SSIS paketleri çalıştıran bir Azure-SSIS tümleştirme çalışma zamanı sağlamak üzere betik çalıştırmak için PowerShell kullanıyorsanız. 

> [!NOTE]
> Azure Data Factory V2 ve Azure-SSIS Integration Runtime tarafından desteklenen tüm bölgelerin listesi için bkz. [Bölgelere göre kullanılabilir ürünler](https://azure.microsoft.com/regions/services/). **Veri ve Analiz**’i genişleterek **Data Factory V2** ve **SSIS Integration Runtime** seçeneklerini görün.

## <a name="azure-portal"></a>Azure portalına
Bu bölümde, bir Azure SSIS IR oluşturmak için Azure portal, veri fabrikası UI özellikle kullanın 

### <a name="create-a-data-factory"></a>Veri fabrikası oluşturma

1. [Azure Portal](https://portal.azure.com/)’da oturum açın.    
2. Soldaki menüde **Yeni**, **Veri + Analiz** ve **Data Factory** öğesine tıklayın. 
   
   ![Yeni->DataFactory](./media/tutorial-create-azure-ssis-runtime-portal/new-data-factory-menu.png)
3. **Yeni veri fabrikası** sayfasında **ad** için **MyAzureSsisDataFactory** adını girin. 
      
     ![Yeni veri fabrikası sayfası](./media/tutorial-create-azure-ssis-runtime-portal/new-azure-data-factory.png)
 
   Azure data factory adı **küresel olarak benzersiz** olmalıdır. Aşağıdaki hatayı alırsanız veri fabrikasının adını değiştirin (örneğin adınızMyAzureSsisDataFactory) ve yeniden oluşturmayı deneyin. Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](naming-rules.md) makalesine bakın.
  
       `Data factory name “MyAzureSsisDataFactory” is not available`
3. Veri fabrikasını oluşturmak istediğiniz Azure **aboneliğini** seçin. 
4. **Kaynak Grubu** için aşağıdaki adımlardan birini uygulayın:
     
      - **Var olanı kullan**’ı seçin ve ardından açılır listeden var olan bir kaynak grubu belirleyin. 
      - **Yeni oluştur**’u seçin ve bir kaynak grubunun adını girin.   
         
      Kaynak grupları hakkında daha fazla bilgi için bkz. [Azure kaynaklarınızı yönetmek için kaynak gruplarını kullanma](../azure-resource-manager/resource-group-overview.md).  
4. **Sürüm** için **V2 (Önizleme)** öğesini seçin.
5. Data factory için **konum** seçin. Listede yalnızca veri fabrikası oluşturma için desteklenen konumlar gösterilir.
6. **Panoya sabitle**’yi seçin.     
7. **Oluştur**’a tıklayın.
8. Panoda şu kutucuğu ve üzerinde şu durumu görürsünüz: **Veri fabrikası dağıtılıyor**. 

    ![veri fabrikası dağıtılıyor kutucuğu](media/tutorial-create-azure-ssis-runtime-portal/deploying-data-factory.png)
9. Oluşturma işlemi tamamlandıktan sonra, resimde gösterildiği gibi **Data Factory** sayfasını görürsünüz.
   
   ![Data factory giriş sayfası](./media/tutorial-create-azure-ssis-runtime-portal/data-factory-home-page.png)
10. Azure Data Factory Kullanıcı Arabirimini (UI) ayrı bir sekmede açmak için **Geliştir ve İzle**’ye tıklayın. 

### <a name="provision-an-azure-ssis-integration-runtime"></a>Azure SSIS tümleştirme çalışma zamanı sağlama

1. Başlarken sayfasında **SSIS Tümleştirme Çalışma Zamanı Yapılandır** kutucuğuna tıklayın. 

   ![SSIS Tümleştirme Çalışma Zamanı Yapılandır kutucuğu](./media/tutorial-create-azure-ssis-runtime-portal/configure-ssis-integration-runtime-tile.png)
2. **Tümleştirme Çalışma Zamanı Kurulumu**’nun **Genel Ayarlar** sayfasında aşağıdaki adımları uygulayın: 

   ![Genel ayarlar](./media/tutorial-create-azure-ssis-runtime-portal/general-settings.png)

    1. Tümleştirme çalışma zamanı için bir **ad** belirtin.
    2. Tümleştirme çalışma zamanının **konumunu** belirtin. Yalnızca desteklenen konumlar görüntülenir.
    3. SSIS çalışma zamanı ile birlikte yapılandırılacak **düğümün boyutunu** seçin.
    4. Kümedeki **düğüm sayısını** belirtin.
    5. **İleri**’ye tıklayın. 
1. **SQL Ayarları** bölümünde aşağıdaki adımları uygulayın: 

    ![SQL ayarları](./media/tutorial-create-azure-ssis-runtime-portal/sql-settings.png)

    1. Azure SQL Server’ı içeren Azure **aboneliğini** belirtin. 
    2. **Katalog Veritabanı Sunucu Uç Noktası** için Azure SQL Server’ınızı seçin.
    3. **Yöneticinin** kullanıcı adını belirtin.
    4. Yöneticinin **parolasını** girin.  
    5. SSISDB veritabanı için **hizmet katmanını** seçin. Varsayılan değer Temel’dir.
    6. **İleri**’ye tıklayın. 
1.  **Gelişmiş Ayarlar** sayfasında **Düğüm Başına En Fazla Paralel Yürütme** için bir değer seçin.   

    ![Gelişmiş ayarlar](./media/tutorial-create-azure-ssis-runtime-portal/advanced-settings.png)    
5. Bu adım **isteğe bağlıdır**. Tümleştirme çalışma zamanının katılmasını istediğiniz klasik bir sanal ağınız (VNet) varsa, **Azure-SSIS tümleştirme çalışma zamanınızın katılması için bir VNet seçin ve Azure hizmetlerinin VNet izinlerini/ayarlarını yapılandırmasına izin verin** seçeneğini belirleyip aşağıdaki adımları uygulayın: 

    ![VNet ile gelişmiş ayarlar](./media/tutorial-create-azure-ssis-runtime-portal/advanced-settings-vnet.png)    

    1. Klasik VNet’i içeren **aboneliği** belirtin. 
    2. **VNet**'i seçin. <br/>
    4. **Alt Ağ**'ı seçin.<br/> 
1. Azure-SSIS tümleştirme çalışma zamanı oluşturma işlemini başlatmak için **Son**’a tıklayın. 

    > [!IMPORTANT]
    > - Bu işlemin tamamlanması yaklaşık 20 dakika sürer
    > - Data Factory hizmeti, SSIS Kataloğu veritabanını (SSISDB) hazırlamak için Azure SQL Veritabanınıza bağlanır. Betik ayrıca belirtilmişse sanal ağınıza ilişkin izin ve ayarları yapılandırır ve yeni Azure SSIS tümleştirme çalışma zamanı örneğini sanal ağa ekler.
7. **Bağlantılar** penceresinde, gerekirse **Tümleştirme Çalışma Zamanları**’na geçin. Durumu yenilemek için **Yenile**’ye tıklayın. 

    ![Oluşturma durumu](./media/tutorial-create-azure-ssis-runtime-portal/azure-ssis-ir-creation-status.png)
8. Tümleştirme çalışma zamanını izlemek, durdurmak/başlatmak, düzenlemek veya silmek için **Eylemler** sütununun altındaki bağlantıları kullanın. Tümleştirme çalışma zamanının JSON kodunu görüntülemek için son bağlantıyı kullanın. Düzenle ve sil düğmeleri yalnızca IR durdurulmuş durumdayken etkin olur. 

    ![Azure SSIS IR - eylemler](./media/tutorial-create-azure-ssis-runtime-portal/azure-ssis-ir-actions.png)        
9. **Eylemler** altında **İzleyici** bağlantısına tıklayın.  

    ![Azure SSIS IR - ayrıntılar](./media/tutorial-create-azure-ssis-runtime-portal/azure-ssis-ir-details.png)
10. Azure SSIS IR ile ilişkili bir **hata** oluşmuşsa bu sayfada hata sayısını ve hatayla ilgili ayrıntıları görüntüleme bağlantısını görürsünüz. Örneğin, veritabanı sunucusunda SSIS Kataloğu zaten mevcutsa SSISDB veritabanının mevcut olduğunu gösteren bir hata görürsünüz.  
11. Veri fabrikasıyla ilişkili tüm tümleştirme çalışma zamanlarını görmek üzere önceki sayfaya dönmek için üstteki **Tümleştirme Çalışma Zamanları**’na tıklayın.  

### <a name="azure-ssis-integration-runtimes-in-the-portal"></a>Portalda Azure SSIS tümleştirmesi çalışma zamanları

1. Veri fabrikanızdaki mevcut tümleştirme çalışma zamanlarını görüntülemek için Azure Data Factory kullanıcı arabiriminde **Düzenle** sekmesine geçin, **Bağlantılar**’a tıklayın ve sonra **Tümleştirme Çalışma Zamanları** sekmesine geçin. 
    ![Mevcut IR’leri görüntüle](./media/tutorial-create-azure-ssis-runtime-portal/view-azure-ssis-integration-runtimes.png)
1. Yeni bir Azure-SSIS IR oluşturmak için **Yeni**'ye tıklayın. 

    ![Menü aracılığıyla tümleştirme çalışma zamanı](./media/tutorial-create-azure-ssis-runtime-portal/edit-connections-new-integration-runtime-button.png)
2. Azure-SSIS tümleştirme çalışma zamanı oluşturmak için resimde gösterildiği gibi **Yeni**’ye tıklayın. 
3. Tümleştirme Çalışma Zamanı Kurulumu penceresinde **Mevcut SSIS paketlerini Azure’da yürütmek üzere lift-and-shift ile taşıma**’yı seçip **İleri**’ye tıklayın.

    ![Tümleştirme çalışma zamanının türünü belirtin](./media/tutorial-create-azure-ssis-runtime-portal/integration-runtime-setup-options.png)
4. Geriye kalan Azure SSIS IR kurulumu adımları için bkz. [Azure SSIS tümleştirme çalışma zamanı sağlama](#provision-an-azure-ssis-integration-runtime).

## <a name="azure-powershell"></a>Azure PowerShell
Bu bölümde, bir Azure SSIS IR oluşturmak için Azure PowerShell kullanma

### <a name="create-variables"></a>Değişken oluşturma
Bu öğreticideki betiklerde kullanılacak değişkenleri tanımlayın:

```powershell
# Azure Data Factory version 2 information 
# If your input contains a PSH special character, e.g. "$", precede it with the escape character "`" like "`$".
$SubscriptionName = "[your Azure subscription name]"
$ResourceGroupName = "[your Azure resource group name]"
$DataFactoryName = "[your data factory name]"
$DataFactoryLocation = "EastUS" 

# Azure-SSIS integration runtime information - This is the Data Factory compute resource for running SSIS packages
$AzureSSISName = "[your Azure-SSIS integration runtime name]"
$AzureSSISDescription = "This is my Azure-SSIS integration runtime"
$AzureSSISLocation = "EastUS" 
# In public preview, only Standard_A4_v2|Standard_A8_v2|Standard_D1_v2|Standard_D2_v2|Standard_D3_v2|Standard_D4_v2 are supported.
$AzureSSISNodeSize = "Standard_D3_v2"
# In public preview, only 1-10 nodes are supported.
$AzureSSISNodeNumber = 2 
# For a Standard_D1_v2 node, 1-4 parallel executions per node are supported. For other nodes, it's 1-8.
$AzureSSISMaxParallelExecutionsPerNode = 2 

# SSISDB info
$SSISDBServerEndpoint = "[your Azure SQL Database server name.database.windows.net or your Azure SQL Managed Instance (private preview) server endpoint]"
$SSISDBServerAdminUserName = "[your server admin username]"
$SSISDBServerAdminPassword = "[your server admin password]"

# Remove the SSISDBPricingTier variable if you are using Azure SQL Managed Instance (private preview)
# This parameter applies only to Azure SQL Database. For the basic pricing tier, specify "Basic", not "B". For standard tiers, specify "S0", "S1", "S2", 'S3", etc.
$SSISDBPricingTier = "[your Azure SQL Database pricing tier. Examples: Basic, S0, S1, S2, S3, etc.]"

## These two parameters apply if you are using a VNet and an Azure SQL Managed Instance (private preview) 
# Specify information about your classic or Azure Resource Manager virtual network (VNet). 
$VnetId = "[your VNet resource ID or leave it empty]" 
$SubnetName = "[your subnet name or leave it empty]" 

```
### <a name="log-in-and-select-subscription"></a>Oturum açma ve abonelik seçme
Oturum açma ve Azure aboneliğinizi seçin komut dosyasını aşağıdaki kodu ekleyin: 

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $SubscriptionName
```

### <a name="validate-the-connection-to-database"></a>Veritabanı bağlantısını doğrulama
Azure SQL veritabanı sunucusu server.database.windows.net veya Azure SQL yönetilen örneği (özel olarak incelenmektedir) sunucusu uç noktası doğrulamak için aşağıdaki betiği ekleyin. 

```powershell
$SSISDBConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $SSISDBConnectionString;
Try
{
    $sqlConnection.Open();
}
Catch [System.Data.SqlClient.SqlException]
{
    Write-Warning "Cannot connect to your Azure SQL DB logical server/Azure SQL MI server, exception: $_"  ;
    Write-Warning "Please make sure the server you specified has already been created. Do you want to proceed? [Y/N]"
    $yn = Read-Host
    if(!($yn -ieq "Y"))
    {
        Return;
    } 
}
```

### <a name="configure-virtual-network"></a>Sanal ağ yapılandırma
Azure-SSIS tümleştirme çalışma zamanının katılacağı sanal ağın izinlerini/ayarlarını otomatik olarak yapılandırmak için aşağıdaki betiği ekleyin.

```powershell
# Register to Azure Batch resource provider
if(![string]::IsNullOrEmpty($VnetId) -and ![string]::IsNullOrEmpty($SubnetName))
{
    $BatchObjectId = (Get-AzureRmADServicePrincipal -ServicePrincipalName "MicrosoftAzureBatch").Id
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
    while(!(Get-AzureRmResourceProvider -ProviderNamespace "Microsoft.Batch").RegistrationState.Contains("Registered"))
    {
    Start-Sleep -s 10
    }
    if($VnetId -match "/providers/Microsoft.ClassicNetwork/")
    {
        # Assign VM contributor role to Microsoft.Batch
        New-AzureRmRoleAssignment -ObjectId $BatchObjectId -RoleDefinitionName "Classic Virtual Machine Contributor" -Scope $VnetId
    }
}
```

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) komutunu kullanarak yeni bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) oluşturun. Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. Aşağıdaki örnek `westeurope` konumunda `myResourceGroup` adlı bir kaynak grubu oluşturur.

```powershell
New-AzureRmResourceGroup -Location $DataFactoryLocation -Name $ResourceGroupName
```

### <a name="create-a-data-factory"></a>Veri fabrikası oluşturma
Veri fabrikası oluşturmak için aşağıdaki komutu çalıştırın:

```powershell
Set-AzureRmDataFactoryV2 -ResourceGroupName $ResourceGroupName `
                         -Location $DataFactoryLocation `
                         -Name $DataFactoryName
```

### <a name="create-an-integration-runtime"></a>Tümleştirme çalışma zamanı oluşturma
SSIS paketleri Azure'da çalışan bir Azure SSIS tümleştirmesi çalışma zamanı oluşturmak için aşağıdaki komutu çalıştırın: veritabanı (Azure SQL veritabanı ile türüne göre bölümünden komut dosyası kullanma Kullanmakta olduğunuz Azure SQL yönetilen örneği (özel olarak incelenmektedir)). 

#### <a name="azure-sql-database-to-host-the-ssisdb-database-ssis-catalog"></a>(SSIS katalog) SSISDB veritabanını barındırmak için Azure SQL veritabanı 

```powershell
$secpasswd = ConvertTo-SecureString $SSISDBServerAdminPassword -AsPlainText -Force
$serverCreds = New-Object System.Management.Automation.PSCredential($SSISDBServerAdminUserName, $secpasswd)
Set-AzureRmDataFactoryV2IntegrationRuntime  -ResourceGroupName $ResourceGroupName `
                                            -DataFactoryName $DataFactoryName `
                                            -Name $AzureSSISName `
                                            -Type Managed `
                                            -CatalogServerEndpoint $SSISDBServerEndpoint `
                                            -CatalogAdminCredential $serverCreds `
                                            -CatalogPricingTier $SSISDBPricingTier `
                                            -Description $AzureSSISDescription `
                                            -Location $AzureSSISLocation `
                                            -NodeSize $AzureSSISNodeSize `
                                            -NodeCount $AzureSSISNodeNumber `
                                            -MaxParallelExecutionsPerNode $AzureSSISMaxParallelExecutionsPerNode
```

VNetId ve alt ağ için değerleri geçirmeniz gerekmez şirket içi veri erişimi gerekmedikçe diğer bir deyişle, şirket içi veri kaynakları/hedefleri SSIS paketlerinizi sahip. CatalogPricingTier parametresi için değer geçmesi gerekir. Azure SQL veritabanı için desteklenen fiyatlandırma katmanlarına listesi için bkz: [SQL veritabanı kaynak sınırları](../sql-database/sql-database-resource-limits.md).

#### <a name="azure-sql-managed-instance-private-preview-to-host-the-ssisdb-database"></a>Azure SQL yönetilen SSISDB veritabanını barındırmak üzere örneği (özel olarak incelenmektedir)

```powershell
$secpasswd = ConvertTo-SecureString $SSISDBServerAdminPassword -AsPlainText -Force
$serverCreds = New-Object System.Management.Automation.PSCredential($SSISDBServerAdminUserName, $secpasswd)
Set-AzureRmDataFactoryV2IntegrationRuntime  -ResourceGroupName $ResourceGroupName `
                                            -DataFactoryName $DataFactoryName `
                                            -Name $AzureSSISName `
                                            -Type Managed `
                                            -CatalogServerEndpoint $SSISDBServerEndpoint `
                                            -CatalogAdminCredential $serverCreds `
                                            -Description $AzureSSISDescription `
                                            -Location $AzureSSISLocation `
                                            -NodeSize $AzureSSISNodeSize `
                                            -NodeCount $AzureSSISNodeNumber `
                                            -MaxParallelExecutionsPerNode $AzureSSISMaxParallelExecutionsPerNode `
                                            -VnetId $VnetId `
                                            -Subnet $SubnetName
```

Azure SQL yönetilen bir VNet katıldığı örneği (özel olarak incelenmektedir) ile VnetId ve alt ağ parametreleri için değerleri geçirmeniz gerekir. CatalogPricingTier parametresi yönetilen Azure SQL örneği için geçerli değildir. 

### <a name="start-integration-runtime"></a>Tümleştirme çalışma zamanını başlatma
Azure-SSIS tümleştirme çalışma zamanını başlatmak için aşağıdaki komutu çalıştırın: 

```powershell
write-host("##### Starting #####")
Start-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                             -DataFactoryName $DataFactoryName `
                                             -Name $AzureSSISName `
                                             -Force

write-host("##### Completed #####")
write-host("If any cmdlet is unsuccessful, please consider using -Debug option for diagnostics.")                                  
```
Bu komutun tamamlanması **20-30 dakika** sürer. 


### <a name="full-script"></a>Tam betik
Burada, Azure SSIS IR oluşturan ve bir sanal ağa katılırsa tam komut verilmiştir. Bu komut dosyası SSIS katalog barındırmak için Azure SQL yönetilen örneği (mı) kullandığınızı varsayar. 

```powershell
# Azure Data Factory version 2 information 
# If your input contains a PSH special character, e.g. "$", precede it with the escape character "`" like "`$". 
$SubscriptionName = "<Azure subscription name>"
$ResourceGroupName = "<Azure resource group name>"
# Data factory name. Must be globally unique
$DataFactoryName = "<Data factory name>" 
$DataFactoryLocation = "EastUS" 

# Azure-SSIS integration runtime information. This is a Data Factory compute resource for running SSIS packages
$AzureSSISName = "<Specify a name for your Azure-SSIS (IR)>"
$AzureSSISDescription = "<Specify description for your Azure-SSIS IR"
$AzureSSISLocation = "EastUS" 
 # In public preview, only Standard_A4_v2, Standard_A8_v2, Standard_D1_v2, Standard_D2_v2, Standard_D3_v2, Standard_D4_v2 are supported
$AzureSSISNodeSize = "Standard_D3_v2"
# In public preview, only 1-10 nodes are supported.
$AzureSSISNodeNumber = 2 
# For a Standard_D1_v2 node, 1-4 parallel executions per node are supported. For other nodes, it's 1-8.
$AzureSSISMaxParallelExecutionsPerNode = 2 

# SSISDB info
$SSISDBServerEndpoint = "<Azure SQL server name>.database.windows.net"
$SSISDBServerAdminUserName = "<Azure SQL server - user name>"
$SSISDBServerAdminPassword = "<Azure SQL server - user password>"
# Remove the SSISDBPricingTier variable if you are using Azure SQL Managed Instance (private preview)
# This parameter applies only to Azure SQL Database. For the basic pricing tier, specify "Basic", not "B". For standard tiers, specify "S0", "S1", "S2", 'S3", etc.
$SSISDBPricingTier = "<pricing tier of your Azure SQL server. Examples: Basic, S0, S1, S2, S3, etc.>" 

$SSISDBConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $SSISDBConnectionString;
Try
{
    $sqlConnection.Open();
}
Catch [System.Data.SqlClient.SqlException]
{
    Write-Warning "Cannot connect to your Azure SQL DB logical server/Azure SQL MI server, exception: $_"  ;
    Write-Warning "Please make sure the server you specified has already been created. Do you want to proceed? [Y/N]"
    $yn = Read-Host
    if(!($yn -ieq "Y"))
    {
        Return;
    } 
}

Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

Set-AzureRmDataFactoryV2 -ResourceGroupName $ResourceGroupName `
                        -Location $DataFactoryLocation `
                        -Name $DataFactoryName

$secpasswd = ConvertTo-SecureString $SSISDBServerAdminPassword -AsPlainText -Force
$serverCreds = New-Object System.Management.Automation.PSCredential($SSISDBServerAdminUserName, $secpasswd)
Set-AzureRmDataFactoryV2IntegrationRuntime  -ResourceGroupName $ResourceGroupName `
                                            -DataFactoryName $DataFactoryName `
                                            -Name $AzureSSISName `
                                            -Type Managed `
                                            -CatalogServerEndpoint $SSISDBServerEndpoint `
                                            -CatalogAdminCredential $serverCreds `
                                            -CatalogPricingTier $SSISDBPricingTier `
                                            -Description $AzureSSISDescription `
                                            -Location $AzureSSISLocation `
                                            -NodeSize $AzureSSISNodeSize `
                                            -NodeCount $AzureSSISNodeNumber `
                                            -MaxParallelExecutionsPerNode $AzureSSISMaxParallelExecutionsPerNode

write-host("##### Starting your Azure-SSIS integration runtime. This command takes 20 to 30 minutes to complete. #####")
Start-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                             -DataFactoryName $DataFactoryName `
                                             -Name $AzureSSISName `
                                             -Force

write-host("##### Completed #####")
write-host("If any cmdlet is unsuccessful, please consider using -Debug option for diagnostics.")
```

## <a name="azure-resource-manager-template"></a>Azure Resource Manager şablonu
Bu bölümde, bir Azure SSIS tümleştirmesi çalışma zamanı oluşturmak için bir Azure Resource Manager şablonunu kullanın. Bir örnek kılavuz şöyledir: 

1. Aşağıdaki Resource Manager şablonu ile bir JSON dosyası oluşturun. Açılı ayraç (yer tutucu) değerleri kendi değerlerinizle değiştirin. 

    ```json
    {
        "contentVersion": "1.0.0.0",
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "parameters": {},
        "variables": {},
        "resources": [{
            "name": "<Specify a name for your data factory>",
            "apiVersion": "2017-09-01-preview",
            "type": "Microsoft.DataFactory/factories",
            "location": "East US",
            "properties": {},
            "resources": [{
                "type": "integrationruntimes",
                "name": "<Specify a name for the Azure SSIS IR>",
                "dependsOn": [ "<The name of the data factory you specified at the beginning>" ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "Managed",
                    "typeProperties": {
                        "computeProperties": {
                            "location": "East US",
                            "nodeSize": "Standard_D1_v2",
                            "numberOfNodes": 1,
                            "maxParallelExecutionsPerNode": 1
                        },
                        "ssisProperties": {
                            "catalogInfo": {
                                "catalogServerEndpoint": "<Azure SQL server>.database.windows.net",
                                "catalogAdminUserName": "<Azure SQL user",
                                "catalogAdminPassword": {
                                    "type": "SecureString",
                                    "value": "<Azure SQL Password>"
                                },
                                "catalogPricingTier": "Basic"
                            }
                        }
                    }
                }
            }]
        }]
    }
    ```
2. Resource Manager şablonu dağıtmak için aşağıdaki exmaple gösterildiği gibi New-AzureRmResourceGroupDeployment komutunu çalıştırın. Bu örnekte, ADFTutorialResourceGroup kaynak grubunun adıdır. C:\adfgetstarted data factory ve Azure SSIS IR için JSON tanımını içeren bir dosyadır 

    ```powershell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json
    ```

    Bu komut, veri fabrikası oluşturur ve bir Azure SSIS IR oluşturur, ancak IR başlamıyor 
3. Azure SSIS IR başlatmak için başlangıç AzureRmDataFactoryV2IntegrationRuntime komutu çalıştırın: 

    ```powershell
    Start-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName "<Resource Group Name> `
                                             -DataFactoryName <Data Factory Name> `
                                             -Name <Azure SSIS IR Name> `
                                             -Force
    ``` 

## <a name="deploy-ssis-packages"></a>SSIS paketlerini dağıtma
Şimdi SQL Server Veri Araçları (SSDT) veya SQL Server Management Studio’yu (SSMS) kullanarak SSIS paketlerinizi Azure’a dağıtın. SSIS kataloğunu (SSISDB) barındıran Azure SQL sunucunuza bağlanın. Azure SQL sunucusunun adı şu biçimdedir: &lt;servername&gt;. database.windows.net (Azure SQL veritabanı için). Yönergeler için [Paket dağıtma](/sql/integration-services/packages/deploy-integration-services-ssis-projects-and-packages#deploy-packages-to-integration-services-server) makalesine bakın. 

## <a name="next-steps"></a>Sonraki adımlar
Bu belge diğer Azure SSIS IR konulara bakın:

- [Azure SSIS tümleştirmesi çalışma zamanı](concepts-integration-runtime.md#azure-ssis-integration-runtime). Bu makalede Azure SSIS IR genel dahil tümleştirme çalışma zamanları hakkında kavramsal bilgiler sağlar 
- [Öğretici: SSIS paketlerini Azure’a dağıtma](tutorial-deploy-ssis-packages-azure.md). Bu makale bir Azure-SSIS IR oluşturmaya ilişkin adım adım yönergeler sağlar ve SSIS kataloğunu barındırmak için bir Azure SQL veritabanı kullanır. 
- [Azure-SSIS IR’yi izleme](monitor-integration-runtime.md#azure-ssis-integration-runtime). Bu makalede bir Azure-SSIS IR ile ilgili bilgileri ve döndürülen bilgilerdeki durumların açıklamalarını alma işlemi gösterilmektedir. 
- [Azure-SSIS IR’yi yönetme](manage-azure-ssis-integration-runtime.md). Bu makale bir Azure-SSIS IR’yi durdurma, başlatma veya kaldırma işlemini gösterir. Ayrıca, IR’ye daha fazla düğüm ekleyerek Azure-SSIS IR’nizi ölçeklendirmeyi gösterir. 
- [Azure-SSIS IR’yi bir sanal ağa ekleme](join-azure-ssis-integration-runtime-virtual-network.md). Bu makale Azure-SSIS IR’yi bir Azure sanal ağına (VNet) ekleme hakkında kavramsal bilgiler sağlar. Ayrıca, Azure portalını kullanarak Azure-SSIS IR’nin sanal ağa katılmasını sağlayacak şekilde sanal ağı yapılandırma adımları sunar. 