---
title: "Azure Otomasyonu aaaVariable varlıkları | Microsoft Docs"
description: "Değişken varlıkları kullanılabilir tooall runbook'ları ve Azure Otomasyonu DSC yapılandırmalarında değerlerdir.  Bu makale, değişkenleri hello ayrıntılarını açıklar ve nasıl metinsel ve grafik yazma içinde toowork onlarla."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a>Azure Otomasyonu değişken varlıkları

Değişken varlıkları kullanılabilir tooall runbook'ları ve Otomasyon hesabınızda DSC yapılandırmaları değerlerdir. Bunlar oluşturulan, değiştirilebilir ve hello Azure portalı, Windows PowerShell ve içinden alınan bir runbook veya DSC yapılandırması. Otomasyon değişkenleri senaryoları aşağıdaki hello için yararlıdır:

- Birden çok runbook'ları veya DSC yapılandırması arasında bir değer paylaşır.

- Bir değeri hello birden çok iş arasında paylaştırma aynı runbook veya DSC yapılandırması.

- Bir değer hello portalından veya runbook'lar veya bir dizi ortak yapılandırma öğelerinin belirli listesi gibi VM adları, belirli bir kaynak grubunun, bir AD etki alanı adı, vb. gibi DSC yapılandırmaları tarafından kullanılan hello Windows PowerShell komut satırından yönetme.  

Otomasyon değişkenleri böylece Hello runbook veya DSC yapılandırması başarısız olsa bile kullanıcılar toobe kullanılabilir devam kalıcıdır.  Bu da ardından bir başkası tarafından kullanılan veya hello tarafından kullanılan bir runbook tarafından ayarlanan değer toobe sağlar aynı runbook veya DSC yapılandırma Merhaba, İleri çalıştırıldığında.

Bir değişken oluşturulduğunda depolanmasını belirtebilirsiniz şifrelenmiş.  Bir değişken şifrelendiğinde, Azure Automation'da güvenli bir şekilde depolanır ve değeri hello alınamıyor [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) hello Azure PowerShell modülünün bir parçası olarak gönderilen cmdlet'i.  Merhaba şifrelenmiş değer alınabilir yalnızca hello yoludur **Get-AutomationVariable** etkinliğini runbook veya DSC yapılandırması.

> [!NOTE]
> Azure Automation güvenli varlıkların kimlik bilgileri, sertifikalar, bağlantıları ve şifrelenmiş değişkenler içerir. Bu varlıklar şifrelenir ve hello Azure her Otomasyon hesabı için oluşturulan benzersiz bir anahtar kullanarak otomasyon depolanır. Bu anahtarı bir sertifika tarafından şifrelenir ve Azure Otomasyonu'nda depolanır. Güvenli bir varlık depolamak önce hello Otomasyon hesabının hello anahtarı hello ana sertifikayı kullanarak şifresi çözülür ve tooencrypt hello varlık kullanılır.

## <a name="variable-types"></a>Değişken türleri

Hello Azure portal ile bir değişkeni oluşturduğunuzda, hello portal hello hello değişken değeri girmek için uygun denetimi görüntüleyebilmesi hello aşağı açılan listeden bir veri türü belirtmeniz gerekir. Merhaba değişken kısıtlı toothis veri değil türü, ancak hello değişkeni toospecify istiyorsanız, Windows PowerShell kullanarak bir değere ayarlamalısınız, farklı bir tür. Belirtirseniz **tanımlanmamış**, hello hello değişkenin değerini çok ayarlayın, sonra da**$null**, ve hello hello değerle ayarlamanız gerekir [kümesi AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet'ini veya **Set-AutomationVariable** etkinlik.  Oluşturma veya karmaşık değişken türü hello portalında hello değerini değiştirin, ancak Windows PowerShell kullanarak herhangi bir türde bir değer sağlayabilir. Karmaşık türler olarak döndürülecek bir [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).

Birden çok değer tooa tek değişken bir dizi ya da karma oluşturma ve toohello değişkeni kaydetme depolayabilirsiniz.

Merhaba, Otomasyon kullanılabilir değişken türlerinin bir listesini şunlardır:

* Dize
* Tamsayı
* Tarih saat
* Boole değeri
* Null

## <a name="cmdlets-and-workflow-activities"></a>Cmdlet'ler ve iş akışı etkinlikleri

Aşağıdaki tablonun hello Hello cmdlet'leri kullanılan toocreate olan ve Windows PowerShell ile Otomasyon değişkenleri yönetebilirsiniz. Merhaba bir parçası olarak sevk [Azure PowerShell Modülü](../powershell-install-configure.md) olduğu Automation runbook'ları ve DSC yapılandırması için kullanılabilir.

|Cmdlet'leri|Açıklama|
|:---|:---|
|[Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)|Mevcut bir değişken Hello değerini alır.|
|[AzureRmAutomationVariable yeni](https://msdn.microsoft.com/library/mt603613.aspx)|Yeni bir değişken oluşturur ve değerini ayarlar.|
|[Remove-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt619354.aspx)|Mevcut bir değişken kaldırır.|
|[Set-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603601.aspx)|Mevcut bir değişken için başlangıç değerini ayarlar.|

Aşağıdaki tablonun hello Hello iş akışı etkinlikleri kullanılan tooaccess Otomasyon değişkenleri bir runbook'ta ' dir. Bunlar yalnızca runbook ya da DSC yapılandırması kullanmak için kullanılabilir ve hello Azure PowerShell modülünün bir parçası olarak bulunmaz.

|İş akışı etkinlikleri|Açıklama|
|:---|:---|
|Get-AutomationVariable|Mevcut bir değişken Hello değerini alır.|
|Set-AutomationVariable|Mevcut bir değişken için başlangıç değerini ayarlar.|

> [!NOTE] 
> Değişkenleri yapmaktan kaçınmalısınız hello – Name parametresinde **Get-AutomationVariable** runbook veya runbook'ları veya DSC yapılandırması ve Otomasyon arasındaki bağımlılıkları getirebileceğinden DSC yapılandırması Tasarım zamanında değişkenleri.

## <a name="creating-a-new-automation-variable"></a>Yeni Otomasyon değişkeni oluşturma

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a>toocreate hello Azure portalı ile yeni bir değişken

1. Otomasyon hesabınızdan hello tıklatın **varlıklar** döşeme ve ardından hello **varlıklar** dikey penceresinde, select **değişkenleri**.
2. Merhaba üzerinde **değişkenleri** kutucuğu, select **değişken Ekle**.
3. Tamamlamak hello hello seçenekleri **yeni değişken** tıklayın ve dikey **Oluştur** hello yeni değişken kaydedin.

### <a name="toocreate-a-new-variable-with-windows-powershell"></a>Windows PowerShell ile yeni bir değişken toocreate

Merhaba [yeni AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet'i yeni bir değişken oluşturur ve ilk değerini ayarlar. Değer hello kullanarak alabilirsiniz [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx). Merhaba değer basit bir tür ise, bu türdeki döndürülür. Karmaşık bir tür ise sonra bir **PSCustomObject** döndürülür.

Merhaba aşağıdaki örnek komutlar Göster nasıl toocreate türünde bir değişken dize ve değerini döndürür.

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

Merhaba aşağıdaki örnek komutlar Göster nasıl toocreate karmaşık sahip bir değişken yazın ve ardından özelliklerini geri dönün. Bir sanal makine bu durumda, nesne **Get-AzureRmVm** kullanılır.

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a>Bir runbook veya DSC yapılandırması bir değişken kullanma

Kullanım hello **Set-AutomationVariable** etkinlik tooset hello değişkenin değeri olarak bir Otomasyon runbook'u veya DSC yapılandırması ve hello **Get-AutomationVariable** tooretrieve onu.  Merhaba kullanmamanız **kümesi AzureAutomationVariable** veya **Get-AzureAutomationVariable** cmdlet'leri runbook veya hello iş akışı etkinlikleri az verimli olduğundan DSC yapılandırması.  Güvenli değişkenlerle hello değeri alınamıyor **Get-AzureAutomationVariable**.  yalnızca yol toocreate bir runbook içindeki yeni bir değişken hello veya DSC yapılandırma toouse hello [yeni AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet'i.


### <a name="textual-runbook-samples"></a>Metin biçiminde runbook örnekleri

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a>Basit bir değer bir değişkeninden alma ve ayarlama

Merhaba aşağıdaki örnek komutlar Göster nasıl tooset ve metin biçiminde runbook bir değişkende alır. Bu örnekte, Tamsayı türünde değişkenleri adlı görünür duruma varsayılır *Numberofıterations* ve *NumberOfRunnings* ve adlı dize türünde bir değişken *SampleMessage* zaten oluşturulmuş.

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a>Karmaşık bir nesne, bir değişkende alma ve ayarlama

Merhaba aşağıdaki örnek kod gösterir nasıl tooupdate metin biçiminde runbook karmaşık bir değere sahip bir değişken. Bu örnekte, bir Azure sanal makinesi ile alınan **Get-AzureVM** ve kaydedilmiş tooan var olan Otomasyon değişkeni.  İçinde anlatıldığı gibi [değişken türleri](#variable-types), bu PSCustomObject depolanır.

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


Koddan hello hello değeri hello değişken ve kullanılan toostart hello sanal makineden alınır.

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a>Bir değişken koleksiyonunda alma ve ayarlama

Merhaba aşağıdaki örnek kod gösterir nasıl toouse metinsel bir runbook'ta karmaşık değerler koleksiyonu sahip bir değişken. Bu örnekte, birden fazla Azure sanal makineler ile alınan **Get-AzureVM** ve kaydedilmiş tooan var olan Otomasyon değişkeni.  İçinde anlatıldığı gibi [değişken türleri](#variable-types), bu PSCustomObjects koleksiyonu olarak depolanır.

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

Koddan hello hello koleksiyonu hello değişkeninden alınır ve her sanal makine toostart kullanılan.

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a>Grafik runbook örnekleri

Bir grafik runbook'ta hello eklemek **Get-AutomationVariable** veya **Set-AutomationVariable** hello değişkeni hello grafik Düzenleyicisi hello Kitaplık bölmesinde sağ tıklayarak ve hello seçme istediğiniz etkinliği.

![Değişken toocanvas Ekle](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a>Bir değişkende değerleri ayarlama
Hello aşağıdaki görüntüde örnek etkinlikleri tooupdate bir değere sahip bir değişken basit bir grafik runbook'u gösterir. Bu örnekte, tek bir Azure sanal makine ile alınan **Get-AzureRmVM** ve hello bilgisayar adı bir dize türü ile tooan var olan Otomasyon değişkeni kaydedilir.  Hello olup olmadığını önemli değildir [bağlantıdır bir ardışık düzen veya dizisi](automation-graphical-authoring-intro.md#links-and-workflow) bu yana yalnızca tek bir nesne hello çıktısında bekliyoruz.

![Basit değişken Ayarla](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a>Sonraki Adımlar

* Grafik yazma etkinlikleri birbirine bağlama hakkında daha fazla toolearn bakın [grafik yazma içindeki bağlantılar](automation-graphical-authoring-intro.md#links-and-workflow)
* Grafik runbook'ları ile çalışmaya tooget bakın [ilk grafik runbook Uygulamam](automation-first-runbook-graphical.md) 

