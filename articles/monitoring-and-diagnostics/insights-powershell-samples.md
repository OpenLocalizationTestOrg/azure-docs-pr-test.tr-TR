---
title: "aaaAzure İzleyici PowerShell hızlı başlangıç örnekleri. | Microsoft Belgeleri"
description: "PowerShell tooaccess otomatik ölçeklendirme, uyarılar, Web kancalarını ve etkinlik günlükleri arama gibi Azure İzleyicisi özellikleri kullanın."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a>Azure İzleyici PowerShell hızlı başlangıç örnekleri
Bu makale Azure İzleyicisi özelliklerine erişim PowerShell komutları toohelp örnek gösterir. Azure İzleyici tooAutoScale bulut Hizmetleri, sanal makineler ve Web uygulamaları ve toosend Uyarı bildirimlerinin veya yapılandırılmış telemetri verilerini değerlerine göre çağrısı web URL'leri sağlar.

> [!NOTE]
> Azure İzleyicisi "Azure Öngörüler" olarak adlandırılmıştı için hello yeni 25 Eylül 2016'ya kadar adıdır. Bununla birlikte, hello ad alanları ve bu nedenle hala komutları aşağıdaki hello hello "ınsights" içerir.
> 
> 

## <a name="set-up-powershell"></a>PowerShell ayarlayın
Henüz yapmadıysanız, bilgisayarınızda PowerShell toorun ayarlayın. Daha fazla bilgi için bkz: [nasıl tooInstall ve yapılandırma PowerShell](/powershell/azure/overview).

## <a name="examples-in-this-article"></a>Bu makaledeki örnekler
Merhaba örnekler hello makalede Azure İzleyici cmdlet'lerini nasıl kullanabileceğinizi gösterir. Merhaba tüm Azure İzleyici PowerShell cmdlet'leri listesini gözden geçirebilirsiniz [Azure İzleyicisi'ni (Öngörüler) cmdlet'leri](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).

## <a name="sign-in-and-use-subscriptions"></a>Oturum açma ve abonelikleri kullanın
İlk olarak, tooyour Azure aboneliği oturum açın.

```PowerShell
Login-AzureRmAccount
```

Bu, toosign gerektirir. Hesabınızı yaptıktan sonra Tenantıd ve varsayılan abonelik kimliği görüntülenir. Tüm Azure cmdlet'lerini iş varsayılan aboneliğinizin hello bağlamında hello. tooview hello Aboneliklerin listesini erişebilirsiniz, komutu aşağıdaki hello kullanın.

```PowerShell
Get-AzureRmSubscription
```

toochange çalışma bağlam tooa farklı aboneliğiniz, komutu aşağıdaki kullanım hello.

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a>Bir abonelik için etkinlik günlüğü Al
Kullanım hello `Get-AzureRmLog` cmdlet'i.  Merhaba, ortak bazı örnekler verilmiştir.

Günlük girişlerini bu saat/tarih toopresent alın:

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

Günlük girdilerini arasında bir saat/tarih aralığı alın:

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Günlük girişlerini belirli kaynak grubundan alın:

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

Bir saat/tarih aralığı arasında belirli bir kaynak Sağlayıcısı'ndan günlük girişlerini alın:

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Tüm günlük girişleri belirli çağıran ile alın:

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

Son 1000 hello etkinlik günlüğü olaylarını alır hello komutu aşağıdaki hello:

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

`Get-AzureRmLog`pek çok parametrelerden destekler. Merhaba bkz `Get-AzureRmLog` daha fazla bilgi için başvuru.

> [!NOTE]
> `Get-AzureRmLog`yalnızca 15 gün geçmişi sağlar. Hello kullanarak **- MaxEvents** parametresi, tooquery hello son N olayları, 15 gün ötesinde verir. 15 günden eski tooaccess olayları hello REST API veya SDK'sı (Merhaba SDK kullanarak C# örnek) kullanın. Dahil etmezseniz **StartTime**, hello varsayılan değer ise **EndTime** bir saat eksi. Dahil etmezseniz **EndTime**, geçerli saati hello varsayılan değeri olur. Tüm saatler UTC biçimindedir.
> 
> 

## <a name="retrieve-alerts-history"></a>Uyarı geçmişini alma
tüm olayları Sorgulayabileceğiniz uyarı tooview örnek hello kullanarak Azure Resource Manager günlüklerini hello.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

tooview hello geçmişi için özel bir uyarı kuralı, hello kullanabileceğiniz `Get-AzureRmAlertHistory` cmdlet, hello uyarı kuralının kaynak Kimliğine hello geçirme.

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

Merhaba `Get-AzureRmAlertHistory` cmdlet çeşitli parametreleri destekler. Daha fazla bilgi için bkz: [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).

## <a name="retrieve-information-on-alert-rules"></a>Uyarı kuralları hakkında bilgi alma
Tüm komutları aşağıdaki hello "montest" adlı bir kaynak grubu üzerinde davranır.

Merhaba uyarı kuralı tüm hello özelliklerini görüntüleyin:

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

Bir kaynak grubu üzerinde tüm uyarıları Al:

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

Tüm uyarı kuralı için bir hedef kaynak kümesini alır. Örneğin, bir VM üzerinde tüm uyarı kurallarını ayarlayın.

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

`Get-AzureRmAlertRule`diğer parametreleri destekler. Bkz: [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) daha fazla bilgi için.

## <a name="create-metric-alerts"></a>Ölçüm uyarı oluşturma
Merhaba kullanabilirsiniz `Add-AlertRule` cmdlet toocreate güncelleştirmek veya bir uyarı kuralı devre dışı bırakın.

Kullanarak e-posta ve Web kancası özellikleri oluşturabilirsiniz `New-AzureRmAlertRuleEmail` ve `New-AzureRmAlertRuleWebhook`sırasıyla. Merhaba uyarı kuralı cmdlet'te, bu eylemleri toohello olarak atamak **Eylemler** hello uyarı kuralı özelliği.

Aşağıdaki tablonun hello hello parametreleri açıklar ve bir ölçüm kullanarak bir uyarı kullanılan toocreate değerleri.

| Parametre | değer |
| --- | --- |
| Ad |simpletestdiskwrite |
| Bu uyarı kuralı konumu |Doğu ABD |
| ResourceGroup |montest |
| Uç noktası Targetresourceıd |/Subscriptions/S1/resourceGroups/montest/providers/Microsoft.COMPUTE/virtualMachines/testconfig |
| Oluşturulan hello uyarının MetricName |\PhysicalDisk (_Total) \Disk Yazma/sn. Merhaba bkz `Get-MetricDefinitions` cmdlet'inin nasıl tooretrieve hello tam ölçüm adlar hakkında |
| işleci |GreaterThan |
| Eşik değeri (sayısı/sn olarak bu ölçüm için) |1 |
| Pencereboyutu (ss: dd: biçimi) |00:05:00 |
| Toplayıcı (ortalama sayısı, bu durumda kullanır hello ölçüsünün istatistiği) |Ortalama |
| özel e-postalar (dize dizisi) |'foo@example.com','bar@example.com' |
| e-posta tooowners, Katkıda Bulunanlar ve okuyucular Gönder |-SendToServiceOwners |

Bir e-posta eylem oluşturun

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

Bir Web kancası eylem oluşturun

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

Merhaba CPU % ölçüm klasik bir VM'de Hello uyarı kuralı oluşturma

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

Merhaba uyarı kuralını Al

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

bir uyarı kuralı özellikleri verilen Merhaba zaten varsa hello Ekle uyarı cmdlet ayrıca hello kuralını güncelleştirir. toodisable bir uyarı kuralı dahil hello parametresi **- DisableRule**.

## <a name="get-a-list-of-available-metrics-for-alerts"></a>Uyarılar için kullanılabilir ölçümler listesini al
Merhaba kullanabilirsiniz `Get-AzureRmMetricDefinition` cmdlet tooview hello belirli bir kaynak için tüm ölçümleri listesi.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

Merhaba aşağıdaki örnek hello ölçüm adı ile tablo ve onun için birim hello oluşturur.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Tam listesi için kullanılabilir seçenekleri `Get-AzureRmMetricDefinition` şu adresten edinilebilir [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).

## <a name="create-and-manage-autoscale-settings"></a>Otomatik ölçeklendirme ayarlarını oluşturun ve yönetin
VM, bulut hizmet veya sanal makine ölçek kümesi, bir Web uygulaması gibi bir kaynak için yapılandırılmış tek otomatik ölçeklendirme ayarı olabilir.
Bununla birlikte, her otomatik ölçeklendirme ayarında birden çok profil olabilir. Örneğin, bir performans tabanlı ölçek profili ve ikinci bir zamanlama tabanlı profil için. Her profil yapılandırılmış birden çok kural bulunabilir. Otomatik ölçeklendirme hakkında daha fazla bilgi için bkz: [nasıl tooAutoscale uygulama](../cloud-services/cloud-services-how-to-scale.md).

Kullanacağız hello adımlar şunlardır:

1. Kuralları oluşturun.
2. Profil oluşturma eşleme hello kuralları toohello profilleri daha önce oluşturduğunuz.
3. İsteğe bağlı: Web kancası ve e-posta özellikleri yapılandırarak otomatik ölçeklendirme bildirimleri oluşturun.
4. Hello profilleri ve hello önceki adımlarda oluşturduğunuz bildirimler eşleyerek hello hedef kaynak üzerindeki bir ada sahip bir otomatik ölçeklendirme ayarı oluşturun.

Merhaba Aşağıdaki örnekler, bir sanal makine ölçek kümesi'hello CPU kullanımı ölçümü kullanarak temel Windows işletim sistemi için otomatik ölçeklendirme ayarının nasıl oluşturabileceğinizi gösterir.

İlk olarak, bir kural tooscale genişletme, örnek sayısı artışı ile oluşturun.

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

Ardından, bir kural tooscale içinde bir örnek sayısı azaltma ile oluşturun.

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

Ardından, hello kuralları için bir profil oluşturun.

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

Bir Web kancası özellik oluşturun.

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

E-posta dahil olmak üzere hello otomatik ölçeklendirme ayarının Hello bildirim özelliği oluşturabilir ve daha önce oluşturduğunuz Web kancası hello.

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

Son olarak, yukarıda oluşturduğunuz hello otomatik ölçeklendirme ayarı tooadd hello profili oluşturun.

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

Otomatik ölçeklendirme ayarlarını yönetme hakkında daha fazla bilgi için bkz: [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).

## <a name="autoscale-history"></a>Otomatik ölçeklendirme geçmişi
Merhaba aşağıdaki örnekte, son otomatik ölçeklendirme ve uyarı olayları nasıl görüntüleyebileceğiniz gösterir. Merhaba etkinlik günlüğü arama tooview hello otomatik ölçeklendirme geçmişini kullanın.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

Merhaba kullanabilirsiniz `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve otomatik ölçeklendirme geçmişi.

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

Daha fazla bilgi için bkz: [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).

### <a name="view-details-for-an-autoscale-setting"></a>Otomatik ölçeklendirme ayarı için ayrıntıları görüntüle
Merhaba kullanabilirsiniz `Get-Autoscalesetting` cmdlet tooretrieve hello otomatik ölçeklendirme ayarı hakkında daha fazla bilgi.

Merhaba aşağıdaki örnekte tüm otomatik ölçeklendirme ayarları hakkında ayrıntılı hello kaynak grubu 'myrg1' gösterilmektedir.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

Merhaba aşağıdaki örnekte tüm otomatik ölçeklendirme ayarları hakkında ayrıntılı hello kaynak grubu 'myrg1' gösterir ve özellikle 'MyScaleVMSSSetting' adlı otomatik ölçeklendirme ayarı hello.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a>Otomatik ölçeklendirme ayarı kaldırın
Merhaba kullanabilirsiniz `Remove-Autoscalesetting` cmdlet toodelete bir otomatik ölçeklendirme ayarı.

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a>Etkinlik günlüğü için günlük profilleri Yönet
Oluşturabileceğiniz bir *oturum profili* ve etkinlik günlüğü tooa depolama hesabınız ve verileri dışa veri saklama için yapılandırabilirsiniz. İsteğe bağlı olarak, hello veri tooyour olay hub'ı akışını sağlayabilirsiniz. Bu özellik şu anda Önizleme ve, olduğuna dikkat edin, yalnızca abonelik başına bir günlük profili oluşturabilirsiniz. Geçerli abonelik toocreate cmdlet'leriyle aşağıdaki hello kullanın ve günlük profillerini yönetin. Belirli bir abonelik de seçebilirsiniz. PowerShell toohello geçerli abonelik Varsayılanları olsalar bile, her zaman bu kullanarak değiştirebilirsiniz `Set-AzureRmContext`. Bu aboneliğin etkinlik günlüğü tooroute veri tooany depolama hesabı veya olay hub'ı yapılandırabilirsiniz. Veriler JSON biçiminde blob dosyaları olarak yazılır.

### <a name="get-a-log-profile"></a>Günlük profilini Al
toofetch mevcut günlük profillerinizi kullanmak hello `Get-AzureRmLogProfile` cmdlet'i.

### <a name="add-a-log-profile-without-data-retention"></a>Veri saklama olmayan günlük profili Ekle
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Günlük profilini Kaldır
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a>Veri saklama günlük profiliyle ekleme
Merhaba belirtebilirsiniz **- RetentionInDays** hello verileri nerede tutulur, pozitif bir tamsayı olarak gün hello sayısı özelliği.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a>Günlük profiliyle saklama ve EventHub ekleyin
Toplama toorouting veri toostorage hesabınızı, ayrıca, sağlanabilir tooan olay hub'ı. Bu önizleme sürümü ve hello depolama hesabı yapılandırması zorunludur ancak olay hub'ı yapılandırma isteğe bağlı olduğunu unutmayın.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a>Tanılama günlüklerini yapılandırma
Çoğu Azure hizmeti ek günlükleri ve yapılandırılmış toosave veriler Azure depolama hesabınızdaki olabilir telemetri Gönder tooEvent hub sağlamak ve/veya tooan OMS günlük analizi çalışma alanı gönderilir. Bu işlem yalnızca bir kaynak düzeyinde gerçekleştirilebilir ve hello depolama hesabı veya olay hub'hello mevcut hello tanılama ayarını yapılandırdığınız yerde aynı bölgede hello hedef kaynak olarak.

### <a name="get-diagnostic-setting"></a>Tanılama ayarını alma
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

Tanılama ayarını devre dışı bırak

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

Bekletme olmadan tanılama ayarını etkinleştirin

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

Bekletme olan tanılama ayarını etkinleştirin

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Bekletme belirli günlük kategori için tanılama ayarıyla etkinleştir

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Olay hub'ları için tanılama ayarını etkinleştirin

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

OMS tanılama ayarını etkinleştirin

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
