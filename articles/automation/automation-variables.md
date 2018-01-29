---
title: "Azure Otomasyonu değişken varlıkları | Microsoft Docs"
description: "Değişken varlıkları tüm runbook'lar ve Azure Otomasyonu DSC yapılandırmalarında kullanılabilen değerlerdir.  Bu makalede, değişkenlerin ve bunlarla metinsel ve grafik yazma çalışma konusunda ayrıntılar açıklanmaktadır."
services: automation
documentationcenter: 
author: georgewallace
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
ms.openlocfilehash: e38d2b751090cfdc078de4e8c683c6bb9b48fac3
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/03/2018
---
# <a name="variable-assets-in-azure-automation"></a>Azure Otomasyonu değişken varlıkları

Değişken varlıkları tüm runbook'lar ve Otomasyon hesabınızda DSC yapılandırmaları kullanılabilen değerlerdir. Bunlar oluşturulan, değiştirilebilir ve Windows PowerShell, Azure portalından ve içinden alınan bir runbook veya DSC yapılandırması. Otomasyon değişkenleri aşağıdaki senaryolarda kullanışlıdır:

- Birden çok runbook'ları veya DSC yapılandırması arasında bir değer paylaşır.

- Bir değeri aynı runbook veya DSC yapılandırması birden çok iş arasında paylaştırma.

- Bir değeri portalından veya runbook'lar veya bir dizi ortak yapılandırma öğelerinin belirli listesi gibi VM adları, belirli bir kaynak grubunun, bir AD etki alanı adı, vb. gibi DSC yapılandırmaları tarafından kullanılan Windows PowerShell komut satırından yönetme.  

Böylece runbook veya DSC yapılandırma başarısız olsa bile kullanılabilir olmaya devam Otomasyon değişkenleri kalıcıdır.  Bu DSC yapılandırması bu İleri çalıştırıldığında ve aynı runbook tarafından kullanılan veya bir başkası tarafından sonra kullanılan bir runbook tarafından ayarlamak için bir değer de sağlar.

Bir değişken oluşturulduğunda depolanmasını belirtebilirsiniz şifrelenmiş.  Bir değişken şifrelendiğinde, Azure Automation'da güvenli bir şekilde depolanır ve değeri alınamaz [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) Azure PowerShell modülünün bir parçası olarak gönderilen cmdlet'i.  Şifrelenmiş değer alınabilir tek yolu **Get-AutomationVariable** etkinliğini runbook veya DSC yapılandırması.

> [!NOTE]
> Azure Automation güvenli varlıkların kimlik bilgileri, sertifikalar, bağlantıları ve şifrelenmiş değişkenler içerir. Bu varlıklar şifrelenir ve her Otomasyon hesabı için oluşturulan benzersiz bir anahtar kullanarak Azure Automation depolanır. Bu anahtarı bir sertifika tarafından şifrelenir ve Azure Otomasyonu'nda depolanır. Güvenli bir varlık depolamak önce anahtar Otomasyon hesabı için sertifika aracılığıyla çözülür ve varlık şifrelemek için kullanılan.

## <a name="variable-types"></a>Değişken türleri

Azure portal ile bir değişkeni oluşturduğunuzda, portal değişken değeri girmek için uygun denetimi görüntüleyebilmesi aşağı açılan listeden bir veri türü belirtmeniz gerekir. Değişkeni bu veri türü için sınırlı değildir, ancak farklı türde bir değer belirtmek istiyorsanız Windows PowerShell kullanarak değişkenini ayarlamalıdır. Belirtirseniz **tanımlanmamış**, değişkenin değeri ayarlanacak sonra **$null**, ve değerle ayarlamanız gerekir [kümesi AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet'ini veya **Set-AutomationVariable** etkinlik.  Oluşturma veya karmaşık değişken türü portalında değerini değiştirin, ancak Windows PowerShell kullanarak herhangi bir türde bir değer sağlayabilir. Karmaşık türler olarak döndürülecek bir [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).

Bir dizi ya da karma tablosu oluşturarak ve değişkenine kaydetme birden çok değeri tek bir değişkende depolayabilirsiniz.

Değişken türleri Otomasyon kullanılabilir bir listesi verilmiştir:

* Dize
* Tamsayı
* Tarih Saat
* Boole
* Null

## <a name="scripting-the-creation-and-management-of-variables"></a>Oluşturulmasını ve yönetimini değişkenlerin komut dosyası oluşturma

Aşağıdaki tabloda yer alan cmdlet'ler oluşturmak ve Otomasyon değişkenleri Windows PowerShell ile yönetmek için kullanılır. Bir parçası olarak sevk [Azure PowerShell Modülü](../powershell-install-configure.md) olduğu Automation runbook'ları ve DSC yapılandırması için kullanılabilir.

|Cmdlet'leri|Açıklama|
|:---|:---|
|[Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)|Mevcut bir değişken değerini alır.|
|[AzureRmAutomationVariable yeni](https://msdn.microsoft.com/library/mt603613.aspx)|Yeni bir değişken oluşturur ve değerini ayarlar.|
|[Remove-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt619354.aspx)|Mevcut bir değişken kaldırır.|
|[Set-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603601.aspx)|Mevcut bir değişken için değeri ayarlar.|

Aşağıdaki tabloda iş akışı etkinlikleri Otomasyon bir runbook'ta değişkenlere erişmek için kullanılır. Bunlar yalnızca runbook ya da DSC yapılandırması kullanmak için kullanılabilir ve Azure PowerShell modülünün bir parçası olarak bulunmaz.

|İş akışı etkinlikleri|Açıklama|
|:---|:---|
|Get-AutomationVariable|Mevcut bir değişken değerini alır.|
|Set-AutomationVariable|Mevcut bir değişken için değeri ayarlar.|

> [!NOTE] 
> Yapmaktan kaçınmalısınız – Name parametresinde **Get-AutomationVariable** runbook veya bu runbook'ları veya DSC yapılandırması ve Otomasyon değişkenleri arasındaki bağımlılıkları tasarım zamanında getirebileceğinden DSC yapılandırması.

Aşağıdaki tabloda işlevleri erişmek ve bir Python2 runbook'ta değişkenlere almak için kullanılır. 

|Python2 işlevleri|Açıklama|
|:---|:---|
|automationassets.get_automation_variable|Mevcut bir değişken değerini alır. |
|automationassets.set_automation_variable|Mevcut bir değişken için değeri ayarlar. |

> [!NOTE] 
> Varlık işlevleri erişmek için Python runbook'unuz üstünde "automationassets" modülü içeri aktarmalısınız.

## <a name="creating-a-new-automation-variable"></a>Yeni Otomasyon değişkeni oluşturma

### <a name="to-create-a-new-variable-with-the-azure-portal"></a>Azure portalı ile yeni bir değişken oluşturmak için

1. Otomasyon hesabınızdan tıklatın **varlıklar** döşeme ve daha sonra **varlıklar** dikey penceresinde, select **değişkenleri**.
2. Üzerinde **değişkenleri** kutucuğu, select **değişken Ekle**.
3. Seçenekleri tamamlayın **yeni değişken** tıklayın ve dikey **oluşturma** yeni değişkeni kaydetmek.

### <a name="to-create-a-new-variable-with-windows-powershell"></a>Windows PowerShell ile yeni bir değişken oluşturmak için

[Yeni AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet'i yeni bir değişken oluşturur ve ilk değerini ayarlar. Değer kullanarak alabilirsiniz [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx). Değer basit bir tür ise, bu türdeki döndürülür. Karmaşık bir tür ise sonra bir **PSCustomObject** döndürülür.

Aşağıdaki örnek komutlar dize türünde bir değişken oluşturma ve değerini döndür göstermektedir.

    New-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

Aşağıdaki örnek komutlar bir karmaşık türü ile bir değişken oluşturun ve özelliklerini dönmek nasıl gösterir. Bir sanal makine bu durumda, nesne **Get-AzureRmVm** kullanılır.

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a>Bir runbook veya DSC yapılandırması bir değişken kullanma

Kullanım **Set-AutomationVariable** bir PowerShell runbook veya DSC yapılandırması, bir Otomasyon değişkenin değerini ayarlamak için etkinlik ve **Get-AutomationVariable** bunu almak için.  Kullanmamanız **kümesi AzureAutomationVariable** veya **Get-AzureAutomationVariable** cmdlet'leri runbook veya iş akışı etkinlikleri az verimli olduğundan DSC yapılandırması.  Güvenli değişkenlerle değeri alınamıyor **Get-AzureAutomationVariable**.  Bir runbook veya DSC yapılandırması içinde yeni bir değişken oluşturmak için tek yolu kullanmaktır [yeni AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet'i.


### <a name="textual-runbook-samples"></a>Metin biçiminde runbook örnekleri

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a>Basit bir değer bir değişkeninden alma ve ayarlama

Aşağıdaki örnek komutlar ayarlamak ve metin biçiminde runbook bir değişkende almak nasıl gösterir. Bu örnekte, Tamsayı türünde değişkenleri adlı görünür duruma varsayılır *Numberofıterations* ve *NumberOfRunnings* ve adlı dize türünde bir değişken *SampleMessage* zaten oluşturulmuş.

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a>Karmaşık bir nesne, bir değişkende alma ve ayarlama

Aşağıdaki örnek kod, metin biçiminde runbook karmaşık bir değere sahip bir değişken güncelleştirme gösterilmiştir. Bu örnekte, bir Azure sanal makinesi ile alınan **Get-AzureVM** ve varolan bir Otomasyon değişkeni kaydedildi.  İçinde anlatıldığı gibi [değişken türleri](#variable-types), bu PSCustomObject depolanır.

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm

Aşağıdaki kodda değeri değişkeninden alınır ve sanal makineyi başlatmak için kullanılır.

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a>Bir değişken koleksiyonunda alma ve ayarlama

Aşağıdaki örnek kod bir metinsel runbook'ta karmaşık değerler koleksiyonu ile bir değişken kullanmayı gösterir. Bu örnekte, birden fazla Azure sanal makineler ile alınan **Get-AzureVM** ve varolan bir Otomasyon değişkeni kaydedildi.  İçinde anlatıldığı gibi [değişken türleri](#variable-types), bu PSCustomObjects koleksiyonu olarak depolanır.

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

Aşağıdaki kodda, koleksiyon değişkeninden alınır ve her sanal makineyi başlatmak için kullanılır.

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }
    
#### <a name="setting-and-retrieving-a-variable-in-python2"></a>Bir değişkende Python2 alma ve ayarlama
Aşağıdaki örnek kod, bir değişken kullanmak için bir değişken ayarlamak ve Python2 runbook'taki mevcut olmayan değişken için bir özel durum işleme gösterilmektedir.

    import automationassets
    from automationassets import AutomationAssetNotFound

    # get a variable
    value = automationassets.get_automation_variable("test-variable")
    print value

    # set a variable (value can be int/bool/string)
    automationassets.set_automation_variable("test-variable", True)
    automationassets.set_automation_variable("test-variable", 4)
    automationassets.set_automation_variable("test-variable", "test-string")

    # handle a non-existent variable exception
    try:
        value = automationassets.get_automation_variable("non-existing variable")
    except AutomationAssetNotFound:
        print "variable not found"


### <a name="graphical-runbook-samples"></a>Grafik runbook örnekleri

Bir grafik runbook'ta eklediğiniz **Get-AutomationVariable** veya **Set-AutomationVariable** grafik düzenleyicisini Kitaplık bölmesinde değişkeni sağ tıklatın ve istediğiniz etkinliği seçerek.

![Tuvale değişken Ekle](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a>Bir değişkende değerleri ayarlama
Aşağıdaki resimde bir grafik runbook basit bir değere sahip bir değişken güncelleştirmek için örnek etkinliklerini gösterir. Bu örnekte, tek bir Azure sanal makine ile alınan **Get-AzureRmVM** ve varolan bir Otomasyon değişkeni dize türünde bir bilgisayar adı kaydedilir.  Önemli değildir olup olmadığını [bağlantıdır bir ardışık düzen veya dizisi](automation-graphical-authoring-intro.md#links-and-workflow) bu yana yalnızca tek bir nesne çıktıda bekliyoruz.

![Basit değişken Ayarla](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a>Sonraki Adımlar

* Grafik yazma etkinlikleri birbirine bağlama hakkında daha fazla bilgi için bkz: [grafik yazma içindeki bağlantılar](automation-graphical-authoring-intro.md#links-and-workflow)
* Grafik runbook'ları kullanmaya başlamak için bkz. [İlk grafik runbook uygulamam](automation-first-runbook-graphical.md) 

