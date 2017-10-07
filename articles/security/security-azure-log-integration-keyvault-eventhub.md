---
title: "Olay hub'ları kullanarak Azure anahtar kasası günlükleri aaaIntegrate | Microsoft Docs"
description: "Merhaba gerekli adımları toomake anahtar kasası sağlar Öğreticisi, Azure günlük tümleştirmeyi kullanarak kullanılabilir tooa SIEM günlüğe kaydeder"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a>Azure günlük tümleştirme Öğreticisi: olay hub'ları kullanarak işlem Azure anahtar kasası olayları

Azure günlük tümleştirme oturum tooretrieve olayları kullanın ve bunları kullanılabilir tooyour güvenlik bilgileri ve Olay yönetimi (SIEM) sistemi sağlayın. Bu öğreticide Azure günlük tümleştirme aracılığıyla Azure Event Hubs alınan kullanılan tooprocess günlüklerini nasıl olabilir bir örnek gösterilmiştir.
 
Bu öğretici tooget nasıl birlikte izleyerek Azure günlük tümleştirme ve Event Hubs iş hello ile örnek adımlar TechNet'in ve her adımın hello çözümü nasıl destekler? anlama kullanın. Neler yapabileceğiniz sonra kendi adımları toosupport toocreate burada öğrendiniz, şirketinizin benzersiz gereksinimleri.

>[!WARNING]
Merhaba adımları ve Bu öğreticide komutları kopyalanır ve yapıştırılan hedeflenen toobe değildir. Bunlar yalnızca örnek demektir. "Olduğu gibi" Merhaba PowerShell komutlarını Canlı ortamınızda kullanmayın. Bunları benzersiz ortamınıza bağlı özelleştirmeniz gerekir.


Bu öğreticide, Azure anahtar kasası etkinlik oturum tooan olay hub'ı almak ve JSON dosyaları tooyour SIEM sistem olarak kullanılabilir hale getirme hello işlemi açıklanmaktadır. Ardından, SIEM sistem tooprocess hello JSON dosyalarınızın yapılandırabilirsiniz.

>[!NOTE]
>Bu öğreticideki adımlardan hello çoğu anahtar kasalarını, depolama hesapları ve olay hub'ları yapılandırma içerir. Merhaba belirli Azure günlük tümleştirme hello Bu öğreticinin sonunda adımlardır. Bu adımları bir üretim ortamında gerçekleştirmeyin. Bunlar yalnızca bir laboratuvar ortamı için tasarlanmıştır. Üretimde kullanmadan önce hello adımları özelleştirmeniz gerekir.

Her adım hello nedenler anlamak hello şekilde yardımcı olur bilgiler sağlanmıştır. Bağlantılar tooother makaleleri belirli konular hakkında daha fazla ayrıntı sağlayacaktır.

Bu öğretici değinmektedir hello hizmetleri hakkında daha fazla bilgi için bkz: 

- [Azure Anahtar Kasası.](../key-vault/key-vault-whatis.md)
- [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Azure günlük tümleştirme](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a>İlk kurulumu

Bu makalede hello adımları tamamlayabilmeniz için önce hello aşağıdaki gerekir:

1. Bir Azure aboneliği ve hesabı bu abonelikte yönetici haklarına sahip. Bir aboneliğiniz yoksa oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/).
 
2. Erişim toohello sistemiyle Azure günlük tümleştirme yüklemek için hello gereksinimleri karşılayan Internet. Merhaba sistem veya şirket içinde barındırılan bir bulut hizmetinde olabilir.

3. [Azure günlük tümleştirme](https://www.microsoft.com/download/details.aspx?id=53324) yüklü. tooinstall onu:

   a. 2. adımda bahsedilen Uzak Masaüstü tooconnect toohello sistemi kullanın.   
   b. Hello Azure günlük tümleştirme yükleyici toohello sistem kopyalayın. Yapabilecekleriniz [hello yükleme dosyalarını indirmek](https://www.microsoft.com/download/details.aspx?id=53324).   
   c. Merhaba Yükleyicisi'ni başlatın ve hello Microsoft Yazılımı Lisans koşulları kabul edin.   
   d. Telemetri bilgileri sağlayacaksa hello onay kutusunu seçili bırakın. Bunun yerine kullanım bilgileri tooMicrosoft göndermek hello onay kutusunu temizleyin.
   
   Azure günlük tümleştirmesi hakkında daha fazla bilgi için ve nasıl tooinstall, bkz: [Azure tanılama günlüğünü ve Windows Olay iletme Azure günlük tümleştirme](security-azure-log-integration-get-started.md).

4. Merhaba son PowerShell sürümü.
 
   Windows Server 2016 sahip sonra en az PowerShell 5.0. Herhangi bir Windows Server sürümünü kullanıyorsanız, PowerShell yüklü önceki bir sürümü olabilir. Girerek hello sürüm denetleyebilirsiniz ```get-host``` bir PowerShell penceresinde. PowerShell 5.0 yüklü yoksa, şunları yapabilirsiniz [karşıdan](https://www.microsoft.com/download/details.aspx?id=50395).

   En az sonra PowerShell 5. 0'da, tooinstall hello en son sürümünü devam edebilirsiniz:
   
   a. Bir PowerShell penceresinde hello girin ```Install-Module Azure``` komutu. Merhaba yükleme adımlarını tamamlayın.    
   b. Merhaba girin ```Install-Module AzureRM``` komutu. Merhaba yükleme adımlarını tamamlayın.

   Daha fazla bilgi için bkz: [Azure PowerShell yükleme](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).


## <a name="create-supporting-infrastructure-elements"></a>Destekleyen altyapı öğeleri oluşturma

1. Yükseltilmiş bir PowerShell penceresi açın ve çok**C:\Program Files\Microsoft Azure günlük tümleştirme**.
2. Merhaba AzLog cmdlet'leri hello betik LoadAzLogModule.ps1 çalıştırarak içeri aktarın. Merhaba girin `.\LoadAzLogModule.ps1` komutu. (Bildirim hello ". \" Bu komutta.) Şuna benzer bir şey görmeniz gerekir:</br>

   ![Yüklenen modüller listesi](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. Merhaba girin `Login-AzureRmAccount` komutu. Merhaba oturum açma penceresinde hello Bu öğretici için kullanacağınız hello abonelik için kimlik bilgilerini girin.

   >[!NOTE]
   >Bu hello tooAzure bu makineden oturum açtığınızdan ilk kez ise, Microsoft toocollect PowerShell kullanım verilerini izin verme hakkında bir ileti görürsünüz. Kullanılan tooimprove Azure PowerShell olacağından, bu veri toplama etkinleştirmenizi öneririz.

4. Başarılı bir kimlik doğrulamasından sonra oturum açtınız ve ekran aşağıdaki hello hello bilgilerine bakın. Merhaba abonelik kimliği ve abonelik adını not edin, bunları gerekir çünkü toocomplete sonraki adımlar.

   ![PowerShell penceresi](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. Değişkenleri daha sonra kullanılacak toostore değerleri oluşturun. Her PowerShell satırlardan hello girin. Ortamınızı tooadjust hello değerleri toomatch gerekebilir.
    - ```$subscriptionName = ‘Visual Studio Ultimate with MSDN’```(Abonelik adınızı farklı olabilir. Merhaba hello önceki komutunun çıktısını bir parçası olarak görebileceğiniz.)
    - ```$location = 'West US'```(Bu değişken, kaynaklar nerede oluşturulacağını kullanılan toopass hello konum olacaktır. "Bu değişken toobe seçtiğiniz herhangi bir konuma değiştirebilirsiniz.)
    - ```$random = Get-Random```
    - ``` $name = 'azlogtest' + $random```(Merhaba adı herhangi bir şey olabilir, ancak yalnızca küçük harf ve sayı içermelidir.)
    - ``` $storageName = $name```(Bu değişken hello depolama hesabı adı için kullanılır.)
    - ```$rgname = $name ```(Bu değişken hello kaynak grubu adı için kullanılır.)
    - ``` $eventHubNameSpaceName = $name```(Bu hello hello olay hub'ı ad alanının adıdır.)
6. İle çalışacaksınız hello abonelik belirtin:
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. Kaynak grubu oluşturun:
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   Girerseniz `$rg` bu noktada, çıktı benzer toothis ekran görmeniz gerekir:

   ![Çıktıdan sonra kaynak grubu oluşturma](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. Durum bilgilerini kullanılan tookeep izini olacak bir depolama hesabı oluşturun:
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. Merhaba olay hub'ad alanı oluşturun. Gerekli toocreate bir event hub budur.
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. Merhaba Öngörüler sağlayıcı ile kullanılacak hello kural kimliği alın:
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. Tüm olası Azure konumlarını almak ve daha sonraki bir adımda kullanılabilir hello adları tooa değişkeni ekleyin:
    
    a. ```$locationObjects = Get-AzureRMLocation```    
    b. ```$locations = @('global') + $locationobjects.location```
    
    Girerseniz `$locations` bu noktada, Get-AzureRmLocation tarafından döndürülen hello ek bilgileri olmadan hello konum adları görürsünüz.
12. Bir Azure Resource Manager günlük profili oluşturun: 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    Hello Azure günlük profili hakkında daha fazla bilgi için bkz: [hello Azure etkinlik günlüğü'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

> [!NOTE]
> Toocreate günlük profili çalıştığınızda bir hata iletisi alabilirsiniz. Get-AzureRmLogProfile ve Kaldır-AzureRmLogProfile hello belgelerine daha sonra gözden geçirebilirsiniz. Get-AzureRmLogProfile çalıştırırsanız, hello günlük profili hakkındaki bilgileri görebilirsiniz. Merhaba girerek hello profil günlük silebilirsiniz ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` komutu.
>
>![Resource Manager profili hatası](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a>Bir anahtar kasası oluşturma

1. Merhaba anahtar kasası oluşturun:

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. Merhaba anahtar kasası için günlüğe kaydetmeyi yapılandırın:

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a>Günlük etkinliği oluştur

İstekleri tooKey kasa toogenerate günlük etkinliği gönderilen toobe gerekir. Eylemler anahtar oluşturma, gizli saklamak ister veya gizli anahtar Kasası'nı okuma günlük girişi oluşturur.

1. Merhaba geçerli depolama anahtarlarını görüntüle:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. Yeni bir **key2**:
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. Merhaba anahtarlarını görüntülemek yeniden ve, görmek **key2** farklı bir değer içerir:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. Ayarlama ve ek günlük girişlerini gizli toogenerate okuyun:
    
   a. ```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b. ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Gizli döndürdü](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a>Azure günlük tümleştirmesini yapılandırma

Tüm hello gerekli öğeler toohave anahtar kasası günlüğü tooan olay hub'ı yapılandırdınız, tooconfigure Azure günlük tümleştirme gerekir:

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

Her olay hub'ına yönelik Hello AzLog komutu çalıştırın:

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

Bir dakika veya bunu hello son iki komutlarını çalıştırarak, sonra oluşturulan JSON dosyaları görmeniz gerekir. Hello dizin izleyerek onaylayın **C:\users\AzLog\EventHubJson**.

## <a name="next-steps"></a>Sonraki adımlar

- [Azure günlük tümleştirme hakkında SSS](security-azure-log-integration-faq.md)
- [Azure günlük tümleştirme ile çalışmaya başlama](security-azure-log-integration-get-started.md)
- [Azure kaynaklarını günlüklerinden SIEM sistemlerinizi tümleştirme](security-azure-log-integration-overview.md)
