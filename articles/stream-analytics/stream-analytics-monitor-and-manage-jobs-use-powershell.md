---
title: "aaaMonitor ve akış analizi işleri PowerShell ile yönetme | Microsoft Docs"
description: "Bilgi nasıl toouse Azure PowerShell ve cmdlet'leri toomonitor ve akış analizi işleri yönetin."
keywords: "Azure powershell, azure powershell cmdlet'leri, powershell komutu, powershell komut dosyası"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a>İzleme ve akış analizi işleri Azure PowerShell cmdlet'leri ile yönetme
Bilgi nasıl toomonitor ve Azure PowerShell cmdlet'leri ve powershell komut dosyası ile temel akış analizi görevleri yürütün akış analizi kaynaklarını yönetme.

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a>Akış analizi için Azure PowerShell cmdlet'lerini çalıştırmak için Önkoşullar
* Aboneliğinizde Azure kaynak grubu oluşturun. Merhaba, örnek bir Azure PowerShell komut dosyası aşağıdadır. Azure PowerShell bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview);  

Azure PowerShell 0.9.8:  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

Azure PowerShell 1.0:  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> Program aracılığıyla oluşturulan stream Analytics işlerini izleme varsayılan olarak etkin gerekmez.  Hello Azure Portal'ı toohello işin izleme sayfası gezinme tarafından izleme el ile etkinleştirebilir ve hello Etkinleştir düğmesini veya tıklatarak yapabilirsiniz konumunda bulunan hello adımları izleyerek program aracılığıyla [Azure akış analizi - İzleyici akış Analytics işleri programlı şekilde](stream-analytics-monitor-jobs.md).
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a>Akış analizi için Azure PowerShell cmdlet'leri
Azure PowerShell cmdlet'lerini aşağıdaki hello kullanılan toomonitor olması ve Azure akış analizi işleri yönetin. Azure PowerShell farklı sürümlerini olduğuna dikkat edin. 
**Listelenen hello ilk Azure PowerShell 0.9.8 komuttur hello örneklerde hello ikinci için Azure PowerShell 1.0 komuttur.** Hello Azure PowerShell 1.0 komutları, her zaman "AzureRM" Merhaba komutta olacaktır.

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a>Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob
Hello Azure aboneliği veya belirtilen kaynak grubunda tanımlanan tüm Stream Analytics işlerini listeler veya bir kaynak grubu içindeki belirli bir iş iş bilgilerini alır.

**Örnek 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob

Bu PowerShell komutunu hello Azure aboneliği tüm hello Stream Analytics işleri hakkında bilgi verir.

**Örnek 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Bu PowerShell komutunu hello kaynak grubunda varsayılan orta ABD StreamAnalytics tüm hello Stream Analytics işleri hakkında bilgi verir.

**Örnek 3**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Bu PowerShell komutunu hello kaynak grubunda varsayılan orta ABD StreamAnalytics hello Stream Analytics işi StreamingJob hakkında bilgi verir.

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a>Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput
Tüm belirtilen Stream Analytics işinde tanımlanan hello girdi listeler veya belirli bir giriş bilgilerini alır.

**Örnek 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Bu PowerShell komutunu hello iş StreamingJob tanımlanan tüm hello girişleri hakkında bilgi verir.

**Örnek 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Bu PowerShell komutunu hello iş StreamingJob tanımlanan EntryStream adlı hello giriş hakkında bilgi verir.

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a>Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput
Tüm belirtilen Stream Analytics işinde tanımlanan hello çıkışları listeler veya belirli bir çıkış hakkındaki bilgileri alır.

**Örnek 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Bu PowerShell komutunu hello iş StreamingJob tanımlanan hello çıkışları hakkında bilgi verir.

**Örnek 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Bu PowerShell komutunu hello iş StreamingJob tanımlanan çıkış adlı hello çıktı hakkında bilgi verir.

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a>Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota
Belirtilen bir bölgede birimleri akış hello kota hakkındaki bilgileri alır.

**Örnek 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

Bu PowerShell komutunu hello Orta ABD bölgesinde hello kota ve akış birimleri kullanımı hakkında bilgi verir.

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a>Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation
Stream Analytics işinde tanımlanan belirli bir dönüşüm hakkındaki bilgileri alır.

**Örnek 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Bu PowerShell komutunu hello iş StreamingJob StreamingJob adlı hello dönüştürme hakkında bilgi döndürür.

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a>AzureStreamAnalyticsInput yeni | AzureRMStreamAnalyticsInput yeni
Akış analizi işi içinde yeni bir giriş oluşturur veya mevcut bir belirtilen giriş güncelleştirir.

Merhaba hello giriş adını hello .json dosyası veya hello komut satırında belirtilebilir. Her ikisi de belirtilirse hello adı hello komut satırında gerekir olması hello hello dosyasındaki hello ile aynı.

Zaten bir girdi belirtin ve belirtmeyin hello – Force parametresini hello cmdlet tooreplace varolan giriş hello olup olmadığını sorar.

Belirtirseniz hello – Force parametresini ve var olan giriş adı, hello giriş onaysız değiştirilecek belirtin.

Toohello hello JSON dosya yapısı ve içeriği hakkında ayrıntılı bilgi için bkz [girişi oluşturun (Azure akış analizi)] [ msdn-rest-api-create-stream-analytics-input] hello bölümünü [Stream Analytics Yönetimi REST API'si Başvuru Kitaplığı][stream.analytics.rest.api.reference].

**Örnek 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Bu PowerShell komutunu Input.json hello dosyasından yeni bir giriş oluşturur. Var olan bir giriş hello giriş tanım dosyasında belirtilen hello adıyla zaten tanımlı olup olmadığını, hello cmdlet ister olsun veya olmasın tooreplace onu.

**Örnek 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Bu PowerShell komutunu hello işe EntryStream adlı yeni bir giriş oluşturur. Bu ada sahip mevcut bir giriş zaten tanımlı olup olmadığını, hello cmdlet ister desteklemediğini tooreplace onu.

**Örnek 3**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Bu PowerShell komutunu hello varolan giriş kaynağı hello dosyasından hello tanımıyla EntryStream adlı hello tanımının yerini alır.

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a>AzureStreamAnalyticsJob yeni | AzureRMStreamAnalyticsJob yeni
Microsoft Azure'da yeni bir akış analizi işi oluşturur veya mevcut bir belirtilen proje hello tanımını güncelleştirir.

Merhaba .json dosyası veya hello komut satırında hello işinin Hello adı belirtilebilir. Her ikisi de belirtilirse hello adı hello komut satırında gerekir olması hello hello dosyasındaki hello ile aynı.

Zaten bir iş adı belirtin ve belirtmeyin hello – Force parametresini hello cmdlet tooreplace mevcut iş hello olup olmadığını sorar.

Var olan bir iş adı belirtin ve hello – Force parametresini belirtirseniz, hello iş tanımı onaysız değiştirilecek.

Toohello hello JSON dosya yapısı ve içeriği hakkında ayrıntılı bilgi için bkz [Stream Analytics işi oluşturmak] [ msdn-rest-api-create-stream-analytics-job] hello bölümünü [Stream Analytics Yönetimi REST API Başvurusu Kitaplık][stream.analytics.rest.api.reference].

**Örnek 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Bu PowerShell komutunu JobDefinition.json hello tanımında yeni bir proje oluşturur. Merhaba iş tanımı dosyasında belirtilen hello ada sahip mevcut bir iş zaten tanımlı olup olmadığını, hello cmdlet ister desteklemediğini tooreplace onu.

**Örnek 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Bu PowerShell komutunu hello iş tanımı için StreamingJob yerini alır.

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a>AzureStreamAnalyticsOutput yeni | AzureRMStreamAnalyticsOutput yeni
Akış analizi işi yeni çıktısı oluşturur veya mevcut bir çıktı güncelleştirir.  

Merhaba Çıktı Hello adını hello .json dosyası veya hello komut satırında belirtilebilir. Her ikisi de belirtilirse hello adı hello komut satırında gerekir olması hello hello dosyasındaki hello ile aynı.

Zaten bir çıktı belirtirseniz ve belirtmeyin hello – Force parametresini hello cmdlet tooreplace varolan çıktı hello olup olmadığını sorar.

Belirtirseniz hello – Force parametresini ve mevcut bir çıktı adı, hello çıkış onaysız değiştirilecek belirtin.

Toohello hello JSON dosya yapısı ve içeriği hakkında ayrıntılı bilgi için bkz [oluşturma çıkış (Azure akış analizi)] [ msdn-rest-api-create-stream-analytics-output] hello bölümünü [Stream Analytics Yönetimi REST API'si Başvuru Kitaplığı][stream.analytics.rest.api.reference].

**Örnek 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Bu PowerShell komutunu hello iş StreamingJob "çıktı" adlı yeni bir çıkış oluşturur. Bu ada sahip mevcut bir çıktı zaten tanımlı olup olmadığını, hello cmdlet ister desteklemediğini tooreplace onu.

**Örnek 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Bu PowerShell komutunu StreamingJob hello işteki "çıktı" Merhaba tanımı değiştirir.

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a>AzureStreamAnalyticsTransformation yeni | AzureRMStreamAnalyticsTransformation yeni
Akış analizi işi içinde yeni bir dönüştürme oluşturur veya hello varolan dönüştürme güncelleştirir.

Merhaba dönüştürme Hello adını hello .json dosyası veya hello komut satırında belirtilebilir. Her ikisi de belirtilirse hello adı hello komut satırında gerekir olması hello hello dosyasındaki hello ile aynı.

Zaten bir dönüşüm belirtirseniz ve belirtmeyin hello – Force parametresini hello cmdlet tooreplace varolan dönüştürme hello olup olmadığını sorar.

Merhaba – Force parametresini ve varolan bir dönüşüm adı belirtirseniz belirtirseniz hello dönüştürme onaysız değiştirilecek.

Toohello hello JSON dosya yapısı ve içeriği hakkında ayrıntılı bilgi için bkz [oluşturma dönüştürme (Azure akış analizi)] [ msdn-rest-api-create-stream-analytics-transformation] hello bölümünü [Stream Analytics Yönetimi REST API Başvurusu Kitaplığı][stream.analytics.rest.api.reference].

**Örnek 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Bu PowerShell komutunu hello iş StreamingJob StreamingJobTransform adlı yeni bir dönüştürme oluşturur. Varolan bir dönüşüm zaten bu ada sahip tanımlı olup olmadığını, hello cmdlet ister desteklemediğini tooreplace onu.

**Örnek 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 Bu PowerShell komutunu hello tanımında StreamingJobTransform hello iş StreamingJob değiştirir.

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a>Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput
Zaman uyumsuz olarak belirli bir giriş Microsoft Azure Stream Analytics işinde siler.  
Belirtirseniz hello – Force parametresini, giriş hello onay silinir.

**Örnek 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Giriş EventStream StreamingJob hello işteki kaldırır hello bu PowerShell komutu.  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a>Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob
Zaman uyumsuz olarak bir belirli Microsoft Azure akış analizi işi siler.  
Belirtirseniz hello – Force parametresini hello iş olacaktır onay silinir.

**Örnek 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Bu PowerShell komutunu hello iş StreamingJob kaldırır.  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a>Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput
Zaman uyumsuz olarak belirli bir çıkış Microsoft Azure Stream Analytics işinde siler.  
Belirtirseniz hello – Force parametresini hello çıkış olacaktır onay silinir.

**Örnek 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Bu PowerShell komutunu kaldırır hello hello iş StreamingJob çıkış çıktı.  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a>Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob
Zaman uyumsuz olarak dağıtır ve Microsoft Azure Stream Analytics işini başlatır.

**Örnek 1**

Azure PowerShell 0.9.8:  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Azure PowerShell 1.0:  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Bu PowerShell komutunu başlatır hello özel çıkış başlangıç saatine sahip StreamingJob ayarlamak tooDecember 12, 2012, 12:12:12 iş UTC.

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a>Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob
Zaman uyumsuz olarak Microsoft Azure üzerinde çalışan bir Stream Analytics işini durdurur ve kullanılmakta olan kaynakları serbest bırakır. Merhaba iş düzenlenen yeniden ve gibi hello iş tanımı ve meta veri aboneliğinizi hello Azure portalı ve yönetim API'si aracılığıyla içinde kullanılabilir kalır. Hello durduruldu durumunda bir iş için ücret alınmaz.

**Örnek 1**

Azure PowerShell 0.9.8:  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0:  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Bu PowerShell komutunu hello işini StreamingJob durdurur.  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a>Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput
Stream Analytics tooconnect tooa testleri hello yeteneğini giriş belirtilmiş.

**Örnek 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Bu PowerShell komutunu testleri hello bağlantı durumunu hello giriş StreamingJob EntryStream.  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a>Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput
Stream Analytics tooconnect tooa testleri hello yeteneğini çıkış belirtilmiş.

**Örnek 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Bu PowerShell komutunu testleri hello bağlantı durumunu hello StreamingJob çıktısında çıktı.  

## <a name="get-support"></a>Destek alın
Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics). 

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

